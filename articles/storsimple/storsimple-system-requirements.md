---
title: "aaaStorSimple 系統需求 |Microsoft 文件"
description: "描述 Microsoft Azure StorSimple 解決方案的軟體、網路及高可用性需求和最佳作法。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2b6ca34a-d758-48e7-ab1e-4fdd80cf48d4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: alkohli
ms.openlocfilehash: ec0bb5ad2f2d4c9901da2d95147dd9daa178f6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-software-high-availability-and-networking-requirements"></a>StorSimple 軟體、高可用性和網路需求
## <a name="overview"></a>概觀
歡迎使用 tooMicrosoft Azure StorSimple。 本文說明重要的系統需求和您的 StorSimple 裝置以及存取 hello 裝置 hello 儲存體用戶端最佳作法。 我們建議您先仔細檢閱 hello 資訊之前您部署您的 StorSimple 系統，然後再參閱回 tooit 視部署和後續作業期間。

hello 系統需求包括：

* **儲存體用戶端的軟體需求**-hello 支援作業系統和任何額外的需求，這些作業系統的描述。
* **Hello StorSimple 裝置的網路需求**-iSCSI、 雲端或管理流量的防火牆 tooallow 中開啟該需要 toobe 提供 hello 連接埠相關資訊。
* **StorSimple 的高可用性需求** - 描述高可用性需求，以及 StorSimple 裝置和主機電腦的最佳作法。 

## <a name="software-requirements-for-storage-clients"></a>儲存體用戶端的軟體需求
下列軟體需求的 hello 會存取您的 StorSimple 裝置 hello 儲存體用戶端。

| 受支援的作業系統 | 必要版本 | 其他需求/注意事項 |
| --- | --- | --- |
| Windows Server |2008R2 SP1、2012、2012R2、2016 |使用下列 Windows 磁碟類型的 hello 支援 StorSimple iSCSI 磁碟區：<ul><li>基本磁碟上的簡單磁碟區</li><li>動態磁碟上的簡單及鏡像磁碟區</li></ul>只有 hello 軟體 iSCSI 啟動器 hello 作業系統中的原生支援。 不支援硬體 iSCSI 啟動器。<br></br>如果您使用 StorSimple iSCSI 磁碟區，則支援 Windows Server 2012 和 2016 精簡佈建及 ODX 功能。<br><br>StorSimple 可以建立精簡佈建和完整佈建的磁碟區。 它無法建立部分佈建的磁碟區。<br><br>重新格式化精簡佈建的磁碟區可能需要很長的時間。 我們建議您刪除 hello 磁碟區，然後建立一個新而不必重新設定。 不過，如果您仍然偏好 tooreformat 磁碟區：<ul><li>執行下列命令之前 hello 重新格式化 tooavoid 空間回收有所延遲 hello: <br>`fsutil behavior set disabledeletenotify 1`</br></li><li>Hello 格式化完成後，使用 hello 下列命令 toore 啟用空間回收：<br>`fsutil behavior set disabledeletenotify 0`</br></li><li>中所述的 hello Windows Server 2012 hotfix 套用[KB 2878635](https://support.microsoft.com/kb/2870270) tooyour Windows Server 電腦。</li></ul></li></ul></ul> 如果您要設定 StorSimple Snapshot Manager 或 StorSimple Adapter for SharePoint，請移至太[選用元件的軟體需求](#software-requirements-for-optional-components)。 |
| VMWare ESX |5.5 和 6.0 |受 VMWare vSphere 支援為 iSCSI 用戶端。 StorSimple 裝置上的 VMWare vSphere 支援 VAAI 區塊功能。 |
| Linux RHEL/CentOS |5、6 和 7 |支援具備 Open-iSCSI 啟動器第 5 版、第 6 版和第 7 版的 Linux iSCSI 用戶端。 |
| Linux |SUSE Linux 11 | |

> [!NOTE]
> StorSimple 目前不支援 IBM AIX。
> 
> 

## <a name="software-requirements-for-optional-components"></a>選用元件的軟體需求
下列軟體需求的 hello 對於 hello 選擇性 StorSimple 元件 （StorSimple Snapshot Manager 和 StorSimple Adapter for SharePoint）。

| 元件 | 主機平台 | 其他需求/注意事項 |
| --- | --- | --- |
| StorSimple Snapshot Manager |Windows Server 2008R2 SP1、2012、2012R2 |在 Windows Server 上需要使用 StorSimple Snapshot Manager，才能備份/還原鏡像動態磁碟及進行任何應用程式一致備份。<br> StorSimple Snapshot Manager 僅在 Windows Server 2008 R2 SP1 (64 位元)、Windows 2012 R2 和 Windows Server 2012 上受到支援。<ul><li>如果您使用 Window Server 2012，您必須先安裝 .NET 3.5 – 4.5，才能安裝 StorSimple Snapshot Manager。</li><li>如果您使用 Windows Server 2008 R2 SP1，您必須先安裝 Windows Management Framework 3.0，才能安裝 StorSimple Snapshot Manager。</li></ul> |
| StorSimple Adapter for SharePoint |Windows Server 2008R2 SP1、2012、2012R2 |<ul><li>StorSimple Adapter for SharePoint 僅在 SharePoint 2010 和 SharePoint 2013 上受到支援。</li><li>RBS 需要 SQL Server Enterprise Edition、2008 R2 或 2012 版。</li></ul> |

## <a name="networking-requirements-for-your-storsimple-device"></a>StorSimple 裝置的網路需求。
您的 StorSimple 裝置是鎖定的裝置。 不過，連接埠必須開啟您的 iSCSI、 雲端和管理流量的防火牆 tooallow toobe。 hello 下表列出必須在防火牆中開啟 toobe hello 連接埠。 下表中*中*或*輸入*參考 toohello 方向從中送用戶端要求存取您的裝置。 *Out*或*輸出*是指您的 StorSimple 裝置中 hello 部署以外傳送資料，toohello 方向： 例如，傳出 toohello 網際網路。

| 連接埠號碼 <sup>1,2</sup> | 內或外 | 連接埠範圍 | 必要 | 注意事項 |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP)<sup>3</sup> |外 |WAN |否 |<ul><li>輸出連接埠用於網際網路存取 tooretrieve 更新。</li><li>hello 傳出的 web proxy 是可由使用者設定。</li><li>tooallow 系統更新，此連接埠也必須針對 hello 控制器固定 Ip 開啟。</li></ul> |
| TCP 443 (HTTPS)<sup>3</sup> |外 |WAN |是 |<ul><li>輸出連接埠用於存取 hello 雲端中的資料。</li><li>hello 傳出的 web proxy 是可由使用者設定。</li><li>tooallow 系統更新，此連接埠也必須針對 hello 控制器固定 Ip 開啟。</li><li>兩個 hello 控制器也會用於此連接埠進行記憶體回收。</li></ul> |
| UDP 53 (DNS) |外 |WAN |在某些情況下，請參閱附註。 |只有當您使用網際網路 DNS 伺服器時，才需要此連接埠。 |
| UDP 123 (NTP) |外 |WAN |在某些情況下，請參閱附註。 |只有當您使用網際網路 NTP 伺服器時，才需要此連接埠。 |
| TCP 9354 |外 |WAN |是 |hello 輸出連接埠正由 hello StorSimple 裝置 toocommunicate 以 hello StorSimple Manager 服務。 |
| 3260 (iSCSI) |在 |LAN |否 |此連接埠是使用的 tooaccess 資料透過 iSCSI。 |
| 5985 |在 |LAN |否 |輸入連接埠正由 StorSimple Snapshot Manager toocommunicate hello StorSimple 裝置。<br>當您從遠端連線 tooWindows PowerShell for StorSimple over HTTP，也會使用此連接埠。 |
| 5986 |在 |LAN |否 |當您從遠端 tooWindows PowerShell for StorSimple 會透過 HTTPS 連線，則會使用此連接埠。 |

<sup>1</sup>輸入連接埠需要 toobe 上開啟 hello 公用網際網路。

<sup>2</sup>如果多個連接埠共用一個閘道組態，將根據所述的 hello 連接埠路由順序決定 hello 輸出路由的流量順序[連接埠路由](#routing-metric)底下。

<sup>3</sup> hello 控制站上您的 StorSimple 裝置固定 Ip 必須可路由傳送，而且可以 tooconnect toohello 網際網路直接或透過 hello 設定 web proxy。 hello 固定 IP 位址用於服務 hello 更新 toohello 裝置。 如果 hello 裝置控制器無法連接網際網路 hello 透過固定 Ip toohello，就能 tooupdate StorSimple 裝置。

> [!IMPORTANT]
> 請確定該 hello 防火牆不會修改或解密 hello StorSimple 裝置與 Azure 之間的任何 SSL 流量。
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>防火牆規則的 URL 模式
網路系統管理員通常可以設定進階的防火牆規則根據 hello URL 模式 toofilter hello 輸入與 hello 輸出流量。 您的 StorSimple 裝置和 hello StorSimple Manager 服務相依於其他 Microsoft 應用程式，例如 Azure 服務匯流排、 Azure Active Directory 存取控制、 儲存體帳戶和 Microsoft Update servers。 hello 與這些應用程式相關聯的 URL 模式可以是使用的 tooconfigure 防火牆規則。 重要 toounderstand hello 與這些應用程式相關聯的 URL 模式可以變更它。 這又需要 hello 網路系統管理員 toomonitor 及更新您的 StorSimple，做為和所需的防火牆規則。

我們建議您，在大部分情況下，根據固定 IP 位址為輸出流量設定防火牆規則。 不過，您可以使用下列 tooset 進階防火牆規則，需要的 toocreate 安全環境的 hello 資訊。

> [!NOTE]
> hello 裝置 （來源） Ip 應一律設 tooall hello 啟用網路介面。 hello 目的地 Ip 應該設定太[Azure 資料中心 IP 範圍](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653)。
> 
> 

#### <a name="url-patterns-for-azure-portal"></a>Azure 入口網站的 URL 模式
| URL 模式 | 元件/功能 | 裝置 IP |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |StorSimple Manager 服務<br>存取控制服務<br>Azure 服務匯流排 |啟用雲端功能的網路介面 |
| `https://*.backup.windowsazure.com` |裝置註冊 |僅限資料 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |憑證撤銷 |啟用雲端功能的網路介面 |
| `https://*.core.windows.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Azure 儲存體帳戶和監視 |啟用雲端功能的網路介面 |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Microsoft Update 伺服器<br> |僅限控制站的固定 IP |
| `http://*.deploy.akamaitechnologies.com` |Akamai CDN |僅限控制站的固定 IP |
| `https://*.partners.extranet.microsoft.com/*` |支援封裝 |啟用雲端功能的網路介面 |

#### <a name="url-patterns-for-azure-government-portal"></a>Azure Government 入口網站的 URL 模式
| URL 模式 | 元件/功能 | 裝置 IP |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.us/*`<br>`https://*.accesscontrol.usgovcloudapi.net/*`<br>`https://*.servicebus.usgovcloudapi.net/*` |StorSimple Manager 服務<br>存取控制服務<br>Azure 服務匯流排 |啟用雲端功能的網路介面 |
| `https://*.backup.windowsazure.us` |裝置註冊 |僅限資料 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |憑證撤銷 |啟用雲端功能的網路介面 |
| `https://*.core.usgovcloudapi.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Azure 儲存體帳戶和監視 |啟用雲端功能的網路介面 |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Microsoft Update 伺服器<br> |僅限控制站的固定 IP |
| `http://*.deploy.akamaitechnologies.com` |Akamai CDN |僅限控制站的固定 IP |
| `https://*.partners.extranet.microsoft.com/*` |支援封裝 |啟用雲端功能的網路介面 |

### <a name="routing-metric"></a>路由度量
路由公制是與 hello 的介面和 hello 閘道路由傳送嗨資料 toohello 指定相關聯的網路。 路由公制正由 hello 路由通訊協定 toocalculate hello 最佳路徑 tooa 指定目的地，藉以了多個路徑存在 toohello 如果相同的目的地。 hello 低 hello 路由公制，hello 高 hello 的喜好設定。

在 hello 內容的 StorSimple，如果多個網路介面和閘道設定 toochannel 流量，hello 路由度量將進入播放 toodetermine hello 相對順序取得使用中的 hello 介面。 hello 使用者無法變更 hello 路由度量。 不過，您可以使用 hello `Get-HcsRoutingTable` cmdlet tooprint 出 hello 路由表 （和度量） 在您的 StorSimple 裝置上。 如需 Get-HcsRoutingTable Cmdlet 的詳細資訊，請參閱 [針對 StorSimple 部署進行疑難排解](storsimple-troubleshoot-deployment.md)。

hello 路由公制演算法會 hello StorSimple 裝置上執行的軟體版本而有所不同。

**釋放先前 tooUpdate 1**

這包括軟體版本先前 tooUpdate hello GA 例如 1、 0.1、 0.2 或 0.3 版。 根據路由的度量的 hello 順序如下所示：

   上次設定的 10 GbE 網路介面 > 其他 10 GbE 網路介面 > 上次設定的 1 GbE 網路介面 > 其他 1 GbE 網路介面

**從 Update 1 和先前 tooUpdate 2 開始的版本**

這包括例如 1、1.1 或 1.2 的軟體版本。 hello 順序根據路由的度量決定，如下所示：

   DATA 0 > 上次設定的 10 GbE 網路介面 > 其他 10 GbE 網路介面 > 上次設定的 1 GbE 網路介面 > 其他 1 GbE 網路介面

   在 Update 1 的 DATA 0 的 hello 路由公制會 hello 最低;因此，所有的 hello 雲端流量路由傳送到 DATA 0。 如果 StorSimple 裝置上有多個已啟用雲端功能的網路介面，請記住這一點。

**從 Update 2 開始的版本**

Update 2 有數項網路相關功能的增強功能和已變更 hello 路由標準。 可以解釋 hello 行為如下所示。

* 一組預先決定的值已指派 toonetwork 介面。     
* 請考慮如下所示 toohello 指派的值不同的網路介面或時，會啟用雲端的雲端已停用，但具有設定閘道的範例資料表。 這裡指派的附註 hello 值為僅為範例值。

    | 網路介面 | 已啟用雲端 | 已停用雲端且具有閘道器 |
    |-----|---------------|---------------------------|
    | Data 0  | 1            | -                        |
    | Data 1  | 2            | 20                       |
    | Data 2  | 3            | 30                       |
    | Data 3  | 4            | 40                       |
    | Data 4  | 5            | 50                       |
    | Data 5  | 6            | 60                       |


* 在其中 hello 雲端流量會透過路由傳送 hello 網路介面的 hello 順序為：
  
    Data 0 > Data 1 > Date 2 > Data 3 > Data 4 > Data 5
  
    這可以在 hello 下列範例所說明。
  
    請考慮具有兩個已啟用雲端網路介面 (Data 0 和 Data 5) 的 StorSimple 裝置。 Data 1 到 Data 4 已停用雲端，但是具有已設定的閘道器。 hello 順序中的流量會路由傳送此裝置便會是：
  
    Data 0 (1) > Data 5 (6) > Data 1 (20) > Data 2 (30) > Data 3 (40) > Data 4 (50)
  
    *其中 hello 括號括住的數字表示 hello 各自的路由公制。*
  
    如果 Data 0 失敗，hello 雲端流量將會路由到 Data 5。 假設閘道上設定了所有其他網路，如果 Data 0 和 Data 5 toofail，hello 雲端流量會通過 Data 1。
* 如果已啟用雲端的網路介面失敗，則重試 3 次以 30 第二個延遲 tooconnect toohello 介面。 如果所有的 hello 重試失敗，hello 流量是路由的 toohello 下一個可用具備雲端功能介面由 hello 路由表。 如果所有 hello 具備雲端功能的網路介面失敗，則 hello 裝置將會容錯移轉 toohello 另一個控制器 （在此情況下沒有重新開機）。
* 如果有已啟用 iSCSI 網路介面的 VIP 失敗，則會重試 3 次 (有 2 秒的延遲)。 此行為一直 hello 舊版 hello 相同。 如果所有 hello iSCSI 網路介面都失敗，控制器容錯移轉會發生 （旁都重新開機）。
* 有 VIP 失敗時，您的 StorSimple 裝置上也會引發警示。 如需詳細資訊，請移至太[警示快速參考](storsimple-manage-alerts.md)。
* 根據重試，iSCSI 將會優先於雲端。
  
    請考慮下列範例中的 hello: StorSimple 裝置有兩個啟用的網路介面、 Data 0 和 1 的資料。 Data 0 已啟用雲端功能，而 Data 1 已啟用雲端和 iSCSI 功能。 此裝置上沒有其他網路介面啟用雲端或 iSCSI。
  
    如果資料 1 失敗，提供 hello 最後一個 iSCSI 網路介面，這會導致控制器容錯移轉 tooData 1 在 hello 另一個控制器。

### <a name="networking-best-practices"></a>網路最佳作法
此外 toohello 上方網路 hello 的最佳效能。 您的 StorSimple 解決方案的需求，請遵守 toohello 下列最佳作法：

* 請確定您的 StorSimple 裝置有專用的 40 Mbps 頻寬 (或以上) 隨時可用。 此頻寬不應共用 （或配置應該保證藉由使用 QoS 原則 hello） 與其他應用程式。
* 確定網際網路的網路連線 toohello 可用在所有的時間。 斷斷續續或不可靠網際網路連線 toohello 裝置，包括恕不另行通知，沒有網際網路連線將會導致不支援的組態。
* 需要專用的網路介面供 iSCSI 和雲端存取裝置上的，以隔離 hello iSCSI 和雲端流量。 如需詳細資訊，請參閱如何太[修改網路介面](storsimple-modify-device-config.md#modify-network-interfaces)StorSimple 裝置上。
* 請勿針對網路介面使用連結彙總控制通訊協定 (LACP) 組態。 這個組態不受支援。

## <a name="high-availability-requirements-for-storsimple"></a>StorSimple 的高可用性需求
隨附於 StorSimple 解決方案 hello hello 硬體平台都有提供基礎的資料中心中的高可用性、 容錯儲存體基礎結構的可用性和可靠性功能。 不過，有需求，而且您應遵守 toohelp 的最佳做法確保您的 StorSimple 解決方案的 hello 可用性。 部署 StorSimple 之前，請仔細檢閱下列需求和最佳作法 hello StorSimple 裝置，且主機電腦連接的 hello。

如需有關監視和維護您的 StorSimple 裝置 hello 硬體元件的詳細資訊，請移至太[使用 hello StorSimple Manager 服務 toomonitor 硬體元件與狀態](storsimple-monitor-hardware-status.md)和[StorSimple硬體元件更換](storsimple-hardware-component-replacement.md)。

### <a name="high-availability-requirements-and-procedures-for-your-storsimple-device"></a>StorSimple 裝置的高可用性需求和程序
下列資訊，請仔細檢閱 hello tooensure hello 高可用性的 StorSimple 裝置。

#### <a name="pcms"></a>PCM
StorSimple 裝置包含備援、可熱交換的電源和冷卻模組 (PCM)。 每個 PCM 已足夠容量 tooprovide 服務 hello 整個底座。 tooensure 高可用性，這兩個 Pcm 必須安裝。

* 如果電源失敗，連接讓 Pcm toodifferent 電源來源 tooprovide 可用性。
* 如果一個 PCM 失敗，請立即要求替代品。
* 當您擁有 hello 取代並準備好 tooinstall 除故障的 PCM 它。
* 請勿同時移除兩個 PCM。 hello PCM 模組包含 hello 備用電池模組。 移除這兩個的 hello Pcm 將導致沒有電池保護關機，將不會儲存 hello 裝置狀態。 如需 hello 電池的詳細資訊，請移至太[維護 hello 備用電池模組](storsimple-battery-replacement.md#maintain-the-backup-battery-module)。

#### <a name="controller-modules"></a>控制器模組
StorSimple 裝置包括備援、可熱交換的控制器模組。 在主動/被動方式運作，hello 控制器模組。 在任何時候，一個控制器模組為作用中，且會提供服務，同時 hello 另一個控制器模組是被動。 hello 被動控制器模組已開啟，並開始運作，如果 hello 作用中控制器模組故障或移除。 每個控制器模組有足夠容量 tooprovide 服務 hello 整個底座。 兩個控制器模組必須安裝的 tooensure 高可用性。

* 請隨時確定兩個控制器模組皆已安裝。
* 如果一個控制器模組失敗，請立即要求替代品。
* 只有當您擁有 hello 取代，並準備好 tooinstall 時，才移除故障的控制器模組它。 對於長期移除模組會影響氣流 hello，並因此 hello hello 系統的冷卻。
* 請確定 hello 網路連線 tooboth 控制器模組是相同的而且 hello 連接的網路介面有相同的網路組態。
* 如果控制器模組故障或需要更換，確定該 hello 另一個控制器模組再取代 hello 故障的控制器模組處於作用中狀態。 tooverify 控制器為作用中，跳過[識別您的裝置上 hello 作用中控制器](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device)。
* 請勿移除 hello 在兩個控制器模組相同的時間。 如果正在進行控制器容錯移轉，請勿關閉 hello 待命控制器模組或移除 hello 底座。
* 控制器容錯移轉後，請先等待至少五分鐘，才移除其中一個控制器模組。

#### <a name="network-interfaces"></a>網路介面
每個 StorSimple 裝置控制器模組有四個 1 GB 和兩個 10 GB 乙太網路介面。

* 確定 hello 網路連線 tooboth 控制器模組是相同的而且 hello 網路介面 hello 控制器模組介面所連接的 toohave 相同的網路組態。
* 可能的話，請將網路連線部署跨不同的交換器 tooensure 服務可用性的網路裝置故障的 hello 事件中。
* 當拔除只 hello 最後一個剩餘具備 iSCSI 功能的介面 （使用 Ip 指派)，先停用 hello 介面，然後再拔除 hello 纜線。 如果 hello 介面未插上第一次，然後它會導致 hello 作用中控制器 toofail 透過 toohello 被動控制站。 如果 hello 被動控制站也有其對應的介面已拔除，然後這兩個 hello 控制器都會重新開機多次之前侷限在一個控制器。
* 在至少兩個資料介面 toohello 網路連線每個控制器模組。
* 如果您已啟用 hello 兩個 10 GbE 介面，可部署的於不同的交換器。
* 可能的話，請使用 MPIO 上伺服器 tooensure hello 伺服器可容許連結、 網路或介面失效。

如需網路裝置的高可用性和效能的詳細資訊，請移至太[安裝 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device)或[安裝 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device)。

#### <a name="ssds-and-hdds"></a>SSD 與 HDD
StorSimple 裝置包含使用鏡像空間保護的固態硬碟 (SSD) 與硬碟 (HDD)。 使用鏡像空間可確保該 hello 裝置無法 tootolerate hello 失敗的一或多個 Ssd 或 Hdd。

* 請確定已安裝所有 SSD 和 HDD 模組。
* 如果一個 SSD 或 HDD 失敗，請立即要求替代品。
* 如果 SSD 或 HDD 故障或需要更換，請確定您移除僅 hello SSD 或需要更換的 HDD。
* 不要移除一個以上的 SSD 或 HDD hello 系統在任何時間點的時間。
  特定類型 (HDD、SSD) 的 2 個以上的磁碟失敗或在短時間範圍內的連續失敗可能會導致系統故障和潛在資料遺失。 如果發生這種情況，請 [連絡 Microsoft 支援](storsimple-contact-microsoft-support.md) 尋求協助。
* 更換期間，監視 hello**硬體狀態**在 hello**維護**頁面 hello hello Ssd 和 Hdd 磁碟機。 綠色勾號狀態表示 hello 磁碟正常或，而紅色驚嘆號則表示 SSD 或 HDD 故障。
* 我們建議您設定您需要 tooprotect 系統故障的所有磁碟區的雲端快照。

#### <a name="ebod-enclosure"></a>EBOD 機箱
StorSimple 裝置型號 8600 加法 toohello 主要機箱中包含延伸磁碟群 (EBOD) 機箱。 EBOD 包含使用鏡像空間保護的 EBOD 控制器和硬碟 (HDD)。 使用鏡像空間可確保該 hello 裝置無法 tootolerate hello 失敗的一或多個 Hdd。 hello EBOD 機箱會透過備援 SAS 纜線的連接的 toohello 主要機箱。

* 請確定這兩個 EBOD 機箱控制器模組 SAS 纜線和所有 hello 硬碟安裝妥當。
* 如果 EBOD 機箱控制器模組故障，請立即要求替代品。
* 如果 EBOD 機箱控制器模組失敗，請確定該 hello 另一個控制器模組為主動，再取代 hello 故障的模組。 tooverify 控制器為作用中，跳過[識別您的裝置上 hello 作用中控制器](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device)。
* EBOD 控制器模組更換期間，持續監視 hello hello StorSimple Manager 服務中的 hello 元件的狀態存取**維護** > **硬體狀態**。
* 如果 SAS 纜線故障或需要的更換 （Microsoft 支援服務應該涉及的 toomake 這類研判），請確定您移除僅 hello SAS 纜線需要更換。
* 請勿同時移除兩條 SAS 纜線從 hello 系統在任何時間點的時間。

### <a name="high-availability-recommendations-for-your-host-computers"></a>主機電腦的高可用性建議
請仔細檢閱這些最佳作法 tooensure hello 高可用性的主機已連線的 tooyour StorSimple 裝置。

* 使用[二節點檔案伺服器叢集組態][1]設定 StorSimple。 藉由移除單點失敗以及 hello 主機端建立備援性，hello 整個方案會成為高可用性。
* 使用持續可用 (CA) 共用可用與 Windows Server 2012 (SMB 3.0) 的高可用性的 hello 存放裝置控制器容錯移轉期間。 如需用於設定 Windows Server 2012 檔案伺服器叢集和持續可用的共用的詳細資訊，請參閱 toothis[視訊示範](http://channel9.msdn.com/Events/IT-Camps/IT-Camps-On-Demand-Windows-Server-2012/DEMO-Continuously-Available-File-Shares)。

## <a name="next-steps"></a>後續步驟
* [了解 StorSimple 系統限制](storsimple-limits.md)。
* [深入了解如何 toodeploy 您於 StorSimple 解決方案](storsimple-deployment-walkthrough-u2.md)。

<!--Reference links-->
[1]: https://technet.microsoft.com/library/cc731844(v=WS.10).aspx
