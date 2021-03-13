---
title:  "Add profile image & File transfer from Window10 to WSL2"
excerpt: "프로필 이미지를 추가하면서 해결한 ssh connection refuse 오류"

categories:
  - Blog
  
tags:
  - Blog
  - ssh

last_modified_at: 2021-03-14T03:51:00-03:55:00

---

프로필 이미지를 추가하려고 아이폰에 저장되있는 사진을 불러오려고 했는데,원래 블로그 작업을 wsl에서 하고 있다 보니까 윈도우에 사진을 옮기고 scp로 wsl로 옮기려고 했다.  
```
scp profile.jpg minje0204@ip:/mnt/c/...(파일저장위치)  
```  
위명령어를 쳤는데 ssh: connect to host (wsl ip) port 22: Connection refused 에러가 떴다.  

찾아본 결과 나는 wsl에서  
```
vi /etc/ssh/sshd_config
```
로 ssh 세팅 환경에서 port지정해주는 부분의 주석처리를 지웠다 default는 22다.  
PasswordAuthentication yes도 No에서 yes로 바꿔주었다.  

이렇게 세팅 2개를 완료하고도 똑같이 connection refused 에러가 뜨길래
찾아보니까 WSL2부터는 hyper-v 엔진위에서 Linux를 돌리기 때문에 별도의 가상 NIC를 가지고 있다는 말을 보고  
WSL 내에서 ip를 확인해보니 왠걸 window 프롬프트에서 wsl로 나온 ip주소와 다른 ip주소가 나왔다.  

WSL에서 찾은 ip주소를 입력해주는 정상적으로 scp 가 작동했다.


  
  
  - - - 
