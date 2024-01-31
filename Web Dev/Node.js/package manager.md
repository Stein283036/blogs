# package manager

安装 yarn

```shell
npm i -g yarn
```

npm源切换工具nrm:

```shell
npm i -g nrm --registry=https://registry.npmmirror.com
nrm use taobao
```

国内源cnpm：https://npmmirror.com

```text
npm install -g cnpm --registry=https://registry.npmmirror.com
```

## npm、cnpm、nvm、nrm、npx、pnpm

npm 是 node package manager。

cpnm 是阿里推出的一个node包管理工具，它是一个完整官方npm.org镜像，完全可以代替官方版本，由于官方的服务器在国外，国内开发者使用时下载依赖包会比较慢，所以阿里推出了cnpm工具，该工具会每隔10分钟同步一次官方镜像源，以保证尽量与官方服务同步。

nvm 是 node version manager，用来管理 Node 版本的工具。

nrm 是 node registry manager，是 Node 依赖仓库的管理工具。

npx 是 node package execute