---
title: "在您的 StorSimple 裝置上的 Update 2 aaaInstall |Microsoft 文件"
description: "說明如何在您的 StorSimple 8000 系列裝置 tooinstall StorSimple 8000 系列 Update 2。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8c8981df-75d9-4d19-b137-d6c6ba39dcfb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 33a0bea4358c944644563192f686af332d2ad7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a>在 StorSimple 裝置上安裝 Update 2
## <a name="overview"></a>概觀
本教學課程說明如何 tooinstall 更新 2 透過 hello Azure 傳統入口網站中執行較早的版本的 StorSimple 裝置上。 hello 教學課程也涵蓋 hello 閘道設定成以外的 hello StorSimple 裝置的 DATA 0 網路介面上，且您嘗試更新前 1 軟體版本從 tooupdate hello 更新所需的步驟。

Update 2 包括裝置軟體更新、LSI 驅動程式更新和磁碟韌體更新。 hello 裝置軟體和 LSI 更新非干擾性更新，並透過 hello Azure 傳統入口網站，可以套用。 hello 磁碟韌體更新更新具有干擾性，並只能透過 hello 裝置 hello Windows PowerShell 介面套用。

> [!IMPORTANT]
> * 您可能不會看到更新 2 立即，因為我們會執行 hello 更新分階段導入。 請在數天內再次掃描更新，因為很快就會提供 Update。
> * 一組預先手動與自動檢查已完成先前 toohello 安裝 toodetermine hello 裝置健全狀況方面硬體狀態和網路連線。 只有當您從 Azure 傳統入口網站 hello 套用 hello 更新時，才執行這些前置檢查。
> * 我們建議您安裝 hello 軟體，並透過的驅動程式更新 hello Azure 傳統入口網站。 如果 hello 入口網站中的 hello 更新前閘道檢查失敗，應該只會順著 hello 裝置 （tooinstall 更新） toohello Windows PowerShell 介面。 hello 更新可能需要 4-7 小時 tooinstall （包括 hello Windows 更新）。 hello 維護模式更新必須透過 hello 裝置 hello Windows PowerShell 介面安裝。 由於維護模式更新是干擾性更新，它們將會導致裝置的停機時間。
> * 如果執行 hello 選擇性 StorSimple Snapshot Manager，請確定您已升級 Snapshot Manager 版本 tooUpdate 2 先前 tooupdating hello 裝置。
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-hello-azure-classic-portal"></a>透過 hello Azure 傳統入口網站安裝 Update 2
執行下列步驟 tooupdate hello 裝置太[Update 2](storsimple-update2-release-notes.md)。

> [!NOTE]
> Update 2 讓 Microsoft toopull 其他診斷資訊從裝置 hello。 如此一來，當我們作業小組會識別發生問題的裝置，我們會更好的配備的 toocollect 資訊從裝置 hello 和診斷問題。 接受 Update 2 中，您允許我們 tooprovide 主動式這項支援。
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. 驗證您的裝置正在執行 **StorSimple 8000 系列 Update 2 (6.3.9600.17673)**。 hello**上次更新日期**也應修改。 您也會看到維護模式更新可供使用 （此訊息可能會繼續顯示總 too24 安裝之後的小時 hello 更新 toobe）。
   
   維護模式更新會導致裝置停機時間，且只能透過您的裝置 hello Windows PowerShell 介面套用干擾性更新。 在某些情況下當您執行更新 1.2、 磁碟韌體可能已經是最新狀態，在此情況下，您不需要 tooinstall 任何維護模式更新。
2. 使用 hello 中所列的步驟來下載 hello 維護模式更新[toodownload hotfix](#to-download-hotfixes)如 toosearch 並下載 KB3121899，這會安裝磁碟韌體更新 （hello 其他更新應該已經安裝到目前為止）。
3. 中所列步驟 hello[安裝，並確認 維護模式 hotfix](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello 維護模式更新。

## <a name="install-update-2-as-a-hotfix"></a>以 Hotfix 的方式安裝 Update 2
如果您無法 hello 閘道核取時，嘗試透過 hello Azure 傳統入口網站的 tooinstall hello 更新，請使用此程序。 hello 檢查失敗，因為您已指派 tooa 非 DATA 0 網路介面閘道和您的裝置正在執行軟體版本先前 tooUpdate 1。

hello 軟體版本，可以使用 hello hotfix 方法來升級為更新 0.1、 更新 0.2，和 Update 0.3、 更新 1、 更新 1.1 和更新 1.2。 hello hotfix 方法牽涉到下列三個步驟的 hello:

* 從 Microsoft Update 類別目錄 hello 下載 hello hotfix。
* 安裝並確認 hello 一般模式 hotfix。
* 安裝並確認 hello 維護模式 hotfix。

tooinstall Update 2，以 hotfix 的形式，您必須下載並安裝下列 hotfix hello:

| 順序 | KB | 說明 | 更新類型 |
| --- | --- | --- | --- |
| 1 |KB3121901 |軟體更新 |定期 |
| 2 |KB3121900 |LSI 驅動程式 |定期 |
| 3 |KB3080728 |Storport 修正程式  </br> Windows Server 2012 R2 |定期 |
| 4 |KB3090322 |Spaceport 修正程式  </br> Windows Server 2012 R2 |定期 |
| 5 |KB3121899 |磁碟韌體 |維護  |

> [!IMPORTANT]
> * 如果您的裝置正在執行版本 (GA) 版本，請連絡[Microsoft 支援服務](storsimple-contact-microsoft-support.md)tooassist hello 與更新。
> * 此程序需求 toobe 只能執行一次 tooapply Update 2。 您可以使用 hello Azure 傳統入口網站 tooapply 後續更新。
> * 每個的 hotfix 安裝可能需要約 20 分鐘 toocomplete。 總計的安裝時間是關閉 too2 小時。
> * 使用此程序 tooapply hello 前更新，請確定兩個裝置控制器都在線上，而且所有 hello 硬體元件都均狀況良好。
> 
> 

執行下列步驟 tooapply hello 這個更新以 hotfix 的形式。

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>後續步驟
深入了解 hello [Update 2 版本](storsimple-update2-release-notes.md)。

