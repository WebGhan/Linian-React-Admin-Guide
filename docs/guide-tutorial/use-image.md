# 使用图片

## 组件中引用图片

```jsx
import exampleImg from '/src/assets/images/example.jpg';

function Example() {
  return (
    <img src={exampleImg} alt=""/>
  );
}
```

## 样式中使用图片

⚠️ 注意：样式中引用图片要以 `/` 开头，否则在 `build` 构建后，生成的 URL 可能是错误的。

```css
.background {
  background-image: url('/src/assets/images/example.png');
}
```
