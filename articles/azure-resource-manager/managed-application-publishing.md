---
title: "建立及發佈 Azure 受服務類別目錄管理的應用程式 | Microsoft Docs"
description: "示範如何建立 Azure 受管理的應用程式，以供組織成員使用。"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 39b74984ec2f89ed39753963de7fe3ff79577c9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="0756d-103">發佈受管理的應用程式，以供內部使用</span><span class="sxs-lookup"><span data-stu-id="0756d-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="0756d-104">您可以建立及發佈 Azure [受管理的應用程式](managed-application-overview.md)，以供組織成員使用。</span><span class="sxs-lookup"><span data-stu-id="0756d-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="0756d-105">例如，IT 部門可以發佈受管理的應用程式，以確保符合組織標準。</span><span class="sxs-lookup"><span data-stu-id="0756d-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="0756d-106">這些受管理的應用程式可透過服務類別目錄 (而不是 Azure Marketplace) 取得。</span><span class="sxs-lookup"><span data-stu-id="0756d-106">These managed applications are available through the service catalog, not the Azure Marketplace.</span></span>

<span data-ttu-id="0756d-107">若要發佈受服務類別目錄管理的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="0756d-107">To publish a managed application for the service catalog, you must:</span></span>

* <span data-ttu-id="0756d-108">建立包含三個必要範本檔案的 .zip 套件。</span><span class="sxs-lookup"><span data-stu-id="0756d-108">Create a .zip package that contains the three required template files.</span></span>
* <span data-ttu-id="0756d-109">決定需要存取使用者訂用帳戶中的資源群組之使用者、群組或應用程式。</span><span class="sxs-lookup"><span data-stu-id="0756d-109">Decide which user, group, or application needs access to the resource group in the user's subscription.</span></span>
* <span data-ttu-id="0756d-110">建立指向 .zip 套件並要求存取身分識別的受管理應用程式定義。</span><span class="sxs-lookup"><span data-stu-id="0756d-110">Create the managed application definition that points to the .zip package and requests access for the identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="0756d-111">建立受管理的應用程式套件</span><span class="sxs-lookup"><span data-stu-id="0756d-111">Create a managed application package</span></span>

<span data-ttu-id="0756d-112">第一個步驟是建立三個必要的範本檔案。</span><span class="sxs-lookup"><span data-stu-id="0756d-112">The first step is to create the three required template files.</span></span> <span data-ttu-id="0756d-113">將這三個檔案封裝為 .zip 檔案，並將它上傳至可存取的位置，例如儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0756d-113">Package all three files into a .zip file, and upload it to an accessible location, such as a storage account.</span></span> <span data-ttu-id="0756d-114">建立受管理的應用程式定義時，您會傳遞此 .zip 檔案的連結。</span><span class="sxs-lookup"><span data-stu-id="0756d-114">You pass a link to this .zip file when creating the managed application definition.</span></span>

* <span data-ttu-id="0756d-115">**applianceMainTemplate.json**：此檔案會將佈建作為受管理應用程式一部分的 Azure 資源進行定義。</span><span class="sxs-lookup"><span data-stu-id="0756d-115">**applianceMainTemplate.json**: This file defines the Azure resources that are provisioned as part of the managed application.</span></span> <span data-ttu-id="0756d-116">此範本與一般 Resource Manager 範本不同。</span><span class="sxs-lookup"><span data-stu-id="0756d-116">The template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="0756d-117">例如，若要透過受管理的應用程式來建立儲存體帳戶，applianceMainTemplate.json 會包含：</span><span class="sxs-lookup"><span data-stu-id="0756d-117">For example, to create a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

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

* <span data-ttu-id="0756d-118">**mainTemplate.json**：建立受管理的應用程式時，使用者會部署此範本。</span><span class="sxs-lookup"><span data-stu-id="0756d-118">**mainTemplate.json**: Users deploy this template when creating the managed application.</span></span> <span data-ttu-id="0756d-119">它會定義受管理的應用程式資源，也就是 Microsoft.Solutions/appliances 資源類型。</span><span class="sxs-lookup"><span data-stu-id="0756d-119">It defines the managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="0756d-120">此檔案包含 applianceMainTemplate.json 中的資源所需之所有參數。</span><span class="sxs-lookup"><span data-stu-id="0756d-120">This file contains all the parameters you need for the resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="0756d-121">您會在此範本中設定兩個重要的屬性。</span><span class="sxs-lookup"><span data-stu-id="0756d-121">You set two important properties in this template.</span></span> <span data-ttu-id="0756d-122">第一個屬性是 **applianceDefinitionId**，該屬性是受管理應用程式定義的識別碼。</span><span class="sxs-lookup"><span data-stu-id="0756d-122">First, the **applianceDefinitionId** property is the ID of the managed application definition.</span></span> <span data-ttu-id="0756d-123">您將在本主題稍後建立定義。</span><span class="sxs-lookup"><span data-stu-id="0756d-123">You create the definition later in this topic.</span></span> <span data-ttu-id="0756d-124">設定此值時，您必須決定要用於儲存受管理應用程式定義的訂用帳戶和資源群組。</span><span class="sxs-lookup"><span data-stu-id="0756d-124">When setting this value, you must decide which subscription and resource group to use for storing the managed application definitions.</span></span> <span data-ttu-id="0756d-125">此外，您必須決定定義的名稱。</span><span class="sxs-lookup"><span data-stu-id="0756d-125">And, you must decide on a name for the definition.</span></span> <span data-ttu-id="0756d-126">識別碼的格式為：</span><span class="sxs-lookup"><span data-stu-id="0756d-126">The ID is in the format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="0756d-127">第二個屬性是 **managedResourceGroupId**，該屬性是資源群組的識別碼，其中會建立 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="0756d-127">Second, the **managedResourceGroupId** property is the ID of the resource group where the Azure resources are created.</span></span> <span data-ttu-id="0756d-128">您可以指派值給這個資源群組名稱，或讓使用者提供名稱。</span><span class="sxs-lookup"><span data-stu-id="0756d-128">You can assign a value for this resource group name or let the user provide a name.</span></span> <span data-ttu-id="0756d-129">識別碼的格式為：</span><span class="sxs-lookup"><span data-stu-id="0756d-129">The format of the ID is:</span></span>

  <span data-ttu-id="0756d-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`。</span><span class="sxs-lookup"><span data-stu-id="0756d-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="0756d-131">下列範例顯示 mainTemplate.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="0756d-131">The following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="0756d-132">它會為已部署的資源指定資源群組。</span><span class="sxs-lookup"><span data-stu-id="0756d-132">It specifies a resource group for the deployed resources.</span></span> <span data-ttu-id="0756d-133">定義識別碼是設定為使用名為 **managedApplicationGroup** 的資源群組中名為 **storageApp** 的定義。</span><span class="sxs-lookup"><span data-stu-id="0756d-133">The definition ID is set to use a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="0756d-134">您可以變更這些值來使用不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="0756d-134">You can change these values to use different names.</span></span> <span data-ttu-id="0756d-135">在定義識別碼中提供您自己的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="0756d-135">Provide your own subscription ID in the definition ID.</span></span>

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

* <span data-ttu-id="0756d-136">**applianceCreateUiDefinition.json**：Azure 入口網站會使用這個檔案，為建立受管理應用程式的使用者產生使用者介面。</span><span class="sxs-lookup"><span data-stu-id="0756d-136">**applianceCreateUiDefinition.json**: The Azure portal uses this file to generate the user interface for users who create the managed application.</span></span> <span data-ttu-id="0756d-137">您可以定義使用者提供每個參數輸入的方式。</span><span class="sxs-lookup"><span data-stu-id="0756d-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="0756d-138">您可以使用諸如下拉式清單、文字方塊、密碼方塊和其他輸入工具等選項。</span><span class="sxs-lookup"><span data-stu-id="0756d-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="0756d-139">若要了解如何建立受管理應用程式的 UI 定義檔案，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0756d-139">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="0756d-140">下列範例顯示 applianceCreateUiDefinition.json 檔案，可讓使用者透過文字方塊指定儲存體帳戶名稱前置詞。</span><span class="sxs-lookup"><span data-stu-id="0756d-140">The following example shows an applianceCreateUiDefinition.json file that enables users to specify the storage account name prefix through a textbox.</span></span>

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
                "toolTip": "Provide a value that is used for the prefix of your storage account. Limit to 11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-11 characters long."
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

<span data-ttu-id="0756d-141">所有必要檔案準備就緒後，請將這些檔案封裝為 .zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="0756d-141">After all the needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="0756d-142">這三個檔案必須位於 .zip 檔案的根層級。</span><span class="sxs-lookup"><span data-stu-id="0756d-142">The three files must be at the root level of the .zip file.</span></span> <span data-ttu-id="0756d-143">如果您將這些檔案放在資料夾中，當建立受管理的應用程式時，您會收到錯誤，指出必要的檔案不存在。</span><span class="sxs-lookup"><span data-stu-id="0756d-143">If you put them in a folder, you receive an error when creating the managed application definition that states the required files are not present.</span></span> <span data-ttu-id="0756d-144">將套件上傳至可從中取用它的可存取位置。</span><span class="sxs-lookup"><span data-stu-id="0756d-144">Upload the package to an accessible location from where it can be consumed.</span></span> <span data-ttu-id="0756d-145">本文其餘部分假設 .zip 檔案存在於可公開存取的儲存體 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="0756d-145">The remainder of this article assumes the .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="0756d-146">建立 Azure Active Directory 使用者群組或應用程式</span><span class="sxs-lookup"><span data-stu-id="0756d-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="0756d-147">第二個步驟是選取要代表客戶管理資源的使用者群組或應用程式。</span><span class="sxs-lookup"><span data-stu-id="0756d-147">The second step is to select a user group or application for managing the resources on behalf of the customer.</span></span> <span data-ttu-id="0756d-148">此使用者群組或應用程式會根據指派的角色，取得受管理資源群組的權限。</span><span class="sxs-lookup"><span data-stu-id="0756d-148">This user group or application has permissions on the managed resource group according to the role that is assigned.</span></span> <span data-ttu-id="0756d-149">角色可以是任何內建的角色型存取控制 (RBAC) 角色，例如擁有者或參與者。</span><span class="sxs-lookup"><span data-stu-id="0756d-149">The role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="0756d-150">您也可以將管理資源的權限提供給個別使用者，但您通常要將此權限指派給使用者群組。</span><span class="sxs-lookup"><span data-stu-id="0756d-150">You also can give an individual user permission to manage the resources, but typically you assign this permission to a user group.</span></span> <span data-ttu-id="0756d-151">若要建立新的 Active Directory 使用者群組，請參閱[在 Azure Active Directory 中建立群組和新增成員](../active-directory/active-directory-groups-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="0756d-151">To create a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="0756d-152">您需要使用者群組的物件識別碼，以便用於管理資源。</span><span class="sxs-lookup"><span data-stu-id="0756d-152">You need the object ID of the user group to use for managing the resources.</span></span> <span data-ttu-id="0756d-153">下列範例會示範如何從群組的顯示名稱取得物件識別碼：</span><span class="sxs-lookup"><span data-stu-id="0756d-153">The following example shows how to get the object ID from the group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="0756d-154">範例命令會傳回下列輸出︰</span><span class="sxs-lookup"><span data-stu-id="0756d-154">The example command returns the following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="0756d-155">若只要擷取物件識別碼，請使用：</span><span class="sxs-lookup"><span data-stu-id="0756d-155">To retrieve just the object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-the-role-definition-id"></a><span data-ttu-id="0756d-156">取得角色定義識別碼</span><span class="sxs-lookup"><span data-stu-id="0756d-156">Get the role definition ID</span></span>

<span data-ttu-id="0756d-157">接下來，您需要的角色定義識別碼，是您想要授與使用者、使用者群組或應用程式存取權的 RBAC 內建角色。</span><span class="sxs-lookup"><span data-stu-id="0756d-157">Next, you need the role definition ID of the RBAC built-in role you want to grant access to the user, user group, or application.</span></span> <span data-ttu-id="0756d-158">您通常會使用「擁有者」或「參與者」或「讀取者」角色。</span><span class="sxs-lookup"><span data-stu-id="0756d-158">Typically, you use the Owner or Contributor or Reader role.</span></span> <span data-ttu-id="0756d-159">下列命令會顯示如何取得「擁有者」角色的角色定義識別碼：</span><span class="sxs-lookup"><span data-stu-id="0756d-159">The following command shows how to get the role definition ID for the Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="0756d-160">該命令會傳回下列輸出︰</span><span class="sxs-lookup"><span data-stu-id="0756d-160">That command returns the following output:</span></span>

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access to resources.",
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

<span data-ttu-id="0756d-161">您需要上述範例中的 "name" 屬性值。</span><span class="sxs-lookup"><span data-stu-id="0756d-161">You need the value of the "name" property from the preceding example.</span></span> <span data-ttu-id="0756d-162">您可以透過下列程式碼只擷取該屬性：</span><span class="sxs-lookup"><span data-stu-id="0756d-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-the-managed-application-definition"></a><span data-ttu-id="0756d-163">建立受管理的應用程式定義</span><span class="sxs-lookup"><span data-stu-id="0756d-163">Create the managed application definition</span></span>

<span data-ttu-id="0756d-164">如果您尚未有可儲存受管理應用程式定義的資源群組，請立即建立一個：</span><span class="sxs-lookup"><span data-stu-id="0756d-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="0756d-165">現在，建立受管理的應用程式定義資源。</span><span class="sxs-lookup"><span data-stu-id="0756d-165">Now, create the managed application definition resource.</span></span>

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

<span data-ttu-id="0756d-166">上述範例中使用的參數：</span><span class="sxs-lookup"><span data-stu-id="0756d-166">The parameters used in the preceding example are:</span></span>

* <span data-ttu-id="0756d-167">**resource-group**：資源群組的名稱，其中會建立受管理的應用程式定義。</span><span class="sxs-lookup"><span data-stu-id="0756d-167">**resource-group**: The name of the resource group where the managed application definition is created.</span></span>
* <span data-ttu-id="0756d-168">**lock-level**：放在受管理資源群組的鎖定類型。</span><span class="sxs-lookup"><span data-stu-id="0756d-168">**lock-level**: The type of lock placed on the managed resource group.</span></span> <span data-ttu-id="0756d-169">它可以避免客戶在此資源群組上執行非預期的作業。</span><span class="sxs-lookup"><span data-stu-id="0756d-169">It prevents the customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="0756d-170">目前唯一支援的鎖定等級是 ReadOnly。</span><span class="sxs-lookup"><span data-stu-id="0756d-170">Currently, ReadOnly is the only supported lock level.</span></span> <span data-ttu-id="0756d-171">指定 ReadOnly 時，客戶只能讀取受管理資源群組中存在的資源。</span><span class="sxs-lookup"><span data-stu-id="0756d-171">When ReadOnly is specified, the customer can only read the resources present in the managed resource group.</span></span>
* <span data-ttu-id="0756d-172">**authorizations**：描述用來授與權限給受管理資源群組的主體識別碼及角色定義識別碼。</span><span class="sxs-lookup"><span data-stu-id="0756d-172">**authorizations**: Describes the principal ID and the role definition ID that are used to grant permission to the managed resource group.</span></span> <span data-ttu-id="0756d-173">它是以 `<principalId>:<roleDefinitionId>` 格式來指定。</span><span class="sxs-lookup"><span data-stu-id="0756d-173">It's specified in the format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="0756d-174">這個屬性也可以指定多個值。</span><span class="sxs-lookup"><span data-stu-id="0756d-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="0756d-175">如果需要多個值，應該以 `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>` 格式來指定。</span><span class="sxs-lookup"><span data-stu-id="0756d-175">If multiple values are needed, they should be specified in the form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="0756d-176">多個值之間以空格分隔。</span><span class="sxs-lookup"><span data-stu-id="0756d-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="0756d-177">**package-file-uri**：包含範本檔案之受管理應用程式套件的位置，它可以是 Azure 儲存體 Blob。</span><span class="sxs-lookup"><span data-stu-id="0756d-177">**package-file-uri**: The location of the managed application package that contains the template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0756d-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0756d-178">Next steps</span></span>

* <span data-ttu-id="0756d-179">如需受管理應用程式的簡介，請參閱[受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0756d-179">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="0756d-180">如需檔案的範例，請參閱[受管理的應用程式範例](https://github.com/Azure/azure-managedapp-samples/tree/master/samples)。</span><span class="sxs-lookup"><span data-stu-id="0756d-180">For examples of the files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="0756d-181">如需使用 Service Catalog 受管理應用程式的詳細資訊，請參閱[使用 Service Catalog 受管理的應用程式](managed-application-consumption.md)。</span><span class="sxs-lookup"><span data-stu-id="0756d-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="0756d-182">如需將受管理的應用程式發佈到 Azure Marketplace 的資訊，請參閱 [Marketplace 中的 Azure 受管理應用程式](managed-application-author-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="0756d-182">For information about publishing managed applications to the Azure Marketplace, see [Azure managed applications in the Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="0756d-183">如需從 Marketplace 使用受管理應用程式的詳細資訊，請參閱[在 Marketplace 中使用 Azure 受管理的應用程式](managed-application-consume-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="0756d-183">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="0756d-184">若要了解如何建立受管理應用程式的 UI 定義檔案，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0756d-184">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
