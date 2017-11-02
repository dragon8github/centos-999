函数的使用并且获取返回值，通常有以下三种：

```js
showage () {
  echo '123'
}
temp=`showage` 
# temp=$(showage) 
echo $temp


showage () {
  return '123'
}
showage
echo $?


temp=''
showage () {
  temp='123'
}
showage
echo $temp
```



