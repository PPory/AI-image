# NanoBananaPro-main Agent Notes

## 项目定位

这是一个单页图片生成工具，页面名为 `Pory.AI绘图`。用户填写自己的生图 API Key 后，可通过网页生成或编辑图片。

项目没有构建流程，核心页面、样式和脚本都在 `index.html` 中。

## 当前文件

- `index.html`：主页面，包含全部 HTML、CSS 和 JavaScript
- `favicon.svg`：SVG 站点图标
- `favicon.ico`：ICO 站点图标
- `AGENTS.md`：项目说明和协作要求
- `agent.md`：给后续 Agent 使用的项目备忘

## 启动方式

```bash
start index.html
```

也可以直接双击 `index.html` 打开。

## 主要功能

- 输入 Prompt 生成图片
- 支持 `GPT Image 2`、`GPT Image 2 VIP` 和 `Nano Banana Pro`
- 支持画幅比例选择
- 支持按模型联动分辨率：`GPT Image 2` 只用 `1K`，`GPT Image 2 VIP` 只用 `2K/4K`，`Nano Banana Pro` 支持 `1K/2K/4K`
- 支持上传参考图或待编辑图片
- 支持保存、查询和清除 API Key
- 支持取消当前生成任务
- 支持生成历史记录
- 支持图片预览、上一张/下一张切换和下载原图
- 支持复制作者微信号和生成 Prompt
- 支持风格示例库，未保存 Key 时可浏览示例图，保存 Key 后可查看 Prompt 并一键套用模型、比例和分辨率
- 说明弹窗支持展示内测额度包、模型消耗、购买流程和售后规则

## 数据保存位置

页面只使用浏览器本地存储。

- API Key：`grsai_pro:key`
- 画幅比例：`grsai_pro:ratio`
- 分辨率：`grsai_pro:size`
- 模型：`grsai_pro:model`
- 历史记录：`grsai_pro:history`

不要把用户 API Key 写进代码、文档或测试数据。

## 接口信息

当前页面使用这些接口：

- 生成接口：`https://grsai.dakka.com.cn/v1/api/generate`
- 结果查询接口：`https://grsai.dakka.com.cn/v1/api/result?id=任务ID`
- 余额查询接口：`https://grsai.dakka.com.cn/client/openapi/getAPIKeyCredits`

请求使用用户填写的 Key，通过 `Authorization: Bearer <key>` 或请求体发送。

页面积分展示采用 `Grsai 官方积分 / 10`：

- `GPT Image 2`：60 积分 / 次，只用于 1K。
- `GPT Image 2 VIP`：130 积分 / 次，用于 2K / 4K。
- `Nano Banana Pro`：180 积分 / 次，用于 1K / 2K / 4K。

## 维护注意事项

- 本项目没有外部依赖，普通修改不应新增构建工具。
- 修改界面、样式、文案或脚本时，优先在 `index.html` 内完成。
- 不要拆分文件，除非用户明确要求重构。
- 不要改动 Key 保存逻辑，除非用户明确要求。
- 调整接口参数时，同步检查页面说明、错误提示、历史记录状态和 `docs/launch-playbook.md`。
- 当前上传区域允许最多 8 张图，新生成接口通过 `images` 数组发送参考图。
- `data/` 是已使用目录；`output/`、`docs/` 仍是约定目录，当前仓库中未实际创建。
- `data/style-examples/` 存放风格示例库使用的本地 PNG 图片。
- `docs/launch-playbook.md` 是公众号和小红书开卖执行手册。
- `docs/launch-tracker.csv` 是手工记录内容发布、咨询、成交和售后的表格模板。
- `PLAN.md` 和 `风格图库.txt` 是本地运营/素材文件，已加入 `.gitignore`，不要上传公开仓库。
- `PUBLIC_R2_DOMAIN`、部分端点常量和辅助函数当前保留在脚本中，但实际请求位置仍有直接写死的 URL。改接口时需要全局搜索确认。

## 验证清单

交付前至少检查：

- `index.html` 能直接打开
- 页面没有明显布局错位
- Prompt、模型、比例、分辨率控件可用
- 模型和分辨率联动正确：GPT Image 2 仅 1K，GPT Image 2 VIP 仅 2K/4K，Nano Banana Pro 可选 1K/2K/4K
- API Key 保存、清除、余额查询按钮可点击
- 参考图上传、缩略图展示和删除可用
- 历史弹窗可打开和关闭
- 预览弹窗可打开和关闭
- 风格卡片可打开详情；未保存 Key 时隐藏 Prompt，保存 Key 后点击“使用此风格”能正确填入 Prompt 和推荐设置
- `data/style-examples/` 中的 12 张本地示例图能正常加载
- 套餐说明、积分消耗、购买流程、Key 共享规则、失败与退款规则在页面中可见
- 没有把真实 API Key 写入项目文件

如需验证真实生成能力，必须由用户提供可用 API Key；不能使用或伪造用户凭据。
