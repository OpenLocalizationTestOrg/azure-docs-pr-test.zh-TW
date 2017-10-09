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
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a>使用媒體服務 .NET SDK 管理資產和相關的實體
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-manage-entities.md)
> * [REST](media-services-rest-manage-entities.md)
> 
> 

本主題說明如何 toomanage Azure Media Services.NET 的實體。 

>[!NOTE]
> 啟動年 4 月 1，2017，超過 90 天您帳戶中的任何工作記錄將會自動刪除，以及其相關聯的工作記錄，即使 hello 的總記錄數低於 hello 配額上限。 例如，在 2017 年 4 月 1 日，您帳戶中任何在 2016 年 12 月 31 日以前的作業記錄將會自動刪除。 如果您需要 tooarchive hello 作業/工作資訊時，您可以使用本主題中所述的 hello 程式碼。

## <a name="prerequisites"></a>必要條件

設定您的開發環境，並填入 hello 與連接資訊的 app.config 檔案中所述[與.NET 的 Media Services 開發](media-services-dotnet-how-to-use.md)。 

## <a name="get-an-asset-reference"></a>取得資產參考
常見的工作是 tooget Media Services 中的參考 tooan 現有資產。 hello 下列程式碼範例示範如何取得資產參考從 hello 資產集合 hello 伺服器上的內容物件，請根據下列程式碼範例會使用資產識別碼 hello Linq 查詢 tooget 參考 tooan 現有 IAsset 物件。

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

## <a name="list-all-assets"></a>列出所有資產
當您有儲存體中的資產的 hello 數目增加時，很有幫助 toolist 資產。 hello，下列程式碼範例示範如何透過 tooiterate hello 資產 hello 伺服器內容物件的集合。 每個資產 hello 程式碼範例也會將其屬性值 toohello 主控台部分。 例如，每個資產可以包含多個媒體檔案。 hello 程式碼範例會寫出與每個資產相關聯的所有檔案。

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

## <a name="get-a-job-reference"></a>取得工作參考

當您使用處理媒體服務程式碼中的工作時，您通常需要的 tooget 參考 tooan 現有的工作根據識別碼 hello，下列程式碼範例示範 tooget 參考 tooan IJob 從 hello 作業集合的物件。

您可能需要長時間執行編碼工作，在啟動時的 tooget 工作參考，而且需要 toocheck hello 作業狀態的執行緒上。 在這種情況下，當 hello 方法傳回的執行緒，您需要 tooretrieve 重新整理的參考 tooa 作業。

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

## <a name="list-jobs-and-assets"></a>列出工作和資產
相關的重要工作是 toolist 資產及其相關的工作，在 Media Services。 hello 下列程式碼範例會示範如何 toolist 每個 IJob 物件，然後為每個工作中，它會顯示 hello 作業、 所有相關的工作、 所有輸入的資產相關的屬性和所有輸出資產。 在此範例中的 hello 程式碼可用於許多其他工作。 比方說，如果您想從一個或多個先前執行的編碼工作 toolist hello 輸出資產，此程式碼將示範如何 tooaccess hello 輸出資產。 當您參考 tooan 輸出資產時，可以再下載或提供 Url 所傳遞 hello 內容 tooother 使用者或應用程式。 

如需傳遞資產選項的詳細資訊，請參閱[hello Media Services SDK for.NET 傳遞資產](media-services-deliver-streaming-content.md)。

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

## <a name="list-all-access-policies"></a>列出所有存取原則
在媒體服務中，您可以定義資產或其檔案的存取原則。 存取原則都會定義 hello 檔案或資產 （何種存取和 hello 持續時間） 的權限。 在您的媒體服務程式碼中，通常會藉由建立 IAccessPolicy 物件，然後將其與現有資產產生關聯，來定義存取原則。 然後您會建立 Locator 物件，這可讓您直接存取 tooassets Media Services 中。 本文件系列所附的 hello Visual Studio 專案包含程式碼範例會顯示如何 toocreate 並指派存取原則和定位器 tooassets。

hello 下列程式碼範例顯示如何 toolist 所有存取原則在 hello 伺服器，並顯示 hello 權限類型的每個相關聯。 另一個實用的方式 tooview 存取原則是 toolist hello 伺服器上的所有 Locator 物件，然後針對每個定位器，您可以列出其相關聯的存取原則使用它的 AccessPolicy 屬性。

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
    
## <a name="limit-access-policies"></a>限制存取原則 

>[!NOTE]
> 對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。 您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。 

例如，您可以建立一組泛用的原則，以下列程式碼，只會執行一次應用程式中的 hello。 您可以記錄識別碼 tooa 記錄檔，以供稍後使用：

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

然後，您可以使用現有 Id 如下的程式碼中的 hello:

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

## <a name="list-all-locators"></a>列出所有定位器
定位器是提供直接路徑 tooaccess 資產，以及權限 toohello 資產 hello 定位器相關的存取原則所定義的 URL。 每個資產在其定位器屬性上可以有與其相關聯的 ILocator 物件的集合。 hello 伺服器內容也有包含所有定位器的定位器集合。

hello 下列程式碼範例會列出 hello 伺服器上所有的定位器。 針對每個定位器，它會顯示 hello 識別碼 hello 相關的資產和存取原則。 它也會顯示 hello 類型權限、 hello 到期日，以及 hello 完整路徑 toohello 資產。

請注意，定位器路徑 tooan 資產只有基底 URL toohello 資產。 toocreate 直接路徑 tooindividual 檔案，使用者或應用程式瀏覽到，您的程式碼必須加入 hello 特定檔案路徑 toohello 定位器路徑。 如需有關如何 toodo，請參閱 hello 主題[hello Media Services SDK for.NET 傳遞資產](media-services-deliver-streaming-content.md)。

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

## <a name="enumerating-through-large-collections-of-entities"></a>透過實體的大型集合列舉
當查詢實體，就會限制為 1000年因為公用 REST v2 限制查詢結果 too1000 結果一次傳回的實體。 您需要 toouse Skip 和 Take 時透過大型實體集合的列舉。 

hello 遵循 hello 提供 Media Services 帳戶中的所有 hello 工作函式執行迴圈。 媒體服務會傳回工作集合中的 1000 個工作。 hello 函式會略過的使用，並確定採取 toomake 所列舉的所有工作 （如果您的帳戶中有超過 1000 個工作）。

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

## <a name="delete-an-asset"></a>刪除資產
下列範例中的 hello 刪除資產。

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a>刪除工作
toodelete 作業，您必須檢查 hello 作業的狀態 hello hello 狀態屬性中所示。 可以刪除已完成或已取消的工作，而其他某些狀態，例如已佇列、已排程或處理中的工作，必須先取消，然後才能刪除。

hello 下列程式碼範例示範用於檢查工作狀態，並將刪除 已完成或取消 hello 狀態時刪除作業的方法。 此程式碼取決於 hello 前一節中本主題適用於取得參考 tooa 作業： 取得作業的參考。

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


## <a name="delete-an-access-policy"></a>刪除存取原則
hello 下列程式碼範例示範如何 tooget 以參考 tooan 存取原則為基礎原則識別碼，然後再 toodelete hello 原則。

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



## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

