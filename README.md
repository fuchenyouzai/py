# CatVodSpider

TV 的 Java、Python 与 QuickJS 爬虫及范例，基于 [CatVod](https://github.com/CatVodTVOfficial/CatVodTVSpider)。

## 开始开发

| 语言 | 范例 |
| --- | --- |
| Java | [Demo.java](app/src/main/java/com/github/catvod/spider/Demo.java) |
| Python | [examples/python/spider.py](examples/python/spider.py) |
| QuickJS | [examples/javascript/spider.js](examples/javascript/spider.js) |

拷贝对应范例，换成站点数据，只保留需要的功能。共通功能、语言差异及 ext 选项见[开发说明](docs/development.md#demo-功能)。

修改 [examples/config.json](examples/config.json) 的 `api` 与 `ext`，再让 TV 加载这份配置。Java 需先打包；Python／QuickJS 可直接加载。

使用本机路径或网站皆可，保留 `examples` 与 `jar` 的相对位置。现有 Java 爬虫配置见 [json/config.json](json/config.json)。

## 打包 JAR

Java 最低支持 Android 7.0。在本项目根目录运行：

```powershell
.\gradlew.bat spiderJar
```

打包会运行 R8，成品为 `jar/custom_spider.jar` 与 `jar/custom_spider.jar.md5`。

| SDK | 来源 |
| --- | --- |
| `app/libs/catvod-api.jar` | TV 的 `apiJar`，产出于 `build/outputs/api/catvod-api.jar` |
| `app/libs/quickjs-api.jar` | quickjs-wrapper [Actions](https://github.com/FongMi/quickjs-wrapper/actions/workflows/build.yml) 的 Java API JAR |

SDK 以 `compileOnly` 引用，不打包进爬虫 JAR；更新后重新打包。Function JAR 使用 `com.fongmi.quickjs` API。

Java 的 `com.github.catvod.bean` 与 [Response](app/src/main/java/com/github/catvod/utils/Response.java) 随爬虫 JAR 打包。

三语言共用 Dialog 参数：Java 用 `dialog.show(...)`，Python 用 `self.dialog(...)`，QuickJS 用 `await dialog(...)`；完整表单、QR Code 与连续对话框见各语言 Demo。Android UI 用法与配套 App／模块需求见[开发说明](docs/development.md#android-ui)。

导出到其他目录可运行 `build.bat "D:\Output"`，也可传入完整 JAR 路径。

## 使用 AI

AI 指引见 [AGENTS.md](AGENTS.md) 与 [catvod-spider 技能](.agents/skills/catvod-spider/SKILL.md)。例如：

> 请用 $catvod-spider 为这个站点写 Python 爬虫，支持分类、筛选与搜索分页。
