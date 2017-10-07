---
title: "aaaStorSimple 技術規格 |Microsoft 文件"
description: "描述 hello 技術規格和法規標準 hello StorSimple 硬體元件的相容性資訊。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 17ebf6b3-0872-4332-ac6e-074cc20a2b8e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: bb73661105dee7f6020a91f8c4f5abd6583023ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="technical-specifications-and-compliance-for-hello-storsimple-device"></a>技術規格和相容性的 hello StorSimple 裝置
## <a name="overview"></a>概觀
Microsoft Azure StorSimple 裝置的 hello 硬體元件遵守 toohello 技術規格和法規標準這篇文章中所述。 hello 技術規格說明 hello 電源和冷卻的模組 (Pcm)、 磁碟機儲存容量和機箱。 hello 相容性資訊涵蓋國際標準、 安全和排放量，及連接纜線的這類事件。

## <a name="power-and-cooling-module-specifications"></a>電源和冷卻模組規格
hello StorSimple 裝置有兩個 100-240V 雙風扇、 SBB 相容的電源和冷卻模組 (Pcm)。 這提供了備援電源設定。 如果 PCM 故障，hello 裝置會繼續 toooperate 通常在其他 PCM 直到 hello 容錯模組已取代的 hello。  

hello EBOD 機箱使用 580 W PCM，與主要機箱則使用 764 W PCM。 hello 以下表格清單 hello 技術規格與 hello Pcm 相關聯。

| 規格 | 580 W PCM (EBOD) | 764 W PCM (主要) |
| --- | --- | --- |
| 最大輸出電力 |580 W |764 |
| 頻率 |50/60 Hz |50/60 Hz |
| 選取電壓範圍 |自動設定範圍：90 - 264 V AC、47/63 Hz |自動設定範圍：90 - 264 V AC、47/63 Hz |
| 最大瞬間電流 |20 A |20 A |
| 功率因素校正 |> 95% 額定輸入電壓 |> 95% 額定輸入電壓 |
| 諧波 |符合 EN61000-3-2 |符合 EN61000-3-2 |
| 輸出 |5V 待機電壓 @ 2.0 A |5V 待機電壓 @ 2.7 A |
| +5V @ 42 A |+5V @ 40 A | |
| +12V @ 38 A |+12V @ 38 A | |
| 隨插即用 |是 |是 |
| 開關和 LED |AC ON/OFF 開關和四個狀態指示器 LED |AC ON/OFF 開關和六個狀態指示器 LED |
| 機箱冷卻 |具有變動風扇速度控制的軸流散熱風扇 |具有變動風扇速度控制的軸流散熱風扇 |

## <a name="power-consumption-statistics"></a>耗電量統計資料
hello 下表列出 hello 典型的功率耗用量資料 （實際值可能會不同 hello 發行） hello 的 StorSimple 裝置的各種模型。 

| 條件 | 240 V AC | 240 V AC | 240 V AC | 110 V AC | 110 V AC | 110 V AC |
| --- | --- | --- | --- | --- | --- | --- |
|  風扇慢速，磁碟機閒置 |1.45 A |0.31 kW |1057.76 BTU/時 |3.19 A |0.34 kW |1160.13 BTU/時 |
|  風扇慢速，磁碟機存取中 |1.54 A |0.33 kW |1126.01 BTU/時 |3.27 A |0.36 kW |1228.37 BTU/時 |
|  風扇快速，磁碟機閒置，兩個 PSU 已運轉 |2.14 A |0.49 kW |1671.95 BTU/時 |4.99 A |0.54 kW |1842.56 BTU/時 |
|  風扇快速，磁碟機閒置，一個 PSU 已運轉、一個 PSU 閒置 |2.05 A |0.48 kW |1637.83 BTU/時 |4.58 A |0.50 kW |1706.07 BTU/時 |
|  風扇快速，磁碟機存取中，兩個 PSU 已運轉 |2.26 A |0.51 kW |1740.19 BTU/時 |4.95 A |0.54 kW |1842.56 BTU/時 |
|  風扇快速，磁碟機存取中，一個 PSU 已運轉、一個 PSU 閒置 |2.14 A |0.49 kW |1671.95 BTU/時 |4.81 A |0.53 kW |1808.44 BTU/時 |

## <a name="disk-drive-specifications"></a>磁碟機規格
您的 StorSimple 裝置支援 too12 3.5 吋規格的序列連接 SCSI (SAS) 磁碟機上。 hello 實際的磁碟機可以是固態磁碟機 (Ssd) 或硬碟機 (Hdd)，視 hello 產品組態而定。 hello 12 磁碟機槽都位於 hello 機箱 3 x 4 設定。 hello EBOD 機箱允許額外的存放裝置的其他的 12 個磁碟機。 這些磁碟機一律為 HDD。  

## <a name="storage-specifications"></a>儲存體規格
hello StorSimple 裝置會出現混合的硬碟機，這兩個 hello 8100 和 8600 固態磁碟機。 hello 總可用容量 hello 8100 和 8600 大約 15 TB 分別為和 38 TB。 下表中的 hello 記載 SSD 及 HDD、 hello StorSimple 解決方案容量 hello 內容中的雲端容量的 hello 詳細資料。

| 裝置型號/容量 | 8100 | 8600 |
| --- | --- | --- |
| 硬碟 (HDD) 數 |8 |19 |
| 固態硬碟 (SSD) 數 |4 |5 |
| 單一 HDD 容量 |4 TB |4 TB |
| 單一 SSD 容量 |400 GB |800 GB |
| 備用容量 |4 TB |4 TB |
| 可用的 HDD 容量 |14 TB |36 TB |
| 可用的 SSD 容量 |800 GB |2 TB |
| 可用容量總計* |~ 15 TB |~ 38 TB |
| 解決方案的最大容量 (含雲端) |200 TB |500 TB |

<sup>* </sup>- *hello 總計的可用容量包括 hello 容量可供資料、 中繼資料，以及緩衝區。*

## <a name="enclosure-dimensions-and-weight-specifications"></a>機箱尺寸和重量規格
下列表格 清單中的 hello hello 各種不同的機箱規格的尺寸和重量。  

### <a name="enclosure-dimensions"></a>機箱尺寸
hello 下表列出以毫米和英吋的 hello 機箱的 hello 維度。

| 機箱 | 公釐 | 英吋 |
| --- | --- | --- |
| 高度 |87.9 |3.46 |
| 法蘭座的寬度 |483 |19.02 |
| 機身的寬度 |443 |17.44 |
| 從法蘭座 tooextremity 機箱主體的深度 |577 |22.72 |
| 從作業深度面板 toofurthest 機箱末端的 |630.5 |24.82 |
| 從裝載墊圈 toofurthest 機箱末端的深度 |603 |23.74 |

### <a name="enclosure-weight"></a>機箱重量
根據 hello 組態，完全載入的主要機箱重量從 21 too33 公斤，需要兩個人員 toohandle 它。 

| 機箱 | Weight |
| --- | --- |
| 最大重量 （視 hello 組態） |30 kg - 33 kg |
| 空的 (未裝入磁碟機) |21 - 23 kg |

## <a name="enclosure-environment-specifications"></a>機箱環境規格
此區段會列出 hello 規格相關的 toohello 機箱環境。 這個類別所包含 hello 溫度、 溼度、 海拔高度、 震盪、 振動、 方向、 安全和電磁相容性 (EMC)。  

### <a name="temperature-and-humidity"></a>溫度和溼度
| 機箱 | 周圍溫度範圍 | 周圍相對溼度 | 最大濕球 |
| --- | --- | --- | --- |
| 運作 |5°C - 35°C(41°F - 95°F) |20% - 80% 無凝結- |28°C (82°F) |
| 無法運作 |-40°C - 70°C(40°F - 158°F) |5% - 100% 無凝結 |29°C (84°F) |

### <a name="airflow-altitude-shock-vibration-orientation-safety-and-emc"></a>氣流、海拔高度、震盪、振動、方向、安全和 EMC
| 機箱 | 運作規格 |
| --- | --- |
| 氣流 |系統氣流是前端 toorear。 系統必須以低壓、尾段排氣安裝操作。 機架門和障礙物所產生的背壓不得超出 5 帕斯卡 (0.5 mm 水位標尺)。 |
| 可運作的海拔高度 |-30 公尺 too3045 公尺 (-100 英呎 too10，000 英呎) 的最大作業溫度取消由 7000 英呎以上為 5 ° C 分級。 |
| 無法運作的海拔高度 |-305 公尺 too12，192 公尺 (-1000 英呎 too40，000 英呎) |
| 可運作的震盪 |5g 10 ms ½ sine |
| 無法運作的震盪 |30g 10 ms ½ sine |
| 可運作的振動 |0.21g RMS 5-500 Hz 隨機 |
| 無法運作的振動 |1.04g RMS 2-200 Hz 隨機 |
| 振動 (重新放置) |3g 2-200 Hz sine |
| 定位和掛接 |19" 機架掛接 (2 個 EIA 單位) |
| 機架滑軌 |toofit 與 IEC 297 相容的最小 700 mm （31.50 英吋） 深度機架 |
| 安全與核可 |CE 和 UL EN 61000-3、IEC 61000-3、UL 61000-3 |
| EMC |EN55022 (CISPR - A)，FCC A |

## <a name="international-standards-compliance"></a>國際標準相容性
Microsoft Azure StorSimple 裝置符合下列國際標準的 hello:  

* CE - EN 60950 - 1  
* CB 報告 tooIEC 60950-1  
* UL 和 cUL tooUL 60950-1  

## <a name="safety-compliance"></a>安全法規遵循
Microsoft Azure StorSimple 裝置符合下列安全分級 hello:  

* 系統產品類型核可：UL、cUL、CE  
* 安全法規遵循：UL 60950、IEC 60950、EN 60950  

## <a name="emc-compliance"></a>EMC 法規遵循
Microsoft Azure StorSimple 裝置符合下列 EMC 評等的 hello。  

### <a name="emissions"></a>放射性規格
hello 裝置符合傳導和輻射放射性層級與 EMC 相容的。  

* 傳導放射性限制層級：CFR 47 Part 15B Class A EN55022 Class A CISPR Class A  
* 輻射放射性限制層級：CFR 47 Part 15B Class A EN55022 Class A CISPR Class A   

### <a name="harmonics-and-flicker"></a>諧波和變動
hello 裝置符合 EN61000-3-2/3。  

### <a name="immunity-limit-levels"></a>免疫限制層級
hello 裝置符合 en55024。  

## <a name="ac-power-cord-compliance"></a>AC 電源線相容性
hello 插頭和完整電源線組件必須符合 hello 標準適合 hello 國家/地區正在使用中的 hello 裝置，而且必須具有該國家/地區中可接受的安全核淮 hello。 hello 以下表格清單 hello 美國和歐洲的標準。  

### <a name="ac-power-cords---usa-must-be-nrtl-listed"></a>AC 電源線 - 美國 (必須由 NRTL 列名)
| 元件 | 規格 |
| --- | --- |
| 電源線類型 |SV 或 SVT、最少 18 AWG、3 導體、最大長度為 2.0 公尺 |
| 插頭 |NEMA 5-15P 接地式插塞插頭，額定電壓 120 V、10 A 或 IEC 320 C14、250 V、10 A |
| 插座 |IEC 320 C-13、250 V、10 A |

### <a name="ac-power-cords---europe"></a>AC 電源線 - 歐洲
| 元件 | 規格 |
| --- | --- |
| 電源線類型 |諧波，H05-VVF-3G1.0 |
| 插座 |IEC 320 C-13、250 V、10 A |

## <a name="supported-network-cables"></a>支援的網路纜線
Hello 10 GbE 網路介面、 DATA 2 和 DATA 3，請參閱 toohello[清單支援的網路纜線和模組](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)。

## <a name="next-steps"></a>後續步驟
現在您已經準備就緒 toodeploy StorSimple 裝置在您的資料中心。 如需詳細資訊，請參閱 [部署您的內部部署裝置](storsimple-deployment-walkthrough-u2.md)。  

