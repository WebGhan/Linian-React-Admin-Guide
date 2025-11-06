# 编码规范

> 规范的约束力强弱依次为【强制】、【建议】两类。

## JavaScript

### 变量命名

【强制】使用小驼峰式命名（camelCase）

### 注释

【强制】请严格遵守 [JSDoc](https://jsdoc.app/) 规范。

## CSS

### 选择器

- 【强制】除了全局覆盖样式，禁止使用通用选择器 *
- 【强制】除了全局覆盖样式，禁止使用标签选择器
- 【强制】非必要不使用 ID 选择器
- 【建议】选择器使用短划线命名方式
- 【建议】应减少选择器的嵌套，使用嵌套也尽量不要超过 3 层

风格示范：

```css
/* 好的例子 */
.layout {}
.layout-head {}
.layout-head-title {}

/* 反例 */
.layout {}
.layout .head {}
.layout .head .title {}
```

### 属性书写顺序

【建议】遵循以下顺序：
1. 类型：display
2. 布局定位：flex / float / position ...
3. 盒模型：margin / padding / width / height / border ...
4. 文字排版：text-align / line-height / font ...
5. 颜色背景：color / background ...
6. 其他：opacity / cursor / box-shadow / transform / animation ...

### 浏览器私有前缀写法

【强制】Vite 打包时会自动处理 CSS 私有前缀，除非特殊情况，一般不用写私有前缀。
