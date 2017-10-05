---
title: "在運算節點上安裝應用程式封裝 - Azure Batch | Microsoft Docs"
description: "使用 Azure Batch 的應用程式封裝功能輕鬆地管理多個應用程式和版本，以便安裝在 Batch 計算節點。"
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
ms.openlocfilehash: afcc04c80ec15872a22de5d5969a7ef6a583562f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-applications-to-compute-nodes-with-batch-application-packages"></a><span data-ttu-id="59809-103">使用 Batch 應用程式套件將應用程式部署至計算節點</span><span class="sxs-lookup"><span data-stu-id="59809-103">Deploy applications to compute nodes with Batch application packages</span></span>

<span data-ttu-id="59809-104">Azure Batch 的應用程式套件功能可讓您輕鬆管理工作應用程式並將其部署到集區中的計算節點。</span><span class="sxs-lookup"><span data-stu-id="59809-104">The application packages feature of Azure Batch provides easy management of task applications and their deployment to the compute nodes in your pool.</span></span> <span data-ttu-id="59809-105">透過應用程式套件，您可以上傳和管理工作所執行的多個應用程式版本，包括其支援檔案。</span><span class="sxs-lookup"><span data-stu-id="59809-105">With application packages, you can upload and manage multiple versions of the applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="59809-106">接著，您可以將一或多個這種類型的應用程式自動部署到集區中的計算節點。</span><span class="sxs-lookup"><span data-stu-id="59809-106">You can then automatically deploy one or more of these applications to the compute nodes in your pool.</span></span>

<span data-ttu-id="59809-107">在本文中，您將了解如何使用 Azure 入口網站上傳和管理應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-107">In this article, you will learn how to upload and manage application packages in the Azure portal.</span></span> <span data-ttu-id="59809-108">然後，您將了解如何使用 [Batch .NET][api_net] 程式庫將套件安裝在集區的計算節點上。</span><span class="sxs-lookup"><span data-stu-id="59809-108">You will then learn how to install them on a pool's compute nodes with the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="59809-109">在 2017 年 7 月 5 日之後建立的所有 Batch 集區都支援應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="59809-110">只有在使用雲端服務設定建立集區時，在 2016 年 3 月 10 日與 2017 年 7 月 5 日之間所建立的 Batch 集區上才支援應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="59809-111">在 2016 年 3 月 10 日之前建立的 Batch 集區不支援應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-111">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="59809-112">用來建立和管理應用程式套件的 API 屬於 [Batch Management .NET][[api_net_mgmt]] 程式庫的一部分。</span><span class="sxs-lookup"><span data-stu-id="59809-112">The APIs for creating and managing application packages are part of the [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="59809-113">用來在計算節點上安裝應用程式套件的 API 則屬於 [Batch .NET][api_net] 程式庫的一部分。</span><span class="sxs-lookup"><span data-stu-id="59809-113">The APIs for installing application packages on a compute node are part of the [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="59809-114">此處所述的應用程式套件功能取代了舊版服務中的「Batch Apps」功能。</span><span class="sxs-lookup"><span data-stu-id="59809-114">The application packages feature described here supersedes the Batch Apps feature available in previous versions of the service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="59809-115">應用程式封裝需求</span><span class="sxs-lookup"><span data-stu-id="59809-115">Application package requirements</span></span>
<span data-ttu-id="59809-116">若要使用應用程式套件，您必須[將 Azure 儲存體帳戶連結](#link-a-storage-account)到 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="59809-116">To use application packages, you need to [link an Azure Storage account](#link-a-storage-account) to your Batch account.</span></span>

<span data-ttu-id="59809-117">[Batch REST API][api_rest] 2015-12-01.2.2 版和對應的 [Batch .NET][api_net] 程式庫 3.1.0 版引進這項功能。</span><span class="sxs-lookup"><span data-stu-id="59809-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and the corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="59809-118">使用 Batch 時，我們建議您一律使用最新的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="59809-118">We recommend that you always use the latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="59809-119">在 2017 年 7 月 5 日之後建立的所有 Batch 集區都支援應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="59809-120">只有在使用雲端服務設定建立集區時，在 2016 年 3 月 10 日與 2017 年 7 月 5 日之間所建立的 Batch 集區上才支援應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="59809-121">在 2016 年 3 月 10 日之前建立的 Batch 集區不支援應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-121">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="59809-122">關於應用程式和應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="59809-122">About applications and application packages</span></span>
<span data-ttu-id="59809-123">在 Azure Batch 中，「應用程式」  是指一組已建立版本的二進位檔，這些檔案可自動下載到集區中的計算節點。</span><span class="sxs-lookup"><span data-stu-id="59809-123">Within Azure Batch, an *application* refers to a set of versioned binaries that can be automatically downloaded to the compute nodes in your pool.</span></span> <span data-ttu-id="59809-124">「應用程式套件」指的是這些二進位檔的「特定組合」，其代表應用程式的特定「版本」。</span><span class="sxs-lookup"><span data-stu-id="59809-124">An *application package* refers to a *specific set* of those binaries and represents a given *version* of the application.</span></span>

<span data-ttu-id="59809-125">![應用程式和應用程式套件的高階圖表][1]</span><span class="sxs-lookup"><span data-stu-id="59809-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="59809-126">應用程式</span><span class="sxs-lookup"><span data-stu-id="59809-126">Applications</span></span>
<span data-ttu-id="59809-127">Batch 中的應用程式包含一或多個應用程式封裝，並且會指定應用程式的組態選項。</span><span class="sxs-lookup"><span data-stu-id="59809-127">An application in Batch contains one or more application packages and specifies configuration options for the application.</span></span> <span data-ttu-id="59809-128">例如，應用程式可以指定要安裝在計算節點上的預設應用程式套件版本，以及應用程式的套件是否可以更新或刪除。</span><span class="sxs-lookup"><span data-stu-id="59809-128">For example, an application can specify the default application package version to install on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="59809-129">應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="59809-129">Application packages</span></span>
<span data-ttu-id="59809-130">應用程式套件為 .zip 檔案，其中包含工作執行應用程式所需的應用程式二進位檔和支援檔案。</span><span class="sxs-lookup"><span data-stu-id="59809-130">An application package is a .zip file that contains the application binaries and supporting files that are required for your tasks to run the application.</span></span> <span data-ttu-id="59809-131">每個應用程式封裝都代表特定版本的應用程式。</span><span class="sxs-lookup"><span data-stu-id="59809-131">Each application package represents a specific version of the application.</span></span>

<span data-ttu-id="59809-132">您可以在集區和工作層級指定應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-132">You can specify application packages at the pool and task levels.</span></span> <span data-ttu-id="59809-133">當您建立集區或工作時，您可以指定這些套件之中的一個或多個，以及 (選擇性) 指定版本。</span><span class="sxs-lookup"><span data-stu-id="59809-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="59809-134">**集區應用程式套件**會部署到集區中的「每個」節點。</span><span class="sxs-lookup"><span data-stu-id="59809-134">**Pool application packages** are deployed to *every* node in the pool.</span></span> <span data-ttu-id="59809-135">當節點加入集區以及重新啟動或重新安裝映像時，就會部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="59809-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="59809-136">當集區中的所有節點都執行某作業的工作時，便適合使用集區應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="59809-137">您可以在建立集區時指定一或多個應用程式套件，而且可以新增或更新現有集區的套件。</span><span class="sxs-lookup"><span data-stu-id="59809-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="59809-138">如果您更新現有集區的應用程式套件，您必須重新啟動它的節點，以安裝新的套件。</span><span class="sxs-lookup"><span data-stu-id="59809-138">If you update an existing pool's application packages, you must restart its nodes to install the new package.</span></span>
* <span data-ttu-id="59809-139">**工作應用程式套件** 只會部署到排程要執行工作的計算節點。</span><span class="sxs-lookup"><span data-stu-id="59809-139">**Task application packages** are deployed only to a compute node scheduled to run a task, just before running the task's command line.</span></span> <span data-ttu-id="59809-140">如果節點上已有指定的應用程式套件和版本，則不會重新部署，而會使用現有套件。</span><span class="sxs-lookup"><span data-stu-id="59809-140">If the specified application package and version is already on the node, it is not redeployed and the existing package is used.</span></span>
  
    <span data-ttu-id="59809-141">在共用集區的環境中，工作應用程式套件裝很有用：不同的作業會在一個集區上執行，而某項作業完成時並不會刪除該集區。</span><span class="sxs-lookup"><span data-stu-id="59809-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and the pool is not deleted when a job is completed.</span></span> <span data-ttu-id="59809-142">如果您的作業擁有的工作少於集區中的節點，工作應用程式套件可以減少資料傳輸，因為您的應用程式只會部署至執行工作的節點。</span><span class="sxs-lookup"><span data-stu-id="59809-142">If your job has fewer tasks than nodes in the pool, task application packages can minimize data transfer since your application is deployed only to the nodes that run tasks.</span></span>
  
    <span data-ttu-id="59809-143">其他可受益於工作應用程式套件的情節為執行大型應用程式，但只用於少數工作的作業。</span><span class="sxs-lookup"><span data-stu-id="59809-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="59809-144">例如，前置處理或合併應用程式非常龐大的前置處理階段或合併工作，將會受益於使用工作應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-144">For example, a pre-processing stage or a merge task, where the pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59809-145">Batch 帳戶中的應用程式和應用程式套件數目，以及應用程式套件的大小上限有其限制。</span><span class="sxs-lookup"><span data-stu-id="59809-145">There are restrictions on the number of applications and application packages within a Batch account and on the maximum application package size.</span></span> <span data-ttu-id="59809-146">如需這些限制的詳細資料，請參閱 [Azure Batch 服務的配額和限制](batch-quota-limit.md) 。</span><span class="sxs-lookup"><span data-stu-id="59809-146">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="59809-147">應用程式封裝的優點</span><span class="sxs-lookup"><span data-stu-id="59809-147">Benefits of application packages</span></span>
<span data-ttu-id="59809-148">應用程式套件可以簡化 Batch 解決方案中的程式碼，以及降低工作所執行之應用程式的必要管理成本。</span><span class="sxs-lookup"><span data-stu-id="59809-148">Application packages can simplify the code in your Batch solution and lower the overhead required to manage the applications that your tasks run.</span></span>

<span data-ttu-id="59809-149">使用應用程式套件，集區的啟動工作就不需要指定在節點上安裝一長串的個別資源檔案。</span><span class="sxs-lookup"><span data-stu-id="59809-149">With application packages, your pool's start task doesn't have to specify a long list of individual resource files to install on the nodes.</span></span> <span data-ttu-id="59809-150">您不需要在 Azure 儲存體中或在節點上手動管理應用程式檔案的多個版本。</span><span class="sxs-lookup"><span data-stu-id="59809-150">You don't have to manually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="59809-151">再者，您也不必費心產生 [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 來提供這些檔案在儲存體帳戶中的存取權限。</span><span class="sxs-lookup"><span data-stu-id="59809-151">And, you don't need to worry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to provide access to the files in your Storage account.</span></span> <span data-ttu-id="59809-152">Batch 會在背景中與 Azure 儲存體合作來儲存應用程式套件，並將其部署到計算節點。</span><span class="sxs-lookup"><span data-stu-id="59809-152">Batch works in the background with Azure Storage to store application packages and deploy them to compute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="59809-153">啟動工作的總大小必須小於或等於 32768 個字元，包括資源檔案和環境變數。</span><span class="sxs-lookup"><span data-stu-id="59809-153">The total size of a start task must be less than or equal to 32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="59809-154">如果啟動工作超過此限制，就可另外選擇使用應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="59809-155">您可以也建立包含資源檔的壓縮封存、將它作為 blob 上傳到 Azure 儲存體，然後從啟動工作的命令列將它解壓縮。</span><span class="sxs-lookup"><span data-stu-id="59809-155">You can also create a zipped archive containing your resource files, upload it as a blob to Azure Storage, and then unzip it from the command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="59809-156">上傳及管理應用程式</span><span class="sxs-lookup"><span data-stu-id="59809-156">Upload and manage applications</span></span>
<span data-ttu-id="59809-157">您可以使用 [Azure 入口網站][portal]或 [Batch 管理 .NET](batch-management-dotnet.md) 程式庫來管理 Batch 帳戶中的應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-157">You can use the [Azure portal][portal] or the [Batch Management .NET](batch-management-dotnet.md) library to manage the application packages in your Batch account.</span></span> <span data-ttu-id="59809-158">在接下來的幾節中，我們會先示範如何連結儲存體帳戶，接著討論如何使用入口網站來新增應用程式和套件以及管理它們。</span><span class="sxs-lookup"><span data-stu-id="59809-158">In the next few sections, we first show how to link a Storage account, then discuss adding applications and packages and managing them with the portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="59809-159">連結儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="59809-159">Link a Storage account</span></span>
<span data-ttu-id="59809-160">若要使用應用程式封裝，您必須先將 Azure 儲存體帳戶連結到 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="59809-160">To use application packages, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="59809-161">如果您尚未設定儲存體帳戶，Azure 入口網站會在您第一次按一下 [Batch 帳戶] 刀鋒視窗中的 [應用程式] 圖格時顯示警告。</span><span class="sxs-lookup"><span data-stu-id="59809-161">If you have not yet configured a Storage account, the Azure portal displays a warning the first time you click the **Applications** tile in the **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59809-162">Batch 目前「僅」支援**一般用途**的儲存體帳戶類型，如[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)中的步驟 5 [建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)所述。</span><span class="sxs-lookup"><span data-stu-id="59809-162">Batch currently supports *only* the **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="59809-163">當您將 Azure 儲存體帳戶連結至 Batch 帳戶時，請「僅」連結**一般用途**的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="59809-163">When you link an Azure Storage account to your Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="59809-164">![Azure 入口網站中的「未設定儲存體帳戶」警告][9]</span><span class="sxs-lookup"><span data-stu-id="59809-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="59809-165">Batch 服務會使用相關聯的儲存體帳戶來儲存應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-165">The Batch service uses the associated Storage account to store your application packages.</span></span> <span data-ttu-id="59809-166">在連結兩個帳戶之後，Batch 便能將儲存在連結之儲存體帳戶中的封裝自動部署到計算節點。</span><span class="sxs-lookup"><span data-stu-id="59809-166">After you've linked the two accounts, Batch can automatically deploy the packages stored in the linked Storage account to your compute nodes.</span></span> <span data-ttu-id="59809-167">若要將現有的儲存體帳戶連結至 Batch 帳戶，請按一下 [警告] 刀鋒視窗中的 [儲存體帳戶設定]，然後按一下 [儲存體帳戶] 刀鋒視窗上的 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="59809-167">To link a Storage account to your Batch account, click **Storage account settings** on the **Warning** blade, and then click **Storage Account** on the **Storage Account** blade.</span></span>

<span data-ttu-id="59809-168">![Azure 入口網站中的選擇儲存體帳戶刀鋒視窗][10]</span><span class="sxs-lookup"><span data-stu-id="59809-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="59809-169">我們建議您建立「專門」用來與 Batch 帳戶搭配使用的儲存體帳戶，並在此處選取它。</span><span class="sxs-lookup"><span data-stu-id="59809-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="59809-170">如需如何建立儲存體帳戶的詳細資訊，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)中的＜建立儲存體帳戶＞。</span><span class="sxs-lookup"><span data-stu-id="59809-170">For details about how to create a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="59809-171">在建立儲存體帳戶之後，您可以使用 [儲存體帳戶]  刀鋒視窗，將它連結到 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="59809-171">After you've created a Storage account, you can then link it to your Batch account by using the **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="59809-172">Batch 服務會使用 Azure 儲存體將應用程式套件儲存為區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="59809-172">The Batch service uses Azure Storage to store your application packages as block blobs.</span></span> <span data-ttu-id="59809-173">區塊 Blob 資料會[如往常收費][storage_pricing]。</span><span class="sxs-lookup"><span data-stu-id="59809-173">You are [charged as normal][storage_pricing] for the block blob data.</span></span> <span data-ttu-id="59809-174">請務必考量應用程式套件的大小和數目，並定期移除過時的套件以降低成本。</span><span class="sxs-lookup"><span data-stu-id="59809-174">Be sure to consider the size and number of your application packages, and periodically remove deprecated packages to minimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="59809-175">檢視目前的應用程式</span><span class="sxs-lookup"><span data-stu-id="59809-175">View current applications</span></span>
<span data-ttu-id="59809-176">若要檢視 Batch 帳戶中的應用程式，請在檢視 [Batch 帳戶] 刀鋒視窗時按一下左側功能表中的 [應用程式] 功能表項目。</span><span class="sxs-lookup"><span data-stu-id="59809-176">To view the applications in your Batch account, click the **Applications** menu item in the left menu while viewing the **Batch account** blade.</span></span>

<span data-ttu-id="59809-177">![應用程式圖格][2]</span><span class="sxs-lookup"><span data-stu-id="59809-177">![Applications tile][2]</span></span>

<span data-ttu-id="59809-178">選取此功能表選項會開啟 [應用程式] 刀鋒視窗：</span><span class="sxs-lookup"><span data-stu-id="59809-178">Selecting this menu option opens the **Applications** blade:</span></span>

<span data-ttu-id="59809-179">![列出應用程式][3]</span><span class="sxs-lookup"><span data-stu-id="59809-179">![List applications][3]</span></span>

<span data-ttu-id="59809-180">[應用程式]  刀鋒視窗會顯示帳戶中每個應用程式的識別碼，以及下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="59809-180">The **Applications** blade displays the ID of each application in your account and the following properties:</span></span>

* <span data-ttu-id="59809-181">**套件**：與此應用程式相關聯的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="59809-181">**Packages**: The number of versions associated with this application.</span></span>
* <span data-ttu-id="59809-182">**預設版本**：如果您在指定集區的應用程式時未指定版本，系統會安裝的應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="59809-182">**Default version**: The application version installed if you do not indicate a version when you specify the application for a pool.</span></span> <span data-ttu-id="59809-183">這項設定是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="59809-183">This setting is optional.</span></span>
* <span data-ttu-id="59809-184">**允許更新**：此值會指定是否允許更新、刪除和新增套件。</span><span class="sxs-lookup"><span data-stu-id="59809-184">**Allow updates**: The value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="59809-185">如果此值設為 [否]，應用程式會停用套件的更新和刪除，</span><span class="sxs-lookup"><span data-stu-id="59809-185">If this is set to **No**, package updates and deletions are disabled for the application.</span></span> <span data-ttu-id="59809-186">而只能新增新的應用程式封裝版本。</span><span class="sxs-lookup"><span data-stu-id="59809-186">Only new application package versions can be added.</span></span> <span data-ttu-id="59809-187">預設值為 [是]。</span><span class="sxs-lookup"><span data-stu-id="59809-187">The default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="59809-188">檢視應用程式詳細資料</span><span class="sxs-lookup"><span data-stu-id="59809-188">View application details</span></span>
<span data-ttu-id="59809-189">若要開啟包含應用程式詳細資料的刀鋒視窗，請在 [應用程式] 刀鋒視窗中選取應用程式。</span><span class="sxs-lookup"><span data-stu-id="59809-189">To open the blade that includes the details for an application, select the application in the **Applications** blade.</span></span>

<span data-ttu-id="59809-190">![應用程式詳細資料][4]</span><span class="sxs-lookup"><span data-stu-id="59809-190">![Application details][4]</span></span>

<span data-ttu-id="59809-191">在應用程式詳細資料刀鋒視窗中，您可以配置應用程式的以下設定。</span><span class="sxs-lookup"><span data-stu-id="59809-191">In the application details blade, you can configure the following settings for your application.</span></span>

* <span data-ttu-id="59809-192">**允許更新**：指定是否可更新或刪除應用程式的應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="59809-193">請參閱本文稍後的＜更新或刪除應用程式封裝＞。</span><span class="sxs-lookup"><span data-stu-id="59809-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="59809-194">**預設版本**：指定要部署至計算節點的預設應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-194">**Default version**: Specify a default application package to deploy to compute nodes.</span></span>
* <span data-ttu-id="59809-195">**顯示名稱**：指定 Batch 解決方案在顯示應用程式相關資訊時 (例如，在透過 Batch 提供給客戶之服務的 UI 中)，可以使用的「易記」名稱。</span><span class="sxs-lookup"><span data-stu-id="59809-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about the application, for example, in the UI of a service that you provide to your customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="59809-196">加入新的應用程式</span><span class="sxs-lookup"><span data-stu-id="59809-196">Add a new application</span></span>
<span data-ttu-id="59809-197">若要建立新應用程式，請新增應用程式封裝並指定新的唯一應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="59809-197">To create a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="59809-198">使用新應用程式識別碼新增的第一個應用程式套件也會建立新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="59809-198">The first application package that you add with the new application ID also creates the new application.</span></span>

<span data-ttu-id="59809-199">按一下 [應用程式] 刀鋒視窗中的 [新增]，以開啟 [新增應用程式] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="59809-199">Click **Add** on the **Applications** blade to open the **New application** blade.</span></span>

<span data-ttu-id="59809-200">![Azure 入口網站中的新增應用程式刀鋒視窗][5]</span><span class="sxs-lookup"><span data-stu-id="59809-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="59809-201">[新增應用程式]  刀鋒視窗提供以下欄位，供您指定新應用程式和應用程式套件的設定。</span><span class="sxs-lookup"><span data-stu-id="59809-201">The **New application** blade provides the following fields to specify the settings of your new application and application package.</span></span>

<span data-ttu-id="59809-202">**應用程式識別碼**</span><span class="sxs-lookup"><span data-stu-id="59809-202">**Application id**</span></span>

<span data-ttu-id="59809-203">此欄位能指定新應用程式的識別碼，其須符合標準 Azure Batch 識別碼驗證規則的規範。</span><span class="sxs-lookup"><span data-stu-id="59809-203">This field specifies the ID of your new application, which is subject to the standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="59809-204">提供應用程式識別碼的規則如下所示：</span><span class="sxs-lookup"><span data-stu-id="59809-204">The rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="59809-205">在 Windows 節點上，識別碼可包含英數字元、連字號及底線的任意組合。</span><span class="sxs-lookup"><span data-stu-id="59809-205">On Windows nodes, the ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="59809-206">在 Linux 節點上，只允許使用英數字元和底線。</span><span class="sxs-lookup"><span data-stu-id="59809-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="59809-207">不能包含超過 64 個字元。</span><span class="sxs-lookup"><span data-stu-id="59809-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="59809-208">在 Batch 帳戶內必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="59809-208">Must be unique within the Batch account.</span></span>
* <span data-ttu-id="59809-209">需保留大小寫和區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="59809-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="59809-210">**版本**</span><span class="sxs-lookup"><span data-stu-id="59809-210">**Version**</span></span>

<span data-ttu-id="59809-211">此欄位會指定要上傳的應用程式套件版本。</span><span class="sxs-lookup"><span data-stu-id="59809-211">This field specifies the version of the application package you are uploading.</span></span> <span data-ttu-id="59809-212">版本字串須符合以下驗證規則的規範︰</span><span class="sxs-lookup"><span data-stu-id="59809-212">Version strings are subject to the following validation rules:</span></span>

* <span data-ttu-id="59809-213">在 Windows 節點上，版本字串可包含英數字元、連字號、底線及句號的任意組合。</span><span class="sxs-lookup"><span data-stu-id="59809-213">On Windows nodes, the version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="59809-214">在 Linux 節點上，版本字串可以只包含英數字元和底線。</span><span class="sxs-lookup"><span data-stu-id="59809-214">On Linux nodes, the version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="59809-215">不能包含超過 64 個字元。</span><span class="sxs-lookup"><span data-stu-id="59809-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="59809-216">在應用程式內必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="59809-216">Must be unique within the application.</span></span>
* <span data-ttu-id="59809-217">需保留大小寫和區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="59809-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="59809-218">**應用程式封裝**</span><span class="sxs-lookup"><span data-stu-id="59809-218">**Application package**</span></span>

<span data-ttu-id="59809-219">此欄位指定包含應用程式執行所需之應用程式二進位檔和支援檔案的 .zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="59809-219">This field specifies the .zip file that contains the application binaries and supporting files that are required to execute the application.</span></span> <span data-ttu-id="59809-220">按一下 [選取檔案]  方塊或資料夾圖示，以瀏覽及選取包含應用程式檔案的 .zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="59809-220">Click the **Select a file** box or the folder icon to browse to and select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="59809-221">在選取檔案之後，請按一下 [確定]  以開始上傳到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="59809-221">After you've selected a file, click **OK** to begin the upload to Azure Storage.</span></span> <span data-ttu-id="59809-222">上傳作業完成時，入口網站會顯示通知，並關閉刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="59809-222">When the upload operation is complete, the portal displays a notification and closes the blade.</span></span> <span data-ttu-id="59809-223">因上傳之檔案的大小和網路連線速度不盡相同，這項作業可能需要花費一些時間。</span><span class="sxs-lookup"><span data-stu-id="59809-223">Depending on the size of the file that you are uploading and the speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="59809-224">上傳作業完成之前，請勿關閉 [新增應用程式] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="59809-224">Do not close the **New application** blade before the upload operation is complete.</span></span> <span data-ttu-id="59809-225">否則上傳程序將會停止。</span><span class="sxs-lookup"><span data-stu-id="59809-225">Doing so will stop the upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="59809-226">加入新應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="59809-226">Add a new application package</span></span>
<span data-ttu-id="59809-227">若要為現有的應用程式新增應用程式套件版本，請在 [應用程式] 刀鋒視窗中選取應用程式，然後依序按一下 [套件] 和 [新增] 以開啟 [新增套件] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="59809-227">To add a new application package version for an existing application, select an application in the **Applications** blade, click **Packages**, then click **Add** to open the **Add package** blade.</span></span>

<span data-ttu-id="59809-228">![Azure 入口網站中的新增應用程式套件刀鋒視窗][8]</span><span class="sxs-lookup"><span data-stu-id="59809-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="59809-229">如您所見，欄位與 [新增應用程式] 刀鋒視窗中的欄位相符，但 [應用程式識別碼] 方塊已停用。</span><span class="sxs-lookup"><span data-stu-id="59809-229">As you can see, the fields match those of the **New application** blade, but the **Application id** box is disabled.</span></span> <span data-ttu-id="59809-230">依照和新增應用程式相同的方式，指定新套件的 [版本]，瀏覽至您的**應用程式套件** .zip 檔案，然後按一下 [確定] 以上傳套件。</span><span class="sxs-lookup"><span data-stu-id="59809-230">As you did for the new application, specify the **Version** for your new package, browse to your **Application package** .zip file, then click **OK** to upload the package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="59809-231">更新或刪除應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="59809-231">Update or delete an application package</span></span>
<span data-ttu-id="59809-232">若要更新或刪除現有的應用程式套件，請開啟應用程式的詳細資料刀鋒視窗，按一下 [套件] 以開啟 [套件] 刀鋒視窗，按一下要修改之應用程式套件資料列中的**省略符號**，然後選取要執行的動作。</span><span class="sxs-lookup"><span data-stu-id="59809-232">To update or delete an existing application package, open the details blade for the application, click **Packages** to open the **Packages** blade, click the **ellipsis** in the row of the application package that you want to modify, and select the action that you want to perform.</span></span>

<span data-ttu-id="59809-233">![在 Azure 入口網站中更新或刪除套件][7]</span><span class="sxs-lookup"><span data-stu-id="59809-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="59809-234">更新</span><span class="sxs-lookup"><span data-stu-id="59809-234">**Update**</span></span>

<span data-ttu-id="59809-235">當您按一下 [更新] 時，[更新套件] 刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="59809-235">When you click **Update**, the *Update package* blade is displayed.</span></span> <span data-ttu-id="59809-236">此刀鋒視窗與 [新增應用程式套件]  刀鋒視窗相似，只不過已啟用套件選取欄位，因此您可以指定要上傳的新 ZIP 檔案。</span><span class="sxs-lookup"><span data-stu-id="59809-236">This blade is similar to the *New application package* blade, however only the package selection field is enabled, allowing you to specify a new ZIP file to upload.</span></span>

<span data-ttu-id="59809-237">![Azure 入口網站中的更新套件刀鋒視窗][11]</span><span class="sxs-lookup"><span data-stu-id="59809-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="59809-238">**刪除**</span><span class="sxs-lookup"><span data-stu-id="59809-238">**Delete**</span></span>

<span data-ttu-id="59809-239">當您按一下 [刪除] 時，系統會要求您確認要刪除套件版本，隨後 Batch 會從 Azure 儲存體中刪除該套件。</span><span class="sxs-lookup"><span data-stu-id="59809-239">When you click **Delete**, you are asked to confirm the deletion of the package version, and Batch deletes the package from Azure Storage.</span></span> <span data-ttu-id="59809-240">如果您刪除應用程式的預設版本，系統會移除應用程式的 [預設版本]  設定。</span><span class="sxs-lookup"><span data-stu-id="59809-240">If you delete the default version of an application, the **Default version** setting is removed for the application.</span></span>

<span data-ttu-id="59809-241">![刪除應用程式][12]</span><span class="sxs-lookup"><span data-stu-id="59809-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="59809-242">將應用程式安裝在計算節點上</span><span class="sxs-lookup"><span data-stu-id="59809-242">Install applications on compute nodes</span></span>
<span data-ttu-id="59809-243">您已了解如何使用 Azure 入口網站管理應用程式套件，接下來我們可以討論如何使用 Batch 工作，將它們部署到計算節點並加以執行。</span><span class="sxs-lookup"><span data-stu-id="59809-243">Now that you've learned how to manage application packages with the Azure portal, we can discuss how to deploy them to compute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="59809-244">安裝集區應用程式套件</span><span class="sxs-lookup"><span data-stu-id="59809-244">Install pool application packages</span></span>
<span data-ttu-id="59809-245">若要將應用程式套件安裝在集區中的所有計算節點上，請為集區指定一或多個應用程式套件「參考」  。</span><span class="sxs-lookup"><span data-stu-id="59809-245">To install an application package on all compute nodes in a pool, specify one or more application package *references* for the pool.</span></span> <span data-ttu-id="59809-246">您針對集區指定的應用程式封裝會在每個電腦節點加入集區時，以及該節點重新啟動或重新安裝映像時，安裝於該節點上。</span><span class="sxs-lookup"><span data-stu-id="59809-246">The application packages that you specify for a pool are installed on each compute node when that node joins the pool, and when the node is rebooted or reimaged.</span></span>

<span data-ttu-id="59809-247">在 Batch .NET 中，請在建立新集區時指定一或多個 [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref]，或為現有集區指定。</span><span class="sxs-lookup"><span data-stu-id="59809-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="59809-248">[ApplicationPackageReference][net_pkgref] 類別能指定要安裝在集區之計算節點上的應用程式識別碼和版本。</span><span class="sxs-lookup"><span data-stu-id="59809-248">The [ApplicationPackageReference][net_pkgref] class specifies an application ID and version to install on a pool's compute nodes.</span></span>

```csharp
// Create the unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify the application and version to install on the compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit the pool so that it's created in the Batch service. As the nodes join
// the pool, the specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="59809-249">如果應用程式套件部署基於任何因素而失敗，Batch 服務會將節點標示為[無法使用][net_nodestate]，而且不會在該節點上排程任何要執行的工作。</span><span class="sxs-lookup"><span data-stu-id="59809-249">If an application package deployment fails for any reason, the Batch service marks the node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="59809-250">在此情況下，您應該 **重新啟動** 節點以重新初始化套件部署。</span><span class="sxs-lookup"><span data-stu-id="59809-250">In this case, you should **restart** the node to reinitiate the package deployment.</span></span> <span data-ttu-id="59809-251">重新啟動節點也會在節點上再次啟用工作排程。</span><span class="sxs-lookup"><span data-stu-id="59809-251">Restarting the node also enables task scheduling again on the node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="59809-252">安裝工作應用程式套件</span><span class="sxs-lookup"><span data-stu-id="59809-252">Install task application packages</span></span>
<span data-ttu-id="59809-253">類似於集區，您可以為工作指定應用程式套件「參考」  。</span><span class="sxs-lookup"><span data-stu-id="59809-253">Similar to a pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="59809-254">在節點上排程要執行的工作時，會先下載並解壓縮套件，再執行工作的命令列。</span><span class="sxs-lookup"><span data-stu-id="59809-254">When a task is scheduled to run on a node, the package is downloaded and extracted just before the task's command line is executed.</span></span> <span data-ttu-id="59809-255">如果節點上已安裝指定的套件和版本，則不會下載套件，而會使用現有套件裝。</span><span class="sxs-lookup"><span data-stu-id="59809-255">If a specified package and version is already installed on the node, the package is not downloaded and the existing package is used.</span></span>

<span data-ttu-id="59809-256">若要安裝工作應用程式套件，請設定工作的 [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] 屬性︰</span><span class="sxs-lookup"><span data-stu-id="59809-256">To install a task application package, configure the task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

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

## <a name="execute-the-installed-applications"></a><span data-ttu-id="59809-257">執行安裝的應用程式</span><span class="sxs-lookup"><span data-stu-id="59809-257">Execute the installed applications</span></span>
<span data-ttu-id="59809-258">您為集區或工作所指定的套件會下載並解壓縮至節點的 `AZ_BATCH_ROOT_DIR` 中的具名目錄。</span><span class="sxs-lookup"><span data-stu-id="59809-258">The packages that you've specified for a pool or task are downloaded and extracted to a named directory within the `AZ_BATCH_ROOT_DIR` of the node.</span></span> <span data-ttu-id="59809-259">Batch 也會建立包含具名目錄路徑的環境變數。</span><span class="sxs-lookup"><span data-stu-id="59809-259">Batch also creates an environment variable that contains the path to the named directory.</span></span> <span data-ttu-id="59809-260">在參考節點上的應用程式時，工作的命令列會使用這個環境變數。</span><span class="sxs-lookup"><span data-stu-id="59809-260">Your task command lines use this environment variable when referencing the application on the node.</span></span> 

<span data-ttu-id="59809-261">在 Windows 節點上，變數格式如下：</span><span class="sxs-lookup"><span data-stu-id="59809-261">On Windows nodes, the variable is in the following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="59809-262">在 Linux 節點上，格式稍有不同。</span><span class="sxs-lookup"><span data-stu-id="59809-262">On Linux nodes, the format is slightly different.</span></span> <span data-ttu-id="59809-263">句號 (.)、連字號 (-) 和數字記號 (#) 已壓平合併為環境變數中的底線。</span><span class="sxs-lookup"><span data-stu-id="59809-263">Periods (.), hypens (-) and number signs (#) are flattened to underscores in the environment variable.</span></span> <span data-ttu-id="59809-264">例如：</span><span class="sxs-lookup"><span data-stu-id="59809-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="59809-265">`APPLICATIONID` 和 `version` 是對應於為部署所指定的應用程式和套件版本的值。</span><span class="sxs-lookup"><span data-stu-id="59809-265">`APPLICATIONID` and `version` are values that correspond to the application and package version you've specified for deployment.</span></span> <span data-ttu-id="59809-266">例如，如果您指定應該在 Windows 節點上安裝 2.7 版的「Blender」應用程式，您的工作命令列就會使用此環境變數來存取其檔案︰</span><span class="sxs-lookup"><span data-stu-id="59809-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable to access its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="59809-267">在 Linux 節點上，將環境變數指定為此格式：</span><span class="sxs-lookup"><span data-stu-id="59809-267">On Linux nodes, specify the environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="59809-268">當您上傳應用程式套件時，您可以指定要部署至運算節點的預設版本。</span><span class="sxs-lookup"><span data-stu-id="59809-268">When you upload an application package, you can specify a default version to deploy to your compute nodes.</span></span> <span data-ttu-id="59809-269">如果您已經指定應用程式的預設版本，當您參考應用程式時就可以省略版本尾碼。</span><span class="sxs-lookup"><span data-stu-id="59809-269">If you have specified a default version for an application, you can omit the version suffix when you reference the application.</span></span> <span data-ttu-id="59809-270">您可以在 Azure 入口網站中的 [應用程式] 刀鋒視窗上指定預設應用程式版本，如[上傳及管理應用程式](#upload-and-manage-applications)中所示。</span><span class="sxs-lookup"><span data-stu-id="59809-270">You can specify the default application version in the Azure portal, on the Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="59809-271">例如，如果您設定「2.7」作為「Blender」應用程式的預設版本，且您的工作是參考下列環境變數，您的 Windows 節點就會執行 2.7 版：</span><span class="sxs-lookup"><span data-stu-id="59809-271">For example, if you set "2.7" as the default version for application *blender*, and your tasks reference the following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="59809-272">下列程式碼片段會顯示工作命令列範例，其可啟動「Blender」  應用程式的預設版本︰</span><span class="sxs-lookup"><span data-stu-id="59809-272">The following code snippet shows an example task command line that launches the default version of the *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="59809-273">如需計算節點環境設定的詳細資訊，請參閱 [Batch 功能概觀](batch-api-basics.md)中的[工作的環境設定](batch-api-basics.md#environment-settings-for-tasks)。</span><span class="sxs-lookup"><span data-stu-id="59809-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in the [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="59809-274">更新集區的應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="59809-274">Update a pool's application packages</span></span>
<span data-ttu-id="59809-275">如果您已設定現有集區的應用程式封裝，可以指定集區的新封裝。</span><span class="sxs-lookup"><span data-stu-id="59809-275">If an existing pool has already been configured with an application package, you can specify a new package for the pool.</span></span> <span data-ttu-id="59809-276">如果您為集區指定新的封裝參考，則會適用下列情況：</span><span class="sxs-lookup"><span data-stu-id="59809-276">If you specify a new package reference for a pool, the following apply:</span></span>

* <span data-ttu-id="59809-277">Batch 服務會在加入新增集區的所有新節點，以及任何重新啟動或重新安裝映像的現有節點上安裝新指定的套件。</span><span class="sxs-lookup"><span data-stu-id="59809-277">The Batch service installs the newly specified package on all new nodes that join the pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="59809-278">在更新封裝參考時已存在集區中的計算節點不會自動安裝新應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="59809-278">Compute nodes that are already in the pool when you update the package references do not automatically install the new application package.</span></span> <span data-ttu-id="59809-279">這些計算節點必須重新啟動或重新安裝映像才能接收新封裝。</span><span class="sxs-lookup"><span data-stu-id="59809-279">These compute nodes must be rebooted or reimaged to receive the new package.</span></span>
* <span data-ttu-id="59809-280">部署新的封裝之後，所建立的環境變數會反映新的應用程式封裝參考。</span><span class="sxs-lookup"><span data-stu-id="59809-280">When a new package is deployed, the created environment variables reflect the new application package references.</span></span>

<span data-ttu-id="59809-281">在此範例中，現有集區已將 Blender 應用程式的 2.7 版設定為其中一個 [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref]。</span><span class="sxs-lookup"><span data-stu-id="59809-281">In this example, the existing pool has version 2.7 of the *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="59809-282">若要將集區的節點更新為 2.76b 版，請將 [ApplicationPackageReference][net_pkgref] 指定為新版本並認可變更。</span><span class="sxs-lookup"><span data-stu-id="59809-282">To update the pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with the new version, and commit the change.</span></span>

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

<span data-ttu-id="59809-283">既然您已設定新版本，Batch 服務就會將 2.76b 版安裝到任何加入集區的「新」節點。</span><span class="sxs-lookup"><span data-stu-id="59809-283">Now that the new version has been configured, the Batch service installs version 2.76b to any *new* node that joins the pool.</span></span> <span data-ttu-id="59809-284">若要將 2.76b 安裝在「已存在」  集區中的節點上，請將節點重新啟動或重新安裝映像。</span><span class="sxs-lookup"><span data-stu-id="59809-284">To install 2.76b on the nodes that are *already* in the pool, reboot or reimage them.</span></span> <span data-ttu-id="59809-285">請注意，重新啟動的節點會保留前次套件部署的檔案。</span><span class="sxs-lookup"><span data-stu-id="59809-285">Note that rebooted nodes retain the files from previous package deployments.</span></span>

## <a name="list-the-applications-in-a-batch-account"></a><span data-ttu-id="59809-286">列出 Batch 帳戶中的應用程式</span><span class="sxs-lookup"><span data-stu-id="59809-286">List the applications in a Batch account</span></span>
<span data-ttu-id="59809-287">您可以使用 [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] 方法列出 Batch 帳戶中的應用程式和應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="59809-287">You can list the applications and their packages in a Batch account by using the [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List the applications and their application packages in the Batch account.
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

## <a name="wrap-up"></a><span data-ttu-id="59809-288">總結</span><span class="sxs-lookup"><span data-stu-id="59809-288">Wrap up</span></span>
<span data-ttu-id="59809-289">透過應用程式封裝，您可以協助客戶選取其作業適用的應用程式，以及指定在以啟用 Batch 功能的服務處理作業時所要使用的確切版本。</span><span class="sxs-lookup"><span data-stu-id="59809-289">With application packages, you can help your customers select the applications for their jobs and specify the exact version to use when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="59809-290">您也可以在服務中提供讓客戶上傳及追蹤其應用程式的功能。</span><span class="sxs-lookup"><span data-stu-id="59809-290">You might also provide the ability for your customers to upload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59809-291">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59809-291">Next steps</span></span>
* <span data-ttu-id="59809-292">[Batch REST API][api_rest] 也提供應用程式套件的使用支援。</span><span class="sxs-lookup"><span data-stu-id="59809-292">The [Batch REST API][api_rest] also provides support to work with application packages.</span></span> <span data-ttu-id="59809-293">例如，請參閱[將集區新增至帳戶][rest_add_pool]中的 [applicationPackageReferences][rest_add_pool_with_packages] 項目，以取得如何使用 REST API 來指定要安裝之套件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="59809-293">For example, see the [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool to an account][rest_add_pool] for information about how to specify packages to install by using the REST API.</span></span> <span data-ttu-id="59809-294">如需如何使用 Batch REST API 來取得應用程式資訊的詳細資料，請參閱[應用程式][rest_applications]。</span><span class="sxs-lookup"><span data-stu-id="59809-294">See [Applications][rest_applications] for details about how to obtain application information by using the Batch REST API.</span></span>
* <span data-ttu-id="59809-295">了解如何以程式設計方式 [使用 Batch Management .NET 管理 Azure Batch 帳戶和配額](batch-management-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="59809-295">Learn how to programmatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="59809-296">[Batch Management .NET][api_net_mgmt] 程式庫可以啟用 Batch 應用程式或服務的帳戶建立和刪除功能。</span><span class="sxs-lookup"><span data-stu-id="59809-296">The [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

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
