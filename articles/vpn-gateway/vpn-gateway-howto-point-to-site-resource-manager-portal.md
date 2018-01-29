---
title: "使用點對站和原生 Azure 憑證驗證將電腦連線至 Azure 虛擬網路︰Azure 入口網站 | Microsoft Docs"
description: "使用憑證驗證建立點對站 VPN 閘道連線，進而將電腦安全地連線到您的 Azure 虛擬網路。 本文適用於 Resource Manager 部署模型並使用 Azure 入口網站。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a15ad327-e236-461f-a18e-6dbedbf74943
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2018
ms.author: cherylmc
ms.openlocfilehash: 39129572ac9908429dc9b9ef64930e896afc355f
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="configure-a-point-to-site-connection-to-a-vnet-using-native-azure-certificate-authentication-azure-portal"></a>使用原生 Azure 憑證驗證設定 VNet 的點對站連線：Azure 入口網站

本文顯示如何使用 Azure 入口網站，在 Resource Manager 部署模型中建立具有點對站連線的 VNet。 此組態會使用憑證來進行驗證。 此組態會由 Azure VPN 閘道執行憑證驗證，而不是由 RADIUS 伺服器來執行。 您也可從下列清單中選取不同的選項，以使用不同的部署工具或部署模型來建立此組態：

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Azure 入口網站 (傳統)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

點對站 (P2S) VPN 閘道可讓您建立從個別用戶端電腦到您的虛擬網路的安全連線。 當您想要從遠端位置 (例如當您從住家或會議進行遠距工作) 連線到您的 VNet 時，點對站 VPN 連線很實用。 當您只有少數用戶端必須連線至 VNet 時，P2S VPN 也是很實用的方案 (而不是使用站對站 VPN)。 P2S VPN 連線會從 Windows 和 Mac 裝置啟動。

您可使用下列驗證方法來與用戶端連線：

* RADIUS 伺服器
* VPN 閘道原生 Azure 憑證驗證

本文會協助您設定使用原生 Azure 憑證驗證來進行驗證的 P2S 組態。 如果您想要使用 RADIUS 來驗證要連線的使用者，請參閱[使用 RADIUS 驗證的 P2S](point-to-site-how-to-radius-ps.md)。

![將電腦連接至 Azure VNet - 點對站連線圖表](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/p2snativeps.png)

點對站連線不需要 VPN 裝置或公眾對應 IP 位址。 P2S 會建立透過 SSTP (安全通訊端通道通訊協定) 或 IKEv2 的 VPN 連線。

* SSTP 是僅在 Windows 用戶端平台上支援的 SSL 型 VPN 通道。 它可以穿透防火牆，這是從任何地方連線到 Azure 的理想選項。 我們在伺服器端上支援 SSTP 1.0、1.1 和 1.2 版。 用戶端會決定要使用的版本。 若為 Windows 8.1 和更新版本，SSTP 預設使用 1.2。

* IKEv2 VPN，標準型 IPsec VPN 解決方案。 IKEv2 VPN 可用於從 Mac 裝置連線 (OSX 版本 10.11 和更新版本)。

點對站原生 Azure 憑證驗證連線需要下列各項：

* RouteBased VPN 閘道。
* 已上傳至 Azure 之根憑證的公開金鑰 (.cer 檔案)。 一旦上傳憑證，憑證就會被視為受信任的憑證並且用於驗證。
* 用戶端憑證是從根憑證產生，並安裝在每部即將連線到 VNet 的用戶端電腦上。 此憑證使用於用戶端憑證。
* VPN 用戶端組態。 VPN 用戶端組態檔包含要讓用戶端連線到 VNet 所需的資訊。 此檔案會設定作業系統原生的現有 VPN 用戶端。 您必須使用組態檔中的設定來設定每個進行連線的用戶端。

如需點對站連線的詳細資訊，請參閱[關於點對站連線](point-to-site-about.md)。

#### <a name="example"></a>範例值

您可以使用下列值來建立測試環境，或參考這些值來進一步了解本文中的範例：

* **VNet 名稱︰**VNet1
* **位址空間：**192.168.0.0/16<br>在此範例中，我們只使用一個位址空間。 您可以針對 VNet 使用一個以上的位址空間。
* **子網路名稱：**FrontEnd
* **子網路位址範圍：**192.168.1.0/24
* **訂用帳戶：**如果您有一個以上的訂用帳戶，請確認您使用正確的訂用帳戶。
* **資源群組：**TestRG
* **位置：**美國東部
* **GatewaySubnet：**192.168.200.0/24<br>
* **DNS 伺服器：**(選擇性) 您想要用於名稱解析之 DNS 伺服器的 IP 位址。
* **虛擬網路閘道名稱：**VNet1GW
* **閘道類型：**VPN
* **VPN 類型：**路由式
* **公用 IP 位址名稱：**VNet1GWpip
* **連線類型：**點對站
* **用戶端位址集區：**172.16.201.0/24<br>使用這個點對站連線來連線到 VNet 的 VPN 用戶端，會收到來自用戶端位址集區的 IP 位址。

## <a name="createvnet"></a>1.建立虛擬網路

在開始之前，請確認您有 Azure 訂用帳戶。 如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial)。
[!INCLUDE [Basic Point-to-Site VNet](../../includes/vpn-gateway-basic-p2s-vnet-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>2.新增閘道子網路

將虛擬網路連接到閘道之前，您必須先建立虛擬網路要連接的閘道子網路。 閘道服務會使用閘道子網路中指定的 IP 位址。 如果可能，請使用 /28 或 /27 的 CIDR 區塊來建立閘道子網路，以提供足夠的 IP 位址來因應未來額外的組態需求。

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-p2s-rm-portal-include.md)]

## <a name="dns"></a>3.指定 DNS 伺服器 (選擇性)

建立虛擬網路之後，您可以新增 DNS 伺服器的 IP 位址，以便處理名稱解析。 在此此組態中，DNS 伺服器為選擇性，但如果您想要進行名稱解析則，為必要。 指定一個值並不會建立新的 DNS 伺服器。 您指定的 DNS 伺服器 IP 位址應該是可以解析您所連線之資源名稱的 DNS 伺服器。 在此範例中，我們使用了私人 IP 位址，但這可能不是您 DNS 伺服器的 IP 位址。 請務必使用您自己的值。 您指定的值會供部署至 VNet 的資源使用，而非供 P2S 連線或 VPN 用戶端使用。

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="creategw"></a>4.建立虛擬網路閘道

[!INCLUDE [create-gateway](../../includes/vpn-gateway-add-gw-p2s-rm-portal-include.md)]

## <a name="generatecert"></a>5.產生憑證

憑證是 Azure 用於驗證透過點對站 VPN 連線來連線至 VNet 的用戶端。 一旦您取得根憑證，您可將公開金鑰資訊[上傳](#uploadfile)至 Azure。 根憑證則會被視為 Azure「信任的」，可供透過 P2S 連線至虛擬網路。 您也可以從受信任的根憑證產生用戶端憑證，然後將它們安裝在每部用戶端電腦上。 在用戶端初始 VNet 連線時，用戶端憑證用來驗證用戶端。 

### <a name="getcer"></a>1.取得根憑證的 .cer 檔案

[!INCLUDE [root-certificate](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="generateclientcert"></a>2.產生用戶端憑證 

[!INCLUDE [generate-client-cert](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="addresspool"></a>6.新增用戶端位址集區

用戶端位址集區是您指定的私人 IP 位址範圍。 透過點對站連線的用戶端會收到來自這個範圍內的 IP 位址。 使用不會重疊的私人 IP 位址範圍搭配您從其連線的內部部署位置，或搭配您要連線至的 VNet。

1. 一旦建立虛擬網路閘道，請瀏覽至虛擬網路閘道頁面的 [設定] 區段。 在 [設定] 區段中，按一下 [點對站組態] 以開啟 [組態] 頁面。

  ![點對站頁面](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/gatewayblade.png)
2. 在 [點對站組態] 頁面，您可以刪除自動填滿的區域，然後新增您要使用的私人 IP 位址範圍。 按一下 [儲存]  來驗證和儲存設定。

  ![用戶端位址集區](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/ipaddresspool.png)

## <a name="uploadfile"></a>7.上傳根憑證公開憑證資料

建立閘道之後，您可將根憑證的公開金鑰資訊上傳至 Azure。 一旦上傳公開憑證資料，Azure 就可以使用它來驗證已安裝從受信任根憑證產生之用戶端憑證的用戶端。 您可以上傳其他受信任的根憑證檔案 (最多總計 20 個憑證)。

1. 新增憑證時，是在 [點對站組態] 頁面的 [根憑證] 區段中新增。  
2. 請確定您以 Base-64 編碼 X.509 (.cer) 檔案形式匯出根憑證。 您需要以這種格式匯出憑證，以便可以使用文字編輯器開啟憑證。
3. 使用文字編輯器 (例如「記事本」) 開啟憑證。 複製憑證資料時，請確定您是以連續一行的形式複製文字，而不含歸位字元或換行字元。 您可能必須將文字編輯器中的檢視修改成 [顯示符號] 或 [顯示所有字元]，才能看到歸位字元和換行字元。 請只以連續一行的形式複製下列區段：

  ![憑證資料](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/copycert.png)
4. 將憑證資料貼到 [公開憑證資料] 欄位中。 提供憑證「名稱」，然後按一下 [儲存]。 您最多可新增 20 個受信任的根憑證。

  ![憑證上傳](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/rootcertupload.png)

## <a name="installclientcert"></a>8.安裝匯出的用戶端憑證

如果您想要從不同於用來產生用戶端憑證的用戶端電腦建立 P2S 連線，您需要安裝用戶端憑證。 安裝用戶端憑證時，您需要匯出用戶端憑證時所建立的密碼。

請確定用戶端憑證已隨著整個憑證鏈結匯出為 .pfx (這是預設值)。 否則，根憑證資訊不存在於用戶端電腦上，而且用戶端將無法正確驗證。

如需安裝步驟，請參閱[安裝用戶端憑證](point-to-site-how-to-vpn-client-install-azure-cert.md)。

## <a name="clientconfig"></a>9.產生和安裝 VPN 用戶端組態套件

VPN 用戶端組態檔所包含的設定，可用來將裝置設定為透過 P2S 連線來連線至 VNet。 如需產生和安裝 VPN 用戶端組態檔的指示，請參閱[建立和安裝適用於原生 Azure 憑證驗證 P2S 組態的 VPN 用戶端組態檔](point-to-site-vpn-client-configuration-azure-cert.md)。

## <a name="connect"></a>10.連接到 Azure

### <a name="to-connect-from-a-windows-vpn-client"></a>從 Windows VPN 用戶端連線

1. 若要連接至您的 VNet，在用戶端電腦上瀏覽到 VPN 連線，然後找出所建立的 VPN 連線。 其名稱會與虛擬網路相同。 按一下 [ **連接**]。 可能會出現與使用憑證有關的快顯訊息。 按一下 [繼續] 以使用較高的權限。

2. 在 [連線] 狀態頁面上，按一下 [連線] 以便開始連線。 如果出現 [選取憑證]  畫面，請確認顯示的用戶端憑證是要用來連接的憑證。 如果沒有，請使用下拉箭頭來選取正確的憑證，然後按一下 [確定] 。

  ![VPN 用戶端連線至 Azure](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/clientconnect.png)
3. 已建立您的連線。

  ![連線已建立](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/connected.png)

#### <a name="troubleshoot-windows-p2s-connections"></a>針對 Windows P2S 連線進行疑難排解

[!INCLUDE [verifies client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <a name="to-connect-from-a-mac-vpn-client"></a>從 Mac VPN 用戶端連線

從 [網路] 對話方塊，找出您要使用的用戶端設定檔，然後按一下 [連線]。

  ![Mac 連線](./media/vpn-gateway-howto-point-to-site-rm-ps/applyconnect.png)

## <a name="verify"></a>驗證您的連線

這些指示適用於 Windows 用戶端。

1. 若要驗證您的 VPN 連線為作用中狀態，請開啟提升權限的命令提示字元，並執行 *ipconfig/all*。
2. 檢視結果。 請注意，您接收到的 IP 位址是您在組態中指定的點對站 VPN 用戶端位址集區中的其中一個位址。 結果類似於此範例：

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>連線至虛擬機器

這些指示適用於 Windows 用戶端。

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <a name="add"></a>新增或移除受信任的根憑證

您可以從 Azure 新增和移除受信任的根憑證。 當您移除根憑證時，從該根憑證產生憑證的用戶端將無法進行驗證，因而無法進行連線。 若希望用戶端進行驗證和連線，您需要安裝從 Azure 信任 (已上傳至 Azure) 的根憑證產生的新用戶端憑證。

### <a name="to-add-a-trusted-root-certificate"></a>若要新增受信任的根憑證

您最多可新增 20 個受信任的根憑證 .cer 檔案至 Azure。 如需指示，請參閱這篇文章的[上傳受信任的根憑證](#uploadfile)一節。

### <a name="to-remove-a-trusted-root-certificate"></a>移除受信任的根憑證

1. 若要移除受信任的根憑證，瀏覽至虛擬網路閘道的 [點對站組態] 頁面。
2. 在頁面的 [根憑證] 區段中，找出您想要移除的憑證。
3. 按一下憑證旁邊的省略符號，然後按一下 [移除]。

## <a name="revokeclient"></a>撤銷用戶端憑證

您可以撤銷用戶端憑證。 憑證撤銷清單可讓您選擇性地拒絕以個別的用戶端憑證為基礎的點對站連線。 這與移除受信任的根憑證不同。 若您從 Azure 移除受信任的根憑證 .cer，就會撤銷所有由撤銷的根憑證所產生/簽署的用戶端憑證之存取權。 撤銷用戶端憑證，而不是根憑證，可以繼續使用從根憑證產生的憑證進行驗證。

常見的做法是使用根憑證管理小組或組織層級的存取權，然後使用撤銷的用戶端憑證針對個別使用者進行細部的存取控制。

### <a name="revoke-a-client-certificate"></a>撤銷用戶端憑證

您可以藉由將指紋新增至撤銷清單來撤銷用戶端憑證。

1. 擷取用戶端憑證指紋。 如需詳細資訊，請參閱[做法：擷取憑證的指紋](https://msdn.microsoft.com/library/ms734695.aspx)。
2. 將資訊複製到文字編輯器，並移除所有的空格，讓它是連續字串。
3. 瀏覽至虛擬網路閘道 [點對站組態] 頁面。 這個頁面與您用來[上傳受信任根憑證](#uploadfile)的頁面相同。
4. 在 [撤銷憑證] 區段中，輸入憑證的易記名稱 (它不一定是憑證 CN)。
5. 將指紋字串複製並貼上到 [指紋]欄位。
6. 指紋會進行驗證，並且自動新增至撤銷清單。 畫面上會出現一則訊息，指出清單正在更新。 
7. 更新完成之後，憑證無法再用於連線。 嘗試使用此憑證進行連線的用戶端會收到訊息，指出憑證不再有效。

## <a name="faq"></a>點對站常見問題集

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-faq-p2s-azurecert-include.md)]

## <a name="next-steps"></a>後續步驟
一旦完成您的連接，就可以將虛擬機器加入您的虛擬網路。 如需詳細資訊，請參閱[虛擬機器](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。 若要了解網路與虛擬機器的詳細資訊，請參閱 [Azure 與 Linux VM 網路概觀](../virtual-machines/linux/azure-vm-network-overview.md)。
