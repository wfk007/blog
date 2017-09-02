# 美团电影在线付款

本来想搞一个1元看电影，结果无功而返。

进入购买页面，把提交表单中所有价钱都用js改成1块钱

```js

document.getElementById('J_SeatShow').setAttribute('data-price','1')
document.getElementById('J_SeatShow').setAttribute('data-fee','0')
document.getElementsByClassName('val')[0].innerHTML = '¥1'
document.getElementsByTagName('em')[3].innerHTML = '¥1'

```
然后提交购买请求，以为就这么简单？naive

验证当然是有的，一开始我认为是在服务端验证，后来发现提交表单数据后，HTTP请求体中originalprice
字段没变化（还是原价），没变化？难道没有使用表单的数据？很兴奋，万一使用这两个字段验证呢。
使用fiddle的bpu断点调试，拦截表单请求的地址，把HTTP请求体的originalprice改成1，然后再发出去。
结果，还！是！原！价！
难受，难受死了！
too naive...

应该是在服务端验证，在服务端...服务端...在服务端怎么搞...
在服务端，直接通过HTTP请求体的id从数据库获取数据（除了id以外其他数据都是迷惑人的？），生成订单返回前端
（能修改HTTP返回体内容么？即便修改成功有用么？~~~），僵住了。


