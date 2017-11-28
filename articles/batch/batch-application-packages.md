---
title: "計算節點-Azure 批次上的 aaaInstall 應用程式封裝 |Microsoft 文件"
description: "使用 hello 應用程式封裝功能的 Azure 批次 tooeasily 管理多個應用程式，並可在批次上安裝的版本的計算節點。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a><span data-ttu-id="a5b3e-103">部署應用程式 toocompute 節點與批次應用程式套件</span><span class="sxs-lookup"><span data-stu-id="a5b3e-103">Deploy applications toocompute nodes with Batch application packages</span></span>

<span data-ttu-id="a5b3e-104">Azure 批次的 hello 應用程式封裝的功能提供便於管理工作的應用程式和其部署 toohello 計算集區中的節點。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-104">hello application packages feature of Azure Batch provides easy management of task applications and their deployment toohello compute nodes in your pool.</span></span> <span data-ttu-id="a5b3e-105">與應用程式封裝，您可以上傳和管理多個版本的 hello 應用程式執行您的工作，包括其支援的檔案。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-105">With application packages, you can upload and manage multiple versions of hello applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="a5b3e-106">然後您可以自動部署一或多個這些應用程式 toohello 計算集區中的節點。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-106">You can then automatically deploy one or more of these applications toohello compute nodes in your pool.</span></span>

<span data-ttu-id="a5b3e-107">在本文中，您將學習如何 tooupload 和管理在 hello Azure 入口網站中的應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-107">In this article, you will learn how tooupload and manage application packages in hello Azure portal.</span></span> <span data-ttu-id="a5b3e-108">然後您將學習 tooinstall 如何當它們在集區的計算節點與 hello[批次.NET] [ api_net]程式庫。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-108">You will then learn how tooinstall them on a pool's compute nodes with hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="a5b3e-109">在 2017 年 7 月 5 日之後建立的所有 Batch 集區都支援應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="a5b3e-110">只有建立 hello 集區時使用的雲端服務組態，10 年 3 月 2016年和 5 年 7 月 2017年之間建立的批次集區中支援它們。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="a5b3e-111">建立先前 too10 2016 年 3 月的批次集區不支援應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-111">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="a5b3e-112">hello 應用程式開發介面來建立和管理應用程式套件屬於 hello [Batch Management.NET] [[api_net_mgmt]] 文件庫。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-112">hello APIs for creating and managing application packages are part of hello [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="a5b3e-113">hello 計算節點上安裝應用程式封裝的應用程式開發介面屬於 hello[批次.NET] [ api_net]程式庫。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-113">hello APIs for installing application packages on a compute node are part of hello [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="a5b3e-114">此處所述的 hello 應用程式套件 」 功能會取代 hello 批次應用程式中可用功能，舊版的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-114">hello application packages feature described here supersedes hello Batch Apps feature available in previous versions of hello service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="a5b3e-115">應用程式封裝需求</span><span class="sxs-lookup"><span data-stu-id="a5b3e-115">Application package requirements</span></span>
<span data-ttu-id="a5b3e-116">toouse 應用程式封裝，您需要太[Azure 儲存體帳戶連結](#link-a-storage-account)tooyour Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-116">toouse application packages, you need too[link an Azure Storage account](#link-a-storage-account) tooyour Batch account.</span></span>

<span data-ttu-id="a5b3e-117">已引入此功能[批次 REST API] [ api_rest]版本 2015年-12-01.2.2 和 hello 對應[批次.NET] [ api_net]程式庫版本3.1.0 來執行實驗。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and hello corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="a5b3e-118">我們建議使用批次時，一律使用最新 API 版本 hello。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-118">We recommend that you always use hello latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="a5b3e-119">在 2017 年 7 月 5 日之後建立的所有 Batch 集區都支援應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="a5b3e-120">只有建立 hello 集區時使用的雲端服務組態，10 年 3 月 2016年和 5 年 7 月 2017年之間建立的批次集區中支援它們。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="a5b3e-121">建立先前 too10 2016 年 3 月的批次集區不支援應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-121">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="a5b3e-122">關於應用程式和應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="a5b3e-122">About applications and application packages</span></span>
<span data-ttu-id="a5b3e-123">Azure 批次內*應用程式*參考 tooa 組的建立版本的二進位檔可以自動下載的 toohello 計算節點的 程式集區。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-123">Within Azure Batch, an *application* refers tooa set of versioned binaries that can be automatically downloaded toohello compute nodes in your pool.</span></span> <span data-ttu-id="a5b3e-124">*應用程式封裝*參考 tooa*組特定*這些二進位檔和代表給定*版本*hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-124">An *application package* refers tooa *specific set* of those binaries and represents a given *version* of hello application.</span></span>

<span data-ttu-id="a5b3e-125">![應用程式和應用程式套件的高階圖表][1]</span><span class="sxs-lookup"><span data-stu-id="a5b3e-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="a5b3e-126">應用程式</span><span class="sxs-lookup"><span data-stu-id="a5b3e-126">Applications</span></span>
<span data-ttu-id="a5b3e-127">批次中的應用程式包含一或多個應用程式封裝，然後指定 hello 應用程式的組態選項。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-127">An application in Batch contains one or more application packages and specifies configuration options for hello application.</span></span> <span data-ttu-id="a5b3e-128">例如，應用程式可以指定 hello 預設應用程式封裝版本 tooinstall 計算節點和其封裝是否可以更新或刪除。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-128">For example, an application can specify hello default application package version tooinstall on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="a5b3e-129">應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="a5b3e-129">Application packages</span></span>
<span data-ttu-id="a5b3e-130">應用程式封裝是包含 hello 應用程式二進位檔.zip 檔案，以及所需的工作 toorun hello 應用程式支援檔案。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-130">An application package is a .zip file that contains hello application binaries and supporting files that are required for your tasks toorun hello application.</span></span> <span data-ttu-id="a5b3e-131">每個應用程式封裝代表 hello 應用程式的特定版本。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-131">Each application package represents a specific version of hello application.</span></span>

<span data-ttu-id="a5b3e-132">您可以指定在 hello 集區和工作層級的應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-132">You can specify application packages at hello pool and task levels.</span></span> <span data-ttu-id="a5b3e-133">當您建立集區或工作時，您可以指定這些套件之中的一個或多個，以及 (選擇性) 指定版本。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="a5b3e-134">**集區的應用程式封裝**太部署*每*hello 集區中的節點。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-134">**Pool application packages** are deployed too*every* node in hello pool.</span></span> <span data-ttu-id="a5b3e-135">當節點加入集區以及重新啟動或重新安裝映像時，就會部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="a5b3e-136">當集區中的所有節點都執行某作業的工作時，便適合使用集區應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="a5b3e-137">您可以在建立集區時指定一或多個應用程式套件，而且可以新增或更新現有集區的套件。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="a5b3e-138">如果您更新現有的集區的應用程式封裝，您必須重新啟動節點 tooinstall hello 新封裝。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-138">If you update an existing pool's application packages, you must restart its nodes tooinstall hello new package.</span></span>
* <span data-ttu-id="a5b3e-139">**工作應用程式封裝**tooa 計算節點排程 toorun 工作之前執行 hello 工作的命令列只會部署。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-139">**Task application packages** are deployed only tooa compute node scheduled toorun a task, just before running hello task's command line.</span></span> <span data-ttu-id="a5b3e-140">如果 hello 指定應用程式套件與版本已 hello 節點上，未重新部署，使用 hello 現有套件。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-140">If hello specified application package and version is already on hello node, it is not redeployed and hello existing package is used.</span></span>
  
    <span data-ttu-id="a5b3e-141">工作應用程式封裝是有用的共用集區，其中一個集區中，執行不同的工作，且環境中的工作完成時，不會刪除 hello 集區。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and hello pool is not deleted when a job is completed.</span></span> <span data-ttu-id="a5b3e-142">如果作業有 hello 集區中的節點比有較少的工作，工作應用程式封裝可以減少資料傳輸因為您的應用程式是執行工作的已部署的唯一 toohello 節點。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-142">If your job has fewer tasks than nodes in hello pool, task application packages can minimize data transfer since your application is deployed only toohello nodes that run tasks.</span></span>
  
    <span data-ttu-id="a5b3e-143">其他可受益於工作應用程式套件的情節為執行大型應用程式，但只用於少數工作的作業。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="a5b3e-144">例如，前置處理階段或合併工作，其中 hello 前置處理或合併式應用程式是重量級，可能會受益於使用工作應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-144">For example, a pre-processing stage or a merge task, where hello pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5b3e-145">有一些限制和 hello 應用程式最大封裝大小上的應用程式和批次帳戶內的應用程式套件的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-145">There are restrictions on hello number of applications and application packages within a Batch account and on hello maximum application package size.</span></span> <span data-ttu-id="a5b3e-146">請參閱[hello Azure 批次服務的配額與限制](batch-quota-limit.md)這些限制的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-146">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="a5b3e-147">應用程式封裝的優點</span><span class="sxs-lookup"><span data-stu-id="a5b3e-147">Benefits of application packages</span></span>
<span data-ttu-id="a5b3e-148">應用程式封裝可以簡化 hello 批次的解決方案和低 hello 負擔必要的 toomanage hello 執行應用程式，您的工作中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-148">Application packages can simplify hello code in your Batch solution and lower hello overhead required toomanage hello applications that your tasks run.</span></span>

<span data-ttu-id="a5b3e-149">應用程式封裝與集區的啟動工作沒有 toospecify 一長串的個別資源檔案 tooinstall hello 節點上。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-149">With application packages, your pool's start task doesn't have toospecify a long list of individual resource files tooinstall on hello nodes.</span></span> <span data-ttu-id="a5b3e-150">您不需要 toomanually 管理應用程式檔案的 Azure 儲存體，或在節點上的多個版本。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-150">You don't have toomanually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="a5b3e-151">而且，您不需要有關產生 tooworry [SAS Url](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide 存取 toohello 檔案在儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-151">And, you don't need tooworry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide access toohello files in your Storage account.</span></span> <span data-ttu-id="a5b3e-152">批次與 Azure 儲存體 toostore 應用程式套件的 hello 背景的運作方式，並將其部署 toocompute 節點。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-152">Batch works in hello background with Azure Storage toostore application packages and deploy them toocompute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="a5b3e-153">hello 啟動工作的總大小必須小於或等於 too32768 字元，包括資源檔和環境變數。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-153">hello total size of a start task must be less than or equal too32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="a5b3e-154">如果啟動工作超過此限制，就可另外選擇使用應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="a5b3e-155">您可以也建立 zip 的封存包含資源檔、 將它上傳為 blob tooAzure 存放裝置，且然後將它解壓縮從 hello 命令列啟動工作。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-155">You can also create a zipped archive containing your resource files, upload it as a blob tooAzure Storage, and then unzip it from hello command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="a5b3e-156">上傳及管理應用程式</span><span class="sxs-lookup"><span data-stu-id="a5b3e-156">Upload and manage applications</span></span>
<span data-ttu-id="a5b3e-157">您可以使用 hello [Azure 入口網站][ portal]或 hello [Batch Management.NET](batch-management-dotnet.md)文件庫 toomanage hello 批次帳戶中的應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-157">You can use hello [Azure portal][portal] or hello [Batch Management .NET](batch-management-dotnet.md) library toomanage hello application packages in your Batch account.</span></span> <span data-ttu-id="a5b3e-158">在 hello 接下來的幾個章節，我們先說明如何 toolink 儲存體帳戶，然後討論新增應用程式及封裝並進行管理與 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-158">In hello next few sections, we first show how toolink a Storage account, then discuss adding applications and packages and managing them with hello portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="a5b3e-159">連結儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a5b3e-159">Link a Storage account</span></span>
<span data-ttu-id="a5b3e-160">toouse 應用程式封裝，您必須先連結的 Azure 儲存體帳戶 tooyour Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-160">toouse application packages, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="a5b3e-161">如果您尚未設定儲存體帳戶，hello Azure 入口網站會顯示警告 hello 第一次按一下 hello**應用程式**磚中 hello**批次帳戶**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-161">If you have not yet configured a Storage account, hello Azure portal displays a warning hello first time you click hello **Applications** tile in hello **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5b3e-162">目前批次支援*只*hello**一般用途**步驟 5 中所述，儲存體帳戶類型[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)，請在[關於 Azure儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-162">Batch currently supports *only* hello **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="a5b3e-163">當您將連結的 Azure 儲存體帳戶 tooyour 批次帳戶時，連結*只***一般用途**儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-163">When you link an Azure Storage account tooyour Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="a5b3e-164">![Azure 入口網站中的「未設定儲存體帳戶」警告][9]</span><span class="sxs-lookup"><span data-stu-id="a5b3e-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="a5b3e-165">hello 批次服務會使用 hello 相關聯的儲存體帳戶 toostore 應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-165">hello Batch service uses hello associated Storage account toostore your application packages.</span></span> <span data-ttu-id="a5b3e-166">連結 hello 兩個帳戶後，批次可自動部署 hello 封裝儲存在 hello 連結儲存體帳戶 tooyour 計算節點。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-166">After you've linked hello two accounts, Batch can automatically deploy hello packages stored in hello linked Storage account tooyour compute nodes.</span></span> <span data-ttu-id="a5b3e-167">按一下 toolink 批次帳戶的儲存體帳戶 tooyour**儲存體帳戶設定**上 hello**警告**刀鋒視窗中，然後再按一下**儲存體帳戶**上 hello **儲存體帳戶**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-167">toolink a Storage account tooyour Batch account, click **Storage account settings** on hello **Warning** blade, and then click **Storage Account** on hello **Storage Account** blade.</span></span>

<span data-ttu-id="a5b3e-168">![Azure 入口網站中的選擇儲存體帳戶刀鋒視窗][10]</span><span class="sxs-lookup"><span data-stu-id="a5b3e-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="a5b3e-169">我們建議您建立「專門」用來與 Batch 帳戶搭配使用的儲存體帳戶，並在此處選取它。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="a5b3e-170">如需詳細資訊，關於如何 toocreate 儲存體帳戶，請參閱 「 建立儲存體帳戶 」 中的[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-170">For details about how toocreate a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="a5b3e-171">在您建立儲存體帳戶後，您可以再將它連結 tooyour 批次帳戶使用 hello**儲存體帳戶**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-171">After you've created a Storage account, you can then link it tooyour Batch account by using hello **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="a5b3e-172">hello 批次服務會使用 Azure 儲存體 toostore 應用程式封裝做為區塊 blob。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-172">hello Batch service uses Azure Storage toostore your application packages as block blobs.</span></span> <span data-ttu-id="a5b3e-173">您是[收費像平常一樣][ storage_pricing] hello 區塊 blob 資料。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-173">You are [charged as normal][storage_pricing] for hello block blob data.</span></span> <span data-ttu-id="a5b3e-174">會確定 tooconsider hello 大小和數目的應用程式封裝，而定期移除已被取代的封裝 toominimize 成本。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-174">Be sure tooconsider hello size and number of your application packages, and periodically remove deprecated packages toominimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="a5b3e-175">檢視目前的應用程式</span><span class="sxs-lookup"><span data-stu-id="a5b3e-175">View current applications</span></span>
<span data-ttu-id="a5b3e-176">在您的 Batch 帳戶 tooview hello 應用程式按一下 hello**應用程式**檢視 hello 時 hello 左側功能表中的功能表項目**批次帳戶**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-176">tooview hello applications in your Batch account, click hello **Applications** menu item in hello left menu while viewing hello **Batch account** blade.</span></span>

<span data-ttu-id="a5b3e-177">![應用程式圖格][2]</span><span class="sxs-lookup"><span data-stu-id="a5b3e-177">![Applications tile][2]</span></span>

<span data-ttu-id="a5b3e-178">選取此功能表選項會開啟 hello**應用程式**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="a5b3e-178">Selecting this menu option opens hello **Applications** blade:</span></span>

<span data-ttu-id="a5b3e-179">![列出應用程式][3]</span><span class="sxs-lookup"><span data-stu-id="a5b3e-179">![List applications][3]</span></span>

<span data-ttu-id="a5b3e-180">hello**應用程式**刀鋒視窗會顯示 hello 您的帳戶中的每個應用程式識別碼及 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="a5b3e-180">hello **Applications** blade displays hello ID of each application in your account and hello following properties:</span></span>

* <span data-ttu-id="a5b3e-181">**封裝**: hello 與此應用程式相關聯的版本數目。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-181">**Packages**: hello number of versions associated with this application.</span></span>
* <span data-ttu-id="a5b3e-182">**預設版本**: hello 如果當您指定 hello 應用程式集區並不表示版本安裝的應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-182">**Default version**: hello application version installed if you do not indicate a version when you specify hello application for a pool.</span></span> <span data-ttu-id="a5b3e-183">這項設定是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-183">This setting is optional.</span></span>
* <span data-ttu-id="a5b3e-184">**允許更新**： 允許 hello 值，指定封裝是否更新、 刪除和新增項目。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-184">**Allow updates**: hello value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="a5b3e-185">如果設定太**否**，封裝更新和刪除停用 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-185">If this is set too**No**, package updates and deletions are disabled for hello application.</span></span> <span data-ttu-id="a5b3e-186">而只能新增新的應用程式封裝版本。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-186">Only new application package versions can be added.</span></span> <span data-ttu-id="a5b3e-187">hello 預設值是**是**。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-187">hello default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="a5b3e-188">檢視應用程式詳細資料</span><span class="sxs-lookup"><span data-stu-id="a5b3e-188">View application details</span></span>
<span data-ttu-id="a5b3e-189">tooopen hello 刀鋒視窗，其中包含 hello 應用程式，請選取 hello 應用程式的詳細資料中 hello**應用程式**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-189">tooopen hello blade that includes hello details for an application, select hello application in hello **Applications** blade.</span></span>

<span data-ttu-id="a5b3e-190">![應用程式詳細資料][4]</span><span class="sxs-lookup"><span data-stu-id="a5b3e-190">![Application details][4]</span></span>

<span data-ttu-id="a5b3e-191">在 hello 應用程式詳細資料 刀鋒視窗，您可以設定下列應用程式設定的 hello。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-191">In hello application details blade, you can configure hello following settings for your application.</span></span>

* <span data-ttu-id="a5b3e-192">**允許更新**：指定是否可更新或刪除應用程式的應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="a5b3e-193">請參閱本文稍後的＜更新或刪除應用程式封裝＞。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="a5b3e-194">**預設版本**： 指定預設應用程式封裝 toodeploy toocompute 節點。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-194">**Default version**: Specify a default application package toodeploy toocompute nodes.</span></span>
* <span data-ttu-id="a5b3e-195">**顯示名稱**： 指定易記名稱，您解決方案可以使用時它會顯示 hello 應用程式的相關資訊，例如 hello 提供 tooyour 客戶透過批次服務的 UI 中的批次。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about hello application, for example, in hello UI of a service that you provide tooyour customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="a5b3e-196">加入新的應用程式</span><span class="sxs-lookup"><span data-stu-id="a5b3e-196">Add a new application</span></span>
<span data-ttu-id="a5b3e-197">toocreate 新的應用程式中，加入應用程式封裝，並指定新的、 唯一的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-197">toocreate a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="a5b3e-198">hello 第一個應用程式套件，您將加入新的應用程式識別碼 hello 也會建立 hello 新應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-198">hello first application package that you add with hello new application ID also creates hello new application.</span></span>

<span data-ttu-id="a5b3e-199">按一下**新增**上 hello**應用程式**刀鋒視窗 tooopen hello**新的應用程式**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-199">Click **Add** on hello **Applications** blade tooopen hello **New application** blade.</span></span>

<span data-ttu-id="a5b3e-200">![Azure 入口網站中的新增應用程式刀鋒視窗][5]</span><span class="sxs-lookup"><span data-stu-id="a5b3e-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="a5b3e-201">hello**新的應用程式**刀鋒視窗提供 hello 下列欄位 toospecify hello 設定新的應用程式和應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-201">hello **New application** blade provides hello following fields toospecify hello settings of your new application and application package.</span></span>

<span data-ttu-id="a5b3e-202">**應用程式識別碼**</span><span class="sxs-lookup"><span data-stu-id="a5b3e-202">**Application id**</span></span>

<span data-ttu-id="a5b3e-203">此欄位會指定新的應用程式，也就是主體 toohello 標準 Azure 批次識別碼的驗證規則的 hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-203">This field specifies hello ID of your new application, which is subject toohello standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="a5b3e-204">提供應用程式識別碼 hello 規則如下所示：</span><span class="sxs-lookup"><span data-stu-id="a5b3e-204">hello rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="a5b3e-205">Windows 節點上 hello 識別碼可包含英數字元、 連字號及底線的任何組合。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-205">On Windows nodes, hello ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="a5b3e-206">在 Linux 節點上，只允許使用英數字元和底線。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="a5b3e-207">不能包含超過 64 個字元。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="a5b3e-208">必須是唯一 hello 批次帳戶內。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-208">Must be unique within hello Batch account.</span></span>
* <span data-ttu-id="a5b3e-209">需保留大小寫和區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="a5b3e-210">**版本**</span><span class="sxs-lookup"><span data-stu-id="a5b3e-210">**Version**</span></span>

<span data-ttu-id="a5b3e-211">此欄位指定 hello hello 您上傳的應用程式封裝版本。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-211">This field specifies hello version of hello application package you are uploading.</span></span> <span data-ttu-id="a5b3e-212">版本字串為主體 toohello 下列驗證規則：</span><span class="sxs-lookup"><span data-stu-id="a5b3e-212">Version strings are subject toohello following validation rules:</span></span>

* <span data-ttu-id="a5b3e-213">Windows 節點上 hello 版本字串可以包含英數字元、 連字號、 底線和句號的任何組合。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-213">On Windows nodes, hello version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="a5b3e-214">在 Linux 節點上 hello 版本字串只能包含英數字元和底線。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-214">On Linux nodes, hello version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="a5b3e-215">不能包含超過 64 個字元。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="a5b3e-216">必須是唯一 hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-216">Must be unique within hello application.</span></span>
* <span data-ttu-id="a5b3e-217">需保留大小寫和區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="a5b3e-218">**應用程式封裝**</span><span class="sxs-lookup"><span data-stu-id="a5b3e-218">**Application package**</span></span>

<span data-ttu-id="a5b3e-219">此欄位會指定包含 hello 應用程式二進位檔的 hello.zip 檔案，以及所需的 tooexecute hello 應用程式支援檔案。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-219">This field specifies hello .zip file that contains hello application binaries and supporting files that are required tooexecute hello application.</span></span> <span data-ttu-id="a5b3e-220">按一下 hello**選取檔案**方塊或 hello 資料夾圖示 toobrowse tooand 選取包含您的應用程式檔案的.zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-220">Click hello **Select a file** box or hello folder icon toobrowse tooand select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="a5b3e-221">您已選取檔案之後，請按一下**確定**toobegin hello 上載 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-221">After you've selected a file, click **OK** toobegin hello upload tooAzure Storage.</span></span> <span data-ttu-id="a5b3e-222">Hello 上傳作業完成時，hello 入口網站會顯示通知，並關閉 [hello] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-222">When hello upload operation is complete, hello portal displays a notification and closes hello blade.</span></span> <span data-ttu-id="a5b3e-223">根據您所上傳和 hello 您的網路連線速度的 hello 檔案 hello 大小，這項作業可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-223">Depending on hello size of hello file that you are uploading and hello speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="a5b3e-224">請勿關閉 hello**新的應用程式**hello 上傳作業完成之前的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-224">Do not close hello **New application** blade before hello upload operation is complete.</span></span> <span data-ttu-id="a5b3e-225">如此一來，將會停止 hello 上傳程序。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-225">Doing so will stop hello upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="a5b3e-226">加入新應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="a5b3e-226">Add a new application package</span></span>
<span data-ttu-id="a5b3e-227">tooadd 新的應用程式封裝版本的現有應用程式中，選取應用程式在 hello**應用程式**刀鋒視窗中，按一下 **封裝**，然後按一下 **新增**tooopenhello**新增封裝**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-227">tooadd a new application package version for an existing application, select an application in hello **Applications** blade, click **Packages**, then click **Add** tooopen hello **Add package** blade.</span></span>

<span data-ttu-id="a5b3e-228">![Azure 入口網站中的新增應用程式套件刀鋒視窗][8]</span><span class="sxs-lookup"><span data-stu-id="a5b3e-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="a5b3e-229">如您所見，hello 欄位相符的 hello**新的應用程式**刀鋒視窗中，但 hello**應用程式識別碼**方塊已停用。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-229">As you can see, hello fields match those of hello **New application** blade, but hello **Application id** box is disabled.</span></span> <span data-ttu-id="a5b3e-230">您可以如同 hello 新應用程式，指定 hello**版本**新套件中，瀏覽 tooyour**應用程式封裝**.zip 檔案，然後按一下  **確定** tooupload hello封裝。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-230">As you did for hello new application, specify hello **Version** for your new package, browse tooyour **Application package** .zip file, then click **OK** tooupload hello package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="a5b3e-231">更新或刪除應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="a5b3e-231">Update or delete an application package</span></span>
<span data-ttu-id="a5b3e-232">tooupdate 或刪除現有的應用程式封裝，開啟 hello hello 應用程式的詳細資料 刀鋒視窗按一下**封裝**tooopen hello**封裝**刀鋒視窗中，按一下 hello**省略**hello toomodify，並選取您想要 tooperform 的 hello 動作 hello 應用程式封裝的資料列中。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-232">tooupdate or delete an existing application package, open hello details blade for hello application, click **Packages** tooopen hello **Packages** blade, click hello **ellipsis** in hello row of hello application package that you want toomodify, and select hello action that you want tooperform.</span></span>

<span data-ttu-id="a5b3e-233">![在 Azure 入口網站中更新或刪除套件][7]</span><span class="sxs-lookup"><span data-stu-id="a5b3e-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="a5b3e-234">更新</span><span class="sxs-lookup"><span data-stu-id="a5b3e-234">**Update**</span></span>

<span data-ttu-id="a5b3e-235">當您按一下**更新**，hello*更新套件*刀鋒視窗會顯示。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-235">When you click **Update**, hello *Update package* blade is displayed.</span></span> <span data-ttu-id="a5b3e-236">此刀鋒視窗會類似 toohello*新應用程式封裝*刀鋒視窗中，但只 hello 封裝選取項目欄位才會啟用，讓您新增的 ZIP 檔案 tooupload toospecify。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-236">This blade is similar toohello *New application package* blade, however only hello package selection field is enabled, allowing you toospecify a new ZIP file tooupload.</span></span>

<span data-ttu-id="a5b3e-237">![Azure 入口網站中的更新套件刀鋒視窗][11]</span><span class="sxs-lookup"><span data-stu-id="a5b3e-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="a5b3e-238">**刪除**</span><span class="sxs-lookup"><span data-stu-id="a5b3e-238">**Delete**</span></span>

<span data-ttu-id="a5b3e-239">當您按一下**刪除**，系統會要求您 tooconfirm hello 刪除 hello 封裝版本，和批次刪除 hello 封裝從 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-239">When you click **Delete**, you are asked tooconfirm hello deletion of hello package version, and Batch deletes hello package from Azure Storage.</span></span> <span data-ttu-id="a5b3e-240">如果您刪除 hello 預設版本的應用程式，hello**預設版本**hello 應用程式已移除設定。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-240">If you delete hello default version of an application, hello **Default version** setting is removed for hello application.</span></span>

<span data-ttu-id="a5b3e-241">![刪除應用程式][12]</span><span class="sxs-lookup"><span data-stu-id="a5b3e-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="a5b3e-242">將應用程式安裝在計算節點上</span><span class="sxs-lookup"><span data-stu-id="a5b3e-242">Install applications on compute nodes</span></span>
<span data-ttu-id="a5b3e-243">既然您已經學會如何 toomanage 應用程式封裝以 hello Azure 入口網站，我們可以在討論如何 toodeploy 它們 toocompute 節點與批次工作加以執行。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-243">Now that you've learned how toomanage application packages with hello Azure portal, we can discuss how toodeploy them toocompute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="a5b3e-244">安裝集區應用程式套件</span><span class="sxs-lookup"><span data-stu-id="a5b3e-244">Install pool application packages</span></span>
<span data-ttu-id="a5b3e-245">tooinstall 上所有應用程式封裝中集區的計算節點中，指定一或多個應用程式封裝*參考*hello 集區。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-245">tooinstall an application package on all compute nodes in a pool, specify one or more application package *references* for hello pool.</span></span> <span data-ttu-id="a5b3e-246">您指定的集區的 hello 應用程式封裝會安裝每個計算節點上，當該節點加入 hello 集區，以及當 hello 節點重新啟動或重新安裝映像。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-246">hello application packages that you specify for a pool are installed on each compute node when that node joins hello pool, and when hello node is rebooted or reimaged.</span></span>

<span data-ttu-id="a5b3e-247">在 Batch .NET 中，請在建立新集區時指定一或多個 [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref]，或為現有集區指定。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="a5b3e-248">hello [ApplicationPackageReference] [ net_pkgref]類別會指定應用程式識別碼和版本的集區上的 tooinstall 計算節點。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-248">hello [ApplicationPackageReference][net_pkgref] class specifies an application ID and version tooinstall on a pool's compute nodes.</span></span>

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="a5b3e-249">如果應用程式套件部署失敗，因為任何原因，hello 批次服務標 hello 節點[無法使用][net_nodestate]，和任何工作都會排定執行該節點上。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-249">If an application package deployment fails for any reason, hello Batch service marks hello node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="a5b3e-250">在此情況下，您應該**重新啟動**hello 節點 tooreinitiate hello 封裝部署。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-250">In this case, you should **restart** hello node tooreinitiate hello package deployment.</span></span> <span data-ttu-id="a5b3e-251">重新啟動的 hello 節點也可以讓工作一次排程 hello 節點上。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-251">Restarting hello node also enables task scheduling again on hello node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="a5b3e-252">安裝工作應用程式套件</span><span class="sxs-lookup"><span data-stu-id="a5b3e-252">Install task application packages</span></span>
<span data-ttu-id="a5b3e-253">類似 tooa 集區中，指定應用程式套件*參考*工作。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-253">Similar tooa pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="a5b3e-254">在節點上的排程的 toorun 工作時，hello 封裝會下載並解壓縮之前執行 hello 工作的命令列。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-254">When a task is scheduled toorun on a node, hello package is downloaded and extracted just before hello task's command line is executed.</span></span> <span data-ttu-id="a5b3e-255">如果 hello 節點上已安裝指定的封裝和版本，不會下載 hello 封裝，且 hello 現有的封裝。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-255">If a specified package and version is already installed on hello node, hello package is not downloaded and hello existing package is used.</span></span>

<span data-ttu-id="a5b3e-256">tooinstall 工作應用程式封裝時，設定 hello 工作[CloudTask][net_cloudtask]。[ApplicationPackageReferences] [ net_cloudtask_pkgref]屬性：</span><span class="sxs-lookup"><span data-stu-id="a5b3e-256">tooinstall a task application package, configure hello task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a><span data-ttu-id="a5b3e-257">執行 hello 安裝應用程式</span><span class="sxs-lookup"><span data-stu-id="a5b3e-257">Execute hello installed applications</span></span>
<span data-ttu-id="a5b3e-258">hello 您所指定的集區或工作的封裝會下載並解壓縮 tooa 名為目錄內 hello `AZ_BATCH_ROOT_DIR` hello 節點。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-258">hello packages that you've specified for a pool or task are downloaded and extracted tooa named directory within hello `AZ_BATCH_ROOT_DIR` of hello node.</span></span> <span data-ttu-id="a5b3e-259">批次也會建立包含名為目錄 hello 路徑 toohello 的環境變數。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-259">Batch also creates an environment variable that contains hello path toohello named directory.</span></span> <span data-ttu-id="a5b3e-260">參考 hello hello 節點上的應用程式時，您的工作命令列會使用這個環境變數。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-260">Your task command lines use this environment variable when referencing hello application on hello node.</span></span> 

<span data-ttu-id="a5b3e-261">Windows 節點上 hello 變數是在 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="a5b3e-261">On Windows nodes, hello variable is in hello following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="a5b3e-262">在 Linux 節點上 hello 格式有些許不同。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-262">On Linux nodes, hello format is slightly different.</span></span> <span data-ttu-id="a5b3e-263">句號 （.）、 連字號 （-） 和數字符號 （#） 都是扁平化的 toounderscores hello 環境變數中。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-263">Periods (.), hypens (-) and number signs (#) are flattened toounderscores in hello environment variable.</span></span> <span data-ttu-id="a5b3e-264">例如：</span><span class="sxs-lookup"><span data-stu-id="a5b3e-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="a5b3e-265">`APPLICATIONID`和`version`對應 toohello 應用程式和套件版本您為部署指定的值。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-265">`APPLICATIONID` and `version` are values that correspond toohello application and package version you've specified for deployment.</span></span> <span data-ttu-id="a5b3e-266">例如，如果您指定應用程式的版本 2.7 *blender*應該安裝 Windows 節點上的所有工作的命令列會都使用這個環境變數 tooaccess 及其檔案：</span><span class="sxs-lookup"><span data-stu-id="a5b3e-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable tooaccess its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="a5b3e-267">在 Linux 節點上指定 hello 環境變數以下列格式：</span><span class="sxs-lookup"><span data-stu-id="a5b3e-267">On Linux nodes, specify hello environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="a5b3e-268">當您上傳應用程式封裝時，您可以指定預設版本 toodeploy tooyour 計算節點。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-268">When you upload an application package, you can specify a default version toodeploy tooyour compute nodes.</span></span> <span data-ttu-id="a5b3e-269">如果您已經指定應用程式的預設版本，您就可以省略 hello 版本尾碼，當您參考 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-269">If you have specified a default version for an application, you can omit hello version suffix when you reference hello application.</span></span> <span data-ttu-id="a5b3e-270">中所示，您可以在 hello hello 應用程式 刀鋒視窗上的 Azure 入口網站中指定 hello 預設應用程式版本[上傳和管理應用程式](#upload-and-manage-applications)。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-270">You can specify hello default application version in hello Azure portal, on hello Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="a5b3e-271">例如，如果您設定 hello 應用程式的預設版本為"2.7" *blender*，而且您的工作參考 hello 下列環境變數，則 Windows 節點將會執行版本 2.7:</span><span class="sxs-lookup"><span data-stu-id="a5b3e-271">For example, if you set "2.7" as hello default version for application *blender*, and your tasks reference hello following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="a5b3e-272">hello 下列程式碼片段示範工作命令列範例，可啟動 hello 預設版的 hello *blender*應用程式：</span><span class="sxs-lookup"><span data-stu-id="a5b3e-272">hello following code snippet shows an example task command line that launches hello default version of hello *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="a5b3e-273">請參閱[工作的環境設定](batch-api-basics.md#environment-settings-for-tasks)在 hello[批次功能概觀](batch-api-basics.md)計算節點環境設定的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in hello [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="a5b3e-274">更新集區的應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="a5b3e-274">Update a pool's application packages</span></span>
<span data-ttu-id="a5b3e-275">如果現有的集區已設定與應用程式套件，您可以指定新套件 hello 集區。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-275">If an existing pool has already been configured with an application package, you can specify a new package for hello pool.</span></span> <span data-ttu-id="a5b3e-276">如果您指定的集區 hello 遵循套用新的封裝參考：</span><span class="sxs-lookup"><span data-stu-id="a5b3e-276">If you specify a new package reference for a pool, hello following apply:</span></span>

* <span data-ttu-id="a5b3e-277">hello 批次服務會在任何現有的節點重新啟動或重新安裝映像和新加入 hello 集區的所有節點上安裝 hello 新指定的封裝。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-277">hello Batch service installs hello newly specified package on all new nodes that join hello pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="a5b3e-278">計算您 hello 封裝參考更新時就已位於 hello 集區的節點不會自動安裝新應用程式封裝 hello。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-278">Compute nodes that are already in hello pool when you update hello package references do not automatically install hello new application package.</span></span> <span data-ttu-id="a5b3e-279">這些運算節點必須重新開機或安裝映像的 tooreceive hello 新的封裝。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-279">These compute nodes must be rebooted or reimaged tooreceive hello new package.</span></span>
* <span data-ttu-id="a5b3e-280">部署新的封裝時，環境變數建立 hello 反映 hello 新應用程式封裝參考。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-280">When a new package is deployed, hello created environment variables reflect hello new application package references.</span></span>

<span data-ttu-id="a5b3e-281">在此範例中，hello 現有集區具有 hello 2.7 版*blender*應用程式設定為其中一個其[CloudPool][net_cloudpool]。[ApplicationPackageReferences][net_cloudpool_pkgref]。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-281">In this example, hello existing pool has version 2.7 of hello *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="a5b3e-282">與版本 2.76b，tooupdate hello 集區的節點指定新[ApplicationPackageReference] [ net_pkgref] hello 新版本，與認可 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-282">tooupdate hello pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with hello new version, and commit hello change.</span></span>

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

<span data-ttu-id="a5b3e-283">既然 hello 已設定新的版本，hello 批次服務會安裝版本 2.76b tooany*新*加入 hello 集區的節點。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-283">Now that hello new version has been configured, hello Batch service installs version 2.76b tooany *new* node that joins hello pool.</span></span> <span data-ttu-id="a5b3e-284">hello 節點上的 tooinstall 2.76b*已經*hello 集區，在重新開機，或它們重新製作映像。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-284">tooinstall 2.76b on hello nodes that are *already* in hello pool, reboot or reimage them.</span></span> <span data-ttu-id="a5b3e-285">請注意，重新啟動的節點從先前的封裝部署的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-285">Note that rebooted nodes retain hello files from previous package deployments.</span></span>

## <a name="list-hello-applications-in-a-batch-account"></a><span data-ttu-id="a5b3e-286">Hello 應用程式清單中的批次帳戶</span><span class="sxs-lookup"><span data-stu-id="a5b3e-286">List hello applications in a Batch account</span></span>
<span data-ttu-id="a5b3e-287">您可以使用 hello 列出 hello 應用程式和其封裝中的批次帳戶[ApplicationOperations][net_appops]。[ListApplicationSummaries] [ net_appops_listappsummaries]方法。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-287">You can list hello applications and their packages in a Batch account by using hello [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a><span data-ttu-id="a5b3e-288">總結</span><span class="sxs-lookup"><span data-stu-id="a5b3e-288">Wrap up</span></span>
<span data-ttu-id="a5b3e-289">應用程式封裝，您可以幫助您選取 hello 應用程式為了完成其工作，並指定 hello 確切版本 toouse 時處理工作與批次啟用服務的客戶。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-289">With application packages, you can help your customers select hello applications for their jobs and specify hello exact version toouse when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="a5b3e-290">您也可能會提供客戶 tooupload hello 能力，並追蹤其自身應用程式在您的服務。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-290">You might also provide hello ability for your customers tooupload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5b3e-291">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a5b3e-291">Next steps</span></span>
* <span data-ttu-id="a5b3e-292">hello[批次 REST API] [ api_rest]也提供支援 toowork 與應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-292">hello [Batch REST API][api_rest] also provides support toowork with application packages.</span></span> <span data-ttu-id="a5b3e-293">例如，請參閱 hello [applicationPackageReferences] [ rest_add_pool_with_packages]中的項目[加入集區 tooan 帳戶][ rest_add_pool]如需如何資訊使用 REST API hello toospecify 封裝 tooinstall。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-293">For example, see hello [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool tooan account][rest_add_pool] for information about how toospecify packages tooinstall by using hello REST API.</span></span> <span data-ttu-id="a5b3e-294">請參閱[應用程式][ rest_applications]如需如何使用 tooobtain 應用程式資訊 hello 批次 REST API 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-294">See [Applications][rest_applications] for details about how tooobtain application information by using hello Batch REST API.</span></span>
* <span data-ttu-id="a5b3e-295">深入了解如何 tooprogrammatically[管理 Azure Batch 帳戶與配額使用 Batch Management.NET](batch-management-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-295">Learn how tooprogrammatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="a5b3e-296">hello [Batch Management.NET][api_net_mgmt]程式庫可以啟用的批次應用程式或服務的帳戶建立和刪除功能。</span><span class="sxs-lookup"><span data-stu-id="a5b3e-296">hello [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "應用程式套件高階圖表"
[2]: ./media/batch-application-packages/app_pkg_02.png "Azure 入口網站中的應用程式圖格"
[3]: ./media/batch-application-packages/app_pkg_03.png "Azure 入口網站中的應用程式刀鋒視窗"
[4]: ./media/batch-application-packages/app_pkg_04.png "Azure 入口網站中的應用程式詳細資料刀鋒視窗"
[5]: ./media/batch-application-packages/app_pkg_05.png "Azure 入口網站中的新增應用程式刀鋒視窗"
[7]: ./media/batch-application-packages/app_pkg_07.png "Azure 入口網站中的更新或刪除套件下拉式清單"
[8]: ./media/batch-application-packages/app_pkg_08.png "Azure 入口網站中的新增應用程式套件刀鋒視窗"
[9]: ./media/batch-application-packages/app_pkg_09.png "沒有連結的儲存體帳戶警示"
[10]: ./media/batch-application-packages/app_pkg_10.png "Azure 入口網站中的選擇儲存體帳戶刀鋒視窗"
[11]: ./media/batch-application-packages/app_pkg_11.png "Azure 入口網站中的更新套件刀鋒視窗"
[12]: ./media/batch-application-packages/app_pkg_12.png "Azure 入口網站中的刪除套件確認對話方塊"
