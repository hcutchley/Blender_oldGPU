# Blender_oldGPU

With the release of blender 5.0 gpu minimum requirements have been update to required cuda compute 5.0 or higher and must be a gtx900 series card or later, this Repository contains a patched version of blender where it allows any gpu, though must still be CUDA capable, there's a release version and a full repo if you wish to compile for yourself


Patch Instructions:

Prerequisties
    Info:
      A version of CUDA downloaded from NVIDIA, this version used CUDA 12.8: 
      Microsoft Visual Studio 2022 - Community edition is fine
      Know Your Graphics Card name and CUDA version

    Instructions:
      CUDA: 
        Download the network version of CUDA from NVIDIA, e.g. https://developer.nvidia.com/cuda-12-8-0-download-archive
        Run installer, when given options for install go to advanced and only select the CUDA, you don't need anything else and don't want to override your current drivers etc.
<img width="254" height="188" alt="image" src="https://github.com/user-attachments/assets/d3d545d1-f73c-4c11-b3ec-0049c1aca735" />


<img width="250" height="186" alt="image" src="https://github.com/user-attachments/assets/32daf24b-f9e8-4ae4-8d5c-0382c09fa746" />

Ignore Any Warnings about visual studio not found at the end

      Visual Studio Code:
        Download from: https://visualstudio.microsoft.com/downloads/   - Community Edition Works
        When installing check the following:  
<img width="146" height="256" alt="image" src="https://github.com/user-attachments/assets/fe53fab3-049b-4c80-af62-3b2dd1d6e0aa" />
 

      CUDA Capability:
      Check your card at https://developer.nvidia.com/cuda-gpus or https://developer.nvidia.com/cuda-legacy-gpus
      Remember your name and cuda compute capability, mine for example was 6.1



Main Instructions

Parent Folder: Must not have spaces in name, then cd into Folder

    e.g.    C:\Blender_git>

Clone Repository - run the following commands in the parent folder

    git clone https://projects.blender.org/blender/blender.git blender

    cd blender

    git checkout blender-v5.0-release

    git lfs install

    git lfs pull

    git submodule update --init --recursive --progress




Making Patch:

    located under \intern\cycles\device\cuda\device.cpp 
    Open the device.ccp in a text/code editor
            example: "C:\Blender_git\blender\intern\cycles\device\cuda\device.cpp"


    Find the function: if (!cudaSupportsDevice(num)) 
        Should look like:

    if (!cudaSupportsDevice(num)) {
      LOG_INFO << "Ignoring device \"" << name << "\", this graphics card is no longer supported.";
      continue;
    }


{    Replace the function with the one below and Save the file - READ THE INSTRUCTIONS ABOVE FUNCTION FIRST

 {   //Using your graphics card name in place of MX350 and the (major == 6 && minor == 1) is for CUDA 6.1, replace with your CUDA structure//
    Function:
    
    if (!cudaSupportsDevice(num)) {
        int major = 0, minor = 0;
        cuDeviceGetAttribute(&major, CU_DEVICE_ATTRIBUTE_COMPUTE_CAPABILITY_MAJOR, num);
        cuDeviceGetAttribute(&minor, CU_DEVICE_ATTRIBUTE_COMPUTE_CAPABILITY_MINOR, num);

        if (major == 6 && minor == 1) {
            // MX350: allow
        } else {
            LOG_INFO << "Ignoring device \"" << name << "\", this graphics card is no longer supported.";
            continue;
        }
    }

    
        

Build Commands, in the blender folder e.g. C:\Blender_git\blender>
    
        python .\build_files\utils\make_update.py

        mkdir build

        cd build
}  
    //In the following replace sm_61 with your cuda graphics architechture (ensures not having to compile every single GPU, only your specific one) //
    Run this command
    
    cmake .. -G "Visual Studio 17 2022" -A x64 ^
    -DWITH_CYCLES_CUDA_BINARIES=ON ^
    -DCUDA_TOOLKIT_ROOT_DIR="C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v12.8" ^
    -DCYCLES_CUDA_BINARIES_ARCH=sm_61
}
    Final command:
    
    cmake --build . --config Release --target install


The build can take hours so remain patient, especially with the CUDA compile, its not stuck, just takes a while.



