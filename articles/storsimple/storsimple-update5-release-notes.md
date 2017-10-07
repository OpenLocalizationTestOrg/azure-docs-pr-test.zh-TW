---
title: "aaaStorSimple 8000 系列 Update 5 版本資訊 |Microsoft 文件"
description: "StorSimple 8000 系列 Update 5 描述 hello 新功能、 問題和因應措施。"
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
ms.date: 08/23/2017
ms.author: alkohli
ms.openlocfilehash: 9eb8ffb97b41ce3d4f1ffdf2975f904d0a2958e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-5-release-notes"></a>StorSimple 8000 系列 Update 5 版本資訊

## <a name="overview"></a>概觀

hello 下列版本資訊說明 hello 新功能和識別 hello 重大議題 StorSimple 8000 系列 Update 5。 也會包含在此版本中所包含的 hello StorSimple 軟體更新清單。

Update 5 可以透過更新 4 中執行 Update 0.1 套用的 tooany StorSimple 裝置。 更新 5 與相關聯的 hello 裝置版本是 6.3.9600.17845。

檢閱附註，然後再部署 hello 更新您的 StorSimple 解決方案中的 hello 版本中所包含的 hello 資訊。

> [!IMPORTANT]
> * Update 5 有裝置軟體、磁碟韌體、作業系統安全性和其他作業系統更新。 它會採用大約 4 小時 tooinstall 這項更新。 磁碟韌體更新是干擾性更新，會導致您的裝置停機。 我們建議您套用更新 5 tookeep 您最新的裝置。
> * 新的版本，您可能不會看到更新立即，因為我們會執行 hello 更新分階段導入。 請等候數天然後再次掃描更新，因為很快就會提供這些更新。

## <a name="whats-new-in-update-5"></a>Update 5 的新功能

hello 下列索引鍵的改進和 bug 修正已進行更新 5 中。

* **使用具有 StorSimple 裝置管理員服務的 Azure Active Directory (AAD) tooauthenticate** – 從更新 5 及更新版本，Azure Active Directory 是一種使用的 tooauthenticate 與 hello StorSimple 裝置管理員服務。 將取代 2017 年 12 月 hello 舊的驗證機制。 Hello 的所有使用者都必須都包含在其防火牆規則的 hello 新驗證 Url。 如需詳細資訊，請移至太[驗證 Url 列在 StorSimple 裝置的網路需求的 hello](storsimple-8000-system-requirements.md#url-patterns-for-azure-portal)。

    如果 hello 驗證 URL 未包含在 hello 的防火牆規則，hello 使用者會看到他們的 StorSimple 裝置無法與 hello 服務驗證重大警示。 如果 hello 使用者看到此警示，它們需要 tooinclude hello 新驗證 URL。 如需詳細資訊，請移至太[StorSimple 網路警示](storsimple-8000-manage-alerts.md#networking-alerts)。

* **新的 StorSimple Snapshot Manager 版本** - Update 5 發行了新的 StorSimple Snapshot Manager 版本。 我們建議您更新 toothis 版本。 這個版本是相容的所有 hello StorSimple 裝置，會執行 Update 3 或更新版本。 如需詳細資訊，請移至太[部署 StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md)。


## <a name="issues-fixed-in-update-5"></a>Update 5 中修正的問題

hello 下表提供更新 5 中已修正的問題的摘要。

| 否 | 功能 | 問題 | 適用於 toophysical 裝置 | 適用於 toovirtual 裝置 |
| --- | --- | --- | --- | --- |
| 1 |Windows PowerShell 遠端處理 |在 hello 先前版本中，使用者會收到錯誤，在嘗試 tooestablish 遠端連線 toohello StorSimple 雲端應用裝置，透過 Windows PowerShell。 此版本已找出此問題的根本原因並加以修正。 |否 |是 |
| 2 |頻寬範本 |在較早版本中，發生問題導致比哪些 hello 裝置已設定為低頻寬的頻寬範本。 本版已經修正這個問題。 |是 |是 |
| 3 |容錯移轉 |在先前版本中，具有大量的磁碟區的裝置已容錯移轉執行 Update 4 tooanother 裝置時 hello 程序都會失敗時嘗試 tooapply hello 存取控制記錄。 此版本已經修正這個問題。 |是 |是 |



## <a name="known-issues-in-update-5-from-previous-releases"></a>Update 5 中舊版的已知問題

Update 5 中沒有新的已知問題。 如轉 tooUpdate 5 舊版問題的清單，請移至太[Update 3 版本資訊](storsimple-update3-release-notes.md#known-issues-in-update-3)。

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-5"></a>Update 5 中的序列連結 SCSI (SAS) 控制器和韌體更新

此版本包含 SAS 控制器和 LSI 驅動程式與韌體的更新。 如需有關如何 tooinstall 這些更新，請參閱[安裝更新 5](storsimple-8000-install-update-5.md) StorSimple 裝置上。

## <a name="storsimple-cloud-appliance-updates-in-update-5"></a>Update 5 中的 StorSimple 雲端設備更新 | Microsoft Docs

此更新不能套用的 toohello StorSimple 雲端應用裝置 （也稱為 hello 虛擬裝置）。 新的雲端應用裝置需要 toobe 使用 hello 更新 5 映像建立。 如需詳細資訊 toocreate StorSimple 雲端應用裝置中，跳過[部署和管理 StorSimple 雲端應用裝置](storsimple-8000-cloud-appliance-u2.md)。

## <a name="next-step"></a>後續步驟

了解如何太[安裝更新 5](storsimple-8000-install-update-5.md) StorSimple 裝置上。

