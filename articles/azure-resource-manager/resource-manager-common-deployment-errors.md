---
title: "aaaTroubleshoot 常見的 Azure 部署錯誤 |Microsoft 文件"
description: "描述如何部署使用 Azure 資源管理員資源 tooAzure 時 tooresolve 常見錯誤。"
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "部署錯誤，azure 部署，部署 tooazure"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a>使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解
本主題說明如何解決可能會遇到的一些常見 Azure 部署錯誤。

本主題將描述下列錯誤碼 hello:

* [AccountNameInvalid](#accountnameinvalid)
* [授權失敗](#authorization-failed)
* [BadRequest](#badrequest)
* [DeploymentFailed](#deploymentfailed)
* [DisallowedOperation](#disallowedoperation)
* [InvalidContentLink](#invalidcontentlink)
* [InvalidTemplate](#invalidtemplate)
* [MissingSubscriptionRegistration](#noregisteredproviderfound)
* [NotFound](#notfound)
* [NoRegisteredProviderFound](#noregisteredproviderfound)
* [OperationNotAllowed](#quotaexceeded)
* [ParentResourceNotFound](#parentresourcenotfound)
* [QuotaExceeded](#quotaexceeded)
* [RequestDisallowedByPolicy](#requestdisallowedbypolicy)
* [ResourceNotFound](#notfound)
* [SkuNotAvailable](#skunotavailable)
* [StorageAccountAlreadyExists](#storagenamenotunique)
* [StorageAccountAlreadyTaken](#storagenamenotunique)

## <a name="deploymentfailed"></a>DeploymentFailed

此錯誤碼指出一般的部署錯誤，但它不是您需要疑難排解 toostart hello 的錯誤代碼。 hello 實際上可協助您解決 hello 問題錯誤碼通常是以下這個錯誤的一個層級。 例如，hello 下列影像顯示 hello **RequestDisallowedByPolicy**低於 hello 部署錯誤的錯誤碼。

![顯示錯誤碼](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a>SkuNotAvailable

部署資源 （通常是虛擬機器），您可能會收到 hello 下錯誤程式碼和錯誤訊息：

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

Hello 資源 （例如 VM 大小），您已選取的 SKU 不適用於您所選取的 hello 位置時，您會收到這個錯誤。 tooresolve 此問題，您需要 toodetermine Sku 可用區域中。 您可以使用 PowerShell、 hello 入口網站或 REST 作業 toofind 可用的 Sku。

- 若是 PowerShell，請使用 [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) 並依位置篩選。 您必須擁有 hello 最新版的 PowerShell 此命令。

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  hello 結果包括 Sku hello 位置清單，以及適用於該 SKU 任何限制。

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- toouse hello[入口網站](https://portal.azure.com)、 登入 toohello 入口網站，並加入透過 hello 介面資源。 當您設定 hello 值，您會看到 hello 可用的 Sku，該資源。 您不需要 toocomplete hello 部署。

    ![可用的 SKU](./media/resource-manager-common-deployment-errors/view-sku.png)

- 虛擬機器的 toouse hello REST API 傳送 hello 下列要求：

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  它會傳回可用的 Sku 和區域中 hello 下列格式：

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

如果您無法 toofind 該地區或符合商務需求的其他區域中的適當 SKU，提交[SKU 要求](https://aka.ms/skurestriction)tooAzure 支援。

## <a name="disallowedoperation"></a>DisallowedOperation

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

如果您收到這個錯誤，您使用的訂用帳戶不允許 tooaccess Azure Active Directory 以外的任何 Azure 服務。 需要 tooaccess hello 傳統入口網站，但不是允許 toodeploy 資源後，您可能會出現這種類型的訂用帳戶。 tooresolve 此問題，您必須使用有權限 toodeploy 資源的訂用帳戶。  

tooview 您可用的訂用帳戶使用 PowerShell，使用：

```powershell
Get-AzureRmSubscription
```

此外，tooset hello 目前訂用帳戶，使用：

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

tooview 您可用的訂用帳戶使用 Azure CLI 2.0 中，使用：

```azurecli
az account list
```

此外，tooset hello 目前訂用帳戶，使用：

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a>InvalidTemplate
此錯誤可能起因於數個不同類型的錯誤。

- 語法錯誤

   如果您收到錯誤訊息，指出 hello 範本無法驗證時，您可能在範本中有語法問題。

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   這個錯誤，所以簡單 toomake 範本運算式可能很複雜。 例如，hello 下列名稱指派儲存體帳戶都包含一組括號、 三個函式、 三組括號、 一組的單引號和一個屬性：

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   如果您未提供 hello 比對語法，hello 範本會產生值將會不同於您的意圖。

   當您收到這種類型的錯誤時，請仔細檢閱 hello 運算式語法。 請考慮使用 [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) 或 [Visual Studio Code](resource-manager-vs-code.md) 等 JSON 編輯器，它們可以警告您有語法錯誤。

- 不正確的區段長度

   Hello 資源名稱不是處於 hello 正確的格式時，就會發生另一個無效的樣板錯誤。

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   根層級的資源必須有一個較少的區段中 hello 名稱，而非在 hello 資源類型。 每個區段是以斜線區分。 在下列範例的 hello，hello 類型有兩個區段和 hello 名稱會有一個區段，所以**有效名稱**。

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   Hello 下一個範例，但是**不是有效的名稱**因為它有 hello 的區段數與 hello 型別一樣。

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   如需子資源，hello 類型和名稱有 hello 相同的區段數目。 因為 hello 完整名稱和 hello 子類型包括 hello 父系名稱和型別，這個區段數目才有意義。 因此，hello 完整名稱仍會有一個較少區段比 hello 完整型別。

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   取得正確的 hello 區段可能很困難會套用於資源提供者的資源管理員類型。 例如，套用資源鎖定 tooa 網站需要四個區段的類型。 因此，hello 名稱是三個區段：

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- 不應該複製索引

   發生此錯誤的**InvalidTemplate**錯誤，當您套用 hello**複製**元素 tooa 範本之一部分的 hello 不支援這個項目。 您只可以套用 hello 複製項目 tooa 資源類型。 您無法套用複製 tooa 屬性內的資源類型。 例如，套用複製 tooa 虛擬機器，但您無法將它套用 toohello OS 磁碟的虛擬機器。 在某些情況下，您可以將轉換子資源 tooa 父資源 toocreate 在複製迴圈。 如需有關使用複製的詳細資訊，請參閱 [在 Azure Resource Manager 中建立資源的多個執行個體](resource-group-create-multiple.md)。

- 參數無效

   如果 hello 範本指定的允許的值的參數，而且您提供的值不是其中一個值，您會收到下列錯誤訊息類似 toohello:

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   檢查 hello hello 範本中允許的值，並提供在部署期間。

- 偵測到循環相依性

   當資源的相依性不會啟動 hello 部署中，您會收到這個錯誤。 只要有相互相依性的組合，就會讓兩個或多個資源等候其他也正在等候的資源。 例如，resource1 相依於 resource3、resource2 相依於 resource1，而 resource3 相依於 resource2。 您通常可以移除不必要的相依性來解決此問題。 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a>NotFound 和 ResourceNotFound
當您的範本包含無法解析資源 hello 名稱時，您會收到類似的錯誤：

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

如果您嘗試 toodeploy hello 遺漏 hello 範本中的資源，請檢查您是否需要 tooadd 相依性。 如果可能，Resource Manager 會以平行方式建立資源，將部署最佳化。 如果另一個資源之後，必須先部署一個資源，您需要 toouse hello **dependsOn**項目中的相依性，在您範本 toocreate hello 其他資源。 例如，在部署 web 應用程式時，必須存在 hello 應用程式服務方案。 如果您未指定該 hello web 應用程式相依於 hello App Service 方案，資源管理員會在 hello 建立兩個資源相同的時間。 您收到錯誤訊息指出找不到應用程式服務計劃的資源，該 hello，因為它尚未存在時嘗試 tooset hello web 應用程式上的屬性。 您可以在 hello web 應用程式中設定 hello 相依性，以避免這個錯誤。

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

如需針對相依性錯誤進行疑難排解的建議，請參閱[檢查部署順序](#check-deployment-sequence)。

Hello 資源位於不同的資源群組的其中一個要部署的 hello 存在時，也會看到這個錯誤。 在此情況下，使用 hello [resourceId 函數](resource-group-template-functions-resource.md#resourceid)tooget hello 完整的 hello 資源名稱。

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

如果您嘗試 toouse hello[參考](resource-group-template-functions-resource.md#reference)或[Listkey](resource-group-template-functions-resource.md#listkeys)函式具有無法解析，您會收到下列錯誤 hello 資源：

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

查詢運算式包含 hello**參考**函式。 再次確認 hello 參數值正確。

## <a name="parentresourcenotfound"></a>ParentResourceNotFound

父 tooanother 資源一個資源時，必須存在 hello 父資源，才能建立 hello 子資源。 如果尚未存在，您會收到下列錯誤 hello:

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

hello hello 子資源名稱包含 hello 父系名稱。 例如，SQL Database 可能定義如下︰

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

但是，如果您未在 hello 父資源上指定相依性，可能會取得 hello 子資源，部署 hello 父系之前。 tooresolve 這個錯誤，包含相依性。

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a>StorageAccountAlreadyExists 和 StorageAccountAlreadyTaken
儲存體帳戶，您必須提供 Azure 中是唯一的 hello 資源的名稱。 如果您未提供唯一的名稱，您會收到類似下列的錯誤：

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

您可以建立一個唯一的名稱，藉由串連 hello hello 結果與您命名慣例[uniqueString](resource-group-template-functions-string.md#uniquestring)函式。

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

如果您部署的 hello 的儲存體帳戶相同名稱與現有的儲存體帳戶訂用帳戶，但是提供不同的位置，您收到的錯誤指出 hello 儲存體帳戶已經存在於不同的位置。 請刪除現有儲存體帳戶 hello，或提供 hello 相同的位置，如 hello 現有儲存體帳戶。

## <a name="accountnameinvalid"></a>AccountNameInvalid
您會看到 hello **AccountNameInvalid**錯誤時嘗試的 toogive 儲存體帳戶名稱包含禁止的字元。 儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能使用數字和小寫字母。 hello [uniqueString](resource-group-template-functions-string.md#uniquestring)函式會傳回 13 個字元。 如果您在串連前置詞 toohello **uniqueString**產生，提供 11 個字元前置詞或更少。

## <a name="badrequest"></a>BadRequest

提供的屬性值無效時，您可能會碰到 BadRequest 狀態。 例如，如果您提供儲存體帳戶 SKU 值不正確，hello 部署將會失敗。 toodetermine 有效的值屬性，查看 hello [REST API](/rest/api)您要部署的 hello 資源類型。

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a>NoRegisteredProviderFound 和 MissingSubscriptionRegistration
在部署資源時，您可能會收到下列錯誤程式碼的 hello 和訊息：

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

或者，您可能會收到類似訊息，指出︰

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

您會因為下列三個原因其中一個而收到此錯誤︰

1. hello 資源提供者尚未註冊訂用帳戶
2. Hello 資源類型不支援的 API 版本
3. Hello 資源類型不支援的位置

hello 錯誤訊息應該提供支援的 hello 位置和 API 版本的建議。 您可以變更您的範本 tooone hello 的建議值。 大部分的提供者會自動註冊 hello 您使用的 Azure 入口網站或 hello 命令列介面，但不是全部。 如果您沒有使用特定的資源提供者之前，您可能需要 tooregister 該提供者。 您可以透過 PowerShell 或 Azure CLI，深入探索資源提供者。

**入口網站**

您可以看到 hello 登錄狀態並登錄資源提供者命名空間，透過 hello 入口網站。

1. 對於您的訂用帳戶，選取**資源提供者**。

   ![選取資源提供者](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. 查看 hello 資源提供者清單，並視需要選取 hello**註冊**連結 tooregister hello 資源提供者的 hello 類型嘗試 toodeploy。

   ![列出資源提供者](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

**PowerShell**

toosee 您的註冊狀態，使用**Get AzureRmResourceProvider**。

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

tooregister 為提供者，使用**暫存器 AzureRmResourceProvider**並提供 hello 名稱想 tooregister hello 資源提供者。

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

tooget hello 支援位置的特定類型的資源，請使用：

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

tooget hello 支援特定類型的資源，使用 API 版本：

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

**Azure CLI**

toosee hello 提供者註冊時，是否使用 hello`azure provider list`命令。

```azurecli
az provider list
```

tooregister 資源提供者，使用 hello`azure provider register`命令，並指定 hello*命名空間*tooregister。

```azurecli
az provider register --namespace Microsoft.Cdn
```

toosee hello 支援位置和資源類型的 API 版本使用：

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a>QuotaExceeded 和 OperationNotAllowed
當部署超過配額時 (也許是每個資源群組、訂用帳戶、帳戶及其他範圍的配額)，可能會發生問題。 例如，您的訂用帳戶可能會設定區域的核心 toolimit hello 數目。 如果您嘗試 toodeploy 具有更多的核心數目超過允許數量的 hello 的虛擬機器，您會收到的錯誤指出 hello 配額超過。
如需完整的配額資訊，請參閱 [Azure 訂用帳戶和服務限制、配額與條件約束](../azure-subscription-service-limits.md)。

tooexamine 您訂用帳戶配額的核心，您可以使用 hello `azure vm list-usage` hello Azure CLI 命令。 hello 下列範例將說明該 hello 核心配額，免費試用帳戶是 4:

```azurecli
az vm list-usage --location "South Central US"
```

它會傳回：

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

如果您部署的 hello 美國西部地區中建立四個以上的核心的範本，您會取得部署錯誤，看起來像：

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

在 PowerShell 中，您可以使用 hello 或者**Get AzureRmVMUsage** cmdlet。

```powershell
Get-AzureRmVMUsage
```

它會傳回：

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

在這些情況下，您應該移 toohello 入口網站，而且檔案支援問題 tooraise hello 區域要 toodeploy 配額。

> [!NOTE]
> 請記住，資源群組的 hello 配額是各地區，不適用於 hello 整個訂用帳戶。 如果您需要在美國西部的 toodeploy 30 個核心，您必須在美國西部 30 資源管理員核心 tooask。 如果您需要在任何 hello 區域 toowhich toodeploy 30 核心可以存取，您應該會尋求 30 的所有區域中的資源管理員核心。
>
>

## <a name="invalidcontentlink"></a>InvalidContentLink
當您收到 hello 錯誤訊息：

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

您最有可能嘗試 toolink tooa 巢狀的樣板，無法使用。 檢查 hello hello 巢狀範本提供的 URI。 如果儲存體帳戶中已有 hello 範本，請確定 hello URI 可供存取。 您可能需要 toopass SAS 權杖。 如需詳細資訊，請參閱 [透過 Azure 資源管理員使用連結的範本](resource-group-linked-templates.md)。

## <a name="requestdisallowedbypolicy"></a>RequestDisallowedByPolicy
當您的訂閱包含讓您在部署期間嘗試 tooperform 動作的資源原則，您會收到這個錯誤。 在 hello 錯誤訊息，尋找 hello 原則識別碼。

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

在**PowerShell**，提供該原則識別碼，則為 hello**識別碼**封鎖部署的 hello 原則的相關參數 tooretrieve 詳細資料。

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

在**Azure CLI**，提供 hello hello 原則定義名稱：

```azurecli
az policy definition show --name regionPolicyAssignment
```

如需詳細資訊，請參閱下列文章 hello:

- [RequestDisallowedByPolicy 錯誤](resource-manager-policy-requestdisallowedbypolicy-error.md)
- [使用原則 toomanage 資源，並控制存取](resource-manager-policy.md)。

## <a name="authorization-failed"></a>授權失敗
您可能會在部署期間收到錯誤，因為 hello 帳戶或服務主體嘗試 toodeploy hello 資源沒有存取 tooperform 那些動作。 Azure Active Directory 可讓您或您的系統管理員 toocontrol 哪些身分識別可以存取哪些資源以很大的有效位數。 例如，如果您的帳戶指派 toohello 讀取者角色，您不能 toocreate 資源。 在此情況下，您會看到錯誤訊息，指出授權失敗。

如需角色型存取控制的詳細資訊，請參閱 [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。


## <a name="next-steps"></a>後續步驟
* toolearn 有關稽核的動作，請參閱[稽核與資源管理員作業](resource-group-audit.md)。
* toolearn 有關動作 toodetermine hello 錯誤，在部署期間，請參閱[檢視部署作業](resource-manager-deployment-operations.md)。
