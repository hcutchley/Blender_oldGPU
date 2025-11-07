# Blender_oldGPU

With the release of blender 5.0 gpu minimum requirements have been update to required cuda compute 5.0 or higher and must be a gtx900 series card or later, this Repository contains a patched version of blender where it allows any gpu, though must still be CUDA capable, there's a release version and a full repo if you wish to compile for yourself



    
Prerequisties and their installation instructions

Full Patch Instructions here
    https://github.com/hcrutchley/Blender_oldGPU/blob/main/Instructions.md

  Info:
  
    A version of CUDA downloaded from NVIDIA, this version used CUDA 12.8: 
    Microsoft Visual Studio 2022 - Community edition is fine
    Know Your Graphics Card name and CUDA version

   Instructions:
    CUDA: 
        Download the network version of CUDA from NVIDIA, 
        
            https://developer.nvidia.com/cuda-12-8-0-download-archive
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




