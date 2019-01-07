# **目录**

#### 初始化接口

 [initTae](#a0)

#### 用户接口

 [showLogin](#a1)
 
 [getUserInfo](#a2)
 
 [logout](#a3)

#### 百川接口

 [showTaokeItemById](#a4)
 
 [showTaokeItemByUrl](#a5)
 
 [addCartPage](#a6)
 
 [shopPage](#a7)
 
 [myOrdersPage](#a8)
 
 [myCartsPage](#a9)

#### 外部WebView

 [showTaokeItemByIdWeb](#a10)
 
 [showTaokeItemByUrlWeb](#a11)
 
 [addCartPageWeb](#a12)
 
 [shopPageWeb](#a13)
 
 [myOrdersPageWeb](#a14)
 
 [myCartsPageWeb](#a15)

#### 外部WebView操作

 [setBlockUrl](#a16)
 
 [removeWeb](#a17)
 
 [addPageDidListener](#a18)
 
 [addLoadingListener](#a19)
 
 [addJsToPage](#a20)
 
 [removeJsListener](#a21)
 
 [webGoBack](#a22)
 
 [webGoForward](#a23)
 
 [webRefresh](#a24)

#### 注意事项

 [关于鹊桥跟单](#a25)
 
 [关于高佣](#a26) 
 
 [关于adzone与appkey](#a27)
 
 [接口快速记忆法](#a28)


# **概述**
> ## 使用须知
> 不同的安卓证书及iOS包会有不同的SDK（其实不同的也就是那一张yw_1222.jpg），并得到不一样的 **"安全图片文件：yw_1222.jpg"** ，所以此版本为测试版本，在APICloud创建项目时候使用默认证书，生成apk时候也请选择测试版。
> 目前使用web的接口存在一定的问题，到手淘app授权时，如果用户点了右上角的返回键，会引起APP退出（百川的机制问题），iOS下一切正常
> 如果在使用过程中有任何的问题及建议，请发邮件到401828628@qq.com
> ## 申请步骤
> 1. 登录[阿里百川](http://baichuan.taobao.com/)，进如控制台
> 2. 新建一个应用，然后在右上角选择新建的应用，左侧记录下这个应用的AppKey **（在config.xml配置中需要用到）**
> 3. 点击左侧『API申请』，右侧确保『初级电商能力』状态为已获得
> 4. 点击左侧『我的产品后台』，右侧开通『百川电商SDK』
> 5. 点击左侧『系统设置』，右侧选择『应用设置』进行相关配置
> 6. 点击左侧『安全图片获取』，右侧填入在APICloud编译的apk与iOS的BundleID，分别获取iOS和Android下的验证图片
> 7. 下载解压 **[自定义模块.zip](https://github.com/bashen1/APICloud-mAliBaiChuan/raw/master/Files/%E8%87%AA%E5%AE%9A%E4%B9%89%E6%A8%A1%E5%9D%97.zip)**，分别复制yw_1222.jpg到各个目录替换原来的yw_1222.jpg。***注意：请压缩mAliBaiChuanPic目录为zip**
> 8. 根据[自定义模块说明](http://docs.apicloud.com/Module-Dev/Upload-custom-module)分别上传模块包至APICloud后台，模块名称默认为 **mAliBaiChuanPic**
> 9. **[案例源码,点击下载](https://github.com/bashen1/APICloud-mAliBaiChuan/raw/master/Files/widget.zip)**

----------
## 需要在config.xml配置如下信息

```xml

<preference name="querySchemes" value="tbopen,tmall"/>
<feature name="mAliBaiChuan">
    <param name="urlScheme" value="tbopen+阿里百川appkey"/>
</feature>
```

<div id="a0"></div>

# **initTae**

初始化阿里百川SDK

initTae(callback(ret, err))

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code:"0" ,               //字符串
    message:"success"
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "1000",                   //错误码，百川返回
    message:"user is not exist"      //错误描述，百川返回
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
alibaichuan.initTae(function(ret, err) {
    if (ret) {
        alert("ret:" + JSON.stringify(ret));
    } else {
        alert("err:" + JSON.stringify(err));
    }
});
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a1"></div>

# **showLogin**

打开手淘授权登陆

showLogin(callback(ret, err))

## callback(ret, err)

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
    code : "1000",                   //错误码
    message:"user is not exist"      //错误描述
}
```

## 示例代码

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

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a2"></div>

# **getUserInfo**

获取登陆的用户的相关信息

getUserInfo(callback(ret, err))

## callback(ret, err)

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
    code : "90000",                     //错误码
    message:"Not logged in"           //错误描述
}
```

## 示例代码

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

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a3"></div>

# **logout**

退出登陆

logout(callback(ret, err))

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "0",                    //正确码
    message:"success"            //描述
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "90000",               //错误码
    message:"Not logged in"     //错误描述
}
```

## 示例代码

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

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a4"></div>

# **showTaokeItemById**

通过itemid打开宝贝

showTaokeItemById({params},callback(ret, err))

## params

itemid:

- 类型：字符串
- 描述：商品的id，如 https://detail.tmall.com/item.htm?id=41799734995 中的itemid为41799734995

mmpid:

- 类型：字符串
- 描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

isvcode:

- 类型：字符串
- 描述：开发者自己传入，可以在订单中跟踪此参数

opentype:

- 类型：字符串
- 描述：选择打开item的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开商品

adzoneid:

- 类型：字符串
- 描述：阿里妈妈推广位ID，三段式PID最后一段

tkkey:

- 类型：字符串
- 描述：阿里妈妈后台，推广渠道ID

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "0",                //正确码
    message:"success",         //描述
    orderid:"102391838774"     //订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "90001",                  //错误码
    message:"Parameter is null"      //错误描述
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    itemid : "522997347023",
    mmpid:"mm_00000000_0_0",
    isvcode:"app",
    opentype:"html5",
    adzoneid: '0',
    tkkey: '0'
};
alibaichuan.showTaokeItemById(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a5"></div>

# **showTaokeItemByUrl**

通过商品URL打开宝贝（可以打开任何页面，包括百度等。**注意此接口如果想跟单到阿里妈妈，必须使用推广链接或者商品裸链接**）

showTaokeItemByUrl({params},callback(ret, err))

## params

url:

- 类型：字符串
- 描述：链接

mmpid:

- 类型：字符串
- 描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

isvcode:

- 类型：字符串
- 描述：开发者自己传入，可以在订单中跟踪此参数

opentype:

- 类型：字符串
- 描述：选择打开item的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开商品

adzoneid:

- 类型：字符串
- 描述：阿里妈妈推广位ID，三段式PID最后一段

tkkey:

- 类型：字符串
- 描述：阿里妈妈后台，推广渠道ID

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "0",                    //正确码
    message:"success",           //描述
    orderid:"102391838774"      //订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "90001",                     //错误码
    message:"Parameter is null"       //错误描述
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    url:"https://detail.tmall.com/item.htm?id=35517204304",
    mmpid:"mm_00000000_0_0",
    isvcode:"app",
    opentype:"html5",
    adzoneid: '0',
    tkkey: '0'
};
alibaichuan.showTaokeItemByUrl(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a6"></div>

# **addCartPage**

添加商品到购物车

addCartPage({params},callback(ret, err))

## params

itemid:

- 类型：字符串
- 描述：商品的id，如 https://detail.tmall.com/item.htm?id=41799734995 中的itemid为41799734995

mmpid:

- 类型：字符串
- 描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

isvcode:

- 类型：字符串
- 描述：开发者自己传入，可以在订单中跟踪此参数

opentype:

- 类型：字符串
- 描述：选择打开item的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开商品

adzoneid:

- 类型：字符串
- 描述：阿里妈妈推广位ID，三段式PID最后一段

tkkey:

- 类型：字符串
- 描述：阿里妈妈后台，推广渠道ID

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "0",                     //正确码
    message:"success",            //描述
    orderid:"102391838774"     //订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "90001",                     //错误码
    message:"Parameter is null"       //错误描述
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    itemid : "522997347023",
    mmpid:"mm_00000000_0_0",
    isvcode:"app",
    opentype:"html5",
    adzoneid: '0',
    tkkey: '0'
};
alibaichuan.addCartPage(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a7"></div>

# **shopPage**

打开店铺

shopPage({params},callback(ret, err))

## params

shopid:

- 类型：字符串
- 描述：店铺ID，如 https://shop137312735.taobao.com/index.htm 中的shopid为137312735

mmpid:

- 类型：字符串
- 描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

isvcode:

- 类型：字符串
- 描述：开发者自己传入，可以在订单中跟踪此参数

opentype:

- 类型：字符串
- 描述：选择打开店铺页面的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开店铺

adzoneid:

- 类型：字符串
- 描述：阿里妈妈推广位ID，三段式PID最后一段

tkkey:

- 类型：字符串
- 描述：阿里妈妈后台，推广渠道ID

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "0",             //正确码
    message:"success",    //描述
    orderid:"102391838774"//订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "90001",                     //错误码
    message:"Parameter is null"       //错误描述
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    shopid : "137312735",
    mmpid:"mm_00000000_0_0",
    isvcode:"app",
    opentype:"html5",
    adzoneid: '0',
    tkkey: '0'
};
alibaichuan.shopPage(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a8"></div>

# **myOrdersPage**

我的订单页

myOrdersPage({params},callback(ret, err))

## params

orderStatus:

- 类型：字符串
- 描述：0: *为全部订单* | 1: *为待付款订单* | 2: *为待发货订单* | 3: *为待收货订单* | 4: *为待评价订单*

allOrder:

- 类型：字符串
- 描述：YES: 显示全部订单，NO : 显示ISV自己创建的订单

mmpid:

- 类型：字符串
- 描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

opentype:

- 类型：字符串
- 描述：选择打开item的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开店铺

isvcode:

- 类型：字符串
- 描述：开发者自己传入，可以在订单中跟踪此参数

adzoneid:

- 类型：字符串
- 描述：阿里妈妈推广位ID，三段式PID最后一段

tkkey:

- 类型：字符串
- 描述：阿里妈妈后台，推广渠道ID

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "0",                     //正确码
    message:"success",            //描述
    orderid:"102391838774"        //订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "90001",                     //错误码
    message:"Parameter is null"       //错误描述
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    orderStatus:"0"
    allOrder:"YES",
    mmpid:"mm_00000000_0_0",
    isvcode:"app",
    opentype:"html5",
    adzoneid: '0',
    tkkey: '0'
};
alibaichuan.myOrdersPage(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a9"></div>

# **myCartsPage**

购物车列表页

myCartsPage({params},callback(ret, err))

## params

mmpid:

- 类型：字符串
- 描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

opentype:

- 类型：字符串
- 描述：选择打开item的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开购物车列表页

isvcode:

- 类型：字符串
- 描述：开发者自己传入，可以在订单中跟踪此参数

adzoneid:

- 类型：字符串
- 描述：阿里妈妈推广位ID，三段式PID最后一段

tkkey:

- 类型：字符串
- 描述：阿里妈妈后台，推广渠道ID

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "0",                    //正确码
    message:"success",           //描述
    orderid:"102391838774"       //订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "90001",                     //错误码
    message:"Parameter is null"       //错误描述
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    mmpid : "mm_00000000_0_0",
    isvcode : "app",
    opentype:"html5",
    adzoneid: '0',
    tkkey: '0'
};
alibaichuan.myCartsPage(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a10"></div>

# **showTaokeItemByIdWeb**

通过itemid打开宝贝

showTaokeItemByIdWeb({params},callback(ret, err))

## params

itemid:

- 类型：字符串
- 描述：商品的id，如 https://detail.tmall.com/item.htm?id=41799734995 中的itemid为41799734995

mmpid:

- 类型：字符串
- 描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

isvcode:

- 类型：字符串
- 描述：开发者自己传入，可以在订单中跟踪此参数

opentype:

- 类型：字符串
- 描述：选择打开item的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开商品

adzoneid:

- 类型：字符串
- 描述：阿里妈妈推广位ID，三段式PID最后一段

tkkey:

- 类型：字符串
- 描述：阿里妈妈后台，推广渠道ID

winObj:

- 类型：字符串
- 描述：(可选项) 注入到h5页面的全局window属性对象名称，与addJsToPage配合使用。

rect：

- 类型：JSON 对象
- 默认值：充满整个父页面
- 描述：（可选项）frame 的位置和大小。
- 内部字段：

```js
{
    x:0,             //左上角x坐标
    y:0,             //左上角y坐标
    w:320,           //宽度
    h:480            //高度
}
```

fixedOn：

- 类型：字符串类型
- 描述：（可选项）模块视图添加到指定 frame 的名字（只指 frame，传 window 无效）
- 默认：模块依附于当前 window


fixed:

- 类型：布尔
- 默认值：true
- 描述：是否将模块视图固定到窗口上，不跟随窗口上下滚动，可为空


pageClose:

- 类型：布尔
- 默认值：false
- 描述：购买完成后，是否关闭页面，可以不传这个参数，默认就带了（仅安卓下有效，false即不关闭付款后的页面，由于机制问题，安卓下如果设为true，会退出整个APP，但并非闪退，而是百川帮我们退出了app）

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "0",                    //正确码
    message:"success",           //描述
    orderid:"102391838774"     //订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "90001",                    //错误码
    message:"Parameter is null"      //错误描述
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    itemid : "522997347023",
    mmpid:"mm_00000000_0_0",
    isvcode:"app",
    opentype:"html5",
    adzoneid: '0',
    tkkey: '0',
    winObj: 'mAliBaiChuan',
    fixedOn: api.frameName,
    fixed: false,
    rect: {
    	x:0,
    	y:0,
    	w:api.frameWidth,
    	h:200
    }
};
alibaichuan.showTaokeItemByIdWeb(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```


## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a11"></div>

# **showTaokeItemByUrlWeb**


通过商品URL打开宝贝（可以打开任何页面，包括百度等。**注意此接口如果想跟单到阿里妈妈，必须使用推广链接或者商品裸链接**）

showTaokeItemByUrlWeb({params},callback(ret, err))

## params

url:

- 类型：字符串
- 描述：链接

mmpid:

- 类型：字符串
- 描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

isvcode:

- 类型：字符串
- 描述：开发者自己传入，可以在订单中跟踪此参数

opentype:

- 类型：字符串
- 描述：选择打开item的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开商品

adzoneid:

- 类型：字符串
- 描述：阿里妈妈推广位ID，三段式PID最后一段

tkkey:

- 类型：字符串
- 描述：阿里妈妈后台，推广渠道ID

winObj:

- 类型：字符串
- 描述：(可选项) 注入到h5页面的全局window属性对象名称，与addJsToPage配合使用。

rect：

- 类型：JSON 对象
- 默认值：充满整个父页面
- 描述：（可选项）frame 的位置和大小。
- 内部字段：

```js
{
    x:0,             //左上角x坐标
    y:0,             //左上角y坐标
    w:320,           //宽度
    h:480            //高度
}
```

fixedOn：

- 类型：字符串类型
- 描述：（可选项）模块视图添加到指定 frame 的名字（只指 frame，传 window 无效）
- 默认：模块依附于当前 window


fixed:

- 类型：布尔
- 默认值：true
- 描述：是否将模块视图固定到窗口上，不跟随窗口上下滚动，可为空


pageClose:

- 类型：布尔
- 默认值：false
- 描述：购买完成后，是否关闭页面，可以不传这个参数，默认就带了（仅安卓下有效，false即不关闭付款后的页面，由于机制问题，安卓下如果设为true，会退出整个APP，但并非闪退，而是百川帮我们退出了app）

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "0",                    //正确码
    message:"success",           //描述
    orderid:"102391838774"      //订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "90001",                     //错误码
    message:"Parameter is null"       //错误描述
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    url:"https://detail.tmall.com/item.htm?id=35517204304",
    mmpid:"mm_00000000_0_0",
    isvcode:"app",
    opentype:"html5",
    adzoneid: '0',
    tkkey: '0',
    winObj: 'mAliBaiChuan',
    fixedOn: api.frameName,
    fixed: false,
    rect: {
    	x:0,
    	y:0,
    	w:api.frameWidth,
    	h:200
    }
};
alibaichuan.showTaokeItemByUrlWeb(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```


## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a12"></div>

# **addCartPageWeb**

添加商品到购物车

addCartPageWeb({params},callback(ret, err))

## params

itemid:

- 类型：字符串
- 描述：商品的id，如 https://detail.tmall.com/item.htm?id=41799734995 中的itemid为41799734995

mmpid:

- 类型：字符串
- 描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

isvcode:

- 类型：字符串
- 描述：开发者自己传入，可以在订单中跟踪此参数

opentype:

- 类型：字符串
- 描述：选择打开item的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开商品

adzoneid:

- 类型：字符串
- 描述：阿里妈妈推广位ID，三段式PID最后一段

tkkey:

- 类型：字符串
- 描述：阿里妈妈后台，推广渠道ID

winObj:

- 类型：字符串
- 描述：(可选项) 注入到h5页面的全局window属性对象名称，与addJsToPage配合使用。

rect：

- 类型：JSON 对象
- 默认值：充满整个父页面
- 描述：（可选项）frame 的位置和大小。
- 内部字段：

```js
{
    x:0,             //左上角x坐标
    y:0,             //左上角y坐标
    w:320,           //宽度
    h:480            //高度
}
```

fixedOn：

- 类型：字符串类型
- 描述：（可选项）模块视图添加到指定 frame 的名字（只指 frame，传 window 无效）
- 默认：模块依附于当前 window


fixed:

- 类型：布尔
- 默认值：true
- 描述：是否将模块视图固定到窗口上，不跟随窗口上下滚动，可为空


pageClose:

- 类型：布尔
- 默认值：false
- 描述：购买完成后，是否关闭页面，可以不传这个参数，默认就带了（仅安卓下有效，false即不关闭付款后的页面，由于机制问题，安卓下如果设为true，会退出整个APP，但并非闪退，而是百川帮我们退出了app）

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "0",                     //正确码
    message:"success",            //描述
    orderid:"102391838774"     //订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "90001",                     //错误码
    message:"Parameter is null"       //错误描述
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    itemid : "522997347023",
    mmpid:"mm_00000000_0_0",
    isvcode:"app",
    opentype:"html5",
    adzoneid: '0',
    tkkey: '0',
    winObj: 'mAliBaiChuan',
    fixedOn: api.frameName,
    fixed: false,
    rect: {
    	x:0,
    	y:0,
    	w:api.frameWidth,
    	h:200
    }
};
alibaichuan.addCartPageWeb(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a13"></div>

# **shopPageWeb**

打开店铺

shopPageWeb({params},callback(ret, err))

## params

shopid:

- 类型：字符串
- 描述：店铺ID，如 https://shop137312735.taobao.com/index.htm 中的shopid为137312735

mmpid:

- 类型：字符串
- 描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

isvcode:

- 类型：字符串
- 描述：开发者自己传入，可以在订单中跟踪此参数

opentype:

- 类型：字符串
- 描述：选择打开店铺页面的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开店铺

adzoneid:

- 类型：字符串
- 描述：阿里妈妈推广位ID，三段式PID最后一段

tkkey:

- 类型：字符串
- 描述：阿里妈妈后台，推广渠道ID

winObj:

- 类型：字符串
- 描述：(可选项) 注入到h5页面的全局window属性对象名称，与addJsToPage配合使用。

rect：

- 类型：JSON 对象
- 默认值：充满整个父页面
- 描述：（可选项）frame 的位置和大小。
- 内部字段：

```js
{
    x:0,             //左上角x坐标
    y:0,             //左上角y坐标
    w:320,           //宽度
    h:480            //高度
}
```

fixedOn：

- 类型：字符串类型
- 描述：（可选项）模块视图添加到指定 frame 的名字（只指 frame，传 window 无效）
- 默认：模块依附于当前 window


fixed:

- 类型：布尔
- 默认值：true
- 描述：是否将模块视图固定到窗口上，不跟随窗口上下滚动，可为空


pageClose:

- 类型：布尔
- 默认值：false
- 描述：购买完成后，是否关闭页面，可以不传这个参数，默认就带了（仅安卓下有效，false即不关闭付款后的页面，由于机制问题，安卓下如果设为true，会退出整个APP，但并非闪退，而是百川帮我们退出了app）

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "0",             //正确码
    message:"success",    //描述
    orderid:"102391838774"//订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "90001",                     //错误码
    message:"Parameter is null"       //错误描述
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    shopid : "137312735",
    mmpid:"mm_00000000_0_0",
    isvcode:"app",
    opentype:"html5",
    adzoneid: '0',
    tkkey: '0',
    winObj: 'mAliBaiChuan',
    fixedOn: api.frameName,
    fixed: false,
    rect: {
    	x:0,
    	y:0,
    	w:api.frameWidth,
    	h:200
    }
};
alibaichuan.shopPageWeb(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a14"></div>

# **myOrdersPageWeb**

我的订单页

myOrdersPageWeb({params},callback(ret, err))

## params

orderStatus:

- 类型：字符串
- 描述：0: *为全部订单* | 1: *为待付款订单* | 2: *为待发货订单* | 3: *为待收货订单* | 4: *为待评价订单*

allOrder:

- 类型：字符串
- 描述：YES: 显示全部订单，NO : 显示ISV自己创建的订单

mmpid:

- 类型：字符串
- 描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

opentype:

- 类型：字符串
- 描述：选择打开item的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开店铺

isvcode:

- 类型：字符串
- 描述：开发者自己传入，可以在订单中跟踪此参数

adzoneid:

- 类型：字符串
- 描述：阿里妈妈推广位ID，三段式PID最后一段

tkkey:

- 类型：字符串
- 描述：阿里妈妈后台，推广渠道ID

winObj:

- 类型：字符串
- 描述：(可选项) 注入到h5页面的全局window属性对象名称，与addJsToPage配合使用。

rect：

- 类型：JSON 对象
- 默认值：充满整个父页面
- 描述：（可选项）frame 的位置和大小。
- 内部字段：

```js
{
    x:0,             //左上角x坐标
    y:0,             //左上角y坐标
    w:320,           //宽度
    h:480            //高度
}
```

fixedOn：

- 类型：字符串类型
- 描述：（可选项）模块视图添加到指定 frame 的名字（只指 frame，传 window 无效）
- 默认：模块依附于当前 window


fixed:

- 类型：布尔
- 默认值：true
- 描述：是否将模块视图固定到窗口上，不跟随窗口上下滚动，可为空


pageClose:

- 类型：布尔
- 默认值：false
- 描述：购买完成后，是否关闭页面，可以不传这个参数，默认就带了（仅安卓下有效，false即不关闭付款后的页面，由于机制问题，安卓下如果设为true，会退出整个APP，但并非闪退，而是百川帮我们退出了app）

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "0",                     //正确码
    message:"success",            //描述
    orderid:"102391838774"        //订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "90001",                     //错误码
    message:"Parameter is null"       //错误描述
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    orderStatus:"0"
    allOrder:"YES",
    mmpid:"mm_00000000_0_0",
    isvcode:"app",
    opentype:"html5",
    adzoneid: '0',
    tkkey: '0',
    winObj: 'mAliBaiChuan',
    fixedOn: api.frameName,
    fixed: false,
    rect: {
    	x:0,
    	y:0,
    	w:api.frameWidth,
    	h:200
    }
};
alibaichuan.myOrdersPageWeb(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a15"></div>

# **myCartsPageWeb**

购物车列表页

myCartsPageWeb({params},callback(ret, err))

## params

mmpid:

- 类型：字符串
- 描述：阿里妈妈的pid，也就是淘宝客ID，eg:mm_00000000_0_0

opentype:

- 类型：字符串
- 描述：选择打开item的方式，可传html5与native，分别对应以taobaoH5打开与跳转淘宝app打开购物车列表页

isvcode:

- 类型：字符串
- 描述：开发者自己传入，可以在订单中跟踪此参数

adzoneid:

- 类型：字符串
- 描述：阿里妈妈推广位ID，三段式PID最后一段

tkkey:

- 类型：字符串
- 描述：阿里妈妈后台，推广渠道ID

winObj:

- 类型：字符串
- 描述：(可选项) 注入到h5页面的全局window属性对象名称，与addJsToPage配合使用。

rect：

- 类型：JSON 对象
- 默认值：充满整个父页面
- 描述：（可选项）frame 的位置和大小。
- 内部字段：

```js
{
    x:0,             //左上角x坐标
    y:0,             //左上角y坐标
    w:320,           //宽度
    h:480            //高度
}
```

fixedOn：

- 类型：字符串类型
- 描述：（可选项）模块视图添加到指定 frame 的名字（只指 frame，传 window 无效）
- 默认：模块依附于当前 window


fixed:

- 类型：布尔
- 默认值：true
- 描述：是否将模块视图固定到窗口上，不跟随窗口上下滚动，可为空


pageClose:

- 类型：布尔
- 默认值：false
- 描述：购买完成后，是否关闭页面，可以不传这个参数，默认就带了（仅安卓下有效，false即不关闭付款后的页面，由于机制问题，安卓下如果设为true，会退出整个APP，但并非闪退，而是百川帮我们退出了app）

## callback(ret, err)

ret：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "0",                    //正确码
    message:"success",           //描述
    orderid:"102391838774"       //订单ID，可以在APP内完成跟单。注意：此返回的订单ID，只能在opentype为html5时才会返回，native或者在手淘APP内付款，都无法返回订单号
}
```

err：

- 类型：JSON对象
- 内部字段：

```js
{
    code : "90001",                     //错误码
    message:"Parameter is null"       //错误描述
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    mmpid : "mm_00000000_0_0",
    isvcode : "app",
    opentype:"html5",
    adzoneid: '0',
    tkkey: '0',
    winObj: 'mAliBaiChuan',
    fixedOn: api.frameName,
    fixed: false,
    rect: {
    	x:0,
    	y:0,
    	w:api.frameWidth,
    	h:200
    }
};
alibaichuan.myCartsPageWeb(param, function(ret, err) {
    if (ret) {
        alert("ret - " + JSON.stringify(ret));
    } else {
        alert("err - " + JSON.stringify(err));
    }
});
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a16"></div>

# **setBlockUrl**

设置要拦截的url。(用来屏蔽页面自动唤醒手淘app)

setBlockUrl({params},callback(ret))

## params

url:

- 类型：字符串
- 默认：无
- 描述：要拦截的url （若不传/为空 则清除已有拦截）

## callback(ret)

ret：

- 类型：JSON对象
- 描述：购买成功后返回
- 内部字段：

```js
{
    set: true                      //布尔值，操作状态
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    url: 'tbopen://'
};
alibaichuan.setBlockUrl(param)
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a17"></div>

# **removeWeb**

从视图中移除webview打开的百川页面。

removeWeb()

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
alibaichuan.removeWeb();
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a18"></div>

# **addPageDidListener**

监听页面加载完成后返回页面的title和url。

addPageDidListener(callback(ret))

## callback(ret)

ret：

- 类型：JSON对象
- 描述：页面加载后返回
- 内部字段：

```js
{
    added: true,                      //布尔值，操作状态
    title: "百度一下",                 //返回当前页面的标题
    url: "https://www.baidu.com"      //返回当前页面的Url
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
alibaichuan.addPageDidListener(function(ret){
    if (ret.title) {
        alert(JSON.stringify(ret));
    }
})
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a19"></div>

# **addLoadingListener**

监听页面加载中返回页面的title和url。

addLoadingListener(callback(ret))

## callback(ret)

ret：

- 类型：JSON对象
- 描述：页面中返回
- 内部字段：

```js
{
    added: true,                      //布尔值，操作状态
    title: "百度一下",                 //返回当前页面的标题
    url: "https://www.baidu.com"      //返回当前页面的Url
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
alibaichuan.addLoadingListener(function(ret){
    if (ret.title) {
        alert(JSON.stringify(ret));
    }
})
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a20"></div>

# **addJsToPage**

在当前打开的淘宝页面加载完成后注入一段js脚本到H5页面。

addJsToPage({params}, callback(ret))

## params

script:

- 类型：字符串
- 默认：无
- 描述：JavaScript脚本
- 注意：必须以"javascript:{js具体内容};"的格式组织
 - 其中javascript:{};不能有空格，还有需要带上最后的分号，切记
 - 如果需要接收webview的返回值，必须是调用window["你再创建webview的winObj值"].jsCallBack(JSON对象)，详见下面示例

## callback(ret)

ret：

- 类型：JSON对象
- 描述：执行后的返回
- 内部字段：

```js
{
    added: true,             //布尔值，操作状态
    status: true,            //是否返回数据
    callback: ""             //返回数据的JSON字符串，取数据需要JSON.parse(ret.callback)
}
```

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
var param = {
    script:'javascript:{'
          +'var bodyHTML = document.querySelectorAll("body")[0].innerHTML;'
          +'var title = document.title;'
+'window["mAliBaiChuan"].jsCallBack({"title": title,"body": bodyHTML});'   
          +'};',
};
alibaichuan.addJsToPage(param,function(ret){
    if(ret && ret.added && ret.status){
        alert(JSON.parse(ret.callback))
    }
})
```


## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a21"></div>

# **removeJsListener**

移除webview页面上的监听事件或js

removeJsListener({params})

## params

name:

- 类型：字符串
- 默认：'' (默认为 同时移除js脚本、PageFinListener和loadingListener)
- 描述：(可选项) 移除的类型
- 取值范围：
 - pageFinishedListener //移除PageFinListener
 - loadingListener' //移除loadingListener
 - javaScript' //移除javaScript脚本

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a22"></div>

# **webGoBack**

控制外部webview的后退

webGoBack(callback(ret))

## callback(ret)

ret：

- 类型：JSON对象
- 描述：当webview不能回退时返回
- 内部字段：

```js
{
    status: true,   //布尔型；true||false
    message: '第一个页面了'
}
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a23"></div>

# **webGoForward**

控制外部webview的前进

webGoForward(callback(ret))

## callback(ret)

ret：

- 类型：JSON对象
- 描述：当webview不能前进时返回
- 内部字段：

```js
{
    status: true,   //布尔型；true||false
    message: '最后一个页面了'
}
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a24"></div>

# **webRefresh**

控制外部webview的刷新

webRefresh()

## 示例代码

```js
var alibaichuan = api.require('mAliBaiChuan');
alibaichuan.webRefresh();
```

## 可用性

iOS系统，Android系统

可提供的1.0.0及更高版本

<div id="a25"></div>

# **关于鹊桥跟单**

鹊桥的商品，基本一律走通用（鹊桥即将下线）

<div id="a26"></div>

# **关于高佣**

1. url打开方式打开商品，这个url必须是纯商品链接才能自动跟到订单（也就是商品裸链接，如https://detail.tmall.com/item.htm?id=560825350079）
2. 关于转链问题：目前，SDK的高佣转链功能需要满足两个条件 1）唤醒手淘  2）使用商品裸链接或者宝贝ID（暂时不能传入二合一页面的链接或其他已经转好的链接

<div id="a27"></div>

# **关于adzone与appkey**

只要填写阿里妈妈pid就能跟到订单，不管adzoneid与tkkey，后两个只是影响是否高佣

<div id="a28"></div>

# **接口快速记忆法**

xxxWeb的接口参数与回调基本是和不带web的接口是一致的，唯一不同的是xxxWeb的接口参数多了winObj、rect、fixedOn、fixed、pageClose(安卓下有效，默认为false，即付完款不关闭页面)四个参数

另外webview操作下面的所有接口都是针对xxxWeb的
