---
title: "Azure 入口網站 toomanage aaaUse Azure 資源 |Microsoft 文件"
description: "使用 Azure 入口網站和 Azure 資源管理 toomanage 您的資源。 示範如何使用儀表板 toomonitor 資源 toowork。"
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="139c5-104">透過入口網站管理 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="139c5-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="139c5-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="139c5-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="139c5-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="139c5-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="139c5-107">入口網站</span><span class="sxs-lookup"><span data-stu-id="139c5-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="139c5-108">REST API</span><span class="sxs-lookup"><span data-stu-id="139c5-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="139c5-109">本主題說明如何 toouse hello [Azure 入口網站](https://portal.azure.com)與[Azure Resource Manager](resource-group-overview.md) toomanage 您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="139c5-109">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toomanage your Azure resources.</span></span> <span data-ttu-id="139c5-110">toolearn 有關部署資源，透過 hello 入口網站，請參閱[部署具有資源管理員範本和 Azure 入口網站資源](resource-group-template-deploy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="139c5-110">toolearn about deploying resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="139c5-111">目前不是每次服務支援 hello 入口網站或資源管理員。</span><span class="sxs-lookup"><span data-stu-id="139c5-111">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="139c5-112">針對這些服務，您需要 toouse hello[傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="139c5-112">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="139c5-113">如需每個服務的 hello 狀態，請參閱[Azure 入口網站的可用性圖表](https://azure.microsoft.com/features/azure-portal/availability/)。</span><span class="sxs-lookup"><span data-stu-id="139c5-113">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="139c5-114">管理資源群組</span><span class="sxs-lookup"><span data-stu-id="139c5-114">Manage resource groups</span></span>

<span data-ttu-id="139c5-115">資源群組是存放 Azure 方案相關資源的容器。</span><span class="sxs-lookup"><span data-stu-id="139c5-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="139c5-116">hello 資源群組可包含 hello 方案的所有 hello 資源或您想 toomanage 為群組的資源。</span><span class="sxs-lookup"><span data-stu-id="139c5-116">hello resource group can include all hello resources for hello solution, or only those resources that you want toomanage as a group.</span></span> <span data-ttu-id="139c5-117">您決定要如何 tooallocate 資源 tooresource 根據錯誤群組構成 hello 最適合您的組織。</span><span class="sxs-lookup"><span data-stu-id="139c5-117">You decide how you want tooallocate resources tooresource groups based on what makes hello most sense for your organization.</span></span> <span data-ttu-id="139c5-118">一般而言，加入共用 hello 資源相同的生命週期 toohello 相同資源群組，因此您可以輕鬆地部署、 更新和刪除它們做為群組。</span><span class="sxs-lookup"><span data-stu-id="139c5-118">Generally, add resources that share hello same lifecycle toohello same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="139c5-119">hello 資源群組，儲存 hello 資源的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="139c5-119">hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="139c5-120">因此，當您指定 hello 資源群組的位置，就指定儲存的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="139c5-120">Therefore, when you specify a location for hello resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="139c5-121">基於相容性因素，您可能需要 tooensure 資料儲存在特定區域中。</span><span class="sxs-lookup"><span data-stu-id="139c5-121">For compliance reasons, you may need tooensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="139c5-122">所有的 hello 資源群組，在您的訂用帳戶中，選取 toosee**資源群組**。</span><span class="sxs-lookup"><span data-stu-id="139c5-122">toosee all hello resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![瀏覽資源群組](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="139c5-124">toocreate 空的資源群組中，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="139c5-124">toocreate an empty resource group, select **Add**.</span></span>
   
    ![新增資源群組](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="139c5-126">提供的名稱和位置 hello 新資源群組。</span><span class="sxs-lookup"><span data-stu-id="139c5-126">Provide a name and location for hello new resource group.</span></span> <span data-ttu-id="139c5-127">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="139c5-127">Select **Create**.</span></span>
   
    ![建立資源群組](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="139c5-129">您可能需要 tooselect**重新整理**toosee hello 最近已建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="139c5-129">You may need tooselect **Refresh** toosee hello recently created resource group.</span></span>
   
    ![重新整理資源群組](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="139c5-131">選取針對您的資源群組，顯示 toocustomize hello 資訊**資料行**。</span><span class="sxs-lookup"><span data-stu-id="139c5-131">toocustomize hello information displayed for your resource groups, select **Columns**.</span></span>
   
    ![自訂資料行](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="139c5-133">選取 hello 資料行 tooadd，，然後選取**更新**。</span><span class="sxs-lookup"><span data-stu-id="139c5-133">Select hello columns tooadd, and then select **Update**.</span></span>
   
    ![新增資料行](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="139c5-135">toolearn 有關部署資源 tooyour 新資源群組，請參閱[部署具有資源管理員範本和 Azure 入口網站資源](resource-group-template-deploy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="139c5-135">toolearn about deploying resources tooyour new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="139c5-136">快速存取 tooa 資源群組，您可以釘選 hello 刀鋒視窗 tooyour 儀表板。</span><span class="sxs-lookup"><span data-stu-id="139c5-136">For quick access tooa resource group, you can pin hello blade tooyour dashboard.</span></span>
   
    ![釘選資源群組](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="139c5-138">hello 儀表板會顯示 hello 資源群組和其資源。</span><span class="sxs-lookup"><span data-stu-id="139c5-138">hello dashboard displays hello resource group and its resources.</span></span> <span data-ttu-id="139c5-139">您可以選取 hello 資源群組或任何其資源 toonavigate toohello 項目。</span><span class="sxs-lookup"><span data-stu-id="139c5-139">You can select either hello resource groups or any of its resources toonavigate toohello item.</span></span>
   
    ![釘選資源群組](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="139c5-141">標記資源</span><span class="sxs-lookup"><span data-stu-id="139c5-141">Tag resources</span></span>
<span data-ttu-id="139c5-142">您可以套用標籤 tooresource 群組和資源 toologically 組織您的資產。</span><span class="sxs-lookup"><span data-stu-id="139c5-142">You can apply tags tooresource groups and resources toologically organize your assets.</span></span> <span data-ttu-id="139c5-143">如需有關使用標記資訊，請參閱[使用標記 tooorganize 您的 Azure 資源](resource-group-using-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="139c5-143">For information about working with tags, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="139c5-144">監視資源</span><span class="sxs-lookup"><span data-stu-id="139c5-144">Monitor resources</span></span>
<span data-ttu-id="139c5-145">當您選取的資源時，hello 資源刀鋒視窗會顯示預設圖形和監視該資源類型的資料表。</span><span class="sxs-lookup"><span data-stu-id="139c5-145">When you select a resource, hello resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="139c5-146">選取資源，並注意 hello**監視**> 一節。</span><span class="sxs-lookup"><span data-stu-id="139c5-146">Select a resource and notice hello **Monitoring** section.</span></span> <span data-ttu-id="139c5-147">它包含相關 toohello 資源類型的圖形。</span><span class="sxs-lookup"><span data-stu-id="139c5-147">It includes graphs that are relevant toohello resource type.</span></span> <span data-ttu-id="139c5-148">hello 下列影像顯示 hello 預設的監視儲存體帳戶的資料。</span><span class="sxs-lookup"><span data-stu-id="139c5-148">hello following image shows hello default monitoring data for a storage account.</span></span>
   
    ![顯示監視](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="139c5-150">您可以藉由選取 hello 區段上方 hello 省略符號 （...） 釘選一段 hello 刀鋒視窗 tooyour 儀表板。</span><span class="sxs-lookup"><span data-stu-id="139c5-150">You can pin a section of hello blade tooyour dashboard by selecting hello ellipsis (...) above hello section.</span></span> <span data-ttu-id="139c5-151">您也可以自訂在 hello 刀鋒視窗中的 hello 大小 hello 區段，或將它完全移除。</span><span class="sxs-lookup"><span data-stu-id="139c5-151">You can also customize hello size hello section in hello blade or remove it completely.</span></span> <span data-ttu-id="139c5-152">hello 下列影像顯示 toopin，如何自訂或移除 hello CPU 與記憶體 > 一節。</span><span class="sxs-lookup"><span data-stu-id="139c5-152">hello following image shows how toopin, customize, or remove hello CPU and Memory section.</span></span>
   
    ![釘選區段](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="139c5-154">釘選 hello 區段 toohello 儀表板，您會看到摘要 hello hello 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="139c5-154">After pinning hello section toohello dashboard, you will see hello summary on hello dashboard.</span></span> <span data-ttu-id="139c5-155">此外，立即將它選取會帶您 toomore hello 資料的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="139c5-155">And, selecting it immediately takes you toomore details about hello data.</span></span>
   
    ![檢視儀表板](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="139c5-157">toocompletely 自訂 hello 資料監視透過 hello 入口網站，瀏覽 tooyour 預設儀表板，並選取**新儀表板**。</span><span class="sxs-lookup"><span data-stu-id="139c5-157">toocompletely customize hello data you monitor through hello portal, navigate tooyour default dashboard, and select **New dashboard**.</span></span>
   
    ![儀表板](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="139c5-159">提供新儀表板名稱，然後拖曳 hello 儀表板的磚。</span><span class="sxs-lookup"><span data-stu-id="139c5-159">Give your new dashboard a name and drag tiles onto hello dashboard.</span></span> <span data-ttu-id="139c5-160">hello 圖格被篩選的不同選項。</span><span class="sxs-lookup"><span data-stu-id="139c5-160">hello tiles are filtered by different options.</span></span>
   
    ![儀表板](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="139c5-162">toolearn 關於使用 儀表板，請參閱[建立和共用 hello Azure 入口網站的儀表板](../azure-portal/azure-portal-dashboards.md)。</span><span class="sxs-lookup"><span data-stu-id="139c5-162">toolearn about working with dashboards, see [Creating and sharing dashboards in hello Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="139c5-163">管理資源</span><span class="sxs-lookup"><span data-stu-id="139c5-163">Manage resources</span></span>
<span data-ttu-id="139c5-164">在 hello 刀鋒視窗中的資源，您會看到管理 hello 資源 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="139c5-164">In hello blade for a resource, you see hello options for managing hello resource.</span></span> <span data-ttu-id="139c5-165">hello 入口網站會顯示該特定資源類型的管理選項。</span><span class="sxs-lookup"><span data-stu-id="139c5-165">hello portal presents management options for that particular resource type.</span></span> <span data-ttu-id="139c5-166">您可以看到 hello 的上方 hello 資源刀鋒視窗和 hello 左邊 hello 管理命令。</span><span class="sxs-lookup"><span data-stu-id="139c5-166">You see hello management commands across hello top of hello resource blade and on hello left side.</span></span>

![管理資源](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="139c5-168">您可以從這些選項中，執行作業，例如啟動和停止虛擬機器，或是重新設定 hello hello 虛擬機器的屬性。</span><span class="sxs-lookup"><span data-stu-id="139c5-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring hello properties of hello virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="139c5-169">移動資源</span><span class="sxs-lookup"><span data-stu-id="139c5-169">Move resources</span></span>
<span data-ttu-id="139c5-170">如果您需要 toomove 資源 tooanother 資源群組或其他訂用帳戶，請參閱[移動資源 toonew 資源群組或訂用帳戶](resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="139c5-170">If you need toomove resources tooanother resource group or another subscription, see [Move resources toonew resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="139c5-171">鎖定資源</span><span class="sxs-lookup"><span data-stu-id="139c5-171">Lock resources</span></span>
<span data-ttu-id="139c5-172">您可以鎖定訂用帳戶、 資源群組或資源 tooprevent 其他使用者不小心刪除或修改重要的資源組織中。</span><span class="sxs-lookup"><span data-stu-id="139c5-172">You can lock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="139c5-173">如需詳細資訊，請參閱[使用 Azure Resource Manager 來鎖定資源](resource-group-lock-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="139c5-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="139c5-174">檢視訂用帳戶和成本</span><span class="sxs-lookup"><span data-stu-id="139c5-174">View your subscription and costs</span></span>
<span data-ttu-id="139c5-175">您可以檢視您的訂用帳戶和 hello 彙總成本的相關資訊的所有資源。</span><span class="sxs-lookup"><span data-stu-id="139c5-175">You can view information about your subscription and hello rolled-up costs for all your resources.</span></span> <span data-ttu-id="139c5-176">選取**訂閱**和您想要 toosee hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="139c5-176">Select **Subscriptions** and hello subscription you want toosee.</span></span> <span data-ttu-id="139c5-177">您可能只有一個訂用帳戶 tooselect。</span><span class="sxs-lookup"><span data-stu-id="139c5-177">You might only have one subscription tooselect.</span></span>

![訂用帳戶](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="139c5-179">Hello 訂用帳戶 刀鋒視窗中，您會看到完工速率。</span><span class="sxs-lookup"><span data-stu-id="139c5-179">Within hello subscription blade, you see a burn rate.</span></span>

![完工速率](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="139c5-181">還有依資源類型的成本分析。</span><span class="sxs-lookup"><span data-stu-id="139c5-181">And, a breakdown of costs by resource type.</span></span>

![資源成本](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="139c5-183">匯出範本</span><span class="sxs-lookup"><span data-stu-id="139c5-183">Export template</span></span>
<span data-ttu-id="139c5-184">設定好您的資源群組之後，您可能想 tooview hello Resource Manager 範本 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="139c5-184">After setting up your resource group, you may want tooview hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="139c5-185">匯出的 hello 範本提供兩個優點：</span><span class="sxs-lookup"><span data-stu-id="139c5-185">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="139c5-186">您可以輕鬆地自動化未來 hello 方案的部署，因為 hello 範本包含所有與 hello 完整的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="139c5-186">You can easily automate future deployments of hello solution because hello template contains all hello complete infrastructure.</span></span>
2. <span data-ttu-id="139c5-187">您先熟悉樣板語法藉由查看 hello JavaScript Object Notation (JSON) 表示您的方案。</span><span class="sxs-lookup"><span data-stu-id="139c5-187">You can become familiar with template syntax by looking at hello JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="139c5-188">如需逐步指引，請參閱 [從現有資源匯出 Azure Resource Manager 範本](resource-manager-export-template.md)。</span><span class="sxs-lookup"><span data-stu-id="139c5-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="139c5-189">刪除資源群組或資源</span><span class="sxs-lookup"><span data-stu-id="139c5-189">Delete resource group or resources</span></span>
<span data-ttu-id="139c5-190">刪除資源群組會刪除所有內含的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="139c5-190">Deleting a resource group deletes all hello resources contained within it.</span></span> <span data-ttu-id="139c5-191">您也可以刪除資源群組內的個別資源。</span><span class="sxs-lookup"><span data-stu-id="139c5-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="139c5-192">當您刪除資源群組，因為其他資源群組中的連結的 tooit 可能有資源時，您會想 tooexercise 警告。</span><span class="sxs-lookup"><span data-stu-id="139c5-192">You want tooexercise caution when you delete a resource group because there might be resources in other resource groups that are linked tooit.</span></span> <span data-ttu-id="139c5-193">資源管理員不會刪除連結的資源，但它們可能無法正常運作不含預期的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="139c5-193">Resource Manager does not delete linked resources, but they may not operate correctly without hello expected resources.</span></span>

![刪除群組](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="139c5-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="139c5-195">Next steps</span></span>
* <span data-ttu-id="139c5-196">tooview 活動記錄，請參閱 <<c0> [ 稽核與資源管理員作業](resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="139c5-196">tooview activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="139c5-197">tooview 部署的詳細資訊，請參閱[檢視部署作業](resource-manager-deployment-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="139c5-197">tooview details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="139c5-198">hello 入口網站，透過 toodeploy 資源，請參閱[部署具有資源管理員範本和 Azure 入口網站資源](resource-group-template-deploy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="139c5-198">toodeploy resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="139c5-199">toomanage 存取 tooresources，請參閱[使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="139c5-199">toomanage access tooresources, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="139c5-200">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="139c5-200">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

