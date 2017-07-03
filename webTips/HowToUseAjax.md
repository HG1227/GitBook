## $AJAX使用方法

```
$.ajax({
    type: 'GET', 
    url: '999.php', 
    data: {
        uname:'Tom', age: 20
    }, 
    beforeSend: function(){ 
        console.log('before send....'); 
        console.log(arguments); 
    }, 
    success: function(){ 
        console.log('success....'); 
        console.log(arguments); 
    }, 
    error: function(){ 
        console.log('error....'); 
        console.log(arguments); 
    }, 
    complete: function(){ 
        console.log('complete....'); 
        console.log(arguments); 
    } 
});
```