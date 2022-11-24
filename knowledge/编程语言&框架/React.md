# React

## 工程实践

- 数据请求: [SWR](https://swr.vercel.app/zh-CN)
- 应用结构
  - 组件按 路由/模块 分组，而不是全放在 `components` 中

    ```text
    // 👍 Group by module/domain
    ├── modules
    |   ├── common
    |   |   ├── components
    |   |   |   ├── Button.jsx
    |   |   |   ├── Input.jsx
    |   ├── dashboard
    |   |   ├── components
    |   |   |   ├── Table.jsx
    |   |   |   ├── Sidebar.jsx
    |   ├── details
    |   |   ├── components
    |   |   |   ├── Form.jsx
    |   |   |   ├── ItemCard.jsx
    ```

  - 使用绝对路径，例如: `import Input from '@modules/common/components/Input'`
  - 包装外部组件
  - 将组件放在单独的文件夹中，并创建一个导出组件的 `index.js` 文件

    ```js
    export { default } from './Button.jsx'
    ```

    ```text
    // 👍 Move them in their own folder
    ├── components
        ├── Header
            ├── index.js
            ├── Header.jsx
            ├── Header.scss
            ├── Header.test.jsx
        ├── Footer
            ├── index.js
            ├── Footer.jsx
            ├── Footer.scss
            ├── Footer.test.jsx
    ```

- 状态管理
- 样式
- icon 库 / ui 库
- 路由
- 布局
- 国际化
