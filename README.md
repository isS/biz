#商用码模板开发

## 目录
*	[开发语言](#开发语言)
*	[模板目录](#模板目录)
*	[配置文件](#配置文件)
*	[商用码数据](#商用码数据)
*	[模块解析代码](#模块解析代码)
	*	[视频模块](#视频模块)
*	[默认脚本说明](#默认脚本说明)
*	[补充说明](#补充说明)

##	[开发语言](id:开发语言)

### 使用JS模板引擎 ***artTemplate*** 进行模板开发.


1. 语法标签: 开始```{` `}```

2. 变量输出

	* json数据:

	```
	{'name':"商用码标题"}
	```

	* 方法:

	```
	{`name`}
	```

	* 结果:

	```
	商用码
	```



3. 编写模板
   使用```<public id="module_title"></public>```模板标签存放模板：
   当调用public标签模板时,必须添加***public-***
    
	*    数据
	
	```
	{
	"tree_list":[                                                                      
	{
	"module":"rich_text",                                                                   
	"soncode_link":"//biz.cli.im/site/m/FJ3548",        
	"item":{                                            
	"title":"网上含APP订餐满就送",                      
	"content":"<p> 肯德基宅急送实行专属菜单及价格。为保证食物品质，肯德基宅急送有送餐范围和服务时间限制。不同城市、不同送餐范围的菜单有所不同。 </p>"
	}
	},
	{
	"module":"clsdir",
	"soncode_link":"//biz.cli.im/site/m/VW3549",
	"item":{
	"title":"分类",
	"content":"<p> <span>kfc肯德基</span> </p>"
	},
	"url":"http://biz.cli.im/site/k/3549"
	}}
	``` 

	* 方法:
	
	```
	<public id="module_title">				
       {`each tree_list as module`}
         <div class="module_header">
          <h2>module: {`module.module`}</h2>
            <div>title:{`module.item.title`}</div>
          <div>content:{`#module.item.content`}</div>
       </div>
       {`/each`}
     </public>
     ```
     
         
	*  结果:

	 ```	
	 <div class="module_header">
          <h2>module: rich_text</h2>
          <div>title:网上含APP订餐满就送</div>
          <div>content:<p> 肯德基宅急送实行专属菜单及价格。为保证食物品质，肯德基宅急送有送餐范围和服务时间限制。不同城市、不同送餐范围的菜单有所不同。 </p></div>
         </div>
         <div class="module_header">
         <h2>module: clsdir</h2>
         <div>title:分类</div>
         <div>content:<p> <span>kfc肯德基</span> </p></div>
     </div>
     ```


         
4. 引入文件模块模板

	```
    {`include 'module-rich_text' data `}
	```

	data 为传递的数据, 为空不传数据. 
	
	
5. 输出html编码

	* 数据:

	```
	{'html_content':'<i>HTML标签斜体</i>'}
	```
	
	* 方法:	(变量名前加 **#** 号.)

	```
	{`#html_content`}							
	```
	
	* 结果:
	
	
	<i>HTML标签斜体</i>
	
	
6. 条件语法
	
	* 数据:
	
	```
	{'data':[{'item':{'content':"商用码图文内容"}]}
	```
	* 方法1:
	
	```
    {`if $data.item.content`}
        <div class="list_des">{`#$data.item.content`}</div>
    {`/if`}
    ```
    
    * 方法2:
    
     ```
     {`if $data.item.play_type == 'youku'`}
          <a>youku</a>
     {`else`}
          <a>alpha</a>
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
*	/skin/										存放配色方案样式文件
	* /red.css								配色样式文件 文件命名跟配置文件 config.json 中的 skin参数值 键名作为
	* /yellow.css								



## [main.html模板写入文件](id:main.html)
模板代码写在此文件中.


## [配置文件](id:配置文件)

 json数据格式的配置文件.


```
{
	"version" : "1.0.1",  //模板版本, 每次更新样式,脚本和图片需要更新版本号来刷新资源.
	"name" : "线型",  //模板中文名用于显示和辨识用
	"descr" : "该模板支持所有模块",  //模板描述,用于选择模板时用.
	"code" : "flow",  //模板目录命名,唯一标识请尽量定义成跟模板名有联系.
	"module" : "rich_text,clsdir,file,audio,video,intera,links,contact,vcard,sms,fav,afatra,weixin",  //模板所支持的模块,配置目录必须要有对应模块解析代码
	"skin" : {  //配色文件名, 唯一标识
		"yellow" : {
			"name":"黄色",  //配色名用于模板选择显示,描述于实际颜色接近.
			"color":"#FF0",  //配色显示值用, 16位色或RGB均可.
			"thumb":"images/thumb/yellow.jpg"  //模板配色预览图
		},
		"green" : {
			"name":"绿色",
			"color":"#F00",
			"thumb":"images/thumb/green.jpg"
		},
		"red" : {
			"name":"红色",
			"color":"#00F",
			"thumb":"images/thumb/red.jpg"
		}
	},
	"plugin" : [  //第三方扩展脚本,资源用绝对路径
		"http://res.wx.qq.com/mmbizwap/zh_CN/htmledition/js/jquery-1.8.3.min176ed4.js",
		"http://biz.cli.im/Public/js/adaptVideoPlay.js",
		"http://biz.cli.im/Public/js/jquery.touchSwipe.min.js"
	]
}

```


## [商用码数据](id:商用码数据)

```
{
    "coding":"IS1868",  /*商用码ID*/
    "qrcode_img":"http://o-clibiz-img.b0.upaiyun.com/qrcode/2013/11/20/528ca467d3444.png",  /*二维码图片*/
    "name":"格力—掌握核心科技",  /*商用码名称*/
    "descr":"成立于1991年的珠海格力电器股份有限公司是目前全球最大的集研发、生产、销售、服务于一体的国有控股专业化空调企业，2012年实现营业总收入1001.10亿元，纳税超过74亿元，连续12年上榜美国《财富》杂志'中国上市公司100强'。",  /*商用码描述*/
    "logo_path":"http://o-clibiz-img.b0.upaiyun.com/ulogo/2014/01/20/52dccb49aa1ab.jpg",  /*商用码logo*/
    "is_addrbook":"1",  /*是否能保存名片:1.可以;0.不可以;*/
    "coope_site_id":"0",  /*是否合作商的商用码*/
    "is_valid":true,  /*是否有效,false 表示:过期 未付款 未开通*/
    "contacts":{  /*商用码基本联系信息[接下来版本会修改]*/
        "phone":[  /*模板目录联系信息*/
        {
            "name":"咨询电话",  /*标题*/
            "type":"tel",  /*类型(tel:固话,email:邮箱,mobile:手机,qq:QQ,sinaweibo:新浪微博,tweibo:腾讯微博;web:网址,)*/
            "link":"tel:0756-8614883",  /*链接值,href=""中的值使用*/
            "number":"0756-8614883"  /*内容,根据需求和标题一起输出.*/
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
                "name":"新浪微博",
                "type":"sinaweibo",
                "link":"http://weibo.com/gree1991",
                "value":"http://weibo.com/gree1991"
            },
            {
                "name":"格力官网",
                "type":"web",
                "link":"http://www.gree.com.cn/",
                "value":"http://www.gree.com.cn/"
            },
            {
                "name":"我我我我我我我我我",
                "type":"web",
                "link":"http://点点滴滴",
                "value":"http://点点滴滴"
            },
            {
                "name":"腾讯微博",
                "type":"tweibo",
                "link":"http://t.qq.com/gree",
                "value":"http://t.qq.com/gree"
            }
        ],
            "baidumap":{  /*联系信息 百度地图信息*/
                "link":"/map/?id=IS1868&lng=113.503079&lat=22.240736",  /*地图链接*/
                "img_link":"http://api.map.baidu.com/staticimage?center=113.503079,22.240736&width=500&height=400&zoom=14&markers=113.503079,22.240736",  /*地图图片地址*/
                "app_link":"baidumap://map/marker?location=22.240736,113.503079&title=格力—掌握核心科技&content=成立于1991年的珠海格力电器股份有限公司是目前全球最大的集研发、生产、销售、服务于一体的国有控股专业化空调企业，2012年实现营业总收入1001.10亿元，纳税超过74亿元，连续12年上榜美国《财富》杂志'中国上市公司100强'。&src=微信|微信"  /*应用链接*/
            }
    },
    "contact_link":"http://biz.cli.me/home/vcard/down?id=IS1868", /*名片下载链接*/
    "agent_info":{"copyright","xxx事务所提供技术支持<br>技术支持热线：0536-0000000"},
    "tree_list":[
    {
        "coding":"TZ3547",
        "module":"rich_text",  //图文模块
        "unfold":"0",  //折叠
        "index":2,  //索引
        "soncode_link":"//biz.cli.me/site/m/TZ3547",  //子码访问链接
        "item":{
            "title":"网上含APP订餐满就送",  //模块标题
            "content":"<p style="text-align:center;"> <br /> </p> <p> <span style="line-height:1.5;"><a href='/unit/img?img=http://img.clewm.net/editor/2014/06/03/538d57bb36ffb.jpg'><img alt='' src='http://img.clewm.net/editor/2014/06/03/538d57bb36ffb.jpg' style='width: 100%;'></a>　</span> </p> <p> <span style="line-height:1.5;"><a href='/unit/img?img=http://img.clewm.net/editor/2014/06/03/538d57cb0a903.jpg'><img alt='' src='http://img.clewm.net/editor/2014/06/03/538d57cb0a903.jpg' style='width: 100%;'></a>　<br /> </span> </p> <p> <span style="line-height:1.5;"><a href='/unit/img?img=http://img.clewm.net/editor/2014/06/03/538d57dbe8185.jpg'><img alt='' src='http://img.clewm.net/editor/2014/06/03/538d57dbe8185.jpg' style='width: 100%;'></a></span> </p>",
            "imgPath":"http://o-clibiz-img.b0.upaiyun.com/richTextCover/2014/01/20/52dcbdfdc65b2.jpg",  //图文模块的图片
            "imgPath_view_link":"/unit/img?img=http://o-clibiz-img.b0.upaiyun.com/richTextCover/2014/01/20/52dcbdfdc65b2.jpg"  //查看图文模块图片大图的链接地址
        },
        "real_module":"cite" //本身是引用模块
    },
    {
        "coding":"VW3549",  //模块coding
        "module":"clsdir",  //分类模块
        "unfold":"0",  //折叠
        "index":3,  //索引
        "soncode_link":"//biz.cli.me/site/m/VW3549",
        "item":{
            "title":"分类",  //模块名
            "content":"<p> <span>kfc肯德基</span> </p>",  //模块内容描述
            "imgPath":"http://o-clibiz-img.b0.upaiyun.com/richTextCover/2013/12/22/52b704304fd9b.jpg",  //分类模块图片
            "imgPath_view_link":"/unit/img?img=http://o-clibiz-img.b0.upaiyun.com/richTextCover/2013/12/22/52b704304fd9b.jpg"  //分类模块图片查看链接
        },
        "url":"http://biz.cli.me/site/k/3549"  //分类访问地址
    },
    {
        "coding":"QY8360",
        "module":"video",  //视频模块
        "unfold":"1",      //展开
        "index":4,  //索引
        "soncode_link":"//biz.cli.me/site/m/QY8360",  //子码访问链接
        "item":{  //视频模块数据
            "title":"离型膜应用",  //视频标题
            "play_vid":"XNTYyOTczODQ4",  //播放id
            "play_image":null,  //视频缩略图
            "play_state":"2",  //视频状态,未来云会对上传的视频进行处理,有以下状态:
            "play_type":"youku"  //视频类型, youku:优酷, asdtv:未来云视频.
        }
    },
    {
        "coding":"AH7494",
        "module":"audio",  //音频模块
        "unfold":"1",  //展开
        "index":5,  //索引
        "soncode_link":"//biz.cli.me/site/m/AH7494",  //子码访问链接
        "item":{
            "title":"肯德基生日歌",  //音频标题
            "play_url":"http://audio.clewm.net/2014/04/30/b9384dc1e176419b8dda5aacd843ceb8.mp3"  //音频播放链接
        }
    },
    {
        "coding":"EG6368",
        "module":"contact",  //联系信息模块
        "unfold":"0", //折叠
        "index":7,  //索引
        "soncode_link":"//biz.cli.me/site/m/EG6368",  //子码访问链接
        "item":{
            "title":"联系信息",   //联系模块标题
            "descr":"各种联系方式！",  //联系模块描述
            "phone":[  //联系数据
            {
                "name":"电话",  //联系信息名
                "type":"tel",  //联系信息类型 tel:固定电话
                "number":"12341234",  //联系信息值
                "link":"tel:12341234"  //联系信息链接值
            },
            {
                "name":"邮箱",  //联系信息名
                "type":"email",  //联系信息类型 email:邮箱
                "number":"12341234@com.com",  //联系信息值
                "link":"mailto:12341234@com.com"  //联系信息链接
            },
            {
                "name":"网址",  //联系信息名
                "type":"web",  //联系信息类型 web:网址
                "number":"http://cli.im",  //联系信息值
                "link":"javascript:;"  //联系信息链接
            },
            {
                "name":"qq",  //联系信息名
                "type":"qq",  //联系信息类型 qq:QQ
                "number":"32227764",  //联系信息值
                "link":"javascript:;"  //联系信息链接
            },
            {
                "name":"手机",  //联系信息名
                "type":"mobile",  //联系信息类型 mobile:手机
                "number":"13105577007",  //联系信息值
                "link":"tel:13105577007"  //联系信息链接
            }
            ]
        }
    },
    {
        "coding":"MQ6638",
        "module":"video",
        "unfold":"0",
        "index":8,
        "soncode_link":"//biz.cli.me/site/m/MQ6638",
        "item":{
            "title":"婚庆视频",  
            "play_vid":"e5ebb9bb15736c56dc63a1bf4d6c8d37_e",
            "play_image":"http://static.asdtv.com/uimage/e/e5ebb9bb15/7/e5ebb9bb15736c56dc63a1bf4d6c8d37_0.jpg",
            "play_state":"2",  //视频状态码
            "play_type":"asdtv", .//视频模块类型,asdtv 未来云
            "play_state_desc":"审核通过" //视频状态描述
        }
    },
    {
        "coding":"JZ6681",
        "module":"intera",  //互动模块
        "unfold":"0",
        "index":9,
        "soncode_link":"//biz.cli.me/site/m/JZ6681",
        "item":{
            "title":"互动",  //互动模块标题
            "descr":"互动描述很长很长很长很长很长很长很长很长很长很长",  //互动模块描述
            "link":"http://in.cli.im/dataform.aspx?module_id=374"  //互动链接
        }
    },
    {
        "coding":"LS6906",
        "module":"links",  //链接模块
        "unfold":"0",  //折叠
        "index":10,  //索引
        "soncode_link":"//biz.cli.me/site/m/LS6906",  //子码访问链接
        "item":{
            "title":"促销商品",  //链接模块标题
            "descr":"本期购物促销产品购物链接：",  //链接模块描述
            "link":{
                {
                "name":"义茂年糕", //链接标题
                "link":"http://item.taobao.com/item.htm?spm=0.0.0.0.EzL3ad&id=16425669267"  //链接值
                },
                {
                "name":"立丰香肠",
                "link":"http://item.taobao.com/item.htm?spm=0.0.0.0.EzL3ad&id=8930856778"
                },
                {
                "name":"52度五粮液",
                "link":"http://item.taobao.com/item.htm?spm=0.0.0.0.EzL3ad&id=16189817541"
                }
            },
            "is_weixin":"1"
        }
    },
    {
        "coding":"UZ25148",
        "module":"vcard",  //名片模块
        "unfold":"1",  //展开
        "index":15,  //索引
        "soncode_link":"//biz.cli.me/site/m/UZ25148",
        "item":{
            "title":"^_^",  //名片模块标题
            "face":"http://o-clibiz-img.b0.upaiyun.com/vcardface/2014/04/30/783f60d130cefcf251a687e5f13bbd43.jpg",   //名片头像图片链接
            "name":"邵坚一",  //名片人名
            "position":"职员",  //名片职位
            "mobiletel":"13105577007",  //名片手机号码
            "v_url":"http://v.2w.ma/AacyU?b=1868&t=^_^&h=ac1cfad17d22fa68a56eb96fa7c77b44"  //名片访问链接
        }
    }
    ]
}


```

## [模块解析代码](id:模块解析代码)
1. [视频模块](id:视频模块)
***JS扩展配置种加载视频解析脚本*** [http://biz.cli.im/Public/js/adaptVideoPlay.js](http://biz.cli.im/Public/js/adaptVideoPlay.js)

          {`include 'module_title' $data`}			引用模板头文件
          {`if $data.item.play_type == 'asdtv'`}   判断视频类型,play_type:asdtv youku 
             {`if $data.item.play_state != '2' `}  未来云视频处理状态码,1为处理完成码.
                <div class="tree_box_content">
                    <div class="list_des video_tips">{$vo.block.play_state_desc}</div>
                </div>
             {`/if`}
          <a href="#" class="video_moudle" data-uid="{`$data.item.play_vid`}" data-width="100%" data-height="100%"> //这段原样调用即可,除了data-uid属性根据实际数据填写.其它属性不作修改.
              <div class="video_view" >
                 <img src="{`$data.item.play_image`}" />  视频预览图片
                 <div class="video_play_btn"></div>       视频带解析标签.使用时不做修改
              </div>
          </a>
          {`/if`}
          {`if $data.item.play_type == 'youku'`}          优酷视频解析标签
          <a href="#" class="video_moudle" data-uid="{`$data.item.play_vid`}" data-use-youku="ture" data-width="100%" data-height="100%"></a>           //这段原样调用即可,除了data-uid属性根据实际数据填写.其它属性不作修改.

          {`/if`}
          


## [默认脚本说明](id:默认脚本说明)

默认支持jQuery.
main.html 只能写脚本事件,无法执行脚本.



## [补充说明](id:补充说明)
2014-08-22 数据中返回代理商版权信息, agent_info 里面的 coypright. 
