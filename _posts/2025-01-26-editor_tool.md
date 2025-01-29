---
title:  "Editor Tool"
excerpt:  "코딩을 하면서 쓰이는 도구들 사용 팁들"
categories: 
- Tools

tags:
- VSCode
toc_label: TOC
toc: true
toc_sticky: true
 
date: 2025-01-26
---



# Colab
- 회사 서버에서 보통 작업을 하다 보니 콜랩을 상대적으로 덜쓰게 됨
- 여러 파일을 다운받으려면 압축해서 다운 받도록 하자
```python
!zip -r /content/file.zip /content/Folder_To_Zip

from google.colab import files
files.download("/content/file.zip")
```

- [콜랩을 로컬머신과 연동하기](https://research.google.com/colaboratory/local-runtimes.html)
```python
jupyter notebook --no-browser --NotebookApp.allow_origin='https://colab.research.google.com'
--port=8888 --NotebookApp.port_retries=0
```


# VSCode

## UI 설명
VS Code Explorer 표시되는 대문자 의미
| 기호 | 의미                                                                                   |
|------|----------------------------------------------------------------------------------------|
| **S** | Submodule (이 Git 저장소 안에 다른 Git 저장소가 포함되어 있는 경우)                     |
| **A** | Added (새로운 파일이 저장소에 추가된 경우)                                             |
| **M** | Modified (기존 파일이 수정된 경우)                                                    |
| **D** | Deleted (파일이 삭제된 경우)                                                          |
| **U** | Untracked (새 파일이 추가되었거나 변경되었지만 아직 저장소에 추가되지 않은 경우)       |
| **C** | Conflict (파일에 충돌이 있는 경우)                                                    |
| **R** | Renamed (파일 이름이 변경된 경우)                                                     |


## 편의 기능 설정

| 항목     | 설정 방법                  |
|---------|---------------------------|
| **Explorer 간격 조절하기**     | - Settings → Tree indent 값 조절하기<br>- wordwrap → on                                               |
| **파일 두 번 클릭 시 열기**    | `"workbench.list.openMode": "doubleClick"`         |
| **Preview 비활성화**          | `"workbench.editor.enablePreview": false`         |
| **Explorer 자동 확장 방지**    | `"explorer.autoReveal": false`      |
| **터미널 디폴트를 CMD로 설정** | - Shift+Ctrl+- → preference 검색 → default profile    |
| **Sticky Scroll**             | `"editor.stickyScroll.enabled": true`            |
| **터미널 색상**               | - Open user settings (Ctrl+,)<br>- [vscode-base16-term](https://glitchbone.github.io/vscode-base16-term/#/atelier-plateau-light) |
| **검색 시 이동 방지**         | "editor.find.cursorMoveOnType": false             |


## 유용한 단축키


## 디버깅
- `.vscode` 폴더 아래의 launch.json을 수정하도록 한다.
- 가장 기본적인 형태는 다음처럼 할 수 있음
- working directory와 어떤 program을 엔트리 포인트로 할지 정할 수 있음
```json
{
    "configurations": [
        {
            "name": "graido",
            "type": "python",
            "request": "launch",
            "program": "/home/aiteam/tykim/ml_infer_gradio/ML_infer_prototype/demo_gen_gradio.py",
            "console": "integratedTerminal",
            "cwd": "/home/aiteam/tykim/ml_infer_gradio/ML_infer_prototype",
            "args": []
        },
    ]
    }
```


```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python Debugger: Current File",
            "type": "debugpy",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal"
        },
        {
            "name": "Python: Remote Attach",
            "type": "debugpy",
            "request": "attach",
            "connect": {
                "host": "localhost",
                "port": 56781
            },
            "pathMappings": [
                {
                    "localRoot": "/purestorage/project/tyk/3_CUProjects/FAS/instruct-pix2pix", //"/purestorage/project/tyk/3_CUProjects/ArtfaceStudio_ML", // //"${workspaceFolder}", //"/purestorage/project/tyk", //"${workspaceFolder}",
                    "remoteRoot": "/purestorage/project/tyk/3_CUProjects/FAS/instruct-pix2pix"// "/purestorage/project/tyk/3_CUProjects/ArtfaceStudio_ML" //"/purestorage/project/tyk/3_CUProjects/FAS/instruct-pix2pix"
                }
            ],
            "requireExactSource": false
        },
        {
            "name": "Remote - Art",
            "type": "debugpy",
            "request": "attach",
            "connect": {
                "host": "localhost",
                "port": 56781
            },
            "pathMappings": [
                {
                    "localRoot": "/purestorage/project/tyk/3_CUProjects/ArtfaceStudio_ML/train/t2i_with_extension", //"${workspaceFolder}", //"/purestorage/project/tyk", //"${workspaceFolder}",
                    "remoteRoot": "/purestorage/project/tyk/3_CUProjects/ArtfaceStudio_ML/train/t2i_with_extension"
                }
            ],
        },
        {
            "name": "Remote-color",
            "type": "debugpy",
            "request": "attach",
            "connect": {
                "host": "localhost",
                "port": 56781
            },
            "pathMappings": [
                {
                    "localRoot": "/purestorage/project/tyk/9_Animation/Colorization",
                    "remoteRoot": "/purestorage/project/tyk/9_Animation/Colorization"
                }
            ],
        },
        {
            "name": "Remote-art",
            "type": "debugpy",
            "request": "attach",
            "connect": {
                "host": "localhost",
                "port": 56781
            },
            "pathMappings": [
                {
                    "localRoot": "/purestorage/project/tyk/3_CUProjects/ArtfaceStudio_ML",
                    "remoteRoot": "/purestorage/project/tyk/3_CUProjects/ArtfaceStudio_ML"
                }
            ],
        },
        {
            "name": "Remote-pbc",
            "type": "debugpy",
            "request": "attach",
            "connect": {
                "host": "localhost",
                "port": 56781
            },
            "pathMappings": [
                {
                    "localRoot": "/purestorage/project/tyk/9_Animation/BasicPBC",
                    "remoteRoot": "/purestorage/project/tyk/9_Animation/BasicPBC"
                }
            ],
        },
        {
            "name": "Remote-sdio",
            "type": "debugpy",
            "request": "attach",
            "connect": {
                "host": "localhost",
                "port": 56781
            },
            "pathMappings": [
                {
                    "localRoot": "/purestorage/project/tyk/9_Animation/Semantics/sd-dino",
                    "remoteRoot": "/purestorage/project/tyk/9_Animation/Semantics/sd-dino"
                }
            ],
        },
        {
            "name": "Remote-seg",
            "type": "debugpy",
            "request": "attach",
            "connect": {
                "host": "localhost",
                "port": 56781
            },
            "pathMappings": [
                {
                    "localRoot": "/purestorage/project/tyk/9_Animation/Segmentation/CartoonSegmentation/animeinsseg/data",
                    "remoteRoot": "/purestorage/project/tyk/9_Animation/Segmentation/CartoonSegmentation/animeinsseg/data"
                }
            ],
            "justMyCode": false
        },
        {
            "name": "Remote-tmp",
            "type": "debugpy",
            "request": "attach",
            "connect": {
                "host": "localhost",
                "port": 56781
            },
            "pathMappings": [
                {
                    "localRoot": "/purestorage/project/tyk/9_Animation/Colorization_diff", //"/purestorage/project/tyk/11_Personalization/IDM-VTON", //"/purestorage/project/tyk/9_Animation/Segmentation/Segment-Everything-Everywhere-All-At-Once", //"/purestorage/project/tyk/9_Animation/sketchdeco-code", //
                    "remoteRoot": "/purestorage/project/tyk/9_Animation/Colorization_diff" //"/purestorage/project/tyk/11_Personalization/IDM-VTON" //"/purestorage/project/tyk/9_Animation/Segmentation/Segment-Everything-Everywhere-All-At-Once" // "/purestorage/project/tyk/9_Animation/sketchdeco-code" //"/purestorage/project/tyk/9_Animation/Segmentation/Segment-Everything-Everywhere-All-At-Once"
                }
            ],
            "justMyCode": false
        }
    ]
}
```

## Remote 관련

### 원격 접속 에러 해결하기
- 가끔씩 `Could not establish connection to xxx` 이렇게 에러가 나면서 remote가 안됨
- 가장 높은 확률로 해결되었던 방법
    - Vscode 상에서 확장을 삭제
    - C:\Users\ty-kim\.ssh\known_hosts 파일에서 IP 적힌 줄 삭제
    - C:\Users\ty-kim\.vscode\extensions 에 있는 Remote관련 폴더도 모두 삭제
    - Remote development extension 재설치
- 저것도 안되면 최후의 방법으로 해당 remote 서버에 직접 들어가서 `rm -r ~/.vscode-server`



## WSL 설치
0. 윈도우 설정
- 하이퍼바이저 플랫폼 긴으 켜기
- CPU 가상화 설정 (AMD SVM or Intel VT-x)
1. powershell을 열고 어떤 종류를 설치할지 확인 후 설치
```python
wsl --list --online
wsl --install -d <DistroName>

# 여러 개 설치후 하나 선택하기
wsl --set-default Ubuntu-20.04
```

2. 패키지 업데이트
```python
sudo apt update && sudo apt upgrade
```

3. WSL용 CUDA 설치
```python
sudo apt-key del 7fa2af80
wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-keyring_1.0-1_all.deb
sudo dpkg -i cuda-keyring_1.0-1_all.deb
rm cuda-keyring_1.0-1_all.deb
sudo apt update
sudo apt install cuda-11-8
```

4. Docker 설치
- Docker 자동 시작
```python
echo '# Start Docker daemon automatically when logging in if not running.' >> ~/.bashrc
echo 'RUNNING=`ps aux | grep dockerd | grep -v grep`' >> ~/.bashrc
echo 'if [ -z "$RUNNING" ]; then' >> ~/.bashrc
echo '    sudo dockerd > /dev/null 2>&1 &' >> ~/.bashrc
echo '    disown' >> ~/.bashrc
echo 'fi' >> ~/.bashrc
```