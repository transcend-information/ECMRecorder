# ECMREC Retail README

[English](README.md) | [繁體中文](README.zh-TW.md)

ECMREC 是一套以 Windows 為主的相機應用程式，提供即時預覽、快照、連續分段 MP4 錄影、遠端控制、相機斷線復原及本機事件記錄功能。預覽與錄影功能必須搭配相容的 Transcend ECM100 相機使用。

<a id="toc"></a>
## 目錄

- [相容性](#compatibility)
- [硬體需求](#hardware-requirements)
- [EXE 執行必備檔案](#exe-runtime-required-files)
- [產品綁定需求](#product-binding-requirement)
- [產品概要](#overview)
- [主要功能介紹](#features)
- [產品定位](#positioning)

<a id="compatibility"></a>
## 相容性

- Transcend ECM100（必須）

[回到目錄](#toc)

<a id="hardware-requirements"></a>
## 硬體需求

1. **支援平台**

- Windows 10/11 x64

2. **CPU 建議規格**

- 建議至少 4 核心。
- 8 核心 / 16 執行緒可穩定執行本軟體。

3. **RAM 建議規格**

- 建議至少 16 GB RAM。

[回到目錄](#toc)

<a id="exe-runtime-required-files"></a>
## EXE 執行必備檔案

目前打包目錄結構如下：

```text
ECM100REC/
	ECM100REC.exe
	config.ini
	FFmpeg/
		ffmpeg.exe
	_internal/
		...（Python 執行期與相依套件）
	<HOSTNAME>/
		ecm100rec.db
```

執行必備：

- `ECM100REC.exe`
- `FFmpeg/ffmpeg.exe`
- `_internal/`

通常建議一併保留：

- `config.ini`（執行期設定檔）

執行後產生資料（新包不一定需要）：

- `<HOSTNAME>/` 與 `ecm100rec.db`

[回到目錄](#toc)

<a id="product-binding-requirement"></a>
## 產品綁定需求

本軟體必須搭配 ECM100 裝置，才能使用預覽與錄影功能。執行時規則如下：

- 當未偵測到裝置名稱包含 `ECM100` 時，禁止啟動預覽。
- 當未偵測到裝置名稱包含 `ECM100` 時，禁止開始錄影。
- 當預覽或錄影啟動檢查觸發 ECM 錯誤時，會立即停止目前預覽串流。

[回到目錄](#toc)

<a id="overview"></a>
## 產品概要

ECM100REC 是一套以 Windows 為主的相機錄影工具，提供以下核心能力：

- 即時相機預覽與解析度切換。
- 連續分段錄影，產出 MP4 檔案。
- 錄影畫面可加上時間浮水印。
- 可將命令紀錄、錄影紀錄與相機事件寫入本機 SQLite。
- 支援 Windows 開機自啟。

[回到目錄](#toc)

<a id="features"></a>
## 主要功能介紹

### 1. 即時預覽與裝置管理

- 掃描可用相機裝置。
- 需要至少一台裝置名稱包含 `ECM100` 的相機。
- 支援切換解析度。
- 提供 HUD 顯示目前狀態、FPS 與輸出檔名。
- 預覽畫面可在 UI 中切換準心顯示與隱藏。

### 2. 錄影與時間浮水印

- 使用 FFmpeg 寫入 MP4。
- 支援連續分段錄影。
- 可在畫面上疊加時間浮水印。
- Windows 版預設提供 `h264_qsv`、`libx264`、`hevc_qsv` 編碼選項。
- 錄影時會在儲存空間偏低時發出提醒，達到門檻時會自動停止錄影。
- 儲存空間預警門檻、硬停止門檻與磁碟檢查頻率都可在 `config.ini` 中設定。
- 使用者手動停止錄影時，會先跳出確認視窗再結束錄影。

### 3. 連續錄影穩定性與復原

- 提供長時間連續分段錄影流程。
- 包含相機斷線偵測與重連流程。
- 在跳過重連時，仍可安全停止錄影。
- 狀態列加入更明顯的層級顏色，警告與錯誤更容易辨識。
- 相機重連或預覽恢復後，UI 會顯示更清楚的停止/重連狀態文字。

### 4. SQLite 與作業紀錄

若設定啟用 SQLite，系統會建立或維護多種資料表，用於紀錄：

- 錄影開始與停止命令
- 影片紀錄
- SAVE 指令送入的外部檔案路徑
- 相機斷線等事件

### 5. 設定持久化與自動啟動

- 使用 `config.ini` 保存儲存路徑、錄影秒數、浮水印、畫質、編碼等設定。
- 可設定 Windows 開機自動啟動。
- 首次執行時會自動產生裝置 UUID。

[回到目錄](#toc)

<a id="positioning"></a>
## 產品定位

ECM100REC 適合需要以下特性的相機錄影場景：

- 長時間穩定分段錄影。
- 本地端可獨立運作。
- 透過單一 UI 集中管理裝置、畫質與錄影行為。

[回到目錄](#toc)
