🧸 AI 桌面精靈 Kuma — 專案使用說明
歡迎使用 Kuma！Kuma 是一隻可愛的 AI 桌面熊，能陪伴你對話、記憶重要事項、提醒行程，並且擁有自己的性格！

本專案使用：

桌面應用程式（C# WPF）

本地大型語言模型推論（DeepSeek-R1 7B）

Docker 部署的後端服務（Ollama + MongoDB）

📦 安裝與啟動流程
1. 安裝 Docker Desktop
如果你的電腦尚未安裝 Docker，請先到 Docker 官方網站 下載並安裝。

安裝完成後，請確保 Docker Desktop 正常運作（右下角有小鯨魚圖示）。

2. 啟動後端服務（MongoDB + Ollama）
打開終端機（Terminal / CMD / PowerShell），進入 docker/ 資料夾，並執行以下指令：

bash
Copy
Edit
cd docker
docker-compose --env-file .env up -d
這個指令會自動：

啟動 MongoDB 資料庫

啟動 Ollama 語言模型推論服務，並加載 DeepSeek-R1 7B 模型

⏳ 第一次啟動時會花一些時間（因為需要下載 DeepSeek-R1 模型，約數 GB 大小，請耐心等待）

3. 啟動桌面精靈應用
後端服務啟動後，請雙擊 YourApp.exe （你的桌面精靈應用程式）。

Kuma 會自動連接到本機服務，開始與你互動！

📝 設定 Kuma 的個性（initial_prompt.txt）
在專案目錄下有一個檔案：

plaintext
Copy
Edit
initial_prompt.txt
這裡設定了 Kuma 的初始個性與行為指令。

✅ 你可以自由修改內容，例如：

改變 Kuma 的語氣（正式、可愛、調皮）

決定 Kuma 回覆的語言（中文、英文）

加入更多指令範例（提醒、記筆記等）

修改後，重新啟動桌面程式，Kuma 就會以新的個性與你互動囉！

🛠️ 常見問題

問題	解決方式
啟動後 .exe 出現連線失敗？	請確認 Docker 是否正在運行 (docker ps)，並檢查 MongoDB/Ollama 是否成功啟動。
Ollama 第一次啟動很慢？	需要時間下載 DeepSeek-R1 7B 模型，可以預先拉取模型加速（見下方進階）。
Docker-compose 指令錯誤？	請確認你的 Docker Desktop 是最新版本，且有權限執行。
⚡ 進階：預先拉取 DeepSeek-R1 7B 模型（加速啟動）
如果想要減少啟動等待時間，可以手動下載模型：

先單獨啟動 Ollama：

bash
Copy
Edit
docker-compose up -d ollama
然後進入 Ollama 容器，手動拉取模型：

bash
Copy
Edit
docker exec -it ollama ollama pull deepseek-r1:7b
完成後，下次啟動就不需要重新下載！

🧹 停止所有服務
若需要關閉後端服務，可以執行：

bash
Copy
Edit
docker-compose down
這樣會停止並移除容器（資料仍保留在 Volume 中）。

📋 注意事項
本專案使用 DeepSeek-R1 7B 本地推論模型，確保你的設備有足夠資源（建議至少16GB記憶體）。

桌面程式（WPF）是在本機 Windows 執行，不在 Docker 裡面。

請確保 Docker 有足夠磁碟空間（建議10GB以上）。

如果需要使用 Notion API、Google Calendar API 等功能，需另外設定 API Key（未來版本會支援）。

🏁 祝你使用愉快！
Kuma 期待成為你的學習與生活好夥伴！
如果覺得有趣，也歡迎分享給朋友一同使用！
