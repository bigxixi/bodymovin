 ## 2017.04.04 更新bodymovin4.6.2 zxp插件汉化版， [下载地址点我](https://raw.githubusercontent.com/bigxixi/bodymovin/master/zxp_CHS/bodymovin4.6.2cn.zxp)   <br />
 1.安装方法见正文，建议用方式1。自签名打包，如介意请使用[英文原版](https://github.com/bodymovin/bodymovin/tree/master/build/extension)。<br />
 2.自带预览失效，似乎是作者未在github更新（可能更新在adobe在线商店版？），如有更新我将跟进。请通过导出html播放的方式预览。<br />
 3.修正了原版导出带透明通道png图片资源会有黑边问题。<br />

-----

***这是bodymovin插件说明的中文版，由[BigXiXi](https://github.com/bigxixi)翻译, 原文地址：https://github.com/bodymovin/bodymovin<br>
 注意！项目中除了readme保持更新，其他文件最新版请[移步原版](https://github.com/bodymovin/bodymovin)获取。<br>
文中After Effects术语参考自官方中文版AE。***   
# bodymovin
After Effects 插件，用于将动画导出为 svg/canvas/html + js。

## V 4.6.2
- 加入中继器支持(支持还不完善，但足以应对大部分情况。译者注：好像bug挺多，慎用。。。)！[repeaters! (partially but should cover many cases)]
- 新的表达式支持[new expressions]
- 渲染效能改进[render improvements]
- 减少了冗余信息[reduced garbage collection]

## V 4.6.1
- 修正3D方向控制[3D orientation fix]
- 渲染性能提升[render improvements]

## V 4.6.0
- 新操作界面！[New UI!]
- 支持投影效果器[Drop shadow effect support]
- 做了偏移的图层动画效能提升[performance improvement on animations with offsetted layers]
- 表达式效能提升[big performance improvement on expressions]
- 加强了表达式支持[expressions expressions expressions]

***完整更新说明（英文）参见https://github.com/bodymovin/bodymovin/blob/master/History.md  ***<br/>
<br/>

**直接从adobe在线商店获取！**
https://creative.adobe.com/addons/products/12557  
支持AE CC2014及以上版本。  

如果需要最最新的版本，可以从这里安装：  

### 安装方式1（推荐）：
- 打包为zip下载整个项目到本地。  
- 解压缩并从 '/build/extension' 找到 bodymovin.zxp 文件  
- 使用aescripts.com出品的 [ZXP安装器](http://aescripts.com/learn/zxp-installer/) 进行安装。  

### 安装方式2：  

- 关闭After Effects<br/>
- 打包为zip下载整个项目到本地并解压 build/extension/bodymovin.zxp 文件到 Adobe CEP 文件夹（CEP插件扩展平台）：<br/>
WINDOWS:<br/>
C:\Program Files (x86)\Common Files\Adobe\CEP\extensions 或者<br/>
C:\<用户名>\AppData\Roaming\Adobe\CEP\extensions<br/>
MAC:<br/>
/Library/Application\ Support/Adobe/CEP/extensions/bodymovin<br/>
(你可以在终端中输入:<br/>
cp -R 你解压后的目录/extension /Library/Application\ Support/Adobe/CEP/extensions/bodymovin<br/>
然后输入:<br/>
ls /Library/Application\ Support/Adobe/CEP/extensions/bodymovin<br/>
来保证正确复制了文件)<br/>

- 编辑注册表:<br/>
WINDOWS:<br/>
找到注册表键值 HKEY_CURRENT_USER/Software/Adobe/CSXS.6 增加一个键值名为 PlayerDebugMode, 类型为字符串(String), 值为 1。<br/>
MAC:<br/>
打开文件 ~/Library/Preferences/com.adobe.CSXS.6.plist（com.adobe.CSXS.？？？.plist其中问号根据AE版本不同会有不同） 新加一行，键(key)为PlayerDebugMode, 类型为字符串(String), 值为 1。<br/>

### 安装方式3：  

按照官方手册的指导安装zxp插件，地址如下(英文):  
https://helpx.adobe.com/x-productkb/global/installingextensionsandaddons.html  
直接跳到 "Install third-party extensions"


### 安装完成后
- 在AE里勾选 `编辑 > 首选项 > 常规 > 允许脚本写入文件和访问网络`（Mac 下为 `After Effects > 首选项 > 常规 > 允许脚本写入文件和访问网络`）。

## 如何使用
### 在After Effects中
- 运行AE程序，选择bodymovin插件，位置是 `窗口 > 扩展 > bodymovin` [`Window > Extensions > bodymovin`]
- 此时将弹出一个面板，列出了项目中的所有合成。
- 在面板上点击刷新[Refresh]。
- 选择你想要导出的合成。
- 选择要导出到的地址[Destination Folder]。
- 点击渲染[Render]。
- 找到导出的json文件 (如果动画中有图片资源或者AI图层, 将会同时生成一个images文件夹存放这些图片资源)。

#### 设置：
**分段：** 分段导出你的动画。 如果你的动画有很多层，可以选择分段导出，这样就不会一次性全部加载。 导出工具将会根据图层开始时间进行分段。<br/>
**快照：** 保存一张svg格式的快照作为动画的封面。渲染完动画后, 你可以截取任意一帧快照并保存到硬盘上。 我建议优化这张svg快照，可以利用一些工具比如 https://jakearchibald.github.io/svgomg/ 并好好设置一番。<br/>

### 用于HTML
**查看demo，有不同的动画加载方式：**
- 从build/player/获取最新 bodymovin.js 文件
- 在你的html文件中包含 bodymovin.js (发布时可以gzip压缩一下减少体积)
```html
<script src="js/bodymovin.js" type="text/javascript"></script>
```
你可以调用 bodymovin.loadAnimation() 来开始动画。
可以用一个对象传递这些参数：
- animationData: 包含导出的动画数据的对象。
- path: 动画数据文件的相对路径。 (animationData 和 path 参数是互斥的)
- loop: 循环设置，值为true / false / number（循环/不循环/循环n次（n为输入值））
- autoplay: 自动播放设置。true为准备就绪后自动播放，false为不自动播放。
- name: 动画名，用于后续引用。
- renderer: 选择渲染器，值为'svg' / 'canvas' / 'html' 。
- container: 需要渲染动画的dom元素。
<br />
返回一个动画对象，你可以控制它播放、暂停、设置速度。。。。  <br/>
<br/>

```js
bodymovin.loadAnimation({
  container: element, // 渲染动画的dom元素
  renderer: 'svg',
  loop: true,
  autoplay: true,
  animationData: JSON.parse(animationData) // 动画数据
});
```

- 如果想用已有的canvas画布来绘制, 可以额外传递一个对象: 'renderer' 并按参考如下配置：

```js
bodymovin.loadAnimation({
  container: element, // 渲染动画的dom元素
  renderer: 'svg',
  loop: true,
  autoplay: true,
  animationData: animationData, // 动画数据
  rendererSettings: {
    context: canvasContext, // canvas画布上下文
    scaleMode: 'noScale',
    clearCanvas: false
  }
});
```
如果你这么做了, 必须在每一帧渲染后清除画布。 
<br/>
另一个加载动画的办法是为dom元素加上特定的属性。
你需要包含一个div元素，并设置他的class为bodymovin。 
如果你在页面加载前这么做了，它将自动检测页面上所有class标签值为"bodymovin"的元素。
或者你可以在页面加载完成后调用bodymovin.searchAnimations()，同样会检测页面上所有class标签值为"bodymovin"的元素。<br/>

**步骤：**  
- 将data.json文件放到html文件同级的一个文件夹中。<br/>
- 创建一个将要包含动画的div元素。<br/>

`必要属性`<br/>
一个名为"bodymovin"的class  
一个 "data-animation-path" 属性，值为 data.json 的相对路径。  
`可选属性`<br/>
一个 "data-anim-loop" 属性，控制循环。  
一个 "data-name" 属性，用于指定一个名字作为播放控制的控制目标。  

**示例**

```html
 <div style="width:1067px;height:600px" class="bodymovin" data-animation-path="animation/" data-anim-loop="true" data-name="ninja"></div>
```

## 用法
***动画实例可用的方法如下：***   
**anim.play()** <br/>
**anim.stop()** <br/>
**anim.pause()** <br/>
**anim.setSpeed(speed)** -- 播放速度 ，1 为正常速度。<br/>
**anim.goToAndStop(value, isFrame)** 跳转到某一时间（或帧）并停在那。第一个参数(value)是数值。第二个参数是布尔值，"true"则第一个参数表示“帧”，“false”则表示“时间”。<br/>
**anim.goToAndPlay(value, isFrame)** 跳转到某一时间（或帧）并播放。第一个参数(value)是数值。第二个参数是布尔值，"true"则第一个参数表示“帧”，“false”则表示“时间”。<br/>
**anim.setDirection(direction)** -- 播放方向，正数和0为正常播放，负数为倒放。 <br/>
**anim.playSegments(segments, forceFlag)** -- 播放指定段落。第一个参数是一个数组，形式为[(a,b),(c,d),(e,f)...]则播放第a帧到b帧，然后第c帧到d帧，e到f…… ，第二个参数为布尔值，“true”则立刻播放参数一中的片段，“false”则播放完当前动画后再开始播放片段。<br/>
**anim.destroy()**<br/>

***bodymovin有8个方法:***  
**bodymovin.play()** -- 播放指定动画，1个参数**动画名**。<br/>
**bodymovin.stop()** -- 停止播放指定动画，1个参数**动画名**。 <br/>
**bodymovin.setSpeed()** -- 第一个参数设置动画速度 (1为正常速度），第二个参数**动画名**可选。 <br/>
**bodymovin.setDirection()** -- f播放方向，正数和0为正常播放，负数为倒放，第二个参数**动画名**可选。 <br/>
**bodymovin.searchAnimations()** -- 检测class值为"bodymovin"的元素。 <br/>
**bodymovin.loadAnimation()** -- 前面已有介绍， 返回一个可单独控制的动画实例。 <br/>
**bodymovin.destroy()** --销毁和释放资源。 DOM 元素将会被清空。<br />
**bodymovin.registerAnimation()** -- 你可以直接用registerAnimation来注册一个自定义元素，它必须包含"data-animation-path"属性并指向data.json的地址。<br />
**bodymovin.setQuality()** -- 画质设置，调整动画播放器性能。默认为高画质(high), 可选值为'high'、'medium'、'low', 或者大于1的数字。对于有的动画这些设置差别不大。<br />

## 事件
- onComplete
- onLoopComplete
- onEnterFrame
- onSegmentStart

或者你可以对以下事件设置监听(addEventListener)：
- complete
- loopComplete
- enterFrame
- segmentStart


查看demo文件夹中的例子，或者访问 http://codepen.io/airnan/ 可以看到精彩的演示动画

## 一些建议

### 文件
如果你使用了图片资源或者未转成形状图层的Adobe Illustrator文件图层, 将会同时生成一个images文件夹存放这些图片资源。(我建议将ai图层转换为形状图层，这样他们会被导出为矢量数据，只需在AE中导入的ai图层上右键 > 从矢量图层创建形状)
注意，如果不同的带图片资源的动画导出到同一地址，images文件夹将会被覆盖。


### 性能
Bodymovin的动画都是实时渲染的。 虽然经过了大量优化，最好还是控制AE工程文件体积在一个必要的值。<br/>
更多的优化也正在进行中，但请避免这种情况：绘制了一个巨大的形状图层，但是只通过遮罩使用其中一小部分。<br/>
过多的节点同样会影响性能。<br/>

### 帮助
如果你有动画导出失败或者想让我帮你导出, 不要犹豫请告诉我。<br/>
我很乐意能找到这个插件的不足之处。 <br/>
我的邮箱是 **hernantorrisi@gmail.com**

## 演示
[访问codepen查看动画演示](http://codepen.io/collection/nVYWZR/) <br/>

## 支持的AE特性
- 插件支持预合成、形状图层、固态层、图片、空对象以及文字图层。
- 支持遮罩和反向遮罩。也许别的模式也会支持，但是会对性能造成巨大影响。 
- 支持时间重映射（是的没错！）。
- 支持形状图层的形状、矩形、椭圆和星形。
- 目前只支持滑块效果。
- 支持部分表达式。更多介绍可以[查看这里（英文）](https://github.com/bodymovin/bodymovin/wiki/Expressions)
- 不支持： 图像序列、视频和音频 (也许未来会支持)。
- **不要伸缩图层**！不知为何，伸缩图层会破坏导出的数据，所以不要做这个操作。

## 其他说明
- 如果你想修改或者解析动画播放器，有一些 gulp 命令可以简化这个操作。  
- 看看这些codepen上的优秀作品 [访问codepen作品集](http://codepen.io/collection/nVYWZR/)
- gzip压缩一下动画json数据文件和播放器js文件可以有效减少文件体积。如果你用在项目里，我建议你这么做。

