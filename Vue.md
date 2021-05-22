# Vue

### 概念

> 概念

​	Vue是一套用于构建用户界面的**渐进式框架**，发布于2014年2月。与其他大型框架不同的是，Vue被设计为可以自底向上逐层应用。**Vue的核心库只关心视图层**，不仅易于上手，还便于于第三方库（如：vue-router：跳转，vue-resource：通信，vuex：管理）或既有项目整合。

​	**官网：https://cn.vuejs.org/v2/guide/**

### 前端三要素

> 前端三要素

- HTML（结构）：超文本标记语言（Hyper Text Markup Language），决定网页的结构和内容
- CSS（表现）：层叠样式表（Cascading Style Sheets），设定网页的表现样式
- JavaScript（行为）：是一种弱类脚本语言，其源代码不需经过编译，而是由浏览器解释运行，用于控制页面的行为

##### 表现层（CSS）

> 表现层（CSS）

CSS层叠样式表是一门标记语言，并不是编程语言，因此不可以自定义变量，不可以引用等，换句话说就是不具备任何语法支持，他的主要缺陷如下：

- 语法不够强大，比如无法嵌套书写，导致模块化开发中需要书写很多重复的选择器
- 没有变量和合理的样式复用机制，使得逻辑上相关的属性值必须以字面量的形式重复输出，导致难以维护

这就导致了我们在工作中无端增加了许多工作量。为了解决这个文件，前端开发人员会使用一种称之为**【CSS预处理器】**的工具，提供CSS缺失的样式层复用机制、减少冗余代码，提高样式代码的可维护性。大大提高了前端在样式上的开发效率

##### 什么是 CSS 预处理器

> 什么是 CSS 预处理器

​	CSS预处理器定义了一种新的语言，其基本思想是，用一种专门的编程语言，为CSS增加了一些编程的特性，将CSS作为目标生成文件，然后开发者就只要使用这种语言进行CSS的编程工作。转化成通俗易懂的话来说就是**“用一种专门的变编程语言，进行Web页面样式设计，再通过编译器转化为正常的CSS文件，以供项目使用”**

​	**常用的CSS预处理器有哪些**

- SASS：基于Ruby，通过服务端处理，功能强大。解析效率高。需要学习Ruby语言，上手难度高于LESS。
- LESS：基于NodeJS，通过客户端处理，使用简单。功能比SASS简单，解析效率也低于SASS，但再实际开发中足够了，所以我们后台人员如果需要的话，建议使用LESS。

##### 行为层（JavaScript）

> 行为层（JavaScript）

​	JavaScript是一门弱类型脚本语言，其源代码再发往客户端运行之前不需要经过编译，而是将文本格式的字符代码发送给浏览器由浏览器解释运行

​	**Native原生JS开发**

​	原生JS开发，也就是让我们按照**【ECMAScript】**标准的开发方式，简称是ES，特点是所有浏览器都支持。

​	**TypeScript微软的标准**

​	TypeScript是一种由微软开发的自由和开源的编程语言。他是JavaScript的一个超集，而且本质上向这个语言添加了可选的静态类型和基于类的面向对象编程。由安德斯·海尔斯伯格（C#、Delphi、TypeScript之父；.NET创立者）主导。

**MVVM：数据双向绑定（Model View View Model）**

**SoC：关注度分离原则**

##### JavaScript 框架

> JavaScript 框架

- jQuery：大家熟知的JavaScript框架，优点是简化了DOM操作，缺点是DOM操作太频繁，影像前端性能；在前端眼里使用它仅仅是为了兼容IE6、7、8；
- Angular：Google收购的前端框架，由一群Java程序员开发，其特点是将后台的MVC模式搬到了前端并增加了**模块化开发**的理念，与微软合作，采用TypeScript语法开发；对后台程序员友好，对前端程序员不太友好；最大的缺点是版本迭代不合理（如1代 -> 2代，除了名字，基本就是两个东西；先已推出Angular6）
- React：Facebook出品，一款高性能的JS前端框架；特点是提出了新概念**【虚拟DOM】**用于真实DOM操作，在内存中模拟DOM操作，有效的提升了前端渲染效率；缺点是使用复杂，因为需要额外学习一门**【JSX】**语言；
- Vue：一款渐进式JavaScript框架，所谓渐进式就是逐步实现新特性的意思，如实现模块化开发、路由、状态管理等新特性。其特点是综合了Angular（模块化）和React（虚拟DOM）的优点；
- Axios：前端通信框架；因为Vue的边界很明确，就是为了处理DOM，所以并不具备通信能力，此时就需要额外使用一个通信框架与服务器交互；当然也可以直接使用jQuery提供的AJAX通信功能；

##### UI 框架

> UI框架

- Ant-Design：阿里巴巴出品，基于React的UI框架
- ElementUI、iview、ice：饿了么出品，基于Vue的UI框架
- Bootstrap：Twitter推出的一个用于前端开发的开源工具包
- AmazeUI：又叫“妹子UI”，一款HTML5跨屏前端框架

##### JavaScript构建工具

> JavaScript 构建工具

- Babel：JS编译工具，主要用于浏览器不支持的ES新特性，比如用于编译TypeScript
- WebPack：模块打包器，主要作用是打包、压缩、合并及按序加载

#### 三端统一

##### 混合开发（Htbrid App）

> 混合开发 （Htbrid App）

主要目的是实现一套代码三端统一（PC、Android：。apk、iOS：.ipa）并能够调用到设备底层硬件（如：传感器、GPS、摄像头等），打包方式主要有以下两种：

- 云打包：HBuild -> HBuildX，DCloud出品；API Cloud
- 本地打包：Cordova（前身是PhoneGap）

##### 微信小程序：WeUI

> 微信小程序：WeUI

##### 后端技术

> 后端技术

​	前端人员为了方便开发也需要掌握一定的后端技术，但我们Java后台人员知道后台知识体系极其庞大复杂，所以为了方便前端人员开发后台应用，就出现了 **NodeJS **这样的技术。

​	NodeJS 的作者已经声称放弃NodeJS （说是架构做的不好再加上笨重的 node_modules，可能让作者不爽了），开始开发全新架构的 **Deno**

​	既然是后台技术，那肯定需要框架和项目管理工具， NodeJS 框架及项目管理工具如下：

- Express：NodeJS 框架
- Koa：Express 简化版
- NPM：项目综合管理工具，类似于 Maven
- YARN：NPM的替代方案，类似于 Maven 和 Gradle 的关系

##### iView

> iView

​	iview是一个强大的基于 Vue 的 UI 库，有很多实用的基础组件比 elementui 的组件更丰富，主要服务于 PC 界面的中后台产品。使用单文件的 Vue 组件化开发模式基于 npm + webpack + babel 开发，支持 ES2015 高质量、功能丰富 友好的 API ，自由灵活地使用空间

- [官网地址](http://v1.iviewui.com/)

- [Github](https://github.com/iview/iview)

- [iview-admin](http://admin.iviewui.com/home)

  **备注：属于前端主流框架，选型时考虑使用，主要特点时移动端支持较多**

##### ElementUI

> ElementUI

Element 是饿了么前端开源维护的 Vue UI 组件库，组件齐全，基本涵盖后台所需的所有组件，文档讲解详细，例子也很丰富。主要用于开发 PC 端的页面，是一个质量比较高的 Vue UI 组件库。

- [官网地址](https://element.eleme.cn/#/zh-CN)

- [Github](https://github.com/ElementUI)

- [vue-element-admin](https://panjiachen.github.io/vue-element-admin-site/zh/)

  **备注：属于前端主流框架，造型时可考虑使用，主要特点时桌面端支持较多**

##### ICE

> ICE

飞冰时阿里巴巴团队基于 React/Angualr/Vue 的中后台应用解决方案，在阿里巴巴内部，已经有270多个来自于几乎所有 BU 的项目在使用。飞冰包含了一条从设计端到开发端的完整链路，帮助用户快速搭建属于自己的中后台应用。

- [官网地址](https://ice.work/)

- [Github](https://github.com/Ice)

  **备注：主要组件还是以 React 为主，截至至今日对 Vue 的支持还不太完善，目前尚处于观望阶段**

##### VantUI

> VantUI

Vant UI 是有赞前端团队基于有赞统一的规范实现的 Vue 组件库，提供了一整套 UI 基础组件和业务组件。通过 Vant，可以快速搭建出风格统一的页面，提升开发效率。

- [官网地址](https://vant-contrib.gitee.io/vant/#/zh-CN/col)
- [Github](https://github.com/topics/vantui)

##### AtUI

> AtUI

at-ui 是一款基于 Vue 2.x 的前端 UI 组件库，主要用于快速开发 PC 网站产品，它提供了一套 npm + webpack + babel 前端开发工作流程，CSS 样式独立，即使采用不同的框架实现都能保持统一的 UI 风格。

- [官网地址](https://aliqin.github.io/atui/)
- [Github](https://github.com/ui-vue/atui)

##### CubeUI

> CubeUI

cube-ui 是滴滴团队开发的基于 Vue.js 实现的精致移动端组件库。支持按需引入后编译，清凉灵活；扩展性强，可以方便地基于现有组件实现二次开发。

- [官网地址](https://didi.github.io/cube-ui/#/zh-CN)
- [Github](https://github.com/cube-ui)

#### 混合开发

##### Flutter

> Flutter

Flutter 是谷歌的移动端 UI 框架，可在极短的时间内构建 Android 和 iOS 上高质量的原生级应用。Fiutter 可与现有代码一起工作，它被世界各地的开发者和组织使用，并且 Flutter 是免费和开源的。

- [官网地址](https://flutterchina.club/)

- [Github](https://github.com/flutter/flutter)

  **备注：Google 出品，主要特点是快速构建原生 APP 应用程序，如做混合应用该框架为必选框架**

##### Ionic

> Ionic

Ionic 既是一个 CSS 框架也是一个 Javascript UI 库，Ionic 是目前最有潜力的一款 HTML5 手机应用开发框架。通过 SASS架构应用程序，它提供了很多 UI 组件来帮助开发者开发强大的应用。它使用 JavaScript MVVM 框架 和 AngularJS/Vue 来增强应用。提供数据的双向绑定，使用它成为 Web 和移动开发者的共同选择。

- [官网地址](https://ionicframework.com/)
- [官网文档](https://ionicframework.com/docs)
- [Github](https://github.com/ionic-team/ionic-framework)

#### 微信小程序

##### mpvue

> mpvue

mpvue 是美团开发的一个使用 Vue.js 开发小程序的前端框架，目前支持 **微信小程序、百度智能小程序、头条小程序** 和 **支付宝小程序**。框架基于 Vue.js，修改了的运行时框架 runtime 和代码编译器 compiler 实现，使其可运行在小程序环境中，从而为小程序开发引入了 Vue.js 开发体验。

- [官网地址](http://mpvue.com/)

- [Github](https://github.com/mpvue)

  **备注：完备的 Vue 开发体验，并且支持多平台的小程序开发，推荐使用**

##### WeUI

> WeUI

WeUI 是一款同微信原生视觉体验一致的基础样式库，由微信官方设计团队为微信内网页和微信小程序量身设计，令用户的使用感知更加统一。包含 **button、cell、dialog、toast、article、icon** 等各式元素。

- [官网地址](https://weui.io/)
- [Github](https://github.com/Tencent/weui)

### 了解前后分离的演变史

​	**为什么需要前后分离**

> 后端为主的 MVC 时代

​	为了降低开发的复杂度，以后端为出发点，比如： **Struts、SpringMVC** 等框架的使用，就是后端的 MVC 时代；

​	以 SpringMVC 流程

![](https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=95178636,3919750076&fm=26&gp=0.jpg)

- 发起请求到前端控制器（DispatcherServlet）
- 前端控制器请求 HandlerMapping 查找 Handler ，可以根据 xml 配置、注解进行查找
- 处理器映射器 HandlerMapping 向前端控制器返回 Handler
- 前端控制器调用处理器适配器去执行 Handler
- 处理器适配器去执行 Handler
- Handler 执行完成给适配器返回 ModelAndView
- 处理器适配器向前端控制器返回 ModelAandView ， ModelAndView 是 SpringMVC 框架的一个底层对象，包含 Model 和 View
- 前端控制器请求视图解析器去进行视图解析，根据逻辑视图名解析真正的视图（JSP）
- 视图解析器向前端控制器返回 View
- 前端控制器进行视图渲染，视图渲染将模型数据（在 ModelAndView 对象中）填充到 request 域
- 前端控制器向用户响应结果

**优点**

MVC 是一个非常好的协作模式，能够有效降低代码的耦合度，从架构上能够让开发者明白代码应该写在哪里。为了让 View 更纯粹，还可以使用 Themeleaf、Freemarker 等模板引擎，使模板里无法写入 Java代码，让前后端分工更加清晰。

**缺点**

- 前端开发重度依赖开发环境，开发效率低，这种架构下，前后端协作有两种模式
  - 第一种是前端写 DEMO ，写好后，让后端去套模板。好处是 DEMO 可以本地开发，很高效。不足是还需要后端套模板，有可能套错，套完后还需要前端确定，来回沟通整的成本比较大；
  - 另一种协作模式是前端负责浏览器端的所有开发和服务器端的 View 层模板开发。好处是 UI 相关的代码都是前端去写就好，后端不用太关注，不足就是前端开发重度绑定后端环境，环境成为影响前端开发效率的重要因素。

- 前后端职责纠缠不清：模板引擎功能强大，依旧可以通过拿到的上下文变量来实现各种业务逻辑。这样，只要前端弱势一点，往往就会被后端要求在模板层写出不少业务代码，还有一个很大的灰色地带是 Controller ，页面路由等功能本应该是前端最关注的，但却是由后端来实现。Controller 本身与 Model 往往也会纠缠不清，看了让人咬牙的业务代码经常会出现在 Controller 层，这些问题不能全归结于程序员的素养，否则 JSP 就够了。

- 对前端发挥的局限性：性能优化如果只在前端做空间非常有限，于是我们经常需要后端合作，但由于后端框架限制，我们很难使用 **【Comet】、【BigPipe】** 等技术方案来优化性能

  > 基于 AJAX 带来的 SPA 时代

时间回到2005年 AJAX（Asynchronous JavaScript And XM，异步 JavaScript 和 XML，老技术新用法）被正式提出并开始使用 CDN 作为静态资源存储，于是出现了 JavaScript 王者归来（在这之前 JS 都是用来在网页上贴广告的）的 SPA （Single Page Application）单页面应用时代。

![](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fgss0.baidu.com%2F9fo3dSag_xI4khGko9WTAnF6hhy%2Fzhidao%2Fpic%2Fitem%2Fa5c27d1ed21b0ef4c17e42b9d6c451da80cb3e47.jpg&refer=http%3A%2F%2Fgss0.baidu.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1612502935&t=74607496119530a9830a49848097438f)

**优点**

这种模式下，**前后端的分工非常清晰，前后端的关键写作点是 AJAX 接口。**看起来是如此美妙，但回过头来看看的话，这与 JSP 时代区别不大。复杂度从服务端的 JSP 里移到了浏览器 JavaScript ，浏览器端变得很复杂，类似于 SpringMVC ，**这个时代开始出现浏览器端的分层架构：**

![](https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=2280532514,761898149&fm=11&gp=0.jpg)

**缺点**

- **前后端接口的约定**：如果后端的接口一塌糊涂，如果后端的业务模型不够稳定，那么前端开发会很痛苦；不少团队也有类似尝试，通过接口规则、接口平台等方式来做。**有了和后端一起沉淀的 接口规则，还可以用来模拟数据，使得前后端可以在约定接口后实现高效并行开发。**
- **前端开发的复杂度控制：**SPA 应用大多功能以功能交互型为主，JavaScript 代码十万行很正常。大量 JS 代码的组织，与 View 层的绑定等，都不是容易的事情。

> 前端为主的 MV* 时代

​	此处的 MV* 模式如下：

- **MVC（同步通信为主）：Model、View、Controller**

- **MVP（异步通信为主）：Model、View、Presenter**

- **MVVM（异步通信为主）：Model、View、ViewModel**

  为了降低前端开发复杂度，涌现了大量的前端框架，比如 **AngularJS、React、Vue.js、EmberJS** 等，这些框架总的原则是先按类型分层，比如 **Templates、Controllers、Models**，然后再在层内做切分，如下图：

![image-20210106134736106](http://zhaocan.fym233.cn/20210121100114.png)

**优点**

- **前后端职责很清晰：**前端工作在浏览器端，后端工作在服务器端，清晰的分工，可以让开发并行，测试数据的模拟不难，前端可以本地开发。后端则可以专注于业务逻辑的处理，输出 RESTful 等接口。
- **前端开发的复杂度可控：**前端代码很重，但合理的分层，让前端代码能各司其职。这一块蛮有意思的，简单如模板特性的选择，就有很多很多讲究。并非越强大越好，限制什么，留下哪些自由，代码应该如何组织，所有这一切设计，得花一本书的厚度去说明。
- **部署相对独立：**可以快速改进产品体验

**缺点**

- 代码不能复用。比如后端依旧需要对数据做各种校验，校验逻辑无法复用浏览器端的代码。如果可以复用，那么对后端的数据校验可以相对简单化。
- 全异步，对 SEO 不利。往往还需要服务端做同步渲染的降级方案
- 性能并非最佳，特别是移动互联网环境下
- SPA 不能满足所有需求，依旧存在大量多页面应用。URL Design 需要后端配合，前端无法完全掌控。

> NodeJS 带来的全栈时代

​	前端为主的 MV* 模式解决了很多很多问题，但如上所述，依旧存在不少不足之处。随着 NodeJS 的兴起，JavaScript 开始有能力运行在服务端。这意味着可以有一种新的研发模式；

在这种研发模式下，前后端的职责很清晰。对前端来说，两个 UI 层各司其职；

- Front-end UI layer 处理浏览器层的展现逻辑。通过 CSS 渲染样式，通过 JavaScript 添加交互功能， HTML 的生成也可以放在这层，具体看应用场景。

- Back-end UI layer 处理路由、模板、数据获取、Cookie 等。通过路由，前端终于可以自主把控 URL Design，这样无论是单页面应用还是多页面应用，前端都可以自由调控。后端也终于可以摆脱对展现的强关注，转而可以专心于业务逻辑层的开发。

  通过 Node，Web Server 层也是 JavaScript 代码，这意味着部分代码可前后复用，需要 SEO的场景可以在服务端同步渲染，由于异步请求太多导致的性能问题也可以通过服务端来缓解。前一种模式的不足，通过这种模式几乎都能完美解决掉。

  与 JSP 模式相比，全栈模式看起来是一种回归，也的确是一种向原始开发模式的回归，不过是一种螺旋上升式的回归。

  基于 NodeJS 的全栈模式，依旧面临很多挑战：

- 需要前端对服务端编程有更进一步的认识。比如 TCP/IP 等网络知识的掌握。
- NodeJS 层与 Java 层的高效通信。NodeJS 模式下，都在服务器端，RESTful HTTP 通信未必高效，通过 SOAP 等方式通信更高效。一切需要在验证中前行。
- 对部署、运维层面的熟练了解，需要更多知识点的实操经验。
- 大量历史遗留问题如何过度。这可能是最大最大的阻力。

### 什么是MVVM

MVVM（Model-View-ViewModel）是一种软件架构设计模式，由微软 WPF （用于替代WinForm，以前就是用这个技术开发桌面应用程序的）和 Ted Peters 开发，是一种简化用户界面的**事件驱动编程方式**。由 John Gossman （同样也是 WPF 和 Silverlight 的架构师）于2005年在他的博客上发表。

MVVM 源自于经典的 MVC （Model-View-Controller）模式。MVVM 的核心是 ViewModel 层，负责转换 Model中的数据对象来让数据变得更加容器管理和使用，其作用如下：

- 该层向上与视图层进行双向绑定
- 向下与 Model 层通过接口请求进行数据交互

### 为什么要使用 MVVM

​	MVVM 模式和 MVC 模式一样，主要目的是分离视图（View）和模型（Model），有几大好处

- 低耦合：视图（View）可以独立与 Model 变化和修改，一个 ViewModel 可以绑定到不同的 View 上，当 View变化的时候 Model 可以不变，当 Model 变化的时候 View 也可以不变。
- 可复用：你可以把一些视图逻辑放在一个 ViewModel 里面，让很多 View 重用这段视图逻辑。
- 独立开发：开发人员可以专注于业务逻辑和数据的开发（ViewModel），设计人员可以专注于页面设计。
- 可测试：界面素来是比较难于测试的，而现在测试可以针对 ViewModel 来写

> View

​	View 是视图层，也就是用户界面。前端主要由 HTML 和 CSS 来构建，为了更方便地展现 ViewModel 或者 Model 层的数据，已经产生了各种各样的前后端分离模板语言，比如 FreeMarker、Thymeleaf 等等，各大 MVVM 框架如 Vue.js、AngularJS、EJS 等也都有自己用来构建用户界面的内置模板语言

> Model

​	Model 是指数据模型，泛指后端进行的各种业务逻辑处理和数据操控，主要围绕数据库系统展开。这里的难点主要在于需要和前端约定统一的  **接口规则**

> ViewModel

​	ViewModel 是由前端开发人员组织生成和维护的视图数据层。在这一层，前端开发者对从后端获取的 Model 数据进行转换处理，做二次封装，以生成符合 View 层的使用预期的视图数据模型。

​	需要注意的是 ViewModel 所封装出来的数据模型包括视图的状态和行为两部分，而 Model 层的数据模型是只包含状态的

- 比如页面的这块展示什么，那一块展示什么这些都属于视图状态（展示）
- 页面加载进来时发生什么，点击这一块发生什么，这一块滚动时发生什么这些都属于视图行为（交互）	

视图状态和行为都封装在了 ViewModel 里。这样的封装使得 ViewModel 可以完整地去描述View层。由于实现了双向绑定，ViewModel 的内容会实时展现在 View 层，这是激动人心的，因为前端开发者再也不必低效又麻烦地通过操纵 DOM 去更新视图。

MVVM 框架已经把所有事情都做好了，我们开发者只需要处理和维护 ViewModel，更新数据视图就会自动得到相应更新，真正实现 **事件驱动编程**

View 层展现的不是 Model 层的数据，而是 ViewModel 的数据，由 ViewModel 负责与 Model 层交互，这就**完全解耦了 View 层 和 Model 层，这个解耦是至关重要的，它是前后端分离方案实施的重要一环。**

##### Vue

> Vue

​	Vue（读音 /vju/，类似于 view）是一套用于构建用户界面的渐进式框架，发布于2014年2月。与其他大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库（如：vue-resource，vuex）或既有项目整合。

##### MVVM模式的实现者

- Model：模型层，在这里表示 JavaScript 对象

- View：视图层，在这里表示 DOM （ HTML 操作的元素）

- ViewModel：连接视图的数据的中间件，Vue.js 就是 MVVM 中的 ViewModel 层的实现者

  在 MVVM 架构中，是不允许 数据 和 视图 直接通信的，只能通过 ViewModel 来通信，而 ViewModel 就是定义了一个 Observer 观察者

- ViewModel 能够观察到数据的变化，并对视图对应的内容进行更形

- ViewModel 能够监听到视图的变化，并能够通知数据发生改变

  **Vue.js 就是一个 MVVM 的实现者，他的核心就是实现了 DOM 监听与数据绑定**

##### 为什么要使用Vue.js

- 轻量级，体积小是一个重要指标。Vue.js 压缩后只有 20多个kb（Angular 压缩后 56kb+，React 压缩后 44kb+）
- 移动有限。更适合移动端，比如移动端的 Touch 事件
- 易上手，学习曲线平稳，文档齐全
- 吸取了 Angular（模块化）和 React（虚拟DOM）的长处，并拥有自己独特的功能，如：计算属性
- 开源，社区活跃度高

### 下载地址

- 开发版本

  - 包含完整的警告和调试模式：https://vuejs.org/js/vue.js
  - 删除了警告，30.96kb min + gzip：https://vuejs.org/js/vue.min.js

- CDN

  ```javascript
  <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.js"></script>
  
  <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
  ```

**显示数据：{{ }}**

### Vue7大属性

**el属性**

- 用来指示vue编译器从什么地方开始解析 vue的语法，可以说是一个占位符。

**data属性**

- 用来组织从view中抽象出来的属性，可以说将视图的数据抽象出来存放在data中。

**template属性**

- 用来设置模板，会替换页面元素，包括占位符。

**methods属性**

- 放置页面中的业务逻辑，js方法一般都放置在methods中

**render属性**

- 创建真正的Virtual Dom

**computed属性**

- 用来计算

**watch属性**

- watch:function(new,old){} 监听data中数据的变化 两个参数，一个返回新值，一个返回旧值，

##### Vue的基本结构

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
</head>
<body>
<!-- view层 模板 -->
<div id="app">
    {{message}}
</div>
<script>
    var vm = new Vue({
        el: "#app",
        data:{
            message: "hello,Vue!"
        }
    });
</script>
</body>
</html>
```

### 指令

>**指令带有前缀v-，以代表它们是 Vue 提供的特殊特性。它们会在渲染的 DOM 上应用特殊的响应式行为。**

###### v-bind

```vue
<div id="app-2">
  <span v-bind:title="message">
    鼠标悬停几秒钟查看此处动态绑定的提示信息！
  </span>
</div>



<script>
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: '页面加载于 ' + new Date().toLocaleString()
  }
})
</script>
```

**该指令的意思是：将这个元素节点的 title 特性和 Vue 实例的 message 属性保持一致**

**如果你再次打开浏览器的 JavaScript 控制台，输入 app2.message = "新消息"，就会再一次看到这个绑定了 title 特性的 HTML 已经进行了更新。**

**v-bind:title 可以缩写为 :title**

###### v-if，v-else

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>demo2</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
</head>
<!-- view层 模板 -->
<body>
    <div id="app">
        <h1 v-if="type==='A'">A</h1>
        <h1 v-else-if="type==='B'">B</h1>
        <h1 v-else>C</h1>
    </div>
</body>
<script>
    var vm = new Vue({
        el:'#app',
        data:{
            type: 'A'
        }
    })
</script>
</html>
```

###### v-for

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>demo3</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
</head>
<body>
<!-- view层 模板 -->
<div id="app">
    <li v-for="item in items">
        {{item.message}}
    </li>
    <li v-for="(num,index) in nums">
        {{num.number}}--{{index}}
    </li>
</div>


<script>
    var vm = new Vue({
        el:'#app',
        data: {
            items: [
                {message: '1'},
                {message: '2'},
                {message: '3'}
            ],
            nums: [
                {number: '001'},
                {number: '002'},
                {number: '003'}
            ]
        }
    })
</script>
</body>
</html>
```

### 事件

###### v-on

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>demo4</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
</head>
<body>
<div id="app">
    <button v-on:click="sayHi">click me</button>
    <!--
    第二种写法：
    <button @click="sayHi">click me</button>
    -->
</div>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            message: 'Hello World'
        },
        methods: {   // 方法必须定义在Vue 的 Methods 对象中
            sayHi: function(event){
                alert(this.message);
            }
        }
    });
</script>
</body>
</html>
```

**v-on:click 可以缩写为 @click**

### 双向绑定

##### 什么是双向绑定

​	Vue.js 是一个 MVVM 框架，即数据双向绑定，即当数据发生变化的时候，视图也就发生变化，当视图发生变化的时候，数据也会跟着同步变化。这也算是Vue.js的精髓之处了。

​	我们所说的数据双向绑定，一定是对于 UI 控件来说的，非 UI 控件不会涉及到数据双向绑定，单向数据绑定是使用状态管理工具的前提。如果我们使用 vuex，那么数据流也是单项的，这时就会和双向数据绑定有冲突。

##### 为什么要实现数据的双向绑定

​	在 Vue.js 中，如果使用 vuex ，实际上数据还是单向的，之所以说是数据双向绑定，这是用的 UI 空间来说，对于我们处理表单， Vue.js 的双向数据绑定用起来就特别舒服了。即两者并不互斥，在全局性数据流使用单项，方便跟踪；局部性数据流使用双向，简单易操作。

##### 在表单中使用双向绑定

​	可以用 v-model 指令在表单 `<input>、<textarea>` 及 `<select>`元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。尽管有些神奇，但 v-model 本质上不过是语法糖。它负责监听用户的输入事件以更新数据，并对一些极端场景进行以西特殊处理。

​	**注意：v-model 会忽略所有表单元素的 value、checked、selected 特性的初始值而总是将 Vue 实例的数据作为数据来源。应该通过 JavaScript 在组件的 data 选项中声明初始值！**

###### **v-model**

**text/textarea**

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>demo1</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
</head>
<body>
<!-- view层 模板 -->
<div id="app">
    输入的文本：<input type="text" v-model="message">{{message}}
    <br/>
    <textarea v-model="message"></textarea>
</div>

<script>
    var vm = new Vue({
        el: "#app",
        data:{
            message: "ok",
        }
    });
</script>
</body>
</html>
```

**单选框  radio**

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>demo1</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
</head>
<body>
<!-- view层 模板 -->
<div id="app">
    性别：
    <!-- v-model="checked -->
    <input type="radio" value="男" name="sex" v-model="checkedValue"> 男
    <input type="radio" value="女" name="sex" v-model="checkedValue"> 女
    <br/>
    <p>选择了：{{checkedValue}}</p>
</div>

<script>
    var vm = new Vue({
        el: "#app",
        data:{
            checked: "false",
            checkedValue: ""
        }
    });
</script>
</body>
</html>
```

**下拉列表  select**

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>demo1</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
</head>
<body>
<!-- view层 模板 -->
<div id="app">
    <select v-model="checkedValue">
        <option value="" disabled>---请选择---</option>
        <option>A</option>
        <option>B</option>
        <option>C</option>
    </select>
    <br/>
    <p>选择了：{{checkedValue}}</p>
</div>

<script>
    var vm = new Vue({
        el: "#app",
        data:{
            checkedValue: ""
        }
    });
</script>
</body>
</html>
```

### 组件

##### 什么是组件

​	组件是可复用的 Vue 实例，说白了就是一组可以重复使用的模板，跟 JSTL 的自定义标签、Themeleaf 的 th:fragment 等框架有着异曲同工之妙。通常一个应用会以一颗嵌套的组件树的形式来组织。

###### **Component**

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>demo6</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
</head>
<body>
<!-- view层 模板 -->
<div id="app">
    <componenttest v-for="item in items" v-bind:zc="item"></componenttest>
</div>

<script>

    // 定义一个Vue 组件 conmponent
    Vue.component("componenttest" ,{
        props: ['zc'],
        template: '<li>{{zc}}</li>'
    });

    var vm = new Vue({
        el: "#app",
        data:{
           items: ["Java","Linux","Spring"]
        }
    });
</script>
</body>
</html>
```

**注：component 有2个参数，第一个是名称，第二个是方法体**

**component 不能从 vm 对象中直接取 data 数据，需要在 componenttest自定义组件中进行绑定，componenttest 中 item 是 vm 对象中 items 遍历出来的数据，而需要传递给 component 对象，则需要进行 v-bind 进行绑定，props 的 zc 属性来绑定从 data 遍历后数据的 item（也可以理解为 item 为形参，zc 为实参）**

### 网络通信

##### 什么是Axios

​	Axios 是一个开源的可以用在浏览器端和 NodeJS 的异步通信框架，它的主要作用就是实现 AJAX 异步通信，其功能特点如下：

- 从浏览器中创建 XMLHttpRequests

- 从 node.js 创建 http 请求

- 支持 Promise API [JS中链式编程]

- 拦截请求和响应

- 转换请求数据和响应数据

- 取消请求

- 自动转换 JSON 数据

- 客户端支持防御 XSRF （跨站请求伪造）

  **Github：http://github.com/axios/axios **

  **中文文档：http://www.axios-js.com **

##### 为什么要使用Axios

​	由于Vue.js 是一个 视图层框架 并且作者（尤雨溪）严格遵守 SoC（关注度分离原则），所以 Vue.js 并不包含 AJAX 的通信功能，为了解决通信问题，作者单独开发了一个名为 vue-resource 的插件，不过在进入 2.0 版本以后停止了对该插件的维护并推荐了 Axios 框架，少用 jQuery，因为它操作 DOM 太频繁。

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>demo7</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>

    <!-- v-clock: 解决闪烁问题 -->
    <style>
        [v-clock]{
            display: none;
        }
    </style>
</head>
<body>
<!-- view层 模板 -->
<div id="vue" v-clock>
    <div>{{info.name}}</div>
    <div>{{info.address.city}}</div>
    <a v-bind:href="info.url">点我</a>
</div>

<script>
    var vm = new Vue({
        el: "#vue",
        data(){
            return{
                // 请求的返回参数合适，必须和 json 字符串一样
                info:{

                }
            }
        },
        mounted(){  //钩子函数
            axios.get('../data.json').then(response=>(this.info=response.data));
        }
    });
</script>
</body>
</html>
```

### Vue 计算属性

​	计算属性的重点突出在 **属性** 两个字上（属性是名词），首先它是个 **属性** 其次这个属性有 **计算** 的能力（计算是动词），这里的 **计算** 就是个函数；简单点说，它就是一个能够将计算结果缓存起来的属性（将行为转化成了静态的属性），仅此而已；可以想象为缓存。

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>demo8</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
</head>
<body>
<!-- view层 模板 -->
<div id="app">
    <p>{{currentTime1()}}</p>
    <br/>
    <p>{{currentTime2}}</p>
</div>

<script>
    var vm = new Vue({
        el: "#app",
        data:{
            message: "hello,world"
        },
        methods: {
            currentTime1: function() {
                return Date.now(); //返回一个时间戳
            }
        },
        computed: { // 计算属性 :  methods 和 computed 中的方法名不能重名,重名后只会执行 methods 的方法
            currentTime2: function() {
                return Date.now(); //返回一个时间戳
            }
        }
    });
</script>
</body>
</html>
```

**methods 和 computer 的区别**

- methods：定义方法，调用方法使用 currentTime1()，需要带括号
- computed：定义计算属性，调用属性使用 currentTime2，不需要代口号；this.message 是为了能够让 currentTime2 观察到数据变化而变化
- 如何在方法中的值发生了变化，则缓存就会刷新！可以在控制台中更改 message 的值，**vm.message="abc"**，改变下数据的值，再次测试观察效果

**结论**

​	调用方法时，每次都需要进行计算，既然有计算过程则必定产生系统开销，那如果这个结果时不经常变化的呢？此时就可以考虑将这个结果缓存起来，采用计算属性可以很方便的做到这一点，**计算属性的主要特性就是为了将不经常变化的计算结果进行缓存，以节约我们的系统开销；**

### 内容分发

​	在 Vue.js 中我们使用 <slot> 元素作为承载分发内容的出口，作者称其为 插槽，可以在应用在组合组件的场景中；

> 测试

​	比如准备制作一个待办事项组件（todo），该组件由代办标题（todo-title）和待办内容（todo-items）组成，但这三个组件又是互相独立的，该如何操作呢

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>demo9</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
</head>
<body>
<!-- view层 模板 -->
<div id="app">
    <todo>
        <todo-title slot="todo-title" v-bind:title="title"></todo-title>
        <todo-items slot="todo-items" v-for="num in todoItems" v-bind:item="num"></todo-items>
    </todo>
</div>

<script>

    //slot： 插槽
    Vue.component("todo",{
        template:'<div>\
                        <slot name="todo-title"></slot>\
                        <ul>\
                            <slot name="todo-items"></slot>\
                        </ul>\
                  </div>'
    });

    Vue.component("todo-title",{
        props: ['title'],
        template: '<div>{{title}}</div>'
    });

    Vue.component("todo-items",{
        props: ['item'],
        template: '<li>{{item}}</li>'
    });

    var vm = new Vue({
        el: "#app",
        data: {
            title: "列表",
            todoItems: ['Vue','Java','Linux']
        }
    });
</script>
</body>
</html>
```

### 自定义事件

​	数据项在 Vue 的实例中，但删除操作需要在组件中完成，那么组件如何才能删除 Vue 实例中的数据呢？此时就涉及到参数传递与事件分发了，Vue 为我们提供了自定义事件的功能很好的帮助我们解决了这个问题；使用 **this.$emit('自定义事件名,参数')**

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>demo9</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
</head>
<body>
<!-- view层 模板 -->
<div id="app">
    <todo>
        <todo-title slot="todo-title" v-bind:title="title"></todo-title>
        <todo-items slot="todo-items" v-for="(item,index) in todoItems"
                    v-bind:item="item" :index="index" @remove="removeItems(index)"></todo-items>
    </todo>
</div>

<script>

    //slot： 插槽
    Vue.component("todo",{
        template:'<div>\
                        <slot name="todo-title"></slot>\
                        <ul>\
                            <slot name="todo-items"></slot>\
                        </ul>\
                  </div>'
    });

    Vue.component("todo-title",{
        props: ['title'],
        template: '<div>{{title}}</div>'
    });

    Vue.component("todo-items",{
        props: ['item','index'],
        template: '<li>{{item}}<input type="button" @click="remove" value="删除"></li>',
        methods: {
            remove: function(index) {
                alert("进入remove方法体");
                // 自定义事件分发
                this.$emit('remove',index);
            }
        }
    });

    var vm = new Vue({
        el: "#app",
        data: {
            title: "列表",
            todoItems: ['Vue','Java','Linux']
        },
        methods: {
            removeItems: function(index) {
                alert("进入 removeItems 方法体");
                console.log("删除了" + this.todoItems[index] + "OK");
                this.todoItems.splice(index,1);
            }
        }
    });
</script>
</body>
</html>
```

### 什么是vue-cli

vue-cli 是官方提供的一个脚手架，用于快速生成一个 vue 的项目模板；

预先定义好的目录结构及基础代码，就好比在创建 Maven 项目时可以选择创建一个骨架项目，这个骨架项目就是脚手架，让我们的开发更加的快速

**主要的功能：**

- 统一的目录结构
- 本地调试
- 热部署
- 单元测试
- 集成打包上线

##### 需要的环境

- Node.js：http://nodejs.cn/download/

  ps：安装就无脑下一步就好，安装在自己的环境目录下

- Git：https://git-scm.com/downloads

  镜像：https://npm.taobao.org/mirrors/git-for-windows/

##### 确认nodejs安装成功：

- cmd 下输入 `node -v`，查看是否能够正确打印出版本号即可

- cmd 下输入 `npm-v`，查看是否能够正确打印出版本号即可

  npm就是一个软件包管理工具，和linux下的 apt 软件安装差不多

##### 安装 Node.js 淘宝镜像加速器（cnpm）

```shell
# -g 就是全局安装
npm install cnpm -g

# 或使用如下语句解决 npm 速度慢的问题
npm install --registry=https://registry.npm.taobao.org
```

**安装后的位置：C:\Users\Administrator\AppData\Roaming\npm**

![](http://zhaocan.fym233.cn/20210121155423.jpg)

##### 安装 vue-cli

```shell
cnpm install vue-cli -g

# 测试是否安装成功
# 查看可以基于哪些模板创建 vue 应用，通常选择 webpack
vue list
```

![](http://zhaocan.fym233.cn/20210121155958.jpg)

### 创建一个 vue-cli 应用程序

**1、创建一个 Vue 项目，随便建立一个空的文件夹在电脑上**

```shell
E:\tools\Vue-project\Vue-study;
```

**2、创建一个基于 webpack 模板的 vue 应用程序**

```shell
# 这里的 myvue 时项目名称
vue init webpack myvue
```

一路都选择 no 即可；

**说明：**

- Project name：项目名称，默认 回车 即可
- Project description：项目描述，默认 回车 即可
- Author：项目作者，默认 回车 即可
- Install vue-router：是否安装 vue-router，选择 n 不安装（后期需要再手动添加）
- Use ESLint to lint your code：是否使用 ESLint 做代码检查，选择 n 不安装（后期需要再手动添加）
- Set up unit tests：单元测试相关，选择 n 不安装（后期需要再手动添加）
- Setup e2e tests with Nightwatch：单元测试相关，选择 n 不安装（后期需要再手动添加）
- Should we run npm install for you after the project has been created：创建完成后直接初始化，选择 n ，我们手动执行。

运行结果：

![](http://zhaocan.fym233.cn/20210121161548.jpg)

### 初始化并运行

```shell
cd myvue
npm install
npm run dev
```

执行完成后，目录多了很多依赖

![](http://zhaocan.fym233.cn/20210121161850.jpg)

**export：导出**

**import：导入**

### 什么是 Webpack

​	本质上，webpack 是一个现代 JavaScript 应用程序的静态模块打包器（module bundler）。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图（dependency graph），其中包含应用程序需要的每个模块，然后将虽有这些模块打包成一个或多个 bundle。

​	Webpack 是当下最热门的前端资源模块化管理和打包工具，它可以将许多松散耦合的模块按照依赖和规则打包成符合生产环境部署的前端资源。还可以将按需加载的模块进行代码分离，等到实际需要时再异步加载。通过 loader 转换，任何形式的资源都可以当作模块，比如 CommonsJS、AMD、ES6、CSS、JSON、CoffeeScript、LESS等；

​	伴随着移动互联网的大潮，当今越来越多的网站已经从网页模式进化到了 WebApp 模式。它们运行在现代浏览器里，使用 HTML5、CSS3、ES6 等新的技术来开发丰富的功能，网页已经不仅仅是完成浏览器的基本需求；WebApp 通常是一个 SPA（单页面应用），每一个视图通过异步的方式加载，这导致页面初始化和应用过程中会加载越来越多的 JS 代码，这给前端的开发流程和资源组织带来了巨大挑战。

​	前端开发和其他开发工作的主要区别，首先是前端基于多语言、多层次的编码和组织工作，其次前端产品的交付是基于浏览器的，这些资源是通过增量加载的方式运行到浏览器端，如何在开发环境组织好这些碎片化的代码和资源，并且保证他们在浏览器端快速、优雅的加载和更新，就需要一个模块化系统，这个理想中的模块化系统是前端工程师多年来一直探索的难题。

##### 模块化的演进

###### Script标签

```javascript
<script src="module1.js"></script>
<script src="module2.js"></script>
<script src="module3.js"></script>
<script src="module4.js"></script>
```

​	这是最原始的 JavaScript 文件加载方式，如果吧每一个文件看作是一个模块，那么它们的接口通常是暴露在全局作用域下，也就是定义在 window 对象中，不同模块的调用都是一个作用域。

​	这种原始的加载方式暴露了一些显而易见的弊端：

- 全局作用域下容易造成变量冲突
- 文件只能按照 `<script>` 的书写顺序进行加载
- 开发人员必须主观解决模块和代码库的依赖关系
- 在大型项目中各种资源难以管理，长期积累的问题导致代码库混乱不堪

###### CommonsJS

​	服务器端的 NodeJS 遵循 CommonsJS 规范，该规范核心思想是允许模块通过 require 方法来同步加载所需依赖的其他模块，然后通过 exports 或 module.exports 来导出需要暴露的接口。

```javascript
require("module");
require("../module.js");
export.doStuff = function() {};
module.exports = someValue;
```

**优点：**

- 服务器端模块便于重用
- NPM 中已经有超过 45 万个可以使用的模块包
- 简单易用

**缺点：**

- 同步的模块加载方式不适合在浏览器环境中，同步意味着阻塞加载，浏览器资源是异步加载的
- 不能非阻塞的并行加载多个模块

**实现：**

- 服务端的 NodeJS
- Browserify，浏览器端的 CommonsJS 实现，可以使用 NPM 的模块，但是编译打包后的文件体积较大
- modules-webmake，类似 Browserify，但不如 Browserify 灵活
- wreq，Browserify 的前身

###### AMD

​	Asynchronous Module Definition 规范其实主要一个主要接口 define(id?,dependencies?,factory)；它要在声明模块的时候指定所有的依赖 dependencies，并且还要当作形参传到 factory 中，对于依赖的模块提前执行。

```javascript
define("module",["dep1","dep2"], function(d1, d2){
   return someExportedValue; 
});
require(["module","../file.js"], function(module, file) {});
```

**优点：**

- 适合在浏览器环境中异步加载模块
- 可以并行加载多个模块

**缺点：**

- 提高了开发成本，代码的阅读和书写比较困难，模块定义方式的语义不畅
- 不符合通用的模块化思维方式，是一种妥协的实现

**实现：**

- RequireJS
- curl

###### CMD

​	Commons Module Definition 规范和 AMD 很相似，尽量保持简单，并与 CommonsJS 和 NodeJS 的 Modules 规范保持了很大的兼容性。

```javascript
define(function(require, exports, module) {
    var $ = require("jquery");
    var Spinning = require("./spinning");
    exports.doSomething = ...;
    module.exports = ...;
})
```

**优点：**

- 依赖就近，延迟执行
- 可以很容易在 NodeJS 中运行

**缺点：**

- 依赖 SPM 打包，模块的加载逻辑偏重

**实现：**

- Sea.js
- coolie

###### ES6 模块

​	EcmaScript6 标准增加了 JavaScript 语言层面的模块体系定义。ES6 模块的设计思想，是尽量静态化，使编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonsJS 和 AMD 模块，都只能在运行时确定这些东西。

```javascript
import "jquery"
export function doStuff() {}
module "localModule" {}
```

**优点：**

- 容易进行静态分析
- 面向未来的 EcmaScript 标准

**缺点：**

- 原生浏览器端还没有实现该标准
- 全新的命令，新版的 NodeJS 才支持

**实现：**

- Babel

**大家期望的模块系统**

​	可以兼容多种模块风格，尽量可以利用已有的代码，不仅仅只是 JavaScript 模块化，还有 CSS、图片、字体等资源也需要模块化。

### 安装 Webpack

​	WebPack 是一款模块加载器兼打包工具，它能把各种资源，如 JS、JSX、ES6、SASS、LESS、图片等都作为模块来处理和使用。

##### 安装

```shell
npm install webpack -g
npm install webpack-cli -g
```

测试安装成功：

- `webpack -v`
- `webpack-cli -v`

![](http://zhaocan.fym233.cn/20210122110228.jpg)

##### 配置

​	创建 `webpack.config.js` 配置文件

- entry：入口文件，指定 WebPack 用哪个文件作为项目的入口
- output：输出，指定 WebPack 把处理完成的文件放置到指定路径
- module：模块，用于处理各种类型的文件
- plugins：插件，如：热更新、代码重用等
- resolve：设置路径指向
- watch：监听，用于设置文件改动后直接打包

```javascript
module.exports = {
    entry: "",
    output: {
        path: "",
        filename: ""
    },
    module: {
        loaders: [
            {test: /\.js$/, loader: ""}
        ]
    },
    plugins: {},
    resolve: {},
    watch: true
}
```

​	**直接运行 `webpack` 命令打包**

### 使用 WebPack

1、创建项目

2、创建一个名为 modules 的目录，用于放置 JS 模块等资源文件

3、在 modules 下创建模块文件，如 hello.js，用于编写 JS 模块相关代码

```javascript
// 暴露一个方法：sayHi
exports.sayHi = function() {
    document.write("<div>Hello WebPack</div>")
}
```

4、在 modules 下创建一个名为 main.js 的入口文件，用于打包时设置 entry 属性

```javascript
// require 导入一个模块，就可以调用这个模块中的方法了
var hello = require("./hello");
hello.sayHi();
```

5、在项目目录下创建 webpack.config.js 配置文件，使用 webpack 命令打包

```javascript
module.exports = {
    entry: "./modules/main.js",
    output: {
        filename: "./js/bundle.js"
    }
};
```

6、在项目目录下创建 HTML 页面，如 index.html，导入 WebPack 打包后的 JS 文件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <!-- 前端的模块化开发 -->
    <script src="dist/js/bundle.js"></script>
</head>
<body>

</body>
</html>
```

7、在 IDEA 控制台中直接执行 webpack；如果失败的话，就使用管理员权限运行即可

![](http://zhaocan.fym233.cn/20210122154127.png)

8、运行 HTML 看效果

![](http://zhaocan.fym233.cn/20210122154234.png)

**说明：**

```shell
# 参数 --watch 用于监听变化
webpack --watch
```

### vue-router路由

​	Vue Router 是 Vue.js 官方的路由管理器。它和 Vue.js 的核心深度集成，让构建单页面应用变得易如反掌，包含的功能有：

- 嵌套的路由/视图表
- 模块化的、基于组件的路由配置
- 路由参数、查询、通配符
- 基于 Vue.js 过滤系统的视图过度效果
- 细粒度的导航控制
- 带有自动激活的 CSS class 的链接
- HTML5 历史模式或 hash 模式，在 IE9 中自动降级
- 自定义的滚动条行为

##### 安装

​	**基于第一个 vue-cli 进行测试学习；先查看 node_modules 中是否存在 vue-router**

​	vue-router 是一个插件包，所以还是需要用 `npm/cnpm` 来进行安装的。打开命令行工具，进入项目目录，输入一下命令。

```shell
npm install vue-router --save-dev
```

​	如果在一个模块化工程中使用它，必须要通过 Vue.use() 明确地安装路由功能：

```javascript
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter);
```

##### 测试

1、先删除没有用的东西

2、`components` 目录下存放自己编写的组件

3、定义一个 Content.vue 的组件

```vue
<template>
  <h1>内容页</h1>
</template>

<script>
  export default {
    name: "Content"
  }
</script>

<style scoped>

</style>
```

4、安装路由，在 src 目录下，新建一个文件夹：`router`，专门存放路由

```javascript
import Vue from 'vue';
// 导入路由插件
import VueRouter from "vue-router";

// 导入上面定义的组件
import Content from "../components/Content";
import Main from "../components/Main";

// 安装路由
Vue.use(VueRouter);

// 配置路由
export default new VueRouter({
  routes: [
    {
      // 路由的路径
      path: '/content',
      // 路由名称
      name: 'content',
      //跳转的组件
      component: Content
    },
    {
      // 路由的路径
      path: '/main',
      // 路由名称
      name: 'main',
      //跳转的组件
      component: Main
    }
  ]
});
```

5、在 `main.js` 中配置路由

```javascript
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import App from './App'

// 导入上面创建的路由配置目录（自动扫描里面的路由配置）
import router from './router'

// 关闭生产模式下给出的提示
Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  // 配置路由
  router,
  components: {App},
  template: '<App/>'
})
```

6、在 `App.vue` 中使用路由

```vue
<template>
  <div id="app">
    <h1>Vue-Router</h1>
    <router-link to="/main">首页</router-link>
    <router-link to="/content">内容</router-link>
    <router-view></router-view>
  </div>
</template>

<script>
  export default {
    name: 'App'
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
```

### 整合 ElementUI

##### 创建工程

​	注：命令行都要使用管理员模式运行

1、创建一个名为 vue-elementui 的工程 `vue init webpack vue-elementui`

2、安装依赖，我们需要安装 vue-router、element-ui、sass-loader 和 node-sass 四个插件

```shell
# 进入工程目录
cd vue-elementui
# 安装 vue-router
npm install vue-router --save-dev
# 安装 element-ui
npm i element-ui -S
# 安装依赖
npm install
# 安装 SASS 加载器
cnpm install sass-loader node-sass --save-dev
# 启动测试
npm run dev
```

3、Npm 命令解释：

- `npm install moduleName`：安装模块到项目目录下
- `npm install -g moduleNmae`：-g 的意思是将模块安装到全局，具体安装到磁盘哪个位置，要看 npm config prefix 的位置
- `npm install -save moduleName`：--save 的意思是将模块安装到项目目录下，并在 package 文件的 dependencies 节点写入依赖，-S 为该命令的缩写
- `npm install --save-dev moduleName`：--save-dev 的意思是将模块安装到项目目录下，并在 package 文件的 devDependevcies 节点写入依赖，-D 为该命令的缩写

##### 创建登录页面

​	源码目录中创建如下结构：

- assets：用于存放资源文件
- components：用于存放 Vue 功能组件
- views：用于存放 Vue 视图组件
- router：用于存放 vue-router 配置

![](http://zhaocan.fym233.cn/20210127142541.png)

**创建首页视图，在 views 目录下创建一个名为 Main.vue 的视图组件**

```vue
<template>
    <h1>首页</h1>
</template>

<script>
    export default {
        name: "Main"
    }
</script>

<style scoped>

</style>
```

**创建登录页面视图在 views 目录下创建一个名为 Login.vue 的视图组件，其中 el-* 的元素为 ElementUI 组件**

```vue
<template>
    <div>
      <el-form ref="loginForm" :model="form" :rules="rules" label-width="80px" class="login-box">
        <h3 class="login-title">欢迎登陆</h3>
        <el-form-item label="账号" prop="username">
          <el-input type="text" placeholder="请输入账号" v-model="form.username" />
        </el-form-item>
        <el-form-item label="密码" prop="password">
          <el-input type="password" placeholder="请输入密码" v-model="form.password" />
        </el-form-item>
        <el-form-item>
          <el-button type="primary" v-on:click="onSubmit('loginForm')">登录</el-button>
        </el-form-item>
      </el-form>

      <el-dialog
        title="温馨提示"
        :visible.sync="dialogVisible"
        width="30%"
        :before-close="handleClose">
        <span>请输入账号和密码</span>
        <span slot="footer" class="dialog-footer">
          <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
        </span>
      </el-dialog>
    </div>
</template>

<script>
    export default {
        name: "Login",
        data() {
          return {
            form: {
              username: '',
              password: ''
            },

            // 表单验证，需要在 el-form-item 元素中加入 prop 属性
            rules: {
              username: [
                {required: true, message: '账号不可为空', trigger: 'blur'}
              ],
              password: [
                {required: true, message: '密码不可为空', trigger: 'blur'}
              ]
            },

            // 对话框显示和隐藏
            dialogVisible: false
          }
        },
      methods: {
          onSubmit(formName) {
            // 为表单绑定验证功能
            this.$refs[formName].validate((valid) => {
              if (valid) {
                // 使用 vue-router 路由到指定页面，该方式称之为编程式导航
                this.$router.push("/main");
              } else {
                this.dialogVisible = true;
                return false;
              }
            });
          }
      }
    }
</script>

<style lang="scss" scoped>
  .login-box {
    border: 1px solid #DCDFE6;
    width: 350px;
    margin: 180px auto;
    padding: 35px 35px 15px 35px;
    border-radius: 5px;
    -webkit-border-radius: 5px;
    -moz-border-radius: 5px;
    box-shadow: 0 0 25px #909399;
  }

  .login-title {
    text-align: center;
    margin: 0 auto 40px auto;
    color: #303133;
  }
</style>
```

**配置 main.js**

```javascript
import Vue from 'vue'
import App from './App'

import router from './router'

// 引入ElementUI
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css';

// 安装路由
Vue.use(router);

// 安装ElementUI
Vue.use(ElementUI);

new Vue({
  el: '#app',
  // 启用ElementUI
  render: h => h(App),  // ElementUI
  //启用路由
  router
})
```

**修改 App.vue 组件代码**

```vue
<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>

export default {
  name: 'App',
}
</script>

<style>
</style>
```

​	测试：在浏览器打开 `http://localhost:8080/#/login`

​	如果出现错误：可能是因为 sass-loader 的版本过高导致的编译错误，当前最高版本是10.x，需要退回到7.3.1

​	去 package.json 文件里面的 "sass-loader" 的版本更换成7.3.1，然后重新 `cnpm install` 就可以了

![](http://zhaocan.fym233.cn/20210127152513.png)

### 路由嵌套

​	嵌套路由又称子路由，在实际应用中，通常由多层嵌套的组件组合而成。同样地，URL 中各段动态路径也按某种结构对应嵌套的各层组件，例如：

![](http://zhaocan.fym233.cn/20210127152734.png)

1、用户信息组件，在 views/user 目录下创建一个名为 Profile.vue 的视图组件

```vue
<template>
    <h1>
      个人信息
    </h1>
</template>

<script>
    export default {
        name: "UserProfile"
    }
</script>

<style scoped>

</style>
```

2、用户列表组件在 views/user 目录下创建一个名为 List.vue 的视图组件

```vue
<template>
    <h1>
      用户列表
    </h1>
</template>

<script>
    export default {
        name: "UserList"
    }
</script>

<style scoped>

</style>
```

3、配置嵌套路由修改 router 目录下的 index.js 路由配置文件，代码如下

```javascript
import Vue from 'vue'
import Router from 'vue-router'

import Main from '../views/Main'
import Login from "../views/Login";

import UserProfile from "../views/user/Profile";
import UserList from "../views/user/List";

Vue.use(Router);

export default new Router({
  routes: [
    {
      path: '/main',
      name: 'main',
      component: Main,
      // 嵌套路由
      children: [
        {
          path: '/user/profile',
          name: 'profile',
          component: UserProfile
        },
        {
          path: '/user/list',
          name: 'list',
          component: UserList
        }
      ]
    },
    {
      path: '/login',
      name: 'login',
      component: Login,
    }
  ]
})
```

4、在 Main.vue 中加入嵌套的路由

```vue
<template>
    <div>
      <el-container>
        <el-aside width="200px">
          <el-menu :default-openeds="['1']">
            <el-submenu index="1">
              <template slot="title"><i class="el-icon-caret-right"></i>用户管理</template>
              <el-menu-item-group>
                <el-menu-item index="1-1">
                  <router-link to="/user/profile">个人信息</router-link>
                </el-menu-item>
                <el-menu-item index="1-2">
                  <router-link to="/user/list">用户列表</router-link>
                </el-menu-item>
                <el-menu-item index="1-3">
                  <router-link to="/goHome">回到首页</router-link>
                </el-menu-item>
              </el-menu-item-group>
            </el-submenu>
            <el-submenu index="2">
              <template slot="title"><i class="el-icon-caret-right"></i>内容管理</template>
              <el-menu-item-group>
                <el-menu-item index="2-1">分类管理</el-menu-item>
                <el-menu-item index="2-2">内容列表</el-menu-item>
              </el-menu-item-group>
            </el-submenu>
          </el-menu>
        </el-aside>

        <el-container>
          <el-header style="text-align: right; font-size: 12px">
            <el-dropdown>
              <i class="el-icon-setting" style="margin-right: 15px"></i>
              <el-dropdown-menu slot="dropdown">
                <el-dropdown-item>个人信息</el-dropdown-item>
                <el-dropdown-item>退出登录</el-dropdown-item>
              </el-dropdown-menu>
            </el-dropdown>
          </el-header>

          <el-main>
            <router-view />
          </el-main>
        </el-container>
      </el-container>
    </div>
</template>

<script>
    export default {
        name: "Main"
    }
</script>

<style scoped lang="css">
  .el-header {
    background-color: #B3C0D1;
    color: #333;
    line-height: 60px;
  }

  .el-aside {
    color: #333;
  }
</style>
```

4、在 main.js 中配置路由及ElementUI

```javascript
import Vue from 'vue'
import App from './App'

import router from './router'

// 引入ElementUI
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css';

// 安装路由
Vue.use(router);

// 安装ElementUI
Vue.use(ElementUI);

new Vue({
  el: '#app',
  // 启用ElementUI
  render: h => h(App),  // ElementUI
  //启用路由
  router
})
```

### 传递参数

##### 方式一

1、在 `<router-link>` 中的 `to` 传递参数

```vue
<!-- name:地址  params:传递参数 -->
<router-link v-bind:to="{name:'/user/profile', params:{id:1}}"></router-link>
```

2、在 index.js 的路由配置中接收参数

```javascript
import Vue from 'vue'
import Router from 'vue-router'

import Main from '../views/Main'
import Login from "../views/Login";

import UserProfile from "../views/user/Profile";
import UserList from "../views/user/List";

Vue.use(Router);

export default new Router({
  routes: [
    {
      path: '/main',
      name: 'main',
      component: Main,
      // 嵌套路由
      children: [
        {
          path: '/user/profile/:id',	//接收参数
          name: 'profile',
          component: UserProfile
        },
        {
          path: '/user/list',
          name: 'list',
          component: UserList
        }
      ]
    },
    {
      path: '/login',
      name: 'login',
      component: Login,
    },
    {
      path: '/goHome',
      redirect: Main
    }
  ]
})
```

3、在 Profile.vue 中渲染数据

```vue
<template>
    <h1>
      个人信息
      <p>{{$route.params.id}}</p>
    </h1>
</template>

<script>
    export default {
        name: "UserProfile"
    }
</script>

<style scoped>

</style>
```

**注：所有的元素不能在根节点下**

##### 方式二

1、在 `<router-link>` 中的 `to` 传递参数

```vue
<!-- name:地址  params:传递参数 -->
<router-link v-bind:to="{name:'/user/profile', params:{id:1}}"></router-link>
```

2、在 index.js 的路由配置中接收参数，并允许通过 props 传递参数

```javascript
import Vue from 'vue'
import Router from 'vue-router'

import Main from '../views/Main'
import Login from "../views/Login";

import UserProfile from "../views/user/Profile";
import UserList from "../views/user/List";

Vue.use(Router);

export default new Router({
  routes: [
    {
      path: '/main',
      name: 'main',
      component: Main,
      // 嵌套路由
      children: [
        {
          path: '/user/profile/:id',	//接收参数
          name: 'profile',
          component: UserProfile,
          props: true  
        },
        {
          path: '/user/list',
          name: 'list',
          component: UserList
        }
      ]
    },
    {
      path: '/login',
      name: 'login',
      component: Login,
    },
    {
      path: '/goHome',
      redirect: Main
    }
  ]
})
```

3、在 Profile.vue 中渲染数据

```vue
<template>
    <h1>
      个人信息
      <p>{{id}}</p>
    </h1>
</template>

<script>
    export default {
        props: ['id'],
        name: "UserProfile"
    }
</script>

<style scoped>

</style>
```

### 重定向

配置 index.js 中的 `path`，并写入 `redirect`

```javascript
import Vue from 'vue'
import Router from 'vue-router'

import Main from '../views/Main'
import Login from "../views/Login";

import UserProfile from "../views/user/Profile";
import UserList from "../views/user/List";

Vue.use(Router);

export default new Router({
  routes: [
    {
      path: '/main',
      name: 'main',
      component: Main,
      // 嵌套路由
      children: [
        {
          path: '/user/profile/:id',
          name: 'UserProfile',
          component: UserProfile
        },
        {
          path: '/user/list',
          name: 'UserList',
          component: UserList
        }
      ]
    },
    {
      path: '/login',
      name: 'login',
      component: Login,
    },
    {
      path: '/goHome',	
      redirect: Main	// 配置重定向
    }
  ]
})
```

在 main.vue 中配置 `/goHome`

```vue
<el-menu-item index="1-3">
	<router-link to="/goHome">回到首页</router-link>
</el-menu-item>
```

### 路由模式与404

路由模式有两种

- hash：路径带 `#` 符号，如：http://localhost/#/login
- history：路径不带 `#` 符号，如：http://localhost/login

修改路由配置，代码如下：

```javascript
export default new Router({
	mode: 'history',
    routes: [
        
    ]
})
```

​	处理 404 创建一个名为 `NotFound.vue` 的视图组件

```vue
<template>
    <h1>404，你的页面走丢了</h1>
</template>

<script>
    export default {
        name: "NotFound"
    }
</script>

<style scoped>

</style>
```

修改路由配置

```javascript
import NotFound from "../views/NotFound";

{
      path: '*',
      component: NotFound
}
```

### 路由钩子与异步请求

**`beforeRouteEnter`：在进入路由前执行**

**`beforeRouteLeave`：在离开路由前执行**

代码如下：

```javascript
export default {
      props: ['id'],
      name: "UserProfile",
      beforeRouteEnter: (to, from, next) => {
        console.log("准备进入个人信息页");
        next();
      },
      beforeRouteLeave: (to, from, next) => {
        console.log("准备离开个人信息页");
        next();
      }
    }
```

参数说明：

- to：路由将要跳转的路径信息
- from：路径跳转前的路径信息
- next：路由的控制参数
  - next() 跳入下一个页面
  - next(/path) 改变路由的跳转方向，使其跳到另一个路由
  - next(false) 返回原来的页面
  - next((vm) => {}) 仅在 `beforeRouteEnter` 中可用，vm 是组件实例

##### 在钩子函数中使用异步请求

1、安装 Axios `cnpm install axios -s`

2、main.js 引入 Axios

```javascript
import axios from 'axios'
Vue.prototype.axios = axios;
```

3、准备数据：只有 static 目录下的文件是可以被访问到的，所以将静态文件放入该目录下

![](http://zhaocan.fym233.cn/20210128151432.png)

4、访问 `localhost:8080/static/mock/data.json` 查看数据

![](http://zhaocan.fym233.cn/20210128151433.png)