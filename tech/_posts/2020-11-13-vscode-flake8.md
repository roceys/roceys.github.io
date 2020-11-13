---
layout: default
title: vscode flake8如何取消module level import not at top错误提示
subtitle: module level import not at top
apptitle: vscode flake8如何取消module level import not at top错误提示
category: tech
description: vscode python flake8如何取消module level import not at top of fileflake8(E402)错误提示 by ROCEYS 20201113
permalink: /:categories/:year/:month/:day/:title
author: ROCEYS
date: 2020/11/13
tags:
    - vscode
    - flake8
    - python
---

## vscode flake8如何取消module level import not at top错误提示

配置setting.json文件即可
```json
  "python.linting.flake8Args": [
		// 每行最大显示字符数设置
        "--max-line-length=600",
        // module level import not at top of fileflake8(E402) 
		// 需要忽略的代码规范提示编号
        "--ignore=E402",
    ]
```
