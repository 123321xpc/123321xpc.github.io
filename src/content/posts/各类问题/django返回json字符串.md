---
title: django返回json字符串
published: 2024-05-25
description: ''
image: ''
tags: [python, django]
category: '各类问题'
draft: false 
---







在`django`框架中，如果要返回`JSON`字符串，例如下面这种：

```python
class Result:
    def __init__(self, code, msg, data):
        self.code = code
        self.msg = msg
        self.data = data

    def to_json(self):
        return json.dumps({"code": self.code, "msg": self.msg, "data": self.data})
```

在返回的时候需要关闭安全模式，具体如下：

```python
return JsonResponse(result.to_json(), safe=False)
```

