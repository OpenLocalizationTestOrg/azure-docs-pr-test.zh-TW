---
title: "使用 Azure 入口網站部署 Azure 資源 | Microsoft Docs"
description: "使用 Azure 入口網站和 Azure Resource Manager 來部署資源。"
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
ms.openlocfilehash: a4cac5834c667976b0a2d1f2748e4309a166d16a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="b194e-103">使用 Resource Manager 範本與 Azure 入口網站來部署資源</span><span class="sxs-lookup"><span data-stu-id="b194e-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b194e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b194e-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="b194e-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b194e-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="b194e-106">入口網站</span><span class="sxs-lookup"><span data-stu-id="b194e-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="b194e-107">REST API</span><span class="sxs-lookup"><span data-stu-id="b194e-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="b194e-108">本主題示範如何使用 [Azure 入口網站](https://portal.azure.com)搭配 [Azure Resource Manager](resource-group-overview.md) 來部署您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="b194e-108">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to deploy your Azure resources.</span></span> <span data-ttu-id="b194e-109">若要了解如何管理您的資源，請參閱 [透過入口網站管理 Azure 資源](resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="b194e-109">To learn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="b194e-110">目前並非所有服務都支援入口網站或資源管理員。</span><span class="sxs-lookup"><span data-stu-id="b194e-110">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="b194e-111">針對這些服務，您必須使用 [傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="b194e-111">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="b194e-112">如需每個服務的狀態，請參閱 [Azure 入口網站可用性圖表](https://azure.microsoft.com/features/azure-portal/availability/)。</span><span class="sxs-lookup"><span data-stu-id="b194e-112">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="b194e-113">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="b194e-113">Create resource group</span></span>
1. <span data-ttu-id="b194e-114">若要建立空的資源群組，請選取 [新增] > [管理] > [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="b194e-114">To create an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![建立空的資源群組](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="b194e-116">提供其名稱和位置，再視需要選取訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b194e-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="b194e-117">您需要提供資源群組的位置，因為資源群組會儲存資源的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="b194e-117">You need to provide a location for the resource group because the resource group stores metadata about the resources.</span></span> <span data-ttu-id="b194e-118">為了符合法規，您可能會想要指定中繼資料的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="b194e-118">For compliance reasons, you may want to specify where that metadata is stored.</span></span> <span data-ttu-id="b194e-119">一般情況下，我們建議您指定大部分資源所在的位置。</span><span class="sxs-lookup"><span data-stu-id="b194e-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="b194e-120">使用相同位置可簡化範本。</span><span class="sxs-lookup"><span data-stu-id="b194e-120">Using the same location can simplify your template.</span></span>
   
    ![設定群組值](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="b194e-122">從 Marketplace 部署資源</span><span class="sxs-lookup"><span data-stu-id="b194e-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="b194e-123">建立資源群組之後，您可以將資源從 Marketplace 部署至該群組。</span><span class="sxs-lookup"><span data-stu-id="b194e-123">After you create a resource group, you can deploy resources to it from the Marketplace.</span></span> <span data-ttu-id="b194e-124">Marketplace 針對常見的案例提供預先定義的解決方案。</span><span class="sxs-lookup"><span data-stu-id="b194e-124">The Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="b194e-125">若要開始部署，請選取 [新增]  以及您想要部署的資源類型。</span><span class="sxs-lookup"><span data-stu-id="b194e-125">To start a deployment, select **New** and the type of resource you would like to deploy.</span></span> <span data-ttu-id="b194e-126">然後，尋找您要部署的特定版本資源。</span><span class="sxs-lookup"><span data-stu-id="b194e-126">Then, look for the particular version of the resource you would like to deploy.</span></span>
   
    ![部署資源](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="b194e-128">如果沒有看到要部署的特定解決方案，您可以在 Marketplace 搜尋。</span><span class="sxs-lookup"><span data-stu-id="b194e-128">If you do not see the particular solution you would like to deploy, you can search the Marketplace for it.</span></span>
   
    ![搜尋 Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="b194e-130">根據所選資源的類型，您必須在部署前設定相關的屬性集合。</span><span class="sxs-lookup"><span data-stu-id="b194e-130">Depending on the type of selected resource, you have a collection of relevant properties to set before deployment.</span></span> <span data-ttu-id="b194e-131">這些選項並未在這裡顯示，因為它們會隨著資源類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="b194e-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="b194e-132">對於所有類型，您必須選取目的地資源群組。</span><span class="sxs-lookup"><span data-stu-id="b194e-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="b194e-133">下圖顯示如何建立 Web 應用程式並將其部署至您建立的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b194e-133">The following image shows how to create a web app and deploy it to the resource group you created.</span></span>
   
    ![建立資源群組](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="b194e-135">或者，您也可以決定在部署資源時建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="b194e-135">Alternatively, you can decide to create a resource group when deploying your resources.</span></span> <span data-ttu-id="b194e-136">選取 [新建]  並提供資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="b194e-136">Select **Create new** and give the resource group a name.</span></span>
   
    ![建立新的資源群組](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="b194e-138">您的部署隨即開始。</span><span class="sxs-lookup"><span data-stu-id="b194e-138">Your deployment begins.</span></span> <span data-ttu-id="b194e-139">部署可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="b194e-139">The deployment could take a few minutes.</span></span> <span data-ttu-id="b194e-140">部署完成後，您就會看到通知。</span><span class="sxs-lookup"><span data-stu-id="b194e-140">When the deployment has finished, you see a notification.</span></span>
   
    ![檢視通知](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="b194e-142">部署您的資源之後，您可以在資源群組刀鋒視窗上使用 [新增]  命令，將更多資源新增至資源群組。</span><span class="sxs-lookup"><span data-stu-id="b194e-142">After deploying your resources, you can add more resources to the resource group by using the **Add** command on the resource group blade.</span></span>
   
    ![新增資源](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="b194e-144">從自訂範本部署資源</span><span class="sxs-lookup"><span data-stu-id="b194e-144">Deploy resources from custom template</span></span>
<span data-ttu-id="b194e-145">如果您想要執行部署，但不使用 Marketplace 中的任何範本，您可建立自訂範本以定義您的解決方案的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="b194e-145">If you want to execute a deployment but not use any of the templates in the Marketplace, you can create a customized template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="b194e-146">若要了解如何建立範本，請參閱 [撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="b194e-146">To learn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="b194e-147">若要透過入口網站來部署自訂的範本，請選取 [新增]，並開始搜尋 [範本部署]，直到您可以從選項中選取它為止。</span><span class="sxs-lookup"><span data-stu-id="b194e-147">To deploy a customized template through the portal, select **New**, and start searching for **Template Deployment** until you can select it from the options.</span></span>
   
    ![搜尋範本部署](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="b194e-149">從可用的資源中選取 [範本部署]  。</span><span class="sxs-lookup"><span data-stu-id="b194e-149">Select **Template Deployment** from the available resources.</span></span>
   
    ![選取範本部署](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="b194e-151">啟動範本部署之後，開啟可供自訂的空白範本。</span><span class="sxs-lookup"><span data-stu-id="b194e-151">After launching the template deployment, open the blank template that is available for customizing.</span></span>
   
    ![建立範本](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="b194e-153">在編輯器中，新增定義要部署資源的 JSON 語法。</span><span class="sxs-lookup"><span data-stu-id="b194e-153">In the editor, add the JSON syntax that defines the resources you want to deploy.</span></span> <span data-ttu-id="b194e-154">完成時選取 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="b194e-154">Select **Save** when done.</span></span> <span data-ttu-id="b194e-155">如需撰寫 JSON 語法的指導方針，請參閱 [Resource Manager 範本逐步解說](resource-manager-template-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="b194e-155">For guidance on writing the JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![編輯範本](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="b194e-157">或者，您可以從 [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)選取既存的範本。</span><span class="sxs-lookup"><span data-stu-id="b194e-157">Or, you can select a pre-existing template from the [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="b194e-158">這些範本是由社群所貢獻。</span><span class="sxs-lookup"><span data-stu-id="b194e-158">These templates are contributed by the community.</span></span> <span data-ttu-id="b194e-159">其中涵蓋許多常見案例，而其他人可能會新增類似於您嘗試部署的範本。</span><span class="sxs-lookup"><span data-stu-id="b194e-159">They cover many common scenarios, and someone may have added a template that is similar to what you are trying to deploy.</span></span> <span data-ttu-id="b194e-160">您可以搜尋範本以找出符合您的案例的範本。</span><span class="sxs-lookup"><span data-stu-id="b194e-160">You can search the templates to find something that matches your scenario.</span></span>
   
    ![選取快速入門範本](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="b194e-162">您可以在編輯器中檢視選取的範本。</span><span class="sxs-lookup"><span data-stu-id="b194e-162">You can view the selected template in the editor.</span></span>
5. <span data-ttu-id="b194e-163">提供所有其他的值之後，請選取 [建立]  來部署範本。</span><span class="sxs-lookup"><span data-stu-id="b194e-163">After providing all the other values, select **Create** to deploy the template.</span></span> 
   
    ![部署範本](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-to-your-account"></a><span data-ttu-id="b194e-165">從儲存至您帳戶的範本部署資源</span><span class="sxs-lookup"><span data-stu-id="b194e-165">Deploy resources from a template saved to your account</span></span>
<span data-ttu-id="b194e-166">入口網站可讓您將範本儲存至您的 Azure 帳戶，並於日後部署它。</span><span class="sxs-lookup"><span data-stu-id="b194e-166">The portal enables you to save a template to your Azure account, and redeploy it later.</span></span> <span data-ttu-id="b194e-167">如需使用這些已儲存範本的詳細資訊，請參閱 [開始在 Azure 入口網站上使用私人範本](../marketplace-consumer/mytemplates-getstarted.md)。</span><span class="sxs-lookup"><span data-stu-id="b194e-167">For more information about working with these saved templates, [Get started with private templates on the Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="b194e-168">若要尋找您已儲存的範本，請選取 [瀏覽] > [範本]。</span><span class="sxs-lookup"><span data-stu-id="b194e-168">To find your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![瀏覽範本](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="b194e-170">在儲存至您帳戶的範本清單中，選取您要使用的範本。</span><span class="sxs-lookup"><span data-stu-id="b194e-170">From the list of templates saved to your account, select the one you wish to work on.</span></span>
   
    ![已儲存的範本](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="b194e-172">選取 [部署]  來重新部署這個已儲存的範本。</span><span class="sxs-lookup"><span data-stu-id="b194e-172">Select **Deploy** to redeploy this saved template.</span></span>
   
    ![部署已儲存的範本](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="b194e-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b194e-174">Next steps</span></span>
* <span data-ttu-id="b194e-175">若要檢視稽核記錄檔，請參閱 [使用 Resource Manager 來稽核作業](resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="b194e-175">To view audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="b194e-176">若要針對部署錯誤進行疑難排解，請參閱[檢視部署作業](resource-manager-deployment-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="b194e-176">To troubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="b194e-177">若要從部署或資源群組擷取範本，請參閱 [從現有資源匯出 Azure Resource Manager 範本](resource-manager-export-template.md)。</span><span class="sxs-lookup"><span data-stu-id="b194e-177">To retrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="b194e-178">如需關於企業如何使用 Resource Manager 有效地管理訂用帳戶的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="b194e-178">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

