---
title: "金鑰保存庫記錄 aaaAzure |Microsoft 文件"
description: "使用開始使用 Azure 金鑰保存庫本教學課程 toohelp 記錄。"
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a><span data-ttu-id="06979-103">Azure 金鑰保存庫記錄</span><span class="sxs-lookup"><span data-stu-id="06979-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="06979-104">大部分地區均提供 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="06979-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="06979-105">如需詳細資訊，請參閱 hello[金鑰保存庫定價頁面](https://azure.microsoft.com/pricing/details/key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="06979-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="06979-106">簡介</span><span class="sxs-lookup"><span data-stu-id="06979-106">Introduction</span></span>
<span data-ttu-id="06979-107">建立一或多個金鑰保存庫之後，您可能會想 toomonitor 如何及何時您金鑰保存庫會存取，以及由誰。</span><span class="sxs-lookup"><span data-stu-id="06979-107">After you have created one or more key vaults, you will likely want toomonitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="06979-108">想要做到這點，您可以啟用金鑰保存庫記錄，以在您提供的 Azure 儲存體帳戶中儲存這方面的資訊。</span><span class="sxs-lookup"><span data-stu-id="06979-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="06979-109">系統會自動為您指定的儲存體帳戶建立新的容器，其名稱為 **insights-logs-auditevent** ，而您也可以使用同一個儲存體帳戶來收集多個金鑰保存庫的記錄。</span><span class="sxs-lookup"><span data-stu-id="06979-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="06979-110">您可以存取您的記錄資訊最多，10 分鐘後 hello 金鑰保存庫作業。</span><span class="sxs-lookup"><span data-stu-id="06979-110">You can access your logging information at most, 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="06979-111">但大多不用這麼久。</span><span class="sxs-lookup"><span data-stu-id="06979-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="06979-112">是由 tooyou toomanage 您儲存體帳戶中的記錄檔：</span><span class="sxs-lookup"><span data-stu-id="06979-112">It's up tooyou toomanage your logs in your storage account:</span></span>

* <span data-ttu-id="06979-113">使用標準的 Azure 存取控制方法 toosecure 記錄藉由限制誰可以存取它們。</span><span class="sxs-lookup"><span data-stu-id="06979-113">Use standard Azure access control methods toosecure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="06979-114">刪除您不再想 tookeep 儲存體帳戶中的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="06979-114">Delete logs that you no longer want tookeep in your storage account.</span></span>

<span data-ttu-id="06979-115">使用開始使用 Azure 金鑰保存庫記錄、 toocreate 此教學課程 toohelp 儲存體帳戶啟用記錄，並解譯 hello 記錄收集的資訊。</span><span class="sxs-lookup"><span data-stu-id="06979-115">Use this tutorial toohelp you get started with Azure Key Vault logging, toocreate your storage account, enable logging, and interpret hello logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="06979-116">本教學課程不包括如何 toocreate 金鑰保存庫、 金鑰或密碼的指示。</span><span class="sxs-lookup"><span data-stu-id="06979-116">This tutorial does not include instructions for how toocreate key vaults, keys, or secrets.</span></span> <span data-ttu-id="06979-117">如需這方面的資訊，請參閱 [開始使用 Azure 金鑰保存庫](key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="06979-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="06979-118">或者，如需跨平台命令列介面的指示，請參閱 [這個對等的教學課程](key-vault-manage-with-cli2.md)。</span><span class="sxs-lookup"><span data-stu-id="06979-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
> <span data-ttu-id="06979-119">目前，您無法在 hello Azure 入口網站中設定 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="06979-119">Currently, you cannot configure Azure Key Vault in hello Azure portal.</span></span> <span data-ttu-id="06979-120">請改用這些 Azure PowerShell 指示。</span><span class="sxs-lookup"><span data-stu-id="06979-120">Instead, use these Azure PowerShell instructions.</span></span>
>
>

<span data-ttu-id="06979-121">如需 Azure 金鑰保存庫的概觀資訊，請參閱 [什麼是 Azure 金鑰保存庫？](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="06979-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06979-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="06979-122">Prerequisites</span></span>
<span data-ttu-id="06979-123">toocomplete 本教學課程中，您必須擁有下列 hello:</span><span class="sxs-lookup"><span data-stu-id="06979-123">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="06979-124">所使用的現有金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="06979-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="06979-125">Azure PowerShell ( **至少必須是 1.0.1 版**)。</span><span class="sxs-lookup"><span data-stu-id="06979-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="06979-126">tooinstall Azure PowerShell，將它與您 Azure 訂用帳戶產生關聯，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="06979-126">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="06979-127">如果您已安裝 Azure PowerShell，並不知道 hello 版本 hello Azure PowerShell 主控台中，輸入`(Get-Module azure -ListAvailable).Version`。</span><span class="sxs-lookup"><span data-stu-id="06979-127">If you have already installed Azure PowerShell and do not know hello version, from hello Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="06979-128">足夠的 Azure 儲存體以儲存金鑰保存庫記錄。</span><span class="sxs-lookup"><span data-stu-id="06979-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <span data-ttu-id="06979-129"><a id="connect"></a>連接 tooyour 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="06979-129"><a id="connect"></a>Connect tooyour subscriptions</span></span>
<span data-ttu-id="06979-130">啟動 Azure PowerShell 工作階段，以登入 Azure 帳戶 tooyour hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="06979-130">Start an Azure PowerShell session and sign in tooyour Azure account with hello following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="06979-131">在 [hello] 快顯瀏覽器視窗中，輸入您的 Azure 帳戶使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="06979-131">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="06979-132">Azure PowerShell 會取得所有 hello 訂用帳戶相關聯，與此帳戶，而且依預設，會使用 hello 第一個。</span><span class="sxs-lookup"><span data-stu-id="06979-132">Azure PowerShell will get all hello subscriptions that are associated with this account and by default, uses hello first one.</span></span>

<span data-ttu-id="06979-133">如果您有多個訂閱，您可能必須 toospecify 已使用的 toocreate 特定的 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="06979-133">If you have multiple subscriptions, you might have toospecify a specific one that was used toocreate your Azure Key Vault.</span></span> <span data-ttu-id="06979-134">輸入下列帳戶 toosee hello 訂閱 hello:</span><span class="sxs-lookup"><span data-stu-id="06979-134">Type hello following toosee hello subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="06979-135">然後，toospecify hello 訂用帳戶與金鑰保存庫會記錄您、 型別相關聯：</span><span class="sxs-lookup"><span data-stu-id="06979-135">Then, toospecify hello subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="06979-136">這個步驟很重要，如果您有多個與帳戶相關聯的訂用帳戶會特別實用。</span><span class="sxs-lookup"><span data-stu-id="06979-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="06979-137">如果略過這個步驟，可能會收到錯誤 tooregister Microsoft.Insights。</span><span class="sxs-lookup"><span data-stu-id="06979-137">You may receive an error tooregister Microsoft.Insights if this step is skipped.</span></span>
>   
>

<span data-ttu-id="06979-138">如需有關如何設定 Azure PowerShell 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="06979-138">For more information about configuring Azure PowerShell, see  [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="06979-139"><a id="storage"></a>建立新的儲存體帳戶來儲存記錄</span><span class="sxs-lookup"><span data-stu-id="06979-139"><a id="storage"></a>Create a new storage account for your logs</span></span>
<span data-ttu-id="06979-140">雖然您可以使用現有的儲存體帳戶記錄，我們將建立新的儲存體帳戶將專用的 tooKey 保存庫的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="06979-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated tooKey Vault logs.</span></span> <span data-ttu-id="06979-141">為了方便起見，當我們的 toospecify 這的更新版本中，我們將會儲存 hello 詳細資料放入變數，名為**sa**。</span><span class="sxs-lookup"><span data-stu-id="06979-141">For convenience for when we have toospecify this later, we'll store hello details into a variable named **sa**.</span></span>

<span data-ttu-id="06979-142">其他易於管理，我們將也使用 hello 相同的資源群組，因為其中包含我們金鑰保存庫 hello。</span><span class="sxs-lookup"><span data-stu-id="06979-142">For additional ease of management, we'll also use hello same resource group as hello one that contains our key vault.</span></span> <span data-ttu-id="06979-143">從 hello[快速入門教學課程](key-vault-get-started.md)，名為此資源群組**ContosoResourceGroup** ，我們將持續 toouse hello 東亞 」 位置。</span><span class="sxs-lookup"><span data-stu-id="06979-143">From hello [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue toouse hello East Asia location.</span></span> <span data-ttu-id="06979-144">請視情況將這些值替換成您自己的值：</span><span class="sxs-lookup"><span data-stu-id="06979-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="06979-145">如果您決定 toouse 現有的儲存體帳戶，則必須使用為金鑰保存庫，它必須使用 hello Resource Manager 部署模型，而非 hello 傳統部署模型 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="06979-145">If you decide toouse an existing storage account, it must use hello same subscription as your key vault and it must use hello Resource Manager deployment model, rather than hello Classic deployment model.</span></span>
>
>

## <span data-ttu-id="06979-146"><a id="identify"></a>識別 hello 記錄金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="06979-146"><a id="identify"></a>Identify hello key vault for your logs</span></span>
<span data-ttu-id="06979-147">取得開始教學課程中，在我們的金鑰保存庫名稱是**ContosoKeyVault**，因此我們將持續的名稱，並將 hello 詳細資料儲存到變數，名為 toouse **kv**:</span><span class="sxs-lookup"><span data-stu-id="06979-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue toouse that name and store hello details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <span data-ttu-id="06979-148"><a id="enable"></a>啟用記錄</span><span class="sxs-lookup"><span data-stu-id="06979-148"><a id="enable"></a>Enable logging</span></span>
<span data-ttu-id="06979-149">tooenable 記錄金鑰保存庫，我們將使用 hello 組 AzureRmDiagnosticSetting cmdlet 時，我們建立我們新的儲存體帳戶和我們的金鑰保存庫以及 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="06979-149">tooenable logging for Key Vault, we'll use hello Set-AzureRmDiagnosticSetting cmdlet, together with hello variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="06979-150">我們也會隨即制定 hello **-啟用**旗標太**$true**並設定 hello 類別 tooAuditEvent （hello 唯一類別進行金鑰保存庫記錄）：</span><span class="sxs-lookup"><span data-stu-id="06979-150">We'll also set hello **-Enabled** flag too**$true** and set hello category tooAuditEvent (hello only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="06979-151">這個 hello 輸出包含：</span><span class="sxs-lookup"><span data-stu-id="06979-151">hello output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="06979-152">這可確認現在您金鑰保存庫，儲存資訊 tooyour 儲存體帳戶啟用記錄。</span><span class="sxs-lookup"><span data-stu-id="06979-152">This confirms that logging is now enabled for your key vault, saving information tooyour storage account.</span></span>

<span data-ttu-id="06979-153">您也可以選擇性地設定記錄檔的保留原則，以便自動刪除較舊的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="06979-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="06979-154">例如，將設定保留原則使用**-RetentionEnabled**旗標太**$true**並設定**-RetentionInDays**參數太**90**讓會自動刪除超過 90 天的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="06979-154">For example, set retention policy using **-RetentionEnabled** flag too**$true** and set **-RetentionInDays** parameter too**90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="06979-155">所記錄的內容：</span><span class="sxs-lookup"><span data-stu-id="06979-155">What's logged:</span></span>

* <span data-ttu-id="06979-156">會記錄所有已驗證的 REST API 要求，包括因為存取權限、系統錯誤或要求錯誤而發生的失敗要求。</span><span class="sxs-lookup"><span data-stu-id="06979-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="06979-157">作業 hello 金鑰保存庫本身，其中包括建立、 刪除、 設定金鑰保存庫的存取原則，並更新金鑰保存庫屬性，例如標記。</span><span class="sxs-lookup"><span data-stu-id="06979-157">Operations on hello key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="06979-158">金鑰和秘密 hello 金鑰保存庫中，包括建立、 修改或刪除這些機碼或密碼; 上的作業作業，例如登入驗證、 加密、 解密、 包裝並解除包裝金鑰、 取得密碼、 列出金鑰和密碼，以及其版本。</span><span class="sxs-lookup"><span data-stu-id="06979-158">Operations on keys and secrets in hello key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="06979-159">產生 401 回應的未經驗證要求。</span><span class="sxs-lookup"><span data-stu-id="06979-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="06979-160">例如，沒有持有人權杖的要求，或格式不正確或已過期的要求，或具有無效權杖的要求。</span><span class="sxs-lookup"><span data-stu-id="06979-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <span data-ttu-id="06979-161"><a id="access"></a>存取記錄</span><span class="sxs-lookup"><span data-stu-id="06979-161"><a id="access"></a>Access your logs</span></span>
<span data-ttu-id="06979-162">金鑰保存庫的記錄檔會儲存在 hello **insights-記錄檔-auditevent** hello 您提供的儲存體帳戶中的容器。</span><span class="sxs-lookup"><span data-stu-id="06979-162">Key vault logs are stored in hello **insights-logs-auditevent** container in hello storage account you provided.</span></span> <span data-ttu-id="06979-163">toolist 所有 hello blob，在此容器中，都輸入：</span><span class="sxs-lookup"><span data-stu-id="06979-163">toolist all hello blobs in this container, type:</span></span>

<span data-ttu-id="06979-164">首先，建立 hello 容器名稱的變數。</span><span class="sxs-lookup"><span data-stu-id="06979-164">First, create a variable for hello container name.</span></span> <span data-ttu-id="06979-165">這將會使用其餘的 hello 逐步 hello。</span><span class="sxs-lookup"><span data-stu-id="06979-165">This will be used throughout hello rest of hello walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="06979-166">toolist 所有 hello blob，在此容器中，都輸入：</span><span class="sxs-lookup"><span data-stu-id="06979-166">toolist all hello blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="06979-167">hello 輸出看起來類似 toothis:</span><span class="sxs-lookup"><span data-stu-id="06979-167">hello output will look something similar toothis:</span></span>

<span data-ttu-id="06979-168">**容器 Uri：https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="06979-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="06979-169">**名稱**</span><span class="sxs-lookup"><span data-stu-id="06979-169">**Name**</span></span>

- - -
<span data-ttu-id="06979-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="06979-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="06979-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="06979-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="06979-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span><span class="sxs-lookup"><span data-stu-id="06979-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span></span>

<span data-ttu-id="06979-173">您可以從這個輸出中看到，hello blob 遵循命名慣例： **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h i n =<hour>/m =<minute>/filename.json**</span><span class="sxs-lookup"><span data-stu-id="06979-173">As you can see from this output, hello blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="06979-174">hello 日期和時間值會使用 UTC。</span><span class="sxs-lookup"><span data-stu-id="06979-174">hello date and time values use UTC.</span></span>

<span data-ttu-id="06979-175">由於 hello 相同儲存體帳戶可以是使用的 toocollect 記錄檔中的多個資源，hello 完整資源識別碼 hello blob 名稱中是很有幫助 tooaccess 或下載僅 hello blob，您需要。</span><span class="sxs-lookup"><span data-stu-id="06979-175">Because hello same storage account can be used toocollect logs for multiple resources, hello full resource ID in hello blob name is very useful tooaccess or download just hello blobs that you need.</span></span> <span data-ttu-id="06979-176">這樣做之前，將會先涵蓋如何 toodownload 所有 hello blob。</span><span class="sxs-lookup"><span data-stu-id="06979-176">But before we do that, we'll first cover how toodownload all hello blobs.</span></span>

<span data-ttu-id="06979-177">首先，建立資料夾 toodownload hello blob。</span><span class="sxs-lookup"><span data-stu-id="06979-177">First, create a folder toodownload hello blobs.</span></span> <span data-ttu-id="06979-178">例如：</span><span class="sxs-lookup"><span data-stu-id="06979-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="06979-179">然後取得所有 blob 的清單：</span><span class="sxs-lookup"><span data-stu-id="06979-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="06979-180">您可以將這份清單透過 ' Get AzureStorageBlobContent' toodownload hello blob 管道傳送至我們的目的資料夾：</span><span class="sxs-lookup"><span data-stu-id="06979-180">Pipe this list through 'Get-AzureStorageBlobContent' toodownload hello blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="06979-181">當您執行這個第二個命令時，hello  **/**  hello blob 名稱中的分隔符號建立完整資料夾結構 hello 目的地資料夾下的，此結構會使用 toodownload 和存放區 hello blob 檔案。</span><span class="sxs-lookup"><span data-stu-id="06979-181">When you run this second command, hello **/** delimiter in hello blob names create a full folder structure under hello destination folder, and this structure will be used toodownload and store hello blobs as files.</span></span>

<span data-ttu-id="06979-182">tooselectively 下載 blob 時，使用萬用字元。</span><span class="sxs-lookup"><span data-stu-id="06979-182">tooselectively download blobs, use wildcards.</span></span> <span data-ttu-id="06979-183">例如：</span><span class="sxs-lookup"><span data-stu-id="06979-183">For example:</span></span>

* <span data-ttu-id="06979-184">如果您有多個金鑰保存庫，並想要只在一個金鑰保存庫，名為 CONTOSOKEYVAULT3 toodownload 記錄檔：</span><span class="sxs-lookup"><span data-stu-id="06979-184">If you have multiple key vaults and want toodownload logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="06979-185">如果您有多個資源群組，並想 toodownload 記錄檔只在一個資源群組，使用`-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span><span class="sxs-lookup"><span data-stu-id="06979-185">If you have multiple resource groups and want toodownload logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="06979-186">如果您想 toodownload hello 的所有記錄的 2016 年 1 月 hello 月，使用`-Blob '*/year=2016/m=01/*'`:</span><span class="sxs-lookup"><span data-stu-id="06979-186">If you want toodownload all hello logs for hello month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="06979-187">您現在準備好 toostart 查看功能的 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="06979-187">You're now ready toostart looking at what's in hello logs.</span></span> <span data-ttu-id="06979-188">但才會繼續，您可能需要 tooknow Get AzureRmDiagnosticSetting 的兩個多個參數：</span><span class="sxs-lookup"><span data-stu-id="06979-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need tooknow:</span></span>

* <span data-ttu-id="06979-189">tooquery hello 狀態的診斷設定金鑰保存庫資源：`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="06979-189">tooquery hello  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="06979-190">toodisable 記錄金鑰保存庫資源：`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="06979-190">toodisable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <span data-ttu-id="06979-191"><a id="interpret"></a>解譯金鑰保存庫記錄</span><span class="sxs-lookup"><span data-stu-id="06979-191"><a id="interpret"></a>Interpret your Key Vault logs</span></span>
<span data-ttu-id="06979-192">各個 blob 皆會儲存為文字，並格式化為 JSON blob。</span><span class="sxs-lookup"><span data-stu-id="06979-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="06979-193">以下是執行 `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`後所得到的範例記錄項目：</span><span class="sxs-lookup"><span data-stu-id="06979-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


<span data-ttu-id="06979-194">hello 下表列出 hello 欄位名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="06979-194">hello following table lists hello field names and descriptions.</span></span>

| <span data-ttu-id="06979-195">欄位名稱</span><span class="sxs-lookup"><span data-stu-id="06979-195">Field name</span></span> | <span data-ttu-id="06979-196">說明</span><span class="sxs-lookup"><span data-stu-id="06979-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="06979-197">分析</span><span class="sxs-lookup"><span data-stu-id="06979-197">time</span></span> |<span data-ttu-id="06979-198">日期和時間 (UTC)。</span><span class="sxs-lookup"><span data-stu-id="06979-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="06979-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="06979-199">resourceId</span></span> |<span data-ttu-id="06979-200">Azure 資源管理員資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="06979-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="06979-201">為金鑰保存庫的記錄檔，這一定是 hello 金鑰保存庫的資源 id。</span><span class="sxs-lookup"><span data-stu-id="06979-201">For Key Vault logs, this is always hello  Key Vault resource ID.</span></span> |
| <span data-ttu-id="06979-202">operationName</span><span class="sxs-lookup"><span data-stu-id="06979-202">operationName</span></span> |<span data-ttu-id="06979-203">Hello 作業，如 hello 下一個表格中所述的名稱。</span><span class="sxs-lookup"><span data-stu-id="06979-203">Name of hello operation, as documented in hello next table.</span></span> |
| <span data-ttu-id="06979-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="06979-204">operationVersion</span></span> |<span data-ttu-id="06979-205">這是 hello hello 用戶端要求的 REST API 版本。</span><span class="sxs-lookup"><span data-stu-id="06979-205">This is hello REST API version requested by hello client.</span></span> |
| <span data-ttu-id="06979-206">category</span><span class="sxs-lookup"><span data-stu-id="06979-206">category</span></span> |<span data-ttu-id="06979-207">適用於金鑰保存庫記錄 AuditEvent hello 單一、 可用值。</span><span class="sxs-lookup"><span data-stu-id="06979-207">For Key Vault logs, AuditEvent is hello single, available value.</span></span> |
| <span data-ttu-id="06979-208">resultType</span><span class="sxs-lookup"><span data-stu-id="06979-208">resultType</span></span> |<span data-ttu-id="06979-209">REST API 要求的結果。</span><span class="sxs-lookup"><span data-stu-id="06979-209">Result of REST API request.</span></span> |
| <span data-ttu-id="06979-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="06979-210">resultSignature</span></span> |<span data-ttu-id="06979-211">HTTP 狀態。</span><span class="sxs-lookup"><span data-stu-id="06979-211">HTTP status.</span></span> |
| <span data-ttu-id="06979-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="06979-212">resultDescription</span></span> |<span data-ttu-id="06979-213">其他 hello 結果可用時的詳細描述。</span><span class="sxs-lookup"><span data-stu-id="06979-213">Additional description about hello result, when available.</span></span> |
| <span data-ttu-id="06979-214">durationMs</span><span class="sxs-lookup"><span data-stu-id="06979-214">durationMs</span></span> |<span data-ttu-id="06979-215">以毫秒為單位 tooservice hello REST API 要求所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="06979-215">Time it took tooservice hello REST API request, in milliseconds.</span></span> <span data-ttu-id="06979-216">這不包括 hello 網路延遲，讓您測量 hello 用戶端 hello 時間可能不符合此時間。</span><span class="sxs-lookup"><span data-stu-id="06979-216">This does not include hello network latency, so hello time you measure on hello client side might not match this time.</span></span> |
| <span data-ttu-id="06979-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="06979-217">callerIpAddress</span></span> |<span data-ttu-id="06979-218">Hello 用戶端 hello 要求者 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="06979-218">IP address of hello client who made hello request.</span></span> |
| <span data-ttu-id="06979-219">correlationId</span><span class="sxs-lookup"><span data-stu-id="06979-219">correlationId</span></span> |<span data-ttu-id="06979-220">選擇性的 GUID，hello 用戶端可以傳遞 toocorrelate 用戶端與服務端 （金鑰保存庫） 記錄檔的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="06979-220">An optional GUID that hello client can pass toocorrelate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="06979-221">身分識別</span><span class="sxs-lookup"><span data-stu-id="06979-221">identity</span></span> |<span data-ttu-id="06979-222">從 hello 權杖提出 hello REST API 要求時提供的身分識別。</span><span class="sxs-lookup"><span data-stu-id="06979-222">Identity from hello token that was presented when making hello REST API request.</span></span> <span data-ttu-id="06979-223">和 Azure PowerShell Cmdlet 所產生之要求的案例一樣，這通常是「使用者」、「服務主體」或「使用者+appId」的組合。</span><span class="sxs-lookup"><span data-stu-id="06979-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="06979-224">屬性</span><span class="sxs-lookup"><span data-stu-id="06979-224">properties</span></span> |<span data-ttu-id="06979-225">此欄位會包含不同 hello 作業 (operationName) 為基礎的資訊。</span><span class="sxs-lookup"><span data-stu-id="06979-225">This field will contain different information based on hello operation (operationName).</span></span> <span data-ttu-id="06979-226">在大部分情況下，包含用戶端資訊 （hello 使用者代理字串 hello 用戶端所傳遞），hello 確切的 REST API 要求 URI、 與 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="06979-226">In most cases, contains client information (hello useragent string passed by hello client), hello exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="06979-227">此外，要求 （例如，KeyCreate 或 VaultGet） 的結果傳回的物件時它也會包含 hello （為"id") 的金鑰 URI、 保存庫 URI 或 URI 密碼。</span><span class="sxs-lookup"><span data-stu-id="06979-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain hello Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="06979-228">hello **operationName**欄位值的 ObjectVerb 格式。</span><span class="sxs-lookup"><span data-stu-id="06979-228">hello **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="06979-229">例如：</span><span class="sxs-lookup"><span data-stu-id="06979-229">For example:</span></span>

* <span data-ttu-id="06979-230">金鑰保存庫的所有作業都有 hello '保存庫`<action>`' 格式，例如`VaultGet`和`VaultCreate`。</span><span class="sxs-lookup"><span data-stu-id="06979-230">All key vault operations have hello 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="06979-231">索引鍵的所有作業都有 hello '索引鍵`<action>`' 格式，例如`KeySign`和`KeyList`。</span><span class="sxs-lookup"><span data-stu-id="06979-231">All  key operations have hello 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="06979-232">密碼的所有作業都有 hello '密碼`<action>`' 格式，例如`SecretGet`和`SecretListVersions`。</span><span class="sxs-lookup"><span data-stu-id="06979-232">All secret operations have hello 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="06979-233">hello 下表列出 hello operationName 和對應的 REST API 命令。</span><span class="sxs-lookup"><span data-stu-id="06979-233">hello following table lists hello operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="06979-234">operationName</span><span class="sxs-lookup"><span data-stu-id="06979-234">operationName</span></span> | <span data-ttu-id="06979-235">REST API 命令</span><span class="sxs-lookup"><span data-stu-id="06979-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="06979-236">驗證</span><span class="sxs-lookup"><span data-stu-id="06979-236">Authentication</span></span> |<span data-ttu-id="06979-237">透過 Azure Active Directory 端點</span><span class="sxs-lookup"><span data-stu-id="06979-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="06979-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="06979-238">VaultGet</span></span> |[<span data-ttu-id="06979-239">取得金鑰保存庫的相關資訊</span><span class="sxs-lookup"><span data-stu-id="06979-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="06979-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="06979-240">VaultPut</span></span> |[<span data-ttu-id="06979-241">建立或更新金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="06979-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="06979-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="06979-242">VaultDelete</span></span> |[<span data-ttu-id="06979-243">刪除金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="06979-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="06979-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="06979-244">VaultPatch</span></span> |[<span data-ttu-id="06979-245">更新金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="06979-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="06979-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="06979-246">VaultList</span></span> |[<span data-ttu-id="06979-247">列出資源群組中的所有金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="06979-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="06979-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="06979-248">KeyCreate</span></span> |[<span data-ttu-id="06979-249">建立金鑰</span><span class="sxs-lookup"><span data-stu-id="06979-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="06979-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="06979-250">KeyGet</span></span> |[<span data-ttu-id="06979-251">取得金鑰的相關資訊</span><span class="sxs-lookup"><span data-stu-id="06979-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="06979-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="06979-252">KeyImport</span></span> |[<span data-ttu-id="06979-253">將金鑰匯入保存庫</span><span class="sxs-lookup"><span data-stu-id="06979-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="06979-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="06979-254">KeyBackup</span></span> |<span data-ttu-id="06979-255">[備份金鑰](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx)。</span><span class="sxs-lookup"><span data-stu-id="06979-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="06979-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="06979-256">KeyDelete</span></span> |[<span data-ttu-id="06979-257">刪除金鑰</span><span class="sxs-lookup"><span data-stu-id="06979-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="06979-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="06979-258">KeyRestore</span></span> |[<span data-ttu-id="06979-259">還原金鑰</span><span class="sxs-lookup"><span data-stu-id="06979-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="06979-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="06979-260">KeySign</span></span> |[<span data-ttu-id="06979-261">使用金鑰簽署</span><span class="sxs-lookup"><span data-stu-id="06979-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="06979-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="06979-262">KeyVerify</span></span> |[<span data-ttu-id="06979-263">使用金鑰驗證</span><span class="sxs-lookup"><span data-stu-id="06979-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="06979-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="06979-264">KeyWrap</span></span> |[<span data-ttu-id="06979-265">包裝金鑰</span><span class="sxs-lookup"><span data-stu-id="06979-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="06979-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="06979-266">KeyUnwrap</span></span> |[<span data-ttu-id="06979-267">解除包裝金鑰</span><span class="sxs-lookup"><span data-stu-id="06979-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="06979-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="06979-268">KeyEncrypt</span></span> |[<span data-ttu-id="06979-269">使用金鑰加密</span><span class="sxs-lookup"><span data-stu-id="06979-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="06979-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="06979-270">KeyDecrypt</span></span> |[<span data-ttu-id="06979-271">使用金鑰解密</span><span class="sxs-lookup"><span data-stu-id="06979-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="06979-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="06979-272">KeyUpdate</span></span> |[<span data-ttu-id="06979-273">更新金鑰</span><span class="sxs-lookup"><span data-stu-id="06979-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="06979-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="06979-274">KeyList</span></span> |[<span data-ttu-id="06979-275">列出保存庫中的 hello 索引鍵</span><span class="sxs-lookup"><span data-stu-id="06979-275">List hello keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="06979-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="06979-276">KeyListVersions</span></span> |[<span data-ttu-id="06979-277">金鑰的清單 hello 版本</span><span class="sxs-lookup"><span data-stu-id="06979-277">List hello versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="06979-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="06979-278">SecretSet</span></span> |[<span data-ttu-id="06979-279">建立密碼</span><span class="sxs-lookup"><span data-stu-id="06979-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="06979-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="06979-280">SecretGet</span></span> |[<span data-ttu-id="06979-281">取得密碼</span><span class="sxs-lookup"><span data-stu-id="06979-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="06979-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="06979-282">SecretUpdate</span></span> |[<span data-ttu-id="06979-283">更新密碼</span><span class="sxs-lookup"><span data-stu-id="06979-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="06979-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="06979-284">SecretDelete</span></span> |[<span data-ttu-id="06979-285">刪除秘密</span><span class="sxs-lookup"><span data-stu-id="06979-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="06979-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="06979-286">SecretList</span></span> |[<span data-ttu-id="06979-287">列出保存庫中的密碼</span><span class="sxs-lookup"><span data-stu-id="06979-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="06979-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="06979-288">SecretListVersions</span></span> |[<span data-ttu-id="06979-289">列出密碼的版本</span><span class="sxs-lookup"><span data-stu-id="06979-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <span data-ttu-id="06979-290"><a id="loganalytics"></a>使用 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="06979-290"><a id="loganalytics"></a>Use Log Analytics</span></span>

<span data-ttu-id="06979-291">您可以在 Azure 金鑰保存庫 AuditEvent 記錄的記錄分析 tooreview 使用 hello Azure 金鑰保存庫的方案。</span><span class="sxs-lookup"><span data-stu-id="06979-291">You can use hello Azure Key Vault solution in Log Analytics tooreview Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="06979-292">如需詳細資訊，包括如何 tooset 其設定，請參閱[記錄分析中的 Azure 金鑰保存庫方案](../log-analytics/log-analytics-azure-key-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="06979-292">For more information, including how tooset this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="06979-293">如果您需要從 hello 舊金鑰保存庫已提供解決方案 hello 記錄分析在預覽期間，您先路由傳送您的記錄檔 tooan Azure 儲存體帳戶並設定從該處的記錄分析 tooread toomigrate 本文也會包含指示。</span><span class="sxs-lookup"><span data-stu-id="06979-293">This article also contains instructions if you need toomigrate from hello old Key Vault solution that was offered during hello Log Analytics preview, where you first routed your logs tooan Azure Storage account and configured Log Analytics tooread from there.</span></span>

## <span data-ttu-id="06979-294"><a id="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="06979-294"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="06979-295">如需在 Web 應用程式中使用 Azure 金鑰保存庫的教學課程，請參閱 [從 Web 應用程式使用 Azure 金鑰保存庫](key-vault-use-from-web-application.md)。</span><span class="sxs-lookup"><span data-stu-id="06979-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="06979-296">程式設計參考，請參閱[hello Azure 金鑰保存庫開發人員手冊 》](key-vault-developers-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="06979-296">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="06979-297">如需 Azure 金鑰保存庫的 Azure PowerShell 1.0 Cmdlet 清單，請參閱 [Azure 金鑰保存庫 Cmdlet](/powershell/module/azurerm.keyvault/#key_vault)。</span><span class="sxs-lookup"><span data-stu-id="06979-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="06979-298">如需金鑰輪替和使用 Azure 金鑰保存庫稽核記錄檔的教學課程，請參閱[如何與結束 tooend toosetup 金鑰保存庫金鑰旋轉和稽核](key-vault-key-rotation-log-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="06979-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How toosetup Key Vault with end tooend key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>
