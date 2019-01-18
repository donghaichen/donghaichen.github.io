# 二进制和字符串相互转换方法

```javascript
//将Blob 对象转换成字符串
function binaryToStr(blob) 
{
    var reader = new FileReader();
    reader.readAsText(blob, 'utf-8');
    reader.onload = function (e) {
        return reader.result;
    }
}

//将字符串 转换成 Blob 对象
function strToBinary(str)
{
    return new Blob([str], {
        type: 'text/plain'
    })
}
```