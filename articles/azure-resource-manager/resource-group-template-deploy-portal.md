---
title: "Azure 入口網站 toodeploy aaaUse Azure 資源 |Microsoft 文件"
description: "使用 Azure 入口網站和 Azure 資源管理 toodeploy 您的資源。"
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="e0856-103">使用 Resource Manager 範本與 Azure 入口網站來部署資源</span><span class="sxs-lookup"><span data-stu-id="e0856-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0856-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0856-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="e0856-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e0856-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="e0856-106">入口網站</span><span class="sxs-lookup"><span data-stu-id="e0856-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="e0856-107">REST API</span><span class="sxs-lookup"><span data-stu-id="e0856-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="e0856-108">本主題說明如何 toouse hello [Azure 入口網站](https://portal.azure.com)與[Azure Resource Manager](resource-group-overview.md) toodeploy 您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="e0856-108">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toodeploy your Azure resources.</span></span> <span data-ttu-id="e0856-109">toolearn 關於管理您的資源，請參閱[透過入口網站管理 Azure 資源](resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e0856-109">toolearn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="e0856-110">目前不是每次服務支援 hello 入口網站或資源管理員。</span><span class="sxs-lookup"><span data-stu-id="e0856-110">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="e0856-111">針對這些服務，您需要 toouse hello[傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="e0856-111">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="e0856-112">如需每個服務的 hello 狀態，請參閱[Azure 入口網站的可用性圖表](https://azure.microsoft.com/features/azure-portal/availability/)。</span><span class="sxs-lookup"><span data-stu-id="e0856-112">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="e0856-113">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="e0856-113">Create resource group</span></span>
1. <span data-ttu-id="e0856-114">toocreate 空的資源群組中，選取**新增** > **管理** > **資源群組**。</span><span class="sxs-lookup"><span data-stu-id="e0856-114">toocreate an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![建立空的資源群組](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="e0856-116">提供其名稱和位置，再視需要選取訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e0856-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="e0856-117">因為儲存 hello 資源的相關中繼資料與 hello 資源群組，您需要 hello 資源群組 tooprovide 位置。</span><span class="sxs-lookup"><span data-stu-id="e0856-117">You need tooprovide a location for hello resource group because hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="e0856-118">基於相容性因素，您可能想的 toospecify 儲存的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="e0856-118">For compliance reasons, you may want toospecify where that metadata is stored.</span></span> <span data-ttu-id="e0856-119">一般情況下，我們建議您指定大部分資源所在的位置。</span><span class="sxs-lookup"><span data-stu-id="e0856-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="e0856-120">使用 hello 相同位置可簡化您的範本。</span><span class="sxs-lookup"><span data-stu-id="e0856-120">Using hello same location can simplify your template.</span></span>
   
    ![設定群組值](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="e0856-122">從 Marketplace 部署資源</span><span class="sxs-lookup"><span data-stu-id="e0856-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="e0856-123">建立資源群組之後，您可以部署從 hello Marketplace 的資源 tooit。</span><span class="sxs-lookup"><span data-stu-id="e0856-123">After you create a resource group, you can deploy resources tooit from hello Marketplace.</span></span> <span data-ttu-id="e0856-124">hello Marketplace 常見案例提供預先定義的解決方案。</span><span class="sxs-lookup"><span data-stu-id="e0856-124">hello Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="e0856-125">toostart 部署中，選取**新增**和 hello 類型的資源，您想要 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="e0856-125">toostart a deployment, select **New** and hello type of resource you would like toodeploy.</span></span> <span data-ttu-id="e0856-126">然後，尋找 hello hello 資源特定版本，您想要 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="e0856-126">Then, look for hello particular version of hello resource you would like toodeploy.</span></span>
   
    ![部署資源](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="e0856-128">如果看不到您想要 toodeploy hello 特定方案，您可以為其搜尋 hello Marketplace。</span><span class="sxs-lookup"><span data-stu-id="e0856-128">If you do not see hello particular solution you would like toodeploy, you can search hello Marketplace for it.</span></span>
   
    ![搜尋 Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="e0856-130">根據選取的資源 hello 類型，您會有相關屬性 tooset 之前部署的集合。</span><span class="sxs-lookup"><span data-stu-id="e0856-130">Depending on hello type of selected resource, you have a collection of relevant properties tooset before deployment.</span></span> <span data-ttu-id="e0856-131">這些選項並未在這裡顯示，因為它們會隨著資源類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e0856-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="e0856-132">對於所有類型，您必須選取目的地資源群組。</span><span class="sxs-lookup"><span data-stu-id="e0856-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="e0856-133">hello 以下影像顯示如何 toocreate web 應用程式並將其部署 toohello 您所建立的資源群組。</span><span class="sxs-lookup"><span data-stu-id="e0856-133">hello following image shows how toocreate a web app and deploy it toohello resource group you created.</span></span>
   
    ![建立資源群組](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="e0856-135">或者，您可以在部署您的資源時，決定 toocreate 資源群組。</span><span class="sxs-lookup"><span data-stu-id="e0856-135">Alternatively, you can decide toocreate a resource group when deploying your resources.</span></span> <span data-ttu-id="e0856-136">選取**建立新**並提供 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="e0856-136">Select **Create new** and give hello resource group a name.</span></span>
   
    ![建立新的資源群組](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="e0856-138">您的部署隨即開始。</span><span class="sxs-lookup"><span data-stu-id="e0856-138">Your deployment begins.</span></span> <span data-ttu-id="e0856-139">hello 部署可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="e0856-139">hello deployment could take a few minutes.</span></span> <span data-ttu-id="e0856-140">Hello 部署完成時，您會看到通知。</span><span class="sxs-lookup"><span data-stu-id="e0856-140">When hello deployment has finished, you see a notification.</span></span>
   
    ![檢視通知](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="e0856-142">部署後您的資源，您可以加入更多資源 toohello 資源群組使用 hello**新增**hello 資源群組 刀鋒視窗上的命令。</span><span class="sxs-lookup"><span data-stu-id="e0856-142">After deploying your resources, you can add more resources toohello resource group by using hello **Add** command on hello resource group blade.</span></span>
   
    ![新增資源](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="e0856-144">從自訂範本部署資源</span><span class="sxs-lookup"><span data-stu-id="e0856-144">Deploy resources from custom template</span></span>
<span data-ttu-id="e0856-145">如果您想 tooexecute 部署，但不是使用任何 hello 範本 hello Marketplace 中，您可以建立自訂的範本，定義您方案的 hello 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="e0856-145">If you want tooexecute a deployment but not use any of hello templates in hello Marketplace, you can create a customized template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="e0856-146">toolearn 有關建立範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="e0856-146">toolearn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="e0856-147">toodeploy hello 入口網站，透過將自訂的範本選取**新增**，並開始搜尋**範本部署**直到您可以從 hello 選項中選取它。</span><span class="sxs-lookup"><span data-stu-id="e0856-147">toodeploy a customized template through hello portal, select **New**, and start searching for **Template Deployment** until you can select it from hello options.</span></span>
   
    ![搜尋範本部署](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="e0856-149">選取**範本部署**從 hello 可用的資源。</span><span class="sxs-lookup"><span data-stu-id="e0856-149">Select **Template Deployment** from hello available resources.</span></span>
   
    ![選取範本部署](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="e0856-151">在啟動 hello 範本部署之後, 開啟 hello 適用於自訂的空白範本。</span><span class="sxs-lookup"><span data-stu-id="e0856-151">After launching hello template deployment, open hello blank template that is available for customizing.</span></span>
   
    ![建立範本](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="e0856-153">在 hello 編輯器中，新增定義您想要 toodeploy hello 資源的 hello JSON 語法。</span><span class="sxs-lookup"><span data-stu-id="e0856-153">In hello editor, add hello JSON syntax that defines hello resources you want toodeploy.</span></span> <span data-ttu-id="e0856-154">完成時選取 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="e0856-154">Select **Save** when done.</span></span> <span data-ttu-id="e0856-155">如需撰寫 hello JSON 語法的指引，請參閱[資源管理員範本逐步解說](resource-manager-template-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="e0856-155">For guidance on writing hello JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![編輯範本](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="e0856-157">或者，您可以選取現有的範本從 hello [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)。</span><span class="sxs-lookup"><span data-stu-id="e0856-157">Or, you can select a pre-existing template from hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="e0856-158">這些範本是由 hello 社群貢獻。</span><span class="sxs-lookup"><span data-stu-id="e0856-158">These templates are contributed by hello community.</span></span> <span data-ttu-id="e0856-159">這些資料涵蓋許多常見的案例，和其他人可能加入的範本來嘗試 toodeploy 類似 toowhat。</span><span class="sxs-lookup"><span data-stu-id="e0856-159">They cover many common scenarios, and someone may have added a template that is similar toowhat you are trying toodeploy.</span></span> <span data-ttu-id="e0856-160">您可以搜尋 hello 範本 toofind 符合您案例的項目。</span><span class="sxs-lookup"><span data-stu-id="e0856-160">You can search hello templates toofind something that matches your scenario.</span></span>
   
    ![選取快速入門範本](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="e0856-162">您可以在 hello 編輯器中檢視 hello 選取的範本。</span><span class="sxs-lookup"><span data-stu-id="e0856-162">You can view hello selected template in hello editor.</span></span>
5. <span data-ttu-id="e0856-163">提供所有 hello 其他值之後, 選取**建立**toodeploy hello 範本。</span><span class="sxs-lookup"><span data-stu-id="e0856-163">After providing all hello other values, select **Create** toodeploy hello template.</span></span> 
   
    ![部署範本](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a><span data-ttu-id="e0856-165">部署範本儲存 tooyour 帳戶的資源</span><span class="sxs-lookup"><span data-stu-id="e0856-165">Deploy resources from a template saved tooyour account</span></span>
<span data-ttu-id="e0856-166">hello 入口網站可讓您 toosave 範本 tooyour Azure 帳戶，並稍後重新部署它。</span><span class="sxs-lookup"><span data-stu-id="e0856-166">hello portal enables you toosave a template tooyour Azure account, and redeploy it later.</span></span> <span data-ttu-id="e0856-167">如需有關使用這些儲存範本，[開始使用 hello Azure 入口網站上的私用範本](../marketplace-consumer/mytemplates-getstarted.md)。</span><span class="sxs-lookup"><span data-stu-id="e0856-167">For more information about working with these saved templates, [Get started with private templates on hello Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="e0856-168">您已儲存的範本中，選取 toofind**瀏覽** > **範本**。</span><span class="sxs-lookup"><span data-stu-id="e0856-168">toofind your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![瀏覽範本](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="e0856-170">從 hello 儲存 tooyour 帳戶的範本清單，選取您想 toowork hello。</span><span class="sxs-lookup"><span data-stu-id="e0856-170">From hello list of templates saved tooyour account, select hello one you wish toowork on.</span></span>
   
    ![已儲存的範本](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="e0856-172">選取**部署**tooredeploy 這儲存範本。</span><span class="sxs-lookup"><span data-stu-id="e0856-172">Select **Deploy** tooredeploy this saved template.</span></span>
   
    ![部署已儲存的範本](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="e0856-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e0856-174">Next steps</span></span>
* <span data-ttu-id="e0856-175">tooview 稽核記錄，請參閱 <<c0> [ 稽核與資源管理員作業](resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="e0856-175">tooview audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="e0856-176">tootroubleshoot 部署錯誤，請參閱[檢視部署作業](resource-manager-deployment-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="e0856-176">tootroubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="e0856-177">tooretrieve 範本部署或資源群組，請參閱[匯出 Azure 資源管理員範本，從現有的資源](resource-manager-export-template.md)。</span><span class="sxs-lookup"><span data-stu-id="e0856-177">tooretrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="e0856-178">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="e0856-178">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

