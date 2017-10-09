---
title: "連接電腦 tooa 虛擬網路使用點對站台和憑證驗證： Azure 入口網站的傳統 |Microsoft 文件"
description: "安全地連線 tooyour 傳統 Azure 虛擬網路建立點對站 VPN 閘道連線使用 hello Azure 入口網站。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 65e14579-86cf-4d29-a6ac-547ccbd743bd
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 9b53ba43ee4dfb61defeec458905fb1f1b18c3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-classic-azure-portal"></a>設定點對站連線 tooa VNet 使用憑證驗證 （傳統）： Azure 入口網站

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

本文章將示範如何在 hello 傳統部署模型中使用的點對站連接的 VNet toocreate hello Azure 入口網站。 此組態會使用用戶端連接的憑證 tooauthenticate hello。 您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Azure 入口網站 (傳統)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>

點對站 (P2S) VPN 閘道，可讓您建立從個別的用戶端電腦的安全連線 tooyour 虛擬網路。 當您想要 tooconnect tooyour 從遠端位置，例如當您從家裡或會議 telecommuting VNet，點對站 VPN 連線會很有用。 您有只有少數的用戶端需要 tooconnect tooa VNet 時 P2S VPN 也很有用的方案 toouse，而不是站對站 VPN。 

使用 P2S hello 安全通訊端通道通訊協定 (SSTP)，這是 SSL 型 VPN 通訊協定。 建立之 P2S VPN 連線從 hello 用戶端電腦。


![Point-to-Site-diagram](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/point-to-site-connection-diagram.png)


點對站憑證驗證的連接需要 hello 下列：

* 動態 VPN 閘道。
* hello 公開金鑰 （.cer 檔案） 的根憑證，也就是上傳的 tooAzure。 這會被視為受信任的憑證並且用於驗證。
* 產生從 hello 根憑證，並會連接每個用戶端電腦上安裝用戶端憑證。 此憑證使用於用戶端憑證。
* 必須在每部連線的用戶端電腦上產生並安裝 VPN 用戶端組態套件。 hello 用戶端組態封裝設定 hello 原生 VPN 用戶端已與 hello 所需的資訊 tooconnect toohello VNet hello 作業系統上。

點對站連線不需要 VPN 裝置或內部部署公眾對應 IP 位址。 hello VPN 連線建立透過 SSTP （安全通訊端通道通訊協定）。 在 hello 伺服器端，我們支援 SSTP 版本 1.0、 1.1 和 1.2。 hello 用戶端決定哪一個版本 toouse。 若為 Windows 8.1 和更新版本，SSTP 預設使用 1.2。 

如需有關點對站連線的詳細資訊，請參閱 hello[點對站常見問題集](#faq)hello 本文結尾處。

### <a name="example-settings"></a>範例設定

您可以使用下列值 toocreate 測試環境的 hello 或 toothese 值，請參閱 toobetter 了解這篇文章中的 hello 範例：

* **名稱：VNet1**
* **位址空間：192.168.0.0/16**<br>在此範例中，我們只使用一個位址空間。 您可以針對 VNet 使用一個以上的位址空間。
* **子網路名稱：FrontEnd**
* **子網路位址範圍：192.168.1.0/24**
* **訂用帳戶：**如果您有多個訂用帳戶，確認您是否使用 hello 正確。
* **資源群組：TestRG**
* **位置：美國東部**
* **連線類型：點對站**
* **用戶端位址空間：172.16.201.0/24**。 VPN 用戶端連線使用這個點對站連接的 VNet 接收 IP 位址從 toohello hello 指定的集區。
* **GatewaySubnet: 192.168.200.0/24**。 hello 閘道子網路必須使用 hello 名稱為 'GatewaySubnet'。
* **大小：**選取 hello 閘道 SKU 的 toouse。
* **路由類型：動態**

## <a name="vnetvpn"></a>1.建立虛擬網路和 VPN 閘道

在開始之前，請確認您有 Azure 訂用帳戶。 如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial)。

### <a name="createvnet"></a>第 1 部分：建立虛擬網路

如果您還沒有虛擬網路，請建立一個。 已提供螢幕擷取畫面做為範例。 是以您自己的確定 tooreplace hello 值。 toocreate 使用 VNet hello Azure 入口網站，使用 hello 下列步驟：

1. 從瀏覽器中，瀏覽 toohello [Azure 入口網站](http://portal.azure.com)且如有需要，使用您的 Azure 帳戶登入。
2. 按一下 [新增] 。 在 hello**搜尋 hello marketplace**欄位中，輸入 虛擬網路。 找出**虛擬網路**hello 傳回從清單中，按一下 tooopen hello**虛擬網路**頁面。

  ![搜尋虛擬網路頁面](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvnetportal700.png)
3. Hello hello 虛擬網路 頁面上，從 hello 底端附近**選取部署模型**清單中，選取**傳統**，然後按一下**建立**。

  ![選取部署模型](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/selectmodel.png)
4. 在 hello**建立虛擬網路**頁面上，設定 hello VNet 設定。 在此頁面上，您會新增您的第一個位址空間和單一子網路位址範圍。 建立 hello VNet 完畢後，您可以返回並新增其他子網路和位址空間。

  ![建立虛擬網路頁面](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/vnet125.png)
5. 請確認該 hello**訂用帳戶**為 hello 正確。 您可以使用 [hello] 下拉式清單來變更訂用帳戶。
6. 按一下 [資源群組]  並選取現有的資源群組，或輸入新的資源群組名稱以建立新的資源群組。 如果您要建立新的資源群組，根據 tooyour 名稱 hello 資源群組已規劃的組態值。 如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md#resource-groups)。
7. 接下來，選取 hello**位置**設定您的 VNet。 hello 位置會決定您將部署 toothis VNet hello 資源所在的位置。
8. 選取**Pin toodashboard**如果您想 toobe 無法 toofind 輕鬆 hello 儀表板上，您的 VNet，然後按一下**建立**。

  ![Pin toodashboard](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/pintodashboard150.png)
9. 按一下 [建立]，圖格就會出現儀表板上，將會反映您的 VNet hello 進度。 hello hello 磚變更正在建立 VNet。

  ![建立虛擬網路圖格](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png)
10. 一旦建立您的虛擬網路之後，您會看到**Created**底下所列**狀態**hello Azure 傳統入口網站中 hello [網路] 頁面上。
11. 新增 DNS 伺服器 (選擇性)。 建立虛擬網路之後，您可以加入 hello 的名稱解析的 DNS 伺服器的 IP 位址。 hello 您指定的 DNS 伺服器 IP 位址應該是 hello 可解析的 VNet 中的 hello 資源 hello 名稱的 DNS 伺服器位址。<br>tooadd DNS 伺服器，開啟 hello 設定虛擬網路、 按一下 DNS 伺服器，並加入您想 toouse hello DNS 伺服器 hello IP 位址。

### <a name="gateway"></a>第 2 部分：建立閘道子網路和動態路由閘道

在此步驟中，您會建立一個閘道子網路和一個動態路由閘道。 在 hello hello 傳統部署模型的 Azure 入口網站，建立 hello 閘道子網路和 hello 閘道可以透過 hello 相同組態頁面。

1. 在 hello 入口網站中，瀏覽 toohello 想 toocreate 閘道的虛擬網路。
2. Hello 頁面上的虛擬網路，在 hello**概觀**hello VPN 連線一節中的頁面上，按一下**閘道**。

  ![按一下 toocreate 閘道](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/beforegw125.png)
3. 在 hello**新的 VPN 連線**頁面上，選取**點對站**。

  ![點對站連線類型](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvpnconnect.png)
4. 如**用戶端的位址空間**，新增 hello IP 位址範圍。 這是 hello VPN 用戶端接收的 IP 位址連接時的 hello 範圍。 搭配 hello 在內部部署位置，您將連接，或您想要 tooconnect 的 VNet hello，請使用私用的 IP 位址範圍不會重疊。 您可以刪除 hello 自動填滿範圍，然後新增 hello 私用 IP 位址範圍的 toouse。

  ![用戶端位址空間](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientaddress.png)
5. 選取 hello**立即建立閘道**核取方塊。

  ![立即建立閘道](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/creategwimm.png)
6. 按一下**選擇性閘道組態**tooopen hello**閘道組態**頁面。

  ![按一下選擇性閘道組態](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/optsubnet125.png)
7. 按一下**子網路設定必要設定**tooadd hello**閘道子網路**。 雖然可能 toocreate 閘道子網路為/29，我們建議您建立較大的子網路選取至少是/28 或 /27 包含多個位址。 這可讓足夠位址 tooaccommodate 可能其他組態，您可能想在 hello 未來。 當使用閘道子網路，避免將網路安全性 (nsg) toohello 閘道子網路產生關聯。 建立關聯的網路安全性群組 toothis 子網路，可能會導致您 VPN 閘道 toostop 如預期般運作。

  ![新增 GatewaySubnet](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsubnet125.png)
8. 選取 hello 閘道**大小**。 hello 大小為您的虛擬網路閘道的 hello 閘道 SKU。 在 hello 入口網站 hello 預設 SKU 是**基本**。 如需關於閘道 SKU 的資訊，請參閱[關於 VPN 閘道設定](vpn-gateway-about-vpn-gateway-settings.md#gwsku)。

  ![閘道大小](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsize125.png)
9. 選取 hello**路由類型**閘道。 P2S 組態需要**動態**路由類型。 完成此頁面的設定時，請按一下 [確定]。

  ![設定路由類型](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/routingtype125.png)
10. 在 hello**新的 VPN 連線**頁面上，按一下**確定**底部 hello hello 頁面 toobegin 建立虛擬網路閘道。 VPN 閘道可能佔用 too45 分鐘 toocomplete，根據您選取的 hello 閘道 sku。

## <a name="generatecerts"></a>2.建立憑證

憑證是由 Azure tooauthenticate VPN 用戶端用於點對站 Vpn。 您上傳 hello 的公開金鑰資訊 hello 根憑證 tooAzure。 hello 公開金鑰則被視為 'trusted'。 用戶端憑證必須從 hello 受信任的根憑證，所產生，並安裝 hello 憑證-目前的使用者/個人憑證存放區中每個用戶端電腦上。 hello 憑證時，使用的 tooauthenticate hello 用戶端會起始連線 toohello VNet。 

如果您使用自我簽署憑證，則必須使用特定參數來建立這些憑證。 您可以建立自我簽署的憑證，使用 hello 指示[PowerShell 和 Windows 10](vpn-gateway-certificates-point-to-site.md)，或[MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)。 請務必使用自我簽署的根憑證，並產生用戶端憑證從 hello 自我簽署的根憑證時，請遵循這些指示中的 hello 步驟。 否則，您所建立的 hello 憑證不會與 P2S 連接相容，而且您會收到連接錯誤。

### <a name="cer"></a>第 1 部分： Hello 公開金鑰 (.cer) 取得 hello 根憑證

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="genclientcert"></a>第 2 部分：產生用戶端憑證

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>3.Hello 根憑證.cer 檔案上傳

建立 hello 閘道之後，您可以上傳 hello.cer 檔案 （其中包含 hello 公開金鑰資訊） 的受信任的根憑證 tooAzure。 您不是私密金鑰 hello 根憑證 tooAzure hello 的上傳。 一旦上傳 a.cer 檔案時，Azure 可以使用它 tooauthenticate 安裝用戶端，已從 hello 信任的根憑證產生用戶端憑證。 如有需要您可以上傳其他受信任的根憑證檔-tooa 總計 20-更新版本中，設定。  

1. 在 hello **VPN 連線**> 一節的 VNet 的 hello 頁面上，按一下 hello**用戶端**圖形 tooopen hello**點對站 VPN 連線**頁面。

  ![用戶端](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. 在 hello**點對站連線**頁面上，按一下**管理憑證**tooopen hello**憑證**頁面。<br>

  ![憑證頁面](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. 在 hello**憑證**頁面上，按一下**上傳**tooopen hello**將憑證上傳**頁面。<br>

    ![上傳憑證頁面](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/uploadcerts.png)<br>
4. 按一下 hello 資料夾圖形 toobrowse hello 選擇.cer 檔案。 選取 hello 檔案，然後按一下 **確定**。 重新整理 hello 頁面 toosee hello 上傳憑證上 hello**憑證**頁面。

  ![Upload certificate](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/upload.png)<br>

## <a name="vpnclientconfig"></a>4.Hello 用戶端設定

tooconnect tooa 使用點對站 VPN 的 VNet，每個用戶端必須安裝封裝 tooconfigure hello 原生 Windows VPN 用戶端。 hello 組態封裝設定原生 Windows VPN 用戶端 hello 與 hello 設定必要 tooconnect toohello 虛擬網路。

只要 hello 版本符合 hello 用戶端 hello 架構，您可以使用相同的 VPN 用戶端組態封裝每個用戶端電腦，hello。 Hello 清單中的用戶端作業系統支援，請參閱 hello[點對站連線常見問題集](#faq)hello 本文結尾處。

### <a name="generateconfigpackage"></a>第 1 部分： 產生並安裝 hello VPN 用戶端組態封裝

1. 在 hello Azure 入口網站中 hello**概觀**頁面為您的 VNet， **VPN 連線**，按一下 hello 用戶端圖形 tooopen hello**點對站 VPN 連線**頁面。
2. 頂端的 hello hello**點對站 VPN 連線**頁面上，按一下對應 toohello 用戶端作業系統將會安裝的 hello 下載封裝：

  * 若為 64 位元用戶端，請選取 [VPN 用戶端 (64 位元)]。
  * 若為 32 位元用戶端，請選取 [VPN 用戶端 (32 位元)]。

  ![下載 VPN 用戶端組態封裝](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/dlclient.png)<br>
3. 一旦 hello 封裝產生，下載並安裝用戶端電腦上。 如果您看到 SmartScreen 快顯視窗，請按一下 [更多資訊]，然後按一下 [仍要執行]。 您也可以儲存 hello 封裝 tooinstall 其他用戶端電腦上。

### <a name="installclientcert"></a>第 2 部分： 安裝 hello 用戶端憑證

如果您想要 toocreate P2S 連線 hello 以外的用戶端電腦從您使用 toogenerate hello 用戶端憑證，您需要 tooinstall 用戶端憑證。 安裝用戶端憑證，必須已建立 hello 用戶端憑證匯出時的 hello 密碼。 一般而言，這是只需按兩下 hello 憑證並將其安裝。 如需詳細資訊，請參閱[安裝匯出的用戶端憑證](vpn-gateway-certificates-point-to-site.md#install)。

## <a name="connect"></a>5.連接 tooAzure

### <a name="connect-tooyour-vnet"></a>連接 tooyour VNet

1. tooconnect tooyour VNet，hello 用戶端電腦上，瀏覽 tooVPN 連線，並尋找您所建立的 hello VPN 連線。 它會命名為與虛擬網路名稱相同的 hello。 按一下 [ **連接**]。 快顯視窗訊息可能會出現參考 toousing hello 憑證。 如果發生這種情況，請按一下**繼續**toouse 提升的權限。
2. 在 hello**連接**狀態] 頁面上，按一下 [**連接**toostart hello 連線。 如果您看到**選取憑證**畫面上，確認憑證顯示 hello 用戶端 hello 其中一個要 toouse tooconnect。 如果不是，使用 hello 下拉箭號 tooselect hello 正確的憑證，，然後按一下**確定**。

  ![VPN 用戶端連線](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientconnect.png)
3. 已建立您的連線。

  ![建立的連線](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>針對 P2S 連線進行疑難排解

[!INCLUDE [verify-client-certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <a name="verifyvpnconnect"></a>確認 hello VPN 連線

1. tooverify VPN 連線為作用中，開啟提升權限的命令提示字元並執行*ipconfig/all*。
2. 檢視 hello 結果。 請注意，您收到 hello IP 位址的其中一個，指定您在建立 VNet 時 hello 點對站連線位址範圍內的 hello 位址。 hello 結果應該類似 toothis 範例：

  ```
    PPP adapter VNet1:
        Connection-specific DNS Suffix .:
        Description.....................: VNet1
        Physical Address................:
        DHCP Enabled....................: No
        Autoconfiguration Enabled.......: Yes
        IPv4 Address....................: 192.168.130.2(Preferred)
        Subnet Mask.....................: 255.255.255.255
        Default Gateway.................:
        NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Tooa 虛擬機器連線

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-classic-include.md)]

## <a name="add"></a>新增或移除受信任的根憑證

您可以從 Azure 新增和移除受信任的根憑證。 當您移除的根憑證時，產生從該根憑證的用戶端將不會無法 tooauthenticate，而且不會因此無法 tooconnect。 如果您想用戶端 tooauthenticate 連接時，您會需要的 tooinstall 從受信任的 （上傳） tooAzure 的根憑證產生新的用戶端憑證。

### <a name="addtrustedroot"></a>tooadd 信任的根憑證

您可以加總 too20 受信任的根憑證.cer 檔案 tooAzure。 如需指示，請參閱[區段 3-上傳 hello 根憑證.cer 檔案](#upload)。

### <a name="removetrustedroot"></a>tooremove 信任的根憑證

1. 在 hello **VPN 連線**> 一節的 VNet 的 hello 頁面上，按一下 hello**用戶端**圖形 tooopen hello**點對站 VPN 連線**頁面。

  ![用戶端](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. 在 hello**點對站連線**頁面上，按一下**管理憑證**tooopen hello**憑證**頁面。<br>

  ![憑證頁面](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. 在 hello**憑證**頁面上，按一下 hello 省略符號 下一步 toohello 憑證您想 tooremove，然後按一下**刪除**。

  ![刪除根憑證](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deleteroot.png)<br>

## <a name="revokeclient"></a>撤銷用戶端憑證

您可以撤銷用戶端憑證。 hello 憑證撤銷清單可讓您 tooselectively 拒絕個別用戶端憑證為基礎的點對站連線。 這不同於移除受信任的根憑證。 如果您從 Azure 移除受信任的根憑證.cer，它就會撤銷所有用戶端憑證產生/簽署由 hello 撤銷的根憑證的 hello 存取權。 撤銷用戶端憑證，而不是 hello 根憑證，可讓 hello 產生從 hello 根憑證 toocontinue toobe 用於 hello 點對站連線的驗證其他憑證。

hello 常見的作法是 toouse hello 根憑證 toomanage 存取小組或組織層級時使用已撤銷用戶端憑證來進行個別使用者的更細緻的存取控制。

### <a name="revokeclientcert"></a>toorevoke 用戶端憑證

您可以藉由新增 hello 指紋 toohello 撤銷清單來撤銷用戶端憑證。

1. 擷取 hello 用戶端憑證指紋。 如需詳細資訊，請參閱[How to： 擷取 hello 憑證的指紋](https://msdn.microsoft.com/library/ms734695.aspx)。
2. 複製 hello 資訊 tooa 文字編輯器，並移除所有的空間，使其連續的字串。
3. 瀏覽 toohello **'傳統虛擬網路名稱' > 點對站 VPN 連線 > 憑證**頁面，然後按一下**撤銷清單**tooopen hello 撤銷清單 頁面。 
4. 在 hello**撤銷清單**頁面上，按一下**+ 加入憑證**tooopen hello**新增憑證 toorevocation 清單**頁面。
5. 在 hello**新增憑證 toorevocation 清單**頁面中，貼上為連續一行文字，不含空格的 hello 憑證指紋。 按一下**確定**hello hello 頁底端。
6. 更新完成後，hello 憑證不再可以使用的 tooconnect。 使用此憑證的 tooconnect 再試一次的用戶端收到訊息，指出該 hello 憑證不再有效。

## <a name="faq"></a>點對站常見問題集

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>後續步驟
一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。 如需詳細資訊，請參閱[虛擬機器](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。 toounderstand 深入了解網路和虛擬機器，請參閱[Azure 與 Linux VM 網路概觀](../virtual-machines/linux/azure-vm-network-overview.md)。
