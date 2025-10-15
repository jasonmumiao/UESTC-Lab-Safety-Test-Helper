# 实验室安全准入自动化工具集 (UESTC Lab Safety Toolkit)

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Stars](https://img.shields.io/github/stars/YOUR_USERNAME/UESTC-Lab-Safety-Toolkit?style=social)](https://github.com/YOUR_USERNAME/UESTC-Lab-Safety-Toolkit/stargazers)

一个面向**电子科技大学（UESTC）实验室安全准入要求**的自动化工具集。本项目旨在帮助学生更高效地完成前置学习和在线考试，包含两大核心工具：

1.  **Python 刷时长脚本**: 自动模拟在线学习心跳，以累积所需的学习时长。
2.  **油猴考试助手脚本**: 在在线考试时，提供自动答题和题库辅助更新功能。

---

## ✨ 主要功能 (Features)

### Part 1: Python 刷时长脚本 (`study_time_script.py`)

本脚本通过模拟浏览器登录后的“心跳请求”来累积学习时长，从而在后台为你累积学习时长，无需手动打开网页。

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

### 1. 配置 Python 刷时长脚本 (`study_time_script.py`)

本脚本通过模拟浏览器登录后的“心跳请求”来累积学习时长。因此，每次运行前，都需要手动获取一次有效的身份凭证 (Cookie)。

#### 步骤 1: 环境准备

-   确保你的电脑已安装 [Python 3](https://www.python.org/downloads/)。
-   打开终端（Windows 用户可使用 PowerShell 或 CMD），安装必需的 `curl_cffi` 库：
    ```bash
    pip install curl_cffi
    ```

#### 步骤 2: 获取并配置 Cookie (关键步骤)

Cookie 是脚本模拟你身份的唯一凭证，具有时效性，**每次运行脚本前都必须获取最新的**。

1.  **登录网站**: 登录 [电子科技大学 WebVPN](https://webvpn.uestc.edu.cn/) 并进入**实验室安全在线学习**页面。

2.  **打开开发者工具**: 在学习页面上，按 `F12` 键打开浏览器“开发者工具”，并切换到 **“网络 (Network)”** 选项卡。

3.  **捕获心跳请求**: 保持页面打开状态，**等待大约一分钟**，让网站自动发送一次**心跳请求**。在网络请求列表中，你会看到一个名为 `exam_xuexi_online.php` 的请求出现。

4.  **定位 Cookie**: 点击这个 `exam_xuexi_online.php` 请求，在右侧弹出的窗口中，依次找到 **标头 (Headers)** > **请求标头 (Request Headers)** > `Cookie`。

    > **提示**: `Cookie` 字段的值是一段非常非常长的字符串，这正是我们需要的。

5.  **复制 Cookie 值**: 右键点击 `Cookie` 字段的**完整值**，选择“复制值”(Copy value)。

6.  **粘贴到脚本**: 打开 `study_time_script.py` 文件，将刚刚复制的**一整行 Cookie 字符串**粘贴到 `cookie_string = '***********'` 的引号内，替换掉原来的星号。

    ```python
    # 修改前:
    cookie_string = '***********'

    # 修改后 (示例):
    cookie_string = 'remember_webvpn_user=a-long-string; other_cookie=another-long-string; ...'
    ```

#### 步骤 3: 运行脚本

1.  保存修改后的 `study_time_script.py` 文件。
2.  在终端中进入该文件所在的目录，运行脚本：
    ```bash
    python study_time_script.py
    ```
3.  脚本会开始每分钟发送一次心跳。你可以将这个终端窗口最小化，让它在后台运行，直到你累积够所需的时长。如果看到 “Cookie 可能已失效” 的提示，请重复**步骤2**更换新的 Cookie。

### 2. 配置油猴考试助手脚本 (`exam_helper.user.js`)

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