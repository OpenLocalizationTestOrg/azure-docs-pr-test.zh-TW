---
title: "使用 Azure 受管理的應用程式 | Microsoft Docs"
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
ms.openlocfilehash: ed8fbaf2a4546c8e31eeced11cd0b5627fd62c0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="f2b65-103">使用內部受管理的應用程式</span><span class="sxs-lookup"><span data-stu-id="f2b65-103">Consume an internal managed application</span></span>

<span data-ttu-id="f2b65-104">您可以使用 Azure [受管理的應用程式](managed-application-overview.md)，以供組織成員使用。</span><span class="sxs-lookup"><span data-stu-id="f2b65-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="f2b65-105">例如，您可以從 IT 部門選取受管理的應用程式，以確保符合組織標準。</span><span class="sxs-lookup"><span data-stu-id="f2b65-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="f2b65-106">這些受管理的應用程式要透過 Service Catalog 取得，而非 Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="f2b65-106">These managed applications are available through the Service Catalog, not the Azure Marketplace.</span></span>

<span data-ttu-id="f2b65-107">在繼續本文之前，您必須先為您的訂用帳戶在 Service Catalog 中提供受管理的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2b65-107">Before proceeding with this article, you must have a managed application available in the service catalog for your subscription.</span></span> <span data-ttu-id="f2b65-108">如果組織中有人尚未建立受管理的應用程式，請參閱[發佈受管理的應用程式以供內部使用](managed-application-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="f2b65-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="f2b65-109">目前，您可以使用 Azure CLI 或 Azure 入口網站來取用受管理的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2b65-109">Currently, you can use either Azure CLI or the Azure portal to consume a managed application.</span></span>

## <a name="create-the-managed-application-by-using-the-portal"></a><span data-ttu-id="f2b65-110">使用入口網站建立受管理的應用程式</span><span class="sxs-lookup"><span data-stu-id="f2b65-110">Create the managed application by using the portal</span></span>

<span data-ttu-id="f2b65-111">若要透過入口網站部署受管理的應用程式，請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f2b65-111">To deploy a managed application through the portal, follow these steps:</span></span>

1. <span data-ttu-id="f2b65-112">移至 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f2b65-112">Go to the Azure portal.</span></span> <span data-ttu-id="f2b65-113">搜尋 **Service Catalog 受管理的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f2b65-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Service Catalog 受管理的應用程式](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="f2b65-115">從可用的解決方案清單中選取您想要建立的受管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2b65-115">Select the managed application you want to create from the list of available solutions.</span></span> <span data-ttu-id="f2b65-116">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="f2b65-116">Select **Create**.</span></span>

   ![受管理的應用程式選取](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="f2b65-118">提供佈建資源所需的參數值。</span><span class="sxs-lookup"><span data-stu-id="f2b65-118">Provide values for the parameters that are required to provision the resources.</span></span> <span data-ttu-id="f2b65-119">選取 [美國中西部] 為位置。</span><span class="sxs-lookup"><span data-stu-id="f2b65-119">Select **West Central US** for location.</span></span> <span data-ttu-id="f2b65-120">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f2b65-120">Select **OK**.</span></span>

   ![受管理的應用程式參數](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="f2b65-122">範本會驗證您所提供的值。</span><span class="sxs-lookup"><span data-stu-id="f2b65-122">The template validates the values you provided.</span></span> <span data-ttu-id="f2b65-123">如果驗證成功，請選取 [確定] 以開始部署。</span><span class="sxs-lookup"><span data-stu-id="f2b65-123">If validation succeeds, select **OK** to start the deployment.</span></span>

   ![受管理的應用程式驗證](./media/managed-application-consumption/validation.png)

<span data-ttu-id="f2b65-125">部署完成之後，範本中定義的適當資源會佈建在您提供的受管理資源群組中。</span><span class="sxs-lookup"><span data-stu-id="f2b65-125">After the deployment finishes, the appropriate resources defined in the template are provisioned in the managed resource group you provided.</span></span>

## <a name="create-the-managed-application-by-using-azure-cli"></a><span data-ttu-id="f2b65-126">使用 Azure CLI 建立受管理的應用程式</span><span class="sxs-lookup"><span data-stu-id="f2b65-126">Create the managed application by using Azure CLI</span></span>

<span data-ttu-id="f2b65-127">有兩種方式可以使用 Azure CLI 來建立受管理的應用程式：</span><span class="sxs-lookup"><span data-stu-id="f2b65-127">There are two ways to create a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="f2b65-128">使用命令以建立受管理的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2b65-128">Use the command for creating managed applications.</span></span>
* <span data-ttu-id="f2b65-129">使用一般範本部署命令。</span><span class="sxs-lookup"><span data-stu-id="f2b65-129">Use the regular template deployment command.</span></span>

### <a name="use-the-template-deployment-command"></a><span data-ttu-id="f2b65-130">使用範本部署命令</span><span class="sxs-lookup"><span data-stu-id="f2b65-130">Use the template deployment command</span></span>

<span data-ttu-id="f2b65-131">部署廠商所建立的 applianceMainTemplate.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="f2b65-131">Deploy the applianceMainTemplate.json file that the vendor created.</span></span>

<span data-ttu-id="f2b65-132">然後建立兩個資源群組。</span><span class="sxs-lookup"><span data-stu-id="f2b65-132">Then create two resource groups.</span></span> <span data-ttu-id="f2b65-133">第一個資源群組是建立受管理應用程式資源的位置：Microsoft.Solutions/appliances。</span><span class="sxs-lookup"><span data-stu-id="f2b65-133">The first resource group is where the managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="f2b65-134">第二個資源群組包含 mainTemplate.json 中定義的所有資源。</span><span class="sxs-lookup"><span data-stu-id="f2b65-134">The second resource group contains all the resources defined in mainTemplate.json.</span></span> <span data-ttu-id="f2b65-135">此資源群組是由 ISV 所管理。</span><span class="sxs-lookup"><span data-stu-id="f2b65-135">This resource group is managed by the ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="f2b65-136">使用 `westcentralus` 作為資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="f2b65-136">Use `westcentralus` as the location of the resource group.</span></span>
>

<span data-ttu-id="f2b65-137">若要在 mainResourceGroup 中部署 applianceMainTemplate.json，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="f2b65-137">To deploy applianceMainTemplate.json in mainResourceGroup, use the following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="f2b65-138">在上述範本執行後，它會提示您提供範本中所定義的參數值。</span><span class="sxs-lookup"><span data-stu-id="f2b65-138">After the preceding template runs, it prompts you for the values of the parameters that are defined in the template.</span></span> <span data-ttu-id="f2b65-139">除了在範本中佈建資源所需的參數之外，您需要兩個金鑰參數值︰</span><span class="sxs-lookup"><span data-stu-id="f2b65-139">In addition to the parameters that are needed to provision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="f2b65-140">**managedResourceGroupId**：資源群組的識別碼包含 applianceMainTemplate.json 中所定義的資源。</span><span class="sxs-lookup"><span data-stu-id="f2b65-140">**managedResourceGroupId**: The ID of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="f2b65-141">識別碼的格式為 `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`。</span><span class="sxs-lookup"><span data-stu-id="f2b65-141">The ID is of the form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="f2b65-142">在上述範例中，則為 `managedResourceGroup` 的識別碼。</span><span class="sxs-lookup"><span data-stu-id="f2b65-142">In the preceding example, it's the ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="f2b65-143">**applianceDefinitionId**：受管理應用程式定義資源的識別碼。</span><span class="sxs-lookup"><span data-stu-id="f2b65-143">**applianceDefinitionId**: The ID of the managed application definition resource.</span></span> <span data-ttu-id="f2b65-144">這個值是由 ISV 所提供。</span><span class="sxs-lookup"><span data-stu-id="f2b65-144">This value is provided by the ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="f2b65-145">發行者必須授與存取權給包含受管理應用程式定義的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f2b65-145">The publisher must grant access to the resource group that contains the managed application definition.</span></span> <span data-ttu-id="f2b65-146">定義資源將在發行者訂用帳戶中建立。</span><span class="sxs-lookup"><span data-stu-id="f2b65-146">The definition resource is created in the publisher subscription.</span></span> <span data-ttu-id="f2b65-147">因此，客戶租用戶中的使用者、使用者群組或應用程式需要這項資源的讀取權限。</span><span class="sxs-lookup"><span data-stu-id="f2b65-147">Therefore, a user, user group, or application in the customer tenant needs read access to this resource.</span></span>

<span data-ttu-id="f2b65-148">順利完成部署之後，您會看到在 mainResourceGroup 中建立了受管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2b65-148">After the deployment finishes successfully, you see the managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="f2b65-149">storageAccount 資源會建立於 managedResourceGroup 中。</span><span class="sxs-lookup"><span data-stu-id="f2b65-149">The storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-the-create-command"></a><span data-ttu-id="f2b65-150">使用 create 命令</span><span class="sxs-lookup"><span data-stu-id="f2b65-150">Use the create command</span></span>

<span data-ttu-id="f2b65-151">您可以使用 `az managedapp create` 命令，從受管理的應用程式定義建立受管理的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2b65-151">You can use the `az managedapp create` command to create a managed application from the managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="f2b65-152">**appliance-definition-Id**：在先前步驟中建立之受管理應用程式定義的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="f2b65-152">**appliance-definition-Id**: The resource ID of the managed application definition created in the preceding step.</span></span> <span data-ttu-id="f2b65-153">若要取得這個識別碼，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f2b65-153">To obtain this ID, run the following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="f2b65-154">此命令會傳回受管理的應用程式定義。</span><span class="sxs-lookup"><span data-stu-id="f2b65-154">This command returns the managed application definition.</span></span> <span data-ttu-id="f2b65-155">您需要 ID 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="f2b65-155">You need the value of the ID property.</span></span>

* <span data-ttu-id="f2b65-156">**managed-rg-id**：資源群組的名稱包含 applianceMainTemplate.json 中所定義的資源。</span><span class="sxs-lookup"><span data-stu-id="f2b65-156">**managed-rg-id**: The name of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="f2b65-157">這個資源群組是受管理的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f2b65-157">This resource group is the managed resource group.</span></span> <span data-ttu-id="f2b65-158">它是由發行者進行管理。</span><span class="sxs-lookup"><span data-stu-id="f2b65-158">It's managed by the publisher.</span></span> <span data-ttu-id="f2b65-159">如果它不存在，則會為您建立。</span><span class="sxs-lookup"><span data-stu-id="f2b65-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="f2b65-160">**resource-group**：受管理應用程式資源建立之資源群組。</span><span class="sxs-lookup"><span data-stu-id="f2b65-160">**resource-group**: The resource group where the managed application resource is created.</span></span> <span data-ttu-id="f2b65-161">Microsoft.Solutions/appliance 資源存在於此資源群組。</span><span class="sxs-lookup"><span data-stu-id="f2b65-161">The Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="f2b65-162">**parameters**：applianceMainTemplate.json 中所定義之資源所需的參數。</span><span class="sxs-lookup"><span data-stu-id="f2b65-162">**parameters**: The parameters that are needed for the resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="f2b65-163">已知問題</span><span class="sxs-lookup"><span data-stu-id="f2b65-163">Known issues</span></span>

<span data-ttu-id="f2b65-164">此預覽版本包含下列問題︰</span><span class="sxs-lookup"><span data-stu-id="f2b65-164">This preview release includes the following issues:</span></span>

* <span data-ttu-id="f2b65-165">受管理的應用程式建立期間會出現 500 內部伺服器錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2b65-165">A 500 internal server error appears during the creation of the managed application.</span></span> <span data-ttu-id="f2b65-166">如果您遇到此問題，有可能是間歇性問題。</span><span class="sxs-lookup"><span data-stu-id="f2b65-166">If you run into this issue, it's likely to be intermittent.</span></span> <span data-ttu-id="f2b65-167">重試作業。</span><span class="sxs-lookup"><span data-stu-id="f2b65-167">Retry the operation.</span></span>
* <span data-ttu-id="f2b65-168">受管理的資源群組需要新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f2b65-168">A new resource group is needed for the managed resource group.</span></span> <span data-ttu-id="f2b65-169">如果您使用現有的資源群組，則部署會失敗。</span><span class="sxs-lookup"><span data-stu-id="f2b65-169">If you use an existing resource group, the deployment fails.</span></span>
* <span data-ttu-id="f2b65-170">包含 Microsoft.Solutions/appliances 資源的資源群組必須建立於 **westcentralus** 位置。</span><span class="sxs-lookup"><span data-stu-id="f2b65-170">The resource group that contains the Microsoft.Solutions/appliances resource must be created in the **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2b65-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f2b65-171">Next steps</span></span>

* <span data-ttu-id="f2b65-172">如需受管理應用程式的簡介，請參閱[受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f2b65-172">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f2b65-173">如需發佈 Service Catalog 受管理應用程式的資訊，請參閱[建立和發佈 Service Catalog 受管理的應用程式](managed-application-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="f2b65-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="f2b65-174">如需將受管理的應用程式發佈到 Azure Marketplace 的資訊，請參閱 [Marketplace 中的 Azure 受管理應用程式](managed-application-author-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="f2b65-174">For information about publishing managed applications to the Azure Marketplace, see [Azure managed applications in the Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="f2b65-175">如需從 Marketplace 使用受管理應用程式的詳細資訊，請參閱[在 Marketplace 中使用 Azure 受管理的應用程式](managed-application-consume-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="f2b65-175">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
