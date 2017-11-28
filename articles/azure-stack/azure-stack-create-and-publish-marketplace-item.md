---
title: "aaaCreate 和發佈 Azure 堆疊中的 Marketplace 項目 |Microsoft 文件"
description: "在 Azure Stack 中建立和發佈 Marketplace 項目。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 77e5f60c-a86e-4d54-aa8d-288e9a889386
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: erikje
ms.openlocfilehash: 6f6a7af96f9d8de9098ac7eee4ba2ac9bc3d6a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-publish-a-marketplace-item"></a><span data-ttu-id="e7059-103">建立及發行 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="e7059-103">Create and publish a Marketplace item</span></span>
## <a name="create-a-marketplace-item"></a><span data-ttu-id="e7059-104">建立 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="e7059-104">Create a Marketplace item</span></span>
1. <span data-ttu-id="e7059-105">[下載](http://www.aka.ms/azurestackmarketplaceitem)hello Azure 圖庫 Packager 工具和 hello 範例 Marketplace</堆疊項目。</span><span class="sxs-lookup"><span data-stu-id="e7059-105">[Download](http://www.aka.ms/azurestackmarketplaceitem) hello Azure Gallery Packager tool and hello sample Azure Stack Marketplace item.</span></span>
2. <span data-ttu-id="e7059-106">開啟 hello 範例 Marketplace 項目，並重新命名 hello **SimpleVMTemplate**資料夾。</span><span class="sxs-lookup"><span data-stu-id="e7059-106">Open hello sample Marketplace item and rename hello **SimpleVMTemplate** folder.</span></span> <span data-ttu-id="e7059-107">(相同的名稱，為您的 Marketplace 項目-例如，使用 hello **Contoso.TodoList**。)此資料夾包含：</span><span class="sxs-lookup"><span data-stu-id="e7059-107">(Use hello same name as your Marketplace item--for example, **Contoso.TodoList**.) This folder contains:</span></span>
   
       /Contoso.TodoList/
       /Contoso.TodoList/Manifest.json
       /Contoso.TodoList/UIDefinition.json
       /Contoso.TodoList/Icons/
       /Contoso.TodoList/Strings/
       /Contoso.TodoList/DeploymentTemplates/
3. <span data-ttu-id="e7059-108">[建立 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)，或從 GitHub 選擇範本。</span><span class="sxs-lookup"><span data-stu-id="e7059-108">[Create an Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) or choose a template from GitHub.</span></span> <span data-ttu-id="e7059-109">hello Marketplace 項目會使用此範本 toocreate 資源。</span><span class="sxs-lookup"><span data-stu-id="e7059-109">hello Marketplace item uses this template toocreate a resource.</span></span>
4. <span data-ttu-id="e7059-110">toomake 確定 hello 資源可以成功地部署、 測試與 Microsoft Azure 堆疊 Api hello hello 範本。</span><span class="sxs-lookup"><span data-stu-id="e7059-110">toomake sure that hello resource can be deployed successfully, test hello template with hello Microsoft Azure Stack APIs.</span></span>
5. <span data-ttu-id="e7059-111">如果您的範本依賴於虛擬機器映像，請依照 hello 指示太[新增虛擬機器映像 tooAzure 堆疊](azure-stack-add-vm-image.md)。</span><span class="sxs-lookup"><span data-stu-id="e7059-111">If your template relies on a virtual machine image, follow hello instructions too[add a virtual machine image tooAzure Stack](azure-stack-add-vm-image.md).</span></span>
6. <span data-ttu-id="e7059-112">將您的 Azure Resource Manager 範本儲存在 hello **/Contoso.TodoList/DeploymentTemplates/**資料夾。</span><span class="sxs-lookup"><span data-stu-id="e7059-112">Save your Azure Resource Manager template in hello **/Contoso.TodoList/DeploymentTemplates/** folder.</span></span>
7. <span data-ttu-id="e7059-113">選擇 hello 圖示與您的 Marketplace 項目的文字。</span><span class="sxs-lookup"><span data-stu-id="e7059-113">Choose hello icons and text for your Marketplace item.</span></span> <span data-ttu-id="e7059-114">新增圖示 toohello**圖示**資料夾，並加入文字 toohello**資源**檔案在 hello**字串**資料夾。</span><span class="sxs-lookup"><span data-stu-id="e7059-114">Add icons toohello **Icons** folder, and add text toohello **resources** file in hello **Strings** folder.</span></span> <span data-ttu-id="e7059-115">使用圖示 hello Small、 Medium、 Large 和通用命名慣例。</span><span class="sxs-lookup"><span data-stu-id="e7059-115">Use hello Small, Medium, Large, and Wide naming convention for icons.</span></span> <span data-ttu-id="e7059-116">如需詳細的說明，請參閱 [Marketplace 項目 UI 參考](#reference-marketplace-item-ui)。</span><span class="sxs-lookup"><span data-stu-id="e7059-116">See [Marketplace item UI reference](#reference-marketplace-item-ui) for a detailed description.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e7059-117">所有四個圖示的大小 （小型、 中型的大，範圍） 所需的正確建立 hello Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="e7059-117">All four icon sizes (small, medium, large, wide) are required for building hello Marketplace item correctly.</span></span>
   > 
   > 
8. <span data-ttu-id="e7059-118">在 hello **manifest.json**檔案中，變更**名稱**toohello 您的 Marketplace 項目名稱。</span><span class="sxs-lookup"><span data-stu-id="e7059-118">In hello **manifest.json** file, change **name** toohello name of your Marketplace item.</span></span> <span data-ttu-id="e7059-119">也會變更**發行者**tooyour 名稱或公司。</span><span class="sxs-lookup"><span data-stu-id="e7059-119">Also change **publisher** tooyour name or company.</span></span>
9. <span data-ttu-id="e7059-120">在下**成品**，變更**名稱**和**路徑**toohello hello Azure 資源管理員範本，包含正確的資訊。</span><span class="sxs-lookup"><span data-stu-id="e7059-120">Under **artifacts**, change **name** and **path** toohello correct information for hello Azure Resource Manager template that you included.</span></span>
   
         "artifacts": [
            {
                "name": "Type your template name",
                "type": "Template",
                "path": "DeploymentTemplates\\Type your path",
                "isDefault": true
            }
10. <span data-ttu-id="e7059-121">取代**我的 Marketplace 項目**與 hello 分類您的 Marketplace 項目應該出現的位置清單。</span><span class="sxs-lookup"><span data-stu-id="e7059-121">Replace **My Marketplace Items** with a list of hello categories where your Marketplace item should appear.</span></span>
    
             "categories":[
                 "My Marketplace Items"
              ],
11. <span data-ttu-id="e7059-122">任何進一步編輯 toomanifest.json 參照太[參考： Marketplace 項目 manifest.json](#reference-marketplace-item-manifestjson)。</span><span class="sxs-lookup"><span data-stu-id="e7059-122">For any further edits toomanifest.json, refer too[Reference: Marketplace item manifest.json](#reference-marketplace-item-manifestjson).</span></span>
12. <span data-ttu-id="e7059-123">toopackage hello 資料夾到.azpkg 檔案中，開啟命令提示字元，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="e7059-123">toopackage hello folders into an .azpkg file, open a command prompt and run hello following command:</span></span>
    
        AzureGalleryPackager.exe package –m <path toomanifest.json> -o <output location for hello package>
    
    > [!NOTE]
    > <span data-ttu-id="e7059-124">hello 完整路徑 toohello 輸出封裝必須存在。</span><span class="sxs-lookup"><span data-stu-id="e7059-124">hello full path toohello output package must exist.</span></span> <span data-ttu-id="e7059-125">例如，如果 hello 輸出路徑 C:\MarketPlaceItem\yourpackage.azpkg，hello 資料夾 C:\MarketPlaceItem 必須存在。</span><span class="sxs-lookup"><span data-stu-id="e7059-125">For example, if hello output path is C:\MarketPlaceItem\yourpackage.azpkg, hello folder C:\MarketPlaceItem must exist.</span></span>
    > 
    > 

## <a name="publish-a-marketplace-item"></a><span data-ttu-id="e7059-126">發佈 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="e7059-126">Publish a Marketplace item</span></span>
1. <span data-ttu-id="e7059-127">使用 PowerShell 或 Azure 儲存體總管 tooupload 您的 Marketplace 項目 (.azpkg) tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e7059-127">Use PowerShell or Azure Storage Explorer tooupload your Marketplace item (.azpkg) tooAzure Blob storage.</span></span> <span data-ttu-id="e7059-128">您可以上傳 toolocal 堆疊 Azure 儲存體，或上傳 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e7059-128">You can upload toolocal Azure Stack storage or upload tooAzure Storage.</span></span> <span data-ttu-id="e7059-129">（它是一個暫存位置的 hello 封裝）。請確定該 hello blob 是可公開存取。</span><span class="sxs-lookup"><span data-stu-id="e7059-129">(It's a temporary location for hello package.) Make sure that hello blob is publicly accessible.</span></span>
2. <span data-ttu-id="e7059-130">在 hello 用戶端 hello Microsoft Azure 堆疊環境中的虛擬機器，請確定您的 PowerShell 工作階段已設定使用您的服務系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="e7059-130">On hello client virtual machine in hello Microsoft Azure Stack environment, make sure that your PowerShell session is set up with your service administrator credentials.</span></span> <span data-ttu-id="e7059-131">您可以找到有關如何 tooauthenticate Azure 堆疊中的 PowerShell 中[部署範本，以使用 PowerShell](azure-stack-deploy-template-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="e7059-131">You can find instructions for how tooauthenticate PowerShell in Azure Stack in [Deploy a template with PowerShell](azure-stack-deploy-template-powershell.md).</span></span>
3. <span data-ttu-id="e7059-132">使用 hello**新增 AzureRMGalleryItem** PowerShell cmdlet toopublish hello Marketplace 項目 tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="e7059-132">Use hello **Add-AzureRMGalleryItem** PowerShell cmdlet toopublish hello Marketplace item tooAzure Stack.</span></span> <span data-ttu-id="e7059-133">例如：</span><span class="sxs-lookup"><span data-stu-id="e7059-133">For example:</span></span>
   
       Add-AzureRMGalleryItem -GalleryItemUri `
       https://sample.blob.core.windows.net/gallerypackages/Microsoft.SimpleTemplate.1.0.0.azpkg –Verbose
   
   | <span data-ttu-id="e7059-134">參數</span><span class="sxs-lookup"><span data-stu-id="e7059-134">Parameter</span></span> | <span data-ttu-id="e7059-135">說明</span><span class="sxs-lookup"><span data-stu-id="e7059-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="e7059-136">SubscriptionID</span><span class="sxs-lookup"><span data-stu-id="e7059-136">SubscriptionID</span></span> |<span data-ttu-id="e7059-137">管理訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="e7059-137">Admin subscription ID.</span></span> <span data-ttu-id="e7059-138">您可以使用 PowerShell 來擷取它。</span><span class="sxs-lookup"><span data-stu-id="e7059-138">You can retrieve it by using PowerShell.</span></span> <span data-ttu-id="e7059-139">如果您想使用 tooget 它在 hello 入口網站移 toohello 提供者的訂用帳戶，並複製 hello 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="e7059-139">If you'd prefer tooget it in hello portal, go toohello provider subscription and copy hello subscription ID.</span></span> |
   | <span data-ttu-id="e7059-140">GalleryItemUri</span><span class="sxs-lookup"><span data-stu-id="e7059-140">GalleryItemUri</span></span> |<span data-ttu-id="e7059-141">已上傳的 toostorage 程式庫封裝的 blob URI。</span><span class="sxs-lookup"><span data-stu-id="e7059-141">Blob URI for your gallery package that has already been uploaded toostorage.</span></span> |
   | <span data-ttu-id="e7059-142">Apiversion</span><span class="sxs-lookup"><span data-stu-id="e7059-142">Apiversion</span></span> |<span data-ttu-id="e7059-143">設定為 **2015-04-01**。</span><span class="sxs-lookup"><span data-stu-id="e7059-143">Set as **2015-04-01**.</span></span> |
4. <span data-ttu-id="e7059-144">移 toohello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="e7059-144">Go toohello portal.</span></span> <span data-ttu-id="e7059-145">您現在可以看到在 hello 入口網站-身為系統管理員或租用戶身分 hello Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="e7059-145">You can now see hello Marketplace item in hello portal--as an admin or as a tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e7059-146">hello 封裝可能需要花費幾分鐘的時間 tooappear。</span><span class="sxs-lookup"><span data-stu-id="e7059-146">hello package might take several minutes tooappear.</span></span>
   > 
   > 
5. <span data-ttu-id="e7059-147">您的 Marketplace 項目現在已儲存 toohello Marketplace</堆疊。</span><span class="sxs-lookup"><span data-stu-id="e7059-147">Your Marketplace item has now been saved toohello Azure Stack Marketplace.</span></span> <span data-ttu-id="e7059-148">您可以選擇 toodelete 它從您的 Blob 儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="e7059-148">You can choose toodelete it from your Blob storage location.</span></span>
6. <span data-ttu-id="e7059-149">您可以移除 Marketplace 項目使用 hello**移除 AzureRMGalleryItem** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e7059-149">You can remove a Marketplace item by using hello **Remove-AzureRMGalleryItem** cmdlet.</span></span> <span data-ttu-id="e7059-150">範例：</span><span class="sxs-lookup"><span data-stu-id="e7059-150">Example:</span></span>
   
        Remove-AzureRMGalleryItem -Name Microsoft.SimpleTemplate.1.0.0  –Verbose
   
   > [!NOTE]
   > <span data-ttu-id="e7059-151">hello Marketplace UI 中移除項目之後，可能會顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="e7059-151">hello Marketplace UI may show an error after you remove an item.</span></span> <span data-ttu-id="e7059-152">toofix hello 錯誤時，按一下 **設定**hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="e7059-152">toofix hello error, click **Settings** in hello portal.</span></span> <span data-ttu-id="e7059-153">然後，在 [入口網站自訂] 之下，選取 [捨棄修改]。</span><span class="sxs-lookup"><span data-stu-id="e7059-153">Then, select **Discard modifications** under **Portal customization**.</span></span>
   > 
   > 

## <a name="reference-marketplace-item-manifestjson"></a><span data-ttu-id="e7059-154">參考：Marketplace 項目 manifest.json</span><span class="sxs-lookup"><span data-stu-id="e7059-154">Reference: Marketplace item manifest.json</span></span>
### <a name="identity-information"></a><span data-ttu-id="e7059-155">身分識別資訊</span><span class="sxs-lookup"><span data-stu-id="e7059-155">Identity information</span></span>
| <span data-ttu-id="e7059-156">名稱</span><span class="sxs-lookup"><span data-stu-id="e7059-156">Name</span></span> | <span data-ttu-id="e7059-157">必要</span><span class="sxs-lookup"><span data-stu-id="e7059-157">Required</span></span> | <span data-ttu-id="e7059-158">類型</span><span class="sxs-lookup"><span data-stu-id="e7059-158">Type</span></span> | <span data-ttu-id="e7059-159">條件約束</span><span class="sxs-lookup"><span data-stu-id="e7059-159">Constraints</span></span> | <span data-ttu-id="e7059-160">說明</span><span class="sxs-lookup"><span data-stu-id="e7059-160">Description</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e7059-161">名稱</span><span class="sxs-lookup"><span data-stu-id="e7059-161">Name</span></span> |<span data-ttu-id="e7059-162">X</span><span class="sxs-lookup"><span data-stu-id="e7059-162">X</span></span> |<span data-ttu-id="e7059-163">String</span><span class="sxs-lookup"><span data-stu-id="e7059-163">String</span></span> |<span data-ttu-id="e7059-164">[A-a-za-z0-9] +</span><span class="sxs-lookup"><span data-stu-id="e7059-164">[A-Za-z0-9]+</span></span> | |
| <span data-ttu-id="e7059-165">發行者</span><span class="sxs-lookup"><span data-stu-id="e7059-165">Publisher</span></span> |<span data-ttu-id="e7059-166">X</span><span class="sxs-lookup"><span data-stu-id="e7059-166">X</span></span> |<span data-ttu-id="e7059-167">String</span><span class="sxs-lookup"><span data-stu-id="e7059-167">String</span></span> |<span data-ttu-id="e7059-168">[A-a-za-z0-9] +</span><span class="sxs-lookup"><span data-stu-id="e7059-168">[A-Za-z0-9]+</span></span> | |
| <span data-ttu-id="e7059-169">版本</span><span class="sxs-lookup"><span data-stu-id="e7059-169">Version</span></span> |<span data-ttu-id="e7059-170">X</span><span class="sxs-lookup"><span data-stu-id="e7059-170">X</span></span> |<span data-ttu-id="e7059-171">String</span><span class="sxs-lookup"><span data-stu-id="e7059-171">String</span></span> |[<span data-ttu-id="e7059-172">SemVer v2</span><span class="sxs-lookup"><span data-stu-id="e7059-172">SemVer v2</span></span>](http://semver.org/) | |

### <a name="metadata"></a><span data-ttu-id="e7059-173">中繼資料</span><span class="sxs-lookup"><span data-stu-id="e7059-173">Metadata</span></span>
| <span data-ttu-id="e7059-174">名稱</span><span class="sxs-lookup"><span data-stu-id="e7059-174">Name</span></span> | <span data-ttu-id="e7059-175">必要</span><span class="sxs-lookup"><span data-stu-id="e7059-175">Required</span></span> | <span data-ttu-id="e7059-176">類型</span><span class="sxs-lookup"><span data-stu-id="e7059-176">Type</span></span> | <span data-ttu-id="e7059-177">條件約束</span><span class="sxs-lookup"><span data-stu-id="e7059-177">Constraints</span></span> | <span data-ttu-id="e7059-178">說明</span><span class="sxs-lookup"><span data-stu-id="e7059-178">Description</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e7059-179">DisplayName</span><span class="sxs-lookup"><span data-stu-id="e7059-179">DisplayName</span></span> |<span data-ttu-id="e7059-180">X</span><span class="sxs-lookup"><span data-stu-id="e7059-180">X</span></span> |<span data-ttu-id="e7059-181">String</span><span class="sxs-lookup"><span data-stu-id="e7059-181">String</span></span> |<span data-ttu-id="e7059-182">建議 80 個字元</span><span class="sxs-lookup"><span data-stu-id="e7059-182">Recommendation of 80 characters</span></span> |<span data-ttu-id="e7059-183">hello 入口網站可能無法顯示項目名稱依正常程序是否超過 80 個字元。</span><span class="sxs-lookup"><span data-stu-id="e7059-183">hello portal might not display your item name gracefully if it is longer than 80 characters.</span></span> |
| <span data-ttu-id="e7059-184">PublisherDisplayName</span><span class="sxs-lookup"><span data-stu-id="e7059-184">PublisherDisplayName</span></span> |<span data-ttu-id="e7059-185">X</span><span class="sxs-lookup"><span data-stu-id="e7059-185">X</span></span> |<span data-ttu-id="e7059-186">String</span><span class="sxs-lookup"><span data-stu-id="e7059-186">String</span></span> |<span data-ttu-id="e7059-187">建議 30 個字元</span><span class="sxs-lookup"><span data-stu-id="e7059-187">Recommendation of 30 characters</span></span> |<span data-ttu-id="e7059-188">hello 入口網站可能無法顯示您的發行者名稱依正常程序是否超過 30 個字元。</span><span class="sxs-lookup"><span data-stu-id="e7059-188">hello portal might not display your publisher name gracefully if it is longer than 30 characters.</span></span> |
| <span data-ttu-id="e7059-189">PublisherLegalName</span><span class="sxs-lookup"><span data-stu-id="e7059-189">PublisherLegalName</span></span> |<span data-ttu-id="e7059-190">X</span><span class="sxs-lookup"><span data-stu-id="e7059-190">X</span></span> |<span data-ttu-id="e7059-191">String</span><span class="sxs-lookup"><span data-stu-id="e7059-191">String</span></span> |<span data-ttu-id="e7059-192">上限 256 個字元</span><span class="sxs-lookup"><span data-stu-id="e7059-192">Maximum of 256 characters</span></span> | |
| <span data-ttu-id="e7059-193">摘要</span><span class="sxs-lookup"><span data-stu-id="e7059-193">Summary</span></span> |<span data-ttu-id="e7059-194">X</span><span class="sxs-lookup"><span data-stu-id="e7059-194">X</span></span> |<span data-ttu-id="e7059-195">String</span><span class="sxs-lookup"><span data-stu-id="e7059-195">String</span></span> |<span data-ttu-id="e7059-196">60 too100 個字元</span><span class="sxs-lookup"><span data-stu-id="e7059-196">60 too100 characters</span></span> | |
| <span data-ttu-id="e7059-197">LongSummary</span><span class="sxs-lookup"><span data-stu-id="e7059-197">LongSummary</span></span> |<span data-ttu-id="e7059-198">X</span><span class="sxs-lookup"><span data-stu-id="e7059-198">X</span></span> |<span data-ttu-id="e7059-199">String</span><span class="sxs-lookup"><span data-stu-id="e7059-199">String</span></span> |<span data-ttu-id="e7059-200">140 too256 個字元</span><span class="sxs-lookup"><span data-stu-id="e7059-200">140 too256 characters</span></span> |<span data-ttu-id="e7059-201">目前在 Azure Stack 中不適用。</span><span class="sxs-lookup"><span data-stu-id="e7059-201">Not yet applicable in Azure Stack.</span></span> |
| <span data-ttu-id="e7059-202">說明</span><span class="sxs-lookup"><span data-stu-id="e7059-202">Description</span></span> |<span data-ttu-id="e7059-203">X</span><span class="sxs-lookup"><span data-stu-id="e7059-203">X</span></span> |[<span data-ttu-id="e7059-204">HTML</span><span class="sxs-lookup"><span data-stu-id="e7059-204">HTML</span></span>](https://auxdocs.azurewebsites.net/en-us/documentation/articles/gallery-metadata#html-sanitization) |<span data-ttu-id="e7059-205">500 too5、 000 個字元</span><span class="sxs-lookup"><span data-stu-id="e7059-205">500 too5,000 characters</span></span> | |

### <a name="images"></a><span data-ttu-id="e7059-206">映像</span><span class="sxs-lookup"><span data-stu-id="e7059-206">Images</span></span>
<span data-ttu-id="e7059-207">hello Marketplace 使用 hello 下列圖示：</span><span class="sxs-lookup"><span data-stu-id="e7059-207">hello Marketplace uses hello following icons:</span></span>

| <span data-ttu-id="e7059-208">名稱</span><span class="sxs-lookup"><span data-stu-id="e7059-208">Name</span></span> | <span data-ttu-id="e7059-209">寬度</span><span class="sxs-lookup"><span data-stu-id="e7059-209">Width</span></span> | <span data-ttu-id="e7059-210">高度</span><span class="sxs-lookup"><span data-stu-id="e7059-210">Height</span></span> | <span data-ttu-id="e7059-211">注意事項</span><span class="sxs-lookup"><span data-stu-id="e7059-211">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e7059-212">寬</span><span class="sxs-lookup"><span data-stu-id="e7059-212">Wide</span></span> |<span data-ttu-id="e7059-213">255 像素</span><span class="sxs-lookup"><span data-stu-id="e7059-213">255 px</span></span> |<span data-ttu-id="e7059-214">115 像素</span><span class="sxs-lookup"><span data-stu-id="e7059-214">115 px</span></span> |<span data-ttu-id="e7059-215">一律需要</span><span class="sxs-lookup"><span data-stu-id="e7059-215">Always required</span></span> |
| <span data-ttu-id="e7059-216">大型</span><span class="sxs-lookup"><span data-stu-id="e7059-216">Large</span></span> |<span data-ttu-id="e7059-217">115 像素</span><span class="sxs-lookup"><span data-stu-id="e7059-217">115 px</span></span> |<span data-ttu-id="e7059-218">115 像素</span><span class="sxs-lookup"><span data-stu-id="e7059-218">115 px</span></span> |<span data-ttu-id="e7059-219">一律需要</span><span class="sxs-lookup"><span data-stu-id="e7059-219">Always required</span></span> |
| <span data-ttu-id="e7059-220">中型</span><span class="sxs-lookup"><span data-stu-id="e7059-220">Medium</span></span> |<span data-ttu-id="e7059-221">90 像素</span><span class="sxs-lookup"><span data-stu-id="e7059-221">90 px</span></span> |<span data-ttu-id="e7059-222">90 像素</span><span class="sxs-lookup"><span data-stu-id="e7059-222">90 px</span></span> |<span data-ttu-id="e7059-223">一律需要</span><span class="sxs-lookup"><span data-stu-id="e7059-223">Always required</span></span> |
| <span data-ttu-id="e7059-224">小型</span><span class="sxs-lookup"><span data-stu-id="e7059-224">Small</span></span> |<span data-ttu-id="e7059-225">40 像素</span><span class="sxs-lookup"><span data-stu-id="e7059-225">40 px</span></span> |<span data-ttu-id="e7059-226">40 像素</span><span class="sxs-lookup"><span data-stu-id="e7059-226">40 px</span></span> |<span data-ttu-id="e7059-227">一律需要</span><span class="sxs-lookup"><span data-stu-id="e7059-227">Always required</span></span> |
| <span data-ttu-id="e7059-228">螢幕擷取畫面</span><span class="sxs-lookup"><span data-stu-id="e7059-228">Screenshot</span></span> |<span data-ttu-id="e7059-229">533 像素</span><span class="sxs-lookup"><span data-stu-id="e7059-229">533 px</span></span> |<span data-ttu-id="e7059-230">32 像素</span><span class="sxs-lookup"><span data-stu-id="e7059-230">32 px</span></span> |<span data-ttu-id="e7059-231">選用</span><span class="sxs-lookup"><span data-stu-id="e7059-231">Optional</span></span> |

### <a name="categories"></a><span data-ttu-id="e7059-232">類別</span><span class="sxs-lookup"><span data-stu-id="e7059-232">Categories</span></span>
<span data-ttu-id="e7059-233">每個 Marketplace 項目應該標記的類別，可識別 hello 入口網站 UI hello 項目出現的位置。</span><span class="sxs-lookup"><span data-stu-id="e7059-233">Each Marketplace item should be tagged with a category that identifies where hello item appears on hello portal UI.</span></span> <span data-ttu-id="e7059-234">您可以選擇其中一個 hello 現有類別目錄中 Azure 堆疊 (運算、 資料 + 儲存體，等) 或選擇新密碼。</span><span class="sxs-lookup"><span data-stu-id="e7059-234">You can choose one of hello existing categories in Azure Stack (Compute, Data + Storage, etc.) or choose a new one.</span></span>

### <a name="links"></a><span data-ttu-id="e7059-235">連結</span><span class="sxs-lookup"><span data-stu-id="e7059-235">Links</span></span>
<span data-ttu-id="e7059-236">每個 Marketplace 項目可以包含各種連結 tooadditional 內容。</span><span class="sxs-lookup"><span data-stu-id="e7059-236">Each Marketplace item can include various links tooadditional content.</span></span> <span data-ttu-id="e7059-237">hello 連結已指定為一份名稱的 Uri。</span><span class="sxs-lookup"><span data-stu-id="e7059-237">hello links are specified as a list of names and URIs.</span></span>

| <span data-ttu-id="e7059-238">名稱</span><span class="sxs-lookup"><span data-stu-id="e7059-238">Name</span></span> | <span data-ttu-id="e7059-239">必要</span><span class="sxs-lookup"><span data-stu-id="e7059-239">Required</span></span> | <span data-ttu-id="e7059-240">類型</span><span class="sxs-lookup"><span data-stu-id="e7059-240">Type</span></span> | <span data-ttu-id="e7059-241">條件約束</span><span class="sxs-lookup"><span data-stu-id="e7059-241">Constraints</span></span> | <span data-ttu-id="e7059-242">說明</span><span class="sxs-lookup"><span data-stu-id="e7059-242">Description</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e7059-243">DisplayName</span><span class="sxs-lookup"><span data-stu-id="e7059-243">DisplayName</span></span> |<span data-ttu-id="e7059-244">X</span><span class="sxs-lookup"><span data-stu-id="e7059-244">X</span></span> |<span data-ttu-id="e7059-245">String</span><span class="sxs-lookup"><span data-stu-id="e7059-245">String</span></span> |<span data-ttu-id="e7059-246">上限 64 個字元</span><span class="sxs-lookup"><span data-stu-id="e7059-246">Maximum of 64 characters</span></span> | |
| <span data-ttu-id="e7059-247">Uri</span><span class="sxs-lookup"><span data-stu-id="e7059-247">Uri</span></span> |<span data-ttu-id="e7059-248">X</span><span class="sxs-lookup"><span data-stu-id="e7059-248">X</span></span> |<span data-ttu-id="e7059-249">URI</span><span class="sxs-lookup"><span data-stu-id="e7059-249">URI</span></span> | | |

### <a name="additional-properties"></a><span data-ttu-id="e7059-250">其他屬性</span><span class="sxs-lookup"><span data-stu-id="e7059-250">Additional properties</span></span>
<span data-ttu-id="e7059-251">加法 toohello 前面中繼資料，在 Marketplace 作者可以提供自訂的索引鍵/值組資料，在下列形式的 hello:</span><span class="sxs-lookup"><span data-stu-id="e7059-251">In addition toohello preceding metadata, Marketplace authors can provide custom key/value pair data in hello following form:</span></span>

| <span data-ttu-id="e7059-252">名稱</span><span class="sxs-lookup"><span data-stu-id="e7059-252">Name</span></span> | <span data-ttu-id="e7059-253">必要</span><span class="sxs-lookup"><span data-stu-id="e7059-253">Required</span></span> | <span data-ttu-id="e7059-254">類型</span><span class="sxs-lookup"><span data-stu-id="e7059-254">Type</span></span> | <span data-ttu-id="e7059-255">條件約束</span><span class="sxs-lookup"><span data-stu-id="e7059-255">Constraints</span></span> | <span data-ttu-id="e7059-256">說明</span><span class="sxs-lookup"><span data-stu-id="e7059-256">Description</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e7059-257">DisplayName</span><span class="sxs-lookup"><span data-stu-id="e7059-257">DisplayName</span></span> |<span data-ttu-id="e7059-258">X</span><span class="sxs-lookup"><span data-stu-id="e7059-258">X</span></span> |<span data-ttu-id="e7059-259">String</span><span class="sxs-lookup"><span data-stu-id="e7059-259">String</span></span> |<span data-ttu-id="e7059-260">上限 25 個字元</span><span class="sxs-lookup"><span data-stu-id="e7059-260">Maximum of 25 characters</span></span> | |
| <span data-ttu-id="e7059-261">值</span><span class="sxs-lookup"><span data-stu-id="e7059-261">Value</span></span> |<span data-ttu-id="e7059-262">X</span><span class="sxs-lookup"><span data-stu-id="e7059-262">X</span></span> |<span data-ttu-id="e7059-263">String</span><span class="sxs-lookup"><span data-stu-id="e7059-263">String</span></span> |<span data-ttu-id="e7059-264">上限 30 個字元</span><span class="sxs-lookup"><span data-stu-id="e7059-264">Maximum of 30 characters</span></span> | |

### <a name="html-sanitization"></a><span data-ttu-id="e7059-265">HTML 病毒掃描</span><span class="sxs-lookup"><span data-stu-id="e7059-265">HTML sanitization</span></span>
<span data-ttu-id="e7059-266">允許 HTML 的任何欄位，hello 下列項目和屬性可：</span><span class="sxs-lookup"><span data-stu-id="e7059-266">For any field that allows HTML, hello following elements and attributes are allowed:</span></span>

<span data-ttu-id="e7059-267">h1、h2、h3、h4、h5、p、ol、ul、li、a[target|href]、br、strong、em、b、i</span><span class="sxs-lookup"><span data-stu-id="e7059-267">h1, h2, h3, h4, h5, p, ol, ul, li, a[target|href], br, strong, em, b, i</span></span>

## <a name="reference-marketplace-item-ui"></a><span data-ttu-id="e7059-268">參考：Marketplace 項目 UI</span><span class="sxs-lookup"><span data-stu-id="e7059-268">Reference: Marketplace item UI</span></span>
<span data-ttu-id="e7059-269">圖示和文字 hello Azure 堆疊入口網站中所見的 Marketplace 項目為，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e7059-269">Icons and text for Marketplace items as seen in hello Azure Stack portal are as follows.</span></span>

### <a name="create-blade"></a><span data-ttu-id="e7059-270">建立刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="e7059-270">Create blade</span></span>
![建立刀鋒視窗](media/azure-stack-marketplace-item-ui-reference/image1.png)

### <a name="marketplace-item-details-blade"></a><span data-ttu-id="e7059-272">Marketplace 項目詳細資料刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="e7059-272">Marketplace item details blade</span></span>
![Marketplace 項目詳細資料刀鋒視窗](media/azure-stack-marketplace-item-ui-reference/image3.png)

