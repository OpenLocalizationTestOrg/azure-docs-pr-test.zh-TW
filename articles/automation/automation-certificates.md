---
title: "Azure 自動化中的憑證資產 | Microsoft Docs"
description: "憑證可以安全地儲存在 Azure 自動化中，使得 Runbook 或 DSC 組態可以存取憑證，以向 Azure 和協力廠商資源進行驗證。  這篇文章說明憑證的詳細資料，以及如何以文字和圖形化編寫形式加以使用。"
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: fd1737a420c132dace9307436bfea98a9bde94a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="0e275-104">Azure 自動化中的憑證資產</span><span class="sxs-lookup"><span data-stu-id="0e275-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="0e275-105">憑證可以安全地儲存在 Azure 自動化中，使得 Runbook 或 DSC 組態可以透過使用 Azure Resource Manager 資源的 **Get-AzureRmAutomationRmCertificate** 活動來存取憑證。</span><span class="sxs-lookup"><span data-stu-id="0e275-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using the **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="0e275-106">這可讓您建立使用憑證進行驗證的 Runbook 和 DSC 組態，或將它們新增至 Azure 或協力廠商的資源。</span><span class="sxs-lookup"><span data-stu-id="0e275-106">This allows you to create runbooks and DSC configurations that use certificates for authentication or adds them to Azure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="0e275-107">Azure 自動化中的安全資產包括認證、憑證、連接和加密的變數。</span><span class="sxs-lookup"><span data-stu-id="0e275-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="0e275-108">這些資產都會經過加密，並使用為每個自動化帳戶產生的唯一索引鍵儲存在 Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="0e275-108">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="0e275-109">這個索引鍵是由主要憑證加密，並且儲存在 Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="0e275-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="0e275-110">儲存安全資產之前，會使用主要憑證解密自動化帳戶的金鑰，然後用來加密資產。</span><span class="sxs-lookup"><span data-stu-id="0e275-110">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="0e275-111">Windows PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="0e275-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="0e275-112">下表中的 Cmdlet 是用來透過 Windows PowerShell 建立和管理自動化憑證資產。</span><span class="sxs-lookup"><span data-stu-id="0e275-112">The cmdlets in the following table are used to create and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="0e275-113">它們是隨著 [Azure PowerShell 模組](../powershell-install-configure.md) 的一部分推出，可供在自動化 Runbook 和 DSC 設定中使用。</span><span class="sxs-lookup"><span data-stu-id="0e275-113">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="0e275-114">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="0e275-114">Cmdlets</span></span>|<span data-ttu-id="0e275-115">說明</span><span class="sxs-lookup"><span data-stu-id="0e275-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="0e275-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="0e275-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="0e275-117">擷取要在 Runbook 或 DSC 組態中使用的憑證相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0e275-117">Retrieves information about a certificate to use in a runbook or DSC configuration.</span></span> <span data-ttu-id="0e275-118">您只能從 Get-AutomationCertificate 活動擷取憑證本身。</span><span class="sxs-lookup"><span data-stu-id="0e275-118">You can only retrieve the certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="0e275-119">New-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="0e275-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="0e275-120">建立新的憑證到 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="0e275-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="0e275-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="0e275-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="0e275-122">從 Azure 自動化中移除憑證。</span><span class="sxs-lookup"><span data-stu-id="0e275-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="0e275-123">建立新的憑證到 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="0e275-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="0e275-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="0e275-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="0e275-125">設定現有的憑證，包括上傳憑證檔案和設定 .pfx 的密碼屬性。</span><span class="sxs-lookup"><span data-stu-id="0e275-125">Sets the properties for an existing certificate including uploading the certificate file and setting the password for a .pfx.</span></span>|
|[<span data-ttu-id="0e275-126">Add-AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="0e275-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="0e275-127">上傳指定雲端服務的服務憑證。</span><span class="sxs-lookup"><span data-stu-id="0e275-127">Uploads a service certificate for the specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="0e275-128">建立新憑證</span><span class="sxs-lookup"><span data-stu-id="0e275-128">Creating a new certificate</span></span>

<span data-ttu-id="0e275-129">建立新憑證時，您會將 cer 或 pfx 檔案上傳到 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="0e275-129">When you create a new certificate, you upload a .cer or .pfx file to Azure Automation.</span></span> <span data-ttu-id="0e275-130">如果您將憑證標示為可匯出，那麼您可以將它傳送到 Azure 自動化憑證存放區外部。</span><span class="sxs-lookup"><span data-stu-id="0e275-130">If you mark the certificate as exportable, then you can transfer it out of the Azure Automation certificate store.</span></span> <span data-ttu-id="0e275-131">如果無法匯出，則只可以將它用在 Runbook 或 DSC 組態內的簽署。</span><span class="sxs-lookup"><span data-stu-id="0e275-131">If it is not exportable, then it can only be used for signing within the runbook or DSC configuration.</span></span>


### <a name="to-create-a-new-certificate-with-the-azure-portal"></a><span data-ttu-id="0e275-132">使用 Azure 入口網站建立新憑證</span><span class="sxs-lookup"><span data-stu-id="0e275-132">To create a new certificate with the Azure portal</span></span>

1. <span data-ttu-id="0e275-133">從您的自動化帳戶，按一下 [資產] 圖格，以開啟 [資產] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0e275-133">From your Automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
1. <span data-ttu-id="0e275-134">按一下 [憑證] 憑證，以開啟 [憑證] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0e275-134">Click the **Certificates** tile to open the **Certificates** blade.</span></span>
1. <span data-ttu-id="0e275-135">在分頁的頂端按一下 [ **加入憑證** ]。</span><span class="sxs-lookup"><span data-stu-id="0e275-135">Click **Add a certificate** at the top of the blade.</span></span>
2. <span data-ttu-id="0e275-136">在 [ **名稱** ] 方塊中輸入憑證的名稱。</span><span class="sxs-lookup"><span data-stu-id="0e275-136">Type a name for the certificate in the **Name** box.</span></span>
2. <span data-ttu-id="0e275-137">按一下 [上傳憑證檔案] 下方的 [選取檔案]，以瀏覽 .cer 或 .pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="0e275-137">Click **Select a file** under **Upload a certificate file** to browse for a .cer or .pfx file.</span></span>  <span data-ttu-id="0e275-138">如果您選取 .pfx 檔案，請指定密碼，以及是否應該允許匯出它。</span><span class="sxs-lookup"><span data-stu-id="0e275-138">If you select a .pfx file, specify a password and whether it should be allowed to be exported.</span></span>
1. <span data-ttu-id="0e275-139">按一下 [ **建立** ] 以儲存新的憑證資產。</span><span class="sxs-lookup"><span data-stu-id="0e275-139">Click **Create** to save the new certificate asset.</span></span>


### <a name="to-create-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="0e275-140">使用 Windows PowerShell 建立新憑證</span><span class="sxs-lookup"><span data-stu-id="0e275-140">To create a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="0e275-141">下列範例示範如何建立新的自動化憑證，並將其標示為可匯出。</span><span class="sxs-lookup"><span data-stu-id="0e275-141">The following example demonstrates how to create a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="0e275-142">這樣會匯入現有的 pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="0e275-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="0e275-143">使用憑證</span><span class="sxs-lookup"><span data-stu-id="0e275-143">Using a certificate</span></span>

<span data-ttu-id="0e275-144">您必須使用 **Get-AutomationCertificate** 活動以使用憑證。</span><span class="sxs-lookup"><span data-stu-id="0e275-144">You must use the **Get-AutomationCertificate** activity to use a certificate.</span></span> <span data-ttu-id="0e275-145">您不能使用 [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) Cmdlet，因為它會傳回憑證資產的相關資訊，而不是憑證本身。</span><span class="sxs-lookup"><span data-stu-id="0e275-145">You cannot use the [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about the certificate asset but not the certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="0e275-146">文字式 Runbook 範例</span><span class="sxs-lookup"><span data-stu-id="0e275-146">Textual runbook sample</span></span>

<span data-ttu-id="0e275-147">下列範例程式碼示範如何將憑證新增到 Runbook 中的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="0e275-147">The following sample code shows how to add a certificate to a cloud service in a runbook.</span></span> <span data-ttu-id="0e275-148">在此範例中，密碼是擷取自加密的自動化變數。</span><span class="sxs-lookup"><span data-stu-id="0e275-148">In this sample, the password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="0e275-149">圖形化 Runbook 範例</span><span class="sxs-lookup"><span data-stu-id="0e275-149">Graphical runbook sample</span></span>

<span data-ttu-id="0e275-150">透過在圖形化編輯器 [文件庫] 窗格的憑證上按一下滑鼠右鍵，然後選取 [加入至畫布]，即可加入 **Get-AutomationCertificate** 至圖形化 Runbook。</span><span class="sxs-lookup"><span data-stu-id="0e275-150">You add a **Get-AutomationCertificate** to a graphical runbook by right-clicking on the certificate in the Library pane of the graphical editor and selecting **Add to canvas**.</span></span>

![將憑證新增至畫布](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="0e275-152">下圖顯示在圖形化 Runbook 中使用憑證的範例。</span><span class="sxs-lookup"><span data-stu-id="0e275-152">The following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="0e275-153">這是如上所示，用於從文字式 Runbook 加入憑證至雲端服務的相同範例。</span><span class="sxs-lookup"><span data-stu-id="0e275-153">This is the same example shown above for adding a certificate to a cloud service from a textual runbook.</span></span>

![<span data-ttu-id="0e275-154">範例圖形化編寫</span><span class="sxs-lookup"><span data-stu-id="0e275-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="0e275-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0e275-155">Next steps</span></span>

- <span data-ttu-id="0e275-156">若要深入了解使用連結控制您的 Runbook 設計用來執行的活動之邏輯流程，請參閱[圖形化編寫中的連結](automation-graphical-authoring-intro.md#links-and-workflow)。</span><span class="sxs-lookup"><span data-stu-id="0e275-156">To learn more about working with links to control the logical flow of activities your runbook is designed to perform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
