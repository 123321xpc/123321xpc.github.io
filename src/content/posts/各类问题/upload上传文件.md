---
title: upload上传文件
published: 2024-05-26
description: ''
image: ''
tags: [python, 上传文件, django]
category: '各类问题'
draft: false 
---









使用`element`的`el-upload`组件上传文件，后端使用`Django`框架接收，前端传入参数类型必须为`formData`，请求方法为`POST`如下：

```typescript
const formData = ref<FormData>(new FormData());

const handleChange: UploadProps['onChange'] = (file, fileList) => {
  formData.value = new FormData();  // 清空formData避免重复添加
  fileList.forEach(fileItem => {
    if (!fileItem.raw) return;
    formData.value.append('file', fileItem.raw);
  });
}
```

如果需要加入其他参数，则必须在`formData`中使用`append`加，如下：

```typescript
formData.value.append('type', 'cartoon');
```



后端使用如下函数接收：

```python
    # 接收文件数据
    uploaded_files = request.FILES.getlist('file')
    # 接收其他数据
    type = request.POST.get('type')
```

