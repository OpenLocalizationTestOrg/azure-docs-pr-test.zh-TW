---
title: "工作進度 aaaMonitor 使用.NET"
description: "了解如何 toouse 事件處理常式程式碼 tootrack 作業進度，並將狀態更新傳送。 hello 程式碼範例以 C# 撰寫，並使用 hello Media Services SDK for.NET。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee720ed6-8ce5-4434-b6d6-4df71fca224e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 530aa1d78437cd7c41b4d9a895f9a0e9de0ad49d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-job-progress-using-net"></a><span data-ttu-id="d29a6-104">使用 .NET 監視工作進度</span><span class="sxs-lookup"><span data-stu-id="d29a6-104">Monitor Job Progress using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d29a6-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="d29a6-105">Portal</span></span>](media-services-portal-check-job-progress.md)
> * [<span data-ttu-id="d29a6-106">.NET</span><span class="sxs-lookup"><span data-stu-id="d29a6-106">.NET</span></span>](media-services-check-job-progress.md)
> * [<span data-ttu-id="d29a6-107">REST</span><span class="sxs-lookup"><span data-stu-id="d29a6-107">REST</span></span>](media-services-rest-check-job-progress.md)
> 
> 

<span data-ttu-id="d29a6-108">當您執行工作時，通常會需要方式 tootrack 工作進度。</span><span class="sxs-lookup"><span data-stu-id="d29a6-108">When you run jobs, you often require a way tootrack job progress.</span></span> <span data-ttu-id="d29a6-109">您可以檢查 hello 進度藉由定義 StateChanged 事件處理常式 （如本主題中所述），或使用 Azure 佇列儲存體 toomonitor Media Services 工作通知 (如所述[這](media-services-dotnet-check-job-progress-with-queues.md)主題)。</span><span class="sxs-lookup"><span data-stu-id="d29a6-109">You can check hello progress by defining a StateChanged event handler (as described in this topic) or using Azure Queue storage toomonitor Media Services job notifications (as described in [this](media-services-dotnet-check-job-progress-with-queues.md) topic).</span></span>

## <a name="define-statechanged-event-handler-toomonitor-job-progress"></a><span data-ttu-id="d29a6-110">定義 StateChanged 事件處理常式 toomonitor 工作進度</span><span class="sxs-lookup"><span data-stu-id="d29a6-110">Define StateChanged event handler toomonitor job progress</span></span>
<span data-ttu-id="d29a6-111">下列程式碼範例的 hello 定義 hello StateChanged 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="d29a6-111">hello following code example defines hello StateChanged event handler.</span></span> <span data-ttu-id="d29a6-112">這個事件處理常式會追蹤工作進度，並提供更新的狀態，視 hello 狀態而定。</span><span class="sxs-lookup"><span data-stu-id="d29a6-112">This event handler tracks job progress and provides updated status, depending on hello state.</span></span> <span data-ttu-id="d29a6-113">hello 程式碼也會定義 hello LogJobStop 方法。</span><span class="sxs-lookup"><span data-stu-id="d29a6-113">hello code also defines hello LogJobStop method.</span></span> <span data-ttu-id="d29a6-114">此協助程式方法會記錄錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d29a6-114">This helper method logs error details.</span></span>

    private static void StateChanged(object sender, JobStateChangedEventArgs e)
    {
        Console.WriteLine("Job state changed event:");
        Console.WriteLine("  Previous state: " + e.PreviousState);
        Console.WriteLine("  Current state: " + e.CurrentState);

        switch (e.CurrentState)
        {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("********************");
                Console.WriteLine("Job is finished.");
                Console.WriteLine("Please wait while local tasks or downloads complete...");
                Console.WriteLine("********************");
                Console.WriteLine();
                Console.WriteLine();
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:
                // Cast sender as a job.
                IJob job = (IJob)sender;
                // Display or log error details as needed.
                LogJobStop(job.Id);
                break;
            default:
                break;
        }
    }

    private static void LogJobStop(string jobId)
    {
        StringBuilder builder = new StringBuilder();
        IJob job = GetJob(jobId);

        builder.AppendLine("\nThe job stopped due toocancellation or an error.");
        builder.AppendLine("***************************");
        builder.AppendLine("Job ID: " + job.Id);
        builder.AppendLine("Job Name: " + job.Name);
        builder.AppendLine("Job State: " + job.State.ToString());
        builder.AppendLine("Job started (server UTC time): " + job.StartTime.ToString());
        builder.AppendLine("Media Services account name: " + _accountName);
        builder.AppendLine("Media Services account location: " + _accountLocation);
        // Log job errors if they exist.  
        if (job.State == JobState.Error)
        {
            builder.Append("Error Details: \n");
            foreach (ITask task in job.Tasks)
            {
                foreach (ErrorDetail detail in task.ErrorDetails)
                {
                    builder.AppendLine("  Task Id: " + task.Id);
                    builder.AppendLine("    Error Code: " + detail.Code);
                    builder.AppendLine("    Error Message: " + detail.Message + "\n");
                }
            }
        }
        builder.AppendLine("***************************\n");
        // Write hello output tooa local file and toohello console. hello template 
        // for an error output file is:  JobStop-{JobId}.txt
        string outputFile = _outputFilesFolder + @"\JobStop-" + JobIdAsFileName(job.Id) + ".txt";
        WriteToFile(outputFile, builder.ToString());
        Console.Write(builder.ToString());
    }

    private static string JobIdAsFileName(string jobID)
    {
        return jobID.Replace(":", "_");
    }



## <a name="next-step"></a><span data-ttu-id="d29a6-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d29a6-115">Next step</span></span>
<span data-ttu-id="d29a6-116">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="d29a6-116">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d29a6-117">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="d29a6-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

