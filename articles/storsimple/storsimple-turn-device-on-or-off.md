---
title: "aaaTurn StorSimple 8000 系列裝置開啟或關閉 |Microsoft 文件"
description: "說明如何在新的 StorSimple 裝置，tooturn 開啟的裝置已關閉或失去電源，並關閉執行中的裝置。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 8e9c6e6c-965c-4a81-81bd-e1c523a14c82
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 85434bde9377e330cd6ba4797fd5fd68bcee944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="turn-on-or-turn-off-your-storsimple-8000-series-device"></a>開啟或關閉 StorSimple 8000 系列裝置
## <a name="overview"></a>概觀
正常系統作業並不需要關閉 Microsoft Azure StorSimple 裝置。 不過，您可能需要新的裝置或裝置已關閉的 toobe tooturn。 一般而言，在您需要更換故障的硬體、實際移動單元，或將裝置報廢的情況下才需要關機。 本教學課程說明開啟和關閉您的 StorSimple 裝置在不同案例中的所需的 hello 程序。

## <a name="turn-on-a-new-device"></a>開啟新的裝置
hello 第一次開啟 hello StorSimple 裝置的步驟有所不同 hello 裝置是否 8100 或 8600 模型。 hello 8100 具有單一主要機箱，而 hello 8600 是雙重機箱裝置，具有主要機箱和 EBOD 機箱。 hello 這兩個模型的詳細的步驟涵蓋下列各節的 hello。

* [只有主要機箱的新裝置](#new-device-with-primary-enclosure-only)
* [具有 EBOD 機箱的新裝置](#new-device-with-ebod-enclosure)

### <a name="new-device-with-primary-enclosure-only"></a>只有主要機箱的新裝置
hello StorSimple 8100 模型是單一機箱裝置。 您的裝置包含備援電源和冷卻模組 (PCM)。 這兩個 Pcm 必須安裝並連接 toodifferent 電源來源 tooensure 高可用性。

執行您的裝置 hello 遵循步驟 toocable 電源。

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

> [!NOTE]
> 完成裝置設定和纜線連接指示，請移過[安裝 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md)。 請確定您確實依照 hello 指示進行。
> 
> 

### <a name="new-device-with-ebod-enclosure"></a>具有 EBOD 機箱的新裝置
hello StorSimple 8600 模型有主要機箱和 EBOD 機箱。 這需要 hello 單位 toobe 接上一起取得序列連接 SCSI (SAS) 連線和電源。

設定此裝置 hello 第一次，請執行 hello 步驟 SAS 佈線第一次，然後完成 hello 電源佈線的步驟。

[!INCLUDE [storsimple-sas-cable-8600](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

> [!NOTE]
> 完成裝置設定和纜線連接指示，請移過[安裝 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)。 請確定您確實依照 hello 指示進行。

## <a name="turn-on-a-device-after-shutdown"></a>在關機後開啟裝置
它已關閉後開啟 StorSimple 裝置 hello 步驟會有所不同 hello 裝置是否 8100 或 8600 模型項目。 hello 8100 具有單一主要機箱，而 hello 8600 是雙重機箱裝置，具有主要機箱和 EBOD 機箱。

* [只有主要機箱的裝置](#device-with-primary-enclosure-only)
* [具有 EBOD 機箱的裝置](#device-with-ebod-enclosure)

### <a name="device-with-primary-enclosure-only"></a>只有主要機箱的裝置
關閉後，使用下列程序 tooturn StorSimple 裝置沒有 EBOD 機箱與主要機箱上的 hello。

#### <a name="tooturn-on-a-device-with-a-primary-enclosure-only"></a>只有主要機箱的裝置上的 tooturn
1. 請確定，hello 電源開關這兩個電源和冷卻模組 (Pcm) 是在 hello OFF 位置。 如果 hello 參數不在 hello 關閉 」 位置，然後翻轉 toohello 關閉 」 位置，並等待 hello 燈號 toogo 關閉。
2. 開啟 hello 裝置 hello 電源開關 」 這兩個 Pcm toohello 開啟 」 位置上。 hello 裝置應開啟。
3. 核取 hello 遵循 hello 裝置的 tooverify 已完全開啟：
   
   1. 這兩個 PCM 模組上的 hello 正常 Led 」 皆為綠色。
   2. 兩個控制器上的 hello 狀態 led 皆為純綠色。
   3. hello 其中一個 hello 控制站上的藍色 LED 閃爍不停，這表示該 hello 控制器為作用中。
      
      如果有任何不符合上述的情況，則裝置的狀態不良。 請 [連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。

### <a name="device-with-ebod-enclosure"></a>具有 EBOD 機箱的裝置
關閉後，使用下列程序 tooturn StorSimple 裝置主要機箱與 EBOD 機箱上的 hello。 請確實遵循說明依序執行每個步驟。 失敗 toodo 因此可能會導致資料遺失。

#### <a name="tooturn-on-a-device-with-a-primary-and-an-ebod-enclosure"></a>tooturn 主要和 EBOD 機箱的裝置上
1. 請確定該 hello EBOD 機箱已連接的 toohello 主要機箱。 如需詳細資訊，請參閱 [安裝您的 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)。
2. 請確定該 hello 電源和冷卻模組 (Pcm) 上同時 hello EBOD 與主要機箱已 hello OFF 位置。 如果 hello 參數不在 hello 關閉 」 位置，然後翻轉 toohello 關閉 」 位置，並等待 hello 燈號 toogo 關閉。
3. 開啟 EBOD 機箱 hello 第一個翻轉 hello 電源開關都在這兩個 Pcm toohello 開啟 」 位置上。 hello PCM Led 應為綠色。 此裝置上的綠色 EBOD 控制器 LED 表示 hello EBOD 機箱已開啟。
4. 開啟主要機箱 hello 翻轉 hello 電源開關都在這兩個 Pcm toohello 開啟 」 位置上。 hello 整個系統現在應該亮起。
5. 請確認 hello SAS Led 為綠色，並確保該 hello 之間的連線 hello EBOD 機箱 hello 主要機箱是理想的狀況。

## <a name="turn-on-a-device-after-a-power-loss"></a>在電源中斷後開啟裝置
電源中斷會關閉 StorSimple 裝置。 hello 斷電情形 hello 電源供應器的其中一個或兩個電源供應器上。 hello 復原步驟會有所不同 hello 裝置是否 8100 或 8600 模型項目。 hello 8100 具有單一主要機箱，而 hello 8600 是雙重機箱裝置，具有主要機箱和 EBOD 機箱。 本節說明每個案例中的 hello 復原程序。

* [只有主要機箱的裝置](#8100)
* [具有 EBOD 機箱的裝置](#8600)

### <a name="device-with-primary-enclosure-only-a-name8100"></a>只有主要機箱的裝置 <a name="8100">
如果有一個電源供應器的電源遺失 tooone hello 系統可以繼續其正常作業。 不過，tooensure 高可用性的 hello 裝置，還原電源 toohello 電源供應器儘速。

如果沒有電源中斷或兩個電源供應器的電源中斷，hello 系統將會關閉以井然有序且受控制的方式。 還原 hello 電源時，將會自動開啟 hello 系統。

### <a name="device-with-ebod-enclosure-a-name8600"></a>具有 EBOD 機箱的裝置 <a name="8600">
#### <a name="power-loss-on-one-power-supply"></a>單一電源供應器電源中斷
如果有一個主要機箱 hello 或 hello EBOD 機箱上的電源供應器的電源遺失 tooone hello 系統可以繼續其正常作業。 不過，tooensure 高可用性的 hello 裝置，請還原電源 toohello 電源供應器儘速。

#### <a name="power-loss-on-both-power-supplies-on-primary-and-ebod-enclosures"></a>主要機箱和 EBOD 機箱的電源供應器同時電源中斷
如果沒有這兩個電源供應器都有電源中斷或電源中斷，hello EBOD 機箱將立即關閉，並以井然有序且受控制的方式將關閉 hello 主要機箱。 當電源恢復時，會自動啟動 hello 應用裝置。

如果以手動方式關閉 hello 電源，然後採取下列步驟 toorestore 電源 toohello 系統 hello。

1. 開啟 hello EBOD 機箱。
2. Hello EBOD 機箱上 」 之後，請開啟 hello 主要機箱。

### <a name="power-loss-on-both-power-supplies-on-ebod-enclosure"></a>EBOD 機箱上的兩個電源供應器同時電源中斷
當您設定您的纜線時，您必須確定 EBOD 絕不會是該 hello 連接單獨 tooa 個別 PDU。 如果在 hello 失敗的 hello EBOD 與主要機箱 hello 系統將復原相同的時間。

如果只有 EBOD 機箱 hello 失敗這兩個電源供應器，hello 系統將不會自動復原。 採用 hello 遵循步驟 tooturn hello 系統上，並將它還原 tooa 狀況良好的狀態：

1. 如果 hello 主要機箱已開啟、 關閉電源和冷卻模組 (Pcm)。
2. 請等候幾分鐘，讓 hello 系統 tooshut 向下。
3. 開啟 hello EBOD 機箱。
4. Hello EBOD 機箱上 」 之後，請開啟 hello 主要機箱。

## <a name="turn-on-a-device-after-hello-primary-and-ebod-enclosure-connection-is-lost"></a>後開啟裝置 hello 主要和 EBOD 機箱連線中斷時
如果遺失之間 hello 待命控制器與對應 EBOD 控制器 hello hello 連接，hello 裝置會繼續 toowork。 Hello hello 系統作用中控制器與對應 EBOD 控制器 hello 之間的連線遺失時，應該會發生容錯移轉，而 hello 裝置應該繼續 toowork 像平常一樣。

當會移除這兩個序列連接 SCSI (SAS) 纜線或切斷 EBOD 機箱 hello 與 hello 主要機箱之間的 hello 連線時，hello 裝置將會停止運作。 此時，執行下列步驟的 hello。

### <a name="tooturn-on-hello-device-after-connection-is-lost"></a>tooturn hello 裝置之後，而失去連接
1. 存取 hello hello 裝置背面。
2. 如果 hello hello EBOD 機箱與 hello 主要機箱之間的 SAS 纜線連接已損毀，hello EBOD 機箱上所有的 SAS lane Led 都會熄滅。
3. 在 hello EBOD 機箱與主要機箱 hello 關閉電源和冷卻模組 (Pcm)。
4. 請等到所有 hello 燈號上兩個 hello 機箱的背面的 hello 都關閉。
5. 重新插入 hello SAS 纜線，並確保沒有 hello EBOD 機箱與主要機箱 hello 之間良好的連接。
6. 開啟 EBOD 機箱 hello 第一次 」 這兩個 PCM 開關 toohello 開啟 」 位置。
7. 請確認 hello EBOD 機箱上檢查 hello 綠色 LED 為 ON。
8. 開啟 hello 主要機箱。
9. 請確認 hello 主要機箱上檢查 hello 控制器綠色 LED 為 「 上。
10. 請確認該 hello hello 主要機箱與 EBOD 機箱連線良好藉由檢查該 hello SAS lane Led （每個 EBOD 控制器的四個） 都上。

> [!IMPORTANT]
> 如果 hello SAS 纜線損壞或 hello hello EBOD 機箱與 hello 主要機箱之間的連線是狀況不佳，當您開啟 hello 系統時，它將會進入修復模式。 如果發生此情況，請 [連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md) 。


## <a name="turn-off-a-running-device"></a>關閉執行中的裝置
執行中的 StorSimple 裝置可能需要 toobe 如果它正在移動、 中斷服務，或有故障元件時，需要取代 toobe 關機。 hello 步驟會有所不同 hello StorSimple 裝置是否 8100 或 8600 模型項目。 hello 8100 具有單一主要機箱，而 hello 8600 是雙重機箱裝置，具有主要機箱和 EBOD 機箱。 本節詳述 hello 步驟 tooshut 關閉執行中的裝置。

* [具有主要機箱的裝置](#8100a)
* [具有 EBOD 機箱的裝置](#8600a)

### <a name="device-with-primary-enclosure-a-name8100a"></a>具有主要機箱的裝置 <a name="8100a">
tooshut hello 裝置以井然有序且受控制的方式，您可以進行透過 hello Azure 傳統入口網站或透過 hello Windows PowerShell for StorSimple。 

> [!IMPORTANT]
> 不會關閉執行中的裝置使用上 hello 裝置背面的 hello hello 電源按鈕。
> 
> 之前關閉 hello 裝置，請確定所有的 hello 裝置元件皆正常運作。 在 hello Azure 傳統入口網站中瀏覽過**裝置** > **維護** > **硬體狀態**，並確認所有 hello 狀態元件為綠色。 這只適用於狀態良好的系統。 如果 hello 系統關機 tooreplace 的故障元件時，您會看到故障 （紅色） 或降級 （黃色） 狀態 hello hello 中的個別元件**硬體狀態**。
> 
> 

您存取 hello Windows PowerShell for StorSimple 或 hello Azure 傳統入口網站之後，請依照中的 hello 步驟[關閉 StorSimple 裝置](storsimple-manage-device-controller.md#shut-down-a-storsimple-device)。 

### <a name="device-with-ebod-enclosure-a-name8600a"></a>具有 EBOD 機箱的裝置 <a name="8600a">
> [!IMPORTANT]
> 之前關閉主要機箱 hello 與 hello EBOD 機箱，請確定所有的 hello 裝置元件皆正常運作。 在 hello Azure 入口網站中瀏覽過**裝置** > **監視器** > **硬體健全狀況**，並確認所有 hello 元件都均狀況良好。


#### <a name="tooshut-down-a-running-device-with-ebod-enclosure"></a>tooshut 關閉具有 EBOD 機箱執行中的裝置
1. 請遵循所列的所有 hello 步驟[關閉 StorSimple 裝置](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device)hello 主要機箱。
2. 之後 hello 主要機箱已關閉，關閉 hello EBOD 開關關閉電源和冷卻模組 (PCM) 的參數。
3. hello EBOD 的 tooverify 已關閉、 已關閉的核取所有燈號上 hello hello EBOD 機箱的背面。

> [!NOTE]
> 會使用的 tooconnect hello EBOD 機箱 toohello 主要機箱的 hello SAS 纜線應該後才會移除之前 hello 系統關機。

## <a name="next-steps"></a>後續步驟
[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) 。

