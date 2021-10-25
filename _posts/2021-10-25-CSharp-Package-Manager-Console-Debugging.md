---
layout: post
title: Entity Framework 에서 Package Manage Console에 Debug Attach 하는 방법 
description: Entity Framework 에서 Package Manage Console에 Debug Attach 하는 방법
summary: Entity Framework 에서 Package Manage Console에 Debug Attach 하는 방법
tags: [C#]
---

# 아래 코드를 사용하여 Debugger 를 lunch하면 됨
```c#
    if(!System.Dignostics.Debugger.IsAttached)
        System.Diagnostics.Debugger.Launch();
```
