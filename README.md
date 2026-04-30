# LYB Engine 2.0 Agent Intro

## 项目概览

这是一个 Windows 桌面项目，当前形态是：

- 原生宿主：C++ / Win32 / WebView2
- 前端界面：本地 `HTML + CSS + JavaScript`
- 核心逻辑：仍由 `exe` 内的 C++ 负责执行

当前目标不是单纯做网页，而是把 HTML 界面作为 `exe` 的展示层，保留原有优化逻辑、硬件探测、进程调度和守护线程能力。

## 当前目录的作用

当前根目录：

- `D:\ai only\LYB ENGNIE\2.0`

这个目录现在更像是“源码工作区 / 编辑区”。

需要注意：

- 这里有核心源码副本
- 这里有 UI 文件副本
- 但这里不是最终完整运行目录

真正用于构建和运行的目录目前是：

- `D:\ai only\LYB ENGNIE\LYB_Engine`

如果后续要发布、构建、验证可执行文件，优先以 `LYB_Engine` 目录为准。

## 关键文件

当前工作区内的重要文件：

- `lyb_webview.cpp`
  - WebView2 宿主层
  - 负责加载本地 HTML
  - 负责前端和原生逻辑的消息通信
  - 保留并驱动原有优化逻辑

- `index.html`
  - 本地前端界面
  - 不依赖 CDN
  - 不依赖在线 React / Tailwind
  - 适合离线运行

- `build.bat`
  - 当前是 MinGW / RedPanda 编译脚本模板
  - 主要用于构建 `LYB_Engine2.0.exe`

- `compiler_info.json`
  - 早期编译环境信息
  - 内容偏旧
  - 当前实际可用编译链以 RedPanda MinGW 为主

- `84f067f8b35e833c4a0dd47553dda6f2.jpg`
  - UI 中使用的背景图资源

- `LYB Engine 2.0.lnk`
  - 指向实际程序目录的快捷方式

## 实际构建环境

当前已验证可用的 GCC 路径：

- `C:\Users\Administrator\AppData\Local\Programs\RedPanda-Cpp\mingw64\bin`

已知可用工具包括：

- `g++.exe`
- `windres.exe`
- `gendef.exe`
- `dlltool.exe`

RedPanda IDE 路径：

- `C:\Users\Administrator\AppData\Local\Programs\RedPanda-Cpp\RedPandaIDE.exe`

## 已完成状态

当前项目已经完成这些工作：

1. 将原本的原生 Win32 控件界面迁移为 WebView2 宿主界面
2. 将 HTML UI 接入 `exe` 逻辑，而不是仅作为独立网页展示
3. 前端可通过消息机制控制原生设置、游戏选择、执行与停止
4. 前端已改为本地静态资源方案，不依赖外网
5. MinGW 编译链已经打通
6. 运行所需的 `libwinpthread-1.dll` 已纳入运行目录方案

## 协作建议

如果后续 agent 接手，建议遵守下面这条工作顺序：

1. 先在 `2.0` 目录修改源码
2. 再同步到 `D:\ai only\LYB ENGNIE\LYB_Engine`
3. 在 `LYB_Engine` 目录做正式构建和运行验证

原因：

- `2.0` 目录目前是更干净的编辑入口
- `LYB_Engine` 目录才有完整的运行时依赖和最终 exe

## 风险与注意事项

- `compiler_info.json` 里的 “preferredCompiler = MSVC cl.exe” 已经过时
- 当前实际稳定路径是 RedPanda 自带 MinGW
- 如果只改 `2.0` 而不同步到 `LYB_Engine`，最终 exe 不会自动更新
- 如果未来重新引入在线前端依赖，离线启动会退化
- 如果移动运行目录，要确认 `WebView2Loader.dll`、`libwinpthread-1.dll` 和 HTML 资源仍在正确位置

## 一句话总结

这是一个“原生逻辑不动、前端界面 WebView2 化”的 Windows 桌面项目；当前源码工作区在 `2.0`，正式构建与运行目录在 `LYB_Engine`。
