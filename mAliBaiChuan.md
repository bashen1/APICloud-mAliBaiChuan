# **目录**
* [initTae](#a0)
* [showLogin](#a1)
* [getUserInfo](#a2)
* [logout](#a3)
* [showTaokeItemById](#a4)
* [showTaokeItemByUrl](#a5)
* [addCartPage](#a6)
* [shopPage](#a7)
* [myOrdersPage](#a8)
* [myCartsPage](#a9)
* [错误码](#a10)

#**概述**
> ##使用须知
> 不同的安卓证书及iOS包会有不同的SDK（其实不同的也就是那一张yw_1222.jpg），并得到不一样的 **"安全图片文件：yw_1222.jpg"** ，所以此版本为测试版本，在APICloud创建项目时候使用默认证书，生成apk时候也请选择测试版。
> 如果在使用过程中有任何的问题及建议，请发邮件到401828628@qq.com
>##申请步骤
> 1. 登录[阿里百川](http://baichuan.taobao.com/)，进如控制台
> 2. 新建一个应用，然后在右上角选择新建的应用，左侧记录下这个应用的AppKey**（在config.xml配置中需要用到）**
> 3. 点击左侧『API申请』，右侧确保『初级电商能力』状态为已获得
> 4. 点击左侧『我的产品后台』，右侧开通『百川电商SDK』
> 5. 点击左侧『系统设置』，右侧选择『应用设置』进行相关配置
> 5. 点击左侧『安全图片获取』，右侧填入在APICloud编译的apk与iOS的BundleID，分别获取iOS和Android下的验证图片
> 6. 下载解压**[自定义模块.zip](http://ol1d6flsx.bkt.clouddn.com/%E8%87%AA%E5%AE%9A%E4%B9%89%E6%A8%A1%E5%9D%97.zip)**，分别复制yw_1222.jpg到各个目录替换原来的yw_1222.jpg。***注意：请压缩mAliBaiChuanPic目录为zip**(当然为了以防万一，这个Git也有下载，在ModuleCustom目录)
> 7. 根据[自定义模块说明](http://docs.apicloud.com/Module-Dev/Upload-custom-module)分别上传模块包至APICloud后台，模块名称默认为***mAliBaiChuanPic***

----------
##需要在config.xml配置如下信息

```xml

<preference name="querySchemes" value="tbopen,tmall"/>
<feature name="mAliBaiChuan">
    <param name="urlScheme" value="tbopen+阿里百川appkey"/>
</feature>
```

<div id="a0"></div>

#**initTae**
初始化阿里百川SDK
initTae()
##示例代码
```js
var alibaichuan = api.require('mAliBaiChuan');
alibaichuan.initTae();
```
##可用性
iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a1"></div>
#**showLogin**
打开手淘授权登陆
showLogin(function(ret, err){})
##callback(ret, err)
ret：
- 类型：JSON对象
- 内部字段：

```js
{
    userNick:"rocke" ,               //用户昵称
    avatarUrl:"http://...",          //用户头像
    openId:"AAE...",                 //用户ID
    isLogin:"true",                  //是否登陆，字符串，true/false
}
```
err：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 1000,                     //错误码
    message:"user is not exist"      //错误描述
}
```
##示例代码
```js
var alibaichuan = api.require('mAliBaiChuan');
alibaichuan.showLogin(function(ret, err) {
    if (ret) {
        alert("登录success:" + JSON.stringify(ret));
    } else {
        alert("登录error:" + JSON.stringify(err));
    }
});
```
##可用性
iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a2"></div>

#**getUserInfo**
获取登陆的用户的相关信息
getUserInfo(function(ret, err){})
##callback(ret, err)
ret：
- 类型：JSON对象
- 内部字段：

```js
{
    userNick:"rocke" ,               //用户昵称
    avatarUrl:"http://...",          //用户头像
    openId:"AAE...",                 //用户ID
    isLogin:"true",                  //是否登陆，字符串，true/false
}
```
err：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 90000,                     //错误码
    message:"Not logged in"           //错误描述
}
```

##示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
alibaichuan.getUserInfo(function(ret, err) {
    if (ret) {
        alert("用户信息 ret - " + JSON.stringify(ret));
    } else {
        alert("用户信息 err - " + JSON.stringify(err));
    }
});
```

##可用性
iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a3"></div>

#**logout**
退出登陆
logout(function(ret, err){})
##callback(ret, err)
ret：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 0,                    //正确码
    message:"success"            //描述
}
```

err：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 90000,               //错误码
    message:"Not logged in"     //错误描述
}
```

##示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
alibaichuan.logout(function(ret, err) {
    if (ret) {
        alert("用户信息 ret - " + JSON.stringify(ret));
    } else {
        alert("用户信息 err - " + JSON.stringify(err));
    }
});
```

##可用性
iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a4"></div>

#**showTaokeItemById**
通过itemid打开宝贝
showTaokeItemById({params},function(ret, err){})
##params

itemid:
-类型：字符串
-描述：商品的id，如 https://detail.tmall.com/item.htm?id=41799734995 中的itemid为41799734995

mmpid:
-类型：字符串
-描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

isvcode:
-类型：字符串
-描述：开发者自己传入，可以在订单中跟踪此参数

opentype:
-类型：字符串
-描述：选择打开item的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开商品

##callback(ret, err)
ret：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 0,                    //正确码
    message:"success",           //描述
    orderid:"102391838774"     //订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 90001,                    //错误码
    message:"Parameter is null"      //错误描述
}
```

##示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    itemid : "522997347023",
    mmpid:"mm_00000000_0_0",
    isvcode:"app",
    opentype:"html5"
};
alibaichuan.showTaokeItemById(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

##可用性
iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a5"></div>

#**showTaokeItemByUrl**
通过商品URL打开宝贝（可以打开任何页面，包括百度等。**注意此接口如果想跟单到阿里妈妈，必须使用推广链接**）
showTaokeItemByUrl({params},function(ret, err){})
##params

url:
-类型：字符串
-描述：完整链接，如果想跟单到阿里妈妈，必须使用推广链接

mmpid:
-类型：字符串
-描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

isvcode:
-类型：字符串
-描述：开发者自己传入，可以在订单中跟踪此参数

opentype:
-类型：字符串
-描述：选择打开item的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开商品

##callback(ret, err)
ret：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 0,                    //正确码
    message:"success",           //描述
    orderid:"102391838774"      //订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 90001,                     //错误码
    message:"Parameter is null"       //错误描述
}
```

##示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    url:"https://detail.tmall.com/item.htm?id=35517204304",
    mmpid:"mm_00000000_0_0",
    isvcode:"app",
    opentype:"html5"
};
alibaichuan.showTaokeItemByUrl(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

##可用性
iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a6"></div>

#**addCartPage**
添加商品到购物车
addCartPage({params},function(ret, err){})
##params

itemid:
-类型：字符串
-描述：商品的id，如 https://detail.tmall.com/item.htm?id=41799734995 中的itemid为41799734995

mmpid:
-类型：字符串
-描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

isvcode:
-类型：字符串
-描述：开发者自己传入，可以在订单中跟踪此参数

opentype:
-类型：字符串
-描述：选择打开item的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开商品

##callback(ret, err)
ret：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 0,                     //正确码
    message:"success",            //描述
    orderid:"102391838774"     //订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 90001,                     //错误码
    message:"Parameter is null"       //错误描述
}
```

##示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    itemid : "522997347023",
    mmpid:"mm_00000000_0_0",
    isvcode:"app",
    opentype:"html5"
};
alibaichuan.addCartPage(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

##可用性
iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a7"></div>

#**shopPage**
打开店铺
shopPage({params},function(ret, err){})
##params

shopid:
-类型：字符串
-描述：店铺ID，如 https://shop137312735.taobao.com/index.htm 中的shopid为137312735

mmpid:
-类型：字符串
-描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

isvcode:
-类型：字符串
-描述：开发者自己传入，可以在订单中跟踪此参数

opentype:
-类型：字符串
-描述：选择打开店铺页面的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开店铺

##callback(ret, err)
ret：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 0,             //正确码
    message:"success",    //描述
    orderid:"102391838774"//订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 90001,                     //错误码
    message:"Parameter is null"       //错误描述
}
```

##示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    shopid : "137312735",
    mmpid:"mm_00000000_0_0",
    isvcode:"app",
    opentype:"html5"
};
alibaichuan.shopPage(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

##可用性
iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a8"></div>

#**myOrdersPage**
我的订单页
myOrdersPage({params},function(ret, err){})
##params

orderStatus:
-类型：字符串
-描述：0: *为全部订单* | 1: *为待付款订单* | 2: *为待发货订单* | 3: *为待收货订单* | 4: *为待评价订单*

allOrder:
-类型：字符串
-描述：YES: 显示全部订单，NO : 显示ISV自己创建的订单

mmpid:
-类型：字符串
-描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

opentype:
-类型：字符串
-描述：选择打开item的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开店铺

isvcode:
-类型：字符串
-描述：开发者自己传入，可以在订单中跟踪此参数

##callback(ret, err)
ret：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 0,                     //正确码
    message:"success",            //描述
    orderid:"102391838774"        //订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 90001,                     //错误码
    message:"Parameter is null"       //错误描述
}
```

##示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    orderStatus:"0"
    allOrder:"YES",
    mmpid:"mm_00000000_0_0",
    isvcode:"app",
    opentype:"html5"
};
alibaichuan.myOrdersPage(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

##可用性
iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a9"></div>

#**myCartsPage**
购物车列表页
myCartsPage({params},function(ret, err){})
##params

mmpid:
-类型：字符串
-描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

opentype:
-类型：字符串
-描述：选择打开item的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开购物车列表页

isvcode:
-类型：字符串
-描述：开发者自己传入，可以在订单中跟踪此参数

##callback(ret, err)
ret：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 0,                    //正确码
    message:"success",           //描述
    orderid:"102391838774"       //订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：
- 类型：JSON对象
- 内部字段：

```js
{
    code : 90001,                     //错误码
    message:"Parameter is null"       //错误描述
}
```

##示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    mmpid : "mm_00000000_0_0",
    isvcode : "app",
    opentype:"html5"
};
alibaichuan.myCartsPage(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

##可用性
iOS系统，Android系统
可提供的1.0.0及更高版本

<div id="a10"></div>

#**错误码**
-0 请求成功
-90000 用户未登陆
-90001 参数为空
-其他，阿里百川返回的code和错误提示

