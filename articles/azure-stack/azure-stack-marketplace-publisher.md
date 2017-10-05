---
title: "使用 Marketplace 工具組來建立和發佈 Marketplace 項目 | Microsoft Docs"
description: "了解如何以發佈工具組快速建立 Marketplace 項目"
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
ms.openlocfilehash: 5b2c04d2cbc06e1572dc2e40712f6cf9d886aa1e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
#  <a name="add-marketplace-items-using-publishing-tool"></a><span data-ttu-id="a23c9-103">使用發佈工具新增 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="a23c9-103">Add marketplace items using publishing tool</span></span>
<span data-ttu-id="a23c9-104">將您的內容新增到 [Azure Stack Marketplace](azure-stack-marketplace.md)，可讓您的解決方案供您和您的租用戶用於部署。</span><span class="sxs-lookup"><span data-stu-id="a23c9-104">Adding your content to the [Azure Stack Marketplace](azure-stack-marketplace.md) makes your solutions available to you and your tenants for deployment.</span></span>  <span data-ttu-id="a23c9-105">Marketplace 工具組會根據您的 IaaS Azure Resource Manager 範本或 VM 擴充功能，建立 Azure Marketplace 套件 (.azpkg) 檔案。</span><span class="sxs-lookup"><span data-stu-id="a23c9-105">The Marketplace Toolkit creates Azure Marketplace Packages (.azpkg) files based on your IaaS Azure Resource Manager templates or VM Extensions.</span></span>  <span data-ttu-id="a23c9-106">您也可以使用 Marketplace 工具組來發佈 .azpkg 檔案 (可使用此工具或使用[手動](azure-stack-create-and-publish-marketplace-item.md)步驟建立)。</span><span class="sxs-lookup"><span data-stu-id="a23c9-106">You can also use the Marketplace Toolkit to publish .azpkg files, either created with the tool or using [manual](azure-stack-create-and-publish-marketplace-item.md) steps.</span></span>  <span data-ttu-id="a23c9-107">本主題會逐步引導您下載工具、根據 VM 範本建立 Marketplace 項目，然後將該項目發佈到 Azure Stack Marketplace。</span><span class="sxs-lookup"><span data-stu-id="a23c9-107">This topic guides you through downloading the tool, creating a marketplace item based on a VM template, and then publishing that item to the Azure Stack Marketplace.</span></span>     


## <a name="prerequisites"></a><span data-ttu-id="a23c9-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="a23c9-108">Prerequisites</span></span>
 - <span data-ttu-id="a23c9-109">您必須在 Azure Stack 主機上執行此工具組，或在執行工具所在的電腦上具有 [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) 連線能力。</span><span class="sxs-lookup"><span data-stu-id="a23c9-109">You must run the toolkit on the Azure Stack host or have [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) connectivity from the machine where you run the tool.</span></span>

 - <span data-ttu-id="a23c9-110">下載 [Azure Stack 快速入門範本](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip)並解壓縮。</span><span class="sxs-lookup"><span data-stu-id="a23c9-110">Download the [Azure Stack Quickstart templates](https://github.com/Azure/AzureStack-QuickStart-Templates/archive/master.zip) and extract.</span></span>

 - <span data-ttu-id="a23c9-111">下載 [Azure 資源庫封裝工具](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe)。</span><span class="sxs-lookup"><span data-stu-id="a23c9-111">Download the [Azure Gallery Packaging tool](http://aka.ms/azurestackmarketplaceitem) (AzureGalleryPackage.exe).</span></span> 

 - <span data-ttu-id="a23c9-112">要發佈到 Marketplace 需要有圖示和縮圖檔案。</span><span class="sxs-lookup"><span data-stu-id="a23c9-112">Publishing to the marketplace requires icons and a thumbnail file.</span></span>  <span data-ttu-id="a23c9-113">您可以使用自己的檔案，或是將此範例的[範例](azure-stack-marketplace-publisher.md#support-files)檔案儲存到本機上。</span><span class="sxs-lookup"><span data-stu-id="a23c9-113">You can use your own, or save the [sample](azure-stack-marketplace-publisher.md#support-files) files locally for this example.</span></span>

## <a name="download-the-tool"></a><span data-ttu-id="a23c9-114">下載工具</span><span class="sxs-lookup"><span data-stu-id="a23c9-114">Download the tool</span></span>
<span data-ttu-id="a23c9-115">可從 [Azure Stack 工具存放庫](azure-stack-powershell-download.md)下載 Marketplace 工具組。</span><span class="sxs-lookup"><span data-stu-id="a23c9-115">The Marketplace Toolkit can be [downloaded from the Azure Stack Tools repo](azure-stack-powershell-download.md).</span></span>


##  <a name="create-marketplace-items"></a><span data-ttu-id="a23c9-116">建立 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="a23c9-116">Create marketplace items</span></span>
<span data-ttu-id="a23c9-117">在本節中，您會使用 Marketplace 工具組建立 .azpkg 格式的 Marketplace 項目套件。</span><span class="sxs-lookup"><span data-stu-id="a23c9-117">In this section, you use the Marketplace Toolkit to create a marketplace item package in .azpkg format.</span></span>  

### <a name="provide-marketplace-information-with-wizard"></a><span data-ttu-id="a23c9-118">以精靈提供 Marketplace 資訊</span><span class="sxs-lookup"><span data-stu-id="a23c9-118">Provide marketplace information with wizard</span></span>
1. <span data-ttu-id="a23c9-119">從 PowerShell 工作階段中執行 Marketplace 工具組：</span><span class="sxs-lookup"><span data-stu-id="a23c9-119">Run the Marketplace Toolkit from a PowerShell session:</span></span>
```PowerShell
    .\MarketplaceToolkit.ps1
```

2. <span data-ttu-id="a23c9-120">按一下 [解決方案] 索引標籤。此畫面會接受您的 Marketplace 項目相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a23c9-120">Click the **Solution** tab.  This screen accepts information about your marketplace item.</span></span> <span data-ttu-id="a23c9-121">請輸入您想要顯示在 Marketplace 中的項目相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a23c9-121">Enter information about your item as you want it to appear in the marketplace.</span></span>  <span data-ttu-id="a23c9-122">您也可以指定[參數檔案](azure-stack-marketplace-publisher.md#use-a-parameters-file)來預先填入表單。</span><span class="sxs-lookup"><span data-stu-id="a23c9-122">You can also specify a [parameters file](azure-stack-marketplace-publisher.md#use-a-parameters-file) to prepopulate the form.</span></span>  
    
    ![Marketplace 工具組第一個畫面的螢幕擷取畫面](./media/azure-stack-marketplace-publisher/image7.png)
3. <span data-ttu-id="a23c9-124">按一下 [瀏覽] 以選取每個圖示和螢幕擷取畫面欄位的影像檔。</span><span class="sxs-lookup"><span data-stu-id="a23c9-124">Click **Browse** and select an image file for each icon and screenshot field.</span></span>  <span data-ttu-id="a23c9-125">您可以使用自己的圖示，或[支援檔案](azure-stack-marketplace-publisher.md#support-files)一節中的範例圖示。</span><span class="sxs-lookup"><span data-stu-id="a23c9-125">You can use your own icons, or the sample icons in the [support files](azure-stack-marketplace-publisher.md#support-files) section.</span></span>
4. <span data-ttu-id="a23c9-126">一旦所有欄位都已填入，請選取「預覽解決方案」來預覽 Marketplace 內的解決方案。</span><span class="sxs-lookup"><span data-stu-id="a23c9-126">Once all fields are populated, select "Preview Solution" for a preview of the solution within the Marketplace.</span></span>  <span data-ttu-id="a23c9-127">您可以修改並編輯文字、影像和螢幕擷取畫面後，再按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a23c9-127">You can revise and edit the text, images, and screenshot before clicking **Next**.</span></span>  

### <a name="import-template-and-create-package"></a><span data-ttu-id="a23c9-128">匯入範本並建立套件</span><span class="sxs-lookup"><span data-stu-id="a23c9-128">Import template and create package</span></span>
<span data-ttu-id="a23c9-129">在本節中，您會匯入範本並使用解決方案的輸入。</span><span class="sxs-lookup"><span data-stu-id="a23c9-129">In this section, you import the template and work with input for your solution.</span></span>

1.  <span data-ttu-id="a23c9-130">按一下 [瀏覽] 並從所下載範本的 101-Simple-Windows-VM 資料夾中選取 *azuredeploy.json*。</span><span class="sxs-lookup"><span data-stu-id="a23c9-130">Click **Browse** and select the *azuredeploy.json* from the 101-Simple-Windows-VM folder in the downloaded templates.</span></span>

    ![Marketplace 工具組第二個畫面的螢幕擷取畫面](./media/azure-stack-marketplace-publisher/image8.png)
2.  <span data-ttu-id="a23c9-132">「部署精靈」中會填入 [基本] 步驟，以及範本中所指定每個參數的輸入項目。</span><span class="sxs-lookup"><span data-stu-id="a23c9-132">The Deployment Wizard is populated with a *Basic* step and input items for each parameter specified in the template.</span></span>  <span data-ttu-id="a23c9-133">您可以新增其他步驟，並在步驟之間移動輸入項。</span><span class="sxs-lookup"><span data-stu-id="a23c9-133">You can add additional steps and move inputs between steps.</span></span>  <span data-ttu-id="a23c9-134">例如，您可能會想要為您的解決方案新增「前端設定」和「後端設定」步驟。</span><span class="sxs-lookup"><span data-stu-id="a23c9-134">As an example, you may want "Front-End Configuration" and "Back-End Configuration" steps for your solution.</span></span>
3.  <span data-ttu-id="a23c9-135">請指定 AzureGalleryPackager.exe 的路徑。</span><span class="sxs-lookup"><span data-stu-id="a23c9-135">Specify the path to AzureGalleryPackager.exe.</span></span>  
4.  <span data-ttu-id="a23c9-136">按一下 [建立]，然後 Marketplace 工具組便會將您的解決方案封裝到 .azpkg 檔案中。</span><span class="sxs-lookup"><span data-stu-id="a23c9-136">Click **Create** and the Marketplace Toolkit packages your solution into an .azpkg file.</span></span>  <span data-ttu-id="a23c9-137">完成後，精靈會顯示您的解決方案檔案路徑，並讓您選擇繼續將您的套件發佈到 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="a23c9-137">Once complete, the wizard displays the path to your solution file and give you the option to continue publishing your package to Azure Stack.</span></span>


## <a name="publish-marketplace-items"></a><span data-ttu-id="a23c9-138">發佈 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="a23c9-138">Publish marketplace items</span></span>
<span data-ttu-id="a23c9-139">在本節中，您會將您的 Marketplace 項目發佈到 Azure Stack Marketplace。</span><span class="sxs-lookup"><span data-stu-id="a23c9-139">In this section, you publish the marketplace item to your Azure Stack Marketplace.</span></span>

![Marketplace 工具組第一個畫面的螢幕擷取畫面](./media/azure-stack-marketplace-publisher/image9.png)

1.  <span data-ttu-id="a23c9-141">精靈需要下列資訊來發佈您的解決方案：</span><span class="sxs-lookup"><span data-stu-id="a23c9-141">The wizard requires information to publish your solution:</span></span>
    
    |<span data-ttu-id="a23c9-142">欄位</span><span class="sxs-lookup"><span data-stu-id="a23c9-142">Field</span></span>|<span data-ttu-id="a23c9-143">說明</span><span class="sxs-lookup"><span data-stu-id="a23c9-143">Description</span></span>|
    |-----|-----|
    | <span data-ttu-id="a23c9-144">服務管理員名稱</span><span class="sxs-lookup"><span data-stu-id="a23c9-144">Service Admin Name</span></span> | <span data-ttu-id="a23c9-145">服務管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="a23c9-145">Service Administrator account.</span></span>  <span data-ttu-id="a23c9-146">範例：ServiceAdmin@mydomain.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="a23c9-146">Example:  ServiceAdmin@mydomain.onmicrosoft.com</span></span> |
    | <span data-ttu-id="a23c9-147">密碼</span><span class="sxs-lookup"><span data-stu-id="a23c9-147">Password</span></span> | <span data-ttu-id="a23c9-148">服務管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="a23c9-148">Password for Service Administrator account.</span></span> |
    | <span data-ttu-id="a23c9-149">API 端點</span><span class="sxs-lookup"><span data-stu-id="a23c9-149">API Endpoint</span></span> | <span data-ttu-id="a23c9-150">Azure Stack Azure Resource Manager 端點。</span><span class="sxs-lookup"><span data-stu-id="a23c9-150">Azure Stack Azure Resource Manager endpoint.</span></span>  <span data-ttu-id="a23c9-151">範例：management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="a23c9-151">Example: management.local.azurestack.external</span></span> |
2.  <span data-ttu-id="a23c9-152">按一下 [發佈]，發佈記錄隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="a23c9-152">Click **Publish** and the publishing log is displayed.</span></span>
3.  <span data-ttu-id="a23c9-153">您現在已可透過 Azure Stack 入口網站部署您發佈的項目。</span><span class="sxs-lookup"><span data-stu-id="a23c9-153">You are now able to deploy your published item via the Azure Stack portal.</span></span>


## <a name="use-a-parameters-file"></a><span data-ttu-id="a23c9-154">使用參數檔案</span><span class="sxs-lookup"><span data-stu-id="a23c9-154">Use a parameters file</span></span>
<span data-ttu-id="a23c9-155">您也可以使用參數檔案來完成 Marketplace 項目資訊。</span><span class="sxs-lookup"><span data-stu-id="a23c9-155">You can also use a parameters file to complete the marketplace item information.</span></span>  

<span data-ttu-id="a23c9-156">Marketplace 工具組包含 *solution.parameters.ps1*，可用來建立您自己的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="a23c9-156">The Marketplace Toolkit includes a *solution.parameters.ps1* you can use to create your own parameters file.</span></span>


## <a name="support-files"></a><span data-ttu-id="a23c9-157">支援檔案</span><span class="sxs-lookup"><span data-stu-id="a23c9-157">Support files</span></span>
| <span data-ttu-id="a23c9-158">說明</span><span class="sxs-lookup"><span data-stu-id="a23c9-158">Description</span></span> | <span data-ttu-id="a23c9-159">範例</span><span class="sxs-lookup"><span data-stu-id="a23c9-159">Sample</span></span> |
| ----- | ----- |
| <span data-ttu-id="a23c9-160">40 x 40.png 圖示</span><span class="sxs-lookup"><span data-stu-id="a23c9-160">40x40 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image1.png) |
| <span data-ttu-id="a23c9-161">90x90 .png 圖示</span><span class="sxs-lookup"><span data-stu-id="a23c9-161">90x90 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image2.png) |
| <span data-ttu-id="a23c9-162">115x115 .png 圖示</span><span class="sxs-lookup"><span data-stu-id="a23c9-162">115x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image3.png) |
| <span data-ttu-id="a23c9-163">255x115 .png 圖示</span><span class="sxs-lookup"><span data-stu-id="a23c9-163">255x115 .png icon</span></span> | ![](./media/azure-stack-marketplace-publisher/image4.png) |
| <span data-ttu-id="a23c9-164">533x324 .png 縮圖</span><span class="sxs-lookup"><span data-stu-id="a23c9-164">533x324 .png thumbnail</span></span> | ![](./media/azure-stack-marketplace-publisher/image5.png) |


