---
title: "aaaResolution Vm 和角色執行個體"
description: "Azure IaaS、混合式解決方案、不同雲端服務之間、Active Directory 以及使用專屬 DNS 伺服器的名稱解析案例  "
services: virtual-network
documentationcenter: na
author: GarethBradshawMSFT
manager: carmonm
editor: tysonn
ms.assetid: 5d73edde-979a-470a-b28c-e103fcf07e3e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/06/2016
ms.author: telmos
ms.openlocfilehash: 0ec7903cf200c1d04d75601a5b0cefe4268f3dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="name-resolution-for-vms-and-role-instances"></a>VM 與角色執行個體的名稱解析
根據您如何使用 Azure toohost IaaS、 PaaS 及混合式解決方案，您可能需要 tooallow hello Vm 和角色執行個體，您會建立 toocommunicate 彼此。 雖然可以完成這項通訊所使用的 IP 位址是更簡單 toouse 名稱可以輕鬆記住並不會變更。 

當角色執行個體和 Azure 中裝載的 Vm 需要 tooresolve 網域名稱 toointernal IP 位址時，可以使用兩種方法之一：

* [Azure 提供的名稱解析](#azure-provided-name-resolution)
* [使用您自己的 DNS 伺服器的名稱解析](#name-resolution-using-your-own-dns-server)（其中可能正查詢 toohello Azure 提供的 DNS 伺服器） 

您使用的名稱解析的 hello 類型取決於您的 Vm 和角色執行個體需要如何彼此 toocommunicate。

**hello 下表說明案例和對應的名稱解析方案：**

| **案例** | **方案** | **尾碼** |
| --- | --- | --- |
| 角色執行個體或 Vm 之間的名稱解析位於 hello 相同雲端服務或虛擬網路 |[Azure 提供的名稱解析](#azure-provided-name-resolution) |主機名稱或 FQDN |
| 位於不同虛擬網路中的角色執行個體或 VM 之間的名稱解析 |客戶管理的 DNS 伺服器將 vnet 之間的查詢轉送供 Azure (DNS Proxy) 解析。  請參閱 [使用專屬 DNS 伺服器的名稱解析](#name-resolution-using-your-own-dns-server) |僅 FQDN |
| 解析 Azure 中角色執行個體或 VM 的內部部署電腦及伺服器名稱 |客戶管理的 DNS 伺服器 (例如內部部署的網域控制站、本機唯讀網域控制站或使用區域傳輸同步的次要 DNS)。  請參閱 [使用專屬 DNS 伺服器的名稱解析](#name-resolution-using-your-own-dns-server) |僅 FQDN |
| 從內部部署電腦解析 Azure 主機名稱 |轉寄查詢 tooa 客戶管理 proxy 中的 DNS 伺服器 hello 對應 vnet，hello proxy 伺服器將轉寄查詢 tooAzure 進行解析。 請參閱 [使用專屬 DNS 伺服器的名稱解析](#name-resolution-using-your-own-dns-server) |僅 FQDN |
| 內部 IP 的反向 DNS |[使用專屬 DNS 伺服器的名稱解析](#name-resolution-using-your-own-dns-server) |n/a |
| 位於不同雲端服務，不在虛擬網路中的 VM 或角色執行個體之間的名稱解析 |不適用。 虛擬網路外部不支援不同雲端服務中 VM 和角色執行個體之間的連線。 |n/a |

## <a name="azure-provided-name-resolution"></a>Azure 提供的名稱解析
公用 DNS 名稱解析，以及 Azure 提供的內部名稱解析的 Vm 和角色執行個體中的 hello 相同虛擬網路或雲端服務。  雲端服務中的 Vm/執行個體共用相同的 DNS 尾碼 （因此 hello 單獨的主機名稱就已足夠），但傳統虛擬網路不同雲端服務中有不同的 DNS 尾碼 hello FQDN 是不同的雲端服務之間所需的 tooresolve 名稱 hello。  Hello Resource Manager 部署模型中的虛擬網路，hello DNS 尾碼一致 hello 虛擬網路上 （因此不需要 hello FQDN），且 DNS 名稱可以指派 tooboth Nic 和 Vm。 雖然 Azure 提供名稱解析不需要任何設定，它並不 hello 適用於所有部署案例中，選擇 hello 如上表所示。

> [!NOTE]
> 在 web 和背景工作角色的 hello 情況下，您也可以存取 hello 內部 IP 位址的 hello 角色名稱和執行個體使用依據編號 hello Azure 服務管理 REST API 角色執行個體。 如需詳細資訊，請參閱 [服務管理 REST API 參考](https://msdn.microsoft.com/library/azure/ee460799.aspx)。
> 
> 

### <a name="features-and-considerations"></a>功能和注意事項
**功能：**

* 容易使用： 在順序 toouse Azure 提供名稱解析不需要任何設定。
* hello Azure 提供名稱解析服務是高可用性，儲存您的 hello 需要 toocreate 和管理叢集的 DNS 伺服器。
* 可以使用您自己的 DNS 伺服器 tooresolve 搭配內部部署和 Azure 的主機名稱。
* 名稱解析是提供角色執行個體/中的 Vm 之間 hello 相同雲端服務，而不需為 fqdn。
* 使用 hello Resource Manager 部署模型，而需要在 hello FQDN 的虛擬網路中的 Vm 之間提供名稱解析。 Hello 傳統部署模型中的虛擬網路需要 hello FQDN 時解析不同雲端服務中的名稱。 
* 您可以使用最能描述部署的主機名稱，而不是使用自動產生的名稱。

<bpt id="p1">**</bpt>Considerations:<ept id="p1">**</ept>

* hello Azure 建立的 DNS 尾碼不能修改。
* 您無法手動註冊您自己的記錄。
* 不支援 WINS 和 NetBIOS。 (您無法在「Windows 檔案總管」中看到您的 VM)。
* 主機名稱必須是 DNS 相容 (只能使用 0-9、a-z 和 '-'，無法以 '-' 開始或結束。 請參閱 RFC 3696 第 2 節)。
* 每個 VM 的 DNS 查詢流量已經過節流。 這應該不會影響大部分的應用程式。  如果觀察到要求節流，請確定用戶端快取已啟用。  如需詳細資訊，請參閱[取得 hello 大部分 Azure 提供名稱解析](#Getting-the-most-from-Azure-provided-name-resolution)。
* 只有 hello 前 180 個雲端服務中的 Vm 會註冊為傳統部署模型中每個虛擬網路。 這不適用 toovirtual 網路資源管理員部署模型中。

### <a name="getting-hello-most-from-azure-provided-name-resolution"></a>取得 hello 大部分 Azure 提供名稱解析
<bpt id="p1">**</bpt>Client-side Caching:<ept id="p1">**</ept>

並非每個 DNS 查詢需要 toobe hello 網路間傳送。  用戶端快取有助於降低延遲，並改善恢復功能 toonetwork 音效解析從本機快取的重複執行 DNS 查詢。  DNS 記錄包含存留時間 (TTL) 可讓 hello 快取 toostore hello 記錄越久，而不會影響記錄的最新狀態，因此用戶端快取是適用於大部分的情況。

hello 預設 Windows DNS 用戶端都有內建的 DNS 快取。  某些 Linux 散發版本不包含快取預設情況下，建議您，加入一個 tooeach Linux VM （檢查後，還沒有在本機快取）。

有不同 DNS 快取可用的封裝，例如 dnsmasq，以下是 hello 步驟 tooinstall dnsmasq hello 最常見的散發版本上：

* Ubuntu (使用 resolvconf)：
  * 只安裝 hello dnsmasq 封裝 ("sudo apt get 安裝 dnsmasq")。
* SUSE (使用 netconf)：
  * 安裝 hello dnsmasq 套件 ("sudo zypper 安裝 dnsmasq") 
  * 啟用 hello dnsmasq 服務 (「 systemctl 啟用 dnsmasq.service") 
  * 啟動 hello dnsmasq 服務 (「 systemctl 開始 dnsmasq.service") 
  * 編輯"/ 等/sysconfig/網路/config"，並變更 NETCONFIG_DNS_FORWARDER =""太"dnsmasq"
  * 更新 resolv.conf （「 netconfig 更新 」） tooset hello 快取為 hello 本機 DNS 解析程式
* OpenLogic (使用 NetworkManager)：
  * 安裝 hello dnsmasq 套件 ("sudo yum 安裝 dnsmasq")
  * 啟用 hello dnsmasq 服務 (「 systemctl 啟用 dnsmasq.service")
  * 啟動 hello dnsmasq 服務 (「 systemctl 開始 dnsmasq.service")
  * 新增 「 前面加上的網域名稱伺服器 127.0.0.1;"too"/etc/dhclient-eth0.conf"
  * hello 本機 DNS 解析程式時重新啟動 hello 網路服務 （「 網路重新啟動服務 」） tooset hello 快取

> [!NOTE]
> hello 'dnsmasq' 封裝都只有一個 hello 許多可用的 DNS 快取適用於 Linux。  使用它之前，請檢查特定需求的適用性，而且沒有安裝其他快取。
> 
> 

<bpt id="p1">**</bpt>Client-side Retries:<ept id="p1">**</ept>

DNS 主要是 UDP 通訊協定。  Hello UDP 通訊協定並不保證訊息傳遞，如 hello DNS 通訊協定本身被處理重試邏輯。  每個 DNS 用戶端 （作業系統） 可以展現不同的重試邏輯，根據 hello 建立者喜好設定：

* Windows 作業系統會在 1 秒後重試，然後再依序隔 2、4、4 秒後重試。 
* hello 預設 Linux 安裝後的重試 5 秒。  它會建議 toochange 此 tooretry 5 次秒的間隔 1。  

toocheck hello Linux VM，'cat /etc/resolv.conf' 上的目前設定，並查看 hello [選項] 行，例如：

    options timeout:1 attempts:5

hello resolv.conf 檔案通常是自動產生，無法編輯。  hello 新增 hello [選項] 列的特定步驟會因 distro:

*  (使用 resolvconf)：
  * 新增 hello 選項列 too'/etc/resolveconf/resolv.conf.d/head' 
  * 執行 ' resolvconf u' tooupdate
*  (使用 netconf)：
  * 新增 ' timeout:1 嘗試次數： 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS =""參數的 '/ 等/sysconfig/網路/config' 
  * 執行 'netconfig 更新' tooupdate
*  (使用 NetworkManager)：
  * 新增 '回應 」 選項 timeout:1 嘗試次數： 5 」' too'/etc/NetworkManager/dispatcher.d/11-dhclient' 
  * 執行 'service 網路 restart' tooupdate

## <a name="name-resolution-using-your-own-dns-server"></a>使用專屬 DNS 伺服器的名稱解析
在您的名稱解析需求可能會超過 Azure 所提供，例如當 hello 功能使用 Active Directory 網域，或當您需要虛擬網路 (vnet) 之間的 DNS 解析，有數個情況。  toocover 這些案例中，Azure 提供 hello 能力您 toouse 您自己的 DNS 伺服器。  

虛擬網路中的 DNS 伺服器可以轉送 tooresolve 該虛擬網路內的主機名稱的 DNS 查詢 tooAzure 的遞迴解析程式。  例如，在 Azure 中執行網域控制站 (DC) 可以回應 tooDNS 查詢其網域，轉送所有其他查詢 tooAzure。  這可讓 Vm toosee 您的內部部署資源 （透過 hello DC) 和 Azure 提供的主機名稱 （透過 hello 轉寄站）。  存取 tooAzure 遞迴解析程式會透過 hello 虛擬 IP 168.63.129.16 提供。

DNS 轉寄也啟用間 vnet DNS 解析，並可讓您在內部部署機器 tooresolve Azure 提供的主機名稱。  若要 tooresolve VM 的主機名稱、 hello VM 的 DNS 伺服器必須位於 hello 相同虛擬網路，而且會設定的 tooforward 主機名稱查詢 tooAzure。  Hello DNS 尾碼不是在每個 vnet 中，您可以使用條件轉寄規則 toosend DNS 查詢 toohello 更正 vnet 進行解析。  hello 下列影像顯示兩個 vnet 與內部部署網路進行間 vnet DNS 解析使用此方法。  範例 DNS 轉寄站位於 hello [Azure 快速入門範本組件庫](https://azure.microsoft.com/documentation/templates/301-dns-forwarder/)和[GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/301-dns-forwarder)。

![虛擬網路之間的 DNS](./media/virtual-networks-name-resolution-for-vms-and-role-instances/inter-vnet-dns.png)

使用 Azure 提供的名稱解析，內部的 DNS 尾碼時 (*。 internal.cloudapp.net) 提供的 tooeach VM 使用 DHCP。  這會啟用主機名稱解析為 hello hello internal.cloudapp.net 區域中的記錄的主機名稱。  當使用您自己的名稱解析方案，hello IDN 尾碼不是會提供 tooVMs，因為它會干擾其他 DNS 的架構 （例如加入網域的案例）。  我們會改為提供一個沒有作用的預留位置 (reddog.microsoft.com)。  

如有需要可以使用 PowerShell 或 hello API 決定 hello 內部的 DNS 尾碼：

* 資源管理員部署模型中的虛擬網路，hello 尾碼是可透過 hello[網路介面卡](https://msdn.microsoft.com/library/azure/mt163668.aspx)資源或透過 hello [Get AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619434.aspx) cmdlet。    
* 在傳統部署模型中，hello 尾碼是可透過 hello[取得部署 API](https://msdn.microsoft.com/library/azure/ee460804.aspx)呼叫或透過 hello [Get-azurevm-偵錯](https://msdn.microsoft.com/library/azure/dn495236.aspx)cmdlet。

如果轉送查詢 tooAzure 不符合您的需求，您需要 tooprovide 自己的 DNS 解決方案。  您的 DNS 解決方案將需要：

* 提供適當的主機名稱解析，例如透過 [DDNS](virtual-networks-name-resolution-ddns.md)。  請注意，如果不當使用 DDNS 您可能需要 toodisable DNS 記錄清除，Azure 的 DHCP 租用很長，以及清除可能會移除 DNS 記錄。 
* 提供適當的遞迴解析 tooallow 解析的外部網域名稱。
* 是可存取 （TCP 和 UDP 連接埠 53） 從它做，是無法 tooaccess 的 hello 用戶端 hello 網際網路。
* 受到保護免於從 hello 存取網際網路，toomitigate 外部代理程式所帶來的威脅。

> [!NOTE]
> 為了達到最佳效能，使用 Azure Vm 做為 DNS 伺服器時，應該停用 IPv6 和[執行個體層級公用 IP](virtual-networks-instance-level-public-ip.md)應指派 tooeach VM 的 DNS 伺服器。  如果您選擇 toouse Windows Server 做為 DNS 伺服器，[本文](http://blogs.technet.com/b/networking/archive/2015/08/19/name-resolution-performance-of-a-recursive-windows-dns-server-2012-r2.aspx)提供額外的效能分析和最佳化。
> 
> 

### <a name="specifying-dns-servers"></a>指定 DNS 伺服器
當使用您自己的 DNS 伺服器，Azure 會提供 hello 能力 toospecify 每個虛擬網路的多個 DNS 伺服器或每個網路介面 （資源管理員）/雲端服務 （傳統）。  指定雲端服務/網路介面的 DNS 伺服器會透過所指定的虛擬網路的 hello 取得優先順序。

> [!NOTE]
> 網路連接屬性，例如 DNS 伺服器 Ip 時，應該不直接在 Windows Vm 內編輯，因為它們可能會取得在服務期間清除治療 hello 虛擬網路介面卡取得取代時。 
> 
> 

使用 hello 資源管理員部署模型時，可以在 hello 入口網站應用程式開發介面/範本中指定 DNS 伺服器 ([vnet](https://msdn.microsoft.com/library/azure/mt163661.aspx)， [nic](https://msdn.microsoft.com/library/azure/mt163668.aspx)) 或 PowerShell ([vnet](https://msdn.microsoft.com/library/mt603657.aspx)， [nic](https://msdn.microsoft.com/library/mt619370.aspx))。

使用 hello 傳統部署模型時，DNS 伺服器可以指定 hello 虛擬網路的 hello 入口網站或[hello*網路組態*檔案](https://msdn.microsoft.com/library/azure/jj157100)。  雲端服務，透過指定 hello DNS 伺服器[hello*服務組態*檔案](https://msdn.microsoft.com/library/azure/ee758710)或在 PowerShell 中 ([New-azurevm](https://msdn.microsoft.com/library/azure/dn495254.aspx))。

> [!NOTE]
> 如果您變更已部署的虛擬網路/虛擬機器的 hello DNS 設定，您需要 toorestart 每個受影響的 VM hello 變更 tootake 效果。
> 
> 

## <a name="next-steps"></a>後續步驟
資源管理員部署模型：

* [建立或更新虛擬網路](https://msdn.microsoft.com/library/azure/mt163661.aspx)
* [建立或更新網路介面卡](https://msdn.microsoft.com/library/azure/mt163668.aspx)
* [New-AzureRmVirtualNetwork](https://msdn.microsoft.com/library/mt603657.aspx)
* [New-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619370.aspx)

傳統部署模型：

* [Azure 服務組態結構描述](https://msdn.microsoft.com/library/azure/ee758710)
* [虛擬網路組態結構描述](https://msdn.microsoft.com/library/azure/jj157100)
* [使用網路組態檔設定虛擬網路](virtual-networks-using-network-configuration-file.md) 

