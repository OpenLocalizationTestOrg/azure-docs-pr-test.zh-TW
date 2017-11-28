---
title: "aaaUse hello Marketplace toolkit toocreate 和發行 marketplace 項目 |Microsoft 文件"
description: "了解 tooquickly 以 hello 發行工具組所建立的 marketplace 項目"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: ByronR
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/14/2017
ms.author: helaw
ms.openlocfilehash: c1cf9ad1da44787901297eec12faf2a3dea82a6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#  <a name="add-marketplace-items-using-publishing-tool"></a><span data-ttu-id="20dfc-103">使用發佈工具新增 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="20dfc-103">Add marketplace items using publishing tool</span></span>
<span data-ttu-id="20dfc-104">加入您的內容 toohello [Marketplace</堆疊](azure-stack-marketplace.md)可讓您的方案使用 tooyou 且您的租用戶部署。</span><span class="sxs-lookup"><span data-stu-id="20dfc-104">Adding your content toohello [Azure Stack Marketplace](azure-stack-marketplace.md) makes your solutions available tooyou and your tenants for deployment.</span></span>  <span data-ttu-id="20dfc-105">hello Marketplace 工具組建立根據您的 IaaS Azure Resource Manager 範本或 VM 擴充功能的 Azure Marketplace 封裝 (.azpkg) 檔案。</span><span class="sxs-lookup"><span data-stu-id="20dfc-105">hello Marketplace Toolkit creates Azure Marketplace Packages (.azpkg) files based on your IaaS Azure Resource Manager templates or VM Extensions.</span></span>  <span data-ttu-id="20dfc-106">您也可以使用 hello Marketplace Toolkit toopublish.azpkg 檔案時，請建立具有 hello 工具或使用[手動](azure-stack-create-and-publish-marketplace-item.md)步驟。</span><span class="sxs-lookup"><span data-stu-id="20dfc-106">You can also use hello Marketplace Toolkit toopublish .azpkg files, either created with hello tool or using [manual](azure-stack-create-and-publish-marketplace-item.md) steps.</span></span>  <span data-ttu-id="20dfc-107">本主題會引導您完成下載 hello 工具、 建立 marketplace 項目，根據 VM 範本中，並再發佈該項目 toohello Marketplace</堆疊。</span><span class="sxs-lookup"><span data-stu-id="20dfc-107">This topic guides you through downloading hello tool, creating a marketplace item based on a VM template, and then publishing that item toohello Azure Stack Marketplace.</span></span>     


## <a name="prerequisites"></a><span data-ttu-id="20dfc-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="20dfc-108">Prerequisites</span></span>
 - <span data-ttu-id="20dfc-109">您必須在 hello Azure 堆疊主機上執行 hello 工具組，或具有[VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)從您執行 hello 工具所在的 hello 機器連線。</span><span class="sxs-lookup"><span data-stu-id="20dfc-109">You must run hello toolkit on hello Azure Stack host or have [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) connectivity from hello machine where you run hello tool.</span></span>

 - <span data-ttu-id="20dfc-110">下載 hello [Azure 堆疊快速入門範本](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip)和擷取。</span><span class="sxs-lookup"><span data-stu-id="20dfc-110">Download hello [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) and extract.</span></span>

 - <span data-ttu-id="20dfc-111">下載 hello [Azure 圖庫封裝工具](http://aka.ms/azurestackmarketplaceitem)(AzureGalleryPackage.exe)。</span><span class="sxs-lookup"><span data-stu-id="20dfc-111">Download hello [Azure Gallery Packaging tool](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe).</span></span> 

 - <span data-ttu-id="20dfc-112">發行 toohello marketplace 需要圖示和縮圖的檔案。</span><span class="sxs-lookup"><span data-stu-id="20dfc-112">Publishing toohello marketplace requires icons and a thumbnail file.</span></span>  <span data-ttu-id="20dfc-113">您可以使用您自己，或是儲存 hello[範例](azure-stack-marketplace-publisher.md#support-files)檔案在本機，這個範例。</span><span class="sxs-lookup"><span data-stu-id="20dfc-113">You can use your own, or save hello [sample](azure-stack-marketplace-publisher.md#support-files) files locally for this example.</span></span>

## <a name="download-hello-tool"></a><span data-ttu-id="20dfc-114">下載 hello 工具</span><span class="sxs-lookup"><span data-stu-id="20dfc-114">Download hello tool</span></span>
<span data-ttu-id="20dfc-115">hello Marketplace Toolkit 可以是[hello Azure 堆疊工具儲存機制從下載](azure-stack-powershell-download.md)。</span><span class="sxs-lookup"><span data-stu-id="20dfc-115">hello Marketplace Toolkit can be [downloaded from hello Azure Stack Tools repo](azure-stack-powershell-download.md).</span></span>


##  <a name="create-marketplace-items"></a><span data-ttu-id="20dfc-116">建立 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="20dfc-116">Create marketplace items</span></span>
<span data-ttu-id="20dfc-117">在本節中，您可以使用 hello Marketplace Toolkit toocreate.azpkg 格式 marketplace 項目封裝。</span><span class="sxs-lookup"><span data-stu-id="20dfc-117">In this section, you use hello Marketplace Toolkit toocreate a marketplace item package in .azpkg format.</span></span>  

### <a name="provide-marketplace-information-with-wizard"></a><span data-ttu-id="20dfc-118">以精靈提供 Marketplace 資訊</span><span class="sxs-lookup"><span data-stu-id="20dfc-118">Provide marketplace information with wizard</span></span>
1. <span data-ttu-id="20dfc-119">從 PowerShell 工作階段中執行 hello Marketplace 工具組：</span><span class="sxs-lookup"><span data-stu-id="20dfc-119">Run hello Marketplace Toolkit from a PowerShell session:</span></span>
```PowerShell
    .\MarketplaceToolkit.ps1
```

2. <span data-ttu-id="20dfc-120">按一下 hello**方案** 索引標籤。此畫面會接受您的 Marketplace 項目相關資訊。</span><span class="sxs-lookup"><span data-stu-id="20dfc-120">Click hello **Solution** tab.  This screen accepts information about your marketplace item.</span></span> <span data-ttu-id="20dfc-121">輸入您要它 tooappear hello marketplace 中的程式項目的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="20dfc-121">Enter information about your item as you want it tooappear in hello marketplace.</span></span>  <span data-ttu-id="20dfc-122">您也可以指定[參數檔案](azure-stack-marketplace-publisher.md#use-a-parameters-file)tooprepopulate hello 表單。</span><span class="sxs-lookup"><span data-stu-id="20dfc-122">You can also specify a [parameters file](azure-stack-marketplace-publisher.md#use-a-parameters-file) tooprepopulate hello form.</span></span>  
    
    ![Marketplace 工具組第一個畫面的螢幕擷取畫面](./media/azure-stack-marketplace-publisher/image7.png)
3. <span data-ttu-id="20dfc-124">按一下 [瀏覽] 以選取每個圖示和螢幕擷取畫面欄位的影像檔。</span><span class="sxs-lookup"><span data-stu-id="20dfc-124">Click **Browse** and select an image file for each icon and screenshot field.</span></span>  <span data-ttu-id="20dfc-125">您可以使用您自己的圖示，或 hello hello 範例圖示[支援檔案](azure-stack-marketplace-publisher.md#support-files)> 一節。</span><span class="sxs-lookup"><span data-stu-id="20dfc-125">You can use your own icons, or hello sample icons in hello [support files](azure-stack-marketplace-publisher.md#support-files) section.</span></span>
4. <span data-ttu-id="20dfc-126">一旦所有欄位都已都填入，選取 「 預覽解決方案 」 hello 方案 hello Marketplace 中的預覽。</span><span class="sxs-lookup"><span data-stu-id="20dfc-126">Once all fields are populated, select "Preview Solution" for a preview of hello solution within hello Marketplace.</span></span>  <span data-ttu-id="20dfc-127">您可以修改並編輯 hello 文字、 影像和螢幕擷取畫面後，再按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="20dfc-127">You can revise and edit hello text, images, and screenshot before clicking **Next**.</span></span>  

### <a name="import-template-and-create-package"></a><span data-ttu-id="20dfc-128">匯入範本並建立套件</span><span class="sxs-lookup"><span data-stu-id="20dfc-128">Import template and create package</span></span>
<span data-ttu-id="20dfc-129">本節中，您可以匯入 hello 範本，並為您的方案使用的輸入。</span><span class="sxs-lookup"><span data-stu-id="20dfc-129">In this section, you import hello template and work with input for your solution.</span></span>

1.  <span data-ttu-id="20dfc-130">按一下**瀏覽**和選取 hello *azuredeploy.json* hello 101 簡單的 Windows VM 資料夾中 hello 下載範本。</span><span class="sxs-lookup"><span data-stu-id="20dfc-130">Click **Browse** and select hello *azuredeploy.json* from hello 101-Simple-Windows-VM folder in hello downloaded templates.</span></span>

    ![Marketplace 工具組第二個畫面的螢幕擷取畫面](./media/azure-stack-marketplace-publisher/image8.png)
2.  <span data-ttu-id="20dfc-132">hello 部署精靈會填入*基本*hello 範本中指定每個參數的步驟和輸入項目。</span><span class="sxs-lookup"><span data-stu-id="20dfc-132">hello Deployment Wizard is populated with a *Basic* step and input items for each parameter specified in hello template.</span></span>  <span data-ttu-id="20dfc-133">您可以新增其他步驟，並在步驟之間移動輸入項。</span><span class="sxs-lookup"><span data-stu-id="20dfc-133">You can add additional steps and move inputs between steps.</span></span>  <span data-ttu-id="20dfc-134">例如，您可能會想要為您的解決方案新增「前端設定」和「後端設定」步驟。</span><span class="sxs-lookup"><span data-stu-id="20dfc-134">As an example, you may want "Front-End Configuration" and "Back-End Configuration" steps for your solution.</span></span>
3.  <span data-ttu-id="20dfc-135">指定 hello 路徑 tooAzureGalleryPackager.exe。</span><span class="sxs-lookup"><span data-stu-id="20dfc-135">Specify hello path tooAzureGalleryPackager.exe.</span></span>  
4.  <span data-ttu-id="20dfc-136">按一下**建立**並 hello Marketplace 工具組封裝您的方案到.azpkg 檔案。</span><span class="sxs-lookup"><span data-stu-id="20dfc-136">Click **Create** and hello Marketplace Toolkit packages your solution into an .azpkg file.</span></span>  <span data-ttu-id="20dfc-137">完成後，hello 精靈會顯示 hello 路徑 tooyour 方案檔和授與 hello 選項 toocontinue 發行您的封裝 tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="20dfc-137">Once complete, hello wizard displays hello path tooyour solution file and give you hello option toocontinue publishing your package tooAzure Stack.</span></span>


## <a name="publish-marketplace-items"></a><span data-ttu-id="20dfc-138">發佈 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="20dfc-138">Publish marketplace items</span></span>
<span data-ttu-id="20dfc-139">在本節中，您可以發行 hello marketplace 項目 tooyour Marketplace</堆疊。</span><span class="sxs-lookup"><span data-stu-id="20dfc-139">In this section, you publish hello marketplace item tooyour Azure Stack Marketplace.</span></span>

![Marketplace 工具組第一個畫面的螢幕擷取畫面](./media/azure-stack-marketplace-publisher/image9.png)

1.  <span data-ttu-id="20dfc-141">hello 精靈需要資訊 toopublish 方案：</span><span class="sxs-lookup"><span data-stu-id="20dfc-141">hello wizard requires information toopublish your solution:</span></span>
    
    |<span data-ttu-id="20dfc-142">欄位</span><span class="sxs-lookup"><span data-stu-id="20dfc-142">Field</span></span>|<span data-ttu-id="20dfc-143">說明</span><span class="sxs-lookup"><span data-stu-id="20dfc-143">Description</span></span>|
    |-----|-----|
    | <span data-ttu-id="20dfc-144">服務管理員名稱</span><span class="sxs-lookup"><span data-stu-id="20dfc-144">Service Admin Name</span></span> | <span data-ttu-id="20dfc-145">服務管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="20dfc-145">Service Administrator account.</span></span>  <span data-ttu-id="20dfc-146">範例：ServiceAdmin@mydomain.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="20dfc-146">Example:  ServiceAdmin@mydomain.onmicrosoft.com</span></span> |
    | <span data-ttu-id="20dfc-147">密碼</span><span class="sxs-lookup"><span data-stu-id="20dfc-147">Password</span></span> | <span data-ttu-id="20dfc-148">服務管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="20dfc-148">Password for Service Administrator account.</span></span> |
    | <span data-ttu-id="20dfc-149">API 端點</span><span class="sxs-lookup"><span data-stu-id="20dfc-149">API Endpoint</span></span> | <span data-ttu-id="20dfc-150">Azure Stack Azure Resource Manager 端點。</span><span class="sxs-lookup"><span data-stu-id="20dfc-150">Azure Stack Azure Resource Manager endpoint.</span></span>  <span data-ttu-id="20dfc-151">範例：management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="20dfc-151">Example: management.local.azurestack.external</span></span> |
2.  <span data-ttu-id="20dfc-152">按一下**發行**，顯示 hello 發行記錄。</span><span class="sxs-lookup"><span data-stu-id="20dfc-152">Click **Publish** and hello publishing log is displayed.</span></span>
3.  <span data-ttu-id="20dfc-153">您是現在可以 toodeploy hello Azure 堆疊入口網站透過您已發行的項目。</span><span class="sxs-lookup"><span data-stu-id="20dfc-153">You are now able toodeploy your published item via hello Azure Stack portal.</span></span>


## <a name="use-a-parameters-file"></a><span data-ttu-id="20dfc-154">使用參數檔案</span><span class="sxs-lookup"><span data-stu-id="20dfc-154">Use a parameters file</span></span>
<span data-ttu-id="20dfc-155">您也可以使用參數檔案 toocomplete hello marketplace 項目資訊。</span><span class="sxs-lookup"><span data-stu-id="20dfc-155">You can also use a parameters file toocomplete hello marketplace item information.</span></span>  

<span data-ttu-id="20dfc-156">hello Marketplace Toolkit 包含*solution.parameters.ps1*使用 toocreate 參數檔案。</span><span class="sxs-lookup"><span data-stu-id="20dfc-156">hello Marketplace Toolkit includes a *solution.parameters.ps1* you can use toocreate your own parameters file.</span></span>


## <a name="support-files"></a><span data-ttu-id="20dfc-157">支援檔案</span><span class="sxs-lookup"><span data-stu-id="20dfc-157">Support files</span></span>
| <span data-ttu-id="20dfc-158">說明</span><span class="sxs-lookup"><span data-stu-id="20dfc-158">Description</span></span> | <span data-ttu-id="20dfc-159">範例</span><span class="sxs-lookup"><span data-stu-id="20dfc-159">Sample</span></span> |
| ----- | ----- |
| <span data-ttu-id="20dfc-160">40 x 40.png 圖示</span><span class="sxs-lookup"><span data-stu-id="20dfc-160">40x40 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image1.png) |
| <span data-ttu-id="20dfc-161">90x90 .png 圖示</span><span class="sxs-lookup"><span data-stu-id="20dfc-161">90x90 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image2.png) |
| <span data-ttu-id="20dfc-162">115x115 .png 圖示</span><span class="sxs-lookup"><span data-stu-id="20dfc-162">115x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image3.png) |
| <span data-ttu-id="20dfc-163">255x115 .png 圖示</span><span class="sxs-lookup"><span data-stu-id="20dfc-163">255x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image4.png) |
| <span data-ttu-id="20dfc-164">533x324 .png 縮圖</span><span class="sxs-lookup"><span data-stu-id="20dfc-164">533x324 .png thumbnail</span></span> | ![](./media/azure-stack-marketplace-publisher/image5.png) |


