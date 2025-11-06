# 依赖

## 如何升级依赖

:::warning

请不要使用 `pnpm update` 一次性更新全部依赖！

:::

你应该明确知道要升级的依赖及其版本，一个一个的单独进行升级。使用 `pnpm` 更新依赖时，不要忘了版本号和版本控制符，否则
package.json 可能不会更新。

```
// 好的例子
pnpm update antd@5.8.5

// 反例一：一次性更新全部依赖
pnpm update

// 反例二：没指明版本
pnpm update antd
```

## Dependencies

项目运行所需的依赖项：

| 名称                                | 版本      | 说明                              |
|-----------------------------------|---------|---------------------------------|
| @amap/amap-jsapi-loader           | 1.0.1   | 高德地图 jsapi 启动器                  |
| @ant-design/icons                 | 6.0.0   | Antd 的图标库                       |
| @ant-design/v5-patch-for-react-19 | 1.0.3   | Antd 的 React 19 兼容包             |
| @antv/g2                          | 5.3.3   | AntV G2 图表组件库                   |
| @dagrejs/dagre                    | 1.1.5   | 流程图布局（与 xyflow 配合使用）            |
| @dnd-kit/core                     | 6.3.1   | dnk-kit 拖放                      |
| @dnd-kit/sortable                 | 10.0.0  | dnk-kit 拖放排序                    |
| @dnd-kit/utilities                | 3.2.2   | dnk-kit 拖放工具包                   |
| @tanstack/react-query             | 5.85.3  | 异步状态管理（获取、缓存、同步和更新服务器状态）        |
| @tiptap/extension-highlight       | 2.24.0  |                                 |
| @tiptap/extension-text-align      | 2.24.0  |                                 |
| @tiptap/pm                        | 2.24.0  | Tiptap 富文本编辑器                   |
| @tiptap/react                     | 2.24.0  | Tiptap 富文本编辑器                   |
| @tiptap/starter-kit               | 2.24.0  | Tiptap 富文本编辑器                   |
| @xyflow/react                     | 12.8.3  | flow 流程图库                       |
| antd                              | 5.27.0  | Antd UI 组件库                     |
| axios                             | 1.11.0  | http 网络请求库                      |
| dayjs                             | 1.11.13 | 日期格式化等处理（⚠️注意版本要和Antd依赖的版本保持一致） |
| i18next                           | 25.3.6  | 国际化                             |
| js-cookie                         | 3.0.5   | 管理 Cookie                       |
| qs                                | 6.14.0  | http 查询参数序列化和解析                 |
| react                             | 19.1.1  | 前端框架 React 的核心库                 |
| react-dom                         | 19.1.1  | React Web 库，与 React 包配合使用       |
| react-i18next                     | 15.6.1  | 国际化 React 适配包，与 i18next 包搭配使用   |
| react-router                      | 7.8.1   | react 路由                        |
| throttle-debounce                 | 5.0.2   | 防抖与节流                           |
| zustand                           | 5.0.7   | 状态管理                            |

## DevDependencies

仅用于开发的依赖项：

| 名称                          | 版本      | 说明                      |
|-----------------------------|---------|-------------------------|
| @eslint/js                  | 9.33.0  | 与 eslint 包搭配使用          |
| @types/js-cookie            | 3.0.6   | js-cookie 的类型定义         |
| @types/node                 | 24.3.0  | node 的类型定义              |
| @types/qs                   | 6.14.0  | qs 的类型定义                |
| @types/react                | 19.1.10 | react 的类型定义             |
| @types/react-dom            | 19.1.7  | react-dom 的类型定义         |
| @types/throttle-debounce    | 5.0.2   | throttle-debounce 的类型定义 |
| @vitejs/plugin-react        | 5.0.4   | vite：react 插件           |
| eslint                      | 9.33.0  | js 规则校验                 |
| eslint-plugin-react-hooks   | 5.2.0   | eslint：react-hooks 插件   |
| eslint-plugin-react-refresh | 0.4.20  | eslint：react-refresh 插件 |
| globals                     | 16.3.0  | 与 eslint 搭配使用           |
| prettier                    | 3.6.2   | 代码格式化                   |
| typescript                  | 5.9.2   |                         |
| typescript-eslint           | 8.39.1  |                         |
| vite                        | 7.1.9   | 前端构建工具                  |
