# 前言

1. 主要解决频繁更替自己的简历文件，可以使用markdown语法编辑简历。
2. 面试也可以给自己加分

## 特性

- 基于 Vite 的开发、简历预览、打包的丝滑体验
- 生成 HTML、PDF
- 基于 Github Actions 实现的 Github Pages 自动部署以及 PDF 自动生成

## 使用方式

### 项目启动

``` bash
pnpm install
pnpm run dev //本地开发
pnpm run build //打包
```

### 配置自动部署

1. github对应的仓库需要配置action选项token字段，字段名为`ACTION_TOKEN`
2. 需要修改`workflow`文件夹下面`yml`文件配置自己的域名
3. `.yml`文件夹下有一个`CNAME`，这个是在域名解析时候映射第三方域名使用（域名需要备案）
4. 配置好自己的`githubpage`
5. 剩下就是自己布局，提交代码就好了，然后访问自己设置的域名


## 配置

**配置文件：** `vite.config.js`

所有配置都需要在 Vite 的插件配置中进行，目前支持的配置如下：

```js
import { defineConfig } from 'vite';
import resumeBuild from './src/plugin';
import markdownItImsize from 'markdown-it-imsize';

export default defineConfig({
  base: './',
  plugins: [
    resumeBuild({
      // 对 markdown-it 的实例进行配置
      markdown(md) {
        // 增加一个 markdown-it 插件
        md.use(markdownItImsize);
      },

      // 生成的 PDf 名称
      pdfName: '姚明飞个人简历',

      // PDF 的边距，会被 `@page { margin: 0px; }` 样式覆盖
      pdfMargin: 0,

      // 生成的 HTML 的 Title
      webTitle: '姚明飞个人简历'
    })
  ]
});
```

## Markdown 编写

本项目使用 `markdown-it` 进行解析，并且默认安装了某些 `markdown-it` 插件对 Markdown 进行语法增强。

### markdown-it-container

增强布局

使用前：
``` html
:::
# 姚明飞
求职意向：高级前端 / 26k / 上海
:::
```

### markdown-it-attrs

添加 `html` 属性，如：`class` 、 `id`。
``` html
::: {.header}
# 姚明飞 {.name}
求职意向：高级前端 / 26k / 上海
:::
```

## 示例

[姚明飞个人简历](https://www.yaomingfei.info)

## 参考
[markdown-to-resume](https://github.com/yuexiaoliang/markdown-to-resume)

