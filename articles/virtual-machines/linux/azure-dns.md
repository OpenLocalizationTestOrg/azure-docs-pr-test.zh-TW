---
title: "aaaDNS Azure 中 Linux 虛擬機器的名稱解析選項"
description: "Azure IaaS 中 Linux 虛擬機器的名稱解析案例 (包括提供的 DNS 服務)：混合式外部 DNS 和自備 DNS 伺服器。"
services: virtual-machines
documentationcenter: na
author: RicksterCDN
manager: timlt
editor: tysonn
ms.assetid: 787a1e04-cebf-4122-a1b4-1fcf0a2bbf5f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/19/2016
ms.author: rclaus
ms.openlocfilehash: 7df2320b6f6b42b479bf4070ea60fe5770a78a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dns-name-resolution-options-for-linux-virtual-machines-in-azure"></a>Azure 中 Linux 虛擬機器的 DNS 名稱解析選項
Azure 預設會提供單一虛擬網路中所有虛擬機器的 DNS 名稱解析。 您可以在 Azure 託管的虛擬機器上設定專屬 DNS 服務，以實作專屬 DNS 名稱解析解決方案。 hello 下列案例應可協助您選擇適合您情況的其中一個 hello。

* [Azure 提供的名稱解析](#azure-provided-name-resolution)
* [使用專屬 DNS 伺服器的名稱解析](#name-resolution-using-your-own-dns-server)

您使用的名稱解析的 hello 類型取決於您的虛擬機器和角色執行個體需要如何與彼此 toocommunicate。

hello 下表說明案例和對應的名稱解析方案：

| **案例** | **方案** | **尾碼** |
| --- | --- | --- |
| 角色執行個體或 hello 中的虛擬機器之間的名稱解析相同虛擬網路 |[Azure 提供的名稱解析](#azure-provided-name-resolution) |主機名稱或完整網域名稱 (FQDN) |
| 不同虛擬網路中的角色執行個體或虛擬機器之間的名稱解析 |客戶管理的 DNS 伺服器將虛擬網路之間的查詢轉送供 Azure (DNS Proxy) 解析。 請參閱[使用專屬 DNS 伺服器的名稱解析](#name-resolution-using-your-own-dns-server)。 |僅 FQDN |
| 解析 Azure 中角色執行個體或虛擬機器的內部部署電腦及伺服器名稱 |客戶管理的 DNS 伺服器 (例如，內部部署的網域控制站、本機唯讀網域控制站或使用區域傳輸同步的次要 DNS)。 請參閱[使用專屬 DNS 伺服器的名稱解析](#name-resolution-using-your-own-dns-server)。 |僅 FQDN |
| 從內部部署電腦解析 Azure 主機名稱 |轉送查詢 tooa 客戶管理 proxy 中 DNS 伺服器 hello 對應的虛擬網路。 hello proxy 伺服器將轉寄查詢 tooAzure 進行解析。 請參閱[使用專屬 DNS 伺服器的名稱解析](#name-resolution-using-your-own-dns-server)。 |僅 FQDN |
| 內部 IP 的反向 DNS |[使用專屬 DNS 伺服器的名稱解析](#name-resolution-using-your-own-dns-server) |n/a |

## <a name="name-resolution-that-azure-provides"></a>Azure 提供的名稱解析
公用 DNS 名稱解析，以及 Azure 提供的內部名稱解析的虛擬機器和角色執行個體中的 hello 相同虛擬網路。 中的採用 Azure 資源管理員的虛擬網路，hello DNS 尾碼都一致 hello 虛擬網路。不需要 hello FQDN。 Tooboth 網路介面卡 (Nic) 與虛擬機器，可以指派 DNS 名稱。 雖然 Azure 提供的 hello 名稱解析不需要任何設定，它並不 hello 適用於所有部署案例中，選擇 hello 上述表格所示。

### <a name="features-and-considerations"></a>功能和注意事項
**功能：**

* 不不需要的 toouse Azure 提供的名稱解析的任何設定。
* Azure 提供的 hello 名稱解析服務是高可用性。 您不需要 toocreate 並管理您自己的 DNS 伺服器的叢集。
* hello Azure 所提供名稱解析服務可以使用您自己的 DNS 伺服器 tooresolve 以及在內部部署和 Azure 的主機名稱。
* 虛擬網路，而需要在 hello FQDN 中的虛擬機器之間提供名稱解析。
* 您可以使用最能描述部署的主機名稱，而不是使用自動產生的名稱。

<bpt id="p1">**</bpt>Considerations:<ept id="p1">**</ept>

* 建立 Azure 的 hello DNS 尾碼不能修改。
* 您無法手動註冊您自己的記錄。
* 不支援 WINS 和 NetBIOS。
* 主機名稱必須是 DNS 相容。
    名稱只能使用 0-9、a-z 和 '-'，無法以 '-' 開始或結束。 請參閱 RFC 3696 第 2 節。
* 每部虛擬機器的 DNS 查詢流量已經過節流。 節流應該不會影響大部分的應用程式。  如果觀察到要求節流，請確定用戶端快取已啟用。  如需詳細資訊，請參閱[取得 hello 從 Azure 提供名稱解析的大部分](#getting-the-most-from-name-resolution-that-azure-provides)。

### <a name="getting-hello-most-from-name-resolution-that-azure-provides"></a>取得 hello 大部分 Azure 提供的名稱解析
**用戶端快取：**

某些 DNS 查詢不會傳送 hello 網路上。 用戶端快取有助於降低延遲，並解決週期性的 DNS 查詢，從本機快取來改善恢復功能 toonetwork 不一致。 DNS 記錄包含存留時間 (TTL)，可讓 hello 快取 toostore hello 記錄越久，而不會影響記錄的有效性。 因此，用戶端快取適用於大部分的情況。

某些 Linux 發行版本預設不包含快取功能。 我們建議您檢查沒有本機快取已經之後，新增快取 tooeach Linux 虛擬機器。

有數個不同的 DNS 快取封裝可供使用，例如 dnsmasq。 以下是 hello 步驟 tooinstall dnsmasq hello 最常見的發佈：

**Ubuntu (使用 resolvconf)**
  * 安裝 hello dnsmasq 套件 ("sudo apt get 安裝 dnsmasq")。

SUSE (使用 netconf)：
1. 安裝 hello dnsmasq 套件 ("sudo zypper 安裝 dnsmasq")。
2. 啟用 hello dnsmasq 服務 (「 systemctl 啟用 dnsmasq.service")。
3. 啟動 hello dnsmasq 服務 (「 systemctl 開始 dnsmasq.service")。
4. 編輯"/ 等/sysconfig/網路/config"，並變更 NETCONFIG_DNS_FORWARDER =""太"dnsmasq"。
5. 更新 resolv.conf （「 netconfig 更新 」） tooset hello 快取為 hello 本機 DNS 解析程式。

**CentOS by Rogue Wave Software (先前稱為 OpenLogic；使用 NetworkManager)**
1. 安裝 hello dnsmasq 套件 ("sudo yum 安裝 dnsmasq")。
2. 啟用 hello dnsmasq 服務 (「 systemctl 啟用 dnsmasq.service")。
3. 啟動 hello dnsmasq 服務 (「 systemctl 開始 dnsmasq.service")。
4. 新增 「 前面加上的網域名稱伺服器 127.0.0.1;"too"/etc/dhclient-eth0.conf"。
5. hello 本機 DNS 解析程式時重新啟動 hello 網路服務 （「 網路重新啟動服務 」） tooset hello 快取

> [!NOTE]
> : hello 'dnsmasq' 封裝是的 hello 許多 DNS 快取適用於 Linux 的其中之一。 在您使用它之前，請檢查您需求的適用性，而且沒有安裝其他快取。
>
>

**用戶端重試**

DNS 主要是 UDP 通訊協定。 由於 hello UDP 通訊協定並不保證訊息傳遞，hello DNS 通訊協定本身會處理重試邏輯。 每個 DNS 用戶端 （作業系統） 可以展現不同的重試邏輯，根據 hello 建立者的喜好設定：

* Windows 作業系統會在 1 秒後重試，然後再依序隔 2、4、4 秒後重試。
* hello 預設 Linux 安裝後的重試五秒。  您應該變更這個 tooretry 五次時，在一秒的時間間隔。  

toocheck hello Linux 虛擬機器，而 'cat /etc/resolv.conf' 上的目前設定，並查看 hello [選項] 行，例如：

    options timeout:1 attempts:5

hello resolv.conf 檔案是自動產生，並不應編輯。 hello 新增 hello '選項' 列因發佈的特定步驟：

**Ubuntu** (使用 resolvconf)
1. 新增 hello 選項列 too'/etc/resolveconf/resolv.conf.d/head'。
2. 執行 ' resolvconf u' tooupdate。

**SUSE** (使用 netconf)
1. 新增 ' timeout:1 嘗試次數： 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS =""參數的 '/ 等/sysconfig/網路/config'。
2. 執行 'netconfig 更新' tooupdate。

**CentOS by Rogue Wave Software (先前稱為 OpenLogic)** (使用 NetworkManager)
1. 新增 '回應 」 選項 timeout:1 嘗試次數： 5 」' too'/etc/NetworkManager/dispatcher.d/11-dhclient'。
2. 執行 'service 網路 restart' tooupdate。

## <a name="name-resolution-using-your-own-dns-server"></a>使用專屬 DNS 伺服器的名稱解析
您的名稱解析需求可能會超越 hello Azure 提供的功能。 例如，您可能需要虛擬網路之間的 DNS 解析。 toocover 此案例中，您可以使用您自己的 DNS 伺服器。  

在虛擬網路可以正向 DNS 查詢 toorecursive Azure tooresolve 主機名稱的解析程式中的 DNS 伺服器 hello 相同虛擬網路。 例如，在 Azure 中執行的 DNS 伺服器可以回應 tooDNS 查詢它自己的 dns 區域檔案中，然後轉送其他所有的查詢 tooAzure。 這項功能可讓虛擬機器 toosee 區域檔案與 Azure 提供 （透過 hello 轉寄站） 的主機名稱中的兩個程式項目。 存取 Azure 的 toohello 遞迴解析程式會透過 hello 虛擬 IP 168.63.129.16 提供。

DNS 轉寄也可讓虛擬網路之間的 DNS 解析，並可讓 Azure 提供您在內部部署機器 tooresolve 主機名稱。 tooresolve hello DNS 伺服器的虛擬機器必須位於虛擬機器的主機名稱，在 hello 相同虛擬網路，而且是已設定的 tooforward 主機名稱查詢 tooAzure。 由於 hello DNS 尾碼不是在每個虛擬網路中，您可以使用條件轉寄規則 toosend DNS 查詢 toohello 更正進行解析的虛擬網路。 hello 圖顯示兩個虛擬網路與內部部署網路進行使用此方法的虛擬網路之間的 DNS 解析：

![虛擬網路之間的 DNS 解析](./media/azure-dns/inter-vnet-dns.png)

當您使用 Azure 提供的名稱解析時，hello 內部的 DNS 尾碼是使用 DHCP 提供 tooeach 虛擬機器。 當您使用您自己的名稱解析方案時，但這個後置詞不是提供的 toovirtual 機器因為 hello 尾碼干擾到其他 DNS 架構。 根據您的虛擬機器上的 FQDN 或 tooconfigure hello 尾碼 toorefer toomachines，您可以使用 PowerShell 或 hello API toodetermine hello 尾碼：

* Azure 資源管理員所管理的虛擬網路，hello 尾碼是可透過 hello[網路介面卡](https://msdn.microsoft.com/library/azure/mt163668.aspx)資源。 您也可以執行 hello`azure network public-ip show <resource group> <pip name>`命令 toodisplay hello 詳細資料，您的公用 IP，其中包含的 hello hello NIC 的 FQDN

如果轉送查詢 tooAzure 不符合您的需求，您需要 tooprovide 自己的 DNS 解決方案。  您的 DNS 解決方案需要：

* 提供適當的主機名稱解析，例如透過 [DDNS](../../virtual-network/virtual-networks-name-resolution-ddns.md)。 如果您使用 DDNS，您可能需要 toodisable DNS 記錄清除。 Azure 的 DHCP 租用期很長，而清除可能會提前移除 DNS 記錄。
* 提供適當的遞迴解析 tooallow 解析的外部網域名稱。
* 是可存取 （TCP 和 UDP 連接埠 53） 從它的作用是 hello 用戶端，而是可以 tooaccess hello 網際網路。
* 受到保護免於從 hello 網際網路 toomitigate 威脅外部代理程式所存取。

> [!NOTE]
> 為了達到最佳效能，當您使用虛擬機器中的 Azure DNS 伺服器時，停用 IPv6，並指派[執行個體層級公用 IP](../../virtual-network/virtual-networks-instance-level-public-ip.md) tooeach DNS 伺服器的虛擬機器。  
>
>
