# Set a Ubuntu for the Tensorflow-gpu (install a cuda toolkit in a native system)

Anaconda 의 tensorflow-gpu 1.12.0 를 사용하기 위한 Ubuntu 설정

1. Ubuntu 설치하기
  - Ubuntu 16.04 를 설치 한다.
    * http://releases.ubuntu.com/16.04/
    * tensorflow 1.12.0 은 cuda 9.2 를 지원하고 cuda 9.2 는 ubuntu 18.04 용이 없다.
    * tensorflow 1.13 은 cuda 10 을 지원한다고 하며 이 경우 ubuntu 18.04 를 설치해야 함. (2019/02/04 현재 1.13 은 python 용으로 없음)

2. Cuda 설치
  - cuda toolkit 9.2 을 download 받는다
    * https://developer.nvidia.com/cuda-92-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu
  - cudnn 7.3.1 을 download 받는다.
    * https://developer.nvidia.com/cudnn
    * nvidia 개발자 가입이 필요 합니다.
  - cuda 를 설치 한다. (cuda toolkit 을 9.2 의 local 을 download)
    $ sudo dpkg -i cuda-repo-ubuntu1604-9-2-local_9.2.148-1_amd64.deb
    $ sudo apt-key add /var/cuda-repo-9-2-local/7fa2af80.pub
    $ sudo apt-get update
    $ sudo apt-get install cuda
  - ~/.profile 에 PATH='/usr/local/cuda-9.2/bin:$PATH' 를 추가한다.
  - ~/.profile 에 LD_LIBRARY_PATH='/usr/local/cuda-9.2/lib64:LD_LIBRARY_PATH' 를 추가한다.
  - cuda toolkit 9.2 를 설치하면 nvidia driver 396 가 설치 된다. 따라서 미리 nvidia driver 를 설치해줄 필요가 없다.
  - reboot 한다.
  - cudnn package 를 설치 한다. (파일 어플리케이션에서 더블 클릭) <-안 해줘도 tensorflow-gpu 동작함..... ???
  - tensorflow 1.10 부터 1.12 는 cuda 9.2 를 사용해야 하며 tensorflow 1.9 는 cuda 9.0 을 사용해야 함. 아니면 insufficient cuda version error 가 발생함.
3. Anaconda 설치
  - Anaconda 를 download 받는다.
    * https://www.anaconda.com/distribution/
  - Anaconda 를 설치 한다.
    $ chmod u+x Anaconda3-2018.12-Linux-x86_64.sh
    $ ./Anaconda3-2018.12-Linux-x86_64.sh
  - 가상 환경을 만든다. (option)
    $ conda create -n tf-gpu
    $ conda activate tf-gpu
  - tensorflow-gpu 설치
    $ conda install tensorflow-gpu matplotlib
  
4. Test
  - sample 을 실행했을 때 아래와 같은 log 가 출력되면 정상적으로 동작하는 것임.
--------------------------------------------------------------------------------------------------------------------
2019-02-04 17:54:15.774332: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1432] Found device 0 with properties: 
name: GeForce GTX 1060 major: 6 minor: 1 memoryClockRate(GHz): 1.6705
pciBusID: 0000:01:00.0
totalMemory: 5.94GiB freeMemory: 5.64GiB
2019-02-04 17:54:15.774389: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1511] Adding visible gpu devices: 0
2019-02-04 17:54:16.787620: I tensorflow/core/common_runtime/gpu/gpu_device.cc:982] Device interconnect StreamExecutor with strength 1 edge matrix:
2019-02-04 17:54:16.787672: I tensorflow/core/common_runtime/gpu/gpu_device.cc:988]      0 
2019-02-04 17:54:16.787686: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1001] 0:   N 
2019-02-04 17:54:16.787939: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1115] Created TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:0 with 5416 MB memory) -> physical GPU (device: 0, name: GeForce GTX 1060, pci bus id: 0000:01:00.0, compute capability: 6.1)
--------------------------------------------------------------------------------------------------------------------
  - 3분 딥러닝 텐스플로우맛의 GAN sample 을 이용하여 test 결과
    CPU : 100회 실행에 21분
    GPU : 100회 실행에 3분

