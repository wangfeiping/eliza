# deploy, build and start

https://github.com/elizaOS/eliza/blob/main/i18n/readme/README_CN.md

## install nvm & nodejs

```
# Download and install nvm:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash

# in lieu of restarting the shell
\. "$HOME/.nvm/nvm.sh"


# Download and install Node.js:
nvm install 23.3.0

# Verify the Node.js version:
node -v # Should print "v23.3.0".
nvm current # Should print "v23.3.0".


# Verify npm version:
npm -v # Should print "10.9.2".
```

## build & start

```
git clone https://github.com/wangfeiping/eliza.git
cd eliza
git checkout dev-v0.25.9

cp ./bak/ellsa.ng.conf /etc/nginx/conf.d/
cp ./bak/.env ./
cp ./bak/Ellsa.character.json ./characters/

# install nginx
apt install nginx
nginx -t
nginx -s reload

sh scripts/start.sh
```

## Test

```
*** 修改配置修改请查看更新文件。

*** 使用IP可以正常访问 http://47.251.163.28 or http://47.251.163.28:3000
nginx 中80与3000端口会代理到同一个端口，但浏览器访问会返回不同内容。
似乎会因为访问端口不同提供客户端页面或Rest API服务。
客户端页面: http://47.251.163.28
Rest API: http://47.251.163.28:3000

*** 使用域名（http://test.eliza/ or http://test.eliza:3000）访问会出现 CORS error
```

## changed

```
scripts/start.sh

因为shell版本原因 "&> /dev/null" 可能需要改为 ">/dev/null 2>&1"

if ! command -v node &> /dev/null; then
改为
if ! command -v node >/dev/null 2>&1; then
```

