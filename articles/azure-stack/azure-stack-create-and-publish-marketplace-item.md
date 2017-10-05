---
title: "在 Azure Stack 中建立和發佈 Marketplace 項目 | Microsoft Azure"
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
ms.openlocfilehash: f1a04567e86ebea722a7de6a86117a49d1205966
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-publish-a-marketplace-item"></a><span data-ttu-id="eb2fa-103">建立及發行 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="eb2fa-103">Create and publish a Marketplace item</span></span>
## <a name="create-a-marketplace-item"></a><span data-ttu-id="eb2fa-104">建立 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="eb2fa-104">Create a Marketplace item</span></span>
1. <span data-ttu-id="eb2fa-105">[下載](http://www.aka.ms/azurestackmarketplaceitem) Azure Gallery Packager 工具和範例 Azure Stack Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-105">[Download](http://www.aka.ms/azurestackmarketplaceitem) the Azure Gallery Packager tool and the sample Azure Stack Marketplace item.</span></span>
2. <span data-ttu-id="eb2fa-106">開啟範例 Marketplace 項目，並重新命名 **SimpleVMTemplate** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-106">Open the sample Marketplace item and rename the **SimpleVMTemplate** folder.</span></span> <span data-ttu-id="eb2fa-107">(使用與您的 Marketplace 項目相同的名稱 - 例如 **Contoso.TodoList**。)此資料夾包含：</span><span class="sxs-lookup"><span data-stu-id="eb2fa-107">(Use the same name as your Marketplace item--for example, **Contoso.TodoList**.) This folder contains:</span></span>
   
       /Contoso.TodoList/
       /Contoso.TodoList/Manifest.json
       /Contoso.TodoList/UIDefinition.json
       /Contoso.TodoList/Icons/
       /Contoso.TodoList/Strings/
       /Contoso.TodoList/DeploymentTemplates/
3. <span data-ttu-id="eb2fa-108">[建立 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)，或從 GitHub 選擇範本。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-108">[Create an Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) or choose a template from GitHub.</span></span> <span data-ttu-id="eb2fa-109">Marketplace 項目會使用此範本來建立資源。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-109">The Marketplace item uses this template to create a resource.</span></span>
4. <span data-ttu-id="eb2fa-110">若要確定可以成功部署資源，請使用 Microsoft Azure Stack API 來測試範本。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-110">To make sure that the resource can be deployed successfully, test the template with the Microsoft Azure Stack APIs.</span></span>
5. <span data-ttu-id="eb2fa-111">如果您的範本依賴於虛擬機器映像，請遵循指示來[將虛擬機器映像新增至 Azure Stack](azure-stack-add-vm-image.md)。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-111">If your template relies on a virtual machine image, follow the instructions to [add a virtual machine image to Azure Stack](azure-stack-add-vm-image.md).</span></span>
6. <span data-ttu-id="eb2fa-112">將 Azure Resource Manager 範本儲存在 **/Contoso.TodoList/DeploymentTemplates/** 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-112">Save your Azure Resource Manager template in the **/Contoso.TodoList/DeploymentTemplates/** folder.</span></span>
7. <span data-ttu-id="eb2fa-113">選擇您的 Marketplace 項目的圖示和文字。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-113">Choose the icons and text for your Marketplace item.</span></span> <span data-ttu-id="eb2fa-114">將圖示新增至 **Icons** 資料夾，以及將文字新增至 **Strings** 資料夾的 **resources** 檔案中。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-114">Add icons to the **Icons** folder, and add text to the **resources** file in the **Strings** folder.</span></span> <span data-ttu-id="eb2fa-115">使用 Small、Medium、Large 和 Wide 圖示命名慣例。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-115">Use the Small, Medium, Large, and Wide naming convention for icons.</span></span> <span data-ttu-id="eb2fa-116">如需詳細的說明，請參閱 [Marketplace 項目 UI 參考](#reference-marketplace-item-ui)。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-116">See [Marketplace item UI reference](#reference-marketplace-item-ui) for a detailed description.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="eb2fa-117">需要全部四個圖示大小 (小、中、大、寬) 才能正確建立 Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-117">All four icon sizes (small, medium, large, wide) are required for building the Marketplace item correctly.</span></span>
   > 
   > 
8. <span data-ttu-id="eb2fa-118">在 **manifest.json** 檔案中，將 [名稱] 變更為您的 Marketplace 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-118">In the **manifest.json** file, change **name** to the name of your Marketplace item.</span></span> <span data-ttu-id="eb2fa-119">同時將 [發行者] 變更為您的姓名或公司。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-119">Also change **publisher** to your name or company.</span></span>
9. <span data-ttu-id="eb2fa-120">在 [構件] 下，將 [名稱] 和 [路徑] 變更為您所併入 Azure Resource Manager 範本的正確資訊。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-120">Under **artifacts**, change **name** and **path** to the correct information for the Azure Resource Manager template that you included.</span></span>
   
         "artifacts": [
            {
                "name": "Type your template name",
                "type": "Template",
                "path": "DeploymentTemplates\\Type your path",
                "isDefault": true
            }
10. <span data-ttu-id="eb2fa-121">將**我的 Marketplace 項目**取代為您的 Marketplace 項目應出現位置的目錄清單。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-121">Replace **My Marketplace Items** with a list of the categories where your Marketplace item should appear.</span></span>
    
             "categories":[
                 "My Marketplace Items"
              ],
11. <span data-ttu-id="eb2fa-122">若要對 manifest.json 進行任何進一步的編輯，請參閱[參考：Marketplace 項目 manifest.json](#reference-marketplace-item-manifestjson)。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-122">For any further edits to manifest.json, refer to [Reference: Marketplace item manifest.json](#reference-marketplace-item-manifestjson).</span></span>
12. <span data-ttu-id="eb2fa-123">若要將資料夾封裝到 .azpkg 檔案中，請開啟命令提示字元，然後執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="eb2fa-123">To package the folders into an .azpkg file, open a command prompt and run the following command:</span></span>
    
        AzureGalleryPackager.exe package –m <path to manifest.json> -o <output location for the package>
    
    > [!NOTE]
    > <span data-ttu-id="eb2fa-124">輸出套件的完整路徑必須存在。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-124">The full path to the output package must exist.</span></span> <span data-ttu-id="eb2fa-125">例如，如果輸出路徑是 C:\MarketPlaceItem\yourpackage.azpkg，資料夾 C:\MarketPlaceItem 必須存在。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-125">For example, if the output path is C:\MarketPlaceItem\yourpackage.azpkg, the folder C:\MarketPlaceItem must exist.</span></span>
    > 
    > 

## <a name="publish-a-marketplace-item"></a><span data-ttu-id="eb2fa-126">發佈 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="eb2fa-126">Publish a Marketplace item</span></span>
1. <span data-ttu-id="eb2fa-127">使用 PowerShell 或 Azure 儲存體總管來將您的 Marketplace 項目 (.azpkg) 上傳至 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-127">Use PowerShell or Azure Storage Explorer to upload your Marketplace item (.azpkg) to Azure Blob storage.</span></span> <span data-ttu-id="eb2fa-128">您可以上傳至本機 Azure Stack 儲存體，或上傳至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-128">You can upload to local Azure Stack storage or upload to Azure Storage.</span></span> <span data-ttu-id="eb2fa-129">(它是套件的暫存位置。)請確定 Blob 可公開存取。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-129">(It's a temporary location for the package.) Make sure that the blob is publicly accessible.</span></span>
2. <span data-ttu-id="eb2fa-130">在 Microsoft Azure Stack 環境中的用戶端虛擬機器上，確定您的 PowerShell 工作階段已設有您服務系統管理員的認證。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-130">On the client virtual machine in the Microsoft Azure Stack environment, make sure that your PowerShell session is set up with your service administrator credentials.</span></span> <span data-ttu-id="eb2fa-131">您可以在[使用 PowerShell 部署範本](azure-stack-deploy-template-powershell.md)中找到如何在 Azure Stack 中驗證 PowerShell 的指示。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-131">You can find instructions for how to authenticate PowerShell in Azure Stack in [Deploy a template with PowerShell](azure-stack-deploy-template-powershell.md).</span></span>
3. <span data-ttu-id="eb2fa-132">使用 **Add-AzureRMGalleryItem** PowerShell Cmdlet，將 Marketplace 項目發佈至 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-132">Use the **Add-AzureRMGalleryItem** PowerShell cmdlet to publish the Marketplace item to Azure Stack.</span></span> <span data-ttu-id="eb2fa-133">例如：</span><span class="sxs-lookup"><span data-stu-id="eb2fa-133">For example:</span></span>
   
       Add-AzureRMGalleryItem -GalleryItemUri `
       https://sample.blob.core.windows.net/gallerypackages/Microsoft.SimpleTemplate.1.0.0.azpkg –Verbose
   
   | <span data-ttu-id="eb2fa-134">參數</span><span class="sxs-lookup"><span data-stu-id="eb2fa-134">Parameter</span></span> | <span data-ttu-id="eb2fa-135">說明</span><span class="sxs-lookup"><span data-stu-id="eb2fa-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="eb2fa-136">SubscriptionID</span><span class="sxs-lookup"><span data-stu-id="eb2fa-136">SubscriptionID</span></span> |<span data-ttu-id="eb2fa-137">管理訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-137">Admin subscription ID.</span></span> <span data-ttu-id="eb2fa-138">您可以使用 PowerShell 來擷取它。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-138">You can retrieve it by using PowerShell.</span></span> <span data-ttu-id="eb2fa-139">如果您偏好在入口網站中取得它，請移至提供者的訂用帳戶，並複製該訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-139">If you'd prefer to get it in the portal, go to the provider subscription and copy the subscription ID.</span></span> |
   | <span data-ttu-id="eb2fa-140">GalleryItemUri</span><span class="sxs-lookup"><span data-stu-id="eb2fa-140">GalleryItemUri</span></span> |<span data-ttu-id="eb2fa-141">已上傳至儲存體的您的資源庫套件的 Blob URI。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-141">Blob URI for your gallery package that has already been uploaded to storage.</span></span> |
   | <span data-ttu-id="eb2fa-142">Apiversion</span><span class="sxs-lookup"><span data-stu-id="eb2fa-142">Apiversion</span></span> |<span data-ttu-id="eb2fa-143">設定為 **2015-04-01**。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-143">Set as **2015-04-01**.</span></span> |
4. <span data-ttu-id="eb2fa-144">移至入口網站。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-144">Go to the portal.</span></span> <span data-ttu-id="eb2fa-145">身為系統管理員或租用戶的使用者，現在可以在入口網站中看到 Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-145">You can now see the Marketplace item in the portal--as an admin or as a tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="eb2fa-146">套件可能需要幾分鐘才會出現。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-146">The package might take several minutes to appear.</span></span>
   > 
   > 
5. <span data-ttu-id="eb2fa-147">您的 Marketplace 項目現在已儲存至 Azure Stack Marketplace。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-147">Your Marketplace item has now been saved to the Azure Stack Marketplace.</span></span> <span data-ttu-id="eb2fa-148">您可以選擇將它從您的 Blob 儲存體位置刪除。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-148">You can choose to delete it from your Blob storage location.</span></span>
6. <span data-ttu-id="eb2fa-149">使用 **Remove-AzureRMGalleryItem** Cmdlet 可移除 Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-149">You can remove a Marketplace item by using the **Remove-AzureRMGalleryItem** cmdlet.</span></span> <span data-ttu-id="eb2fa-150">範例：</span><span class="sxs-lookup"><span data-stu-id="eb2fa-150">Example:</span></span>
   
        Remove-AzureRMGalleryItem -Name Microsoft.SimpleTemplate.1.0.0  –Verbose
   
   > [!NOTE]
   > <span data-ttu-id="eb2fa-151">移除項目之後，Marketplace UI 可能會顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-151">The Marketplace UI may show an error after you remove an item.</span></span> <span data-ttu-id="eb2fa-152">若要修正錯誤，請按一下入口網站中的 [設定]。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-152">To fix the error, click **Settings** in the portal.</span></span> <span data-ttu-id="eb2fa-153">然後，在 [入口網站自訂] 之下，選取 [捨棄修改]。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-153">Then, select **Discard modifications** under **Portal customization**.</span></span>
   > 
   > 

## <a name="reference-marketplace-item-manifestjson"></a><span data-ttu-id="eb2fa-154">參考：Marketplace 項目 manifest.json</span><span class="sxs-lookup"><span data-stu-id="eb2fa-154">Reference: Marketplace item manifest.json</span></span>
### <a name="identity-information"></a><span data-ttu-id="eb2fa-155">身分識別資訊</span><span class="sxs-lookup"><span data-stu-id="eb2fa-155">Identity information</span></span>
| <span data-ttu-id="eb2fa-156">名稱</span><span class="sxs-lookup"><span data-stu-id="eb2fa-156">Name</span></span> | <span data-ttu-id="eb2fa-157">必要</span><span class="sxs-lookup"><span data-stu-id="eb2fa-157">Required</span></span> | <span data-ttu-id="eb2fa-158">類型</span><span class="sxs-lookup"><span data-stu-id="eb2fa-158">Type</span></span> | <span data-ttu-id="eb2fa-159">條件約束</span><span class="sxs-lookup"><span data-stu-id="eb2fa-159">Constraints</span></span> | <span data-ttu-id="eb2fa-160">說明</span><span class="sxs-lookup"><span data-stu-id="eb2fa-160">Description</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="eb2fa-161">名稱</span><span class="sxs-lookup"><span data-stu-id="eb2fa-161">Name</span></span> |<span data-ttu-id="eb2fa-162">X</span><span class="sxs-lookup"><span data-stu-id="eb2fa-162">X</span></span> |<span data-ttu-id="eb2fa-163">String</span><span class="sxs-lookup"><span data-stu-id="eb2fa-163">String</span></span> |<span data-ttu-id="eb2fa-164">[A-a-za-z0-9] +</span><span class="sxs-lookup"><span data-stu-id="eb2fa-164">[A-Za-z0-9]+</span></span> | |
| <span data-ttu-id="eb2fa-165">發行者</span><span class="sxs-lookup"><span data-stu-id="eb2fa-165">Publisher</span></span> |<span data-ttu-id="eb2fa-166">X</span><span class="sxs-lookup"><span data-stu-id="eb2fa-166">X</span></span> |<span data-ttu-id="eb2fa-167">String</span><span class="sxs-lookup"><span data-stu-id="eb2fa-167">String</span></span> |<span data-ttu-id="eb2fa-168">[A-a-za-z0-9] +</span><span class="sxs-lookup"><span data-stu-id="eb2fa-168">[A-Za-z0-9]+</span></span> | |
| <span data-ttu-id="eb2fa-169">版本</span><span class="sxs-lookup"><span data-stu-id="eb2fa-169">Version</span></span> |<span data-ttu-id="eb2fa-170">X</span><span class="sxs-lookup"><span data-stu-id="eb2fa-170">X</span></span> |<span data-ttu-id="eb2fa-171">String</span><span class="sxs-lookup"><span data-stu-id="eb2fa-171">String</span></span> |[<span data-ttu-id="eb2fa-172">SemVer v2</span><span class="sxs-lookup"><span data-stu-id="eb2fa-172">SemVer v2</span></span>](http://semver.org/) | |

### <a name="metadata"></a><span data-ttu-id="eb2fa-173">中繼資料</span><span class="sxs-lookup"><span data-stu-id="eb2fa-173">Metadata</span></span>
| <span data-ttu-id="eb2fa-174">名稱</span><span class="sxs-lookup"><span data-stu-id="eb2fa-174">Name</span></span> | <span data-ttu-id="eb2fa-175">必要</span><span class="sxs-lookup"><span data-stu-id="eb2fa-175">Required</span></span> | <span data-ttu-id="eb2fa-176">類型</span><span class="sxs-lookup"><span data-stu-id="eb2fa-176">Type</span></span> | <span data-ttu-id="eb2fa-177">條件約束</span><span class="sxs-lookup"><span data-stu-id="eb2fa-177">Constraints</span></span> | <span data-ttu-id="eb2fa-178">說明</span><span class="sxs-lookup"><span data-stu-id="eb2fa-178">Description</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="eb2fa-179">DisplayName</span><span class="sxs-lookup"><span data-stu-id="eb2fa-179">DisplayName</span></span> |<span data-ttu-id="eb2fa-180">X</span><span class="sxs-lookup"><span data-stu-id="eb2fa-180">X</span></span> |<span data-ttu-id="eb2fa-181">String</span><span class="sxs-lookup"><span data-stu-id="eb2fa-181">String</span></span> |<span data-ttu-id="eb2fa-182">建議 80 個字元</span><span class="sxs-lookup"><span data-stu-id="eb2fa-182">Recommendation of 80 characters</span></span> |<span data-ttu-id="eb2fa-183">如果超過 80 個字元，入口網站可能無法正常顯示項目名稱。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-183">The portal might not display your item name gracefully if it is longer than 80 characters.</span></span> |
| <span data-ttu-id="eb2fa-184">PublisherDisplayName</span><span class="sxs-lookup"><span data-stu-id="eb2fa-184">PublisherDisplayName</span></span> |<span data-ttu-id="eb2fa-185">X</span><span class="sxs-lookup"><span data-stu-id="eb2fa-185">X</span></span> |<span data-ttu-id="eb2fa-186">String</span><span class="sxs-lookup"><span data-stu-id="eb2fa-186">String</span></span> |<span data-ttu-id="eb2fa-187">建議 30 個字元</span><span class="sxs-lookup"><span data-stu-id="eb2fa-187">Recommendation of 30 characters</span></span> |<span data-ttu-id="eb2fa-188">如果超過 30 個字元，入口網站可能無法正常顯示發行者名稱。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-188">The portal might not display your publisher name gracefully if it is longer than 30 characters.</span></span> |
| <span data-ttu-id="eb2fa-189">PublisherLegalName</span><span class="sxs-lookup"><span data-stu-id="eb2fa-189">PublisherLegalName</span></span> |<span data-ttu-id="eb2fa-190">X</span><span class="sxs-lookup"><span data-stu-id="eb2fa-190">X</span></span> |<span data-ttu-id="eb2fa-191">String</span><span class="sxs-lookup"><span data-stu-id="eb2fa-191">String</span></span> |<span data-ttu-id="eb2fa-192">上限 256 個字元</span><span class="sxs-lookup"><span data-stu-id="eb2fa-192">Maximum of 256 characters</span></span> | |
| <span data-ttu-id="eb2fa-193">摘要</span><span class="sxs-lookup"><span data-stu-id="eb2fa-193">Summary</span></span> |<span data-ttu-id="eb2fa-194">X</span><span class="sxs-lookup"><span data-stu-id="eb2fa-194">X</span></span> |<span data-ttu-id="eb2fa-195">String</span><span class="sxs-lookup"><span data-stu-id="eb2fa-195">String</span></span> |<span data-ttu-id="eb2fa-196">60 到 100 個字元</span><span class="sxs-lookup"><span data-stu-id="eb2fa-196">60 to 100 characters</span></span> | |
| <span data-ttu-id="eb2fa-197">LongSummary</span><span class="sxs-lookup"><span data-stu-id="eb2fa-197">LongSummary</span></span> |<span data-ttu-id="eb2fa-198">X</span><span class="sxs-lookup"><span data-stu-id="eb2fa-198">X</span></span> |<span data-ttu-id="eb2fa-199">String</span><span class="sxs-lookup"><span data-stu-id="eb2fa-199">String</span></span> |<span data-ttu-id="eb2fa-200">140 到 256 個字元</span><span class="sxs-lookup"><span data-stu-id="eb2fa-200">140 to 256 characters</span></span> |<span data-ttu-id="eb2fa-201">目前在 Azure Stack 中不適用。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-201">Not yet applicable in Azure Stack.</span></span> |
| <span data-ttu-id="eb2fa-202">說明</span><span class="sxs-lookup"><span data-stu-id="eb2fa-202">Description</span></span> |<span data-ttu-id="eb2fa-203">X</span><span class="sxs-lookup"><span data-stu-id="eb2fa-203">X</span></span> |[<span data-ttu-id="eb2fa-204">HTML</span><span class="sxs-lookup"><span data-stu-id="eb2fa-204">HTML</span></span>](https://auxdocs.azurewebsites.net/en-us/documentation/articles/gallery-metadata#html-sanitization) |<span data-ttu-id="eb2fa-205">500 到 5,000 個字元</span><span class="sxs-lookup"><span data-stu-id="eb2fa-205">500 to 5,000 characters</span></span> | |

### <a name="images"></a><span data-ttu-id="eb2fa-206">映像</span><span class="sxs-lookup"><span data-stu-id="eb2fa-206">Images</span></span>
<span data-ttu-id="eb2fa-207">Marketplace 會使用下列圖示：</span><span class="sxs-lookup"><span data-stu-id="eb2fa-207">The Marketplace uses the following icons:</span></span>

| <span data-ttu-id="eb2fa-208">名稱</span><span class="sxs-lookup"><span data-stu-id="eb2fa-208">Name</span></span> | <span data-ttu-id="eb2fa-209">寬度</span><span class="sxs-lookup"><span data-stu-id="eb2fa-209">Width</span></span> | <span data-ttu-id="eb2fa-210">高度</span><span class="sxs-lookup"><span data-stu-id="eb2fa-210">Height</span></span> | <span data-ttu-id="eb2fa-211">注意事項</span><span class="sxs-lookup"><span data-stu-id="eb2fa-211">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eb2fa-212">寬</span><span class="sxs-lookup"><span data-stu-id="eb2fa-212">Wide</span></span> |<span data-ttu-id="eb2fa-213">255 像素</span><span class="sxs-lookup"><span data-stu-id="eb2fa-213">255 px</span></span> |<span data-ttu-id="eb2fa-214">115 像素</span><span class="sxs-lookup"><span data-stu-id="eb2fa-214">115 px</span></span> |<span data-ttu-id="eb2fa-215">一律需要</span><span class="sxs-lookup"><span data-stu-id="eb2fa-215">Always required</span></span> |
| <span data-ttu-id="eb2fa-216">大型</span><span class="sxs-lookup"><span data-stu-id="eb2fa-216">Large</span></span> |<span data-ttu-id="eb2fa-217">115 像素</span><span class="sxs-lookup"><span data-stu-id="eb2fa-217">115 px</span></span> |<span data-ttu-id="eb2fa-218">115 像素</span><span class="sxs-lookup"><span data-stu-id="eb2fa-218">115 px</span></span> |<span data-ttu-id="eb2fa-219">一律需要</span><span class="sxs-lookup"><span data-stu-id="eb2fa-219">Always required</span></span> |
| <span data-ttu-id="eb2fa-220">中型</span><span class="sxs-lookup"><span data-stu-id="eb2fa-220">Medium</span></span> |<span data-ttu-id="eb2fa-221">90 像素</span><span class="sxs-lookup"><span data-stu-id="eb2fa-221">90 px</span></span> |<span data-ttu-id="eb2fa-222">90 像素</span><span class="sxs-lookup"><span data-stu-id="eb2fa-222">90 px</span></span> |<span data-ttu-id="eb2fa-223">一律需要</span><span class="sxs-lookup"><span data-stu-id="eb2fa-223">Always required</span></span> |
| <span data-ttu-id="eb2fa-224">小型</span><span class="sxs-lookup"><span data-stu-id="eb2fa-224">Small</span></span> |<span data-ttu-id="eb2fa-225">40 像素</span><span class="sxs-lookup"><span data-stu-id="eb2fa-225">40 px</span></span> |<span data-ttu-id="eb2fa-226">40 像素</span><span class="sxs-lookup"><span data-stu-id="eb2fa-226">40 px</span></span> |<span data-ttu-id="eb2fa-227">一律需要</span><span class="sxs-lookup"><span data-stu-id="eb2fa-227">Always required</span></span> |
| <span data-ttu-id="eb2fa-228">螢幕擷取畫面</span><span class="sxs-lookup"><span data-stu-id="eb2fa-228">Screenshot</span></span> |<span data-ttu-id="eb2fa-229">533 像素</span><span class="sxs-lookup"><span data-stu-id="eb2fa-229">533 px</span></span> |<span data-ttu-id="eb2fa-230">32 像素</span><span class="sxs-lookup"><span data-stu-id="eb2fa-230">32 px</span></span> |<span data-ttu-id="eb2fa-231">選用</span><span class="sxs-lookup"><span data-stu-id="eb2fa-231">Optional</span></span> |

### <a name="categories"></a><span data-ttu-id="eb2fa-232">類別</span><span class="sxs-lookup"><span data-stu-id="eb2fa-232">Categories</span></span>
<span data-ttu-id="eb2fa-233">每個 Marketplace 項目應該以可識別項目出現在入口網站 UI 上位置的類別加以標記。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-233">Each Marketplace item should be tagged with a category that identifies where the item appears on the portal UI.</span></span> <span data-ttu-id="eb2fa-234">您可以在 Azure Stack 中選擇其中一個現有的類別 (運算、資料 + 儲存體等等) 或選擇新的類別。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-234">You can choose one of the existing categories in Azure Stack (Compute, Data + Storage, etc.) or choose a new one.</span></span>

### <a name="links"></a><span data-ttu-id="eb2fa-235">連結</span><span class="sxs-lookup"><span data-stu-id="eb2fa-235">Links</span></span>
<span data-ttu-id="eb2fa-236">每個 Marketplace 項目可以包含各種其他內容的連結。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-236">Each Marketplace item can include various links to additional content.</span></span> <span data-ttu-id="eb2fa-237">連結已指定為名稱與 URI 的清單。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-237">The links are specified as a list of names and URIs.</span></span>

| <span data-ttu-id="eb2fa-238">名稱</span><span class="sxs-lookup"><span data-stu-id="eb2fa-238">Name</span></span> | <span data-ttu-id="eb2fa-239">必要</span><span class="sxs-lookup"><span data-stu-id="eb2fa-239">Required</span></span> | <span data-ttu-id="eb2fa-240">類型</span><span class="sxs-lookup"><span data-stu-id="eb2fa-240">Type</span></span> | <span data-ttu-id="eb2fa-241">條件約束</span><span class="sxs-lookup"><span data-stu-id="eb2fa-241">Constraints</span></span> | <span data-ttu-id="eb2fa-242">說明</span><span class="sxs-lookup"><span data-stu-id="eb2fa-242">Description</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="eb2fa-243">DisplayName</span><span class="sxs-lookup"><span data-stu-id="eb2fa-243">DisplayName</span></span> |<span data-ttu-id="eb2fa-244">X</span><span class="sxs-lookup"><span data-stu-id="eb2fa-244">X</span></span> |<span data-ttu-id="eb2fa-245">String</span><span class="sxs-lookup"><span data-stu-id="eb2fa-245">String</span></span> |<span data-ttu-id="eb2fa-246">上限 64 個字元</span><span class="sxs-lookup"><span data-stu-id="eb2fa-246">Maximum of 64 characters</span></span> | |
| <span data-ttu-id="eb2fa-247">Uri</span><span class="sxs-lookup"><span data-stu-id="eb2fa-247">Uri</span></span> |<span data-ttu-id="eb2fa-248">X</span><span class="sxs-lookup"><span data-stu-id="eb2fa-248">X</span></span> |<span data-ttu-id="eb2fa-249">URI</span><span class="sxs-lookup"><span data-stu-id="eb2fa-249">URI</span></span> | | |

### <a name="additional-properties"></a><span data-ttu-id="eb2fa-250">其他屬性</span><span class="sxs-lookup"><span data-stu-id="eb2fa-250">Additional properties</span></span>
<span data-ttu-id="eb2fa-251">除了前述中繼資料，Marketplace 作者可以下列形式提供自訂的成對索引鍵/值資料：</span><span class="sxs-lookup"><span data-stu-id="eb2fa-251">In addition to the preceding metadata, Marketplace authors can provide custom key/value pair data in the following form:</span></span>

| <span data-ttu-id="eb2fa-252">名稱</span><span class="sxs-lookup"><span data-stu-id="eb2fa-252">Name</span></span> | <span data-ttu-id="eb2fa-253">必要</span><span class="sxs-lookup"><span data-stu-id="eb2fa-253">Required</span></span> | <span data-ttu-id="eb2fa-254">類型</span><span class="sxs-lookup"><span data-stu-id="eb2fa-254">Type</span></span> | <span data-ttu-id="eb2fa-255">條件約束</span><span class="sxs-lookup"><span data-stu-id="eb2fa-255">Constraints</span></span> | <span data-ttu-id="eb2fa-256">說明</span><span class="sxs-lookup"><span data-stu-id="eb2fa-256">Description</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="eb2fa-257">DisplayName</span><span class="sxs-lookup"><span data-stu-id="eb2fa-257">DisplayName</span></span> |<span data-ttu-id="eb2fa-258">X</span><span class="sxs-lookup"><span data-stu-id="eb2fa-258">X</span></span> |<span data-ttu-id="eb2fa-259">String</span><span class="sxs-lookup"><span data-stu-id="eb2fa-259">String</span></span> |<span data-ttu-id="eb2fa-260">上限 25 個字元</span><span class="sxs-lookup"><span data-stu-id="eb2fa-260">Maximum of 25 characters</span></span> | |
| <span data-ttu-id="eb2fa-261">值</span><span class="sxs-lookup"><span data-stu-id="eb2fa-261">Value</span></span> |<span data-ttu-id="eb2fa-262">X</span><span class="sxs-lookup"><span data-stu-id="eb2fa-262">X</span></span> |<span data-ttu-id="eb2fa-263">String</span><span class="sxs-lookup"><span data-stu-id="eb2fa-263">String</span></span> |<span data-ttu-id="eb2fa-264">上限 30 個字元</span><span class="sxs-lookup"><span data-stu-id="eb2fa-264">Maximum of 30 characters</span></span> | |

### <a name="html-sanitization"></a><span data-ttu-id="eb2fa-265">HTML 病毒掃描</span><span class="sxs-lookup"><span data-stu-id="eb2fa-265">HTML sanitization</span></span>
<span data-ttu-id="eb2fa-266">任何可使用 HTML 的欄位，都可以使用下列項目與屬性：</span><span class="sxs-lookup"><span data-stu-id="eb2fa-266">For any field that allows HTML, the following elements and attributes are allowed:</span></span>

<span data-ttu-id="eb2fa-267">h1、h2、h3、h4、h5、p、ol、ul、li、a[target|href]、br、strong、em、b、i</span><span class="sxs-lookup"><span data-stu-id="eb2fa-267">h1, h2, h3, h4, h5, p, ol, ul, li, a[target|href], br, strong, em, b, i</span></span>

## <a name="reference-marketplace-item-ui"></a><span data-ttu-id="eb2fa-268">參考：Marketplace 項目 UI</span><span class="sxs-lookup"><span data-stu-id="eb2fa-268">Reference: Marketplace item UI</span></span>
<span data-ttu-id="eb2fa-269">在 Azure Stack 入口網站中所看見 Marketplace 項目的圖示和文字如下所示。</span><span class="sxs-lookup"><span data-stu-id="eb2fa-269">Icons and text for Marketplace items as seen in the Azure Stack portal are as follows.</span></span>

### <a name="create-blade"></a><span data-ttu-id="eb2fa-270">建立刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="eb2fa-270">Create blade</span></span>
![建立刀鋒視窗](media/azure-stack-marketplace-item-ui-reference/image1.png)

### <a name="marketplace-item-details-blade"></a><span data-ttu-id="eb2fa-272">Marketplace 項目詳細資料刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="eb2fa-272">Marketplace item details blade</span></span>
![Marketplace 項目詳細資料刀鋒視窗](media/azure-stack-marketplace-item-ui-reference/image3.png)

