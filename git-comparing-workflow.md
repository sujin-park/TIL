작성중

## Git을 이용하여 협업하기

보통 많이 사용하는 Git 협업 방식에는 4가지가 있다.

1. Centralized Workflow
2. Feature Branch Workflow
3. Gitflow Workflow
4. Forking Workflow


### Centralized Workflow



### Feature Branch Workflow

master란 브랜치를 기본적으로 사용하며 각자 새로운 브랜치를 생성하고, master 브랜치에 마지막 결과물을 push한다.

한 사람이 repository 를 생성하고 다른 팀원들은

* git clone url을 입력하거나 IDE tool에서 저장소를 clone 한다.

* git branch -b "sujin"
* git checkout sujin
* git push origin sujin

* git add .
* git commit -m "branch-practice"
* git checkout master
* git merge sujin
* git push origin master

 






### Gitflow Workflow



### Forking Workflow
