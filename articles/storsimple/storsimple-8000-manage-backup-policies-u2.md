---
title: "aaaManage StorSimple 8000 系列的備份原則 |Microsoft 文件"
description: "說明如何使用 hello StorSimple 裝置管理員服務 toocreate，及管理手動備份、 備份排程，以及備份保留在 StorSimple 8000 系列裝置上。"
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a>在 Azure 入口網站 toomanage 備份原則中使用 hello StorSimple 裝置管理員服務


## <a name="overview"></a>概觀

本教學課程說明如何 toouse hello StorSimple 裝置管理員服務**備份原則**刀鋒視窗 toocontrol 備份程序和備份保留您的 StorSimple 磁碟區。 它也會說明如何 toocomplete 手動備份。

當您將備份磁碟區時，您可以選擇 toocreate 本機快照或雲端快照。 如果您正在備份固定在本機的磁碟區，我們建議您指定雲端快照。 拍下大量的固定在本機的磁碟區的本機快照，再加上具大量變換的資料集，將會導致本機空間很快就不足的情況。 如果您選擇 tootake 本機快照集時，我們建議您 hello 最新狀態會佔用較少的每日快照集 tooback，它們保留每日，然後再刪除它們。

當本機固定磁碟區的雲端快照，您可以複製只有變更的 hello 資料 toohello 雲端，它是重複資料刪除和壓縮。

## <a name="hello-backup-policy-blade"></a>hello 備份原則 刀鋒視窗

hello**備份原則**StorSimple 裝置的刀鋒視窗可讓您 toomanage 備份原則排程本機和雲端快照。 備份原則不使用的 tooconfigure 備份排程和備份保留的磁碟區集合。 備份原則可讓您的多個磁碟區快照集 tootake 同時。 這表示建立的備份原則的 hello 備份將會損毀一致的複本。

hello 備份原則的表格式清單也可讓您 toofilter hello 現有的備份原則由一或多個 hello 下列欄位：

* **原則名稱**– hello 與 hello 原則相關聯的名稱。 hello 不同類型的原則包括：

  * 排程的原則，由 hello 使用者明確建立。
  * 匯入原則，最初建立於 hello StorSimple Snapshot Manager。 這些具有描述 hello 原則匯入從 hello StorSimple Snapshot Manager 主控件的標記。

  > [!NOTE]
  > 在建立磁碟區的 hello 階段不再啟用自動] 或 [預設的備份原則。

* **上次成功備份**– hello 的日期和時間 hello 最後一個成功備份與此原則。

* **下一次備份**– hello 的日期和時間 hello 下一個排定的備份將會起始此原則。

* **磁碟區**– hello 與 hello 原則相關聯的磁碟區。 建立備份時，會一起分組與備份原則相關聯的所有 hello 磁碟區。

* **排程**– hello 的 hello 備份原則相關聯的排程數目。

您可以執行的備份原則的 hello 常用作業為：

* 新增備份原則
* 新增或修改排程
* 新增或移除磁碟區
* 刪除備份原則
* 進行手動備份

## <a name="add-a-backup-policy"></a>新增備份原則

加入備份原則 tooautomatically 排程備份。 當您第一次建立磁碟區時，沒有與您的磁碟區相關聯的預設備份原則。 您需要 tooadd，並指定備份原則 tooprotect 磁碟區資料。

執行下列步驟在 hello Azure 入口網站 tooadd StorSimple 裝置的備份原則中的 hello。 您將加入 hello 原則之後，您可以定義排程 (請參閱[新增或修改排程](#add-or-modify-a-schedule))。

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a>新增或修改排程

您可以新增或修改附加的 tooan 備份原則存在您的 StorSimple 裝置上的排程。 執行下列步驟，在 Azure 入口網站 tooadd hello hello 或修改排程。

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a>新增或移除磁碟區

您可以新增或移除磁碟區指派 tooa StorSimple 裝置上的備份原則。 執行下列步驟，在 Azure 入口網站 tooadd hello hello 或移除磁碟區。

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a>刪除備份原則

執行 hello 遵循您的 StorSimple 裝置上 hello Azure 入口網站 toodelete 備份原則中的步驟。

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>進行手動備份

執行下列步驟，在單一磁碟區的 hello Azure 入口網站 toocreate 隨 （手動） 備份中的 hello。

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>後續步驟

深入了解[使用您的 StorSimple 裝置 hello StorSimple 裝置管理員服務 tooadminister](storsimple-8000-manager-service-administration.md)。

