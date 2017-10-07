---
title: "aaaManage StorSimple 8000 系列裝置控制器 |Microsoft 文件"
description: "了解 toostop，重新啟動、 關機或重設您的 StorSimple 裝置控制站的方式。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/19/2017
ms.author: alkohli
ms.openlocfilehash: 5c59582b7ccf7cfeae9e7efbd0e4df9dc1d3871c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>管理 StorSimple 裝置控制器

## <a name="overview"></a>概觀

本教學課程描述 hello 可在您的 StorSimple 裝置控制站執行的不同作業。 您的 StorSimple 裝置中的 hello 控制站會在主動-被動組態的備援 （對等） 控制器。 在指定的時間，只能有一個控制器為作用中，並處理所有的 hello 磁碟和網路作業。 hello 另一個控制器處於被動模式。 Hello 主動控制器失效，如果 hello 被動控制器會自動變成使用中。

本教學課程使用包含 toomanage hello 裝置控制站的逐步指示:

* **控制站**hello StorSimple 裝置管理員服務在裝置的刀鋒視窗。
* Windows PowerShell for StorSimple

我們建議您管理透過 hello StorSimple 裝置管理員服務的 hello 裝置控制器。 如果只可以使用 Windows PowerShell for StorSimple 執行某個動作，hello 教學課程還會記錄下來。

閱讀本教學課程之後，您將能夠：

* 重新啟動或關閉 StorSimple 裝置控制器
* 關閉 StorSimple 裝置
* 重設您的 StorSimple 裝置 toofactory 預設值

## <a name="restart-or-shut-down-a-single-controller"></a>重新啟動或關閉單一控制器
一般系統作業並不需要重新啟動或關閉控制器。 只有在故障的裝置硬體元件需要更換時，才會常常使用單一裝置控制器的關閉作業。 只有在記憶體過度使用或控制器故障影響效能時，才會需要重新啟動控制器。 您也可能需要 toorestart 控制站之後在成功更換控制器，如果您希望 tooenable 測試 hello 取代控制器。

重新啟動的裝置不干擾 tooconnected 啟動器，假設 hello 被動控制站可用。 如果是被動控制器無法使用或已關閉，然後重新啟動 hello active 控制器可能會導致 hello 服務中斷和停機時間。

> [!IMPORTANT]
> * **執行中的控制器應該永遠不會實際移除，因為這會導致失去備援並增加停機的風險。**
> * hello 下列程序適用於僅 toohello StorSimple 實體裝置。 如需有關如何 toostart、 停止及重新啟動 hello StorSimple 雲端應用裝置，請參閱資訊[搭配 hello 雲端應用裝置](storsimple-8000-cloud-appliance-u2.md##work-with-the-storsimple-cloud-appliance)。

您可以重新啟動或關閉透過 hello hello StorSimple 裝置管理員服務或 Windows PowerShell 的 Azure 入口網站的單一裝置控制站 for StorSimple。

toomanage hello Azure 入口網站，從您的裝置控制站執行下列步驟 hello。

#### <a name="toorestart-or-shut-down-a-controller-in-azure-portal"></a>toorestart 或 Azure 入口網站中的控制站關機
1. 在您的 StorSimple 裝置管理員服務移過**裝置**。 從裝置 hello 清單中選取您的裝置。 

    ![選擇裝置](./media/storsimple-8000-manage-device-controller/manage-controller1.png)

2. 跳過**設定 > 控制站**。
   
    ![確認 StorSimple 裝置控制器的狀況良好](./media/storsimple-8000-manage-device-controller/manage-controller2.png)
3. 在 hello**控制器**刀鋒視窗中，確認您的裝置上的兩個 hello 控制器的 hello 狀態為**狀況良好**。 選取控制器，以滑鼠右鍵按一下，然後選取 [重新啟動] 或 [關閉]。

    ![選擇重新啟動或關閉 StorSimple 裝置控制器](./media/storsimple-8000-manage-device-controller/manage-controller3.png)

4. 工作建立 toorestart 或關閉 hello 控制器，您會有適用於警告，如果有的話。 toomonitor hello 重新啟動或關機，跳過**服務 > 活動記錄**然後篩選參數特定 tooyour 服務。 如果控制器已關閉，則您必須在 hello 控制器 tooturn toopush hello 電源按鈕 tooturn 其上。

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart 或關機的控制站，在 Windows PowerShell for StorSimple
StorSimple 的重新啟動 StorSimple 裝置 hello Windows PowerShell 從單一控制器或執行向下遵循步驟 tooshut hello。

1. 存取 hello hello 序列主控台或 telnet 工作階段從遠端電腦的裝置。 tooconnect tooController 0 或控制器 1，請依照下列中的 hello 步驟[使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)。
2. 在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。
3. 在 hello 橫幅訊息中，記下過，您所連接的 hello 控制器 （控制器 0 或控制器 1），以及是否使用中的 hello 被動 （待命） 控制站。
   
   * tooshut 關閉單一控制器，在 hello 提示字元，輸入：
     
       `Stop-HcsController`
     
       這會關閉您所連接的 hello 控制站。 如果您停止 hello 作用中控制器，hello 裝置容錯移轉 toohello 被動控制器。

   * toorestart 控制站，在 hello 提示字元中輸入：
     
       `Restart-HcsController`
     
       這會重新啟動您所連接的 hello 控制站。 如果您重新啟動 hello 作用中控制器，它會容錯移轉 toohello 被動控制站之前 hello 重新啟動。

## <a name="shut-down-a-storsimple-device"></a>關閉 StorSimple 裝置

本章節將說明如何 tooshut 關閉執行中或失敗的 StorSimple 裝置，從遠端電腦。 兩個 hello 裝置控制器都關閉之後，裝置已關閉。 Hello 裝置實際移動，或帶離服務時，是完成裝置關機。

> [!IMPORTANT]
> 您關閉 hello 裝置之前，請檢查 hello hello 裝置元件健全狀況。 導覽 tooyour 裝置，然後按一下**設定 > 硬體健全狀況**。 在 hello**狀態和硬體的健全狀況**刀鋒視窗中，確認所有 hello 元件 hello LED 狀態為綠色。 只有狀況良好的裝置才會有綠色的狀態。 如果您的裝置關機 tooreplace 的故障元件時，您會看到故障 （紅色） 或降級 （黃色） 狀態 hello 個別元件。


#### <a name="tooshut-down-a-storsimple-device"></a>tooshut StorSimple 裝置

1. 使用 hello[重新啟動或關閉控制器](#restart-or-shut-down-a-single-controller)程序 tooidentify 並關機 hello 裝置上的被動控制器。 您可以針對 StorSimple hello Azure 入口網站或 Windows PowerShell 中執行這項作業。
2. 重複上述步驟 tooshut 向 hello 作用中控制器的 hello。
3. 您必須立即查看 hello 回 hello 裝置面板。 Hello 兩個控制器都關閉之後，hello 兩個 hello 控制器狀態 Led 應閃爍紅燈。 如果您完全在這個階段需要關閉裝置 hello tooturn 上電源和冷卻模組 (Pcm), 翻轉 hello 電源開關 toohello OFF 位置。 這應該關閉 hello 裝置。

## <a name="reset-hello-device-toofactory-default-settings"></a>重設 hello 裝置 toofactory 預設值

> [!IMPORTANT]
> 如果您需要 tooreset 裝置 toofactory 預設設定，請連絡 Microsoft 支援服務。 hello 如下所述的程序只應該用於搭配 Microsoft 支援服務。

此程序描述如何 tooreset 您 Microsoft Azure StorSimple 裝置 toofactory 的預設設定使用 Windows PowerShell for StorSimple。
重設裝置移除所有資料和設定預設的 hello 整個叢集。

您的 Microsoft Azure StorSimple 裝置 toofactory 預設設定執行下列步驟 tooreset hello:

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset hello toodefault 的裝置設定 Windows PowerShell for StorSimple
1. 透過序列主控台存取 hello 裝置。 請檢查您所連接的 toohello hello 橫幅訊息 tooensure **Active**控制站。
2. 在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。
3. 在 hello 提示中輸入下列命令 tooreset hello 整個叢集，移除所有的資料、 中繼資料及控制器設定 hello:
   
    `Reset-HcsFactoryDefault`
   
    tooinstead 重設一個控制器，請使用 hello [Reset-hcsfactorydefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet 搭配 hello`-scope`參數。)
   
    hello 系統將會重新啟動多次。 Hello 重設已順利完成時，系統會通知您。 根據 hello 系統模型，它可能需要 45-60 分鐘 8100 裝置和 60-90 分鐘的 8600 toofinish 此程序。
   
## <a name="questions-and-answers-about-managing-device-controllers"></a>有關管理裝置控制器的問題與解答
在本節中，我們有摘要一些 hello 常見問題集有關管理 StorSimple 裝置控制站。

**問：** 如果兩者 hello 我的裝置上控制站，會發生什麼情況都是狀況良好並已在與我重新啟動或關閉 hello 主動控制器？

**答：** 如果您的裝置上的兩個 hello 控制器皆狀況良好並已 on 時，系統會提示您確認。 您可以選擇：

* **重新啟動主動控制器的 hello** – 您會收到通知，重新啟動主動控制器造成 hello 裝置 toofail 透過 toohello 被動控制站。 hello 控制器會重新啟動。
* **關閉主動控制器** – 您會收到通知，告知您關閉主動控制器將導致停機。 您也需要 hello hello 控制站上的裝置 tooturn toopush hello 電源按鈕。

**問：** 如果我的裝置上的 hello 被動控制器無法使用或已關閉，因此我重新啟動或關閉 hello 主動控制器，則會發生什麼事？

**答：** 如果您的裝置上的 hello 被動控制器無法使用或已關閉，而且您選擇：

* **重新啟動主動控制器的 hello** – 繼續 hello 作業將會導致 hello 服務暫時中斷，系統會提示您確認您會收到通知。
* **關閉主動控制器**– 就會通知您繼續 hello 作業會導致停機時間。 您也需要 hello 裝置上的一個或兩個控制器 tooturn toopush hello 電源按鈕。 系統會提示您進行確認。

**問：** 何時沒有 hello 控制器重新啟動或關機失敗 tooprogress？

**答：** 重新啟動或關閉控制器可能會在下列情況下失敗：

* 裝置更新進行中。
* 控制器重新啟動已在進行中。
* 控制器關閉已在進行中。

**問：** 您如何判斷控制器已重新啟動或關閉？

**答：** 您可以檢查 hello 控制器刀鋒視窗上的控制器狀態。 hello 控制器狀態會指出控制器是否在重新啟動或關閉 hello 程序。 此外，hello**警示**刀鋒視窗包含資訊警示，如果 hello 控制站重新啟動或關機。 hello 控制器重新啟動及關閉作業也會記錄在 hello 活動記錄檔。 如需活動記錄檔的詳細資訊，請移至太[檢視 hello 活動記錄檔](storsimple-8000-service-dashboard.md#view-the-activity-logs)。

**問：** 是否有任何影響 toohello I/O 控制器容錯移轉後？

**答：** 由於控制器容錯移轉，將會重設 hello 啟動器與主動控制站之間的 TCP 連線，但 hello 被動控制器繼續作業時就會重新建立。 Hello 課程的這項作業期間可能會暫時 （少於 30 秒） 暫停啟動器與 hello 裝置之間的 I/O 活動。

**問：** 如何關閉和移除之後傳回我控制器 tooservice？

**答：** tooreturn 控制器 tooservice，您必須將它插入 hello 底座中所述[取代您的 StorSimple 裝置上的控制器模組](storsimple-8000-controller-replacement.md)。

## <a name="next-steps"></a>後續步驟
* 如果您遇到任何問題，您無法使用此教學課程中所列的 hello 程序來解決您 StorSimple 裝置控制站與[連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。
* toolearn 進一步了解使用 hello StorSimple 裝置管理員服務，請跳過[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。

