---
title: "aaaAzure VPN 閘道常見問題集 |Microsoft 文件"
description: "hello VPN 閘道常見問題集。 Microsoft Azure 虛擬網路跨單位連線、混合式組態連線和 VPN 閘道的常見問題集。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6ce36765-250e-444b-bfc7-5f9ec7ce0742
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/30/2017
ms.author: cherylmc,yushwang
ms.openlocfilehash: e1737f5832728f513e31f97cc7e752147faaaeb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-faq"></a>VPN 閘道常見問題集

## <a name="connecting"></a>Toovirtual 網路連接

### <a name="can-i-connect-virtual-networks-in-different-azure-regions"></a>是否可以連接不同 Azure 區域中的虛擬網路？

是。 事實上，沒有區域限制。 一個虛擬網路可以連接 tooanother hello 中的虛擬網路相同的區域，或在不同的 Azure 區域中。 

### <a name="can-i-connect-virtual-networks-in-different-subscriptions"></a>是否可以使用不同訂用帳戶連接虛擬網路？

是。

### <a name="can-i-connect-toomultiple-sites-from-a-single-virtual-network"></a>可以從單一虛擬網路連接 toomultiple 網站嗎？

您可以使用 Windows PowerShell 和 hello Azure REST Api 連接 toomultiple 站台。 請參閱 hello[多網站和 VNet 對 VNet 連線能力](#V2VMulti)常見問題集 > 一節。

### <a name="what-are-my-cross-premises-connection-options"></a>有哪些跨單位連線選項？

支援連線 hello 下列跨單位：

* 站對站 – 透過 IPsec (IKE v1 和 IKE v2) 的 VPN 連線。 此類型的連線需要 VPN 裝置或 RRAS。 如需詳細資訊，請參閱[站對站](vpn-gateway-howto-site-to-site-resource-manager-portal.md)。
* 點對站 – 透過 SSTP (安全通訊端通道通訊協定) 的 VPN 連線。 此連線不需要 VPN 裝置。 如需詳細資訊，請參閱[點對站](vpn-gateway-howto-point-to-site-resource-manager-portal.md)。
* VNet 對 VNet – 這種類型的連接是 hello 做為站對站組態相同。 VNet tooVNet 是透過 IPsec （IKE v1 和 IKE v2） 的 VPN 連線。 並不需要 VPN 裝置。 如需詳細資訊，請參閱 [VNet 對 VNet](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)。
* 這是一種可讓您 tooconnect 站對站組態的多站台 – 多個內部部署站台 tooa 虛擬網路。 如需詳細資訊，請參閱[多網站](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)。
* ExpressRoute – ExpressRoute 是從您的 WAN 不 hello 透過 VPN 連線的直接連線 tooAzure 公用網際網路。 如需詳細資訊，請參閱 hello [ExpressRoute 技術概觀](../expressroute/expressroute-introduction.md)和 hello [ExpressRoute 常見問題集](../expressroute/expressroute-faqs.md)。

如需 VPN 閘道連線的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。

### <a name="what-is-hello-difference-between-a-site-to-site-connection-and-point-to-site"></a>Hello 站對站連接和點對站台之間的差異為何？

**站對站**(IPsec/IKE VPN 通道) 介於內部部署位置與 Azure 之間。 這表示您可以從您的電腦位於您的內部部署 tooany 虛擬機器或虛擬網路，視您選擇 tooconfigure 路由和權限中的角色執行個體連接。 對於永遠可用的跨單位連線而言，這是不錯的選項，而且非常適合於混合式組態。 這種連接會依賴的 IPsec VPN 應用裝置 （硬體裝置或軟體應用裝置），必須部署在您的網路 hello 邊緣。 toocreate 這種連接，您必須具有對外開放的 IPv4 位址不是 NAT 後方。

**點對站台**(透過 SSTP VPN) 組態可讓您從單一電腦從任何地方連線 tooanything 位於您虛擬網路中。 它會使用 Windows 內建 VPN 用戶端 hello。 Hello 點對站組態的一部分，您必須安裝憑證和 VPN 用戶端組態封裝，其中包含 hello 設定可讓您的電腦 tooconnect tooany 虛擬機器或 hello 虛擬網路內的角色執行個體。 當您想 tooconnect tooa 虛擬網路，但不是位在內部，很棒。 它時也是不錯的選擇您沒有存取 tooVPN 硬體或對外的 IPv4 位址，兩者都是必要的站對站連線。

您可以設定虛擬網路 toouse 這兩個站台間和點對站同時，只要您在建立使用路由式 VPN 站對站連線您的閘道類型。 路由式 VPN 類型 hello 傳統部署模型中稱為動態閘道。

## <a name="gateways"></a>虛擬網路閘道

### <a name="is-a-vpn-gateway-a-virtual-network-gateway"></a>VPN 閘道是虛擬網路閘道嗎？

VPN 閘道是一種虛擬網路閘道。 VPN 閘道可透過公用連線在您的虛擬網路和內部部署位置之間傳送加密流量。 您也可以使用虛擬網路之間的 VPN 閘道 toosend 流量。 當您建立 VPN 閘道時，您會使用 hello-gatewaytype 的授權值 'Vpn'。 如需詳細資訊，請參閱[關於 VPN 閘道組態設定](vpn-gateway-about-vpn-gateway-settings.md)。

### <a name="what-is-a-policy-based-static-routing-gateway"></a>什麼是以原則為基礎的 (靜態路由) 閘道？

以原則為基礎的閘道會實作原則式 VPN。 原則式 Vpn 會加密，並直接透過 IPsec 通道，根據您在內部部署網路與 hello Azure VNet 之間的位址首碼的 hello 組合的封包。 hello 原則 （或傳輸選取器） 通常定義為存取清單中 hello VPN 組態。

### <a name="what-is-a-route-based-dynamic-routing-gateway"></a>什麼是以路由為基礎的 (動態路由) 閘道？

路由式閘道實作 hello 路由式 Vpn。 路由式 Vpn hello IP 轉送或路由資料表 toodirect 封包傳送至其相對應的通道介面中使用 「 路由 」。 然後 hello 通道介面加密或解密出 hello 通道 hello 封包。 路由式 Vpn 會設定為任何-到-any hello 原則或流量的選取器 （或萬用字元）。

### <a name="do-i-need-a-gatewaysubnet"></a>是否需要 'GatewaySubnet'？

是。 hello 閘道子網路包含 hello hello 虛擬網路閘道服務使用的 IP 位址。 您的 VNet 中順序 tooconfigure 虛擬網路閘道需要 toocreate 閘道子網路。 所有的閘道子網路必須命名為 'GatewaySubnet' toowork 正確。 請勿將閘道子網路命名為其他名稱。 並不會部署到 Vm 或任何其他 toohello 閘道子網路。

當您建立 hello 閘道子網路時，您可以指定包含 hello hello 子網路的 IP 位址數目。 hello hello 閘道子網路中的 IP 位址被配置 toohello 閘道服務。 部分設定需要多個 IP 位址 toobe 配置 toohello 閘道服務一樣，其他人。 您想 toomake 確定您的閘道子網路包含足夠的 IP 位址 tooaccommodate 未來的成長和可能的其他新連線設定。 所以﹐您可以建立像 /29 這麼小的閘道子網路，但建議您建立 /27 或更大 (/27、/26、/25 等) 的閘道子網路。 您想 toocreate，並確認您擁有 hello 閘道子網路會符合這些需求，請查看 hello hello 組態需求。

### <a name="can-i-deploy-virtual-machines-or-role-instances-toomy-gateway-subnet"></a>可以部署虛擬機器或角色執行個體 toomy 閘道子網路嗎？

否。

### <a name="can-i-get-my-vpn-gateway-ip-address-before-i-create-it"></a>在建立之前是否可以取得我的 VPN 閘道 IP 位址？

否。 您有 toocreate 您第一次 tooget hello 閘道的 IP 位址。 如果您刪除然後重新建立 VPN 閘道，就會變更 hello IP 位址。

### <a name="can-i-request-a-static-public-ip-address-for-my-vpn-gateway"></a>是否可以要求我的 VPN 閘道的靜態公用 IP 位址？

否。 僅支援動態 IP 位址指派。 不過，這不表示 hello IP 位址變更之後已被指派 tooyour VPN 閘道。 hello VPN 閘道 IP 位址變更為當 hello 閘道 hello 才會刪除並重新建立。 hello VPN 閘道的公用 IP 位址不會在調整大小、 重設，或其他內部維護/升級您的 VPN 閘道的變更。 

### <a name="how-does-my-vpn-tunnel-get-authenticated"></a>我的 VPN 通道如何獲得驗證？

Azure VPN 使用 PSK (預先共用金鑰) 驗證。 當我們建立 hello VPN 通道，我們就會產生預先共用的金鑰 (PSK)。 您可以變更 hello 自動產生 PSK tooyour 自己與 hello 設定預先共用金鑰 PowerShell cmdlet 或 REST API。

### <a name="can-i-use-hello-set-pre-shared-key-api-tooconfigure-my-policy-based-static-routing-gateway-vpn"></a>我可以使用 hello 設定預先共用金鑰 API tooconfigure 我以原則為基礎 （靜態路由） 閘道 VPN 嗎？

是，hello 設定預先共用金鑰 API 和 PowerShell 指令程式可以使用的 tooconfigure Azure 的以原則為基礎 （靜態） Vpn 和路由為基礎的 （動態） 路由 Vpn。

### <a name="can-i-use-other-authentication-options"></a>是否可以使用其他驗證選項？

我們很有限的 toousing 的預先共用的金鑰 (PSK) 進行驗證。

### <a name="how-do-i-specify-which-traffic-goes-through-hello-vpn-gateway"></a>如何指定的流量通過 hello VPN 閘道？

#### <a name="resource-manager-deployment-model"></a>資源管理員部署模型。

* PowerShell: hello 本機網路閘道，使用"AddressPrefix"toospecify 流量。
* Azure 入口網站： 瀏覽 toohello 區域網路閘道 > 組態 > 位址空間。

#### <a name="classic-deployment-model"></a>傳統部署模型

* Azure 入口網站： 瀏覽 toohello 傳統虛擬網路 > VPN 連線 > 站台對站 VPN 連線 > 本機站台名稱 > 本機站台 > 用戶端的位址空間。 
* 傳統入口網站： 新增您想要透過 hello 閘道傳送您在本機網路 下 hello 網路 頁面上的虛擬網路的每個範圍。 

### <a name="can-i-configure-forced-tunneling"></a>是否可以設定強制通道？

是。 請參閱 [設定強制通道](vpn-gateway-about-forced-tunneling.md)。

### <a name="can-i-set-up-my-own-vpn-server-in-azure-and-use-it-tooconnect-toomy-on-premises-network"></a>我可以將我自己在 Azure 中的 VPN 伺服器設定並使用此 tooconnect toomy 在內部部署網路嗎？

是，您可以部署您自己的 VPN 閘道或 Azure 從 hello Azure Marketplace 或建立您自己的 VPN 路由器中的伺服器。 您需要 tooconfigure 使用者定義的路由虛擬網路中 tooensure 流量路由傳送正確的內部網路與您的虛擬網路子網路之間。

### <a name="why-are-certain-ports-opened-on-my-vpn-gateway"></a>為什麼 VPN 閘道上的某些連接埠已開啟？

Azure 基礎結構通訊需要這些連接埠。 它們受到 Azure 憑證的保護 (鎖定)。 沒有適當的憑證，外部實體，包括 hello 客戶的這些閘道，將不會無法 toocause 任何這些端點生效。

VPN 閘道本質上是多重主目錄裝置使用一個點選到 hello 客戶的私人網路，以及一個 NIC 面對 hello 公用網路的 NIC。 Azure 基礎結構的實體無法挖掘客戶的私人網路，用於相容性因素，因此它們需要 tooutilize 公用端點的通訊基礎結構。 Azure 的安全性稽核會定期掃描 hello 公用端點。

### <a name="more-information-about-gateway-types-requirements-and-throughput"></a>閘道類型、需求和輸送量的詳細資訊

如需詳細資訊，請參閱[關於 VPN 閘道組態設定](vpn-gateway-about-vpn-gateway-settings.md)。

## <a name="s2s"></a>站對站連線和 VPN 裝置

### <a name="what-should-i-consider-when-selecting-a-vpn-device"></a>選取 VPN 裝置時應該考慮什麼？

我們已與裝置廠商合作驗證一組標準網站間 VPN 裝置。 已知的相容 VPN 裝置、 其對應的組態設定指示或範例和裝置規格的清單位於 hello[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)發行項。 Hello 列為已知相容的裝置系列中的所有裝置應該都使用虛擬網路。 toohelp 設定 VPN 裝置，請參閱 toohello 裝置組態範例或對應 tooappropriate 裝置家族的連結。

### <a name="where-can-i-find-vpn-device-configuration-settings"></a>哪裡可以找到 VPN 裝置組態設定？

[!INCLUDE [vpn devices](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="how-do-i-edit-vpn-device-configuration-samples"></a>如何編輯 VPN 裝置組態範例？

如需編輯裝置組態範例的相關資訊，請參閱[編輯範例](vpn-gateway-about-vpn-devices.md#editing)。

### <a name="where-do-i-find-ipsec-and-ike-parameters"></a>哪裡可以找到 IPsec 和 IKE 參數？

如需 IPsec/IKE 參數，請參閱[參數](vpn-gateway-about-vpn-devices.md#ipsec)。

### <a name="why-does-my-policy-based-vpn-tunnel-go-down-when-traffic-is-idle"></a>為什麼我的原則型 VPN 通道會在流量閒置時終止？

這是原則型 (也稱為靜態路由) VPN 閘道的預期行為。 當透過 hello 通道 hello 流量閒置超過 5 分鐘，hello 通道將會終止。 當流量會開始流向任一方向時，將會立即重新建立 hello 通道。

### <a name="can-i-use-software-vpns-tooconnect-tooazure"></a>可以使用軟體 Vpn tooconnect tooAzure 嗎？

我們支援 Windows Server 2012 路由及遠端存取 (RRAS) 伺服器進行網站間跨單位設定。

其他軟體 VPN 解決方案應該使用我們的閘道，只要它們符合 tooindustry 標準 IPsec 實作。 如需設定和支援的指示，請連絡 hello hello 軟體廠商。

## <a name="P2S"></a>點對站連線

[!INCLUDE [vpn-gateway-point-to-site-faq-include](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="V2VMulti"></a>VNet 對 VNet 和多站台連線

[!INCLUDE [vpn-gateway-vnet-vnet-faq-include](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

### <a name="can-i-use-azure-vpn-gateway-tootransit-traffic-between-my-on-premises-sites-or-tooanother-virtual-network"></a>可以使用我的內部部署站台或 tooanother 虛擬網路之間的 Azure VPN 閘道 tootransit 流量嗎？

**Resource Manager 部署模型**<br>
是。 請參閱 hello [BGP](#bgp)節的詳細資訊。

**傳統部署模型**<br>
透過 Azure VPN 閘道傳輸流量可以使用 hello 傳統部署模型，但依賴 hello 網路組態檔中靜態定義的位址空間。 BGP 尚未支援與 Azure 虛擬網路和 VPN 閘道使用 hello 傳統部署模型。 若沒有 BGP，手動定義傳輸位址空間很容易出錯，因此並不建議。

### <a name="does-azure-generate-hello-same-ipsecike-pre-shared-key-for-all-my-vpn-connections-for-hello-same-virtual-network"></a>Azure 不會產生相同的 IPsec/IKE 預先共用的 hello 鍵 hello 我所有的 VPN 連線的相同虛擬網路嗎？

否，Azure 預設會針對不同 VPN 連線產生不同的預先共用金鑰。 不過，您可以使用 hello 設定 VPN 閘道金鑰 REST API 或 PowerShell cmdlet tooset hello 索引鍵值您偏好。 hello 索引鍵必須是長度的英數字元字串是長度的介於 1 too128 個字元之間。

### <a name="do-i-get-more-bandwidth-with-more-site-to-site-vpns-than-for-a-single-virtual-network"></a>比起單一虛擬網路，是否可以使用更多的網站間 VPN，取得更多的頻寬？

否，所有 VPN 通道，包括點對站 Vpn 都共用 hello 相同 Azure VPN 閘道與 hello 可用的頻寬。

### <a name="can-i-configure-multiple-tunnels-between-my-virtual-network-and-my-on-premises-site-using-multi-site-vpn"></a>是否可以使用多網站 VPN，在我的虛擬網路與內部部署網站之間設定多個通道？

是的但是您必須將 BGP 設定這兩個通道 toohello 上相同的位置。

### <a name="can-i-use-point-to-site-vpns-with-my-virtual-network-with-multiple-vpn-tunnels"></a>是否可以使用點對站台 VPN 搭配具有多個 VPN 通道的虛擬網路？

是，點對站 (P2S) Vpn 可以搭配 hello 連接 toomultiple 在內部部署網站和其他虛擬網路的 VPN 閘道。

### <a name="can-i-connect-a-virtual-network-with-ipsec-vpns-toomy-expressroute-circuit"></a>可以連接的虛擬網路與 IPsec Vpn toomy ExpressRoute 電路嗎？

是，支援此做法。 如需詳細資訊，請參閱 [設定並存的 ExpressRoute 和網站間 VPN 連線](../expressroute/expressroute-howto-coexist-classic.md)。

## <a name="ipsecike"></a>IPsec/IKE 原則

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="bgp"></a>BGP

[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="vms"></a>跨單位連線與 VM

### <a name="if-my-virtual-machine-is-in-a-virtual-network-and-i-have-a-cross-premises-connection-how-should-i-connect-toohello-vm"></a>如果我的虛擬機器位於虛擬網路，而且有跨單位連線，應該如何我連接 toohello VM？

您有幾個選項。 如果您有 vm 啟用 RDP，您可以使用私人 IP 位址 hello 連接 tooyour 虛擬機器。 在此情況下，您可以指定 hello 私人 IP 位址和您想 tooconnect 太 (通常為 3389) 的 hello 連接埠。 您將需要 tooconfigure hello 連接埠 hello 流量的虛擬機器上。

您也可以從另一個已位於 hello 相同的虛擬機器的私人 IP 位址連線 tooyour 虛擬機器虛擬網路。 您無法使用 hello 私人 IP 位址，如果您從一個位置連接虛擬網路外部的 RDP tooyour 虛擬機器。 例如，如果您已設定點對站虛擬網路，而且您不要從您的電腦建立連接，您無法連線 toohello 虛擬機器的私人 IP 位址。

### <a name="if-my-virtual-machine-is-in-a-virtual-network-with-cross-premises-connectivity-does-all-hello-traffic-from-my-vm-go-through-that-connection"></a>如果我的虛擬機器位於具有跨單位連線的虛擬網路，並從我的 VM 的所有 hello 流量都經過該連線？

否。 目的地 hello 流量包含在 hello 虛擬網路本機網路 IP 位址範圍，您所指定的 IP 會通過 hello 虛擬網路閘道。 流量具有 hello 虛擬網路內的 IP 保持在 hello 虛擬網路內的目的地。 其他流量是透過 hello 負載平衡器 toohello 公用網路中，傳送，或使用強制通道時，如果傳送 hello Azure VPN 閘道。

### <a name="how-do-i-troubleshoot-an-rdp-connection-tooa-vm"></a>如何疑難排解 RDP 連接 tooa VM

[!INCLUDE [Troubleshoot VM connection](../../includes/vpn-gateway-connect-vm-troubleshoot-include.md)]


## <a name="faq"></a>虛擬網路常見問題集

您可以檢視其他虛擬網路資訊在 hello[虛擬網路常見問題集](../virtual-network/virtual-networks-faq.md)。

## <a name="next-steps"></a>後續步驟

* 如需 VPN 閘道的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。
* 如需 VPN 閘道組態設定的詳細資訊，請參閱[關於 VPN 閘道組態設定](vpn-gateway-about-vpn-gateway-settings.md)。
