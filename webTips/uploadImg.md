###图片上传预览的原理
*使用 类型为file 表单的提交 
*`new FileReader()`读取本地文件 进行预览  
*表单提交避免刷新页面 让`form` 指向 `iframe`再监听`iframe`中返回的内容 
####效果展示

![上传图片效果展示](/assets/uploadImg.jpg)

```html
<form action="/uploadAuditInf.do" id="myForm" method="post"  enctype="multipart/form-data" accept-charset="UTF-8" target="aa">
  <div class="upload-area">
    <div class="upload-item">
      <div class="upload-placeholder">
        <div class="upload-add-icon"></div>
        <p>上传手持银行卡照</p>
        <input type="file" name="file" class="upload-file" onchange="preview(this,3)" accept="image/gif, image/jpeg" >
        <div class="upload-img"></div>
        <div class="upload-hover" onclick="removeImg(this,3)">
          <span >点击重新上传</span>
        </div>
      </div>
    </div>
  </div>
</form>
//防止防止表单提交页面跳转
<iframe name="aa" src="" style="display:none"></iframe>
```

```javascript
  // 图片预览
  function preview(file,num) {
    var viewImg = $('.upload-img')[num];
    if (file.files && file.files[0]) {
      if(checkSize(file)){
        var reader = new FileReader();
        reader.onload = function(evt) {
          viewImg.innerHTML = '<img src="' + evt.target.result + '" />';
          $(viewImg).next().addClass('upload-hover2')
        }
        reader.readAsDataURL(file.files[0]);
      }else{
        Walert('图片质量不要超过2M',3)
        file.value=''
      }
    } else {
      viewImg.innerHTML = '<div class="img" style="filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale,src=\'' + file.value + '\'"></div>';
    }
  }
  // 检查图片大小 不超过2M
  function checkSize(file){
    if(file.files[0].size >1024*1024*2){
      return false
    }else{
      return true
    }
  }
  // 提交图片
  function submitImg(){
    //触发表单提交
    //监听页面返回值 
    var t = setInterval(function() {
      //获取iframe标签里body元素里的文字。即服务器响应过来的"上传成功"或"上传失败"
      var word = $("iframe[name='aa']").contents().find("body").text();
      if (word != "") {
          alert('finishUpload')//上传成功后的操作
          clearInterval(t);   //清除定时器
        }
      }, 1000);
  }
```

