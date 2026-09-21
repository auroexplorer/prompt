# 🌟 AuroExplorer: 亞斯/自閉光譜 AI 社交探索小幫手

🚀 [立即體驗 AuroExplorer](https://gemini.google.com/gem/1yyRhRyPnM1DJFW5IHn1JpZ5ub0q1mOqd)

## 💡 專案簡介

**AuroExplorer** 是一個專門設計給在亞斯/自閉光譜中的人使用的 LLM 客製化提示。它命令大型語言模型扮演一個耐心提供協助的社交探索小幫手，協助你探索、分析和練習虛構的社交情境。目前底層 LLM 為 Gemini。

AuroExplorer 的設計遵循[多項嚴格的原則](./design.markdown)，以確保安全、心理健康與實用性。

## 🚫 警告與免責聲明 (使用前必讀)

1. **非專業建議：** AI 的建議不具備法律責任，無法取代專業醫療或危機輔導。尤其遇重大困難或高壓力情境時，應立即尋求專業協助，勿依賴本工具做出重大決定。
2. **隱私保護：** 由於底層 Gemini 欠缺隱私保護，請絕對使用**虛構資訊**，不要輸入自己或他人的任何隱私資訊。
3. **模型限制：** 本工具基於大型語言模型，其分析與預測僅基於大多數人的想像，可能充滿社會或文化偏見，與實際情況完全不同。模型對相同情境可能會給出隨機且截然不同的分析或建議，請將其視為多種可能性之一。

## 🛠️ 如何協助開發測試

如果你想測試更改後的指令，以下是測試步驟：

1. **取得指令：** 複製 [`prompt-gemini.markdown`](./prompt-gemini.markdown) 的完整內容（在 GitHub 上記得用 “Raw”）。
2. **開啟 Gemini 介面：** 前往 Gemini 網頁或應用程式。
3. **貼上指令：**
   - 如果你可以使用 **Gem 管理工具**，請新增 Gem, 並將指令貼入該設定中。
   - 你也可以把指令當作與 Gemini 互動的**第一個訊息**直接貼上，以啟用 AuroExplorer。

### 格式與 CI 驗證

每個 pull request 與推送至 `main` 的變更，都會由 CI 檢查受 Git 追蹤的 Markdown 格式，以及 GitHub Actions workflow。格式規則見 [`.mdformat.toml`](./.mdformat.toml)。

本機使用 Python 3.14 建立虛擬環境，安裝與 CI 相同的套件後執行檢查：

```sh
python3.14 -m venv .venv
. .venv/bin/activate
python -m pip install --require-hashes --requirement .github/workflows/mdformat-requirements.txt
git ls-files -z '*.md' '*.markdown' | xargs -0 python -m mdformat --check
git diff --check
```

修改 workflow 時，另以 actionlint 1.7.12 執行 `actionlint -shellcheck shellcheck`；此檢查需要先安裝 ShellCheck。

更新 Markdown 工具時，修改 [直接依賴清單](./.github/workflows/mdformat-requirements.in)，再用 Python 3.14 產生包含間接依賴與雜湊的鎖定檔：

```sh
python -m pip install pip-tools
pip-compile --generate-hashes --output-file=.github/workflows/mdformat-requirements.txt --strip-extras .github/workflows/mdformat-requirements.in
```

將兩份依賴清單一起提交，並重新安裝鎖定的套件、執行上述檢查。

這些自動檢查涵蓋格式與 workflow 靜態檢查。Prompt 的語意變更仍須依照[設計原則](./design.markdown)人工檢視隱私保護、重大決定提醒及高壓力安全流程；目前沒有可執行的 prompt 語意測試。

## 🤝 回饋與支持

Auro 是一個開源項目，歡迎任何形式的貢獻和反饋！

如果你發現指令有任何需要改進的地方，請[提交 issue](https://github.com/auroexplorer/prompt/new)。特別歡迎亞斯/自閉光譜中的用戶、從事相關工作的研究人員或醫護人員提供意見，以確保工具真正符合用戶需求。

## 📜 授權協議 (License)

本專案採用 **Apache License 2.0** 授權協議。詳情請見 [LICENSE](LICENSE) 文件。
