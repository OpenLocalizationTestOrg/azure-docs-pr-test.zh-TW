---
title: "連接您在內部部署網路 tooan Azure 虛擬網路： 站對站 VPN （傳統）： 入口網站 |Microsoft 文件"
description: "IPsec 連線從您內部網路 tooan Azure 虛擬網路上的步驟 toocreate hello 公用網際網路。 這些步驟將協助您建立使用 hello 入口網站的跨單位站對站 VPN 閘道連線。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/010/2017
ms.author: cherylmc
ms.openlocfilehash: b260bdf610b264458660b278bd32bf0fc5b519ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-using-hello-azure-portal-classic"></a>建立站對站連線使用 hello Azure 入口網站 （傳統）

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

本文章將示範如何 toouse 會 hello Azure 入口網站 toocreate 站對站 VPN 閘道連線從您的內部部署網路 toohello VNet。 本文章中的 hello 步驟適用於 toohello 傳統部署模型。 您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure 入口網站 (傳統)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

站對站 VPN 閘道連線是使用的 tooconnect 您內部網路 tooan Azure 虛擬網路透過 VPN IPsec/IKE （IKEv1 或 IKEv2） 通道。 這種類型的連線需要 VPN 裝置位於內部部署具有對外開放的公用 IP 位址指派 tooit。 如需 VPN 閘道的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。

![站對站 VPN 閘道跨單位連線圖表](./media/vpn-gateway-howto-site-to-site-classic-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>開始之前

請確認您已符合下列準則，開始設定之前的 hello:

* 請確認您想 toowork hello 傳統部署模型中。 如果您想 toowork hello Resource Manager 部署模型中的，請參閱[建立站對站連線 （資源管理員）](vpn-gateway-howto-site-to-site-resource-manager-portal.md)。 如果可能的話，我們建議您使用 hello Resource Manager 部署模型。
* 請確定您擁有相容的 VPN 裝置和人能夠 tooconfigure 它。 如需相容 VPN 裝置和裝置組態的詳細資訊，請參閱[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)。
* 確認您的 VPN 裝置有對外開放的公用 IPv4 位址。 此 IP 位址不能位於 NAT 後方。
* 如果您不熟悉 hello IP 位址範圍位於內部網路組態，您需要 toocoordinate 的人可以為您提供這些詳細資料。 當您建立此設定時，您必須指定 hello IP 位址範圍前置詞，則 Azure 會路由傳送 tooyour 在內部部署位置。 無 hello 的內部部署網路的子網路可以透過圈具有您想要 tooconnect hello 虛擬網路子網路。
* 目前，PowerShell 是必要的 toospecify hello 共用的金鑰，並建立 hello VPN 閘道連線。 安裝 hello hello Azure 服務管理 (SM) 的 PowerShell 指令程式最新版本。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。 使用 PowerShell 進行這項設定時，請確定您是以系統管理員身分執行。 

### <a name="values"></a>此練習的範例組態值

本文章中的 hello 範例會使用下列值的 hello。 您可以使用這些值 toocreate 測試環境中，或參閱 toothem toobetter 了解這篇文章中的 hello 範例。

* **VNet 名稱︰**TestVNet1
* **位址空間：** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (對此練習是選擇性的)
* **子網路：**
  * FrontEnd：10.11.0.0/24
  * BackEnd：10.12.0.0/24 (對此練習是選擇性的)
* **GatewaySubnet：**10.11.255.0/27
* **資源群組︰**TestRG1
* **位置：**美國東部
* **DNS 伺服器：** 10.11.0.3 (對此練習是選擇性的)
* **本機網站名稱︰** Site2
* **用戶端的位址空間：** hello 位於內部部署網站的位址空間。

## <a name="CreatVNet"></a>1.建立虛擬網路

當您建立虛擬網路 toouse S2S 連線時，您必須確定您指定的 hello 位址空間沒有與任何 hello 您想要 tooconnect hello 本機站台的用戶端位址空間重疊 toomake。 如果有重疊的子網路，您的連線便無法正常運作。

* 如果您沒有 VNet，請確認 hello 設定與您的 VPN 閘道設計相容。 請特別注意 tooany 的子網路，可能會與其他網路重疊。 

* 如果您還沒有虛擬網路，請建立一個。 已提供螢幕擷取畫面做為範例。 是以您自己的確定 tooreplace hello 值。

### <a name="toocreate-a-virtual-network"></a>toocreate 虛擬網路

1. 從瀏覽器中，瀏覽 toohello [Azure 入口網站](http://portal.azure.com)且如有需要，使用您的 Azure 帳戶登入。
2. 按一下頁面底部的 [新增] **+**來單一登入應用程式。 在 hello**搜尋 hello marketplace**欄位中，輸入 虛擬網路。 找出**虛擬網路**hello 傳回從清單中，按一下 tooopen hello**虛擬網路**頁面。

  ![搜尋虛擬網路頁面](./media/vpn-gateway-howto-site-to-site-classic-portal/newvnetportal700.png)
3. Hello hello 虛擬網路 頁面上，從 hello 底端附近**選取部署模型**下拉式清單中，選取**傳統**，然後按一下**建立**。

  ![選取部署模型](./media/vpn-gateway-howto-site-to-site-classic-portal/selectmodel.png)
4. 在 hello**建立虛擬 network(classic)**頁面上，設定 hello VNet 設定。 在此頁面上，您會新增您的第一個位址空間和單一子網路位址範圍。 建立 hello VNet 完畢後，您可以返回並新增其他子網路和位址空間。

  ![建立虛擬網路頁面](./media/vpn-gateway-howto-site-to-site-classic-portal/createvnet.png "建立虛擬網路頁面")
5. 請確認該 hello**訂用帳戶**為 hello 正確。 您可以使用 [hello] 下拉式清單來變更訂用帳戶。
6. 按一下 [資源群組] 並選取現有的資源群組，或輸入名稱以建立新的資源群組。 如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md#resource-groups)。
7. 接下來，選取 hello**位置**設定您的 VNet。 hello 位置會決定您將部署 toothis VNet hello 資源所在的位置。
8. 如果您想 toobe 無法 toofind VNet 輕鬆 hello 儀表板上的，選取**Pin toodashboard**。 按一下**建立**toocreate VNet。

  ![Pin toodashboard](./media/vpn-gateway-howto-site-to-site-classic-portal/pintodashboard150.png "Pin toodashboard")
9. 按一下 [建立] 之後, 磚會出現在 hello 儀表板，以反映您的 VNet hello 進度。 hello hello 磚變更正在建立 VNet。

  ![建立虛擬網路圖格](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png "建立虛擬網路")

您的虛擬網路建立之後，您會看到**Created**底下所列**狀態**hello Azure 傳統入口網站中 hello [網路] 頁面上。

## <a name="additionaladdress"></a>2.新增其他位址空間

建立虛擬網路之後，您可以新增其他位址空間。 加入其他位址空間不是使用 S2S 設定，設定的必要的部分，但如果您需要多個位址空間，請使用下列步驟的 hello:

1. Hello 入口網站中，找出 hello 虛擬網路。
2. Hello 頁面上的虛擬網路，在 hello**設定**區段中，按一下**位址空間**。
3. 在 hello 位址空間 頁面上，按一下  **+ 加**輸入其他位址空間。

## <a name="dns"></a>3.指定 DNS 伺服器

DNS 設定不是 S2S 組態的必要部分，但如果您想要名稱解析，則需要 DNS。 指定一個值並不會建立新的 DNS 伺服器。 hello 您指定的 DNS 伺服器 IP 位址應該可以解決 hello 您所連接的 hello 資源名稱的 DNS 伺服器。 Hello 範例設定，我們使用私人 IP 位址。 hello，我們使用的 IP 位址可能不是您的 DNS 伺服器 hello IP 位址。 為確定 toouse 您自己的值。

建立虛擬網路之後，您可以加入 hello IP 位址的 DNS 伺服器 toohandle 名稱解析。 開啟您的虛擬網路的 hello 設定、 按一下 DNS 伺服器，並加入 hello hello toouse 需名稱解析的 DNS 伺服器的 IP 位址。

1. Hello 入口網站中，找出 hello 虛擬網路。
2. Hello 頁面上的虛擬網路，在 hello**設定**區段中，按一下**DNS 伺服器**。
3. 新增 DNS 伺服器。
4. 您的設定，按一下 toosave**儲存**hello 頁面頂端的 hello。

## <a name="localsite"></a>4.Hello 本機站台設定

hello 本機站台通常是指 tooyour 在內部部署位置。 它包含您將建立連線，以及 hello 而必須路由傳送透過 hello VPN 閘道 toohello VPN 裝置 IP 位址範圍的 hello VPN 裝置 toowhich hello IP 位址。

1. 在 hello 入口網站中，瀏覽 toohello 想 toocreate 閘道的虛擬網路。
2. Hello 頁面上的虛擬網路，在 hello**概觀**hello VPN 連線一節中的頁面上，按一下**閘道**tooopen hello**新的 VPN 連線**頁面。

  ![按一下 tooconfigure 閘道設定](./media/vpn-gateway-howto-site-to-site-classic-portal/beforegw125.png "按一下 tooconfigure 閘道設定")
3. 在 hello**新的 VPN 連線**頁面上，選取**站對站**。
4. 按一下**本機站台-必要的設定**tooopen hello**本機站台**頁面。 設定 hello 設定，然後按一下**確定**toosave hello 設定。
  - **名稱：**建立本機站台 toomake 名稱讓您 tooidentify 輕易。
  - **VPN 閘道 IP 位址：**這是在內部部署網路的 hello VPN 裝置的 hello 公用 IP 位址。 hello VPN 裝置需要 IPv4 公用 IP 位址。 指定您想要 tooconnect VPN 裝置 toowhich hello 的有效公用 IP 位址。 它不得位於 NAT 後方且 toobe 連線到 azure。 如果您不知道 hello 的 VPN 裝置 IP 位址，您可以一律放在預留位置的值 （只要其為有效的公用 IP 位址的 hello 格式），然後稍後變更。
  - **用戶端的位址空間：**清單 hello IP 位址範圍要路由傳送到此閘道 toohello 本機內部網路。 您可以加入多個位址空間範圍。 請確定您的虛擬網路連接的其他網路的範圍或 hello 位址範圍的 hello 虛擬網路本身與 hello 您在此處指定的範圍不會重疊。

  ![本機站台](./media/vpn-gateway-howto-site-to-site-classic-portal/localnetworksite.png "設定本機站台")

## <a name="gatewaysubnet"></a>5.設定 hello 閘道子網路

您必須為 VPN 閘道建立閘道子網路。 hello 閘道子網路包含 hello hello VPN 閘道服務使用的 IP 位址。

1. 在 hello**新的 VPN 連線**頁面上，選取 hello 核取方塊**立即建立閘道**。 hello '選擇性閘道設定 頁面隨即出現。 如果您沒有選取 hello 核取方塊，就看 hello 頁面 tooconfigure hello 閘道子網路。

  ![閘道組態 - 子網路、大小、路由類型](./media/vpn-gateway-howto-site-to-site-classic-portal/optional.png "閘道組態 - 子網路、大小、路由類型")
2. tooopen hello**閘道組態**頁面上，按一下**選擇性閘道組態-子網路、 大小和路由類型**。
3. 在 hello**閘道組態**頁面上，按一下**子網路-設定必要的設定**tooopen hello**加入子網路**頁面。

  ![閘道組態 - 閘道子網路](./media/vpn-gateway-howto-site-to-site-classic-portal/subnetrequired.png "閘道組態 - 閘道子網路")
4. 在 hello**加入子網路**頁面上，新增 hello 閘道子網路。 您指定的 hello 閘道子網路的 hello 大小取決於 hello VPN 閘道設定您想 toocreate。 雖然可能 toocreate 閘道子網路為/29，我們建議您使用 /27 或/28。 這可建立包含更多位址的較大子網路。 使用較大的閘道子網路允許足夠的 IP 位址 tooaccommodate 可能未來設定。

  ![新增閘道子網路](./media/vpn-gateway-howto-site-to-site-classic-portal/addgwsubnet.png "新增閘道子網路")

## <a name="sku"></a>6.指定 hello SKU 和 VPN 類型

1. 選取 hello 閘道**大小**。 這是您使用 toocreate 虛擬網路閘道 SKU 的 hello 閘道。 在 hello 入口網站 hello 預設 SKU =**基本**。 傳統 VPN 閘道使用 hello 舊 （舊版） 的閘道 Sku。 如需 hello 舊版的閘道 Sku 的詳細資訊，請參閱[使用虛擬網路閘道 Sku (舊 Sku)](vpn-gateway-about-skus-legacy.md)。

  ![選取 SKUL 和 VPN 類型](./media/vpn-gateway-howto-site-to-site-classic-portal/sku.png "選取 SKU 和 VPN 類型")
2. 選取 hello**路由類型**閘道。 這也稱為是 hello VPN 類型。 這是重要的 tooselect hello 正確的閘道類型，因為您無法從一個類型 tooanother 轉換 hello 閘道。 您的 VPN 裝置必須相容於您所選取的 hello 路由類型。 如需 VPN 類型的詳細資訊，請參閱[關於 VPN 閘道設定](vpn-gateway-about-vpn-gateway-settings.md#vpntype)。 您可能會看到文件參考 too'RouteBased' 和 'PolicyBased' VPN 類型。 ' 動態 '對應 too'RouteBased'，而 'Static' 會對應至 'PolicyBased'。
3. 按一下**確定**toosave hello 設定。
4. 在 hello**新的 VPN 連線**頁面上，按一下**確定**底部 hello hello 頁面 toobegin 建立虛擬網路閘道。 根據您選取的 SKU hello，就可以在 too45 分鐘 toocreate 虛擬網路閘道。

## <a name="vpndevice"></a>7.設定 VPN 裝置

站台對站連線 tooan 在內部部署網路需要 VPN 裝置。 在此步驟中，設定 VPN 裝置。 當設定 VPN 裝置，您會需要 hello 下列：

- 共用金鑰。 這是共用相同 hello 建立您的站對站 VPN 連線時所指定的索引鍵。 在我們的範例中，我們會使用基本的共用金鑰。 我們建議您產生更複雜金鑰 toouse。
- hello 的虛擬網路閘道的公用 IP 位址。 您可以使用 hello Azure 入口網站、 PowerShell 或 CLI 檢視 hello 公用 IP 位址。

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>8.建立 hello 連線
在此步驟中，您可以設定 hello 共用的金鑰，並建立 hello 連線。 您所設定的 hello 機碼必須是 hello VPN 裝置組態中所使用的相同索引鍵。

> [!NOTE]
> 目前，這個步驟不適用於 hello Azure 入口網站。 您必須使用 hello 服務管理 (SM) 版的 hello Azure PowerShell cmdlet。
>

### <a name="step-1-connect-tooyour-azure-account"></a>步驟 1. 連接 tooyour Azure 帳戶

1. 使用提高的權限開啟 PowerShell 主控台和 tooyour 帳戶連接。 使用下列範例 toohelp 您連接的 hello:

  ```powershell
  Add-AzureAccount
  ```
2. 請檢查 hello hello 帳戶的訂用帳戶。

  ```powershell
  Get-AzureSubscription
  ```
3. 如果您有多個訂閱，選取您想 toouse hello 訂用帳戶。

  ```powershell
  Select-AzureSubscription -SubscriptionId "Replace_with_your_subscription_ID"
  ```

### <a name="step-2-set-hello-shared-key-and-create-hello-connection"></a>步驟 2. 設定 hello 共用的金鑰，並建立 hello 連線

當使用 PowerShell 和 hello 傳統部署模型，有時 hello hello 入口網站中的資源的名稱時使用 PowerShell toosee 所預期的 hello 名稱 hello Azure。 hello 下列步驟協助您匯出 hello 網路組態檔 tooobtain hello 確切值 hello 名稱。

1. 您的電腦上建立目錄，然後匯出 hello 網路組態檔 toohello 目錄。 在此範例中，hello 網路組態檔會是匯出的 tooC:\AzureNet。

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. 使用 xml 編輯器開啟 hello 網路組態檔，並檢查 hello 'LocalNetworkSite name' 和 'VirtualNetworkSite name' 的值。 修改 hello 範例 tooreflect hello 您需要的值。 在指定的名稱包含空格，使用單一引號括住 hello 值。

3. 設定 hello 共用的金鑰，並建立 hello 連線。 hello '-SharedKey' 是產生及指定的值。 在 hello 範例中，我們已使用 'abc123'，但您可以產生 （且應該） 使用更複雜的項目。 hello 重要件事就是您在此處指定的 hello 該值必須是相同的值，指定設定 VPN 裝置時的 hello。

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group TestRG1 TestVNet1' `
  -LocalNetworkSiteName 'D1BFC9CB_Site2' -SharedKey abc123
  ```
建立 hello 連接時，hello 結果是：**狀態： 成功**。

## <a name="verify"></a>9.確認您的連接

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

如果您有連線問題，請參閱 hello**疑難排解**hello 目錄 hello 左窗格中的區段。

## <a name="reset"></a>如何 tooreset VPN 閘道

如果您遺失一或多個站對站 VPN 通道上的跨單位 VPN 連線，重設 Azure VPN 閘道會很有幫助。 在此情況下，您在內部部署 VPN 裝置是所有運作正常，但您不能 tooestablish 與 hello Azure VPN 閘道 IPsec 通道。 如需相關步驟，請參閱[重設 VPN 閘道](vpn-gateway-resetgw-classic.md)。

## <a name="changesku"></a>如何 toochange 閘道 SKU

Hello 步驟 toochange 閘道 SKU，請參閱[調整大小的閘道 SKU](vpn-gateway-about-SKUS-legacy.md)。

## <a name="next-steps"></a>後續步驟

* 一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。 如需詳細資訊，請參閱[虛擬機器](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。
* 如需強制通道的相關資訊，請參閱[關於強制通道](vpn-gateway-about-forced-tunneling.md)。