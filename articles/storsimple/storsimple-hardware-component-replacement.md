---
title: "aaaStorSimple 硬體元件更換 |Microsoft 文件"
description: "描述如何 toosafely 取代 hello Pcm、 電池、 控制器模組、 EBOD 控制器、 磁碟機和 StorSimple 裝置的底座。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e8087ba7-0b66-4f59-8988-e53aad52ee21
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 472d9dc1c31b61550fe079cc9b9419510487db3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-hardware-component-on-your-storsimple-8000-series-device"></a>更換 StorSimple 8000 系列裝置上的硬體元件

## <a name="overview"></a>概觀
hello 硬體元件更換教學課程描述您 Microsoft Azure StorSimple 8000 系列裝置和 hello 步驟需要 tooremove hello 硬體元件，並將其取代。 這篇文章描述 hello 安全性圖示，提供的指標 toohello 詳細的教學課程中，並列出 hello 可取代的元件。

> [!IMPORTANT]
> 然後再嘗試 tooremove 或取代任何 StorSimple 元件，請確定您檢閱 hello[安全圖示慣例](#safety-icon-conventions)和其他[安全措施](storsimple-safety.md)。
> 
> 

### <a name="safety-icon-conventions"></a>安全性圖示慣例
hello 下表說明用於這些教學課程中的 hello 安全性圖示。 當您瀏覽 hello 步驟 tooremove 並取代裝置元件特別注意 toothese 安全性圖示。

| 圖示 | 文字 | 其他資訊 |
|:--- |:--- |:--- |
| ![警告圖示](./media/storsimple-hardware-component-replacement/Warning.png) |**危險！** |指出危險的情況，如果無法避免，將會導致死亡或嚴重傷害。 此一指示文字是有限的 toohello 最危險的狀況。 |
| ![警告圖示](./media/storsimple-hardware-component-replacement/Warning.png) |**警告！** |指出危險的情況，如果無法避免，可能會導致死亡或嚴重傷害。 |
| ![注意圖示](./media/storsimple-hardware-component-replacement/Caution.png) |**小心！** |指出危險的情況，如果無法避免，可能會導致次要或中度的傷害。 |
| ![注意事項圖示](./media/storsimple-hardware-component-replacement/NoticeIcon.png) |**注意事項：** |表示重要資訊，但與危險無關。 |
| ![電擊圖示](./media/storsimple-hardware-component-replacement/Electric.png) |**電擊危險** |表示高電壓。 |
| ![超重圖示](./media/storsimple-hardware-component-replacement/Weight.png) |**超重** | |
| ![沒有使用者可自行維修的零件圖示](./media/storsimple-hardware-component-replacement/NoUserServiceableParts.png) |**沒有使用者可自行維修的零件** |除非受過適當訓練，否則請勿觸碰。 |
| ![閱讀指示圖示](./media/storsimple-hardware-component-replacement/ReadInstructions.png) |**請先閱讀所有指示** | |
| ![傾倒危險圖示](./media/storsimple-hardware-component-replacement/TipHazard.png) |**傾倒危險** | |

### <a name="before-you-begin"></a>開始之前
熟悉您在本教學課程中使用的裝置和安全圖示 hello 安全性資訊。 跳過[安全地安裝及操作您的 StorSimple 裝置](storsimple-safety.md)如需完整資訊。 要確定 tooreview hello[安全措施](storsimple-safety.md#handling-precautions)之前處理您的 StorSimple 裝置。 

您嘗試 tooreplace 元件之前，請考慮下列資訊的 hello。

![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Electrical Shock Icon](./media/storsimple-hardware-component-replacement/Electric.png) **警告！** 

* 處理 StorSimple 裝置的模組和元件時，請使用靜電防護或防靜電墊，讓您自己適當地接地。
* 請勿觸及任何電路。 使用提供的 hello 控點和輔助線時處理可能有裸露電路系統的元件。

![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Notice Icon](./media/storsimple-hardware-component-replacement/NoticeIcon.png) **注意事項：**

當您取代的模組，**永遠不會留下空槽中 hello hello 機箱的背面**。 取得替換模組或空模組移除 hello 問題的零件之前。

## <a name="hardware-component-replacement-procedures"></a>硬體元件更換程序
您的 StorSimple 8000 系列裝置是由數個外掛模組中主要的 hello 和/或 EBOD 機箱所組成。 hello 8100 具有單一主要機箱，而 hello 8600 是雙重機箱裝置，具有主要機箱和 EBOD 機箱。

hello 下表中摘要說明您的裝置中的 hello 主要硬體元件。 按一下 hello 中的 hello 連結**更換程序**資料行 toogo toohello 相關教學課程。

| 元件 | # Present | 外掛程式模組？ | 更換程序 |
|:--- |:--- |:--- |:--- |
| 底座 |1 |否 |[取代您的 StorSimple 裝置上的 hello 底座](storsimple-chassis-replacement.md) |
| 主要控制器 |2 |是 |[更換 StorSimple 裝置上的控制器模組](storsimple-controller-replacement.md) |
| 764 瓦電源和冷卻模組 (PCM) |2 |是 |[更換 StorSimple 裝置上的電源和冷卻模組](storsimple-power-cooling-module-replacement.md) |
| 備用電池 |2 |是 |[取代您的 StorSimple 裝置上的 hello 備用電池模組](storsimple-battery-replacement.md) |
| 磁碟機 |12 |是 |[更換 StorSimple 裝置上的磁碟機](storsimple-disk-drive-replacement.md) |

**表 1** hello 主要機箱中的硬體元件

hello 主要機箱和 hello EBOD 機箱的 I/O 模組不同。 此外，Pcm hello 瓦數不同。 hello 主要機箱中的 hello Pcm 為 764 W，而在 hello EBOD 機箱是 580 W hello Pcm 中 hello 主要機箱也包含備用電池模組。

| 元件 | # Present | 外掛程式模組？ | 更換程序 |
|:--- |:--- |:--- |:--- |
| 底座 |1 |否 |[取代您的 StorSimple 裝置上的 hello 底座](storsimple-chassis-replacement.md) |
| EBOD 控制器 |2 |是 |[更換 StorSimple 裝置上的 EBOD 控制器](storsimple-ebod-controller-replacement.md) |
| 580 瓦電源和冷卻模組 (PCM) |2 |是 |[更換 StorSimple 裝置上的電源和冷卻模組](storsimple-power-cooling-module-replacement.md) |
| 磁碟機 |12 |是 |[更換 StorSimple 裝置上的磁碟機](storsimple-disk-drive-replacement.md) |

**表 2** hello EBOD 機箱中的硬體元件

hello 裝置上的 hello 外掛模組會在 hello 下列正面和背面圖中反白顯示。 如果需要更換的話您可以使用指定的 hello 這些圖表 toodetermine hello 位置各種外掛模組。 hello 正面圖顯示 hello 磁碟機，而 hello 背面圖 hello EBOD 機箱與主要機箱 hello 顯示 hello 外掛模組。

![具有磁碟機的裝置前擋板](./media/storsimple-hardware-component-replacement/IC741028.png)

**圖 1** hello 裝置的正面

| 標籤 | 說明 |
|:--- |:--- |
| 0 - 11 |磁碟機 (總共 12 部) |

Hello 主要機箱和 hello EBOD 機箱都有磁碟機拖架模組。 hello 底座容納 12 個 3.5"磁碟機以 3 x 4 格式排列。

![裝置主要機箱模組的後擋板](./media/storsimple-hardware-component-replacement/IC740994.png)

**圖 2** hello 主要機箱背面

| 標籤 | 說明 |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |控制器 0 |
| 4 |控制器 1 |

![裝置 EBOD 機箱外掛程式模組的後擋板](./media/storsimple-hardware-component-replacement/IC769599.png)

**圖 3** hello EBOD 機箱的背面

| 標籤 | 說明 |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |EBOD 控制器 0 |
| 4 |EBOD 控制器 1 |

## <a name="field-replaceable-units"></a>現場可更換裝置
hello 遵循埸可更換裝置 (Fru) 可供您的 StorSimple 裝置：

* 底座 （包括 hello 整合的操作面板）
* 764 W AC PCM
* 580 W AC PCM
* 具有磁碟機載具模組的硬碟機
* 控制器模組
* EBOD 控制器模組
* 備用電池模組
* 機架掛接滑軌套件

請[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)tooorder 其中任何更換裝置。

## <a name="next-steps"></a>後續步驟
檢閱所有[安全性資訊](storsimple-safety.md)嘗試 tooreplace StorSimple 硬體元件之前。

