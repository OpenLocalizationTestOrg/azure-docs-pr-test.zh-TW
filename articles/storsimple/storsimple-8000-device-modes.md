---
title: "aaaChange StorSimple 裝置模式 |Microsoft 文件"
description: "描述 hello StorSimple 裝置模式，並說明如何 toouse Windows PowerShell for StorSimple toochange hello 裝置模式。"
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 058ca6cc38954bce3679cc21b39d341b10cb4dfb
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


### <a name="recovery-mode"></a>復原模式

復原模式可以形容成「含網路支援的 Windows 安全模式」。 復原模式會 hello Microsoft 支援服務團隊，並讓他們 tooperform 診斷 hello 系統上。 hello 的復原模式的主要目標是 tooretrieve hello 系統記錄檔。

如果您的系統進入復原模式，您應該連絡 Microsoft 支援服務來請示後續步驟。 如需詳細資訊，請移至太[請連絡 Microsoft 支援](storsimple-8000-contact-microsoft-support.md)。

> [!NOTE]
> **您不能放置 hello 裝置進入修復模式。如果 hello 裝置處於不正常的狀態，復原模式會嘗試 tooget hello 裝置進入 Microsoft 支援人員可以檢查它的狀態。**

## <a name="determine-storsimple-device-mode"></a>判斷 StorSimple 裝置模式

#### <a name="toodetermine-hello-current-device-mode"></a>toodetermine hello 目前裝置模式

1. 登入 toohello 裝置序列主控台中的 hello 步驟[使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)。
2. 查看 hello hello 裝置序列主控台功能表中的 hello 橫幅訊息。 此訊息會明確指出 hello 裝置是否為維護或復原模式。 如果 hello 訊息沒有任何相關 toohello 系統模式的特定資訊，請 hello 裝置處於正常模式。

## <a name="change-hello-storsimple-device-mode"></a>變更 hello StorSimple 裝置模式

您可以將 hello StorSimple 裝置放入維護模式 （從標準模式） tooperform 維護或安裝維護模式更新。 執行下列程序 tooenter 或離開維護模式的 hello。

> [!IMPORTANT]
> 之前進入維護模式，請確認兩個裝置控制器會處於狀況良好，藉由存取 hello**裝置設定 > 硬體健全狀況**為您的裝置 hello Azure 入口網站中。 如果一或兩個 hello 控制站狀況良好，請連絡 Microsoft 支援 hello 接下來的步驟。 如需詳細資訊，請移至太[請連絡 Microsoft 支援](storsimple-8000-contact-microsoft-support.md)。
 

#### <a name="tooenter-maintenance-mode"></a>tooenter 維護模式

1. 登入 toohello 裝置序列主控台中的 hello 步驟[使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)。
2. 在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。 出現提示時，提供 hello**裝置系統管理員密碼**。 hello 預設密碼為： `Password1`。
3. 在 hello 命令提示字元中輸入 
   
    `Enter-HcsMaintenanceMode`
4. 您會看到警告訊息，告知您該維護模式將會中斷所有的 I/O 要求並切斷 hello 連接 toohello Azure 入口網站，系統將提示您確認。 型別**Y** tooenter 維護模式。
5. 這兩個控制站都將重新啟動。 Hello 重新啟動完成時，會指出 hello 序列主控台橫幅，該 hello 裝置處於維護模式。 下方顯示一項範例輸出。

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="tooexit-maintenance-mode"></a>tooexit 維護模式

1. 登入 toohello 裝置序列主控台。 請確認從您的裝置處於維護模式的 hello 橫幅訊息。
2. 在 hello 命令提示字元中輸入：
   
    `Exit-HcsMaintenanceMode`
3. 隨即會出現警告訊息和確認訊息。 型別**Y** tooexit 維護模式。
4. 這兩個控制站都將重新啟動。 Hello 重新啟動完成時，hello 序列主控台橫幅指出該 hello 裝置處於正常模式。 下方顯示一項範例輸出。

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure tooinstall on each controller could result in data corruption. Exiting maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooexit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a>後續步驟

了解如何太[適用於 [標準] 和 [維護模式更新](storsimple-update-device.md)StorSimple 裝置上。

