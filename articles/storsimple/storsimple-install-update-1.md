---
title: "在您的 StorSimple 裝置上的更新 1.2 aaaInstall |Microsoft 文件"
description: "說明如何在您的 StorSimple 8000 系列裝置 tooinstall StorSimple 8000 系列 Update 1.2。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 7a513923-eb77-4078-b0ab-f8e90183796a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0a7601dc0b1ce60eb854227243ecb02d6fb2c678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-12-on-your-storsimple-8000-series-device"></a>在 StorSimple 8000 系列裝置上安裝 Update 1.2
## <a name="overview"></a>概觀
本教學課程說明如何 tooinstall 更新 1.2 執行軟體版本先前 tooUpdate 1 在 StorSimple 裝置。 hello 教學課程也涵蓋 hello hello 更新以外的 hello StorSimple 裝置的 DATA 0 網路介面上設定閘道時所需的額外步驟。

Update 1.2 包括裝置軟體更新、LSI 驅動程式更新和磁碟韌體更新。 hello 軟體和 LSI 驅動程式更新非干擾性更新，所以可以套用透過 hello Azure 傳統入口網站。 hello 磁碟韌體更新更新具有干擾性，並只能透過 hello 裝置 hello Windows PowerShell 介面套用。

根據正在執行的裝置版本，您可以判斷是否套用 Update 1.2。 您可以檢查您的裝置 hello 軟體版本，瀏覽 toohello**快速概覽**> 一節，您的裝置**儀表板**。

</br>

| 如果執行的軟體版本... | Hello 入口網站中會發生什麼事？ |
| --- | --- |
| Release - GA |如果您正在執行 Release 版本 (GA)，請勿套用此更新。 請[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)tooupdate 您的裝置。 |
| Update 0.1 |入口網站套用 Update 1.2。 |
| Update 0.2 |入口網站套用 Update 1.2。 |
| Update 0.3 |入口網站套用 Update 1.2。 |
| Update 1 |此更新將無法使用。 |
| Update 1.1 |此更新將無法使用。 |

</br>

> [!IMPORTANT]
> * 您可能不會看到更新 1.2 立即，因為我們會執行 hello 更新分階段導入。 請在數天內再次掃描更新，因為很快就會提供 Update。
> * 此更新包括手動和自動預先檢查 toodetermine hello 裝置的健全狀況方面硬體狀態和網路連線的一組。 只有當您從 Azure 傳統入口網站 hello 套用 hello 更新時，才執行這些前置檢查。
> * 我們建議您安裝 hello 軟體，並透過的驅動程式更新 hello Azure 傳統入口網站。 如果 hello 入口網站中的 hello 更新前閘道檢查失敗，應該只會順著 hello 裝置 （tooinstall 更新） toohello Windows PowerShell 介面。 hello 更新可能需要 5-10 小時 tooinstall （包括 hello Windows 更新）。 hello 維護模式更新必須透過 hello 裝置 hello Windows PowerShell 介面安裝。 由於維護模式更新是干擾性更新，它們將會導致裝置的停機時間。
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-12-via-hello-azure-classic-portal"></a>安裝更新 1.2 透過 hello Azure 傳統入口網站
執行下列步驟 tooupdate hello 裝置太[更新 1.2](storsimple-update1-release-notes.md)。 只有當您在裝置上的 DATA 0 網路介面上設定閘道器時才使用此程序。

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. 確認您的裝置是否正在執行 **StorSimple 8000 Series Update 1.2 (6.3.9600.17584)**。 hello**上次更新日期**也應修改。 您也會看到維護模式更新可供使用 （此訊息可能會繼續顯示總 too24 安裝之後的小時 hello 更新 toobe）。
   
   維護模式更新會導致裝置停機時間，且只能透過您的裝置 hello Windows PowerShell 介面套用干擾性更新。
   
   ![維護頁面](./media/storsimple-install-update-1/InstallUpdate12_10M.png "維護頁面")
2. 使用 hello 中所列的步驟來下載 hello 維護模式更新[toodownload hotfix](#to-download-hotfixes)如 toosearch 並下載 KB3063416，這會安裝磁碟韌體更新 （hello 其他更新應該已經安裝到目前為止）。
3. 中所列步驟 hello[安裝，並確認 維護模式 hotfix](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello 維護模式更新。
4. 在 hello Azure 傳統入口網站中瀏覽 toohello**維護**頁面，然後在 hello hello 頁面底部，按一下**掃描更新**toocheck 的任何 Windows 更新，然後按一下**安裝更新**. 您已完成在所有的 hello 成功安裝更新。

## <a name="install-update-12-on-a-device-that-has-a-gateway-configured-for-a-non-data-0-network-interface"></a>在含有為非 DATA 0 網路介面設定之閘道器的裝置上安裝 Update 1.2
只有當您檢查無法通過 hello 閘道嘗試 tooinstall hello 更新 hello Azure 傳統入口網站時，您應該使用此程序。 hello 檢查失敗，因為您已指派 tooa 非 DATA 0 網路介面閘道和您的裝置正在執行軟體版本先前 tooUpdate 1。 如果您的裝置上的非 DATA 0 網路介面沒有閘道，您可以更新您的裝置直接從 hello Azure 傳統入口網站。 請參閱[透過 hello Azure 傳統入口網站安裝更新 1.2](#install-update-1.2-via-the-azure-classic-portal)。

hello 軟體版本，可以使用這個方法來升級為更新 0.1，更新 0.2 和 Update 0.3。

> [!IMPORTANT]
> * 如果您的裝置正在執行版本 (GA) 版本，請連絡[Microsoft 支援服務](storsimple-contact-microsoft-support.md)tooassist hello 與更新。
> * 此程序需求 toobe 只能執行一次 tooapply 更新 1.2。 您可以使用 hello Azure 傳統入口網站 tooapply 後續更新。
> 
> 

如果您的裝置正在執行更新前 1 軟體，而且它有一組不同於 DATA 0 網路介面閘道，您可以在 hello 下列兩種方式套用更新 1.2:

* **選項 1**： 下載 hello 更新，並將它套用使用 hello `Start-HcsHotfix` cmdlet 從 hello 裝置 hello Windows PowerShell 介面。 這是 hello 建議使用的方法。 **如果您的裝置正在執行更新 1.0 或更新 1.1，請勿使用此方法 tooapply 更新 1.2。**
* **選項 2**： 移除 hello 閘道組態和安裝 hello 直接從 hello Azure 傳統入口網站的更新。

Hello 下列各節提供每個詳細的指示。

## <a name="option-1-use-windows-powershell-for-storsimple-tooapply-update-12-as-a-hotfix"></a>選項 1： 使用 Windows PowerShell for StorSimple tooapply 更新 1.2 以 hotfix 的形式
只有在您執行更新 0.1，0.2、 0.3，所以如果您的閘道簽入失敗嘗試 tooinstall 更新從 hello Azure 傳統入口網站時，您應該使用此程序。 如果您正在執行軟體版本 (GA)，請[Microsoft 支援服務](storsimple-contact-microsoft-support.md)tooupdate 您的裝置。

tooinstall 更新 1.2 以 hotfix 的形式，您必須下載並安裝下列 hotfix hello:

| 順序 | KB | 說明 | 更新類型 |
| --- | --- | --- | --- |
| 1 |KB3063418 |軟體更新 |定期 |
| 2 |KB3043005 |LSI SAS 控制器更新 |定期 |
| 3 |KB3063416 |磁碟韌體 |維護  |

使用此程序 tooapply hello 前更新，請確定：

* 這兩個裝置控制器都在線上。

執行下列步驟 tooapply 更新 1.2 hello。 **hello 更新可能需要大約 2 小時 toocomplete （大約 30 分鐘的軟體，30 分鐘的時間驅動程式，如磁碟韌體 45 分鐘內）。**

[!INCLUDE [storsimple-install-update-option1](../../includes/storsimple-install-update-option1.md)]

## <a name="option-2-use-hello-azure-classic-portal-tooapply-update-12-after-removing-hello-gateway-configuration"></a>選項 2： 使用 Azure 傳統入口網站 tooapply 更新 1.2 hello 移除 hello 閘道設定之後
此程序適用於正在執行軟體版本先前 tooUpdate 1，且有不同於 DATA 0 網路介面上設定的閘道 tooStorSimple 裝置。 您將需要 tooclear hello 閘道設定先前 tooapplying hello 更新。

hello 更新可能需要幾小時 toocomplete。 如果您的主機位於不同子網路，移除 hello hello iSCSI 介面上的閘道設定可能會導致停機時間。 我們建議您在 iSCSI 流量 tooreduce hello 停機時間的設定資料 0。

執行下列步驟 toodisable hello 與 hello 閘道的網路介面的 hello，然後套用 hello 更新。

[!INCLUDE [storsimple-install-update-option2](../../includes/storsimple-install-update-option2.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>後續步驟
深入了解 hello[更新 1.2 版本](storsimple-update1-release-notes.md)。

