---
title: "aaaUse 與 Azure RemoteApp PowerShell cmdlet |Microsoft 文件"
description: "深入了解如何 toouse Azure RemoteApp 中的 Windows PowerShell cmdlet。"
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="71e0a-103">將 Windows PowerShell Cmdlet 搭配 Azure RemoteApp 使用</span><span class="sxs-lookup"><span data-stu-id="71e0a-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="71e0a-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="71e0a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="71e0a-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="71e0a-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="71e0a-106">您可以使用 hello Azure RemoteApp PowerShell cmdlet tooadminister 及維護您的集合。</span><span class="sxs-lookup"><span data-stu-id="71e0a-106">You can use hello Azure RemoteApp PowerShell cmdlets tooadminister and maintain your collections.</span></span> <span data-ttu-id="71e0a-107">使用下列資訊 tooget 啟動 hello。</span><span class="sxs-lookup"><span data-stu-id="71e0a-107">Use hello following information tooget started.</span></span>

## <a name="get-hello-cmdlets"></a><span data-ttu-id="71e0a-108">取得 hello cmdlet</span><span class="sxs-lookup"><span data-stu-id="71e0a-108">Get hello cmdlets</span></span>
- - -
<span data-ttu-id="71e0a-109">第一次下載 hello Azure Powershell cmdlet[這裡](http://go.microsoft.com/?linkid=9811175)，hello RemoteApp 指令程式會包含在內般。</span><span class="sxs-lookup"><span data-stu-id="71e0a-109">First download hello Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), hello RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="71e0a-110">簽出 hello [Azure RemoteApp 指令程式說明](/powershell/module/azure?view=azuresmps-3.7.0)。</span><span class="sxs-lookup"><span data-stu-id="71e0a-110">Check out hello [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a><span data-ttu-id="71e0a-111">設定 Azure cmdlet toouse 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="71e0a-111">Configure Azure cmdlets toouse your subscription</span></span>
- - -
<span data-ttu-id="71e0a-112">請遵循[本指南](/powershell/azure/overview)因此您可以針對您的 Azure 訂用帳戶使用 hello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="71e0a-112">Follow [this guide](/powershell/azure/overview) so you can use hello cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="71e0a-113">您可以使用這些步驟 tooget，快速入門：</span><span class="sxs-lookup"><span data-stu-id="71e0a-113">You can use these steps tooget started quickly:</span></span>

1. <span data-ttu-id="71e0a-114">下載並安裝 hello [Azure PowerShell cmdlet](http://go.microsoft.com/?linkid=9811175)。</span><span class="sxs-lookup"><span data-stu-id="71e0a-114">Download and install hello [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="71e0a-115">啟動 Microsoft Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="71e0a-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="71e0a-116">執行**Add-azureaccount** tooauthenticate tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="71e0a-116">Run **Add-AzureAccount** tooauthenticate tooyour Azure subscription.</span></span> <span data-ttu-id="71e0a-117">出現提示時，輸入 hello 相同使用者名稱和密碼，您會使用 toosign tooAzure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="71e0a-117">When prompted, enter hello same user name and password that you use toosign in tooAzure portal.</span></span>  
4. <span data-ttu-id="71e0a-118">執行**Get-azuresubscription** toolist hello 訂用帳戶與您的使用者帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="71e0a-118">Run **Get-AzureSubscription** toolist hello subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="71e0a-119">執行**Select-azuresubscription SubscriptionName&lt;訂用帳戶名稱&gt;**或**Select-azuresubscription SubscriptionId&lt;訂用帳戶 ID&gt;**  toospecify hello 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="71e0a-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** toospecify hello subscription toouse.</span></span>

<span data-ttu-id="71e0a-120">恭喜，您的 Azure PowerShell 主控台已設定且已準備 toouse。</span><span class="sxs-lookup"><span data-stu-id="71e0a-120">Congratulations, your Azure PowerShell console is configured and ready toouse.</span></span> <span data-ttu-id="71e0a-121">請注意，您必須 toorepeate 步驟 2 到 5，每次啟動 hello hello Azure PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="71e0a-121">Be aware that you'll need toorepeate steps 2 through 5 each time you start hello hello Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="71e0a-122">列出所有集合</span><span class="sxs-lookup"><span data-stu-id="71e0a-122">List all collections</span></span>
- - -
     <span data-ttu-id="71e0a-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="71e0a-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="71e0a-124">刪除集合</span><span class="sxs-lookup"><span data-stu-id="71e0a-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="71e0a-125">Remove-AzureRemoteAppCollection <enter collection name></span><span class="sxs-lookup"><span data-stu-id="71e0a-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="71e0a-126">範例：`Remove-AzureRemoteAppCollection ContosoProduction`。</span><span class="sxs-lookup"><span data-stu-id="71e0a-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="71e0a-127">建立雲端收藏</span><span class="sxs-lookup"><span data-stu-id="71e0a-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="71e0a-128">它很簡單，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="71e0a-128">It's simple, run hello following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="71e0a-129">hello 上述命令會自動發佈 （Excel、 OneNote、 Outlook、 PowerPoint、 Visio 及 Word） 的 Microsoft Office 365 應用程式。</span><span class="sxs-lookup"><span data-stu-id="71e0a-129">hello above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="71e0a-130">集合建立作業可能需要 30 分鐘或更長的 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="71e0a-130">Collection creation can take 30 minutes or longer toocomplete.</span></span> <span data-ttu-id="71e0a-131">因此，此命令會傳回可使用的追蹤識別碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="71e0a-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="71e0a-132">Hello 收集完成之後，您可以新增使用者 toohello 集合以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="71e0a-132">After hello collection is done, you can add users toohello collection with hello following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="71e0a-133">大功告成！</span><span class="sxs-lookup"><span data-stu-id="71e0a-133">And you're done!</span></span> <span data-ttu-id="71e0a-134">該使用者應該能夠 tooconnect toohello 應用程式使用 hello Azure RemoteApp 用戶端找到[這裡](https://www.remoteapp.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="71e0a-134">That user should be able tooconnect toohello application using hello Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="71e0a-135">可用的 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="71e0a-135">Available cmdlets</span></span>
<span data-ttu-id="71e0a-136">其他命令，我們有很多，將會很快即將 hello 它們的文件：</span><span class="sxs-lookup"><span data-stu-id="71e0a-136">There are lots of other commands that we have, hello documentation for them will be coming shortly:</span></span>

<span data-ttu-id="71e0a-137">基本 RemoteApp 集合 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="71e0a-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="71e0a-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="71e0a-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="71e0a-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="71e0a-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="71e0a-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="71e0a-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="71e0a-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="71e0a-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="71e0a-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="71e0a-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="71e0a-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="71e0a-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="71e0a-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="71e0a-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="71e0a-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="71e0a-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="71e0a-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="71e0a-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="71e0a-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="71e0a-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="71e0a-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="71e0a-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="71e0a-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="71e0a-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="71e0a-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="71e0a-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="71e0a-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="71e0a-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="71e0a-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="71e0a-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="71e0a-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="71e0a-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="71e0a-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="71e0a-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="71e0a-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="71e0a-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="71e0a-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="71e0a-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="71e0a-157">RemoteApp virtual network cmdlets:</span><span class="sxs-lookup"><span data-stu-id="71e0a-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="71e0a-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="71e0a-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="71e0a-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="71e0a-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="71e0a-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="71e0a-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="71e0a-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="71e0a-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="71e0a-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="71e0a-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="71e0a-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="71e0a-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="71e0a-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="71e0a-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="71e0a-165">RemoteApp template image cmdlets:</span><span class="sxs-lookup"><span data-stu-id="71e0a-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="71e0a-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="71e0a-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="71e0a-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="71e0a-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="71e0a-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="71e0a-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="71e0a-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="71e0a-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="71e0a-170">Other RemoteApp cmdlets:</span><span class="sxs-lookup"><span data-stu-id="71e0a-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="71e0a-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="71e0a-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="71e0a-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="71e0a-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="71e0a-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="71e0a-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="71e0a-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="71e0a-174">Get-AzureRemoteAppOperationResult</span></span>

