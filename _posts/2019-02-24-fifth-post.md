---
title : "LightGBM-GPU Python Interface install on windows10(using OpenCL, Boost, CMake, and VS Build Tools, OpenCL by CUDA Toolkit)"
date : 2019-02-24 20:20
categories : jekyll update
---
<br/>
Catboost만 주구장창 사용하던 중 LightGBM이 regression에서 더 좋은 성능을 보인다는 글을 보고, GPU 버전으로 LightGBM을 설치해 봤다.<br/>
그리고 Build를 직접 해야하는 여느 패키지들에서 그렇듯 LightGBM 설치 시에도 약간의 Error들을 겪었다.<br/>
<br/>
나처럼 LightGBM GPU를 Windows 10에 설치하려는 분들이 원활하게 설치할 수 있게 도움을 줄 겸, 
그리고 나중에 내가 다시 설치할 때를 대비할 겸 그 과정을 정리해 본다.<br/>
(내가 맞닥뜨린(문법 맞음 ㅎㅎ) Error Code들을 함께 올려 정리하면 좋겠지만... 이미 command prompt와 git bash를 종료해버려서 ㅠ 아쉽지만 패스한다.)<br/>
<br/>
Windows10에 LightGBM GPU 버전을 Build 하는 방법은 두 가지로 나뉘는 듯 하다.<br/>
나는 이 중 뭔가 덜 복잡해 보이는 MSVC(Microsoft Visual C++) 사용을 택했다.<br/>
만약 MinGW를 사용하는 방법을 택하고 싶다면 [여기](https://lightgbm.readthedocs.io/en/latest/GPU-Windows.html) 를 참고하면 된다.<br/>
<br/>
LightGBM gpu 버전 Build를 위해서는 OpenCL이 필요한데, Intel SDK, AMD APP SDK, NVIDIA CUDA Toolkit의 세 가지 중 선택할 수 있다.<br/>
본 포스팅에서는 CUDA Toolkit이 설치돼 있음을 가정하고 진행한다.<br/>
<br/>
그리고 버전 호환 등 자세한 내용은 본 포스팅 맨 아래에 있는 링크(LightGBM 공식 Document를 참고하길 바란다.)<br/>
<br/>
<br/>

1. 먼저 필요한 Tool들을 설치한다.
- [Git for Windows](https://git-scm.com/download/win)</br>
<code>
	Git 설치 및 기초적인 사용 방법은 구글링하면 많이 나오니 한 번 찾아보길 바란다.
</code>
- [CMake](https://cmake.org/download/)</br>
<code>
	이 페이지에서 Binary distributions의 cmake-3.14.0-rc2-win64-x64.zip 다운로드 / 잠시 후 cmake 명령어를 사용해야 하니, cmake 설치 과정 중 환경 변수 등록 여부를 묻는 순서에 반드시 등록을 체크하자.
</code>
- [Microsoft Visual Studio Build Tools](https://visualstudio.microsoft.com/ko/downloads/?rr=https%3A%2F%2Flightgbm.readthedocs.io%2Fen%2Flatest%2FInstallation-Guide.html)</br>
<code>
	이 페이지 하단 Visual Studio 2017용 도구 의 Visual Studio 2017용 Build Tools 다운로드 / 설치 시 반드시 'Visual C++ 빌드 도구'를 선택해 함께 설치해야 한다. / 이미 Visual Studio와 C++ 빌드 도구가 설치돼 있을 경우 이 단계는 당연히 패스해도 된다.
</code>
- [Boost Binaries](https://bintray.com/boostorg/release/boost-binaries/1.69.0#files/1.69.0/binaries)</br>
<code>
	boost_1_69_0-msvc-14.1-64.exe 다운로드 / 나만 그런 것인지는 모르겠지만 다운로드가 100%인 순간에 완료가 안 되고 꽤나 한참 멈춰있다. 기다리다 보면 완료가 되니 인내심을 가지고 기다리자.(필자는 이 상태로 컴퓨터 켜놓고 자고 일어났더니 완료돼 있었다.)
</code>
</br>

2. boost binaries에 대해 환경변수를 등록해줘야 한다. 공식 문서에는 command prompt에서 Set ~~~ 하는 걸로 소개를 했지만, 확실하게 하기 위해서 시스템 환경 변수 편집에 들어가서 직접 path를 추가하자.(혹시 환경변수 추가하는 방법과 동작 원리를 모른다면, 당장 구글링 해서 습득해야 한다. 환경 변수 등록은 어떤 작업에서든 기본 중 기본이다.)(아래의 Path는 물론 boost binaries를 기본 옵션 경로로 설치했다는 전제 하에 쓴 것이다.)
- <code>BOOST_ROOT 는 C:\local\boost_1_69_0\ 로 등록</code>
- <code>BOOST_LIBRARYDIR 은 C:\local\boost_1_69_0\lib64-msvc-14.1\ 로 등록</code>
</br>

3. git을 사용해 LightGBM의 github repository 속 소스들을 복사해 온다.(적당한 폴더를 골라 그 폴더에 진입한 후 진행한다.) 이 때 git을 환경변수 등록해서 command prompt에서 진행해도 되고, git bash에서 진행해도 된다.
- <code>git clone --recursive https://github.com/Microsoft/LightGBM</code>
</br>

4. 복사된 LightGBM 폴더에 진입해 build 폴더를 만들고 source build를 진행한다.
- <code>cd LightGBM</code>
- <code>mkdir build</code>
- <code>cmake -DCMAKE_GENERATOR_PLATFORM=x64 -DUSE_GPU=1 ..</code>
- <code>cmake --build . --target ALL_BUILD --config Release</code>

5. 이제 Python Interface를 설치한다. 두 가지 방법이 있는 것 같은데 테스트 결과 두 가지 방법 모두 잘 작동하는 듯 하다.
- <code>git clone 한 LightGBM 폴더 속 python-package 폴더로 이동 후, python setup.py install --precompile</code>
- <code>pip install lightgbm --install-option=--gpu</br>
(가상환경을 사용할 경우 그 가상환경의 pip를 잘 선택해 설치하자. 필자의 경우 특정 가상환경의 python과 pip를 환경변수 등록해 놓고 사용하고 있다.)</code>
</br>
</br>

<hr />
- 참고
### [LightGBM 공식 Document Installation Guide - Build GPU Version - Windows](https://lightgbm.readthedocs.io/en/latest/Installation-Guide.html#id18)
### [LightGBM 공식 Document GPU Tutorial - Install Python Interface(optional)](https://lightgbm.readthedocs.io/en/latest/GPU-Tutorial.html#install-python-interface-optional)
### [LightGBM github repository LightGBM Python-package - Installation - Build GPU Version](https://github.com/Microsoft/LightGBM/tree/master/python-package)