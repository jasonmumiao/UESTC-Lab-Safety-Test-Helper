# 实验室安全考试助手 (UESTC Lab Safety Test Helper)

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Stars](https://img.shields.io/github/stars/YOUR_USERNAME/UESTC-Lab-Safety-Test-Helper?style=social)](https://github.com/YOUR_USERNAME/UESTC-Lab-Safety-Test-Helper/stargazers)

一个用于**电子科技大学（UESTC）实验室安全准入考试**的油猴（Tampermonkey）脚本。它旨在帮助学生更高效地完成考试和维护题库，主要功能包括自动答题和智能提取新题/错题。

A Tampermonkey script designed for the **UESTC Lab Safety Exam**. It aims to help students complete the exam and maintain the question bank more efficiently, featuring auto-answering and intelligent question extraction.

---

## ✨ 主要功能 (Features)

本脚本具有两大核心功能，并能自动识别所在页面（答题页或答卷查看页）以提供相应功能。

1.  **📝 智能自动答题 (On Exam Page)**
    * **一键答题**：在考试页面点击按钮，即可为当前页面的所有题目自动填写答案。
    * **模糊匹配**：采用字符串相似度算法，即使题目与题库中的题目有细微差别（如空格、标点），只要相似度超过80%，也能成功匹配。
    * **匹配提示**：对于通过模糊匹配找到的题目，脚本会在题目下方显示题库中的原题，方便快速核对。

2.  **🔍 题库辅助更新 (On Review Page)**
    * **一键提取**：在考后的“答卷查看”页面，脚本提供一个按钮，可自动扫描整份试卷。
    * **智能比对**：自动找出您本地题库中**不存在的新题目**或**答案错误的题目**。
    * **格式化输出**：将所有新发现或已更正的题目和答案，以可以直接粘贴到脚本中的代码格式，生成在一个文本框中。
    * **轻松更新**：您只需一键复制生成的代码，粘贴到自己的脚本文件中，即可完成题库的扩充和修正。

## 🚀 安装 (Installation)

1.  **安装脚本管理器**
    首先，你的浏览器需要安装一个用户脚本管理器。推荐使用 [**Tampermonkey**](https://www.tampermonkey.net/)，它支持大多数主流浏览器，如 Chrome, Firefox, Edge, Safari。

2.  **安装本脚本**
    * **从 GitHub 手动安装**:
        * 打开项目中的 `实验室安全考试自动答题 & 题库提取脚本 v3.0-3.0.user.js` 文件。
        * 点击右上角的 "Raw" 按钮。
        * Tampermonkey 会自动弹出安装页面，点击“安装”即可。

## 📖 使用指南 (How to Use)

### 1. 自动答题

-   进入实验室安全考试的**答题页面**。
-   在页面右侧会出现一个蓝色的 **[自动答题 (模糊匹配)]** 按钮。
-   点击该按钮，脚本会自动填充当前页面的答案。
-   对于模糊匹配的题目，请检查下方显示的题库原题是否正确对应。
-   完成一页后，手动点击“下一页”，然后再次点击答题按钮，直到所有页面完成。
-   **提交前请务必检查一遍所有答案！**

### 2. 更新与校对题库

-   完成一次考试后，进入**“答卷查看”页面**。
-   在页面右侧会出现一个青色的 **[提取新题/错题]** 按钮。
-   点击该按钮，脚本会开始扫描并与您当前脚本内置的题库进行比对。
-   完成后，页面上会弹出一个包含格式化代码的文本框。
-   点击 **[复制到剪贴板]** 按钮。
-   打开 Tampermonkey 管理面板，编辑本脚本，将复制的内容粘贴到 `const questionBank = { ... };` 对象内部，即可完成题库的更新。

#### 示例：如何粘贴新题库
```javascript
// ...
// --- 题库数据 (最终修正版 v2.1) ---
const questionBank = {
    // 在这里粘贴你复制的新代码
    "新题目1": "答案A",
    "已更正的题目2": "答案B",
    // 原有的旧题目...
};
// ...
```

## ⚠️ 免责声明 (Disclaimer)

* 本脚本仅供学习和技术交流使用，旨在减少重复性劳动。
* 题库答案来源于过往考试，**不保证100%的准确性**。请务必在提交前自行核对，特别是那些您不确定的题目。
* 因使用本脚本导致的任何后果（包括但不限于考试成绩不理想、账号问题等），作者概不负责。

## 📄 许可证 (License)

This project is licensed under the [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0).
