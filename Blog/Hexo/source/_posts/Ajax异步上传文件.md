---
title: ASP.NET MVC Web 异步上传文件示例
comments: true
categories:
  - .Net
tags:
  - Ajax
  - Web
  - 文件上传
  - Asp.Net Mvc Web
date: 2018-06-25 12:50:21
updated:
---

```html
//Html
<input type="file" name="uploadFile" />

//JavaScript，这里使用了 JQuery，也可以使用 Js 的 XMLHttpRequest 对象
<script>
	var fileObj = $("input[name=uploadFile]")[0].files[0];
	var formData = new FormData();
	$.ajax({
	        url: 'UploadSchemeWordFile.ashx',
	        type: 'POST',
	        data: formData,
	        async: true,
	        cache: false,
	        processData: false,
	        contentType: false,
	        success: function (resTxt) {
	            console.log(resTxt);
	        },
	        error: function (xhr, error, msg) {
	            console.log(xhr,error,msg);
	        }
	    });
</script>
```