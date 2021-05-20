## 로컬 브랜치와 리모트 브랜치 싱크 맞추기

```
git reset --hard origin/[REMOTE_BRANCH]
git clean -f -d
```
- 파일을 삭제 생성 등 stash로 되돌릴 수 없을때 사용한다.
- `git clean`: 작업하던 unstaged file들을 stash하지 않고 삭제하고 싶을때 사용한다.
  - `-f`: force
  - `-d`: 디렉토리까지 삭제
