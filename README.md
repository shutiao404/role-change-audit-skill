# 为角色变更添加审计记录和失败回滚

《信息安全管理》个人作业。用定制 Codex Skill 修改一个 Python / SQLite 示例，让角色更新和成功审计记录一起提交。若审计写入失败，调用方收到错误，角色更新一并回滚。

## 提交材料

- [两页说明文档](report.pdf) · 开发任务和验收标准、参考 Skill、定制规则、实际结果、人工复核范围。
- [定制 Skill](SKILL.md) · 可在 Codex 中使用的角色变更审计流程。
- [试用材料压缩包](trial-evidence.zip) · 关键交互、修改前后的代码、统一差异、四份实际运行日志与复跑说明。

## 测试结果

基线 3 项测试通过。实现前，两项新增关键测试因审计功能缺失而按预期失败。实现后，完整套件 7 项通过。数据库回查确认，成功时角色与审计记录一同写入，模拟写入失败时角色保持原值且审计表无新增记录。

解压后，`evidence/interaction.md` 是关键交互，`change.diff` 是实际改动，`evidence/01-baseline.log` 至 `evidence/04-readback.log` 含命令、输出和退出码。示例仅使用虚构账号和临时数据库。

## 复跑与使用

使用 Python 3.8 或以上版本。在解压后的 `baseline/` 和 `demo/` 中分别执行 `python -B -m unittest -v`。在 `demo/` 额外执行 `python -B ../trial_readback.py` 可复现数据库回查。

如需安装 Skill，把 `SKILL.md` 放在项目的 `.agents/skills/role-change-audit/` 下。压缩包中的 `demo/` 已包含这个目录。也可以在 Codex 中直接指定文件路径并要求按其规则执行，本次试验验证了这一用法。
