


## 一、开发工具
### 开发工具
#### 1.【强制】前端代码编辑器：Visual Studio Code。
说明：请使用VS Code进行前端代码编码，版本不限。除特殊情况均使用此编辑器。

#### 2.【建议】VS Code安装如下常用插件：
+ 1)Chinese （中文(简体中文) 语言包中文插件）
+ 2)Error Lens （主要用于代码编辑时错误及警告的提示和展示）
+ 3)Code Spell Checker （源代码拼写检查器，提示代码中单词拼写错误）
+ 4)Auto Close Tag （标签自动闭合html标签）
+ 5)auto rename tag（使用该插件，可以在重命名一个 HTML 标签时，自动重命名 HTML 标签的开始和结束标签。避免只修改了开始标签，而忘记修改结束标签。该扩展适用于 HTML、XML、PHP 和 JavaScript）
+ 6)Prettier- Code formatter （对应的格式化的具体的风格）
+ 7)Vetur （开发vue2项目必须安装，但是要禁用vue3的插件）
+ 8)Volar （这个是语法高亮，安装成功以后记得禁用vue2的vetur，有冲突）
+ 9)vue-snippets：可以直接使用vfor-arr并且写的时候还有提示，方便快速查看和使用

        1.支持快速定义vue的模板：使用vbase可以快速生成一下代码

        2.支持模板语法：使用vfor-arr可以快速生成for循环的代码

        3.支持vue script语法，使用vref可以快速生成如下代码

        4.支持vue-router相关代码，比如使用vrouter-beforeRouteEnter指令可以快速生成如下代码 

        5.支持vuex相关代码，使用vuexbase-type可以快速生成vuex的配置模板并且还带typescript

+ 10)Git Graph （类似于SourceTree的可视化版本控制插件，可以更新、提交代码，查看提交记录，审视代码）
+ 11)CSS Peek （允许查看css，并从HTML文件定位到css文件，文件定义跳转）

#### 3.【建议】VS Code基础配置setting.json配置如下：
Command+Shift+P 搜索 settings.json
```JSON
{
	// 換行
	"editor.wordWrap": "on",
	// 是否允许自定义的snippet片段提示
	"editor.snippetSuggestions": "top",
	// vscode默认启用了根据文件类型自动设置tabsize的选项 不检查缩进，保存后统一按设置项來设置 false
	"editor.detectIndentation": false,
	// 重新设定tabsize 代码缩进修改成 2 个空格
	"editor.tabSize": 2,
	// #每次保存的时候将代码按照 eslint 格式进行修复 true
	"editor.codeActionsOnSave": {
		"source.fixAll.eslint": true
	},
	// #每次保存的时候自动格式化（true / false）
	"editor.formatOnSave": true,
	"editor.formatOnType": false, // 键入一行后是否自动格式化该行
	"editor.formatOnPaste": false, // 是否自动格式化粘贴的内容
	// #每次保存的时候将代码按eslint格式进行修复 使用eslint 風格使用standard 進行代碼規則限制
	"editor.fontWeight": "200",
	"workbench.activityBar.visible": true,
	"workbench.statusBar.visible": true,
	"workbench.colorTheme": "Default Dark+",
	"workbench.editorAssociations": {
		"*.vsd": "default"
	},
	// "workbench.colorTheme": "SynthWave '84",
	// "workbench.iconTheme": "vscode-icons-mac",
	"team.showWelcomeMessage": false,
	"editor.renderWhitespace": "boundary",
	"editor.cursorBlinking": "smooth",
	"editor.minimap.enabled": true,
	"editor.minimap.renderCharacters": false,
	"window.title": "${dirty}${activeEditorMedium}${separator}${rootName}",
	"editor.codeLens": true,
	// eslint 代码自动检查相关配置
	"eslint.enable": true,
	"eslint.run": "onType",
	"eslint.options": {
		"configFile": "D:/.eslintrc.js",
		"plugins": ["html"],
		"extensions": [".js", ".vue"]
	},
	// 添加 vue 支持
	"eslint.validate": ["javascript", "javascriptreact", "html", "vue"],
	// #让prettier使用eslint的代码格式进行校验 true
	"prettier.eslintIntegration": true,
	// #去掉代码结尾的分号（true / false）（建议不要去掉 ： true）
	"prettier.semi": true,
	// #使用单引号替代双引号（建议不要替代：false）
	"prettier.singleQuote": false,
	"prettier.tabWidth": 4, // 每个制表符占用的空格数
    // 指定添加尾后逗号的方式。选项：none──无尾后逗号、 es5──在 ES5 中有效的尾后逗号（如对象与数组等）、 all──尽可能添加尾后逗号（如函数参数）。
    // "prettier.trailingComma": "none",
	// #让函数(名)和后面的括号之间加个空格 true
	"javascript.format.insertSpaceBeforeFunctionParenthesis": true,
	// #这个按用户自身习惯选择 html格式化
	"vetur.format.defaultFormatter.html": "js-beautify-html",
	// #让vue中的js按"prettier"格式进行格式化
	"vetur.format.defaultFormatter.js": "prettier",
	// #让vue中的js按编辑器自带的ts格式进行格式化
	// "vetur.format.defaultFormatter.js": "vscode-typescript",
	"vetur.format.defaultFormatterOptions": {
		"js-beautify-html": {
			// #vue组件中html代码格式化样式
			"wrap_attributes": "force-aligned", // 也可以设置为"auto", 效果会不一样
			"wrap_line_length": 200,
			"end_with_newline": false,
			"semi": false,
			"singleQuote": true
		},
		"prettier": {
			"semi": false,
			"singleQuote": true
		}
	},
	"[jsonc]": {
		"editor.defaultFormatter": "esbenp.prettier-vscode"
	},
	// 格式化stylus, 需安装Manta's Stylus Supremacy插件
	"stylusSupremacy.insertColons": false, // 是否插入冒号
	"stylusSupremacy.insertSemicolons": false, // 是否插入分号
	"stylusSupremacy.insertBraces": false, // 是否插入大括号
	"stylusSupremacy.insertNewLineAroundImports": false, // import之后是否换行
	"stylusSupremacy.insertNewLineAroundBlocks": false, // 两个选择器中是否换行
	// "prettier.useTabs": true, // 使用制表符（tab）缩进
	"explorer.confirmDelete": false,
	"[javascript]": {
		"editor.defaultFormatter": "esbenp.prettier-vscode"
	},
	"[json]": {
		"editor.defaultFormatter": "esbenp.prettier-vscode"
	},
	"diffEditor.ignoreTrimWhitespace": false,
	"[javascriptreact]": {
		"editor.defaultFormatter": "esbenp.prettier-vscode"
	},
	"leek-fund.fundSort": 2, // 两个选择器中是否换行
	// "terminal.integrated.shell.osx": "zsh",
 
	"files.associations": {
		"*.cjson": "jsonc",
		"*.wxss": "css",
		"*.wxs": "javascript"
	},
	"emmet.includeLanguages": {
		"wxml": "html"
	},
	"minapp-vscode.disableAutoConfig": true,
	"window.menuBarVisibility": "visible",
	// 调整窗口的缩放级别
	"window.zoomLevel": 1,
	"git.autofetch": true,
	"git.confirmSync": false,
	"git.enableSmartCommit": true,
	"git.ignoreLegacyWarning": true,
	// "git.path": "D:/git/Git/mingw64/bin/git.exe",
	"liveServer.settings.donotShowInfoMsg": true,
	"[html]": {
		"editor.defaultFormatter": "vscode.html-language-features"
		// "editor.defaultFormatter": "esbenp.prettier-vscode"
	},
	"javascript.updateImportsOnFileMove.enabled": "always",
	// 字體大小
	"editor.fontSize": 15,
	"files.exclude": {
		"node_modules/": true
	},
	// 設置行高
	"editor.lineHeight": 20,
	"search.followSymlinks": false,
	"seetingsSync.ignoredExtensions": [],
	"workbench.sideBar.location": "left",
	"vscode_custom_css.policy": true,
	"vscode_custom_css.imports": [
		"file:///C:/vscode-transparent/synthwave84.css",
		"file:///C:/vscode-transparent/toolbar.css",
		"file:///C:/vscode-transparent/vscode-vibrancy-style.css",
		"file:///C:/vscode-transparent/enable-electron-vibrancy.js"
	],
	// 高亮的颜色，emm暂时只支持这样写
	"wxmlConfig.activeColor": {
		"color": "#e5c07b"
	},
	// 是否禁用高亮组件
	"wxmlConfig.activeDisable": false,
	// 是否开启保存自动格式化
	"wxmlConfig.onSaveFormat": false,
	"wxmlConfig.format": {
		"brace_style": "collapse",
		"end_with_newline": false,
		"indent_char": "",
		"indent_handlebars": false,
		"indent_inner_html": false,
		"indent_scripts": "keep",
		"indent_size": 2,
		"indent_with_tabs": false,
		"max_preserve_newlines": 1,
		"preserve_newlines": false,
		"wrap_attributes": "force-expand-multiline"
	},
	// 高亮所忽略的组件数组
	"wxmlConfig.tagNoActiveArr": [
		"view",
		"button",
		"text",
		"icon",
		"image",
		"navigator",
		"block",
		"input",
		"template",
		"form",
		"camera",
		"textarea"
	],
	"zenMode.restore": true,
	"breadcrumbs.enabled": true,
	// "terminal.integrated.shell.windows": "C:\\WINDOWS\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
	// "[wxml]": {
	// 	"editor.defaultFormatter": "qiu8310.minapp-vscode"
	// },
	"gitlens.advanced.messages": {
		"suppressLineUncommittedWarning": true
	},
	"javascript.format.placeOpenBraceOnNewLineForControlBlocks": true,
	"vsicons.presets.hideFolders": true,
	"editor.cursorStyle": "line-thin",
	"editor.suggestSelection": "first",
	"vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue",
	"terminal.integrated.rendererType": "dom",
	"terminal.integrated.tabs.enabled": true,
	"vscode_vibrancy.opacity": 1,
	"npm.fetchOnlinePackageInfo": false,
	"tabnine.experimentalAutoImports": true,
	"[vue]": {
		"editor.defaultFormatter": "esbenp.prettier-vscode"
	},
	"files.autoSave": "onFocusChange", // "afterDelay" 控制自动保存未保存的编辑器
    // "files.autoSaveDelay": 100, // 之前经过的延迟（仅当 afterDelay 才适用）
	"projectManager.hg.maxDepthRecursion": 1,
	"projectManager.vscode.baseFolders": ["/Users/jimmy/Desktop"],
	"projectManager.any.baseFolders": ["/Users/jimmy/Desktop/PROJECT"],
	"projectManager.any.maxDepthRecursion": 1,
	"[scss]": {
		"editor.defaultFormatter": "esbenp.prettier-vscode"
	}
	// "sonarlint.rules": {},
	// "sonarlint.output.showVerboseLogs": true,
}
```
说明：代码格式化使用prettier-eslint，行尾不加分号，tabWidth为2，使用单引号，保存的时候自动格式化。
#### 4.【建议】使用nvm管理node和npm版本。
说明：推荐node稳定版，可根据需要安装其他版本。



## 二、HTML规范
###  HTML规范
#### 1.【强制】html编写时也应书写相关代码块的注释，方便别人阅读并了解当前注释区域的代码功能等。
— 开始注释：`<!-- 注释文案 -->`   
— 结束注释：`<!-- /注释文案 -->`  
— 允许只有开始注释。

#### 2.【建议】应当以最严格的xhtml strict标准来嵌套，比如内联元素不能包含块级元素等等。
#### 3.【强制】正确闭合标签且必须闭合
#### 4.【强制】属性和值全部小写，每个属性都必须有一个值，每个值必须加双引号。
#### 5.【强制】没有值的属性必须使用自己的名称做为值（checked、disabled、readonly、selected等等）。
#### 6.【强制】省略style标签和script标签的type属性,因为无论现代和老的浏览器都可以正确识别。
#### 7.【强制】所有的代码都用小写字母：适用于元素名，属性，属性值（除了文本和 CDATA ）， 选择器，特性，特性值（除了字符串）
```html
   <!-- 不推荐 -->
    <DIV class="DIV-CLASS" DATA-TYPE="1">HELLO WORLD</DIV>
    <!-- 推荐, 比大写更容易阅读-->
    <div class="div-class" data-type="1">HELLO WORLD</div>
```
### （二）CSS规范
#### 1.【强制】class命名以小写字母开头，小写字母、下划线和数字组成。不建议使用驼峰法命名 class 的属性。以下是一些常用到的 class的名字。示例：
```css
    /* 包裹层 */
    .xx_wrap{}
    /* 列表 */
    .xx_list{} 
    /* 列表项 */
    .xx_list-item{}
    /* 左边内容 */
    .xx_left{}
    /* 中间内容 */
    .xx_middle{}
    /* 右边内容 */
    .xx_right{}
    /* 某个页面 */
    .xx_page{}
 ```
#### 2.【强制】CSS的class和id命名尽量简短，而非简化，必须为小写英文字母，示例：
```css
    /* 不推荐: 无意义 不易理解 */
    #zhongtiexinke-1901 {}

    /* 不推荐: 表达不具体 */
    .button-green {}
    .clear {}
    /* 推荐: 明确详细 */
    #gallery {}
    #login {}
    .video {}
    /* 推荐: 通用 */
    .aux {}
    .alt {}
    /* 不推荐 该简短的没有简短，不该简短的做了简化*/
    #navigation {}
    .atr {}
    /* 推荐 该简短的就简短，不该简短的要描述清楚*/
    #nav {}
    .author {}
```
#### 3.【强制】使用2个空格做为一个缩进层级，如想使用tab字符需要设置IDE一个tab等于2个空格
```css
  @media screen, projection {
    html {
      background: #fff;
      color: #444;
    }
  }
```
#### 4.【强制】所有声明都要用“;”结尾
```css
      /* 不推荐 */
      .test {
          display: block;
          height: 100px
      }
      /* 推荐 */
      .test {
          display: block;
          height: 100px;
      }
```
#### 5.【强制】规则分行，每个规则独立一行，两个规则之间隔行
```css
      /* 不推荐 */
      div {
          background: #fff; color: '#ffffff';
      }
      /* 推荐 */
      div {
          background: #fff; 
          color: '#ffffff';
      }
```
#### 6.【建议】 使用 border / margin / padding 等缩写时，应注意隐含值对实际数值的影响，确实需要设置多个方向的值时才使用缩写。
说明： border / margin / padding 等缩写会同时设置多个属性的值，容易覆盖不需要覆盖的设定。如某些方向需要继承其他声明的值，则应该分开设置。
```css
      article {
        margin: 5px;
        border: 1px solid #999;
      }
      /* 推荐 */
      .page {
        margin-right: auto;
        margin-left: auto;
      }
      .featured {
        border-color: #69c;
      }
      /* 不推荐 */
      .page {
        margin: 5px auto; / introducing redundancy /
      }
      .featured {
        border: 1px solid #69c; / introducing redundancy /
      }
```
#### 7.【强制】 带私有前缀的属性由长到短排列，按冒号位置对齐，不带前缀的一定要放在最后，示例：
```css
    .box {
        -webkit-box-sizing: border-box;
            -moz-box-sizing: border-box;
                box-sizing: border-box;
    }
```
#### 8.【强制】选择器和声明分行，每个选择器和声明都要独立新行
```css
    /* 不推荐 */
    h1, h2, h3 {
        font-weight: normal;
        line-height: 1.2;
    }
    /* 推荐 */
    h1,
    h2,
    h3 {
        font-weight: normal;
        line-height: 1.2;
    }
     /* 不推荐 */
    .content .title {
        font-size: 2rem;
    }
    /* 推荐 */
    .content > .title {
        font-size: 2rem;
    }
```
#### 9.【建议】选择器的嵌套层级应不大于 3 级，位置靠后的限定条件应尽可能精确
```css
/* 不推荐 */
  .main {
   .title { 
      .name { 
           color: #fff;  
             } 
        }
    }

  /* 推荐 */
    .main-title {
        .name { color: #fff; }
    }
```
#### 10.css性能优化及注意事项
+ 注意选择器的性能，不要使用低性能的选择器
+ 禁止在css中使用*选择符
+ 0后面不需要单位，比如0px可以省略成0，0.8px可以省略成.8px
+ 如果是16进制表示颜色，则颜色取值应该大写。
+ 如果可以，颜色尽量用三位字符表示，例如#AABBCC写成#ABC
+ 如果没有边框时，不要写成border:0，应该写成border:none
+ 在保持代码解耦的前提下，尽量合并重复的样式
+ background、font等可以缩写的属性，尽量使用缩写形式；
+ 书写代码前, 考虑并提高样式的重复使用率
+ 不要轻易改动通用的CSS库，如改动，需要经过全面的测试
+ 避免过小的图片平铺
+ 绝对不要在CSS中使用“*”选择符
+ css命名尽量采用class类名
+ 大区块样式必须添加注释, 小区块适量注释
+ 减少使用影响性能的属性, 比如position:absolute || float

## 三、JavaScript规范
### 三 JavaScript规范
JavaScript规范应在遵守现有ES5规范的基础上，尽量拥抱ES6/7规范，因为后者是未来JavaScript发展的方向，并且现有的新框架和工具库都鼓励使用新语法。
#### 1.【强制】代码缩进问题，统一使用2个空格缩进，在不同的IDE中如果使用tab缩进，一定要设置IDE的tab缩进为2个空格。
#### 2.【建议】注释要求，每一个函数(方法)必须书写代码注释，注释的书写应突出为什么要这么写，以及这么写的作用，而不能仅仅注释函数(方法)的简介，示例:
```js
    /** 
    * 函数说明 
    * @关键字 
    */
    /**
     * 合并Grid的行
     * @param {Grid} grid 需要合并的Grid
     * @param {Array} cols 需要合并列的Index(序号)数组；从0开始计数，序号也包含。
     * @param {Boolean} isAllSome 是否2个tr的cols必须完成一样才能进行合并。true：完成一样；false(默认)：不完全一样
     * @return void
     * @author barry
     */
    function mergeCells(grid, cols, isAllSome) {
        // Do Something
    }
```
#### 3.【强制】变量命名规范：小驼峰式命名法。
命名建议：尽量在变量名字中体现所属类型，如:length、count等表示数字类型；而包含name、title表示为字符串类型
```js
    // 好的命名方式
    const maxCount = 10;
    const tableTitle = 'LoginTable';
    // 不好的命名方式
    const setCount = 10;
    const getTitle = 'LoginTable';
```

 #### 4.【强制】常量命名规范：名称全部大写，使用大写字母和下划线来组合命名，下划线用以分割单词。

```js
    const MAX_COUNT = 10;
    const URL = 'http://www.crecg.cn';
```
#### 5.【强制】构造函数命名规范：大驼峰式命名法，首字母大写。
```js
    function Student(name) {
        this.name = name;
    }
    var st = new Student('tom');
```
#### 5.【强制】运算符之==和===。
项目中强制使用===,当值类型不固定是使用==
#### 6.【强制】对象命名规则：小驼峰式命名法
命名建议：尽量在名字中体现出对象的整体功能和作用等
## 四、Vue.js规范
### Vue.js规范
#### 1.【强制】组件名为多个单词，采用大驼峰命名法(帕斯卡命名法)
```js
    // 反例
    export default {
        name: 'item'
    }
    // 正例 
    export default {
        name: 'PageArticleItem'
    }
```
#### 2.【强制】组件的名字应该采用大驼峰命名法(帕斯卡命名法)，一方面可与组件名一致，使项目更加清晰，另一方面这样的写法对编辑器引入也很友好, 示例:
```js
    // 反例 
    ├── index.html
    ├── main.js
    └── components
        ├── page-header
        ├── PageArticle
        └── pageheader
    // 正例
    ├── index.html
    ├── main.js
    └── components
        ├── PageHeader
        ├── PageArticle
        └── PageHeader
```
对于例如按钮、下拉框或表格这样的基础组件应该始终以一个特定的前缀开头，区别与其他业务组件。
```js
    // 反例
    ├── index.html
    ├── main.js
    └── components
        ├── page-header
        ├── page-article
        ├── page-header
        ├── crec-button
        ├── crec-select
        └── crec-table
    // 正例
    ├── index.html
    ├── main.js
    └── components
    |   ├── PageHeader
    |   ├── PageArticle
    |   └── PageHeader
    └── base
        ├── CrecButton
        ├── CrecSelect
        └── CrecTable
```
#### 3.【强制】定义 Prop 的时候应该始终以驼峰格式（camelCase）命名，在父组件赋值的时候使用连接线（-）。这里遵循每个语言的特性，因为在 HTML 标记中对大小写是不敏感的，使用连接线更加友好；而在 JavaScript 中更自然的是驼峰命名,示例:
```vue
    // 反例
    // Vue
    props: {
        article-status: Boolean
    }
    // HTML
    <article-item :articleStatus="true"></article-item>
    // 正例
    // Vue
    props: {
        articleStatus: Boolean
    }
    // HTML
    <article-item :article-status="true"></article-item>
```
#### 4.【强制】Prop 定义应该尽量详细。示例:
```vue
    // 反例
    props: ['attrM', 'attrA', 'attrZ']
    // 正例
    props: {
    // 组件状态，用于控制组件的颜色
    status: {
     type: String,
     required: true,
     validator: function (value) {
       return [
         'succ',
         'info',
         'error'
       ].indexOf(value) !== -1
     }
   },
    // 用户级别，用于显示皇冠个数
    userLevel：{
      type: String,
      required: true
   }
}
```
#### 5.【强制】在执行 v-for 遍历的时候，总是应该带上key值使更新 DOM 时渲染效率更高。
```vue
    // 反例
    <ul>
        <li v-for="item in list">
            {{ item.title }}
        </li>
    </ul>
    // 正例
    <ul>
        <li v-for="item in list" :key="item.id">
            {{ item.title }}
        </li>
    </ul>
```
#### 6.【建议】v-for应该避免与v-if在同一个元素 (例如在li标签) 上使用，因为v-for的优先级比 v-if 更高，为了避免无效计算和渲染，应该尽量将 v-if 放到容器的父元素之上，示例：
```vue
    // 反例
    <ul>
        <li v-for="item in list" :key="item.id" v-if="showList">
            {{ item.title }}
        </li>
    </ul>
    // 正例
    <ul v-if="showList">
        <li v-for="item in list" :key="item.id">
            {{ item.title }}
        </li>
    </ul>
```
#### 7.【建议】若同一组 v-if 逻辑控制中的元素逻辑相同，Vue 为了更高效的元素切换，会复用相同的部分，例如：value。为了避免复用带来的不合理效果，应该在同种元素上加上 key 做标识。
```vue
    // 反例
    <div v-if="hasData">
        <span>{{ crecData }}</span>
    </div>
    <div v-else>
        <span>无数据</span>
    </div>
    // 正例
    <div v-if="hasData" key="crec-data">
        <span>{{ crecData }}</span>
    </div>
    <div v-else key="crec-none">
        <span>无数据</span>
    </div>
```
#### 8.【强制】模板中使用简单的表达式,示例:
组件模板应该只包含简单的表达式，复杂的表达式则应该重构为计算属性或方法。复杂表达式会让你的模板变得不那么声明式。我们应该尽量描述应该出现的是什么，而非如何计算那个值。而且计算属性和方法使得代码可以重用。
+ 反例
```vue
   <template>
     <p>
        {{
            fullName.split(' ').map(function (word) {
                return word[0].toUpperCase() + word.slice(1)
            }).join(' ')
        }}
        </p>
    </template>   
```
+ 正例
```vue
    <template>
    <p>{{ normalizedFullName }}</p>
    </template>
    /* 复杂表达式已经移入一个计算属性 */
    computed: {
    normalizedFullName: function () {
        return this.fullName.split(' ').map(function (word) {
        return word[0].toUpperCase() + word.slice(1)
        }).join(' ')
      }
    }   
```
#### 9.【强制】router 中的命名规范,示例:
```bash
// 动态加载
export const reload = [
  {
    path: '/reload/index',
    name: 'reload',
    component: Main,
    meta: {
      title: '动态加载',
      icon: 'icon iconfont'
    },
    children: [
      {
        path: '/reload/smartReloadList',
        name: 'SmartReloadList',
        meta: {
          title: 'SmartReload',
          childrenPoints: [
            {
              title: '查询',
              name: 'smart-reload-search'
            },
            {
              title: '执行reload',
              name: 'smart-reload-update'
            },
            {
              title: '查看执行结果',
              name: 'smart-reload-result'
            }
          ]
        },
        component: () =>
          import('@/views/reload/smartReloadList.vue')
      }
    ]
  }
];
```
#### 10.【强制】为了统一和便于阅读，应该按`<template> `、`<script>`、`<style>`的顺序放置,示例:
+ 反例
```vue
  <style>
  /* CSS */
  </style>
  <script>
  /* JavaScript */
  </script>
  <template>
  <!-- HTML -->
  </template>
```
+ 正例
```vue
  <template>
  <!-- HTML -->
  </template>
  <script>
  /* JavaScript */
  </script>
  <style>
  /* CSS */
  </style>
```
#### 11.【强制】Vue 项目目录规范。示例:
```js
    src                                  源码目录
    |-- api                              所有api接口
    |-- assets                           静态资源，images, icons, styles等
    |-- components                       公用组件
    |-- config                           配置信息
    |-- constants                        常量信息，项目所有Enum, 全局常量等
    |-- directives                       自定义指令
    |-- filters                          过滤器，全局工具
    |-- datas                            模拟数据，临时存放
    |-- lib                              外部引用的插件存放及修改文件
    |-- mock                             模拟接口，临时存放
    |-- plugins                          插件，全局使用
    |-- router                           路由，统一管理
    |-- store                            vuex, 统一管理
    |-- themes                           自定义样式主题
    |-- views                            视图目录
    |   |-- role                                 role模块名
    |   |-- |-- index.vue                        role主页面
    |   |-- |-- roleAdd.vue                      role新建页面
    |   |-- |-- roleUpdate.vue                   role更新页面
    |   |-- |-- index.less                       role模块样式
    |   |-- |-- components                       role模块通用组件文件夹
```
#### 12.【强制】Vue api目录规范。示例:
```js
    src                                  源码目录
    |-- api                              所有api接口
    |   |-- role                         role模块名
    |   |-- commonApi                    公共接口页面（页面调用一次以上放入）
```
#### 12.【强制】Vue 请求函数统一使用。示例:
+ 反例
```js
    export function listDefinition(query) {
    return request({
        url: '/workflow/processDefinition/list',
        method: 'get',
        params: query
    })
    }
   export const findTransportateInspecteStatisticsDLDRQ = (sszf, sbid,type) => {
   return request({
        url: '/ef-business-pc/newOtherDeviceView/findTransportateInspecteStatisticsDLDRQ?sszf=' + sszf + '&sbid=' + sbid+ '&type=' + type,
        method: 'get'
    })
    }
```
+ 正例
 ```js
    export function addJob(data) {
    return request({
        url: '/schedule/job',
        method: 'post',
        data
    })
    }

    export function addJob(params) {
    return request({
        url: '/schedule/job',
        method: 'post',
        params
    })
    }
```
