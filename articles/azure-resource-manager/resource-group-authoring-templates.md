---
title: "aaaAzure 資源管理員範本結構和語法 |Microsoft 文件"
description: "描述 hello 結構以及使用 JSON 的宣告式語法的 Azure Resource Manager 範本的屬性。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a>了解 hello 結構和語法的 Azure 資源管理員範本
本主題描述 Azure Resource Manager 範本 hello 結構。 它會呈現 hello 的範本和 hello 可用屬性的這些章節中的各區段。 hello 範本包含 JSON 和您可以為您的部署使用 tooconstruct 值的運算式。 如需建立範本的逐步教學課程，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。

## <a name="template-format"></a>範本格式
在最簡單的結構中，範本包含下列項目 hello:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| 元素名稱 | 必要 | 說明 |
|:--- |:--- |:--- |
| $schema |是 |描述 hello hello 範本語言版本的 hello JSON 結構描述檔案的位置。 使用 hello hello 前面範例所示的 URL。 |
| contentVersion |是 |Hello 範本 （例如 1.0.0.0) 的版本。 您可以為此元素提供任何值。 在部署時使用 hello 範本的資源，這個值可以是使用的 toomake 確定已使用該 hello 是正確的範本。 |
| 參數 |否 |部署時所提供的值執行 toocustomize 資源部署。 |
| variables |否 |會做為 JSON 片段 hello 範本 toosimplify 範本語言運算式中的值。 |
| resources |是 |在資源群組中部署或更新的資源類型。 |
| outputs |否 |部署後傳回的值。 |

每個元素都包含可以設定的屬性。 下列範例中的 hello 包含 hello 範本的完整語法：

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-hello parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

我們會檢查在本主題稍後的更詳細的 hello 範本 hello 區段。

## <a name="expressions-and-functions"></a>運算式和函式
hello 的 hello 範本的基本語法為 JSON。 不過，運算式和函數延伸 hello 範本內可用的 hello JSON 值。  運算式撰寫 JSON 字串常值內的第一個和最後一個字元是 hello 方括號：`[`和`]`分別。 部署 hello 範本時，會評估 hello hello 運算式值。 寫入字串常值，同時 hello 運算式的評估 hello 結果可以是不同的 JSON 型別，例如陣列或根據 hello 實際運算式的整數。  常值字串的開頭是括號 toohave `[`，而不是將它解譯為運算式，請加入一個額外的括號 toostart hello 字串`[[`。

一般而言，您可以使用運算式的函式 tooperform 作業，用來設定 hello 部署和作業。 和在 JavaScript 中相同，函式呼叫的格式為 `functionName(arg1,arg2,arg3)`。 您可以使用 hello 點和 [index] 運算子，以參考屬性。

下列範例中的 hello 顯示的 toouse 建構時，數個函數的值：

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

Hello 的樣板函式的完整清單，請參閱[Azure Resource Manager 範本函式](resource-group-template-functions.md)。 

## <a name="parameters"></a>參數
在 hello 參數區段中的 hello 範本，您可以指定部署時，您可以輸入哪些值 hello 資源。 這些參數值可讓您 toocustomize hello 部署 （例如開發、 測試和生產環境） 的特定環境提供量身訂做的值。 在範本中，沒有 tooprovide 參數，但不含參數範本會一律將部署 hello 與相同資源 hello 相同的名稱、 位置及內容。

您可以定義參數以 hello 下列結構：

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| 元素名稱 | 必要 | 說明 |
|:--- |:--- |:--- |
| parameterName |是 |Hello 參數的名稱。 必須是有效的 JavaScript 識別碼。 |
| type |是 |Hello 參數值的類型。 在此資料表之後，請參閱 hello 允許類型清單。 |
| defaultValue |否 |Hello 參數，如果未不提供任何值為 hello 參數的預設值。 |
| allowedValues |否 |允許的值為 hello 參數 toomake 確定係 hello 右值的陣列。 |
| minValue |否 |hello int 型別參數的最小值，這個值都包含在內。 |
| maxValue |否 |hello int 型別參數的最大值，這個值都包含在內。 |
| minLength |否 |hello 的最小長度字串、 secureString 和陣列型別參數，這個值都包含在內。 |
| maxLength |否 |hello 最大長度字串、 secureString 和陣列型別參數，這個值都包含在內。 |
| 說明 |否 |Toousers 透過 hello 入口網站顯示 hello 參數的描述。 |

hello 允許的類型和值如下：

* **字串**
* **secureString**
* **int**
* **bool**
* **object** 
* **secureObject**
* **array**

toospecify 參數為選擇性，提供預設值 （可以是空字串）。 

如果您在範本符合 hello 命令 toodeploy hello 範本中的參數中指定參數名稱，沒有關於 hello 所提供的值可能模稜兩可。 資源管理員會藉由新增 hello 後置解析混淆**FromTemplate** toohello 樣板參數。 例如，如果您包含名為的參數**ResourceGroupName**在範本中，與衝突 hello **ResourceGroupName**中 hello 參數[新 AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet。 在部署期間，您會提示的 tooprovide 值**ResourceGroupNameFromTemplate**。 一般情況下，您應該避免混淆，未指名參數，以做為部署作業所使用的參數名稱相同的 hello。

> [!NOTE]
> 所有密碼、 金鑰和其他機密資料，則應該使用 hello **secureString**型別。 如果您在 JSON 物件傳送機密資料，使用 hello **secureObject**型別。 部署資源後，無法讀取類型為 secureString 或 secureObject 的範本參數。 
> 
> 例如，hello hello 部署歷程記錄中的下列項目會顯示 hello 值對字串和物件，但對 secureString 和 secureObject。
>
> ![show deployment values](./media/resource-group-authoring-templates/show-parameters.png)  
>

下列範例會示範如何 hello toodefine 參數：

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

如何 tooinput hello 參數值在部署期間，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。 

## <a name="variables"></a>變數
在 hello 變數區段中，您可以建構可用的值在您的範本。 您不需要 toodefine 變數，但是它們通常範本減少簡化複雜運算式。

您可以定義變數以下列結構的 hello:

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

下列範例會示範如何 hello toodefine 建構自兩個參數值的變數：

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

hello 下一個範例顯示的變數是複雜的 JSON 型別和從其他變數建構的變數：

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a>資源
在 hello 資源區段中，您可以定義 hello 資源是已部署或更新。 本章節變得複雜，因為您必須了解 hello 類型與您要部署 tooprovide hello 正確的值。 如需 hello 特定資源值 （Microsoft.authorization、 類型和屬性），您需要 tooset，請參閱[Azure Resource Manager 範本中定義的資源](/azure/templates/)。 

您可以定義資源以 hello 下列結構：

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| 元素名稱 | 必要 | 說明 |
|:--- |:--- |:--- |
| condition | 否 | 布林值，指出是否要部署 hello 資源。 |
| apiVersion |是 |Hello REST API toouse 建立 hello 資源的版本。 |
| 類型 |是 |Hello 資源類型。 這個值是 hello hello 資源提供者和 hello 資源類型的命名空間的組合 (例如**microsoft.storage /**)。 |
| 名稱 |是 |Hello 資源的名稱。 hello 名稱必須遵照 RFC3986 中定義的 URI 元件限制。 此外，Azure hello 資源名稱 toooutside 合作對象所公開的服務驗證 hello 名稱 toomake 確定它不是嘗試 toospoof 其他身分識別。 |
| location |視情況而異 |提供資源的 hello 的支援的地理位置。 您可以選取任何 hello 可用的位置，但通常它使意義 toopick 是關閉 tooyour 使用者。 通常，也是合理 tooplace 資源彼此互動 hello 中相同的區域。 大部分的資源類型都需要有位置，但某些類型 (例如角色指派) 不需要位置。 請參閱[設定 Azure Resource Manager 範本中的資源位置](resource-manager-template-location.md)。 |
| tags |否 |Hello 資源相關聯的標記。 請參閱[標記 Azure Resource Manager 範本中的資源](resource-manager-template-tags.md)。 |
| comments |否 |記錄您的範本中的 hello 資源便箋 |
| copy |否 |如果需要多個執行個體，則 hello 資源 toocreate 數目。 hello 預設模式是平行處理。 指定序列的模式，當您不想要所有或 hello 資源 toodeploy hello 在相同的時間。 如需詳細資訊，請參閱[在 Azure Resource Manager 中建立資源的多個執行個體](resource-group-create-multiple.md)。 |
| dependsOn |否 |在部署這項資源之前必須部署的資源。 資源管理員會評估 hello 資源之間的相依性，並將它們部署在 hello 正確的順序。 資源若不互相依賴，則會平行部署資源。 hello 值可以是以逗號分隔的清單資源名稱或資源的唯一識別碼。 只會列出此範本中已部署的資源。 此範本中未定義的資源必須已經存在。 避免加入不必要的相依性，因為可能會降低部署速度並產生循環相依性。 如需設定相依性的指引，請參閱[定義 Azure Resource Manager 範本中的相依性](resource-group-define-dependencies.md)。 |
| properties |否 |資源特定的組態設定。 hello hello 屬性值是 hello 做為您提供 hello 要求主體中的 hello REST API 作業 （PUT 方法） toocreate hello 資源 hello 值相同。 您也可以指定複製陣列 toocreate 屬性的多個執行個體。 如需詳細資訊，請參閱[在 Azure Resource Manager 中建立資源的多個執行個體](resource-group-create-multiple.md)。 |
| resources |否 |正在定義的 hello 資源而定的子資源。 僅提供所允許的 hello hello 父資源結構描述的資源類型。 hello hello 子資源的完整型別包含 hello 父資源類型，例如**Microsoft.Web/sites/extensions**。 沒有隱含 hello 父資源上的相依性。 您必須明確定義該相依性。 |

hello 資源區段包含 hello 資源 toodeploy 的陣列。 在每個資源內，您也可以定義子資源陣列。 因此，您的 resources 區段可能會有類似以下的結構：

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

如需定義子資源的詳細資訊，請參閱[在 Resource Manager 範本中設定子資源的名稱和類型](resource-manager-template-child-resource.md)。

hello**條件**項目會指定是否要部署 hello 資源。 此項目的 hello 值解析 tootrue 或 false。 比方說，toospecify 是否在部署新的儲存體帳戶時，使用：

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

toospecify 是否以密碼或 SSH 金鑰部署虛擬機器定義兩個版本的 hello 虛擬機器在您的範本並使用**條件**toodifferentiate 使用量。 傳遞的參數會指定哪一個案例 toodeploy。

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

如需使用密碼或 SSH 金鑰 toodeploy 虛擬機器的範例，請參閱[使用者名稱或 SSH 條件範本](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json)。

## <a name="outputs"></a>輸出
在 hello 輸出區段中，您可以指定從部署所傳回的值。 例如，您可能會傳回 hello URI tooaccess 已部署的資源。

hello 下列範例顯示輸出定義 hello 的結構：

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| 元素名稱 | 必要 | 說明 |
|:--- |:--- |:--- |
| outputName |是 |Hello 輸出值的名稱。 必須是有效的 JavaScript 識別碼。 |
| type |是 |Hello 輸出值的類型。 輸出值支援在 hello 相同類型做為範本的輸入參數。 |
| value |是 |評估並傳回做為輸出值的範本語言運算式。 |

hello 下列範例顯示傳回 hello 輸出區段中的值。

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

如需使用輸出的相關資訊，請參閱 [Azure Resource Manager 範本中的共用狀態](best-practices-resource-manager-state.md)。

## <a name="template-limits"></a>範本限制

Hello 大小限制的範本 too1 MB，而每個參數檔案 too64 KB。 它已擴充與反覆的資源定義和變數和參數值之後，hello 1 MB 的限制會套用 hello 範本 toohello 最終狀態。 

您也受限於：

* 256 個參數
* 256 個變數
* 800 個資源 (包括複本計數)
* 64 個輸出值
* 範本運算式中的 24,576 個字元

使用巢狀範本，即可超出一些範本限制。 如需詳細資訊，請參閱[在部署 Azure 資源時使用連結的範本](resource-group-linked-templates.md)。 tooreduce hello 數目的參數、 變數或輸出，您可以結合數個值的物件。 如需詳細資訊，請參閱[物件作為參數](resource-manager-objects-as-parameters.md)。

## <a name="next-steps"></a>後續步驟
* tooview 完成範本的許多不同類型的方案，請參閱 hello [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)。
* 如需您可以使用從範本中的 hello 函式的詳細資訊，請參閱[Azure 資源管理員範本函式](resource-group-template-functions.md)。
* toocombine 多個範本，在部署期間，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)。
* 您可能需要 toouse 資源存在於不同的資源群組內。 這案例常見於使用多個資源群組之間所共用的儲存體帳戶或虛擬網路時。 如需詳細資訊，請參閱 hello [resourceId 函數](resource-group-template-functions-resource.md#resourceid)。
