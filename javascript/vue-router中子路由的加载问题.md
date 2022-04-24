在学习vu-router时，我们往往会看到这样的例子

```
const routes = [
  {
    path: '/home',
    name: 'Home',
    component: Home,
    children: [
      {
        path: 'son',
        name: 'Son',
        component: Son
      }
    ]
  }
]
```

这时候访问son组件的路由是```/home/son```
但是在项目中配置的时候我们往往都要配置一个重定向，由父页面指向子页面

```
const routes = [
  {
    path: '/home',
    name: 'Home',
    component: Home,
    redirect: '/son',//这里配置了重定向
    children: [
      {
        path: '/son',//这里的路径跟上边的不一样，前边加上了'/'
        name: 'Son',
        component: Son
      }
    ]
  }
]
```

这时候只要我们访问主页面```/home```页面就会跳转到```/son```路由，并把home组件连带son组件一起加载出来。这与上边有什么不同呢？上边访问的路径是```/home/son```，而这里只要访问```/son```就能直接打开同样的页面。在网上找了好多资料，最后在官网找到这样一句话
![image.png](https://upload-images.jianshu.io/upload_images/23374955-15e786334f7176a9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我理解的意思是，如果在嵌套路由的path前加上了'/'，那么这个path就会被当作根路径。所谓根路径应该就是可以直接访问到的路径，vue-router应该会把以'/'开头的子路由与它所在的父组件默认绑定在一起，当我们访问```/son```时就相当于访问了```/home/son```。

> 最后总结一句话就是：子路由的path如果前边带 **'/ '** 则访问这个子路由时只需要访问子路由的path，系统会默认加载它所在的父组件。如果前边没有 **'/ '** 那么需要按照  /父路由/子路由的形式访问
