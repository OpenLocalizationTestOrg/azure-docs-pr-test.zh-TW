---
title: "政府入口網站中的 aaaDeploy StorSimple 8000 系列裝置 |Microsoft 文件"
description: "描述 hello 步驟和最佳做法部署 hello StorSimple 8000 系列裝置執行 Update 3 及更新版本中，與 hello 服務在 hello Azure 政府入口網站。"
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
ms.workload: NA
ms.date: 06/22/2017
ms.author: alkohli
ms.openlocfilehash: ea643cd59dcdf17482268d14c1348a3b5fb098b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-hello-government-portal"></a>部署在內部部署 StorSimple 裝置在 hello 政府入口網站

## <a name="overview"></a>概觀
歡迎使用 tooMicrosoft Azure StorSimple 裝置部署。 Toohello StorSimple 8000 系列執行 Update 3 軟體或更新版本在 hello Azure 政府入口網站，就會套用這些部署教學課程。 這一系列的教學課程包含 StorSimple 裝置的設定檢查清單、設定必要條件的清單，以及詳細的設定步驟。

這些教學課程中的 hello 資訊假設您已檢閱 hello 安全措施，並解壓縮、 racked，和妥您的 StorSimple 裝置。 如果您仍然需要的 tooperform 這些工作，以檢閱 hello 開頭[安全措施](storsimple-safety.md)。 請遵循 toounpack，機架掛接，並以纜線連接您的裝置 hello 裝置的特定指示。

* [打開封裝、掛接機架，並將纜線接上 8100](storsimple-8100-hardware-installation.md)
* [打開封裝、掛接機架，並將纜線接上 8600](storsimple-8600-hardware-installation.md)

您需要系統管理員權限 toocomplete hello 安裝和設定程序。 我們建議您先檢閱 hello 組態檢查清單。 hello 部署和設定程序可能需要一些時間 toocomplete。

> [!NOTE]
> hello hello Microsoft Azure 網站上發行的 StorSimple 部署資訊適用於 tooStorSimple 8000 系列的裝置。 如需 hello 7000 系列裝置的完整資訊，請移至： [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com)。 如需 7000 系列部署資訊，請參閱 hello [StorSimple 系統快速入門指南](http://onlinehelp.storsimple.com/111_Appliance/)。


## <a name="deployment-steps"></a>部署步驟
執行下列必要的步驟 tooconfigure StorSimple 裝置，並將它連接 tooyour StorSimple 裝置管理員服務。 此外 toohello 所需的步驟，選擇性的步驟和程序，您可能需要 toocomplete hello 部署期間。 您應該執行每一個選擇性的步驟時，就會指出 hello 逐步部署指示。

| 步驟 | 說明 |
| --- | --- |
| **必要條件** |這些需要 toobe 完成在 hello 即將部署的準備。 |
| [部署設定檢查清單](#deployment-configuration-checklist) |使用此檢查清單 toogather 和記錄資訊先前 tooand hello 部署期間。 |
| [部署必要條件](#deployment-prerequisites) |這些驗證該 hello 環境是否準備好進行部署。 |
|  | |
| **逐步部署** |這些步驟是必要的 toodeploy StorSimple 裝置在生產環境中的。 |
| [步驟 1：建立新的服務](#step-1-create-a-new-service) |設定雲端管理和 StorSimple 裝置的儲存體。 *如果您現在已經有針對其他 StorSimple 裝置的服務，請略過此步驟*。 |
| [步驟 2： 取得 hello 服務註冊金鑰](#step-2-get-the-service-registration-key) |使用此索引鍵 tooregister 和連線您的 StorSimple 裝置 hello 管理服務。 |
| [步驟 3： 設定 hello 裝置透過 Windows PowerShell for StorSimple 和註冊](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |Hello 裝置 tooyour 網路連線，並向使用 hello 管理服務的 Azure toocomplete hello 安裝程式。 |
| [步驟 4: Hello 完成最低裝置設定](#step-4-complete-minimum-device-setup) </br>選用：更新您的 StorSimple 裝置。 |使用 hello management 服務 toocomplete hello 裝置安裝程式並啟用它 tooprovide 儲存體。 |
| [步驟 5：建立磁碟區容器](#step-5-create-a-volume-container) |建立容器 tooprovision 磁碟區。 磁碟區容器有儲存體帳戶、 頻寬和加密設定，其包含的所有 hello 磁碟區。 |
| [步驟 6：建立磁碟區](#step-6-create-a-volume) |佈建伺服器 hello StorSimple 裝置上的存放磁碟區。 |
| [步驟 7：掛接、初始化及格式化磁碟區](#step-7-mount-initialize-and-format-a-volume) </br>選用：設定 MPIO。 |連接伺服器 toohello iSCSI 存放裝置 hello 裝置所提供。 （選擇性） 設定 MPIO tooensure 伺服器可容許連結、 網路和介面失敗。 |
| [步驟 8：進行備份](#step-8-take-a-backup) |設定備份原則 tooprotect 您的資料 |
|  | |
| **其他程序** |當您部署方案，您可能需要 toorefer toothese 程序。 |
| [設定新的儲存體帳戶 hello 服務](#configure-a-new-storage-account-for-the-service) | |
| [使用 PuTTY tooconnect toohello 裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console) | |
| [掃描並套用更新](#scan-for-and-apply-updates) | |
| [取得 Windows Server 主機的 IQN hello](#get-the-iqn-of-a-windows-server-host) | |
| [建立手動備份](#create-a-manual-backup) | |


## <a name="deployment-configuration-checklist"></a>部署設定檢查清單
部署您的 StorSimple 裝置之前，您將需要 toocollect 資訊 tooconfigure hello 軟體在裝置上。 準備某些事先這項資訊可協助簡化的部署環境中的 hello StorSimple 裝置 hello 程序。 下載並使用此檢查清單 toonote hello 設定詳細資料，與部署您的裝置。

[下載 StorSimple 部署設定檢查清單](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a>部署必要條件
hello 下列各節說明 hello StorSimple 裝置 Manager 服務和您的 StorSimple 裝置的組態先決條件。

### <a name="for-hello-storsimple-device-manager-service"></a>Hello StorSimple 裝置管理員服務
在您開始前，請確定：

* 您擁有的 Microsoft 帳戶具有存取認證。
* 您擁有的 Microsoft Azure 儲存體帳戶具有存取認證。
* Hello StorSimple 裝置管理員服務已啟用 Microsoft Azure 訂用帳戶。 您的訂用帳戶應採購 hello [Enterprise 合約](https://azure.microsoft.com/pricing/enterprise-agreement/)。
* 您必須存取 tooterminal 模擬軟體，例如 PuTTY。

### <a name="for-hello-device-in-hello-datacenter"></a>Hello hello 資料中心內的裝置
在設定之前 hello 裝置，請確認：

* 您已完全打開裝置包裝、掛接到機架上，並連接所有的電源、網路及序列存取纜線，如下所述：
  
  * [打開封裝、掛接機架，並將纜線接上 8100 裝置](storsimple-8100-hardware-installation.md)
  * [打開封裝、掛接機架，並將纜線接上 8600 裝置](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Hello 資料中心中的 hello 網路
在您開始前，請確定：

* hello 中您資料中心的防火牆連接埠是開啟的 tooallow iSCSI 和雲端流量中所述[StorSimple 裝置的網路需求](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device)。

## <a name="step-by-step-deployment"></a>逐步部署
使用您的 StorSimple 裝置 hello 遵循逐步指示 toodeploy hello 資料中心內。

## <a name="step-1-create-a-new-service"></a>步驟 1：建立新的服務
StorSimple 裝置管理員服務可以管理多個 StorSimple 裝置。 執行下列步驟 toocreate hello StorSimple 裝置管理員服務的新執行個體的 hello。

[!INCLUDE [storsimple-8000-create-new-service-gov](../../includes/storsimple-8000-create-new-service-gov.md)]

> [!IMPORTANT]
> 如果您未啟用 hello 自動建立儲存體帳戶與您的服務，您將需要 toocreate 至少一個儲存體帳戶之後，您已成功建立服務。 當您建立磁碟區容器時，將會使用此儲存體帳戶。
> 
> * 如果您未自動建立儲存體帳戶，請移至太[設定新的儲存體帳戶 hello 服務](#configure-a-new-storage-account-for-the-service)如需詳細指示。
> * 如果您啟用 hello 自動建立儲存體帳戶，請移至太[步驟 2： 取得 hello 服務註冊金鑰](#step-2-get-the-service-registration-key)。


## <a name="step-2-get-hello-service-registration-key"></a>步驟 2： 取得 hello 服務註冊金鑰
Hello StorSimple 裝置管理員服務已啟動並執行之後，您將需要 tooget hello 服務註冊金鑰。 這個金鑰是使用的 tooregister，而且連接您的 StorSimple 裝置 toohello 服務。

執行下列步驟在 hello 政府入口網站中的 hello。

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>步驟 3： 設定 hello 裝置透過 Windows PowerShell for StorSimple 和註冊
Hello 遵循程序中所述，您的 StorSimple 裝置的 StorSimple toocomplete hello 初始設定使用 Windows PowerShell。 您將需要 toouse 終端機模擬軟體 toocomplete 此步驟。 如需詳細資訊，請參閱[使用 PuTTY tooconnect toohello 裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console)。

[!INCLUDE [storsimple-8000-configure-and-register-device-gov](../../includes/storsimple-8000-configure-and-register-device-gov-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a>步驟 4：完成最小量裝置設定
您的 StorSimple 裝置 hello 最低裝置設定，您都必須：

* 為裝置提供 [易記名稱]。
* 設定裝置時區 hello。
* Tooboth hello 控制器指派固定的 IP 位址。

執行下列步驟在 hello Azure 政府入口 toocomplete hello 最低裝置設定中的 hello。

[!INCLUDE [storsimple-8000-complete-minimum-device-setup-u2](../../includes/storsimple-8000-complete-minimum-device-setup-u2.md)]

## <a name="step-5-create-a-volume-container"></a>步驟 5：建立磁碟區容器
磁碟區容器有儲存體帳戶、 頻寬和加密設定，其包含的所有 hello 磁碟區。 您可以開始佈建您的 StorSimple 裝置上的磁碟區之前，您將需要 toocreate 磁碟區容器。

執行下列步驟在 hello 政府入口 toocreate 磁碟區容器中的 hello。

[!INCLUDE [storsimple-8000-create-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>步驟 6：建立磁碟區
建立磁碟區容器之後，您可以為您的伺服器來佈建 hello StorSimple 裝置上的存放磁碟區。 執行下列步驟在 hello 政府入口 toocreate 磁碟區中的 hello。

> [!IMPORTANT]
> StorSimple 裝置管理員只能建立精簡佈建的磁碟區。  然而，您無法建立部分佈建的磁碟機。

[!INCLUDE [storsimple-8000-create-volume](../../includes/storsimple-8000-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>步驟 7：掛接、初始化及格式化磁碟區
請在 Windows Server 主機上執行這些步驟。

> [!IMPORTANT]
> * Hello 的 StorSimple 解決方案的高可用性，建議您在您的主機伺服器 （選擇性） 先前 tooconfiguring iSCSI 上設定 MPIO。 在主機伺服器上的 MPIO 設定可確保 hello 伺服器可容許連結、 網路或介面失效。
> * MPIO 與 iSCSI 安裝和設定指示 Windows Server 主機上，移過[設定 MPIO StorSimple 裝置的](storsimple-configure-mpio-windows-server.md)。 這些也會包含 hello 步驟 toomount、 初始化及格式化 StorSimple 磁碟區。
> * MPIO 與 iSCSI 安裝和設定指示在 Linux 主機上，移過[設定 MPIO StorSimple Linux 主機](storsimple-configure-mpio-on-linux.md)

如果您決定 tooconfigure MPIO，執行下列步驟 toomount hello、 初始化及格式化您的 StorSimple 磁碟區，Windows Server 主機上。

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>步驟 8：進行備份
備份可提供磁碟區的時間點保護，並改善復原能力，同時讓還原時間降至最低。 您可以在 StorSimple 裝置上進行兩種備份類型：本機快照與雲端快照。 每一種備份類型都可以是 [排程] 或 [手動]。

執行下列步驟在 hello 政府入口 toocreate 排定的備份中的 hello。

[!INCLUDE [storsimple-8000-take-backup](../../includes/storsimple-8000-take-backup.md)]

您可以隨時進行手動備份。 程序，跳過[建立手動備份](#create-a-manual-backup)。

## <a name="configure-a-new-storage-account-for-hello-service"></a>設定新的儲存體帳戶 hello 服務
這是選擇性的步驟，您需要 tooperform，只有當您未啟用 hello 自動建立儲存體帳戶與您的服務。 Microsoft Azure 儲存體帳戶是必要的 toocreate StorSimple 磁碟區容器。

如果您需要 toocreate 不同區域中的 Azure 儲存體帳戶，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)如需逐步指示。

執行下列步驟在 hello 政府入口網站上 hello hello **StorSimple 裝置管理員服務**頁面。

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>使用 PuTTY tooconnect toohello 裝置序列主控台
tooconnect tooWindows PowerShell for StorSimple 中，您需要 toouse 終端機模擬軟體，例如 PuTTY。 當您存取 hello 裝置直接透過 hello 序列主控台或從遠端電腦開啟 telnet 工作階段時，您可以使用 PuTTY。

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>掃描並套用更新
更新裝置可能需要數小時的時間。 如需有關如何 tooinstall hello 最新的更新詳細的步驟，請移過[安裝更新的 4](storsimple-8000-install-update-4.md)。

## <a name="get-hello-iqn-of-a-windows-server-host"></a>取得 Windows Server 主機的 IQN hello
執行下列步驟 tooget hello iSCSI hello 限定名稱 (IQN) 正在執行 Windows Server® 2012年的 Windows 主機。

[!INCLUDE [Get IQN of your Windows Server host](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>建立手動備份
執行 hello 遵循您的 StorSimple 裝置上 hello 政府入口 toocreate 隨需手動備份單一磁碟區中的步驟。

[!INCLUDE [Create a manual backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>後續步驟
* 設定 [虛擬裝置](storsimple-8000-cloud-appliance-u2.md)。
* 使用 hello [StorSimple 裝置管理員服務](storsimple-8000-manager-service-administration.md)toomanage StorSimple 裝置。

