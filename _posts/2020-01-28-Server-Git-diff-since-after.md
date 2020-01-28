---
layout: post
title: "[Git] Git diff"
category: Server
tags:
- Server
- Git
- GitHub
- git_diff

lastmod : 2020-01-28 15:00:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

<!--미리보기-->
## Git diff

### ago
- 3일전부터 2일전까지 수정된 파일 조회
```linux
git diff --name-only "@{3 days ago}" "@{2 days ago}"
```

- 3일전부터 2일전까지 수정된 파일 조회(jpg 파일 제외)
```linux
git diff --name-only "@{3 days ago}" "@{2 days ago}" | grep -v jpg
```

### 특정기간

- 2020-01-08 이후 수정된 파일 조회(jpg 파일 제외)
```linux
git diff --name-only master@{2020-01-08}..master@{now} | grep -v jpg
```

참고 : [git: list all files added/modified on a day (or week/month…)](https://stackoverflow.com/questions/8016645/git-list-all-files-added-modified-on-a-day-or-week-month)

