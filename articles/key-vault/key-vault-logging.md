---
title: "Azure 金鑰保存庫記錄 | Microsoft Docs"
description: "使用本教學課程來協助您開始使用 Azure 金鑰保存庫記錄。"
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
ms.openlocfilehash: e9a4f16f048833dab49f7db79892fe47a5aeff37
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-key-vault-logging"></a><span data-ttu-id="5d111-103">Azure 金鑰保存庫記錄</span><span class="sxs-lookup"><span data-stu-id="5d111-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="5d111-104">大部分地區均提供 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="5d111-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="5d111-105">如需詳細資訊，請參閱 [金鑰保存庫價格頁面](https://azure.microsoft.com/pricing/details/key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="5d111-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="5d111-106">簡介</span><span class="sxs-lookup"><span data-stu-id="5d111-106">Introduction</span></span>
<span data-ttu-id="5d111-107">在建立一或多個金鑰保存庫之後，您可能會想要監視金鑰保存庫的存取方式、時間和存取者。</span><span class="sxs-lookup"><span data-stu-id="5d111-107">After you have created one or more key vaults, you will likely want to monitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="5d111-108">想要做到這點，您可以啟用金鑰保存庫記錄，以在您提供的 Azure 儲存體帳戶中儲存這方面的資訊。</span><span class="sxs-lookup"><span data-stu-id="5d111-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="5d111-109">系統會自動為您指定的儲存體帳戶建立新的容器，其名稱為 **insights-logs-auditevent** ，而您也可以使用同一個儲存體帳戶來收集多個金鑰保存庫的記錄。</span><span class="sxs-lookup"><span data-stu-id="5d111-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="5d111-110">您最多在執行過金鑰保存庫作業 10 分鐘後，就能存取其記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="5d111-110">You can access your logging information at most, 10 minutes after the key vault operation.</span></span> <span data-ttu-id="5d111-111">但大多不用這麼久。</span><span class="sxs-lookup"><span data-stu-id="5d111-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="5d111-112">儲存體帳戶中的記錄由您全權管理：</span><span class="sxs-lookup"><span data-stu-id="5d111-112">It's up to you to manage your logs in your storage account:</span></span>

* <span data-ttu-id="5d111-113">請使用標準的 Azure 存取控制方法限制可存取記錄的人員，藉此來保護記錄。</span><span class="sxs-lookup"><span data-stu-id="5d111-113">Use standard Azure access control methods to secure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="5d111-114">刪除不想繼續保留在儲存體帳戶中的記錄。</span><span class="sxs-lookup"><span data-stu-id="5d111-114">Delete logs that you no longer want to keep in your storage account.</span></span>

<span data-ttu-id="5d111-115">請使用本教學課程來協助您開始使用 Azure 金鑰保存庫記錄、建立儲存體帳戶、啟用記錄，以及解譯所收集到的記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="5d111-115">Use this tutorial to help you get started with Azure Key Vault logging, to create your storage account, enable logging, and interpret the logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="5d111-116">本教學課程不會指示如何建立金鑰保存庫、金鑰或密碼。</span><span class="sxs-lookup"><span data-stu-id="5d111-116">This tutorial does not include instructions for how to create key vaults, keys, or secrets.</span></span> <span data-ttu-id="5d111-117">如需這方面的資訊，請參閱 [開始使用 Azure 金鑰保存庫](key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="5d111-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="5d111-118">或者，如需跨平台命令列介面的指示，請參閱 [這個對等的教學課程](key-vault-manage-with-cli2.md)。</span><span class="sxs-lookup"><span data-stu-id="5d111-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
> <span data-ttu-id="5d111-119">目前，您無法在 Azure 入口網站中設定 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="5d111-119">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="5d111-120">請改用這些 Azure PowerShell 指示。</span><span class="sxs-lookup"><span data-stu-id="5d111-120">Instead, use these Azure PowerShell instructions.</span></span>
>
>

<span data-ttu-id="5d111-121">如需 Azure 金鑰保存庫的概觀資訊，請參閱 [什麼是 Azure 金鑰保存庫？](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="5d111-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d111-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="5d111-122">Prerequisites</span></span>
<span data-ttu-id="5d111-123">若要完成本教學課程，您必須具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="5d111-123">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="5d111-124">所使用的現有金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="5d111-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="5d111-125">Azure PowerShell ( **至少必須是 1.0.1 版**)。</span><span class="sxs-lookup"><span data-stu-id="5d111-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="5d111-126">若要安裝 Azure PowerShell，並將它與 Azure 訂用帳戶建立關聯，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5d111-126">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="5d111-127">如果您已安裝 Azure PowerShell 但不知道版本，請在 Azure PowerShell 主控台中輸入 `(Get-Module azure -ListAvailable).Version`。</span><span class="sxs-lookup"><span data-stu-id="5d111-127">If you have already installed Azure PowerShell and do not know the version, from the Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="5d111-128">足夠的 Azure 儲存體以儲存金鑰保存庫記錄。</span><span class="sxs-lookup"><span data-stu-id="5d111-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <span data-ttu-id="5d111-129"><a id="connect"></a>連線到您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5d111-129"><a id="connect"></a>Connect to your subscriptions</span></span>
<span data-ttu-id="5d111-130">開始 Azure PowerShell 工作階段，並使用下列命令登入您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="5d111-130">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="5d111-131">在快顯瀏覽器視窗中，輸入您的 Azure 帳戶使用者名稱與密碼。</span><span class="sxs-lookup"><span data-stu-id="5d111-131">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="5d111-132">Azure PowerShell 會取得與此帳戶相關聯的所有訂用帳戶，並依預設使用第一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d111-132">Azure PowerShell will get all the subscriptions that are associated with this account and by default, uses the first one.</span></span>

<span data-ttu-id="5d111-133">如果您有多個訂用帳戶，您可能必須指定用來建立 Azure 金鑰保存庫的那一個特定訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d111-133">If you have multiple subscriptions, you might have to specify a specific one that was used to create your Azure Key Vault.</span></span> <span data-ttu-id="5d111-134">輸入下列命令以查看您帳戶的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="5d111-134">Type the following to see the subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="5d111-135">然後，輸入下列命令以指定與所要記錄之金鑰保存庫相關聯的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="5d111-135">Then, to specify the subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="5d111-136">這個步驟很重要，如果您有多個與帳戶相關聯的訂用帳戶會特別實用。</span><span class="sxs-lookup"><span data-stu-id="5d111-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="5d111-137">若您略過此步驟，則可能會收到註冊 Microsoft.Insights 的錯誤。</span><span class="sxs-lookup"><span data-stu-id="5d111-137">You may receive an error to register Microsoft.Insights if this step is skipped.</span></span>
>   
>

<span data-ttu-id="5d111-138">如需設定 Azure PowerShell 的詳細資訊，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5d111-138">For more information about configuring Azure PowerShell, see  [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="5d111-139"><a id="storage"></a>建立新的儲存體帳戶來儲存記錄</span><span class="sxs-lookup"><span data-stu-id="5d111-139"><a id="storage"></a>Create a new storage account for your logs</span></span>
<span data-ttu-id="5d111-140">雖然您可以使用現有儲存體帳戶來儲存記錄，但我們將建立新的儲存體帳戶來專用儲存金鑰保存庫記錄。</span><span class="sxs-lookup"><span data-stu-id="5d111-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated to Key Vault logs.</span></span> <span data-ttu-id="5d111-141">為了方便起見，在稍後遇到必須指定此帳戶時，我們會將詳細資料儲存到名為 **sa**的變數中。</span><span class="sxs-lookup"><span data-stu-id="5d111-141">For convenience for when we have to specify this later, we'll store the details into a variable named **sa**.</span></span>

<span data-ttu-id="5d111-142">為了進一步簡化管理，我們也會使用包含我們的金鑰保存庫的同一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="5d111-142">For additional ease of management, we'll also use the same resource group as the one that contains our key vault.</span></span> <span data-ttu-id="5d111-143">在 [開始使用教學課程](key-vault-get-started.md)中，此資源群組的名稱是 **ContosoResourceGroup** ，並且我們會繼續使用「東亞」位置。</span><span class="sxs-lookup"><span data-stu-id="5d111-143">From the [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue to use the East Asia location.</span></span> <span data-ttu-id="5d111-144">請視情況將這些值替換成您自己的值：</span><span class="sxs-lookup"><span data-stu-id="5d111-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="5d111-145">如果您決定使用現有儲存體帳戶，則必須使用和金鑰保存庫相同的訂用帳戶，此外也必須使用 Resource Manager 部署模型，而非傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="5d111-145">If you decide to use an existing storage account, it must use the same subscription as your key vault and it must use the Resource Manager deployment model, rather than the Classic deployment model.</span></span>
>
>

## <span data-ttu-id="5d111-146"><a id="identify"></a>識別用來儲存記錄的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="5d111-146"><a id="identify"></a>Identify the key vault for your logs</span></span>
<span data-ttu-id="5d111-147">在開始使用教學課程中，金鑰保存庫名稱是 **ContosoKeyVault**，因此我們會繼續使用該名稱，並將詳細資料儲存到名為 **kv** 的變數中：</span><span class="sxs-lookup"><span data-stu-id="5d111-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue to use that name and store the details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <span data-ttu-id="5d111-148"><a id="enable"></a>啟用記錄</span><span class="sxs-lookup"><span data-stu-id="5d111-148"><a id="enable"></a>Enable logging</span></span>
<span data-ttu-id="5d111-149">為了啟用金鑰保存庫記錄，我們將使用 Set-AzureRmDiagnosticSetting Cmdlet，並搭配針對新儲存體帳戶和金鑰保存庫所建立的變數。</span><span class="sxs-lookup"><span data-stu-id="5d111-149">To enable logging for Key Vault, we'll use the Set-AzureRmDiagnosticSetting cmdlet, together with the variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="5d111-150">我們也會將 **-Enabled** 旗標設定為 **$true**，並將類別設定為 AuditEvent (金鑰保存庫記錄適用的唯一類別)：</span><span class="sxs-lookup"><span data-stu-id="5d111-150">We'll also set the **-Enabled** flag to **$true** and set the category to AuditEvent (the only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="5d111-151">此命令的輸出包含：</span><span class="sxs-lookup"><span data-stu-id="5d111-151">The output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="5d111-152">這個結果可確認金鑰保存庫記錄現已啟用，系統會將資訊儲存到儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="5d111-152">This confirms that logging is now enabled for your key vault, saving information to your storage account.</span></span>

<span data-ttu-id="5d111-153">您也可以選擇性地設定記錄檔的保留原則，以便自動刪除較舊的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5d111-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="5d111-154">例如，使用 **-RetentionEnabled** 旗標將保留原則設為 **$true** 並將 **-RetentionInDays** 參數設為 **90**，以便自動刪除超過 90 天的舊記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5d111-154">For example, set retention policy using **-RetentionEnabled** flag to **$true** and set **-RetentionInDays** parameter to **90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="5d111-155">所記錄的內容：</span><span class="sxs-lookup"><span data-stu-id="5d111-155">What's logged:</span></span>

* <span data-ttu-id="5d111-156">會記錄所有已驗證的 REST API 要求，包括因為存取權限、系統錯誤或要求錯誤而發生的失敗要求。</span><span class="sxs-lookup"><span data-stu-id="5d111-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="5d111-157">對金鑰保存庫本身所執行的作業，包括建立、刪除、設定金鑰保存庫存取原則，以及更新金鑰保存庫屬性 (例如標記)。</span><span class="sxs-lookup"><span data-stu-id="5d111-157">Operations on the key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="5d111-158">對金鑰保存庫中的金鑰和密碼所執行的作業，包括建立、修改或刪除這些金鑰或密碼，以及簽署、驗證、加密、解密、包裝和解除包裝金鑰、取得密碼、列出金鑰和密碼及其版本等等的作業。</span><span class="sxs-lookup"><span data-stu-id="5d111-158">Operations on keys and secrets in the key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="5d111-159">產生 401 回應的未經驗證要求。</span><span class="sxs-lookup"><span data-stu-id="5d111-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="5d111-160">例如，沒有持有人權杖的要求，或格式不正確或已過期的要求，或具有無效權杖的要求。</span><span class="sxs-lookup"><span data-stu-id="5d111-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <span data-ttu-id="5d111-161"><a id="access"></a>存取記錄</span><span class="sxs-lookup"><span data-stu-id="5d111-161"><a id="access"></a>Access your logs</span></span>
<span data-ttu-id="5d111-162">金鑰保存庫記錄儲存在所提供儲存體帳戶的 **insights-logs-auditevent** 容器中。</span><span class="sxs-lookup"><span data-stu-id="5d111-162">Key vault logs are stored in the **insights-logs-auditevent** container in the storage account you provided.</span></span> <span data-ttu-id="5d111-163">若要列出此容器中的所有 blob，請輸入：</span><span class="sxs-lookup"><span data-stu-id="5d111-163">To list all the blobs in this container, type:</span></span>

<span data-ttu-id="5d111-164">首先，建立容器名稱的變數。</span><span class="sxs-lookup"><span data-stu-id="5d111-164">First, create a variable for the container name.</span></span> <span data-ttu-id="5d111-165">此變數會用於逐步解說剩餘的各個部分。</span><span class="sxs-lookup"><span data-stu-id="5d111-165">This will be used throughout the rest of the walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="5d111-166">若要列出此容器中的所有 blob，請輸入：</span><span class="sxs-lookup"><span data-stu-id="5d111-166">To list all the blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="5d111-167">其輸出類似如下範例：</span><span class="sxs-lookup"><span data-stu-id="5d111-167">The output will look something similar to this:</span></span>

<span data-ttu-id="5d111-168">**容器 Uri：https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="5d111-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="5d111-169">**名稱**</span><span class="sxs-lookup"><span data-stu-id="5d111-169">**Name**</span></span>

- - -
<span data-ttu-id="5d111-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="5d111-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="5d111-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="5d111-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="5d111-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span><span class="sxs-lookup"><span data-stu-id="5d111-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span></span>

<span data-ttu-id="5d111-173">在此輸出中我們可以看到，blob 遵循以下命名慣例：**resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span><span class="sxs-lookup"><span data-stu-id="5d111-173">As you can see from this output, the blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="5d111-174">日期和時間值使用 UTC。</span><span class="sxs-lookup"><span data-stu-id="5d111-174">The date and time values use UTC.</span></span>

<span data-ttu-id="5d111-175">因為可以使用相同的儲存體帳戶來收集多個資源的記錄，blob 名稱中的完整資源識別碼很適合用來只存取或下載所需 blob。</span><span class="sxs-lookup"><span data-stu-id="5d111-175">Because the same storage account can be used to collect logs for multiple resources, the full resource ID in the blob name is very useful to access or download just the blobs that you need.</span></span> <span data-ttu-id="5d111-176">但在這麼做之前，我們要先討論如何下載所有 blob。</span><span class="sxs-lookup"><span data-stu-id="5d111-176">But before we do that, we'll first cover how to download all the blobs.</span></span>

<span data-ttu-id="5d111-177">首先，建立資料夾來下載 blob。</span><span class="sxs-lookup"><span data-stu-id="5d111-177">First, create a folder to download the blobs.</span></span> <span data-ttu-id="5d111-178">例如：</span><span class="sxs-lookup"><span data-stu-id="5d111-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="5d111-179">然後取得所有 blob 的清單：</span><span class="sxs-lookup"><span data-stu-id="5d111-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="5d111-180">透過 'Get-AzureStorageBlobContent' 以管道傳送這份清單，將 blob 下載到目的地資料夾：</span><span class="sxs-lookup"><span data-stu-id="5d111-180">Pipe this list through 'Get-AzureStorageBlobContent' to download the blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="5d111-181">在執行第二個命令時，blob 名稱中的 **/** 分隔符號會在目的地資料夾下建立完整資料夾結構，而此結構將會用來下載 blob 並儲存為檔案。</span><span class="sxs-lookup"><span data-stu-id="5d111-181">When you run this second command, the **/** delimiter in the blob names create a full folder structure under the destination folder, and this structure will be used to download and store the blobs as files.</span></span>

<span data-ttu-id="5d111-182">若要有所選擇地下載 blob，請使用萬用字元。</span><span class="sxs-lookup"><span data-stu-id="5d111-182">To selectively download blobs, use wildcards.</span></span> <span data-ttu-id="5d111-183">例如：</span><span class="sxs-lookup"><span data-stu-id="5d111-183">For example:</span></span>

* <span data-ttu-id="5d111-184">如果您有多個金鑰保存庫，並且只想下載其中的 CONTOSOKEYVAULT3 金鑰保存庫的記錄：</span><span class="sxs-lookup"><span data-stu-id="5d111-184">If you have multiple key vaults and want to download logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="5d111-185">如果您有多個資源群組，並且只想下載其中某個資源群組的記錄，請使用 `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`：</span><span class="sxs-lookup"><span data-stu-id="5d111-185">If you have multiple resource groups and want to download logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="5d111-186">如果您想下載 2016 年 1 月份當月的所有記錄，請使用 `-Blob '*/year=2016/m=01/*'`：</span><span class="sxs-lookup"><span data-stu-id="5d111-186">If you want to download all the logs for the month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="5d111-187">您現在已做好準備，可以開始查看記錄中有何內容。</span><span class="sxs-lookup"><span data-stu-id="5d111-187">You're now ready to start looking at what's in the logs.</span></span> <span data-ttu-id="5d111-188">但在開始之前，您可能還需要了解 Get-AzureRmDiagnosticSetting 的兩個參數：</span><span class="sxs-lookup"><span data-stu-id="5d111-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need to know:</span></span>

* <span data-ttu-id="5d111-189">若要查詢金鑰保存庫資源的診斷設定狀態：`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="5d111-189">To query the  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="5d111-190">若要停用金鑰保存庫資源記錄： `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="5d111-190">To disable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <span data-ttu-id="5d111-191"><a id="interpret"></a>解譯金鑰保存庫記錄</span><span class="sxs-lookup"><span data-stu-id="5d111-191"><a id="interpret"></a>Interpret your Key Vault logs</span></span>
<span data-ttu-id="5d111-192">各個 blob 皆會儲存為文字，並格式化為 JSON blob。</span><span class="sxs-lookup"><span data-stu-id="5d111-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="5d111-193">以下是執行 `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`後所得到的範例記錄項目：</span><span class="sxs-lookup"><span data-stu-id="5d111-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

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


<span data-ttu-id="5d111-194">下表列出各個欄位的名稱和其描述。</span><span class="sxs-lookup"><span data-stu-id="5d111-194">The following table lists the field names and descriptions.</span></span>

| <span data-ttu-id="5d111-195">欄位名稱</span><span class="sxs-lookup"><span data-stu-id="5d111-195">Field name</span></span> | <span data-ttu-id="5d111-196">說明</span><span class="sxs-lookup"><span data-stu-id="5d111-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5d111-197">分析</span><span class="sxs-lookup"><span data-stu-id="5d111-197">time</span></span> |<span data-ttu-id="5d111-198">日期和時間 (UTC)。</span><span class="sxs-lookup"><span data-stu-id="5d111-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="5d111-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="5d111-199">resourceId</span></span> |<span data-ttu-id="5d111-200">Azure 資源管理員資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="5d111-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="5d111-201">對於金鑰保存庫記錄來說，這一律是金鑰保存庫的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="5d111-201">For Key Vault logs, this is always the  Key Vault resource ID.</span></span> |
| <span data-ttu-id="5d111-202">operationName</span><span class="sxs-lookup"><span data-stu-id="5d111-202">operationName</span></span> |<span data-ttu-id="5d111-203">下一份表格所述作業的名稱。</span><span class="sxs-lookup"><span data-stu-id="5d111-203">Name of the operation, as documented in the next table.</span></span> |
| <span data-ttu-id="5d111-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="5d111-204">operationVersion</span></span> |<span data-ttu-id="5d111-205">這是用戶端所要求的 REST API 版本。</span><span class="sxs-lookup"><span data-stu-id="5d111-205">This is the REST API version requested by the client.</span></span> |
| <span data-ttu-id="5d111-206">category</span><span class="sxs-lookup"><span data-stu-id="5d111-206">category</span></span> |<span data-ttu-id="5d111-207">對於金鑰保存庫記錄來說，AuditEvent 是其唯一可用的值。</span><span class="sxs-lookup"><span data-stu-id="5d111-207">For Key Vault logs, AuditEvent is the single, available value.</span></span> |
| <span data-ttu-id="5d111-208">resultType</span><span class="sxs-lookup"><span data-stu-id="5d111-208">resultType</span></span> |<span data-ttu-id="5d111-209">REST API 要求的結果。</span><span class="sxs-lookup"><span data-stu-id="5d111-209">Result of REST API request.</span></span> |
| <span data-ttu-id="5d111-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="5d111-210">resultSignature</span></span> |<span data-ttu-id="5d111-211">HTTP 狀態。</span><span class="sxs-lookup"><span data-stu-id="5d111-211">HTTP status.</span></span> |
| <span data-ttu-id="5d111-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="5d111-212">resultDescription</span></span> |<span data-ttu-id="5d111-213">結果的其他描述 (若有提供)。</span><span class="sxs-lookup"><span data-stu-id="5d111-213">Additional description about the result, when available.</span></span> |
| <span data-ttu-id="5d111-214">durationMs</span><span class="sxs-lookup"><span data-stu-id="5d111-214">durationMs</span></span> |<span data-ttu-id="5d111-215">服務 REST API 要求時所花費的時間，以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="5d111-215">Time it took to service the REST API request, in milliseconds.</span></span> <span data-ttu-id="5d111-216">此時間不包括網路延遲，因此在用戶端所測量到的時間可能不符合此時間。</span><span class="sxs-lookup"><span data-stu-id="5d111-216">This does not include the network latency, so the time you measure on the client side might not match this time.</span></span> |
| <span data-ttu-id="5d111-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="5d111-217">callerIpAddress</span></span> |<span data-ttu-id="5d111-218">提出要求之用戶端的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5d111-218">IP address of the client who made the request.</span></span> |
| <span data-ttu-id="5d111-219">correlationId</span><span class="sxs-lookup"><span data-stu-id="5d111-219">correlationId</span></span> |<span data-ttu-id="5d111-220">選擇性的 GUID，用戶端可傳遞此 GUID 來讓用戶端記錄與服務端 (金鑰保存庫) 記錄相互關聯。</span><span class="sxs-lookup"><span data-stu-id="5d111-220">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="5d111-221">身分識別</span><span class="sxs-lookup"><span data-stu-id="5d111-221">identity</span></span> |<span data-ttu-id="5d111-222">在提出 REST API 要求時所提供之權杖中的身分識別。</span><span class="sxs-lookup"><span data-stu-id="5d111-222">Identity from the token that was presented when making the REST API request.</span></span> <span data-ttu-id="5d111-223">和 Azure PowerShell Cmdlet 所產生之要求的案例一樣，這通常是「使用者」、「服務主體」或「使用者+appId」的組合。</span><span class="sxs-lookup"><span data-stu-id="5d111-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="5d111-224">properties</span><span class="sxs-lookup"><span data-stu-id="5d111-224">properties</span></span> |<span data-ttu-id="5d111-225">在不同作業 (operationName) 中，此欄位會包含不同的資訊。</span><span class="sxs-lookup"><span data-stu-id="5d111-225">This field will contain different information based on the operation (operationName).</span></span> <span data-ttu-id="5d111-226">在大部分情況下，會包含用戶端資訊 (用戶端所傳遞的使用者代理程式字串)、確切的 REST API 要求 URI 和 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="5d111-226">In most cases, contains client information (the useragent string passed by the client), the exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="5d111-227">此外，在因為提出要求 (例如，KeyCreate 或 VaultGet) 而傳回物件時，此欄位還將包含金鑰 URI (形式為 "id")、保存庫 URI 或密碼 URI。</span><span class="sxs-lookup"><span data-stu-id="5d111-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain the Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="5d111-228">**operationName** 欄位值的格式為 ObjectVerb。</span><span class="sxs-lookup"><span data-stu-id="5d111-228">The **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="5d111-229">例如：</span><span class="sxs-lookup"><span data-stu-id="5d111-229">For example:</span></span>

* <span data-ttu-id="5d111-230">所有金鑰保存庫作業都有 'Vault`<action>`' 格式，例如 `VaultGet` 和 `VaultCreate`。</span><span class="sxs-lookup"><span data-stu-id="5d111-230">All key vault operations have the 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="5d111-231">所有金鑰作業都有 'Key`<action>`' 格式，例如 `KeySign` 和 `KeyList`。</span><span class="sxs-lookup"><span data-stu-id="5d111-231">All  key operations have the 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="5d111-232">所有密碼作業都有 'Secret`<action>`' 格式，例如 `SecretGet` 和 `SecretListVersions`。</span><span class="sxs-lookup"><span data-stu-id="5d111-232">All secret operations have the 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="5d111-233">下表列出 operationName 和相對應的 REST API 命令。</span><span class="sxs-lookup"><span data-stu-id="5d111-233">The following table lists the operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="5d111-234">operationName</span><span class="sxs-lookup"><span data-stu-id="5d111-234">operationName</span></span> | <span data-ttu-id="5d111-235">REST API 命令</span><span class="sxs-lookup"><span data-stu-id="5d111-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="5d111-236">驗證</span><span class="sxs-lookup"><span data-stu-id="5d111-236">Authentication</span></span> |<span data-ttu-id="5d111-237">透過 Azure Active Directory 端點</span><span class="sxs-lookup"><span data-stu-id="5d111-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="5d111-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="5d111-238">VaultGet</span></span> |[<span data-ttu-id="5d111-239">取得金鑰保存庫的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5d111-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="5d111-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="5d111-240">VaultPut</span></span> |[<span data-ttu-id="5d111-241">建立或更新金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="5d111-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="5d111-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="5d111-242">VaultDelete</span></span> |[<span data-ttu-id="5d111-243">刪除金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="5d111-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="5d111-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="5d111-244">VaultPatch</span></span> |[<span data-ttu-id="5d111-245">更新金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="5d111-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="5d111-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="5d111-246">VaultList</span></span> |[<span data-ttu-id="5d111-247">列出資源群組中的所有金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="5d111-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="5d111-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="5d111-248">KeyCreate</span></span> |[<span data-ttu-id="5d111-249">建立金鑰</span><span class="sxs-lookup"><span data-stu-id="5d111-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="5d111-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="5d111-250">KeyGet</span></span> |[<span data-ttu-id="5d111-251">取得金鑰的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5d111-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="5d111-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="5d111-252">KeyImport</span></span> |[<span data-ttu-id="5d111-253">將金鑰匯入保存庫</span><span class="sxs-lookup"><span data-stu-id="5d111-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="5d111-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="5d111-254">KeyBackup</span></span> |<span data-ttu-id="5d111-255">[備份金鑰](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5d111-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="5d111-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="5d111-256">KeyDelete</span></span> |[<span data-ttu-id="5d111-257">刪除金鑰</span><span class="sxs-lookup"><span data-stu-id="5d111-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="5d111-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="5d111-258">KeyRestore</span></span> |[<span data-ttu-id="5d111-259">還原金鑰</span><span class="sxs-lookup"><span data-stu-id="5d111-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="5d111-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="5d111-260">KeySign</span></span> |[<span data-ttu-id="5d111-261">使用金鑰簽署</span><span class="sxs-lookup"><span data-stu-id="5d111-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="5d111-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="5d111-262">KeyVerify</span></span> |[<span data-ttu-id="5d111-263">使用金鑰驗證</span><span class="sxs-lookup"><span data-stu-id="5d111-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="5d111-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="5d111-264">KeyWrap</span></span> |[<span data-ttu-id="5d111-265">包裝金鑰</span><span class="sxs-lookup"><span data-stu-id="5d111-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="5d111-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="5d111-266">KeyUnwrap</span></span> |[<span data-ttu-id="5d111-267">解除包裝金鑰</span><span class="sxs-lookup"><span data-stu-id="5d111-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="5d111-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="5d111-268">KeyEncrypt</span></span> |[<span data-ttu-id="5d111-269">使用金鑰加密</span><span class="sxs-lookup"><span data-stu-id="5d111-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="5d111-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="5d111-270">KeyDecrypt</span></span> |[<span data-ttu-id="5d111-271">使用金鑰解密</span><span class="sxs-lookup"><span data-stu-id="5d111-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="5d111-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="5d111-272">KeyUpdate</span></span> |[<span data-ttu-id="5d111-273">更新金鑰</span><span class="sxs-lookup"><span data-stu-id="5d111-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="5d111-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="5d111-274">KeyList</span></span> |[<span data-ttu-id="5d111-275">列出保存庫中的金鑰</span><span class="sxs-lookup"><span data-stu-id="5d111-275">List the keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="5d111-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="5d111-276">KeyListVersions</span></span> |[<span data-ttu-id="5d111-277">列出金鑰的版本</span><span class="sxs-lookup"><span data-stu-id="5d111-277">List the versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="5d111-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="5d111-278">SecretSet</span></span> |[<span data-ttu-id="5d111-279">建立密碼</span><span class="sxs-lookup"><span data-stu-id="5d111-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="5d111-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="5d111-280">SecretGet</span></span> |[<span data-ttu-id="5d111-281">取得密碼</span><span class="sxs-lookup"><span data-stu-id="5d111-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="5d111-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="5d111-282">SecretUpdate</span></span> |[<span data-ttu-id="5d111-283">更新密碼</span><span class="sxs-lookup"><span data-stu-id="5d111-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="5d111-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="5d111-284">SecretDelete</span></span> |[<span data-ttu-id="5d111-285">刪除秘密</span><span class="sxs-lookup"><span data-stu-id="5d111-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="5d111-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="5d111-286">SecretList</span></span> |[<span data-ttu-id="5d111-287">列出保存庫中的密碼</span><span class="sxs-lookup"><span data-stu-id="5d111-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="5d111-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="5d111-288">SecretListVersions</span></span> |[<span data-ttu-id="5d111-289">列出密碼的版本</span><span class="sxs-lookup"><span data-stu-id="5d111-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <span data-ttu-id="5d111-290"><a id="loganalytics"></a>使用 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="5d111-290"><a id="loganalytics"></a>Use Log Analytics</span></span>

<span data-ttu-id="5d111-291">您可以使用 Log Analytics 中的 Azure 金鑰保存庫解決方案來檢閱 Azure 金鑰保存庫 AuditEvent 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5d111-291">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="5d111-292">如需詳細資訊 (包括如何進行此設定)，請參閱 [Log Analytics 中的 Azure Key Vault 解決方案](../log-analytics/log-analytics-azure-key-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="5d111-292">For more information, including how to set this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="5d111-293">如果您需要從 Log Analytics 預覽版時期所提供的舊 Key Vault 解決方案 (其中您是先將記錄檔路由遞送至「Azure 儲存體」帳戶，然後將 Log Analytics 設定成從該處讀取) 移轉，本文也包含相關指示。</span><span class="sxs-lookup"><span data-stu-id="5d111-293">This article also contains instructions if you need to migrate from the old Key Vault solution that was offered during the Log Analytics preview, where you first routed your logs to an Azure Storage account and configured Log Analytics to read from there.</span></span>

## <span data-ttu-id="5d111-294"><a id="next"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d111-294"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="5d111-295">如需在 Web 應用程式中使用 Azure 金鑰保存庫的教學課程，請參閱 [從 Web 應用程式使用 Azure 金鑰保存庫](key-vault-use-from-web-application.md)。</span><span class="sxs-lookup"><span data-stu-id="5d111-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="5d111-296">如需程式設計參考，請參閱 [Azure 金鑰保存庫開發人員指南](key-vault-developers-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="5d111-296">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="5d111-297">如需 Azure 金鑰保存庫的 Azure PowerShell 1.0 Cmdlet 清單，請參閱 [Azure 金鑰保存庫 Cmdlet](/powershell/module/azurerm.keyvault/#key_vault)。</span><span class="sxs-lookup"><span data-stu-id="5d111-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="5d111-298">如需有關 Azure 金鑰保存庫的金鑰輪替和記錄檔稽核的教學課程，請參閱 [如何使用端對端金鑰輪替和稽核設定金鑰保存庫](key-vault-key-rotation-log-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="5d111-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How to setup Key Vault with end to end key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>
