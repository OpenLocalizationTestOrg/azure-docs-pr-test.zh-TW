---
title: "aaaAzure 雲端殼層 （預覽） 的概觀 |Microsoft 文件"
description: "Hello Azure 雲端殼層概觀。"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="751ef-103">Azure Cloud Shell 的功能概觀 (預覽)</span><span class="sxs-lookup"><span data-stu-id="751ef-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="751ef-104">Azure Cloud Shell 是可經由瀏覽器存取的互動式殼層，應用在 Azure 資源管理上。</span><span class="sxs-lookup"><span data-stu-id="751ef-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="751ef-105">特性</span><span class="sxs-lookup"><span data-stu-id="751ef-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="751ef-106">以瀏覽器為基礎的體驗</span><span class="sxs-lookup"><span data-stu-id="751ef-106">Browser-based shell experience</span></span>
<span data-ttu-id="751ef-107">雲端殼層啟用存取 tooa 瀏覽器型命令列建置體驗與 Azure 的管理工作納入考量。</span><span class="sxs-lookup"><span data-stu-id="751ef-107">Cloud Shell enables access tooa browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="751ef-108">利用雲端殼層 toowork untethered 從本機機器只有 hello 雲端可提供的方式。</span><span class="sxs-lookup"><span data-stu-id="751ef-108">Leverage Cloud Shell toowork untethered from a local machine in a way only hello cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="751ef-109">預先設定的 Azure 工作站</span><span class="sxs-lookup"><span data-stu-id="751ef-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="751ef-110">Cloud Shell 預先安裝受歡迎的命令列工具和語言支援，能加快您的工作速度。</span><span class="sxs-lookup"><span data-stu-id="751ef-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="751ef-111">檢視 hello 完整的工具清單 Azure 雲端 shell。</span><span class="sxs-lookup"><span data-stu-id="751ef-111">View hello full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="751ef-112">自動驗證</span><span class="sxs-lookup"><span data-stu-id="751ef-112">Automatic authentication</span></span>
<span data-ttu-id="751ef-113">雲端殼層安全地透過 hello Azure CLI 2.0 的立即存取 tooyour 資源的每個工作階段上自動驗證。</span><span class="sxs-lookup"><span data-stu-id="751ef-113">Cloud Shell securely authenticates automatically on each session for instant access tooyour resources through hello Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="751ef-114">連接您的 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="751ef-114">Connect your Azure File storage</span></span>
<span data-ttu-id="751ef-115">雲端殼層電腦是暫時性的因此需要裝載為 Azure 檔案共用 toobe `clouddrive` toopersist $Home 目錄。</span><span class="sxs-lookup"><span data-stu-id="751ef-115">Cloud Shell machines are temporary and as a result require an Azure file share toobe mounted as `clouddrive` toopersist your $Home directory.</span></span>
<span data-ttu-id="751ef-116">第一次啟動雲端殼層提示的 toocreate 代替您共用的資源群組、 儲存體帳戶和檔案。</span><span class="sxs-lookup"><span data-stu-id="751ef-116">On first launch Cloud Shell prompts toocreate a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="751ef-117">這是一次性的步驟，而且會針對所有工作階段自動連接。</span><span class="sxs-lookup"><span data-stu-id="751ef-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="751ef-118">建立新的儲存體</span><span class="sxs-lookup"><span data-stu-id="751ef-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="751ef-119">可代替您建立的本地備援儲存體 (LRS) 帳戶有一個 Azure 檔案共用，其中包含預設是 5 GB 的磁碟映像。</span><span class="sxs-lookup"><span data-stu-id="751ef-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="751ef-120">hello 檔案共用做為所掛接`clouddrive`檔案共用互動 hello 磁碟映像正在使用的 toosync 和保存 $Home 目錄。</span><span class="sxs-lookup"><span data-stu-id="751ef-120">hello file share mounts as `clouddrive` for file share interaction with hello disk image being used toosync and persist your $Home directory.</span></span> <span data-ttu-id="751ef-121">所需成本和一般儲存體相同。</span><span class="sxs-lookup"><span data-stu-id="751ef-121">Regular storage costs apply.</span></span>

<span data-ttu-id="751ef-122">將代替您建立下列三個資源：</span><span class="sxs-lookup"><span data-stu-id="751ef-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="751ef-123">名稱如下的資源群組：`cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="751ef-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="751ef-124">名稱如下的儲存體帳戶：`cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="751ef-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="751ef-125">名稱如下的檔案共用：`cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="751ef-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="751ef-126">$Home 目錄中的所有檔案 (例如 SSH 金鑰) 會都保存於已掛接檔案共用中儲存的使用者磁碟映像中。</span><span class="sxs-lookup"><span data-stu-id="751ef-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="751ef-127">在 $Home 目錄和已掛接的檔案共用中儲存檔案時，請套用最佳作法。</span><span class="sxs-lookup"><span data-stu-id="751ef-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="751ef-128">使用現有的資源</span><span class="sxs-lookup"><span data-stu-id="751ef-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="751ef-129">進階的選項也會提供允許您 tooassociate 現有資源 tooCloud 殼層。</span><span class="sxs-lookup"><span data-stu-id="751ef-129">An advanced option is also provided allowing you tooassociate existing resources tooCloud Shell.</span></span> <span data-ttu-id="751ef-130">當看到 hello 儲存安裝程式提示字元中，按一下 [顯示進階設定] tooselect 其他選項。</span><span class="sxs-lookup"><span data-stu-id="751ef-130">When presented with hello storage setup prompt, click "Show advanced settings" tooselect additional options.</span></span> <span data-ttu-id="751ef-131">下拉式清單會針對您指派的 Cloud Shell 區域和本地/全域備援儲存體帳戶進行篩選。</span><span class="sxs-lookup"><span data-stu-id="751ef-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="751ef-132">[了解 Cloud Shell 儲存體、更新檔案共用，以及上傳/下載檔案。](persisting-shell-storage.md)</span><span class="sxs-lookup"><span data-stu-id="751ef-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="751ef-133">概念</span><span class="sxs-lookup"><span data-stu-id="751ef-133">Concepts</span></span>
* <span data-ttu-id="751ef-134">Cloud Shell 會在以每一工作階段、每位使用者為基礎所提供的暫存機器上執行</span><span class="sxs-lookup"><span data-stu-id="751ef-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="751ef-135">Cloud Shell 會在無互動活動的 20 分鐘後逾時</span><span class="sxs-lookup"><span data-stu-id="751ef-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="751ef-136">只有在已連接檔案共用時才能存取 Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="751ef-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="751ef-137">Cloud Shell 會以一台機器、一個使用者帳戶的方式指派</span><span class="sxs-lookup"><span data-stu-id="751ef-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="751ef-138">權限設定為一般 Linux 使用者</span><span class="sxs-lookup"><span data-stu-id="751ef-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="751ef-139">深入了解所有 Cloud Shell 功能。</span><span class="sxs-lookup"><span data-stu-id="751ef-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="751ef-140">範例</span><span class="sxs-lookup"><span data-stu-id="751ef-140">Examples</span></span>
* <span data-ttu-id="751ef-141">建立或編輯指令碼 tooautomate Azure 管理</span><span class="sxs-lookup"><span data-stu-id="751ef-141">Create or edit scripts tooautomate Azure management</span></span>
* <span data-ttu-id="751ef-142">同時透過 Azure 入口網站和 Azure CLI 2.0 管理 資源</span><span class="sxs-lookup"><span data-stu-id="751ef-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="751ef-143">試用 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="751ef-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="751ef-144">嘗試在 hello 殼層雲端快速入門的上述所有範例。</span><span class="sxs-lookup"><span data-stu-id="751ef-144">Try out all these examples at hello Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="751ef-145">價格</span><span class="sxs-lookup"><span data-stu-id="751ef-145">Pricing</span></span>
<span data-ttu-id="751ef-146">主控雲端殼層 hello 機器是免費的與掛接的 Azure 檔案的必要共用 toopersist $Home 目錄。</span><span class="sxs-lookup"><span data-stu-id="751ef-146">hello machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share toopersist your $Home directory.</span></span> <span data-ttu-id="751ef-147">所需成本和一般儲存體相同。</span><span class="sxs-lookup"><span data-stu-id="751ef-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="751ef-148">支援的瀏覽器</span><span class="sxs-lookup"><span data-stu-id="751ef-148">Supported browsers</span></span>
<span data-ttu-id="751ef-149">Cloud Shell 建議用於 Chrome、Edge 和 Safari 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="751ef-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="751ef-150">支援雲端殼層 Chrome、 Firefox、 Safari、 IE 以及邊緣，雲端殼層是主體 toospecific 瀏覽器設定。</span><span class="sxs-lookup"><span data-stu-id="751ef-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject toospecific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="751ef-151">疑難排解</span><span class="sxs-lookup"><span data-stu-id="751ef-151">Troubleshooting</span></span>
1. <span data-ttu-id="751ef-152">當使用 Azure Active Directory 訂閱，無法建立儲存體到期 tooError: 400 DisallowedOperation。</span><span class="sxs-lookup"><span data-stu-id="751ef-152">When using an Azure Active Directory subscription, I cannot create storage due tooError: 400 DisallowedOperation.</span></span> <span data-ttu-id="751ef-153">tooresolve，請使用能夠建立儲存體資源的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="751ef-153">tooresolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="751ef-154">AD 訂用帳戶會無法 toocreate Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="751ef-154">AD subscriptions are not able toocreate Azure resources.</span></span>

<span data-ttu-id="751ef-155">如需特定已知的限制，請瀏覽 [Cloud Shell 的限制](limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="751ef-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
