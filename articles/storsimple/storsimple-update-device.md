---
title: "aaaUpdate StorSimple 裝置 |Microsoft 文件"
description: "說明如何 toouse hello StorSimple 更新功能 tooinstall 規則和維護模式更新和 hotfix。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a>更新您的 StorSimple 8000 系列裝置
## <a name="overview"></a>概觀
hello StorSimple 更新功能可讓您 tooeasily 保持您的 StorSimple 裝置。 根據 hello 更新類型，您可以套用更新 toohello 裝置透過 hello Azure 傳統入口網站或透過 hello Windows PowerShell 介面。 這個教學課程描述 hello 更新類型及如何 tooinstall 每個。

您可以套用兩種類型的裝置更新： 

* 一般 (或標準模式) 更新
* 維護模式更新

您可以安裝 hello Azure 傳統入口網站或 Windows PowerShell 中; 透過定期更新不過，您必須使用 Windows PowerShell tooinstall 維護模式更新。 

以下將個別說明每個更新類型。

### <a name="regular-updates"></a>一般更新
定期更新將會非干擾性更新可以在 hello 裝置處於正常模式時安裝。 這些更新會透過 hello Microsoft Update 網站 tooeach 裝置控制器套用。 

> [!IMPORTANT]
> 控制器容錯移轉可能會發生 hello 更新程序期間。 不過，這不會影響系統的可用性或運作。
> 
> 

* 如需 tooinstall regular 更新的方式透過 hello Azure 傳統入口網站的詳細資訊，請參閱[安裝定期更新 hello Azure 傳統入口網站透過](#install-regular-updates-via-the-azure-classic-portal)。
* 您也可以透過 Windows PowerShell for StorSimple 安裝一般更新。 如需詳細資訊，請參閱 [透過 Windows PowerShell for StorSimple 安裝一般更新](#install-regular-updates-via-windows-powershell-for-storsimple)。

### <a name="maintenance-mode-updates"></a>維護模式更新
維護模式更新是干擾性更新，例如磁碟韌體升級。 這些更新需要 hello 裝置 toobe 放入維護模式。 如需詳細資訊，請參閱 [步驟 2：進入維護模式](#step2)。 您無法使用 hello Azure 傳統入口網站 tooinstall 維護模式更新。 您必須改用 Windows PowerShell for StorSimple。 

如需 tooinstall 維護模式更新的方式的詳細資訊，請參閱[透過 Windows PowerShell for StorSimple 安裝維護模式更新](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple)。

> [!IMPORTANT]
> 維護模式更新必須個別套用 tooeach 控制站。 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a>安裝定期更新，透過 hello Azure 傳統入口網站
您可以使用 hello Azure 傳統入口網站 tooapply 更新 tooyour StorSimple 裝置。

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a>透過 Windows PowerShell for StorSimple 安裝一般更新
或者，您可以使用 Windows PowerShell for StorSimple tooapply 一般 （一般模式） 的更新。

> [!IMPORTANT]
> 雖然您可以安裝使用 Windows PowerShell for StorSimple 的定期更新，但是我們強烈建議您安裝定期更新，透過 hello Azure 傳統入口網站。 預先檢查更新 1 開始，將會執行先前 tooinstalling 更新從 hello 入口網站。 這些前置檢查可防止失敗，並確保提供更順暢的體驗。 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>透過 Windows PowerShell for StorSimple 安裝維護模式更新
您可以使用 Windows PowerShell for StorSimple tooapply 維護模式更新 tooyour StorSimple 裝置。 在此模式中，所有的 I/O 要求都會暫停。 也會停止服務，例如非揮發性隨機存取記憶體 (NVRAM) 或 hello 叢集服務。 這兩個控制站會在您進入或結束此模式時重新啟動。 當您結束此模式中時，所有 hello 服務將會繼續，而且應該是狀況良好。 (這可能需要數分鐘的時間)。

如果您需要 tooapply 維護模式更新，您會收到 hello Azure 傳統入口網站透過警示您有必須安裝的更新。 此警示將會包含使用 Windows PowerShell for StorSimple tooinstall hello 更新的指示。 更新您的裝置之後，使用 hello 相同程序 toochange hello 裝置 tooRegular 模式。 如需逐步指示，請參閱 [步驟 4：結束維護模式](#step4)。

> [!IMPORTANT]
> * 之前進入維護模式，請確認兩個裝置控制器會處於狀況良好，藉由檢查 hello**硬體狀態**上 hello**維護**hello Azure 傳統入口網站中的頁面。 如果 hello 控制器未正常運作，請連絡 Microsoft 支援 hello 接下來的步驟。 如需詳細資訊，請移 tooContact Microsoft 支援服務。 
> * 當您處於維護模式時，您需要 tooapply hello 更新第一次一個控制站上，然後在 hello 另一個控制器。
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a>步驟 1： 連接 toohello 序列主控台<a name="step1">
首先，使用應用程式，例如 PuTTY tooaccess hello 序列主控台。 hello 下列程序說明如何 toouse PuTTY tooconnect toohello 序列主控台。

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a>步驟 2：進入維護模式 <a name="step2">
連接 toohello 主控台之後，判斷是否有更新 tooinstall，然後輸入 維護模式 tooinstall 它們。

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a>步驟 3：安裝更新 <a name="step3">
接下來，安裝您的更新。

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a>步驟 4：結束維護模式 <a name="step4">
最後，結束維護模式。

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a>透過 Windows PowerShell for StorSimple 安裝 Hotfix
不同於 Microsoft Azure StorSimple 的更新，Hotfix 是從共用資料夾進行安裝的。 和更新一樣，有兩種類型的 Hotfix： 

* 一般的 Hotfix 
* 維護模式的 Hotfix  

hello 下列程序說明如何 toouse Windows PowerShell for StorSimple tooinstall 規則和維護模式 hotfix。

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a>發生什麼事 tooupdates，如果您執行原廠重設的 hello 裝置？
如果裝置重設 toofactory 設定，然後所有 hello 更新都都將遺失。 Hello 原廠重設裝置在註冊及設定之後，您必須將安裝更新 toomanually 透過 hello Azure 傳統入口網站及/或 Windows PowerShell for StorSimple。 如需原廠重設的詳細資訊，請參閱[hello 裝置 toofactory 預設設定重設](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings)。

## <a name="next-steps"></a>後續步驟
* 深入了解[使用 Windows PowerShell for StorSimple tooadminister StorSimple 裝置](storsimple-windows-powershell-administration.md)。
* 深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。

