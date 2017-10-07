---
title: "連接電腦 tooa 虛擬網路使用點對站台和憑證驗證： Azure 入口網站 |Microsoft 文件"
description: "安全地連接 Azure 虛擬網路的電腦 tooyour 藉由建立點對站 VPN 閘道連線使用憑證驗證。 本文適用於 toohello Resource Manager 部署模型，並使用 hello Azure 入口網站。"
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
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 1419d6b4c160140b62d656b25bd02f6af7fd6655
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-azure-portal"></a>設定點對站連線 tooa VNet 使用憑證驗證： Azure 入口網站

本文章將示範如何在 hello 資源管理員部署模型中使用的點對站連接的 VNet toocreate hello Azure 入口網站。 此組態會使用用戶端連接的憑證 tooauthenticate hello。 您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Azure 入口網站 (傳統)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

點對站 (P2S) VPN 閘道，可讓您建立從個別的用戶端電腦的安全連線 tooyour 虛擬網路。 當您想要 tooconnect tooyour 從遠端位置，例如當您從家裡或會議 telecommuting VNet，點對站 VPN 連線會很有用。 您有只有少數的用戶端需要 tooconnect tooa VNet 時 P2S VPN 也很有用的方案 toouse，而不是站對站 VPN。 

使用 P2S hello 安全通訊端通道通訊協定 (SSTP)，這是 SSL 型 VPN 通訊協定。 建立之 P2S VPN 連線從 hello 用戶端電腦。

![Point-to-Site-diagram](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/point-to-site-connection-diagram.png)

點對站憑證驗證的連接需要 hello 下列：

* RouteBased VPN 閘道。
* hello 公開金鑰 （.cer 檔案） 的根憑證，也就是上傳的 tooAzure。 一旦上傳 hello 憑證時，它會被視為受信任的憑證，並用於驗證。
* 會產生從 hello 根憑證，並將連接 toohello VNet 每部用戶端電腦上安裝用戶端憑證。 此憑證使用於用戶端憑證。
* VPN 用戶端組態套件。 hello VPN 用戶端組態封裝包含 hello 的 hello 用戶端 tooconnect toohello VNet 的必要資訊。 hello 封裝設定 hello 現有 VPN 用戶端是原生 toohello Windows 作業系統。 每個連接的用戶端必須使用 hello 組態封裝設定。

點對站連線不需要 VPN 裝置或內部部署公眾對應 IP 位址。 hello VPN 連線建立透過 SSTP （安全通訊端通道通訊協定）。 在 hello 伺服器端，我們支援 SSTP 版本 1.0、 1.1 和 1.2。 hello 用戶端決定哪一個版本 toouse。 若為 Windows 8.1 和更新版本，SSTP 預設使用 1.2。

如需有關點對站連線的詳細資訊，請參閱 hello[點對站常見問題集](#faq)hello 本文結尾處。

#### <a name="example"></a>範例值

您可以使用下列值 toocreate 測試環境的 hello 或 toothese 值，請參閱 toobetter 了解這篇文章中的 hello 範例：

* **VNet 名稱︰**VNet1
* **位址空間：**192.168.0.0/16<br>在此範例中，我們只使用一個位址空間。 您可以針對 VNet 使用一個以上的位址空間。
* **子網路名稱：**FrontEnd
* **子網路位址範圍：**192.168.1.0/24
* **訂用帳戶：**如果您有多個訂用帳戶，確認您是否使用 hello 正確。
* **資源群組：**TestRG
* **位置：**美國東部
* **GatewaySubnet：**192.168.200.0/24<br>
* **DNS 伺服器：** （選擇性） hello toouse 需名稱解析的 DNS 伺服器的 IP 位址。
* **虛擬網路閘道名稱：**VNet1GW
* **閘道類型：**VPN
* **VPN 類型：**路由式
* **公用 IP 位址名稱：**VNet1GWpip
* **連線類型：**點對站
* **用戶端位址集區：**172.16.201.0/24<br>連接 toohello VNet 使用這個點對站連線的 VPN 用戶端收到 hello 用戶端位址集區的 IP 位址。

## <a name="createvnet"></a>1.建立虛擬網路

在開始之前，請確認您有 Azure 訂用帳戶。 如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial)。

[!INCLUDE [Basic Point-to-Site VNet](../../includes/vpn-gateway-basic-p2s-vnet-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>2.新增閘道子網路

連接您的虛擬網路 tooa 閘道之前，您首先需要 toocreate hello 閘道子網路要為 hello 虛擬網路 toowhich tooconnect。 hello 閘道服務會使用 hello hello 閘道子網路中指定的 IP 位址。 可能的話，請建立閘道子網路使用 CIDR 區塊/28 或 /27 tooprovide 足夠的 IP 位址 tooaccommodate 額外設定需求。

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-p2s-rm-portal-include.md)]

## <a name="dns"></a>3.指定 DNS 伺服器 (選擇性)

建立虛擬網路之後，您可以加入 hello IP 位址的 DNS 伺服器 toohandle 名稱解析。 hello DNS 伺服器是針對此設定，選擇性，但如果您想名稱解析。 指定一個值並不會建立新的 DNS 伺服器。 hello 您指定的 DNS 伺服器 IP 位址應該可以解決 hello 您所連接的 hello 資源名稱的 DNS 伺服器。 例如，我們使用私人 IP 位址，但很可能這不是您的 DNS 伺服器 hello IP 位址。 為確定 toouse 您自己的值。

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="creategw"></a>4.建立虛擬網路閘道

[!INCLUDE [create-gateway](../../includes/vpn-gateway-add-gw-p2s-rm-portal-include.md)]

## <a name="generatecert"></a>5.產生憑證

Azure tooauthenticate 連接 tooa VNet 透過點對站 VPN 連線的用戶端會使用憑證。 一旦您取得根憑證，您[上傳](#uploadfile)hello tooAzure 公開金鑰資訊。 hello 根憑證便會視為 azure 的 ' trusted'，連線透過 P2S toohello 虛擬網路。 您也會從 hello 的受信任的根憑證產生用戶端憑證，然後將它們安裝在每部用戶端電腦上。 hello 用戶端憑證時，使用的 tooauthenticate hello 用戶端會起始連線 toohello VNet。 

### <a name="getcer"></a>1.取得 hello hello 根憑證的.cer 檔案

[!INCLUDE [root-certificate](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="generateclientcert"></a>2.產生用戶端憑證 

[!INCLUDE [generate-client-cert](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="addresspool"></a>6.新增 hello 用戶端位址集區

hello 用戶端位址集區是您指定的私人 IP 位址範圍。 透過點對站 VPN 連接的 hello 用戶端會接收來自這個範圍內的 IP 位址。 搭配您從，連接的 hello 在內部部署位置或 hello 您想要 tooconnect 的 VNet 的私用的 IP 位址範圍不會重疊。

1. 一旦建立 hello 虛擬網路閘道之後，瀏覽 toohello**設定**hello 虛擬網路閘道頁面區段。 在 hello**設定**區段中，按一下**點對站組態**tooopen hello**點-到-站台-設定**頁面。

  ![點對站頁面](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/gatewayblade.png)
2. 在 hello**點-到-站台-設定** 頁面上，您可以刪除 hello 自動填滿範圍，然後新增 hello 私用 IP 位址範圍的 toouse。 按一下**儲存**toovalidate 和儲存 hello 設定。

  ![用戶端位址集區](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/ipaddresspool.png)

## <a name="uploadfile"></a>7.上傳 hello 根憑證的公開憑證資料

建立 hello 閘道之後，您上傳 hello 的公開金鑰資訊 hello 根憑證 tooAzure。 一旦上傳 hello 公用憑證資料時，Azure 可以使用它 tooauthenticate 安裝用戶端，已從 hello 信任的根憑證產生用戶端憑證。 您可以上傳其他受信任的根憑證總 tooa 總共 20。

1. 憑證會加入在 hello**點對站組態**頁面 hello**根憑證**> 一節。  
2. 請確定您匯出 hello 根憑證，為 base-64 編碼 X.509 (.cer) 檔案。 因此您可以使用文字編輯器開啟 hello 憑證，您會需要 tooexport hello 憑證，這種格式。
3. 使用文字編輯器，例如 [記事本] 開啟 hello 的憑證。 複製 hello 憑證資料時，請確認您已複製的 hello 文字做為一個連續的一行，而不換行字元或換。 您可能需要 toomodify 您 hello 文字編輯器 too'Show 符號/顯示所有字元 toosee hello 歸位字元傳回和行摘要中的檢視。 複製下列區段以連續一行只 hello:

  ![憑證資料](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/copycert.png)
4. Hello 憑證資料貼入 hello**公用憑證資料**欄位。 **名稱**hello 憑證，然後按一下**儲存**。 您可以加入 too20 受信任的根憑證。

  ![憑證上傳](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/rootcertupload.png)

## <a name="clientconfig"></a>8.產生並安裝 hello VPN 用戶端組態封裝

tooconnect tooa 使用點對站 VPN 的 VNet，每個用戶端必須安裝以 hello 設定來設定原生 VPN 用戶端 hello 用戶端組態封裝及其必要 tooconnect toohello 虛擬網路的檔案。 hello VPN 用戶端組態封裝設定 hello 原生 Windows VPN 用戶端，它不會安裝新的或不同的 VPN 用戶端。

只要 hello 版本符合 hello 用戶端 hello 架構，您可以使用相同的 VPN 用戶端組態封裝每個用戶端電腦，hello。 Hello 清單中的用戶端作業系統支援，請參閱 hello[點對站連線常見問題集](#faq)hello 本文結尾處。

### <a name="step-1---generate-and-download-hello-client-configuration-package"></a>步驟 1-產生並下載 hello 用戶端組態封裝

1. 在 hello**點對站組態**頁面上，按一下**下載 VPN 用戶端**tooopen hello**下載 VPN 用戶端**頁面。 花一分鐘或兩個 hello 封裝 toogenerate 進行。

  ![VPN 用戶端下載 1](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/downloadvpnclient1.png)
2. 選取針對您的用戶端 hello 正確的封裝，然後按一下**下載**。 儲存 hello 組態封裝檔案。 您在每個連線 toohello 虛擬網路的用戶端電腦上安裝 hello VPN 用戶端組態封裝。

  ![VPN 用戶端下載 2](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/vpnclient.png)

### <a name="step-2---install-hello-client-configuration-package"></a>步驟 2-安裝 hello 用戶端組態封裝

1. 複製 hello 設定檔在本機 toohello 電腦，您想 tooconnect tooyour 虛擬網路。 
2. 按兩下 hello.exe 檔案 tooinstall hello 套件 hello 用戶端電腦上。 建立 hello 組態套件，因為未簽署，您可能會看到警告。 如果您取得 Windows SmartScreen 快顯視窗，請按一下**進一歩**（左側 hello），然後**繼續執行**tooinstall hello 封裝。
3. Hello 用戶端電腦上安裝 hello 套件。 如果您取得 Windows SmartScreen 快顯視窗，請按一下**進一歩**（左側 hello），然後**繼續執行**tooinstall hello 封裝。
4. Hello 用戶端電腦上，瀏覽過**網路設定**按一下**VPN**。 hello VPN 連線會顯示 hello hello 連接到的虛擬網路名稱。

## <a name="installclientcert"></a>9.安裝匯出的用戶端憑證

如果您想要 toocreate P2S 連線 hello 以外的用戶端電腦從您使用 toogenerate hello 用戶端憑證，您需要 tooinstall 用戶端憑證。 安裝用戶端憑證，必須已建立 hello 用戶端憑證匯出時的 hello 密碼。 一般而言，它是只需按兩下 hello 憑證並將其安裝。

請確定 hello 用戶端憑證匯出為.pfx 以及 hello 整個憑證鏈結 （這是 hello 預設值）。 否則 hello 根憑證資訊不存在 hello 用戶端電腦上，而且 hello 用戶端將不會無法 tooauthenticate 正確。 如需詳細資訊，請參閱[安裝匯出的用戶端憑證](vpn-gateway-certificates-point-to-site.md#install)。

## <a name="connect"></a>10.連接 tooAzure

1. tooconnect tooyour VNet，hello 用戶端電腦上，瀏覽 tooVPN 連線，並尋找您所建立的 hello VPN 連線。 它會命名為與虛擬網路名稱相同的 hello。 按一下 [ **連接**]。 快顯視窗訊息可能會出現參考 toousing hello 憑證。 按一下**繼續**toouse 提升的權限。

2. 在 hello**連接**狀態] 頁面上，按一下 [**連接**toostart hello 連線。 如果您看到**選取憑證**畫面上，確認憑證顯示 hello 用戶端 hello 其中一個要 toouse tooconnect。 如果不是，使用 hello 下拉箭號 tooselect hello 正確的憑證，，然後按一下**確定**。

  ![VPN 用戶端連線 tooAzure](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/clientconnect.png)
3. 已建立您的連線。

  ![連線已建立](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>針對 P2S 連線進行疑難排解

[!INCLUDE [verifies client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>11.確認您的連接

1. tooverify VPN 連線為作用中，開啟提升權限的命令提示字元並執行*ipconfig/all*。
2. 檢視 hello 結果。 請注意，您收到 hello IP 位址的其中一個 hello 內 hello 點對站 VPN 用戶端位址集區，您在您的組態中指定的位址。 hello 結果會類似 toothis 範例：

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

## <a name="connectVM"></a>Tooa 虛擬機器連線

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <a name="add"></a>新增或移除受信任的根憑證

您可以從 Azure 新增和移除受信任的根憑證。 當您移除的根憑證時，產生從該根憑證的用戶端將不會無法 tooauthenticate，而且不會因此無法 tooconnect。 如果您想用戶端 tooauthenticate 連接時，您會需要的 tooinstall 從受信任的 （上傳） tooAzure 的根憑證產生新的用戶端憑證。

### <a name="tooadd-a-trusted-root-certificate"></a>tooadd 信任的根憑證

您可以加總 too20 受信任的根憑證.cer 檔案 tooAzure。 如需指示，請參閱 hello 節[受信任的根憑證上傳](#uploadfile)本文中。

### <a name="tooremove-a-trusted-root-certificate"></a>tooremove 信任的根憑證

1. tooremove 信任的根憑證，瀏覽 toohello**點對站組態**虛擬網路閘道的頁面。
2. 在 [hello**根憑證**區段 hello] 頁面上，找出您想要 tooremove hello 憑證。
3. 按一下 hello 省略符號 下一步 toohello 憑證，然後按一下移除。

## <a name="revokeclient"></a>撤銷用戶端憑證

您可以撤銷用戶端憑證。 hello 憑證撤銷清單可讓您 tooselectively 拒絕個別用戶端憑證為基礎的點對站連線。 這與移除受信任的根憑證不同。 如果您從 Azure 移除受信任的根憑證.cer，它就會撤銷所有用戶端憑證產生/簽署由 hello 撤銷的根憑證的 hello 存取權。 撤銷用戶端憑證，而不是 hello 根憑證，可讓 hello 產生從 hello 根憑證 toocontinue toobe 用來驗證其他憑證。

hello 常見的作法是 toouse hello 根憑證 toomanage 存取小組或組織層級時使用已撤銷用戶端憑證來進行個別使用者的更細緻的存取控制。

### <a name="toorevoke-a-client-certificate"></a>toorevoke 用戶端憑證

您可以藉由新增 hello 指紋 toohello 撤銷清單來撤銷用戶端憑證。

1. 擷取 hello 用戶端憑證指紋。 如需詳細資訊，請參閱[tooretrieve 如何 hello 憑證的指紋](https://msdn.microsoft.com/library/ms734695.aspx)。
2. 複製 hello 資訊 tooa 文字編輯器，並移除所有的空間，使其連續的字串。
3. 瀏覽 toohello 虛擬網路閘道**點-到-站台-設定**頁面。 這是 hello 您用過的相同頁面[受信任的根憑證上傳](#uploadfile)。
4. 在 hello**撤銷的憑證**區段中，輸入 hello 憑證 （不需要 toobe hello 憑證 CN） 的好記名稱。
5. 複製並貼上 hello 指紋字串 toohello**指紋**欄位。
6. hello 指紋驗證，並會自動加入 toohello 撤銷清單。 囉 」 畫面上出現訊息該 hello 正在更新清單。 
7. 更新完成後，hello 憑證不再可以使用的 tooconnect。 使用此憑證的 tooconnect 再試一次的用戶端收到訊息，指出該 hello 憑證不再有效。

## <a name="faq"></a>點對站常見問題集

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>後續步驟
一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。 如需詳細資訊，請參閱[虛擬機器](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。 toounderstand 深入了解網路和虛擬機器，請參閱[Azure 與 Linux VM 網路概觀](../virtual-machines/linux/azure-vm-network-overview.md)。
