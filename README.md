# LYB Engine 2.0

一款基于 **Windows** 的桌面游戏优化工具，采用 **C++ + Win32 + WebView2** 架构。项目将现代化 HTML 界面与原生系统优化能力深度融合，提供专业级的游戏性能调整和进程管理方案。

## 🎯 项目特性

### 核心优化功能
- **电源计划管理** - 一键切换系统电源策略到高性能模式
- **VBS 管理** - 虚拟化安全（Hyper-V 相关）控制
- **VSync 控制** - NVIDIA 显卡 VSync 禁用
- **进程抑制** - Edge / WeGame / Steam / ACE 等进程后台限制
- **HPET 禁用** - AMD 处理器平台时钟优化
- **大小核调度** - Intel 12/13/14/15 代及 AMD Ryzen AI 的核心亲和性管理
- **游戏进程守护** - 实时后台进程监控与资源调度

### 支持的游戏
- Valorant（国际服）
- Delta Force（国区）
- CS:GO 2
- PUBG

### 技术栈
- **宿主层**：C++ / Win32 / WebView2
- **界面层**：本地静态 HTML + CSS + JavaScript（完全离线运行）
- **编译链**：MinGW (RedPanda C++)
- **依赖**：WebView2 Runtime、libwinpthread-1.dll

## 📦 项目结构

```
LYB-s-Public-Repository/
├── lyb_webview.cpp          # WebView2 宿主应用主程序（C++ 核心逻辑）
├── index.html               # 前端界面（本地 HTML）
├── build.bat                # MinGW 编译脚本
├── compiler_info.json       # 编译环境配置（参考用）
├── 84f067f8b35e833c4a0dd47553dda6f2.jpg  # UI 背景图资源
├── LYB Engine 2.0.lnk       # 快捷方式
├── agent.MD                 # 项目协作说明
├── LICENSE                  # MIT 许可证
└── README.md                # 本文件
```

## 🚀 快速开始

### 环境要求
- **操作系统**：Windows 10 / 11（64 位）
- **编译器**：MinGW-w64（RedPanda C++ 内置）
- **WebView2 Runtime**：[下载安装](https://developer.microsoft.com/en-us/microsoft-edge/webview2/)

### 编译步骤

1. **安装编译环境**
   - 下载并安装 [RedPanda C++](https://sourceforge.net/projects/redpanda-cpp/)
   - 确认 MinGW 路径：`C:\Users\YourUser\AppData\Local\Programs\RedPanda-Cpp\mingw64\bin`

2. **编译项目**
   ```bash
   build.bat
   ```
   或使用 RedPanda IDE 打开项目编译

3. **运行**
   编译成功后，生成 `LYB_Engine2.0.exe`，直接运行即可

## 🎮 使用说明

### 基本操作流程

1. **启动应用** - 运行 `LYB_Engine2.0.exe`
2. **硬件检测** - 首次启动自动检测 CPU / GPU / 内存速度
3. **选择游戏** - 在界面中选择要优化的游戏
4. **配置选项** - 根据需要勾选各项优化开关
5. **执行优化** - 点击"启动守护"按钮
6. **实时监控** - 系统每 60 秒检查游戏进程，每 61 秒检查平台进程

### 优化选项说明

| 选项 | 说明 | 适用场景 |
|------|------|--------|
| **电源计划** | 切换到高性能模式 | 所有游戏 |
| **VBS 禁用** | 关闭虚拟化安全 | 对帧率影响明显的硬件 |
| **VSync 禁用** | 移除垂直同步 | NVIDIA 显卡 + 高刷新率屏幕 |
| **Edge 后台抑制** | 限制 Edge 浏览器资源占用 | 常见场景 |
| **ACE 进程限制** | 腾讯游戏安全模块限制 | 腾讯游戏（Valorant/Delta） |
| **WeGame 抑制** | 限制 WeGame 平台进程 | 腾讯游戏 |
| **游戏核心亲和性** | 让游戏使用所有 P 核 | 混合架构 CPU（Intel 12 代+） |
| **禁用 E 核** | 游戏独占 P 核心 | 混合架构 CPU + 低延迟要求 |

## 🔧 高级配置

### 工作目录说明

项目使用两个主要目录：

- **编辑工作区**：`D:\ai only\LYB ENGNIE\2.0`
  - 存储源代码与 UI 文件副本
  - 用于开发与修改

- **运行目录**：`D:\ai only\LYB ENGNIE\LYB_Engine`
  - 完整的编译输出与运行时文件
  - 包含 WebView2Loader.dll、libwinpthread-1.dll

### 部署建议

1. 修改源码在编辑工作区
2. 编译后同步到运行目录
3. 在运行目录执行正式构建与测试

## ⚙️ 系统恢复

应用停止守护后自动执行以下恢复操作：

- 恢复原始电源计划
- 恢复 VBS 设置
- 恢复 NVIDIA VSync 设置
- 恢复所有受控进程的优先级与亲和性

所有修改都会被记录与还原，**不会产生系统残留**。

## 📋 依赖文件清单

| 文件 | 来源 | 用途 |
|------|------|------|
| `WebView2Loader.dll` | WebView2 Runtime | 加载 WebView2 组件 |
| `libwinpthread-1.dll` | MinGW 运行时 | 线程库支持 |
| `html/index.html` | 项目内含 | 前端界面资源 |

**确保以上文件与 exe 位于同一目录或正确的子目录结构中。**

## 🐛 故障排除

### 常见问题

**Q: 启动时显示"创建 WebView2 控制器失败"**
- A: 请安装最新版 [WebView2 Runtime](https://developer.microsoft.com/en-us/microsoft-edge/webview2/)

**Q: "缺少界面文件"错误**
- A: 确认 `html\index.html` 与可执行文件在同一目录结构中

**Q: 编译失败 - 找不到 gcc**
- A: 检查 MinGW 路径是否正确，或使用 RedPanda IDE 打开项目

**Q: HPET 禁用选项灰显**
- A: Intel CPU 默认不支持 HPET 禁用（该选项仅对 AMD 有效）

**Q: 优化后游戏无明显改善**
- A: 不同硬件与游戏优化效果差异大；建议逐项测试找到最适配的配置

## 📝 协作指南

如果后续进行开发维护，请遵循以下工作流：

1. **源码编辑** → `2.0` 目录修改 `lyb_webview.cpp` 或 `index.html`
2. **编译测试** → 运行 `build.bat`
3. **同步部署** → 将编译结果复制到 `LYB_Engine` 目录
4. **最终验证** → 在 `LYB_Engine` 目录测试可执行文件

详见 [agent.MD](./agent.MD) 了解更多技术细节。

## ⚠️ 注意事项

- **提升权限**：部分优化功能需要管理员权限
- **系统修改**：涉及注册表与进程管理，仅在信任的环境中使用
- **备份建议**：首次使用前建议系统还原点
- **独立分发**：适合本地离线运行，不依赖在线服务

## 📄 许可证

本项目采用 **MIT License** 开源许可证。

**所有人都可以自由使用、修改和分发本项目代码，包括商业用途。**

详见 [LICENSE](./LICENSE) 文件。

## 👤 作者

**laiyanbiao66-debug**  
GitHub: [@laiyanbiao66-debug](https://github.com/laiyanbiao66-debug)

---

**最后更新**：2026-05-08  
**项目状态**：活跃开发中

有问题或建议？欢迎提交 Issue 或 Pull Request！
