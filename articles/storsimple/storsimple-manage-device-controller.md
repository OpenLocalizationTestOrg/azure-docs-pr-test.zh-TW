---
title: "aaaManage StorSimple 裝置控制站 |Microsoft 文件"
description: "了解 toostop，重新啟動、 關機或重設您的 StorSimple 裝置控制站的方式。"
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
ms.openlocfilehash: 9a86aa0f4a8fd96c36df206774972602c47a49a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>管理 StorSimple 裝置控制器
## <a name="overview"></a>概觀
本教學課程描述 hello 可在您的 StorSimple 裝置控制站執行的不同作業。 您的 StorSimple 裝置中的 hello 控制站會在主動-被動組態的備援 （對等） 控制器。 在指定的時間，只能有一個控制器為作用中，並處理所有的 hello 磁碟和網路作業。 hello 另一個控制器處於被動模式。 Hello 主動控制器失效，如果 hello 被動控制器會自動啟動。

本教學課程使用包含 toomanage hello 裝置控制站的逐步指示:

* **控制站**區段 hello**維護**hello StorSimple Manager 服務中的頁面
* Windows PowerShell for StorSimple

我們建議您管理透過 hello StorSimple Manager 服務的 hello 裝置控制器。 如果只可以使用 Windows PowerShell for StorSimple 執行某個動作，hello 教學課程還會記錄下來。

閱讀本教學課程之後，您將能夠：

* 重新啟動或關閉 StorSimple 裝置控制器
* 關閉 StorSimple 裝置
* 重設您的 StorSimple 裝置 toofactory 預設值

## <a name="restart-or-shut-down-a-single-controller"></a>重新啟動或關閉單一控制器
一般系統作業並不需要重新啟動或關閉控制器。 只有在故障的裝置硬體元件需要更換時，才會常常使用單一裝置控制器的關閉作業。 只有在記憶體過度使用或控制器故障影響效能時，才會需要重新啟動控制器。 您也可能需要 toorestart 控制站之後在成功更換控制器，如果您希望 tooenable 測試 hello 取代控制器。

重新啟動的裝置不干擾 tooconnected 啟動器，假設 hello 被動控制站可用。 如果是被動控制器無法使用或已關閉，然後重新啟動 hello active 控制器可能會導致 hello 服務中斷和停機時間。

> [!IMPORTANT]
> * **執行中的控制器應該永遠不會實際移除，因為這會導致失去備援並增加停機的風險。**
> * hello 下列程序適用於僅 toohello StorSimple 實體裝置。 如需有關如何 toostart、 停止及重新啟動 hello 虛擬裝置，請參閱資訊[與 hello 虛擬裝置搭配使用](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device)。
> 
> 

您可以重新啟動或關機的單一裝置控制站使用 for StorSimple 的 hello hello StorSimple Manager 服務或 Windows PowerShell 的 Azure 傳統入口網站

toomanage hello Azure 傳統入口網站，從您的裝置控制站執行下列步驟 hello。

#### <a name="toorestart-or-shut-down-a-controller-in-classic-portal"></a>toorestart 或傳統入口網站中的控制站關機
1. 瀏覽過**裝置 > 維護**。
2. 跳過**硬體狀態**，並確認您的裝置上的兩個 hello 控制器 hello 狀態**狀況良好**。
   
    ![確認 StorSimple 裝置控制器的狀況良好](./media/storsimple-manage-device-controller/IC766017.png)
3. 從 hello 底部 hello**維護**頁面上，按一下**管理控制器**。
   
    ![管理 StorSimple 裝置控制器](./media/storsimple-manage-device-controller/IC766018.png)</br>
   
   > [!NOTE]
   > 如果您看**管理控制器**，則您需要 tooinstall 更新。 如需詳細資訊，請參閱 [更新您的 StorSimple 裝置](storsimple-update-device.md)。
   > 
   > 
4. 在 hello**變更控制器設定**對話方塊方塊中，執行下列 hello:
   
   1. 從 hello**選取控制器**下拉式清單中，您想 toomanage 選取 hello 控制站。 hello 選項為控制器 0 及控制器 1。 這些控制器也可識別為主動或被動。
      
      > [!NOTE]
      > 控制器無法使用，便無法使用或已關閉，而且它不會出現在 hello 下拉式清單中。
      > 
      > 
   2. 從 hello**選取動作**下拉式清單中，選擇**重新啟動控制器**或**關閉控制器**。
      
       ![重新啟動 StorSimple 裝置被動控制器](./media/storsimple-manage-device-controller/IC766020.png)
   3. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-manage-device-controller/IC740895.png).

這將會重新啟動或關閉 hello 控制器。 hello 下表摘要說明 hello 詳細資料，根據您 hello 中所做的 hello 選項發生什麼事**變更控制器設定** 對話方塊。  

| 選取項目 # | 如果您選擇... | 就會發生這個狀況。 |
| --- | --- | --- |
| 1. |重新啟動 hello 被動控制器。 |Toorestart hello 控制站，將會建立一個作業，且 hello 工作成功建立後將會通知您。 這會起始 hello 控制器重新啟動。 您可以藉由存取監視 hello 重新啟動程序**服務 > 儀表板 > 檢視作業記錄檔**然後篩選參數特定 tooyour 服務。 |
| 2. |重新啟動 hello 作用中控制器。 |您會看到下列警告 hello: 「 如果您重新啟動 hello 作用中控制器，hello 裝置將無法透過 toohello 被動控制站。 您想 toocontinue？ 」 </br>如果您選擇 tooproceed 進行這項作業，hello 下一個步驟將會使用相同 toothose toorestart hello 被動控制站 （請參閱選取項目 1）。 |
| 3. |Hello 被動控制站關機。 |您會看到下列訊息的 hello: 「 關閉已完成之後，您將需要 toopush hello 電源按鈕上控制器 tooturn 它。 確定要關閉此控制站 tooshut？ 」 </br>如果您選擇 tooproceed 進行這項作業，hello 下一個步驟將會使用相同 toothose toorestart hello 被動控制站 （請參閱選取項目 1）。 |
| 4. |關閉 hello 作用中控制器。 |您會看到下列訊息的 hello: 「 關閉已完成之後，您將需要 toopush hello 電源按鈕上控制器 tooturn 它。 確定要關閉此控制站 tooshut？ 」 </br>如果您選擇 tooproceed 進行這項作業，hello 下一個步驟將會使用相同 toothose toorestart hello 被動控制站 （請參閱選取項目 1）。 |

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart 或關機的控制站，在 Windows PowerShell for StorSimple
執行 hello 遵循步驟 tooshut 關閉或重新啟動 StorSimple 裝置 hello Azure 傳統入口網站從單一控制器。

1. 使用 hello 序列主控台或 telnet 工作階段從遠端電腦存取 hello 裝置。 連線 tooController 0 或控制器 1，由下列 hello 中的步驟[使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)。
2. 在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。
3. 在 hello 橫幅訊息中，記下過，您所連接的 hello 控制器 （控制器 0 或控制器 1），以及是否使用中的 hello 被動 （待命） 控制站。
   
   * tooshut 關閉單一控制器，在 hello 提示字元，輸入：
     
       `Stop-HcsController`
     
       這將會關閉您所連接的 hello 控制器。 如果您停止 hello 作用中控制器，然後它將會容錯移轉 toohello 被動控制器在關閉之前。
   * toorestart 控制站，在 hello 提示字元中輸入：
     
       `Restart-HcsController`
     
       這會重新啟動您所連接的 hello 控制站。 如果您重新啟動 hello 作用中控制器，它將容錯移轉 toohello 被動控制站之前 hello 重新啟動。

## <a name="shut-down-a-storsimple-device"></a>關閉 StorSimple 裝置
本章節將說明如何 tooshut 關閉執行中或失敗的 StorSimple 裝置，從遠端電腦。 裝置已關閉之後關閉兩個 hello 裝置控制器。 Hello 裝置實際移動，或帶離服務時，是完成裝置關機。

> [!IMPORTANT]
> 您關閉 hello 裝置之前，請檢查 hello hello 裝置元件健全狀況。 瀏覽過**裝置 > 維護 > 硬體狀態**並確認所有 hello 元件 hello LED 狀態為綠色。 只有狀況良好的裝置才會有綠色的狀態。 如果您的裝置關機 tooreplace 的故障元件時，您會看到故障 （紅色） 或降級 （黃色） 狀態 hello 個別元件。
> 
> 

#### <a name="tooshut-down-a-storsimple-device"></a>tooshut StorSimple 裝置
1. 使用 hello[重新啟動或關閉控制器](#restart-or-shut-down-a-single-controller)程序 tooidentify 並關機 hello 裝置上的被動控制器。 您可以針對 StorSimple hello Azure 傳統入口網站或 Windows PowerShell 中執行這項作業。
2. 重複上述步驟 tooshut 向 hello 作用中控制器的 hello。
3. 您現在就必須在 hello toolook 背 hello 裝置。 Hello 兩個控制器都關閉之後，hello 兩個 hello 控制器狀態 Led 應閃爍紅燈。 如果您完全在這個階段需要關閉裝置 hello tooturn 上電源和冷卻模組 (Pcm), 翻轉 hello 電源開關 toohello OFF 位置。 這應該關閉 hello 裝置。

<!--#### tooshut down a StorSimple device in Windows PowerShell for StorSimple

1. Connect toohello serial console of hello StorSimple device by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-serial-console).

1. In hello serial console menu, verify from hello banner message that hello controller you are connected toois hello passive controller. If you are connected toohello active controller, disconnect from this controller and connect toohello other controller.

1. In hello serial console menu, choose option 1, **log in with full access**.

1. At hello prompt, type:

    `Stop-HCSController`

    This should shut down hello current controller. tooverify whether hello shutdown has finished, check hello back of hello device. hello controller status LED should be solid red.

1. Repeat steps 1 through 4 tooconnect toohello active controller and then shut it down.

1. After both hello controllers are completely shut down, hello status LEDs on both should be blinking red. If you need tooturn off hello device completely at this time, flip hello power switches on both Power and Cooling Modules (PCMs) toohello OFF position.-->

## <a name="reset-hello-device-toofactory-default-settings"></a>重設 hello 裝置 toofactory 預設值
> [!IMPORTANT]
> 如果您需要 tooreset 裝置 toofactory 預設設定，請連絡 Microsoft 支援服務。 hello 如下所述的程序只應該用於搭配 Microsoft 支援服務。
> 
> 

此程序描述如何 tooreset 您 Microsoft Azure StorSimple 裝置 toofactory 的預設設定使用 Windows PowerShell for StorSimple。
重設裝置移除所有資料和設定預設的 hello 整個叢集。

您的 Microsoft Azure StorSimple 裝置 toofactory 預設設定執行下列步驟 tooreset hello:

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset hello toodefault 的裝置設定 Windows PowerShell for StorSimple
1. 透過序列主控台存取 hello 裝置。 請檢查您是連接的 toohello 作用中控制器的 hello 橫幅訊息 tooensure。
2. 在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。
3. 在 hello 提示中輸入下列命令 tooreset hello 整個叢集，移除所有的資料、 中繼資料及控制器設定 hello:
   
    `Reset-HcsFactoryDefault`
   
    tooinstead 重設一個控制器，請使用 hello [Reset-hcsfactorydefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet 搭配 hello`-scope`參數。)
   
    hello 系統將會重新啟動多次。 Hello 重設已順利完成時，系統會通知您。 根據 hello 系統模型，它可能需要 45-60 分鐘 8100 裝置和 60-90 分鐘的 8600 toofinish 此程序。
   
   > [!TIP]
   > * 如果您使用更新 1.2 或是之前使用 hello`–SkipFirmwareVersionCheck`參數 tooskip hello 韌體版本檢查 (否則，您會看到韌體不符錯誤： 無法繼續原廠重設，因為 tooa hello 韌體版本不符。 )。
   > * 正在更新 1 或 1.1 hello 政府入口網站中，且已執行成功的單一或雙重控制器更換 （與 Update 1 所隨附的替換控制器的 StorSimple 裝置 hello 原廠重設程序可能會失敗軟體）。 發生這種情況時 hello 原廠重設映像驗證 hello SHA1 檔案不存在的 hello 控制站上的更新前 1 軟體存在。 如果您看到此原廠重設失敗，請連絡 Microsoft 支援服務 tooassist 您 hello 與後續步驟。 此問題不會出現與出貨從更新 1 或更新版本的軟體 hello 原廠替換控制器。
   > 
   > 

## <a name="questions-and-answers-about-managing-device-controllers"></a>有關管理裝置控制器的問題與解答
在本節中，我們有摘要一些 hello 常見問題集有關管理 StorSimple 裝置控制站。

**問：** 如果兩者 hello 我的裝置上控制站，會發生什麼情況都是狀況良好並已在與我重新啟動或關閉 hello 主動控制器？

**答：** 如果您的裝置上的兩個 hello 控制器皆狀況良好並已 on 時，系統會提示您確認。 您可以選擇：

* **重新啟動主動控制器的 hello** – 您將會收到通知，重新啟動主動控制器將會導致 hello 裝置 toofail 透過 toohello 被動控制站。 hello 控制器將會重新啟動。
* **關閉主動控制器** – 您將會收到通知，告知您關閉主動控制器將導致停機。 您也必須上 hello hello 控制站上的裝置 tooturn toopush hello 電源 按鈕。

**問：** 如果我的裝置上的 hello 被動控制器無法使用或已關閉，因此我重新啟動或關閉 hello 主動控制器，則會發生什麼事？

**答：** 如果您的裝置上的 hello 被動控制器無法使用或已關閉，而且您選擇：

* **重新啟動主動控制器的 hello** – 系統會通知您繼續 hello 作業將會導致 hello 服務暫時中斷，系統將提示您確認。
* **關閉主動控制器**– 系統會通知您，繼續 hello 作業將導致停機時間，而且您必須在 hello 裝置上的一個或兩個控制器 tooturn toopush hello 電源 按鈕。 系統將提示您進行確認。

**問：** 何時沒有 hello 控制器重新啟動或關機失敗 tooprogress？

**答：** 重新啟動或關閉控制器可能會在下列情況下失敗：

* 裝置更新進行中。
* 控制器重新啟動已在進行中。
* 控制器關閉已在進行中。

**問：** 您如何判斷控制器已重新啟動或關閉？

**答：** 您可以檢查 hello hello 維護 頁面上的控制器狀態。 hello 控制器狀態會指出控制器是否已重新啟動或關機。 此外，如果 hello 控制器重新啟動或關閉 hello 警示 頁面會包含資訊警示。 hello 控制器重新啟動及關閉作業也會記錄在 hello 作業記錄檔。 如需作業記錄檔的詳細資訊，請移至太[檢視 hello 作業記錄檔](storsimple-service-dashboard.md#view-the-operations-logs)。

**問：** 是否有任何影響 toohello I/o 控制器容錯移轉後？

**答：** 由於控制器容錯移轉，將會重設 hello 啟動器與主動控制站之間的 TCP 連線，但 hello 被動控制器繼續作業時就會重新建立。 Hello 課程的這項作業期間可能會暫時 （少於 30 秒） 暫停啟動器與 hello 裝置之間的 I/O 活動。

**問：** 如何關閉和移除之後傳回我控制器 tooservice？

**答：** tooreturn 控制器 tooservice，您必須將它插入 hello 底座中所述[取代您的 StorSimple 裝置上的控制器模組](storsimple-controller-replacement.md)。

## <a name="next-steps"></a>後續步驟
* 如果您遇到任何問題，您無法使用此教學課程中所列的 hello 程序來解決您 StorSimple 裝置控制站與[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。
* toolearn 進一步了解使用 hello StorSimple Manager 服務，請跳過[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。

