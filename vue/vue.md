## vue的基本使用

### 一、前端优化

##### （1）、合适的时候使用合适的指令

​	v-if和v-show：

​	v-if：直接控制元素的显示隐藏，页面上看不倒指令包含的标签

​	v-show:是在元素上添加行内样式【display：none】来控制元素的显示隐藏

总结：v-if：在页面需要的时候才会加载，不需要的时候不加载，控制元素dom层的加载，效率远远低于v-show

​	v-show：加载行内样式，控制元素的显示隐藏，一直加载，但是只操作一次dom，所以效率会高。

【频繁的切换使用v-show，不频繁的时候使用v-if】

#### （2）、v-bind简单说明

![](C:\Users\吕运学\Desktop\vue\img\v-bind.png)

![](C:\Users\吕运学\Desktop\vue\img\v-bind的其他属性.png)

### 二、组件间参数的传递

1、自定义事件使用【子传父】

![](C:\Users\吕运学\Desktop\vue\img\子传父之（自定义事件的处理）.png)

2、子传父【通过回调函数】

![](C:\Users\吕运学\Desktop\vue\img\子传父（通过回调函数）.png)

3、父传子

![](C:\Users\吕运学\Desktop\vue\img\父传子.png)

三、动画

1、

![](C:\Users\吕运学\Desktop\vue\img\过度动画.png)

![](C:\Users\吕运学\Desktop\vue\img\过度动画结构.png)

2、animate的基本使用【先下载引入使用】

![](C:\Users\吕运学\Desktop\vue\img\animate的基本使用（先下载引入使用）.png)



3、动画实现组件的切换

![](C:\Users\吕运学\Desktop\vue\img\组件的切换.png)

4、标签内是多元素的话，需要使用 <transition-group></transition-group>

```
<transition-group
enter-active-class="animeted slideInLeft"
leave-active-class="animeted slideOutRight"
>
<div v-if="show" class="box"></div>
<div v-if="show" class="box"></div>
<div v-if="show" class="box"></div>
</transition-group>
```

四、生命周期

1、beforeCreate:-------------------------------实例创建前

(1)、能获取到实例

（2）、能获取到data里边的数据

(3)、不能获取到元素的节点

（4）、对data里边的数据修改无效

2、created：-------------------------------实例创完成

（1）、能更改data里边的数据

（2）、不能获取dom元素，此时vue实例创建完成，还没有真正挂载数据，所以还在是操作虚拟3dom

（3）、可以再此发起ajax请求

​	原因：此时还没有挂载元素，在这里可以更改数据，修改数据，基本不消耗资源，等到元素挂载了的时候，更改的数据会和dom树进行对比，然后一次性渲染数据，只会操作一次dom节点。

3、beforeMount:-------------------------------元素挂在前

  (1)、还不能获取到dom节点

（2）、可以修改data里边的数据，

（3）、也可以在此请求数据

4、mountd：-------------------------------元素挂载完成

（1）、可以获取到dom节点了，进行相关的dom操作

（2）、可以修改数据，

（3）、也可以请求数据

5、beforeUpdate：-------------------------------数据更新前

（1）、能获取到节点

（2）、有数据更新时才会触发，只有一次数据更新时，只会触发一次

6、updated：-------------------------------数据更新完成

（1）、能获取到节点

（2）、有数据更新时才会触发，只有一次数据更新时，只会触发一次

7、beforeDestroy:-------------------------------销毁前

(1)、一般执行不到，主要在事件里边

（2）、处理遗憾【回忆人生】

（3）、![](C:\Users\吕运学\Desktop\vue\img\触发销毁.png)

（4）、移除事件，双向绑定，生命周期，dom元素和数据依然保留，移除定时器等

8、destroyed：-------------------------------销毁完成

（1）、这两个生命周期做的事情都差不多，都可以在任意一个里边做相关的操作









