---
title: "aaaManage 您 StorSimple 備份原則 |Microsoft 文件"
description: "說明如何使用 hello StorSimple Manager 服務 toocreate，及管理手動備份、 備份排程，以及備份保留。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 4a2db707-bbfc-425c-bfeb-bc5c97781873
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 7b01f29a8d8a096d9890c8406557021317b9baff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies-update-2"></a>使用 hello StorSimple Manager 服務 toomanage 備份原則 (Update 2)
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a>概觀
本教學課程說明如何 toouse hello StorSimple Manager 服務**備份原則**toocontrol 備份程序和為您的 StorSimple 磁碟區的備份保留頁面上。 它也會說明如何 toocomplete 手動備份。

當您將備份磁碟區時，您可以選擇 toocreate 本機快照或雲端快照。 如果您正在備份固定在本機的磁碟區，我們建議您指定雲端快照。 拍下大量的固定在本機的磁碟區的本機快照，再加上具大量變換的資料集，將會導致本機空間很快就不足的情況。 如果您選擇 tootake 本機快照集時，我們建議您 hello 最新狀態會佔用較少的每日快照集 tooback，它們保留每日，然後再刪除它們。

當本機固定磁碟區的雲端快照，您可以複製只有變更的 hello 資料 toohello 雲端，它是重複資料刪除和壓縮。 

## <a name="hello-backup-policies-page"></a>hello 備份原則 頁面
hello**備份原則**頁面可讓您 toomanage 備份原則排程本機和雲端快照。 （備份原則是使用的 tooconfigure 備份排程和備份保留磁碟區的集合）。備份原則可讓您的多個磁碟區快照集 tootake 同時。 這表示建立的備份原則的 hello 備份將會損毀一致的複本。 hello**備份原則**hello 備份原則、 其類型、 相關聯的 hello 磁碟區、 hello 數目的備份保留，頁面會列出與 hello 選項 tooenable 這些原則。

hello**備份原則**頁面也可讓您 toofilter hello 現有的備份原則的一或多個 hello 下列欄位：

* **原則名稱**– hello 與 hello 原則相關聯的名稱。 hello 不同類型的原則包括：
  
  * 排程的原則，由 hello 使用者明確建立。
  * 自動原則，會建立 hello 這個磁碟區選項的預設備份的磁碟區建立 hello 次啟用時。 這些原則會命名為*VolumeName*_Default 其中*VolumeName*參考 toohello hello hello Azure 傳統入口網站中的 hello 使用者所設定的 StorSimple 磁碟區名稱。 hello 自動原則會導致每日開始時間 22:30 裝置的雲端快照集。
  * 匯入原則，最初建立於 hello StorSimple Snapshot Manager。 這些具有描述 hello 原則匯入從 hello StorSimple Snapshot Manager 主控件的標記。
* **磁碟區**– hello 與 hello 原則相關聯的磁碟區。 建立備份時，會一起分組與備份原則相關聯的所有 hello 磁碟區。
* **上次成功備份**– hello 的日期和時間 hello 最後一個成功備份與此原則。
* **下一次備份**– hello 的日期和時間 hello 下一個排定的備份將會起始此原則。
* **排程**– hello 的 hello 備份原則相關聯的排程數目。

您可以從這個頁面上執行的常用的 hello 作業為：

* 新增備份原則 
* 新增或修改排程 
* 刪除備份原則 
* 進行手動備份 
* 建立具有多個磁碟區和排程的自訂備份原則 

## <a name="add-a-backup-policy"></a>新增備份原則
加入備份原則 tooautomatically 排程備份。 執行下列步驟在 hello Azure 傳統入口網站 tooadd StorSimple 裝置的備份原則中的 hello。 您將加入 hello 原則之後，您可以定義排程 (請參閱[新增或修改排程](#add-or-modify-a-schedule))。

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

![提供的影片](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **提供的影片**

toowatch 的視訊示範 toocreate 本機或雲端備份原則，按一下[這裡](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/)。

## <a name="add-or-modify-a-schedule"></a>新增或修改排程
您可以新增或修改附加的 tooan 備份原則存在您的 StorSimple 裝置上的排程。 執行下列步驟在 hello Azure 傳統入口網站 tooadd hello 或修改排程。

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a>刪除備份原則
執行 hello 遵循您的 StorSimple 裝置上 hello Azure 傳統入口網站 toodelete 備份原則中的步驟。

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>進行手動備份
執行下列步驟，在單一磁碟區的 hello Azure 傳統入口網站 toocreate 隨 （手動） 備份中的 hello。

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a>建立具有多個磁碟區和排程的自訂備份原則
執行下列步驟在 hello Azure 傳統入口網站 toocreate 具有多個磁碟區和排程的自訂備份原則中的 hello。

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a>後續步驟
深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。

