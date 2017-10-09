---
title: "aaaChange hello StorSimple 裝置模式 |Microsoft 文件"
description: "描述 hello StorSimple 裝置模式，並說明如何 toouse Windows PowerShell for StorSimple toochange hello 裝置模式。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: e9d7d277-8a2f-45eb-9fef-355486e14cbc
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 299fd380a83bcd06780c97937f4064f0791b440d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a>變更您的 StorSimple 裝置上的 hello 裝置模式
本文章會提供各種不同的模式，您的 StorSimple 裝置能 hello 的簡短描述。 StorSimple 裝置有三種運作模式：標準、維護和復原。 

閱讀本文之後，您將了解：

* Hello StorSimple 裝置模式為何
* Toofigure 出哪些模式 hello StorSimple 裝置的方式是在
* 如何從一般 toomaintenance 模式 toochange 和*反之亦然*

hello 上方管理工作只能透過您的 StorSimple 裝置 hello Windows PowerShell 介面執行。

## <a name="about-storsimple-device-modes"></a>關於 StorSimple 裝置模式
StorSimple 裝置可以在標準、維護和復原模式下運作。 以下簡短描述每一種模式。

### <a name="normal-mode"></a>標準模式
這被定義為 hello 正常作業模式的完整設定 StorSimple 裝置。 根據預設，您的裝置會以標準模式運作。

### <a name="maintenance-mode"></a>維護模式
有時候 hello StorSimple 裝置可能需要 toobe 放入維護模式。 這個模式可讓您在 hello 裝置上的 tooperform 維護，而且安裝更新具有干擾性，例如那些相關 toodisk 韌體。

您可以進入 hello 系統維護模式僅透過 hello Windows PowerShell for StorSimple。 在此模式中，所有的 I/O 要求都會暫停。 也會停止服務，例如非揮發性隨機存取記憶體 (NVRAM) 或 hello 叢集服務。 當您進入或退出此模式中，兩個 hello 控制器會重新啟動。 當您結束 hello 維護模式時，所有的 hello 服務將會繼續，而且應該是狀況良好。 這可能需要幾分鐘的時間。

> [!NOTE]
> **僅正常運作的裝置才支援維護模式。不支援在其中之一或兩者的 hello 控制器無法運作的裝置上。**
> </br>
> 
> 

### <a name="recovery-mode"></a>復原模式
復原模式可以形容成「含網路支援的 Windows 安全模式」。 復原模式會 hello Microsoft 支援服務團隊，並讓他們 tooperform 診斷 hello 系統上。 hello 的復原模式的主要目標是 tooretrieve hello 系統記錄檔。

如果您的系統進入復原模式，您應該連絡 Microsoft 支援服務來請示後續步驟。 如需詳細資訊，請移至太[請連絡 Microsoft 支援](storsimple-contact-microsoft-support.md)。

> [!NOTE]
> **您不能放置 hello 裝置進入修復模式。如果 hello 裝置處於不正常的狀態，復原模式會嘗試 tooget hello 裝置進入 Microsoft 支援人員可以檢查它的狀態。**
> 
> 

## <a name="determine-storsimple-device-mode"></a>判斷 StorSimple 裝置模式
#### <a name="toodetermine-hello-current-device-mode"></a>toodetermine hello 目前裝置模式
1. 登入 toohello 裝置序列主控台中的 hello 步驟[使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)。
2. 查看 hello hello 裝置序列主控台功能表中的 hello 橫幅訊息。 此訊息會明確指出 hello 裝置是否為維護或復原模式。 如果 hello 訊息沒有任何相關 toohello 系統模式的特定資訊，請 hello 裝置處於正常模式。

## <a name="change-hello-storsimple-device-mode"></a>變更 hello StorSimple 裝置模式
您可以將 hello StorSimple 裝置放入維護模式 （從標準模式） tooperform 維護或安裝維護模式更新。 執行下列程序 tooenter 或離開維護模式的 hello。

> [!IMPORTANT]
> 之前進入維護模式，請確認兩個裝置控制器會處於狀況良好，藉由存取 hello**硬體狀態**上 hello**維護**hello Azure 傳統入口網站中的頁面。 如果一或兩個 hello 控制站狀況良好，請連絡 Microsoft 支援 hello 接下來的步驟。 如需詳細資訊，請移至太[請連絡 Microsoft 支援](storsimple-contact-microsoft-support.md)。
> 
> 

#### <a name="tooenter-maintenance-mode"></a>tooenter 維護模式
1. 登入 toohello 裝置序列主控台中的 hello 步驟[使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)。
2. 在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。 出現提示時，提供 hello**裝置系統管理員密碼**。 hello 預設密碼為： `Password1`。
3. 在 hello 命令提示字元中輸入 
   
    `Enter-HcsMaintenanceMode`
4. 您會看到警告訊息，告知您該維護模式將會中斷所有的 I/O 要求並切斷 hello 連接 toohello Azure 傳統入口網站，系統將提示您確認。 型別**Y** tooenter 維護模式。
5. 這兩個控制站都將重新啟動。 Hello 重新啟動完成時，會出現另一個訊息，指出該 hello 裝置處於維護模式。

#### <a name="tooexit-maintenance-mode"></a>tooexit 維護模式
1. 登入 toohello 裝置序列主控台。 請確認從您的裝置處於維護模式的 hello 橫幅訊息。
2. 在 hello 命令提示字元中輸入：
   
    `Exit-HcsMaintenanceMode`
3. 隨即會出現警告訊息和確認訊息。 型別**Y** tooexit 維護模式。
4. 這兩個控制站都將重新啟動。 Hello 重新啟動完成時，會出現另一個訊息，指出該 hello 裝置處於正常模式。

## <a name="next-steps"></a>後續步驟
了解如何太[適用於 [標準] 和 [維護模式更新](storsimple-update-device.md)StorSimple 裝置上。

