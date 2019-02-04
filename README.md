# Set a Ubuntu for the Tensorflow-gpu (install a cuda toolkit in a native system)

Anaconda 의 tensorflow-gpu 1.12.0 를 사용하기 위한 Ubuntu 설정

1. Ubuntu 설치하기
  - Ubuntu 16.04 를 설치 한다.
    * http://releases.ubuntu.com/16.04/
    * tensorflow 1.12.0 은 cuda 9.2 를 지원하고 cuda 9.2 는 ubuntu 18.04 용이 없다.

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
  
    
