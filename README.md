# 深蹲教練 (Squat Coach)

單檔 MediaPipe 深蹲自我檢測工具，繁體中文介面。目標是用舊安卓手機接近 BodyPark ATOM 的訓練回饋體驗。

線上版：https://p0217-ai.github.io/squat-coach/

## 功能

- 全身骨架疊圖（MediaPipe Pose Landmarker lite）
- **腰椎估點**：以髖－肩幾何估算下背位置，側面偵測屁股眨眼／腰椎代償
- 姿勢問題提示：前傾過大、膝蓋內夾（正面）、腳跟抬起、左右重心偏移
- **本次動作分數（0–100）**：依深度、背、膝蓋、速度評分；**累積動作分數**為每次分數加總
- **組數訓練**：自訂每組目標次數、組數；環形進度（如 10/12）；組間休息計時
- **語音回饋**（Web Speech API，zh-TW）：預設年輕台灣女聲；報數與改法同一句（如「第5下，膝蓋往外推」）；設定可選語音並試聽；同改法最多隔一下再說；可靜音
- 大字回饋橫幅與即時提示
- **熱量估算**（MET × 體重，標示為估計值）；可選 **藍牙心率帶**（Web Bluetooth Heart Rate 0x180D）
- 每下離心／向心秒數；結束摘要（逐下分數與主要問題）
- 訓練紀錄（localStorage）與 CSV 匯出
- 可選：畫布 MediaRecorder 錄製含疊圖影片並下載
- 螢幕常亮（Wake Lock）；舊手機自動降幀

## 限制（請留意）

- **腰椎點是幾何估算**，不是 BodyPark 那種專用腰椎模型，準度受拍攝角度與遮擋影響。
- **心率**需裝置支援 Web Bluetooth，且心率帶／手錶有廣播 Heart Rate Service；否則顯示「—」，熱量仍用 MET 估算。
- 熱量為公式估算，非間接測熱。
- GitHub Pages 為靜態託管；相機需 **HTTPS**（或 localhost）。
- 錄影依瀏覽器支援（多為 webm），部分舊安卓可能無法錄。

## 手機用法

1. 三腳架、鏡頭約髖高、距離 2–3 公尺、全身入鏡
2. 瀏覽器打開 HTTPS 網址，允許相機
3. 設定組數／目標次數／體重；側面練腰椎與深度，正面練內夾與偏移
4. 按開始偵測；做完按停止並儲存

## 本機預覽

```bash
python3 -m http.server 8765
# 開 http://127.0.0.1:8765 （相機需 HTTPS 或 localhost）
```

## 技術

- 單檔 `index.html`（CDN：`@mediapipe/tasks-vision`）
- 設定鍵：`squatCoach.settings.v2`；紀錄：`squatCoach.sessions.v2`
