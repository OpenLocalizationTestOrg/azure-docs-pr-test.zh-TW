---
title: "aaaAzure 資源提供者和資源類型 |Microsoft 文件"
description: "描述 hello 資源提供者支援資源管理員、 結構描述和可用的 API 版本，以及可以裝載 hello 資源 hello 區域。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a>資源提供者和類型

在部署資源時，您經常需要 tooretrieve hello 資源提供者和類型資訊。 在本文中，您將了解：

* 在 Azure 中檢視所有資源提供者
* 檢查資源提供者的註冊狀態
* 註冊資源提供者
* 檢視資源提供者的資源類型
* 檢視資源類型的有效位置
* 檢視資源類型的有效 API 版本

您可以執行下列步驟透過 hello 入口網站、 PowerShell 或 Azure CLI。

## <a name="powershell"></a>PowerShell

toosee 所有資源提供者，在 Azure 和 hello 登錄狀態，您的訂用帳戶，都使用：

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

傳回的結果類似於：

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

註冊資源提供者會設定您的訂用帳戶 toowork hello 資源提供者。 註冊的 hello 範圍一律是 hello 訂用帳戶。 許多資源提供者都會預設為自動註冊。 不過，您可能需要 toomanually 註冊一些資源提供者。 tooregister 資源提供者，您必須擁有的權限 tooperform hello `/register/action` hello 資源提供者的作業。 這項作業包含在 hello 參與者和擁有者角色。

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

傳回的結果類似於：

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

當訂用帳戶中仍有資源提供者的資源類型時，您無法取消註冊該資源提供者。

為特定資源提供者，使用 toosee 資訊：

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

傳回的結果類似於：

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

toosee hello 資源類型為資源提供者，使用：

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

它會傳回：

```powershell
batchAccounts
operations
locations
locations/quotas
```

hello API 版本對應 tooa 版本會釋出 hello 資源提供者的 REST API 作業。 資源提供者啟用新功能，因為它會釋出 hello REST API 的新版本。 

tooget hello 可用的 API 版本的資源類型，使用：

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

它會傳回：

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

資源管理員支援在所有區域，但您部署的 hello 資源可能不支援在所有區域。 此外，可能會禁止您使用支援 hello 資源某些地區的訂用帳戶限制。 

資源類型的 tooget hello 支援位置使用。

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

它會傳回：

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a>Azure CLI
toosee 所有資源提供者，在 Azure 和 hello 登錄狀態，您的訂用帳戶，都使用：

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

傳回的結果類似於：

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

註冊資源提供者會設定您的訂用帳戶 toowork hello 資源提供者。 註冊的 hello 範圍一律是 hello 訂用帳戶。 許多資源提供者都會預設為自動註冊。 不過，您可能需要 toomanually 註冊一些資源提供者。 tooregister 資源提供者，您必須擁有的權限 tooperform hello `/register/action` hello 資源提供者的作業。 這項作業包含在 hello 參與者和擁有者角色。

```azurecli
az provider register --namespace Microsoft.Batch
```

它會傳回一則訊息說明註冊持續進行中。

當訂用帳戶中仍有資源提供者的資源類型時，您無法取消註冊該資源提供者。

為特定資源提供者，使用 toosee 資訊：

```azurecli
az provider show --namespace Microsoft.Batch
```

傳回的結果類似於：

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

toosee hello 資源類型為資源提供者，使用：

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

它會傳回：

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

hello API 版本對應 tooa 版本會釋出 hello 資源提供者的 REST API 作業。 資源提供者啟用新功能，因為它會釋出 hello REST API 的新版本。 

tooget hello 可用的 API 版本的資源類型，使用：

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

它會傳回：

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

資源管理員支援在所有區域，但您部署的 hello 資源可能不支援在所有區域。 此外，可能會禁止您使用支援 hello 資源某些地區的訂用帳戶限制。 

資源類型的 tooget hello 支援位置使用。

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

它會傳回：

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a>入口網站

所有資源提供者，在 Azure 和 hello 登錄狀態，您的訂用帳戶中，都選取 toosee**訂閱**。

![選取 [訂用帳戶]](./media/resource-manager-supported-services/select-subscriptions.png)

選擇 hello 訂用帳戶 tooview。

![指定訂用帳戶](./media/resource-manager-supported-services/subscription.png)

選取**資源提供者**和檢視 hello 可用的資源提供者清單。

![顯示資源提供者](./media/resource-manager-supported-services/show-resource-providers.png)

註冊資源提供者會設定您的訂用帳戶 toowork hello 資源提供者。 註冊的 hello 範圍一律是 hello 訂用帳戶。 許多資源提供者都會預設為自動註冊。 不過，您可能需要 toomanually 註冊一些資源提供者。 tooregister 資源提供者，您必須擁有的權限 tooperform hello `/register/action` hello 資源提供者的作業。 這項作業包含在 hello 參與者和擁有者角色。 tooregister 資源提供者中，選取**註冊**。

![註冊資源提供者](./media/resource-manager-supported-services/register-provider.png)

當訂用帳戶中仍有資源提供者的資源類型時，您無法取消註冊該資源提供者。

選取 為特定資源提供者，toosee 資訊**更多服務**。

![選取 [更多服務]](./media/resource-manager-supported-services/more-services.png)

搜尋**資源總管**和選取從 hello 可用的選項。

![選取 [資源總管]](./media/resource-manager-supported-services/select-resource-explorer.png)

選取 [提供者]。

![選取 [提供者]](./media/resource-manager-supported-services/select-providers.png)

選取 hello 資源提供者和資源類型的 tooview。

![選取 [資源類型]](./media/resource-manager-supported-services/select-resource-type.png)

資源管理員支援在所有區域，但您部署的 hello 資源可能不支援在所有區域。 此外，可能會禁止您使用支援 hello 資源某些地區的訂用帳戶限制。 hello 資源總管會顯示 hello 資源類型的有效位置。

![顯示位置](./media/resource-manager-supported-services/show-locations.png)

hello API 版本對應 tooa 版本會釋出 hello 資源提供者的 REST API 作業。 資源提供者啟用新功能，因為它會釋出 hello REST API 的新版本。 hello 資源總管會顯示 hello 資源類型的有效應用程式開發介面版本。

![顯示 API 版本](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a>後續步驟
* toolearn 有關建立資源管理員範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。
* toolearn 有關部署資源，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。
* tooview hello 作業為資源提供者，請參閱[Azure REST API](/rest/api/)。

