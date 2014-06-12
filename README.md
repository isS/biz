#商用码模板开发

## 目录
*	[开发语言](#开发语言)
*	[模板目录](#模板目录)
*	[配置文件](#配置文件)
*	[商用码数据](#商用码数据)
*	[模块解析代码](#模块解析代码)
**	[视频模块](#视频模块)
*	[默认脚本说明](#默认脚本说明)

##	[开发语言](id:开发语言)

### 使用JS模板引擎 ***artTemplate*** 进行模板开发.


1. 语法标签: 开始```{` `}```

2. 编写模板
   使用```<public id="module_title"></public>```模板标签存放模板：

         <public id="module_title">				
         {`each $data as mheader`}                //这里的tree_list 为全局变量.
         <div class="module_header">
            <h2>{`mheader.title`}</h2>
            <div>{`mheader.desc`}</div>
         </div>
         {`/each`}
         </public>
       
  调用方法: ```{`include 'module_title'`}``` 当调用public标签模板时,必须添加***public-***
         
3. 变量输出
``
{`name`}
``

4. 引入子模板
	{`include 'module_title' $data`}		$data 为传递的数据, 为空不传数据. 当调用public标签模板时,必须添加***public-***
	
5. 输出html编码
	{`#html_content`}							变量名前加 ***#*** 号.
	
6. 条件语法

	 ```
     {`if $data.item.content`}
         <div class="list_des">{`#$data.item.content`}</div>
     {`/if`}
     ```
     
     ```
     {`if $data.item.play_type == 'youku'`}
          <a href="#" class="test" data-uid="{`$data.item.play_vid`}" data-use-youku="ture" data-width="100%" data-height="100%"></a>
     {`/if`}
     ```

## [模板目录](id:模板目录)


商用码模板目录下的/Mobile/main/***demo*** demo目录即模板的存放目录,里面包含:

*	[config.json](#配置文件)						模板所使用的配置文件
*	/images										样式文件中所需要调用的图片存放目录
*	[main.html](#main.html)				模板入口文件
*	module-audio.html							音频模块代码
*	module-clsdir.html							分类模块代码
*	module-contact.html							联系人模块代码
*	module-file.html								文件模块代码
*	module-intera.html							音频模块代码
*	module-links.html							链接模块代码
*	module-rich_text.html							富文本模块代码
*	module-vcard.html							名片模块代码
*	module-video.html							音频模块代码
*	module-weixin.html							加微信模块代码
*	module-sms.html								短信信模块代码
*	module-fav.html								收藏模块代码
*	module-afatra.html							访问模块代码
*	reso-javascript.js							脚本代码都写这里自动调用
*	reso-style.css								样式代码都写这里自动调用
*	/skin										存放配色方案样式文件
*	/skin/red.css								配色样式文件 文件命名跟配置文件 config.json 中的 skin参数值 键名作为
*	/skin/yellow.css								



## [main.html模板写入文件](id:main.html)
模板代码写在此文件中.


## [配置文件](id:配置文件)

```javascript
{
	"version" : "1.0.4"							//模板版本, 每次更新样式,脚本和图片需要更新版本号来刷新资源.
	"name" : "九宫格",							//模板中文名用于显示和辨识用.
	"code" : "grid",								//模板目录命名,唯一标识请尽量定义成跟模板名有联系.
	"module" : "rich_text,clsdir,file,audio,video,intera,links,contact,vcard",    //模板所支持的模块
	"skin" : {									//模板可选择配色
		"yellow" : {								//配色文件名, 唯一标识
			"name":"黄色",						//配色名用于模板选择显示,描述于实际颜色接近.
			"color":"#FF0"						//配色显示值用, 16位色或RGB均可.
		},
		"green" : {
			"name":"绿色",
			"color":"#F00"
		},
		"red" : {
			"name":"红色",
			"color":"#00F"
		}
	},
	"plugin" : [									//第三方扩展脚本
		"http://res.wx.qq.com/mmbizwap/zh_CN/htmledition/js/jquery-1.8.3.min176ed4.js",//资源用绝对路径
		"http://cache.clewm.net/p/video.js",
		"http://biz.cli.me/Public/js/jquery.touchSwipe.min.js"
	]
}
```


## [商用码数据](id:商用码数据)

```javascript
{
"coding":"IS1868",								                         商用码ID
"qrcode_img":"http://img.clewm.net/qrcode/2013/11/20/528ca467d3444.png", 二维码图片
"name":"格力—掌握核心科技",						                          商用码名称
"descr":"",										                         商用码描述
"logo_path":"http://img.clewm.net/ulogo/2014/01/20/52dccb49aa1ab.jpg",   商用码logo
"is_addrbook":"1",								                         是否能保存名片:1.可以;0.不可以;
"coope_site_id":"0",							                         是否合作商的商用码
"is_valid":true,                                                         是否有效,false 表示:过期 未付款 未开通
"contacts":{										                     商用码基本联系信息[接下来版本会修改]
"phone":[										                         模板目录联系信息
{
"name":"咨询电话",							                 标题
"type":"tel",                                                   类型(tel,email,mobile,qq,sina,web,)
"link":"tel:0756-8614883",			                          链接值,href=""中的值使用
"number":"0756-8614883"                                         内容,根据需求和标题一起输出.
},
{
"name":"邮箱",
"type":"email",
"link":"mailto:sale@cn.gree.com",
"number":"sale@cn.gree.com"
},
{
"name":"电话",
"type":"mobile",
"link":"tel:13105577007",
"number":"13105577007"
}
],
"addr":"珠海市前山金鸡西路格力电器股份有限公司",
"link":[
{
"name":"qq",
"type":"qq",
"link":"http://123412341234.qq.com",
"value":"http://123412341234.qq.com"
},
{
"name":"微博",
"type":"sina",
"link":"http://weibo.com/gree1991",
"value":"http://weibo.com/gree1991"
},
{
"name":"格力官网",
"type":"web",
"link":"http://www.gree.com.cn/",
"value":"http://www.gree.com.cn/"
}
],
"baidumap":{										联系信息 百度地图信息
"link":"/map/?id=IS1868&lng=113.503079&lat=22.240736", 地图链接
"img_link":"http://api.map.baidu.com/staticimage?center=113.503079,22.240736&width=500&height=400&zoom=14&markers=113.503079,22.240736",
"app_link":"baidumap://map/marker?location=22.240736,113.503079&title=格力—掌握核心科技&content=&src=微信|微信"										地图图片地址
}
},
"contact_link":"http://biz.cli.im/home/vcard/down?id=IS1868", 名片下载地址
"tree_list":[									           模块树,一般通过循环进行遍历                         
{
"coding":"FJ3548",								模块id,
"module":"rich_text",								模块类型, 图文模块
"unfold":1,										是否折叠,1.不折叠;0.折叠
"index":1,										模块树中的排序位置. 从1开始.
"soncode_link":"//biz.cli.im/site/m/FJ3548",		该模块的子码访问地址, 9宫格等特殊性模板才使用. 默认不使用该地址.
"item":{											模块内容
"title":"网上含APP订餐满就送",						标题
"content":"<p> 肯德基宅急送实行专属菜单及价格。为保证食物品质，肯德基宅急送有送餐范围和服务时间限制。不同城市、不同送餐范围的菜单有所不同。 </p> <p> <br /> </p>",内容
"imgPath":"http://img.clewm.net/richTextCover/2014/01/20/52dcbdfdc65b2.jpg",模块图片
"imgPath_view_link":"/unit/img?img=http://img.clewm.net/richTextCover/2014/01/20/52dcbdfdc65b2.jpg" 模块图片原图查看地址.
}
},
{
"coding":"VW3549",
"module":"clsdir",
"unfold":1,
"index":2,
"soncode_link":"//biz.cli.im/site/m/VW3549",
"item":{
"title":"分类",
"content":"<p> <span>kfc肯德基</span> </p>",
"imgPath":"http://img.clewm.net/richTextCover/2013/12/22/52b704304fd9b.jpg",
"imgPath_view_link":"/unit/img?img=http://img.clewm.net/richTextCover/2013/12/22/52b704304fd9b.jpg"
},
"url":"http://biz.cli.im/site/k/3549"
},
{
"coding":"AH7494",
"module":"audio",
"unfold":1,
"index":3,
"soncode_link":"//biz.cli.im/site/m/AH7494",
"item":{
"title":"肯德基生日歌",
"play_url":"http://up.chshcms.com/wl/url/csdj/130533/csdj.mp3"
}
},
{
"coding":"EG6368",
"module":"contact",
"unfold":1,
"index":4,
"soncode_link":"//biz.cli.im/site/m/EG6368",
"item":{
"title":"联系信息",
"descr":"公司介绍公司介绍公司介绍公司介绍公司介绍公司介绍公司介绍公司介绍公司介绍公司介绍公司介绍公司介绍公司介绍公司介绍公司介绍公司介绍公司介绍点击联系",
"phone":[
{
"name":"电话",
"type":"tel",
"number":"12341234",
"link":"tel:12341234"
},
{
"name":"邮箱",
"type":"email",
"number":"12341234@com.com",
"link":"mailto:12341234@com.com"
},
{
"name":"网址",
"type":"web",
"number":"http://cli.im",
"link":"javascript:;"
},
{
"name":"qq",
"type":"qq",
"number":"32227764",
"link":"javascript:;"
},
{
"name":"手机",
"type":"mobile",
"number":"13105577007",
"link":"tel:13105577007"
},
{
"name":"我我我我我我哦我窝哦",
"type":"tel",
"number":"1111",
"link":"tel:1111"
}
]
}
},
{
"coding":"MQ6638",
"module":"video",
"unfold":1,
"index":5,
"soncode_link":"//biz.cli.im/site/m/MQ6638",
"item":{
"title":"婚庆视频",
"play_vid":"e5ebb9bb15736c56dc63a1bf4d6c8d37_e",
"play_image":"http://static.asdtv.com/uimage/e/e5ebb9bb15/7/e5ebb9bb15736c56dc63a1bf4d6c8d37_0.jpg",
"play_state":"2",
"play_type":"asdtv",
"play_state_desc":"审核通过"
}
},
{
"coding":"JZ6681",
"module":"intera",
"unfold":1,
"index":6,
"soncode_link":"//biz.cli.im/site/m/JZ6681",
"item":{
"title":"互动",
"descr":"互动描述很长很长很长很长很长很长很长很长很长很长",
"link":"http://in.cli.im/dataform.aspx?module_id=374"
}
},
{
"coding":"LS6906",
"module":"links",
"unfold":1,
"index":7,
"soncode_link":"//biz.cli.im/site/m/LS6906",
"item":{
"title":"促销商品",
"descr":"本期购物促销产品购物链接：",
"link":{
"义茂年糕":"http://item.taobao.com/item.htm?spm=0.0.0.0.EzL3ad&id=16425669267",
"立丰香肠":"http://item.taobao.com/item.htm?spm=0.0.0.0.EzL3ad&id=8930856778",
"52度五粮液":"http://item.taobao.com/item.htm?spm=0.0.0.0.EzL3ad&id=16189817541"
},
"is_weixin":"1"
}
},
{
"coding":"HT10742",
"module":"audio",
"unfold":1,
"index":8,
"soncode_link":"//biz.cli.im/site/m/HT10742",
"item":{
"title":"打发打发",
"play_url":""
}
},
{
"coding":"SW16517",
"module":"intera",
"unfold":1,
"index":9,
"soncode_link":"//biz.cli.im/site/m/SW16517",
"item":{
"title":"123",
"descr":"123",
"link":"http://in.cli.im/dataform.aspx?module_id=961"
}
},
{
"coding":"KZ25027",
"module":"audio",
"unfold":"1",
"index":10,
"soncode_link":"//biz.cli.im/site/m/KZ25027",
"item":{
"title":null,
"play_url":null
}
},
{
"coding":"BL25206",
"module":"rich_text",
"unfold":"1",
"index":11,
"soncode_link":"//biz.cli.im/site/m/BL25206",
"item":{
"title":null,
"content":"",
"imgPath":"",
"imgPath_view_link":"/unit/img?img="
}
},
{
"coding":"EN25251",
"module":"rich_text",
"unfold":1,
"index":12,
"soncode_link":"//biz.cli.im/site/m/EN25251",
"item":{
"title":"啊是对方",
"content":"哎是的发送",
"imgPath":"",
"imgPath_view_link":"/unit/img?img="
}
},
{
"coding":"DO35976",
"module":"vcard",
"unfold":1,
"index":13,
"soncode_link":"//biz.cli.im/site/m/DO35976",
"item":{
"title":"ohohoh",
"face":"http://img.clewm.net/vcardface/2014/05/28/f604ab3343347b398859664fa7f983a1.jpg",
"name":"邵坚一",
"position":"职员",
"mobiletel":"13105577007",
"v_url":"http://v.2w.ma/A0lqt?b=1868&t=ohohoh&h=009841b374cf19c5669512d64316a8e7"
}
},
{
"coding":"LT36402",
"module":"vcard",
"unfold":1,
"index":14,
"soncode_link":"//biz.cli.im/site/m/LT36402",
"item":{
"title":"----^_^----",
"face":"http://img.clewm.net/vcardface/2014/04/24/528c28ca21002bbd7851c46f6b613349.jpg",
"name":"tom",
"position":"总经理",
"mobiletel":"131055577007",
"v_url":"http://v.2w.ma/AhntF?b=1868&t=----^_^----&h=86d4e676ce00c21fd64c96481870ec00"
}
},
{
"coding":"AO41802",
"module":"vcard",
"unfold":1,
"index":15,
"soncode_link":"//biz.cli.im/site/m/AO41802",
"item":{
"title":"asdfasdf",
"face":null,
"name":"张三",
"position":"",
"mobiletel":"13012345678",
"v_url":"http://v.2w.ma/A3tJV?b=1868&t=asdfasdf&h=b5c67047d32f2f724dc82d002a8a9a2b"
}
}
]
}
```

## [模块解析代码](id:模块解析代码)
1. [视频模块](id:视频模块)
***JS扩展配置种加载视频解析脚本*** [http://biz.cli.im/Public/mobile/js/adaptVideoPlay.js](http://biz.cli.im/Public/mobile/js/adaptVideoPlay.js)

          {`include 'module_title' $data`}			引用模板头文件
          {`if $data.item.play_type == 'asdtv'`}   判断视频类型,play_type:asdtv youku 
             {`if $data.item.play_state != '2' `}  未来云视频处理状态码,1为处理完成码.
                <div class="tree_box_content">
                    <div class="list_des video_tips">{$vo.block.play_state_desc}</div>
                </div>
             {`/if`}
          <a href="#" class="test" data-uid="{`$data.item.play_vid`}" data-width="100%" data-height="100%">
              <div class="video_view" >
                 <img src="{`$data.item.play_image`}" />  视频预览图片
                 <div class="video_play_btn"></div>       视频带解析标签.使用时不做修改
              </div>
          </a>
          {`/if`}
          {`if $data.item.play_type == 'youku'`}          优酷视频解析标签
          <a href="#" class="test" data-uid="{`$data.item.play_vid`}" data-use-youku="ture" data-width="100%" data-height="100%"></a>
          {`/if`}
          


## [默认脚本说明](id:默认脚本说明)

默认支持jQuery.
main.html 只能写脚本时间,无法执行脚本.
