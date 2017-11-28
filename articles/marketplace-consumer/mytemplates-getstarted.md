---
title: "aaaGet 入門私用的範本 |Microsoft 文件"
description: "新增、 管理及共用您的私人範本使用 hello Azure 入口網站、 hello Azure CLI 或 PowerShell。"
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
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a><span data-ttu-id="5a0c0-103">開始使用私用 hello Azure 入口網站上的範本</span><span class="sxs-lookup"><span data-stu-id="5a0c0-103">Get started with private Templates on hello Azure Portal</span></span>
<span data-ttu-id="5a0c0-104">[Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)範本是宣告式的樣板使用 toodefine 您的部署。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used toodefine your deployment.</span></span> <span data-ttu-id="5a0c0-105">您可以定義 hello 資源 toodeploy 解決方案，並指定參數和變數可讓您針對不同的環境 tooinput 值。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-105">You can define hello resources toodeploy for a solution, and specify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="5a0c0-106">hello 範本包含 JSON 和您可以使用運算式 tooconstruct 值為您的部署。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-106">hello template consists of JSON and expressions which you can use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="5a0c0-107">您可以使用 hello 新**範本**功能 hello [Azure 入口網站](https://portal.azure.com)以及 hello **Microsoft.Gallery**資源提供者，來擴充 hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable 使用者 toocreate、 管理及部署個人的程式庫從私用的範本。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-107">You can use hello new **Templates** capability in hello [Azure Portal](https://portal.azure.com) along with hello **Microsoft.Gallery** resource provider as an extension of hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable users toocreate, manage and deploy private templates from a personal library.</span></span>

<span data-ttu-id="5a0c0-108">本文件將逐步引導您新增、 管理及共用私用**範本**使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-108">This document walks you through adding, managing and sharing a private **Template** using hello Azure Portal.</span></span>

## <a name="guidance"></a><span data-ttu-id="5a0c0-109">指引</span><span class="sxs-lookup"><span data-stu-id="5a0c0-109">Guidance</span></span>
<span data-ttu-id="5a0c0-110">hello 下列建議可協助您充分利用**範本**使用您的方案時：</span><span class="sxs-lookup"><span data-stu-id="5a0c0-110">hello following suggestions will help you take full advantage of **Templates** when working with your solutions:</span></span>

* <span data-ttu-id="5a0c0-111">**範本** 是一項封裝資源，其中包含 Resource Manager 範本和其他中繼資料。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span></span> <span data-ttu-id="5a0c0-112">其行為非常類似 tooan hello Marketplace 中的項目。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-112">It behaves very similarly tooan item in hello Marketplace.</span></span> <span data-ttu-id="5a0c0-113">hello 主要差異是，它是私用的項目相對於的 toohello 公用 Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-113">hello key difference is that it is a private item as opposed toohello public Marketplace items.</span></span>
* <span data-ttu-id="5a0c0-114">hello**範本**適用於使用者需要 toocustomize 其部署的程式庫。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-114">hello **Templates** library works well for users who need toocustomize their deployments.</span></span>
* <span data-ttu-id="5a0c0-115">**範本** 適用於在 Azure 中需要簡單儲存機制的使用者。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-115">**Templates** work well for users who need a simple repository within Azure.</span></span>
* <span data-ttu-id="5a0c0-116">開始使用現有的 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-116">Start with an existing Resource Manager template.</span></span> <span data-ttu-id="5a0c0-117">在 [github](https://github.com/Azure/azure-quickstart-templates) 中尋找範本，或從現有資源群組[匯出範本](../azure-resource-manager/resource-manager-export-template.md)。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span></span>
* <span data-ttu-id="5a0c0-118">**範本**是繫結的 toohello 使用者，才能將其發行。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-118">**Templates** are tied toohello user who publishes them.</span></span> <span data-ttu-id="5a0c0-119">hello 發行者名稱就是擁有讀取權限 tooit 可見 tooeveryone。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-119">hello publisher name is visible tooeveryone who has read access tooit.</span></span>
* <span data-ttu-id="5a0c0-120">**範本** 是 Resource Manager 資源，一旦發佈便無法重新命名。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span></span>

## <a name="add-a-template-resource"></a><span data-ttu-id="5a0c0-121">新增範本資源</span><span class="sxs-lookup"><span data-stu-id="5a0c0-121">Add a Template resource</span></span>
<span data-ttu-id="5a0c0-122">有兩種方式 toocreate**範本**hello Azure 入口網站中的資源。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-122">There are two ways toocreate a **Template** resource in hello Azure portal.</span></span>

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a><span data-ttu-id="5a0c0-123">方法 1︰從執行中的資源群組建立新的範本資源</span><span class="sxs-lookup"><span data-stu-id="5a0c0-123">Method 1 : Create a new Template resource from a running resource group</span></span>
1. <span data-ttu-id="5a0c0-124">瀏覽 hello Azure 入口網站上的 tooan 現有資源群組。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-124">Navigate tooan existing resource group on hello Azure Portal.</span></span> <span data-ttu-id="5a0c0-125">在 [設定] 中選取 [匯出範本]。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-125">Select **Export template** in **Settings**.</span></span>
2. <span data-ttu-id="5a0c0-126">一旦 hello Resource Manager 範本匯出時，使用 hello**儲存範本**按鈕 toosave 它 toohello**範本**儲存機制。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-126">Once hello Resource Manager template is exported, use hello **Save Template** button toosave it toohello **Templates** repository.</span></span> <span data-ttu-id="5a0c0-127">在 [這裡](../azure-resource-manager/resource-manager-export-template.md)尋找匯出範本的完整詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span></span>
   <br /><br /><span data-ttu-id="5a0c0-128">
   ![資源群組匯出](media/rg-export-portal1.PNG)</span><span class="sxs-lookup"><span data-stu-id="5a0c0-128">
![Resource group export](media/rg-export-portal1.PNG)</span></span>  <br />
3. <span data-ttu-id="5a0c0-129">選取 hello**儲存 tooTemplate**命令按鈕。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-129">Select hello **Save tooTemplate** command button.</span></span>
   <br /><br />
4. <span data-ttu-id="5a0c0-130">輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="5a0c0-130">Enter hello following information:</span></span>
   
   * <span data-ttu-id="5a0c0-131">名稱 – hello 範本物件的名稱 (請注意： 這是基礎的 Azure 資源管理員名稱。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-131">Name – Name of hello template object (NOTE: This is an Azure Resource Manager based name.</span></span> <span data-ttu-id="5a0c0-132">適用所有命名限制，一旦建立便無法變更)。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-132">All naming restrictions apply and it cannot be changed once created).</span></span>
   * <span data-ttu-id="5a0c0-133">說明-關於 hello 範本的簡短摘要。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-133">Description – Quick summary about hello template.</span></span>
     
     ![儲存範本](media/save-template-portal1.PNG)  <br />
5. <span data-ttu-id="5a0c0-135">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-135">Click **Save**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5a0c0-136">hello 匯出範本刀鋒視窗中顯示通知時 hello 匯出的資源管理員範本發生錯誤，但是您仍然可以無法 toosave 這個資源管理員範本 toohello 範本。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-136">hello Export template blade shows notifications when hello exported Resource Manager template has errors, but you will still be able toosave this Resource Manager template toohello Templates.</span></span> <span data-ttu-id="5a0c0-137">請確定您檢查並修正任何資源管理員範本問題，才能重新部署的 hello 匯出 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-137">Ensure that you check and fix any Resource Manager template issues before redeploying hello exported Resource Manager template.</span></span>
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a><span data-ttu-id="5a0c0-138">方法 2 ︰從瀏覽加入新的範本資源</span><span class="sxs-lookup"><span data-stu-id="5a0c0-138">Method 2 : Add a new Template resource from browse</span></span>
<span data-ttu-id="5a0c0-139">您也可以加入新**範本**使用 hello + 新增] 命令按鈕從頭**瀏覽 > 範本**。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-139">You can also add a new **Template** from scratch using hello +Add command button in **Browse > Templates**.</span></span> <span data-ttu-id="5a0c0-140">您將需要 tooprovide 描述與 hello Resource Manager 範本 JSON 的名稱。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-140">You will need tooprovide a Name, Description and hello Resource Manager template JSON.</span></span>

![新增範本](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> <span data-ttu-id="5a0c0-142">Microsoft.Gallery 是以租用戶為基礎的 Azure 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span></span> <span data-ttu-id="5a0c0-143">hello 範本資源是建立它的相等的 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-143">hello Template resource is tied toohello user who created it.</span></span> <span data-ttu-id="5a0c0-144">不繫結的 tooany 特定訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-144">It is not tied tooany specific subscription.</span></span> <span data-ttu-id="5a0c0-145">訂用帳戶必須 toobe 選擇只有在部署範本。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-145">A subscription needs toobe chosen only when deploying a Template.</span></span>
> 
> 

## <a name="view-template-resources"></a><span data-ttu-id="5a0c0-146">檢視範本資源</span><span class="sxs-lookup"><span data-stu-id="5a0c0-146">View Template resources</span></span>
<span data-ttu-id="5a0c0-147">所有**範本**可用 tooyou 可以看到在**瀏覽 > 範本**。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-147">All **Templates** available tooyou can be seen at **Browse > Templates**.</span></span> <span data-ttu-id="5a0c0-148">這包括您所建立的**範本**以及利用各種權限層級與您共用的範本。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span></span> <span data-ttu-id="5a0c0-149">詳細資料請參閱 hello[存取控制](#access-control-for-a-tenant-resource-provider)下一節。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-149">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section below.</span></span>

![檢視範本](media/view-template-portal1.PNG)  <br />

<span data-ttu-id="5a0c0-151">您可以檢視 hello 詳細資料**範本**按 hello 清單中的項目執行。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-151">You can view hello details of a **Template** by clicking into an item in hello list.</span></span>

![檢視範本](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a><span data-ttu-id="5a0c0-153">編輯範本資源</span><span class="sxs-lookup"><span data-stu-id="5a0c0-153">Edit a Template resource</span></span>
<span data-ttu-id="5a0c0-154">您可以起始 hello 編輯流程**範本**hello 瀏覽清單上按一下滑鼠右鍵 hello 項目，或是選擇 hello 編輯命令按鈕。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-154">You can initiate hello edit flow for a **Template** by right clicking hello item on hello Browse list or by choosing hello Edit command button.</span></span>

![編輯範本](media/edit-template-portal1a.PNG)  <br />

<span data-ttu-id="5a0c0-156">您可以編輯 hello 描述或資源管理員範本文字。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-156">You can edit hello description or Resource Manager template text.</span></span> <span data-ttu-id="5a0c0-157">您無法編輯 hello 名稱，因為它是資源管理員資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-157">You cannot edit hello name since it is an Resource Manager resource name.</span></span> <span data-ttu-id="5a0c0-158">當您編輯 hello Resource Manager 範本 JSON 我們將會驗證 tooensure 它是有效的 JSON。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-158">When you edit hello Resource Manager template JSON we will validate tooensure that it is valid JSON.</span></span> <span data-ttu-id="5a0c0-159">選擇**確定**然後**儲存**toosave 更新的範本。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-159">Choose **OK** and then **Save** toosave your updated template.</span></span>

![編輯範本](media/edit-template-portal2a.PNG)  <br />

<span data-ttu-id="5a0c0-161">一次 hello**範本**會儲存您會看到確認通知。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-161">Once hello **Template** is saved you will see a confirmation notification.</span></span>

![編輯範本](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a><span data-ttu-id="5a0c0-163">部署範本資源</span><span class="sxs-lookup"><span data-stu-id="5a0c0-163">Deploy a Template resource</span></span>
<span data-ttu-id="5a0c0-164">您可以部署任何您有**讀取**權限的**範本**。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-164">You can deploy any **Template** that you have **Read** permissions on.</span></span> <span data-ttu-id="5a0c0-165">hello 部署流程會啟動 hello 標準 Azure 範本部署刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-165">hello deployment flow launches hello standard Azure Template deployment blade.</span></span> <span data-ttu-id="5a0c0-166">填寫 hello 資源管理員範本參數 tooproceed hello 部署的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-166">Fill out hello values for hello Resource Manager template parameters tooproceed with hello deployment.</span></span>

![部署範本](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a><span data-ttu-id="5a0c0-168">共用範本資源</span><span class="sxs-lookup"><span data-stu-id="5a0c0-168">Share a Template resource</span></span>
<span data-ttu-id="5a0c0-169">可與您的同事共用 **範本** 資源。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-169">A **Template** resource can be shared with your peers.</span></span> <span data-ttu-id="5a0c0-170">共用的行為類似太[Azure 上的任何資源的角色指派](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-170">Sharing behaves similarly too[role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="5a0c0-171">hello**範本**擁有者提供權限可以進行互動的 tooother 使用者範本資源。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-171">hello **Template** owner provides permissions tooother users who can interact with a Template resource.</span></span> <span data-ttu-id="5a0c0-172">hello 個人或群組的人員共用 hello**範本**將能 toosee hello Resource Manager 範本和其組件庫內容。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-172">hello person or group of people you share hello **Template** with will be able toosee hello Resource Manager template and its gallery properties.</span></span>

### <a name="access-control-for-hello-microsoftgallery-resources"></a><span data-ttu-id="5a0c0-173">Hello Microsoft.Gallery 資源的存取控制</span><span class="sxs-lookup"><span data-stu-id="5a0c0-173">Access control for hello Microsoft.Gallery resources</span></span>
| <span data-ttu-id="5a0c0-174">角色</span><span class="sxs-lookup"><span data-stu-id="5a0c0-174">Role</span></span> | <span data-ttu-id="5a0c0-175">權限</span><span class="sxs-lookup"><span data-stu-id="5a0c0-175">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="5a0c0-176">擁有者</span><span class="sxs-lookup"><span data-stu-id="5a0c0-176">Owner</span></span> |<span data-ttu-id="5a0c0-177">可讓 hello 樣板資源，包括共用的完整控制</span><span class="sxs-lookup"><span data-stu-id="5a0c0-177">Allows full control on hello Template resource including Share</span></span> |
| <span data-ttu-id="5a0c0-178">讀取者</span><span class="sxs-lookup"><span data-stu-id="5a0c0-178">Reader</span></span> |<span data-ttu-id="5a0c0-179">在 [hello 範本資源上允許的讀取與 Execute(Deploy)</span><span class="sxs-lookup"><span data-stu-id="5a0c0-179">Allows Read and Execute(Deploy) on hello Template resource</span></span> |
| <span data-ttu-id="5a0c0-180">參與者</span><span class="sxs-lookup"><span data-stu-id="5a0c0-180">Contributor</span></span> |<span data-ttu-id="5a0c0-181">Hello 範本資源上允許編輯和刪除權限。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-181">Allows Edit and Delete permission on hello Template resource.</span></span> <span data-ttu-id="5a0c0-182">使用者無法與其他人共用 hello 範本</span><span class="sxs-lookup"><span data-stu-id="5a0c0-182">User cannot Share hello Template with others</span></span> |

<span data-ttu-id="5a0c0-183">選取**共用**hello 瀏覽項目以滑鼠右鍵按一下，或在 hello 特定項目的 [檢視] 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-183">Select **Share** on hello browse item by right clicking or on hello view blade of a specific item.</span></span> <span data-ttu-id="5a0c0-184">這會啟動共用經驗。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-184">This launches a Share experience.</span></span>

![共用範本](media/share-template-portal1a.png)  <br />

 <span data-ttu-id="5a0c0-186">您現在可以選擇一種角色和使用者或群組 tooprovide 存取 tooa 特定**範本**。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-186">You can now choose a role and a user or group tooprovide access tooa particular **Template**.</span></span> <span data-ttu-id="5a0c0-187">hello 可用的角色是擁有者、 讀取器和參與者。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-187">hello available roles are Owner, Reader and Contributor.</span></span> <span data-ttu-id="5a0c0-188">詳細資料請參閱 hello[存取控制](#access-control-for-a-tenant-resource-provider)上一節。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-188">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section above.</span></span>

![共用範本](media/share-template-portal2b.png)  <br />

![共用範本](media/share-template-portal3b.png)  <br />

<span data-ttu-id="5a0c0-191">按一下 [選取] 和 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-191">Click **Select** and **Ok**.</span></span> <span data-ttu-id="5a0c0-192">您現在可以看到 hello 使用者或群組加入 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-192">You can now see hello users or groups you added toohello resource.</span></span>

![共用範本](media/share-template-portal4b.png)  <br />

> [!NOTE]
> <span data-ttu-id="5a0c0-194">範本只可共用給使用者和群組 hello 中相同的 Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-194">A Template can only be shared with users and groups in hello same Azure Active Directory tenant.</span></span> <span data-ttu-id="5a0c0-195">如果您不在您的租用戶的電子郵件地址共用範本，將會詢問 hello 做為來賓使用者 toojoin hello 租用傳送邀請。</span><span class="sxs-lookup"><span data-stu-id="5a0c0-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking hello user toojoin hello tenant as a guest.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5a0c0-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a0c0-196">Next steps</span></span>
* <span data-ttu-id="5a0c0-197">toolearn 有關建立資源管理員範本，請參閱[撰寫範本](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="5a0c0-197">toolearn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="5a0c0-198">toounderstand hello 函式，您可以使用資源管理員範本中，請參閱[樣板函式](../azure-resource-manager/resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="5a0c0-198">toounderstand hello functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span></span>
* <span data-ttu-id="5a0c0-199">如需設計範本的指引，請參閱 [設計 Azure 資源管理員範本的最佳做法](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span><span class="sxs-lookup"><span data-stu-id="5a0c0-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span></span>

