# PyTorch-GFX803
Torch and TorchVision compiled on Alma Linux 9 for GFX803 arch.

## 💻 Requirements

This is what I recommend. If you want to use anything other than this, you will be on your own.

- Alma Linux 9 (or another RHEL 9-based distro)
- Python 3.9


## AMDGPU and ROCm Repositories

rocm.repo file content:

```
[amdgpu]
name=amdgpu
baseurl=https://repo.radeon.com/amdgpu/6.1.2/rhel/9.4/main/x86_64/
enabled=1
priority=50
gpgcheck=1
gpgkey=https://repo.radeon.com/rocm/rocm.gpg.key
```


rocm.repo file content:

```
[ROCm-5.7.3]
name=ROCm5.7.3
baseurl=https://repo.radeon.com/rocm/rhel9/5.7.3/main
enabled=1
priority=50
gpgcheck=1
gpgkey=https://repo.radeon.com/rocm/rocm.gpg.key
```


## AMDGPU and ROCm Packges

AMDGPU packages:
```
dnf install amdgpu-dkms python3-pip python3-devel gperftools
```

ROCm packages:
```
dnf install rocm-hip-sdk5.7.3 rocminfo5.7.3 roctracer5.7.3 miopen-hip5.7.3
```


## ROCm Post-installation

```
sudo tee --append /etc/ld.so.conf.d/rocm.conf <<EOF
/opt/rocm/lib
/opt/rocm/lib64
EOF
sudo ldconfig
```
```
export PATH=$PATH:/opt/rocm-5.7.3/bin
```

## Get Stable Diffusion
```
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
```

## Options for low-vram
```
--precision full --no-half --lowvram --opt-split-attention-v1 --upcast-sampling
```
