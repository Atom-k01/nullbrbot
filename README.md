# nullbrbot - Telegram 媒体资源搜索机器人

**nullbrbot** 是一个基于 nullbr和Telegram 的媒体资源搜索机器人，
可帮助用户搜索电影、电视剧、人物及合集的信息和资源链接，
支持网盘、磁力和 ed2k 等多种资源类型。

## 功能特点

- 搜索电影、电视剧、人物及合集信息
- 获取多种格式的资源链接（115 网盘、磁力链接、ed2k、m3u8）
- 支持电视剧单集精确搜索（格式：剧集名 SXXEXX）
- 简洁的 Telegram 交互界面
- 资源结果中显示中文字幕信息

## Docker 部署指南

### 前提条件

- 已安装 Docker 和 Docker Compose
- 在 [nullbr.eu.org](https://nullbr.eu.org) 注册并获取 API 密钥
- 通过 [@BotFather](https://t.me/BotFather) 获取 Telegram 机器人令牌

### 快速部署

创建一个 `docker-compose.yml` 文件，内容如下：

```yaml
version: '3'
services:
  nullbrbot:
    image: atomkk/nullbrbot:latest
    container_name: nullbrbot
    volumes:
      - /opt/nullbrbot/config:/nullbrbot/config
      - /opt/nullbrbot/logs:/nullbrbot/logs
    restart: unless-stopped
```

启动容器：

```bash
docker compose up -d
```

容器启动后，在 `/opt/nullbrbot/config` 目录下会自动生成 `config.json` 文件，内容如下：（切记！！！USER_CHAT_IDS和ALLOWED_GROUP_IDS不能留空或填“0”，否则所有人都可以使用。不需要群组使用的话，ALLOWED_GROUP_IDS设置为一个不存在的数值，如-9999999999。）

```json
{
  "TG_BOT_TOKEN": "123456:abcdefghijklmnopqrstuvwxyz",
  "USER_CHAT_IDS": "123456789",
  "ALLOWED_GROUP_IDS": "-9999999999",
  "NULLBR_APP_ID": "abcdefghijklmnopqrstuvwxyz",
  "NULLBR_API_KEY": "abcdefghijklmnopqrstuvwxyz"
}
```

编辑 `config.json` 文件，填入你的配置信息。

重启容器使配置生效：

```bash
docker compose restart
```

部署完成！现在你可以在 Telegram 中使用你的机器人了。


###############################################################################
## 更新日志

### v1.2 - 2025年9月8日
- 🔧 重构代码，减少冗余
- 🔍 在搜索结果中添加 `tmdbid` 
- 👥 新增支持多用户、群组
- ⚠️ **重要提示：务必删除原有的 `config.json` 文件，并按提示重新配置**


### v1.1 - 2025年9月8日
- 🎛️ 新增季集按钮选择功能，同时保留原有的「归队 S01E01」等单集搜索
- 🔗 添加 m3u8 资源链接支持
- ✨ 优化用户体验
