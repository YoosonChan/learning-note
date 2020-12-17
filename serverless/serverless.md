# [Serverless 极简入门手册](https://yun.serverless80.com/)

# 目录
- [第01篇：题外话，为什么要写这个教程](#第01篇：题外话，为什么要写这个教程)
- [第02篇：通过Serverless窥探一些技术商业化趋势](#第02篇：通过Serverless窥探一些技术商业化趋势)
- [第03篇：云开发有哪些能力](#第03篇：云开发有哪些能力)
- [第04篇：了解腾讯云控制台](#第04篇：了解腾讯云控制台)
- [第05篇：编写第一个云函数](#第05篇：编写第一个云函数)
- [第06篇：数据库CRUD](#第06篇：数据库CRUD)
- [第07篇：云存储：上传、下载、CDN地址、删除文件](#第07篇：云存储：上传、下载、CDN地址、删除文件)
- [第08篇：静态网站部署怎么玩](#第08篇：静态网站部署怎么玩)
- [第09篇：尝试使用CLI来开发项目](#第09篇：尝试使用CLI来开发项目)
- [第10篇：再谈云+端开发模式，采用JS-SDK示例](#第10篇：再谈云+端开发模式，采用JS-SDK示例)
- [第11篇：三个小案例](#第11篇：三个小案例)
- [第12篇：附录](#第12篇：附录)

-------------------------

# 第01篇：题外话，为什么要写这个教程
## 这个教程讲什么的？
讲 Serverless 的，把这个高大上的概念落到地上，可以实操的教程。

## 为什么写这个教程？
本来不想写的，都转产品经理了，写点代码是为了“保持兴趣”。

但是这个“云开发”这种模式，的确很新，不少有较为丰富经验的同学还可以轻松上手，但是刚进入行业的同学对繁琐的流程和概念，却是很空洞，相对有一些门槛。但是目前没有一个可以把入门这件事做的很好，大多是高大上的 Serverless 的空泛概念。

这里说“云开发”模式其实对 Serverless 的一种映射，说模式是希望可以在产品的眼界里跳出来，去看云计算的发展 。当然也因为雇主是腾讯，所以通篇案例都是基于腾讯云云开发这款产品介绍，这个大家应该都可以理解的吧。

另外我这个人比较任性，我认为好的，我认为有用的，我会坚持。即使有人觉得不一定对，但是我想把自己想尝试的，自己的想法融入进去。

## 对这个教程就两个要求：

- 【要求】尽量通俗易懂，舍弃高大上的概念；尝试加一些语气词；
- 【要求】有过程，有细节；
- 【奢望】希望有趣，这个要求太高，争取可以把应用做到实用，其次是奢望有趣；
## 这里的云开发包含哪些内容

入门教程中以 web 云开发为主；因为关于小程序云开发的内容已经比较多了。
案例会夹杂小程序云开发和 Web 云开发的实际项目；

---

# 第02篇：通过Serverless窥探一些技术商业化趋势
当前业界 Serverless 是一个热词，各种高大上概念的包装，好似空中楼阁。但是绝大数的开发只能是隔岸观花、望梅止渴。讲清楚趋势很重要，让人落地也很重要。下面从商业侧技术侧的角度，以云开发为例，剖析技术的发展。

## 降本提效
首先，我们要清楚技术的发展趋势。首先我们看商业的发展，商业的发展一般围绕下面4个要素展开。
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/1.png)

- 助力盈利
- 降低成本
- 提高效率
- 体验增强

商业的发展一定是依赖上下游的，那么在角色的定位中，最重要的是，你能给客户带来什么业务价值，能否帮助他盈利。如果这个问题能够回答的很清楚，公司活下来是大概率事件。也就是能够帮助客户的实现业务价值。这个要求很高，也很难，尤其是技术的商业化。

云计算行业更多的是跟后面三者相关。技术很难直观地帮客户产生商业价值，这个非常难衡量。自我论证是一个非常难的过程，你很难说用了 C 家的云就带来了多少用户的增长，也很难说不用你这个云就会损失多少收入。往往技术的商业化第一步是“降低成本”。

**降低成本**这个看似简单，其实非常难，需要做很深的技术创新。如果你发现了一个极大降低成本的方法，那么这个行业将发生巨大的改变，包括上下游关系都会被重新定义。现在云服务的竞争是火热的🔥，每个云厂商都在绞尽脑汁的做技术创新，期望通过技术创新降低成本。整个行业，有多家云厂商是幸福的，珍惜这个还没有完全分出胜负的年代；假如只剩寡头，消费者没有议价权的。所以在 ```IaaS```（基础设施即服务） 上，唯一的出路只有一个：创新。剖开来说就是：降本和稳定。

**提高效率**很直白，就是如何让客户的业务发展的更快，如何让人的效率可以提高。如下图所示，目前绝大多数的云厂商都是做着二道贩子的生意，只是这个二道贩子对技术的要求比其他行业要高很多。没有云计算的年代，就是基础资源，各家自我加工。有了云计算，粗加工的工作云厂商都做了，在 ```IaaS``` 层都是标品，但是这里的成本和收益是透明的。多少利润空间，早就成为了行业共同的认知。所以云厂商的想获得高额回报的出路是将资源可以做到“精细服务”，提供可以靠近业务的价值。这个过程很难，所以```PaaS```(平台即服务) 和 ```SaaS```(软件即服务)是必由之路，它们可以模糊掉一些价值评估，尤其是靠近业务的 ```SaaS``` 可以带来溢价。
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/2.png)

云计算基本围绕“降本提效”展开。目前来看并不是一门可以 “快速” 挣大钱的生意，更多的是提升了行业的生产力。但是我们不能否认的是，未来自来水公司、燃气公司也是可以挣钱的。

另外一个就是“体验增强”。用户是发展的，对美和体验是有追求的。2000年的互联网产品体验估计现在没有人可以瞧的上一眼。那么围绕“体验增强”的服务，就是每一步都需要的，也是贴近客户和用户的。比如视频云服务，比如直播云服务，CDN 服务，都是体验增强的一个表现。

云计算从粗加工到精细加工，再到增值服务，其趋势就是“整合云服务，套餐出售”，说得更直白些就是“能不能拎包入住”，开发者不要知道细节，开发者也不想触碰细节。是不是可以从“云服务”到“应用云”，或者说“云应用”。

## 封装复杂，暴露简单
很显然，```Serverless``` 概念的提出，就是希望“封装复杂，暴露简单”。
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/3.png)


互联网从初始到高速发展，应用和业务模型越来越复杂，对技术团队的挑战越来越大，所以岗位职能出现了精细分工。但是技术的发展总是会螺旋式上升，慢慢的运维开始自我革命。那能不能运维自动化，能不能 ```devops```？再往后，研发自我革命，能不能进一步提高效率？是否可以 ```devopsless``` , 是否只需要应用开发工程师....

所以“封装复杂，暴露简单”一定是技术的趋势，也是商业化的趋势。

## FaaS
```Serverless``` 从技术层面看，是“封装复杂，暴露简单”；从商业角度看，则是带动资源多次加工，精细化深加工，能不能带动 PaaS 层服务的整合和融合。

```Serverless``` 是一种理念，目前没有一种标准的产品，有的是 ```FaaS``` (函数即服务)来作为产品承载，有的是 ```FaaS + BaaS``` (后端即服务)来作为产品承载。serverless.com 是不是标准，需要值得思考。是不是理念的实践和商业的落地，也需要思考。🤔

如下图，是一个简易的 ```FaaS``` 模型。
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/4.png)

我们希望也是要求：

- 一个函数就是一个服务，可以独立部署、调试、监控；当然可以配合 ```API``` 网管使用；
- 函数之间可以调用，可以抽象一些中间件的服务，以函数形态存在；
- 每个函数，有流量时，可以快速冷启动，响应要快；同时可以根据流量进行伸缩，没有流量可以维持冷冻状态，不需要保持资源的消耗。

因此 ```FaaS``` 带来的好处是：

- **高可扩展，伸缩自动**： 有洪峰就快速扩展，无需关心峰值压力；
- **成本降低**：资源不需要预采购，理想状态就是有流量就消耗，没有流量就降至 0；
- **解构架构**：将服务拆分，架构扁平；
> **TIP**   
结论：```FaaS``` 整合了 ```IaaS``` 层的云服务器和网络，重组了计算单元。

## BaaS
函数只是运行逻辑的地方，光有函数是不行的。云数据库可不可以提供？云存储可不可以提供？监控要不要提供？日志服务要不要提供？这时候，就会发现 ```FaaS``` 只是一个计算容器，或者说“计算单元”。我们开发一个业务，不能只做运算，不做数据存储，不做文件存储。

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/5.png)

因此 ```BaaS```（后端即服务） 服务商解决的问题就是将 ```PaaS```(平台即服务) 产品做整合，所有都在云上，不需要本地搭建和部署。性能和稳定性、安全性由云厂商提供服务支持。

> **TIP**   
```BaaS``` 将服务进行组装，尝试封装复杂。

## 云开发：尝试垂直整合，做到拎包入住
有了 ```FaaS``` 和 ```BaaS```，```Serverless``` 的理念就不再是空中楼阁了。服务的计算容器有了，或者说计算单元更加合理了，基础的 ```IaaS``` 和 ```PaaS``` 层是不是也可以做融合？

**以前需要关心的**：

- API 网关，流量如何控制
- 数据库如何部署，数据库如何优化，分布式怎么做
- Web 容器
- 代码如何构建
- 系统安全
- 日志与监控服务
- 如何计算服务用量，服务器如何扩展
- ......
目前腾讯推出了云开发（https://cloudbase.net/），是 ```Serverless``` 的一种产品实现。这些在云开发中都不需要关心。

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/6.png)

整合了这么多，我觉得完成了拎包入住的第一步，就是“云”侧 OK 了。

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/7.png)

如上图方式1，一般情况，使用云函数构建 ```Serverless``` 服务，云函数起到逻辑和胶水的作用。目前市面上大多数 ```Serverless``` 方案都走到了这一步。那么“端”侧要不要改进？比如我在安全的客户端环境中，上传一张图片，要不要先写一个云函数，然后云函数再去调用数据库服务？获取一个列表数据，是不是也得先写个云函数，然后请求函数拿到数据？

端侧如何进一步提升效率，进一步整合掉。腾讯云云开发因此提供了端侧 SDK，例如提供 JS-SDK , 可以直接操作云数据库，云存储；这样有些能力，不再需要编写云函数，可以直接在客户端用 SDK 提供的 API 进行操作，如下图方式2所示。**那就是需要“云 + 端一体化”，也是云开发诞生的初衷，让开发者只用关心应用开发的最后一公里。**

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/8.png)

```js
const tcb = require('tcb-js-sdk');
const app = tcb.init({
  env: "环境ID, 环境是一个集合，包含数据库、存储、云函数的资源"
});
// 1. 获取数据库引用
var db = app.database();
//2.获取数据库集合
//3.条件查询
db.collection("users")
  .where({
  	name: 'vczero'
	})
  .get()
  .then(res => {
    console.log(res.data);
  });
```
这样一个客户端工程师，就可以承担起所有的“应用开发”的任务，协同的工种就只有自己。真正做到，**SDK 在手，应用说有就有**。目前云开发提供了不只有 ```JS-SDK```，还有 ```Flutter SDK```、```.NET SDK```、```Node.js SDK```。

## 后话
通过 ```Serverless``` 和云开发核心理念的分析，我们可以清楚的看到技术发展的大趋势，是不可逆的：

成本依赖创新，会进一步的压缩；无论是机器的成本，还是人的成本；
云计算服务会进一步降低使用门槛，封装复杂；
从人肉运维到 ```devops```,  再到 ```devopsless``` 和 ```serverless```，趋势不可抗争，先“做没”自己，再给自己创造新机会；能够贴近业务，帮助业务成功的云服务一定是好服务。

---

# 第03篇：云开发有哪些能力
> 再次强调下，云开发是 Serverless 理念落地的一种产品方案，其首推 云 + 端的研发模式。

## 云开发可以做什么
云开发本质上是提供服务端能力的，一个没有后端能力的同学，可以使用云开发构建「高质量」的服务，可以独立完成一款应用的前后端全栈开发。所以云开发可以助力大前端同学扩展边界。 一开始云开发是跟这微信小程序一起发布的，只能在微信小程序里使用；现在云开发还支持各个端，在 ```PC Web```、```H5```、微信公众号、```iOS```、```Android``` 等等应用里可以使用。

## 云开发的能力
上一篇提到云开发提供了 ```FaaS + BaaS``` 的能力，具体能力如下：

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/9.png)

**云存储**
我们可以通过客户端 ``````SDK`````` 或者服务端 ``````SDK``````，在前端页面或者云函数里，上传/删除文件。 该文件可以是 ``````js``````、``````css``````、``````html``````、也可以是图片、``````pdf``````、``````word``````、``````excel``````、视频.....同时，云开发的存储默认提供 ``````CDN`````` 加速能力。

**云函数**
这个就是 ```FaaS``` 的实现，一般用于接口开发、定时任务等等；云函数间可以互相调用。目前云开发的云函数提供 ```HTTP``` 调用方式和客户端 ```callFunction``` 方式。

**数据库**
云开发支持 ```NoSQL``` 数据库，存储的记录类型为 ```JSON``` 格式；同时可以在云函数中通过专有网络（```VPC```）通道调用 ```MySQL```，也可以使用 ```redis```。

**云调用**
云调用是云开发提供的基于云函数使用小程序开放接口的能力。比如获取微信小程序用户信息、小程序码、```OCR``` 能力等等，具体见：https://developers.weixin.qq.com/miniprogram/dev/api-backend/

**静态网站托管**
部署一个包含 ```html```、```css```、```js``` + 媒体资源的网站，再也不用购买服务器。以前可以选择 ```github pages```，现在可以选择稳定的托管服务，所有的流量和资源消耗都是按量付费，用了多少就付多少。目前静态网站托管提供默认域名访问，但是限速。可以绑定自己的域名和申请免费的 ```SSL``` 证书。

**云接入** 云接入能力是和云函数一起使用的，比如开启云函数的 ```HTTP``` 访问，比如将整个 ```Node.js``` 应用部署到函数中，这样 ```Node.js``` 就可以自动扩所容。还可以托管 ```Next.js SSR``` 应用等。

**扩展能力**
整个腾讯云的云服务都可以直接在云开发里使用，比如 ```AI``` 的图像识别、短信能力等等。

## 产品架构
上面具体介绍了每部分能力做什么，下面这一张是整个云开发的能力架构图。

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/10.png)

目前云开发提供了各个端侧 ```SDK```，也提供了两个项目管理工具，一个是可视化的控制台(https://console.cloud.tencent.com/tcb), 另外就是 ```CLI``` 工具。

---

# 第04篇：了解腾讯云控制台

前面聊到了很多概念和能力，现在可以一步步实际操练了。我们可以按照如下步骤来。在使用云开发的能力之前，首先我们需要在腾讯云创建一个可以环境，该环境就包括了各种资源。

**第 1 步：注册腾讯云账号**
注册地址：https://cloud.tencent.com/register

**第 2 步：登录云开发控制台**
地址：https://console.cloud.tencent.com/tcb

**第 3 步：创建一个「按量计费」的环境**
这里可以选择“按量计费”环境，记得勾选开启免费资源，默认是有一定的免费额度，完全够一些小应用跑跑，一般个人博客也没什么问题。作为学习和实验就资源就更够用了。

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/11.png)

**第 4 步：点击环境，进入控制台**
进入控制台后可以看到如下图。

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/12.png)

目前云开发的设计是环境，环境包含各个资源的统计和能力，一个环境一般对应一个应用，当然也可以部署多个应用。你可以把环境类似为虚拟机，但是这是有本质的区别的，因为当应用没有被访问的时候，是不占空间和资源的。这就是 ```serverless``` 的魅力，可以自动伸缩。

如上图，

- A 区：环境的设置，比如开发的函数可以被哪些网站调用，可以设置安全域名以便跨域等等；
- B 区：核心能力区，例如数据库（提供简易的DBMS）、云存储（可以手动上传/删除等管理文件）、云函数
- C 区：运维的服务，例如日志监控告警，比如资源用超了，配置告警策略；
- D 区：扩展能力，比如想用 AI 能力，可以使用这里的扩展；
- E 区：环境的切换，环境是最上层的概念，每个环境里面的配置和数据库都是独立的；

---

# 第05篇：编写第一个云函数

在 ```Serverless``` 中，云函数是作为计算容器存在的，可以作为服务接口使用，也可以做为中转服务使用，也可以编写业务逻辑。我们经常谈的 ```FaaS（Functions as a Service）```中最核心的是云函数。如果需要简单理解，那就是写了一段代码（一个函数），可以直接部署在服务器上，但是这个函数是具备伸缩性的。流量来了，可以直接将函数拉起，可以进行资源扩充；流量回落，可以降至 ```0```。这里不讨论业界如何实现冷启动或者 ```0 - 1``` 的优化。

上一节，我们在控制台创建了自己的环境；这里我们就可以在控制台编写第一个函数了。

## 创建函数
**第 1 步：登录云开发控制台**

网址：https://console.cloud.tencent.com/tcb

**第 2 步：创建云函数**

如下图：

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/13.png)

- 选择基础服务中的侧边栏【云函数】
- 选择之前创建的环境，一定要选择在腾讯云云开发控制台创建的，目前小程序云开发的环境管理没有放开。
- 点击【新建云函数】按钮；
> **TIP**   
如果云函数不需要占用大内存， 可以选择 128 MB；在控制台默认选择的是 256 MB 。

然后，可以直接点击【下一步】即可，如下图：

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/14.png)

## 编写函数
我们在控制台创建函数完成，下面即可编写代码了。目前控制台默认提供了 ```Cloud Studio``` 作为编辑器，基本满足基础的 ```Web IDE``` 需要。
点击「函数名」，进入函数配置和详情页。

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/15.png)
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/16.png)

我们精简默认生成的，修改代码成如下：

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/17.png)
```js
'use strict';
exports.main = async (event, context) => {
    //这里代码比较简单
    //后期会准备从数据库取数据，然后返回结果
    return {
        msg: 'Hello Serverless! Good good study !',
        maybe: '从入门到放弃'
    }
};
```
这里点击【保存】。【保存】和【保存并安装依赖】是有区别的：

- 【保存并安装依赖】需要根据该函数目录下的 ```package.json``` 来安装依赖库，比如 ```node_modules```；目前我们这个例子不依赖任何库，也没有 ```package.json``` 文件，所以不需要安装依赖；
- 【保存】则是直接保存代码；
> **TIP**   
如果实在分不清楚，就直接点击【保存并安装依赖】吧。

## 设置函数可以使用 HTTP 访问
访问函数的形式有好几种，比如函数间调用，客户端 ```SDK``` 调用等；当前这里只介绍「开启 ```HTTP```」触发的形式。有的同学对触发不理解，其实可以理解为 “使用 ```HTTP``` 访问“。

点击【函数配置】，对函数进行设置。
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/18.png)

点击【编辑】，开始设定 HTTP 访问路径，这里设置为 “/say-hello” 。只需要修改这一个地方点击保存。
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/19.png)

#访问并验证返回的结果
点击生成的链接，即可在浏览器看到返回的数据。
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/20.png)

浏览器返回数据如下：
```json
{
  "msg": "Hello Serverless! Good good study !",
  "maybe": "从入门到放弃"
}
```
当你发布完成，这个云函数就具备下面特性：

- 具备应对流量的伸缩性，这个是云开发底层做的，无需开发者关系；
- 无需安装 ```Web``` 容器，例如 ```Tomcat```、```Apache```、```Node.js Server```;
- 无需设置和暴露端口；
- 无需``` Nginx``` 、```API``` 网关；
- 可以自定义函数域名
当然真实的服务不止这么简单，例如：

- 需要设置跨域访问。控制台侧边栏【环境】、【安全设置】【WEB安全域名】可以开启；
- 需要查询数据库返回数据，请看下一节；
## 通过 HTTP URL 传递参数到云函数
通过前面小节，我们已经可以编写和发布云函数了。但是有个问题，既然是 ```HTTP``` 服务，前端传递的参数如何获取呢？
```js
http://api.serverless80.com/say-hello?name=vczero
```
例如上面 ```url``` 中的 ```name``` 参数该如何获取呢？可以通过 ```queryStringParameters``` 获取。例如计算两个数之和，代码如下：
```js
'use strict';
exports.main = async (event, context) => {
    //这里代码比较简单
    //这里通过 queryStringParameters 获取请求参数
    let a = parseInt(event.queryStringParameters.a || 0)
    let b = parseInt(event.queryStringParameters.b || 0)
    return {
        msg: 'Hello Serverless! Good good study !',
        maybe: '从入门到放弃',
        sum: a + b
    }
}
```
```HTTP``` 请求参数如下：
```js
//可以点击生成的路径直接方案，需要加上 a, b 两个参数
https://你的环境ID.service.tcloudbase.com/say-hello?a=1&b=23     
```
返回结果如下：
```json
{
  "msg": "Hello Serverless! Good good study !",
  "maybe": "从入门到放弃",
  "sum": 24
}
```
详细内容可以参考 [云接入](https://docs.cloudbase.net/service/access-cloud-function.html#yun-han-shu-de-ru-can)

## 开启跨域访问
云函数可以通过 ```HTTP``` 访问了，也可以获取请求参数了，那么。在前端应用中，使用 ```ajax``` 请求生成的 ```http url``` 肯定会存在跨域情况。那么，在哪设置该函数可以被「指定域名」访问，其他域名不能访问呢。那就是开启 ```「安全域名」```。

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/27.png)

可以配置：

- 域名，例如 serverless80.com;
- IP，例如 127.0.0.1:8000；
- localhost:8000
> **TIP**   
可以根据开发、正式环境进行修改；应用正式上线后，记得删除无关域名。

## 自定义云函数服务域名
一般情况，可以使用默认生成的域名进行服务调用。但是如果有自己的域名，也可以配置。因为默认的域名生成的比较长，也没有规律，配置自定义域名显得统一性高一些。

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/28.png)

可以按照上图进行配置，如果没有 ```SSL``` 安全证书，可以选择腾讯云的免费证书。免费证书只能配置一个域名，不能配置通配符域名，也就是子域名都需要重新申请。

---

# 第06篇：数据库CRUD
上一节演示了云函数的基本 ```DEMO```，但是比较简单，就直接返回了一个“好好学习” 的 ```JSON ```对象。这一小节来熟悉数据库。

云开发提供了一个 ```NoSQL``` 数据库，数据库中的每条记录都是一个 ```JSON ```格式的对象。一个数据库可以有多个集合（相当于关系型数据中的表），集合可看做一个 ```JSON ```数组，数组中的每个对象就是一条记录。

一般我们称数据记录的增加(```Create```)、读取(```Retrieve```)、更新(```Update```)和删除(```Delete```) 统称为 ```CRUD```。下面，我们基于云函数对数据库进行操作。

## 创建数据库集合（表）和创建一个云函数
**第1步**：创建一个数据集合，取名为 ```users ```
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/21.png)
**第2步**：创建 4 个云函数，分别取名为:

- ```insert_db```
- ```query_db```
- ```update_db```
- ```delete_db```
如下图：

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/22.png)

如果还不了解如何创建云函数，可以查看上一篇「编写第一个云函数」

## 插入数据
点击云函数列表中的 “```insert_db```” 函数，进入代码编辑页面。在编写代码之前，我们需要安装一个 ```Node.js``` 模块 ```tcb-admin-node``` , 该模块提供了在云函数或者说在```Node.js``` 服务端器环境下，可以操作数据库、云存储等的一些方法/```API```。

## 创建 package.json 文件
因为需要引入 ```tcb-admin-node``` 模块，所以先要创建 ```package.json``` 文件，可以按照如下图片1，2，3，4进行。最后记得点击【保存并安装依赖】。

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/23.png)

```package.json``` 文件内容如下，可以复制进去。
```json
{
  "dependencies": {
    "tcb-admin-node": "*"
  }
}
```
## 编写代码
**第 1 步： 获取该环境 ID**
在控制台左侧边栏点击【环境】，点击【环境纵览】，复制环境 ID。后面代码需要通过环境 ID，访问环境的资源，例如数据库。

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/24.png)

**第 2 步： 编写代码**
往 ```index.js``` 文件中编写如下代码，并点击【保存并安装依赖】，代码如下：
```js
'use strict';
const tcb = require('tcb-admin-node')
const app = tcb.init({
  env: '你的环境 ID'
})

const db = app.database()

exports.main = async (event, context) => {
    let result = await db.collection('users').add({
        name:  'test',
        age: 25,
        create_time: new Date()
    })
    return result
}
```
下面分析代码：

- ```const tcb = require('tcb-admin-node')``` 引入云开发 ```Node.js SDK```；
- ```const app = tcb.init({})``` 初始化环境；
- ```app.database()``` 获取数据的引用；
- ```db.collection('users')``` 其中 ```users``` 是 ```6.1``` 节中创建的数据库集合，或者说“表”，这里获取集合的引用；
- ```add({})``` 方法，输入参数为 ```JSON``` 对象，这里是一个 ```user``` 记录；
- ```async``` 和 ```await``` [```JavaSript API```](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/await)，可以将异步转成同步操作；
**第 3 步：开启 HTTP 触发和路径配置**
整个配置过程可以参见上一篇 「编写第一个云函数」 。配置一个触发路径，如下图：

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/25.png)

**第 4 步：访问 HTTP 并验证数据是否插入**
点击链接，浏览器打开访问一次，就插入一次数据。我们点击左侧边栏【数据库】，再点击数据库【users】，即可看到如下数据：

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/26.png)

多请求几次数据库就会出现多几条数据。

## 查询数据
这里，我们使用一开始创建的 ```query_db``` 云函数。当然你可以继续使用 ```insert_db``` 函数。如果不是使用上面的函数，这里我们同样需要做以下几件事：

- 创建 ```package.json``` 并且填写 ```package.json``` 内容，见 ```6.2.1``` 节；
- 使用【保存并安装依赖】按钮；
- 需要复制环境 ```ID```；
- 需要配置云函数 ```HTTP``` 触发路径, 例如 ```/query_db```；
查询的代码具体如下所示：
```js
'use strict';
const tcb = require('tcb-admin-node')
//初始化环境
const app = tcb.init({
  env: '你的环境 ID'
})

//获取数据引用
const db = app.database()

exports.main = async (event, context) => {
    //使用 where 方法查询 name 为 test 数据
    //链式调用 get 方法，执行查询过程并返回数据
    let result = await db.collection('users').where({
        name:  'test'
    })
    .get() 
    //获取返回的数据结果
    return result.data
}      
```
访问配置的 ```HTTP``` 触发路径，即可查询之前插入的数据，上面的插入请求了 ```3``` 次，所以数据返回的 ```3``` 条。
```json
[
  {
  "_id": "5e847ab25ebfe17b0112ef031602897d",
  "age": 25,
  "create_time": "2020-05-16T12:50:03.492Z",
  "name": "test"
  },
  {
  "_id": "e2297d935ebfe86b00bcb9cb6e7c7f1a",
  "age": 25,
  "create_time": "2020-05-16T13:19:39.931Z",
  "name": "test"
  },
  {
  "_id": "a9bfcffc5ebfe88700b26c896baeac9f",
  "age": 25,
  "create_time": "2020-05-16T13:20:07.279Z",
  "name": "test"
  }
] 
```
如果需要返回两条数据，可以使用 ```limit(2)``` ，返回 ```N``` 条，就 ```limit(N)``` 例如：
```js
let result = await db.collection('users').where({ name: 'test'})
    .limt(2)
    .get() 
```
## 更新数据
同样，如果是使用新创建的云函数，需要做以下几件事：

- 创建 ```package.json``` 并且填写 ```package.json``` 内容，见 ```6.2.1``` 节；
- 使用【保存并安装依赖】按钮；
- 需要复制环境 ```ID```；
- 需要配置云函数 ```HTTP``` 触发路径, 例如 ```/update_db```；
这里我想更新所有符合要求的记录的 ```age``` 值，全部更新为 ```88``` 岁，代码如下：
```js
'use strict';
const tcb = require('tcb-admin-node')
//初始化环境
const app = tcb.init({
  env: '你的环境 ID'
})

//获取数据引用
const db = app.database()

exports.main = async (event, context) => {
    //使用 where 方法查询 name 为 test 数据
    //将符合要求的数据的 age 字段值更新为 88
    let result = await db.collection('users').where({
        name:  'test'
    }).update({
        age: 88
    })
    return result
}
```
同样请求 ```HTTP``` 服务，完成更新操作，浏览器返回数据如下，说明符合要求的 ```3``` 条数据均已更新。
```json
{
  "requestId": "1589636820392_1_01781",
  "updated": 3
}
```
```update``` 方法是局部更新，用于更新字段；如果替换某条记录，可以使用 ```set``` 方法，具体见 数据库替换更新

## 删除数据
同样，如果是使用新创建的云函数，需要做以下几件事：

- 创建 ```package.json``` 并且填写 ```package.json``` 内容，见 ```6.2.1``` 节；
- 使用【保存并安装依赖】按钮；
- 需要复制环境 ```ID```；
- 需要配置云函数 ```HTTP``` 触发路径, 例如 ```/delete_db```；
```js
'use strict';
const tcb = require('tcb-admin-node')
//初始化环境
const app = tcb.init({
  env: 'serverless-1d83e7'
})

//获取数据引用
const db = app.database()

exports.main = async (event, context) => {
    //使用 where 方法查询 name 为 test 数据
    //remove 删除符合条件的所有数据
    let result = await db.collection('users').where({
        name:  'test'
    }).remove()
    return result
}
```
通过 ```HTTP``` 触发云函数，浏览器返回 ```3``` 条数据被删除：
```json
{
  "requestId": "1589637228874_1_51061",
  "deleted": 3
}
```
通过 ```where``` 方法可以删除符合条件的所有数据，如果只想删除指定 ```_id``` 字段的 ```1``` 条数据，可以参见 [删除一条记录](https://docs.cloudbase.net/database/delete.html#shan-chu-yi-tiao-ji-lu)

## 附录
更多请参考 [数据库参考指南](https://docs.cloudbase.net/database/introduce.html)

---

# 第07篇：云存储：上传、下载、CDN地址、删除文件
前面章节分享了云函数、数据库，基本上可以完成一个简单应用开发了。但是一款应用应该还会有图片、视频之类的，那么这些数据存放在哪呢？那就是云存储。云存储每个云厂商的叫法不一样，有的叫 ```OSS```、有的叫 ```COS```。

我们打开腾讯云[云开发控制台](https://cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Ftcb%2Fstorage)，如下图是云开发的云存储界面。
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/29.png)

云存储的作用或者说能力有：

- 可以设置访问权限，比如公开图片或者私人相册，可以点击【权限设置】进行设置；
- 可以作为图片上传的图床，比如存放 ```icon``` 、```image```、```svg```......
- 可以作为一些素材或者物料仓库，例如存放 ```pdf```、```word```、```excel```......
- 云开发的云存储默认是 ```CDN``` 加速的；
下面的环节，都是在云函数的基础上操作的，假如对云函数不了解，可以阅读 第 ```05``` 篇：编写第一个云函数。

## 上传文件
我们可以使用 云开发 [Node.js SDK](https://docs.cloudbase.net/api-reference/server/node/initialization.html)，在云函数中进行图片的上传。
```js
'use strict';
const tcb = require("tcb-admin-node")
const fs = require("fs")
const app = tcb.init({
  env: '你的环境 ID'
})

exports.main = async (event, context) => {
    
    // uploadFile 上传文件
    let data = await app.uploadFile({
        cloudPath: "/test-00001.jpg",
        // fileContent: buffer 或要上传的文件可读流
        // 后续会将更简单的方法，在前端直接通过 JS-SDK 上传
        fileContent: fs.createReadStream('./test.png') 
    })

    return {
        status: 1,
        file_id: res.fileID
    }

}
```
## 下载文件
有了文件上传，就有文件的下载动作。
```js
'use strict';
const tcb = require("tcb-admin-node")
const fs = require("fs")
const app = tcb.init({
  env: '你的环境 ID'
})

exports.main = async (event, context) => {

  // downloadFile 下载图片
  let res = await app.downloadFile({
    fileID: '云存储中文件的 fileID',
  })

  // fileContent 类型为 Buffer
  return res.fileContent
}
```
## 获取文件的 CDN 访问路径
一般情况，手动上传的文件，都可以复制到 CDN 的访问链接。但是如果是代码大批量上传的，我们可以写程序获取，例如获取用户的头像。

```js
const tcb = require('tcb-admin-node')

const app = tcb.init({
  env: '你的环境 ID'
})

exports.main = async (event, context) => {

  // getTempFileURL 获取 CDN 访问地址
  let res = await app.getTempFileURL({
    // fileID 数组
    fileList: ['fileID-1', 'fileID-2']
  })

  res.fileList.forEach(item => {
    // 打印文件访问链接
    console.log(item.tempFileURL) 
  })

}
```
## 删除文件
删除文件也比较简单。
```js
const tcb = require('tcb-admin-node')

const app = tcb.init({
  env: '你的环境 ID'
})

exports.main = async (event, context) => {

  // deleteFile 删除文件
  let res = await app.deleteFile({
    fileList: [
        'cloud://a/b/c',
        'cloud://d/e/f'
    ]
  })

  return res.fileList

}
```

---

# 第08篇：静态网站部署怎么玩
一般情况下，我们开发好了 ```html```, ```css```, ```js``` 以及一些媒体资源（如图片、视频）都需要部署到一个静态服务器。比如 ：

- Github pages 就是静态网站服务；
- Nginx 路由静态页面也是最基础的静态网站；
- Vuepress 项目的产物的也是静态网站；
所以，一般情况下我们说到静态网站，就是指网站没有动态内容，就是纯 ```HTML```，没有动态请求。云开发也提供了静态网站托管（服务），可以：

- 部署任何资源和文件；
- 可以设置网站的首页，例如 ```index.html```；
- 可以设置网站的 ```404``` 页面，例如 ```404.html```；
- 也可以自定义域名，建议这么做；因为如果使用的是默认域名，网站的访问会被限速；
- 可以和云函数结合，云函数负责动态调用数据库数据，静态网站托管负责部署 ```html```、```js```、```css```文件；这样一个**动态网站就诞生了**，就全部是 ```Serverless```化了。
> ```TIP```   
静态网站托管需要选择**按量付费套餐**才可以开启。

## 将静态页面部署托管
假定前面没有选择按量付费套餐，则可以选择将环境切换为“按量付费” 或者重新新建环境，如下图所示：
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/30.png)

比如当前的文档站点就是 Vuepress 上传上去的，如下图：
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/31.png)

静态网站托管会提供一个默认域名，可以在基础配置页面对首页和404页面进行设置。
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/32.png)

## 推荐范式：云端一体化模式
一个网站离不开动态数据，也离不开静态页面。因此推荐动静结合的方式。如下图，

**第 1 种方式**，可以在云函数中访问数据库和云存储，也是前面篇章提到的方式；然后在静态托管中通过 ```Ajax``` 请求云函数的 ```HTTP``` 服务。

**第 2 种方式**，可以使用云开发端上 ```SDK```，直接请求数据库和云存储等服务，可以不写云函数，整个站点全部都是前端 ```JavaScript``` 代码。

**第 3 种方式**，就是第一种和第二种方式的结合体，适当时机用云函数 ```HTTP``` 触发，适当时机用端侧 ```SDK```，然后配合静态网站托管，也就是云端一体化开发模式。

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/33.png)

---

# 第09篇：尝试使用CLI来开发项目
在前面篇章我们使用控制台编写代码、管理我们的内容。从这一节开始使用「命令行工具 CLI」 来进行开发。
首先我们需要安装 ```CLI``` 工具。

安装云开发 ```CLI``` 之前需要安装 ```Node.js```。如果本机没有安装 ```Node.js```，请从 ```Node.js``` 官网下载二进制文件直接安装，建议选择 ```LTS``` 版本，版本必须为 ```8.6.0+```。

## 安装
可以使用 ```npm``` 来安装，在命令行输入如下命令：
```sh
npm i -g @cloudbase/cli  
```         
如果遇到提示权限不足的情况，请加 ```sudo``` 命令，如下：
```sh
sudo npm i -g @cloudbase/cli        
```   
如果提示输入密码，请输入本机的当前用户的开机密码。

测试是否安装成功，可以使用 -v 命令，如下：
```sh
cloudbase -v      
```  
如果正确返回版本号，代表安装成功。

这时候你发现 ```cloudbase``` 这么从长，足足 9 个字母，难拼写难记忆；其实可以使用 tcb 代替 ```cloudbase```，比如：
```sh
tcb -v     
```   
## CLI、控制台什么关系
可以这么理解，控制台是一个平台，可以在上面使用 ```Web IDE(cloud studio)``` 编写代码，也可以管理各种配置，例如安全域名、独立域名设置、文件管理等等。但是有一些操作其实可以放到命令行的，比如静态网站部署是不是可以一行命令，就可以将文件上传上去。因此：

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/34.png)

- ```CLI``` 提供一些简单的命令用于开发工具调度，例如在 ```Vuepress package.json``` 中集成 ```hosting```(静态网站托管)的命令；
- 控制台包含了更多配置信息、资源信息，一般属于低频操作；更多的是操作层面；
- 无论是控制台，还是 ```CLI``` , 第一件是登录，否则无法管理自己的资源，这个很好理解的。
## 部署静态网站
在 第 08 篇：静态网站部署怎么玩 中提到可以通过控制台部署静态文件。其实，CLI 也支持部署命令。举个例子🌰，```Vuepress``` 生成 ```dist``` 的目录下面的文件都可以部署到静态网站托管上面。我们可以在 ```Vuepress``` 项目的 ```package.json``` 中加一个命令：
```json
{
  "scripts": {
    "dev": "vuepress dev docs",
    "build": "vuepress build docs",
    "deploy": "tcb hosting:deploy docs/.vuepress/dist/ -e 你的环境 ID"
  },
  "dependencies": {
    "vuepress": "*"
  }
}
```
首先执行 ```login``` 命令，获取鉴权，这样才能对环境和资源进行操作：
```sh
tcb login  
```  
然后可以执行
```sh
tcb hosting:deploy docs/.vuepress/dist/ -e 你的环境 ID
```
如果按照上面对 ```package.json``` 进行了配置，也可以执行：
```sh
npm run deploy
```
之后就可以看到整个上传的过程以及状态，比如当前站点的部署效果如下：
```sh
LEEHUAWANG-MB0:vuepress wanglihua$ npm run deploy

> @ deploy /Users/wanglihua/code/cloud-developer/vuepress
> tcb hosting:deploy docs/.vuepress/dist/ -e 你的环境 ID

文件传输中 [=========================================] 100% 0.0s
✔ 
部署完成 👉 https://open-cloud-5d89b0-1300954686.tcloudbaseapp.com
✔ 文件共计 43 个
✔ 文件上传成功 43 个
┌──────┬──────────────────────────────────┐
│ 状态  │               文件               │
├──────┼──────────────────────────────────┤
│  ✔   │             404.html             │
├──────┼──────────────────────────────────┤
│  ✔   │            index.html            │
├──────┼──────────────────────────────────┤
│  ✔   │          posts/01.html           │
├──────┼──────────────────────────────────┤
│  ✔   │          posts/03.html           │
├──────┼──────────────────────────────────┤
│  ✔   │          posts/04.html           │
├──────┼──────────────────────────────────┤
│  ✔   │          posts/02.html           │
├──────┼──────────────────────────────────┤
│  ✔   │  assets/img/search.83621669.svg  │
├──────┼──────────────────────────────────┤
│  ✔   │ assets/css/0.styles.5eaf5755.css │
├──────┼──────────────────────────────────┤
│  ✔   │     assets/js/10.97930671.js     │
├──────┼──────────────────────────────────┤
│  ✔   │     assets/js/12.ae757b08.js     │
├──────┼──────────────────────────────────┤
│  ✔   │    assets/js/app.840f7c0a.js     │
└──────┴──────────────────────────────────┘
✖ 文件上传失败 0 个
```
这里使用到的就是 ```tcb hosting:deploy``` 命令，第一个参数你的目录地址，```-e``` 后面跟上你的环境 ```ID```。
当然不仅可以用于 ```Vuepress```，其实任何需要托管的页面或者内容都可以通过 ```tcb hosting:deploy``` 命令进行操作。

```tcb hosting``` 命令是一个集合，不止一个 ```deploy```，还有删除和查看文件列表等子命令，具体见 [CLI-静态托管](https://docs.cloudbase.net/cli/hosting.html#quan-liang-bu-shu)

## 创建和部署云函数
一个命令搞定整个静态网站的部署，当然云函数也不在话下。

**第 0 步：tcb login**
同样是登录，只有登录了才能获取环境的操作权限，这个道理都懂的。
```sh
tcb login   
``` 
**第 1 步：tcb init**
选择环境和初始化函数模板
```sh
tcb init
```
如下图，按上下键选择环境：
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/35.png)

然后选择语言和模板，这里选择 ```Node.js``` 和云函数的简单模板：
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/36.png)

执行完成的结果如下：
```sh
LEEHUAWANG-MB0:code wanglihua$ tcb init
✔ 选择关联环境 · serverless80 - [你的环境 ID]
✔ 请输入项目名称 · cloudbase-demo
✔ 选择开发语言 · Node
✔ 选择云开发模板 · Hello World
✔ 已存在同名文件夹：cloudbase-demo，是否覆盖？ (y/N) · true
✔ 创建项目 cloudbase-demo 成功！

👉 执行命令 cd cloudbase-demo 进入项目文件夹！
👉 执行命令 cloudbase functions:deploy app 部署云函数
```
创建的项目目录如下图：

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/37.png)

整个目录中最核心的文件是 ```cloudbaserc.js```，该文件中是整个项目的配置。比如：

- ```envId```: 通过 ```envId``` 指明了是哪个环境，一个开发者有多个环境，代码要准确上传到指定环境；
- ```functionRoot```: 云函数存放的目录，这样可以一个命令部署所有的函数；
- ```functions```: 一个函数的数组，指明每个函数的配置，因为每个函数的配置可能不一样；该配置在上传时会覆盖控制台的函数设置。
例如在 ```functions``` 目录下有 ```app``` 目录，即函数的名称为 ```app```，其配置信息为：

- 超时时间 ```5``` 秒，最长可以设置 ```60``` 秒；
- 在 ```Node.js v10.15``` 环境中执行该函数；
- 内存占用 ```128 MB```，目前最小占用内存为 ```128 MB```；
**第 2 步：tcb functions:deploy**
我们按照刚才创建项目完成的命令行提示进行执行：
```sh
cd cloudbase-demo
tcb functions:deploy app
```
命令行执行结果如下，并且可以根据提示查看函数列表或者创建 ```HTTP``` 触发：

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/38.png)

**第 3 步：tcb functions:list**
查看函数是否部署完成及其状态，如下图：
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/39.png)

更多可参见 [CLI-云函数命令](https://docs.cloudbase.net/cli/functions/deploy.html#fu-gai-tong-ming-han-shu)。

## 附录
- [CLI-环境操作命令](https://docs.cloudbase.net/cli/envs/basement.html)；
- [CLI-云存储命令](https://docs.cloudbase.net/cli/storage.html)；
- [CLI-云接入命令/HTTP 触发](https://docs.cloudbase.net/cli/http-service.html)；

---

# 第10篇：再谈云+端开发模式，采用JS-SDK示例
在第 8 篇的末尾谈到了 [云端一体化模式](https://yun.serverless80.com/posts/08.html#%E6%8E%A8%E8%8D%90%E8%8C%83%E5%BC%8F%EF%BC%9A%E4%BA%91%E7%AB%AF%E4%B8%80%E4%BD%93%E5%8C%96%E6%A8%A1%E5%BC%8F)，这里做一些实操。

**第一种方式**，在前后端分离的开发模式下，一般我们通过 ```Ajax``` 直接对后端（云函数）发起请求，然后后端操作数据库和云存储。
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/40.png)

这种开发方式其实已经 ```run``` 了很多年了，当云函数出现后，可以使用云函数代替服务器环境。

**第二种方式**，就是综合运用端和云的优势，如下图：

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/41.png)

我们可以在客户端中集成云开发的 ```SDK```，直接使用 ```SDK``` 对数据库、云存储等发起请求，当然也可以直接使用 ```callFunction ```方法去请求云函数，这样就不用开启云函数的 ```HTTP``` 请求。所以整个应用架构，建议综合采取此方案。

## 先贴代码，看效果
**第 1 步：在控制台【数据库】模块创建一个集合（表）：test-js-sdk**
因为下面演示使用 ```JS-SDK```，在前端页面直接向数据库插入和读取数据，所以第一步建集合，也就是建表。

**第 2 步：创建一个 html 文件**，将下面代码复制进去保存，比如文件取名为 ```web-demo.html```。同时在控制台将环境 ID 替换成自己的。
```html
<html lang="zh-CN">
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
  </head>
  <body>
    Hello 云开发! <br/>
    Hello Serverless! <br/>
    Hello 云计算! <br/>
    <script src="https://imgcache.qq.com/qcloud/tcbjs/1.6.1/tcb.js"></script>
    <script>
      let app = tcb.init({ env: '你的环境 ID'})
      let auth = app.auth()
      let db = app.database()

      //匿名登录
      //用于演示作用
      async function login(){
        await auth.signInAnonymously()
        const loginState = await auth.getLoginState()
        //为 true 表示登录成功
        console.log(loginState.isAnonymous)
      }

      login()

      //向数据库插入一条数据
      db.collection("test-js-sdk")
          .add({
            text: 'Hello 云计算',
            due: new Date()
          }).then(res => {
              //res 返回插入数据的  id和 requestId  
              console.log(res)
              //读取刚插入的数据
              db.collection("test-js-sdk").doc(res.id).get().then(res=>{
                console.log(res.data)
              })
            })
    </script>
  </body>
</html>
```
**第 3 步：将文件上传到静态托管**，其实也可以本地开启一个 ```localhost``` 静态服务器。这里的目的是为了第 ```3``` 步，配置安全域名（用于跨域访问）。
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/42.png)


**第 4 步：设置安全域名**，在环境中默认添加了静态托管的域名，因此可以直接访问，如果是本地起了静态服务器，也可以添加域名，如下图。
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/43.png)


**第 5 步：打开网页，验证效果**
如果文件上传到了静态托管的根目录，则是静态托管默认域名```/web-demo.html```的访问路径 ，例如这里是：
```sh
https://open-cloud-5d89b0-1300954686.tcloudbaseapp.com/web-demo.html
```
也可以可以点击```web-demo``` 看效果，如下图。
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/44.png)


这个案例可以清楚的看到，没有使用云函数，直接使用了 JS-SDK 即可向数据库插入数据、也可以读取数据，当然也可以上传/删除文件等，当然也可使用 [云函数-callFunction](https://docs.cloudbase.net/api-reference/web/functions.html#callfunction) 直接触发云函数。云端一体化的模式，是不是比较爽呢。

## 代码解释
通过 ```CDN``` 引入 ```JS-SDK``` 这个很好理解，可以通过 [```NPM``` 安装](https://docs.cloudbase.net/api-reference/web/initialization.html#an-zhuang)。

## 登录鉴权
这里使用了 ```auth``` 模块，目的是开启授权，同时也提供了用户管理模块，可以到控制台【用户管理】模块查看。
```js
let app = tcb.init({ env: '你的环境 ID'})
let auth = app.auth()
```
目前支持的登录方式有 4 种：

- [微信公众号登录；](https://docs.cloudbase.net/authentication/wechat-login.html#kai-tong-liu-cheng)
- [微信开放平台登录；](https://docs.cloudbase.net/authentication/wechat-login.html#kai-tong-liu-cheng)
- [匿名登录：为了演示正好使用的是匿名登录，即无感知；](https://docs.cloudbase.net/authentication/anonymous.html#kai-tong-liu-cheng)
- [自定义登录](https://docs.cloudbase.net/authentication/custom-login.html)
## 插入和读取数据
使用 ```db.collection("test-js-sdk")``` 直接获取集合的引用，然后使用 ```add``` 方法，是不是跟 第 06 篇：数据库 CRUD 很像，只不过这代码是运行在浏览器里的。
```js
let db = app.database()
db.collection("test-js-sdk")
  .add({
    text: 'Hello 云计算',
    due: new Date()
  }).then(res => {
    //res 返回插入数据的  id和 requestId  
    console.log(res)
  })
```
同样读取一条数据数据使用了 ```doc``` 方法，如果是多条，可以使用 ```where``` 查询条件查询。
```js
db.collection("test-js-sdk").doc(res.id).get().then(res=>{
  console.log(res.data)
})
```
因此可以根据应用的情况，开启安全域名，比如部分数据库写入操作可以放在云函数里，读取操作完全可以在浏览器中进行。

## 附录
- [JS-SDK 数据库插入](https://docs.cloudbase.net/database/insert.html)
- [JS-SDK 数据库查询](https://docs.cloudbase.net/database/query.html)
- [JS-SDK 数据库查询指令](https://docs.cloudbase.net/api-reference/web/database.html#cha-xun-zhi-ling)
- [JS-SDK 云存储操作](https://docs.cloudbase.net/storage/introduce.html#cdn)
- [JS-SDK 云函数操作](https://docs.cloudbase.net/api-reference/web/functions.html)

---

# 第11篇：三个小案例
## 案例 1：文章阅读数服务
我们搭建自己的博客、或者个人网站，往往需要统计服务。统计服务分为两种，一种是类似百度、友盟的统计，可以根据数据来看 ```PV/UV``` 或者人群画像。但是有时候也需要展示每一篇文章的阅读数给“读者”看。阅读统计服务既可以服务后者的，也可以服务自己。
可以参考 [serverless实践：打造自己的阅读计数组件](https://serverless80.com/wu-fu-wu-de-yue-du-shu-zu-jian-she-ji-yu-pei-zhi/) 这篇文章。

### 统计单篇文章/单个页面的阅读计数
核心代码如下：
```js
'use strict';
const tcb = require('tcb-admin-node')
const app = tcb.init({
  env: "你的环境 ID"
})
const db = app.database()
const _ = db.command

exports.main = async (event, context) => {
  let coll = "read_count"
  let path = decodeURIComponent(event.queryStringParameters.path || '')
  let host = decodeURIComponent(event.queryStringParameters.host || '')
  
  if(!path && !host){
    return {
        status: 0,
        info: '必须传入 host 和 path 参数'
    }
  }
  let data = await db.collection(coll).where({
    host: host,
    path: path
  }).limit(1).get()

  //更新
  if(data.data.length){
    let doc_id = data.data[0]._id
    await db.collection(coll).doc(doc_id).update({
        count: _.inc(1)
    })
    let obj = await db.collection(coll).doc(doc_id).get()
    return {
        status: 1,
        count: obj.data[0].count
    }
  }
  //增加
  else{  
    let o =  await db.collection(coll).add({
      host: host,
      path: path,
      count: 1
    })
    return {
      status: 1,
      count: 1
    }
  } 

};
```
如果自己不想开发和搭建，但是想使用现成的服务，可以参考阅读 https://github.com/serverless80/tongji，已经部署为独立服务了。

## 案例 2：大学之巅小程序
2018 年，开发了一款小程序名叫「大学之巅」，里面包含2600 + 所高校数据；2019 年将小程序数据库改造成了「小程序云开发」，当然目前还有些图片是存在 OSS 上，没有搬迁。可以扫码体验 。
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/minapp-dxzd00011.jpeg)

小程序效果如下：
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/45.jpeg)
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/46.jpeg)



当然，这个小程序的数据开源了，在 https://github.com/vczero/serverless-colleage。有了数据，再使用云开发造一个小程序见识很 easy 的事了。

## 案例 3: 个人相册小程序
有很多美好的回忆，有很多重要的图片，图片管理难很棘手。手机一年换一部，图片传输费劲还经常丢失。经常提示空间不足，删了一遍又一遍。于是开发了一款小程序：小小收藏夹，用来管理自己需要收藏的私人图片。可以扫描体验：

![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/47.png)

小程序效果如下：
![](https://6f70-open-cloud-5d89b0-1300954686.tcb.qcloud.la/serverless-reading/48.png)

代码已经开源，请参考：https://github.com/vczero/CloudPhoto。

## 结语
拥抱 Serverless，拥抱云开发吧，用时代的生产力，去做一些有趣的事情......

---

# 第12篇：附录
## 实践方案
- [将一个 Node.js 应用托管](https://docs.cloudbase.net/service/hosting-server.html)
- [托管 Next.js 应用](https://docs.cloudbase.net/service/hosting-next-app.html#di-1-bu-chu-shi-hua-xiang-mu)
- [如何使用 Redis，MySQL 也可以参考](https://cloud.tencent.com/developer/article/1571537)
- [如何使用云开发自带的 CMS ](https://blog.csdn.net/TCB_CloudBase/article/details/106207911)
## 案例
- [serverless实践：打造自己的阅读计数组件](https://serverless80.com/wu-fu-wu-de-yue-du-shu-zu-jian-she-ji-yu-pei-zhi/)
- [阅读计数服务](https://github.com/serverless80/tongji)
- [大学之巅开放2600所高校数据](https://github.com/vczero/serverless-colleage)
- [打造个人私有.云相册；Serverless + 小程序 + 免费空间/流量/计算服务](https://github.com/vczero/CloudPhoto)

......(待补充)

---

