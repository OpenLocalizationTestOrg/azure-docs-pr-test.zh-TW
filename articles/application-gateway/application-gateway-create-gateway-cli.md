---
title: "aaaCreate Azure 應用程式閘道-Azure CLI 2.0 |Microsoft 文件"
description: "了解如何使用應用程式閘道 toocreate hello Azure CLI 2.0 在資源管理員"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a>使用 Azure CLI 2.0 hello 建立應用程式閘道

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure 傳統 PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager 範本](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI 1.0](application-gateway-create-gateway-cli.md)
> * [Azure CLI 2.0](application-gateway-create-gateway-cli.md)

「應用程式閘道」是專用的虛擬設備，會以服務形式提供應用程式傳遞控制器 (ADC)，為您的應用程式提供各種第 7 層負載平衡功能。

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作

您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

* [Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) -我們 CLI hello 傳統和資源管理部署模型。
* [Azure CLI 2.0](application-gateway-create-gateway-cli.md) -hello 資源管理部署模型我們下一個層代 CLI

## <a name="prerequisite-install-hello-azure-cli-20"></a>必要條件： 安裝 hello Azure CLI 2.0

tooperform hello 步驟在本文中，您需要[hello Azure 命令列介面安裝的 Mac、 Linux 及 Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。

> [!NOTE]
> 如果您沒有 Azure 帳戶，就需要申請一個。 請 [在此處註冊免費試用](../active-directory/sign-up-organization.md)。

## <a name="scenario"></a>案例

在此案例中，您學會如何應用程式閘道使用 toocreate hello Azure 入口網站。

此案例將會：

* 建立含有兩個執行個體的中型應用程式閘道。
* 建立名為 AdatumAppGatewayVNET 且含有 10.0.0.0/16 保留 CIDR 區塊的虛擬網路。
* 建立名為 Appgatewaysubnet 且使用 10.0.0.0/28 做為其 CIDR 區塊的子網路。

> [!NOTE]
> 額外設定 hello 應用程式閘道，包括自訂健全狀況探查，hello 應用程式閘道設定之後，而不會在初始部署設定後端集區位址，以及其他規則。

## <a name="before-you-begin"></a>開始之前

「Azure 應用程式閘道」需要有自己的子網路。 當建立虛擬網路，請確定您保留足夠的位址空間 toohave 多個子網路。 一旦您部署應用程式閘道 tooa 子網路時，唯一的額外應用程式閘道可以加入 toohello 子網路。

## <a name="log-in-tooazure"></a>登入 tooAzure

開啟 hello **Microsoft Azure 命令提示字元**，並登入。 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> 您也可以使用`az login`不需要輸入 aka.ms/devicelogin 在程式碼的裝置登入的 hello 參數。

一旦您輸入 hello 前面範例中，將程式碼。 瀏覽 toohttps://aka.ms/devicelogin 瀏覽器 toocontinue hello 登入處理序。

![顯示裝置登入的 cmd][1]

在 hello 瀏覽器中，輸入您收到 hello 程式碼。 您已重新導向的 tooa 登入頁面。

![瀏覽器 tooenter 程式碼][2]

一旦輸入 hello 程式碼後您登入，關閉 hello 瀏覽器 toocontinue 與 hello 案例。

![已順利登入][3]

## <a name="create-hello-resource-group"></a>建立 hello 資源群組

建立 hello 應用程式閘道之前, 建立 toocontain hello 應用程式閘道資源群組。 hello 下列範例示範 hello 命令。

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a>建立 hello 應用程式閘道

hello 用於 hello 後端的 IP 位址是後端伺服器的 hello IP 位址。 這些值可以是任一個私用 Ip hello 虛擬網路、 公用 ip 時或針對後端伺服器的完整的網域名稱。 hello 下列範例會建立應用程式閘道的 http 設定、 連接埠和規則的其他組態設定。

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

hello 上述範例中顯示的應用程式閘道的 hello 建立期間不需要的許多屬性。 下列程式碼範例的 hello hello 所需資訊以建立應用程式閘道。

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> 如需可以在下列命令執行的建立 hello 期間提供的參數清單： `az network application-gateway create --help`。

這個範例會建立基本應用程式閘道 hello 接聽程式、 後端集區、 後端 http 設定和規則的預設設定。 可以修改這些設定 toosuit 部署一旦 hello 佈建成功。
如果您已經使用在先前步驟中，一旦建立，hello hello 後端集區定義的 web 應用程式負載平衡開始。

## <a name="get-application-gateway-dns-name"></a>取得應用程式閘道 DNS 名稱

一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。 當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。 tooensure 終端使用者可以叫用 hello 應用程式閘道，CNAME 記錄可使用的 toopoint toohello 公用端點的 hello 應用程式閘道。 [在 Azure 中設定自訂網域名稱](../dns/dns-custom-domain.md)。 tooconfigure 別名，擷取 hello 應用程式閘道和其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 項目附加的 toohello 應用程式閘道的詳細資料。 hello 應用程式閘道的 DNS 名稱應該使用的 toocreate CNAME 記錄，哪個點 hello 兩個 web 應用程式 toothis DNS 名稱。 不建議 hello 使用 A 記錄，因為可能會在重新啟動應用程式閘道變更 hello VIP。


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="delete-all-resources"></a>刪除所有資源

在本文中完成下列步驟的 hello 建立 toodelete 所有資源：

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a>後續步驟

了解如何 toocreate 自訂健全狀況探查造訪[建立自訂的健全狀況探查](application-gateway-create-probe-portal.md)

了解如何 tooconfigure SSL 卸載且採用 hello 昂貴 SSL 解密關閉您的 web 伺服器造訪[設定 SSL 卸載](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
