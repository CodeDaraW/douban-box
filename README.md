# douban-box
![Update Gist](https://github.com/CodeDaraW/douban-box/workflows/Update%20Gist/badge.svg)

## 安装
``` sh
$ npm i -g douban-box
```

## 基本原理
提供四个环境变量：
| 变量 | 含义 |
|---|---|
| GIST_ID | Gist ID |
| GITHUB_TOKEN | GitHub Token |
| DOUBAN_ID | 豆瓣用户 ID |
| DOUBAN_COOKIE | 豆瓣登录态 Cookie |

执行 CLI 时会读取环境变量，抓取指定用户的主页，更新对应的 Gist，若无报错则说明更新成功。 

``` sh
$ douban-box
```

另外可以通过 GitHub Actions 免费实现定时更新的功能。

## 使用
### 1. 创建 Gist
Gist 中新建名为 `douban.md` 的文件，并从 URL 中得到 Gist ID。

### 2. 创建 GitHub Token
访问 [Personal Access Tokens](https://github.com/settings/tokens) 创建更新 Gist 专用的 Token，需要勾选 `gist - Create gists` 权限，记住新生成的 Token。

### 3. 获取豆瓣 ID 和 Cookie
豆瓣 ID 是个人主页中 `people` 后紧接的那串数字或者自定义字符，例如我的主页链接 `https://www.douban.com/people/daraw/` 中是 `daraw`，在登录态下查看 Cookie，其中 `dbcl2` 是关键，复制这个 key 对应的值，构造出 `dbcl2="xxxxxxx"` 即可当做 Cookie，当然把整个 Cookie 都复制过去也是可以的。

### 4. 通过 GitHub Actions 自动更新 Gist
- 创建一个 Repo 并启用 GitHub Actions，可以参考本项目的 [.github/workflows/main.yml](https://github.com/CodeDaraW/douban-box/blob/master/.github/workflows/main.yml) 文件。

- 修改 `GIST_ID` 和 `DOUBAN_ID` 为刚刚所得到的 Gist ID 和豆瓣 ID。  

- 为了不暴露自己的 GitHub Token 和豆瓣 Cookie，在项目的 `Settings -> Secrets` 中创建两个变量 `TOKEN` 和 `DOUBAN_COOKIE`，分别为 GitHub Token 和豆瓣 Cookie。  

之后每次 `push` 和每日 00:00 UTC+0 时会触发更新 Gist，如果需要修改触发时机可以调整刚刚的 GitHub Actions 配置文件。

## License
[MIT License](https://github.com/CodeDaraW/douban-box/blob/master/LICENSE)