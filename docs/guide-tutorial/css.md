# CSS 样式

## 直接使用 CSS

```css title="example.css"
.title {
  text-align: center;
  font-weight: bold;
}
```

导入 CSS 文件可以直接使用样式：

```jsx
import './example.css'

function example() {
  return <div className="title">文字</div>
}
```

:::warning

直接引入 CSS 文件，会产生样式全局污染问题，我们通常使用 CSS Modules 技术。

:::

## CSS Modules

CSS Modules 的核心作用是解决 CSS 样式全局污染问题。CSS Modules 会自动将类名编译为唯一哈希值（如 button 可能变成
Button__button--1a2b3），确保每个类名仅在当前模块（文件）内有效，从根本上避免冲突。

任何以 `.module.css` 为后缀名的 CSS 文件都被认为是一个 CSS modules
文件。可参考 [CSS Module 文档](https://cn.vitejs.dev/guide/features.html#css-modules)。

```css title="example.module.css"
.red {
  color: red;
}
```

导入这样的文件会返回一个相应的模块对象。

```jsx
import styles from './example.module.css'

function example() {
  return <div className={styles.red}>文字</div>
}
```

### 覆盖样式

有时候我们需要覆盖第三方组件的样式，使用 `:global()` 可以让内部的选择器跳过哈希化，保持全局生效，从而覆盖其他模块的样式。

```css
/* 用 :global() 包裹需要全局生效的选择器 */
:global(.ant-btn) {
  background: red; /* 覆盖 Antd 按钮的背景色 */
}

/* 也可以嵌套使用，限制作用范围 */
.container :global(.ant-btn) {
  background: red /* 仅覆盖 .container 内的 Antd 按钮 */
}
```

