<div align="center">

# 👋 你好，我是 John

**数字 IC 验证工程师 / Digital IC Verification Engineer**

杭州 · 5 年经验 · Hangzhou · 5 Years Experience

*用 UVM 验证芯片，用 Python 造工具，用 AI 探索 EDA 新范式*

[![Email](https://img.shields.io/badge/Email-johnmc104%40qq.com-blue?style=flat-square&logo=qq)](mailto:johnmc104@qq.com)
[![GitHub](https://img.shields.io/badge/GitHub-Johnmc104-181717?style=flat-square&logo=github)](https://github.com/Johnmc104)

</div>

---

## 关于我

数字 IC 验证工程师，围绕 SoC 功能验证展开日常工作——搭 UVM 环境、写 case、跑回归、追覆盖率、定位 Bug。

在验证主线之外，我持续做两件事：

1. **造工具**：围绕验证全生命周期，开发了 VCM（仿真管理）、VRG（覆盖率分析）、vtrack（验证追踪）、VReg（寄存器平台）、vtool（命令行工具集）五套核心工具，覆盖从仿真执行到追踪闭环，已在团队日常使用。
2. **用 AI 拉通**：在工具平台基础上开发 ChipAgents — 终端 AI Agent 框架，将散落的 CLI 工具编排为 AI 驱动的自动化工作流，从 Spec 解析到覆盖率收敛一次对话完成。

同时自建综合→布局布线→签核的完整后端流程框架（chip_flow），在多个 SoC 上跑通，加深从 RTL 到 GDSII 的全局理解。

> I'm a DV engineer building UVM testbenches and a full verification automation toolchain. On top of that, I developed ChipAgents — an LLM agent framework that orchestrates EDA tools into AI-driven workflows, taking chip verification from spec analysis to coverage closure in a single conversation.

---

## 技术栈

<table>
<tr>
<td valign="top" width="50%">

**验证 / Verification**
- `UVM` (VCS / Xcelium) · `SystemVerilog` 断言 & 覆盖率
- Synopsys `Verdi` 调试 · NPI 编程接口
- Synopsys VIP (SVT APB/SPI Agent) · `OVL`
- `SpyGlass` Lint / CDC / Low Power

**后端 / Backend Flow**
- Synopsys: DC · ICC2 · FC · RTLA · PT · FM · DSO.ai
- Cadence: Innovus · Xcelium
- 开源: OpenROAD · OpenLane · Yosys

</td>
<td valign="top" width="50%">

**语言与开发 / Languages**
- `SystemVerilog` · `Verilog` · `Tcl` · `Shell`
- `Python` · `C/C++` · `TypeScript`
- `React` · `FastAPI` · `SQLite`
- `SystemRDL` · `ANTLR` · `LaTeX`

</td>
</tr>
</table>

---

## 验证工具生态

从手动工具到 AI 编排——六套工具组成完整的验证自动化栈：

```mermaid
flowchart TD
    CA["🤖 ChipAgent<br/><i>Playbook 编排 · Checker · 多模型分层</i>"]:::agent

    CA --> Platform

    subgraph Platform["验证工具平台"]
        direction LR
        vreg["vreg<br/><i>寄存器</i>"]:::reg
        vtool["vtool<br/><i>搭建</i>"]:::tool
        vcm["vcm<br/><i>仿真</i>"]:::tool
        vrg["vrg<br/><i>覆盖率</i>"]:::tool
        vtrack["vtrack<br/><i>追踪</i>"]:::track
        vreg --> vtool --> vcm --> vrg --> vtrack
    end

    vtrack -. "Gap 迭代" .-> vtool

    classDef agent fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px,color:#000
    classDef reg fill:#fff3e0,stroke:#ef6c00,color:#000
    classDef tool fill:#e3f2fd,stroke:#1565c0,color:#000
    classDef track fill:#e8f5e9,stroke:#2e7d32,color:#000
```

| 层 | 工具 | 职责 |
|---|------|------|
| **AI 编排** | ChipAgent | Playbook 阶段编排，驱动下层工具完成端到端流程 |
| **工具平台** | vreg · vtool · vcm · vrg · vtrack | 寄存器定义 · 项目搭建 · 仿真管理 · 覆盖率分析 · 验证追踪 |

---

### 🤖 ChipAgent — AI 驱动的 EDA 终端助手

独立开发的 LLM Agent 框架（Python 16K 行 · 1138+ 测试），部署于网络隔离的 EDA 服务器，通过终端交互或管道模式驱动芯片设计全流程。

**核心：不是通用聊天，而是流程编排。** Agent 不自由发挥，而是被 Playbook 逐阶段强制驱动，每步都有 Checker 质量门把关。

```mermaid
flowchart LR
    S1["🏷 分类<br/><i>fast</i>"]:::fast
    S2["🔍 分析<br/><i>strong</i>"]:::strong
    S3["🔧 实施<br/><i>strong</i>"]:::strong
    S4["✅ 验证<br/><i>fast</i>"]:::fast
    G{{"Pipeline Gate"}}

    S1 -->|"✓"| S2 -->|"✓"| S3 -->|"✓"| S4 -->|"✓"| G

    classDef fast fill:#e8f5e9,stroke:#43a047,color:#000
    classDef strong fill:#e3f2fd,stroke:#1e88e5,color:#000
```

#### 架构特色

| 设计 | 说明 |
|------|------|
| **三层知识模型** | Position（岗位）→ Playbook（事项）→ Skill（知识），声明式 YAML + Markdown，扩展免改代码 |
| **Coordinator-Worker** | 6 岗位 Agent 按需创建：DV · DV-VTool · Syn · RE · IPC · Coordinator 路由 |
| **28 Playbook** | 验证调试、环境搭建、Spec 分析、覆盖率收敛、综合运行……每个都有阶段定义和质量门 |
| **29 Skill 知识库** | UVM 方法学 · VCS 仿真 · DC 综合 · SDC 约束 · SV 语法 — 自动注入对应岗位 |
| **多模型分层** | strong 模型做分析/修复，fast 模型做分类/验证，按阶段自动切换，降低 60%+ 成本 |

#### 记忆与上下文

| 能力 | 说明 |
|------|------|
| **项目记忆** | 绑定 Git 仓库，跨会话持久化项目事实、修复经验、任务笔记 |
| **AI 召回** | 每次提问前从记忆库检索相关上下文，自动注入 system prompt |
| **三级压缩** | Microcompact（零成本清理旧工具输出）→ Smart Summarization（LLM 摘要）→ Session Truncation（防 OOM） |
| **记忆工具** | Agent 可主动写入记忆——修复经验自动积累，下次遇到同类问题直接复用 |

#### 现成工作流示例

**Spec 解析 → 验证计划生成**：

```bash
chip-agent -c "解析 @doc/apb_timer_spec.pdf 生成 Feature 列表和验证计划" -y
```

→ 自动编排 2 个 Leaf Playbook：  
`dv-spec-analyze`（文档解析 → Feature 提取 → vtrack feature add）→ `dv-vplan-create`（VP 生成 → Checkpoint 定义 → testplan.md 输出）  
→ 每步 Checker 校验 vtrack 数据完整性，Pipeline Gate 审查交付件质量

**验证环境搭建**（Workflow: `dv-foundation`）：

```bash
chip-agent -c "搭建 APB Timer 的 UVM 验证环境并通过编译" -y
```

→ 自动编排 3 个 Leaf Playbook：  
`dv-proj-init`（目录结构 + Makefile + vtrack init）→ `dv-tvc-create`（UVM Agent + Sequence）→ `dv-env-setup`（TB Top + Environment + 编译通过）  
→ file_check / compile_check / vtrack_status 三重 Checker 逐阶段把关

两个 Workflow 串联，即可从一份 Spec 文档到一个可编译的验证环境——中间不需要人工介入。

#### 与通用 Agent 的差异

| | 通用 Agent (Claude Code) | ChipAgent |
|--|--------------------------|-----------|
| **场景** | 开放式编码与研究 | EDA 规范化流程 |
| **部署** | 完整开发环境 | 终端二进制，网络隔离 EDA 服务器 |
| **流程控制** | 自由对话 | Playbook 强制阶段编排 + Checker |
| **成本** | 单一强模型 | strong/fast 分层，自动切换 |
| **领域知识** | 手动注入 | 29 Skill 自动加载 |
| **工具集成** | 通用文件操作 | 原生 vtrack / vcm / vrg 集成 |

#### 技术栈

Python 3.11+ · LangChain Deep Agents · LangGraph · Rich 终端 UI · PyInstaller 跨平台打包  
v0.6.1 · 1138 测试 · 57 模块 · 16K 行

---

### 工具平台详述

#### 🔗 vtrack — 验证追踪管理系统

基于 Feature→VP→Case 三层模型的验证追踪工具，连接功能需求与测试执行的完整可追溯链路。

| 能力 | 说明 |
|------|------|
| **三层追踪** | Feature (功能点) → VP (验证点) → Case (测试用例)，支持多对多映射 |
| **功能组** | Feature 按 group 分组，支持按功能域聚合查看与分析 |
| **追踪矩阵** | 自动生成 Feature×VP×Case 覆盖矩阵，直观呈现验证进度 |
| **GAP 分析** | 识别未覆盖功能点、无用例 VP、失败用例，按优先级/功能组过滤 |
| **数据同步** | 对接 VCM 仿真结果 + VRG 覆盖率数据 (`sync vcm/vrg`) |
| **快照迭代** | 验证快照管理，追踪收敛趋势 |

**典型工作流**：
```bash
vtrack init pcie_ctrl --project GP28
vtrack feature add "LTSSM 状态机" --group "链路训练" --priority P0
vtrack vp add "状态遍历" --features F001 --method directed
vtrack case add "ltssm_walk" --vp VP001
vtrack matrix --group "链路训练"    # 追踪矩阵
vtrack gap --priority P0           # 覆盖率缺口
```

支持 Human / JSON / YAML 多格式输出，同时服务于工程师手动操作和 ChipAgent AI 工具调用。

#### 📋 vreg — 寄存器管理与代码生成平台

芯片寄存器定义、管理与多格式代码生成的一站式平台。

| 层 | 技术 | 能力 |
|----|------|------|
| **前端** | React + Vite | 多项目管理、可视化编辑、Markdown 文档、全局搜索、批量地址编辑 |
| **后端** | FastAPI + SQLite | RESTful API、JWT 三级权限、版本锁定防并发 |
| **生成引擎** | Python + SystemRDL | SystemRDL · UVM Model · RTL · C Header · Config · Functional Coverage |

支持 Excel 导入（智能解析宏定义/数组/版本）、地址重叠/位域冲突校验、32/64 位自定义位宽。

#### 🛠️ vtool — DV 命令行工具集

部署于 EDA 服务器的一站式验证辅助工具，统一入口 `vtool -<option>`。

| 功能 | 命令 | 说明 |
|------|------|------|
| 项目脚手架 | `-init bt\|st` | 一键生成模块级 / 系统级 UVM 项目结构 |
| 组件生成 | `-c agent\|tvc\|env\|tmc\|tms` | 自动创建 UVM Agent / TVC / Env 等组件 |
| 回归管理 | `-testlist` · `-emc` · `-check` | case 扫描 → 回归配置 → 日志/timing 检查 |
| 日志分析 | `-log` · `-bug` | 仿真日志检查 + Markdown Bug 报告（含 seed/git） |
| Case 索引 | `-findsw` | 全量扫描 UVM case，按 group/case/class 索引 |
| 调试 | `-tarmac fg` | tarmac.log → 火焰图 SVG |
| 设计辅助 | `-inst` · `-port` · `-power` | 模块例化 / IO List / FSDB 功耗分析 |

内置 svlib + OVL 库引用。

#### 📊 vcm — 验证用例管理系统

面向数字验证仿真流程的全生命周期管理系统。`v1.5.0`

| 架构 | 说明 |
|------|------|
| **存储** | 本地 SQLite + 远程 Flask API，按环境自动切换 |
| **CLI** | `vcm` 统一入口，10 大命令组：project / module / case / task / sim / regr / info / emc / db / init |
| **Web** | Flask + HTML 模板，仿真数据可视化与回归报告 |
| **集成** | Makefile 驱动：`make build_ssh → make regr → make check → make report` |

**典型场景：**
- **单次仿真**：`vcm task add` → `vcm sim add_basic_single` — 自动采集编译信息、仿真日志、种子、用例名、通过状态
- **集群回归**：Slurm 批量提交 → 状态查询 → 结果统计 → 报告生成
- **EMC 多 Build**：多工艺角 test-build 映射、编译命令自动获取
- **一键调试**：`vcm info sim <id>` 直接启动 Verdi

#### 📈 vrg — VDB 覆盖率分析引擎

Synopsys VDB 覆盖率数据库的解析与报告工具，支持用例级覆盖率归因分析。

| 层 | 技术 | 能力 |
|----|------|------|
| **解析层** | C lib (Synopsys VDB API) | 直接读取 VDB 二进制数据库，零中间格式 |
| **接口层** | Python API (`VRGSession`) | 编程式访问，支持批量查询与脚本集成 |
| **报告层** | JSON / 文本 | 7 维覆盖率报告 + 用例级归因 |

**7 维覆盖率**：Line · Branch · Condition · Toggle · FSM · Assert · Group

**核心能力**：
- 按用例粒度归因覆盖率贡献，识别冗余 case
- 双数据源：VDB 直连 / JSON 报告，按环境自动切换
- 与 vtrack 联动：`vtrack sync vrg` 自动同步覆盖率至追踪系统
---

## 更多效率工具

| 工具 | 功能 | 技术 |
|------|------|------|
| **tool_cov** | Verdi/VCS 覆盖率提取 → Excel 报告 | NPI + Python |
| **tool_wave** | FSDB 波形读取 + 网表 signal driver/load 追踪 | Verdi NPI · C/S 架构 |
| **tool_soc** | IP-XACT SoC 自动互联 → RTL / C Header / Device Tree | Python 3.11+ |
| **tool_clkrst_network** | 时钟复位网络可视化设计 → Verilog 导出 | React + ReactFlow |
| **tool_disasm_8051** | 8051 固件反汇编 · 跳转分析 · 内存利用率 | Python |
| **python_tool** | spec2rdl · spec2xlsx · json2docx · pinmux · IO list · 工时报告 | Python 脚本集 |

---

## 后端全流程框架

### chip_flow

Makefile 驱动的 Synopsys 数字后端流程，覆盖 RTL 到签核，用于拉通全链路理解。

- **7 工具**：RTLA → DC → ICC2 → FC → DSO.ai → FM → PT
- **3 条路径**：DC→ICC2→FM→PT / FC 统一 / DSO 优化
- **4 层分离**：PDK / 设计 / 公共 / 工具脚本 — 支持 SAED32 / TSMC40 / SAED14 多工艺
- 已在 servant (RISC-V)、m0plus_top (ARM) 上验证全流程

---

## 开源项目

| 项目 | 描述 |
|------|------|
| [hvp-language-support](https://github.com/Johnmc104/hvp-language-support) | VSCode 插件：层次化验证计划语法支持 (TypeScript) |
| [sdc-xdc-support](https://github.com/Johnmc104/sdc-xdc-support) | VSCode 插件：SDC/XDC 时序约束支持 (TypeScript) |
| [reg_tool_manage](https://github.com/Johnmc104/reg_tool_manage) | SystemRDL 寄存器管理流程 (Python) |
| [sv_parser](https://github.com/Johnmc104/sv_parser) | 基于 ANTLR 的 SystemVerilog 解析器 |

---

## 技术写作

基于 LaTeX (elegantbook) 编写：

**书籍**：SoC 功能验证 · ASIC 设计与综合 · 低功耗与存储管理 · ECC 密码学 · 物理设计

**手册**：Design Compiler · Fusion Compiler · 数字验证 · Git 工作流 · Tcl Workshop

---

## 当前方向

- ChipAgent 多规模 DUT 适配——从小型 IP 到 SoC 级验证场景
- 验证追踪闭环自动化——AI 驱动的 Spec→Feature→VP→Case→Coverage 全链路收敛
- 工具平台与 AI 编排的深度集成——vcm 回归结果自动驱动 debug-fix-verify 循环

---

<div align="center">

*"写好每一个 testcase，造好每一个工具"*

</div>
