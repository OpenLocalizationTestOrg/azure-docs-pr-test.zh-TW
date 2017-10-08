---
title: "aaaConsume Azure 受管理應用程式 |Microsoft 文件"
description: "描述客戶如何從已發佈的檔案建立 Azure 受管理的應用程式。"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a>使用內部受管理的應用程式

您可以使用 Azure [受管理的應用程式](managed-application-overview.md)，以供組織成員使用。 例如，您可以從 IT 部門選取受管理的應用程式，以確保符合組織標準。 這些受管理的應用程式皆可透過服務類別目錄，hello Azure Marketplace hello。

與此發行項之前，您必須擁有 hello 服務類別目錄中可用的受管理應用程式為您的訂用帳戶。 如果組織中有人尚未建立受管理的應用程式，請參閱[發佈受管理的應用程式以供內部使用](managed-application-publishing.md)。

目前，您可以使用 Azure CLI 或 hello Azure 入口網站 tooconsume 受管理的應用程式。

## <a name="create-hello-managed-application-by-using-hello-portal"></a>使用 hello 入口網站建立 hello 受管理應用程式

toodeploy 受管理的應用程式，透過 hello 入口網站，請遵循下列步驟：

1. 移 toohello Azure 入口網站。 搜尋 **Service Catalog 受管理的應用程式**。

   ![Service Catalog 受管理的應用程式](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. 選取 hello 管理您想從可用方案清單 hello toocreate 應用程式。 選取 [ **建立**]。

   ![受管理的應用程式選取](./media/managed-application-consumption/select-offer.png)

1. 提供所需要的 tooprovision hello 資源 hello 參數的值。 選取 [美國中西部] 為位置。 選取 [確定] 。

   ![受管理的應用程式參數](./media/managed-application-consumption/input-parameters.png)

1. hello 範本會驗證您所提供的 hello 值。 如果驗證成功，請選取**確定**toostart hello 部署。

   ![受管理的應用程式驗證](./media/managed-application-consumption/validation.png)

Hello 部署完成後，hello hello 範本中定義適當的資源會在您提供的 hello 受管理的資源群組中佈建。

## <a name="create-hello-managed-application-by-using-azure-cli"></a>使用 Azure CLI 建立 hello 受管理應用程式

有兩種方式 toocreate 受管理的應用程式使用 Azure CLI:

* 建立受管理的應用程式使用 hello 命令。
* 使用 hello 一般範本部署命令。

### <a name="use-hello-template-deployment-command"></a>使用 hello 範本部署命令

部署 hello 廠商建立的 hello applianceMainTemplate.json 檔案。

然後建立兩個資源群組。 hello 第一個資源群組是 hello 受管理的應用程式資源建立的位置： Microsoft.Solutions/appliances。 hello 第二個資源群組包含所有 hello mainTemplate.json 中定義。 此資源群組是由 hello ISV 管理。

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> 使用`westcentralus`做為 hello hello 資源群組的位置。
>

toodeploy applianceMainTemplate.json mainResourceGroup，下列命令使用 hello 中：

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

之後 hello 之前執行範本，它會提示您輸入 hello hello 範本中所定義的 hello 參數值。 此外 toohello 參數需要 tooprovision 資源範本中的，您需要兩個索引鍵的參數值：

- **managedResourceGroupId**: hello hello 資源群組包含 hello 資源 applianceMainTemplate.json 中定義的識別碼。 hello 識別碼是 hello 表單的`/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`。 在上述範例中的 hello，它的 hello 識別碼`managedResourceGroup`。
- **applianceDefinitionId**: hello 識別碼 hello 的受管理應用程式定義的資源。 這個值是由 hello ISV 提供。

> [!NOTE]
> hello 發行者必須授與存取 toohello 資源群組含有 hello 受管理應用程式定義。 hello 發行者訂用帳戶中建立 hello 定義資源。 因此，使用者、 使用者群組或在 hello 客戶租用戶中的應用程式需要讀取權限 toothis 資源。

Hello 部署成功完成之後，您會看到受管理的 hello mainResourceGroup 中建立應用程式。 managedResourceGroup 中建立 hello storageAccount 資源。

### <a name="use-hello-create-command"></a>使用 hello 建立命令

您可以使用 hello`az managedapp create`命令 toocreate hello 從 managed 應用程式受管理應用程式定義。

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* **應用裝置定義 Id**: hello 資源識別碼 hello 受管理的 hello 前面步驟中建立的應用程式定義。 tooobtain 這個識別碼，執行下列命令的 hello:

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  此命令會傳回 hello 受管理應用程式定義。 您需要 hello hello ID 屬性值。

* **管理 rg 識別碼**: hello hello 資源群組包含 hello 資源 applianceMainTemplate.json 中定義的名稱。 此資源群組是 hello 受管理的資源群組。 它被受 hello 發行者。 如果它不存在，則會為您建立。
* **資源群組**： 建立 hello hello 要受管理應用程式資源的資源群組。 hello Microsoft.Solutions/appliance 資源存在於此資源群組。
* **參數**: hello applianceMainTemplate.json 中定義的 hello 資源所需的參數。

## <a name="known-issues"></a>已知問題

此預覽版本包含下列問題的 hello:

* 500 內部伺服器錯誤會出現在 hello 建立 hello 受管理的應用程式。 如果您遇到此問題時，很可能 toobe 間歇性。 重試 hello 作業。
* 新的資源群組所需的 hello 受管理的資源群組。 如果您使用現有的資源群組，hello 部署將會失敗。
* hello 包含 hello Microsoft.Solutions/appliances 資源的資源群組必須在建立 hello **westcentralus**位置。

## <a name="next-steps"></a>後續步驟

* 對於簡介 toomanaged 應用程式，請參閱[受管理應用程式概觀](managed-application-overview.md)。
* 如需發佈 Service Catalog 受管理應用程式的資訊，請參閱[建立和發佈 Service Catalog 受管理的應用程式](managed-application-publishing.md)。
* 發佈受管理的應用程式 toohello Azure Marketplace 的相關資訊，請參閱[Azure 受管理應用程式在 hello Marketplace](managed-application-author-marketplace.md)。
* 使用來自 hello Marketplace 的受管理應用程式的相關資訊，請參閱[取用 Azure managed hello Marketplace 中的應用程式](managed-application-consume-marketplace.md)。
