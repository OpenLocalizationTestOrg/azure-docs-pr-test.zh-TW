---
title: "Azure 資源的 aaaSet 部署順序 |Microsoft 文件"
description: "描述如何將 tooset 一個資源依存於另一個資源期間部署 tooensure 資源部署 hello 正確的順序。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a>定義 hello 順序來部署 Azure 資源管理員範本中的資源
指定的資源，可以有其他資源，必須先建立 hello 資源部署。 比方說，SQL server 必須存在，然後再嘗試 toodeploy SQL 資料庫。 您定義此關聯性標示一個資源依存於 hello 與其他資源。 您定義的相依性以 hello **dependsOn**項目，或使用 hello**參考**函式。 

資源管理員會評估 hello 資源之間的相依性，並將它們部署在其相依順序。 資源若不互相依賴，資源管理員就會平行部署資源。 您只需要 toodefine 相依性的 hello 以部署的資源相同的範本。 

## <a name="dependson"></a>dependsOn
在您的範本，hello dependsOn 元素可讓您 toodefine 一個資源當做一個或多個資源相依性。 其值可以是以逗號分隔的資源名稱清單。 

hello 下列範例顯示取決於負載平衡器、 虛擬網路和一個迴圈，建立多個儲存體帳戶的虛擬機器規模集。 這些其他的資源不會顯示 hello 遵循範例中，但它們需要 tooexist hello 範本中的其他位置。

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

建立名為複製迴圈的 hello 資源相依性都會包含在上述範例中的 hello， **storageLoop**。 例如，請參閱 [在 Azure 資源管理員中建立多個資源的執行個體](resource-group-create-multiple.md)。

當定義相依性，您可以加入 hello 資源提供者命名空間和資源類型 tooavoid 模稜兩可。 例如，tooclarify 負載平衡器和虛擬網路，可能會有相同名稱與其他資源，使用下列的 hello hello 格式：

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

雖然您的資源之間可以想的 toouse dependsOn toomap 關聯性，是為什麼您所做的重要 toounderstand。 Toodocument 資源互連的方式，例如 dependsOn 不 hello 正確的方法。 您無法查詢哪些資源 hello dependsOn 元素中定義部署後。 使用 dependsOn 可能會影響部署時間，因為 Resource Manager 不會平行部署具有相依性的兩個資源。 toodocument 資源之間的關聯性改用[連結資源](/rest/api/resources/resourcelinks)。

## <a name="child-resources"></a>子資源
hello 資源屬性可讓您正在定義的相關的 toohello 資源的 toospecify 子資源。 定義子資源時，深度只能有 5 層。 請務必子資源與 hello 父資源之間建立 toonote 不是隱含的相依性。 如果您需要 hello 子資源 toobe 部署 hello 父資源之後，您必須明確 hello dependsOn 屬性與該相依性。 

每個父資源只接受特定的資源類型做為子資源。 hello 接受 hello 中指定的資源類型[範本結構描述](https://github.com/Azure/azure-resource-manager-schemas)的 hello 父資源。 hello 子資源類型名稱包含 hello 型別的名稱 hello 父資源，例如**Microsoft.Web/sites/config**和**Microsoft.Web/sites/extensions**這兩個的子資源 hello **Microsoft.Web/sites**。

hello 下列範例會顯示 SQL server 和 SQL database。 即使 hello 資料庫 hello 伺服器的子系，請注意 hello SQL database 與 SQL server 之間的已定義明確的相依性。

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a>reference 函式
hello[參考函式](resource-group-template-functions-resource.md#reference)可讓運算式 tooderive 它從其他的 JSON 名稱 / 值組或執行階段資源的值。 reference 運算式會隱含地宣告某個資源相依於另一個資源。 hello 一般格式為：

```json
reference('resourceName').propertyPath
```

在下列範例的 hello，CDN 端點明確相依於 hello 的 CDN 設定檔，並以隱含方式取決於 web 應用程式。

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

您可以使用這個項目 」 或 「 hello dependsOn 元素 toospecify 相依性，但是您不需要這兩個 toouse hello 相同的相依資源。 可能的話，請使用 加入不必要的相依性的隱含參考 tooavoid。

詳細資訊，請參閱 toolearn[參考函式](resource-group-template-functions-resource.md#reference)。

## <a name="recommendations-for-setting-dependencies"></a>設定相依性的建議

在決定哪些相依性 tooset 時，使用下列指導方針的 hello:

* 設定越少相依性越好。
* 設定子資源為相依於其父資源。
* 使用 hello**參考**函式之間需要 tooshare 屬性資源 tooset 隱含的相依性。 當您已經定義隱含的相依性時，不要新增明確的相依性 (**dependsOn**)。 這種方法可減少 hello 風險不必要的相依性。 
* 當資源必須有另一個資源的功能才能**建立**時，請設定相依性。 如果在部署之後只能互動 hello 資源未設定相依性。
* 讓相依性重疊顯示，而不需要明確設定它們。 例如，在虛擬網路介面，取決於您的虛擬機器和 hello 虛擬網路介面取決於虛擬網路與公用 IP 位址。 因此，hello 虛擬機器是部署在所有三個資源，但未明確設定 hello 虛擬機器做為相依於所有的三個資源。 此方法將釐清 hello 相依性順序並讓它更容易 toochange hello 範本稍後。
* 如果值無法決定部署之前，請嘗試部署 hello 資源，而不相依。 例如，如果設定值需要 hello 名稱的另一個資源，您可能不需要相依性。 本指南不會永遠運作，因為某些資源確認 hello hello 存在其他資源。 如果您收到錯誤，請加入相依性。 

Resource Manager 範本會在驗證期間識別循環相依性。 如果您收到錯誤訊息指出循環相依性存在時，評估範本 toosee，如果不需要任何相依性，而且可以移除。 如果移除相依性無法運作，您可以避免循環相依性，將某些部署作業移到部署後 hello 循環相依性的 「 hello 」 資源的子資源。 例如，假設您要部署兩部虛擬機器，但您必須設定，請參閱 toohello 其他每一個屬性。 您可以將它們部署在 hello 順序：

1. vm1
2. vm2
3. vm1 的擴充相依於 vm1 和 vm2。 hello 延伸模組設定 vm1 它 vm2 從取得的值。
4. vm2 的擴充相依於 vm1 和 vm2。 hello 延伸模組設定 vm2 它 vm1 從取得的值。

評估 hello 部署順序及解決相依性錯誤的相關資訊，請參閱[疑難排解常見的 Azure 部署錯誤與 Azure 資源管理員](resource-manager-common-deployment-errors.md)。

## <a name="next-steps"></a>後續步驟
* toolearn 有關疑難排解的相依性，在部署期間，請參閱[疑難排解常見的 Azure 部署錯誤與 Azure 資源管理員](resource-manager-common-deployment-errors.md)。
* toolearn 有關建立 Azure 資源管理員範本，請參閱[撰寫樣板](resource-group-authoring-templates.md)。 
* 如需在範本中的 hello 可用函數的清單，請參閱[樣板函式](resource-group-template-functions.md)。

