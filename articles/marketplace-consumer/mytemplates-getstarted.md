---
title: "開始使用私人範本 | Microsoft Docs"
description: "使用 Azure 入口網站、Azure CLI 或 PowerShell 新增、管理及共用私人範本。"
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 01657619cbe579c6818a790cc3ab95a33936a565
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-private-templates-on-the-azure-portal"></a><span data-ttu-id="f9bdd-103">開始在 Azure 入口網站上使用私人範本</span><span class="sxs-lookup"><span data-stu-id="f9bdd-103">Get started with private Templates on the Azure Portal</span></span>
<span data-ttu-id="f9bdd-104">[Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) 範本是用來定義您的部署的宣告式範本。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used to define your deployment.</span></span> <span data-ttu-id="f9bdd-105">您可以定義要對解決方案部署的資源，並指定可讓您針對不同環境輸入值的參數和變數。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-105">You can define the resources to deploy for a solution, and specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="f9bdd-106">範本由 JSON 與運算式所組成，可讓您用來為部署建構值。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-106">The template consists of JSON and expressions which you can use to construct values for your deployment.</span></span>

<span data-ttu-id="f9bdd-107">您可以在 [Azure 入口網站](https://portal.azure.com)中使用的新 [範本] 功能，並以 **Microsoft.Gallery** 資源提供者作為 [Azure Marketplace](https://azure.microsoft.com/marketplace/) 的擴充功能，讓使用者得以從個人程式庫建立、管理和部署私人範本。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-107">You can use the new **Templates** capability in the [Azure Portal](https://portal.azure.com) along with the **Microsoft.Gallery** resource provider as an extension of the [Azure Marketplace](https://azure.microsoft.com/marketplace/) to enable users to create, manage and deploy private templates from a personal library.</span></span>

<span data-ttu-id="f9bdd-108">本文將逐步引導您使用 Azure 入口網站來新增、管理及共用私人 **範本** 。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-108">This document walks you through adding, managing and sharing a private **Template** using the Azure Portal.</span></span>

## <a name="guidance"></a><span data-ttu-id="f9bdd-109">指引</span><span class="sxs-lookup"><span data-stu-id="f9bdd-109">Guidance</span></span>
<span data-ttu-id="f9bdd-110">下列建議將協助您在使用您的方案時充分利用 **範本** ：</span><span class="sxs-lookup"><span data-stu-id="f9bdd-110">The following suggestions will help you take full advantage of **Templates** when working with your solutions:</span></span>

* <span data-ttu-id="f9bdd-111">**範本** 是一項封裝資源，其中包含 Resource Manager 範本和其他中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span></span> <span data-ttu-id="f9bdd-112">其操作方式非常類似 Marketplace 中的項目。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-112">It behaves very similarly to an item in the Marketplace.</span></span> <span data-ttu-id="f9bdd-113">主要差別在於它是私人項目 (相對於公用 Marketplace 項目)。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-113">The key difference is that it is a private item as opposed to the public Marketplace items.</span></span>
* <span data-ttu-id="f9bdd-114">**範本** 程式庫適用於需要自訂其部署的使用者。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-114">The **Templates** library works well for users who need to customize their deployments.</span></span>
* <span data-ttu-id="f9bdd-115">**範本** 適用於在 Azure 中需要簡單儲存機制的使用者。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-115">**Templates** work well for users who need a simple repository within Azure.</span></span>
* <span data-ttu-id="f9bdd-116">開始使用現有的 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-116">Start with an existing Resource Manager template.</span></span> <span data-ttu-id="f9bdd-117">在 [github](https://github.com/Azure/azure-quickstart-templates) 中尋找範本，或從現有資源群組[匯出範本](../azure-resource-manager/resource-manager-export-template.md)。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span></span>
* <span data-ttu-id="f9bdd-118">**範本** 會繫結至發佈它們的使用者。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-118">**Templates** are tied to the user who publishes them.</span></span> <span data-ttu-id="f9bdd-119">每個具有範本讀取權限的使用者都可以看到發佈者名稱。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-119">The publisher name is visible to everyone who has read access to it.</span></span>
* <span data-ttu-id="f9bdd-120">**範本** 是 Resource Manager 資源，一旦發佈便無法重新命名。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span></span>

## <a name="add-a-template-resource"></a><span data-ttu-id="f9bdd-121">新增範本資源</span><span class="sxs-lookup"><span data-stu-id="f9bdd-121">Add a Template resource</span></span>
<span data-ttu-id="f9bdd-122">在 Azure 入口網站中建立 **範本** 資源的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-122">There are two ways to create a **Template** resource in the Azure portal.</span></span>

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a><span data-ttu-id="f9bdd-123">方法 1︰從執行中的資源群組建立新的範本資源</span><span class="sxs-lookup"><span data-stu-id="f9bdd-123">Method 1 : Create a new Template resource from a running resource group</span></span>
1. <span data-ttu-id="f9bdd-124">瀏覽至 Azure 入口網站上的現有資源群組。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-124">Navigate to an existing resource group on the Azure Portal.</span></span> <span data-ttu-id="f9bdd-125">在 [設定] 中選取 [匯出範本]。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-125">Select **Export template** in **Settings**.</span></span>
2. <span data-ttu-id="f9bdd-126">匯出 Resource Manager 範本後，使用 [儲存範本] 按鈕將它儲存到 [範本] 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-126">Once the Resource Manager template is exported, use the **Save Template** button to save it to the **Templates** repository.</span></span> <span data-ttu-id="f9bdd-127">在 [這裡](../azure-resource-manager/resource-manager-export-template.md)尋找匯出範本的完整詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span></span>
   <br /><br /><span data-ttu-id="f9bdd-128">
   ![資源群組匯出](media/rg-export-portal1.PNG)</span><span class="sxs-lookup"><span data-stu-id="f9bdd-128">
![Resource group export](media/rg-export-portal1.PNG)</span></span>  <br />
3. <span data-ttu-id="f9bdd-129">選取 [儲存至範本]  命令按鈕。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-129">Select the **Save to Template** command button.</span></span>
   <br /><br />
4. <span data-ttu-id="f9bdd-130">輸入以下資訊：</span><span class="sxs-lookup"><span data-stu-id="f9bdd-130">Enter the following information:</span></span>
   
   * <span data-ttu-id="f9bdd-131">名稱 – 範本物件的名稱 (注意︰這是以 Azure Resource Manager 為基礎的名稱。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-131">Name – Name of the template object (NOTE: This is an Azure Resource Manager based name.</span></span> <span data-ttu-id="f9bdd-132">適用所有命名限制，一旦建立便無法變更)。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-132">All naming restrictions apply and it cannot be changed once created).</span></span>
   * <span data-ttu-id="f9bdd-133">說明 – 關於此範本的簡短摘要。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-133">Description – Quick summary about the template.</span></span>
     
     ![儲存範本](media/save-template-portal1.PNG)  <br />
5. <span data-ttu-id="f9bdd-135">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-135">Click **Save**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f9bdd-136">[匯出範本] 刀鋒視窗會在匯出的 Resource Manager 範本有誤時顯示通知，但您仍可將此 Resource Manager 範本儲存至 [範本]。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-136">The Export template blade shows notifications when the exported Resource Manager template has errors, but you will still be able to save this Resource Manager template to the Templates.</span></span> <span data-ttu-id="f9bdd-137">請確保在重新部署已匯出的 Resource Manager 範本之前，先檢查並修正所有的 Resource Manager 範本問題。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-137">Ensure that you check and fix any Resource Manager template issues before redeploying the exported Resource Manager template.</span></span>
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a><span data-ttu-id="f9bdd-138">方法 2 ︰從瀏覽加入新的範本資源</span><span class="sxs-lookup"><span data-stu-id="f9bdd-138">Method 2 : Add a new Template resource from browse</span></span>
<span data-ttu-id="f9bdd-139">您也可以在 [瀏覽] > [範本] 中使用 [+新增] 命令按鈕，從頭新增**範本**。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-139">You can also add a new **Template** from scratch using the +Add command button in **Browse > Templates**.</span></span> <span data-ttu-id="f9bdd-140">您必須提供 [名稱]、[說明] 和 Resource Manager 範本 JSON。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-140">You will need to provide a Name, Description and the Resource Manager template JSON.</span></span>

![新增範本](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> <span data-ttu-id="f9bdd-142">Microsoft.Gallery 是以租用戶為基礎的 Azure 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span></span> <span data-ttu-id="f9bdd-143">[範本] 資源會繫結至建立它的使用者。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-143">The Template resource is tied to the user who created it.</span></span> <span data-ttu-id="f9bdd-144">但不會繫結至任何特定的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-144">It is not tied to any specific subscription.</span></span> <span data-ttu-id="f9bdd-145">只有在部署範本時才需要選擇訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-145">A subscription needs to be chosen only when deploying a Template.</span></span>
> 
> 

## <a name="view-template-resources"></a><span data-ttu-id="f9bdd-146">檢視範本資源</span><span class="sxs-lookup"><span data-stu-id="f9bdd-146">View Template resources</span></span>
<span data-ttu-id="f9bdd-147">在 [瀏覽 > 範本] 可以看見您可用的所有**範本**。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-147">All **Templates** available to you can be seen at **Browse > Templates**.</span></span> <span data-ttu-id="f9bdd-148">這包括您所建立的**範本**以及利用各種權限層級與您共用的範本。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span></span> <span data-ttu-id="f9bdd-149">如需詳細資料，請參閱下面的[存取控制](#access-control-for-a-tenant-resource-provider)一節。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-149">More details in the [access control](#access-control-for-a-tenant-resource-provider) section below.</span></span>

![檢視範本](media/view-template-portal1.PNG)  <br />

<span data-ttu-id="f9bdd-151">按一下清單中的項目，即可檢視 **範本** 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-151">You can view the details of a **Template** by clicking into an item in the list.</span></span>

![檢視範本](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a><span data-ttu-id="f9bdd-153">編輯範本資源</span><span class="sxs-lookup"><span data-stu-id="f9bdd-153">Edit a Template resource</span></span>
<span data-ttu-id="f9bdd-154">以滑鼠右鍵按一下瀏覽清單上的項目，或選擇 [編輯] 命令按鈕，即可起始 **範本** 的編輯流程。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-154">You can initiate the edit flow for a **Template** by right clicking the item on the Browse list or by choosing the Edit command button.</span></span>

![編輯範本](media/edit-template-portal1a.PNG)  <br />

<span data-ttu-id="f9bdd-156">您可以編輯說明或 Resource Manager 範本文字。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-156">You can edit the description or Resource Manager template text.</span></span> <span data-ttu-id="f9bdd-157">但無法編輯名稱，因為這是 Resource Manager 資源名稱。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-157">You cannot edit the name since it is an Resource Manager resource name.</span></span> <span data-ttu-id="f9bdd-158">當您編輯 Resource Manager 範本 JSON 時，我們會進行驗證以確保它是有效的 JSON。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-158">When you edit the Resource Manager template JSON we will validate to ensure that it is valid JSON.</span></span> <span data-ttu-id="f9bdd-159">選擇 [確定]，然後選擇 [儲存] 以儲存更新後的範本。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-159">Choose **OK** and then **Save** to save your updated template.</span></span>

![編輯範本](media/edit-template-portal2a.PNG)  <br />

<span data-ttu-id="f9bdd-161">儲存 **範本** 後，您就會看到確認通知。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-161">Once the **Template** is saved you will see a confirmation notification.</span></span>

![編輯範本](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a><span data-ttu-id="f9bdd-163">部署範本資源</span><span class="sxs-lookup"><span data-stu-id="f9bdd-163">Deploy a Template resource</span></span>
<span data-ttu-id="f9bdd-164">您可以部署任何您有**讀取**權限的**範本**。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-164">You can deploy any **Template** that you have **Read** permissions on.</span></span> <span data-ttu-id="f9bdd-165">部署流程會啟動標準 Azure 範本部署刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-165">The deployment flow launches the standard Azure Template deployment blade.</span></span> <span data-ttu-id="f9bdd-166">填妥 Resource Manager 範本參數的值以繼續進行部署。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-166">Fill out the values for the Resource Manager template parameters to proceed with the deployment.</span></span>

![部署範本](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a><span data-ttu-id="f9bdd-168">共用範本資源</span><span class="sxs-lookup"><span data-stu-id="f9bdd-168">Share a Template resource</span></span>
<span data-ttu-id="f9bdd-169">可與您的同事共用 **範本** 資源。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-169">A **Template** resource can be shared with your peers.</span></span> <span data-ttu-id="f9bdd-170">共用行為類似於 [Azure 上任何資源的角色指派](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-170">Sharing behaves similarly to [role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="f9bdd-171">**範本** 擁有者會提供權限給可與範本資源互動的其他使用者。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-171">The **Template** owner provides permissions to other users who can interact with a Template resource.</span></span> <span data-ttu-id="f9bdd-172">與您共用 **範本** 的個人或一群人將可看到 Resource Manager 範本和其資源庫屬性。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-172">The person or group of people you share the **Template** with will be able to see the Resource Manager template and its gallery properties.</span></span>

### <a name="access-control-for-the-microsoftgallery-resources"></a><span data-ttu-id="f9bdd-173">Microsoft.Gallery 資源的存取控制</span><span class="sxs-lookup"><span data-stu-id="f9bdd-173">Access control for the Microsoft.Gallery resources</span></span>
| <span data-ttu-id="f9bdd-174">角色</span><span class="sxs-lookup"><span data-stu-id="f9bdd-174">Role</span></span> | <span data-ttu-id="f9bdd-175">權限</span><span class="sxs-lookup"><span data-stu-id="f9bdd-175">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="f9bdd-176">擁有者</span><span class="sxs-lookup"><span data-stu-id="f9bdd-176">Owner</span></span> |<span data-ttu-id="f9bdd-177">允許完整控制範本資源 (包括共用)</span><span class="sxs-lookup"><span data-stu-id="f9bdd-177">Allows full control on the Template resource including Share</span></span> |
| <span data-ttu-id="f9bdd-178">讀取者</span><span class="sxs-lookup"><span data-stu-id="f9bdd-178">Reader</span></span> |<span data-ttu-id="f9bdd-179">允許讀取和執行 (部署) 範本資源</span><span class="sxs-lookup"><span data-stu-id="f9bdd-179">Allows Read and Execute(Deploy) on the Template resource</span></span> |
| <span data-ttu-id="f9bdd-180">參與者</span><span class="sxs-lookup"><span data-stu-id="f9bdd-180">Contributor</span></span> |<span data-ttu-id="f9bdd-181">允許範本資源的編輯和刪除權限</span><span class="sxs-lookup"><span data-stu-id="f9bdd-181">Allows Edit and Delete permission on the Template resource.</span></span> <span data-ttu-id="f9bdd-182">使用者不能與其他人共用範本</span><span class="sxs-lookup"><span data-stu-id="f9bdd-182">User cannot Share the Template with others</span></span> |

<span data-ttu-id="f9bdd-183">按一下滑鼠右鍵或在特定項目的 [檢視] 刀鋒視窗上選取瀏覽項目上的 [共用]  。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-183">Select **Share** on the browse item by right clicking or on the view blade of a specific item.</span></span> <span data-ttu-id="f9bdd-184">這會啟動共用經驗。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-184">This launches a Share experience.</span></span>

![共用範本](media/share-template-portal1a.png)  <br />

 <span data-ttu-id="f9bdd-186">您現在可以選擇角色及使用者或群組，以提供特定 **範本**的存取權。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-186">You can now choose a role and a user or group to provide access to a particular **Template**.</span></span> <span data-ttu-id="f9bdd-187">可用的角色為 [擁有者]、[讀取者] 和 [參與者]。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-187">The available roles are Owner, Reader and Contributor.</span></span> <span data-ttu-id="f9bdd-188">如需詳細資料，請參閱上面的 [存取控制](#access-control-for-a-tenant-resource-provider) 一節。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-188">More details in the [access control](#access-control-for-a-tenant-resource-provider) section above.</span></span>

![共用範本](media/share-template-portal2b.png)  <br />

![共用範本](media/share-template-portal3b.png)  <br />

<span data-ttu-id="f9bdd-191">按一下 [選取] 和 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-191">Click **Select** and **Ok**.</span></span> <span data-ttu-id="f9bdd-192">您現在可以看到您加入至資源的使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-192">You can now see the users or groups you added to the resource.</span></span>

![共用範本](media/share-template-portal4b.png)  <br />

> [!NOTE]
> <span data-ttu-id="f9bdd-194">只能與相同 Azure Active Directory 租用戶中的使用者和群組共用範本。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-194">A Template can only be shared with users and groups in the same Azure Active Directory tenant.</span></span> <span data-ttu-id="f9bdd-195">如果您與不在您的租用戶中的電子郵件地址共用範本，將會傳送邀請來要求使用者以來賓身分加入租用戶。</span><span class="sxs-lookup"><span data-stu-id="f9bdd-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking the user to join the tenant as a guest.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f9bdd-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f9bdd-196">Next steps</span></span>
* <span data-ttu-id="f9bdd-197">若要了解如何建立 Resource Manager 範本，請參閱 [撰寫範本](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="f9bdd-197">To learn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="f9bdd-198">若要了解您可用於 Resource Manager 範本中的函數，請參閱 [範本函式](../azure-resource-manager/resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="f9bdd-198">To understand the functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span></span>
* <span data-ttu-id="f9bdd-199">如需設計範本的指引，請參閱 [設計 Azure 資源管理員範本的最佳做法](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span><span class="sxs-lookup"><span data-stu-id="f9bdd-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span></span>

