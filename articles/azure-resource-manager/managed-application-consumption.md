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
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="cbe00-103">使用內部受管理的應用程式</span><span class="sxs-lookup"><span data-stu-id="cbe00-103">Consume an internal managed application</span></span>

<span data-ttu-id="cbe00-104">您可以使用 Azure [受管理的應用程式](managed-application-overview.md)，以供組織成員使用。</span><span class="sxs-lookup"><span data-stu-id="cbe00-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="cbe00-105">例如，您可以從 IT 部門選取受管理的應用程式，以確保符合組織標準。</span><span class="sxs-lookup"><span data-stu-id="cbe00-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="cbe00-106">這些受管理的應用程式皆可透過服務類別目錄，hello Azure Marketplace hello。</span><span class="sxs-lookup"><span data-stu-id="cbe00-106">These managed applications are available through hello Service Catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="cbe00-107">與此發行項之前，您必須擁有 hello 服務類別目錄中可用的受管理應用程式為您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cbe00-107">Before proceeding with this article, you must have a managed application available in hello service catalog for your subscription.</span></span> <span data-ttu-id="cbe00-108">如果組織中有人尚未建立受管理的應用程式，請參閱[發佈受管理的應用程式以供內部使用](managed-application-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="cbe00-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="cbe00-109">目前，您可以使用 Azure CLI 或 hello Azure 入口網站 tooconsume 受管理的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbe00-109">Currently, you can use either Azure CLI or hello Azure portal tooconsume a managed application.</span></span>

## <a name="create-hello-managed-application-by-using-hello-portal"></a><span data-ttu-id="cbe00-110">使用 hello 入口網站建立 hello 受管理應用程式</span><span class="sxs-lookup"><span data-stu-id="cbe00-110">Create hello managed application by using hello portal</span></span>

<span data-ttu-id="cbe00-111">toodeploy 受管理的應用程式，透過 hello 入口網站，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cbe00-111">toodeploy a managed application through hello portal, follow these steps:</span></span>

1. <span data-ttu-id="cbe00-112">移 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="cbe00-112">Go toohello Azure portal.</span></span> <span data-ttu-id="cbe00-113">搜尋 **Service Catalog 受管理的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cbe00-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Service Catalog 受管理的應用程式](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="cbe00-115">選取 hello 管理您想從可用方案清單 hello toocreate 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbe00-115">Select hello managed application you want toocreate from hello list of available solutions.</span></span> <span data-ttu-id="cbe00-116">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="cbe00-116">Select **Create**.</span></span>

   ![受管理的應用程式選取](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="cbe00-118">提供所需要的 tooprovision hello 資源 hello 參數的值。</span><span class="sxs-lookup"><span data-stu-id="cbe00-118">Provide values for hello parameters that are required tooprovision hello resources.</span></span> <span data-ttu-id="cbe00-119">選取 [美國中西部] 為位置。</span><span class="sxs-lookup"><span data-stu-id="cbe00-119">Select **West Central US** for location.</span></span> <span data-ttu-id="cbe00-120">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="cbe00-120">Select **OK**.</span></span>

   ![受管理的應用程式參數](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="cbe00-122">hello 範本會驗證您所提供的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="cbe00-122">hello template validates hello values you provided.</span></span> <span data-ttu-id="cbe00-123">如果驗證成功，請選取**確定**toostart hello 部署。</span><span class="sxs-lookup"><span data-stu-id="cbe00-123">If validation succeeds, select **OK** toostart hello deployment.</span></span>

   ![受管理的應用程式驗證](./media/managed-application-consumption/validation.png)

<span data-ttu-id="cbe00-125">Hello 部署完成後，hello hello 範本中定義適當的資源會在您提供的 hello 受管理的資源群組中佈建。</span><span class="sxs-lookup"><span data-stu-id="cbe00-125">After hello deployment finishes, hello appropriate resources defined in hello template are provisioned in hello managed resource group you provided.</span></span>

## <a name="create-hello-managed-application-by-using-azure-cli"></a><span data-ttu-id="cbe00-126">使用 Azure CLI 建立 hello 受管理應用程式</span><span class="sxs-lookup"><span data-stu-id="cbe00-126">Create hello managed application by using Azure CLI</span></span>

<span data-ttu-id="cbe00-127">有兩種方式 toocreate 受管理的應用程式使用 Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="cbe00-127">There are two ways toocreate a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="cbe00-128">建立受管理的應用程式使用 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="cbe00-128">Use hello command for creating managed applications.</span></span>
* <span data-ttu-id="cbe00-129">使用 hello 一般範本部署命令。</span><span class="sxs-lookup"><span data-stu-id="cbe00-129">Use hello regular template deployment command.</span></span>

### <a name="use-hello-template-deployment-command"></a><span data-ttu-id="cbe00-130">使用 hello 範本部署命令</span><span class="sxs-lookup"><span data-stu-id="cbe00-130">Use hello template deployment command</span></span>

<span data-ttu-id="cbe00-131">部署 hello 廠商建立的 hello applianceMainTemplate.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="cbe00-131">Deploy hello applianceMainTemplate.json file that hello vendor created.</span></span>

<span data-ttu-id="cbe00-132">然後建立兩個資源群組。</span><span class="sxs-lookup"><span data-stu-id="cbe00-132">Then create two resource groups.</span></span> <span data-ttu-id="cbe00-133">hello 第一個資源群組是 hello 受管理的應用程式資源建立的位置： Microsoft.Solutions/appliances。</span><span class="sxs-lookup"><span data-stu-id="cbe00-133">hello first resource group is where hello managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="cbe00-134">hello 第二個資源群組包含所有 hello mainTemplate.json 中定義。</span><span class="sxs-lookup"><span data-stu-id="cbe00-134">hello second resource group contains all hello resources defined in mainTemplate.json.</span></span> <span data-ttu-id="cbe00-135">此資源群組是由 hello ISV 管理。</span><span class="sxs-lookup"><span data-stu-id="cbe00-135">This resource group is managed by hello ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="cbe00-136">使用`westcentralus`做為 hello hello 資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="cbe00-136">Use `westcentralus` as hello location of hello resource group.</span></span>
>

<span data-ttu-id="cbe00-137">toodeploy applianceMainTemplate.json mainResourceGroup，下列命令使用 hello 中：</span><span class="sxs-lookup"><span data-stu-id="cbe00-137">toodeploy applianceMainTemplate.json in mainResourceGroup, use hello following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="cbe00-138">之後 hello 之前執行範本，它會提示您輸入 hello hello 範本中所定義的 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="cbe00-138">After hello preceding template runs, it prompts you for hello values of hello parameters that are defined in hello template.</span></span> <span data-ttu-id="cbe00-139">此外 toohello 參數需要 tooprovision 資源範本中的，您需要兩個索引鍵的參數值：</span><span class="sxs-lookup"><span data-stu-id="cbe00-139">In addition toohello parameters that are needed tooprovision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="cbe00-140">**managedResourceGroupId**: hello hello 資源群組包含 hello 資源 applianceMainTemplate.json 中定義的識別碼。</span><span class="sxs-lookup"><span data-stu-id="cbe00-140">**managedResourceGroupId**: hello ID of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="cbe00-141">hello 識別碼是 hello 表單的`/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`。</span><span class="sxs-lookup"><span data-stu-id="cbe00-141">hello ID is of hello form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="cbe00-142">在上述範例中的 hello，它的 hello 識別碼`managedResourceGroup`。</span><span class="sxs-lookup"><span data-stu-id="cbe00-142">In hello preceding example, it's hello ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="cbe00-143">**applianceDefinitionId**: hello 識別碼 hello 的受管理應用程式定義的資源。</span><span class="sxs-lookup"><span data-stu-id="cbe00-143">**applianceDefinitionId**: hello ID of hello managed application definition resource.</span></span> <span data-ttu-id="cbe00-144">這個值是由 hello ISV 提供。</span><span class="sxs-lookup"><span data-stu-id="cbe00-144">This value is provided by hello ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="cbe00-145">hello 發行者必須授與存取 toohello 資源群組含有 hello 受管理應用程式定義。</span><span class="sxs-lookup"><span data-stu-id="cbe00-145">hello publisher must grant access toohello resource group that contains hello managed application definition.</span></span> <span data-ttu-id="cbe00-146">hello 發行者訂用帳戶中建立 hello 定義資源。</span><span class="sxs-lookup"><span data-stu-id="cbe00-146">hello definition resource is created in hello publisher subscription.</span></span> <span data-ttu-id="cbe00-147">因此，使用者、 使用者群組或在 hello 客戶租用戶中的應用程式需要讀取權限 toothis 資源。</span><span class="sxs-lookup"><span data-stu-id="cbe00-147">Therefore, a user, user group, or application in hello customer tenant needs read access toothis resource.</span></span>

<span data-ttu-id="cbe00-148">Hello 部署成功完成之後，您會看到受管理的 hello mainResourceGroup 中建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbe00-148">After hello deployment finishes successfully, you see hello managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="cbe00-149">managedResourceGroup 中建立 hello storageAccount 資源。</span><span class="sxs-lookup"><span data-stu-id="cbe00-149">hello storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-hello-create-command"></a><span data-ttu-id="cbe00-150">使用 hello 建立命令</span><span class="sxs-lookup"><span data-stu-id="cbe00-150">Use hello create command</span></span>

<span data-ttu-id="cbe00-151">您可以使用 hello`az managedapp create`命令 toocreate hello 從 managed 應用程式受管理應用程式定義。</span><span class="sxs-lookup"><span data-stu-id="cbe00-151">You can use hello `az managedapp create` command toocreate a managed application from hello managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="cbe00-152">**應用裝置定義 Id**: hello 資源識別碼 hello 受管理的 hello 前面步驟中建立的應用程式定義。</span><span class="sxs-lookup"><span data-stu-id="cbe00-152">**appliance-definition-Id**: hello resource ID of hello managed application definition created in hello preceding step.</span></span> <span data-ttu-id="cbe00-153">tooobtain 這個識別碼，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbe00-153">tooobtain this ID, run hello following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="cbe00-154">此命令會傳回 hello 受管理應用程式定義。</span><span class="sxs-lookup"><span data-stu-id="cbe00-154">This command returns hello managed application definition.</span></span> <span data-ttu-id="cbe00-155">您需要 hello hello ID 屬性值。</span><span class="sxs-lookup"><span data-stu-id="cbe00-155">You need hello value of hello ID property.</span></span>

* <span data-ttu-id="cbe00-156">**管理 rg 識別碼**: hello hello 資源群組包含 hello 資源 applianceMainTemplate.json 中定義的名稱。</span><span class="sxs-lookup"><span data-stu-id="cbe00-156">**managed-rg-id**: hello name of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="cbe00-157">此資源群組是 hello 受管理的資源群組。</span><span class="sxs-lookup"><span data-stu-id="cbe00-157">This resource group is hello managed resource group.</span></span> <span data-ttu-id="cbe00-158">它被受 hello 發行者。</span><span class="sxs-lookup"><span data-stu-id="cbe00-158">It's managed by hello publisher.</span></span> <span data-ttu-id="cbe00-159">如果它不存在，則會為您建立。</span><span class="sxs-lookup"><span data-stu-id="cbe00-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="cbe00-160">**資源群組**： 建立 hello hello 要受管理應用程式資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="cbe00-160">**resource-group**: hello resource group where hello managed application resource is created.</span></span> <span data-ttu-id="cbe00-161">hello Microsoft.Solutions/appliance 資源存在於此資源群組。</span><span class="sxs-lookup"><span data-stu-id="cbe00-161">hello Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="cbe00-162">**參數**: hello applianceMainTemplate.json 中定義的 hello 資源所需的參數。</span><span class="sxs-lookup"><span data-stu-id="cbe00-162">**parameters**: hello parameters that are needed for hello resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="cbe00-163">已知問題</span><span class="sxs-lookup"><span data-stu-id="cbe00-163">Known issues</span></span>

<span data-ttu-id="cbe00-164">此預覽版本包含下列問題的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbe00-164">This preview release includes hello following issues:</span></span>

* <span data-ttu-id="cbe00-165">500 內部伺服器錯誤會出現在 hello 建立 hello 受管理的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbe00-165">A 500 internal server error appears during hello creation of hello managed application.</span></span> <span data-ttu-id="cbe00-166">如果您遇到此問題時，很可能 toobe 間歇性。</span><span class="sxs-lookup"><span data-stu-id="cbe00-166">If you run into this issue, it's likely toobe intermittent.</span></span> <span data-ttu-id="cbe00-167">重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="cbe00-167">Retry hello operation.</span></span>
* <span data-ttu-id="cbe00-168">新的資源群組所需的 hello 受管理的資源群組。</span><span class="sxs-lookup"><span data-stu-id="cbe00-168">A new resource group is needed for hello managed resource group.</span></span> <span data-ttu-id="cbe00-169">如果您使用現有的資源群組，hello 部署將會失敗。</span><span class="sxs-lookup"><span data-stu-id="cbe00-169">If you use an existing resource group, hello deployment fails.</span></span>
* <span data-ttu-id="cbe00-170">hello 包含 hello Microsoft.Solutions/appliances 資源的資源群組必須在建立 hello **westcentralus**位置。</span><span class="sxs-lookup"><span data-stu-id="cbe00-170">hello resource group that contains hello Microsoft.Solutions/appliances resource must be created in hello **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbe00-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cbe00-171">Next steps</span></span>

* <span data-ttu-id="cbe00-172">對於簡介 toomanaged 應用程式，請參閱[受管理應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="cbe00-172">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="cbe00-173">如需發佈 Service Catalog 受管理應用程式的資訊，請參閱[建立和發佈 Service Catalog 受管理的應用程式](managed-application-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="cbe00-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="cbe00-174">發佈受管理的應用程式 toohello Azure Marketplace 的相關資訊，請參閱[Azure 受管理應用程式在 hello Marketplace](managed-application-author-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="cbe00-174">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="cbe00-175">使用來自 hello Marketplace 的受管理應用程式的相關資訊，請參閱[取用 Azure managed hello Marketplace 中的應用程式](managed-application-consume-marketplace.md)。</span><span class="sxs-lookup"><span data-stu-id="cbe00-175">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
