# 시작하기

git remote add origin https://github.com/rtgo/gitbook-javascript2.git
git branch -M main
git push -u origin main



각각의 로컬 레포의 리모트 저장소 URL을 확인합니다.
git remote -v



그러면, 다음과 같은 값을 확인할 수 있습니다. 아래는 chullino_1의 계정을 쓰는 레포에 저장된 리모트 저장소 URL입니다



origin https://github.com/chullino_1/project.git (fetch)
origin https://github.com/chullino_1/project.git (push)


각의 로컬 레포의 리모트 저장소 URL을 아래처럼 변경합니다. 계정 정보를 포함시키는 방식입니다. 예를 들어, chullino_1계정을 쓰는 로컬 레포에서는 아래 명령어를 입력합니다.



git remote set-url origin https://chullino_1@github.com/chullino_1/project.git


이렇게 하고 나니, 두 개 이상의 계정에 대해서도 패스워드 입력 과정을 자동화할 수 있게 되었습니다.


# 구조 

```shell
📂 [프로젝트 루트]
  📂.gitbook
    📂assets      #  여기에 이미지 파일을 둔다.
  📂java-8        # 하위페이지를 포함하는 경우 폴더를 만들고
     📄README.md  # 그 아래에 README.md 파일을 두어 페이지의 내용을 표시한다.
  📄README.md      # README 파일을 하나 둔다. 
  📄SUMMARYE.md    # 목차 파일을 하나 만든다
  📄page1.md    # 최상위 페이지
  📄page3.md    # 최상위 페이지
  ... 
```


## 목차 파일 구조 

```markdown
# Table of contents

* [Initial page](README.md)
* [Vi](vi.md)
* [apt-get](apt-get.md)
* [ifconfig](ifconfig.md)
* [JDK](jdk.md)
* [iptables](iptables.md)
* [systemctl 명령어](systemctl.md)
* [mariadb 설치](mariadb.md)
```

