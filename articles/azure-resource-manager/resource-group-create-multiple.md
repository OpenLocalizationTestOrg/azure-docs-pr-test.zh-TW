---
title: "aaaDeploy Azure 資源的多個執行個體 |Microsoft 文件"
description: "複製作業時使用和陣列中的 Azure Resource Manager 範本 tooiterate 多次部署資源。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a>在 Azure Resource Manager 範本中部署資源或屬性的多個執行個體
本主題說明如何在您的 Azure Resource Manager 範本 toocreate tooiterate 多個執行個體的資源或多個執行個體的資源上的屬性。

如果需要可讓您 toospecify tooadd 邏輯 tooyour 範本是否已部署的資源，請參閱[有條件地部署資源](#conditionally-deploy-resource)。

## <a name="resource-iteration"></a>資源反覆項目
toocreate 資源類型的多個執行個體加入`copy`元素 toohello 資源類型。 在 hello 複製項目，您可以指定 hello 反覆項目與名稱，此迴圈的數目。 hello 計數值必須是正整數，而且不能超過 800。 資源管理員會以平行方式建立 hello 資源。 因此，不保證它們建立所在的 hello 順序。 依序逐一查看 toocreate 資源，請參閱[序列複製](#serial-copy)。 

hello 資源 toocreate 多次採用下列格式的 hello:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

請注意該 hello 的每個資源名稱包含 hello`copyIndex()`函式，以傳回 hello 迴圈中的 hello 目前反覆項目。 `copyIndex()`是以零為基礎。 下列範例是，hello:

```json
"name": "[concat('storage', copyIndex())]",
```

會建立這些名稱︰

* storage0
* storage1
* storage2.

toooffset hello 索引值時，您可以在 hello copyIndex() 函式中傳遞的值。 hello tooperform 反覆項目數目仍中指定 hello 複製項目，但依指定的 hello copyIndex hello 值位移值。 下列範例是，hello:

```json
"name": "[concat('storage', copyIndex(1))]",
```

會建立這些名稱︰

* storage1
* storage2
* storage3

使用陣列，因為您可以逐一 hello 陣列中每個項目時，很有幫助 hello 複製作業。 使用 hello `length` hello 陣列 toospecify hello 計數反覆項目上的函式和`copyIndex`tooretrieve hello 目前陣列中的索引 hello。 下列範例是，hello:

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

會建立這些名稱︰

* storagecontoso
* storagefabrikam
* storagecoho

## <a name="serial-copy"></a>序列副本

當您使用 hello 複製項目 toocreate 多個執行個體的資源類型，資源管理員 中，依預設，會將部署這些執行個體，以平行方式。 不過，您可能想 toospecify 該資源會部署在順序中的 hello。 例如，在更新生產環境時，您可能想 toostagger hello 更新，只讓特定數目會更新一次。

資源管理員提供 hello 複製項目上的屬性，讓您 tooserially 部署多個執行個體。 在 hello 複製項目，設定`mode`太**序列**和`batchSize`toohello 一次的執行個體 toodeploy 數目。 序列模式中，資源管理員會在 hello 迴圈中，先前的執行個體上建立相依性，讓它不會啟動一個批次，直到 hello 前一個批次完成。

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

hello 模式屬性也會接受**平行**，這是 hello 預設值。

tootest 序列複製而不需要建立實際的資源，使用下列範本，將空的巢狀的範本部署的 hello:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

在 hello 部署歷程記錄，請注意，hello 巢狀的部署處理順序。

![序列部署](./media/resource-group-create-multiple/serial-copy.png)

比較實際的案例中，hello 下列範例會將兩個執行個體部署 Linux VM 從巢狀樣板一次：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a>屬性反覆運算

toocreate 屬性的資源上的多個值加入`copy`hello 屬性項目中的陣列。 這個陣列包含的物件，且每個物件具有下列屬性的 hello:

* 名稱-hello 名稱 hello 屬性 toocreate 的多個值
* 計數-hello 值 toocreate 數目
* 輸入層包含 hello 值 tooassign toohello 屬性的物件  

下列範例會示範如何 hello tooapply `copy` toohello dataDisks 屬性在虛擬機器上：

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

請注意，當使用`copyIndex`內屬性的反覆項目，您必須提供 hello hello 反覆項目名稱。 您沒有 tooprovide hello 名稱與資源的反覆項目搭配使用時。

資源管理員會展開 hello`copy`在部署期間的陣列。 hello hello 陣列名稱會變成 hello hello 屬性名稱。 hello 輸入的值會變成 hello 物件屬性。 部署的 hello 範本會變成：

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

您可以一起使用資源和屬性反覆運算。 參考 hello 屬性反覆項目名稱。

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

您只可包含一個複製項目中的每個資源的 hello 屬性。 toospecify 的反覆項目迴圈，針對多個屬性，定義 hello 複製陣列中的多個物件。 每個物件會分開反覆運算。 比方說，toocreate 多個執行個體的兩個 hello`frontendIPConfigurations`屬性和 hello`loadBalancingRules`負載平衡器上的屬性會定義這兩個物件中的單一複本項目： 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a>依迴圈中的資源而定
您可以指定資源部署另一個資源之後，使用 hello`dependsOn`項目。 toodeploy 取決於 hello 集合的資源在迴圈中，資源會提供 hello dependsOn 元素中的 hello 複製迴圈 hello 名稱。 hello 下列範例會示範如何在部署之前 toodeploy 三個儲存體帳戶 hello 虛擬機器。 不會顯示 hello 完整的虛擬機器定義。 請注意該 hello 複製項目沒有名稱設定得`storagecopy`和 hello 虛擬機器的 hello dependsOn 元素也會設定太`storagecopy`。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a>為子資源建立多個執行個體
您無法為子資源使用複製迴圈。 toocreate 通常定義為資源的多個執行個體巢狀方式置於另一個資源，您必須改為建立該資源為最上層資源。 您定義 hello 與 hello 透過 hello 類型和名稱屬性的父資源的關聯性。

例如，假設您通常將資料集定義為 Data Factory 中的子資源。

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

toocreate 多個執行個體的資料集，將它移之外 hello 資料 factory。 hello 資料集必須位於相同層級為 hello 的 data factory，hello，但它仍然是 hello data factory 的子資源。 您保留 hello 資料集和資料處理站，透過 hello 類型和名稱屬性之間的關聯性。 從其 hello 範本中的位置不再能夠推斷類型，因為您必須提供完整的 hello hello 格式類型： `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`。

tooestablish 父子式關聯性與 hello 的 data factory，執行個體提供 hello 包含 hello 父資源名稱的資料集的名稱。 使用 hello 格式： `{parent-resource-name}/{child-resource-name}`。  

hello 下列範例顯示 hello 實作：

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="conditionally-deploy-resource"></a>有條件地部署資源

toospecify 部署資源時，是否使用 hello`condition`項目。 此項目的 hello 值解析 tootrue 或 false。 當 hello 值為 true 時，部署 hello 資源。 當 hello 值為 false 時，未部署 hello 資源。 比方說，toospecify 是否已部署新的儲存體帳戶，或使用現有的儲存體帳戶時，使用：

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

如需使用新的或現有資源的範例，請參閱[新的或現有條件範本](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json)。

如需使用密碼或 SSH 金鑰 toodeploy 虛擬機器的範例，請參閱[使用者名稱或 SSH 條件範本](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json)。

## <a name="next-steps"></a>後續步驟
* 如果您想 toolearn 關於 hello 區段的範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。
* toolearn 如何 toodeploy 您的範本，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。

