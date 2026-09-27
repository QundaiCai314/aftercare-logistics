# aftercare-logistics 1.0.0

售后助手第九个 Skill：核对单件售后的退货条件、两种地址、取件时间与费用，准备平台内取件或自行寄件计划并解释当前退货物流。

Skill只输出LogisticsPlan，不操作网页、不预约、不提交或覆盖运单、不取消改约、不发送地址、不支付、不实际寄件，也不后台查询或启动Spark。

## 下载

- [可加载 Skill 包](aftercare-logistics-1.0.0.zip)：解压后使用 `aftercare-logistics/`。
- [完整工程包](aftercare-logistics-1.0.0-full.zip)：含Skill、合成请求/结果、校验代码、测试报告和未启用的契约提案。
- [测试报告](测试报告.md)
- [契约修订提案](契约修订提案.md)
- [SHA-256 清单](SHA256SUMS.json)

## 验证与限制

26类作者合成场景、184项检查通过，Skill Creator格式校验通过。已有interact、verify校验器仅做实际结构入口检查，不是模型调用或生产链路联调。

没有独立模型前向验证、真实平台预约、生产授权/引用/台账服务或实际物流验证。中央接口仍为1.0.0；两地址角色、费用性质和预约去重绑定缺口尚未迁移，因此正式预约与运单准备保持阻断。计划完成不等于预约、寄件或退款成功。

## 复现

Python 3与jsonschema>=4,<5。完整包解压后运行：

```text
python -B -X utf8 tests/run_tests.py
```

源文件指纹和既有检查器结构测试需要额外参考文件：设置 `AFTERCARE_SOURCE_ROOT`，其下以 `baseline/` 放置中央接口与规划，以 `aftercare-order/`、`aftercare-remedy/`、`aftercare-interact/`、`aftercare-verify/`、`aftercare-recover/`、`aftercare-resume/` 放置对应版本Skill包。具体来源及原始SHA-256见包内provenance.json。未提供外部依赖时明确记录未通过，不把缺失检查当成功；Skill自身校验器与派生Schema不依赖这些外部目录。

发布副本移除了本机路径，排除了缓存，保留来源摘要并重新生成发布摘要。仅含合成数据；未修改原交付、其他Skills或中央接口，未全局安装。仓库未附许可证，也未声明开源许可。
