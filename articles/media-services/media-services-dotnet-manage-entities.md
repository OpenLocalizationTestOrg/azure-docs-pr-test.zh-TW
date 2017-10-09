---
title: "aaaManaging 資產及使用媒體服務.NET SDK 的相關實體"
description: "了解如何 toomanage 資產與相關的實體與 hello Media Services SDK for.NET。"
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1bd8fd42-7306-463d-bfe5-f642802f1906
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 59a8543ffc6f7f30da2c67a6fcae09bc46da7a52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a><span data-ttu-id="de9a4-103">使用媒體服務 .NET SDK 管理資產和相關的實體</span><span class="sxs-lookup"><span data-stu-id="de9a4-103">Managing Assets and Related Entities with Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="de9a4-104">.NET</span><span class="sxs-lookup"><span data-stu-id="de9a4-104">.NET</span></span>](media-services-dotnet-manage-entities.md)
> * [<span data-ttu-id="de9a4-105">REST</span><span class="sxs-lookup"><span data-stu-id="de9a4-105">REST</span></span>](media-services-rest-manage-entities.md)
> 
> 

<span data-ttu-id="de9a4-106">本主題說明如何 toomanage Azure Media Services.NET 的實體。</span><span class="sxs-lookup"><span data-stu-id="de9a4-106">This topic shows how toomanage Azure Media Services entities with .NET.</span></span> 

>[!NOTE]
> <span data-ttu-id="de9a4-107">啟動年 4 月 1，2017，超過 90 天您帳戶中的任何工作記錄將會自動刪除，以及其相關聯的工作記錄，即使 hello 的總記錄數低於 hello 配額上限。</span><span class="sxs-lookup"><span data-stu-id="de9a4-107">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="de9a4-108">例如，在 2017 年 4 月 1 日，您帳戶中任何在 2016 年 12 月 31 日以前的作業記錄將會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="de9a4-108">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="de9a4-109">如果您需要 tooarchive hello 作業/工作資訊時，您可以使用本主題中所述的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="de9a4-109">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de9a4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="de9a4-110">Prerequisites</span></span>

<span data-ttu-id="de9a4-111">設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="de9a4-111">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="get-an-asset-reference"></a><span data-ttu-id="de9a4-112">取得資產參考</span><span class="sxs-lookup"><span data-stu-id="de9a4-112">Get an Asset Reference</span></span>
<span data-ttu-id="de9a4-113">常見的工作是 tooget Media Services 中的參考 tooan 現有資產。</span><span class="sxs-lookup"><span data-stu-id="de9a4-113">A frequent task is tooget a reference tooan existing asset in Media Services.</span></span> <span data-ttu-id="de9a4-114">hello 下列程式碼範例示範如何取得資產參考從 hello 資產集合 hello 伺服器上的內容物件，請根據下列程式碼範例會使用資產識別碼 hello Linq 查詢 tooget 參考 tooan 現有 IAsset 物件。</span><span class="sxs-lookup"><span data-stu-id="de9a4-114">hello following code example shows how you can get an asset reference from hello Assets collection on hello server context object, based on an asset Id. hello following code example uses a Linq query tooget a reference tooan existing IAsset object.</span></span>

    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query tooget an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference hello asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }

## <a name="list-all-assets"></a><span data-ttu-id="de9a4-115">列出所有資產</span><span class="sxs-lookup"><span data-stu-id="de9a4-115">List All Assets</span></span>
<span data-ttu-id="de9a4-116">當您有儲存體中的資產的 hello 數目增加時，很有幫助 toolist 資產。</span><span class="sxs-lookup"><span data-stu-id="de9a4-116">As hello number of assets you have in storage grows, it is helpful toolist your assets.</span></span> <span data-ttu-id="de9a4-117">hello，下列程式碼範例示範如何透過 tooiterate hello 資產 hello 伺服器內容物件的集合。</span><span class="sxs-lookup"><span data-stu-id="de9a4-117">hello following code example shows how tooiterate through hello Assets collection on hello server context object.</span></span> <span data-ttu-id="de9a4-118">每個資產 hello 程式碼範例也會將其屬性值 toohello 主控台部分。</span><span class="sxs-lookup"><span data-stu-id="de9a4-118">With each asset, hello code example also writes some of its property values toohello console.</span></span> <span data-ttu-id="de9a4-119">例如，每個資產可以包含多個媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="de9a4-119">For example, each asset can contain many media files.</span></span> <span data-ttu-id="de9a4-120">hello 程式碼範例會寫出與每個資產相關聯的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="de9a4-120">hello code example writes out all files associated with each asset.</span></span>

    static void ListAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display hello collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display hello files associated with each asset. 
            foreach (IAssetFile fileItem in asset.AssetFiles)
            {
                builder.AppendLine("Name: " + fileItem.Name);
                builder.AppendLine("Size: " + fileItem.ContentFileSize);
                builder.AppendLine("==============");
            }
        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="get-a-job-reference"></a><span data-ttu-id="de9a4-121">取得工作參考</span><span class="sxs-lookup"><span data-stu-id="de9a4-121">Get a Job Reference</span></span>

<span data-ttu-id="de9a4-122">當您使用處理媒體服務程式碼中的工作時，您通常需要的 tooget 參考 tooan 現有的工作根據識別碼 hello，下列程式碼範例示範 tooget 參考 tooan IJob 從 hello 作業集合的物件。</span><span class="sxs-lookup"><span data-stu-id="de9a4-122">When you work with processing tasks in Media Services code, you often need tooget a reference tooan existing job based on an Id. hello following code example shows how tooget a reference tooan IJob object from hello Jobs collection.</span></span>

<span data-ttu-id="de9a4-123">您可能需要長時間執行編碼工作，在啟動時的 tooget 工作參考，而且需要 toocheck hello 作業狀態的執行緒上。</span><span class="sxs-lookup"><span data-stu-id="de9a4-123">You may need tooget a job reference when starting a long-running encoding job, and need toocheck hello job status on a thread.</span></span> <span data-ttu-id="de9a4-124">在這種情況下，當 hello 方法傳回的執行緒，您需要 tooretrieve 重新整理的參考 tooa 作業。</span><span class="sxs-lookup"><span data-stu-id="de9a4-124">In cases like this, when hello method returns from a thread, you need tooretrieve a refreshed reference tooa job.</span></span>

    static IJob GetJob(string jobId)
    {
        // Use a Linq select query tooget an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return hello job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }

## <a name="list-jobs-and-assets"></a><span data-ttu-id="de9a4-125">列出工作和資產</span><span class="sxs-lookup"><span data-stu-id="de9a4-125">List Jobs and Assets</span></span>
<span data-ttu-id="de9a4-126">相關的重要工作是 toolist 資產及其相關的工作，在 Media Services。</span><span class="sxs-lookup"><span data-stu-id="de9a4-126">An important related task is toolist assets with their associated job in Media Services.</span></span> <span data-ttu-id="de9a4-127">hello 下列程式碼範例會示範如何 toolist 每個 IJob 物件，然後為每個工作中，它會顯示 hello 作業、 所有相關的工作、 所有輸入的資產相關的屬性和所有輸出資產。</span><span class="sxs-lookup"><span data-stu-id="de9a4-127">hello following code example shows you how toolist each IJob object, and then for each job, it displays properties about hello job, all related tasks, all input assets, and all output assets.</span></span> <span data-ttu-id="de9a4-128">在此範例中的 hello 程式碼可用於許多其他工作。</span><span class="sxs-lookup"><span data-stu-id="de9a4-128">hello code in this example can be useful for numerous other tasks.</span></span> <span data-ttu-id="de9a4-129">比方說，如果您想從一個或多個先前執行的編碼工作 toolist hello 輸出資產，此程式碼將示範如何 tooaccess hello 輸出資產。</span><span class="sxs-lookup"><span data-stu-id="de9a4-129">For example, if you want toolist hello output assets from one or more encoding jobs that you ran previously, this code shows how tooaccess hello output assets.</span></span> <span data-ttu-id="de9a4-130">當您參考 tooan 輸出資產時，可以再下載或提供 Url 所傳遞 hello 內容 tooother 使用者或應用程式。</span><span class="sxs-lookup"><span data-stu-id="de9a4-130">When you have a reference tooan output asset, you can then deliver hello content tooother users or applications by downloading it, or providing URLs.</span></span> 

<span data-ttu-id="de9a4-131">如需傳遞資產選項的詳細資訊，請參閱[hello Media Services SDK for.NET 傳遞資產](media-services-deliver-streaming-content.md)。</span><span class="sxs-lookup"><span data-stu-id="de9a4-131">For more information on options for delivering assets, see [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

    // List all jobs on hello server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display hello collection of jobs on hello server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display hello associated tasks (a job  
            // has one or more tasks). 
            builder.AppendLine("******TASKS*******");
            foreach (ITask task in job.Tasks)
            {
                builder.AppendLine("Task Id: " + task.Id);
                builder.AppendLine("Name: " + task.Name);
                builder.AppendLine("Progress: " + task.Progress);
                builder.AppendLine("Configuration: " + task.Configuration);
                if (task.ErrorDetails != null)
                {
                    builder.AppendLine("Error: " + task.ErrorDetails);
                }
                builder.AppendLine("==============");
            }

            // For each job, display hello list of input media assets.
            builder.AppendLine("******JOB INPUT MEDIA ASSETS*******");
            foreach (IAsset inputAsset in job.InputMediaAssets)
            {

                if (inputAsset != null)
                {
                    builder.AppendLine("Input Asset Id: " + inputAsset.Id);
                    builder.AppendLine("Name: " + inputAsset.Name);
                    builder.AppendLine("==============");
                }
            }

            // For each job, display hello list of output media assets.
            builder.AppendLine("******JOB OUTPUT MEDIA ASSETS*******");
            foreach (IAsset theAsset in job.OutputMediaAssets)
            {
                if (theAsset != null)
                {
                    builder.AppendLine("Output Asset Id: " + theAsset.Id);
                    builder.AppendLine("Name: " + theAsset.Name);
                    builder.AppendLine("==============");
                }
            }

        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="list-all-access-policies"></a><span data-ttu-id="de9a4-132">列出所有存取原則</span><span class="sxs-lookup"><span data-stu-id="de9a4-132">List all Access Policies</span></span>
<span data-ttu-id="de9a4-133">在媒體服務中，您可以定義資產或其檔案的存取原則。</span><span class="sxs-lookup"><span data-stu-id="de9a4-133">In Media Services, you can define an access policy on an asset or its files.</span></span> <span data-ttu-id="de9a4-134">存取原則都會定義 hello 檔案或資產 （何種存取和 hello 持續時間） 的權限。</span><span class="sxs-lookup"><span data-stu-id="de9a4-134">An access policy defines hello permissions for a file or an asset (what type of access, and hello duration).</span></span> <span data-ttu-id="de9a4-135">在您的媒體服務程式碼中，通常會藉由建立 IAccessPolicy 物件，然後將其與現有資產產生關聯，來定義存取原則。</span><span class="sxs-lookup"><span data-stu-id="de9a4-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span></span> <span data-ttu-id="de9a4-136">然後您會建立 Locator 物件，這可讓您直接存取 tooassets Media Services 中。</span><span class="sxs-lookup"><span data-stu-id="de9a4-136">Then you create a ILocator object, which lets you provide direct access tooassets in Media Services.</span></span> <span data-ttu-id="de9a4-137">本文件系列所附的 hello Visual Studio 專案包含程式碼範例會顯示如何 toocreate 並指派存取原則和定位器 tooassets。</span><span class="sxs-lookup"><span data-stu-id="de9a4-137">hello Visual Studio project that accompanies this documentation series contains several code examples that show how toocreate and assign access policies and locators tooassets.</span></span>

<span data-ttu-id="de9a4-138">hello 下列程式碼範例顯示如何 toolist 所有存取原則在 hello 伺服器，並顯示 hello 權限類型的每個相關聯。</span><span class="sxs-lookup"><span data-stu-id="de9a4-138">hello following code example shows how toolist all access policies on hello server, and shows hello type of permissions associated with each.</span></span> <span data-ttu-id="de9a4-139">另一個實用的方式 tooview 存取原則是 toolist hello 伺服器上的所有 Locator 物件，然後針對每個定位器，您可以列出其相關聯的存取原則使用它的 AccessPolicy 屬性。</span><span class="sxs-lookup"><span data-stu-id="de9a4-139">Another useful way tooview access policies is toolist all ILocator objects on hello server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span></span>

    static void ListAllPolicies()
    {
        foreach (IAccessPolicy policy in _context.AccessPolicies)
        {
            Console.WriteLine("");
            Console.WriteLine("Name:  " + policy.Name);
            Console.WriteLine("ID:  " + policy.Id);
            Console.WriteLine("Permissions: " + policy.Permissions);
            Console.WriteLine("==============");

        }
    }
    
## <a name="limit-access-policies"></a><span data-ttu-id="de9a4-140">限制存取原則</span><span class="sxs-lookup"><span data-stu-id="de9a4-140">Limit Access Policies</span></span> 

>[!NOTE]
> <span data-ttu-id="de9a4-141">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="de9a4-141">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="de9a4-142">您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。</span><span class="sxs-lookup"><span data-stu-id="de9a4-142">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> 

<span data-ttu-id="de9a4-143">例如，您可以建立一組泛用的原則，以下列程式碼，只會執行一次應用程式中的 hello。</span><span class="sxs-lookup"><span data-stu-id="de9a4-143">For example, you can create a generic set of policies with hello following code that would only run one time in your application.</span></span> <span data-ttu-id="de9a4-144">您可以記錄識別碼 tooa 記錄檔，以供稍後使用：</span><span class="sxs-lookup"><span data-stu-id="de9a4-144">You can log IDs tooa log file for later use:</span></span>

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

<span data-ttu-id="de9a4-145">然後，您可以使用現有 Id 如下的程式碼中的 hello:</span><span class="sxs-lookup"><span data-stu-id="de9a4-145">Then, you can use hello existing IDs in your code like this:</span></span>

    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get hello standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get hello existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("hello locator base path is " + originLocator.BaseUri.ToString());

## <a name="list-all-locators"></a><span data-ttu-id="de9a4-146">列出所有定位器</span><span class="sxs-lookup"><span data-stu-id="de9a4-146">List All Locators</span></span>
<span data-ttu-id="de9a4-147">定位器是提供直接路徑 tooaccess 資產，以及權限 toohello 資產 hello 定位器相關的存取原則所定義的 URL。</span><span class="sxs-lookup"><span data-stu-id="de9a4-147">A locator is a URL that provides a direct path tooaccess an asset, along with permissions toohello asset as defined by hello locator's associated access policy.</span></span> <span data-ttu-id="de9a4-148">每個資產在其定位器屬性上可以有與其相關聯的 ILocator 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="de9a4-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span></span> <span data-ttu-id="de9a4-149">hello 伺服器內容也有包含所有定位器的定位器集合。</span><span class="sxs-lookup"><span data-stu-id="de9a4-149">hello server context also has a Locators collection that contains all locators.</span></span>

<span data-ttu-id="de9a4-150">hello 下列程式碼範例會列出 hello 伺服器上所有的定位器。</span><span class="sxs-lookup"><span data-stu-id="de9a4-150">hello following code example lists all locators on hello server.</span></span> <span data-ttu-id="de9a4-151">針對每個定位器，它會顯示 hello 識別碼 hello 相關的資產和存取原則。</span><span class="sxs-lookup"><span data-stu-id="de9a4-151">For each locator, it shows hello Id for hello related asset and access policy.</span></span> <span data-ttu-id="de9a4-152">它也會顯示 hello 類型權限、 hello 到期日，以及 hello 完整路徑 toohello 資產。</span><span class="sxs-lookup"><span data-stu-id="de9a4-152">It also displays hello type of permissions, hello expiration date, and hello full path toohello asset.</span></span>

<span data-ttu-id="de9a4-153">請注意，定位器路徑 tooan 資產只有基底 URL toohello 資產。</span><span class="sxs-lookup"><span data-stu-id="de9a4-153">Note that a locator path tooan asset is only a base URL toohello asset.</span></span> <span data-ttu-id="de9a4-154">toocreate 直接路徑 tooindividual 檔案，使用者或應用程式瀏覽到，您的程式碼必須加入 hello 特定檔案路徑 toohello 定位器路徑。</span><span class="sxs-lookup"><span data-stu-id="de9a4-154">toocreate a direct path tooindividual files that a user or application could browse to, your code must add hello specific file path toohello locator path.</span></span> <span data-ttu-id="de9a4-155">如需有關如何 toodo，請參閱 hello 主題[hello Media Services SDK for.NET 傳遞資產](media-services-deliver-streaming-content.md)。</span><span class="sxs-lookup"><span data-stu-id="de9a4-155">For more information on how toodo this, see hello topic [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

    static void ListAllLocators()
    {
        foreach (ILocator locator in _context.Locators)
        {
            Console.WriteLine("***********");
            Console.WriteLine("Locator Id: " + locator.Id);
            Console.WriteLine("Locator asset Id: " + locator.AssetId);
            Console.WriteLine("Locator access policy Id: " + locator.AccessPolicyId);
            Console.WriteLine("Access policy permissions: " + locator.AccessPolicy.Permissions);
            Console.WriteLine("Locator expiration: " + locator.ExpirationDateTime);
            // hello locator path is hello base or parent path (with included permissions) tooaccess  
            // hello media content of an asset. toocreate a full URL tooa specific media file, take 
            // hello locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="de9a4-156">透過實體的大型集合列舉</span><span class="sxs-lookup"><span data-stu-id="de9a4-156">Enumerating through large collections of entities</span></span>
<span data-ttu-id="de9a4-157">當查詢實體，就會限制為 1000年因為公用 REST v2 限制查詢結果 too1000 結果一次傳回的實體。</span><span class="sxs-lookup"><span data-stu-id="de9a4-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="de9a4-158">您需要 toouse Skip 和 Take 時透過大型實體集合的列舉。</span><span class="sxs-lookup"><span data-stu-id="de9a4-158">You need toouse Skip and Take when enumerating through large collections of entities.</span></span> 

<span data-ttu-id="de9a4-159">hello 遵循 hello 提供 Media Services 帳戶中的所有 hello 工作函式執行迴圈。</span><span class="sxs-lookup"><span data-stu-id="de9a4-159">hello following function loops through all hello jobs in hello provided Media Services Account.</span></span> <span data-ttu-id="de9a4-160">媒體服務會傳回工作集合中的 1000 個工作。</span><span class="sxs-lookup"><span data-stu-id="de9a4-160">Media Services returns 1000 jobs in Jobs Collection.</span></span> <span data-ttu-id="de9a4-161">hello 函式會略過的使用，並確定採取 toomake 所列舉的所有工作 （如果您的帳戶中有超過 1000 個工作）。</span><span class="sxs-lookup"><span data-stu-id="de9a4-161">hello function makes use of Skip and Take toomake sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span></span>

    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in hello Media Services account
                IQueryable _jobsCollectionQuery = _context.Jobs.Skip(skipSize).Take(batchSize);
                foreach (IJob job in _jobsCollectionQuery)
                {
                    currentBatch++;
                    Console.WriteLine("Processing Job Id:" + job.Id);
                }

                if (currentBatch == batchSize)
                {
                    skipSize += batchSize;
                    currentBatch = 0;
                }
                else
                {
                    break;
                }
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

## <a name="delete-an-asset"></a><span data-ttu-id="de9a4-162">刪除資產</span><span class="sxs-lookup"><span data-stu-id="de9a4-162">Delete an Asset</span></span>
<span data-ttu-id="de9a4-163">下列範例中的 hello 刪除資產。</span><span class="sxs-lookup"><span data-stu-id="de9a4-163">hello following example deletes an asset.</span></span>

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a><span data-ttu-id="de9a4-164">刪除工作</span><span class="sxs-lookup"><span data-stu-id="de9a4-164">Delete a Job</span></span>
<span data-ttu-id="de9a4-165">toodelete 作業，您必須檢查 hello 作業的狀態 hello hello 狀態屬性中所示。</span><span class="sxs-lookup"><span data-stu-id="de9a4-165">toodelete a job, you must check hello state of hello job as indicated in hello State property.</span></span> <span data-ttu-id="de9a4-166">可以刪除已完成或已取消的工作，而其他某些狀態，例如已佇列、已排程或處理中的工作，必須先取消，然後才能刪除。</span><span class="sxs-lookup"><span data-stu-id="de9a4-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span></span>

<span data-ttu-id="de9a4-167">hello 下列程式碼範例示範用於檢查工作狀態，並將刪除 已完成或取消 hello 狀態時刪除作業的方法。</span><span class="sxs-lookup"><span data-stu-id="de9a4-167">hello following code example shows a method for deleting a job by checking job states and then deleting when hello state is finished or canceled.</span></span> <span data-ttu-id="de9a4-168">此程式碼取決於 hello 前一節中本主題適用於取得參考 tooa 作業： 取得作業的參考。</span><span class="sxs-lookup"><span data-stu-id="de9a4-168">This code depends on hello previous section in this topic for getting a reference tooa job: Get a job reference.</span></span>

    static void DeleteJob(string jobId)
    {
        bool jobDeleted = false;

        while (!jobDeleted)
        {
            // Get an updated job reference.  
            IJob job = GetJob(jobId);

            // Check and handle various possible job states. You can 
            // only delete a job whose state is Finished, Error, or Canceled.   
            // You can cancel jobs that are Queued, Scheduled, or Processing,  
            // and then delete after they are canceled.
            switch (job.State)
            {
                case JobState.Finished:
                case JobState.Canceled:
                case JobState.Error:
                    // Job errors should already be logged by polling or event 
                    // handling methods such as CheckJobProgress or StateChanged.
                    // You can also call job.DeleteAsync toodo async deletes.
                    job.Delete();
                    Console.WriteLine("Job has been deleted.");
                    jobDeleted = true;
                    break;
                case JobState.Canceling:
                    Console.WriteLine("Job is cancelling and will be deleted "
                        + "when finished.");
                    Console.WriteLine("Wait while job finishes canceling...");
                    Thread.Sleep(5000);
                    break;
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    job.Cancel();
                    Console.WriteLine("Job is scheduled or processing and will "
                        + "be deleted.");
                    break;
                default:
                    break;
            }

        }
    }


## <a name="delete-an-access-policy"></a><span data-ttu-id="de9a4-169">刪除存取原則</span><span class="sxs-lookup"><span data-stu-id="de9a4-169">Delete an Access Policy</span></span>
<span data-ttu-id="de9a4-170">hello 下列程式碼範例示範如何 tooget 以參考 tooan 存取原則為基礎原則識別碼，然後再 toodelete hello 原則。</span><span class="sxs-lookup"><span data-stu-id="de9a4-170">hello following code example shows how tooget a reference tooan access policy based on a policy Id, and then toodelete hello policy.</span></span>

    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // toodelete a specific access policy, get a reference toohello policy.  
        // based on hello policy Id passed toohello method.
        var policyInstance =
                from p in _context.AccessPolicies
                where p.Id == existingPolicyId
                select p;
        IAccessPolicy policy = policyInstance.FirstOrDefault();

        policy.Delete();

    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="de9a4-171">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="de9a4-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="de9a4-172">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="de9a4-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

