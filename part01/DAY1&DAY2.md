## Storybook与其设计系统

storybook是我见过目前市面上社区最活跃，插件最丰富的组件库制作工具了。

说到storybook，就应该说说它的设计系统。

### 什么是设计系统？

我一开始也没明白设计系统是什么，以为只是做个组件库就叫设计系统？

后来翻阅各种他们社区文章后发现这么一句：

```
If a UI pattern is used more than three times, turn it into a reusable UI component.
If a UI component is used in 3 or more projects/teams, put it in your design system.
```

翻译下就是，**如果一个样式被复用过3次，那么这个样式应该写到组件里，如果一个组件被复用3次以上，那么这个组件应该拿来做成设计系统。**

![](https://www.learnstorybook.com/design-systems-for-developers/design-system-contents.jpg)



```
A design system consolidates common UI components in a central well-maintained repository that gets distributed via a package manager. Developers import standardized UI components instead of pasting the same UI code in multiple projects.

Most design systems aren’t built from scratch. Instead, they’re assembled from tried-and-true UI components used across a company which are repackaged as a design system. Our project is no exception. We’ll cherry-pick components from existing production component libraries to save time and deliver our design system to stakeholders faster.
```

简单意思就是已经被验证的基本组件会被放入设计系统中，然后通过设计系统进行二次开发或者调整风格直接进行复用。

### 如何构建一个设计系统？

storybook制作了个给开发人员文档书

https://www.learnstorybook.com/design-systems-for-developers

这里面基本写了制作设计系统会遇到的问题。

### 什么是原子设计系统？

storybook的出现，也让原子设计系统兴起。

可以看一下原子设计系统的创始人Brad Frost制作的完美贯彻原子设计系统的网站https://bradfrostdotcom-pl.netlify.app/?p=pages-homepage

这个案例并非storybook制作，但storybook官网也有引用他说的一段话：

```
“Storybook is a powerful frontend workshop environment tool that allows teams to design, build, and organize UI components (and even full screens!) without getting tripped up over business logic and plumbing.”
```

原子设计系统主要是通过原子造分子，一直造下去，直至把整个网页造出来。

我以前在群里吹牛聊起过原子设计系统，其中有人觉得，将所有css进行语义化之后写网页就是原子设计。我个人觉得这是个错误的理解。原子设计的目的不仅是在于复用原子，更需要复用分子，复用组织，复用整体，如果仅仅是复用原子，那就没什么意思，反而让人在类名上不断重复写一长串。

### 什么是CDD？

CDD是组件驱动开发(Component-Driven Development)。

模块化是软件开发的原则，随着现在react等框架兴起，模块化通过组件形式在软件应用程序设计中存在。这样催生了一种新的模块化形式，称为**CDD**，即**组件驱动开发**。通过了解CDD以及如何利用CDD，我们可以使用组件来驱动应用程序的开发，从而受益于这种新的模块化带来的优势。

原子设计其实是CDD的一种实现模式，CDD的好处有很多：

- **更快的开发**：将开发分为组件，使您可以使用重点狭窄的API构建模块化的部件。这意味着构建每个组件并学习的时间会更快。
- **维护更简单**：当您需要修改或更新应用程序的一部分时，可以扩展或更新组件，而不必重构应用程序的较大部分。可以将其视为对特定器官而不是整个身体系统进行手术。
- **更好的可重用性**：通过分离关注点，组件可以被重用和扩展以构建多个应用程序，而不必一遍又一遍地重写它们 。
- **更好的TDD**：构建模块化组件时，执行单元测试以验证每个组件的重点功能变得容易得多。大型系统可以更容易地进行测试，因为它更容易理解和区分系统各部分的职责。
- **较短的学习曲线**：当开发人员必须投入新项目时，学习和理解已定义组件的结构比投入整个应用程序要容易得多。
- **更好的系统建模**：当系统由模块化组件组成时，更易于掌握，理解和操作。



###  通用化还是定制化？

storybook的关注点和优势主要是在定制化上并非通用化（这在storybook官网上有写，原句是他们做的这个不与通用型组件库竞争），我个人做的这个组件库是一种通用化设计，而antd，elementui等等也是一种通用化设计。

对于一个公司来说，定制化的组件库往往是比较好的策略，本次训练营将带你探索定制化原子设计系统的实现。如果想自由发挥做通用型组件库的可以参考我的仓库https://github.com/yehuozhili/bigbear-ui



## 今日作业 

storybook贴心的为大家做了基于cra的cli，直接使用基于cra的配置，避免配置繁琐。

首先使用npm或者yarn建一个cra的typescript项目。**注意，最好别用cnpm 并且最好别混用安装工具，否则可能会产生冲突。**

```
create-react-app  yourProjectName --template typescript
```

之后使用storybook的cli进行安装

```
npx -p @storybook/cli sb init --type react_scripts
```

安装完毕后，src目录下会有个stories的文件夹，里面做了2个stories的示例。

package.json里有启动storybook的命令。

使用npm run storybook即可看见构建后的故事书样例。

仅有这些工具并不够用。storybook提供了丰富的插件。

打开根目录下的.storybook文件夹，其中main.js的配置：

```javascript
module.exports = {
  stories: ['../src/**/*.stories.js'],
  addons: [
    '@storybook/preset-create-react-app',
    '@storybook/addon-actions',
    '@storybook/addon-links',
  ],
};
```

默认提供了actions插件和links插件。

actions插件有点像jest的fn一样，用来在触发事件时显示在action面板上，避免人为打开控制台查看输出了啥。

actions插件文档地址https://github.com/storybookjs/storybook/tree/master/addons/actions

links插件用来在各个故事书中进行跳转，相当于a标签一样，是个很常用的插件。

links插件文档地址https://github.com/storybookjs/storybook/tree/master/addons/links

除了这几个，还有些比较常用而且好用的插件：

viewport插件，用来自由调整视口大小。

插件文档地址https://github.com/storybookjs/storybook/tree/master/addons/viewport

knob插件，用来调整输入范例。

插件文档地址https://github.com/storybookjs/storybook/tree/master/addons/knobs

docs插件，用来制作文档。

插件文档地址https://github.com/storybookjs/storybook/tree/master/addons/docs

a11y插件，用来自动检测组件是否支持视障人士等规范的。

插件文档地址https://github.com/storybookjs/storybook/tree/master/addons/a11y

source插件，故事书上的源码映射。

插件文档地址https://github.com/storybookjs/storybook/tree/master/addons/storysource

这里我们把上面的都装上。使用-D安装上述组件，并配置如下：

```javascript
module.exports = {
	stories: ["../src/**/*.stories.js"],
	addons: [
		"@storybook/preset-create-react-app",
		"@storybook/addon-actions",
		"@storybook/addon-links",
		"@storybook/addon-viewport",
		"@storybook/addon-knobs",
		"@storybook/addon-docs",
		"@storybook/addon-a11y",
		"@storybook/addon-storysource",
	],
};
```

重新使用npm run storybook打开，可以发现页面多了很多工具，有了这些工具，就能使我们开发一个更完备的组件。

下面说下webpack配置。

尽管cra内部已经配了webpack，但实际storybook用来构建的webpack设置是抄cra的，2个用的不是一个webpack，实际这个项目有3个webpack，为了满足多样的需求，仍需要对webpack进行配置。

storybook内部分为2个应用，一个应用用来构建storybook自己的ui，一个应用就是我们用户所配置的应用，通过main.js进行注入。

其中，managerWebpack为storybook自己ui的webpack，一般不需要配置，需要做处理的是webpackFinal，这个是用户的webpack配置。

由于doc插件不支持ts，为了使doc插件支持typescript，以及story支持tsx，将配置进行更改：

```javascript
module.exports = {
	stories: ["../src/**/*.stories.tsx"],
	addons: [
		"@storybook/preset-create-react-app",
		"@storybook/addon-actions",
		"@storybook/addon-links",
		"@storybook/addon-viewport",
		"@storybook/addon-knobs",
		"@storybook/addon-docs",
		"@storybook/addon-a11y",
		"@storybook/addon-storysource",
	],
	webpackFinal: async (config) => {
		config.module.rules.push({
			test: /\.(ts|tsx)$/,
			use: [
				{
					loader: require.resolve("react-docgen-typescript-loader"),
				},
			],
		});
		config.resolve.extensions.push(".ts", ".tsx");
		return config;
	},
};
```

将文件进行更改，stories文件夹下的button删除，welcome的后缀名改为tsx。

新建components文件夹，文件夹里建个button文件夹，先试着写个例子，看配置是否生效。

button下的index.tsx

```typescript
import React, { ButtonHTMLAttributes, PropsWithChildren } from "react";

interface ButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {}

function Button(props: PropsWithChildren<ButtonProps>) {
	const { children, ...rest } = props;
	return <button {...rest}>{children}</button>;
}
export default Button;
```

button下的button.stories.tsx

```typescript
import React from "react";
import { action } from "@storybook/addon-actions";
import Button from "./index";

export default {
	title: "Button",
	component: Button,
};

export const Text = () => (
	<Button onClick={action("clicked")}>Hello Button</Button>
);

export const Emoji = () => (
	<Button onClick={action("clicked")}>hello storybook</Button>
);

```

将cra产生的多余文件删除，保留setupTest.ts和react-app-env.d.ts。一个用来测试用的，一个用来编译用的。

重新打开storybook，出现自己的button以及docs文档下自动获取的属性值就成功了。

### STYLED-COMPONENTS

原子设计系统比较推崇css in js的使用方式，便于对各种属性变量进行控制以及复用。如果是通用型组件库会使用类名进行控制，并且仍会有不少属性是必须使用js才能实现的，所以定制型组件库推荐使用styled components这种css in js的实现方式。

首先进行安装styled-components，以及其声明文件。

```
npm install  styled-components @types/styled-components -D
```

对昨天留下的button进行样式替换：

```typescript
import React, { ButtonHTMLAttributes, PropsWithChildren } from "react";
import styled from "styled-components";

const Mybutton = styled.button({
	color: "red",
});

interface ButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {}

function Button(props: PropsWithChildren<ButtonProps>) {
	const { children, ...rest } = props;
	return <Mybutton {...rest}>{children}</Mybutton>;
}
export default Button;
```

打开storybook，文字变红则成功生效。

styled-components更多用法参考官网https://styled-components.com/docs/basics

### 全局样式与插件

全局样式一般是用来抹平浏览器默认差异的。

以前的做法是使用reset.css，现在普遍做法是使用normalize.css，antd的全局样式也是normalize.css上改的。

normalize.css地址https://necolas.github.io/normalize.css/latest/normalize.css

在components下新建shared文件夹，用来存放通用样式。

新建global.tsx ，我们使用styled-component作为GlobalStyle变量加进来。由于normalize注释里面有些反引号，为防止最后编译有问题，去掉所有注释。

```typescript
import { createGlobalStyle } from "styled-components";

export const GlobalStyle = createGlobalStyle`
... 
...
...
```

对于全局插件，storybook在编译时会先去.storybook文件夹下执行preview文件。

我们将全局样式与全局插件添加至这里：

preview.js

```javascript
import React from "react";
import { GlobalStyle } from "../src/components/shared/global";
import { addDecorator, addParameters } from "@storybook/react";
import { withA11y } from "@storybook/addon-a11y";

addParameters({
	options: {
		showRoots: true,
	},
	dependencies: {
		withStoriesOnly: true,
		hideEmpty: true,
	},
});
addDecorator(withA11y);
addDecorator((story) => (
	<>
		<GlobalStyle />
		{story()}
	</>
));

```

我们可以运行storybook然后检查控制台。

如果控制台出现报错：

```
Cannot update during an existing state transition (such as within `render`)...
```

不用理会，这是viewport插件产生的错误。低版本react下不会产生此错误。

查看canvas的html，如果上面line-height为1.15，下面还有个text-size-adjust则配置成功。

### TOKEN制作

token是原子化的关键，有了styled-component，便于我们将所有样式token化。

#### 颜色

对于颜色，通常情况是设置其中性色与主题色。除了这些颜色，可能还有边框颜色等等。

将颜色统一做成一个token并导出，后续使用时即可保证颜色风格的统一。

shared下新建style.tsx:

```javascript
import { css } from "styled-components";

export const color = {
	// Palette
	primary: "#FF4785",
	secondary: "#1EA7FD",
	tertiary: "#DDDDDD",

	orange: "#FC521F",
	gold: "#FFAE00",
	green: "#66BF3C",
	seafoam: "#37D5D3",
	purple: "#6F2CAC",
	ultraviolet: "#2A0481",

	// Monochrome
	lightest: "#FFFFFF",
	lighter: "#F8F8F8",
	light: "#F3F3F3",
	mediumlight: "#EEEEEE",
	medium: "#DDDDDD",
	mediumdark: "#999999",
	dark: "#666666",
	darker: "#444444",
	darkest: "#333333",

	border: "rgba(0,0,0,.1)",

	// Status
	positive: "#66BF3C",
	negative: "#FF4400",
	warning: "#E69D00",
};
```

除了上述颜色，背景色与一般颜色也不太一样，可以单独做个token：

```javascript
export const background = {
	app: "#F6F9FC",
	appInverse: "#7A8997",
	positive: "#E1FFD4",
	negative: "#FEDED2",
	warning: "#FFF5CF",
};
```

#### 排版

排版除了字体大小，还有字重，字体类型。等等，根据需求自行设置：

```javascript
export const typography = {
	type: {
		primary:
			'"Nunito Sans", "Helvetica Neue", Helvetica, Arial, sans-serif',
		code://书写字体
			'"SFMono-Regular", Consolas, "Liberation Mono", Menlo, Courier, monospace',
	},
	weight: {
		regular: "400",
		bold: "700",
		extrabold: "800",
		black: "900",
	},
	size: {
		s1: "12",
		s2: "14",
		s3: "16",
		m1: "20",
		m2: "24",
		m3: "28",
		l1: "32",
		l2: "40",
		l3: "48",
	},
};
```

#### 间距与圆角

间距也是个特别常用的属性，依据个人对其进行设置：

```javascript
export const spacing = {
	padding: {
		small: 10,
		medium: 20,
		large: 30,
	},
	borderRadius: {
		small: 5,
		default: 10,
	},
};
export const breakpoint = 600;
export const pageMargin = 5;

```

### StoryOf&CSF&MDX

写故事一般有3种写法，一种是用StoryOf的API，一种是CSF，Component Story Format。一种是MDX，这里不讲第一种写法，本次训练营使用CSF+MDX形式组合制作。

默认故事书写法就是CSF，对于每个导出会有个名字，以及一些配置装饰器插件参数配置等等。

```javascript
import MyComponent from './MyComponent';

export default {
  title: 'Path/To/MyComponent',
  component: MyComponent,
  decorators: [ ... ],
  parameters: { ... }
}
```

默认情况下，每个导出代表一个故事。一个stories文件里只能有一个默认导出。

当安装了docs插件后，storybook便也可以支持MDX写法。

MDX是MD格式的变体，旨在用类似md和jsx的语法写文档。

storybook的MDX工作模式是通过MDX来映射成对应的CSF写法。所以其实2者最后写出来都是一个玩意。

由于MD文档的便捷性，推荐使用MDX写纯文档，CSF写带故事的组件。我的组件库使用的mdx写所有文档和包含故事的页面，个人认为虽然简单但效果不是很好。带有故事的用CSF写，然后配合TS可以检测出类型上的错误，如果用MDX写就检测不出类型上的问题，只有link或者发布后才能发现这些本该避免的问题。

为了支持MDX，对main.js后缀名进行扩展，同时配置docs插件对JSX的支持：

```javascript
	stories: ["../src/**/*.stories.(tsx|mdx)"],
	addons: [
		"@storybook/preset-create-react-app",
		"@storybook/addon-actions",
		"@storybook/addon-links",
		"@storybook/addon-viewport",
		"@storybook/addon-knobs",
		{ name: "@storybook/addon-docs", options: { configureJSX: true } },
		"@storybook/addon-a11y",
		"@storybook/addon-storysource",
	],
```

将Welcome.stories.tsx删除，建立自己的欢迎页Welcome.stories.mdx：

```
<Meta title="ATOM DESIGN /Intro" />

## ATOM DESIGN EXPLORE

<br />

作者：yehuozhili

此项目用来探索原子设计的实现

## 设计理念

balabalabala

## 安装

balabalabala

## 引入样式

balabalabala
```

mdx需要有个meta标签，对应着CSF写法的默认导出。 title中有分隔符存在，可以对标题与storyName进行分隔。

### 完成颜色与排版文档

颜色与排版token已经完成，剩下的是使用MDX展示这些token。

MDX的写法非常方便，并且支持导入。导入token并进行展示:

```jsx
import { Meta, ColorPalette, ColorItem } from "@storybook/addon-docs/blocks";

import { color } from "../components/shared/styles";

<Meta title="COLOR /Colors" />

# Colors

<ColorPalette>
	<ColorItem
		title="theme.color.primary"
		subtitle="Coral"
		colors={[color.primary]}
	/>
	<ColorItem
		title="theme.color.secondary"
		subtitle="Blue"
		colors={[color.secondary]}
	/>
	<ColorItem
		title="theme.color.tertiary"
		subtitle="Grey"
		colors={[color.tertiary]}
	/>
	<ColorItem
		title="theme.color.positive"
		subtitle="Green"
		colors={[color.positive]}
	/>
	<ColorItem
		title="theme.color.warning"
		subtitle="Ochre"
		colors={[color.warning]}
	/>
	<ColorItem
		title="theme.color.negative"
		subtitle="Red"
		colors={[color.negative]}
	/>
	<ColorItem
		title="theme.color.orange"
		subtitle="Orange"
		colors={[color.orange]}
	/>
	<ColorItem title="theme.color.gold" subtitle="Gold" colors={[color.gold]} />
	<ColorItem
		title="theme.color.green"
		subtitle="Green"
		colors={[color.green]}
	/>
	<ColorItem
		title="theme.color.seafoam"
		subtitle="Seafoam"
		colors={[color.seafoam]}
	/>
	<ColorItem
		title="theme.color.purple"
		subtitle="Purple"
		colors={[color.purple]}
	/>
	<ColorItem
		title="theme.color.ultraviolet"
		subtitle="Ultraviolet"
		colors={[color.ultraviolet]}
	/>
	<ColorItem
		title="Monochrome"
		colors={[
			color.darkest,
			color.darker,
			color.dark,
			color.mediumdark,
			color.medium,
			color.mediumlight,
			color.light,
			color.lighter,
			color.lightest,
		]}
	/>
</ColorPalette>
```

排版：

```jsx
import { Meta, Typeset } from "@storybook/addon-docs/blocks";

import { typography } from "../components/shared/styles";

<Meta title="Typography /Typography" />

# Typography

**Font:** Nunito Sans

**Weights:** 400(regular), 700(bold), 800(extrabold), 900(black)

<Typeset
	fontSizes={[
		Number(typography.size.s1),
		Number(typography.size.s2),
		Number(typography.size.s3),
		Number(typography.size.m1),
		Number(typography.size.m2),
		Number(typography.size.m3),
		Number(typography.size.l1),
		Number(typography.size.l2),
		Number(typography.size.l3),
	]}
	fontWeight={typography.weight.black}
/>

```

### 可选作业

cra的eslint使用了react-app的预设，如果有需要，可以设置额外的规则，参见eslint官网https://eslint.org/docs/rules/

除此之外，还有个很流行的插件 prettier ，结合vscode的prettier插件可以做到代码自动格式化。格式化规则可以自行选择。prettier官网https://prettier.io/docs/en/index.html