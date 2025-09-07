# nullbrbot - Telegram 媒体资源搜索机器人

**nullbrbot** 是一个基于 Telegram 的媒体资源搜索机器人，
可帮助用户搜索电影、电视剧、人物及合集的信息和资源链接，
支持网盘、磁力和 ed2k 等多种资源类型。

## 功能特点

- 搜索电影、电视剧、人物及合集信息
- 获取多种格式的资源链接（115 网盘、磁力链接、ed2k）
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

容器启动后，在 `/opt/nullbrbot/config` 目录下会自动生成 `config.json` 文件，内容如下：

```json
{
  "TG_BOT_TOKEN": "请替换为通过@BotFather获取的机器人令牌",
  "USER_CHAT_ID": "请替换为你的Telegram用户ID（纯数字）",
  "NULLBR_APP_ID": "请替换为在nullbr.eu.org注册的应用ID",
  "NULLBR_API_KEY": "请替换为在nullbr.eu.org获取的API密钥"
}
```

编辑 `config.json` 文件，填入你的配置信息。

重启容器使配置生效：

```bash
docker compose restart
```

部署完成！现在你可以在 Telegram 中使用你的机器人了。


###############################################################################

2025.9.8 新增季集按钮选择功能，同时保留原有的「归队 S01E01」等单集搜索；添加m3u8资源链接；优化用户体验
