---
title: "aaaCreate Azure 應用程式閘道-範本 |Microsoft 文件"
description: "本頁面提供的指示 toocreate Azure 應用程式閘道使用 hello Azure Resource Manager 範本"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a>使用 hello Azure Resource Manager 範本來建立應用程式閘道

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure 傳統 PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager 範本](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI](application-gateway-create-gateway-cli.md)

Azure 應用程式閘道是第 7 層負載平衡器。 它提供容錯移轉和效能路由不同的伺服器之間的 HTTP 要求是否位於 hello 雲端或內部部署。 應用程式閘道提供許多應用程式傳遞控制器 (ADC) 功能，包括 HTTP 負載平衡、以 Cookie 為基礎的工作階段同質性、安全通訊端層 (SSL) 卸載、自訂健康情況探查、多網站支援，以及許多其他功能。 toofind 完整支援的功能清單，請瀏覽[應用程式閘道概觀](application-gateway-introduction.md)

這篇文章會逐步引導您下載並修改現有的 Azure Resource Manager 範本從 GitHub 及部署從 GitHub、 PowerShell 和 hello Azure CLI hello 範本。

如果您只需部署 hello Azure Resource Manager 範本，直接從 GitHub 不進行任何變更，請從 GitHub 略過 toodeploy 範本。

## <a name="scenario"></a>案例

在此案例中，您將會：

* 建立具有 Web 應用程式防火牆的應用程式閘道
* 建立名為 VirtualNetwork1 且含有 10.0.0.0/16 保留 CIDR 區塊的虛擬網路。
* 建立名為 Appgatewaysubnet 且使用 10.0.0.0/28 做為其 CIDR 區塊的子網路。
* 您想讓 tooload 平衡 hello 流量 hello 網頁伺服器先前已設定兩個後端 Ip 設定。 在此範本範例，hello 後端 Ip 是 10.0.1.10 和 10.0.1.11。

> [!NOTE]
> 這些設定是 hello 參數，此範本。 toocustomize hello 範本，您可以變更規則、 hello 接聽程式、 SSL 及 hello azuredeploy.json 檔案中的其他選項。

![案例](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>下載並了解 hello Azure Resource Manager 範本

您可以從 GitHub 下載現有 Azure Resource Manager 範本 toocreate hello 虛擬網路和兩個子網路，進行任何變更，您可能會想要並重複使用它。 toodo 因此，使用下列步驟的 hello:

1. 瀏覽過[啟用 web 應用程式防火牆的 建立應用程式閘道](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf)。
1. 依序按一下 [azuredeploy.json] 和 [RAW]。
1. 在電腦上儲存 hello 檔案 tooa 本機資料夾。
1. 如果您已熟悉 Azure 資源管理員範本，請略過 toostep 7。
1. 開啟您儲存的 hello 檔案，並查看下 hello 內容**參數**一行
1. Azure 資源管理員範本的參數提供值的預留位置，可以在部署期間填寫。

  | 參數 | 說明 |
  | --- | --- |
  | **subnetPrefix** |Hello 應用程式閘道子網路的 CIDR 區塊。 |
  | **applicationGatewaySize** | Hello 應用程式閘道的大小。  WAF 只允許中型和大型。 |
  | **backendIpaddress1** |Hello 第一部 web 伺服器的 IP 位址。 |
  | **backendIpaddress2** |Hello 第二部 web 伺服器的 IP 位址。 |
  | **wafEnabled** | 如果已啟用 WAF，設定 toodetermine。|
  | **wafMode** | Hello web 應用程式防火牆模式。  可用的選項為 **prevention** 或 **detection**。|
  | **wafRuleSetType** | WAF 的規則集類型。  目前 OWASP 是 hello 只支援的選項。 |
  | **wafRuleSetVersion** |規則集版本。 OWASP CRS 2.2.9 和 3.0 目前正在 hello 支援選項。 |

1. 檢查下的 hello 內容**資源**和注意事項 hello 下列屬性：

   * **type**。 Hello 範本所建立的資源類型。 在此情況下，hello 類型是`Microsoft.Network/applicationGateways`，用來表示應用程式閘道。
   * **名稱**。 Hello 資源的名稱。 請注意 hello 使用`[parameters('applicationGatewayName')]`，這表示該 hello 名稱做為輸入您或參數檔期間所部署。
   * **屬性**。 Hello 資源屬性的清單。 此範本建立應用程式閘道期間將使用 hello 虛擬網路和公用 IP 位址。

   > [!NOTE]
   > 如需範本的詳細資訊，請造訪︰[Resource Manager 範本參考](/templates/)

1. 瀏覽回太[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf)。
1. 按一下 azuredeploy-parameters.json，然後按一下RAW。
1. 在電腦上儲存 hello 檔案 tooa 本機資料夾。
1. 開啟您儲存的 hello 檔案並編輯 hello hello 參數值。 使用下列值 toodeploy hello 應用程式閘道我們的案例中所述的 hello。

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. 儲存 hello 檔案。 您可以使用線上 JSON 驗證工具，像是測試 hello JSON 範本和參數範本[JSlint.com](http://www.jslint.com/)。

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a>使用 PowerShell 來部署 hello Azure Resource Manager 範本

如果您從未使用過 Azure PowerShell，請瀏覽：[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)並遵循 hello 指示 toosign 至 Azure，然後選取您的訂用帳戶。

1. 登入 tooPowerShell

    ```powershell
    Login-AzureRmAccount
    ```

1. 請檢查 hello hello 帳戶的訂用帳戶。

    ```powershell
    Get-AzureRmSubscription
    ```

    您必須提示的 tooauthenticate 和您的認證。

1. 選擇 Azure 訂用帳戶 toouse。

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. 如有需要建立資源群組使用 hello**新增 AzureResourceGroup** cmdlet。 在下列範例的 hello，您可以建立呼叫 AppgatewayRG 美國東部位置中的資源群組。

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. 執行 hello**新增 AzureRmResourceGroupDeployment** cmdlet toodeploy hello 新的虛擬網路使用 hello 前下載，並修改範本和參數檔案。
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a>使用 Azure CLI hello 部署 hello Azure Resource Manager 範本

您使用 Azure CLI 下載 toodeploy hello Azure Resource Manager 範本，請依照下列步驟的 hello:

1. 如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](/cli/azure/install-azure-cli)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。

1. 如果有必要，請執行的 hello`az group create`命令 toocreate 資源群組，如下列程式碼片段的 hello 中所示。 請注意 hello hello 命令輸出。 之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。 如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    **-n (or --name)**。 Hello 新資源群組名稱。 在本文案例中為「appgatewayRG」 。
    
    **-l (或 --location)**。 Hello 新資源群組建立所在的 azure 區域。 在我們的案例中為 *westus*。

1. 執行 hello `az group deployment create` cmdlet toodeploy hello 新的虛擬網路使用 hello 範本和參數檔案，您可以下載並在 hello 前面步驟中修改。 之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a>使用部署按一下部署 hello Azure Resource Manager 範本

按一下 部署是另一個方式 toouse Azure Resource Manager 範本。 它是以 hello Azure 入口網站輕鬆 toouse 範本。

1. 跳過[建立 web 應用程式防火牆應用程式閘道](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/)。

1. 按一下**部署 tooAzure**。

    ![部署 tooAzure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. Hello hello 入口網站上的部署範本的 hello 參數，然後按一下 **確定**。

    ![參數](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. 選取**toohello 條款和條件前面所述，即表示我同意**按一下**購買**。

1. 在 hello 自訂部署刀鋒視窗中，按一下 **建立**。

## <a name="providing-certificate-data-tooresource-manager-templates"></a>提供憑證資料 tooResource 管理員範本

當使用範本中的 SSL，hello 憑證需要 toobe 而不是正在上傳的 base64 字串中提供。 tooconvert.pfx 或.cer tooa base64 字串可使用其中一個 hello 下列命令。 hello 下列命令會將轉換 hello 憑證 tooa base64 字串，它可以提供 toohello 範本。 hello 預期輸出，則可以儲存在變數中，且在 hello 範本中貼上的字串。

### <a name="macos"></a>macOS
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a>Windows
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a>刪除所有資源

toodelete 本文完成其中一個 hello 步驟中建立的所有資源：

### <a name="powershell"></a>PowerShell

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a>Azure CLI

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a>後續步驟

如果您想的 tooconfigure SSL 卸載，請造訪：[設定 SSL 卸載的應用程式閘道](application-gateway-ssl.md)。

如果您想 tooconfigure 內部負載平衡器的應用程式閘道 toouse，請造訪：[內部負載平衡器 (ILB) 建立應用程式閘道](application-gateway-ilb.md)。

如果您想進一步了解一般負載平衡選項，請造訪：

* [Azure 負載平衡器](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure 流量管理員](https://azure.microsoft.com/documentation/services/traffic-manager/)

