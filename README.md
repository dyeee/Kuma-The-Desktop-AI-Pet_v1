🧸 AI 桌面精靈 — Docker 環境使用說明
本專案包含：

桌面 AI 精靈應用程式（WPF，.exe）

Docker 部署的後端服務（Ollama + MongoDB）

精靈依賴這些服務才能正常執行，因此本專案提供一鍵啟動的 docker-compose 環境。

🚀 安裝與啟動流程
1. 安裝 Docker Desktop
請至 Docker 官方網站 下載並安裝 Docker Desktop。

安裝後，請確保 Docker 可以正常運行（右下角小鯨魚圖示）。

2. 準備專案
請確保你已經取得專案資料夾，結構如下：

plaintext
Copy
Edit
DesktopAIPet/
├── YourApp.exe   （桌面精靈程式）
└── docker/
    ├── docker-compose.yml
    ├── .env
3. 啟動後端服務
打開命令提示字元（或 PowerShell），進入 docker/ 資料夾，執行：

bash
Copy
Edit
cd docker
docker-compose --env-file .env up -d
這個指令會自動下載並啟動：

MongoDB 資料庫（localhost:27017）

Ollama 語言模型推論服務（localhost:11434）

第一次執行需要一點時間（因為會下載 DeepSeek-r1 模型，模型約幾GB）。

4. 啟動桌面應用
啟動完 Docker 後，直接雙擊 YourApp.exe 啟動桌面精靈！

桌面精靈會自動連線到本機的 Ollama / MongoDB：

AI 對話 → 呼叫 DeepSeek-r1 模型

筆記 → 記錄到 Notion

提醒 → 新增到 Google Calendar

使用者資訊 → 存在 MongoDB

📋 .env 配置說明
在 docker/.env 中，可以調整啟動的參數，例如：

dotenv
Copy
Edit
MONGO_PORT=27017
OLLAMA_PORT=11434
OLLAMA_MODEL=deepseek-r1
如果有需要換模型、換端口，可以在這裡改！

🛠️ 常見問題

問題	解決方式
問：啟動後 .exe 出現連線失敗？	確認 Docker 是否正在運行 (docker ps)，MongoDB 與 Ollama 是否有啟動。
問：第一次啟動 Ollama 下載模型很慢？	下載 DeepSeek-r1 模型需要時間，耐心等待，或考慮預先拉好（看下方進階加速）。
問：如何重啟服務？	docker-compose down 關掉後，docker-compose up -d 重啟即可。
⚡ 進階：預先拉取 DeepSeek-r1 模型（加速第一次啟動）
如果你想要在一開始就快速啟動 DeepSeek 模型，可以手動先拉好：

啟動 Ollama 服務（docker-compose up -d ollama）

執行：

bash
Copy
Edit
docker exec -it ollama ollama pull deepseek-r1
這樣 Ollama 會事先下載模型，之後重啟就不必等待！

🧹 停止服務
如果需要關掉所有 Docker 服務：

bash
Copy
Edit
docker-compose down
這樣可以釋放本機資源。

📢 注意事項
桌面精靈 .exe 本身不在 Docker 中運行，它仍然在 Windows 本機跑。

所有資料會保存在 Docker Volume（MongoDB）與本機 Ollama Volume（模型資料夾）。

請確保 Docker 有足夠的磁碟空間（至少10GB以上）。

🏁 完成！
現在，你擁有一個 能對話、能記憶、能提醒 的桌面 AI 精靈啦！

如果遇到任何問題，請記得先檢查：

Docker 是否正常運作

MongoDB 與 Ollama 服務是否啟動

.env 參數是否正確設定

祝你使用愉快！✨
