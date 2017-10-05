---
title: "管理 StorSimple 裝置控制器 | Microsoft Docs"
description: "了解如何停止、重新啟動、關閉或重設您的 StorSimple 裝置控制器。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4ee989d0-956f-4c14-951e-fd4e490ea09d
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/11/2016
ms.author: alkohli
ms.openlocfilehash: 67dbb0c4066002256efbab6061157c641527e441
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>管理 StorSimple 裝置控制器
## <a name="overview"></a>Overview
本教學課程描述可在 StorSimple 裝置控制器上執行的不同作業。 StorSimple 裝置中的控制器在主動-被動組態中是備援 (對等) 控制器。 在指定的時間中，只能有一個控制器在主動模式，並處理所有磁碟和網路作業。 另一個控制器處於被動模式。 如果主動控制器發生故障，被動控制器便會自動變為主動。

本教學課程包含使用下列內容管理裝置控制器的逐步指示：

* StorSimple Manager 服務中 [維護] 頁面的 [控制器] 區段
* Windows PowerShell for StorSimple

我們建議您透過 StorSimple Manager 服務管理裝置控制器。 如果動作只能使用 Windows PowerShell for StorSimple 執行，本教學課程會記錄下來。

閱讀本教學課程之後，您將能夠：

* 重新啟動或關閉 StorSimple 裝置控制器
* 關閉 StorSimple 裝置
* 將 StorSimple 裝置重設為原廠預設值

## <a name="restart-or-shut-down-a-single-controller"></a>重新啟動或關閉單一控制器
一般系統作業並不需要重新啟動或關閉控制器。 只有在故障的裝置硬體元件需要更換時，才會常常使用單一裝置控制器的關閉作業。 只有在記憶體過度使用或控制器故障影響效能時，才會需要重新啟動控制器。 成功更換控制器之後，如果您想要啟用並測試更換的控制器，也可能需要重新啟動控制器。

假設被動控制器可用，重新啟動裝置並不會干擾連線的啟動器。 如果被動控制器不可用或已關閉，重新啟動主動控制器可能會導致服務中斷和停機。

> [!IMPORTANT]
> * **執行中的控制器應該永遠不會實際移除，因為這會導致失去備援並增加停機的風險。**
> * 下列程序只適用於 StorSimple 實體裝置。 如需有關如何啟動、停止和重新啟動虛擬裝置的資訊，請參閱[使用虛擬裝置](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device)。
> 
> 

您可以使用 StorSimple Manager 服務或 Windows PowerShell for StorSimple 的 Azure 傳統入口網站重新啟動或關閉單一裝置控制器。

若要從 Azure 傳統入口網站管理您的裝置控制器，請執行下列步驟。

#### <a name="to-restart-or-shut-down-a-controller-in-classic-portal"></a>若要在傳統入口網站中重新啟動或關閉控制器
1. 請瀏覽至 [裝置] > [維護]。
2. 移至 [硬體狀態] 並確認裝置上的兩個控制器狀態為 [狀況良好]。
   
    ![確認 StorSimple 裝置控制器的狀況良好](./media/storsimple-manage-device-controller/IC766017.png)
3. 在 [維護] 頁面的底部，按一下 [管理控制器]。
   
    ![管理 StorSimple 裝置控制器](./media/storsimple-manage-device-controller/IC766018.png)</br>
   
   > [!NOTE]
   > 如果您沒看到 [ **管理控制器**]，表示您需要安裝更新。 如需詳細資訊，請參閱 [更新您的 StorSimple 裝置](storsimple-update-device.md)。
   > 
   > 
4. 在 [ **變更控制器設定** ] 對話方塊中，執行下列動作：
   
   1. 從 [ **選取控制器** ] 下拉式清單中，選取您想要管理的控制器。 選項為控制器 0 和控制器 1。 這些控制器也可識別為主動或被動。
      
      > [!NOTE]
      > 如果控制器無法使用或已關閉，就無法管理它，而它也不會出現在下拉式清單中。
      > 
      > 
   2. 從 [選取動作] 下拉式清單中，選擇 [重新啟動控制器] 或 [關閉控制器]。
      
       ![重新啟動 StorSimple 裝置被動控制器](./media/storsimple-manage-device-controller/IC766020.png)
   3. 按一下核取圖示  ![核取圖示](./media/storsimple-manage-device-controller/IC740895.png)。

這將會重新啟動或關閉控制器。 下表根據您在 [ **變更控制器設定** ] 對話方塊中選取的項目，整理出所發生狀況的詳細資料摘要。  

| 選取項目 # | 如果您選擇... | 就會發生這個狀況。 |
| --- | --- | --- |
| 1. |重新啟動被動控制器。 |會建立工作以重新啟動控制器，且您會在工作成功建立之後收到通知。 這樣會起始控制器重新啟動。 依序存取[服務] > [儀表板] > [檢視作業記錄檔]，然後根據您服務的特定參數進行篩選，您就能監視重新啟動程序。 |
| 2. |重新啟動主動控制器。 |您會看到下列警告：「如果您重新啟動主動控制器，裝置將容錯移轉到被動控制器。 您要繼續嗎？ </br>如果您選擇繼續進行這項作業，接下來的步驟與重新啟動被動控制器的步驟相同 (請參閱選取項目 1)。 |
| 3. |關閉被動控制器。 |您會看到下列訊息：「關閉完成之後，您必須按下控制器上的電源按鈕以將其開啟。 您確定要關閉此控制器嗎？ </br>如果您選擇繼續進行這項作業，接下來的步驟與重新啟動被動控制器的步驟相同 (請參閱選取項目 1)。 |
| 4. |關閉主動控制器。 |您會看到下列訊息：「關閉完成之後，您必須按下控制器上的電源按鈕以將其開啟。 您確定要關閉此控制器嗎？ </br>如果您選擇繼續進行這項作業，接下來的步驟與重新啟動被動控制器的步驟相同 (請參閱選取項目 1)。 |

#### <a name="to-restart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>重新啟動或關閉 Windows PowerShell for StorSimple 中的控制器
執行下列步驟以從 Azure 傳統入口網站關閉或重新啟動 StorSimple 裝置上的單一控制器。

1. 使用序列主控台或 telnet 工作階段，從遠端電腦存取裝置。 遵循 [使用 PuTTY 連接到裝置序列主控台](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)中的步驟，連接到控制器 0 或控制器 1。
2. 在序列主控台功能表中，選擇選項 1 [使用完整存取權登入] 。
3. 在橫幅訊息中，記下您已連接的控制器 (控制器 0 或控制器 1) 以及它是主動或被動 (待命) 控制器。
   
   * 若要關閉單一控制器，請在提示中輸入：
     
       `Stop-HcsController`
     
       這會關閉您所連接的控制器。 如果您停止主動控制器，它會在關閉之前容錯移轉到被動控制器。
   * 若要重新啟動控制器，請在提示中輸入：
     
       `Restart-HcsController`
     
       這會重新啟動您所連接的控制器。 如果您重新啟動主動控制器，它會在重新啟動之前容錯移轉到主動控制器。

## <a name="shut-down-a-storsimple-device"></a>關閉 StorSimple 裝置
本節說明如何從遠端電腦關閉執行中或失敗的 StorSimple 裝置。 裝置會在關閉兩個裝置控制器之後關閉。 當裝置正在實際移動，或被帶離服務時，則已經完成裝置關閉。

> [!IMPORTANT]
> 關閉裝置之前，請檢查裝置元件的健全狀態。 瀏覽至 [裝置] > [維護] > [硬體狀態] 並確認所有元件的 LED 燈狀態為綠色。 只有狀況良好的裝置才會有綠色的狀態。 如果您的裝置正在關閉以更換故障的元件，您會看到個別元件的失敗 (紅色) 或降級 (黃色) 狀態。
> 
> 

#### <a name="to-shut-down-a-storsimple-device"></a>關閉 StorSimple 裝置
1. 透過 [重新啟動或關閉控制器](#restart-or-shut-down-a-single-controller) 程序，識別和關閉裝置上的被動控制器。 您可以在 Azure 傳統入口網站或 Windows PowerShell for StorSimple 中執行這項作業。
2. 重複上述步驟來關閉主動控制器。
3. 您現在必須查看裝置的背板。 完全關閉兩個控制器之後，兩個控制器上的狀態 Led 應該為閃爍的紅色。 如果您需要在此時將裝置完全關閉，請將電源和冷卻模組 (PCM) 上的電源開關切換為 OFF 的位置。 這樣可以關閉裝置。

<!--#### To shut down a StorSimple device in Windows PowerShell for StorSimple

1. Connect to the serial console of the StorSimple device by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-serial-console).

1. In the serial console menu, verify from the banner message that the controller you are connected to is the passive controller. If you are connected to the active controller, disconnect from this controller and connect to the other controller.

1. In the serial console menu, choose option 1, **log in with full access**.

1. At the prompt, type:

    `Stop-HCSController`

    This should shut down the current controller. To verify whether the shutdown has finished, check the back of the device. The controller status LED should be solid red.

1. Repeat steps 1 through 4 to connect to the active controller and then shut it down.

1. After both the controllers are completely shut down, the status LEDs on both should be blinking red. If you need to turn off the device completely at this time, flip the power switches on both Power and Cooling Modules (PCMs) to the OFF position.-->

## <a name="reset-the-device-to-factory-default-settings"></a>將裝置重設為出廠預設設定。
> [!IMPORTANT]
> 如果您需要將裝置重設為原廠預設設定，請聯絡 Microsoft 支援服務。 以下所述的程序，應只用於搭配 Microsoft 支援服務時使用。
> 
> 

此程序描述如何將 Microsoft Azure StorSimple 裝置重設為使用 Windows PowerShell for StorSimple 的出廠預設設定。
根據預設，重設裝置會從整個叢集移除所有資料和設定。

執行下列步驟來將 Microsoft Azure StorSimple 裝置重設為出廠預設設定：

### <a name="to-reset-the-device-to-default-settings-in-windows-powershell-for-storsimple"></a>將裝置重設為 Windows PowerShell for StorSimple 中的預設設定
1. 透過裝置的序列主控台存取裝置。 檢查橫幅訊息以確保您已連接到主動控制器。
2. 在序列主控台功能表中，選擇選項 1 [使用完整存取權登入] 。
3. 在提示中，輸入下列命令來重設整個叢集，移除所有資料、中繼資料和控制器設定︰
   
    `Reset-HcsFactoryDefault`
   
    若要改為重設單一控制站，請使用 [Reset-HcsFactoryDefault`-scope` Cmdlet 搭配 ](http://technet.microsoft.com/library/dn688132.aspx) 參數。)
   
    系統會重新啟動多次。 重設成功完成時，系統將會通知您。 根據系統模型，8100 裝置可能需要 45-60 分鐘來完成此程序，而 8600 需要 60-90 分鐘。
   
   > [!TIP]
   > * 如果您使用 Update 1.2 或更早版本，請使用 `–SkipFirmwareVersionCheck` 參數略過韌體版本檢查 (否則您將看到韌體不符錯誤：恢復出廠預設值因韌體版本不相符而無法繼續。 )。
   > * 在 Government 入口網站中執行 Update 1 或 1.1 ，且已執行成功的單一或雙重控制器更換 (含 pre-Update 1 軟體所隨附的更換控制器) 的 StorSimple 裝置的恢復出廠預設值程序可能會失敗。 這會發生在針對不存在於 pre-Update 1 軟體的控制器上的 SHA1 檔案的目前狀態驗證恢復出廠預設值時。 如果您看到這個恢復出廠預設值失敗，請連絡 Microsoft 支援服務以協助您進行下一個步驟。 在具有 Update 1 或更新版本軟體的原廠出貨更換控制器不會看到這個問題。
   > 
   > 

## <a name="questions-and-answers-about-managing-device-controllers"></a>有關管理裝置控制器的問題與解答
在本節中，我們摘要說明一些有關管理 StorSimple 裝置控制器的常見問題。

**問：** 如果裝置上的兩個控制器都狀況良好且已開啟，而我重新啟動或關閉主動控制器，會發生什麼事？

**答：** 如果裝置上的兩個控制器皆狀況良好且已開啟，您會收到確認提示。 您可以選擇：

* **重新啟動主動控制器** – 您會收到通知，告知您重新啟動主動控制器將使裝置容錯移轉到被動控制器。 控制器將重新啟動。
* **關閉主動控制器** – 您將會收到通知，告知您關閉主動控制器將導致停機。 您也必須在按下裝置上的電源按鈕以開啟控制器。

**問：** 如果裝置上的被動控制器無法使用或已關閉，而我重新啟動或關閉主動控制器，會發生什麼事？

**答：** 如果裝置上的被動控制器無法使用或已關閉，而您選擇：

* **重新啟動主動控制器** – 您會收到通知，告知您繼續執行作業會導致服務暫時中斷，且您會收到確認提示。
* **關閉主動控制器** – 您會收到通知，告知您繼續執行作業會導致停機，而且您必須按下一或兩個控制器上的電源按鈕來開啟裝置。 系統將提示您進行確認。

**問：** 何時控制器重新啟動或關機會無法進行？

**答：** 重新啟動或關閉控制器可能會在下列情況下失敗：

* 裝置更新進行中。
* 控制器重新啟動已在進行中。
* 控制器關閉已在進行中。

**問：** 您如何判斷控制器已重新啟動或關閉？

**答：** 您可以檢查 [維護] 頁面上的控制器狀態。 控制器狀態會指出控制器已重新啟動或關閉。 此外，如果控制器已重新啟動或關閉，[警示] 頁面會包含資訊警示。 控制器重新啟動和關閉作業也會記錄在作業記錄檔中。 如需有關作業記錄檔的詳細資訊，請移至 [檢視作業記錄檔](storsimple-service-dashboard.md#view-the-operations-logs)。

**問：** 控制器容錯移轉會不會對 I/O 造成任何影響？

**答：** 啟動器和主動控制器之間的 TCP 連接將會因為控制器容錯移轉而重設，但會在被動控制器繼續作業時重新建立。 在這項作業的過程中，啟動器與裝置之間的 I/O 活動中可能會有暫時的 (少於 30 秒) 暫停。

**問：** 如何在控制器關閉並遭移除後，將控制器傳回給服務？

**答：** 若要將控制器傳回給服務，您必須依照 [更換 StorSimple 裝置上的控制器模組](storsimple-controller-replacement.md)。

## <a name="next-steps"></a>後續步驟
* 如果發生任何無法使用本教學課程中所列之程序解決的 StorSimple 裝置控制器相關問題，請 [連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。
* 若要深入了解使用 StorSimple Manager 的方式，請移至 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。

