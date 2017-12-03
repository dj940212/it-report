### 项目简介

[*项目预览*](http://www.huxiaofei.me/webApp)

本项目为一个H5报告页面，运用了HTML5、CSS3、JS等技术，采用组件式开发，页面滚动采用了基于jQuery的FullPage.js，运用Canvas制作了柱形图、折线图、饼图、散点图等多种动态图表组件。

### 项目结构

![核心对象](http://imglf.nosdn.127.net/img/MklXTVZ2ekNiL0JqaHcvVlpGTk5rMDQyVGk1aXdRUE9uU0hDWnI2TzVmR2d1TWtBQkZTTVRRPT0.png?imageView&thumbnail=1680x0&quality=96&stripmeta=0&type=jpg)

### 事件

```javascript
    //page 上绑定进入和离开事件处理程序
    $('.page').on('onLeave',function(){
        console.log( $(this).attr('id') ,'==>>' ,'onLeave' );
        $(this).find('.component').trigger('onLeave');
    })
    $('.page').on('onLoad',function(){
        console.log( $(this).attr('id') ,'==>>' ,'onLoad' );
        $(this).find('.component').trigger('onLoad');
    })

    //component上绑定进入和离开事件处理程序
    $('.component').on('onLoad',function(){
        $(this).fadeIn();
        return false;
    })
```

### 核心对象与方法

H5为整个项目的内容组件对象，H5包含addPage（）、addComponent（）、loader（）三个方法。addComponent()方法接受两个参数，第一个参数为组件名name，第二个参数为一个对象cfg，储存组件基本参数。loader()方法,每个方法都返回`this`,使其能形成链式调用。
```javascript

    h5
    .addPage('face')
        .addComponent('logo',{
            text:'logo',
            width:400,
            height:100,
            css:{backgroundColor:'red',top:200,opacity:0},
            center:true,
            animateIn:{opacity:1},
            animateOut:{opacity:0}
        })
        .addComponent('slogan',{
            text:'slogan',
            width:400,
            height:100,
            css:{backgroundColor:'red',top:350},
        })
    .addPage('desc')
        .addComponent('caption',{
            width:400,
            height:100,
            css:{backgroundColor:'green',top:350},
            center:true,
        })
    .addPage('page-3')
        .addComponent('caption',{text:'课程方向分布'})
    .loader( );
```
#### loader( )方法

```javascript
this.loader = function( firstPage ){
        this.el.fullpage({
            onLeave:function( index, nextIndex, direction) {
                $(this).find('.h5_component').trigger('onLeave');
            },
            afterLoad:function( anchorLink, index ) {
            }
        });
        this.page[0].find('.h5_component').trigger('onLoad');
        if(firstPage){
            $.fn.fullpage.moveTo( firstPage );
        }
    }
```






