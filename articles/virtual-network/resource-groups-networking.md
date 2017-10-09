---
title: "aaaNetwork 資源提供者概觀 |Microsoft 文件"
description: "深入了解 hello 新的網路資源提供者在 「 Azure 資源管理員"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 79bf09da-4809-45cb-8d21-705616ef24dc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 81b8f51fe8ee180d8f7885c6e04eb953904d7be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="network-resource-provider"></a>網路資源提供者
支柱需要在今天的商務成就，是 hello 能力 toobuild 和敏捷式軟體開發、 彈性、 安全和可重複的方式來管理大規模的網路應用程式。 Azure 資源管理員可讓您 toocreate 這類應用程式，當做單一集合的資源群組中的資源。 管理這類資源時，是透過 Resource Manager 底下的各種資源提供者進行管理。

Azure 資源管理員必須使用不同的資源提供者 tooprovide 存取 tooyour 資源。 有三個主要的資源提供者：網路、儲存體和運算。 本文將討論 hello 特性和 hello 網路的資源提供者的優點包括：

* **中繼資料**– 您可以新增資訊 tooresources 使用標記。 這些標記也有使用的 tootrack 資源使用量的資源群組和訂閱。
* **更進一步控制網路** - 網路資源是進行鬆散偶合，而您可以更精密地控制它們。 這表示您可以更靈活地管理 hello 網路資源。
* **設定更快速** - 因為網路資源是進行鬆散偶合，所以您可以平行建立並協調網路資源。 這已經大幅減少設定時間。
* **Role Based Access Control** -RBAC 提供預設的角色，與特定安全性範圍，在加法 tooallowing hello 建立自訂的角色，安全管理。
* **更容易管理和部署**-它是更容易 toodeploy 和管理應用程式，因為您可以可以當做單一集合的資源群組中的資源建立整個應用程式堆疊。 和更快的 toodeploy，因為您可以部署只提供範本的 JSON 裝載。
* **快速自訂**-您可以使用宣告式樣式範本 tooenable 可重複且快速自訂部署。
* **可重複自訂**-您可以使用宣告式樣式範本 tooenable 可重複且快速自訂部署。
* **管理介面**-您可以使用任何下列介面 toomanage hello 資源：
  * REST 型 API
  * PowerShell
  * .NET SDK
  * Node.JS SDK
  * Java SDK
  * Azure CLI
  * 預覽入口網站
  * Resource Manager 範本語言

## <a name="network-resources"></a>網路資源
您現在可以獨立地管理網路資源，而不是透過單一計算資源 (虛擬機器) 進行管理。 這確保具有較高程度的彈性和靈活性可在資源群組中撰寫複雜且大型的基礎結構。

含有多介層應用程式之範例部署的概念檢視顯示如下。 您看到的每項資源 (如 NIC、公用 IP 位址和 VM 等) 都可以分開管理。

![網路資源模型](./media/resource-groups-networking/Figure2.png)

每項資源均包含一組通用屬性，以及其個別的屬性集。 hello 的通用屬性包括：

| 屬性 | 說明 | 範例值 |
| --- | --- | --- |
| **name** |唯一的資源名稱。 每個資源類型都有自己的命名限制。 |PIP01、VM01、NIC01 |
| **位置** |Azure 中的 hello 資源所在的區域 |westus、eastus |
| **id** |唯一的 URI 型識別 |/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP |

您可以檢查 hello 個別 hello 的以下各節中的資源屬性。

[!INCLUDE [virtual-networks-nrp-pip-include](../../includes/virtual-networks-nrp-pip-include.md)]

[!INCLUDE [virtual-networks-nrp-nic-include](../../includes/virtual-networks-nrp-nic-include.md)]

[!INCLUDE [virtual-networks-nrp-nsg-include](../../includes/virtual-networks-nrp-nsg-include.md)]

[!INCLUDE [virtual-networks-nrp-udr-include](../../includes/virtual-networks-nrp-udr-include.md)]

[!INCLUDE [virtual-networks-nrp-vnet-include](../../includes/virtual-networks-nrp-vnet-include.md)]

[!INCLUDE [virtual-networks-nrp-dns-include](../../includes/virtual-networks-nrp-dns-include.md)]

[!INCLUDE [virtual-networks-nrp-lb-include](../../includes/virtual-networks-nrp-lb-include.md)]

[!INCLUDE [virtual-networks-nrp-appgw-include](../../includes/virtual-networks-nrp-appgw-include.md)]

[!INCLUDE [virtual-networks-nrp-vpn-include](../../includes/virtual-networks-nrp-vpn-include.md)]

[!INCLUDE [virtual-networks-nrp-tm-include](../../includes/virtual-networks-nrp-tm-include.md)]

## <a name="management-interfaces"></a>管理介面
您可以使用不同的介面管理您的 Azure 網路資源。 在本文件中，我們將著重在指引這些介面：REST API 和範本。

### <a name="rest-api"></a>REST API
如前所述，網路資源可以透過各種介面進行管理，包括 REST API、.NET SDK、Node.JS SDK、Java SDK、PowerShell、CLI、Azure 入口網站和範本。

hello Rest API 的符合 toohello HTTP 1.1 通訊協定規格。 下列顯示 hello 一般 URI 結構 hello API:

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

和大括號中的 hello 參數代表 hello 下列項目：

* **subscription-id** - Azure 訂用帳戶識別碼。
* **資源提供者命名空間**-hello 所使用的提供者的命名空間。 hello hello 網路資源提供者的值是*Microsoft.Network*。
* **區域名稱**-hello Azure 區域名稱

hello HTTP 支援下列方法進行呼叫 toohello REST API 時：

* **PUT** -用 toocreate 指定類型的資源會修改資源屬性，或變更資源之間的關聯。
* **取得**-tooretrieve 資訊用於佈建的資源。
* **刪除**-使用 toodelete 現有的資源。

Hello 要求和回應符合 tooa JSON 裝載格式。 如需詳細資料，請參閱 [Azure 資源管理 API](https://msdn.microsoft.com/library/azure/dn948464.aspx)。

### <a name="resource-manager-template-language"></a>Resource Manager 範本語言
在加法 toomanaging 資源以命令方式 （透過應用程式開發介面或 SDK） 中，您也可以使用宣告式程式設計樣式 toobuild 和管理網路資源使用資源管理員範本語言 hello。

範本的範例表示法提供如下 –

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

hello 範本是主要的 JSON 描述 hello 資源和透過參數插入 hello 執行個體的值。 下列的 hello 範例可以使用的 toocreate 具有 2 的子網路的虛擬網路。

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/VNET.json",
        "contentVersion": "1.0.0.0",
        "parameters" : {
          "location": {
            "type": "String",
            "allowedValues": ["East US", "West US", "West Europe", "East Asia", "South East Asia"],
            "metadata" : {
              "Description" : "Deployment location"
            }
          },
          "virtualNetworkName":{
            "type" : "string",
            "defaultValue":"myVNET",
            "metadata" : {
              "Description" : "VNET name"
            }
          },
          "addressPrefix":{
            "type" : "string",
            "defaultValue" : "10.0.0.0/16",
            "metadata" : {
              "Description" : "Address prefix"
            }

          },
          "subnet1Name": {
            "type" : "string",
            "defaultValue" : "Subnet-1",
            "metadata" : {
              "Description" : "Subnet 1 Name"
            }
          },
          "subnet2Name": {
            "type" : "string",
            "defaultValue" : "Subnet-2",
            "metadata" : {
              "Description" : "Subnet 2 name"
            }
          },
          "subnet1Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.0.0/24",
            "metadata" : {
              "Description" : "Subnet 1 Prefix"
            }
          },
          "subnet2Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.1.0/24",
            "metadata" : {
              "Description" : "Subnet 2 Prefix"
            }
          }
        },
        "resources": [
        {
          "apiVersion": "2015-05-01-preview",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[parameters('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[parameters('subnet1Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet1Prefix')]"
                }
              },
              {
                "name": "[parameters('subnet2Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet2Prefix')]"
                }
              }
            ]
          }
        }
        ]
    }

您擁有 hello 選項時使用範本，以手動方式提供 hello 參數值，或者您可以使用參數檔案。 hello 下面範例會顯示一組可能的參數值 toobe 上述 hello 範本搭配使用：

    {
      "location": {
          "value": "East US"
      },
      "virtualNetworkName": {
          "value": "VNET1"
      },
      "subnet1Name": {
          "value": "Subnet1"
      },
      "subnet2Name": {
          "value": "Subnet2"
      },
      "addressPrefix": {
          "value": "192.168.0.0/16"
      },
      "subnet1Prefix": {
          "value": "192.168.1.0/24"
      },
      "subnet2Prefix": {
          "value": "192.168.2.0/24"
      }
    }


hello 的使用範本的主要優點包括：

* 您可以透過宣告樣式在資源群組中建置複雜的基礎結構。 hello 建立 hello 資源，包括相依性管理的協調流程會處理由資源管理員。
* hello 基礎結構可以建立可重複的方式在各個區域和區域內只要變更參數。
* hello 宣告式方法會導致 tooshorter 前置重疊時間建置 hello 範本與推出 hello 基礎結構。

如需範例範本，請參閱 [Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates)。

如需有關 hello 資源管理員範本語言的詳細資訊，請參閱[Azure 資源管理員範本語言](../azure-resource-manager/resource-group-authoring-templates.md)。

hello 虛擬網路和子網路資源，則會使用上述的 hello 範例範本。 下列是其他您可以使用的網路資源：

### <a name="using-a-template"></a>使用範本
使用 PowerShell、 AzureCLI，或按一下 toodeploy 執行從 GitHub，您可以部署服務 tooAzure 從範本。 toodeploy 服務範本，以在 GitHub 中，執行下列步驟的 hello:

1. 從 GitHub 開啟 hello template3 檔案。 在此範例中，請開啟 [具有兩個子網路的虛擬網路](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network)。
2. 按一下**部署 tooAzure**，然後登入 toohello 在 Azure 入口網站使用您的認證。
3. 確認 hello 範本，然後按一下**儲存**。
4. 按一下**編輯參數**選取一個位置，例如*美國西部*、 hello vnet 和子網路。
5. 如有必要，變更 hello **ADDRESSPREFIX**和**SUBNETPREFIX**參數，然後再按一下**確定**。
6. 按一下**選取資源群組**，然後按一下您想 tooadd hello vnet 和子網路與 hello 資源群組。 或者，您可以按一下 [或建立新的] 來建立新的資源群組。
7. 按一下 [建立] 。 請注意 hello 磚顯示**佈建的範本部署**。 一旦 hello 部署完成，您會看到以下畫面類似 tooone。

![範例範本部署](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a>後續步驟
[Azure 資源管理員範本語言](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure 網路 - 常用範本](https://github.com/Azure/azure-quickstart-templates)

[Azure Resource Manager 與傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)

[Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)

