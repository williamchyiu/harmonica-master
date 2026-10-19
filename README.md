# 🎵 口琴全能大師 | Harmonica Master (v6 Flagship)

> **專業半音階口琴即時調音、初學特訓營與自由入譜評分系統**
>
>
>
> *A High-Performance Web Audio DSP Tuner, Beginner Drill Coach & Interactive Score Assessment Tool for 12-Hole Chromatic Harmonica.*

## 📖 專案簡介 (Introduction)

**口琴全能大師 (Harmonica Master)** 是一套專為 **12 孔 C 調半音階口琴（Solo Tuning，音域 C4 至 C#7）** 打造的極致輕量、零安裝單檔案 Web 應用程式。

傳統調音器通常針對吉他或人聲設計，容易被口琴尖銳的高階泛音干擾而發生「八度跳躍（Octave Jumping）」，更會因瀏覽器預設的降噪演算法將口琴長音當成背景雜音過濾。本專案透過純原生 **Web Audio API** 與 **時域自相關（Autocorrelation）演算法**，打造無失真、高靈敏的即時音準與氣流反饋體驗。

## 🌟 核心特色 (Key Features)

### 1. 🎛️ 自由吹奏調音模式 (Free Tuner Mode)

- **12 孔即時互動位圖 (Dynamic 12-Hole Layout)**：隨吹隨亮，即時標記「吹氣（藍色）」、「吸氣（綠色）」以及「推鍵（橘黃色按鍵狀態）」。
- **音域診斷與統計**：自動即時分類低音區（1~4孔）、中音區（5~8孔）、高音區（9~12孔），並統計各音域的長音穩定度百分比。
- **60 FPS 音準軌跡儀 (Pitch Contour)**：以平滑曲線可視化音高波動，綠線基準精準捕捉微小音準起伏。
- **點擊試聽發聲**：支援直接點擊位圖上的任何孔位格子，系統將發出合成簧片標準音供調音對照。

### 2. 🎓 初學者特訓營 (Beginner Drills & Coach)

- **🔊 大聲程度控制 (Dynamics Coach)**：設定弱音 p、中音 mf、強音 f 吹奏目標，檢測大聲吹是否壓音偏低、小聲吹是否斷氣。
- **🔘 按鍵準確度 (Slide Button Accuracy)**：兩步驟引導同孔「自然音 → 推鍵到底」，偵測推鍵是否果斷、嘴角有無漏氣。
- **🥁 節奏感卡拍訓練 (Rhythm & Attack)**：以起音波形上升斜率精確測量起始吹氣時間，與 BPM 拍點比對，誤差在 ±85ms 內判定為「完美卡拍」。
- **〰️ 震音/抖音分析器 (Vibrato Analyzer)**：利用過零率演算法即時運算手震音（Wah-Wah）或喉腹震音的頻率（Hz）與深度（Cents）。

### 3. 🎼 自由入譜闖關與評分 (Score & Play Mode)

- **彈性入譜工作台**：支援一鍵點選簡譜小鍵盤（`1~7`、高低音點、`#` 升半音）或直接貼上純文字簡譜與音名（如 `C4 D4 G4`）。
- **不卡關設計**：內建「新手寬鬆模式（忽略八度，唱名對即過關）」與「手動跳過按鈕（Skip）」。
- **100 分制診斷報告**：挑戰結算後產生包含「平均音準偏差（Cents）」、「最大連擊數（Max Combo）」、「氣流穩定評級」與客製化練琴改善建議。

### 4. 🎚️ 專業音頻前級與校準

- **A4 基準音動態校準 (**440Hz∼443Hz**)**： 支援一鍵切換 `440Hz`（國際標準）、`441Hz`、`442Hz`（口琴主流出廠基準）、`443Hz`。
- **硬體前級軟體增益 (Mic Sensitivity Gain)**： 提供 1.0×∼8.0× 動態放大倍率，適配不同設備的麥克風阻抗。
- **調性首調唱名 (Movable Do)**： 支援 C、D、F、G、A、B♭ 調性轉換，音名與簡譜唱名即時切換。

## 🔬 音訊 DSP 與技術規格 (Audio DSP Architecture)

```
[ Microphone Input ]
        │ (echoCancellation: false, noiseSuppression: false)
        ▼
[ Mic Gain Node ] ── (1.0x ~ 8.0x 前級訊號放大)
        │
        ▼
[ Biquad Lowpass Filter ] ── (3200Hz 截止頻率, 濾除吹氣高頻嘶聲)
        │
        ▼
[ AnalyserNode (FFT 2048) ]
        │
        ▼
[ Time-Domain Autocorrelation + Parabolic Interpolation ]
        │
        ├──> RMS 均方根 ───> 0~100% 氣流力度條
        └──> 基頻週期 T0 ──> 精準頻率 (0.1 Hz) ──> MIDI / Cents 計算
```

- **音準換算數學公式**：
   MIDI Note=round(12×log2​(A4​f​))+69Cents=1200×log2​(ftarget​f​)
- **口琴音域覆蓋**：MIDI 60 (C4​=261.63Hz) 至 MIDI 97 (C7♯​=2217.46Hz)。

## 🚀 如何執行 (How to Run)

本專案採用 **Single-File（單檔案架構）**，完全不需要安裝 Node.js、npm 或任何後端伺服器！

1. **直接開啟**： 下載專案後，直接雙擊 `harmonica_master_v6.html`，以 Chrome、Edge、Safari 或 Firefox 開啟即可。
2. **本機伺服器（推薦）**： 在專案目錄下開啟終端機執行：

   ```
   npx serve .
   # 或使用 Python
   python -m http.server 8080
   ```
3. **GitHub Pages 免費託購**： 在 GitHub 倉庫設定中開啟 **Pages**，將分支設為 `main`，即可獲得線上免安裝口琴調音網站。

## 🛡️ 版本控制防退化指南 (Git Safety)

為避免後續修改代碼造成功能倒退，專案已建立防護標籤機制：

| 操作情境 | 推薦指令 |
| --- | --- |
| **打上全新穩定標籤** | `git tag -a v6.0-stable -m "v6 穩定版本"` |
| **代碼改壞，強制還原** | `git reset --hard v6.0-stable` |
| **開新分支測試新功能** | `git checkout -b feature/new-idea` |
| **同步更新到 GitHub** | `git push origin main --tags` |

## 🤖 Cursor IDE 開發防護規則 (.cursorrules)

本專案包含 `.cursorrules` 與 `.cursor/rules/harmonica-master.mdc`。當使用 AI 輔助編輯代碼時，必須遵守以下鐵律：

1. **單檔案結構原則**：嚴禁擅自將 HTML、CSS、JS 拆分為外部檔案。
2. **不可重啟瀏覽器降噪**：`echoCancellation`、`noiseSuppression`、`autoGainControl` 必須維持 `false`。
3. **不可替換時域自相關**：嚴禁改用粗糙的頻域 FFT 峰值法。
4. **維持三大模式變數隔離**：自由調音、初學特訓、樂譜挑戰的狀態變數不得互相污染。

## 📄 授權條款 (License)

MIT License © 2026 [William Chiu](https://github.com/williamchyiu)
