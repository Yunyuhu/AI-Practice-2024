# AI 實作與互動展示

這裡保存我於 2024 年進行的 AI 課程實作與延伸練習，包含模型訓練、遷移學習、對話設計及 API 串接。2026 年進一步將部分內容整理成可直接操作的網頁，並分開提供原始碼、資料流程與驗證紀錄。

## 直接體驗成果

| 專案 | 可以操作什麼 | 原始碼 | 公開 Demo |
|---|---|---|---|
| 對話與文字處理 | 多輪角色對話；先擷取關鍵字，再整理成文 | [AI-Dialogue-Demo](https://github.com/Yunyuhu/AI-Dialogue-Demo) | [開啟展示](https://yunyuhu.github.io/AI-Dialogue-Demo/) |
| 氣象資料與 AI 助理 | 查看中央氣象署預報，並取得有資料依據的說明 | [Weather-Assistant](https://github.com/Yunyuhu/Weather-Assistant) | [開啟展示](https://yunyuhu.github.io/Weather-Assistant/) |
| 手寫數字辨識 | 直接手寫數字，查看模型輸入與十類分數 | [AI-Vision-Demos](https://github.com/Yunyuhu/AI-Vision-Demos) | [開啟展示](https://yunyuhu.github.io/AI-Vision-Demos/) |

手寫辨識、對話／文字整理與氣象問答皆已提供可直接操作的公開展示。

網頁整理版與原始 Notebook 的實作範圍分開記錄。對話展示補上獨立訪客狀態與錯誤處理；氣象展示將官方資料與 AI 說明接通；手寫辨識保留原 Dense 架構，以 NumPy 重新訓練並在瀏覽器推論。新的程式與修正不回溯視為 2024 年已完成的功能。

屋況分類原型後續發展為 [WallGuard 牆面危害 AI 辨識系統](https://github.com/Yunyuhu/WallGuard)。人臉比對與 LINE 串接的原始程式仍保留於下列來源，尚未納入上述公開網頁的完成範圍。

## 原始實作紀錄

以下 Notebook 保留當時的程式、實驗觀察與執行輸出，可對照各項應用的起點。

## 課堂作業（`course/`）

| 週次 | 筆記本 | 內容 | 技術 |
|---|---|---|---|
| Week 1 | [`week01_numpy_plotting`](course/week01_numpy_plotting.ipynb) | 用 NumPy 產生資料、Matplotlib 畫函數圖形；作業是畫出心形曲線 | NumPy、Matplotlib |
| Week 5 | [`week05_mnist_dense_nn`](course/week05_mnist_dense_nn.ipynb) | MNIST 手寫數字辨識：4 層全連接神經網路，比較 8 組 batch size 與 epoch 的設定，最後選用的版本測試集正確率 93.09% | TensorFlow／Keras |
| Week 10 | [`week10_resnet_house_damage`](course/week10_resnet_house_damage.ipynb) | 以預訓練的 ResNet50V2 做遷移學習，辨識牆面的裂縫、壁癌與鏽蝕，並用 Gradio 做成網頁；先用 42 張小樣本試做 | ResNet50V2、Gradio |
| Week 11 | [`week11_chatgpt_chatbot`](course/week11_chatgpt_chatbot.ipynb) | 串接 ChatGPT API，把對話紀錄送回去做多輪對話，再用 Gradio 做成電影推薦、戀愛顧問聊天機器人 | OpenAI API、Gradio |
| Week 13 | [`week13_deepface_face_match`](course/week13_deepface_face_match.ipynb) | 用 DeepFace 比對人臉，建立猜 BLACKPINK 成員的人臉比對原型，勝負流程尚未完成 | DeepFace、Gradio |

Week 10 的屋況辨識後來發展成課程專題 **[WallGuard 牆面危害 AI 辨識系統](https://github.com/Yunyuhu/WallGuard)**：改用 3,000 張照片，再加入 U-Net 影像分割與 GPT 處理建議。

## API 與串接練習（`practice/`）

| 筆記本 | 內容 | 技術 |
|---|---|---|
| [`openai_api_basics`](practice/openai_api_basics.ipynb) | OpenAI API 基本用法：問答、延續對話、翻譯、關鍵字擷取 | OpenAI API |
| [`linebot_echo`](practice/linebot_echo.ipynb) | 用 Flask 接收 LINE 的 webhook、ngrok 對外開放，做出會回覆相同訊息的 LINE Bot | Flask、LINE Messaging API、ngrok |
| [`weather_crawler_linebot_gpt`](practice/weather_crawler_linebot_gpt.ipynb) | 分別實作中央氣象署臺北市預報摘要，以及 LINE webhook 與 GPT 回覆程式；原版未將兩者接成氣象問答 | requests、LINE Bot SDK v3、OpenAI API |

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

