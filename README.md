# 实验室安全准入自动化工具集 (UESTC Lab Safety Toolkit)

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Stars](https://img.shields.io/github/stars/jasonmumiao/UESTC-Lab-Safety-Toolkit?style=social)](https://github.com/jasonmumiao/UESTC-Lab-Safety-Toolkit/stargazers)

一个面向**电子科技大学（UESTC）实验室安全准入要求**的自动化工具集。本项目旨在帮助学生更高效地完成前置学习和在线考试，包含两大核心工具：

1.  **Python 刷时长脚本**: 自动模拟在线学习心跳，以累积所需的学习时长。
2.  **油猴考试助手脚本**: 在在线考试时，提供自动答题和题库辅助更新功能。

---

## ✨ 主要功能 (Features)

### Part 1: Python 刷时长脚本 (`study_time_script.py`)

本脚本通过模拟浏览器行为，自动向服务器发送“在线学习”心跳请求，从而在后台为你累积学习时长，无需手动打开网页。

-   **高效稳定**: 每分钟发送一次心跳请求，确保时长稳定增长。
-   **浏览器模拟**: 使用 `curl_cffi` 库模拟 Chrome 110 浏览器的底层指纹，有效绕过常见的脚本检测。
-   **智能检测**: 能够检测 Cookie 失效或被 WebVPN 网关拦截的情况，并自动停止。

### Part 2: 油猴考试助手脚本 (`exam_helper.user.js`)

本脚本在浏览器端运行，为在线考试提供强大的辅助功能。

-   **智能自动答题**: 在考试页面一键为当前页面的所有题目自动填写答案。
-   **模糊匹配**: 即使题目与题库有细微差别，只要相似度超过80%，也能成功匹配并提示。
-   **题库辅助更新**: 在考后的“答卷查看”页面，可一键扫描并提取**新题目**或**错误答案**，并生成可直接复制的代码，方便你快速更新和完善个人题库。

## 🚀 安装与配置 (Installation & Setup)

两个工具的安装和使用方法不同，请根据需要分别配置。

### 1. 配置 Python 刷时长脚本

#### 步骤 1: 环境准备

-   确保你的电脑已安装 [Python 3](https://www.python.org/downloads/)。
-   打开终端（Windows 用户可使用 PowerShell 或 CMD），安装必需的 `curl_cffi` 库：
    ```bash
    pip install curl_cffi
    ```

#### 步骤 2: 获取 Cookie

这是最关键的一步！Cookie 是脚本的身份凭证，有效期较短，**每次运行前都需要获取最新的**。

1.  登录 [电子科技大学 WebVPN](https://webvpn.uestc.edu.cn/)。
2.  进入“实验室与设备处” -> “实验室安全考试系统” -> 点击**开始学习**，进入学习页面。
3.  按下 `F12` 键打开浏览器开发者工具，切换到 **“网络 (Network)”** 选项卡。
4.  在页面上等待约一分钟，开发者工具的列表中会出现一个名为 `exam_xuexi_online.php` 的请求。
5.  点击该请求，在右侧窗口中找到 **“标头 (Headers)”** -> **“请求标头 (Request Headers)”**。
6.  找到 `Cookie:` 字段，**复制其完整的、超长的值**。
    > **注意**: 这个 Cookie 值非常长，请确保全部复制。

#### 步骤 3: 运行脚本

1.  将复制的 Cookie 字符串粘贴到 `study_time_script.py` 文件中的 `cookie_string = '***********'` 处，替换掉星号。
2.  在终端中运行脚本：
    ```bash
    python study_time_script.py
    ```
3.  脚本会开始每分钟发送一次心跳。你可以将这个终端窗口最小化，让它在后台运行。

### 2. 配置油猴考试助手脚本

#### 步骤 1: 安装脚本管理器

-   你的浏览器需要安装一个用户脚本管理器。推荐使用 [**Tampermonkey**](https://www.tampermonkey.net/) (支持 Chrome, Firefox, Edge 等)。

#### 步骤 2: 安装本脚本

-   打开本项目中的 `exam_helper.user.js` 文件。
-   点击右上角的 "Raw" 按钮。
-   Tampermonkey 会自动弹出安装页面，点击“安装”即可。

## 📖 使用指南 (How to Use)

### 自动答题

-   进入实验室安全考试的**答题页面**。
-   页面右侧会出现蓝色的 **[自动答题 (模糊匹配)]** 按钮，点击即可填充答案。
-   完成一页后，手动翻页，再次点击按钮。

### 更新题库

-   考试结束后，进入**“答卷查看”页面**。
-   页面右侧会出现青色的 **[提取新题/错题]** 按钮。
-   点击后会生成一个文本框，包含需要更新的题库代码。
-   点击 **[复制到剪贴板]**，然后打开 Tampermonkey 编辑器，将代码粘贴到 `questionBank` 中即可。

## ⚠️ 免责声明 (Disclaimer)

-   本工具集仅供学习和技术交流使用，旨在减少重复性劳动，请勿用于任何商业或非法用途。
-   Cookie 包含个人敏感信息，请妥善保管，切勿泄露。
-   题库答案来源于过往考试，**不保证100%的准确性**。请务必在提交前自行核对。
-   因使用本脚本导致的任何后果（包括但不限于账号问题、考试成绩不佳等），作者概不负责。

## 📄 许可证 (License)

This project is licensed under the [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0).
