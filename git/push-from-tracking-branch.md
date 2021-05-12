## Local에 존재하지 않는 remote branch를 가져와서 작업 후 PR 생성하기
### Remote Branch 가져오기
```
git checkout -t origin/remote_branch
```
로컬에 `remote_branch`로 브랜치가 생성됨

### Tracking Branch 확인하기
아래와 같이 `git branch -vv`로 어떤 브랜치가 트래킹되고 아닌지 확인 가능

![Untitled](https://user-images.githubusercontent.com/45524783/117829697-f9810280-b2ad-11eb-9a1c-de5d34a3ce51.png)

### 참고
- 리모트 브랜치 확인하기: `git branch -r`
- 로컬 브랜치 확인: `git branch -l`
- 리모트+로컬 브랜치 확인: `git branch -a`

### 작업내용 추가하기
- 가져온 브랜치에서 새로운 feature branch 생성
- 기존에 하던 방식과는 다르게 맨 끝에 기준이 되는 branch를 적어주는 것에 주의‼️
```
git checkout -b feature/new_feature remote_branch
```

- 작업 후 git add, git commit
- git push origin **feature/new_feature** → PR 생성됨
