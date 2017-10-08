---
title: "建置 Visual Studio 專案範本 Azure 批次方案 aaaStart |Microsoft 文件"
description: "了解 Visual Studio 專案範本如何協助您在 Azure Batch 中實作和執行計算密集型工作負載。"
services: batch
documentationcenter: .net
author: fayora
manager: timlt
editor: 
ms.assetid: 5e041ae2-25af-4882-a79e-3aa63c4bfb20
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a61c480ddc4dffd66c01220a137a3e852e39c338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-project-templates-toojump-start-batch-solutions"></a><span data-ttu-id="d1241-103">使用 Visual Studio 專案範本 toojump 啟動批次方案</span><span class="sxs-lookup"><span data-stu-id="d1241-103">Use Visual Studio project templates toojump-start Batch solutions</span></span>

<span data-ttu-id="d1241-104">hello**作業管理員**和**工作處理器 Visual Studio 範本**批次提供的程式碼 toohelp 您 tooimplement 及執行運算密集的工作負載，以批次上至少 hello 的投入時間量。</span><span class="sxs-lookup"><span data-stu-id="d1241-104">hello **Job Manager** and **Task Processor Visual Studio templates** for Batch provide code toohelp you tooimplement and run your compute-intensive workloads on Batch with hello least amount of effort.</span></span> <span data-ttu-id="d1241-105">本文件說明這些範本，並提供的指導 toouse 它們。</span><span class="sxs-lookup"><span data-stu-id="d1241-105">This document describes these templates and provides guidance for how toouse them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1241-106">這篇文章討論唯一資訊適用 toothese 兩個範本，並假設您熟悉 hello 批次服務和主要概念相關的 tooit： 集區，計算節點、 工作和工作、 作業管理員工作、 環境變數和其他相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="d1241-106">This article discusses only information applicable toothese two templates, and assumes that you are familiar with hello Batch service and key concepts related tooit: pools, compute nodes, jobs and tasks, job manager tasks, environment variables, and other relevant information.</span></span> <span data-ttu-id="d1241-107">您可以找到更多資訊[Azure Batch 基本概念](batch-technical-overview.md)，[批次功能概觀，讓開發人員](batch-api-basics.md)，和[開始使用 hello Azure Batch library for.NET](batch-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="d1241-107">You can find more information in [Basics of Azure Batch](batch-technical-overview.md), [Batch feature overview for developers](batch-api-basics.md), and [Get started with hello Azure Batch library for .NET](batch-dotnet-get-started.md).</span></span>
> 
> 

## <a name="high-level-overview"></a><span data-ttu-id="d1241-108">高階概述</span><span class="sxs-lookup"><span data-stu-id="d1241-108">High-level overview</span></span>
<span data-ttu-id="d1241-109">hello 工作管理員] 和 [工作處理器範本可以是使用的 toocreate 兩個有用元件：</span><span class="sxs-lookup"><span data-stu-id="d1241-109">hello Job Manager and Task Processor templates can be used toocreate two useful components:</span></span>

* <span data-ttu-id="d1241-110">作業管理員工作，此工作會實作作業分割器，後者可將作業細分為多個可以平行且獨立執行的工作。</span><span class="sxs-lookup"><span data-stu-id="d1241-110">A job manager task that implements a job splitter that can break a job down into multiple tasks that can run independently, in parallel.</span></span>
* <span data-ttu-id="d1241-111">可以使用的 tooperform 前置處理和應用程式的命令列周圍的後續處理工作處理器。</span><span class="sxs-lookup"><span data-stu-id="d1241-111">A task processor that can be used tooperform pre-processing and post-processing around an application command line.</span></span>

<span data-ttu-id="d1241-112">比方說，在影片轉譯案例中，hello 作業分隔器會變成單一的電影作業數百或數千個不同的工作會分開處理個別畫面格。</span><span class="sxs-lookup"><span data-stu-id="d1241-112">For example, in a movie rendering scenario, hello job splitter would turn a single movie job into hundreds or thousands of separate tasks that would process individual frames separately.</span></span> <span data-ttu-id="d1241-113">相對的 hello 工作處理器會叫用 hello 呈現應用程式和所有相依的程序所需的 toorender 每個畫面格，以及執行任何額外的動作 （例如，複製 hello 轉譯畫面格 tooa 儲存位置）。</span><span class="sxs-lookup"><span data-stu-id="d1241-113">Correspondingly, hello task processor would invoke hello rendering application and all dependent processes that are needed toorender each frame, as well as perform any additional actions (for example, copying hello rendered frame tooa storage location).</span></span>

> [!NOTE]
> <span data-ttu-id="d1241-114">hello 工作管理員] 和 [工作處理器範本無關，因此兩者，或只有一個項目，視您計算的工作並在您的喜好設定的 hello 需求而定，您可以選擇 toouse。</span><span class="sxs-lookup"><span data-stu-id="d1241-114">hello Job Manager and Task Processor templates are independent of each other, so you can choose toouse both, or only one of them, depending on hello requirements of your compute job and on your preferences.</span></span>
> 
> 

<span data-ttu-id="d1241-115">Hello 如下圖所示，計算作業會使用這些範本會經歷三個階段：</span><span class="sxs-lookup"><span data-stu-id="d1241-115">As shown in hello diagram below, a compute job that uses these templates will go through three stages:</span></span>

1. <span data-ttu-id="d1241-116">hello 用戶端程式碼 （例如，應用程式、 web 服務等） 會提交作業 toohello 批次服務在 Azure 上，指定為其作業管理員工作 hello 工作管理員程式。</span><span class="sxs-lookup"><span data-stu-id="d1241-116">hello client code (e.g., application, web service, etc.) submits a job toohello Batch service on Azure, specifying as its job manager task hello job manager program.</span></span>
2. <span data-ttu-id="d1241-117">hello 批次服務在計算節點上執行 hello 作業管理員工作和 hello 作業分隔器會啟動 hello 工作處理器工作數目，在上指定做為許多計算節點做為必要項目，根據 hello 參數和 hello 作業分隔器程式碼中的規格。</span><span class="sxs-lookup"><span data-stu-id="d1241-117">hello Batch service runs hello job manager task on a compute node and hello job splitter launches hello specified number of task processor tasks, on as many compute nodes as required, based on hello parameters and specifications in hello job splitter code.</span></span>
3. <span data-ttu-id="d1241-118">hello 工作處理器工作獨立作業，以平行方式執行，tooprocess hello 輸入的資料，並產生 hello 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="d1241-118">hello task processor tasks run independently, in parallel, tooprocess hello input data and generate hello output data.</span></span>

![顯示以 hello 批次服務用戶端程式碼的互動方式的圖表][diagram01]

## <a name="prerequisites"></a><span data-ttu-id="d1241-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="d1241-120">Prerequisites</span></span>
<span data-ttu-id="d1241-121">toouse hello 批次的範本，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="d1241-121">toouse hello Batch templates, you will need hello following:</span></span>

* <span data-ttu-id="d1241-122">已安裝 Visual Studio 2015 的電腦。</span><span class="sxs-lookup"><span data-stu-id="d1241-122">A computer with Visual Studio 2015 installed.</span></span> <span data-ttu-id="d1241-123">目前只有針對 Visual Studio 2015 支援批次範本。</span><span class="sxs-lookup"><span data-stu-id="d1241-123">Batch templates are currently only supported for Visual Studio 2015.</span></span>
* <span data-ttu-id="d1241-124">hello 批次範本都是從 hello [Visual Studio 組件庫][ vs_gallery]做為 Visual Studio 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="d1241-124">hello Batch templates, which are available from hello [Visual Studio Gallery][vs_gallery] as Visual Studio extensions.</span></span> <span data-ttu-id="d1241-125">有兩種方式 tooget hello 範本：</span><span class="sxs-lookup"><span data-stu-id="d1241-125">There are two ways tooget hello templates:</span></span>
  
  * <span data-ttu-id="d1241-126">安裝使用 hello hello 範本**擴充功能和更新**Visual Studio 中的對話方塊 (如需詳細資訊，請參閱[尋找及使用 Visual Studio 擴充功能][vs_find_use_ext])。</span><span class="sxs-lookup"><span data-stu-id="d1241-126">Install hello templates using hello **Extensions and Updates** dialog box in Visual Studio (for more information, see [Finding and Using Visual Studio Extensions][vs_find_use_ext]).</span></span> <span data-ttu-id="d1241-127">在 hello**擴充功能和更新**對話方塊中，下列兩個延伸模組的搜尋和下載 hello:</span><span class="sxs-lookup"><span data-stu-id="d1241-127">In hello **Extensions and Updates** dialog box, search and download hello following two extensions:</span></span>
    
    * <span data-ttu-id="d1241-128">具有作業分割器的 Azure Batch 作業管理員</span><span class="sxs-lookup"><span data-stu-id="d1241-128">Azure Batch Job Manager with Job Splitter</span></span>
    * <span data-ttu-id="d1241-129">Azure Batch 工作處理器</span><span class="sxs-lookup"><span data-stu-id="d1241-129">Azure Batch Task Processor</span></span>
  * <span data-ttu-id="d1241-130">從 hello 線上組件庫下載 hello 範本，適用於 Visual Studio: [Microsoft Azure 批次的專案範本][vs_gallery_templates]</span><span class="sxs-lookup"><span data-stu-id="d1241-130">Download hello templates from hello online gallery for Visual Studio: [Microsoft Azure Batch Project Templates][vs_gallery_templates]</span></span>
* <span data-ttu-id="d1241-131">如果您計劃 toouse hello[應用程式封裝](batch-application-packages.md)功能 toodeploy hello 工作管理員和工作處理器 toohello 批次計算節點，您必須 toolink 儲存體帳戶 tooyour Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d1241-131">If you plan toouse hello [Application Packages](batch-application-packages.md) feature toodeploy hello job manager and task processor toohello Batch compute nodes, you need toolink a storage account tooyour Batch account.</span></span>

## <a name="preparation"></a><span data-ttu-id="d1241-132">準備工作</span><span class="sxs-lookup"><span data-stu-id="d1241-132">Preparation</span></span>
<span data-ttu-id="d1241-133">我們建議您建立工作管理員，以及您工作的處理器，可包含的方案，因為這樣可以使它與您的作業管理員工作處理器程式更容易 tooshare 程式碼。</span><span class="sxs-lookup"><span data-stu-id="d1241-133">We recommend creating a solution that can contain your job manager as well as your task processor, because this can make it easier tooshare code between your job manager and task processor programs.</span></span> <span data-ttu-id="d1241-134">toocreate 此解決方案，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d1241-134">toocreate this solution, follow these steps:</span></span>

1. <span data-ttu-id="d1241-135">開啟 Visual Studio，然後選取 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="d1241-135">Open Visual Studio and select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="d1241-136">在 [範本] 底下展開 [其他專案類型]、按一下 [Visual Studio 方案]，然後選取 [空白方案]。</span><span class="sxs-lookup"><span data-stu-id="d1241-136">Under **Templates**, expand **Other Project Types**, click **Visual Studio Solutions**, and then select **Blank Solution**.</span></span>
3. <span data-ttu-id="d1241-137">輸入描述您應用程式和 hello 的用途，此解決方案 (例如，"LitwareBatchTaskPrograms") 的名稱。</span><span class="sxs-lookup"><span data-stu-id="d1241-137">Type a name that describes your application and hello purpose of this solution (e.g., "LitwareBatchTaskPrograms").</span></span>
4. <span data-ttu-id="d1241-138">toocreate hello 新方案時，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="d1241-138">toocreate hello new solution, click **OK**.</span></span>

## <a name="job-manager-template"></a><span data-ttu-id="d1241-139">作業管理員範本</span><span class="sxs-lookup"><span data-stu-id="d1241-139">Job Manager template</span></span>
<span data-ttu-id="d1241-140">hello 作業管理員範本可協助您 tooimplement 可以執行下列動作的 hello 作業管理員工作：</span><span class="sxs-lookup"><span data-stu-id="d1241-140">hello Job Manager template helps you tooimplement a job manager task that can perform hello following actions:</span></span>

* <span data-ttu-id="d1241-141">將作業分割成多個工作。</span><span class="sxs-lookup"><span data-stu-id="d1241-141">Split a job into multiple tasks.</span></span>
* <span data-ttu-id="d1241-142">提交這些批次的工作 toorun。</span><span class="sxs-lookup"><span data-stu-id="d1241-142">Submit those tasks toorun on Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="d1241-143">如需作業管理員工作的詳細資訊，請參閱 [適用於開發人員的 Batch 功能概觀](batch-api-basics.md#job-manager-task)。</span><span class="sxs-lookup"><span data-stu-id="d1241-143">For more information about job manager tasks, see [Batch feature overview for developers](batch-api-basics.md#job-manager-task).</span></span>
> 
> 

### <a name="create-a-job-manager-using-hello-template"></a><span data-ttu-id="d1241-144">建立作業管理員使用 hello 範本</span><span class="sxs-lookup"><span data-stu-id="d1241-144">Create a Job Manager using hello template</span></span>
<span data-ttu-id="d1241-145">tooadd 作業管理員 toohello 建立的方案，您更早版本，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d1241-145">tooadd a job manager toohello solution that you created earlier, follow these steps:</span></span>

1. <span data-ttu-id="d1241-146">在 Visual Studio 中開啟現有方案。</span><span class="sxs-lookup"><span data-stu-id="d1241-146">Open your existing solution in Visual Studio.</span></span>
2. <span data-ttu-id="d1241-147">在 方案總管 中，以滑鼠右鍵按一下 hello 方案中，按一下 **新增** > **新專案**。</span><span class="sxs-lookup"><span data-stu-id="d1241-147">In Solution Explorer, right-click hello solution, click **Add** > **New Project**.</span></span>
3. <span data-ttu-id="d1241-148">在 Visual C# 底下按一下 雲端，然後按一下具有作業分割器的 Azure Batch 作業管理員。</span><span class="sxs-lookup"><span data-stu-id="d1241-148">Under **Visual C#**, click **Cloud**, and then click **Azure Batch Job Manager with Job Splitter**.</span></span>
4. <span data-ttu-id="d1241-149">輸入描述您的應用程式，且 （例如識別為 hello 作業管理員的這個專案的名稱"LitwareJobManager")。</span><span class="sxs-lookup"><span data-stu-id="d1241-149">Type a name that describes your application and identifies this project as hello job manager (e.g. "LitwareJobManager").</span></span>
5. <span data-ttu-id="d1241-150">toocreate hello 專案中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="d1241-150">toocreate hello project, click **OK**.</span></span>
6. <span data-ttu-id="d1241-151">最後，建置 hello 專案 tooforce Visual Studio tooload 所有參考的 NuGet 封裝，並 hello 專案的 tooverify 有效，然後再開始進行修改。</span><span class="sxs-lookup"><span data-stu-id="d1241-151">Finally, build hello project tooforce Visual Studio tooload all referenced NuGet packages and tooverify that hello project is valid before you start modifying it.</span></span>

### <a name="job-manager-template-files-and-their-purpose"></a><span data-ttu-id="d1241-152">作業管理員範本檔案及其用途</span><span class="sxs-lookup"><span data-stu-id="d1241-152">Job Manager template files and their purpose</span></span>
<span data-ttu-id="d1241-153">當您使用範本建立專案 hello 工作管理員時，它會產生三個群組的程式碼檔案：</span><span class="sxs-lookup"><span data-stu-id="d1241-153">When you create a project using hello Job Manager template, it generates three groups of code files:</span></span>

* <span data-ttu-id="d1241-154">hello 主要程式檔案 (Program.cs)。</span><span class="sxs-lookup"><span data-stu-id="d1241-154">hello main program file (Program.cs).</span></span> <span data-ttu-id="d1241-155">這包含 hello 程式進入點和最上層的例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="d1241-155">This contains hello program entry point and top-level exception handling.</span></span> <span data-ttu-id="d1241-156">您通常不應該這樣需要 toomodify。</span><span class="sxs-lookup"><span data-stu-id="d1241-156">You shouldn't normally need toomodify this.</span></span>
* <span data-ttu-id="d1241-157">hello Framework 目錄。</span><span class="sxs-lookup"><span data-stu-id="d1241-157">hello Framework directory.</span></span> <span data-ttu-id="d1241-158">這包含 hello 檔案負責 hello 工作管理員程式-解除封裝參數，加入等工作 toohello 批次作業所完成的 hello '未定案' 工作。您通常應該不需要 toomodify 這些檔案。</span><span class="sxs-lookup"><span data-stu-id="d1241-158">This contains hello files responsible for hello 'boilerplate' work done by hello job manager program – unpacking parameters, adding tasks toohello Batch job, etc. You shouldn't normally need toomodify these files.</span></span>
* <span data-ttu-id="d1241-159">hello 作業分隔檔 (JobSplitter.cs)。</span><span class="sxs-lookup"><span data-stu-id="d1241-159">hello job splitter file (JobSplitter.cs).</span></span> <span data-ttu-id="d1241-160">此處可供存放用於將作業分割成多個工作的應用程式特定邏輯。</span><span class="sxs-lookup"><span data-stu-id="d1241-160">This is where you will put your application-specific logic for splitting a job into tasks.</span></span>

<span data-ttu-id="d1241-161">當然您可以加入其他檔案，需要 toosupport 做您工作分隔器的程式碼，視分割邏輯 hello 作業 hello 複雜度而定。</span><span class="sxs-lookup"><span data-stu-id="d1241-161">Of course you can add additional files as required toosupport your job splitter code, depending on hello complexity of hello job splitting logic.</span></span>

<span data-ttu-id="d1241-162">hello 範本也會產生標準的.NET 專案檔，例如.csproj 檔案、 app.config、 packages.config 等等。</span><span class="sxs-lookup"><span data-stu-id="d1241-162">hello template also generates standard .NET project files such as a .csproj file, app.config, packages.config, etc.</span></span>

<span data-ttu-id="d1241-163">hello 本節其餘部分描述 hello 不同的檔案和程式碼結構，並說明每個類別的用途。</span><span class="sxs-lookup"><span data-stu-id="d1241-163">hello rest of this section describes hello different files and their code structure, and explains what each class does.</span></span>

![Visual Studio 方案總管中顯示 hello 作業管理員範本解決方案][solution_explorer01]

<span data-ttu-id="d1241-165">**架構檔案**</span><span class="sxs-lookup"><span data-stu-id="d1241-165">**Framework files**</span></span>

* <span data-ttu-id="d1241-166">`Configuration.cs`： 封裝 hello 載入的工作組態資料，例如批次帳戶詳細資料、 連結的儲存體帳戶認證、 作業和工作資訊和作業參數。</span><span class="sxs-lookup"><span data-stu-id="d1241-166">`Configuration.cs`: Encapsulates hello loading of job configuration data such as Batch account details, linked storage account credentials, job and task information, and job parameters.</span></span> <span data-ttu-id="d1241-167">它也提供存取 tooBatch 定義環境變數 （請參閱 hello 批次的文件中的工作環境設定） 透過 hello Configuration.EnvironmentVariable 類別。</span><span class="sxs-lookup"><span data-stu-id="d1241-167">It also provides access tooBatch-defined environment variables (see Environment settings for tasks, in hello Batch documentation) via hello Configuration.EnvironmentVariable class.</span></span>
* <span data-ttu-id="d1241-168">`IConfiguration.cs`： 摘要 hello hello 設定類別的實作，單元，讓您可以測試您的工作分隔器使用假或模擬的組態物件。</span><span class="sxs-lookup"><span data-stu-id="d1241-168">`IConfiguration.cs`: Abstracts hello implementation of hello Configuration class, so that you can unit test your job splitter using a fake or mock configuration object.</span></span>
* <span data-ttu-id="d1241-169">`JobManager.cs`： 會協調 hello hello 工作管理員程式元件。</span><span class="sxs-lookup"><span data-stu-id="d1241-169">`JobManager.cs`: Orchestrates hello components of hello job manager program.</span></span> <span data-ttu-id="d1241-170">它會負責初始化 hello 作業分隔器，叫用 hello 作業分隔器的 hello 和分派 hello 工作 hello 作業分隔器 toohello 工作傳送者所傳回。</span><span class="sxs-lookup"><span data-stu-id="d1241-170">It is responsible for hello initializing hello job splitter, invoking hello job splitter, and dispatching hello tasks returned by hello job splitter toohello task submitter.</span></span>
* <span data-ttu-id="d1241-171">`JobManagerException.cs`： 表示需要 hello 作業管理員 tooterminate 發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="d1241-171">`JobManagerException.cs`: Represents an error that requires hello job manager tooterminate.</span></span> <span data-ttu-id="d1241-172">JobManagerException 是使用的 toowrap '必須是' 錯誤，即提供特定的診斷資訊，做為終止的一部分。</span><span class="sxs-lookup"><span data-stu-id="d1241-172">JobManagerException is used toowrap 'expected' errors where specific diagnostic information can be provided as part of termination.</span></span>
* <span data-ttu-id="d1241-173">`TaskSubmitter.cs`： 這個類別是負責 tooadding hello 作業分隔器 toohello 批次作業所傳回的工作。</span><span class="sxs-lookup"><span data-stu-id="d1241-173">`TaskSubmitter.cs`: This class is responsible tooadding tasks returned by hello job splitter toohello Batch job.</span></span> <span data-ttu-id="d1241-174">hello JobManager 類別彙總成有效但及時加法 toohello 作業，批次工作 hello 順序，然後在背景執行緒上呼叫 TaskSubmitter.SubmitTasks，每個批次。</span><span class="sxs-lookup"><span data-stu-id="d1241-174">hello JobManager class aggregates hello sequence of tasks into batches for efficient but timely addition toohello job, then calls TaskSubmitter.SubmitTasks on a background thread for each batch.</span></span>

<span data-ttu-id="d1241-175">**作業分割器**</span><span class="sxs-lookup"><span data-stu-id="d1241-175">**Job Splitter**</span></span>

<span data-ttu-id="d1241-176">`JobSplitter.cs`： 這個類別包含應用程式特有邏輯將 hello 工作分割成多個工作。</span><span class="sxs-lookup"><span data-stu-id="d1241-176">`JobSplitter.cs`: This class contains application-specific logic for splitting hello job into tasks.</span></span> <span data-ttu-id="d1241-177">hello 架構會叫用 hello JobSplitter.Split 方法 tooobtain 一連串的工作，它會將它們做為 hello 方法 toohello 作業傳回。</span><span class="sxs-lookup"><span data-stu-id="d1241-177">hello framework invokes hello JobSplitter.Split method tooobtain a sequence of tasks, which it adds toohello job as hello method returns them.</span></span> <span data-ttu-id="d1241-178">這是您會在此插入您工作的 hello 邏輯 hello 類別。</span><span class="sxs-lookup"><span data-stu-id="d1241-178">This is hello class where you will inject hello logic of your job.</span></span> <span data-ttu-id="d1241-179">實作 hello 分割方法 tooreturn CloudTask 代表 hello 工作要 toopartition hello 作業的執行個體的序列。</span><span class="sxs-lookup"><span data-stu-id="d1241-179">Implement hello Split method tooreturn a sequence of CloudTask instances representing hello tasks into which you want toopartition hello job.</span></span>

<span data-ttu-id="d1241-180">**標準 .NET 命令列專案檔**</span><span class="sxs-lookup"><span data-stu-id="d1241-180">**Standard .NET command line project files**</span></span>

* <span data-ttu-id="d1241-181">`App.config`︰標準的 .NET 應用程式組態檔。</span><span class="sxs-lookup"><span data-stu-id="d1241-181">`App.config`: Standard .NET application configuration file.</span></span>
* <span data-ttu-id="d1241-182">`Packages.config`︰標準的 NuGet 套件相依性檔案。</span><span class="sxs-lookup"><span data-stu-id="d1241-182">`Packages.config`: Standard NuGet package dependency file.</span></span>
* <span data-ttu-id="d1241-183">`Program.cs`： 包含 hello 程式進入點和最上層的例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="d1241-183">`Program.cs`: Contains hello program entry point and top-level exception handling.</span></span>

### <a name="implementing-hello-job-splitter"></a><span data-ttu-id="d1241-184">實作 hello 作業分隔器</span><span class="sxs-lookup"><span data-stu-id="d1241-184">Implementing hello job splitter</span></span>
<span data-ttu-id="d1241-185">當您開啟 hello 作業管理員範本專案時，hello 專案將會有預設開啟的 hello JobSplitter.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="d1241-185">When you open hello Job Manager template project, hello project will have hello JobSplitter.cs file open by default.</span></span> <span data-ttu-id="d1241-186">您可以實作 hello 分割您的工作負載中的 hello 工作邏輯使用 hello Split() 方法顯示如下：</span><span class="sxs-lookup"><span data-stu-id="d1241-186">You can implement hello split logic for hello tasks in your workload by using hello Split() method show below:</span></span>

```csharp
/// <summary>
/// Gets hello tasks into which toosplit hello job. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello job manager framework invokes hello Split method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation should return tasks lazily, for example using a C#
/// iterator and hello "yield return" statement; this allows tasks toobe added
/// and toostart running while splitting is still in progress.
/// </summary>
/// <returns>hello tasks toobe added toohello job. Tasks are added automatically
/// by hello job manager framework as they are returned by this method.</returns>
public IEnumerable<CloudTask> Split()
{
    // Your code for hello split logic goes here.
    int startFrame = Convert.ToInt32(_parameters["StartFrame"]);
    int endFrame = Convert.ToInt32(_parameters["EndFrame"]);

    for (int i = startFrame; i <= endFrame; i++)
    {
        yield return new CloudTask("myTask" + i, "cmd /c dir");
    }
}
```

> [!NOTE]
> <span data-ttu-id="d1241-187">hello 附註 > 一節中 hello`Split()`方法是 hello 只有 hello 僅供您 toomodify 將 hello 邏輯 toosplit 您的工作新增至不同的工作的作業管理員範本程式碼區段。</span><span class="sxs-lookup"><span data-stu-id="d1241-187">hello annotated section in hello `Split()` method is hello only section of hello Job Manager template code that is intended for you toomodify by adding hello logic toosplit your jobs into different tasks.</span></span> <span data-ttu-id="d1241-188">如果您想 toomodify hello 範本的其他部分，請確定您以批次的運作方式，請嘗試幾個 hello 和[批次程式碼範例][github_samples]。</span><span class="sxs-lookup"><span data-stu-id="d1241-188">If you want toomodify a different section of hello template, please ensure you are familiarized with how Batch works, and try out a few of hello [Batch code samples][github_samples].</span></span>
> 
> 

<span data-ttu-id="d1241-189">Split() 實作具有下列項目的存取權︰</span><span class="sxs-lookup"><span data-stu-id="d1241-189">Your Split() implementation has access to:</span></span>

* <span data-ttu-id="d1241-190">hello 工作參數，透過 hello`_parameters`欄位。</span><span class="sxs-lookup"><span data-stu-id="d1241-190">hello job parameters, via hello `_parameters` field.</span></span>
* <span data-ttu-id="d1241-191">hello CloudJob 物件代表 hello 工作，透過 hello`_job`欄位。</span><span class="sxs-lookup"><span data-stu-id="d1241-191">hello CloudJob object representing hello job, via hello `_job` field.</span></span>
* <span data-ttu-id="d1241-192">hello CloudTask 物件代表 hello 作業管理員工作，透過 hello`_jobManagerTask`欄位。</span><span class="sxs-lookup"><span data-stu-id="d1241-192">hello CloudTask object representing hello job manager task, via hello `_jobManagerTask` field.</span></span>

<span data-ttu-id="d1241-193">您`Split()`實作不直接需要 tooadd 工作 toohello 作業。</span><span class="sxs-lookup"><span data-stu-id="d1241-193">Your `Split()` implementation does not need tooadd tasks toohello job directly.</span></span> <span data-ttu-id="d1241-194">相反地，您的程式碼應該傳回 CloudTask 物件序列，這些會被加入 toohello 作業會自動叫用 hello 作業分隔器的 hello 架構類別。</span><span class="sxs-lookup"><span data-stu-id="d1241-194">Instead, your code should return a sequence of CloudTask objects, and these will be added toohello job automatically by hello framework classes that invoke hello job splitter.</span></span> <span data-ttu-id="d1241-195">它是一般 toouse C# 的迭代器 (`yield return`) 功能 tooimplement 作業分隔器，因為這可讓 hello 工作 toostart 儘速執行，而不是等待所有工作 toobe 計算。</span><span class="sxs-lookup"><span data-stu-id="d1241-195">It's common toouse C#'s iterator (`yield return`) feature tooimplement job splitters as this allows hello tasks toostart running as soon as possible rather than waiting for all tasks toobe calculated.</span></span>

<span data-ttu-id="d1241-196">**作業分割器失敗**</span><span class="sxs-lookup"><span data-stu-id="d1241-196">**Job splitter failure**</span></span>

<span data-ttu-id="d1241-197">如果作業分割器發生錯誤，它應該︰</span><span class="sxs-lookup"><span data-stu-id="d1241-197">If your job splitter encounters an error, it should either:</span></span>

* <span data-ttu-id="d1241-198">終止使用 hello C# 的 hello 順序`yield break`陳述式，在其中案例 hello 作業管理員會被處理為成功; 或</span><span class="sxs-lookup"><span data-stu-id="d1241-198">Terminate hello sequence using hello C# `yield break` statement, in which case hello job manager will be treated as successful; or</span></span>
* <span data-ttu-id="d1241-199">會擲回例外狀況，case hello 作業管理員會被視為失敗，取決於 hello 用戶端的設定方式，它可能會重試）。</span><span class="sxs-lookup"><span data-stu-id="d1241-199">Throw an exception, in which case hello job manager will be treated as failed and may be retried depending on how hello client has configured it).</span></span>

<span data-ttu-id="d1241-200">在這兩種情況下，hello 作業分隔器已經傳回的任何工作，並加入的 toohello 批次作業將會符合資格 toorun。</span><span class="sxs-lookup"><span data-stu-id="d1241-200">In both cases, any tasks already returned by hello job splitter and added toohello Batch job will be eligible toorun.</span></span> <span data-ttu-id="d1241-201">如果您不想這個 toohappen，然後您可以：</span><span class="sxs-lookup"><span data-stu-id="d1241-201">If you don't want this toohappen, then you could:</span></span>

* <span data-ttu-id="d1241-202">傳回從 hello 作業分隔器之前終止 hello 工作</span><span class="sxs-lookup"><span data-stu-id="d1241-202">Terminate hello job before returning from hello job splitter</span></span>
* <span data-ttu-id="d1241-203">編寫 hello 整個工作集合，再加以傳回 (也就是傳回`ICollection<CloudTask>`或`IList<CloudTask>`而不是實作您使用的 C# 迭代器的作業分隔器)</span><span class="sxs-lookup"><span data-stu-id="d1241-203">Formulate hello entire task collection before returning it (that is, return an `ICollection<CloudTask>` or `IList<CloudTask>` instead of implementing your job splitter using a C# iterator)</span></span>
* <span data-ttu-id="d1241-204">使用所有的工作取決於 hello hello 作業管理員成功完成的工作相依性 toomake</span><span class="sxs-lookup"><span data-stu-id="d1241-204">Use task dependencies toomake all tasks depend on hello successful completion of hello job manager</span></span>

<span data-ttu-id="d1241-205">**作業管理員重試**</span><span class="sxs-lookup"><span data-stu-id="d1241-205">**Job manager retries**</span></span>

<span data-ttu-id="d1241-206">如果 hello 作業管理員失敗，可能會重試 hello 批次服務取決於 hello 用戶端重試設定。</span><span class="sxs-lookup"><span data-stu-id="d1241-206">If hello job manager fails, it may be retried by hello Batch service depending on hello client retry settings.</span></span> <span data-ttu-id="d1241-207">一般情況下，這是安全的因為當 hello 架構就會將工作 toohello 作業，它會忽略任何存在的工作。</span><span class="sxs-lookup"><span data-stu-id="d1241-207">In general, this is safe, because when hello framework adds tasks toohello job, it ignores any tasks that already exist.</span></span> <span data-ttu-id="d1241-208">不過，如果計算的工作是高度耗費資源，您可能不希望 tooincur hello 成本的重新計算已加入 toohello 作業; 的工作相反地，如果 hello 重新執行不是保證的 toogenerate hello 相同工作 Id 則 hello 「 略過重複的項目 」 行為不會開始運作。</span><span class="sxs-lookup"><span data-stu-id="d1241-208">However, if calculating tasks is expensive, you may not wish tooincur hello cost of recalculating tasks that have already been added toohello job; conversely, if hello re-run is not guaranteed toogenerate hello same task IDs then hello 'ignore duplicates' behavior will not kick in.</span></span> <span data-ttu-id="d1241-209">在這些情況下，您應該設計工作分隔器 toodetect hello 工作已完成且不重複，例如啟動 tooyield 工作之前執行 CloudJob.ListTasks。</span><span class="sxs-lookup"><span data-stu-id="d1241-209">In these cases you should design your job splitter toodetect hello work that has already been done and not repeat it, for example by performing a CloudJob.ListTasks before starting tooyield tasks.</span></span>

### <a name="exit-codes-and-exceptions-in-hello-job-manager-template"></a><span data-ttu-id="d1241-210">結束碼和 hello 作業管理員範本中的例外狀況</span><span class="sxs-lookup"><span data-stu-id="d1241-210">Exit codes and exceptions in hello Job Manager template</span></span>
<span data-ttu-id="d1241-211">結束代碼和例外狀況提供機制 toodetermine hello 結果執行的程式時，它們可協助 tooidentify hello hello 程式執行的任何問題。</span><span class="sxs-lookup"><span data-stu-id="d1241-211">Exit codes and exceptions provide a mechanism toodetermine hello outcome of running a program, and they can help tooidentify any problems with hello execution of hello program.</span></span> <span data-ttu-id="d1241-212">hello 作業管理員範本實作 hello 結束碼和本節中所述的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d1241-212">hello Job Manager template implements hello exit codes and exceptions described in this section.</span></span>

<span data-ttu-id="d1241-213">實作與 hello 作業管理員範本的作業管理員工作可能會傳回三個可能的結束代碼：</span><span class="sxs-lookup"><span data-stu-id="d1241-213">A job manager task that is implemented with hello Job Manager template can return three possible exit codes:</span></span>

| <span data-ttu-id="d1241-214">代碼</span><span class="sxs-lookup"><span data-stu-id="d1241-214">Code</span></span> | <span data-ttu-id="d1241-215">說明</span><span class="sxs-lookup"><span data-stu-id="d1241-215">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1241-216">0</span><span class="sxs-lookup"><span data-stu-id="d1241-216">0</span></span> |<span data-ttu-id="d1241-217">hello 作業管理員已順利完成。</span><span class="sxs-lookup"><span data-stu-id="d1241-217">hello job manager completed successfully.</span></span> <span data-ttu-id="d1241-218">作業的分隔器程式碼執行 toocompletion，和所有工作都已都加入 toohello 作業。</span><span class="sxs-lookup"><span data-stu-id="d1241-218">Your job splitter code ran toocompletion, and all tasks were added toohello job.</span></span> |
| <span data-ttu-id="d1241-219">1</span><span class="sxs-lookup"><span data-stu-id="d1241-219">1</span></span> |<span data-ttu-id="d1241-220">hello 作業管理員工作失敗，'必須是' hello 程式一部分的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d1241-220">hello job manager task failed with an exception in an 'expected' part of hello program.</span></span> <span data-ttu-id="d1241-221">hello 發生例外狀況轉譯的 tooa JobManagerException 與診斷資訊，並解決建議盡可能 hello 失敗。</span><span class="sxs-lookup"><span data-stu-id="d1241-221">hello exception was translated tooa JobManagerException with diagnostic information and, where possible, suggestions for resolving hello failure.</span></span> |
| <span data-ttu-id="d1241-222">2</span><span class="sxs-lookup"><span data-stu-id="d1241-222">2</span></span> |<span data-ttu-id="d1241-223">hello 作業管理員工作失敗，意外' 的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d1241-223">hello job manager task failed with an 'unexpected' exception.</span></span> <span data-ttu-id="d1241-224">hello 發生例外狀況記錄的 toostandard 輸出，但 hello 作業管理員無法 tooadd 任何額外的診斷或修復資訊。</span><span class="sxs-lookup"><span data-stu-id="d1241-224">hello exception was logged toostandard output, but hello job manager was unable tooadd any additional diagnostic or remediation information.</span></span> |

<span data-ttu-id="d1241-225">在作業管理員工作失敗的 hello 情況下，某些工作可能仍已新增 toohello 服務 hello 錯誤發生之前。</span><span class="sxs-lookup"><span data-stu-id="d1241-225">In hello case of job manager task failure, some tasks may still have been added toohello service before hello error occurred.</span></span> <span data-ttu-id="d1241-226">這些工作會如常執行。</span><span class="sxs-lookup"><span data-stu-id="d1241-226">These tasks will run as normal.</span></span> <span data-ttu-id="d1241-227">請參閱上面的「作業分割器失敗」以取得有關此程式碼路徑的討論。</span><span class="sxs-lookup"><span data-stu-id="d1241-227">See "Job Splitter Failure" above for discussion of this code path.</span></span>

<span data-ttu-id="d1241-228">所有例外狀況所傳回的 hello 資訊會寫入 stdout.txt 和 stderr.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="d1241-228">All hello information returned by exceptions is written into stdout.txt and stderr.txt files.</span></span> <span data-ttu-id="d1241-229">如需詳細資訊，請參閱 [錯誤處理](batch-api-basics.md#error-handling)。</span><span class="sxs-lookup"><span data-stu-id="d1241-229">For more information, see [Error Handling](batch-api-basics.md#error-handling).</span></span>

### <a name="client-considerations"></a><span data-ttu-id="d1241-230">用戶端考量</span><span class="sxs-lookup"><span data-stu-id="d1241-230">Client considerations</span></span>
<span data-ttu-id="d1241-231">本節說明在根據此範本叫用作業管理員時的一些用戶端實作需求。</span><span class="sxs-lookup"><span data-stu-id="d1241-231">This section describes some client implementation requirements when invoking a job manager based on this template.</span></span> <span data-ttu-id="d1241-232">請參閱[toopass 參數和環境變數從 hello 用戶端程式碼](#pass-environment-settings)如傳遞參數和環境設定的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d1241-232">See [How toopass parameters and environment variables from hello client code](#pass-environment-settings) for details on passing parameters and environment settings.</span></span>

<span data-ttu-id="d1241-233">**必要認證**</span><span class="sxs-lookup"><span data-stu-id="d1241-233">**Mandatory credentials**</span></span>

<span data-ttu-id="d1241-234">在訂單 tooadd 工作 toohello Azure 批次作業，hello 作業管理員工作需要您的 Azure Batch 帳戶 URL 和金鑰。</span><span class="sxs-lookup"><span data-stu-id="d1241-234">In order tooadd tasks toohello Azure Batch job, hello job manager task requires your Azure Batch account URL and key.</span></span> <span data-ttu-id="d1241-235">您必須在名為 YOUR_BATCH_URL 和 YOUR_BATCH_KEY 的環境變數中傳遞這些資料。</span><span class="sxs-lookup"><span data-stu-id="d1241-235">You must pass these in environment variables named YOUR_BATCH_URL and YOUR_BATCH_KEY.</span></span> <span data-ttu-id="d1241-236">您可以設定在 hello 作業管理員工作環境設定。</span><span class="sxs-lookup"><span data-stu-id="d1241-236">You can set these in hello Job Manager task environment settings.</span></span> <span data-ttu-id="d1241-237">例如，在 C# 用戶端︰</span><span class="sxs-lookup"><span data-stu-id="d1241-237">For example, in a C# client:</span></span>

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    new EnvironmentSetting("YOUR_BATCH_URL", "https://account.region.batch.azure.com"),
    new EnvironmentSetting("YOUR_BATCH_KEY", "{your_base64_encoded_account_key}"),
};
```
<span data-ttu-id="d1241-238">**儲存體認證**</span><span class="sxs-lookup"><span data-stu-id="d1241-238">**Storage credentials**</span></span>

<span data-ttu-id="d1241-239">通常，hello 用戶端不需要 tooprovide hello 連結儲存體帳戶認證 toohello 作業管理員工作 （a） 大部分的工作管理員不需要 tooexplicitly 存取 hello 連結儲存體帳戶，而且 （b) hello 連結儲存體帳戶通常是因為常見的環境設定為 hello 工作 tooall 工作。</span><span class="sxs-lookup"><span data-stu-id="d1241-239">Typically, hello client does not need tooprovide hello linked storage account credentials toohello job manager task because (a) most job managers do not need tooexplicitly access hello linked storage account and (b) hello linked storage account is often provided tooall tasks as a common environment setting for hello job.</span></span> <span data-ttu-id="d1241-240">如果您未提供 hello 連結 hello 一般環境設定，透過儲存體帳戶，hello 作業管理員需要存取 toolinked 儲存體，然後您就應該提供 hello 連結儲存體認證，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d1241-240">If you are not providing hello linked storage account via hello common environment settings, and hello job manager requires access toolinked storage, then you should supply hello linked storage credentials as follows:</span></span>

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    /* other environment settings */
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

<span data-ttu-id="d1241-241">**作業管理員工作設定**</span><span class="sxs-lookup"><span data-stu-id="d1241-241">**Job manager task settings**</span></span>

<span data-ttu-id="d1241-242">hello 用戶端應該設定 hello 作業管理員*killJobOnCompletion*旗標太**false**。</span><span class="sxs-lookup"><span data-stu-id="d1241-242">hello client should set hello job manager *killJobOnCompletion* flag too**false**.</span></span>

<span data-ttu-id="d1241-243">通常可以放心的 hello 用戶端 tooset *runExclusive*太**false**。</span><span class="sxs-lookup"><span data-stu-id="d1241-243">It is usually safe for hello client tooset *runExclusive* too**false**.</span></span>

<span data-ttu-id="d1241-244">hello 用戶端應使用 hello *resourceFiles*或*applicationPackageReferences*集合 toohave hello 作業管理員可執行檔 （和其所需的 Dll） 部署 toohello 計算節點。</span><span class="sxs-lookup"><span data-stu-id="d1241-244">hello client should use hello *resourceFiles* or *applicationPackageReferences* collection toohave hello job manager executable (and its required DLLs) deployed toohello compute node.</span></span>

<span data-ttu-id="d1241-245">根據預設，hello 作業管理員將不會失敗時的重試。</span><span class="sxs-lookup"><span data-stu-id="d1241-245">By default, hello job manager will not be retried if it fails.</span></span> <span data-ttu-id="d1241-246">根據您的工作管理員邏輯 hello 用戶端可能會想透過 tooenable 重試*條件約束*/*maxTaskRetryCount*。</span><span class="sxs-lookup"><span data-stu-id="d1241-246">Depending on your job manager logic, hello client may want tooenable retries via *constraints*/*maxTaskRetryCount*.</span></span>

<span data-ttu-id="d1241-247">**作業設定**</span><span class="sxs-lookup"><span data-stu-id="d1241-247">**Job settings**</span></span>

<span data-ttu-id="d1241-248">如果 hello 作業分隔器發出工作具相依性，hello 用戶端必須設定 hello 作業 usesTaskDependencies tootrue。</span><span class="sxs-lookup"><span data-stu-id="d1241-248">If hello job splitter emits tasks with dependencies, hello client must set hello job's usesTaskDependencies tootrue.</span></span>

<span data-ttu-id="d1241-249">在 hello 作業分隔器模型中，它並不常見的用戶端 toowish tooadd 工作 toojobs 除了哪些 hello 作業分隔器會建立項目。</span><span class="sxs-lookup"><span data-stu-id="d1241-249">In hello job splitter model, it is unusual for clients toowish tooadd tasks toojobs over and above what hello job splitter creates.</span></span> <span data-ttu-id="d1241-250">hello 用戶端應該因此通常設定 hello 作業*onAllTasksComplete*太**terminatejob**。</span><span class="sxs-lookup"><span data-stu-id="d1241-250">hello client should therefore normally set hello job's *onAllTasksComplete* too**terminatejob**.</span></span>

## <a name="task-processor-template"></a><span data-ttu-id="d1241-251">工作處理器範本</span><span class="sxs-lookup"><span data-stu-id="d1241-251">Task Processor template</span></span>
<span data-ttu-id="d1241-252">工作處理器範本可協助您 tooimplement 工作處理器可以執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="d1241-252">A Task Processor template helps you tooimplement a task processor that can perform hello following actions:</span></span>

* <span data-ttu-id="d1241-253">設定所需的每個批次工作 toorun hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="d1241-253">Set up hello information required by each Batch task toorun.</span></span>
* <span data-ttu-id="d1241-254">執行每個 Batch 工作所需的所有動作。</span><span class="sxs-lookup"><span data-stu-id="d1241-254">Run all actions required by each Batch task.</span></span>
* <span data-ttu-id="d1241-255">儲存工作輸出 toopersistent 儲存體。</span><span class="sxs-lookup"><span data-stu-id="d1241-255">Save task outputs toopersistent storage.</span></span>

<span data-ttu-id="d1241-256">雖然工作處理器不需要的 toorun 工作批次，但 hello 主要優點使用工作處理器是它提供包裝函式 tooimplement 某一個位置中的所有工作執行動作。</span><span class="sxs-lookup"><span data-stu-id="d1241-256">Although a task processor is not required toorun tasks on Batch, hello key advantage of using a task processor is that it provides a wrapper tooimplement all task execution actions in one location.</span></span> <span data-ttu-id="d1241-257">例如，如果您需要 toorun hello 內容中數個應用程式的每項工作，或如果您需要 toocopy toopersistent 儲存資料之後完成各項工作。</span><span class="sxs-lookup"><span data-stu-id="d1241-257">For example, if you need toorun several applications in hello context of each task, or if you need toocopy data toopersistent storage after completing each task.</span></span>

<span data-ttu-id="d1241-258">hello hello 工作處理器所執行的動作可能也為簡單或複雜，和最大數量越少，所需的工作負載。</span><span class="sxs-lookup"><span data-stu-id="d1241-258">hello actions performed by hello task processor can be as simple or complex, and as many or as few, as required by your workload.</span></span> <span data-ttu-id="d1241-259">此外，藉由實作所有的工作動作到一個工作的處理器，您可以輕易地更新或新增根據變更 tooapplications 或工作負載需求的動作。</span><span class="sxs-lookup"><span data-stu-id="d1241-259">Additionally, by implementing all task actions into one task processor, you can readily update or add actions based on changes tooapplications or workload requirements.</span></span> <span data-ttu-id="d1241-260">不過，在某些情況下工作處理器可能會無法 hello 最佳化解決方案實作作為它可以將不必要的複雜性，例如當執行可以快速地從簡單的命令列啟動的工作。</span><span class="sxs-lookup"><span data-stu-id="d1241-260">However, in some cases a task processor might not be hello optimal solution for your implementation as it can add unnecessary complexity, for example when running jobs that can be quickly started from a simple command line.</span></span>

### <a name="create-a-task-processor-using-hello-template"></a><span data-ttu-id="d1241-261">建立工作處理器使用 hello 範本</span><span class="sxs-lookup"><span data-stu-id="d1241-261">Create a Task Processor using hello template</span></span>
<span data-ttu-id="d1241-262">tooadd 工作處理器 toohello 建立的方案，您更早版本，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d1241-262">tooadd a task processor toohello solution that you created earlier, follow these steps:</span></span>

1. <span data-ttu-id="d1241-263">在 Visual Studio 中開啟現有方案。</span><span class="sxs-lookup"><span data-stu-id="d1241-263">Open your existing solution in Visual Studio.</span></span>
2. <span data-ttu-id="d1241-264">在 方案總管 中，以滑鼠右鍵按一下 hello 方案中，按一下 **新增**，然後按一下**新專案**。</span><span class="sxs-lookup"><span data-stu-id="d1241-264">In Solution Explorer, right-click hello solution, click **Add**, and then click **New Project**.</span></span>
3. <span data-ttu-id="d1241-265">在 Visual C# 底下按一下 雲端，然後按一下Azure Batch 工作處理器。</span><span class="sxs-lookup"><span data-stu-id="d1241-265">Under **Visual C#**, click **Cloud**, and then click **Azure Batch Task Processor**.</span></span>
4. <span data-ttu-id="d1241-266">輸入的名稱來描述您的應用程式，以及識別這個專案時 （例如 hello 工作處理器"LitwareTaskProcessor")。</span><span class="sxs-lookup"><span data-stu-id="d1241-266">Type a name that describes your application and identifies this project as hello task processor (e.g. "LitwareTaskProcessor").</span></span>
5. <span data-ttu-id="d1241-267">toocreate hello 專案中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="d1241-267">toocreate hello project, click **OK**.</span></span>
6. <span data-ttu-id="d1241-268">最後，建置 hello 專案 tooforce Visual Studio tooload 所有參考的 NuGet 封裝，並 hello 專案的 tooverify 有效，然後再開始進行修改。</span><span class="sxs-lookup"><span data-stu-id="d1241-268">Finally, build hello project tooforce Visual Studio tooload all referenced NuGet packages and tooverify that hello project is valid before you start modifying it.</span></span>

### <a name="task-processor-template-files-and-their-purpose"></a><span data-ttu-id="d1241-269">工作處理器範本檔案及其用途</span><span class="sxs-lookup"><span data-stu-id="d1241-269">Task Processor template files and their purpose</span></span>
<span data-ttu-id="d1241-270">當您使用範本建立專案 hello 工作處理器時，它會產生三個群組的程式碼檔案：</span><span class="sxs-lookup"><span data-stu-id="d1241-270">When you create a project using hello task processor template, it generates three groups of code files:</span></span>

* <span data-ttu-id="d1241-271">hello 主要程式檔案 (Program.cs)。</span><span class="sxs-lookup"><span data-stu-id="d1241-271">hello main program file (Program.cs).</span></span> <span data-ttu-id="d1241-272">這包含 hello 程式進入點和最上層的例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="d1241-272">This contains hello program entry point and top-level exception handling.</span></span> <span data-ttu-id="d1241-273">您通常不應該這樣需要 toomodify。</span><span class="sxs-lookup"><span data-stu-id="d1241-273">You shouldn't normally need toomodify this.</span></span>
* <span data-ttu-id="d1241-274">hello Framework 目錄。</span><span class="sxs-lookup"><span data-stu-id="d1241-274">hello Framework directory.</span></span> <span data-ttu-id="d1241-275">這包含 hello 檔案負責 hello 工作管理員程式-解除封裝參數，加入等工作 toohello 批次作業所完成的 hello '未定案' 工作。您通常應該不需要 toomodify 這些檔案。</span><span class="sxs-lookup"><span data-stu-id="d1241-275">This contains hello files responsible for hello 'boilerplate' work done by hello job manager program – unpacking parameters, adding tasks toohello Batch job, etc. You shouldn't normally need toomodify these files.</span></span>
* <span data-ttu-id="d1241-276">hello 工作處理器檔案 (TaskProcessor.cs)。</span><span class="sxs-lookup"><span data-stu-id="d1241-276">hello task processor file (TaskProcessor.cs).</span></span> <span data-ttu-id="d1241-277">這是您將在其中放置您應用程式特定的邏輯 （通常是藉由呼叫出 tooan 現有可執行檔） 執行工作。</span><span class="sxs-lookup"><span data-stu-id="d1241-277">This is where you will put your application-specific logic for executing a task (typically by calling out tooan existing executable).</span></span> <span data-ttu-id="d1241-278">前置和後置處理程式碼 (例如下載額外資料或上傳結果檔案) 也存放在此。</span><span class="sxs-lookup"><span data-stu-id="d1241-278">Pre- and post-processing code, such as downloading additional data or uploading result files, also goes here.</span></span>

<span data-ttu-id="d1241-279">當然您可以加入其他檔案，需要 toosupport 做您工作處理器的程式碼，視分割邏輯 hello 作業 hello 複雜度而定。</span><span class="sxs-lookup"><span data-stu-id="d1241-279">Of course you can add additional files as required toosupport your task processor code, depending on hello complexity of hello job splitting logic.</span></span>

<span data-ttu-id="d1241-280">hello 範本也會產生標準的.NET 專案檔，例如.csproj 檔案、 app.config、 packages.config 等等。</span><span class="sxs-lookup"><span data-stu-id="d1241-280">hello template also generates standard .NET project files such as a .csproj file, app.config, packages.config, etc.</span></span>

<span data-ttu-id="d1241-281">hello 本節其餘部分描述 hello 不同的檔案和程式碼結構，並說明每個類別的用途。</span><span class="sxs-lookup"><span data-stu-id="d1241-281">hello rest of this section describes hello different files and their code structure, and explains what each class does.</span></span>

![Visual Studio 方案總管中顯示 hello 工作處理器範本解決方案][solution_explorer02]

<span data-ttu-id="d1241-283">**架構檔案**</span><span class="sxs-lookup"><span data-stu-id="d1241-283">**Framework files**</span></span>

* <span data-ttu-id="d1241-284">`Configuration.cs`： 封裝 hello 載入的工作組態資料，例如批次帳戶詳細資料、 連結的儲存體帳戶認證、 作業和工作資訊和作業參數。</span><span class="sxs-lookup"><span data-stu-id="d1241-284">`Configuration.cs`: Encapsulates hello loading of job configuration data such as Batch account details, linked storage account credentials, job and task information, and job parameters.</span></span> <span data-ttu-id="d1241-285">它也提供存取 tooBatch 定義環境變數 （請參閱 hello 批次的文件中的工作環境設定） 透過 hello Configuration.EnvironmentVariable 類別。</span><span class="sxs-lookup"><span data-stu-id="d1241-285">It also provides access tooBatch-defined environment variables (see Environment settings for tasks, in hello Batch documentation) via hello Configuration.EnvironmentVariable class.</span></span>
* <span data-ttu-id="d1241-286">`IConfiguration.cs`： 摘要 hello hello 設定類別的實作，單元，讓您可以測試您的工作分隔器使用假或模擬的組態物件。</span><span class="sxs-lookup"><span data-stu-id="d1241-286">`IConfiguration.cs`: Abstracts hello implementation of hello Configuration class, so that you can unit test your job splitter using a fake or mock configuration object.</span></span>
* <span data-ttu-id="d1241-287">`TaskProcessorException.cs`： 表示需要 hello 作業管理員 tooterminate 發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="d1241-287">`TaskProcessorException.cs`: Represents an error that requires hello job manager tooterminate.</span></span> <span data-ttu-id="d1241-288">TaskProcessorException 是使用的 toowrap '必須是' 錯誤，即提供特定的診斷資訊，做為終止的一部分。</span><span class="sxs-lookup"><span data-stu-id="d1241-288">TaskProcessorException is used toowrap 'expected' errors where specific diagnostic information can be provided as part of termination.</span></span>

<span data-ttu-id="d1241-289">**工作處理器**</span><span class="sxs-lookup"><span data-stu-id="d1241-289">**Task Processor**</span></span>

* <span data-ttu-id="d1241-290">`TaskProcessor.cs`： 執行 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="d1241-290">`TaskProcessor.cs`: Runs hello task.</span></span> <span data-ttu-id="d1241-291">hello 架構會叫用 hello TaskProcessor.Run 方法。</span><span class="sxs-lookup"><span data-stu-id="d1241-291">hello framework invokes hello TaskProcessor.Run method.</span></span> <span data-ttu-id="d1241-292">這是工作的您會在此插入您 hello 特定應用程式邏輯 hello 類別。</span><span class="sxs-lookup"><span data-stu-id="d1241-292">This is hello class where you will inject hello application-specific logic of your task.</span></span> <span data-ttu-id="d1241-293">實作 hello Run 方法：</span><span class="sxs-lookup"><span data-stu-id="d1241-293">Implement hello Run method to:</span></span>
  * <span data-ttu-id="d1241-294">剖析及驗證任何工作參數</span><span class="sxs-lookup"><span data-stu-id="d1241-294">Parse and validate any task parameters</span></span>
  * <span data-ttu-id="d1241-295">撰寫 hello 命令列的任何外部程式，您想 tooinvoke</span><span class="sxs-lookup"><span data-stu-id="d1241-295">Compose hello command line for any external program you want tooinvoke</span></span>
  * <span data-ttu-id="d1241-296">記錄為了偵錯所可能需要的任何診斷資訊</span><span class="sxs-lookup"><span data-stu-id="d1241-296">Log any diagnostic information you may require for debugging purposes</span></span>
  * <span data-ttu-id="d1241-297">使用該命令列開始處理序</span><span class="sxs-lookup"><span data-stu-id="d1241-297">Start a process using that command line</span></span>
  * <span data-ttu-id="d1241-298">等候 hello 程序 tooexit</span><span class="sxs-lookup"><span data-stu-id="d1241-298">Wait for hello process tooexit</span></span>
  * <span data-ttu-id="d1241-299">擷取 hello 程序 toodetermine hello 結束代碼，如果它是成功或是失敗</span><span class="sxs-lookup"><span data-stu-id="d1241-299">Capture hello exit code of hello process toodetermine if it succeeded or failed</span></span>
  * <span data-ttu-id="d1241-300">儲存所有您想要的輸出檔案 tookeep toopersistent 儲存體</span><span class="sxs-lookup"><span data-stu-id="d1241-300">Save any output files you want tookeep toopersistent storage</span></span>

<span data-ttu-id="d1241-301">**標準 .NET 命令列專案檔**</span><span class="sxs-lookup"><span data-stu-id="d1241-301">**Standard .NET command line project files**</span></span>

* <span data-ttu-id="d1241-302">`App.config`︰標準的 .NET 應用程式組態檔。</span><span class="sxs-lookup"><span data-stu-id="d1241-302">`App.config`: Standard .NET application configuration file.</span></span>
* <span data-ttu-id="d1241-303">`Packages.config`︰標準的 NuGet 套件相依性檔案。</span><span class="sxs-lookup"><span data-stu-id="d1241-303">`Packages.config`: Standard NuGet package dependency file.</span></span>
* <span data-ttu-id="d1241-304">`Program.cs`： 包含 hello 程式進入點和最上層的例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="d1241-304">`Program.cs`: Contains hello program entry point and top-level exception handling.</span></span>

## <a name="implementing-hello-task-processor"></a><span data-ttu-id="d1241-305">實作 hello 工作處理器</span><span class="sxs-lookup"><span data-stu-id="d1241-305">Implementing hello task processor</span></span>
<span data-ttu-id="d1241-306">當您開啟 hello 工作處理器範本專案時，hello 專案將會有預設開啟的 hello TaskProcessor.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="d1241-306">When you open hello Task Processor template project, hello project will have hello TaskProcessor.cs file open by default.</span></span> <span data-ttu-id="d1241-307">您可以實作您的工作負載中的 hello 工作執行的 hello 邏輯使用 hello run （） 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d1241-307">You can implement hello run logic for hello tasks in your workload by using hello Run() method shown below:</span></span>

```csharp
/// <summary>
/// Runs hello task processing logic. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello task processor framework invokes hello Run method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation will execute an external program (from resource files or
/// an application package), check hello exit code of that program and
/// save output files toopersistent storage.
/// </summary>
public async Task<int> Run()

{
    try
    {
        //Your code for hello task processor goes here.
        var command = $"compare {_parameters["Frame1"]} {_parameters["Frame2"]} compare.gif";
        using (var process = Process.Start($"cmd /c {command}"))
        {
            process.WaitForExit();
            var taskOutputStorage = new TaskOutputStorage(
            _configuration.StorageAccount,
            _configuration.JobId,
            _configuration.TaskId
            );
            await taskOutputStorage.SaveAsync(
            TaskOutputKind.TaskOutput,
            @"..\stdout.txt",
            @"stdout.txt"
            );
            return process.ExitCode;
        }
    }
    catch (Exception ex)
    {
        throw new TaskProcessorException(
        $"{ex.GetType().Name} exception in run task processor: {ex.Message}",
        ex
        );
    }
}
```
> [!NOTE]
> <span data-ttu-id="d1241-308">hello hello run （） 方法中的註解式的區段是 hello 只有 hello 工作處理器範本之程式碼區段供您 toomodify 加入您的工作負載中的 hello 工作的 hello 執行邏輯。</span><span class="sxs-lookup"><span data-stu-id="d1241-308">hello annotated section in hello Run() method is hello only section of hello Task Processor template code that is intended for you toomodify by adding hello run logic for hello tasks in your workload.</span></span> <span data-ttu-id="d1241-309">如果您想 toomodify hello 範本的其他部分，請先熟悉批次檢閱 hello 批次的文件，並嘗試幾個 hello 批次的程式碼範例的運作方式。</span><span class="sxs-lookup"><span data-stu-id="d1241-309">If you want toomodify a different section of hello template, please first familiarize yourself with how Batch works by reviewing hello Batch documentation and trying out a few of hello Batch code samples.</span></span>
> 
> 

<span data-ttu-id="d1241-310">hello run （） 方法負責啟動 hello 命令列、 啟動一或多個處理序，等候所有處理序 toocomplete、 儲存 hello 結果，以及最後傳回，結束代碼。</span><span class="sxs-lookup"><span data-stu-id="d1241-310">hello Run() method is responsible for launching hello command line, starting one or more processes, waiting for all process toocomplete, saving hello results, and finally returning with an exit code.</span></span> <span data-ttu-id="d1241-311">hello run （） 方法是您用來實作 hello 處理您的工作的邏輯。</span><span class="sxs-lookup"><span data-stu-id="d1241-311">hello Run() method is where you implement hello processing logic for your tasks.</span></span> <span data-ttu-id="d1241-312">hello 工作處理器架構會叫用 hello run （） 方法。您不需要 toocall 它自己。</span><span class="sxs-lookup"><span data-stu-id="d1241-312">hello task processor framework invokes hello Run() method for you; you do not need toocall it yourself.</span></span>

<span data-ttu-id="d1241-313">Run() 實作具有下列項目的存取權︰</span><span class="sxs-lookup"><span data-stu-id="d1241-313">Your Run() implementation has access to:</span></span>

* <span data-ttu-id="d1241-314">hello 工作參數，透過 hello`_parameters`欄位。</span><span class="sxs-lookup"><span data-stu-id="d1241-314">hello task parameters, via hello `_parameters` field.</span></span>
* <span data-ttu-id="d1241-315">hello 作業和工作的識別碼，透過 hello`_jobId`和`_taskId`欄位。</span><span class="sxs-lookup"><span data-stu-id="d1241-315">hello job and task ids, via hello `_jobId` and `_taskId` fields.</span></span>
* <span data-ttu-id="d1241-316">hello 工作設定，透過 hello`_configuration`欄位。</span><span class="sxs-lookup"><span data-stu-id="d1241-316">hello task configuration, via hello `_configuration` field.</span></span>

<span data-ttu-id="d1241-317">**工作失敗**</span><span class="sxs-lookup"><span data-stu-id="d1241-317">**Task failure**</span></span>

<span data-ttu-id="d1241-318">發生失敗時，您可以結束 hello run （） 方法擲回例外狀況，但這會保留 hello 上方層級例外狀況處理常式中的 hello 工作結束代碼的控制項。</span><span class="sxs-lookup"><span data-stu-id="d1241-318">In case of failure, you can exit hello Run() method by throwing an exception, but this leaves hello top level exception handler in control of hello task exit code.</span></span> <span data-ttu-id="d1241-319">或如果您需要 toocontrol hello 結束代碼，以便您可以進行診斷，例如區分不同類型的失敗，因為某些失敗模式應該終止 hello 工作和其他項目不應該則您應該藉由傳回結束 hello run （） 方法非零結束代碼。</span><span class="sxs-lookup"><span data-stu-id="d1241-319">If you need toocontrol hello exit code so that you can distinguish different types of failure, for example for diagnostic purposes or because some failure modes should terminate hello job and others should not, then you should exit hello Run() method by returning a non-zero exit code.</span></span> <span data-ttu-id="d1241-320">這會成為 hello 工作結束代碼。</span><span class="sxs-lookup"><span data-stu-id="d1241-320">This becomes hello task exit code.</span></span>

### <a name="exit-codes-and-exceptions-in-hello-task-processor-template"></a><span data-ttu-id="d1241-321">結束碼和 hello 工作處理器範本中的例外狀況</span><span class="sxs-lookup"><span data-stu-id="d1241-321">Exit codes and exceptions in hello Task Processor template</span></span>
<span data-ttu-id="d1241-322">結束代碼和例外狀況提供機制 toodetermine hello 結果執行的程式時，它們可協助您識別 hello hello 程式執行的任何問題。</span><span class="sxs-lookup"><span data-stu-id="d1241-322">Exit codes and exceptions provide a mechanism toodetermine hello outcome of running a program, and they can help identify any problems with hello execution of hello program.</span></span> <span data-ttu-id="d1241-323">hello 工作處理器範本實作 hello 結束碼和本節中所述的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d1241-323">hello Task Processor template implements hello exit codes and exceptions described in this section.</span></span>

<span data-ttu-id="d1241-324">實作與 hello 處理器工作範本的工作處理器工作可能會傳回三個可能的結束代碼：</span><span class="sxs-lookup"><span data-stu-id="d1241-324">A task processor task that is implemented with hello Task Processor template can return three possible exit codes:</span></span>

| <span data-ttu-id="d1241-325">代碼</span><span class="sxs-lookup"><span data-stu-id="d1241-325">Code</span></span> | <span data-ttu-id="d1241-326">說明</span><span class="sxs-lookup"><span data-stu-id="d1241-326">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1241-327">[Process.ExitCode][process_exitcode]</span><span class="sxs-lookup"><span data-stu-id="d1241-327">[Process.ExitCode][process_exitcode]</span></span> |<span data-ttu-id="d1241-328">hello 工作處理器已 toocompletion。</span><span class="sxs-lookup"><span data-stu-id="d1241-328">hello task processor ran toocompletion.</span></span> <span data-ttu-id="d1241-329">請注意，這不表示您叫用該 hello 程式已順利完成，只有該 hello 工作處理器順利叫用及執行任何後置處理，沒有例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d1241-329">Note that this does not imply that hello program you invoked was successful – only that hello task processor invoked it successfully and performed any post-processing without exceptions.</span></span> <span data-ttu-id="d1241-330">hello hello 結束程式碼的意義取決於 hello 叫用程式 – 通常結束碼 0 表示成功 hello 程式和任何其他的結束代碼表示 hello 程式失敗。</span><span class="sxs-lookup"><span data-stu-id="d1241-330">hello meaning of hello exit code depends on hello invoked program – typically exit code 0 means hello program succeeded and any other exit code means hello program failed.</span></span> |
| <span data-ttu-id="d1241-331">1</span><span class="sxs-lookup"><span data-stu-id="d1241-331">1</span></span> |<span data-ttu-id="d1241-332">hello 工作處理器失敗 '必須是' hello 程式一部分的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d1241-332">hello task processor failed with an exception in an 'expected' part of hello program.</span></span> <span data-ttu-id="d1241-333">hello 發生例外狀況轉譯的 tooa`TaskProcessorException`與診斷資訊以及解決建議盡可能 hello 失敗。</span><span class="sxs-lookup"><span data-stu-id="d1241-333">hello exception was translated tooa `TaskProcessorException` with diagnostic information and, where possible, suggestions for resolving hello failure.</span></span> |
| <span data-ttu-id="d1241-334">2</span><span class="sxs-lookup"><span data-stu-id="d1241-334">2</span></span> |<span data-ttu-id="d1241-335">hello 工作處理器無法以 '預期' 的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d1241-335">hello task processor failed with an 'unexpected' exception.</span></span> <span data-ttu-id="d1241-336">hello 例外狀況記錄的 toostandard 輸出，但 hello 工作處理器是無法 tooadd 任何額外的診斷或修復資訊。</span><span class="sxs-lookup"><span data-stu-id="d1241-336">hello exception was logged toostandard output, but hello task processor was unable tooadd any additional diagnostic or remediation information.</span></span> |

> [!NOTE]
> <span data-ttu-id="d1241-337">如果您叫用的 hello 程式使用結束碼 1 和 2 tooindicate 特定失敗模式，然後使用工作處理器錯誤結束代碼 1 和 2 模稜兩可。</span><span class="sxs-lookup"><span data-stu-id="d1241-337">If hello program you invoke uses exit codes 1 and 2 tooindicate specific failure modes, then using exit codes 1 and 2 for task processor errors is ambiguous.</span></span> <span data-ttu-id="d1241-338">您可以變更這些工作處理器錯誤代碼 toodistinctive 結束代碼，藉由編輯 hello Program.cs 檔案中的 hello 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d1241-338">You can change these task processor error codes toodistinctive exit codes by editing hello exception cases in hello Program.cs file.</span></span>
> 
> 

<span data-ttu-id="d1241-339">所有例外狀況所傳回的 hello 資訊會寫入 stdout.txt 和 stderr.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="d1241-339">All hello information returned by exceptions is written into stdout.txt and stderr.txt files.</span></span> <span data-ttu-id="d1241-340">如需詳細資訊，請參閱錯誤處理，hello 批次的文件。</span><span class="sxs-lookup"><span data-stu-id="d1241-340">For more information, see Error Handling, in hello Batch documentation.</span></span>

### <a name="client-considerations"></a><span data-ttu-id="d1241-341">用戶端考量</span><span class="sxs-lookup"><span data-stu-id="d1241-341">Client considerations</span></span>
<span data-ttu-id="d1241-342">**儲存體認證**</span><span class="sxs-lookup"><span data-stu-id="d1241-342">**Storage credentials**</span></span>

<span data-ttu-id="d1241-343">如果您工作的處理器會使用 Azure blob 儲存體 toopersist 輸出，例如使用 hello 檔慣例協助程式程式庫，則它需要存取太*任一*hello 雲端儲存體帳戶認證*或*blob 容器 URL，其中包含共用的存取簽章 (SAS)。</span><span class="sxs-lookup"><span data-stu-id="d1241-343">If your task processor uses Azure blob storage toopersist outputs, for example using hello file conventions helper library, then it needs access too*either* hello cloud storage account credentials *or* a blob container URL that includes a shared access signature (SAS).</span></span> <span data-ttu-id="d1241-344">hello 範本包括提供認證能夠透過常見的環境變數的支援。</span><span class="sxs-lookup"><span data-stu-id="d1241-344">hello template includes support for providing credentials via common environment variables.</span></span> <span data-ttu-id="d1241-345">您的用戶端可以傳遞 hello 儲存體認證，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d1241-345">Your client can pass hello storage credentials as follows:</span></span>

```csharp
job.CommonEnvironmentSettings = new [] {
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

<span data-ttu-id="d1241-346">hello 儲存體帳戶位於然後 hello TaskProcessor 類別，透過 hello`_configuration.StorageAccount`屬性。</span><span class="sxs-lookup"><span data-stu-id="d1241-346">hello storage account is then available in hello TaskProcessor class via hello `_configuration.StorageAccount` property.</span></span>

<span data-ttu-id="d1241-347">如果您偏好 toouse SAS 的容器 URL，您也可以將這個工作一般環境設定，透過但 hello 工作處理器範本目前不包括內建支援。</span><span class="sxs-lookup"><span data-stu-id="d1241-347">If you prefer toouse a container URL with SAS, you can also pass this via an job common environment setting, but hello task processor template does not currently include built-in support for this.</span></span>

<span data-ttu-id="d1241-348">**儲存體設定**</span><span class="sxs-lookup"><span data-stu-id="d1241-348">**Storage setup**</span></span>

<span data-ttu-id="d1241-349">建議的 hello 的用戶端或作業管理員工作建立任何所需的工作，然後再加入 hello 工作 toohello 工作的容器。</span><span class="sxs-lookup"><span data-stu-id="d1241-349">It is recommended that hello client or job manager task create any containers required by tasks before adding hello tasks toohello job.</span></span> <span data-ttu-id="d1241-350">這是強制性，如果您使用 SAS 容器 URL，因此 URL 未包含的權限 toocreate hello 容器。</span><span class="sxs-lookup"><span data-stu-id="d1241-350">This is mandatory if you use a container URL with SAS, as such a URL does not include permission toocreate hello container.</span></span> <span data-ttu-id="d1241-351">建議即使傳遞儲存體帳戶認證，因為它會將儲存每個工作各自 toocall CloudBlobContainer.CreateIfNotExistsAsync 具有 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="d1241-351">It is recommended even if you pass storage account credentials, as it saves every task having toocall CloudBlobContainer.CreateIfNotExistsAsync on hello container.</span></span>

## <a name="pass-parameters-and-environment-variables"></a><span data-ttu-id="d1241-352">傳遞參數和環境變數</span><span class="sxs-lookup"><span data-stu-id="d1241-352">Pass parameters and environment variables</span></span>
### <a name="pass-environment-settings"></a><span data-ttu-id="d1241-353">傳遞環境設定</span><span class="sxs-lookup"><span data-stu-id="d1241-353">Pass environment settings</span></span>
<span data-ttu-id="d1241-354">用戶端傳遞資訊的環境設定 hello 形式 toohello 作業管理員工作。</span><span class="sxs-lookup"><span data-stu-id="d1241-354">A client can pass information toohello job manager task in hello form of environment settings.</span></span> <span data-ttu-id="d1241-355">這項資訊然後 hello 作業管理員工作所使用，當產生 hello 工作的處理器工作會執行一部分 hello 計算作業。</span><span class="sxs-lookup"><span data-stu-id="d1241-355">This information can then be used by hello job manager task when generating hello task processor tasks that will run as part of hello compute job.</span></span> <span data-ttu-id="d1241-356">您可以傳遞做為環境設定的 hello 資訊的範例如下：</span><span class="sxs-lookup"><span data-stu-id="d1241-356">Examples of hello information that you can pass as environment settings are:</span></span>

* <span data-ttu-id="d1241-357">儲存體帳戶名稱和帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="d1241-357">Storage account name and account keys</span></span>
* <span data-ttu-id="d1241-358">Batch 帳戶 URL</span><span class="sxs-lookup"><span data-stu-id="d1241-358">Batch account URL</span></span>
* <span data-ttu-id="d1241-359">Batch 帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="d1241-359">Batch account key</span></span>

<span data-ttu-id="d1241-360">hello 批次服務有簡單的機制，toopass 環境設定 tooa 作業管理員工作使用 hello`EnvironmentSettings`屬性[Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask]。</span><span class="sxs-lookup"><span data-stu-id="d1241-360">hello Batch service has a simple mechanism toopass environment settings tooa job manager task by using hello `EnvironmentSettings` property in [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask].</span></span>

<span data-ttu-id="d1241-361">例如，tooget hello`BatchClient`執行個體批次帳戶，您可以將傳遞為環境變數從 hello 用戶端 hello URL 的程式碼和共用金鑰 hello 批次帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="d1241-361">For example, tooget hello `BatchClient` instance for a Batch account, you can pass as environment variables from hello client code hello URL and shared key credentials for hello Batch account.</span></span> <span data-ttu-id="d1241-362">同樣地，tooaccess hello 儲存體帳戶連結 toohello 批次帳戶，您可以為環境變數傳遞 hello 儲存體帳戶名稱和 hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="d1241-362">Likewise, tooaccess hello storage account that is linked toohello Batch account, you can pass hello storage account name and hello storage account key as environment variables.</span></span>

### <a name="pass-parameters-toohello-job-manager-template"></a><span data-ttu-id="d1241-363">傳遞參數 toohello 作業管理員範本</span><span class="sxs-lookup"><span data-stu-id="d1241-363">Pass parameters toohello Job Manager template</span></span>
<span data-ttu-id="d1241-364">在許多情況下，它有用 toopass 每個作業參數 toohello 作業管理員工作，可能是 toocontrol hello 工作分割程序或 tooconfigure hello 工作 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="d1241-364">In many cases, it's useful toopass per-job parameters toohello job manager task, either toocontrol hello job splitting process or tooconfigure hello tasks for hello job.</span></span> <span data-ttu-id="d1241-365">您可以上傳 parameters.json 稱為 hello 作業管理員工作的資源檔的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="d1241-365">You can do this by uploading a JSON file named parameters.json as a resource file for hello job manager task.</span></span> <span data-ttu-id="d1241-366">hello 參數可供在 hello `JobSplitter._parameters` hello 作業管理員範本中的欄位。</span><span class="sxs-lookup"><span data-stu-id="d1241-366">hello parameters can then become available in hello `JobSplitter._parameters` field in hello Job Manager template.</span></span>

> [!NOTE]
> <span data-ttu-id="d1241-367">hello 內建的參數處理常式支援只有字串的字串字典。</span><span class="sxs-lookup"><span data-stu-id="d1241-367">hello built-in parameter handler supports only string-to-string dictionaries.</span></span> <span data-ttu-id="d1241-368">如果您想 toopass 複雜 JSON 值做為參數值時，您將需要 toopass 這些字串的形式和剖析它們在 hello 作業分隔器，或修改 hello framework`Configuration.GetJobParameters`方法。</span><span class="sxs-lookup"><span data-stu-id="d1241-368">If you want toopass complex JSON values as parameter values, you will need toopass these as strings and parse them in hello job splitter, or modify hello framework's `Configuration.GetJobParameters` method.</span></span>
> 
> 

### <a name="pass-parameters-toohello-task-processor-template"></a><span data-ttu-id="d1241-369">傳遞參數 toohello 處理器工作範本</span><span class="sxs-lookup"><span data-stu-id="d1241-369">Pass parameters toohello Task Processor template</span></span>
<span data-ttu-id="d1241-370">您也可以傳遞參數 tooindividual 工作使用 hello 工作處理器樣板實作。</span><span class="sxs-lookup"><span data-stu-id="d1241-370">You can also pass parameters tooindividual tasks implemented using hello Task Processor template.</span></span> <span data-ttu-id="d1241-371">就像 hello 作業管理員範本，與 hello 工作處理器範本會尋找名為</span><span class="sxs-lookup"><span data-stu-id="d1241-371">Just as with hello job manager template, hello task processor template looks for a resource file named</span></span>

<span data-ttu-id="d1241-372">parameters.json 和如果找到它載入為 hello 參數字典。</span><span class="sxs-lookup"><span data-stu-id="d1241-372">parameters.json, and if found it loads it as hello parameters dictionary.</span></span> <span data-ttu-id="d1241-373">有幾個選項的方式 toopass 參數 toohello 工作處理器工作：</span><span class="sxs-lookup"><span data-stu-id="d1241-373">There are a couple of options for how toopass parameters toohello task processor tasks:</span></span>

* <span data-ttu-id="d1241-374">重複使用 JSON 的 hello 作業參數。</span><span class="sxs-lookup"><span data-stu-id="d1241-374">Reuse hello job parameters JSON.</span></span> <span data-ttu-id="d1241-375">這適用於 hello 參數可用作業範圍 （適用於範例中，呈現高度和寬度） 的情況。</span><span class="sxs-lookup"><span data-stu-id="d1241-375">This works well if hello only parameters are job-wide ones (for example, a render height and width).</span></span> <span data-ttu-id="d1241-376">toodo，建立時 CloudTask hello 作業分隔器中，新增參考 toohello parameters.json 資源檔案物件從 hello 作業管理員工作的 ResourceFiles (`JobSplitter._jobManagerTask.ResourceFiles`) toohello CloudTask ResourceFiles 集合。</span><span class="sxs-lookup"><span data-stu-id="d1241-376">toodo this, when creating a CloudTask in hello job splitter, add a reference toohello parameters.json resource file object from hello job manager task's ResourceFiles (`JobSplitter._jobManagerTask.ResourceFiles`) toohello CloudTask's ResourceFiles collection.</span></span>
* <span data-ttu-id="d1241-377">產生並上傳工作特有 parameters.json 文件一部分的分隔器執行作業，以及參考該 hello 工作的資源檔案集合中的 blob。</span><span class="sxs-lookup"><span data-stu-id="d1241-377">Generate and upload a task-specific parameters.json document as part of job splitter execution, and reference that blob in hello task's resource files collection.</span></span> <span data-ttu-id="d1241-378">如果不同的工作有不同的參數，就必須這麼做。</span><span class="sxs-lookup"><span data-stu-id="d1241-378">This is necessary if different tasks have different parameters.</span></span> <span data-ttu-id="d1241-379">範例可能是其中 hello 框架索引時，會當做參數傳遞 toohello 工作的 3D 轉譯案例。</span><span class="sxs-lookup"><span data-stu-id="d1241-379">An example might be a 3D rendering scenario where hello frame index is passed toohello task as a parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="d1241-380">hello 內建的參數處理常式支援只有字串的字串字典。</span><span class="sxs-lookup"><span data-stu-id="d1241-380">hello built-in parameter handler supports only string-to-string dictionaries.</span></span> <span data-ttu-id="d1241-381">如果您想 toopass 複雜 JSON 值做為參數值時，您將需要 toopass 這些字串的形式和剖析它們在 hello 工作處理器，或修改 hello framework`Configuration.GetTaskParameters`方法。</span><span class="sxs-lookup"><span data-stu-id="d1241-381">If you want toopass complex JSON values as parameter values, you will need toopass these as strings and parse them in hello task processor, or modify hello framework's `Configuration.GetTaskParameters` method.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d1241-382">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1241-382">Next steps</span></span>
### <a name="persist-job-and-task-output-tooazure-storage"></a><span data-ttu-id="d1241-383">保存工作和工作輸出 tooAzure 儲存體</span><span class="sxs-lookup"><span data-stu-id="d1241-383">Persist job and task output tooAzure Storage</span></span>
<span data-ttu-id="d1241-384">開發 Batch 解決方案時的另一個實用工具是 [Azure Batch 檔案慣例][nuget_package]。</span><span class="sxs-lookup"><span data-stu-id="d1241-384">Another helpful tool in Batch solution development is [Azure Batch File Conventions][nuget_package].</span></span> <span data-ttu-id="d1241-385">使用這個.NET 類別庫 （目前處於預覽階段） 在批次.NET 應用程式 tooeasily 存放區，並擷取工作輸出 tooand 從 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="d1241-385">Use this .NET class library (currently in preview) in your Batch .NET applications tooeasily store and retrieve task outputs tooand from Azure Storage.</span></span> <span data-ttu-id="d1241-386">[保存 Azure 批次作業和工作的輸出](batch-task-output.md)包含 hello 程式庫和其使用方式的完整討論。</span><span class="sxs-lookup"><span data-stu-id="d1241-386">[Persist Azure Batch job and task output](batch-task-output.md) contains a full discussion of hello library and its usage.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="d1241-387">Batch 論壇</span><span class="sxs-lookup"><span data-stu-id="d1241-387">Batch Forum</span></span>
<span data-ttu-id="d1241-388">hello [Azure Batch 論壇][ forum] MSDN 上會很大的放置 toodiscuss 批次，並詢問 hello 服務有關的問題。</span><span class="sxs-lookup"><span data-stu-id="d1241-388">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="d1241-389">請前去查看很有幫助的「便利貼」文章，在建立 Batch 解決方案時，出現問題就張貼。</span><span class="sxs-lookup"><span data-stu-id="d1241-389">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[net_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobmanagertask.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[process_exitcode]: https://msdn.microsoft.com/library/system.diagnostics.process.exitcode.aspx
[vs_gallery]: https://visualstudiogallery.msdn.microsoft.com/
[vs_gallery_templates]: https://go.microsoft.com/fwlink/?linkid=820714
[vs_find_use_ext]: https://msdn.microsoft.com/library/dd293638.aspx

[diagram01]: ./media/batch-visual-studio-templates/diagram01.png
[solution_explorer01]: ./media/batch-visual-studio-templates/solution_explorer01.png
[solution_explorer02]: ./media/batch-visual-studio-templates/solution_explorer02.png
