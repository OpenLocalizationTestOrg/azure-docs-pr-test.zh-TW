---
title: "在您的 StorSimple 裝置上的更新 2.2 aaaInstall |Microsoft 文件"
description: "說明如何在您的 StorSimple 8000 系列裝置 tooinstall StorSimple 8000 系列 Update 2.2。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 047c7a4b-73d0-45ea-8d51-c54d71871392
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/02/2016
ms.author: alkohli
ms.openlocfilehash: cedb83ce42bc6bb81a4e43345da3f25b71036d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-22-on-your-storsimple-device"></a>在 StorSimple 裝置上安裝 Update 2.2
## <a name="overview"></a>概觀
本教學課程說明如何在執行較舊的軟體版本，透過 StorSimple 裝置上的更新 2.2 tooinstall hello Azure 傳統入口網站，並使用 hello hotfix 方法。 不同於 hello StorSimple 裝置的 DATA 0 網路介面上已設定閘道和您嘗試更新前 1 軟體版本從 tooupdate 時使用 hello hotfix 方法。

Update 2.2 包括裝置軟體、WMI 及 iSCSI 更新。 如果從 2.1 版的更新，只有 hello 裝置的軟體更新必須套用 toobe。 如果更新從更新前 2 的版本，您也會需要的 tooapply LSI 驅動程式、 太空、 Storport，與磁碟韌體更新。 hello 裝置軟體、 WMI、 iSCSI、 LSI 驅動程式、 太空和 Storport 修正非干擾性更新作業，而且可以透過 hello Azure 傳統入口網站套用。 hello 磁碟韌體更新更新具有干擾性，並只能透過 hello 裝置 hello Windows PowerShell 介面套用。 

> [!IMPORTANT]
> * 一組預先手動與自動檢查已完成先前 toohello 安裝 toodetermine hello 裝置健全狀況方面硬體狀態和網路連線。 只有當您從 Azure 傳統入口網站 hello 套用 hello 更新時，才執行這些前置檢查。
> * 我們建議您安裝 hello 軟體，並透過的驅動程式更新 hello Azure 傳統入口網站。 如果 hello 入口網站中的 hello 更新前閘道檢查失敗，應該只會順著 hello 裝置 （tooinstall 更新） toohello Windows PowerShell 介面。 您正在從 hello 版本而定，hello 更新可能需要 1.5-2.5 小時 tooinstall。 hello 維護模式更新必須透過 hello 裝置 hello Windows PowerShell 介面安裝。 由於維護模式更新是干擾性更新，它們將會導致裝置的停機時間。
> * 如果執行 hello 選擇性 StorSimple Snapshot Manager，請確定您已升級 Snapshot Manager 版本 tooUpdate 2.2 先前 tooupdating hello 裝置。
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-22-via-hello-azure-classic-portal"></a>安裝更新 2.2 透過 hello Azure 傳統入口網站
執行下列步驟 tooupdate hello 裝置太[更新 2.2](storsimple-update21-release-notes.md)。

> [!NOTE]
> 如果您要套用 Update 2 或更新版本 （包括 Update 2.1)，Microsoft 將會無法 toopull 其他診斷的資訊從裝置 hello。 如此一來，當我們作業小組會識別發生問題的裝置，我們會更好的配備的 toocollect 資訊從裝置 hello 和診斷問題。 接受更新 2 或更新版本，您允許我們 tooprovide 主動式這項支援。
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. 確認您裝置執行的是 **StorSimple 8000 系列 2.2 (6.3.9600.17708)**。 hello**上次更新日期**也應修改。 
   
   如果您要更新的版本先前 tooUpdate 2，您也會看到 hello 維護模式更新可供使用 （此訊息可能會繼續顯示總 too24 安裝之後的小時 hello 更新 toobe）。
   
   維護模式更新會導致裝置停機時間，且只能透過您的裝置 hello Windows PowerShell 介面套用干擾性更新。 在某些情況下當您執行更新 1.2、 磁碟韌體可能已經是最新狀態，在此情況下，您不需要 tooinstall 任何維護模式更新。
   
   如果您是從 Update 2 更新，您的裝置現在應該是最新狀態。 您可以略過 hello 剩餘步驟。
2. 使用 hello 中所列的步驟來下載 hello 維護模式更新[toodownload hotfix](#to-download-hotfixes)如 toosearch 並下載 KB3121899，這會安裝磁碟韌體更新 （hello 其他更新應該已經安裝到目前為止）。
3. 中所列步驟 hello[安裝，並確認 維護模式 hotfix](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello 維護模式更新。 

## <a name="install-update-22-as-a-hotfix"></a>以 Hotfix 的方式安裝 Update 2.2
如果您無法 hello 閘道核取時，嘗試透過 hello Azure 傳統入口網站的 tooinstall hello 更新，請使用此程序。 hello 檢查失敗，因為您已指派 tooa 非 DATA 0 網路介面閘道和您的裝置正在執行軟體版本先前 tooUpdate 1。

可以使用 hello hotfix 方法來升級的 hello 軟體版本如下：

* Update 0.1、0.2、0.3
* Update 1、1.1、1.2
* Update 2、2.1 

> [!IMPORTANT]
> * 如果您的裝置正在執行版本 (GA) 版本，請連絡[Microsoft 支援服務](storsimple-contact-microsoft-support.md)tooassist hello 與更新。
> 
> 

hello hotfix 方法牽涉到下列三個步驟的 hello:

* 從 Microsoft Update 類別目錄 hello 下載 hello hotfix。
* 安裝並確認 hello 一般模式 hotfix。
* 安裝並確認 hello 維護模式 hotfix （只有在從更新前 2 的軟體更新）。

#### <a name="download-updates-for-a-device-running-update-21-software"></a>下載適用於執行 Update 2.1 軟體之裝置的更新
**如果您的裝置正在執行更新 2.1**，您必須下載只有 hello 裝置軟體更新 KB3179904。 只安裝 hello 二進位檔案做為 ' all hcsmdssoftwareudpate' 開頭。 未安裝 hello Ci 且 hello MDS 代理程式更新前面加上`all-cismdsagentupdatebundle`。 失敗 toodo 因此將會導致錯誤。 這是在非干擾性更新，不會中斷 IO 和 hello 裝置不會有任何停機時間。

#### <a name="download-updates-for-a-device-running-update-2-software"></a>下載適用於執行 Update 2 軟體的裝置的更新
**如果您的裝置正在執行 Update 2**，您必須下載並安裝下列 hotfix hello 規定順序中的 hello:

| 順序 | KB | 說明 | 更新類型 | 安裝時間 |
| --- | --- | --- | --- | --- |
| 1. |KB3179904 |軟體更新 &#42; |定期  <br></br>非干擾性 |~ 45 分鐘 |
| 2. |KB3146621 |iSCSI 封裝 |定期  <br></br>非干擾性 |~ 20 分鐘 |
| 3. |KB3103616 |WMI 封裝 |定期  <br></br>非干擾性 |~ 12 分鐘 |

 &#42; *請注意，軟體更新是由兩個二進位檔案所組成： 裝置軟體更新，前面加上`all-hcsmdssoftwareupdate`hello Ci 和 Mds 代理程式做為開頭`all-cismdsagentupdatebundle`。 hello Ci 和 Mds 代理程式之前必須先安裝 hello 裝置軟體更新。您也必須重新啟動 hello 作用中的控制器透過 hello `Restart-HcsController` cmdlet 套用 hello Ci 和 MDS 代理程式更新之後 （和套用 hello 剩餘更新之前）。* 

#### <a name="download-updates-for-a-device-running-pre-update-2-software"></a>下載適用於執行 Update 2 之前版本軟體的裝置的更新
**如果您的裝置執行 0.2、 0.3、 1.0 和 1.1 版**，您必須下載並安裝 hello LSI 驅動程式與韌體更新此外 toohello 軟體、 iSCSI 及 WMI 更新。 如果您是執行 Update 1.2 或 2，則已經安裝此更新。 

| 順序 | KB | 說明 | 更新類型 | 安裝時間 |
| --- | --- | --- | --- | --- |
| 4. |KB3121900 |LSI 驅動程式與韌體 |定期  <br></br>非干擾性 |~ 20 分鐘 |

<br></br>
**如果您的裝置正在執行版本 0.2、 0.3、 1.0、 1.1 和 1.2**，您必須下載並安裝 hello 太空和 hello Storport 修正程式。 如果您是執行 Update 2，則已經安裝這些修正程式。

| 順序 | KB | 說明 | 更新類型 | 安裝時間 |
| --- | --- | --- | --- | --- |
| 5. |KB3090322 |Spaceport 修正程式  </br> Windows Server 2012 R2 |定期  <br></br>非干擾性 |~ 20 分鐘 |
| 6. |KB3080728 |Storport 修正程式  </br> Windows Server 2012 R2 |定期  <br></br>非干擾性 |~ 20 分鐘 |

<br></br>
您可能也需要 tooinstall 磁碟韌體更新。 您可以確認您是否需要執行 hello 來 hello 磁碟韌體更新`Get-HcsFirmwareVersion`cmdlet。 如果您執行這些韌體版本： `XMGG`， `XGEG`， `KZ50`， `F6C2`， `VR08`，則您不需要 tooinstall 這些更新。

| 順序 | KB | 說明 | 更新類型 | 安裝時間 |
| --- | --- | --- | --- | --- |
| 7. |KB3121899 |磁碟韌體 |維護  <br></br>干擾性 |~ 30 分鐘 |

<br></br>

> [!IMPORTANT]
> * 此程序需求 toobe 只能執行一次 tooapply 更新 2.2。 您可以使用 hello Azure 傳統入口網站 tooapply 後續更新。
> * 如果從 Update 2 的更新，hello 總計的安裝時間將會是關閉 too1.5 小時。
> * 使用此程序 tooapply hello 前更新，請確定兩個 hello 裝置控制器都在線上，而且所有 hello 硬體元件都均狀況良好。
> 
> 

執行下列步驟 toodownload hello 和安裝 hello hotfix。

[!INCLUDE [storsimple-install-update21-hotfix](../../includes/storsimple-install-update21-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>後續步驟
深入了解 hello [Update 2.1 版本](storsimple-update21-release-notes.md)。

