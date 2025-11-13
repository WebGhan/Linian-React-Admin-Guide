# 目录结构

```
.
├── dist                  # 构建输出目录
├── docs                  # 项目文档
├── public                # 静态资源(不参与编译，构建时文件直接复制到项目根目录)
├── src
│   ├── api               # api 请求
│   │   ├── query-fn      # 请求方法
│   │   └── query-hooks   # 请求 Hooks
│   ├── assets            # 静态资源(参与编译)，可用于存放项目中引用的图片、字体等文件
│   │   ├── font          # 存放项目中所引用的字体
│   │   ├── iconfont      # iconfont 字体图标文件
│   │   ├── icon          # 图标
│   │   └── images        # 存放项目中所引用的图片
│   ├── common            # 全局公用方法
│   │   ├── auth          # 鉴权相关
│   │   ├── config        # 公用配置
│   │   └── utils         # 工具方法
│   ├── components        # 全局公用组件
│   │   └── icons         # 自定义图标组件
│   ├── i18n        	  # 国际化
│   │   └── locales       # 语言文件
│   │       ├── en-US     # 英语(美国)
│   │       └── zh-CN     # 中文(简体)
│   ├── layout            # 全局公用布局
│   ├── router            # 全局路由
│   │   └── routes        # 路由定义模块
│   ├── stores            # 全局状态
│   ├── types             # 全局类型
│   ├── views             # 视图
│   ├── main.css          # 全局样式
│   ├── main.jsx          # React 项目入口
│   └── vite-env.d.ts     
├── .env.development      # 开发环境变量文件（development 模式）
├── .env.production       # 生产环境变量文件（production 模式）
├── .env.testing          # 测试环境变量文件（testing 模式）
├── .gitignore
├── .prettierrc.js        # prettier 配置文件
├── eslint.config.js      # eslint 配置文件
├── index.html            # vite 项目入口文件
├── nginx.conf            # Nginx 配置文件
├── package.json
├── pnpm-lock.yaml        # pnpm 锁定文件
├── pnpm-workspace.yaml   # pnpm 工作空间
├── README.md
├── tsconfig.app.json
├── tsconfig.json
├── tsconfig.node.json
└── vite.config.ts        # vite 配置文件
```
