# pnpm

> https://pnpm.io/

项目使用 pnpm 替代 npm/yarn 进行包管理。

## 安装 pnpm

使用 npm 全局安装 pnpm

```shell
sudo npm install -g pnpm
```

## 清除残留

pnpm 的包不直接安装到项目目录中，而是全局统一存储的。这样的好处是如果多个项目有相同的依赖则不会重复占用储存空间；但是，如果项目移除了，或者项目中的依赖发生了变动，则会导致未被依赖的占用我们的存储空间。

pnpm 提供了清理这些未被依赖的包的命令，我们可以定期（例如项目升级依赖后）执行以下命令，清理储存空间：

```shell
pnpm store prune
```
