---
title: "aaaView 及管理 StorSimple 作業 |Microsoft 文件"
description: "描述 hello StorSimple Manager 服務作業 頁面以及 toouse 它 tootrack 最近、 目前和已排程備份工作。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a>使用 hello StorSimple Manager 服務 tooview 及管理 StorSimple 工作 (Update 2)
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a>概觀
hello**作業**頁面會提供單一中央入口網站檢視和管理裝置所啟動的工作連接 tooyour StorSimple Manager 服務。 您可以針對多個裝置，檢視已排程、執行中、完成、已取消和失敗的工作。 結果會以表格式格式呈現。 

![[工作] 頁面](./media/storsimple-manage-jobs-u2/jobs.png)

您可以快速尋找您感興趣的這類的欄位進行篩選的 hello 工作：

* **狀態** – 工作可以是執行中、完成、已取消、失敗、取消中，或是完成但發生錯誤。
* **From 和 To** – 工作可以篩選根據的 hello 日期和時間範圍。
* **型別**– hello 工作類型可以是備份、 手動備份、 還原、 複製、 裝置容錯移轉，建立本機固定磁碟區、 修改磁碟區、 更新、 支援套件，或虛擬裝置佈建。
* **裝置**– 特定連接裝置 tooyour 服務上起始工作。
  hello 已篩選的工作會再製成資料表的下列屬性的 hello hello 基礎：
  
  * **類型** – 備份、手動備份、還原、複製、裝置容錯移轉、建立固定在本機的磁碟區、修改磁碟區、更新、支援封裝，或佈建虛擬裝置。
  * **狀態** – 執行中、完成、已取消、失敗、取消中，或是完成但發生錯誤。
  * **實體**– hello 工作可以與磁碟區、 備份原則或裝置產生關聯。 例如，複製工作與磁碟區相關聯，而排程的備份工作則與備份原則相關聯。 裝置工作是透過災害復原 (DR) 或還原作業而建立。
  * **裝置**– hello hello 裝置的 hello 已啟動工作的名稱。
  * **在啟動**– hello hello 作業啟動時的時間。
  * **進度**– hello 執行工作的完成百分比。 對於完成的工作，百分比應該永遠是 100%。

hello 工作清單會重新整理每隔 30 秒。

您可以執行下列作業相關的動作，此頁面上的 hello:

* 檢視工作詳細資料
* 取消工作

## <a name="view-job-details"></a>檢視工作詳細資料
執行下列步驟 tooview hello 詳細資料的任何作業的 hello。

#### <a name="tooview-job-details"></a>tooview 工作詳細資料
1. 在 hello**作業**頁面上，顯示您有興趣使用適當的篩選器執行查詢的 hello 工作。 您可以搜尋完成、執行中或已取消工作。
2. 選取一個工作。
3. 在 hello hello 頁面底部，按一下**詳細資料**。
4. 在 hello**備份工作詳細資料**對話方塊中，您可以檢視 hello 狀態、 詳細資料、 時間統計資料，以及資料的統計資料。
   
    ![工作詳細資料頁面](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a>取消工作
執行下列步驟 toocancel 執行作業的 hello。

> [!NOTE]
> 某些工作，例如修改磁碟區 toochange hello 磁碟區類型，或展開磁碟區，無法取消。
> 
> 

### <a name="toocancel-a-job"></a>toocancel 作業
1. 在 hello**作業**頁面上，顯示 hello 執行工作的 toocancel 使用適當的篩選器執行查詢。
2. 選取 hello 作業。
3. 在 hello hello 頁面底部，按一下**取消**。
4. 系統提示您進行確認時，按一下 [是] 。

即會取消此工作。

## <a name="next-steps"></a>後續步驟
* 了解如何太[管理您的 StorSimple 備份原則](storsimple-manage-backup-policies.md)。
* 了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。

