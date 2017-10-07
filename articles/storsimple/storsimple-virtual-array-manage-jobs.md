---
title: "aaaView 及管理 StorSimple Virtual Array 工作 |Microsoft 文件"
description: "描述 hello StorSimple 裝置管理員服務工作 頁面以及 toouse 它的 hello StorSimple Virtual Array 的 tootrack 最近和目前工作。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a>用於 hello StorSimple Virtual Array hello StorSimple 裝置管理員服務 tooview 工作
## <a name="overview"></a>概觀
hello**作業**刀鋒視窗提供單一中央入口網站，以檢視及管理連線的 tooyour StorSimple 裝置管理員服務的虛擬陣列已啟動的工作。 您可以針對多個虛擬裝置，檢視執行中、完成和失敗的作業。 結果會以表格式格式呈現。

![[作業] 刀鋒視窗](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

您可以快速尋找您感興趣的這類的欄位進行篩選的 hello 工作：

* **時間範圍**– 工作可以篩選根據的 hello 日期和時間範圍。
* **裝置**– 連接的特定裝置 tooyour 服務上起始工作。 hello 已篩選的工作會再製成資料表根據 hello 下列屬性：
  
  * **名稱**– hello 工作名稱可以是**所有**，**備份**，**複製**，**容錯移轉**，**下載更新**，或**安裝更新**。
  * **狀態** – 作業可以是 [全部]、[進行中]、[成功]、[失敗]或 [已取消]。
  * **實體**– hello 工作可以與磁碟區、 共用或裝置產生關聯。
  * **裝置**– hello hello 裝置的 hello 已啟動工作的名稱。
  * **在啟動**– hello hello 作業啟動時的時間。
  * **持續時間**– hello 執行 hello 作業的持續時間。
* **狀態** – 您可以搜尋全部、執行中、完成或已取消的作業。
* **作業類型**– hello 作業類型可為 all、 備份、 還原容錯移轉、 下載更新，或安裝更新。

hello 工作清單會重新整理每隔 30 秒。

## <a name="view-job-details"></a>檢視工作詳細資料
執行下列步驟 tooview hello 詳細資料的任何作業的 hello。

#### <a name="tooview-job-details"></a>tooview 工作詳細資料
1. 在 hello**作業**刀鋒視窗，顯示 hello 工作，您有興趣使用適當的篩選器執行查詢。 您可以搜尋完成或執行中作業。
2. 從工作 hello 表格式清單中選取工作。
   
    ![[作業] 刀鋒視窗](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. 在 hello hello 頁面底部，按一下**詳細資料**。
4. 在 hello**詳細資料**對話方塊中，您可以檢視狀態、 詳細資料，以及時間統計資料。 hello 如下圖所示的 hello 範例**備份工作詳細資料** 對話方塊。
   
    ![工作詳細資料](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a>當 hello 虛擬機器已經暫停 hello hypervisor 中的工作失敗
當工作處於大於 15 分鐘暫停您的 StorSimple Virtual Array 和 hello 裝置 （虛擬機器在 hypervisor 中佈建） 的進度，hello 作業失敗時。 這由於超過 tooyour StorSimple Virtual Array 時間正在與 hello Microsoft Azure 時間同步處理。 

您會看到下列錯誤 hello: 「 您的裝置時間是 15 分鐘以上的 hello Microsoft Azure 時間與同步處理。 請確定 hello hypervisor 和 hello 裝置時間與 NTP 伺服器同步。 請確定沒有連線問題。 tootroubleshoot 連線問題，執行診斷測試從 hello 本機 web UI 虛擬裝置。 」

這些失敗會套用 toobackup、 還原、 更新和容錯移轉作業。 如果您的虛擬機器已佈建為 HYPER-V 中，hello 機器最終同步處理時間與您的 hypervisor。 一旦發生這種情況，您可以重新啟動您的作業。

## <a name="next-steps"></a>後續步驟
[了解如何 toouse 會 hello 本機 web UI tooadminister 您 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。

