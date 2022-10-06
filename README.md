# chapter6

## 6.1 새로운 작업 <br>
브랜치: 나뭇가지, 지사, 분점 등 줄기 하나에서 뻗어 나온 갈림길 <br>
저장 공간 하나에서 가상의 또 다른 저장 공간을 만드는 것

### 6.1.1 브랜치 작업 <br>
기존의 브랜치 작업: 새로운 기능을 추가하거나 많은 변경이 예상될 때 작업 폴더를 통째로 복사하고, <br>
복사한 폴더 이름을 변경함 <br>
안정적인 기존 코드는 남겨 두고, 복제된 작업 폴더에서 도전적인 작업들을 하기 위해 코드를 분리함 <br>
+ 브랜치는 프로젝트를 독립적으로 관리하는 데 사용 <br>

개발자는 항상 안정된 코드 상태를 유지하고, 개발 중인 작업과 구분하여 관리해야 함 <br>
잦은 버그 수정과 새로운 기능을 구현할 때마다 작업 폴더를 복사하는 것은 프로젝트 유지 관리 측면에서 좋지 않음 <br>
많은 프로젝트 폴더를 복제하면 향후 코드를 통합하기 어려움 <br>
+ 깃을 사용하면 프로젝트 작업 폴더를 복사하지 않고 기존 코드와 분리해서 작업할 수 있음

### 6.1.2 깃 브랜치 특징
**1. 가상 폴더** <br>
작업 폴더를 실제로 복사하지 않고, 가상 폴더로 생성 <br>
외부적으로는 물리적인 파일 하나만 있는 것으로 보임 <br>
생성된 작업 폴더는 물리적으로 복제된 구조보다 유연하게 처리할 수 있음 <br>
브랜치로 생성된 가상 폴더는 빠른 공간 이동이 가능

**2. 독립적인 동작** <br>
브랜치를 이용하면 원본 폴더와 분리해 독립적으로 개발 작업을 수행 <br>
기존에는 소스 코드의 작업 폴더를 별도로 생성해 각자의 폴더에서 코드를 작업한 후 <br>
소스 코드 2개를 다시 하나로 합쳐야 했음 <br>
깃과 같은 버전 관리 시스템을 이용하면 분리된 코드를 좀 더 쉽게 병합할 수 있음 <br>
분리된 브랜치에서 소스 코드를 각자 수정한 후 원본 코드에 병합하는 명령만 실행하면 됨 <br>
깃 브랜치는 규모가 큰 코드를 처리할 때 매우 유용함

**3. 빠른 동작** <br>
다양한 버전 관리 도구도 브랜치 기능 지원 <br>
깃의 브랜치 기능은 다른 버전 관리 도구보다 가볍고, 브랜치 전환이 빠른 것이 특징 <br>
깃은 **Blob** 개념을 도입해 내부를 구조화 <br>
**Blob**: 포인트와 유사한 객체 <br>
깃은 브랜치를 변경할 때 포인터를 이동해 빠르게 전환 <br>
브랜치 명령을 사용하면 내부적으로 커밋을 생성해 브랜치로 할당 <br>
다른 버전 관리 시스템: 폴더의 파일 전체를 복사 <br>
깃: 41바이트를 가지는 해시(SHA1) 파일 하나만 만들면 됨

## 6.2 실습 준비 <br>
깃은 기본적으로 **master** 브랜치를 하나 가지고 있음 <br>
브랜치는 **HEAD 포인터**를 가지고 있음


### 6.2.1 저장소 생성 및 초기화 <br>
브랜치 실습을 위한 환경 구축 <br>

> $ cd 메인폴더 <span style="color:orange"> <br>
> $ mkdir gitstudy06 <span style="color:orange"> -------- 새 폴더 만들기 <br>
> $ cd gitstudy06 <span style="color:orange"> <br>
> infoh@DESKTOP MINGW64 /e/gitstudy06 <br>
> $ git init <span style="color:orange"> -------- 저장소 초기화 <br>
> initialized empty Git repository in E:/gitstudy06/.git/


깃 배시에서 초기화 명령어를 실행, 저장소가 초기화되면 터미널 프롬프트 창에 현재 브랜치 이름이 같이 출력

> infoh@DESKTOP MINGW64 /e/gitstudy06 
  (master)<span style="color:orange">


현재 브랜치가 master라는 것을 확인할 수 있음 <br>
깃 배시는 리눅스 명령을 사용할 수 있고, 현재 브랜치의 작업 위치도 쉽게 알 수 있음

### 6.2.2 기본 브랜치 <br>
모든 커밋과 이력은 브랜치에 기록 <br>
깃은 최소한 브랜치가 1개 이상 필요함 <br>
저장소를 처음 초기화하면 master 브랜치 하나가 자동으로 생성  <br>
첫 번째 커밋은 master 브랜치에서 시작 <br>
초기화한 후에 status 명령어를 실행

> infoh@DESKTOP MINGW64 /e/gitstudy06 
  (master) <span style="color:orange"> <br>
> $ git status <span style="color:orange"> <br>
> On branch master <span style="color:orange"> -------- 브랜치 작업 위치  <br>
> No commits yet  <br>
> nothing to commit (create/copy files and use "git add" to track)  <br>

status 명령어의 출력 결과 메시지에서 "On branch master"를 확인할 수 있음 <br>
깃에서는 항상 현재 작업하는 브랜치 위치를 확인하는 것이 중요 <br>
또는 branch 명령어로 현재 브랜치를 확인할 수 있음

> infoh@DESKTOP MINGW64 /e/gitstudy06 
  (master) <span style="color:orange"> <br>
> $ git branch <span style="color:orange"> -------- 브랜치 목록  <br>
>* master 

branch 명령어는 생성된 모든 브랜치를 출력함 <br>
깃에서 기본적으로 선택되는 브랜치는 master <br>
하지만 기본값인 master 이름을 그대로 사용할 필요는 없음
