---
title: "aaaAzure 虛擬網路常見問題集 |Microsoft 文件"
description: "有關 Microsoft Azure 虛擬網路的最常見問題集解答 toohello。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 54bee086-a8a5-4312-9866-19a1fba913d0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/18/2017
ms.author: jdial
ms.openlocfilehash: c2f9faee41b9c45e8bb196c58282d597ae732e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network-frequently-asked-questions-faq"></a>Azure 虛擬網路的常見問題 (FAQ)

## <a name="virtual-network-basics"></a>虛擬網路基本概念

### <a name="what-is-an-azure-virtual-network-vnet"></a>什麼是 Azure 虛擬網路 (VNet)？
Azure 虛擬網路 (VNet) 是網路的您自己 hello 雲端中的表示法。 它是 hello 的隔離的邏輯專用的 Azure 雲端 tooyour 訂用帳戶。 您可以使用 Vnet tooprovision 和管理虛擬私人網路 (Vpn) 在 Azure，並選擇性地連結 hello Vnet 與在 Azure 中，其他 Vnet 或您內部部署 IT 基礎結構 toocreate 混合或跨內部部署解決方案。 您所建立的每個 VNet 有它自己的 CIDR 區塊，而且可以是連結的 tooother Vnet 和內部部署網路，只要 hello CIDR 區塊不會重疊。 您也可以控制的 Vnet DNS 伺服器設定與分割的 hello VNet 至子網路。

您可以使用 VNet：

* 建立專用的僅限私人雲端 VNet 您並非每次都需要為解決方案取得跨單位組態。 當您建立 VNet 時，您的服務和您的 VNet 中的 Vm 可以直接且安全地彼此通訊 hello 雲端中。 這會保留內 hello VNet、 安全的流量，但是仍然允許 tooconfigure hello Vm 和服務需要做為方案一部分的網際網路通訊的端點連線。
* 安全地擴充資料中心與 Vnet，您可以建置傳統的站台對站台 (S2S) Vpn toosecurely 延展您的資料中心容量。 S2S Vpn 使用 IPSEC tooprovide 您公司的 VPN 閘道與 Azure 之間的安全連接。
* Vnet 可讓您啟用混合式雲端案例 hello 彈性 toosupport 某個範圍的混合式雲端案例。 您可以安全地連接雲端型應用程式的內部部署系統，例如大型主機及 Unix 系統的 tooany 型別。

### <a name="how-do-i-know-if-i-need-a-vnet"></a>如何得知是否需要 VNet？
hello[虛擬網路概觀](virtual-networks-overview.md)文章提供可協助您決定 hello 最佳網路設計選項的決策表。

### <a name="how-do-i-get-started"></a>如何開始使用？
請瀏覽 hello[虛擬網路文件](https://docs.microsoft.com/azure/virtual-network/)tooget 啟動。 本內容提供所有 hello VNet 功能的概觀和部署資訊。

### <a name="can-i-use-vnets-without-cross-premises-connectivity"></a>我可以使用不包含跨單位連線的 VNet 嗎？
是。 您可以使用不包含混合式連線能力的 VNet。 這是特別有用，如果您想 toorun Microsoft Windows Server Active Directory 網域控制站和在 Azure 中的 SharePoint 伺服器陣列。

### <a name="can-i-perform-wan-optimization-between-vnets-or-a-vnet-and-my-on-premises-data-center"></a>我可以在一或多個 VNet 與我的內部部署資料中心之間執行 WAN 最佳化嗎？

是。 您可以部署[WAN 最佳化網路的虛擬設備](https://azure.microsoft.com/marketplace/?term=wan+optimization)透過 hello Azure Marketplace 的數個廠商。

## <a name="configuration"></a>組態

### <a name="what-tools-do-i-use-toocreate-a-vnet"></a>工具的作用為何使用 toocreate VNet 嗎？
您可以使用下列工具 toocreate hello 或設定 VNet:

* Azure 入口網站 (適用於傳統與資源管理員 VNet)。
* 網路組態檔 (netcfg - 僅適用於傳統 VNet)。 請參閱 hello[設定使用網路組態檔的 VNet](virtual-networks-using-network-configuration-file.md)發行項。
* PowerShell (適用於傳統與資源管理員 VNet)。
* Azure CLI (適用於傳統與資源管理員 VNet)。

### <a name="what-address-ranges-can-i-use-in-my-vnets"></a>我可以在 VNet 中使用哪些位址範圍？
[RFC 1918](http://tools.ietf.org/html/rfc1918) 中定義的任何 IP 位址範圍。 例如：10.0.0.0/16。

### <a name="can-i-have-public-ip-addresses-in-my-vnets"></a>我可以在 VNet 擁有公用 IP 位址嗎？
是。 如需公用 IP 位址範圍的詳細資訊，請參閱 hello[虛擬網路中的公用 IP 位址空間](virtual-networks-public-ip-within-vnet.md)發行項。 您的公用 IP 位址不會直接從 hello 網際網路存取。

### <a name="is-there-a-limit-toohello-number-of-subnets-in-my-vnet"></a>是否有在 VNet 中的子網路限制 toohello 數目？
是。 讀取 hello [Azure 限制](../azure-subscription-service-limits.md#networking-limits)文件以取得詳細資料。 子網路位址空間不能互相重疊。

### <a name="are-there-any-restrictions-on-using-ip-addresses-within-these-subnets"></a>在這些子網路內使用 IP 位址是否有任何限制？
是。 Azure 會在每個子網路中保留一些 IP 位址。 hello hello 子網路的第一個和最後一個 IP 位址已保留給為了符合的通訊協定，以及 3 用於 Azure 服務的多個位址。

### <a name="how-small-and-how-large-can-vnets-and-subnets-be"></a>VNet 和子網路的大小限制為何？
hello 我們支援的最小子網路是/29，最大的 hello （使用 CIDR 子網路定義） / 8。

### <a name="can-i-bring-my-vlans-tooazure-using-vnets"></a>可以將帶我使用 Vnet 的 Vlan tooAzure 嗎？
否。 VNet 是 Layer-3 重疊。 Azure 不支援任何 Layer-2 語意。

### <a name="can-i-specify-custom-routing-policies-on-my-vnets-and-subnets"></a>可以在我的 Vnet 和子網路上指定自訂路由原則嗎？
是。 您可以使用「使用者定義的路由」(UDR)。 如需有關 UDR 的詳細資訊，請造訪 [使用者定義的路由和 IP 轉送](virtual-networks-udr-overview.md)。

### <a name="do-vnets-support-multicast-or-broadcast"></a>VNet 是否支援多點傳送或廣播？
否。 我們不支援多點傳送或廣播。

### <a name="what-protocols-can-i-use-within-vnets"></a>我可以在 VNet 中使用哪些通訊協定？
您可以在 VNet 中使用 TCP、UDP 和 ICMP TCP/IP 通訊協定。 多點傳送、廣播、IP-in-IP 封裝式封包和 Generic Routing Encapsulation (GRE) 封包在 VNet 內會遭到封鎖。 

### <a name="can-i-ping-my-default-routers-within-a-vnet"></a>我可以在 VNet 中偵測我的預設路由器嗎？
否。

### <a name="can-i-use-tracert-toodiagnose-connectivity"></a>可以使用 tracert toodiagnose 連線嗎？
否。

### <a name="can-i-add-subnets-after-hello-vnet-is-created"></a>可以在 hello VNet 建立後新增子網路嗎？
是。 子網路可以加入 tooVNets 在任何時候只要 hello 子網路位址不是在 hello VNet 中的另一個子網路的一部分。

### <a name="can-i-modify-hello-size-of-my-subnet-after-i-create-it"></a>我在建立之後可以修改我的子網路的 hello 大小嗎？
是。 如果其中沒有部署任何 VM 或服務，您可以新增、移除、展開或縮小子網路。

### <a name="can-i-modify-subnets-after-i-created-them"></a>我可以在建立子網路之後進行修改嗎？
是。 您可以新增、 移除和修改使用 VNet hello CIDR 區塊。

### <a name="can-i-connect-toohello-internet-if-i-am-running-my-services-in-a-vnet"></a>我可以連接 toohello 網際網路如果在 VNet 中執行我的服務嗎？
是。 VNet 中部署的所有服務都可以都連線 toohello 網際網路。 在 Azure 中部署每個雲端服務有指派 tooit 公開可定址的 VIP。 您必須 toodefine PaaS 角色的輸入的端點和端點的虛擬機器 tooenable hello 從這些服務 tooaccept 連接網際網路。

### <a name="do-vnets-support-ipv6"></a>VNet 是否支援 IPv6？
否。 目前您無法使用 IPv6 搭配 VNet。

### <a name="can-a-vnet-span-regions"></a>VNet 可以跨區域嗎？
否。 VNet 是有限的 tooa 單一區域。

### <a name="can-i-connect-a-vnet-tooanother-vnet-in-azure"></a>可以連接的 VNet tooanother 在 Azure 中的 VNet 嗎？
是。 您可以連接一個 VNet tooanother VNet 使用：
- Azure VPN 閘道。 讀取 hello[設定 VNet 對 VNet 連線](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)文件以取得詳細資料。 
- VNet 對等互連。 讀取 hello [VNet 對等互連概觀](virtual-network-peering-overview.md)文件以取得詳細資料。

## <a name="name-resolution-dns"></a>名稱解析 (DNS)

### <a name="what-are-my-dns-options-for-vnets"></a>適用於 VNet 的 DNS 選項為何？
使用 hello 決策表上 hello [Vm 和角色執行個體的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md)提供頁面 tooguide 您完成所有 hello DNS 選項。

### <a name="can-i-specify-dns-servers-for-a-vnet"></a>我可以指定適用於 VNet 的 DNS 伺服器嗎？
是。 您可以在 hello VNet 設定中指定 DNS 伺服器 IP 位址。 這將會套用為 hello 預設 DNS 伺服器 hello VNet 中的所有 Vm。

### <a name="how-many-dns-servers-can-i-specify"></a>我可以指定多少部 DNS 伺服器？
參考 hello [Azure 限制](../azure-subscription-service-limits.md#networking-limits)文件以取得詳細資料。

### <a name="can-i-modify-my-dns-servers-after-i-have-created-hello-network"></a>我已建立 hello 網路之後可以修改我的 DNS 伺服器嗎？
是。 您可以隨時變更您的 VNet hello DNS 伺服器清單。 如果您變更您的 DNS 伺服器清單，您需要 toorestart 每個 hello Vm 在 VNet 中，toopick 出 hello 新 DNS 伺服器。

### <a name="what-is-azure-provided-dns-and-does-it-work-with-vnets"></a>什麼是 Azure 提供的 DNS，以及它是否可搭配 VNet 使用？
Azure 提供的 DNS 是由 Microsoft 所提供的多租用戶 DNS 服務。 Azure 會註冊您在此服務中的所有 VM 和雲端服務角色執行個體。 此服務依據主機名稱提供名稱解析，讓 Vm 和角色執行個體包含在相同的雲端服務，並依 FQDN Vm 和角色執行個體中的 hello 相同的 hello VNet。 讀取 hello [Vm 和角色執行個體的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md)文章 toolearn 深入了解 DNS。

> [!NOTE]
> 目前限制在此時間 toohello 第一次 100 個雲端服務中使用 Azure 提供的 DNS 進行跨租用戶名稱解析的 VNet。 如果您使用自己的 DNS 伺服器，則不適用這項限制。
> 
> 

### <a name="can-i-override-my-dns-settings-on-a-per-vm--service-basis"></a>我是否可以根據每個 VM/服務來覆寫 DNS 設定？
是。 您可以設定 DNS 伺服器上每個雲端服務基礎 toooverride hello 預設網路設定。 不過，我們建議您盡可能使用全網路 DNS。

### <a name="can-i-bring-my-own-dns-suffix"></a>我可以加上自己的 DNS 尾碼嗎？
否。 您無法針對 VNet 指定自訂的 DNS 尾碼。

## <a name="connecting-virtual-machines"></a>連接虛擬機器

### <a name="can-i-deploy-vms-tooa-vnet"></a>可以部署 Vm tooa VNet 嗎？
是。 透過 hello Resource Manager 部署模型部署 VM 的所有網路介面 (NIC) 附加的 tooa 都必須連接的 tooa VNet。 透過 hello 傳統部署模型所部署的 Vm 可選擇性地連接的 tooa VNet。

### <a name="what-are-hello-different-types-of-ip-addresses-i-can-assign-toovms"></a>什麼是 hello 不同類型的 IP 位址可以指派 tooVMs？
* **私用：**指派 tooeach 內每個 VM NIC。 hello 位址指派使用 hello 靜態或動態方法。 從您指定 hello VNet 子網路設定中的 hello 範圍指派私用 IP 位址。 透過 hello 傳統部署模型所部署的資源指派私人 IP 位址，即使它們未連接 tooa VNet。 以 hello 動態方法會維持指派一個私人 IP 位址指派 tooa 資源，直到刪除 hello 資源 (Vm 或雲端服務部署位置)。 已經在 hello 停止 （取消配置） 的狀態之後，重新啟動 VM 時，可能會變更與 hello 動態方法指派的私人 IP 位址。 指定與 hello 靜態方法會維持指派 tooa 資源，直到刪除 hello 資源私用 IP 位址。 如果您需要 tooensure 該 hello 私人 IP 位址資源的絕對不會改變刪除 hello 資源之前，將私人 IP 位址指派與 hello 靜態方法。
* **公用：**選擇性地指派的 tooNICs 附加 tooVMs 透過 hello Azure Resource Manager 部署模型部署。 hello 位址可以指派與 hello 靜態或動態配置方法。 透過 hello 傳統部署模型所部署的所有 Vm 和雲端服務角色執行個體存在於雲端服務，會指派*動態*，公用虛擬 IP (VIP) 位址。 公用*靜態* IP 位址，稱為[保留的 IP 位址](virtual-networks-reserved-public-ip.md)，可選擇性地被指派為 VIP。 您可以指派公用 IP 位址 tooindividual 透過 hello 傳統部署模型部署到 Vm 或雲端服務的角色執行個體。 這些位址稱為[執行個體層級公用 IP (ILPIP](virtual-networks-instance-level-public-ip.md)位址，並可動態指派。

### <a name="can-i-reserve-a-private-ip-address-for-a-vm-that-i-will-create-at-a-later-time"></a>我可以為稍後建立的 VM 保留私人 IP 位址嗎？
否。 您不能保留私人 IP 位址。 私人 IP 位址是否可用則會由 hello DHCP 伺服器指派 tooa VM 或角色執行個體。 VM 可能會或可能不是您想要 hello 私用 IP 位址 toobe 指派給一個 hello。 不過，您就可以變更 hello 私人 IP 位址已經建立 VM tooany 可用的私人 IP 位址。

### <a name="do-private-ip-addresses-change-for-vms-in-a-vnet"></a>VNet 中的私人 IP 位址會根據 VM 進行變更嗎？
這要看狀況。 VM 中仍會保留動態私人 IP 位址，直到 IP 位址停止 (重新分配) 或刪除為止。 靜態私人 IP 位址在刪除後才會從 VM 中釋放。

### <a name="can-i-manually-assign-ip-addresses-toonics-within-hello-vm-operating-system"></a>我可以手動將 hello VM 作業系統內的 IP 位址 tooNICs 嗎？
可以，但我們不建議這樣做。 手動變更 VM 的作業系統內的 NIC hello IP 位址可能會導致 toolosing 連線 toohello VM toochange hello 分派 tooa NIC hello Azure VM 中的 IP 位址一樣。

### <a name="what-happens-toomy-ip-addresses-if-i-stop-a-cloud-service-deployment-slot-or-shutdown-a-vm-from-within-hello-operating-system"></a>如果停止雲端服務部署位置或關機的 VM 從 hello 作業系統內，怎樣 toomy IP 位址？
不會受到影響。 hello IP 位址 (公開 VIP，公用和私用) 會保留指派的 toohello 雲端服務部署位置或 VM。 動態位址只會在 VM 停止 (重新分配) 或刪除，或雲端服務部署位置已刪除時釋放。 按一下 hello**停止**hello Azure 入口網站內的 VM 組 （取消配置） 其狀態 tooStopped 按鈕。 在此情況下，hello VM 將會遺失其 IP 位址。

### <a name="can-i-move-vms-from-one-subnet-tooanother-subnet-in-a-vnet-without-re-deploying"></a>我可以移動 Vm 在 VNet 中的一個子網路 tooanother 子網路不需要重新部署嗎？
是。 您可以找到詳細資訊，在 hello[如何 toomove VM 或角色執行個體 tooa 不同的子網路](virtual-networks-move-vm-role-to-subnet.md)發行項。

### <a name="can-i-configure-a-static-mac-address-for-my-vm"></a>我可以針對 VM 設定靜態 MAC 位址嗎？
否。 MAC 位址無法以靜態方式設定。

### <a name="will-hello-mac-address-remain-hello-same-for-my-vm-once-it-has-been-created"></a>Hello MAC 位址會保留相同 hello 對我的 VM，一旦建立之後嗎？
是，hello MAC 位址會維持的 hello 相同的 VM 部署透過 hello 資源管理員和傳統部署模型刪除為止。 先前，如果 hello VM 已停止 （取消配置），但即使 hello VM 處於 hello 取消配置狀態現在保留 hello MAC 位址，已發行 hello MAC 位址。

### <a name="can-i-connect-toohello-internet-from-a-vm-in-a-vnet"></a>我可以連接 toohello 從 VM 在 VNet 中的網際網路嗎？
是。 VNet 中部署的所有 Vm 和雲端服務角色執行個體可以連線 toohello 網際網路。

## <a name="azure-services-that-connect-toovnets"></a>連接 tooVNets 的 azure 服務

### <a name="can-i-use-azure-app-service-web-apps-with-a-vnet"></a>我可以搭配使用 Azure App Service Web Apps 和 VNet 嗎？
是。 您可以使用 ASE (App Service 環境) 在 VNet 中部署 Web Apps。 如果您已針對 VNet 設定點對站連線，則 Web Apps 可以安全地連線並存取 Azure VNet 中的資源。 如需詳細資訊，請參閱下列文章 hello:

* [在 App Service 環境中建立 Web Apps](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [將您的應用程式與 Azure 虛擬網路整合](../app-service-web/web-sites-integrate-with-vnet.md)
* [使用 VNet 整合和混合式連接搭配 Web Apps](../app-service-web/web-sites-integrate-with-vnet.md#hybrid-connections-and-app-service-environments)

### <a name="can-i-deploy-cloud-services-with-web-and-worker-roles-paas-in-a-vnet"></a>我可以在 VNet 中使用 Web 和背景工作角色 (PaaS) 部署雲端服務嗎？
是。 您可以 (選擇性地) 在 VNet 內部署雲端服務角色執行個體。 toodo 因此，您的服務組態 hello 網路組態區段中指定 hello VNet 名稱和 hello 角色/子網路對應。 您不需要 tooupdate 任何二進位編碼檔案。

### <a name="can-i-connect-a-virtual-machine-scale-set-vmss-tooa-vnet"></a>可以連接的虛擬機器設定小數位數 (VMSS) tooa VNet 嗎？
是。 您必須連接 VMSS tooa VNet。

### <a name="can-i-move-my-services-in-and-out-of-vnets"></a>我可以將服務移入和移出 VNet 嗎？
否。 您無法將服務移入和移出 VNet。 您將有 toodelete 和重新部署 hello 服務 toomove 它 tooanother VNet。

## <a name="security"></a>安全性

### <a name="what-is-hello-security-model-for-vnets"></a>Vnet 的 hello 安全性模型是什麼？
Vnet 彼此完全隔離，並裝載在 hello Azure 基礎結構的其他服務。 VNet 是一種信任邊界。

### <a name="can-i-restrict-inbound-or-outbound-traffic-flow-toovnet-connected-resources"></a>我可以限制傳入或傳出流量流程 tooVNet 連接資源嗎？
是。 您可以套用[網路安全性群組](virtual-networks-nsg.md)tooindividual 子網路內的 VNet，Nic 附加 tooa VNet，或兩者。

### <a name="can-i-implement-a-firewall-between-vnet-connected-resources"></a>我可以在與 VNet 連線的資源之間實作防火牆嗎？
是。 您可以部署[防火牆網路的虛擬設備](https://azure.microsoft.com/en-us/marketplace/?term=firewall)透過 hello Azure Marketplace 的數個廠商。

### <a name="is-there-information-available-about-securing-vnets"></a>我可以怎樣取得關於保護 VNet 的資訊？
是。 請參閱 hello [Azure 網路安全性概觀](../security/security-network-overview.md)文件以取得詳細資料。

## <a name="apis-schemas-and-tools"></a>API、結構描述和工具

### <a name="can-i-manage-vnets-from-code"></a>我可以從程式碼管理 VNet 嗎？
是。 您可以使用 REST Api 的 Vnet 中 hello [Azure Resource Manager](https://msdn.microsoft.com/library/mt163658.aspx)和[傳統 （服務管理）](http://go.microsoft.com/fwlink/?LinkId=296833)) 部署模型。

### <a name="is-there-tooling-support-for-vnets"></a>是否有工具支援 VNet？
是。 深入了解如何使用：
- hello hello 透過 Azure 入口網站 toodeploy Vnet [Azure Resource Manager](virtual-networks-create-vnet-arm-pportal.md)和[傳統](virtual-networks-create-vnet-classic-pportal.md)部署模型。
- 透過 hello 部署 Vnet PowerShell toomanage[資源管理員](/powershell/resourcemanager/azurerm.network/v3.1.0/azurerm.network.md)和[傳統](/powershell/module/azure/?view=azuresmps-3.7.0)部署模型。
- hello [Azure 命令列介面 (CLI)](../virtual-machines/azure-cli-arm-commands.md#azure-network-commands-to-manage-network-resources) toomanage 透過兩種部署模型所部署的 Vnet。  
