---
AssetType: Protocol
Status: Active
Version: v1.0
LoadPolicy: Full
Date: 2025-12-24T16:00:59
ProtocolLayer: Structural
---
# 《认知资产标准格式协议》（CASFP）v1.0

---

## 1. 协议目的（Purpose）

本协议用于定义**认知资产库中所有资产的标准格式、元数据字段及其设计原理**，以确保：

- 资产可被长期稳定保存
- 资产可被 AI 显式、可控地调用
- 资产之间具备清晰的结构与依赖关系
- 资产体系可持续演进，而不因规模扩大而失序  

本协议属于 **Meta 级 Protocol**，对资产库具有全局约束力。

---

## 2. 设计原则（Design Principles）

### 2.1 认知资产 ≠ 文本片段

- 每个认知资产是一个**完整、可整体理解的认知单元**
- 不是为了最大化召回率，而是为了**保持内部逻辑完整性**

### 2.2 元数据与正文语义正交

- 元数据用于**调度、约束与治理** 
- 正文用于**表达知识本身**
- 两者职责严格区分，避免语义污染 

### 2.3 AI 是调度器，而非裁决者

- AI 不对资产之间的冲突做自动裁决
- 语义分歧必须通过人工分析解决
- 资产演进通过新增 / 替换实现，而非覆盖

---

## 3. 通用元数据标准（Global Metadata Schema）

所有认知资产**必须**在文档头部以 YAML Front Matter 形式声明以下字段。

```yaml
---
AssetType: Knowledge | Procedure | Protocol | Registry
Status: Draft | Active | Deprecated
UsageMode:
  - Divergent
  - Hybrid
  - Convergent
LoadPolicy: Full | Reference
tags:
  - tag1
  - tag2
Date: YYYY-MM-DDThh:mm:ss
---
```

---

## 4. 字段定义与约束说明

### 4.1 AssetType（资产角色类型）

```yaml
AssetType: Knowledge | Procedure | Protocol | Registry
```

**定义：**

用于描述该资产在认知体系中的“功能角色”，而非内容主题或使用方式。

- `Knowledge`：概念、理论、背景知识
- `Procedure`：步骤性、可执行或可检查的流程    
- `Protocol`：规则、标准、调度与组织方式
- `Registry`：索引、注册表、资产目录

该字段必须与 `UsageMode`、`LoadPolicy` 保持语义正交。

---

### 4.2 Status（生命周期状态）

```yaml
Status: Draft | Active | Deprecated
```

- `Draft`：存在但禁止调用 
- `Active`：稳定，可被调用
- `Deprecated`：历史保留，不允许新调用 

Status 用于**调用许可控制**，而非质量评估。

---

### 4.3 UsageMode（默认使用模式）

```yaml
UsageMode:
  - Hybrid
```

表示该资产**默认**适用于哪些思维 / 使用模式：

- `Divergent`：发散型 
- `Hybrid`：混合型 
- `Convergent`：收敛型

> UsageMode 为默认值，可在具体调用时被人工显式覆盖。

---

### 4.4 LoadPolicy（加载策略）

```yaml
LoadPolicy: Full | Reference
```

- `Full`：调用时必须整体加载，不允许拆解
- `Reference`：仅作为背景或局部引用

该字段用于防止因相关性匹配导致的**逻辑结构破坏**。
> LoadPolicy 为默认值，可在具体调用时被人工显式覆盖。

---

### 4.5 tags（非约束型标签）

```yaml
tags:
  - 系统思维
  - 思维模型
```

用于：

- 人类导航
- 搜索与联想
- 主题标记

tags 不参与任何调用裁决逻辑。

---

### 4.6 Date（创建或最近确认时间）

用于记录资产的时间上下文，辅助人工判断其时效性。

---

## 5. 类型差异化要求

### 5.1 Protocol 类型补充字段

Protocol 资产**必须**增加版本字段：

```yaml
Version: v1.0
```

**原因：**

- Protocol 具有制度性影响
- 需要支持版本演进与历史回溯
- 禁止隐式修改

---

### 5.2 其他类型是否需要 Version

- `Knowledge`：❌ 不强制（内容演进通过新资产）
- `Procedure`：⚠️ 可选（当流程具有明确版本语义时） 
- `Registry`：⚠️ 可选（当注册表结构发生变化时）

---

## 6. 正文结构建议（非强制）

协议不强制正文模板，但推荐包含：

- 定义 / 目的
- 适用范围
- 核心原则或步骤
- 示例（如适用）
- 边界说明

---

## 7. 与其他协议的关系

- 本协议负责：**资产格式与字段规范**
- 《认知资产引用与链接协议》负责：**资产之间的引用与依赖**

两者共同构成认知资产库的基础制度层。

---

## 8. 协议演进规则

- 新版本必须以新 Protocol 资产形式存在
- 不允许覆盖旧版本
- Registry 中应显式标注当前生效版本

---
## 9. 结语

该协议的目标不是约束思考，而是**为复杂认知提供稳定的结构载体**。

当资产数量增加时，秩序将来自协议，而非记忆。

