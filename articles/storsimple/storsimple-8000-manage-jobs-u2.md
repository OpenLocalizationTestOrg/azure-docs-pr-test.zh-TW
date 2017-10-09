---
title: "aaaView 及管理 StorSimple 8000 系列的作業 |Microsoft 文件"
description: "描述 hello StorSimple 裝置管理員服務作業 刀鋒視窗以及 toouse 它 tootrack 最近、 目前和已排程備份工作。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a>使用 hello StorSimple 裝置管理員服務 tooview 及管理工作 (Update 3 及更新版本)

## <a name="overview"></a>概觀
hello**作業**刀鋒視窗會提供單一中央入口網站檢視和管理裝置所啟動的作業已連線 tooyour StorSimple 裝置管理員服務。 您可以針對多個裝置，檢視已排程、執行中、完成、已取消和失敗的工作。 結果會以表格式格式呈現。

![[作業] 刀鋒視窗](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

您可以快速尋找您感興趣的這類的欄位進行篩選的 hello 工作：

* **狀態** – 作業可能在進行中、成功、已取消、失敗、取消中，或是成功但發生錯誤。
* **時間範圍**– 工作可以篩選根據的 hello 日期和時間範圍。 hello 範圍是過去 1 小時、 過去 24 小時、 過去 7 天、 過去 30 天、 過去一年或自訂的日期。
* **型別**– hello 作業類型可以是已排程的備份、 手動備份、 還原備份複製磁碟區、 容錯移轉磁碟區容器、 建立本機固定磁碟區，修改磁碟區、 安裝更新、 收集支援記錄檔和建立雲端應用裝置。
* **裝置**– 特定連接裝置 tooyour 服務上起始工作。
  
hello 已篩選的工作會再製成資料表的下列屬性的 hello hello 基礎：
  
* **名稱** – 排程備份、手動備份、還原備份、複製磁碟區、容錯移轉磁碟區容器、建立固定在本機的磁碟區、修改磁碟區、安裝更新、收集支援記錄，以及建立雲端設備。
* **狀態** – 執行中、完成、已取消、失敗、取消中，或是完成但發生錯誤。
* **實體**– hello 工作可以與磁碟區、 備份原則或裝置產生關聯。 例如，複製工作與磁碟區相關聯，而排程的備份工作則與備份原則相關聯。 裝置工作是透過災害復原 (DR) 或還原作業而建立。
* **裝置**– hello hello 裝置的 hello 已啟動工作的名稱。
* **在啟動**– hello hello 作業啟動時的時間。
* **持續時間**– hello 時間必要的 toocomplete hello 作業。

hello 工作清單會重新整理每隔 30 秒。

您可以執行下列作業相關的動作，此頁面上的 hello:

* 檢視工作詳細資料
* 取消工作

## <a name="view-job-details"></a>檢視工作詳細資料
執行下列步驟 tooview hello 詳細資料的任何作業的 hello。

#### <a name="tooview-job-details"></a>tooview 工作詳細資料
1. 在 tooyour StorSimple 裝置管理員服務的 **作業**。

2. 在 hello**作業**刀鋒視窗，顯示 hello 工作，您有興趣使用適當的篩選器執行查詢。 您可以搜尋完成、執行中或已取消工作。

    ![[作業] 刀鋒視窗](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. 選取並按一下 [作業]。

    ![[作業] 刀鋒視窗](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. 您可以在 hello 工作詳細資料 刀鋒視窗，檢視 hello 狀態、 詳細資料、 時間統計資料和資料的統計資料。
   
    ![工作詳細資料](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a>取消工作
執行下列步驟 toocancel 執行作業的 hello。

> [!NOTE]
> 某些工作，例如修改磁碟區 toochange hello 磁碟區類型，或展開磁碟區，無法取消。


### <a name="toocancel-a-job"></a>toocancel 作業
1. 在 hello**作業**頁面上，顯示 hello 執行工作的 toocancel 使用適當的篩選器執行查詢。 選取 hello 作業。

2. 以滑鼠右鍵按一下 hello 選取的作業 tooinvoke hello 操作功能表上，按一下 **取消**。

    ![工作詳細資料](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. 系統提示您進行確認時，按一下 [是] 。 即會取消此工作。

## <a name="next-steps"></a>後續步驟
* 了解如何太[管理您的 StorSimple 備份原則](storsimple-8000-manage-backup-policies-u2.md)。
* 了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。

