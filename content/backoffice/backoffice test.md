[[Journal/2026-08-19]]

- citations에서 지정한 경로의 루트 path가 vault의 기본 폴더가 아니라 quartz의 기본 설치 폴더를 기준으로 동작하는 거 같다.
- 폴더 이름에  `.` 이 들어갈 경우 아래처럼 설정한 뒤 해당 폴더를 클릭하면 404 페이지로 이동한다.

```
source: "@quartz-community/explorer"
enabled: false
options:
title: Explorer
folderClickBehavior: link # "link" to navigate or "collapse" to toggle
folderDefaultState: collapsed # "collapsed" or "open"
useSavedState: true
```
