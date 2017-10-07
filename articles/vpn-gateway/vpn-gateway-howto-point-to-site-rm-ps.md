---
title: "連接電腦 tooan 使用點對站 Azure 虛擬網路和憑證驗證： PowerShell |Microsoft 文件"
description: "安全地連接電腦 tooyour 虛擬網路建立點對站 VPN 閘道連線使用憑證驗證。 本文適用於 toohello Resource Manager 部署模型，並使用 PowerShell。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a>設定點對站連線 tooa VNet 使用憑證驗證： PowerShell

本文章將示範如何 toocreate hello 資源管理員部署中的點對站連接的 VNet 模型使用 PowerShell。 此組態會使用用戶端連接的憑證 tooauthenticate hello。 您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Azure 入口網站 (傳統)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

點對站 (P2S) VPN 閘道，可讓您建立從個別的用戶端電腦的安全連線 tooyour 虛擬網路。 當您想要 tooconnect tooyour 從遠端位置，例如當您從家裡或會議 telecommuting VNet，點對站 VPN 連線會很有用。 您有只有少數的用戶端需要 tooconnect tooa VNet 時 P2S VPN 也很有用的方案 toouse，而不是站對站 VPN。

使用 P2S hello 安全通訊端通道通訊協定 (SSTP)，這是 SSL 型 VPN 通訊協定。 建立之 P2S VPN 連線從 hello 用戶端電腦。

![連接電腦 tooan Azure VNet 的點對站連接圖表](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

點對站憑證驗證的連接需要 hello 下列：

* RouteBased VPN 閘道。
* hello 公開金鑰 （.cer 檔案） 的根憑證，也就是上傳的 tooAzure。 一旦上傳 hello 憑證時，它會被視為受信任的憑證，並用於驗證。
* 會產生從 hello 根憑證，並將連接 toohello VNet 每部用戶端電腦上安裝用戶端憑證。 此憑證使用於用戶端憑證。
* VPN 用戶端組態套件。 hello VPN 用戶端組態封裝包含 hello 的 hello 用戶端 tooconnect toohello VNet 的必要資訊。 hello 封裝設定 hello 現有 VPN 用戶端是原生 toohello Windows 作業系統。 每個連接的用戶端必須使用 hello 組態封裝設定。

點對站連線不需要 VPN 裝置或內部部署公眾對應 IP 位址。 hello VPN 連線建立透過 SSTP （安全通訊端通道通訊協定）。 在 hello 伺服器端，我們支援 SSTP 版本 1.0、 1.1 和 1.2。 hello 用戶端決定哪一個版本 toouse。 若為 Windows 8.1 和更新版本，SSTP 預設使用 1.2。 

如需有關點對站連線的詳細資訊，請參閱 hello[點對站常見問題集](#faq)hello 本文結尾處。

## <a name="before-beginning"></a>開始之前

* 請確認您有 Azure 訂用帳戶。 如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial)。
* 安裝 hello hello Azure 資源管理員的 PowerShell 指令程式最新版本。 如需安裝 PowerShell cmdlet 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

### <a name="example"></a>範例值

您可以使用 hello 範例值 toocreate 測試環境中，或參閱 toothese 值 toobetter 了解這篇文章中的 hello 範例。 我們設定一節中的 hello 變數[1](#declare) hello 發行項。 您可以使用 hello 步驟逐步解說，以和使用 hello 值而不需要變更，或變更這些 tooreflect 您的環境。 

* **名稱：VNet1**
* **位址空間：192.168.0.0/16** 和 **10.254.0.0/16**<br>此範例中，我們使用一個以上的位址空間 tooillustrate 這項設定適用於多個位址空間。 不過，此組態不需要多個位址空間。
* **子網路名稱：FrontEnd**
  * **子網路位址範圍：192.168.1.0/24**
* **子網路名稱：BackEnd**
  * **子網路位址範圍：10.254.1.0/24**
* **子網路名稱：GatewaySubnet**<br>hello 子網路名稱*GatewaySubnet*對於 hello VPN 閘道 toowork 是必要的。
  * **閘道子網路位址範圍：192.168.200.0/24** 
* **VPN 用戶端位址集區：172.16.201.0/24**<br>連接 toohello VNet 使用這個點對站連線的 VPN 用戶端收到 hello VPN 用戶端位址集區的 IP 位址。
* **訂用帳戶：**如果您有多個訂用帳戶，確認您是否使用 hello 正確。
* **資源群組：TestRG**
* **位置：美國東部**
* **DNS 伺服器： IP 位址**hello toouse 需名稱解析的 DNS 伺服器。
* **GW 名稱：Vnet1GW**
* **公用 IP 名稱：VNet1GWPIP**
* **VpnType：RouteBased** 

## <a name="declare"></a>1.登入和設定變數

在本節中，您可以登入，並宣告 hello 值用於此設定。 hello 宣告 hello 範例指令碼中使用值。 變更 hello 值 tooreflect 您自己的環境。 或者，您可以使用 hello 宣告值，並瀏覽 hello 步驟中，當做練習。

1. 使用提高的權限開啟 PowerShell 主控台，並登入 tooyour Azure 帳戶。 此 cmdlet 會提示您輸入 hello 登入認證。 登入之後，它會下載您的帳戶設定，使其可用 tooAzure PowerShell。

  ```powershell
  Login-AzureRmAccount
  ```
2. 取得您的 Azure 訂用帳戶清單。

  ```powershell
  Get-AzureRmSubscription
  ```
3. 指定您想 toouse hello 訂用帳戶。

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. 宣告您想 toouse hello 變數。 下列範例中，替代 hello 值供自己在必要時，就會使用 hello。

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <a name="ConfigureVNet"></a>2.設定 VNet

1. 建立資源群組。

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. 建立 hello hello 虛擬網路，請加以命名的子網路組態*前端*，*後端*，和*GatewaySubnet*。 這些前置詞必須是 hello 您宣告的 VNet 位址空間的一部分。

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. 建立 hello 虛擬網路。

  在此範例中，hello DNS 伺服器是選擇性的。 指定一個值並不會建立新的 DNS 伺服器。 hello 您指定的 DNS 伺服器 IP 位址應該可以解決 hello 您所連接的 hello 資源名稱的 DNS 伺服器。 例如，我們使用私人 IP 位址，但很可能這不是您的 DNS 伺服器 hello IP 位址。 為確定 toouse 您自己的值。

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. 指定您所建立的 hello 虛擬網路的 hello 變數。

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. VPN 閘道必須具有公用 IP 位址。 您第一次要求 hello IP 位址資源，並建立您的虛擬網路閘道時參考 tooit。 hello IP 位址建立 hello VPN 閘道時，會動態指定 toohello 資源。 VPN 閘道目前僅支援*動態*公用 IP 位址配置。 您無法要求靜態公用 IP 位址指派。 不過，它並不表示 hello IP 位址變更之後已被指派 tooyour VPN 閘道。 hello 公用 IP 位址變更為當 hello 閘道 hello 才會刪除並重新建立。 它不會因為重新調整、重設或 VPN 閘道的其他內部維護/升級而變更。

  要求動態指派的公用 IP 位址。

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <a name="creategateway"></a>3.建立 hello VPN 閘道

設定並建立 hello 虛擬網路閘道的 VNet。

* hello *-gatewaytype 的授權*必須**Vpn**和 hello *-VpnType*必須**RouteBased**。
* VPN 閘道可能會佔用 too45 分鐘 toocomplete 根據 hello[閘道 sku](vpn-gateway-about-vpn-gateway-settings.md)您選取。

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <a name="addresspool"></a>4.新增 hello VPN 用戶端位址集區

Hello VPN 閘道完成建立之後，您可以加入 hello VPN 用戶端位址集區。 hello VPN 用戶端位址集區是 hello VPN 用戶端接收的 IP 位址連接時的 hello 範圍。 搭配您從，連接的 hello 在內部部署位置或 hello 您想要 tooconnect 的 VNet，請使用私用的 IP 位址範圍不會重疊。 在此範例中，宣告 hello VPN 用戶端位址集區為[變數](#declare)在步驟 1 中。

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <a name="Certificates"></a>5.產生憑證

憑證是由 Azure tooauthenticate VPN 用戶端用於點對站 Vpn。 您上傳 hello 的公開金鑰資訊 hello 根憑證 tooAzure。 hello 公開金鑰則被視為 'trusted'。 用戶端憑證必須從 hello 受信任的根憑證，所產生，並安裝 hello 憑證-目前的使用者/個人憑證存放區中每個用戶端電腦上。 hello 憑證時，使用的 tooauthenticate hello 用戶端會起始連線 toohello VNet。 

如果您使用自我簽署憑證，則必須使用特定參數來建立這些憑證。 您可以建立自我簽署的憑證，使用 hello 指示[PowerShell 和 Windows 10](vpn-gateway-certificates-point-to-site.md)，或者，如果您沒有 Windows 10，您可以使用[MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)。 請務必產生自我簽署的根憑證和用戶端憑證時，請遵循 hello hello 指示中的步驟。 否則，您所產生的 hello 憑證不會 P2S 連線與相容，而且您會收到連接錯誤。

### <a name="cer"></a>1.取得 hello hello 根憑證的.cer 檔案

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <a name="generate"></a>2.產生用戶端憑證 

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>6.上傳 hello 根憑證的公開金鑰資訊

確認 VPN 閘道已完成建立。 完成後，您可以上傳 hello.cer 檔案 （其中包含 hello 公開金鑰資訊） 的受信任的根憑證 tooAzure。 一旦上傳 a.cer 檔案時，Azure 可以使用它 tooauthenticate 安裝用戶端，已從 hello 信任的根憑證產生用戶端憑證。 如有需要您可以上傳其他受信任的根憑證檔-tooa 總計 20-更新版本中，設定。

1. 您的憑證名稱，取代 hello 值以您自己的 hello 變數宣告。

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. 取代您自己，hello 檔案路徑，然後執行 hello cmdlet。

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. 上傳 hello 公開金鑰資訊 tooAzure。 一旦上傳 hello 憑證資訊時，Azure 會將此 toobe 視為信任的根憑證。

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <a name="clientconfig"></a>7.下載 hello VPN 用戶端組態封裝

tooconnect tooa 使用點對站 VPN 的 VNet，每個用戶端必須安裝以 hello 設定來設定原生 VPN 用戶端 hello 用戶端組態封裝及其必要 tooconnect toohello 虛擬網路的檔案。 hello VPN 用戶端組態封裝設定 hello 原生 Windows VPN 用戶端，它不會安裝新的或不同的 VPN 用戶端。 

只要 hello 版本符合 hello 用戶端 hello 架構，您可以使用相同的 VPN 用戶端組態封裝每個用戶端電腦，hello。 Hello 清單中的用戶端作業系統支援，請參閱 hello[點對站連線常見問題集](#faq)hello 本文結尾處。

1. 建立 hello 閘道之後，您可以產生並下載 hello 用戶端組態封裝。 這個範例會將 hello 套件下載 64 位元用戶端。 如果您想 toodownload hello 32 位元用戶端，請將 'Amd64' 取代 'x86'。 您也可以使用 hello Azure 入口網站下載 hello VPN 用戶端。

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. 複製並貼上傳回 tooa web 瀏覽器 toodownload hello 套件，小心 tooremove hello 引號括住 hello 連結 hello 連結。 
3. 下載並安裝 hello 套件 hello 用戶端電腦上。 如果您看到 SmartScreen 快顯視窗，請按一下 [更多資訊]，然後按一下 [仍要執行]。 您也可以儲存 hello 封裝 tooinstall 其他用戶端電腦上。
4. Hello 用戶端電腦上，瀏覽過**網路設定**按一下**VPN**。 hello VPN 連線會顯示 hello hello 連接到的虛擬網路名稱。

## <a name="clientcertificate"></a>8.安裝匯出的用戶端憑證

如果您想要 toocreate P2S 連線 hello 以外的用戶端電腦從您使用 toogenerate hello 用戶端憑證，您需要 tooinstall 用戶端憑證。 安裝用戶端憑證，必須已建立 hello 用戶端憑證匯出時的 hello 密碼。 一般而言，它是只需按兩下 hello 憑證並將其安裝。

請確定 hello 用戶端憑證匯出為.pfx 以及 hello 整個憑證鏈結 （這是 hello 預設值）。 否則 hello 根憑證資訊不存在 hello 用戶端電腦上，而且 hello 用戶端將不會無法 tooauthenticate 正確。 如需詳細資訊，請參閱[安裝匯出的用戶端憑證](vpn-gateway-certificates-point-to-site.md#install)。 

## <a name="connect"></a>9.連接 tooAzure

1. tooconnect tooyour VNet，hello 用戶端電腦上，瀏覽 tooVPN 連線，並尋找您所建立的 hello VPN 連線。 它會命名為與虛擬網路名稱相同的 hello。 按一下 [ **連接**]。 快顯視窗訊息可能會出現參考 toousing hello 憑證。 按一下**繼續**toouse 提升的權限。 
2. 在 hello**連接**狀態] 頁面上，按一下 [**連接**toostart hello 連線。 如果您看到**選取憑證**畫面上，確認憑證顯示 hello 用戶端 hello 其中一個要 toouse tooconnect。 如果不是，使用 hello 下拉箭號 tooselect hello 正確的憑證，，然後按一下**確定**。

  ![VPN 用戶端連線 tooAzure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. 已建立您的連線。

  ![連線已建立](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>針對 P2S 連線進行疑難排解

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>10.確認您的連接

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

## <a name="addremovecert"></a>新增或移除根憑證

您可以從 Azure 新增和移除受信任的根憑證。 當您移除的根憑證時，產生從 hello 根憑證的憑證的用戶端會無法進行驗證，且將無法能 tooconnect。 如果您想用戶端 tooauthenticate 連接時，您會需要的 tooinstall 從受信任的 （上傳） tooAzure 的根憑證產生新的用戶端憑證。

### <a name="addtrustedroot"></a>tooadd 信任的根憑證

您可以加總 too20 根憑證.cer 檔案 tooAzure。 hello 下列步驟可幫助您加入根憑證：

#### <a name="certmethod1"></a>方法 1

這是最有效方法 tooupload hello 的根憑證。

1. 準備 hello.cer 檔案 tooupload:

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. Hello 檔案上傳。 您一次只能上傳一個檔案。

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. hello 憑證檔案上傳的 tooverify:

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <a name="certmethod2"></a>方法 2

這個方法會比方法 1 的詳細步驟，但有 hello 相同的結果。 它是為了，以防您需要 tooview hello 憑證資料。

1. 建立並準備 hello 新的根憑證 tooadd tooAzure。 Hello 公開金鑰匯出成 base-64 編碼 X.509 (。CER) 和以文字編輯器中開啟它。 請複製 hello 值 hello 下列範例所示：

  ![憑證](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > 複製 hello 憑證資料時，請確認您已複製的 hello 文字做為一個連續的一行，而不換行字元或換。 您可能需要 toomodify 您 hello 文字編輯器 too'Show 符號/顯示所有字元 toosee hello 歸位字元傳回和行摘要中的檢視。
  >
  >

2. 為變數指定 hello 憑證名稱和金鑰資訊。 取代您自己 hello 所示的下列範例中的 hello 資訊：

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. 新增 hello 新的根憑證。 您一次只能新增一個憑證。

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. 您可以確認使用下列範例中的 hello 已正確新增該 hello 新憑證：

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <a name="removerootcert"></a>tooremove 根憑證

1. Hello 變數宣告。

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. 移除 hello 憑證。

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. 已成功移除下列 hello 憑證的範例 tooverify 使用 hello。

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <a name="revoke"></a>撤銷用戶端憑證

您可以撤銷用戶端憑證。 hello 憑證撤銷清單可讓您 tooselectively 拒絕個別用戶端憑證為基礎的點對站連線。 這與移除受信任的根憑證不同。 如果您從 Azure 移除受信任的根憑證.cer，它就會撤銷所有用戶端憑證產生/簽署由 hello 撤銷的根憑證的 hello 存取權。 撤銷用戶端憑證，而不是 hello 根憑證，可讓 hello 產生從 hello 根憑證 toocontinue toobe 用來驗證其他憑證。

hello 常見的作法是 toouse hello 根憑證 toomanage 存取小組或組織層級時使用已撤銷用戶端憑證來進行個別使用者的更細緻的存取控制。

### <a name="revokeclientcert"></a>toorevoke 用戶端憑證

1. 擷取 hello 用戶端憑證指紋。 如需詳細資訊，請參閱[tooretrieve 如何 hello 憑證的指紋](https://msdn.microsoft.com/library/ms734695.aspx)。
2. 複製 hello 資訊 tooa 文字編輯器，並移除所有的空間，使其連續的字串。 這個字串 hello 下一個步驟中宣告的變數。
3. Hello 變數宣告。 Hello 上一個步驟中，請確定您所擷取的 toodeclare hello 憑證指紋。

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. 新增 hello 撤銷憑證的指紋 toohello 清單。 已加入 hello 指紋時，您會看到 「 成功 」。

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. 請確認該 hello 指紋已加入 toohello 憑證撤銷清單。

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. 加入 hello 指紋之後，hello 憑證不再可以使用的 tooconnect。 使用此憑證的 tooconnect 再試一次的用戶端收到訊息，指出該 hello 憑證不再有效。

### <a name="reinstateclientcert"></a>tooreinstate 用戶端憑證

您可以從已撤銷用戶端憑證的 hello 清單移除 hello 指紋恢復用戶端憑證。

1. Hello 變數宣告。 請確定您宣告 hello 正確的 tooreinstate hello 憑證指紋。

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. 移除 hello 憑證撤銷清單中的 hello 憑證指紋。

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. 如果從 hello 移除 hello 指紋的核取撤銷清單。

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <a name="faq"></a>點對站常見問題集

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>後續步驟
一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。 如需詳細資訊，請參閱[虛擬機器](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。 toounderstand 深入了解網路和虛擬機器，請參閱[Azure 與 Linux VM 網路概觀](../virtual-machines/linux/azure-vm-network-overview.md)。
