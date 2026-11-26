# AI 互動 Demo

三個打開就能用的 AI 小專案，以及它們一路發展過來的實作紀錄。

## 🧪 直接試用

| 專案 | 可以做什麼 | 試用 | 介紹 | 原始碼 |
|---|---|---|---|---|
| **天氣問問** | 選縣市看中央氣象署 36 小時預報，再問 AI 要不要帶傘、怎麼穿；AI 只根據同一份預報回答 | [開啟](https://yunyuhu.github.io/Weather-Assistant/) | [專案頁](https://yunyu-web-digital-profile.vercel.app/projects/weather-assistant) | [Weather-Assistant](https://github.com/Yunyuhu/Weather-Assistant) |
| **聊聊** | 跟會記得上下文的電影推薦、文字修潤角色聊天；或把一段筆記交給 AI，先抓關鍵字再寫成短文 | [開啟](https://yunyuhu.github.io/AI-Dialogue-Demo/) | [專案頁](https://yunyu-web-digital-profile.vercel.app/projects/chat-demo) | [AI-Dialogue-Demo](https://github.com/Yunyuhu/AI-Dialogue-Demo) |
| **數字辨識筆記** | 手寫一個數字，神經網路邊看邊猜；看得到它眼中的 28×28 影像、學習曲線與混淆矩陣 | [開啟](https://yunyuhu.github.io/AI-Vision-Demos/) | [專案頁](https://yunyu-web-digital-profile.vercel.app/projects/handwriting-notebook) | [AI-Vision-Demos](https://github.com/Yunyuhu/AI-Vision-Demos) |

前端都放在 GitHub Pages；需要金鑰的對話與氣象 API 部署在 Vercel，金鑰只存在伺服器。

## 📓 開發紀錄

這個 repo 保留 2024 年的 Jupyter Notebook，是上面三個 Demo 的起點：

| Demo | 從哪份筆記本發展而來 |
|---|---|
| 天氣問問 | [`weather_crawler_linebot_gpt`](practice/weather_crawler_linebot_gpt.ipynb)：氣象資料爬蟲、LINE Bot 與 GPT 回覆 |
| 聊聊 | [`week11_chatgpt_chatbot`](course/week11_chatgpt_chatbot.ipynb)、[`openai_api_basics`](practice/openai_api_basics.ipynb)：多輪對話與關鍵字擷取 |
| 數字辨識筆記 | [`week05_mnist_dense_nn`](course/week05_mnist_dense_nn.ipynb)：MNIST 全連接神經網路（當時測試集正確率 93.09%，Demo 以 NumPy 重新訓練為 93.23%） |

筆記本保留當時的程式與執行輸出；Demo 的介面、伺服器與重新訓練是之後的整理，兩者分開記錄。屋況辨識的筆記本後來發展成 [WallGuard 牆面危害 AI 辨識系統](https://github.com/Yunyuhu/WallGuard)。

### 模型與對話（`course/`）

| 週次 | 筆記本 | 內容 | 技術 |
|---|---|---|---|
| Week 1 | [`week01_numpy_plotting`](course/week01_numpy_plotting.ipynb) | 用 NumPy 產生資料、Matplotlib 畫函數圖形；作業是畫出心形曲線 | NumPy、Matplotlib |
| Week 5 | [`week05_mnist_dense_nn`](course/week05_mnist_dense_nn.ipynb) | MNIST 手寫數字辨識：4 層全連接神經網路，比較 8 組 batch size 與 epoch 的設定，最後選用的版本測試集正確率 93.09% | TensorFlow／Keras |
| Week 10 | [`week10_resnet_house_damage`](course/week10_resnet_house_damage.ipynb) | 以預訓練的 ResNet50V2 做遷移學習，辨識牆面的裂縫、壁癌與鏽蝕，並用 Gradio 做成網頁；先用 42 張小樣本試做 | ResNet50V2、Gradio |
| Week 11 | [`week11_chatgpt_chatbot`](course/week11_chatgpt_chatbot.ipynb) | 串接 ChatGPT API，把對話紀錄送回去做多輪對話，再用 Gradio 做成電影推薦、戀愛顧問聊天機器人 | OpenAI API、Gradio |
| Week 13 | [`week13_deepface_face_match`](course/week13_deepface_face_match.ipynb) | 用 DeepFace 比對人臉，建立猜 BLACKPINK 成員的人臉比對原型，勝負流程尚未完成 | DeepFace、Gradio |

Week 10 的屋況辨識後來發展成課程專題 **[WallGuard 牆面危害 AI 辨識系統](https://github.com/Yunyuhu/WallGuard)**：改用 3,000 張照片，再加入 U-Net 影像分割與 GPT 處理建議。

### API 串接（`practice/`）

| 筆記本 | 內容 | 技術 |
|---|---|---|
| [`openai_api_basics`](practice/openai_api_basics.ipynb) | OpenAI API 基本用法：問答、延續對話、翻譯、關鍵字擷取 | OpenAI API |
| [`linebot_echo`](practice/linebot_echo.ipynb) | 用 Flask 接收 LINE 的 webhook、ngrok 對外開放，做出會回覆相同訊息的 LINE Bot | Flask、LINE Messaging API、ngrok |
| [`weather_crawler_linebot_gpt`](practice/weather_crawler_linebot_gpt.ipynb) | 分別實作中央氣象署臺北市預報摘要，以及 LINE webhook 與 GPT 回覆程式；原版未將兩者接成氣象問答 | requests、LINE Bot SDK v3、OpenAI API |

### 執行筆記本

用 Google Colab 或 Jupyter 開啟。需要金鑰的筆記本會用 `get_secret()` 讀取，不把金鑰寫在程式裡：在 Colab 左側欄的 🔑 **Secrets** 新增下列名稱並開啟筆記本存取權，或設成同名的環境變數。

| 名稱 | 用途 | 用到的筆記本 |
|---|---|---|
| `OPENAI_API_KEY` | OpenAI API | Week 11、openai_api_basics、weather_crawler_linebot_gpt |
| `LINE_CHANNEL_ACCESS_TOKEN`、`LINE_CHANNEL_SECRET` | LINE Messaging API | linebot_echo、weather_crawler_linebot_gpt |
| `NGROK_AUTHTOKEN` | ngrok | linebot_echo |
| `CWA_API_KEY` | 中央氣象署開放資料平臺的授權碼 | weather_crawler_linebot_gpt |

### 備註

- 這些筆記本依 2024 年的套件版本撰寫，部分套件之後改版，可能無法直接執行。例如 `linebot_echo` 用的 LINE Bot SDK v2 與 ngrok v2 都已改版，當時的執行也沒能成功連上 ngrok，程式碼僅供參考。
- Week 5 最後的 Gradio 手寫板展示當時沒有成功，程式碼保留為註解。
- Week 10 的範例照片來自 [concrete](https://github.com/Yunyuhu/concrete)；Week 13 原本的照片資料集已設為私人，想執行需要自備照片。

