外贸客户背景调查 Skill
[![License: PolyForm Noncommercial 1.0.0](https://img.shields.io/badge/License-PolyForm%20Noncommercial%201.0.0-blue.svg)](https://polyformproject.org/licenses/noncommercial/1.0.0/)

一个面向外贸销售、渠道开发和交易风控的公开信息调查 Skill。输入公司名称、官网、域名、邮箱、电话或联系人后，系统化调查企业身份、产品范围、成立历史、地址、商业模式、负责人、联系方式、贸易活动与风险信号，并将结构化结果写入飞书多维表格。

## 能做什么

- 核验法定名称、注册号、成立时间、经营状态和关联主体
- 整理产品范围、品牌、目标市场、销售渠道和客户类型
- 判断企业更接近制造商、贸易商、进口商、经销商还是品牌商
- 查找公开的老板、创始人、CEO、采购负责人和销售联系人
- 收集公司电话、业务邮箱、WhatsApp、LinkedIn 与其他社交页面
- 交叉验证注册地址、办公室、工厂、仓库和门店
- 调查公开海关、供应链、认证、商标、诉讼、制裁与负面信号
- 按固定字段写入飞书 Base，并在写入后回读确认

## 核心原则

1. **证据优先**：优先使用政府注册、海关、法院、认证机构和公司官网。
2. **区分事实与判断**：重要字段标记为已核实、有支持、公司自述、有冲突或未查到。
3. **不凭自述认定工厂**：官网写着 `manufacturer` 不等于已经证明其拥有生产设施。
4. **不猜联系人**：不生成或猜测邮箱，只记录公开披露的职业联系方式。
5. **一家公司一条记录**：优先按域名或官网去重，已有记录则更新。
6. **写入后回读**：只有 Base 回读成功，才算完成交付。

## 调查结果

Skill 会输出并写入以下几类信息：

- 企业身份与发展历史
- 产品、品牌与应用行业
- 制造商/贸易商/进口商/经销商判断
- 注册、办公、工厂和仓库地址
- 老板、管理层、采购和销售联系人
- 电话、邮箱、WhatsApp 和社交账号
- 进出口、供应商、客户与认证线索
- 合作价值、风险等级、证据状态和下一步建议

完整字段定义见 [`references/feishu-schema.json`](references/feishu-schema.json)，报告结构见 [`references/report-template.md`](references/report-template.md)。

## 安装

将仓库克隆到支持 Skills 的智能体目录。Codex 示例：

```powershell
git clone https://github.com/Elvinaskill/foreign-trade-customer-background-check.git "$env:USERPROFILE\.codex\skills\foreign-trade-customer-background-check"
```

也可以下载 ZIP 后，将整个目录复制到智能体的 Skills 目录。重新启动或刷新 Skills 列表后即可使用。

## 使用示例

```text
背调 https://example.com/ 这家公司，判断它是制造商还是贸易商，并写入飞书多维表格。
```

```text
调查 Example Trading Ltd. 的产品范围、成立历史、老板、电话、邮箱和进口记录。
```

```text
核验这家客户有没有真实工厂，找出采购负责人，并给出付款风险建议。
```

## 飞书 Base

如果用户提供现有 Base 链接，Skill 会先读取真实字段，再按字段类型写入；如果没有目标 Base，则使用内置 schema 建议创建：

- Base：`Foreign Trade Customer Background Checks`
- 数据表：`Customer Dossiers`

运行时所需的 Base 链接、访问令牌、表格 ID 和记录 ID 不应写入仓库。

## 目录结构

```text
customer_background/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── feishu-schema.json
    ├── report-template.md
    └── source-playbook.md
```

## 隐私与合规

- 只收集公开披露、与企业业务相关的职业信息。
- 不收集私人住址、私人邮箱、身份证件、家庭成员等无关个人信息。
- 仓库不保存真实客户调查结果、登录凭据、Cookie、API 密钥或飞书令牌。
- 公开数据库可能存在延迟、拼写错误或覆盖不完整，结果应作为销售与风控线索，不替代法律、税务或专业信用审查。

## 兼容性

适用于支持 `SKILL.md` 工作流的 AI Agent。完整执行需要：

- 网页搜索或浏览能力
- 可访问的公开企业、政府或贸易数据源
- 飞书/Lark Base 操作能力（需要写入多维表格时）

## 许可与商业使用

本项目采用 **PolyForm Noncommercial License 1.0.0**，不是 MIT 许可。MIT 允许商业使用、再销售和集成到商业产品中，不符合本项目的授权目标。

在遵守 [`LICENSE`](LICENSE) 的前提下，允许个人学习、非商业研究、测试和其他非商业用途。下列行为未经版权所有者事先书面授权均不允许：

- 企业或商业主体将本 Skill 用于日常获客、客户背调、员工培训或其他经营活动；
- 将本 Skill 或其修改版用于付费课程、付费社群、咨询交付、代运营或商业服务；
- 集成到收费软件、SaaS、Agent、工作流、插件、模板包或其他商业产品；
- 销售、转售、出租、再许可或以商业利益为目的重新分发；
- 删除版权、许可文件或来源说明后发布修改版。

公开仓库仅表示源码可查看，不代表放弃版权，也不代表授予商业使用权。分发副本或修改版时必须保留 `LICENSE`、版权声明和来源说明。商业授权请联系仓库所有者 Elvina。

## 参与完善

欢迎提交 Issue，分享新的国家工商查询入口、海关数据源、字段建议或企业性质判定经验。请勿在 Issue 中提交真实客户凭据或个人敏感信息。
