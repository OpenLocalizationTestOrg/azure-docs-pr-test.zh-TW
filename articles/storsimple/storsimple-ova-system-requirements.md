---
title: "aaaMicrosoft Azure StorSimple Virtual Array 系統需求 |Microsoft 文件"
description: "深入了解您的 StorSimple Virtual Array 的 hello 軟體和網路需求"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: ea1d3bca-e71b-453d-aa82-440d2638f5e3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.openlocfilehash: 7a124873fdd806d409c7279851456e6347e7ec0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-system-requirements"></a>StorSimple Virtual Array 系統需求
## <a name="overview"></a>概觀
本文將告訴您 Microsoft Azure StorSimple Virtual Array 及 hello 存取 hello 陣列的儲存體用戶端 hello 重要的系統需求。 我們建議您先仔細檢閱 hello 資訊之前您部署您的 StorSimple 系統，然後再參閱回 tooit 視部署和後續作業期間。

hello 系統需求包括：

* **儲存體用戶端的軟體需求**-描述 hello 支援虛擬化平台、 網頁瀏覽器，iSCSI 啟動器，SMB 用戶端、 最低虛擬裝置需求，以及這些作業系統的任何其他需求。
* **Hello StorSimple 裝置的網路需求**-iSCSI、 雲端或管理流量的防火牆 tooallow 中開啟該需要 toobe 提供 hello 連接埠相關資訊。

這篇文章中發行資訊 hello StorSimple 系統需求適用於僅 tooStorSimple 虛擬陣列。

* 適用於 8000 系列裝置跳過[StorSimple 8000 系列裝置的系統需求](storsimple-system-requirements.md)。
* 7000 系列裝置跳過[StorSimple 5000 7000 系列裝置的系統需求](http://onlinehelp.storsimple.com/1_StorSimple_System_Requirements)。

## <a name="software-requirements"></a>軟體需求
hello 軟體需求包括 hello 有關 hello 支援網頁瀏覽器、 SMB 版本、 虛擬化平台和 hello 最低虛擬裝置需求。

### <a name="supported-virtualization-platforms"></a>支援的虛擬化平台
| **Hypervisor** | **版本** |
| --- | --- |
| Hyper-V |Windows Server 2008 R2 SP1 和更新版本 |
| VMware ESXi |5.5 和更新版本 |

### <a name="virtual-device-requirements"></a>虛擬裝置需求
| **元件** | **需求** |
| --- | --- |
| 虛擬處理器 (核心) 的最小數目 |4 |
| 最小記憶體 (RAM) |8 GB <br> 對於檔案伺服器，8 GB 適用於 2 百萬個以下的檔案，而 16 GB 則適用於 2 - 4 百萬個檔案|
| 磁碟空間<sup>1</sup> |OS 磁碟 - 80 GB  <br></br>資料磁碟-500 GB too8 TB |
| 最小網路介面數目 |1 |
| 最小網際網路頻寬<sup>2</sup> |5 Mbps |

<sup>1</sup> - 精簡佈建

<sup>2</sup> -網路需求會根據每日資料變更速率 hello 而有所不同。 例如，如果裝置在一天期間的需求 tooback 10 GB 或更多的變更，然後 hello 透過 5 Mbps 連線的每日備份最多可能需要 too4.25 小時 （如果 hello 資料無法壓縮或重複資料刪除）。

### <a name="supported-web-browsers"></a>支援的網頁瀏覽器
| **元件** | **版本** | **其他需求/注意事項** |
| --- | --- | --- |
| Microsoft Edge |最新版本 | |
| Internet Explorer |最新版本 |通過 Internet Explorer 11 測試 |
| Google Chrome |最新版本 |通過 Chrome 46 測試 |

### <a name="supported-storage-clients"></a>支援的儲存體用戶端
下列軟體需求的 hello 對於 hello iSCSI 啟動器存取您 StorSimple Virtual Array （設定為 iSCSI 伺服器）。

| **受支援的作業系統** | **必要版本** | **其他需求/注意事項** |
| --- | --- | --- |
| Windows Server |2008R2 SP1、2012、2012R2 |StorSimple 可以建立精簡佈建和完整佈建的磁碟區。 它無法建立部分佈建的磁碟區。 StorSimple iSCSI 磁碟區只支援︰ <ul><li>Windows 基本磁碟上的簡單磁碟區。</li><li>Windows NTFS 以進行磁碟區格式化。</li> |

下列軟體需求的 hello 是 hello 存取您 StorSimple Virtual Array （設定為檔案伺服器） 的 SMB 用戶端。

| **SMB 版本** |
| --- |
| SMB 2.x |
| SMB 3.0 |
| SMB 3.02 |

> [!IMPORTANT]
> 不要複製或儲存檔案受到 Windows 加密檔案系統 (EFS) toohello StorSimple Virtual Array 檔案伺服器。這會導致不支援的組態。 
> 

### <a name="supported-storage-format"></a>支援的儲存體格式
支援 hello Azure 區塊 blob 儲存體。 不支援分頁 Blob。 關於[區塊 Blob 和分頁 Blob](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) 的其他資訊。

## <a name="networking-requirements"></a>網路需求
hello 下表列出必須在您的 iSCSI、 SMB、 雲端或管理流量的防火牆 tooallow 中開啟 toobe hello 連接埠。 下表中*中*或*輸入*參考 toohello 方向從中送用戶端要求存取您的裝置。 *Out*或*輸出*是指您的 StorSimple 裝置中 hello 部署以外傳送資料，toohello 方向： 例如，傳出 toohello 網際網路。

| **連接埠號碼<sup>1</sup>** | **內或外** | **連接埠範圍** | **必要** | **注意事項** |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP) |外 |WAN |否 |輸出連接埠用於網際網路存取 tooretrieve 更新。 <br></br>hello 傳出的 web proxy 是可由使用者設定。 |
| TCP 443 (HTTPS) |外 |WAN |是 |輸出連接埠用於存取 hello 雲端中的資料。 <br></br>hello 傳出的 web proxy 是可由使用者設定。 |
| UDP 53 (DNS) |外 |WAN |在某些情況下，請參閱附註。 |只有當您使用網際網路 DNS 伺服器時，才需要此連接埠。 <br></br> 注意，如果部署的是檔案伺服器，建議使用本機 DNS 伺服器。 |
| UDP 123 (NTP) |外 |WAN |在某些情況下，請參閱附註。 |只有當您使用網際網路 NTP 伺服器時，才需要此連接埠。<br></br> 注意，如果部署的是檔案伺服器，建議將時間與您的 Active Directory 網域控制站同步。 |
| TCP 80 (HTTP) |在 |LAN |是 |這是本機管理的 hello StorSimple 裝置上的本機 UI hello 輸入連接埠。 <br></br> 請注意，存取 hello 透過 HTTP 的本機 UI 會自動重新導向 tooHTTPS。 |
| TCP 443 (HTTPS) |在 |LAN |是 |這是本機管理的 hello StorSimple 裝置上的本機 UI hello 輸入連接埠。 |
| TCP 3260 (iSCSI) |在 |LAN |否 |此連接埠是使用的 tooaccess 資料透過 iSCSI。 |

<sup>1</sup>輸入連接埠需要 toobe 上開啟 hello 公用網際網路。

> [!IMPORTANT]
> 請確定該 hello 防火牆不會修改或解密 hello StorSimple 裝置與 Azure 之間的任何 SSL 流量。
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>防火牆規則的 URL 模式
網路系統管理員通常可以設定進階的防火牆規則根據 hello URL 模式 toofilter hello 輸入與 hello 輸出流量。 您的虛擬陣列和 hello StorSimple 裝置管理員服務相依於其他 Microsoft 應用程式，例如 Azure 服務匯流排、 Azure Active Directory 存取控制、 儲存體帳戶和 Microsoft Update servers。 hello 與這些應用程式相關聯的 URL 模式可以是使用的 tooconfigure 防火牆規則。 重要 toounderstand hello 與這些應用程式相關聯的 URL 模式可以變更它。 這又需要 hello 網路系統管理員 toomonitor 及更新您的 StorSimple，做為和所需的防火牆規則。 

我們建議您，在大部分情況下，根據固定 IP 位址為輸出流量設定防火牆規則。 不過，您可以使用下列 tooset 進階防火牆規則，需要的 toocreate 安全環境的 hello 資訊。

> [!NOTE]
> 
> * hello 裝置 （來源） Ip 應一律設 tooall hello 具備雲端功能的網路介面。 
> * hello 目的地 Ip 應該設定太[Azure 資料中心 IP 範圍](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653)。
> 
> 

| URL 模式 | 元件/功能 |
| --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |StorSimple 裝置管理員服務<br>存取控制服務<br>Azure 服務匯流排 |
| `http://*.backup.windowsazure.com` |裝置註冊 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |憑證撤銷 |
| `https://*.core.windows.net/*`<br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Azure 儲存體帳戶和監視 |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Microsoft Update 伺服器<br> |
| `http://*.deploy.akamaitechnologies.com` |Akamai CDN |
| `https://*.partners.extranet.microsoft.com/*` |支援封裝 |
| `http://*.data.microsoft.com ` |遙測服務在 Windows 中，請參閱 hello[更新客戶經驗和診斷遙測](https://support.microsoft.com/en-us/kb/3068708) |

## <a name="next-step"></a>後續步驟
* [準備您的 StorSimple Virtual Array hello 入口 toodeploy](storsimple-virtual-array-deploy1-portal-prep.md)

