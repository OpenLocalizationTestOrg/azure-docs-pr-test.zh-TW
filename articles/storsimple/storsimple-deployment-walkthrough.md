---
title: "在內部部署 StorSimple 裝置 aaaDeploy |Microsoft 文件"
description: "描述 hello 步驟和部署的 hello StorSimple 裝置和服務的最佳作法。 (適用於 Azure StorSimple 版本.3 tooMicrosoft 及更早版本。)"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b27f87a2-1363-4e0d-90f7-37b5dd1f21c9
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d45abba1786ceae586a99ca77b90de3f290c2f0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device"></a>部署內部部署 StorSimple 裝置
> [!div class="op_single_selector"]
> * [Update 2](storsimple-deployment-walkthrough-u2.md)
> * [Update 1](storsimple-deployment-walkthrough-u1.md)
> * [GA 版本](storsimple-deployment-walkthrough.md)
> 
> 

## <a name="overview"></a>概觀
歡迎使用 tooMicrosoft Azure StorSimple 裝置部署。 這些部署教學課程適用於 tooStorSimple 8000 系列發行版本、 StorSimple 8000 系列 Update 0.1、 StorSimple 8000 系列 Update 0.2 和 StorSimple 8000 系列 Update 0.3。 這一系列的教學課程說明如何 tooconfigure StorSimple 裝置，而且包含設定檢查清單、 設定必要條件和詳細的設定步驟。

這些教學課程中的 hello 資訊假設您已檢閱 hello 安全措施，並解壓縮、 racked，和妥您的 StorSimple 裝置。 如果您仍然需要的 tooperform 這些工作，以檢閱 hello 開頭[安全措施](storsimple-safety.md)。 根據您裝置的模型，您可以接著先解壓縮，機架掛接和纜線中的 hello 指示：

* [打開封裝、掛接機架，並將纜線接上 8100](storsimple-8100-hardware-installation.md)
* [打開封裝、掛接機架，並將纜線接上 8600](storsimple-8600-hardware-installation.md)

您需要系統管理員權限 toocomplete hello 安裝和設定程序。 我們建議您先檢閱 hello 組態檢查清單。 hello 部署和設定程序可能需要一些時間 toocomplete。

> [!NOTE]
> hello hello Microsoft Azure 網站上發行的 StorSimple 部署資訊適用於 tooStorSimple 8000 系列的裝置。 如需 hello 5000 和 7000 系列裝置的完整資訊，請移至： [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com)。 5000 到 7000 系列部署資訊，請參閱 hello [StorSimple 系統快速入門指南](http://onlinehelp.storsimple.com/111_Appliance/)。
> 
> 

## <a name="deployment-steps"></a>部署步驟
執行下列必要的步驟 tooconfigure StorSimple 裝置，並將它連接 tooyour StorSimple Manager 服務。 此外 toohello 所需的步驟，選擇性的步驟和程序，您可能需要在 hello 部署期間。 您應該執行每一個選擇性的步驟時，就會指出 hello 逐步部署指示。

| 步驟 | 說明 |
| --- | --- |
| **必要條件** |這些需要 toobe 完成在 hello 即將部署的準備。 |
| 部署設定檢查清單。 |使用此檢查清單 toogather 和記錄資訊先前 tooand hello 部署期間。 |
| 部署必要條件。 |這些驗證 hello 環境是否準備好進行部署。 |
|  | |
| **逐步部署** |這些步驟是必要的 toodeploy StorSimple 裝置在生產環境中的。 |
| 步驟 1：建立新的服務。 |設定雲端管理和 StorSimple 裝置的儲存體。 如果您現在已經有針對其他 StorSimple 裝置的服務，請略過此步驟。 |
| 步驟 2： 取得 hello 服務註冊金鑰。 |使用此索引鍵 tooregister （& s) 連線您的 StorSimple 裝置 hello 管理服務。 |
| 步驟 3： 設定 hello 裝置透過 Windows PowerShell for StorSimple 和註冊。 |Hello 裝置 tooyour 網路連線，並向使用 hello 管理服務的 Azure toocomplete hello 安裝程式。 |
| 步驟 4：完成最小量裝置設定</br>選用：更新您的 StorSimple 裝置。 |使用 hello management 服務 toocomplete hello 裝置安裝程式並啟用它 tooprovide 儲存體。 |
| 步驟 5：建立磁碟區容器。 |建立容器 tooprovision 磁碟區。 磁碟區容器有儲存體帳戶、 頻寬和加密設定，其包含的所有 hello 磁碟區。 |
| 步驟 6：建立磁碟區。 |佈建伺服器 hello StorSimple 裝置上的存放磁碟區。 |
| 步驟 7：掛接、初始化及格式化磁碟區。</br>選用：設定 MPIO。 |連接伺服器 toohello iSCSI 存放裝置 hello 裝置所提供。 選擇性地設定 MPIO tooensure 伺服器可容許連結、 網路和介面失敗。 |
| 步驟 8：進行備份。 |設定備份原則 tooprotect 您的資料 |
|  | |
| **其他程序** |當您部署方案，您可能需要 toorefer toothese 程序。 |
| 設定新的儲存體帳戶 hello 服務。 | |
| 使用 PuTTY tooconnect toohello 裝置序列主控台。 | |
| 收到 hello Windows Server 主機的 IQN。 | |
| 建立手動備份。 | |

## <a name="deployment-configuration-checklist"></a>部署設定檢查清單
hello 下列部署組態檢查清單描述您在之前，以及當您設定 StorSimple 裝置上的 hello 軟體需要 toocollect hello 資訊。 準備某些事先這項資訊可協助簡化的部署環境中的 hello StorSimple 裝置 hello 程序。 與部署您的裝置，請使用此檢查清單 tooalso 請注意，關閉 hello 設定詳細資料。

| 階段 | 參數 | 詳細資料 | 值 |
| --- | --- | --- | --- |
| **將裝置接上纜線** |序列存取 |初始裝置組態 |是/否 |
|  | | | |
| **設定和註冊裝置** |Data 0 網路設定 |Data 0 IP 位址：</br>子網路遮罩：</br>閘道器：</br>主要 DNS 伺服器：</br>主要 NTP 伺服器：</br>Web Proxy 伺服器 IP/FQDN (選擇性)︰</br>Web proxy 連接埠： | |
| &nbsp; |裝置系統管理員密碼 |密碼必須介於 8 到 15 個字元之間，包含小寫字母、大寫字母、數字和特殊字元。 | |
| &nbsp; |StorSimple Snapshot Manager 密碼 |密碼必須是 14 或 15 個字元，包含小寫字母、大寫字母、數字和特殊字元。 | |
| &nbsp; |服務註冊金鑰 |此機碼會產生從 hello Azure 傳統入口網站。 | |
| &nbsp; |服務資料加密金鑰 |Hello 裝置註冊與 hello 管理服務，透過 hello Windows PowerShell for StorSimple 時，會建立此金鑰。 複製這個金鑰，並將它儲存在安全的位置。 | |
|  | | | |
| **完成最小裝置設定** |裝置的易記名稱 |這是 hello 裝置的描述性名稱。 | |
| &nbsp; |時區 |裝置將針對所有排程的操作使用這個時區。 | |
| &nbsp; |次要 DNS 伺服器 |這是必要設定。 | |
| &nbsp; |網路介面：Data 0 控制器固定 IP |這些 IP 必須可路由傳送 toohello 網際網路。</br>控制器 0 固定 IP 位址︰</br>控制器 1 固定 IP 位址︰ | |
|  | | | |
| **其他的網路介面設定** |網路介面：Data 1</br>如果啟用 iSCSI，請勿設定 hello 閘道。 |用途：雲端/iSCSI/未使用</br>IP 位址：</br>子網路遮罩：</br>閘道器： | |
| &nbsp; |網路介面：Data 2</br>如果啟用 iSCSI，請勿設定 hello 閘道。 |用途：雲端/iSCSI/未使用</br>IP 位址：</br>子網路遮罩：</br>閘道器： | |
| &nbsp; |網路介面：Data 3</br>如果啟用 iSCSI，請勿設定 hello 閘道。 |用途：雲端/iSCSI/未使用</br>IP 位址：</br>子網路遮罩：</br>閘道器： | |
| &nbsp; |網路介面：Data 4</br>如果啟用 iSCSI，請勿設定 hello 閘道。 |用途：雲端/iSCSI/未使用</br>IP 位址：</br>子網路遮罩：</br>閘道器： | |
| &nbsp; |網路介面：Data 5</br>如果啟用 iSCSI，請勿設定 hello 閘道。 |用途：雲端/iSCSI/未使用</br>IP 位址：</br>子網路遮罩：</br>閘道器： | |
|  | | | |
| **建立磁碟區容器** |磁碟區容器名稱： |Hello 容器名稱 | |
| &nbsp; |Azure 儲存體帳戶： |儲存體帳戶名稱和存取金鑰 tooassociate 與此磁碟區容器 | |
| &nbsp; |雲端儲存體加密金鑰： |每個容器中儲存體的加密金鑰 | |
|  | | | |
| **建立磁碟區** |每個磁碟區的詳細資料 |磁碟區名稱： | |
| &nbsp; |&nbsp; |大小： | |
| &nbsp; |&nbsp; |使用類型： | |
| &nbsp; |&nbsp; |ACR 名稱： | |
| &nbsp; |&nbsp; |預設備份原則： | |
|  | | | |
| **掛接、初始化及格式化磁碟區** |每個主機伺服器連線 toohello 儲存體的詳細資料 |Windows Server 名稱： | |
| &nbsp; |&nbsp; |Windows Server IQN： | |
| &nbsp; |&nbsp; |Windows Server 磁碟區名稱： | |
| &nbsp; |&nbsp; |NTFS 掛接點/磁碟機代號： | |

## <a name="deployment-prerequisites"></a>部署必要條件
hello 下列各節說明 hello StorSimple Manager 服務，您 StorSimple 裝置和資料中心中的 hello 網路的組態先決條件。

### <a name="for-hello-storsimple-manager-service"></a>Hello StorSimple Manager 服務
在您開始前，請確定：

* 您擁有的 Microsoft 帳戶具有存取認證。
* 您擁有的 Microsoft Azure 儲存體帳戶具有存取認證。
* Hello StorSimple Manager 服務已啟用 Microsoft Azure 訂用帳戶。 您的訂用帳戶應採購 hello [Enterprise 合約](https://azure.microsoft.com/pricing/enterprise-agreement/)。
* 您必須存取 tooterminal 模擬軟體，例如 PuTTY。

### <a name="for-hello-device-in-hello-datacenter"></a>Hello hello 資料中心內的裝置
在設定之前 hello 裝置，請確認：

* 您已完全打開裝置包裝、掛接到機架上，並連接所有的電源、網路及序列存取纜線，如下所述：
  
  * [打開封裝、掛接機架，並將纜線接上 8100 裝置](storsimple-8100-hardware-installation.md)
  * [打開封裝、掛接機架，並將纜線接上 8600 裝置](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Hello 資料中心中的 hello 網路
在您開始前，請確定：

* hello 中您資料中心的防火牆連接埠是開啟的 tooallow iSCSI 和雲端流量中所述[StorSimple 裝置的網路需求](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device)。
* 資料中心中的 hello 裝置可以 toooutside 網路連線。 執行下列 hello [Windows PowerShell 4.0](http://www.microsoft.com/download/details.aspx?id=40855) （下面製成資料表） 的 cmdlet toovalidate hello 連線 toohello 網路外部。 在已連線 tooAzure （資料中心網路中） 的電腦上執行此驗證，您將在其中部署您的 StorSimple 裝置。  

| 針對此參數… | toocheck hello 有效性... | 執行這些命令/Cmdlet。 |
| --- | --- | --- |
| **IP**</br>**子網路**</br>**閘道** |這是否為有效的 IPv4 或 IPv6 位址？</br>這是否為有效的子網路？</br>這是否為有效的閘道？</br>這是否為網路上的重複 IP？ |`ping ip`</br>`arp -a`</br>hello`ping`和`arp`命令應該會失敗，表示正在使用此 IP 的 hello 資料中心網路中已沒有裝置。 |
|  | | |
| **DNS** |這是有效的 DNS 且可以解析 Azure URL 嗎？ |`Resolve-DnsName -Name www.bing.com -Server <DNS server IP address>` </br>可使用的替代命令是：</br>`nslookup --dns-ip=<DNS server IP address> www.bing.com` |
| &nbsp; |檢查連接埠 53 是否開啟。 只有在您為裝置使用外部 DNS 時才適用。 內部 DNS 應自動解決 hello 外部 Url。 |`Test-Port -comp dc1 -port 53 -udp -UDPtimeout 10000`  </br>[有關此 Cmdlet 的詳細資訊](http://learn-powershell.net/2011/02/21/querying-udp-ports-with-powershell/) |
|  | | |
| **NTP** |我們會在 NTP 伺服器輸入時觸發時間同步處理。 請在您輸入 `time.windows.com` 或公用時間伺服器時檢查 UDP 連接埠 123 是否開啟)。 |[下載並使用此指令碼](https://gallery.technet.microsoft.com/scriptcenter/Get-Network-NTP-Time-with-07b216ca)。 |
|  | | |
| **Proxy (選用)** |這是有效的 Proxy URI 和連接埠嗎？ </br> 是正確的 hello 驗證模式？ |<code>wget http://bing.com &#124; % {$_.StatusCode}</code></br>此命令應該在設定 Web Proxy 後立即執行。 如果傳回狀態碼 200，則它會指出 hello 連線就會成功。 |
| &nbsp; |流量是否可透過 Proxy 路由？ |執行 hello DNS 驗證、 NTP 核取或 HTTP 檢查您的裝置上設定 proxy 之後，一次。 這會清楚的反映流量是否在 Proxy 或其他地方遭到封鎖。 |
|  | | |
| **註冊** |檢查輸出 TCP 連接埠 443、80、9354 是否開啟。 |`Test-NetConnection -Port   443 -InformationLevel Detailed`</br>[Test-NetConnection Cmdlet 的詳細資訊](https://technet.microsoft.com/library/dn372891.aspx) |

## <a name="step-by-step-deployment"></a>逐步部署
使用您的 StorSimple 裝置 hello 遵循逐步指示 toodeploy hello 資料中心內。

## <a name="step-1-create-a-new-service"></a>步驟 1：建立新的服務
StorSimple Manager 服務可以管理多個 StorSimple 裝置。 針對您的第一個 StorSimple 裝置 hello 部署，您必須使用 toocreate 新的 StorSimple Manager 服務。

> [!IMPORTANT]
> 如果您有現有的 StorSimple Manager 服務，而且您想 toodeploy StorSimple 裝置與該服務，請略過此步驟。
> 
> 

執行下列步驟 toocreate hello StorSimple Manager 服務的新執行個體的 hello。

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

> [!IMPORTANT]
> 如果您未啟用 hello 自動建立儲存體帳戶與您的服務，您將需要 toocreate 至少一個儲存體帳戶之後，您已成功建立服務。 當您建立磁碟區容器時，將會使用此儲存體帳戶。
> 
> 如果您未自動建立儲存體帳戶，請移至太[設定新的儲存體帳戶 hello 服務](#configure-a-new-storage-account-for-the-service)如需詳細指示。
> 如果您啟用 hello 自動建立儲存體帳戶，請移至太[步驟 2： 取得 hello 服務註冊金鑰](#step-2:-get-the-service-registration-key)。
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>步驟 2： 取得 hello 服務註冊金鑰
Hello StorSimple Manager 服務已啟動並執行之後，您將需要 tooget hello 服務註冊金鑰。 這個金鑰是使用的 tooregister，而且與 hello 服務連接您的 StorSimple 裝置。

執行下列步驟在 hello Azure 傳統入口網站中的 hello。

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>步驟 3： 設定 hello 裝置透過 Windows PowerShell for StorSimple 和註冊
> [!IMPORTANT]
> 先前 tooperforming 此組態中，拔下所有 hello 網路介面不同於 DATA 0 上兩個 （主動和被動） hello 控制器。
> 
> 

Hello 遵循程序中所述，您的 StorSimple 裝置的 StorSimple toocomplete hello 初始設定使用 Windows PowerShell。 您將需要 toouse 終端機模擬軟體 toocomplete 此步驟。 如需詳細資訊，請參閱[使用 PuTTY tooconnect toohello 裝置序列主控台](#use-putty-to-connect-to-the-device-serial-console)。

[!INCLUDE [storsimple-configure-and-register-device](../../includes/storsimple-configure-and-register-device.md)]

## <a name="step-4-complete-minimum-device-setup"></a>步驟 4：完成最小量裝置設定
您的 StorSimple 裝置 hello 最低裝置設定，您都必須：

* 設定次要 DNS 伺服器 hello。
* 至少在一個網路介面上啟用 iSCSI。
* Tooboth hello 控制器指派固定的 IP 位址。

執行下列步驟在 hello Azure 傳統入口網站 toocomplete hello 最低裝置設定中的 hello。

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup.md)]

Hello 裝置設定完成之後，您必須掃描更新，並如果有的話，安裝更新。 hello 更新可能需要數個小時 toocomplete。 請依照下列中的 hello 指示[掃描並套用更新](#scan-for-and-apply-updates)。

## <a name="step-5-create-a-volume-container"></a>步驟 5：建立磁碟區容器
磁碟區容器有儲存體帳戶、 頻寬和加密設定，其包含的所有 hello 磁碟區。 您可以開始佈建您的 StorSimple 裝置上的磁碟區之前，您將需要 toocreate 磁碟區容器。

執行下列步驟在 hello Azure 傳統入口網站 toocreate 磁碟區容器中的 hello。

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>步驟 6：建立磁碟區
建立磁碟區容器之後，您可以為您的伺服器來佈建 hello StorSimple 裝置上的存放磁碟區。 執行下列步驟在 hello Azure 傳統入口網站 toocreate 磁碟區中的 hello。

> [!IMPORTANT]
> StorSimple Manager 只能建立精簡佈建的磁碟區。  您無法建立完整或部分佈建的磁碟機。
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>步驟 7：掛接、初始化及格式化磁碟區
> [!IMPORTANT]
> * 您的 StorSimple 解決方案的高可用性的 hello，我們建議您的 Windows Server 主機 （選擇性） 先前 tooconfiguring iSCSI 上設定 MPIO，您的 Windows Server 主機上。 在主機伺服器上的 MPIO 設定可確保 hello 伺服器可容許連結、 網路或介面失效。
> * MPIO 與 iSCSI 安裝和組態指示，跳過[設定 MPIO StorSimple 裝置的](storsimple-configure-mpio-windows-server.md)。 這些也會包含 hello 步驟 toomount、 初始化及格式化 StorSimple 磁碟區。
> 
> 

如果您決定 tooconfigure MPIO，執行下列步驟 toomount hello、 初始化及格式化您的 StorSimple 磁碟區。

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>步驟 8：進行備份
備份可提供磁碟區的時間點保護，並改善復原能力，同時讓還原時間降至最低。 您可以在 StorSimple 裝置上進行兩種備份類型：本機快照與雲端快照。 每一種備份類型都可以是 [排程] 或 [手動]。

執行下列步驟在 hello Azure 傳統入口網站 toocreate 排定的備份中的 hello。

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

您可以隨時進行手動備份。 程序，跳過[建立手動備份](#Create-a-manual-backup)。

## <a name="configure-a-new-storage-account-for-hello-service"></a>設定新的儲存體帳戶 hello 服務
這是選擇性的步驟，您需要 tooperform，只有當您未啟用 hello 自動建立儲存體帳戶與您的服務。 Microsoft Azure 儲存體帳戶是必要的 toocreate StorSimple 磁碟區容器。

如果您需要 toocreate 不同區域中的 Azure 儲存體帳戶，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)如需逐步指示。

執行 hello Azure 傳統入口網站，在 hello 中步驟的 hello **StorSimple Manager 服務**頁面。

[!INCLUDE [storsimple-configure-new-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>使用 PuTTY tooconnect toohello 裝置序列主控台
tooconnect tooWindows PowerShell for StorSimple 中，您需要 toouse 終端機模擬軟體，例如 PuTTY。 當您存取 hello 裝置直接透過 hello 序列主控台或從遠端電腦開啟 telnet 工作階段時，您可以使用 PuTTY。

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>掃描並套用更新
更新裝置可能會花費 1 到 4 小時。 執行下列步驟 tooscan 的 hello 和您的裝置上套用更新。

> [!NOTE]
> 如果您有不同於 Data 0 網路介面上設定的閘道，您必須 toodisable Data 2 和 Data 3 網路介面然後再安裝 hello 更新。 跳過**裝置 > 設定**和停用資料 2 和 Data 3 介面。 更新 hello 裝置之後，您應該重新啟用這些介面。
> 
> 

#### <a name="tooupdate-your-device"></a>tooupdate 您的裝置
1. Hello 裝置上**快速入門**頁面上，按一下**裝置**。 選取 hello 實體裝置，請按一下**維護**，然後按一下**掃描更新**。  
2. 建立工作 tooscan 可用的更新。 如果有可用的更新，hello**掃描更新**變更太**安裝更新**。 按一下 [安裝更新] 。 您可能會要求的 toodisable Data 2 與 Data 3 先前 tooinstalling hello 更新。 您必須停用這些網路介面或 hello 更新可能會失敗。
3. 更新工作將會建立。 監視的瀏覽過您的更新 hello 狀態**作業**。
   
   > [!NOTE]
   > Hello 更新工作啟動時，它立即顯示 hello 狀態為 50%。 hello 狀態只在 hello 更新工作完成後，然後變更 too100 百分比。 沒有 hello 更新程序的即時狀態。
   > 
   > 
4. Hello 裝置已成功更新之後，啟用這些已停用資料 2 和 Data 3 網路介面。

## <a name="get-hello-iqn-of-a-windows-server-host"></a>取得 Windows Server 主機的 IQN hello
執行下列步驟 tooget hello iSCSI hello 限定名稱 (IQN) 正在執行 Windows Server 2012 的 Windows 主機。

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>建立手動備份
執行 hello 遵循您的 StorSimple 裝置上 hello Azure 傳統入口網站 toocreate 隨需手動備份的單一磁碟區中的步驟。

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="next-steps"></a>後續步驟
* 設定 [虛擬裝置](storsimple-virtual-device-u2.md)。
* 使用 hello [StorSimple Manager 服務](https://msdn.microsoft.com/library/azure/dn772396.aspx)toomanage StorSimple 裝置。
