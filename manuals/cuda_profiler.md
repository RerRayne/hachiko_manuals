# CUDA Profiler

To understand how optimal your code utilizes GPUs and how much time is spent for different operations,  use **NVIDIA Profiler**  to count times and **CUDA Toolkit** to visualize a timeline.
 
1. Install Nvidia Profiler inside your docker container (you should have CUDA installed inside the container!):

  ```apt install  nvidia-profiler```
2. Download Wrapper for CUDA profiler start/stop API functions https://github.com/bshillingford/python-cuda-profile .
Use  ```cudaprofile.start()``` and  ```cudaprofile.stop()``` functions in your yourscript.py to select programm's part you want to profile.
3. Create a timeline file prof.nvvp:
  ```CUDA_DEVICE_ORDER=PCI_BUS_ID CUDA_VISIBLE_DEVICES=1 nvprof  -o prof.nvvp python yourscript.py```
4. Copy prof.nvvp file to your local computer
 
5. Install CUDA Toolkit on your local computer (you don't need GPU for that) https://developer.nvidia.com/cuda-toolkit
6. Open CUDA Toolkit app, select File -> Open -> prof.nvvp. Enjoy the visualization and analytics of your timeline!


## Example of yourscript.py file (PyTorch)
 
 ```python
 import cudaprofile
  
 import torch
 import torch.nn as nn 
 from torchvision.models import resnet50
  
 if __name__=="__main__":
  
     loader = ...  # Create here any dataset loader you want
     device = 'cuda'
  
     cudaprofile.start()
 
     model =  resnet50()  # Create your neural network
     model = model.to(device)
  
     # Warm up GPU by making several forward passes
     x = torch.randn(1, 3, 224, 224).to(device)
     _ = model(x)
  
     # Iterate through dataset doing forward pass for each batch 
     for i, (b, _) in enumerate(loader):
         b = b.to(device)
         _ = model(b)
  
         if i > 10:
             break
  
     cudaprofile.stop()
 ```