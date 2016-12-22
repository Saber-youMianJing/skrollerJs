# skrollr.js
***
>[skrollr][1]是一个开源的视差滚动js插件，兼容性极强，可以兼容各种浏览器（包括IE）以及手机端（IOS/Android），基本上没有兼容不了的。
skrollr自身体积只有8k，加上兼容ie和手机端的插件也不到30k，对于一个展示用页面来说这个体积确实不大了。

### 如何使用
~~~html
<script type="text/javascript" src="dist/skrollr.min.js"></script>
<script type="text/javascript">  
    skrollr.init();  
</script> 
~~~


#### 先看一下他可以做什么
* 目标：滚动条在最上方时，让div的background-color为rgb(74,74,74)；当滚动条滚动到500px时div的background-color变化为rgb(140,201,220)；
>设置元素的“data-开始位置”和“data-结束位置”的值即可，skrollr会自动处理颜色随滚动渐变效果。
参考 d1.html
~~~html
<div class="sky "  
data-0="background: rgb(74,74,74);" 
data-1000="background: rgb(140,201,220);" >
~~~
* 目标：让太阳转起来
~~~html
<img src="examples/img/sun.png"  alt="Sun"  class="sun" 
data-100="top: 100%; right: 20%;transform:rotate(0deg)" 
data-1000="top: 10%; right: 0% ;transform:rotate(720deg)" 
style="top: 100%; right: 20%;">
~~~
***
### 初始化及參數
~~~html
<script type="text/javascript">
var scrollObj = skrollr.init({
  smoothScrolling : true,
  smoothScrollingDuration:200,
   //主要都是让scroll事件不要这么敏感，动画才不会看起來卡卡的。
  constants:{
    initTop:100
  },
  //可以定义一些常数在影格使用，Example: data-_myconst-200 and skrollr.init({constants: {myconst: 300}}) result in data-500.
  scale:1,
  //可以調整ScrollBar往下拉对应到keyframe的值等倍放大
  forceHeight:true,
  //让文本高度自动滿足Keyframe的條件
  mobileCheck:function(){},
  mobileDeceleration:0.004,
  //真多移动装置的功能
  easing：linear
  //运动曲线，定义新的或者覆盖原有的曲线
  //1、linear: default 
  //2、quadratic 
  //3、cubic 
  //4、begin/end
  //4、swing
  //6、sqrt
  //7、outCubic
  //8、bounce: Bounces like a ball. 
  
  render: function(data) {
      //Log the current scroll position.

      console.log(data.curTop);
  }
});
  //render事件可以取得一些对象的信息
 {
    curTop: 10, //the current scroll top offset

    lastTop: 0, //the top value of last time

    maxTop: 100, //the max value you can scroll to. curTop/maxTop will give you the current progress.

    direction: 'down' //either up or down

}
</script>
~~~

#### 注意事项
>1、例子中只有两个“data-xxx”，但是你可以添加任意多的“data-xxx”，skrollr会自动创建之间的过渡动画。
2、两个“data-xxx”的值最好对应，比如 data-0="top:0%;left:0%;" data-500="top:10%;left:10%;" 而不是 data-0="left:0%;" data-500="top:10%;left:10%;" 如果缺项的话skrollr可能会创建出来不符合你想法的过渡动画。

#### 基本步骤说完了，接下来我们看一下视差网站的效果
参考 myscroll.html

