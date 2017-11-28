---
title: "與其他的 Azure AD aaaRole 型存取控制 |Microsoft 文件"
description: "使用 hello REST API 管理角色型存取控制"
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
ms.openlocfilehash: ccd402fd4fe4583288076cac23753dd067694681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-rest-api"></a><span data-ttu-id="ce086-103">管理角色型存取控制以 hello REST API</span><span class="sxs-lookup"><span data-stu-id="ce086-103">Manage Role-Based Access Control with hello REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce086-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce086-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="ce086-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ce086-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="ce086-106">REST API</span><span class="sxs-lookup"><span data-stu-id="ce086-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="ce086-107">角色型存取控制 (RBAC) 在 hello Azure 入口網站和 Azure 資源管理員 API，可協助您管理存取 tooyour 訂用帳戶和細微的層級的資源。</span><span class="sxs-lookup"><span data-stu-id="ce086-107">Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API helps you manage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="ce086-108">利用此功能，您可以藉由指定在特定範圍的某些角色 toothem 授與存取 Active Directory 使用者、 群組或服務主體。</span><span class="sxs-lookup"><span data-stu-id="ce086-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="ce086-109">列出所有角色指派</span><span class="sxs-lookup"><span data-stu-id="ce086-109">List all role assignments</span></span>
<span data-ttu-id="ce086-110">列出所有的 hello 角色指派，在指定的 hello 範圍及 subscopes。</span><span class="sxs-lookup"><span data-stu-id="ce086-110">Lists all hello role assignments at hello specified scope and subscopes.</span></span>

<span data-ttu-id="ce086-111">toolist 角色指派，您必須能夠存取太`Microsoft.Authorization/roleAssignments/read`hello 範圍的作業。</span><span class="sxs-lookup"><span data-stu-id="ce086-111">toolist role assignments, you must have access too`Microsoft.Authorization/roleAssignments/read` operation at hello scope.</span></span> <span data-ttu-id="ce086-112">所有的 hello 內建的角色會授與存取 toothis 作業。</span><span class="sxs-lookup"><span data-stu-id="ce086-112">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="ce086-113">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="ce086-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="ce086-114">要求</span><span class="sxs-lookup"><span data-stu-id="ce086-114">Request</span></span>
<span data-ttu-id="ce086-115">使用 hello**取得**方法具有下列 URI 的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce086-115">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="ce086-116">內 hello URI，請遵循替代 toocustomize hello 您的要求：</span><span class="sxs-lookup"><span data-stu-id="ce086-116">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="ce086-117">取代*{範圍}*與 hello 想 toolist hello 角色指派的範圍。</span><span class="sxs-lookup"><span data-stu-id="ce086-117">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="ce086-118">hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="ce086-118">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="ce086-119">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="ce086-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="ce086-120">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="ce086-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="ce086-121">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="ce086-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="ce086-122">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="ce086-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="ce086-123">取代*{filter}* hello 條件，您會希望 tooapply toofilter hello 角色指派清單：</span><span class="sxs-lookup"><span data-stu-id="ce086-123">Replace *{filter}* with hello condition that you wish tooapply toofilter hello role assignment list:</span></span>

   * <span data-ttu-id="ce086-124">清單只 hello 的角色指派指定範圍內，不包括在 subscopes hello 角色指派：`atScope()`</span><span class="sxs-lookup"><span data-stu-id="ce086-124">List role assignments for only hello specified scope, not including hello role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="ce086-125">僅列出特定使用者、群組或應用程式的角色指派： `principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="ce086-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="ce086-126">僅列出特定使用者的角色指派，包括從群組繼承的角色指派 | `assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="ce086-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="ce086-127">Response</span><span class="sxs-lookup"><span data-stu-id="ce086-127">Response</span></span>
<span data-ttu-id="ce086-128">狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="ce086-128">Status code: 200</span></span>

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

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="ce086-129">取得角色指派的相關資訊</span><span class="sxs-lookup"><span data-stu-id="ce086-129">Get information about a role assignment</span></span>
<span data-ttu-id="ce086-130">取得 hello 角色指派的識別項所指定的單一角色指派的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ce086-130">Gets information about a single role assignment specified by hello role assignment identifier.</span></span>

<span data-ttu-id="ce086-131">tooget 資訊有關角色指派，您必須能夠存取太`Microsoft.Authorization/roleAssignments/read`作業。</span><span class="sxs-lookup"><span data-stu-id="ce086-131">tooget information about a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="ce086-132">所有的 hello 內建的角色會授與存取 toothis 作業。</span><span class="sxs-lookup"><span data-stu-id="ce086-132">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="ce086-133">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="ce086-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="ce086-134">要求</span><span class="sxs-lookup"><span data-stu-id="ce086-134">Request</span></span>
<span data-ttu-id="ce086-135">使用 hello**取得**方法具有下列 URI 的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce086-135">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="ce086-136">內 hello URI，請遵循替代 toocustomize hello 您的要求：</span><span class="sxs-lookup"><span data-stu-id="ce086-136">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="ce086-137">取代*{範圍}*與 hello 想 toolist hello 角色指派的範圍。</span><span class="sxs-lookup"><span data-stu-id="ce086-137">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="ce086-138">hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="ce086-138">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="ce086-139">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="ce086-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="ce086-140">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="ce086-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="ce086-141">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="ce086-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="ce086-142">取代*{角色-指派-識別碼}* hello hello 角色指派的 GUID 識別碼。</span><span class="sxs-lookup"><span data-stu-id="ce086-142">Replace *{role-assignment-id}* with hello GUID identifier of hello role assignment.</span></span>
3. <span data-ttu-id="ce086-143">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="ce086-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="ce086-144">Response</span><span class="sxs-lookup"><span data-stu-id="ce086-144">Response</span></span>
<span data-ttu-id="ce086-145">狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="ce086-145">Status code: 200</span></span>

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

## <a name="create-a-role-assignment"></a><span data-ttu-id="ce086-146">建立角色指派</span><span class="sxs-lookup"><span data-stu-id="ce086-146">Create a Role Assignment</span></span>
<span data-ttu-id="ce086-147">建立角色指派在 hello hello 指定主體授與的 hello 指定的角色，請指定範圍。</span><span class="sxs-lookup"><span data-stu-id="ce086-147">Create a role assignment at hello specified scope for hello specified principal granting hello specified role.</span></span>

<span data-ttu-id="ce086-148">toocreate 角色指派，您必須能夠存取太`Microsoft.Authorization/roleAssignments/write`作業。</span><span class="sxs-lookup"><span data-stu-id="ce086-148">toocreate a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="ce086-149">Hello 內建角色時，只有*擁有者*和*使用者存取系統管理員*授與存取 toothis 作業。</span><span class="sxs-lookup"><span data-stu-id="ce086-149">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="ce086-150">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="ce086-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="ce086-151">要求</span><span class="sxs-lookup"><span data-stu-id="ce086-151">Request</span></span>
<span data-ttu-id="ce086-152">使用 hello**放**方法具有下列 URI 的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce086-152">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="ce086-153">內 hello URI，請遵循替代 toocustomize hello 您的要求：</span><span class="sxs-lookup"><span data-stu-id="ce086-153">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="ce086-154">取代*{範圍}*與 hello 範圍，此時您希望 toocreate hello 角色指派。</span><span class="sxs-lookup"><span data-stu-id="ce086-154">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="ce086-155">當您在父範圍中建立角色指派時，所有的子領域會繼承 hello 相同的角色指派。</span><span class="sxs-lookup"><span data-stu-id="ce086-155">When you create a role assignment at a parent scope, all child scopes inherit hello same role assignment.</span></span> <span data-ttu-id="ce086-156">hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="ce086-156">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="ce086-157">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="ce086-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="ce086-158">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="ce086-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="ce086-159">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="ce086-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="ce086-160">取代*{角色-指派-識別碼}*以新的 GUID，而成為 hello hello 新角色指派的 GUID 識別碼。</span><span class="sxs-lookup"><span data-stu-id="ce086-160">Replace *{role-assignment-id}* with a new GUID, which becomes hello GUID identifier of hello new role assignment.</span></span>
3. <span data-ttu-id="ce086-161">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="ce086-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="ce086-162">Hello 要求主體中，提供 hello 遵循格式中的 hello 值：</span><span class="sxs-lookup"><span data-stu-id="ce086-162">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="ce086-163">元素名稱</span><span class="sxs-lookup"><span data-stu-id="ce086-163">Element Name</span></span> | <span data-ttu-id="ce086-164">必要</span><span class="sxs-lookup"><span data-stu-id="ce086-164">Required</span></span> | <span data-ttu-id="ce086-165">類型</span><span class="sxs-lookup"><span data-stu-id="ce086-165">Type</span></span> | <span data-ttu-id="ce086-166">說明</span><span class="sxs-lookup"><span data-stu-id="ce086-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ce086-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="ce086-167">roleDefinitionId</span></span> |<span data-ttu-id="ce086-168">是</span><span class="sxs-lookup"><span data-stu-id="ce086-168">Yes</span></span> |<span data-ttu-id="ce086-169">String</span><span class="sxs-lookup"><span data-stu-id="ce086-169">String</span></span> |<span data-ttu-id="ce086-170">hello hello 角色識別碼。</span><span class="sxs-lookup"><span data-stu-id="ce086-170">hello identifier of hello role.</span></span> <span data-ttu-id="ce086-171">hello hello 識別項的格式如下：`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="ce086-171">hello format of hello identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="ce086-172">principalId</span><span class="sxs-lookup"><span data-stu-id="ce086-172">principalId</span></span> |<span data-ttu-id="ce086-173">是</span><span class="sxs-lookup"><span data-stu-id="ce086-173">Yes</span></span> |<span data-ttu-id="ce086-174">String</span><span class="sxs-lookup"><span data-stu-id="ce086-174">String</span></span> |<span data-ttu-id="ce086-175">hello Azure AD 主體 （使用者、 群組或服務主體） 的 objectId toowhich hello 角色指派。</span><span class="sxs-lookup"><span data-stu-id="ce086-175">objectId of hello Azure AD principal (user, group, or service principal) toowhich hello role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="ce086-176">Response</span><span class="sxs-lookup"><span data-stu-id="ce086-176">Response</span></span>
<span data-ttu-id="ce086-177">狀態碼：201</span><span class="sxs-lookup"><span data-stu-id="ce086-177">Status code: 201</span></span>

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

## <a name="delete-a-role-assignment"></a><span data-ttu-id="ce086-178">刪除角色指派</span><span class="sxs-lookup"><span data-stu-id="ce086-178">Delete a Role Assignment</span></span>
<span data-ttu-id="ce086-179">刪除角色指派 hello 在指定範圍。</span><span class="sxs-lookup"><span data-stu-id="ce086-179">Delete a role assignment at hello specified scope.</span></span>

<span data-ttu-id="ce086-180">toodelete 角色指派，您必須擁有存取 toohello`Microsoft.Authorization/roleAssignments/delete`作業。</span><span class="sxs-lookup"><span data-stu-id="ce086-180">toodelete a role assignment, you must have access toohello `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="ce086-181">Hello 內建角色時，只有*擁有者*和*使用者存取系統管理員*授與存取 toothis 作業。</span><span class="sxs-lookup"><span data-stu-id="ce086-181">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="ce086-182">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="ce086-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="ce086-183">要求</span><span class="sxs-lookup"><span data-stu-id="ce086-183">Request</span></span>
<span data-ttu-id="ce086-184">使用 hello**刪除**方法具有下列 URI 的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce086-184">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="ce086-185">內 hello URI，請遵循替代 toocustomize hello 您的要求：</span><span class="sxs-lookup"><span data-stu-id="ce086-185">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="ce086-186">取代*{範圍}*與 hello 範圍，此時您希望 toocreate hello 角色指派。</span><span class="sxs-lookup"><span data-stu-id="ce086-186">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="ce086-187">hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="ce086-187">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="ce086-188">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="ce086-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="ce086-189">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="ce086-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="ce086-190">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="ce086-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="ce086-191">取代*{角色-指派-識別碼}* hello 角色指派 id 的 GUID。</span><span class="sxs-lookup"><span data-stu-id="ce086-191">Replace *{role-assignment-id}* with hello role assignment id GUID.</span></span>
3. <span data-ttu-id="ce086-192">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="ce086-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="ce086-193">Response</span><span class="sxs-lookup"><span data-stu-id="ce086-193">Response</span></span>
<span data-ttu-id="ce086-194">狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="ce086-194">Status code: 200</span></span>

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

## <a name="list-all-roles"></a><span data-ttu-id="ce086-195">列出所有角色</span><span class="sxs-lookup"><span data-stu-id="ce086-195">List all Roles</span></span>
<span data-ttu-id="ce086-196">列出所有 hello 角色可供使用時指定的 hello 的指派範圍。</span><span class="sxs-lookup"><span data-stu-id="ce086-196">Lists all hello roles that are available for assignment at hello specified scope.</span></span>

<span data-ttu-id="ce086-197">toolist 角色必須具有存取太`Microsoft.Authorization/roleDefinitions/read`hello 範圍的作業。</span><span class="sxs-lookup"><span data-stu-id="ce086-197">toolist roles, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation at hello scope.</span></span> <span data-ttu-id="ce086-198">所有的 hello 內建的角色會授與存取 toothis 作業。</span><span class="sxs-lookup"><span data-stu-id="ce086-198">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="ce086-199">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="ce086-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="ce086-200">要求</span><span class="sxs-lookup"><span data-stu-id="ce086-200">Request</span></span>
<span data-ttu-id="ce086-201">使用 hello**取得**方法具有下列 URI 的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce086-201">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="ce086-202">內 hello URI，請遵循替代 toocustomize hello 您的要求：</span><span class="sxs-lookup"><span data-stu-id="ce086-202">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="ce086-203">取代*{範圍}*與 hello 想 toolist hello 角色的範圍。</span><span class="sxs-lookup"><span data-stu-id="ce086-203">Replace *{scope}* with hello scope for which you wish toolist hello roles.</span></span> <span data-ttu-id="ce086-204">hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="ce086-204">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="ce086-205">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="ce086-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="ce086-206">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="ce086-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="ce086-207">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="ce086-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="ce086-208">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="ce086-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="ce086-209">取代*{filter}* hello 條件，您希望角色 tooapply toofilter hello 清單：</span><span class="sxs-lookup"><span data-stu-id="ce086-209">Replace *{filter}* with hello condition that you wish tooapply toofilter hello list of roles:</span></span>

   * <span data-ttu-id="ce086-210">清單角色在 hello 分派可用的指定範圍和其子範圍的任何：`atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="ce086-210">List roles available for assignment at hello specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="ce086-211">使用確切的顯示名稱來搜尋角色： `roleName%20eq%20'{role-display-name}'`。</span><span class="sxs-lookup"><span data-stu-id="ce086-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="ce086-212">使用 hello URL 編碼形式的 hello 角色 hello 確切的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="ce086-212">Use hello URL encoded form of hello exact display name of hello role.</span></span> <span data-ttu-id="ce086-213">例如， `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="ce086-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="ce086-214">Response</span><span class="sxs-lookup"><span data-stu-id="ce086-214">Response</span></span>
<span data-ttu-id="ce086-215">狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="ce086-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
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

## <a name="get-information-about-a-role"></a><span data-ttu-id="ce086-216">取得角色的相關資訊</span><span class="sxs-lookup"><span data-stu-id="ce086-216">Get information about a Role</span></span>
<span data-ttu-id="ce086-217">取得 hello 角色定義識別項所指定的單一角色的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ce086-217">Gets information about a single role specified by hello role definition identifier.</span></span> <span data-ttu-id="ce086-218">tooget 使用它的顯示名稱的單一角色的相關的資訊，請參閱[列出所有角色](role-based-access-control-manage-access-rest.md#list-all-roles)。</span><span class="sxs-lookup"><span data-stu-id="ce086-218">tooget information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="ce086-219">tooget 有關角色的資訊，您必須能夠存取太`Microsoft.Authorization/roleDefinitions/read`作業。</span><span class="sxs-lookup"><span data-stu-id="ce086-219">tooget information about a role, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="ce086-220">所有的 hello 內建的角色會授與存取 toothis 作業。</span><span class="sxs-lookup"><span data-stu-id="ce086-220">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="ce086-221">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="ce086-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="ce086-222">要求</span><span class="sxs-lookup"><span data-stu-id="ce086-222">Request</span></span>
<span data-ttu-id="ce086-223">使用 hello**取得**方法具有下列 URI 的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce086-223">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="ce086-224">內 hello URI，請遵循替代 toocustomize hello 您的要求：</span><span class="sxs-lookup"><span data-stu-id="ce086-224">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="ce086-225">取代*{範圍}*與 hello 想 toolist hello 角色指派的範圍。</span><span class="sxs-lookup"><span data-stu-id="ce086-225">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="ce086-226">hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="ce086-226">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="ce086-227">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="ce086-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="ce086-228">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="ce086-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="ce086-229">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="ce086-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="ce086-230">取代*{角色-定義-識別碼}* hello 角色定義的 hello GUID 識別碼。</span><span class="sxs-lookup"><span data-stu-id="ce086-230">Replace *{role-definition-id}* with hello GUID identifier of hello role definition.</span></span>
3. <span data-ttu-id="ce086-231">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="ce086-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="ce086-232">Response</span><span class="sxs-lookup"><span data-stu-id="ce086-232">Response</span></span>
<span data-ttu-id="ce086-233">狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="ce086-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
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

## <a name="create-a-custom-role"></a><span data-ttu-id="ce086-234">建立自訂角色</span><span class="sxs-lookup"><span data-stu-id="ce086-234">Create a Custom Role</span></span>
<span data-ttu-id="ce086-235">建立自訂角色。</span><span class="sxs-lookup"><span data-stu-id="ce086-235">Create a custom role.</span></span>

<span data-ttu-id="ce086-236">toocreate 自訂安全性角色，您必須能夠存取太`Microsoft.Authorization/roleDefinitions/write`作業上所有的 hello `AssignableScopes`。</span><span class="sxs-lookup"><span data-stu-id="ce086-236">toocreate a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="ce086-237">Hello 內建角色時，只有*擁有者*和*使用者存取系統管理員*授與存取 toothis 作業。</span><span class="sxs-lookup"><span data-stu-id="ce086-237">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="ce086-238">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="ce086-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="ce086-239">要求</span><span class="sxs-lookup"><span data-stu-id="ce086-239">Request</span></span>
<span data-ttu-id="ce086-240">使用 hello**放**方法具有下列 URI 的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce086-240">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="ce086-241">內 hello URI，請遵循替代 toocustomize hello 您的要求：</span><span class="sxs-lookup"><span data-stu-id="ce086-241">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="ce086-242">取代*{範圍}* hello 與第一個*AssignableScope*的 hello 自訂角色。</span><span class="sxs-lookup"><span data-stu-id="ce086-242">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="ce086-243">hello 遵循範例顯示如何 toospecify hello 不同層級的範圍。</span><span class="sxs-lookup"><span data-stu-id="ce086-243">hello following examples show how toospecify hello scope for different levels.</span></span>

   * <span data-ttu-id="ce086-244">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="ce086-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="ce086-245">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="ce086-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="ce086-246">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="ce086-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="ce086-247">取代*{角色-定義-識別碼}*以新的 GUID，而成為新的自訂角色 hello hello GUID 識別碼。</span><span class="sxs-lookup"><span data-stu-id="ce086-247">Replace *{role-definition-id}* with a new GUID, which becomes hello GUID identifier of hello new custom role.</span></span>
3. <span data-ttu-id="ce086-248">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="ce086-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="ce086-249">Hello 要求主體中，提供 hello 遵循格式中的 hello 值：</span><span class="sxs-lookup"><span data-stu-id="ce086-249">For hello request body, provide hello values in hello following format:</span></span>

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

| <span data-ttu-id="ce086-250">元素名稱</span><span class="sxs-lookup"><span data-stu-id="ce086-250">Element Name</span></span> | <span data-ttu-id="ce086-251">必要</span><span class="sxs-lookup"><span data-stu-id="ce086-251">Required</span></span> | <span data-ttu-id="ce086-252">類型</span><span class="sxs-lookup"><span data-stu-id="ce086-252">Type</span></span> | <span data-ttu-id="ce086-253">說明</span><span class="sxs-lookup"><span data-stu-id="ce086-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ce086-254">名稱</span><span class="sxs-lookup"><span data-stu-id="ce086-254">name</span></span> |<span data-ttu-id="ce086-255">是</span><span class="sxs-lookup"><span data-stu-id="ce086-255">Yes</span></span> |<span data-ttu-id="ce086-256">String</span><span class="sxs-lookup"><span data-stu-id="ce086-256">String</span></span> |<span data-ttu-id="ce086-257">Hello 自訂角色的 GUID 識別碼。</span><span class="sxs-lookup"><span data-stu-id="ce086-257">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="ce086-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="ce086-258">properties.roleName</span></span> |<span data-ttu-id="ce086-259">是</span><span class="sxs-lookup"><span data-stu-id="ce086-259">Yes</span></span> |<span data-ttu-id="ce086-260">String</span><span class="sxs-lookup"><span data-stu-id="ce086-260">String</span></span> |<span data-ttu-id="ce086-261">Hello 自訂角色的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="ce086-261">Display name of hello custom role.</span></span> <span data-ttu-id="ce086-262">大小上限為 128 個字元。</span><span class="sxs-lookup"><span data-stu-id="ce086-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="ce086-263">properties.description</span><span class="sxs-lookup"><span data-stu-id="ce086-263">properties.description</span></span> |<span data-ttu-id="ce086-264">否</span><span class="sxs-lookup"><span data-stu-id="ce086-264">No</span></span> |<span data-ttu-id="ce086-265">String</span><span class="sxs-lookup"><span data-stu-id="ce086-265">String</span></span> |<span data-ttu-id="ce086-266">Hello 自訂角色的描述。</span><span class="sxs-lookup"><span data-stu-id="ce086-266">Description of hello custom role.</span></span> <span data-ttu-id="ce086-267">大小上限為 1024 個字元。</span><span class="sxs-lookup"><span data-stu-id="ce086-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="ce086-268">properties.type</span><span class="sxs-lookup"><span data-stu-id="ce086-268">properties.type</span></span> |<span data-ttu-id="ce086-269">是</span><span class="sxs-lookup"><span data-stu-id="ce086-269">Yes</span></span> |<span data-ttu-id="ce086-270">String</span><span class="sxs-lookup"><span data-stu-id="ce086-270">String</span></span> |<span data-ttu-id="ce086-271">設定得 「 CustomRole。 」</span><span class="sxs-lookup"><span data-stu-id="ce086-271">Set too"CustomRole."</span></span> |
| <span data-ttu-id="ce086-272">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="ce086-272">properties.permissions.actions</span></span> |<span data-ttu-id="ce086-273">yes</span><span class="sxs-lookup"><span data-stu-id="ce086-273">Yes</span></span> |<span data-ttu-id="ce086-274">String[]</span><span class="sxs-lookup"><span data-stu-id="ce086-274">String[]</span></span> |<span data-ttu-id="ce086-275">字串 hello 自訂角色所授與的指定 hello 作業的動作陣列。</span><span class="sxs-lookup"><span data-stu-id="ce086-275">An array of action strings specifying hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="ce086-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="ce086-276">properties.permissions.notActions</span></span> |<span data-ttu-id="ce086-277">否</span><span class="sxs-lookup"><span data-stu-id="ce086-277">No</span></span> |<span data-ttu-id="ce086-278">String[]</span><span class="sxs-lookup"><span data-stu-id="ce086-278">String[]</span></span> |<span data-ttu-id="ce086-279">指定 hello 作業 tooexclude hello 自訂角色所授與的 hello 作業的動作字串的陣列。</span><span class="sxs-lookup"><span data-stu-id="ce086-279">An array of action strings specifying hello operations tooexclude from hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="ce086-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="ce086-280">properties.assignableScopes</span></span> |<span data-ttu-id="ce086-281">是</span><span class="sxs-lookup"><span data-stu-id="ce086-281">Yes</span></span> |<span data-ttu-id="ce086-282">String[]</span><span class="sxs-lookup"><span data-stu-id="ce086-282">String[]</span></span> |<span data-ttu-id="ce086-283">陣列的範圍中的 hello 可以使用自訂角色。</span><span class="sxs-lookup"><span data-stu-id="ce086-283">An array of scopes in which hello custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="ce086-284">Response</span><span class="sxs-lookup"><span data-stu-id="ce086-284">Response</span></span>
<span data-ttu-id="ce086-285">狀態碼：201</span><span class="sxs-lookup"><span data-stu-id="ce086-285">Status code: 201</span></span>

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

## <a name="update-a-custom-role"></a><span data-ttu-id="ce086-286">更新自訂角色</span><span class="sxs-lookup"><span data-stu-id="ce086-286">Update a Custom Role</span></span>
<span data-ttu-id="ce086-287">修改自訂角色。</span><span class="sxs-lookup"><span data-stu-id="ce086-287">Modify a custom role.</span></span>

<span data-ttu-id="ce086-288">toomodify 自訂安全性角色，您必須能夠存取太`Microsoft.Authorization/roleDefinitions/write`作業上所有的 hello `AssignableScopes`。</span><span class="sxs-lookup"><span data-stu-id="ce086-288">toomodify a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="ce086-289">Hello 內建角色時，只有*擁有者*和*使用者存取系統管理員*授與存取 toothis 作業。</span><span class="sxs-lookup"><span data-stu-id="ce086-289">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="ce086-290">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="ce086-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="ce086-291">要求</span><span class="sxs-lookup"><span data-stu-id="ce086-291">Request</span></span>
<span data-ttu-id="ce086-292">使用 hello**放**方法具有下列 URI 的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce086-292">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="ce086-293">內 hello URI，請遵循替代 toocustomize hello 您的要求：</span><span class="sxs-lookup"><span data-stu-id="ce086-293">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="ce086-294">取代*{範圍}* hello 與第一個*AssignableScope*的 hello 自訂角色。</span><span class="sxs-lookup"><span data-stu-id="ce086-294">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="ce086-295">hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="ce086-295">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="ce086-296">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="ce086-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="ce086-297">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="ce086-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="ce086-298">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="ce086-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="ce086-299">取代*{角色-定義-識別碼}* hello 自訂角色的 hello GUID 識別碼。</span><span class="sxs-lookup"><span data-stu-id="ce086-299">Replace *{role-definition-id}* with hello GUID identifier of hello custom role.</span></span>
3. <span data-ttu-id="ce086-300">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="ce086-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="ce086-301">Hello 要求主體中，提供 hello 遵循格式中的 hello 值：</span><span class="sxs-lookup"><span data-stu-id="ce086-301">For hello request body, provide hello values in hello following format:</span></span>

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

| <span data-ttu-id="ce086-302">元素名稱</span><span class="sxs-lookup"><span data-stu-id="ce086-302">Element Name</span></span> | <span data-ttu-id="ce086-303">必要</span><span class="sxs-lookup"><span data-stu-id="ce086-303">Required</span></span> | <span data-ttu-id="ce086-304">類型</span><span class="sxs-lookup"><span data-stu-id="ce086-304">Type</span></span> | <span data-ttu-id="ce086-305">說明</span><span class="sxs-lookup"><span data-stu-id="ce086-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ce086-306">名稱</span><span class="sxs-lookup"><span data-stu-id="ce086-306">name</span></span> |<span data-ttu-id="ce086-307">是</span><span class="sxs-lookup"><span data-stu-id="ce086-307">Yes</span></span> |<span data-ttu-id="ce086-308">String</span><span class="sxs-lookup"><span data-stu-id="ce086-308">String</span></span> |<span data-ttu-id="ce086-309">Hello 自訂角色的 GUID 識別碼。</span><span class="sxs-lookup"><span data-stu-id="ce086-309">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="ce086-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="ce086-310">properties.roleName</span></span> |<span data-ttu-id="ce086-311">是</span><span class="sxs-lookup"><span data-stu-id="ce086-311">Yes</span></span> |<span data-ttu-id="ce086-312">String</span><span class="sxs-lookup"><span data-stu-id="ce086-312">String</span></span> |<span data-ttu-id="ce086-313">Hello 更新自訂角色的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="ce086-313">Display name of hello updated custom role.</span></span> |
| <span data-ttu-id="ce086-314">properties.description</span><span class="sxs-lookup"><span data-stu-id="ce086-314">properties.description</span></span> |<span data-ttu-id="ce086-315">否</span><span class="sxs-lookup"><span data-stu-id="ce086-315">No</span></span> |<span data-ttu-id="ce086-316">String</span><span class="sxs-lookup"><span data-stu-id="ce086-316">String</span></span> |<span data-ttu-id="ce086-317">Hello 的描述更新自訂角色。</span><span class="sxs-lookup"><span data-stu-id="ce086-317">Description of hello updated custom role.</span></span> |
| <span data-ttu-id="ce086-318">properties.type</span><span class="sxs-lookup"><span data-stu-id="ce086-318">properties.type</span></span> |<span data-ttu-id="ce086-319">是</span><span class="sxs-lookup"><span data-stu-id="ce086-319">Yes</span></span> |<span data-ttu-id="ce086-320">String</span><span class="sxs-lookup"><span data-stu-id="ce086-320">String</span></span> |<span data-ttu-id="ce086-321">設定得 「 CustomRole。 」</span><span class="sxs-lookup"><span data-stu-id="ce086-321">Set too"CustomRole."</span></span> |
| <span data-ttu-id="ce086-322">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="ce086-322">properties.permissions.actions</span></span> |<span data-ttu-id="ce086-323">yes</span><span class="sxs-lookup"><span data-stu-id="ce086-323">Yes</span></span> |<span data-ttu-id="ce086-324">String[]</span><span class="sxs-lookup"><span data-stu-id="ce086-324">String[]</span></span> |<span data-ttu-id="ce086-325">指定 hello 作業 toowhich hello 的動作字串的陣列會更新自訂角色授與的存取。</span><span class="sxs-lookup"><span data-stu-id="ce086-325">An array of action strings specifying hello operations toowhich hello updated custom role grants access.</span></span> |
| <span data-ttu-id="ce086-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="ce086-326">properties.permissions.notActions</span></span> |<span data-ttu-id="ce086-327">否</span><span class="sxs-lookup"><span data-stu-id="ce086-327">No</span></span> |<span data-ttu-id="ce086-328">String[]</span><span class="sxs-lookup"><span data-stu-id="ce086-328">String[]</span></span> |<span data-ttu-id="ce086-329">從 hello 作業的 hello 更新自訂角色授與的指定 hello 作業 tooexclude 之字串的動作陣列。</span><span class="sxs-lookup"><span data-stu-id="ce086-329">An array of action strings specifying hello operations tooexclude from hello operations which hello updated custom role grants.</span></span> |
| <span data-ttu-id="ce086-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="ce086-330">properties.assignableScopes</span></span> |<span data-ttu-id="ce086-331">是</span><span class="sxs-lookup"><span data-stu-id="ce086-331">Yes</span></span> |<span data-ttu-id="ce086-332">String[]</span><span class="sxs-lookup"><span data-stu-id="ce086-332">String[]</span></span> |<span data-ttu-id="ce086-333">陣列的範圍中的 hello 更新自訂角色可用。</span><span class="sxs-lookup"><span data-stu-id="ce086-333">An array of scopes in which hello updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="ce086-334">Response</span><span class="sxs-lookup"><span data-stu-id="ce086-334">Response</span></span>
<span data-ttu-id="ce086-335">狀態碼：201</span><span class="sxs-lookup"><span data-stu-id="ce086-335">Status code: 201</span></span>

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

## <a name="delete-a-custom-role"></a><span data-ttu-id="ce086-336">刪除自訂角色</span><span class="sxs-lookup"><span data-stu-id="ce086-336">Delete a Custom Role</span></span>
<span data-ttu-id="ce086-337">刪除自訂角色。</span><span class="sxs-lookup"><span data-stu-id="ce086-337">Delete a custom role.</span></span>

<span data-ttu-id="ce086-338">toodelete 自訂安全性角色，您必須能夠存取太`Microsoft.Authorization/roleDefinitions/delete`作業上所有的 hello `AssignableScopes`。</span><span class="sxs-lookup"><span data-stu-id="ce086-338">toodelete a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/delete` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="ce086-339">Hello 內建角色時，只有*擁有者*和*使用者存取系統管理員*授與存取 toothis 作業。</span><span class="sxs-lookup"><span data-stu-id="ce086-339">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="ce086-340">如需有關角色指派和管理 Azure 資源存取權的詳細資訊，請參閱 [Azure 角色型存取控制](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="ce086-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="ce086-341">要求</span><span class="sxs-lookup"><span data-stu-id="ce086-341">Request</span></span>
<span data-ttu-id="ce086-342">使用 hello**刪除**方法具有下列 URI 的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce086-342">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="ce086-343">內 hello URI，請遵循替代 toocustomize hello 您的要求：</span><span class="sxs-lookup"><span data-stu-id="ce086-343">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="ce086-344">取代*{範圍}*與 hello 想 toodelete hello 角色定義的範圍。</span><span class="sxs-lookup"><span data-stu-id="ce086-344">Replace *{scope}* with hello scope at which you wish toodelete hello role definition.</span></span> <span data-ttu-id="ce086-345">hello 遵循範例顯示如何 toospecify hello 不同層級的範圍：</span><span class="sxs-lookup"><span data-stu-id="ce086-345">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="ce086-346">訂用帳戶：/subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="ce086-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="ce086-347">資源群組：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="ce086-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="ce086-348">資源：/subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="ce086-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="ce086-349">取代*{角色-定義-識別碼}* hello GUID 角色定義識別碼為 hello 自訂角色。</span><span class="sxs-lookup"><span data-stu-id="ce086-349">Replace *{role-definition-id}* with hello GUID role definition id of hello custom role.</span></span>
3. <span data-ttu-id="ce086-350">將 *{api-version}* 取代為 2015-07-01。</span><span class="sxs-lookup"><span data-stu-id="ce086-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="ce086-351">Response</span><span class="sxs-lookup"><span data-stu-id="ce086-351">Response</span></span>
<span data-ttu-id="ce086-352">狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="ce086-352">Status code: 200</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ce086-353">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ce086-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
