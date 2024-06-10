# Dokcer_hammal

Hammal 是运行于 cloudflare workers 上的 Docker 镜像加速工具，用于解决获取 Docker 官方镜像无法正常访问的问题。

# 使用方式


## 步骤
1. 克隆Workers(CloudFlare)项目
```
git clone https://github.com/Oruola/docker_hammal.git
```
2. 安装node环境
```
下载地址: https://nodejs.cn/download/
```
3. 执行部署命令
```
#1. 安装pnpm
npm install pnpm -g

#2. 安装项目依赖
pnpm install

#3. 将wrangler.toml.sample 文件改名 wrangler.toml 并修改其 account_id
文件名 wrangler.toml.sample -> wrangler.toml 

#4. 创建 cache 缓存 kv,记录执行结束后输出的 id，填写到 wrangler.toml 文件中
npx wrangler kv:namespace create hammal_cache

#5. 部署到Cloudflare,中间需要登录Cloudflare并授权
pnpm run deploy

```
4. Workers自定义域名(默认的 workers.dev 域名有墙)
```
进入CloudFlare的Dashboard -> Workers和Pages -> docker_hammal -> 设置 -> 触发器 -> 添加自定义域
```

5. 配置Docker镜像地址
```
sudo vi /etc/docker/daemon.json

{
  "registry-mirrors": [
    "https://hammal.example.com"
  ]
}

```
