# Git 명령어 - merge

## basic
```
git merge 브랜치명
```
- 병합하는 방법 두 종류
    - rebase : 이력을 다듬어야 할 때.(Git flow를 정확히 이해해야 사용할 수 있음)
    - merge : 단순히 명령만 입력하면 병합이 됨

- 병합 순서
    1. ```git checkout master```로 옮겨감
    2. ```git merge 브랜치명``` 을 하면 master에 병합됨

## Conflict
- 다른 브랜치에 같은 파일이 다른 내용으로 있으면 충돌하기 때문에 merge되지 않음
- 이럴 때는 사용자가 저장을 원하는 버전을 수동으로 지정해주어야 함
- ```vim 파일명```으로 충돌된 파일에 들어가 충돌된 부분 확인

![images_grinding_hannah_post_3bb861d6-7323-4452-a247-a19fec6e9eeb_image](https://user-images.githubusercontent.com/97326130/172914760-595aa27e-3c85-4db2-9061-c363186f8afc.png)

- 필요없는 부분 삭제 후 ```:wq```로 저장
- 그리고 다시 ```git add```, ```git commit```으로 커밋을 해주면 됨!

## vim
```
vim 파일경로
```
내용 추가 후 ```esc``` + ```:wq```로 저장
