---
title: "在 Government 入口網站中部署 StorSimple 裝置 | Microsoft Docs"
description: "描述在 Azure Government 入口網站中部署 StorSimple Update 2 裝置和服務的步驟與最佳做法。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 5277538c-797e-4e8e-b613-31b5c10cf5a9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/16/2016
ms.author: v-sharos
ms.openlocfilehash: 0b22dcdfc0432533b286e70d130bfe2ee2db92b2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-the-government-portal-update-2"></a>在 Government 入口網站中部署您的內部部署 StorSimple 裝置 (Update 2)
[!INCLUDE [storsimple-version-selector-deploy-gov](../../includes/storsimple-version-selector-deploy-gov.md)]

## <a name="overview"></a>概觀
歡迎使用 Microsoft Azure StorSimple 裝置部署。 這些部署教學課程適用於 Azure Government 入口網站中執行 Update 2 軟體的 StorSimple 8000 系列。 這一系列的教學課程包含 StorSimple 裝置的設定檢查清單、設定必要條件的清單，以及詳細的設定步驟。

這些教學課程中的資訊均假設您已經檢閱安全性預防措施，並已打開 StorSimple 裝置包裝、裝上機架並接好纜線。 如果您仍然需要執行這些工作，請從檢閱 [安全性預防措施](storsimple-safety.md)開始。 請遵循裝置特定的指示打開包裝、掛接機架和佈線您的裝置。

* [打開封裝、掛接機架，並將纜線接上 8100](storsimple-8100-hardware-installation.md)
* [打開封裝、掛接機架，並將纜線接上 8600](storsimple-8600-hardware-installation.md)

您必須需要有系統管理員權限，才能完成安裝和設定程序。 建議您在開始之前，檢閱設定檢查清單。 部署與設定程序可能需要一些時間才能完成。

> [!NOTE]
> 發佈於 Microsoft Azure 網站上的 StorSimple 部署資訊僅適用於 StorSimple 8000 系列裝置。 如需 7000 系列裝置的完整資訊，請移至： [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com)。 如需 7000 系列部署資訊，請參閱 [StorSimple 系統快速入門指南](http://onlinehelp.storsimple.com/111_Appliance/)。
> 
> 

## <a name="deployment-steps"></a>部署步驟
請執行這些必要步驟來設定 StorSimple 裝置，並將它連接到 StorSimple Manager 服務。 除了這些必要步驟外，部署期間也會有一些您可能需要完成的選擇性步驟和程序。 逐步部署指出您應該執行各選擇性步驟的時機。

| 步驟 | 說明 |
| --- | --- |
| **必要條件** |這些是針對將要進行的部署而需要完成的準備工作。 |
| [部署設定檢查清單](#deployment-configuration-checklist) |使用此檢查清單來收集並記錄部署之前和部署期間的資訊。 |
| [部署必要條件](#deployment-prerequisites) |這些項目會驗證環境是否準備就緒以供部署。 |
|  | |
| **逐步部署** |需要執行這些步驟，才能在生產環境中部署您的 StorSimple 裝置。 |
| [步驟 1：建立新的服務](#step-1-create-a-new-service) |設定雲端管理和 StorSimple 裝置的儲存體。 *如果您現在已經有針對其他 StorSimple 裝置的服務，請略過此步驟*。 |
| [步驟 2：取得服務註冊金鑰](#step-2-get-the-service-registration-key) |使用此金鑰註冊並將 StorSimple 裝置與管理服務連接。 |
| [步驟 3：透過 Windows PowerShell for StorSimple 設定和註冊裝置](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |使用管理服務將裝置連線到您的網路並使用 Azure 註冊以完成設定。 |
| [步驟 4：完成最小量裝置設定](#step-4-complete-minimum-device-setup) </br>選用：更新您的 StorSimple 裝置。 |使用管理服務來完成裝置設定並啟用裝置以提供儲存體。 |
| [步驟 5：建立磁碟區容器](#step-5-create-a-volume-container) |建立容器以佈建磁碟區。 磁碟區容器具有其中所含之所有磁碟區的儲存體帳戶、頻寬及加密設定。 |
| [步驟 6：建立磁碟區](#step-6-create-a-volume) |在您伺服器的 StorSimple 裝置上佈建儲存體磁碟區。 |
| [步驟 7：掛接、初始化及格式化磁碟區](#step-7-mount-initialize-and-format-a-volume) </br>選用：設定 MPIO。 |將您的伺服器連接至裝置提供的 iSCSI 儲存體。 選擇性地設定 MPIO，以確保您的伺服器可以容許連結、網路和介面失敗。 |
| [步驟 8：進行備份](#step-8-take-a-backup) |設定備份原則以保護您的資料 |
|  | |
| **其他程序** |在您部署解決方案時可能需要參考這些程序。 |
| [針對服務設定新的儲存體帳戶](#configure-a-new-storage-account-for-the-service) | |
| [使用 PuTTY 連接到裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console) | |
| [掃描並套用更新](#scan-for-and-apply-updates) | |
| [取得 Windows Server 主機的 IQN](#get-the-iqn-of-a-windows-server-host) | |
| [建立手動備份](#create-a-manual-backup) | |
| [設定 MPIO](#configure-mpio) | |

## <a name="deployment-configuration-checklist"></a>部署設定檢查清單
在部署 StorSimple 裝置之前，您必須收集資訊以設定您裝置上的軟體。 事先備妥部分的這些資訊可協助簡化在環境中部署 StorSimple 裝置的程序。 下載並使用此檢查清單，以記下您部署裝置時的設定詳細資訊。  

[下載 StorSimple 部署設定檢查清單](http://www.microsoft.com/download/details.aspx?id=49159)  

## <a name="deployment-prerequisites"></a>部署必要條件
下列各節說明 StorSimple Manager 服務與 StorSimple 裝置的設定必要條件。

### <a name="for-the-storsimple-manager-service"></a>對於 StorSimple Manager 服務
在您開始前，請確定：

* 您擁有的 Microsoft 帳戶具有存取認證。
* 您擁有的 Microsoft Azure 儲存體帳戶具有存取認證。
* StorSimple Manager 服務已啟用您的 Microsoft Azure 訂用帳戶。 您應該透過 [企業合約](https://azure.microsoft.com/pricing/enterprise-agreement/)購買訂用帳戶。
* 您有權限可存取終端機模擬軟體，例如 PuTTY。

### <a name="for-the-device-in-the-datacenter"></a>對於資料中心的裝置
在設定裝置前，請確認：

* 您已完全打開裝置包裝、掛接到機架上，並連接所有的電源、網路及序列存取纜線，如下所述：
  
  * [打開封裝、掛接機架，並將纜線接上 8100 裝置](storsimple-8100-hardware-installation.md)
  * [打開封裝、掛接機架，並將纜線接上 8600 裝置](storsimple-8600-hardware-installation.md)

### <a name="for-the-network-in-the-datacenter"></a>針對資料中心內的網路
在您開始前，請確定：

* 資料中心防火牆中的連接埠已開放，以允許 iSCSI 和雲端流量，如 [StorSimple 裝置的網路需求](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device)中所述。

## <a name="step-by-step-deployment"></a>逐步部署
請在資料中心使用下列逐步指示來部署 StorSimple 裝置。

## <a name="step-1-create-a-new-service"></a>步驟 1：建立新的服務
StorSimple Manager 服務可以管理多個 StorSimple 裝置。 請執行下列步驟以建立 StorSimple Manager 服務的新執行個體。

[!INCLUDE [storsimple-create-new-service-gov](../../includes/storsimple-create-new-service-gov.md)]

> [!IMPORTANT]
> 如果您並未啟用服務自動建立儲存體帳戶，您將必須在成功建立服務後，至少建立一個儲存體帳戶。 當您建立磁碟區容器時，將會使用此儲存體帳戶。
> 
> * 如果您未自動建立儲存體帳戶，請移至 [針對服務設定新的儲存體帳戶](#configure-a-new-storage-account-for-the-service) 以取得詳細指示。
> * 如果您已啟用自動建立儲存體帳戶，請移至 [步驟 2：取得服務註冊金鑰](#step-2-get-the-service-registration-key)。
> 
> 

## <a name="step-2-get-the-service-registration-key"></a>步驟 2：取得服務註冊金鑰
當 StorSimple Manager 服務啟動後處於執行中時，您就必須取得服務註冊金鑰。 這個金鑰可用以註冊並將 StorSimple 裝置連接至服務。

請在 Government 入口網站中執行下列步驟。

[!INCLUDE [storsimple-get-service-registration-key-gov](../../includes/storsimple-get-service-registration-key-gov.md)]

## <a name="step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple"></a>步驟 3：透過 Windows PowerShell for StorSimple 設定和註冊裝置
您可以使用 Windows PowerShell for StorSimple 來完成 StorSimple 裝置的初始安裝，如下列程序所述。 您必須使用終端機模擬軟體來完成這個步驟。 如需詳細資訊，請參閱 [使用 PuTTY 連接到裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console)。

[!INCLUDE [storsimple-configure-and-register-device-gov](../../includes/storsimple-configure-and-register-device-gov-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a>步驟 4：完成最小量裝置設定
為完成 StorSimple 裝置的最小量裝置設定，您必須：

* 設定次要 DNS 伺服器。
* 至少在一個網路介面上啟用 iSCSI。
* 針對兩個控制器指派固定的 IP 位址。

請在 Government 入口網站中執行下列步驟，以完成最小量裝置設定。

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>步驟 5：建立磁碟區容器
磁碟區容器具有其中所含之所有磁碟區的儲存體帳戶、頻寬及加密設定。 您必須建立磁碟區容器，才能開始在 StorSimple 裝置上佈建磁碟區。

請在 Government 入口網站中執行下列步驟，以建立磁碟區容器。

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>步驟 6：建立磁碟區
建立磁碟區容器之後，您就可以為伺服器在 StorSimple 裝置上佈建存放磁碟區。 請在 Government 入口網站中執行下列步驟，以建立磁碟區。

> [!IMPORTANT]
> Azure StorSimple 只能建立精簡佈建的磁碟區。  您無法在 Azure StorSimple 系統上建立完整佈建或部分佈建的磁碟區。
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>步驟 7：掛接、初始化及格式化磁碟區
請在 Windows Server 主機上執行這些步驟。

> [!IMPORTANT]
> * 為獲得 StorSimple 解決方案的高可用性，建議您先在主機伺服器 (選用) 上設定 MPIO，再設定 iSCSI。 主機伺服器上的 MPIO 設定會確保伺服器可以容許連結、網路，或介面失敗。
> * 如需在 Windows Server 主機上安裝和設定 MPIO 和 iSCSI 的指示，請移至 [為 StorSimple 裝置設定 MPIO](storsimple-configure-mpio-windows-server.md)。 其中也會包括掛接、初始化和格式化 StorSimple 磁碟區的步驟。
> * 如需在 Linux 主機上安裝和設定 MPIO 和 iSCSI 的指示，請移至 [為 StorSimple Linux 主機設定 MPIO](storsimple-configure-mpio-on-linux.md)
> 
> 

如果您決定不設定 MPIO，請執行下列步驟在 Windows Server 主機上掛接、初始化及格式化您的 StorSimple 磁碟區。

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>步驟 8：進行備份
備份可提供磁碟區的時間點保護，並改善復原能力，同時讓還原時間降至最低。 您可以在 StorSimple 裝置上進行兩種備份類型：本機快照與雲端快照。 每一種備份類型都可以是 [排程] 或 [手動]。

請在 Government 入口網站中執行下列步驟，以建立排程備份。

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

您可以隨時進行手動備份。 如需相關程序，請移至 [建立手動備份](#create-a-manual-backup)。

## <a name="configure-a-new-storage-account-for-the-service"></a>針對服務設定新的儲存體帳戶
這是選擇性步驟，只有當您並未啟用服務自動建立儲存體帳戶時才需要執行。 必須要有 Microsoft Azure 儲存體帳戶，才能建立 StorSimple 磁碟區容器。

如果您需要在不同區域建立 Azure 儲存體帳戶，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md) 以取得逐步指示。

請在 Government 入口網站上的 [StorSimple Manager 服務]  頁面，執行下列步驟。

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-to-connect-to-the-device-serial-console"></a>使用 PuTTY 連接到裝置序列主控台
若要連接到 Windows PowerShell for StorSimple，您需要使用終端機模擬軟體，例如 PuTTY。 您可以在存取裝置時，直接透過序列主控台或從遠端電腦開啟 Telnet 工作階段來使用 PuTTY。

[!INCLUDE [Use PuTTY to connect to the device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>掃描並套用更新
更新裝置可能需要數小時的時間。 在裝置上執行下列步驟來掃描並套用更新。

<!--If you have a gateway configured on a network interface other than Data 0, you will need to disable Data 2 and Data 3 network interfaces before installing the update. Go to **Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after the device is updated.-->

#### <a name="to-update-your-device"></a>若要更新裝置
1. 在裝置的 [快速入門] 頁面上，按一下 [裝置]。 選取實體裝置，按一下 [維護]，然後按一下 [掃描更新]。  
2. 系統會建立掃描可用更新的工作。 如果有可用的更新，[掃描更新] 會變更為 [安裝更新]。 按一下 [安裝更新] 。
3. 更新工作將會建立。 巡覽至 [工作] 以監視更新的狀態。
   
   > [!NOTE]
   > 當更新工作啟動時，狀態會立即顯示為 50 %。 只有在更新工作完成之後，狀態才會變更為 100%。 更新程序沒有即時狀態。
   > 
   > 
4. 裝置成功更新之後，請啟用 Data 2 和 Data 3 網路介面 (如果已停用)。

## <a name="get-the-iqn-of-a-windows-server-host"></a>取得 Windows Server 主機的 IQN
請執行下列步驟，以取得正在執行 Windows Server® 2012 之 Windows 主機的 iSCSI 限定名稱 (IQN)。

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>建立手動備份
請在 Government 入口網站中執行下列步驟，以針對 StorSimple 裝置上的單一磁碟區建立隨選手動備份。

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup-gov.md)]

## <a name="configure-mpio"></a>設定 MPIO
多重路徑 I/O (MPIO) 是 Windows Server 預設不會安裝的選擇性功能。 您應該透過伺服器管理員將它安裝為功能。 如需 MPIO 安裝指示，請移至 [為 StorSimple 裝置設定 MPIO](storsimple-configure-mpio-windows-server.md)。

如需為連接到 Linux 主機之 StorSimple 裝置安裝 MPIO 的指示，請移至 [為 Linux 主機設定 MPIO](storsimple-configure-mpio-on-linux.md)。

> [!NOTE]
> 在 Azure 中 StorSimple 虛擬裝置不支援 MPIO。
> 
> 

## <a name="next-steps"></a>後續步驟
* 設定 [虛擬裝置](storsimple-virtual-device-u2.md)。
* 使用 [StorSimple Manager 服務](storsimple-manager-service-administration.md) 以管理 StorSimple 裝置。

