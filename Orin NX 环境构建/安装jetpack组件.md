安装其他的jetpack组件如CUDA，cudn等

sudo apt update

sudo apt install nvidia-jetpack



配置cuda 环境变量

```
# CUDA 12.6 Environment
export CUDA_HOME=/usr/local/cuda-12.6
export PATH=${CUDA_HOME}/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=${CUDA_HOME}/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
export LIBRARY_PATH=${CUDA_HOME}/lib64${LIBRARY_PATH:+:${LIBRARY_PATH}}
```

