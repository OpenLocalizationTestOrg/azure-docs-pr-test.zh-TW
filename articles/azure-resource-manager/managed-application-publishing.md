---
title: "aaaCreate 和發行的 Azure 服務管理的類別目錄的應用程式 |Microsoft 文件"
description: "顯示如何 toocreate Azure 管理應用程式，僅供貴組織的成員。"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 31f2f9e3b50f57dae7f4dcf2edefa7366bfff25c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="03826-103">發佈受管理的應用程式，以供內部使用</span><span class="sxs-lookup"><span data-stu-id="03826-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="03826-104">您可以建立及發佈 Azure [受管理的應用程式](managed-application-overview.md)，以供組織成員使用。</span><span class="sxs-lookup"><span data-stu-id="03826-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="03826-105">例如，IT 部門可以發佈受管理的應用程式，以確保符合組織標準。</span><span class="sxs-lookup"><span data-stu-id="03826-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="03826-106">這些受管理的應用程式皆可透過 hello 服務類別目錄，hello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="03826-106">These managed applications are available through hello service catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="03826-107">toopublish hello 服務類別目錄的受管理應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="03826-107">toopublish a managed application for hello service catalog, you must:</span></span>

* <span data-ttu-id="03826-108">建立包含三個所需的範本檔案 hello 以.zip 封裝。</span><span class="sxs-lookup"><span data-stu-id="03826-108">Create a .zip package that contains hello three required template files.</span></span>
* <span data-ttu-id="03826-109">決定哪些使用者、 群組或應用程式需要存取 toohello hello 使用者訂用帳戶中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="03826-109">Decide which user, group, or application needs access toohello resource group in hello user's subscription.</span></span>
* <span data-ttu-id="03826-110">建立 hello 受管理應用程式定義點 toohello.zip 套件，並要求 hello 身分識別的存取權。</span><span class="sxs-lookup"><span data-stu-id="03826-110">Create hello managed application definition that points toohello .zip package and requests access for hello identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="03826-111">建立受管理的應用程式套件</span><span class="sxs-lookup"><span data-stu-id="03826-111">Create a managed application package</span></span>

<span data-ttu-id="03826-112">hello 第一個步驟是 toocreate hello 三個所需的範本檔案。</span><span class="sxs-lookup"><span data-stu-id="03826-112">hello first step is toocreate hello three required template files.</span></span> <span data-ttu-id="03826-113">這三個檔案封裝成.zip 檔，並將它上傳 tooan 可存取的位置，例如儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="03826-113">Package all three files into a .zip file, and upload it tooan accessible location, such as a storage account.</span></span> <span data-ttu-id="03826-114">建立 hello 受管理的應用程式定義時，您可以傳遞連結 toothis.zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="03826-114">You pass a link toothis .zip file when creating hello managed application definition.</span></span>

* <span data-ttu-id="03826-115">**applianceMainTemplate.json**： 此檔案會定義 hello Azure 管理應用程式的一部分 hello 佈建的資源。</span><span class="sxs-lookup"><span data-stu-id="03826-115">**applianceMainTemplate.json**: This file defines hello Azure resources that are provisioned as part of hello managed application.</span></span> <span data-ttu-id="03826-116">hello 範本並無不同規則的 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="03826-116">hello template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="03826-117">例如，toocreate 透過 managed 應用程式的儲存體帳戶，applianceMainTemplate.json 包含：</span><span class="sxs-lookup"><span data-stu-id="03826-117">For example, toocreate a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]",
            "apiVersion": "2016-01-01",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {}
  }
  ```

* <span data-ttu-id="03826-118">**mainTemplate.json**： 建立 hello 受管理的應用程式時，使用者將部署此範本。</span><span class="sxs-lookup"><span data-stu-id="03826-118">**mainTemplate.json**: Users deploy this template when creating hello managed application.</span></span> <span data-ttu-id="03826-119">它會定義受管理的 hello 應用程式資源，也就是 Microsoft.Solutions/appliances 資源類型。</span><span class="sxs-lookup"><span data-stu-id="03826-119">It defines hello managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="03826-120">此檔案包含所有的 hello 參數，您需要的 applianceMainTemplate.json hello 資源。</span><span class="sxs-lookup"><span data-stu-id="03826-120">This file contains all hello parameters you need for hello resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="03826-121">您會在此範本中設定兩個重要的屬性。</span><span class="sxs-lookup"><span data-stu-id="03826-121">You set two important properties in this template.</span></span> <span data-ttu-id="03826-122">首先，hello **applianceDefinitionId**屬性是 hello 識別碼 hello 受管理應用程式定義。</span><span class="sxs-lookup"><span data-stu-id="03826-122">First, hello **applianceDefinitionId** property is hello ID of hello managed application definition.</span></span> <span data-ttu-id="03826-123">您在本主題稍後建立 hello 定義。</span><span class="sxs-lookup"><span data-stu-id="03826-123">You create hello definition later in this topic.</span></span> <span data-ttu-id="03826-124">設定此值時，您必須決定哪些訂用帳戶和儲存資源群組 toouse hello 受管理的應用程式定義。</span><span class="sxs-lookup"><span data-stu-id="03826-124">When setting this value, you must decide which subscription and resource group toouse for storing hello managed application definitions.</span></span> <span data-ttu-id="03826-125">而且，您必須決定 hello 定義的名稱。</span><span class="sxs-lookup"><span data-stu-id="03826-125">And, you must decide on a name for hello definition.</span></span> <span data-ttu-id="03826-126">hello 識別碼的 hello 格式：</span><span class="sxs-lookup"><span data-stu-id="03826-126">hello ID is in hello format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="03826-127">第二，hello **managedResourceGroupId**屬性是 hello hello 資源群組識別碼 hello Azure 資源建立的位置。</span><span class="sxs-lookup"><span data-stu-id="03826-127">Second, hello **managedResourceGroupId** property is hello ID of hello resource group where hello Azure resources are created.</span></span> <span data-ttu-id="03826-128">您可以指派值給這個資源群組名稱，或讓 hello 使用者提供的名稱。</span><span class="sxs-lookup"><span data-stu-id="03826-128">You can assign a value for this resource group name or let hello user provide a name.</span></span> <span data-ttu-id="03826-129">hello 的 hello 識別碼的格式如下：</span><span class="sxs-lookup"><span data-stu-id="03826-129">hello format of hello ID is:</span></span>

  <span data-ttu-id="03826-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`。</span><span class="sxs-lookup"><span data-stu-id="03826-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="03826-131">下列範例中的 hello 顯示 mainTemplate.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="03826-131">hello following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="03826-132">它會指定部署的 hello 資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="03826-132">It specifies a resource group for hello deployed resources.</span></span> <span data-ttu-id="03826-133">hello 定義 ID 已定義命名集 toouse **storageApp**資源群組中名為**managedApplicationGroup**。</span><span class="sxs-lookup"><span data-stu-id="03826-133">hello definition ID is set toouse a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="03826-134">您可以變更這些值 toouse 不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="03826-134">You can change these values toouse different names.</span></span> <span data-ttu-id="03826-135">提供您自己的訂用帳戶 ID 中 hello 定義 id。</span><span class="sxs-lookup"><span data-stu-id="03826-135">Provide your own subscription ID in hello definition ID.</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "variables": {
        "managedRGId": "[concat(resourceGroup().id,'-application-resources')]",
        "managedAppName": "[concat('managedStorage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Solutions/appliances",
            "name": "[variables('managedAppName')]",
            "apiVersion": "2016-09-01-preview",
            "location": "[resourceGroup().location]",
            "kind": "ServiceCatalog",
            "properties": {
                "managedResourceGroupId": "[variables('managedRGId')]",
                "applianceDefinitionId": "/subscriptions/<subscription-id>/resourceGroups/managedApplicationGroup/providers/Microsoft.Solutions/applianceDefinitions/storageApp",
                "parameters": {
                    "storageAccountNamePrefix": {
                        "value": "[parameters('storageAccountNamePrefix')]"
                    }
                }
            }
        }
    ]
  }
  ```

* <span data-ttu-id="03826-136">**applianceCreateUiDefinition.json**: hello Azure 入口網站會使用這個檔案 toogenerate hello 使用者介面的使用者建立 hello 受管理的應用程式。</span><span class="sxs-lookup"><span data-stu-id="03826-136">**applianceCreateUiDefinition.json**: hello Azure portal uses this file toogenerate hello user interface for users who create hello managed application.</span></span> <span data-ttu-id="03826-137">您可以定義使用者提供每個參數輸入的方式。</span><span class="sxs-lookup"><span data-stu-id="03826-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="03826-138">您可以使用諸如下拉式清單、文字方塊、密碼方塊和其他輸入工具等選項。</span><span class="sxs-lookup"><span data-stu-id="03826-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="03826-139">如何 toocreate UI 定義檔案為受管理的應用程式，請參閱的 toolearn[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="03826-139">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="03826-140">hello 下列範例顯示 applianceCreateUiDefinition.json 檔案，可讓使用者 toospecify hello 儲存體帳戶名稱前置詞到文字方塊。</span><span class="sxs-lookup"><span data-stu-id="03826-140">hello following example shows an applianceCreateUiDefinition.json file that enables users toospecify hello storage account name prefix through a textbox.</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {
                "name": "storageAccounts",
                "type": "Microsoft.Common.TextBox",
                "label": "Storage account name prefix",
                "defaultValue": "storage",
                "toolTip": "Provide a value that is used for hello prefix of your storage account. Limit too11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-11 characters long."
                },
                "visible": true
            }
        ],
        "steps": [],
        "outputs": {
            "storageAccountNamePrefix": "[basics('storageAccounts')]"
        }
    }
  }
  ```

<span data-ttu-id="03826-141">準備好 hello 所需的所有檔案後，封裝它們的.zip 檔。</span><span class="sxs-lookup"><span data-stu-id="03826-141">After all hello needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="03826-142">hello 三個檔案必須位於根層級 hello hello.zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="03826-142">hello three files must be at hello root level of hello .zip file.</span></span> <span data-ttu-id="03826-143">如果您將其放在資料夾中，建立 hello 受管理的應用程式定義指出 hello 所需的檔案不存在時收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="03826-143">If you put them in a folder, you receive an error when creating hello managed application definition that states hello required files are not present.</span></span> <span data-ttu-id="03826-144">上傳從可以取用它的 hello 封裝 tooan 存取位置。</span><span class="sxs-lookup"><span data-stu-id="03826-144">Upload hello package tooan accessible location from where it can be consumed.</span></span> <span data-ttu-id="03826-145">hello 本文其餘部分會假設 hello.zip 檔案存在於可公開存取的儲存體 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="03826-145">hello remainder of this article assumes hello .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="03826-146">建立 Azure Active Directory 使用者群組或應用程式</span><span class="sxs-lookup"><span data-stu-id="03826-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="03826-147">tooselect 使用者群組或應用程式管理 hello 資源代表 hello 客戶 hello 第二個步驟。</span><span class="sxs-lookup"><span data-stu-id="03826-147">hello second step is tooselect a user group or application for managing hello resources on behalf of hello customer.</span></span> <span data-ttu-id="03826-148">此使用者群組或應用程式對 hello 受管理的資源群組相應 toohello 角色指派的權限。</span><span class="sxs-lookup"><span data-stu-id="03826-148">This user group or application has permissions on hello managed resource group according toohello role that is assigned.</span></span> <span data-ttu-id="03826-149">hello 角色可以是任何內建的角色型存取控制 (RBAC) 角色，例如擁有者或參與者。</span><span class="sxs-lookup"><span data-stu-id="03826-149">hello role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="03826-150">您也可以提供個別的使用者權限 toomanage hello 資源，但您通常指派此權限 tooa 使用者群組。</span><span class="sxs-lookup"><span data-stu-id="03826-150">You also can give an individual user permission toomanage hello resources, but typically you assign this permission tooa user group.</span></span> <span data-ttu-id="03826-151">toocreate 新的 Active Directory 使用者群組，請參閱[建立群組並新增 Azure Active Directory 中的成員](../active-directory/active-directory-groups-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="03826-151">toocreate a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="03826-152">您用於管理 hello 資源需要 hello 使用者群組 toouse hello 物件識別碼。</span><span class="sxs-lookup"><span data-stu-id="03826-152">You need hello object ID of hello user group toouse for managing hello resources.</span></span> <span data-ttu-id="03826-153">hello 下列範例顯示如何 tooget hello 從 hello 群組的顯示名稱的物件識別碼：</span><span class="sxs-lookup"><span data-stu-id="03826-153">hello following example shows how tooget hello object ID from hello group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="03826-154">hello 範例命令會傳回下列輸出的 hello:</span><span class="sxs-lookup"><span data-stu-id="03826-154">hello example command returns hello following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="03826-155">tooretrieve 只 hello 物件識別碼，使用：</span><span class="sxs-lookup"><span data-stu-id="03826-155">tooretrieve just hello object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a><span data-ttu-id="03826-156">取得 hello 角色定義 ID</span><span class="sxs-lookup"><span data-stu-id="03826-156">Get hello role definition ID</span></span>

<span data-ttu-id="03826-157">接下來，您需要 hello RBAC toogrant 存取 toohello 使用者、 使用者群組或應用程式的內建角色 hello 角色定義 ID。</span><span class="sxs-lookup"><span data-stu-id="03826-157">Next, you need hello role definition ID of hello RBAC built-in role you want toogrant access toohello user, user group, or application.</span></span> <span data-ttu-id="03826-158">通常，您會使用 hello 擁有者或參與者或讀取器角色。</span><span class="sxs-lookup"><span data-stu-id="03826-158">Typically, you use hello Owner or Contributor or Reader role.</span></span> <span data-ttu-id="03826-159">hello，下列命令顯示如何 tooget hello hello 擁有者角色的角色定義 ID:</span><span class="sxs-lookup"><span data-stu-id="03826-159">hello following command shows how tooget hello role definition ID for hello Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="03826-160">該命令會傳回下列輸出的 hello:</span><span class="sxs-lookup"><span data-stu-id="03826-160">That command returns hello following output:</span></span>

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access tooresources.",
      "permissions": [
        {
          "actions": [
            "*"
         ],
         "notActions": []
        }
      ],
      "roleName": "Owner",
      "type": "BuiltInRole"
    },
    "type": "Microsoft.Authorization/roleDefinitions"
}
```

<span data-ttu-id="03826-161">您需要從前面範例中的 hello hello"name"屬性 hello 值。</span><span class="sxs-lookup"><span data-stu-id="03826-161">You need hello value of hello "name" property from hello preceding example.</span></span> <span data-ttu-id="03826-162">您可以透過下列程式碼只擷取該屬性：</span><span class="sxs-lookup"><span data-stu-id="03826-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a><span data-ttu-id="03826-163">建立 hello 受管理應用程式定義</span><span class="sxs-lookup"><span data-stu-id="03826-163">Create hello managed application definition</span></span>

<span data-ttu-id="03826-164">如果您尚未有可儲存受管理應用程式定義的資源群組，請立即建立一個：</span><span class="sxs-lookup"><span data-stu-id="03826-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="03826-165">現在，建立 hello 受管理應用程式定義的資源。</span><span class="sxs-lookup"><span data-stu-id="03826-165">Now, create hello managed application definition resource.</span></span>

```azurecli-interactive
az managedapp definition create \
  --name storageApp \
  --location "westcentralus" \
  --resource-group managedApplicationGroup \
  --lock-level ReadOnly \
  --display-name myteststorageapp \
  --description storageapp \
  --authorizations "$groupid:$roleid" \
  --package-file-uri <uri-path-to-zip-file>
```

<span data-ttu-id="03826-166">hello hello 前面範例中使用的參數如下：</span><span class="sxs-lookup"><span data-stu-id="03826-166">hello parameters used in hello preceding example are:</span></span>

* <span data-ttu-id="03826-167">**資源群組**： 建立 hello hello hello 要受管理應用程式定義的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="03826-167">**resource-group**: hello name of hello resource group where hello managed application definition is created.</span></span>
* <span data-ttu-id="03826-168">**鎖定層級**: hello 鎖定類型的放置 hello 受管理的資源群組。</span><span class="sxs-lookup"><span data-stu-id="03826-168">**lock-level**: hello type of lock placed on hello managed resource group.</span></span> <span data-ttu-id="03826-169">它可以防止 hello 客戶執行非預期的作業上此資源群組。</span><span class="sxs-lookup"><span data-stu-id="03826-169">It prevents hello customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="03826-170">目前，ReadOnly 是 hello 才支援鎖定層級。</span><span class="sxs-lookup"><span data-stu-id="03826-170">Currently, ReadOnly is hello only supported lock level.</span></span> <span data-ttu-id="03826-171">當指定 ReadOnly 時，hello 客戶只能讀取 hello hello 受管理的資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="03826-171">When ReadOnly is specified, hello customer can only read hello resources present in hello managed resource group.</span></span>
* <span data-ttu-id="03826-172">**授權**： 描述 hello 主體識別碼和 hello 角色定義 ID 使用的 toogrant 權限 toohello 受管理的資源群組。</span><span class="sxs-lookup"><span data-stu-id="03826-172">**authorizations**: Describes hello principal ID and hello role definition ID that are used toogrant permission toohello managed resource group.</span></span> <span data-ttu-id="03826-173">指定格式的 hello `<principalId>:<roleDefinitionId>`。</span><span class="sxs-lookup"><span data-stu-id="03826-173">It's specified in hello format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="03826-174">這個屬性也可以指定多個值。</span><span class="sxs-lookup"><span data-stu-id="03826-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="03826-175">如果需要多個值，則應該指定 hello 形式`<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`。</span><span class="sxs-lookup"><span data-stu-id="03826-175">If multiple values are needed, they should be specified in hello form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="03826-176">多個值之間以空格分隔。</span><span class="sxs-lookup"><span data-stu-id="03826-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="03826-177">**封裝檔案 uri**: hello hello hello 範本，其中包含檔案可以是 Azure 儲存體 blob 的受管理的應用程式封裝的位置。</span><span class="sxs-lookup"><span data-stu-id="03826-177">**package-file-uri**: hello location of hello managed application package that contains hello template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03826-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="03826-178">Next steps</span></span>

* <span data-ttu-id="03826-179">對於簡介 toomanaged 應用程式，請參閱[受管理應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="03826-179">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="03826-180">如需 hello 檔案的範例，請參閱[受管理應用程式範例](https://github.com/Azure/azure-managedapp-samples/tree/master/samples)。</span><span class="sxs-lookup"><span data-stu-id="03826-180">For examples of hello files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="03826-181">如需使用 Service Catalog 受管理應用程式的詳細資訊，請參閱[使用 Service Catalog 受管理的應用程式](managed-application-consumption.md)。</span><span class="sxs-lookup"><span data-stu-id="03826-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="03826-182">發佈受管理的應用程式 toohello Azure Marketplace 的相關資訊，請參閱[Azure 受管理應用程式在 hello Marketplace](managed-application-author-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="03826-182">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="03826-183">使用來自 hello Marketplace 的受管理應用程式的相關資訊，請參閱[取用 Azure managed hello Marketplace 中的應用程式](managed-application-consume-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="03826-183">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="03826-184">如何 toocreate UI 定義檔案為受管理的應用程式，請參閱的 toolearn[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="03826-184">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
