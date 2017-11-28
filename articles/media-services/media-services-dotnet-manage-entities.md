---
title: "使用媒體服務 .NET SDK 管理資產和相關的實體"
description: "深入了解使用 Media Services SDK for .NET 管理資產和相關的實體"
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
ms.openlocfilehash: 5efe16a09808267d0797521f9e1df2b60aec9cbb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a><span data-ttu-id="5ec13-103">使用媒體服務 .NET SDK 管理資產和相關的實體</span><span class="sxs-lookup"><span data-stu-id="5ec13-103">Managing Assets and Related Entities with Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ec13-104">.NET</span><span class="sxs-lookup"><span data-stu-id="5ec13-104">.NET</span></span>](media-services-dotnet-manage-entities.md)
> * [<span data-ttu-id="5ec13-105">REST</span><span class="sxs-lookup"><span data-stu-id="5ec13-105">REST</span></span>](media-services-rest-manage-entities.md)
> 
> 

<span data-ttu-id="5ec13-106">本主題說明如何使用 .NET 管理 Azure 媒體服務實體。</span><span class="sxs-lookup"><span data-stu-id="5ec13-106">This topic shows how to manage Azure Media Services entities with .NET.</span></span> 

>[!NOTE]
> <span data-ttu-id="5ec13-107">從 2017 年 4 月 1 日起，您的帳戶中任何超過 90 天的作業記錄以及其相關工作記錄都會自動刪除，即使記錄總數低於配額上限亦然。</span><span class="sxs-lookup"><span data-stu-id="5ec13-107">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if the total number of records is below the maximum quota.</span></span> <span data-ttu-id="5ec13-108">例如，在 2017 年 4 月 1 日，您帳戶中任何在 2016 年 12 月 31 日以前的作業記錄將會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="5ec13-108">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="5ec13-109">如果您需要封存作業/工作資訊，您可以使用本主題中所述的程式碼。</span><span class="sxs-lookup"><span data-stu-id="5ec13-109">If you need to archive the job/task information, you can use the code described in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ec13-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5ec13-110">Prerequisites</span></span>

<span data-ttu-id="5ec13-111">設定您的開發環境並在 app.config 檔案中填入連線資訊，如[使用 .NET 進行 Media Services 開發](media-services-dotnet-how-to-use.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="5ec13-111">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="get-an-asset-reference"></a><span data-ttu-id="5ec13-112">取得資產參考</span><span class="sxs-lookup"><span data-stu-id="5ec13-112">Get an Asset Reference</span></span>
<span data-ttu-id="5ec13-113">常見的工作是在媒體服務中取得現有資產的參考。</span><span class="sxs-lookup"><span data-stu-id="5ec13-113">A frequent task is to get a reference to an existing asset in Media Services.</span></span> <span data-ttu-id="5ec13-114">下列程式碼範例顯示如何根據資產識別碼，從伺服器內容物件的資產集合取得資產參考。下列程式碼範例會使用 Linq 查詢來取得現有 IAsset 物件的參考。</span><span class="sxs-lookup"><span data-stu-id="5ec13-114">The following code example shows how you can get an asset reference from the Assets collection on the server context object, based on an asset Id. The following code example uses a Linq query to get a reference to an existing IAsset object.</span></span>

    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query to get an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference the asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }

## <a name="list-all-assets"></a><span data-ttu-id="5ec13-115">列出所有資產</span><span class="sxs-lookup"><span data-stu-id="5ec13-115">List All Assets</span></span>
<span data-ttu-id="5ec13-116">當您在儲存體中的資產數目增加時，最好能將資產列出。</span><span class="sxs-lookup"><span data-stu-id="5ec13-116">As the number of assets you have in storage grows, it is helpful to list your assets.</span></span> <span data-ttu-id="5ec13-117">下列程式碼範例顯示如何在伺服器內容物件上逐一查看「資產」集合。</span><span class="sxs-lookup"><span data-stu-id="5ec13-117">The following code example shows how to iterate through the Assets collection on the server context object.</span></span> <span data-ttu-id="5ec13-118">使用各個資產時，程式碼範例也會將它的某些屬性值寫入主控台。</span><span class="sxs-lookup"><span data-stu-id="5ec13-118">With each asset, the code example also writes some of its property values to the console.</span></span> <span data-ttu-id="5ec13-119">例如，每個資產可以包含多個媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="5ec13-119">For example, each asset can contain many media files.</span></span> <span data-ttu-id="5ec13-120">程式碼範例會寫出與每個資產相關聯的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="5ec13-120">The code example writes out all files associated with each asset.</span></span>

    static void ListAssets()
    {
        string waitMessage = "Building the list. This may take a few "
            + "seconds to a few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder to store the list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display the collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display the files associated with each asset. 
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

## <a name="get-a-job-reference"></a><span data-ttu-id="5ec13-121">取得工作參考</span><span class="sxs-lookup"><span data-stu-id="5ec13-121">Get a Job Reference</span></span>

<span data-ttu-id="5ec13-122">當您使用媒體服務程式碼中的處理工作時，您通常需要根據識別碼取得現有工作的參考。下列程式碼範例顯示如何從「工作」集合取得 IJob 物件的參考。</span><span class="sxs-lookup"><span data-stu-id="5ec13-122">When you work with processing tasks in Media Services code, you often need to get a reference to an existing job based on an Id. The following code example shows how to get a reference to an IJob object from the Jobs collection.</span></span>

<span data-ttu-id="5ec13-123">您可能需要在開始長時間執行編碼作業時，取得作業參考，並且需要檢查執行緒上的作業狀態。</span><span class="sxs-lookup"><span data-stu-id="5ec13-123">You may need to get a job reference when starting a long-running encoding job, and need to check the job status on a thread.</span></span> <span data-ttu-id="5ec13-124">在這種情況下，當此方法從執行緒傳回時，您需要擷取作業的重新整理的參考。</span><span class="sxs-lookup"><span data-stu-id="5ec13-124">In cases like this, when the method returns from a thread, you need to retrieve a refreshed reference to a job.</span></span>

    static IJob GetJob(string jobId)
    {
        // Use a Linq select query to get an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return the job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }

## <a name="list-jobs-and-assets"></a><span data-ttu-id="5ec13-125">列出工作和資產</span><span class="sxs-lookup"><span data-stu-id="5ec13-125">List Jobs and Assets</span></span>
<span data-ttu-id="5ec13-126">重要的相關工作是在媒體服務中列出資產及其相關聯的工作。</span><span class="sxs-lookup"><span data-stu-id="5ec13-126">An important related task is to list assets with their associated job in Media Services.</span></span> <span data-ttu-id="5ec13-127">下列程式碼範例會示範如何列出每個 IJob 物件，然後它會針對每個工作，顯示作業的相關屬性、所有相關工作、所有輸入資產，以及所有輸出資產。</span><span class="sxs-lookup"><span data-stu-id="5ec13-127">The following code example shows you how to list each IJob object, and then for each job, it displays properties about the job, all related tasks, all input assets, and all output assets.</span></span> <span data-ttu-id="5ec13-128">此範例中的程式碼可用於許多其他工作。</span><span class="sxs-lookup"><span data-stu-id="5ec13-128">The code in this example can be useful for numerous other tasks.</span></span> <span data-ttu-id="5ec13-129">例如，如果您想要從您先前執行的一或多個編碼工作列出輸出資產，此程式碼會示範如何存取輸出資產。</span><span class="sxs-lookup"><span data-stu-id="5ec13-129">For example, if you want to list the output assets from one or more encoding jobs that you ran previously, this code shows how to access the output assets.</span></span> <span data-ttu-id="5ec13-130">當您有輸出資產的參考時，可以透過下載或提供 URL，將內容傳遞給其他使用者或應用程式。</span><span class="sxs-lookup"><span data-stu-id="5ec13-130">When you have a reference to an output asset, you can then deliver the content to other users or applications by downloading it, or providing URLs.</span></span> 

<span data-ttu-id="5ec13-131">如需傳遞資產之選項的詳細資訊，請參閱 [使用 Media Services SDK for .NET 傳遞資產](media-services-deliver-streaming-content.md)。</span><span class="sxs-lookup"><span data-stu-id="5ec13-131">For more information on options for delivering assets, see [Deliver Assets with the Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

    // List all jobs on the server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building the list. This may take a few "
            + "seconds to a few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder to store the list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display the collection of jobs on the server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display the associated tasks (a job  
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

            // For each job, display the list of input media assets.
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

            // For each job, display the list of output media assets.
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

## <a name="list-all-access-policies"></a><span data-ttu-id="5ec13-132">列出所有存取原則</span><span class="sxs-lookup"><span data-stu-id="5ec13-132">List all Access Policies</span></span>
<span data-ttu-id="5ec13-133">在媒體服務中，您可以定義資產或其檔案的存取原則。</span><span class="sxs-lookup"><span data-stu-id="5ec13-133">In Media Services, you can define an access policy on an asset or its files.</span></span> <span data-ttu-id="5ec13-134">存取原則會定義檔案或資產 (存取的類型和持續時間) 的權限。</span><span class="sxs-lookup"><span data-stu-id="5ec13-134">An access policy defines the permissions for a file or an asset (what type of access, and the duration).</span></span> <span data-ttu-id="5ec13-135">在您的媒體服務程式碼中，通常會藉由建立 IAccessPolicy 物件，然後將其與現有資產產生關聯，來定義存取原則。</span><span class="sxs-lookup"><span data-stu-id="5ec13-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span></span> <span data-ttu-id="5ec13-136">然後您會建立 ILocator 物件，這可讓您直接存取媒體服務中的資產。</span><span class="sxs-lookup"><span data-stu-id="5ec13-136">Then you create a ILocator object, which lets you provide direct access to assets in Media Services.</span></span> <span data-ttu-id="5ec13-137">本文件系列隨附的 Visual Studio 專案包含數個程式碼範例，示範如何建立及指派存取原則和定位器給資產。</span><span class="sxs-lookup"><span data-stu-id="5ec13-137">The Visual Studio project that accompanies this documentation series contains several code examples that show how to create and assign access policies and locators to assets.</span></span>

<span data-ttu-id="5ec13-138">下列程式碼範例顯示如何列出伺服器上的所有存取原則，並顯示每個相關聯的權限的類型。</span><span class="sxs-lookup"><span data-stu-id="5ec13-138">The following code example shows how to list all access policies on the server, and shows the type of permissions associated with each.</span></span> <span data-ttu-id="5ec13-139">檢視存取原則的另一個實用方式，是列出伺服器上的所有 ILocator 物件，然後針對每個定位器，您可以使用其 AccessPolicy 屬性列出其相關聯的存取原則。</span><span class="sxs-lookup"><span data-stu-id="5ec13-139">Another useful way to view access policies is to list all ILocator objects on the server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span></span>

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
    
## <a name="limit-access-policies"></a><span data-ttu-id="5ec13-140">限制存取原則</span><span class="sxs-lookup"><span data-stu-id="5ec13-140">Limit Access Policies</span></span> 

>[!NOTE]
> <span data-ttu-id="5ec13-141">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="5ec13-141">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="5ec13-142">如果您一律使用相同的日期 / 存取權限，例如，要長時間維持就地 (非上載原則) 的定位器原則，您應該使用相同的原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="5ec13-142">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> 

<span data-ttu-id="5ec13-143">例如，您可以使用只會在您應用程式中執行一次的下列程式碼來建立一組標準的原則。</span><span class="sxs-lookup"><span data-stu-id="5ec13-143">For example, you can create a generic set of policies with the following code that would only run one time in your application.</span></span> <span data-ttu-id="5ec13-144">您可以記錄識別碼至記錄檔以供稍後使用︰</span><span class="sxs-lookup"><span data-stu-id="5ec13-144">You can log IDs to a log file for later use:</span></span>

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

<span data-ttu-id="5ec13-145">然後，您可以使用您程式碼中的現有識別碼，就像這樣︰</span><span class="sxs-lookup"><span data-stu-id="5ec13-145">Then, you can use the existing IDs in your code like this:</span></span>

    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get the standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get the existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("The locator base path is " + originLocator.BaseUri.ToString());

## <a name="list-all-locators"></a><span data-ttu-id="5ec13-146">列出所有定位器</span><span class="sxs-lookup"><span data-stu-id="5ec13-146">List All Locators</span></span>
<span data-ttu-id="5ec13-147">定位器是 URL，提供存取資產的直接路徑，以及由定位器相關聯的存取原則所定義之對於資產的權限。</span><span class="sxs-lookup"><span data-stu-id="5ec13-147">A locator is a URL that provides a direct path to access an asset, along with permissions to the asset as defined by the locator's associated access policy.</span></span> <span data-ttu-id="5ec13-148">每個資產在其定位器屬性上可以有與其相關聯的 ILocator 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="5ec13-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span></span> <span data-ttu-id="5ec13-149">伺服器內容也有定位器集合，其中包含所有定位器。</span><span class="sxs-lookup"><span data-stu-id="5ec13-149">The server context also has a Locators collection that contains all locators.</span></span>

<span data-ttu-id="5ec13-150">下列程式碼範例列出伺服器上的所有定位器。</span><span class="sxs-lookup"><span data-stu-id="5ec13-150">The following code example lists all locators on the server.</span></span> <span data-ttu-id="5ec13-151">針對每個定位器，它會顯示相關資產與存取原則的識別碼。</span><span class="sxs-lookup"><span data-stu-id="5ec13-151">For each locator, it shows the Id for the related asset and access policy.</span></span> <span data-ttu-id="5ec13-152">也會顯示資產的權限類型、到期日和完整路徑。</span><span class="sxs-lookup"><span data-stu-id="5ec13-152">It also displays the type of permissions, the expiration date, and the full path to the asset.</span></span>

<span data-ttu-id="5ec13-153">請注意，資產的定位器路徑只是資產的基底 URL。</span><span class="sxs-lookup"><span data-stu-id="5ec13-153">Note that a locator path to an asset is only a base URL to the asset.</span></span> <span data-ttu-id="5ec13-154">若要建立使用者或應用程式可以瀏覽之個別檔案的直接路徑，您的程式碼必須將特定檔案路徑加入至定位器路徑。</span><span class="sxs-lookup"><span data-stu-id="5ec13-154">To create a direct path to individual files that a user or application could browse to, your code must add the specific file path to the locator path.</span></span> <span data-ttu-id="5ec13-155">如需如何執行此動作的詳細資訊，請參閱 [使用 Media Services SDK for .NET 傳遞資產](media-services-deliver-streaming-content.md)主題。</span><span class="sxs-lookup"><span data-stu-id="5ec13-155">For more information on how to do this, see the topic [Deliver Assets with the Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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
            // The locator path is the base or parent path (with included permissions) to access  
            // the media content of an asset. To create a full URL to a specific media file, take 
            // the locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="5ec13-156">透過實體的大型集合列舉</span><span class="sxs-lookup"><span data-stu-id="5ec13-156">Enumerating through large collections of entities</span></span>
<span data-ttu-id="5ec13-157">查詢項目時，有一次最多傳回 1000 個實體的限制，因為公用 REST v2 有 1000 個查詢結果數目的限制。</span><span class="sxs-lookup"><span data-stu-id="5ec13-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results to 1000 results.</span></span> <span data-ttu-id="5ec13-158">透過實體的大型集合列舉時您需要使用 Skip 和 Take。</span><span class="sxs-lookup"><span data-stu-id="5ec13-158">You need to use Skip and Take when enumerating through large collections of entities.</span></span> 

<span data-ttu-id="5ec13-159">下列函式會對「媒體服務帳戶」中提供的所有工作進行迴圈。</span><span class="sxs-lookup"><span data-stu-id="5ec13-159">The following function loops through all the jobs in the provided Media Services Account.</span></span> <span data-ttu-id="5ec13-160">媒體服務會傳回工作集合中的 1000 個工作。</span><span class="sxs-lookup"><span data-stu-id="5ec13-160">Media Services returns 1000 jobs in Jobs Collection.</span></span> <span data-ttu-id="5ec13-161">此函式利用 Skip 和 Take 來確保已列舉所有工作 (以免您帳戶中的工作超過 1000 個)。</span><span class="sxs-lookup"><span data-stu-id="5ec13-161">The function makes use of Skip and Take to make sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span></span>

    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in the Media Services account
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

## <a name="delete-an-asset"></a><span data-ttu-id="5ec13-162">刪除資產</span><span class="sxs-lookup"><span data-stu-id="5ec13-162">Delete an Asset</span></span>
<span data-ttu-id="5ec13-163">下列範例會刪除資產。</span><span class="sxs-lookup"><span data-stu-id="5ec13-163">The following example deletes an asset.</span></span>

    static void DeleteAsset( IAsset asset)
    {
        // delete the asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted the Asset");

    }

## <a name="delete-a-job"></a><span data-ttu-id="5ec13-164">刪除工作</span><span class="sxs-lookup"><span data-stu-id="5ec13-164">Delete a Job</span></span>
<span data-ttu-id="5ec13-165">若要刪除工作，您必須檢查工作的狀態，如 State 屬性所示。</span><span class="sxs-lookup"><span data-stu-id="5ec13-165">To delete a job, you must check the state of the job as indicated in the State property.</span></span> <span data-ttu-id="5ec13-166">可以刪除已完成或已取消的工作，而其他某些狀態，例如已佇列、已排程或處理中的工作，必須先取消，然後才能刪除。</span><span class="sxs-lookup"><span data-stu-id="5ec13-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span></span>

<span data-ttu-id="5ec13-167">下列程式碼範例示範刪除工作的方法，方法是檢查工作狀態，然後於狀態為已完成或已取消時刪除工作。</span><span class="sxs-lookup"><span data-stu-id="5ec13-167">The following code example shows a method for deleting a job by checking job states and then deleting when the state is finished or canceled.</span></span> <span data-ttu-id="5ec13-168">此程式碼相依於本主題中的前一節，以取得工作的參考：取得工作參考。</span><span class="sxs-lookup"><span data-stu-id="5ec13-168">This code depends on the previous section in this topic for getting a reference to a job: Get a job reference.</span></span>

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
                    // You can also call job.DeleteAsync to do async deletes.
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


## <a name="delete-an-access-policy"></a><span data-ttu-id="5ec13-169">刪除存取原則</span><span class="sxs-lookup"><span data-stu-id="5ec13-169">Delete an Access Policy</span></span>
<span data-ttu-id="5ec13-170">下列程式碼範例顯示如何根據原則識別碼，取得存取原則的參考，然後刪除原則。</span><span class="sxs-lookup"><span data-stu-id="5ec13-170">The following code example shows how to get a reference to an access policy based on a policy Id, and then to delete the policy.</span></span>

    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // To delete a specific access policy, get a reference to the policy.  
        // based on the policy Id passed to the method.
        var policyInstance =
                from p in _context.AccessPolicies
                where p.Id == existingPolicyId
                select p;
        IAccessPolicy policy = policyInstance.FirstOrDefault();

        policy.Delete();

    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="5ec13-171">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="5ec13-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5ec13-172">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="5ec13-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

