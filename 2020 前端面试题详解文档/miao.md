# 双向绑定简单实现

```html
<body>
  <input type="text" id='in'>
  <span id='out'></span>
</body>
<script>
  let obj = {
    hello:null
  }
  Object.defineProperty(obj,'hello',{
    set:function(newValue){
      document.getElementById('in').value = newValue
      document.getElementById('out').innerHTML = newValue
    }
  })
  document.getElementById('in').addEventListener('keyup',function(e){
    obj.hello = e.target.value //这里先动然后set 调用改变页面
  })
</script>
```



2020年2月18日，我们家来了一位新的家庭成员：一只价值800元的小蓝猫（这800块钱还是我帮朋友公司写了一个官方主页挣来的，算是写代码来的第一桶金吧）。

这是喵喵到家的第一个天

3月1号，到家两周，我们发现它得了猫藓，小可怜不到两个月就带上耻辱圈，刚戴上的时候只能倒着走超搞笑

3月9号，与猫藓战斗一周后终于妥协，把毛得猫藓的毛给剃了，发现了隐藏在毛下更多的猫藓，可怜

3月24号，继续战斗了两周，有所好了不少，毛也长了不少，不再是秃头怪了

3月30号，感觉好的差不多了，摘下了耻辱圈，开始皮

4月3号，现在长得超级大了耶

4月6号，复发猫藓现

4月16号，治疗，疯狂药浴

4月27号，基本康复，再戴几天

5月30号，又发现皮下又猫藓好像，下狠心把身上毛剃了

6月28号，基本放弃治疗，也不掉毛，也不破

8月20号，现在从小猫咪变成了一只超凶的喵喵







