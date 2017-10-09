---
title: "aaaReplace StorSimple 裝置控制站 |Microsoft 文件"
description: "說明如何 tooremove 並取代您的 StorSimple 裝置上的一個或兩個控制器模組。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e25b52b7-60f5-47f3-bffc-6c157d57ab5d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/03/2017
ms.author: alkohli
ms.openlocfilehash: ebf5c5830120857f69909113e3a111f4dda30e57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-controller-module-on-your-storsimple-device"></a>更換 StorSimple 裝置上的控制器模組
## <a name="overview"></a>概觀
本教學課程說明如何 tooremove 並取代在 StorSimple 裝置中的一個或兩個控制器模組。 它也會討論 hello 基礎邏輯 hello 單一和雙重控制器更換案例。

> [!NOTE]
> Tooperforming 控制器更換之前，我們建議您一律更新您控制器韌體 toohello 最新版本。
> 
> tooprevent 損壞 tooyour StorSimple 裝置，請勿退出 hello 控制站，直到 hello Led 顯示為 hello 下列其中一種：
> 
> * 所有燈都已關閉。
> * LED 3、![綠色勾號圖示](./media/storsimple-controller-replacement/HCS_GreenCheckIcon.png)和![紅色叉號圖示](./media/storsimple-controller-replacement/HCS_RedCrossIcon.png)是閃爍，而 LED 0 和 LED 7 是**開啟**。
> 
> 

hello 下表顯示支援的 hello 控制器更換案例。

| 案例 | 更換案例 | 適用程序 |
|:--- |:--- |:--- |
| 1 |一個控制器處於失敗狀態，hello 另一個控制器狀況良好，作用中。 |[單一控制器更換](#replace-a-single-controller)，用來描述 hello[背後單一控制器更換邏輯](#single-controller-replacement-logic)，以及 hello[更換步驟](#single-controller-replacement-steps)。 |
| 2 |兩個 hello 控制器已失敗且需要更換。 hello 底座、 磁碟和磁碟機箱均狀況良好。 |[更換雙重控制器時](#replace-both-controllers)，用來描述 hello[背後雙重控制器更換邏輯](#dual-controller-replacement-logic)，以及 hello[更換步驟](#dual-controller-replacement-steps)。 |
| 3 |從控制器 hello 相同的裝置，或從不同裝置互換。 hello 底座、 磁碟和磁碟機箱均狀況良好。 |插槽不符警示訊息將出現。 |
| 4 |一個控制器遺漏，hello 其他控制器失敗。 |[更換雙重控制器時](#replace-both-controllers)，用來描述 hello[背後雙重控制器更換邏輯](#dual-controller-replacement-logic)，以及 hello[更換步驟](#dual-controller-replacement-steps)。 |
| 5 |一個或兩個控制器故障。 您無法存取 hello 裝置透過 hello 序列主控台或 Windows PowerShell 遠端功能。 |[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md) 。 |
| 6 |hello 控制器有不同的組建版本，這可能是因為：<ul><li>控制器有不同的軟體版本。</li><li>控制器有不同的韌體版本。</li></ul> |如果 hello 控制器軟體版本不同，hello 更換邏輯會偵測，並更新 hello hello 替換控制器上的軟體版本。<br><br>如果 hello 控制器韌體版本不同，hello 舊的韌體版本是**不**自動升級，警示訊息會出現在 hello Azure 傳統入口網站。 您應該掃描更新，並安裝 hello 韌體更新。</br></br>如果 hello 控制器韌體版本不同，hello 舊的韌體版本可以自動升級，hello 控制器更換邏輯會偵測，並 hello 韌體 hello 控制器啟動之後，將會自動更新。 |

如果失敗，您會需要 tooremove 控制器模組。 一或兩個 hello 控制器模組可能會失敗，從而會導致更換單一控制器或更換雙重控制器時。 替代程序及 hello 背後的邏輯，請參閱下列 hello:

* [更換單一控制器](#replace-a-single-controller)
* [更換兩個控制器](#replace-both-controllers)
* [取下控制器](#remove-a-controller)
* [插入控制器](#insert-a-controller)
* [識別您的裝置上的 hello 主動控制站](#identify-the-active-controller-on-your-device)

> [!IMPORTANT]
> 移除或取代控制站，請檢閱中的 hello 安全性資訊之前[StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。
> 
> 

## <a name="replace-a-single-controller"></a>更換單一控制器
當 hello Microsoft Azure StorSimple 裝置上的 hello 兩個控制器之一發生故障無法正常運作，或遺失時，您會需要 tooreplace 單一控制器。 

### <a name="single-controller-replacement-logic"></a>單一控制器更換邏輯
單一控制器更換時，您應該先移除 hello 故障的控制器。 （hello hello 裝置中其餘的控制器是作用中控制器的 hello）。當您插入 hello 替換控制器時，hello 執行下列動作：

1. hello 替換控制器會立即開始與 hello StorSimple 裝置通訊。
2. Hello 虛擬硬碟 (VHD) 的 hello 作用中控制器的快照集複製 hello 替換控制器上。
3. hello 快照經過修改，以便從此 VHD 啟動 hello 替換控制器，當它將其視為待命控制器。
4. 完成 hello 修改後，hello 替換控制器將會開始為 hello 待命控制器。
5. 當兩個 hello 控制器正在執行時，hello 叢集就會上線。

### <a name="single-controller-replacement-steps"></a>單一控制器更換步驟
完成下列步驟，如果其中一個 Microsoft Azure StorSimple 裝置中的 hello 控制站失敗 hello。 （hello 另一個控制器必須是有效且在執行。 如果兩個控制器故障或運作失常，請移至太[雙重控制器更換步驟](#dual-controller-replacement-steps)。)

> [!NOTE]
> 它可以使用 hello 控制器 toorestart 30-45 分鐘，並從 hello 單一控制器更換程序中完全復原。 hello 整個程序，包括接上纜線 hello hello 總時間是大約 2 小時。
> 
> 

#### <a name="tooremove-a-single-failed-controller-module"></a>tooremove 單一故障的控制器模組
1. 在 hello Azure 傳統入口網站，移 toohello StorSimple Manager 服務中，按一下 hello**裝置**索引標籤，然後再按一下您想 toomonitor hello 裝置 hello 名稱。
2. 跳過**維護 > 硬體狀態**。 控制器 0 或控制器 1 的 hello 狀態應為紅色，表示故障。
   
   > [!NOTE]
   > hello 單一控制器更換中故障的控制器一律是待命控制器。
   > 
   > 
3. 使用圖 1 和 hello 下列資料表 toolocate hello 故障的控制器模組。  
   
    ![裝置主要機箱模組的後擋板](./media/storsimple-controller-replacement/IC740994.png)
   
    **圖 1** StorSimple 裝置的背面
   
   | 標籤 | 說明 |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |控制器 0 |
   | 4 |控制器 1 |
4. 在 hello 故障的控制器，移除所有 hello 連接網路纜線從 hello 資料連接埠。 如果您使用 8600 的模型，也會移除的 hello SAS 纜線連接 hello 控制器 toohello EBOD 控制器。
5. 中的 hello 步驟[移除控制器](#remove-a-controller)tooremove hello 無法控制站。 
6. 安裝在相同位置中的 hello 故障的控制器的 hello hello 原廠更換品已移除。 這會觸發 hello 單一控制器更換邏輯。 如需詳細資訊，請參閱 [單一控制器更換邏輯](#single-controller-replacement-logic)。
7. 當 hello 單一控制器更換邏輯進行 hello 背景時時，請重新連接 hello 纜線。 需要小心 tooconnect hello 的纜線完全 hello hello 更換前連接它們的方式相同。
8. Hello 控制器重新啟動之後，請檢查 hello**控制器狀態**和 hello**叢集狀態**在 hello Azure 傳統入口網站 tooverify hello 控制站，是回復 tooa 狀況良好狀態，而處於待命模式.

> [!NOTE]
> 如果您要監視 hello 裝置透過 hello 序列主控台，您可能會在 hello 控制器從 hello 更換程序中復原時看到多次重新啟動。 當 hello 序列主控台功能表呈現時，您便知道 hello 取代已完成。 如果 hello 功能表啟動 hello 控制器更換的 2 小時內未出現，請[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。
>
> 從更新 4 的開始，您也可以使用 hello cmdlet `Get-HCSControllerReplacementStatus` hello hello 裝置 toomonitor hello 狀態 hello 控制器更換程序的 Windows PowerShell 介面中。
> 

## <a name="replace-both-controllers"></a>更換兩個控制器
當兩個控制器 hello Microsoft Azure StorSimple 裝置上的失敗、 運作失常，或遺漏時，您需要 tooreplace 兩個控制器。 

### <a name="dual-controller-replacement-logic"></a>雙重控制器更換
在雙重控制器更換中，先移除兩個故障的控制器，再插入更換控制器。 當插入 hello 兩個替換控制器時，hello 執行下列動作：

1. 插槽 0 中的 hello 替換控制器會檢查 hello 下列：
   
   1. 是否使用目前版本的 hello 韌體及軟體？
   2. 它是 hello 叢集的一部分嗎？
   3. 是 hello 同儕節點控制器執行並已叢集處理？
      
      如果以上條件都成立，hello 控制器會尋找 hello 最新每日備份 (位於 hello **nonDOMstorage**磁碟機 S 上)。 hello 控制站複製 hello 備份 hello hello VHD 的最新快照集。
2. 插槽 0 中的 hello 控制器會使用 hello 快照 tooimage 本身。
3. 同時，插槽 1 中的 hello 控制器等待控制器 0 toocomplete hello 製作映像開始。
4. 控制器 0 啟動之後，控制器 1 會偵測控制器 0 時，所建立的觸發程序 hello 單一控制器更換邏輯 hello 叢集。 如需詳細資訊，請參閱 [單一控制器更換邏輯](#single-controller-replacement-logic)。
5. 之後，將會執行兩個控制器，而且 hello 叢集會上線。

> [!IMPORTANT]
> 更換雙重控制器時，下列 hello StorSimple 裝置設定之後，很重要，您會製作手動備份 hello 裝置。 直到過了 24 小時之後，才會觸發每日裝置組態備份。 使用[Microsoft 支援服務](storsimple-contact-microsoft-support.md)toomake 手動備份您的裝置。
> 
> 

### <a name="dual-controller-replacement-steps"></a>雙重控制器更換步驟
這兩個 Microsoft Azure StorSimple 裝置中的 hello 控制站失敗時，需要這個工作流程。 這種情形的資料中心所在 hello 冷卻系統停止運作，如此一來，兩個 hello 控制器失敗的時間在短時間內。 取決於是否 hello StorSimple 裝置已關閉或開啟後，無論您使用 8600，或 8100 機型，一組不同的步驟。

> [!IMPORTANT]
> 它可以 hello 控制器 toorestart 45 分鐘內 too1 小時，並從雙重控制器更換程序中完全復原。 hello 整個程序，包括接上纜線 hello hello 總時間是大約 2.5 小時。
> 
> 

#### <a name="tooreplace-both-controller-modules"></a>tooreplace 兩個控制器模組
1. 如果 hello 裝置已關閉，請略過此步驟，然後繼續 toohello 下一個步驟。 如果開啟 hello 裝置時，關閉 hello 裝置。
   
   1. 如果您使用 8600 的模型，請先關閉主要機箱 hello，，，然後將關閉 hello EBOD 機箱。
   2. 請等到 hello 裝置完全關閉。 在 hello hello 裝置背面的所有 hello Led 都將關閉。
2. 移除所有 hello 網路纜線連接的 toohello 資料的連接埠。 如果您使用 8600 的模型，也會移除的 hello SAS 纜線連接 hello 主要機箱 toohello EBOD 機箱。
3. Hello StorSimple 裝置中移除兩個控制器。 如需詳細資訊，請參閱[取下控制器](#remove-a-controller)。
4. 首先，插入控制器 0 的 hello 原廠更換品，然後再插入控制器 1。 如需詳細資訊，請參閱[插入控制器](#insert-a-controller)。 這會觸發 hello 雙重控制器更換邏輯。 如需詳細資訊，請參閱[雙重控制器更換邏輯](#dual-controller-replacement-logic)。
5. 當 hello 控制器更換邏輯進行 hello 背景時時，請重新連接 hello 纜線。 需要小心 tooconnect hello 的纜線完全 hello hello 更換前連接它們的方式相同。 請參閱 hello 詳細 hello 纜線的模型指示您裝置區段[安裝 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md)或[安裝 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)。
6. 開啟 hello StorSimple 裝置。 如果您使用的是 8600 機型：
   
   1. 確定首先開啟 EBOD 機箱的 hello。
   2. 請等到執行 hello EBOD 機箱。
   3. 開啟 hello 主要機箱。
   4. Hello 第一個控制器重新啟動，並處於狀況良好狀態之後，將會執行 hello 系統。
      
      > [!NOTE]
      > 如果您要監視 hello 裝置透過 hello 序列主控台，您可能會在 hello 控制器從 hello 更換程序中復原時看到多次重新啟動。 Hello 序列主控台功能表中出現時，您便知道 hello 取代已完成。 如果 hello 功能表啟動 hello 控制器更換的 2.5 小時內沒有出現，請[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。
      > 
      > 

## <a name="remove-a-controller"></a>取下控制器
使用您的 StorSimple 裝置中的下列程序 tooremove 發生故障的控制器模組的 hello。

> [!NOTE]
> 下列圖例 hello 適用於控制器 0。 若為控制器 1，這些將相反。
> 
> 

#### <a name="tooremove-a-controller-module"></a>tooremove 控制器模組
1. 掌握用姆指與食指 hello 模組閂鎖。
2. 輕輕擠壓您姆指與食指同時 toorelease hello 控制器閂鎖。
   
    ![鬆開控制器閂鎖](./media/storsimple-controller-replacement/IC741047.png)
   
    **圖 2** 鬆開控制器閂鎖
3. Hello 閂鎖作為超出 hello 底座的控制代碼 tooslide hello 控制站。
   
    ![將控制器滑出底座](./media/storsimple-controller-replacement/IC741048.png)
   
    **圖 3** hello 控制器滑出底座 hello

## <a name="insert-a-controller"></a>插入控制器
使用下列程序 tooinstall 廠的控制器模組故障的模組移除您的 StorSimple 裝置之後 hello。

#### <a name="tooinstall-a-controller-module"></a>tooinstall 控制器模組
1. 如果有任何損毀 toohello 介面連接器，請檢查 toosee。 如果任何 hello 連接器針腳插腳損壞或彎曲，請勿安裝 hello 模組。
2. Hello 控制器模組滑入底座 hello 中 hello 閂鎖完全鬆開時。 
   
    ![將控制器滑入底座](./media/storsimple-controller-replacement/IC741053.png)
   
    **圖 4**將控制器滑入底座 hello
3. Hello 插入控制器模組後，開始關閉至 hello 底座 hello 閂鎖，同時繼續 toopush hello 控制器模組。 hello 閂鎖會連絡 tooguide hello 控制器位置。
   
    ![關閉控制器閂鎖](./media/storsimple-controller-replacement/IC741054.png)
   
    **圖 5**關閉 hello 控制器閂鎖
4. 您已大功告成 hello 閂鎖卡入定位時。 hello**確定**LED 現在應該亮起。  
   
   > [!NOTE]
   > 就可以在 hello 控制器和 LED tooactivate hello too5 分鐘。
   > 
   > 
5. hello 取代為成功，請在的 tooverify 太 hello Azure 傳統入口網站中，移至**裝置** > **維護** > **硬體狀態**，並確定控制器 0 及控制器 1 的狀況良好 （狀態為綠色）。

## <a name="identify-hello-active-controller-on-your-device"></a>識別您的裝置上的 hello 主動控制站
有許多情況下，第一次裝置註冊或控制站取代，例如，必須在 StorSimple 裝置 toolocate hello 作用中的控制器。 hello 作用中控制器會處理所有 hello 磁碟韌體和網路作業。 您可以使用任何下列方法 tooidentify hello 作用中控制器的 hello:

* [使用 hello Azure 傳統入口網站 tooidentify hello 作用中控制器](#use-the-azure-classic-portal-to-identify-the-active-controller)
* [使用 Windows PowerShell for StorSimple tooidentify hello 作用中控制器](#use-windows-powershell-for-storsimple-to-identify-the-active-controller)
* [檢查 hello 實體裝置 tooidentify hello 作用中控制器](#check-the-physical-device-to-identify-the-active-controller)

接著說明上述各程序。

### <a name="use-hello-azure-classic-portal-tooidentify-hello-active-controller"></a>使用 hello Azure 傳統入口網站 tooidentify hello 作用中控制器
在 hello Azure 傳統入口網站中瀏覽過**裝置** > **維護**，並捲動 toohello**控制器**> 一節。 在這裡您可以確認哪一個控制站作用中。

![識別 Azure 傳統入口網站中的作用中控制器](./media/storsimple-controller-replacement/IC752072.png)

**圖 6** Azure 傳統入口網站顯示 hello 作用中控制器

### <a name="use-windows-powershell-for-storsimple-tooidentify-hello-active-controller"></a>使用 Windows PowerShell for StorSimple tooidentify hello 作用中控制器
當您透過 hello 序列主控台存取您的裝置時，會顯示橫幅訊息。 hello 橫幅訊息包含基本裝置資訊，例如 hello 模型、 名稱、 已安裝的軟體版本，以及您要存取的 hello 控制站的狀態。 hello 下列影像顯示橫幅訊息範例：

![序列橫幅訊息](./media/storsimple-controller-replacement/IC741098.png)

**圖 7** 橫幅訊息將控制器 0 顯示為作用中

無論您是 hello 控制站，您可以使用 hello 橫幅訊息 toodetermine 連接 toois 主動或被動。

### <a name="check-hello-physical-device-tooidentify-hello-active-controller"></a>檢查 hello 實體裝置 tooidentify hello 作用中控制器
tooidentify hello 作用中控制器上您的裝置，找出 hello 藍色 LED hello DATA 5 連接埠上 hello 主要機箱背面的 hello 上方。

如果此 LED 閃爍不停，hello 控制器為作用中且 hello 另一個控制器處於待命模式。 使用下列圖表中的 hello 和表格作為輔助工具。

![包含資料連接埠的裝置主要機箱後擋板](./media/storsimple-controller-replacement/IC741055.png)

**圖 8** 具有資料連接埠和監視 LED 的主要機箱背面

| 標籤 | 說明 |
|:--- |:--- |
| 1-6 |DATA 0 – 5 個網路連接埠 |
| 7 |藍色 LED |

## <a name="next-steps"></a>後續步驟
深入了解 [StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。

