# handsome主题自定义CSS

将以下代码添加至后台主题设置 自定义CSS。

```
/*无盒子模型依然带背景*/
html{
    background-image: url("https://image.creat.kim/picgo/20190326213706.jpg");
    background-attachment: fixed;
}
/*歌单圆角化，以及歌单前面小点配色*/
#skPlayer .skPlayer-list {
    border-radius: 1px 1px 10px 10px; 
    /*圆角度自行修改，如果想实现上面圆角请修改1px为其他数值，规则为上左，上右，下右，下左，方向为顺时针方向，最大圆角度为50px*/
}
#skPlayer .skPlayer-list .skPlayer-list-sign{
    background-color: #b822c1;
}

/*为右上头像弹出框增加圆角*/
.dropdown-menu{
  border-radius: 1px 1px 10px 10px; /*修改圆角度方法同上*/
}

/*定义滚动条高宽及背景 高宽分别对应横竖滚动条的尺寸*/
::-webkit-scrollbar{
    width: 3px;
    height: 16px;
    background-color: rgba(255,255,255,0);
}
 
/*定义滚动条轨道 内阴影+圆角*/
::-webkit-scrollbar-track{
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
    border-radius: 10px;
    background-color: rgba(255,255,255,0);
}
 
/*定义滑块 内阴影+圆角*/
::-webkit-scrollbar-thumb{
    border-radius: 10px;
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,.3);
    background-color: #555;
}



/*标题、一言居中*/
.center-part header{
    text-align:center;
}

/*首页文章版式圆角化*/
.panel{
    border: none;
    border-radius: 15px;
}

.panel-small{
    border: none;
    border-radius: 15px;
}

.item-thumb{
    border-radius: 15px;  
}



/*首页文章图片获取焦点放大*/
.item-thumb{
    cursor: pointer;  
    transition: all 0.6s;  
}

.item-thumb:hover{
      transform: scale(1.05);  
}

.item-thumb-small{
    cursor: pointer;  
    transition: all 0.6s;
}

.item-thumb-small:hover{
    transform: scale(1.05);
}

/*鼠标样式*/
  * {
      cursor: url("/assets/mouse/cursor_5.png"),auto!important
  }
  :active {
      cursor: url("/assets/mouse/cursor_6.png"),auto!important
  }
/*首页头像自动旋转*/
.thumb-lg{
    width:100px;
}

.avatar{
    -webkit-transition: 0.4s;
    -webkit-transition: -webkit-transform 0.4s ease-out;
    transition: transform 0.4s ease-out;
    -moz-transition: -moz-transform 0.4s ease-out; 
}

.avatar:hover{
    transform: rotateZ(360deg);
    -webkit-transform: rotateZ(360deg);
    -moz-transform: rotateZ(360deg);
}

#aside-user span.avatar{
    animation-timing-function:cubic-bezier(0,0,.07,1)!important;
    border:0 solid
}

#aside-user span.avatar:hover{
    transform:rotate(360deg) scale(1.2);
    border-width:5px;

```