# web路线--极简教程

本文主要带大家从前端到后端简单走一遍，目的是形成一些概念，遇到问题知道解决的方向。并非系统教学，但也足够应付日常开发需求

讨论范围：在浏览器中运行的Web应用



## 一个网站大多数时候都在做什么？

1. 展示内容、提供用户一个图形化操作界面
2. 网页向后端发送请求：问服务器要东西（文本、图片、视频、音频，或是什么奇奇怪怪的文件）；提交一些信息给服务器进行处理，对服务器返回的信息进行处理
3. 后端服务器处理请求：给出前端要的东西；对前端提交的信息进行处理（比如：存入服务器上的数据库）



## 浏览器

主流浏览器：Edge，Chrome，Safari，Firefox，Opera

![StatCounter-browser-ww-monthly-201806-201906-bar](http://storage.szulib.top/szulib/image-hosting/StatCounter-browser-ww-monthly-201806-201906-bar.png)



Chrome 已经多年占有率第一了，大多数国产浏览器都是基于 [Chromium](https://www.chromium.org/) 内核进行开发，如今连 Edge 也采用了Chromium 内核，这足以说明这个...历史的潮流已经无法阻挡。所以我们就面向 Chrome 进行开发就完事了，不考虑不同浏览器的兼容性问题。

[下载 Chrome (官网)](https://www.google.com/intl/zh-CN/chrome/)

[下载Chrome安装程序](http://172.30.234.8:8001/szulib/software/ChromeSetup.exe)（校园网访问）

### 浏览器的工作

简单讲，浏览器主要干三件事情：

1. 处理网络请求
2. 渲染页面
3. JS引擎运行js代码

当浏览器从输入的 url 地址下载到资源（HTML/CSS/JS代码/图片）后，对代码进行解析[^1]，渲染成我们看到的可交互页面。

[^1]:“解析”是浏览器将通过网络接收的数据转换为DOM和CSSOM的步骤，通过渲染器把DOM和CSSOM在屏幕上绘制成页面。



### DevTools

[Chrome DevTools Doc](https://developer.chrome.com/docs/devtools/)

浏览器中的网页开发者工具

在浏览器中打开一个网页，按 `F12` 出现开发者工具。

![image-devtools](http://storage.szulib.top/szulib/image-hosting/devtools1.png)



可以看到在顶部，有一个菜单栏。一般常用的就是这几个标签项： `Element`、`Console`、`Network`、`Application`

![devtools-topbar](https://storage.szulib.top/szulib/image-hosting/devtools2.png)



**Elements** 

就是如它的名字一般，用于检查元素，可以看到在左边是页面的 html标签信息，右边是css样式信息。可以直接在这个地方修改css样式，修改完可以马上看到变化。

![devtools3](https://storage.szulib.top/szulib/image-hosting/devtools3.png)

例如，我们给百度网页的背景换个颜色

1. 首先 我们访问一下百度 https://www.baidu.com/ ，然后按 `F12` 出现开发者工具。

2. 点击 `Elements` 选项卡，在右边的css信息中找到下面的片段

    ~~~css
    body {
       height: 100%;
       min-width: 1250px;
       cursor: default;
    }    
    ...
    ~~~

3. 点击这个片段，然后添加内容，使之变成：

   ~~~css
   body {
      height: 100%;
      min-width: 1250px;
      cursor: default;
      background: pink;
   }    
   ...
   ~~~

4. 再次按 `F12` 退出开发者工具，可以看到页面已经有了变化

   ![devtools4](https://storage.szulib.top/szulib/image-hosting/devtools4.png)

5. 如果这个时候你刷新页面，所有的更改就会消失，恢复原样。

**Console**

Console翻译一下叫控制台。可以在这里执行js代码，操作网页的文档结构，发送网络请求等等。

![devtools5](https://storage.szulib.top/szulib/image-hosting/devtools5.png)



尝试在 Console 输入： 

~~~js
console.log("hello")
~~~

可以看见控制台输出一个 ` hello `

![devtools6](https://storage.szulib.top/szulib/image-hosting/devtools6.png)



**Note: ** `console.log()` 在调试js代码的时候经常用到。

例如，我们想要修改一下页面的文档结构，给百度页面添加一个写着 Hello baidu 的 ` <p>` 标签

1. 在控制台逐行复制粘贴下面的代码，然后回车。（如果要一次多行输入，可以使用 `Shift` + `Enter` 进行换行）

    ~~~js
    var s_kw_wrap = document.getElementById("s_kw_wrap"); //获取到id为 s_kw_wrap 的元素
    var p = document.createElement('p');				  //创建一个 p 标签
    p.innerText = "Hello baidu";						  //向刚刚创建的p标签中写入字符串“Hello baidu”
    s_kw_wrap.appenChild(p);							  //将刚刚的p标签作为id=s_kw_wrap的元素的子元素加入
    ~~~

2. 结果如下

    ![devtools7](https://storage.szulib.top/szulib/image-hosting/devtools7.png)

    

3. 在 `Elements` 中查找元素，可以看到刚刚添加上的p标签
   
    ![devtools8](https://storage.szulib.top/szulib/image-hosting/devtools8.png)



**Network**

此处可以查看访问网站过程的所有网络请求。

左边的是一个个的网络请求，点击之后可以在右边看到一个请求的详细信息（请求头、源IP、Response...）

![devtools9](https://storage.szulib.top/szulib/image-hosting/devtools9.png)

左上角的这个按钮用于清除网络请求的记录

![devtools10](https://storage.szulib.top/szulib/image-hosting/devtools10.png)

**Application**

在这里查看 localStorage Cookies 等等本地缓存信息

![devtools11](https://storage.szulib.top/szulib/image-hosting/devtools11.png)



**Tip:** 在开发过程中，可能会遇到更改了文件都是在浏览器中刷新页面没有变化的情况。这可能是浏览器缓存策略导致的。我们可以在开发者模式右键熟悉按钮，然后出现下述的选项，点击 `清空缓存并硬性重新加载` 

![devtools12](https://storage.szulib.top/szulib/image-hosting/devtools12.png)





## 开始之前的准备

现在，我们都有了 chrome 浏览器，再准备一个文本编辑器。[Visual Studio Code](https://code.visualstudio.com/)、[Sublime Text](https://www.sublimetext.com)  ...

如果你网络条件不佳，可以使用校园网内的下载链接：

|                           下载链接                           |                             说明                             |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| [VS Code (Mac)](http://172.30.234.8:8001/szulib/software/VSCode-darwin-universal.zip) | [如何安装](https://blog.csdn.net/u014028317/article/details/106089299) |
| [VS Code (Windows)](http://172.30.234.8:8001/szulib/software/VSCodeUserSetup-x64-1.60.2.exe) |      [如何安装](https://www.jianshu.com/p/51dfbe2c9583)      |
| [Sublime Text 3 (Windows)](http://172.30.234.8:8001/szulib/software/Sublime%20Text%20Build%203211%20x64%20Setup.exe) |                     想用自己折腾 （doge                      |
|                        Sublime Text 4                        |                            凑个数                            |
|                             Vim                              |                             凑数                             |

Note: 本文档均使用 VS Code 进行操作。

安装完成后，在 VS Code 中安装以下插件：

[Chinese (Simplified) Language Pack for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-zh-hans) （可选）

[HTML CSS Support](https://marketplace.visualstudio.com/items?itemName=ecmel.vscode-html-css)

[HTML Snippets](https://marketplace.visualstudio.com/items?itemName=abusaidm.html-snippets)

[Auto Close Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-close-tag)

[JavaScript (ES6) code snippets](https://marketplace.visualstudio.com/items?itemName=xabikos.JavaScriptSnippets)

[ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

[Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)

[vscode-icons](https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons) （可选）

完成



## HTML

HTML 不是一门编程语言，而是一种用于定义内容结构的*标记语言*。HTML 由一系列的**元素（elements）**组成，这些元素可以用来包围不同部分的内容，使其以某种方式呈现或者工作。 一对标签可以为一段文字或者一张图片添加超链接，将文字设置为斜体，改变字号，等等。 [source](https://developer.mozilla.org/zh-CN/docs/Learn/Getting_started_with_the_web/HTML_basics) 

例如，键入下面一行内容

~~~html
HJQ的xp非常奇怪
~~~

可以将这行文字封装成一个段落（**p**aragraph）元素来使其在单独一行呈现：

~~~html
<p>HJQ的xp非常奇怪</p>
~~~

让我们深入探索一下这个段落元素。

![html2](https://storage.szulib.top/szulib/image-hosting/html2.png)

这个元素的主要部分有：

1. **开始标签**（Opening tag）：包含元素的名称（本例为 p），被大于号、小于号所包围。表示元素从这里开始或者开始起作用 —— 在本例中即段落由此开始。
2. **结束标签**（Closing tag）：与开始标签相似，只是其在元素名之前包含了一个斜杠。这表示着元素的结尾 —— 在本例中即段落在此结束。初学者常常会犯忘记包含结束标签的错误，这可能会产生一些奇怪的结果。
3. **内容**（Content）：元素的内容，本例中就是所输入的文本本身。
4. **元素**（Element）：开始标签、结束标签与内容相结合，便是一个完整的元素。



元素也可以有属性（Attribute）：

![html3](https://storage.szulib.top/szulib/image-hosting/html3.png)

属性包含了关于元素的一些额外信息，这些信息本身不显现在内容中。本例中，`class` 是属性名称，`editor-note` 是属性的值 。

`class` 属性可为元素提供一个标识名称（方便我们在 css/js 中选中该元素），以便进一步为元素指定样式或进行其他操作时使用。一个元素可以有多个不同的 `class` 



### HTML 文档结构

[source](https://developer.mozilla.org/zh-CN/docs/Learn/Getting_started_with_the_web/HTML_basics#html_%E6%96%87%E6%A1%A3%E8%AF%A6%E8%A7%A3)

现在来看看单个元素如何彼此协同构成一个完整的 HTML 页面。

~~~html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>测试页面</title>
    <link rel="stylesheet" href="">
  </head>
  <body>
    <img src="images/demo.png" alt="测试图片">
  </body>
</html>
~~~

这里有：

- `<!DOCTYPE html>` — 文档类型。混沌初分，HTML 尚在襁褓（大约是 1991/92 年）之时，`DOCTYPE` 用来链接一些 HTML 编写守则，比如自动查错之类。`DOCTYPE` 在当今作用有限，仅用于保证文档正常读取。现在知道这些就足够了。（反正每个html的前面都写这个就对了）
- `<html></html>` — html元素。该元素包含整个页面的内容，也称作根元素。
- `<head></head>` — head元素。该元素的内容对用户不可见，其中包含例如面向搜索引擎的搜索关键字（[keywords](https://developer.mozilla.org/zh-CN/docs/Glossary/Keyword)）、页面描述、CSS 样式表和字符编码声明等。
- `<meta charset="utf-8">` — 该元素指定文档使用 UTF-8 字符编码 ，UTF-8 包括绝大多数人类已知语言的字符。基本上 UTF-8 可以处理任何文本内容，还可以避免以后出现某些问题，没有理由再选用其他编码。
- `<title></title>` — title元素。该元素设置页面的标题，显示在浏览器标签页上，也作为收藏网页的描述文字。
- `<body></body>` — body元素。该元素包含期望让用户在访问页面时看到的内容，包括文本、图像、视频、游戏、可播放的音轨或其他内容。



### 各种HTML标签

~~~html
<!DOCTYPE html>

<html>
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <title>demo</title>
        <meta name="keywords" content="keyword1, keyword2">
        <meta name="description" content="...">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="stylesheet" href="">
    </head>
    <body>
        <h1>这是h1</h1>
        <h2>这是h2</h2>
        <h3>h3</h3>
        <h4>h4</h4>
        <h5>h5</h5>
        <h6>h6</h6>
        <p>这是一个p标签</p>

        <div>我是一个div:用于内容区域的划分</div>
        <nav>我是一个nav</nav>
        <footer>我是一个footer</footer>
        <article>我是一个article</article>
        <section>我是一个section</section>

        <div>
            <a href="#">a标签</a>
            <br/> <!-- br是换行 -->    
            <a href="http://www.baidu.com">baidu</a>            
        </div>

        <div>
            <p>下面是一张图片</p>
            <img src="https://www.google.com.hk/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png" width="200" alt="无法加载图片时，你会看到我">
        </div>
        
        <ul>
            <li>无序列表1</li>
            <li>无序列表2</li>
            <li>无序列表3</li>
            <li>无序列表4</li>
            <li>无序列表5</li>
            <li>无序列表6</li>
        </ul>

        <ol>
            <li>有序列表1</li>
            <li>有序列表2</li>
            <li>有序列表3</li>
            <li>有序列表4</li>
            <li>有序列表5</li>
            <li>有序列表6</li>
        </ol>

        <div>
            <button>button</button>
        </div>

        <div>
            <strong>各种input</strong>
            <div>
                <label for="username">User Name</label>
                <input type="text" id="username" name="uname" required placeholder="文本输入框">
            </div>
            <div>
                <label for="passwd">Password</label>
                <input type="password" id="passwd" required placeholder="密码输入框">
            </div>
    
            <div>
                <p>自律的大学生</p>
                <input type="checkbox" id="cbox1" name="checkbox1" checked>
                <label for="checkbox1">吃饭</label>

                <input type="checkbox" id="cbox2" name="checkbox2">
                <label for="checkbox2">睡觉</label>

                <input type="checkbox" id="cbox3" name="checkbox3">
                <label for="checkbox3">玩游戏</label>

                <input type="checkbox" id="cbox4" name="checkbox4">
                <label for="checkbox4">刷b站</label>

                <input type="checkbox" id="cbox5" name="checkbox5" disabled>
                <label for="checkbox4">学习</label>

            </div>

            <div style="margin-bottom: 20px;">
                <p>你每天睡多少小时:</p>

                <div>
                    <input type="radio" id="fiveH" name="sleep" value="5" checked>
                    <label for="fiveH">5 hours</label>
                </div>

                <div>
                    <input type="radio" id="sevenH" name="sleep" value="7">
                    <label for="sevenH">7 hours</label>
                </div>

                <div>
                    <input type="radio" id="tenH" name="sleep" value="10">
                    <label for="tenH">10 hours</label>
                </div>
            </div>
        </div >

        <div>
            <label for="select">你有几个儿子:</label>

            <select name="pets" id="select">
                
                <option value="dog">0</option>
                <option value="cat">1</option>
                <option value="hamster">2</option>
                <option value="parrot">3</option>
                <option value="spider">4</option>
                <option value="goldfish">5</option>
            </select>
        </div>

        <div style="margin: 10px;">
            <textarea name="textarea" id="" cols="20" rows="5" placeholder="这是textarea"></textarea>            
        </div>



        <hr> <!-- hr是分界线 -->

        <table>
            <caption style="caption-side: bottom;">这个表格的名称</caption>
            <thead>
                <th>表头1</th>
                <th>表头2</th>
                <th>表头3</th>
                <th>表头4</th>
                <th>表头5</th>
            </thead>
            <tbody>
                <tr>
                    <th>th 1</th>
                    <td>1:1</td>
                    <td>1:2</td>
                    <td>1:3</td>
                    <td>1:4</td>
                </tr>
                <tr>
                    <th>th 2</th>
                    <td>2:1</td>
                    <td>2:2</td>
                    <td>2:3</td>
                    <td>2:4</td>
                </tr>
                <tr>
                    <th>th 3</th>
                    <td>3:1</td>
                    <td>3:2</td>
                    <td>3:3</td>
                    <td>3:4</td>
                </tr>
            </tbody>
            <tfoot>
                <tr>
                    <th scope="row">table foot</th>
                    <td>10086</td>
                </tr>
            </tfoot>
        </table>



        <style>
            body{
                background-color: #e1e6b6;
            }
        </style>
        
        <script  type="text/javascript" src="js/demo.js (js文件的路径)" ></script>
        <script>
            //这是内联 javascript
            var text = "Hello";
        </script>
    </body>
</html>
~~~

如果想要查看上面的 html 代码渲染出来长什么样子：

1. 随便找个地方新建文件夹，进入文件夹 （我建立了一个名为 `demo1` 的文件夹）

2. 打开`Visual Studio Code` ，点击 `打开文件夹...`

   ![html7](https://storage.szulib.top/szulib/image-hosting/html7.png)

3. 选择刚刚新建的文件夹，点击下图所指的小图标 新建文件

   ![html8](https://storage.szulib.top/szulib/image-hosting/html8.png)

4. 给新文件命名为 `index.html` ，回车。然后把上面的代码复制粘贴一下

5. 点击右下角的 `Go Live` 图标，应该会自动打开浏览器展示页面，这时如果修改 html 文件，浏览器会自动刷新（前提是已经安装 [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) 插件）

   ![html9](https://storage.szulib.top/szulib/image-hosting/html9.png)

   ![html10](https://storage.szulib.top/szulib/image-hosting/html10.png)

   

**Suggestion:** 打开文件资源管理器 的 `查看` 选项卡，把 `文件拓展名` 给勾上

![html5](https://storage.szulib.top/szulib/image-hosting/html5.png)



常用标签：

[input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)

[div](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/div)

[ul](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/ul)  [ol](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/ol)

[select](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select)



一些可能会有帮助的文章：

[checkbox的value和checked属性详解——CSDN](https://blog.csdn.net/kouryoushine/article/details/87984749)



### DOM

浏览器会用HTML解析算法将HTML转换成DOM树。下面让我们看一下HTML到DOM树的转换：

~~~html
<html>
    <head>
	...
    </head>
    <body>
        <h1>text</h1>
        <p>text</p>
        <h2>text</h2>
        <p>text</p>
    </body>
</html>
~~~

![html1](https://storage.szulib.top/szulib/image-hosting/html1.png)

## CSS

层叠样式表（**C**ascading **S**tyle **S**heet，简称：CSS）是为网页添加样式的代码。CSS干嘛的：改变文本的颜色 将内容显示在屏幕的特定位置 给背景换个颜色 把直角边框变成圆角 调整元素之间间距 ...

[CSS Tutorial —— W3schools](https://www.w3schools.com/css/)

CSS 的语法

![css1](https://storage.szulib.top/szulib/image-hosting/css1.gif)

~~~css
h1 {
    color: blue;      /* 设置文本颜色为蓝色 */
    font-size:12px;   /* 设置字体大小为 12px*/
}
~~~

这里的 `h1` 作为一个标签选择器，选中页面中的所有 `h1` 标签，应用 `{...}` 中的样式。每个样式声明后面以 `;` 结束

可以尝试将上面的css代码复制粘贴到之前 `demo1` 文件夹中的 `index.html` 

放在 `<style>...</style>`标签之间

~~~css
<style>
body{
    background-color: #e1e6b6;
}
h1 {
    color: blue;      /* 设置文本颜色为蓝色 */
    font-size:12px;   /* 设置字体大小为 12px*/
}
</style>
~~~

然后点击`Go Live` 在浏览器中看见CSS的效果

#### [Selector](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Selectors)

常用选择器有三种：元素选择器、类选择器、id选择器

元素选择器

~~~html
<!-- demo-css1.html -->
...
<body>
	<div>
        <h1>Hello CSS</h1> <!-- 这个元素被选中 -->
    </div>
</body>
...
~~~

~~~css
/** demo-css1.css*/
/*元素选择器*/
h1 {
    color: blue;      
    font-size:12px;   
}
~~~



id选择器


~~~html
<!-- demo-css2.html -->
...
<body>
    <div id="navbar"> <!-- 这个元素以及内部的所有元素被选中，id是唯一标识，同一个页面中id的值不可重复 -->
    	<nav>...</nav>
    </div>
</body>
...
~~~

~~~css
/** demo-css2.css */
/**id选择器
* 用法：一个'#'加上html中元素属性id的值 
*/ 
...
#navbar {
    padding: 10px 0px;
    color: rgb(242, 246, 250);
    background-color: rgb(5, 185, 146);
    min-width: 500px;
}
~~~



class选择器

~~~html
<!-- demo-css3.html-->
<nav id="navbar">
	<ul>               
		<li class="nav-item nav-home">  <!-- 一个元素可以有多个class； -->
            <a href="./index.html">Home</a> 
        </li>
        <li class="nav-item">  <!-- class是可重复的；一个class可以选中多个元素 -->
            <a href="./html.html">HTML</a>
        </li>
        <li class="nav-item">
            <a href="./css.html">CSS</a>
        </li>
        <li class="nav-item">
            <a href="">About</a>
        </li>
    </ul>
</nav>
~~~

~~~css
/** demo-css3.css */
/** class选择器
* 用法：一个'.'加上html中元素属性class的值 
*/
.nav-item {
    display: inline;   /*行内显示*/
    margin: 20px;
    font-size: large;  /*字体变大*/
}
.nav-home {
    font-weight: bold; /*字体变粗*/
}
~~~



选择器的组合

~~~html
<!-- 仍然是demo-css3.html -->
<nav id="navbar">
	<ul>               
		<li class="nav-item nav-home">  
            <a href="./index.html">Home</a> <!-- 被选中 -->
        </li>
        <li class="nav-item">  
            <a href="./html.html">HTML</a>  <!-- 被选中 -->
        </li>
        <li class="nav-item">
            <a href="./css.html">CSS</a>    <!-- 被选中 -->
        </li>
        <a href="">About</a>            <!-- 被选中 -->

    </ul>
</nav>
~~~

~~~css
/** demo-css4.css */
/** 后代组合器
* 用法：各个选择器中间加上 空格，表示选择前一个元素的后代节点  
* 此处匹配 id=navbar 的元素内部的所有 a标签 
*/
#navbar a {
    color: azure;
    text-decoration:none;
}

#navbar ul li a {
    color: azure;
    text-decoration:none;
}

~~~

[伪类 `:hover`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:hover) 

剩下的自己看文档就好了...



## Layout 

掌握两种布局足够应付大多数情况，大概看看下面的教程了解概念即可

**Tip:**  Layout 这部分可以先跳过，回过头再来看

#### Flex

[A Complete Guide to Flexbox —— CSS-TRICKS](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

[Flex 布局教程——阮一峰](https://www.ruanyifeng.com/blog/2015/07/flex-grammar.html) （如果你懒得看英文就看这个吧）



#### Grid

[A Complete Guide to Grid —— CSS-TRICKS](https://css-tricks.com/snippets/css/complete-guide-grid/)

[CSS Grid 网格布局教程 —— 阮一峰](https://www.ruanyifeng.com/blog/2019/03/grid-layout-tutorial.html)



#### 案例

[卡片——MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Layout_cookbook/Card)



*****

上面的学习不用花太多时间，简单浏览留下印象即可，以便拿到需求时有一个大概方向。具体实现可以通过查找文档和博客了解更多技术细节



## Bootstrap

当你大概明白 html 和 css 是如何产生效果的，可以尝试使用 Bootstrap 框架

Bootstrap 是一组用于网站和网络应用程序开发的开源前端框架，包括HTML、CSS及JavaScript的框架，提供字体排印、窗体、按钮、导航及其他各种组件及 Javascript 扩展，旨在使动态网页和Web应用的开发更加容易。

简单说，就是 Bootstrap 为你写好了许多 CSS 样式，你只需要给元素的 `class`写上一些特定的关键字就可以应用 CSS 样式了

怎么用？

~~~html
<div class="mx-auto" style="width: 200px;">
  Centered element
</div>
~~~

上面的 `mx-auto` class 值相当于下面 CSS 的 `margin:auto; `

~~~html
<div class="element">
  Centered element
</div>
~~~

~~~css
.element{
    margin:auto; 
    width: 200px;
}
~~~



具体看官方文档就完事了。使用体验非常爽。顺便从 bootstrap 中学习如何构建页面的 html 结构

[Bootstrap Docs](https://getbootstrap.com/docs/5.1/getting-started/introduction/)



## Javascript

前端重点在于学习 

0. 基础语法就不说了

1. [操作DOM文档树](https://zh.javascript.info/document)（增加、移除、更改样式、获取用户输入）
2. [触发事件](https://zh.javascript.info/events) （各种事件、了解**冒泡**是什么？）
3. [了解 回调函数](https://zh.javascript.info/callbacks)
4. 了解 同步异步 [Promise](https://zh.javascript.info/promise-chaining)
5. 发送网络请求 
   1. [HTTP 请求方法](https://www.w3schools.com/tags/ref_httpmethods.asp)
   2. XMLHttpRequest (可以跳过，现在已经很少用到)  
   3. [Fetch](https://zh.javascript.info/fetch) 
   4. 使用网络请求库 (如：[Axios](https://axios-http.com/zh/docs/intro)) 在项目中使用这种第三方库，可以提高开发效率
   5. [Websocket](https://zh.javascript.info/websocket) (第三方库 [Socket.IO](https://socket.io/)) 一种在浏览器和服务器之间建立持久连接来交换数据的方法
   
   

一些问题：

[我应该把 script 标签放哪里？](https://stackoverflow.com/questions/436411/where-should-i-put-script-tags-in-html-markup) 

...



## Node.js

**Node.js** 是能够在服务器端运行 JavaScript 的开放源代码、跨平台运行环境。

这里主要是被用来编写一些后端服务、之后会用于运行一些前端工具。

### Install node

* windows：

  1. 在 [Node官网](https://nodejs.org/en/) 点击下方按钮进行下载

     ![node1](https://storage.szulib.top/szulib/image-hosting/node1.png)

  2. 下载完成后，按照指引进行安装，安装路径可自定义修改。安装包默认会将 node 添加到全局变量

  3. 打开 PowerShell / CMD，输入

     ~~~powershell
     node -v
     ~~~

     可以看到输出 node 的版本号

     ~~~powershell
     v14.18.0 
     ~~~

     执行 `npm -v` 查看 `npm` 版本

     ~~~powershell
     6.14.10 #可能版本号不同，没有关系
     ~~~

  4. 到这说明 node 和 npm 已经安装完成，并且添加到全局系统变量

* Mac：

  可以参考一下[这个文章](http://nodejs.cn/learn/how-to-install-nodejs)，使用 Mac 上的包管理工具 [Homebrew](https://brew.sh/) 进行安装

  1. 需要先安装 Homebrew，打开 Terminal，粘贴下面的代码并运行

     ~~~bash
     /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
     ~~~

  2. 然后执行下面的命令，安装 node

     ~~~bash
     brew install node
     ~~~





## 上手 Linux 系统

[Linux](https://zh.wikipedia.org/wiki/Linux%E5%86%85%E6%A0%B8) 与 Windows 是同一层级的概念，都是操作系统。Linux 的分支、发行版非常多，我们选择比较友好的 [Ubuntu](https://cn.ubuntu.com/) 来进行学习（默认所有的操作在Windows版的Vmware虚拟机上完成）

### 在虚拟机上安装 Ubuntu 20.04

1. 下载 VMware 和 Ubuntu 的镜像文件

   下载链接：

   * VMware Workstation  [校园网(v15.5)](http://172.30.234.8:8001/szulib/software/VMware-workstation-full-15.5.2-15785246.exe)   [官网(v16.1)](https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html)
   * Ubuntu 20.04 Desktop (ISO)  校园网  [官网](https://ubuntu.com/download/desktop)

2. 安装VMware Workstation

   上网找一些注册码

3. 打开 VMware Workstation -> 创建新的虚拟机

   ![linux1](https://storage.szulib.top/szulib/image-hosting/linux1.png)

4. 选择典型，下一步

   ![linux2](https://storage.szulib.top/szulib/image-hosting/linux2.png)

5. 选择 稍后安装操作系统，下一步

   ![linux3](https://storage.szulib.top/szulib/image-hosting/linux3.png)

6. 客户机操作系统选择 Linux ，版本选 Ubuntu 64位

   ![linux4](https://storage.szulib.top/szulib/image-hosting/linux4.png)

7. 虚拟机名称和位置根据自己的喜好自定义

   ![linux4](https://storage.szulib.top/szulib/image-hosting/linux4.png)

8. 设置磁盘大小，一般默认就可以了，下一步

   ![linux6](https://storage.szulib.top/szulib/image-hosting/linux6.png)

9. 点击完成，出现以下界面

   ![linux8](https://storage.szulib.top/szulib/image-hosting/linux8.png)

10. 点击 编辑虚拟机设置 

11. 选择 CD/DVD (SATA) ，在连接那里选择 `使用ISO映像文件`，点击 `浏览` 选择之前下载的 Ubuntu xxx.iso 文件

    ![linux9](https://storage.szulib.top/szulib/image-hosting/linux9.png)

12. 更改虚拟机网络设置为桥接模式（如果你的电脑不是接在自己宿舍内的路由器上，请不要做此项更改，默认 NAT 即可）

    ![linux10](https://storage.szulib.top/szulib/image-hosting/linux10.png)

13. 启动虚拟机，走完安装流程

    等待进度条走完...

    ![linux11](http://storage.szulib.top/szulib/image-hosting/linux11.png)

    选择语言，一般默认英语，点击 `Install Ubuntu`

    ![linux12](http://storage.szulib.top/szulib/image-hosting/linux12.png)

    选择键盘布局，默认即可，点 `Continue`

    ![linux13](http://storage.szulib.top/szulib/image-hosting/linux13.png)

    选择最小化安装，下面的安装选项取消勾选。你保持默认也可以，看你喜好

    ![linux14](http://storage.szulib.top/szulib/image-hosting/linux14.png)

    点击 `Install Now` ，再点 `Continue`

    ![linux15](http://storage.szulib.top/szulib/image-hosting/linux15.png)

    选择时区，默认 `Shanghai` 即可

    ![linux16](H:\Code\AL-2021\images\linux16.png)

    填写信息，设置用户名和密码。前两项随便填，第三项为用户名，第四第五为密码，点击继续

    ![linux17](http://storage.szulib.top/szulib/image-hosting/linux17.png)

    等待进度条走完，点击 `Restart Now`。等待重启，启动过程可能需要按一下回车

    不出意外，开起来之后就可以看到桌面了

    ![linux17](http://storage.szulib.top/szulib/image-hosting/linux18.png)

    

### 尝试使用命令行操作

14. 设置 root 用户的密码。在桌面右键可以看到右键菜单

    ![linux19](http://storage.szulib.top/szulib/image-hosting/linux19.png)

    点击 `Open in Terminal` ，在终端输入 `sudo passwd root` ，回车

     ~~~bash
     $ sudo passwd root
     # sudo: 以系统管理者的身份执行指令，也就是说，经由 sudo 所执行的指令就好像是 root 亲自执行。 
     # passwd: 创建或修改用户的密码
     # root: Linux 系统的超级管理员
     ~~~

    先输入你安装时候设置的密码，再填写 root 的密码，输入完就回车

    ![linux20](http://storage.szulib.top/szulib/image-hosting/linux20.png)

    **note:** 输入密码的时候都是不显示的，并不是键盘坏了...

    尝试使用 `su` 命令，切换到 root 用户。当看到提示符由 `$` 变成 `#` 说明你已经处于 root 用户

    ![linux21](http://storage.szulib.top/szulib/image-hosting/linux21.png)

    

15. 尝试使用 nano文本编辑器 

    在桌面打开 终端 (Terminal)，输入：

    ~~~bash
    $ nano test
    # nano: 打开nano文本编辑器
    # test: 文件名，可以写你喜欢的
    ~~~

    回车后可以看到下面这个界面

    ![linux22](http://storage.szulib.top/szulib/image-hosting/linux22.png)

    随便写点什么然后 同时按 `Ctrl` + `S` 保存，如果是按 `Ctrl` + `O` (就是下方菜单中的 `^O` )，写入文件，可以保存到 test 文件也可以另存到另一个文件

    ![linux23](http://storage.szulib.top/szulib/image-hosting/linux23.png)

    回车，保存成功。然后，按 `Ctrl` + `X` 退出编辑器。在桌面上应该可以看到一个新建的文本，双击打开看看是否有刚刚输入的内容

    接下来我们打算更换软件源，这一步不是必须的，如果你认为你的网络环境还不错可以不更换。

    更换软件源为 清华源 [source](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)

    在终端输入：

    ~~~bash
    $ sudo nano /etc/apt/sources.list #使用 nano 打开文件 sources.list
    ~~~

    ![linux24](http://storage.szulib.top/szulib/image-hosting/linux24.png)

    将原有的源地址注释掉，在前面加个 `#`

    复制以下内容粘贴（`Ctrl` + `Shift` + `v`）到文档底部，保存退出

    ~~~bash
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
    # deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
    # deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
    # deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
    # deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
    ~~~

    尝试使用 `cat` 命令输出文件内容，查看是否已经修改了文件

    ~~~bash
    $ cat /etc/apt/sources.list
    ~~~

    修改完的文件应该是长这样：

    ~~~bash
    #deb cdrom:[Ubuntu 20.04.1 LTS _Focal Fossa_ - Release amd64 (20200731)]/ focal main restricted
    
    # See http://help.ubuntu.com/community/UpgradeNotes for how to upgrade to
    # newer versions of the distribution.
    # deb http://cn.archive.ubuntu.com/ubuntu/ focal main restricted
    # deb-src http://cn.archive.ubuntu.com/ubuntu/ focal main restricted
    
    ## Major bug fix updates produced after the final release of the
    ## distribution
    # deb http://cn.archive.ubuntu.com/ubuntu/ focal-updates main restricted
    # deb-src http://cn.archive.ubuntu.com/ubuntu/ focal-updates main restricted
    
    ## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu
    ## team. Also, please note that software in universe WILL NOT receive any
    ## review or updates from the Ubuntu security team.
    # deb http://cn.archive.ubuntu.com/ubuntu/ focal universe
    # deb-src http://cn.archive.ubuntu.com/ubuntu/ focal universe
    # deb http://cn.archive.ubuntu.com/ubuntu/ focal-updates universe
    # deb-src http://cn.archive.ubuntu.com/ubuntu/ focal-updates universe
    
    ## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu 
    ## team, and may not be under a free licence. Please satisfy yourself as to 
    ## your rights to use the software. Also, please note that software in 
    ## multiverse WILL NOT receive any review or updates from the Ubuntu
    ## security team.
    # deb http://cn.archive.ubuntu.com/ubuntu/ focal multiverse
    # deb-src http://cn.archive.ubuntu.com/ubuntu/ focal multiverse
    # deb http://cn.archive.ubuntu.com/ubuntu/ focal-updates multiverse
    # deb-src http://cn.archive.ubuntu.com/ubuntu/ focal-updates multiverse
    
    ## N.B. software from this repository may not have been tested as
    ## extensively as that contained in the main release, although it includes
    ## newer versions of some applications which may provide useful features.
    ## Also, please note that software in backports WILL NOT receive any review
    ## or updates from the Ubuntu security team.
    # deb http://cn.archive.ubuntu.com/ubuntu/ focal-backports main restricted universe multiverse
    # deb-src http://cn.archive.ubuntu.com/ubuntu/ focal-backports main restricted universe multiverse
    
    ## Uncomment the following two lines to add software from Canonical's
    ## 'partner' repository.
    ## This software is not part of Ubuntu, but is offered by Canonical and the
    ## respective vendors as a service to Ubuntu users.
    # deb http://archive.canonical.com/ubuntu focal partner
    # deb-src http://archive.canonical.com/ubuntu focal partner
    
    # deb http://security.ubuntu.com/ubuntu focal-security main restricted
    # deb-src http://security.ubuntu.com/ubuntu focal-security main restricted
    # deb http://security.ubuntu.com/ubuntu focal-security universe
    # deb-src http://security.ubuntu.com/ubuntu focal-security universe
    # deb http://security.ubuntu.com/ubuntu focal-security multiverse
    # deb-src http://security.ubuntu.com/ubuntu focal-security multiverse
    
    # This system was installed using small removable media
    # (e.g. netinst, live or single CD). The matching "deb cdrom"
    # entries were disabled at the end of the installation process.
    # For information about how to configure apt package sources,
    # see the sources.list(5) manual.
    
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
    # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
    # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
    # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
    # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
    ~~~

    

16. 使用包管理器 `apt`

    运行：

    ~~~bash
    $ sudo apt update #检查更新
    ~~~

    [apt 是什么？](https://www.runoob.com/linux/linux-comm-apt.html)

    如果你使用的是https的源，有可能会出现以下错误

    ~~~bash
    Certificate verification failed: The certificate is NOT trusted. The certificate chain uses expired certificate.  Could not handshake: Error in the certificate verification....
    ~~~

    解决方法：

    先把源换成http，把https的s删掉 -> http，然后 `apt update`，再安装  ca-certificates ：`apt install ca-certificates `

    进行软件包更新：

    ~~~bash
    $ sudo apt upgrade #更新软件包
    ~~~

    ![linux25](http://storage.szulib.top/szulib/image-hosting/linux25.png)

    按 `Y` 或者 `y`, 回车

    

    **note:** 如果你想了解一个命令的用法，可以在命令后面加上 `--help` 或者使用 `man` 命令进行查看

    一个命令的组成：

    ~~~bash
    $ apt-get install gedit
    ~~~
    
    ![img](http://embeddedinventor.com/wp-content/uploads/2021/01/image-29-1024x389.png)

    

    比如，想查看 apt 的用法
    ~~~bash
    $ apt --help
    或者
    $ man apt
    ~~~
    
    ![linux26](http://storage.szulib.top/szulib/image-hosting/linux26.png)
    
    它会告诉你这个apt命令是一个命令行的包管理器balabala， apt 的用法（list search show ...）


​    

17. 操作文件/文件夹

    `ls` : 列出文件

    `pwd`：显示当前所在目录

    `cd`：change directory 切换目录

    `mkdir`：看字就知道是新建文件夹

    `touch`：可以用于新建文件

    `rm`：remove 删除

    补充：[Linux 目录结构](https://www.cnblogs.com/silence-hust/p/4319415.html)

    尝试自己玩一玩以上命令：

    **note：**在输入命令或者路径的时候多按按键盘上的 `Tab` 键，可以帮助你自动补全 

    ![linux27](http://storage.szulib.top/szulib/image-hosting/linux27.png)

    顺便一提：`ll` 命令相当于 `ls -l` 可以显示更多文件信息。`ll` 命令是来自于bash对 `ls -l` 的别名设置，而不是 `ls` 本身自带。我们可以在 `~/.bashrc` 文件中找到

    ~~~bash
    vi ~/.bashrc # vi与nano一样是一个文本编辑器，自己查找vi的用法
    ~~~

    进入编辑器后，按 `:` 然后输入`set number` ，回车，可以出现行数

    ![linux30](http://storage.szulib.top/szulib/image-hosting/linux30.png)

    ![linux28](http://storage.szulib.top/szulib/image-hosting/linux28.png)

    看到第79行

    ~~~bash
    alias ls='ls --color=auto'
    ~~~

    可以看到 `ls` 命令会自动带上`--color=auto` 的选项，就是你在使用`ls` 所看到的列出不同类型文件/文件夹会有不同颜色

    ~~~bash
    alias ll='ls -alF'
    ~~~

    而 `ll` 是 `ls -alF` 的别称

    你也可以设置自己喜欢的别称，就像文件中说的

    ![linux29](http://storage.szulib.top/szulib/image-hosting/linux29.png)

    退出编辑器请按 `:` 再输入`q`  回车

    我们可以新建一个文件叫 `.bash_aliases` 放在 `~/` 目录（就是家目录的意思）下

    ~~~bash
    vi ~/.bash_aliases
    ~~~

    进入[vi编辑器](https://www.cnblogs.com/itech/archive/2009/04/17/1438439.html)后，按 `i` 进入插入模式（或者你想叫编辑模式也行）

    补充：[Learn Vim](https://danielmiessler.com/study/vim/)

    ![linux31](http://storage.szulib.top/szulib/image-hosting/linux31.png)

    可以看到左下角出现了 `-- INSERT --`，就可以开始输入了

    我们写上
    
    ~~~bash
    alias cle='clear'
    ~~~

    好，退出 `INSERT` 模式需要你按下键盘上的 `Esc` 键

    然后保存退出，按下`:` 接着输入 `wq`  回车（w是保存的意思，q是退出） 

    ![linux33](http://storage.szulib.top/szulib/image-hosting/linux33.png)
    
    在终端运行：
    
    ~~~bash
    $ source  ~/.bashrc #为了应用刚刚的更改
    ~~~

    ![linux32](http://storage.szulib.top/szulib/image-hosting/linux32.png)

    我们尝试一下刚刚设置的别名 `cle` 看看是不是和 `clear` 是同样的效果——清除屏幕，发现是一样的，OK
    
    刚刚好像有点不务正业了... 现在我们继续学习关于文件权限的内容 （咳咳
    
    感觉有篇笔记写的还行，那就看这个吧 [文件权限基础](https://itboon.github.io/linux-20/file-permission/basic/)，我就不用写了，也不用看太多，会用 `chmod` 修改权限 用`chown` 修改所属就可以了 。
    
    
    
18. 请自行完成下面的小任务

    1. 在 VS Code 官网查找安装文档，为 Ubuntu 安装 VS Code  [Visual Studio Code on Linux](https://code.visualstudio.com/docs/setup/linux)

    2. 在 Nginx 的官网上查找安装方法，为 Ubuntu 安装 Nginx 服务器  [Nginx install](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/#official-debian-ubuntu-packages) 

    3. 安装 Nginx 完成后，使用文本编辑器修改 Nginx 的配置

    4. 自行查找 `systemctl` 命令的使用方法，尝试启动、停止 Nginx 服务，查看服务状态、设置开机启动等等

       ![linux34](http://storage.szulib.top/szulib/image-hosting/linux34.png)

    5. 把前面写的网页放上去替换默认的 html 文件，确保在浏览器中通过 `http://127.0.0.1/` 或者 `http://localhost/` 可以访问得到 [Guidance](https://ubuntu.com/tutorials/install-and-configure-nginx#1-overview)

19. 查看本机的网络

    使用 `ip add` 或者 `ifconfig` 可以查看本机的网络，在 Windows 中，使用 `ipconfig` 可以查看本机网络

    这里 ens33 是网卡名称，192.168.1.199 是上面路由器分配给 Ubuntu 的ip地址

    ![linux35](http://storage.szulib.top/szulib/image-hosting/linux35.png)

    开启 Nginx 之后尝试在浏览器中访问你的 Ubuntu 的ip地址，应该可以看到自己的网页

    

    附：电子书[《鸟哥的Linux私房菜》](http://172.30.234.8:8001/szulib/books/%E3%80%8A%E9%B8%9F%E5%93%A5%E7%9A%84Linux%E7%A7%81%E6%88%BF%E8%8F%9C-%E5%9F%BA%E7%A1%80%E7%AF%87%E3%80%8B%E7%AC%AC%E5%9B%9B%E7%89%88.pdf)
    
    

## 网络通信相关  

1. 自行了解一些基础概念

    * ip地址
    * 域名
    * DNS 服务 （可以使用 `nslookup` 命令进行查询）
    * 子网掩码
    * url 的组成
    * get 请求、post 请求
    * Mac 地址的作用
    * 路由器的作用

    附：电子书[《网络是怎么连接的》](http://172.30.234.8:8001/szulib/books/%E7%BD%91%E7%BB%9C%E6%98%AF%E6%80%8E%E6%A0%B7%E8%BF%9E%E6%8E%A5%E7%9A%84_%E6%88%B7%E6%A0%B9%E5%8B%A4.pdf) [《计算机网络——自顶向下法》](http://172.30.234.8:8001/szulib/books/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C-%E8%87%AA%E9%A1%B6%E5%90%91%E4%B8%8B%E6%96%B9%E6%B3%95%E7%AC%AC%E4%B8%83%E7%89%88.pdf)

2. 一个小demo

   * 下载一个工具 [Postman](https://www.postman.com/downloads/)
   
   新建一个文本文件，命名为 `dingDong.js` 
   
   ~~~bash
   code dingDong.js
   ~~~
   
   复制粘贴以下内容，保存
   
   ~~~javascript
   const http = require('http');
   
   // Create a local server to receive data from
   const server = http.createServer((req, res) => {
       let responseText = '带上参数q=ding试试看'
       console.log('request url: '+ req.url);//打印出 req.url 的值
       const params = Object.fromEntries(new URLSearchParams(req.url.replace('/','')));//从url中解析出请求参数，不必理会
   
       for (let key in params){
           if( key == 'q' && params[key] == 'ding') {
               responseText = 'dong'
               console.log('dong');
           }
       }
   
       res.writeHead(200, { 'Content-Type': 'application/json' });
       res.end(JSON.stringify({
           data: responseText
       }));
   });
   
   server.listen(9090, ()=>{
       console.log('Server is running on http://localhost:9090')
   });
   ~~~
   
   在 VS Code 中，点击右上角的运行按钮，可以看到底部终端的输出
   
   ![network2](http://storage.szulib.top/szulib/image-hosting/network2.png)
   
   或者，也可以自己打开终端，输入 `node .\dingDong.js ` 运行js文件
   
   ![network3](http://storage.szulib.top/szulib/image-hosting/network3.png)
   
   这时，一个简单的nodejs 的服务就启动了，要结束程序只需在终端按下 `Ctrl` + `C`就能停止运行
   
   启动程序后打开 Postman ，File -> New...  -> HTTP Request ，选择  GET 方法，复制粘贴下面的地址，点 Send
   
   ~~~bahs
   http://localhost:9090
   ~~~
   
   ![network4](http://storage.szulib.top/szulib/image-hosting/network4.png)
   
   尝试带上参数
   
   ~~~bash
   http://localhost:9090?q=ding 
   ~~~
   
   ![network5](http://storage.szulib.top/szulib/image-hosting/network5.png)
   
   服务器程序可以根据我们发送请求的不同参数做出反应，服务器程序大部分时候都在做这件事情。可能会拿请求中携带的参数去数据库中查找，把查找结果返回给前端。。。
   
   
   
3. 了解浏览器的同源策略

    简单理解，就是浏览器会限制网页向与网站本身不是同一个来源的地址发送网络请求，[同源的定义](https://developer.mozilla.org/zh-CN/docs/Web/Security/Same-origin_policy)

    ![network1](http://storage.szulib.top/szulib/image-hosting/network1.png)

    Q：如何解决同源策略的限制？

    A：[允许跨源资源共享（CORS）](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS)

    在服务端的返回请求中加上请求头`'Access-Control-Allow-Origin': '*'`，这个请求头设置会导致安全问题，但我们先不关心，程序和人只要有一个能 Run 就行。。。又不是不能用。。

    自己尝试运行下面的小demo：

    把 server1.js 和 server2.js 都运行起来，打开 index.html 网页。

    开启控制台，分别点击两个按钮观察结果

    ![network6](http://storage.szulib.top/szulib/image-hosting/network6.png)

    index.js

    ~~~html
    <!DOCTYPE html>
    
    <html>
        <head>
            <meta charset="utf-8">
            <title>demo-cors</title>
        </head>
        <body>
    
            <h1>Hello, this is demo-cors</h1>
            <button onclick="reqServer1()" style="margin: 20px;">reqServer1</button>
            <button onclick="reqServer2()" style="margin: 20px;">reqServer2</button>
    
            <script>
    
                function reqServer1() {
                    console.log("reqServer1")
                    request('http://127.0.0.1:8000',(res) => {
                        showRes(res);
                    })
                }
    
                function reqServer2() {
                    console.log("reqServer2")
                    request('http://127.0.0.1:9000',(res) => {
                        showRes(res);
                    })
                }
    
                function showRes(res) {
                    let resDate = document.createElement('p');
                    resDate.innerText = res;
                    document.body.appendChild(resDate);
                }
                
                function request(url, callback) {
                    let xhr = new XMLHttpRequest();
                    
                    xhr.open('GET', url);
    
                    xhr.onload =  () => {
                        callback(xhr.response);
                    };
    
                    xhr.onerror = () => {
                        callback('error'); 
                    };
    
                    xhr.send();
                }
                
            </script>
        </body>
    </html>
    ~~~

    server1.js

    ~~~javascript
    const http = require('http');
    const port = 8000
    const requestListener = function (req, res) {
        res.writeHead(200);
        res.end('Hello, World! This is server1');
    }
    
    const server = http.createServer(requestListener);
    server.listen(port);
    console.log(`Server running at http://127.0.0.1:${port}`);
    ~~~

    server2.js

    ~~~javascript
    const http = require('http');
    const port = 9000
    const requestListener = function (req, res) {
    
        const headers = {
            'Access-Control-Allow-Origin': '*',
            'Access-Control-Allow-Methods': 'POST, GET'
        };
        
        // console.log(req);
        if(['GET', 'POST'].indexOf(req.method) !== -1){
            res.writeHead(200, headers);
            res.end('Hello, World! This is server2');
            return;
        }
        res.writeHead(405, headers);
        res.end(`${req.method} is not allowed for the request.`);
    }
    
    const server = http.createServer(requestListener);
    server.listen(port);
    console.log(`Server running at http://127.0.0.1:${port}`);
    ~~~

    面试知识点：[解决跨源的方法](https://blog.csdn.net/weixin_46000410/article/details/109442391)

 

## 简单使用数据库

1. [安装配置 Mysql](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04)
2. [了解一下SQL语句](https://www.liaoxuefeng.com/wiki/1177760294764384/1179610544539040)
3. [使用nodejs连接mysql数据库](https://juejin.cn/post/6920948406055616526)



## 一些实用的东西：

* [pm2](https://pm2.keymetrics.io/)

* 连接出现问题，先排查防火墙 ([ufw](https://blog.csdn.net/fd214333890/article/details/115410168) iptables ...

* [Ubuntu查看端口占用及关闭](https://www.jianshu.com/p/acb085a8f1cb)

* ...




## 美观

### 颜色

![color1](http://storage.szulib.top/szulib/image-hosting/color1.jpg)

[uigradients](https://uigradients.com/#JShine)

[colorhunt](https://www.colorhunt.co/)

https://www.palettable.io/FC788D

https://webgradients.com/

### 动画

[greensock]( https://greensock.com/)

[anime.js](https://github.com/juliangarnier/anime)

...



## 杂项

[JavaScript Guidebook](https://tsejx.github.io/javascript-guidebook/)

[前端基础进阶](https://www.jianshu.com/p/996671d4dcc4)

[前端进阶指南](https://juejin.cn/post/6977258091662278669)

[Node.js 入门教程](https://yunnysunny.gitbooks.io/nodebook/content/01_node_introduce.html)

[從無到有，打造一個漂亮乾淨俐落的 RESTful API](https://andy6804tw.gitbooks.io/restful-api/content/)

[Vue3](https://v3.vuejs.org/)



## 写在后面

看起来好像有好多东西可以学，但是大一的同学先不要着急。我个人是认为不要过早地对一样东西死磕深挖（不要把太多时间耗损在琐碎的细节里），应该让自己接触的面广一些，多多尝试新的方向。因为你当前认为很有意思的东西不一定是自己最喜欢的。也可以找找 学院内/其他学院 的老师，看看是在做什么，有没有自己感兴趣的。

更重要的是找到自己生活的锚点，或者说，意义... 得找到一个能支撑你付出的东西。

有趣的东西很多，时间往往不够用，所以学习和做项目也要有方向，有规划，避免出现那种什么都学但是又什么都没学的感觉

还有一个重要的事情：绩点，平时课内学习不要太浪... 不管你的学习方式怎么样，即便你认为这个课程本身没有太大意义，老师教的一般，也要想办法让绩点尽量高。 比赛就当是调剂或者一种娱乐，没有绩点重要。保证绩点的同时通过课外学习提升个人能力是最理想的模式。



## Contributors 

teamone xiaojiang

