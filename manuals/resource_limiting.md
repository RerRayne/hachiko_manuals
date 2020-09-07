# Resource Limiting

Every docker container now is capped with 4CPU and 16Gb RAM.

For GPU resources limiting please use CUDA_VISIBLE_DEVICES.
Running Python scripts:
```bash
CUDA_VISIBLE_DEVICES=0 python script.py # change 0  with whatever card is available
```

To make it a bit easier, add the following to your `~/.bashrc`:
```bash 
export CUDA_VISIBLE_DEVICES=0 # change 0  with whatever card is preferable
```
Now re-login and run the usual:
```bash
python script.py
```

**NB** GPU IDs in **nvidia-smi** do not correspond to IDs in Tensorflow.

Running code from Jupyter notebook:

If you didn't add the above export line to your _~/.bashrc_, or for some reason need to use a different GPU for the current piece of code, you can use the following:
```python
import os
os.environ["CUDA_DEVICE_ORDER"]="PCI_BUS_ID"  
os.environ["CUDA_VISIBLE_DEVICES"]="0" # change 0  with whatever card is available
``` 
To pick which GPU to use, take a look at **nvidia-smi** output (you’d prefer the one with less utility/memory usage).

Now, if you have no good reason to require memory on all of the GPUs, it is crucial to use the following configs to your Tensorflow session:
```python
config = tf.ConfigProto()
config.gpu_options.allow_growth = True # will use the minimum necessary amount of memory
```
Finally,
`sess =  tf.Session(config=config)` 
or
```python
with tf.Session(config=config) as sess:
	doSmth()
```

Always remember that both DGX-1 are shared among many individuals, so make sure you release the resources whenever you don't need them:)