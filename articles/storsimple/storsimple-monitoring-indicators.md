---
title: "監控指示器 aaaStorSimple |Microsoft 文件"
description: "描述 hello 淺-發光二極體 (Led) 和警報用 toomonitor hello 狀態 hello StorSimple 裝置。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 59dee7b9-ca6d-4fd9-96e6-a0071e8d248e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: e690b8f4727272f5fbb8886a594a046f794a1380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-monitoring-indicators-toomanage-your-device"></a>使用 StorSimple 監控指示器 toomanage 您的裝置
## <a name="overview"></a>概觀
您的 StorSimple 裝置包括淺-發光二極體 (Led) 和警示，您可以使用 toomonitor hello 模組和 hello StorSimple 裝置的整體狀態。 hello 監控指示器位於 hello hello 裝置主要機箱和 hello EBOD 機箱的硬體元件。 監控指示器 hello 可以 Led 或警報。

有三種 LED 狀態用 tooindicate hello 的模組狀態： 綠色、 閃爍綠色 toored 琥珀色，或紅琥珀色。  

* 綠色 LED 代表運作狀態良好  
* 閃爍綠色 toored 琥珀色 Led 代表 hello 可能需要使用者介入的非嚴重狀況存在。  
* 紅琥珀色 Led 指出 hello 模組內出現重大錯誤。  

hello 這篇文章的其餘部分描述的 hello 各種監控指示器 Led，與其 hello StorSimple 裝置上的位置、 hello 裝置狀態根據 hello LED 狀態和任何相關警報。

## <a name="front-panel-indicator-leds"></a>前端面板 LED 指示燈
hello 前端面板，也稱為 hello*操作面板*或*前置 ops 面板*，顯示 hello 系統中所有的 hello 模組 hello 彙總狀態。 hello 前端面板 hello StorSimple 主要和 EBOD 機箱，hello 上都相同，如下所示。  

   ![裝置正面面板][1]

hello 前端面板包含下列指示器 hello:  

1. 靜音按鈕
2. 電源 LED 指示燈 (綠色/紅琥珀色)
3. 模組錯誤 LED 指示燈 (開時為紅琥珀色/關)
4. 邏輯錯誤 LED 指示燈 (開時為紅琥珀色/關)
5. 單元識別碼顯示  

hello hello 前端面板 Led hello 裝置以及 hello EBOD 機箱之間的主要差異為 hello**系統單元識別碼**hello LED 顯示器上顯示。 hello 預設單元識別碼 hello 裝置上顯示**00**，而 hello hello EBOD 機箱上顯示的預設單元識別碼為**01**。 這可讓您 tooquickly hello 裝置開啟時區分 hello 裝置和 hello EBOD 機箱。 如果您的裝置已關閉，請使用所提供的 hello 資訊[開啟新裝置](storsimple-turn-device-on-or-off.md#turn-on-a-new-device)toodifferentiate hello hello EBOD 機箱裝置。  

## <a name="front-panel-led-status"></a>前端面板 LED 狀態
使用下列資料表 tooidentify hello 狀態 hello hello 裝置或 hello EBOD 機箱的前端面板上的 hello Led 所指示的 hello。  

| 系統電源 | 模組錯誤 | 邏輯錯誤 | 警示 | 狀態 |
| --- | --- | --- | --- | --- |
| 紅琥珀色 |關 |關 |N/A |AC 電源中斷、 備用電源，或 AC 電源，hello 控制器模組已移除。 |
| 綠色 |開啟 |開啟 |N/A |操作面板電源開啟 (5 秒) 測試狀態 |
| 綠色 |關 |關 |N/A |電源開啟、所有功能正常 |
| 綠色 |開啟 |N/A |PCM 故障 LED、風扇故障 LED |任何 PCM 故障、 風扇故障、 溫度過高或過低 |
| 綠色 |開啟 |N/A |I/O 模組 LED |任何控制器模組錯誤 |
| 綠色 |開啟 |N/A |N/A |機箱邏輯錯誤 |
| 綠色 |閃爍 |N/A |控制器模組上的模組狀態 LED。 PCM 故障 LED、風扇故障 LED |安裝的控制器模組類型不明、I2C 匯流排故障、控制器模組重要產品資料 (VPD) 組態錯誤 |

## <a name="power-cooling-module-pcm-indicator-leds"></a>電源冷卻模組 (PCM) LED 指示燈
電源冷卻模組 (PCM) 指示器 Led 位於 hello hello 主要機箱或 EBOD 機箱上每個 PCM 模組的背面。 本主題討論如何 toouse hello 遵循您的 StorSimple 裝置的 Led toomonitor hello 狀態。  

* Hello 主要機箱的 PCM Led
* Hello EBOD 機箱的 PCM Led

## <a name="pcm-leds-for-hello-primary-enclosure"></a>Hello 主要機箱的 PCM Led
hello StorSimple 裝置有 764W PCM 模組和額外電池。 hello 如下圖所示為 hello 裝置 hello LED 面板。  

   ![Hello 主要機箱的 PCM Led][2]

LED 燈圖例：

1. AC 電源故障
2. 風扇故障
3. 電池故障
4. PCM 正常
5. DC 故障
6. 電池良好  

hello 狀態 hello hello 指出 PCM LED 面板。 hello 裝置 PCM LED 面板有六個 Led。 其中四個 Led 顯示 hello 電源供應器和風扇 hello hello 狀態。 hello 其餘兩個 Led 指出 hello hello PCM 中的 hello 備用電池模組狀態。 您可以使用下列資料表 toodetermine hello 狀態 hello PCM hello。  

### <a name="pcm-indicator-leds-for-power-supply-and-fan"></a>電源供應器與風扇的 PCM LED 指示燈
| 狀態 | PCM 正常 (綠色) | AC 故障 (琥珀色) | 風扇故障 (琥珀色) | DC 故障 (琥珀色) |
| --- | --- | --- | --- | --- |
| 沒有 AC 電源 (tooenclosure) |關 |關 |關 |關 |
| 沒有 AC 電源 (只有此 PCM) |關 |開啟 |關 |開啟 |
| 有 AC 且 PCM 開啟 - 正常 |開啟 |關 |關 |關 |
| PCM 故障 (風扇故障) |關 |關 |開啟 |N/A |
| PCM 故障 (安培、 電壓、電流過高) |關 |開啟 |開啟 |開啟 |
| PCM (風扇超出容許範圍) |開啟 |關 |關 |開啟 |
| 待命模式 |不停閃爍 |關 |關 |關 |
| PCM 韌體下載 |關 |不停閃爍 |不停閃爍 |不停閃爍 |

### <a name="pcm-indicator-leds-for-hello-backup-battery"></a>Hello 備用電池的 PCM 指示器 Led
| 狀態 | 電池良好 (綠色) | 電池故障 (琥珀色) |
| --- | --- | --- |
| 沒有電池 |關 |關 |
| 有電池且已充電 |開啟 |關 |
| 電池充電中或維護放電 |不停閃爍 |關 |
| 電池「軟性」故障 (可修復) |關 |不停閃爍 |
| 電池「硬性」故障 (不可修復) |關 |開啟 |
| 已卸除電池 |不停閃爍 |關 |

## <a name="pcm-leds-for-hello-ebod-enclosure"></a>Hello EBOD 機箱的 PCM Led
hello EBOD 機箱都有一個 580W PCM，沒有額外電池。 hello hello EBOD 機箱的 PCM 面板有僅適用於 hello 電源供應器和 hello 風扇的指示器 Led。 hello 下圖顯示這些 Led。

   ![在 hello EBOD 機箱的 PCM Led][3] 

您可以使用下列資料表 toodetermine hello 狀態 hello PCM hello。  

| 狀態 | PCM 正常 (綠色) | AC 故障 (琥珀色) | 風扇故障 (琥珀色) | DC 故障 (琥珀色) |
| --- | --- | --- | --- | --- |
| 沒有 AC 電源 (tooenclosure) |關 |關 |關 |關 |
| 沒有 AC 電源 (只有此 PCM) |關 |開啟 |關 |開啟 |
| 有 AC 且 PCM 為開 - 正常 |開啟 |關 |關 |關 |
| PCM 故障 (風扇故障) |關 |關 |開啟 |X |
| PCM 故障 (安培、 電壓、電流過高) |關 |開啟 |開啟 |開啟 |
| PCM (風扇超出容許範圍) |開啟 |關 |關 |開啟 |
| 待命模式 |不停閃爍 |關 |關 |關 |
| PCM 韌體下載 |關 |不停閃爍 |不停閃爍 |不停閃爍 |

## <a name="controller-module-indicator-leds"></a>控制器模組 LED 指示燈
hello StorSimple 裝置包含 hello 主要控制站和 hello EBOD 控制器模組的 Led。   

### <a name="monitoring-leds-for-hello-primary-controller"></a>Hello 主要控制器的監控 Led
hello 圖可協助您識別 hello hello 主要控制站上的 Led。 （所有 hello 元件是列出的 tooaid 方向）。  

   ![監視 LED 燈 - 主要控制器][4]

使用下列資料表 toodetermine 是否 hello 控制器模組皆運作正常的 hello。  

### <a name="controller-indicator-leds"></a>控制器 LED 指示燈
| LED | 說明 |
| --- | --- |
| ID LED (藍色) |表示正在識別該 hello 模組。 如果 hello 藍色 LED 閃爍不停執行中控制器，則 hello 控制站是 hello 主動控制站且 hello 另一個則 hello 待命控制器。 如需詳細資訊，請參閱[識別您的裝置上 hello 作用中控制器](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device)。 |
| 錯誤 LED (琥珀色) |指出 hello 控制器中的錯誤。 |
| 正常 LED (綠色) |穩定的綠燈表示該 hello 控制器很正常。 不停閃爍綠色表示控制器 VPD 組態錯誤。 |
| SAS 活動 LED (綠色) |持續亮著綠色表示連線目前沒有活動。 閃爍的綠燈表示 hello 連線有進行中的活動。 |
| 乙太網路狀態 LED |右側代表連結/網路活動：連結作用中 (持續亮著綠色)、有網路活動 (不停閃爍綠色)。 左側代表網路速度：1000 MB/秒 (黃色)、100 MB/秒 (綠色) 及 10 MB/秒 (關)。 根據 hello 元件模型，此燈可能閃爍即使未啟用 hello 網路介面。 |
| POST LED |開啟 hello 控制站時，請指出 hello 開機進度。 Tooboot hello StorSimple 裝置時，此 LED 將協助 Microsoft 支援服務識別 hello 失敗發生所在的 hello 開機程序中的 hello 點。 |

> [!IMPORTANT]
> 如果 hello 故障 LED 亮起，則問題可能會重新啟動 hello 控制站可以解決的 hello 控制器模組。 請如果重新啟動的 hello 控制器並未解決此問題，連絡 Microsoft 支援服務。  
> 
> 

### <a name="monitoring-leds-for-hello-ebod-ebod-enclosure"></a>Hello EBOD （EBOD 機箱） 的監控 Led
每個 hello 6 Gb/s SAS EBOD 控制器有 hello 下列圖例所示，指出其狀態的 Led。  

  ![監視 LED 燈 - EBOD 機相][5]

使用下列資料表 toodetermine 是否 hello EBOD 控制器模組運作正常的 hello。  

### <a name="ebod-controller-module-indicator-leds"></a>EBOD 控制器模組 LED 指示燈
| 狀態 | I/O 模組正常 (綠色) | I/O 模組故障 (琥珀色) | 主機連接埠活動 (綠色) |
| --- | --- | --- | --- |
| 控制器模組確定 |開啟 |關 |- |
| 控制器模組錯誤 |關 |開啟 |- |
| 沒有外部主機連接埠連接 |- |- |關 |
| 外部主機連接埠連接 – 沒有活動 |- |- |開啟 |
| 外部主機連接埠連接 – 活動 |- |- |不停閃爍 |
| 控制器模組中繼資料錯誤 |不停閃爍 |- |- |

## <a name="disk-drive-indicator-leds-for-hello-primary-enclosure-and-ebod-enclosure"></a>Hello 主要機箱和 EBOD 機箱的磁碟機指示器 Led
hello StorSimple 裝置有主要機箱 hello 和 hello EBOD 機箱中的磁碟機。 每個磁碟機都有各自的監控 LED 指示燈，如本節中所述。 

Hello 磁碟機，hello 磁碟機狀態由綠色 LED 與紅琥珀色 LED 掛接在每個磁碟機載具模組的 hello 正面。 hello 下圖顯示這些 Led。

  ![磁碟機 LED 燈][6]

使用下列資料表 toodetermine hello 狀態的每個磁碟機，接著會影響整體前端面板 LED 狀態 hello hello。  

### <a name="disk-drive-indicator-leds-for-hello-ebod-enclosure"></a>Hello EBOD 機箱的磁碟機指示器 Led
| 狀態 | 活動正常 LED (綠色) | 錯誤 LED (紅琥珀色) | 相關聯操作面板 LED |
| --- | --- | --- | --- |
| 未安裝磁碟機 |關 |關 |None |
| 磁碟機已安裝且可運作 |有活動時會不停開/關地閃爍 |X |None |
| SCSI 機箱服務 (SES) 裝置身分識別已設定 |開啟 |每 2 秒閃爍 1 次 |None |
| SES 裝置錯誤位元已設定 |開啟 |開啟 |邏輯錯誤 (紅色) |
| 電源控制電路故障 |關 |開啟 |模組錯誤 (紅色) |

## <a name="audible-alarms"></a>有聲警報器
StorSimple 裝置中包含音效與 hello 主要機箱和 hello EBOD 機箱相關聯的警示。 可發出聲音的警示位於 hello 的前端面板 （也稱為 hello 操作面板） 兩個機箱。 hello 可發出聲音的警示表示出現錯誤狀況時。 hello 下列條件時，會啟動 hello 警示：  

* 風扇錯誤或故障
* 電壓超出範圍
* 超過或低於溫度條件
* 熱超限
* 系統錯誤
* 邏輯錯誤
* 電源供應器故障
* 卸下電源冷卻模組 (PCM)  

hello 以下表格說明 hello 各種警示狀態。  

### <a name="alarm-states"></a>警報器狀態
| 警報器狀態 | 動作 | 已按靜音按鈕時的動作 |
| --- | --- | --- |
| S0 |標準模式：靜音 |嗶兩聲 |
| S1 |錯誤模式：每 2 秒嗶 1 聲 |轉換 tooS2 或 S3 （請參閱備註） |
| S2 |提醒模式：間歇嗶聲 |None |
| S3 |靜音模式：靜音 |None |
| S4 |重大錯誤模式：連續警示 |無法使用：未啟用靜音 |

> [!NOTE]
> * 在警示狀態 S1 中，如果您不要按下靜音 2 分鐘的時間內 hello 狀態會自動轉換 tooS2 或 S3。  
> * 警示狀態 S1 tooS4 hello 錯誤狀況清除之後，傳回 tooS0。  
> * 任何其他狀態都能進入重大錯誤狀態 S4。  


您可以按下 hello 靜音按鈕 hello ops 面板上靜音 hello 可發出聲音的警示。 將自動靜音兩分鐘後如果未以手動方式操作 hello 靜音開關。 當 hello 警示靜音時，它會繼續與問題仍然存在的短的間歇嗶聲 tooindicate toosound。 hello 警示將靜音時清除了所有 hello 問題。

hello 以下表格說明 hello 各種警示條件。

### <a name="alarm-conditions"></a>警示狀況
| 狀態 | 嚴重性 | 警示 | 操作面板 LED |
| --- | --- | --- | --- |
| PCM 警示 – 失去單一 PCM 提供的 DC 電源 |錯誤 – 未失去備援 |S1 |模組錯誤 |
| PCM 警示 – 失去單一 PCM 提供的 DC 電源 |錯誤 – 失去備援 |S1 |模組錯誤 |
| PCM 風扇故障 |錯誤 – 失去備援 |S1 |模組錯誤 |
| SBB 模組偵測到 PCM 錯誤 |錯誤 |S1 |模組錯誤 |
| 已卸下 PCM |組態錯誤 |None |模組錯誤 |
| 機箱組態錯誤 |錯誤 – 重大 |S1 |模組錯誤 |
| 警告低溫警示 |警告 |S1 |模組錯誤 |
| 警告高溫警示 |警告 |S1 |模組錯誤 |
| 溫度過高警示 |錯誤 – 重大 |S1 |模組錯誤 |
| I2C 匯流排故障 |錯誤 – 失去備援 |S1 |模組錯誤 |
| 操作面板通訊錯誤 (I2C) |錯誤 – 重大 |S1 |模組錯誤 |
| 控制器錯誤 |錯誤 – 重大 |S1 |模組錯誤 |
| SBB 介面模組錯誤 |錯誤 – 重大 |S1 |模組錯誤 |
| SBB 介面模組錯誤 – 沒有運作中的模組 |錯誤 – 重大 |S4 |模組錯誤 |
| 已卸下 SBB 介面模組 |警告 |None |模組錯誤 |
| 磁碟機電源控制故障 |警告 – 未失去磁碟機電源 |S1 |模組錯誤 |
| 磁碟機電源控制故障 |錯誤 – 重大；失去磁碟機電源 |S1 |模組錯誤 |
| 已卸下磁碟機 |警告 |None |模組錯誤 |
| 沒有足夠的可用電源 |警告 |None |模組錯誤 |

## <a name="next-steps"></a>後續步驟
深入了解 [StorSimple 硬體元件與狀態](storsimple-8000-monitor-hardware-status.md)。

[1]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE01.png
[2]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE02.png
[3]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE03.png
[4]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE04.png
[5]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE05.png
[6]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE06.png


