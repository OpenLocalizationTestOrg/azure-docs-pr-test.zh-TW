---
title: "在 Azure 自動化中的 aaaCertificate 資產 |Microsoft 文件"
description: "讓 runbook 或針對 Azure 和協力廠商資源的 DSC 組態 tooauthenticate 存取，則可以在 Azure 自動化中安全地儲存憑證。  這篇文章說明憑證的 hello 詳細資料以及如何與它們的 toowork 文字及圖形化撰寫。"
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
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="7f887-104">Azure 自動化中的憑證資產</span><span class="sxs-lookup"><span data-stu-id="7f887-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="7f887-105">憑證可以安全地存放在 Azure 自動化中以便存取 runbook 的 DSC 設定使用 hello **Get AzureRmAutomationRmCertificate** Azure 資源管理員資源的活動。</span><span class="sxs-lookup"><span data-stu-id="7f887-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using hello **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="7f887-106">這可讓您 toocreate runbook 和使用憑證進行驗證的 DSC 設定，或將它們加入 tooAzure 或協力廠商資源。</span><span class="sxs-lookup"><span data-stu-id="7f887-106">This allows you toocreate runbooks and DSC configurations that use certificates for authentication or adds them tooAzure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="7f887-107">Azure 自動化中的安全資產包括認證、憑證、連接和加密的變數。</span><span class="sxs-lookup"><span data-stu-id="7f887-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="7f887-108">這些資產都會經過加密並儲存在 hello 使用產生的唯一索引鍵，每個自動化帳戶的 Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="7f887-108">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="7f887-109">這個索引鍵是由主要憑證加密，並且儲存在 Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="7f887-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="7f887-110">之前儲存安全資產，hello 自動化帳戶的 hello 金鑰會解密使用 hello 主要憑證，並接著使用 tooencrypt hello 資產。</span><span class="sxs-lookup"><span data-stu-id="7f887-110">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="7f887-111">Windows PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="7f887-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="7f887-112">hello 下表中的 hello cmdlet 會使用的 toocreate 和管理使用 Windows PowerShell 的自動化憑證資產。</span><span class="sxs-lookup"><span data-stu-id="7f887-112">hello cmdlets in hello following table are used toocreate and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="7f887-113">這些 cmdlet 隨附 hello [Azure PowerShell 模組](../powershell-install-configure.md)可用於自動化 runbook 和 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="7f887-113">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="7f887-114">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="7f887-114">Cmdlets</span></span>|<span data-ttu-id="7f887-115">說明</span><span class="sxs-lookup"><span data-stu-id="7f887-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="7f887-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="7f887-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="7f887-117">擷取憑證 toouse runbook 或 DSC 設定中的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7f887-117">Retrieves information about a certificate toouse in a runbook or DSC configuration.</span></span> <span data-ttu-id="7f887-118">您只能從 Get-automationcertificat 活動擷取 hello 憑證本身。</span><span class="sxs-lookup"><span data-stu-id="7f887-118">You can only retrieve hello certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="7f887-119">New-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="7f887-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="7f887-120">建立新的憑證到 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="7f887-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="7f887-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="7f887-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="7f887-122">從 Azure 自動化中移除憑證。</span><span class="sxs-lookup"><span data-stu-id="7f887-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="7f887-123">建立新的憑證到 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="7f887-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="7f887-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="7f887-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="7f887-125">設定包括 hello 憑證檔案和設定.pfx 的 hello 密碼上傳現有憑證的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="7f887-125">Sets hello properties for an existing certificate including uploading hello certificate file and setting hello password for a .pfx.</span></span>|
|[<span data-ttu-id="7f887-126">Add-AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="7f887-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="7f887-127">上傳服務憑證的 hello 指定雲端服務。</span><span class="sxs-lookup"><span data-stu-id="7f887-127">Uploads a service certificate for hello specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="7f887-128">建立新憑證</span><span class="sxs-lookup"><span data-stu-id="7f887-128">Creating a new certificate</span></span>

<span data-ttu-id="7f887-129">當您建立新的憑證時，您上傳.cer 或.pfx 檔案 tooAzure 自動化。</span><span class="sxs-lookup"><span data-stu-id="7f887-129">When you create a new certificate, you upload a .cer or .pfx file tooAzure Automation.</span></span> <span data-ttu-id="7f887-130">如果您要標示為可匯出的 hello 憑證，則可以將它從 hello Azure 自動化憑證存放區。</span><span class="sxs-lookup"><span data-stu-id="7f887-130">If you mark hello certificate as exportable, then you can transfer it out of hello Azure Automation certificate store.</span></span> <span data-ttu-id="7f887-131">如果不是可匯出，然後它只能用於簽章 hello runbook 或 DSC 設定內。</span><span class="sxs-lookup"><span data-stu-id="7f887-131">If it is not exportable, then it can only be used for signing within hello runbook or DSC configuration.</span></span>


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a><span data-ttu-id="7f887-132">toocreate hello Azure 入口網站的新憑證</span><span class="sxs-lookup"><span data-stu-id="7f887-132">toocreate a new certificate with hello Azure portal</span></span>

1. <span data-ttu-id="7f887-133">從您的自動化帳戶，按一下 hello**資產**磚 tooopen hello**資產**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7f887-133">From your Automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
1. <span data-ttu-id="7f887-134">按一下 hello**憑證**磚 tooopen hello**憑證**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7f887-134">Click hello **Certificates** tile tooopen hello **Certificates** blade.</span></span>
1. <span data-ttu-id="7f887-135">按一下**將憑證加入**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="7f887-135">Click **Add a certificate** at hello top of hello blade.</span></span>
2. <span data-ttu-id="7f887-136">輸入 hello 憑證的名稱在 hello**名稱**方塊。</span><span class="sxs-lookup"><span data-stu-id="7f887-136">Type a name for hello certificate in hello **Name** box.</span></span>
2. <span data-ttu-id="7f887-137">按一下**選取檔案**下**憑證檔案上傳**toobrowse.cer 或.pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="7f887-137">Click **Select a file** under **Upload a certificate file** toobrowse for a .cer or .pfx file.</span></span>  <span data-ttu-id="7f887-138">如果您選取.pfx 檔案，指定密碼，以及是否應該允許 toobe 匯出。</span><span class="sxs-lookup"><span data-stu-id="7f887-138">If you select a .pfx file, specify a password and whether it should be allowed toobe exported.</span></span>
1. <span data-ttu-id="7f887-139">按一下**建立**toosave hello 新憑證資產。</span><span class="sxs-lookup"><span data-stu-id="7f887-139">Click **Create** toosave hello new certificate asset.</span></span>


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="7f887-140">toocreate Windows PowerShell 的新憑證</span><span class="sxs-lookup"><span data-stu-id="7f887-140">toocreate a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="7f887-141">hello 下列範例會示範如何 toocreate 新的自動化憑證，並將它標示為可匯出。</span><span class="sxs-lookup"><span data-stu-id="7f887-141">hello following example demonstrates how toocreate a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="7f887-142">這樣會匯入現有的 pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="7f887-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="7f887-143">使用憑證</span><span class="sxs-lookup"><span data-stu-id="7f887-143">Using a certificate</span></span>

<span data-ttu-id="7f887-144">您必須使用 hello **Get-automationcertificat**活動 toouse 憑證。</span><span class="sxs-lookup"><span data-stu-id="7f887-144">You must use hello **Get-AutomationCertificate** activity toouse a certificate.</span></span> <span data-ttu-id="7f887-145">您無法使用 hello [Get AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet，因為它會傳回 hello 憑證資產，但不是 hello 憑證本身的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7f887-145">You cannot use hello [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about hello certificate asset but not hello certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="7f887-146">文字式 Runbook 範例</span><span class="sxs-lookup"><span data-stu-id="7f887-146">Textual runbook sample</span></span>

<span data-ttu-id="7f887-147">hello，下列程式碼範例顯示如何 tooadd 憑證 tooa 雲端在 runbook 中的服務。</span><span class="sxs-lookup"><span data-stu-id="7f887-147">hello following sample code shows how tooadd a certificate tooa cloud service in a runbook.</span></span> <span data-ttu-id="7f887-148">在此範例中，從加密的自動化變數擷取 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="7f887-148">In this sample, hello password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="7f887-149">圖形化 Runbook 範例</span><span class="sxs-lookup"><span data-stu-id="7f887-149">Graphical runbook sample</span></span>

<span data-ttu-id="7f887-150">您將加入**Get-automationcertificat** tooa 圖形化 runbook，以滑鼠右鍵按一下 hello hello 圖形化編輯器和選取的程式庫 窗格中的 hello 憑證**新增 toocanvas**。</span><span class="sxs-lookup"><span data-stu-id="7f887-150">You add a **Get-AutomationCertificate** tooa graphical runbook by right-clicking on hello certificate in hello Library pane of hello graphical editor and selecting **Add toocanvas**.</span></span>

![新增憑證 toohello 畫布](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="7f887-152">hello 下列影像顯示在圖形化 runbook 中使用憑證的範例。</span><span class="sxs-lookup"><span data-stu-id="7f887-152">hello following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="7f887-153">這是 hello 相同憑證 tooa 雲端服務加入從文字的 runbook，如上所示的範例。</span><span class="sxs-lookup"><span data-stu-id="7f887-153">This is hello same example shown above for adding a certificate tooa cloud service from a textual runbook.</span></span>

![<span data-ttu-id="7f887-154">範例圖形化編寫</span><span class="sxs-lookup"><span data-stu-id="7f887-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="7f887-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7f887-155">Next steps</span></span>

- <span data-ttu-id="7f887-156">更多有關連結 toocontrol hello 邏輯流程的活動使用您的 runbook 是的 toolearn 設計 tooperform，請參閱[連結在圖形化撰寫](automation-graphical-authoring-intro.md#links-and-workflow)。</span><span class="sxs-lookup"><span data-stu-id="7f887-156">toolearn more about working with links toocontrol hello logical flow of activities your runbook is designed tooperform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
