---
title: "角色型存取控制與 REST | Microsoft Docs"
description: "使用 REST API 管理角色型存取控制"
services: active-directory
documentationcenter: na
author: andredm7
manager: femila
editor: 
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: andredm
ms.openlocfilehash: a5c19fd87ce1ae3e199bf1dfc8cf82f5653baac2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-rest-api"></a><span data-ttu-id="859ae-103">使用 REST API 管理角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="859ae-103">Manage Role-Based Access Control with the REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="859ae-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="859ae-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="859ae-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="859ae-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="859ae-106">REST API</span><span class="sxs-lookup"><span data-stu-id="859ae-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="859ae-107">Azure 入口網站及 Azure Resource Manager API 中的「角色型存取控制」(RBAC) 可協助您精確管理對您訂用帳戶與資源的存取。</span><span class="sxs-lookup"><span data-stu-id="859ae-107">Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API helps you manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="859ae-108">透過這項功能，您可以為 Active Directory 使用者、群組或是服務主體指派特定範圍的一些角色，藉此賦予其存取權限。</span><span class="sxs-lookup"><span data-stu-id="859ae-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="859ae-109">列出所有角色指派</span><span class="sxs-lookup"><span data-stu-id="859ae-109">List all role assignments</span></span>
<span data-ttu-id="859ae-110">列出在指定的範圍和子範圍內的所有角色指派。</span><span class="sxs-lookup"><span data-stu-id="859ae-110">Lists all the role assignments at the specified scope and subscopes.</span></span>

<span data-ttu-id="859ae-111">若要列出角色指派，您必須具有範圍內的 `Microsoft.Authorization/roleAssignments/read` 作業存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-111">To list role assignments, you must have access to `Microsoft.Authorization/roleAssignments/read` operation at the scope.</span></span> <span data-ttu-id="859ae-112">所有內建角色都會獲得這項作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-112">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="859ae-113">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="859ae-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="859ae-114">要求</span><span class="sxs-lookup"><span data-stu-id="859ae-114">Request</span></span>
<span data-ttu-id="859ae-115">搭配下列 URI 使用 **GET** 方法：</span><span class="sxs-lookup"><span data-stu-id="859ae-115">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="859ae-116">在 URI 內進行下列替代動作以自訂要求：</span><span class="sxs-lookup"><span data-stu-id="859ae-116">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="859ae-117">將 *{scope}* 取代為您要列出角色指派的範圍。</span><span class="sxs-lookup"><span data-stu-id="859ae-117">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="859ae-118">下列範例顯示如何指定不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="859ae-118">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="859ae-119">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="859ae-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="859ae-120">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="859ae-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="859ae-121">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="859ae-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="859ae-122">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="859ae-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="859ae-123">將 *{filter}* 取代為要針對角色指派清單篩選套用的條件：</span><span class="sxs-lookup"><span data-stu-id="859ae-123">Replace *{filter}* with the condition that you wish to apply to filter the role assignment list:</span></span>

   * <span data-ttu-id="859ae-124">僅列出指定範圍的角色指派，不包括子範圍內的角色指派： `atScope()`</span><span class="sxs-lookup"><span data-stu-id="859ae-124">List role assignments for only the specified scope, not including the role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="859ae-125">僅列出特定使用者、群組或應用程式的角色指派： `principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="859ae-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="859ae-126">僅列出特定使用者的角色指派，包括從群組繼承的角色指派 | `assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="859ae-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="859ae-127">Response</span><span class="sxs-lookup"><span data-stu-id="859ae-127">Response</span></span>
<span data-ttu-id="859ae-128">狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="859ae-128">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="859ae-129">取得角色指派的相關資訊</span><span class="sxs-lookup"><span data-stu-id="859ae-129">Get information about a role assignment</span></span>
<span data-ttu-id="859ae-130">取得由角色指派識別碼所指定的單一角色指派相關資訊。</span><span class="sxs-lookup"><span data-stu-id="859ae-130">Gets information about a single role assignment specified by the role assignment identifier.</span></span>

<span data-ttu-id="859ae-131">若要取得角色指派的相關資訊，您必須具有 `Microsoft.Authorization/roleAssignments/read` 作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-131">To get information about a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="859ae-132">所有內建角色都會獲得這項作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-132">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="859ae-133">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="859ae-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="859ae-134">要求</span><span class="sxs-lookup"><span data-stu-id="859ae-134">Request</span></span>
<span data-ttu-id="859ae-135">搭配下列 URI 使用 **GET** 方法：</span><span class="sxs-lookup"><span data-stu-id="859ae-135">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="859ae-136">在 URI 內進行下列替代動作以自訂要求：</span><span class="sxs-lookup"><span data-stu-id="859ae-136">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="859ae-137">將 *{scope}* 取代為您要列出角色指派的範圍。</span><span class="sxs-lookup"><span data-stu-id="859ae-137">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="859ae-138">下列範例顯示如何指定不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="859ae-138">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="859ae-139">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="859ae-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="859ae-140">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="859ae-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="859ae-141">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="859ae-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="859ae-142">將 *{role-assignment-id}* 取代為角色指派的 GUID 識別碼。</span><span class="sxs-lookup"><span data-stu-id="859ae-142">Replace *{role-assignment-id}* with the GUID identifier of the role assignment.</span></span>
3. <span data-ttu-id="859ae-143">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="859ae-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="859ae-144">Response</span><span class="sxs-lookup"><span data-stu-id="859ae-144">Response</span></span>
<span data-ttu-id="859ae-145">狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="859ae-145">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a><span data-ttu-id="859ae-146">建立角色指派</span><span class="sxs-lookup"><span data-stu-id="859ae-146">Create a Role Assignment</span></span>
<span data-ttu-id="859ae-147">在指定範圍中建立指定主體授與指定角色的角色指派。</span><span class="sxs-lookup"><span data-stu-id="859ae-147">Create a role assignment at the specified scope for the specified principal granting the specified role.</span></span>

<span data-ttu-id="859ae-148">若要建立角色指派，您必須具有 `Microsoft.Authorization/roleAssignments/write` 作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-148">To create a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="859ae-149">在內建角色中，只有「擁有者」和「使用者存取系統管理員」會獲得這項作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-149">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="859ae-150">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="859ae-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="859ae-151">要求</span><span class="sxs-lookup"><span data-stu-id="859ae-151">Request</span></span>
<span data-ttu-id="859ae-152">搭配下列 URI 使用 **PUT** 方法：</span><span class="sxs-lookup"><span data-stu-id="859ae-152">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="859ae-153">在 URI 內進行下列替代動作以自訂要求：</span><span class="sxs-lookup"><span data-stu-id="859ae-153">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="859ae-154">將 *{scope}* 取代為您要建立角色指派的範圍。</span><span class="sxs-lookup"><span data-stu-id="859ae-154">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="859ae-155">當您在父範圍內建立角色指派時，所有的子範圍會繼承相同的角色指派。</span><span class="sxs-lookup"><span data-stu-id="859ae-155">When you create a role assignment at a parent scope, all child scopes inherit the same role assignment.</span></span> <span data-ttu-id="859ae-156">下列範例顯示如何指定不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="859ae-156">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="859ae-157">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="859ae-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="859ae-158">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="859ae-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="859ae-159">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="859ae-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="859ae-160">將 *{role-assignment-id}* 取代為新的 GUID，此 GUID 將成為新角色指派的 GUID 識別碼。</span><span class="sxs-lookup"><span data-stu-id="859ae-160">Replace *{role-assignment-id}* with a new GUID, which becomes the GUID identifier of the new role assignment.</span></span>
3. <span data-ttu-id="859ae-161">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="859ae-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="859ae-162">對於要求本文，提供下列格式的值：</span><span class="sxs-lookup"><span data-stu-id="859ae-162">For the request body, provide the values in the following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="859ae-163">元素名稱</span><span class="sxs-lookup"><span data-stu-id="859ae-163">Element Name</span></span> | <span data-ttu-id="859ae-164">必要</span><span class="sxs-lookup"><span data-stu-id="859ae-164">Required</span></span> | <span data-ttu-id="859ae-165">類型</span><span class="sxs-lookup"><span data-stu-id="859ae-165">Type</span></span> | <span data-ttu-id="859ae-166">說明</span><span class="sxs-lookup"><span data-stu-id="859ae-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="859ae-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="859ae-167">roleDefinitionId</span></span> |<span data-ttu-id="859ae-168">是</span><span class="sxs-lookup"><span data-stu-id="859ae-168">Yes</span></span> |<span data-ttu-id="859ae-169">String</span><span class="sxs-lookup"><span data-stu-id="859ae-169">String</span></span> |<span data-ttu-id="859ae-170">角色的識別碼。</span><span class="sxs-lookup"><span data-stu-id="859ae-170">The identifier of the role.</span></span> <span data-ttu-id="859ae-171">此識別碼的格式是： `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="859ae-171">The format of the identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="859ae-172">principalId</span><span class="sxs-lookup"><span data-stu-id="859ae-172">principalId</span></span> |<span data-ttu-id="859ae-173">是</span><span class="sxs-lookup"><span data-stu-id="859ae-173">Yes</span></span> |<span data-ttu-id="859ae-174">String</span><span class="sxs-lookup"><span data-stu-id="859ae-174">String</span></span> |<span data-ttu-id="859ae-175">做為角色指派對象之 Azure AD 主體的 objectId (使用者、群組或服務主體)。</span><span class="sxs-lookup"><span data-stu-id="859ae-175">objectId of the Azure AD principal (user, group, or service principal) to which the role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="859ae-176">Response</span><span class="sxs-lookup"><span data-stu-id="859ae-176">Response</span></span>
<span data-ttu-id="859ae-177">狀態碼：201</span><span class="sxs-lookup"><span data-stu-id="859ae-177">Status code: 201</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a><span data-ttu-id="859ae-178">刪除角色指派</span><span class="sxs-lookup"><span data-stu-id="859ae-178">Delete a Role Assignment</span></span>
<span data-ttu-id="859ae-179">刪除指定範圍內的角色指派。</span><span class="sxs-lookup"><span data-stu-id="859ae-179">Delete a role assignment at the specified scope.</span></span>

<span data-ttu-id="859ae-180">若要刪除角色指派，您必須具有 `Microsoft.Authorization/roleAssignments/delete` 作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-180">To delete a role assignment, you must have access to the `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="859ae-181">在內建角色中，只有「擁有者」和「使用者存取系統管理員」會獲得這項作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-181">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="859ae-182">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="859ae-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="859ae-183">要求</span><span class="sxs-lookup"><span data-stu-id="859ae-183">Request</span></span>
<span data-ttu-id="859ae-184">搭配下列 URI 使用 **DELETE** 方法：</span><span class="sxs-lookup"><span data-stu-id="859ae-184">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="859ae-185">在 URI 內進行下列替代動作以自訂要求：</span><span class="sxs-lookup"><span data-stu-id="859ae-185">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="859ae-186">將 *{scope}* 取代為您要建立角色指派的範圍。</span><span class="sxs-lookup"><span data-stu-id="859ae-186">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="859ae-187">下列範例顯示如何指定不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="859ae-187">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="859ae-188">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="859ae-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="859ae-189">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="859ae-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="859ae-190">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="859ae-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="859ae-191">將 *{role-assignment-id}* 取代為角色指派識別碼 GUID。</span><span class="sxs-lookup"><span data-stu-id="859ae-191">Replace *{role-assignment-id}* with the role assignment id GUID.</span></span>
3. <span data-ttu-id="859ae-192">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="859ae-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="859ae-193">Response</span><span class="sxs-lookup"><span data-stu-id="859ae-193">Response</span></span>
<span data-ttu-id="859ae-194">狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="859ae-194">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a><span data-ttu-id="859ae-195">列出所有角色</span><span class="sxs-lookup"><span data-stu-id="859ae-195">List all Roles</span></span>
<span data-ttu-id="859ae-196">列出在指定的範圍內可供指派的所有角色。</span><span class="sxs-lookup"><span data-stu-id="859ae-196">Lists all the roles that are available for assignment at the specified scope.</span></span>

<span data-ttu-id="859ae-197">若要列出角色，您必須具有該範圍內 `Microsoft.Authorization/roleDefinitions/read` 作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-197">To list roles, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation at the scope.</span></span> <span data-ttu-id="859ae-198">所有內建角色都會獲得這項作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-198">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="859ae-199">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="859ae-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="859ae-200">要求</span><span class="sxs-lookup"><span data-stu-id="859ae-200">Request</span></span>
<span data-ttu-id="859ae-201">搭配下列 URI 使用 **GET** 方法：</span><span class="sxs-lookup"><span data-stu-id="859ae-201">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="859ae-202">在 URI 內進行下列替代動作以自訂要求：</span><span class="sxs-lookup"><span data-stu-id="859ae-202">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="859ae-203">將 *{scope}* 取代為您要列出角色的範圍。</span><span class="sxs-lookup"><span data-stu-id="859ae-203">Replace *{scope}* with the scope for which you wish to list the roles.</span></span> <span data-ttu-id="859ae-204">下列範例顯示如何指定不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="859ae-204">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="859ae-205">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="859ae-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="859ae-206">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="859ae-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="859ae-207">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="859ae-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="859ae-208">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="859ae-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="859ae-209">將 *{filter}* 取代為要針對角色清單篩選套用的條件：</span><span class="sxs-lookup"><span data-stu-id="859ae-209">Replace *{filter}* with the condition that you wish to apply to filter the list of roles:</span></span>

   * <span data-ttu-id="859ae-210">列出在指定的範圍及其任何子範圍內可供指派的角色： `atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="859ae-210">List roles available for assignment at the specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="859ae-211">使用確切的顯示名稱來搜尋角色： `roleName%20eq%20'{role-display-name}'`。</span><span class="sxs-lookup"><span data-stu-id="859ae-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="859ae-212">使用角色確切顯示名稱的 URL 編碼型式。</span><span class="sxs-lookup"><span data-stu-id="859ae-212">Use the URL encoded form of the exact display name of the role.</span></span> <span data-ttu-id="859ae-213">例如， `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="859ae-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="859ae-214">Response</span><span class="sxs-lookup"><span data-stu-id="859ae-214">Response</span></span>
<span data-ttu-id="859ae-215">狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="859ae-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a><span data-ttu-id="859ae-216">取得角色的相關資訊</span><span class="sxs-lookup"><span data-stu-id="859ae-216">Get information about a Role</span></span>
<span data-ttu-id="859ae-217">取得由角色定義識別碼所指定的單一角色相關資訊。</span><span class="sxs-lookup"><span data-stu-id="859ae-217">Gets information about a single role specified by the role definition identifier.</span></span> <span data-ttu-id="859ae-218">若要使用角色的顯示名稱來取得單一角色的相關資訊，請參閱 [列出所有角色](role-based-access-control-manage-access-rest.md#list-all-roles)。</span><span class="sxs-lookup"><span data-stu-id="859ae-218">To get information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="859ae-219">若要取得角色的相關資訊，您必須具有 `Microsoft.Authorization/roleDefinitions/read` 作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-219">To get information about a role, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="859ae-220">所有內建角色都會獲得這項作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-220">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="859ae-221">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="859ae-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="859ae-222">要求</span><span class="sxs-lookup"><span data-stu-id="859ae-222">Request</span></span>
<span data-ttu-id="859ae-223">搭配下列 URI 使用 **GET** 方法：</span><span class="sxs-lookup"><span data-stu-id="859ae-223">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="859ae-224">在 URI 內進行下列替代動作以自訂要求：</span><span class="sxs-lookup"><span data-stu-id="859ae-224">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="859ae-225">將 *{scope}* 取代為您要列出角色指派的範圍。</span><span class="sxs-lookup"><span data-stu-id="859ae-225">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="859ae-226">下列範例顯示如何指定不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="859ae-226">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="859ae-227">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="859ae-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="859ae-228">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="859ae-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="859ae-229">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="859ae-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="859ae-230">將 *{role-definition-id}* 取代為角色定義的 GUID 識別碼。</span><span class="sxs-lookup"><span data-stu-id="859ae-230">Replace *{role-definition-id}* with the GUID identifier of the role definition.</span></span>
3. <span data-ttu-id="859ae-231">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="859ae-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="859ae-232">Response</span><span class="sxs-lookup"><span data-stu-id="859ae-232">Response</span></span>
<span data-ttu-id="859ae-233">狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="859ae-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a><span data-ttu-id="859ae-234">建立自訂角色</span><span class="sxs-lookup"><span data-stu-id="859ae-234">Create a Custom Role</span></span>
<span data-ttu-id="859ae-235">建立自訂角色。</span><span class="sxs-lookup"><span data-stu-id="859ae-235">Create a custom role.</span></span>

<span data-ttu-id="859ae-236">若要建立自訂角色，您必須在所有 `AssignableScopes` 上都具有 `Microsoft.Authorization/roleDefinitions/write` 作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-236">To create a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="859ae-237">在內建角色中，只有「擁有者」和「使用者存取系統管理員」會獲得這項作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-237">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="859ae-238">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="859ae-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="859ae-239">要求</span><span class="sxs-lookup"><span data-stu-id="859ae-239">Request</span></span>
<span data-ttu-id="859ae-240">搭配下列 URI 使用 **PUT** 方法：</span><span class="sxs-lookup"><span data-stu-id="859ae-240">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="859ae-241">在 URI 內進行下列替代動作以自訂要求：</span><span class="sxs-lookup"><span data-stu-id="859ae-241">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="859ae-242">將 *{scope}* 取代為自訂角色的第一個 *AssignableScope*。</span><span class="sxs-lookup"><span data-stu-id="859ae-242">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="859ae-243">下列範例顯示如何指定不同層級的範圍。</span><span class="sxs-lookup"><span data-stu-id="859ae-243">The following examples show how to specify the scope for different levels.</span></span>

   * <span data-ttu-id="859ae-244">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="859ae-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="859ae-245">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="859ae-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="859ae-246">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="859ae-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="859ae-247">將 *{role-definition-id}* 取代為新的 GUID，此 GUID 將成為新自訂角色的 GUID 識別碼。</span><span class="sxs-lookup"><span data-stu-id="859ae-247">Replace *{role-definition-id}* with a new GUID, which becomes the GUID identifier of the new custom role.</span></span>
3. <span data-ttu-id="859ae-248">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="859ae-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="859ae-249">對於要求本文，提供下列格式的值：</span><span class="sxs-lookup"><span data-stu-id="859ae-249">For the request body, provide the values in the following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="859ae-250">元素名稱</span><span class="sxs-lookup"><span data-stu-id="859ae-250">Element Name</span></span> | <span data-ttu-id="859ae-251">必要</span><span class="sxs-lookup"><span data-stu-id="859ae-251">Required</span></span> | <span data-ttu-id="859ae-252">類型</span><span class="sxs-lookup"><span data-stu-id="859ae-252">Type</span></span> | <span data-ttu-id="859ae-253">說明</span><span class="sxs-lookup"><span data-stu-id="859ae-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="859ae-254">名稱</span><span class="sxs-lookup"><span data-stu-id="859ae-254">name</span></span> |<span data-ttu-id="859ae-255">是</span><span class="sxs-lookup"><span data-stu-id="859ae-255">Yes</span></span> |<span data-ttu-id="859ae-256">String</span><span class="sxs-lookup"><span data-stu-id="859ae-256">String</span></span> |<span data-ttu-id="859ae-257">自訂角色的 GUID 識別碼。</span><span class="sxs-lookup"><span data-stu-id="859ae-257">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="859ae-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="859ae-258">properties.roleName</span></span> |<span data-ttu-id="859ae-259">是</span><span class="sxs-lookup"><span data-stu-id="859ae-259">Yes</span></span> |<span data-ttu-id="859ae-260">String</span><span class="sxs-lookup"><span data-stu-id="859ae-260">String</span></span> |<span data-ttu-id="859ae-261">自訂角色的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="859ae-261">Display name of the custom role.</span></span> <span data-ttu-id="859ae-262">大小上限為 128 個字元。</span><span class="sxs-lookup"><span data-stu-id="859ae-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="859ae-263">properties.description</span><span class="sxs-lookup"><span data-stu-id="859ae-263">properties.description</span></span> |<span data-ttu-id="859ae-264">否</span><span class="sxs-lookup"><span data-stu-id="859ae-264">No</span></span> |<span data-ttu-id="859ae-265">String</span><span class="sxs-lookup"><span data-stu-id="859ae-265">String</span></span> |<span data-ttu-id="859ae-266">自訂角色的說明。</span><span class="sxs-lookup"><span data-stu-id="859ae-266">Description of the custom role.</span></span> <span data-ttu-id="859ae-267">大小上限為 1024 個字元。</span><span class="sxs-lookup"><span data-stu-id="859ae-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="859ae-268">properties.type</span><span class="sxs-lookup"><span data-stu-id="859ae-268">properties.type</span></span> |<span data-ttu-id="859ae-269">是</span><span class="sxs-lookup"><span data-stu-id="859ae-269">Yes</span></span> |<span data-ttu-id="859ae-270">String</span><span class="sxs-lookup"><span data-stu-id="859ae-270">String</span></span> |<span data-ttu-id="859ae-271">設定為 "CustomRole"。</span><span class="sxs-lookup"><span data-stu-id="859ae-271">Set to "CustomRole."</span></span> |
| <span data-ttu-id="859ae-272">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="859ae-272">properties.permissions.actions</span></span> |<span data-ttu-id="859ae-273">yes</span><span class="sxs-lookup"><span data-stu-id="859ae-273">Yes</span></span> |<span data-ttu-id="859ae-274">String[]</span><span class="sxs-lookup"><span data-stu-id="859ae-274">String[]</span></span> |<span data-ttu-id="859ae-275">動作字串陣列，此陣列指定自訂角色所授權的作業。</span><span class="sxs-lookup"><span data-stu-id="859ae-275">An array of action strings specifying the operations granted by the custom role.</span></span> |
| <span data-ttu-id="859ae-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="859ae-276">properties.permissions.notActions</span></span> |<span data-ttu-id="859ae-277">否</span><span class="sxs-lookup"><span data-stu-id="859ae-277">No</span></span> |<span data-ttu-id="859ae-278">String[]</span><span class="sxs-lookup"><span data-stu-id="859ae-278">String[]</span></span> |<span data-ttu-id="859ae-279">動作字串陣列，此陣列指定要從自訂角色所授權的作業中排除的作業。</span><span class="sxs-lookup"><span data-stu-id="859ae-279">An array of action strings specifying the operations to exclude from the operations granted by the custom role.</span></span> |
| <span data-ttu-id="859ae-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="859ae-280">properties.assignableScopes</span></span> |<span data-ttu-id="859ae-281">是</span><span class="sxs-lookup"><span data-stu-id="859ae-281">Yes</span></span> |<span data-ttu-id="859ae-282">String[]</span><span class="sxs-lookup"><span data-stu-id="859ae-282">String[]</span></span> |<span data-ttu-id="859ae-283">範圍陣列，此陣列指定可在其中使用自訂角色的範圍。</span><span class="sxs-lookup"><span data-stu-id="859ae-283">An array of scopes in which the custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="859ae-284">Response</span><span class="sxs-lookup"><span data-stu-id="859ae-284">Response</span></span>
<span data-ttu-id="859ae-285">狀態碼：201</span><span class="sxs-lookup"><span data-stu-id="859ae-285">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a><span data-ttu-id="859ae-286">更新自訂角色</span><span class="sxs-lookup"><span data-stu-id="859ae-286">Update a Custom Role</span></span>
<span data-ttu-id="859ae-287">修改自訂角色。</span><span class="sxs-lookup"><span data-stu-id="859ae-287">Modify a custom role.</span></span>

<span data-ttu-id="859ae-288">若要修改自訂角色，您必須在所有 `AssignableScopes` 上都具有 `Microsoft.Authorization/roleDefinitions/write` 作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-288">To modify a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="859ae-289">在內建角色中，只有「擁有者」和「使用者存取系統管理員」會獲得這項作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-289">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="859ae-290">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="859ae-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="859ae-291">要求</span><span class="sxs-lookup"><span data-stu-id="859ae-291">Request</span></span>
<span data-ttu-id="859ae-292">搭配下列 URI 使用 **PUT** 方法：</span><span class="sxs-lookup"><span data-stu-id="859ae-292">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="859ae-293">在 URI 內進行下列替代動作以自訂要求：</span><span class="sxs-lookup"><span data-stu-id="859ae-293">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="859ae-294">將 *{scope}* 取代為自訂角色的第一個 *AssignableScope*。</span><span class="sxs-lookup"><span data-stu-id="859ae-294">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="859ae-295">下列範例顯示如何指定不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="859ae-295">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="859ae-296">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="859ae-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="859ae-297">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="859ae-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="859ae-298">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="859ae-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="859ae-299">將 *{role-definition-id}* 取代為自訂角色的 GUID 識別碼。</span><span class="sxs-lookup"><span data-stu-id="859ae-299">Replace *{role-definition-id}* with the GUID identifier of the custom role.</span></span>
3. <span data-ttu-id="859ae-300">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="859ae-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="859ae-301">對於要求本文，提供下列格式的值：</span><span class="sxs-lookup"><span data-stu-id="859ae-301">For the request body, provide the values in the following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="859ae-302">元素名稱</span><span class="sxs-lookup"><span data-stu-id="859ae-302">Element Name</span></span> | <span data-ttu-id="859ae-303">必要</span><span class="sxs-lookup"><span data-stu-id="859ae-303">Required</span></span> | <span data-ttu-id="859ae-304">類型</span><span class="sxs-lookup"><span data-stu-id="859ae-304">Type</span></span> | <span data-ttu-id="859ae-305">說明</span><span class="sxs-lookup"><span data-stu-id="859ae-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="859ae-306">名稱</span><span class="sxs-lookup"><span data-stu-id="859ae-306">name</span></span> |<span data-ttu-id="859ae-307">是</span><span class="sxs-lookup"><span data-stu-id="859ae-307">Yes</span></span> |<span data-ttu-id="859ae-308">String</span><span class="sxs-lookup"><span data-stu-id="859ae-308">String</span></span> |<span data-ttu-id="859ae-309">自訂角色的 GUID 識別碼。</span><span class="sxs-lookup"><span data-stu-id="859ae-309">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="859ae-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="859ae-310">properties.roleName</span></span> |<span data-ttu-id="859ae-311">是</span><span class="sxs-lookup"><span data-stu-id="859ae-311">Yes</span></span> |<span data-ttu-id="859ae-312">String</span><span class="sxs-lookup"><span data-stu-id="859ae-312">String</span></span> |<span data-ttu-id="859ae-313">已更新的自訂角色顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="859ae-313">Display name of the updated custom role.</span></span> |
| <span data-ttu-id="859ae-314">properties.description</span><span class="sxs-lookup"><span data-stu-id="859ae-314">properties.description</span></span> |<span data-ttu-id="859ae-315">否</span><span class="sxs-lookup"><span data-stu-id="859ae-315">No</span></span> |<span data-ttu-id="859ae-316">String</span><span class="sxs-lookup"><span data-stu-id="859ae-316">String</span></span> |<span data-ttu-id="859ae-317">已更新的自訂角色說明。</span><span class="sxs-lookup"><span data-stu-id="859ae-317">Description of the updated custom role.</span></span> |
| <span data-ttu-id="859ae-318">properties.type</span><span class="sxs-lookup"><span data-stu-id="859ae-318">properties.type</span></span> |<span data-ttu-id="859ae-319">是</span><span class="sxs-lookup"><span data-stu-id="859ae-319">Yes</span></span> |<span data-ttu-id="859ae-320">String</span><span class="sxs-lookup"><span data-stu-id="859ae-320">String</span></span> |<span data-ttu-id="859ae-321">設定為 "CustomRole"。</span><span class="sxs-lookup"><span data-stu-id="859ae-321">Set to "CustomRole."</span></span> |
| <span data-ttu-id="859ae-322">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="859ae-322">properties.permissions.actions</span></span> |<span data-ttu-id="859ae-323">yes</span><span class="sxs-lookup"><span data-stu-id="859ae-323">Yes</span></span> |<span data-ttu-id="859ae-324">String[]</span><span class="sxs-lookup"><span data-stu-id="859ae-324">String[]</span></span> |<span data-ttu-id="859ae-325">動作字串的陣列會指定已更新自訂角色授與存取權的作業。</span><span class="sxs-lookup"><span data-stu-id="859ae-325">An array of action strings specifying the operations to which the updated custom role grants access.</span></span> |
| <span data-ttu-id="859ae-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="859ae-326">properties.permissions.notActions</span></span> |<span data-ttu-id="859ae-327">否</span><span class="sxs-lookup"><span data-stu-id="859ae-327">No</span></span> |<span data-ttu-id="859ae-328">String[]</span><span class="sxs-lookup"><span data-stu-id="859ae-328">String[]</span></span> |<span data-ttu-id="859ae-329">動作字串陣列，此陣列指定要從已更新之自訂角色所授權的作業中排除的作業。</span><span class="sxs-lookup"><span data-stu-id="859ae-329">An array of action strings specifying the operations to exclude from the operations which the updated custom role grants.</span></span> |
| <span data-ttu-id="859ae-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="859ae-330">properties.assignableScopes</span></span> |<span data-ttu-id="859ae-331">是</span><span class="sxs-lookup"><span data-stu-id="859ae-331">Yes</span></span> |<span data-ttu-id="859ae-332">String[]</span><span class="sxs-lookup"><span data-stu-id="859ae-332">String[]</span></span> |<span data-ttu-id="859ae-333">範圍陣列，此陣列指定可在其中使用已更新之自訂角色的範圍。</span><span class="sxs-lookup"><span data-stu-id="859ae-333">An array of scopes in which the updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="859ae-334">Response</span><span class="sxs-lookup"><span data-stu-id="859ae-334">Response</span></span>
<span data-ttu-id="859ae-335">狀態碼：201</span><span class="sxs-lookup"><span data-stu-id="859ae-335">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a><span data-ttu-id="859ae-336">刪除自訂角色</span><span class="sxs-lookup"><span data-stu-id="859ae-336">Delete a Custom Role</span></span>
<span data-ttu-id="859ae-337">刪除自訂角色。</span><span class="sxs-lookup"><span data-stu-id="859ae-337">Delete a custom role.</span></span>

<span data-ttu-id="859ae-338">若要刪除自訂角色，您必須在所有 `AssignableScopes` 上都具有 `Microsoft.Authorization/roleDefinitions/delete` 作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-338">To delete a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/delete` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="859ae-339">在內建角色中，只有「擁有者」和「使用者存取系統管理員」會獲得這項作業的存取權。</span><span class="sxs-lookup"><span data-stu-id="859ae-339">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="859ae-340">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="859ae-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="859ae-341">要求</span><span class="sxs-lookup"><span data-stu-id="859ae-341">Request</span></span>
<span data-ttu-id="859ae-342">搭配下列 URI 使用 **DELETE** 方法：</span><span class="sxs-lookup"><span data-stu-id="859ae-342">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="859ae-343">在 URI 內進行下列替代動作以自訂要求：</span><span class="sxs-lookup"><span data-stu-id="859ae-343">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="859ae-344">將 *{scope}* 取代為您要刪除角色定義的範圍。</span><span class="sxs-lookup"><span data-stu-id="859ae-344">Replace *{scope}* with the scope at which you wish to delete the role definition.</span></span> <span data-ttu-id="859ae-345">下列範例顯示如何指定不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="859ae-345">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="859ae-346">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="859ae-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="859ae-347">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="859ae-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="859ae-348">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="859ae-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="859ae-349">將 *{role-definition-id}* 取代為自訂角色的 GUID 角色定義識別碼。</span><span class="sxs-lookup"><span data-stu-id="859ae-349">Replace *{role-definition-id}* with the GUID role definition id of the custom role.</span></span>
3. <span data-ttu-id="859ae-350">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="859ae-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="859ae-351">Response</span><span class="sxs-lookup"><span data-stu-id="859ae-351">Response</span></span>
<span data-ttu-id="859ae-352">狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="859ae-352">Status code: 200</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a><span data-ttu-id="859ae-353">後續步驟</span><span class="sxs-lookup"><span data-stu-id="859ae-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
