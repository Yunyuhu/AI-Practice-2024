# AI-Practice-2024

2024 年碩一時的 AI 練習，包含課堂作業與自己做的 API 串接練習：神經網路、遷移學習、ChatGPT API、人臉比對，以及 LINE Bot。全部是 Jupyter Notebook。

## 課堂作業（`course/`）

| 週次 | 筆記本 | 內容 | 技術 |
|---|---|---|---|
| Week 1 | [`week01_numpy_plotting`](course/week01_numpy_plotting.ipynb) | 用 NumPy 產生資料、Matplotlib 畫函數圖形；作業是畫出心形曲線 | NumPy、Matplotlib |
| Week 5 | [`week05_mnist_dense_nn`](course/week05_mnist_dense_nn.ipynb) | MNIST 手寫數字辨識：4 層全連接神經網路，比較 8 組 batch size 與 epoch 的設定，最後選用的版本測試集正確率 93.09% | TensorFlow／Keras |
| Week 10 | [`week10_resnet_house_damage`](course/week10_resnet_house_damage.ipynb) | 以預訓練的 ResNet50V2 做遷移學習，辨識牆面的裂縫、壁癌與鏽蝕，並用 Gradio 做成網頁；先用 42 張小樣本試做 | ResNet50V2、Gradio |
| Week 11 | [`week11_chatgpt_chatbot`](course/week11_chatgpt_chatbot.ipynb) | 串接 ChatGPT API，把對話紀錄送回去做多輪對話，再用 Gradio 做成電影推薦、戀愛顧問聊天機器人 | OpenAI API、Gradio |
| Week 13 | [`week13_deepface_face_match`](course/week13_deepface_face_match.ipynb) | 用 DeepFace 比對人臉，做成猜 BLACKPINK 成員的 PK 遊戲 | DeepFace、Gradio |

Week 10 的屋況辨識後來發展成課程專題 **[WallGuard 牆面危害 AI 辨識系統](https://github.com/Yunyuhu/WallGuard)**：改用 3,000 張照片，再加入 U-Net 影像分割與 GPT 處理建議。

## API 與串接練習（`practice/`）

| 筆記本 | 內容 | 技術 |
|---|---|---|
| [`openai_api_basics`](practice/openai_api_basics.ipynb) | OpenAI API 基本用法：問答、延續對話、翻譯、關鍵字擷取 | OpenAI API |
| [`linebot_echo`](practice/linebot_echo.ipynb) | 用 Flask 接收 LINE 的 webhook、ngrok 對外開放，做出會回覆相同訊息的 LINE Bot | Flask、LINE Messaging API、ngrok |
| [`weather_crawler_linebot_gpt`](practice/weather_crawler_linebot_gpt.ipynb) | 從中央氣象署開放資料抓臺北市的天氣預報並整理成每日摘要，再把 LINE Bot 接上 GPT 回覆訊息 | requests、LINE Bot SDK v3、OpenAI API |

## 怎麼執行

用 Google Colab 或 Jupyter 開啟。需要金鑰的筆記本會用 `get_secret()` 讀取，不把金鑰寫在程式裡：在 Colab 左側欄的 🔑 **Secrets** 新增下列名稱並開啟筆記本存取權，或設成同名的環境變數。

| 名稱 | 用途 | 用到的筆記本 |
|---|---|---|
| `OPENAI_API_KEY` | OpenAI API | Week 11、openai_api_basics、weather_crawler_linebot_gpt |
| `LINE_CHANNEL_ACCESS_TOKEN`、`LINE_CHANNEL_SECRET` | LINE Messaging API | linebot_echo、weather_crawler_linebot_gpt |
| `NGROK_AUTHTOKEN` | ngrok | linebot_echo |
| `CWA_API_KEY` | 中央氣象署開放資料平臺的授權碼 | weather_crawler_linebot_gpt |

## 備註

- 這些筆記本依 2024 年的套件版本撰寫，部分套件之後改版，可能無法直接執行。例如 `linebot_echo` 用的 LINE Bot SDK v2 與 ngrok v2 都已改版，當時的執行也沒能成功連上 ngrok，程式碼僅供參考。
- Week 5 最後的 Gradio 手寫板展示當時沒有成功，程式碼保留為註解。
- Week 10 的範例照片來自 [concrete](https://github.com/Yunyuhu/concrete)；Week 13 原本的照片資料集已設為私人，想執行需要自備照片。
