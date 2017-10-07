---
title: "Snapshot Manager 系統管理 aaaStorSimple |Microsoft 文件"
description: "提供概觀，以及連結 toomore StorSimple Snapshot Manager 解決方案管理工作和工作流程資訊。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 1cdbb61d-bd16-4be4-ade2-ceab11508acb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2016
ms.author: v-sharos
ms.openlocfilehash: d875f2efbdeb844b412cf8d9f1f971f18da7526e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooadminister-your-storsimple-solution"></a>使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister

## <a name="overview"></a>概觀
StorSimple Snapshot Manager 是 Microsoft Management Console (MMC) 嵌入式管理單元，可簡化資料保護和備份管理 Microsoft Azure StorSimple 環境中。 使用 StorSimple Snapshot Manager 中，您可以管理在 hello 資料中心和 hello 雲端的 Microsoft Azure StorSimple 資料做為單一整合式儲存體解決方案，因而簡化備份程序，並降低成本。

hello StorSimple Snapshot Manager 中央管理主控台可讓您 toocreate 一致，時間點備份複本的本機和雲端資料。 例如，您可以使用 hello 主控台：

* 設定、備份及刪除磁碟區。
* 設定磁碟區群組 tooensure 該備份資料是應用程式一致。
* 管理備份原則，以便在預先決定的排程上備份資料。
* 建立獨立的資料複本，它可以儲存在 hello 雲端並用於災害復原。

本文章提供描述 StorSimple Snapshot Manager 的連結 tootutorials 以及 toouse 它 toocomplete 系統管理工作和工作流程。

* 如需有關 StorSimple Snapshot Manager 元件和架構的詳細資訊，請參閱 [什麼是 StorSimple Snapshot Manager？](storsimple-what-is-snapshot-manager.md) 
* toodownload StorSimple Snapshot Manager，跳過[hello StorSimple Snapshot Manager 下載頁面](https://www.microsoft.com/download/details.aspx?id=44220)。
* StorSimple Snapshot Manager 部署程序，跳過[部署 StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md)。

> [!NOTE]
> 您無法使用 StorSimple Snapshot Manager toomanage Microsoft Azure StorSimple 虛擬陣列 （也稱為 StorSimple 內部部署虛擬裝置）。


## <a name="storsimple-snapshot-manager-tasks-and-workflows"></a>StorSimple Snapshot Manager 工作和工作流程
您可以使用 hello StorSimple Snapshot Manager toomonitor 和管理目前、 排程，以及完成備份工作。 此外，StorSimple Snapshot Manager 提供 too64 完成備份的目錄。 您可以使用 hello 目錄 toofind 並還原磁碟區或個別檔案。 

| 如果您想要 tooDO THIS... | 使用本教學課程... |
|:--- |:--- |
| 深入了解 StorSimple Snapshot Manager |[什麼是 StorSimple Snapshot Manager？ ](storsimple-what-is-snapshot-manager.md) |
| 安裝 StorSimple Snapshot Manager<br>重新安裝 StorSimple Snapshot Manager<br>移除 StorSimple Snapshot Manager |[部署 StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md) |
| 使用 StorSimple Snapshot Manager 功能表和功能：<ul><li>功能表列</li><li>工具列</li><li>範圍窗格</li><li>結果窗格</li><li>動作窗格</li><li>鍵盤瀏覽和快速鍵</li></ul> |[StorSimple Snapshot Manager 使用者介面](storsimple-use-snapshot-manager.md) |
| 使用 hello 包含 StorSimple Snapshot Manager 中常見 MMC 功能：<ul><li>檢視</li><li>從這裡開啟新視窗</li><li>重新整理</li><li>匯出清單</li><li>說明</li></ul> |[StorSimple Snapshot Manager 中使用 hello MMC 功能表動作](storsimple-snapshot-manager-mmc-menu.md) |
| 新增或更換裝置<br>連接裝置<br>確認匯入的磁碟區群組<br>重新整理已連接的裝置<br>驗證裝置<br>檢視裝置詳細資料<br>刪除裝置組態<br>變更裝置密碼<br>更換故障的裝置<br> |[使用 StorSimple Snapshot Manager tooconnect 和管理 StorSimple 裝置](storsimple-snapshot-manager-manage-devices.md) |
| 掛接磁碟區<br>檢視磁碟區的相關資訊<br>刪除磁碟區<br>重新掃描磁碟區<br>設定和備份基本磁碟區<br>設定及備份動態鏡像磁碟區 |[使用 StorSimple Snapshot Manager tooview 及管理磁碟區](storsimple-snapshot-manager-manage-volumes.md) |
| 檢視磁碟區群組<br>建立磁碟區群組<br>備份磁碟區群組<br>編輯磁碟區群組<br>刪除磁碟區群組 |[使用 StorSimple Snapshot Manager toocreate 及管理磁碟區群組](storsimple-snapshot-manager-manage-volume-groups.md) |
| 建立備份原則 <br>編輯備份原則<br>刪除備份原則 |[使用 StorSimple Snapshot Manager toocreate 及管理備份原則](storsimple-snapshot-manager-manage-backup-policies.md) |
| 檢視和管理排程的備份工作<br>檢視和管理最近的備份作業<br>檢視和管理目前正在執行的備份工作 |[使用 StorSimple Snapshot Manager tooview 及管理備份工作](storsimple-snapshot-manager-manage-backup-jobs.md) |
| 還原磁碟區<br>複製磁碟區或磁碟區群組<br>刪除備份<br>復原檔案<br>還原 hello StorSimple Snapshot Manager 資料庫 |[使用 StorSimple Snapshot Manager toomanage hello 備份類別目錄](storsimple-snapshot-manager-manage-backup-catalog.md) |

## <a name="next-steps"></a>後續步驟
[下載 StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220)。

