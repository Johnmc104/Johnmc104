<div align="center">

# 你好，我是 John

**数字 IC 验证工程师 / Digital IC Verification Engineer**

杭州 · 5 年经验 · Hangzhou · 5 Years Experience

*用 UVM 验证芯片，用 Python 造工具，用 AI 探索 EDA 新范式*

[![Email](https://img.shields.io/badge/Email-johnmc104%40qq.com-blue?style=flat-square&logo=qq)](mailto:johnmc104@qq.com)
[![GitHub](https://img.shields.io/badge/GitHub-Johnmc104-181717?style=flat-square&logo=github)](https://github.com/Johnmc104)

</div>

---

## 关于我

我是一名数字 IC 验证工程师，日常工作围绕 SoC 芯片的功能验证展开——搭建 UVM 环境、编写测试用例、执行回归仿真、推动覆盖率收敛，以及定位和修复设计缺陷。

在完成验证主业的同时，我持续投入两个方向的探索：

1. **全栈工具链开发**：针对验证生命周期中的效率瓶颈，独立设计并落地了多套核心工具——VCM（仿真管理）、VRG（覆盖率分析）、VReg（寄存器平台），并通过 VCtrl（VS Code 扩展）统一为可视化交互界面，覆盖了从仿真执行到追踪闭环的完整链路。
2. **AI 驱动的验证工作流**：在工具链的基础上，研发了终端 AI Agent 框架——ChipAgent。它将零散的命令行工具编排成 AI 可驱动的自动化流程，让"从 Spec 解析到环境搭建"可以通过自然语言对话完成。独立的 vtrack 验证追踪系统管理 Feature → VP → Case 全链路闭环，通过 VCtrl 实现可视化。

此外，为了建立从 RTL 到 GDSII 的全局物理视野，我自建了一套覆盖综合、布局布线与签核的完整后端流程框架（chip_flow），并在多个开源 SoC 上跑通验证。

> I am a Digital IC Verification Engineer building UVM testbenches and robust verification automation toolchains. Beyond traditional DV tasks, I have developed ChipAgent — an LLM-based agent framework that orchestrates fragmented EDA tools into AI-driven workflows, transforming chip verification from manual routines into intelligent, end-to-end conversations.

---

## 技术栈

```mermaid
mindmap
  root((核心能力))
    芯片验证
      UVM · SystemVerilog
      VCS · Xcelium
      Verdi 调试 · NPI
      SpyGlass CDC Lint
      Synopsys VIP
    后端物理设计
      DC · ICC2 · FC
      PT · FM · RTLA
      DSO.ai
      OpenROAD · Yosys
    软件开发
      Python 全栈
      React · TypeScript
      FastAPI · SQLite
      C C++ 扩展
    AI Agent
      LangChain
      Claude · OpenAI API
      Prompt Engineering
      Tool Orchestration
```

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

**AI 与 Agent / AI & Agent**
- `LangChain` · `Deep Agents` 生态
- `Claude` · `OpenAI` · `Google GenAI` 多模型接入
- YAML/Markdown 驱动的知识编排体系

</td>
</tr>
</table>

---

## 验证工具生态

从设计定义到追踪闭环——十一套系统组成完整的验证自动化栈：

```mermaid
flowchart LR
    vreg["vreg<br/><i>寄存器定义</i>"]:::reg
    clkrst["crn design<br/><i>时钟复位设计</i>"]:::reg
    vtool["vtool<br/><i>环境搭建</i>"]:::scaffold
    vcm["vcm<br/><i>仿真执行</i>"]:::tool
    wave["tool_wave<br/><i>波形调试</i>"]:::debug
    ktm["tool_ktm<br/><i>内核追踪</i>"]:::debug
    vrg["vrg<br/><i>覆盖率分析</i>"]:::tool
    vtrack["vtrack<br/><i>需求追踪</i>"]:::track
    CA["ChipAgent<br/><i>流程编排</i>"]:::agent

    vreg --> vtool
    clkrst --> vtool
    vtool --> vcm
    vcm --> wave --> vrg
    vcm --> ktm --> vrg
    vrg --> vtrack
    vtrack -. "Gap 迭代" .-> vcm

    vctrl["vctrl<br/><i>VS Code 统一视图</i>"]:::gui
    tplan["tool_plan<br/><i>项目排期</i>"]:::plan

    vctrl -.-> vtrack
    vctrl -.-> vcm
    vctrl -.-> vrg

    classDef agent fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px,color:#000
    classDef reg fill:#fff3e0,stroke:#ef6c00,color:#000
    classDef tool fill:#e3f2fd,stroke:#1565c0,color:#000
    classDef scaffold fill:#f3e5f5,stroke:#7b1fa2,color:#000
    classDef track fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#000
    classDef debug fill:#e8f5e9,stroke:#2e7d32,color:#000
    classDef gui fill:#e0f2f1,stroke:#00796b,stroke-width:2px,color:#000
    classDef plan fill:#fce4ec,stroke:#ad1457,stroke-width:2px,color:#000
```

| 架构分层 | 核心组件 | 定位与核心职责 |
|---|---|---|
| **流程编排** | **ChipAgent** | 自研Agent。通过结构化 Playbook 驱动底层工具，内置多种应用场景和skill。 |
| **设计定义** | **vreg** | 寄存器管理平台。可视化编辑寄存器定义，一键生成 RTL / UVM / C 代码。 |
| **设计定义** | **crn design** | 时钟复位网络可视化设计，基于 ReactFlow 交互式编辑，导出 Verilog 代码。 |
| **环境搭建** | **vtool** | 命令行工具集。覆盖 UVM 骨架生成、回归用例管理、日志分析与代码检索。 |
| **仿真执行** | **vcm** | 仿真管理系统。统管单次仿真与 SLURM 集群回归，处理多工艺角 EMC 自动化构建。 |
| **调试分析** | **tool_wave** | FSDB 波形读取与网表信号 driver/load 追踪，基于 Verdi NPI 的 C/S 架构。 |
| **调试分析** | **tool_ktm** | Cortex-M 内核追踪分析器，支持工程师与 AI 双模式交互。 |
| **覆盖分析** | **vrg** | 覆盖率分析引擎。通过 C 层引擎直接解析 VDB，实现用例级覆盖率归因与冗余识别。 |
| **需求追踪** | **vtrack** | 验证追踪系统。管理 Feature → VP → Case 三层追溯链路，提供缺口分析与覆盖率同步。 |
| **视窗交互** | **vctrl** | IDE 控制台。以 VS Code 扩展形式，统一可视化 vtrack 追踪、覆盖率与仿真状态。 |
| **项目管理** | **tool_plan** | 排期管理平台。多产品线项目排期、资源负载分析与 Jira 工时对比，单二进制部署。 |

---

## 更多效率工具

| 工具 | 功能 | 技术 | 应用场景 |
|------|------|------|------|
| **tool_cov** | Verdi/VCS 覆盖率提取 → Excel 报告 | NPI + Python | 周期性覆盖率汇报 |
| **tool_soc** | IP-XACT SoC 自动互联 → RTL / C Header / Device Tree | Python 3.11+ | SoC 集成 |
| **tool_disasm_8051** | 8051 固件反汇编 · 跳转分析 · 内存利用率 | Python | 嵌入式固件分析 |
| **python_tool** | spec2rdl · spec2xlsx · json2docx · pinmux · IO list · 工时报告 | Python 脚本集 | 日常数据转换 |

---

## 后端全流程框架

### chip_flow

Makefile 驱动的 Synopsys 数字后端流程框架，覆盖 RTL 到签核全链路。搭建初衷是建立从逻辑设计到物理实现的全局理解。

```mermaid
flowchart LR
    RTL["📦 RTL"]:::src
    RTLA["RTLA<br/><i>可综合性分析</i>"]:::tool
    DC["DC<br/><i>逻辑综合</i>"]:::tool
    ICC2["ICC2<br/><i>布局布线</i>"]:::tool
    FC["FC<br/><i>统一流程</i>"]:::tool
    DSO["DSO.ai<br/><i>AI 优化</i>"]:::tool
    FM["FM<br/><i>等价验证</i>"]:::tool
    PT["PT<br/><i>时序签核</i>"]:::tool
    GDS["📐 GDSII"]:::src

    RTL --> RTLA --> DC

    DC -->|"路径 A: 传统"| ICC2 --> FM
    DC -->|"路径 B: 统一"| FC --> FM
    DC -->|"路径 C: AI"| DSO --> FM

    FM --> PT --> GDS

    classDef src fill:#e8eaf6,stroke:#283593,stroke-width:2px,color:#000
    classDef tool fill:#e3f2fd,stroke:#1565c0,color:#000
```

| 维度 | 详情 |
|------|------|
| **工具覆盖** | RTLA → DC → ICC2 → FC → DSO.ai → FM → PT，共 7 个 Synopsys 工具 |
| **流程路径** | 路径 A (DC → ICC2)、路径 B (FC 统一)、路径 C (DSO.ai 优化) |
| **四层分离** | PDK / 设计 / 公共 / 工具脚本——支持 SAED32 / TSMC40 / SAED14 多工艺切换 |
| **验证实例** | 已在 servant (RISC-V) 和 m0plus_top (ARM) 上跑通全流程 |

---

## 开源项目

| 项目 | 描述 | 技术 |
|------|------|------|
| [hvp-language-support](https://github.com/Johnmc104/hvp-language-support) | VSCode 插件：层次化验证计划语法支持 | TypeScript |
| [sdc-xdc-support](https://github.com/Johnmc104/sdc-xdc-support) | VSCode 插件：SDC/XDC 时序约束支持 | TypeScript |
| [reg_tool_manage](https://github.com/Johnmc104/reg_tool_manage) | SystemRDL 寄存器管理与多格式代码生成 | Python |
| [sv_parser](https://github.com/Johnmc104/sv_parser) | 基于 ANTLR4 的 SystemVerilog 解析器 | Python · ANTLR |


---

## 未来焦点

1. **拓展 Agent 的能力边界**：从中小型模块级验证，向更大规模的异构 SoC 场景延伸——跨模块联调、多子系统并行验证。
2. **构建无人值守的闭环修复流**：深度耦合工具平台，实现"仿真报错 / 覆盖率缺口"场景下的 Debug → Fix → Verify 自动化循环。

---

<div align="center">

*"用严谨的思路构建高品质环境，用智能的编排消散碎片化劳作"*

</div>
