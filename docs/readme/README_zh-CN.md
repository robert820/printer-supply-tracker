<div align="center">

<a href="https://blog.dei3c.com" target="_blank" rel="noopener noreferrer">
  <img src="https://github.com/user-attachments/assets/2830eb70-512c-4ddb-87ec-5213a6e465b1" alt="得翼科技 | 打印机耗材追踪器" height="70" />
</a>

<br /><br />

[繁體中文](../../README.md) · [English](README_en.md) · **简体中文**

# 打印机耗材追踪器 (Printer Supply Tracker)

### 专为企业办公室、总务采购与电脑网络管理员打造的打印机耗材自动监控与 Google 表格同步工具
告别手动巡检与逐台抄表！通过 SNMP 自动轮询碳粉剩余量与打印计数，智能排程后台上传，开机自动补查补登。

[![Platform](https://img.shields.io/badge/Platform-Windows%207%20%7C%208%20%7C%2010%20%7C%2011%20%7C%20WinPE-blue?style=flat-square&logo=windows)](https://github.com/robert820/printer-supply-tracker)
[![License](https://img.shields.io/badge/License-Freeware-informational?style=flat-square)](../../LICENSE)
[![Type](https://img.shields.io/badge/Type-Freeware%20%7C%20Portable-success?style=flat-square)](#-下载与使用说明)
[![Download](https://img.shields.io/badge/Download-GitHub%20Releases-blue?style=flat-square&logo=github)](https://github.com/robert820/printer-supply-tracker/releases)

**彻底摆脱 Windows 任务计划程序失灵困扰，以轻量常驻系统托盘实现 100% 无人值守自动化管理！**

[软件简介](#-软件简介) · [核心功能](#-核心功能) · [软件操作画面](#-软件操作画面) · [下载与使用说明](#-下载与使用说明) · [系统需求](#-系统兼容性与需求) · [常见问题](#-常见问题-faq) · [问题反馈](#-问题反馈与支持)

</div>

---

## 📖 软件简介

在企业、学校、办公室或租用复印机管理中，行政总务与 IT 人员每逢月底或固定结算周期，往往面临繁琐的手工流程：
1. **逐台抄表耗时费力**：必须亲自走到每台打印机/复印机前调出计数器菜单，逐一记录黑白与彩色打印张数。
2. **耗材库存猝不及防**：无法实时掌握黑色、青色、品红、黄色（CMYK）碳粉消耗速度，常等到打印机亮红灯停机才紧急采购。
3. **传统任务计划容易漏跑**：使用 Windows 自带的任务计划程序执行脚本时，常因电脑休眠、密码过期、权限不一致或节假日断电而错过排程，导致整期报表数据脱节。

**“打印机耗材追踪器 (Printer Supply Tracker)”** 是一款专为 Windows 平台打造的原生免安装绿色常驻工具。本工具通过标准 SNMP 网络协议定期自动轮询所有网络打印设备，准确读取打印总张数与各色碳粉剩余百分比，并通过 Web API 自动同步写入指定的 **Google 表格 (Google Sheets)**。

内置自研的**智能排程与补登引擎**，能够自动顺延避开周末与公众假日。若开机时检测到错过指定排程时间，程序将立即主动触发“开机补查”，确保报表统计万无一失！

---

## ✨ 核心功能

### 1. ⚡ 自动扫描多品牌打印机状态 (SNMP 协议)
- 通过局域网以 SNMP 协议自动查询所有网络打印设备。
- 完整获取：设备型号、序列号、放置物理位置、黑白打印总张数、彩色打印总张数、CMYK 各色碳粉剩余百分比。
- **具体支持品牌与型号适配清单**：
  - **Ricoh (理光)**：
    - 彩色机型：全系列商用彩色数码复合机（支持黑白/彩色独立计数与 CMYK 4 色碳粉刻度）
    - 黑白机型：MP 3554、MP 3555、IM 3500、MP 6054、MP 6055、MP 6502、MP 6503、MP 7502、MP 7503
  - **Fuji Xerox / FUJIFILM (富士施乐 / 富士胶片)**：
    - 彩色机型：ApeosPort 系列、DocuCentre 系列彩色复合机
    - 黑白机型：ApeosPort 3060、ApeosPort 3560、DocuCentre 3060
  - **SHARP (夏普)**：
    - 彩色机型：MX 彩色系列、BP 彩色系列数码复合机
    - 黑白机型：MX-M 系列（包含 MX-M365N）、BP-M 系列
- 防卡死设计：若某台设备离线或无响应，自动标注“连接失败”并继续轮询下一台，查询过程绝不挂起中断。

### 2. 📊 自动同步至 Google 表格 (云端集中汇总)
- 轮询完成后，自动将所有设备的计数、碳粉剩余值与时间戳格式化上传至 Google 表格。
- 支持轻量级 Google Apps Script Web App 接口集成，无需在本地配置笨重的 Python 或 Node.js 运行环境。
- 提供完备的上传格式验证，若接口地址错误或权限受限，界面清晰提示精准报错原因，便于快速定位。

### 3. ⏰ 智能排程与开机补登机制 (告别任务计划程序)
- **内置轻量排程引擎**：放弃易受系统休眠干扰的 Windows Task Scheduler，改由程序内部常驻计时，精准唤醒。
- **支持每月多日排程**：可灵活勾选每月固定多个日期执行（如每月 1 号、15 号、25 号）。
- **周末自动提前／顺延**：遇周六、周日自动调整至相近的工作日执行。
- **节假日智能识别**：自动比对行政假期日历，遇长假顺延至开工首日。
- **开机自动补查机制**：若排程预定时刻电脑处于关机状态，开机启动后程序会自动检测错过的任务并立即补跑，防止报表开天窗。

### 4. 🛡️ 系统托盘 (System Tray) 常驻与三色状态指示灯
- 最小化至任务栏右下角系统托盘，不占用桌面任务栏空间。
- 实时状态 LED 指示灯：
  - 🔵 **蓝灯**：正在执行 SNMP 轮询或向表格上传中
  - 🟢 **绿灯**：所有设备连接正常且排程就绪
  - 🔴 **红灯**：存在设备连接异常或尚未配置 IP 列表
- 双击托盘图标随时呼出主窗口；右键快捷菜单支持“立即执行”与“安全退出”。

### 5. 🧪 手动测试与立即执行
- **测试 SNMP 连接**：即刻探测指定 IP 列表连通性与 SNMP 响应，不会触发云端数据写入。
- **立即执行与上传**：随时手动完整走完一次扫描与云端上传流程，无需苦等排程触发。

### 6. 📝 完整本地审计日志 (Log)
每次查询状态、上传返回、时间记录与网络报错信息均详细持久化于本地日志文件（`PST_Unattended.log`），便于管理员追溯排查。

---

## 📸 软件操作画面

<div align="center">
  <img src="../../images/應用程式執行畫面.png" alt="打印机耗材追踪器操作界面" width="720" />
  <p>▲ 打印机耗材追踪器主界面：设备状态列表、CMYK 碳粉刻度指示条与排程规则设置</p>
</div>

---

## 📦 下载与使用说明

### 📥 下载方式
1. 前往本项目的 [Releases 页面](https://github.com/robert820/printer-supply-tracker/releases) 下载最新版编译程序。
2. 本程序为**单一免安装绿色二进制可执行文件**，无需安装任何额外依赖或运行库，下载解压即开即用。

### 🚀 快速上手五步骤

1. **设置目标打印机列表**：进入“目标设备与 SNMP”页面，逐行输入要监控的打印机 IP 地址，并设置 SNMP Community 团体字串（通常默认为 `public`）。
2. **配置 Google 表格同步**：进入“一般设定”页面，粘贴 Google Apps Script Web App 部署地址（以 `https://.../exec` 结尾）并填写目标工作表名称。
3. **连接测试**：点击“测试 SNMP 连接”按钮，验证所有打印设备网络连通与响应正常。
4. **设置执行周期**：进入“执行时间参数”页面，选择每月执行日期与时刻，勾选**周末提前**、**节假日顺延**与**开机补查**。
5. **开启开机自启**：在“系统设置”页面开启“开机自动启动”，即可在电脑开机后自动常驻后台无感运行。

---

## 🖥️ 系统兼容性与需求

- **操作系统**：Windows 11 / 10 / 8.1 / 8 / 7 (SP1) 及 Windows Server 2012+
- **硬件架构**：通用兼容 64 位 (x64) 与 32 位 (x86) 架构
- **网络环境**：本机需与打印机处于同一局域网 (LAN) 并具备外网访问权限以上传 Google 表格
- **依赖环境**：原生 Rust 编译单文件，无须安装 .NET Framework、VC++ 运行库或 Python

---

## ❓ 常见问题 (FAQ)

<details>
<summary><b>Q1: 这款软件完全免费吗？企业内部可以使用吗？</b></summary>
A: 是的！本软件基于专有免费软件协议（Freeware）发布，完全免费供个人、企业机构及电脑维保服务商在内部或客户现场使用。严禁单独售卖或重新打包捆绑商业付费产品牟利。
</details>

<details>
<summary><b>Q2: 目前具体支持哪些打印机品牌与型号？</b></summary>
A: 本工具核心已针对办公复合机三大主力品牌建立专属 OID 解析规则，具体支持机型涵盖：
- **Ricoh (理光)**：
  - 彩色机型：全系列商用彩色多功能数码复合机（黑白与彩色打印张数、CMYK 四色碳粉剩余量）
  - 黑白机型：MP 3554、MP 3555、IM 3500、MP 6054、MP 6055、MP 6502、MP 6503、MP 7502、MP 7503
- **Fuji Xerox / FUJIFILM (富士施乐 / 富士胶片)**：
  - 彩色机型：ApeosPort 系列、DocuCentre 系列彩色复合机
  - 黑白机型：ApeosPort 3060、ApeosPort 3560、DocuCentre 3060
- **SHARP (夏普)**：
  - 彩色机型：MX 彩色系列、BP 彩色系列数码复合机
  - 黑白机型：MX-M 系列（含 MX-M365N）、BP-M 系列
只要设备开启标准 SNMP 服务，程序即可自动识别机型并提取正确字段数据。
</details>

<details>
<summary><b>Q3: 为什么不直接使用 Windows 任务计划程序？</b></summary>
A: 任务计划程序在系统休眠、用户密码变动时极易静默失败，且无智能补登机制。本软件自带轻量常驻引擎，彻底解决漏报问题。
</details>

---

## 💬 问题反馈与支持

- 🐛 **错误报告与功能建议**：欢迎前往 [GitHub Issues](https://github.com/robert820/printer-supply-tracker/issues) 提交。
- 🌐 **得翼科技官方网站**：[https://blog.dei3c.com](https://blog.dei3c.com)

---

## 📄 授权条款 (License)

本软件采用专有免费软件授权（Proprietary Freeware），完整条款请参阅 [LICENSE](../../LICENSE) 文件。
