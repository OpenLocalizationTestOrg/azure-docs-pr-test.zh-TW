---
title: "使用 .NET 監視工作進度"
description: "了解如何使用事件處理常式程式碼來追蹤工作進度及傳送狀態更新。 程式碼範例是以 C# 撰寫，並使用 Media Services SDK for .NET。"
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
ms.openlocfilehash: 851981b291115ba31dc40535f8bcc71cdb475717
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-job-progress-using-net"></a><span data-ttu-id="17963-104">使用 .NET 監視工作進度</span><span class="sxs-lookup"><span data-stu-id="17963-104">Monitor Job Progress using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="17963-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="17963-105">Portal</span></span>](media-services-portal-check-job-progress.md)
> * [<span data-ttu-id="17963-106">.NET</span><span class="sxs-lookup"><span data-stu-id="17963-106">.NET</span></span>](media-services-check-job-progress.md)
> * [<span data-ttu-id="17963-107">REST</span><span class="sxs-lookup"><span data-stu-id="17963-107">REST</span></span>](media-services-rest-check-job-progress.md)
> 
> 

<span data-ttu-id="17963-108">執行作業時，您通常需要設法追蹤作業進度。</span><span class="sxs-lookup"><span data-stu-id="17963-108">When you run jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="17963-109">定義 StateChanged 事件處理常式 (如本主題中所述) 或使用 Azure 佇列儲存體監視媒體服務工作通知 (如 [本主題](media-services-dotnet-check-job-progress-with-queues.md) 中所述)，即可檢查進度。</span><span class="sxs-lookup"><span data-stu-id="17963-109">You can check the progress by defining a StateChanged event handler (as described in this topic) or using Azure Queue storage to monitor Media Services job notifications (as described in [this](media-services-dotnet-check-job-progress-with-queues.md) topic).</span></span>

## <a name="define-statechanged-event-handler-to-monitor-job-progress"></a><span data-ttu-id="17963-110">定義 StateChanged 事件處理常式來監視工作進度</span><span class="sxs-lookup"><span data-stu-id="17963-110">Define StateChanged event handler to monitor job progress</span></span>
<span data-ttu-id="17963-111">下列程式碼定義 StateChanged 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="17963-111">The following code example defines the StateChanged event handler.</span></span> <span data-ttu-id="17963-112">此事件處理常式可追蹤作業進度，並根據狀態來提供更新的狀態。</span><span class="sxs-lookup"><span data-stu-id="17963-112">This event handler tracks job progress and provides updated status, depending on the state.</span></span> <span data-ttu-id="17963-113">程式碼也定義 LogJobStop 方法。</span><span class="sxs-lookup"><span data-stu-id="17963-113">The code also defines the LogJobStop method.</span></span> <span data-ttu-id="17963-114">此協助程式方法會記錄錯誤詳細資料。</span><span class="sxs-lookup"><span data-stu-id="17963-114">This helper method logs error details.</span></span>

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

        builder.AppendLine("\nThe job stopped due to cancellation or an error.");
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
        // Write the output to a local file and to the console. The template 
        // for an error output file is:  JobStop-{JobId}.txt
        string outputFile = _outputFilesFolder + @"\JobStop-" + JobIdAsFileName(job.Id) + ".txt";
        WriteToFile(outputFile, builder.ToString());
        Console.Write(builder.ToString());
    }

    private static string JobIdAsFileName(string jobID)
    {
        return jobID.Replace(":", "_");
    }



## <a name="next-step"></a><span data-ttu-id="17963-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17963-115">Next step</span></span>
<span data-ttu-id="17963-116">檢閱媒體服務學習路徑。</span><span class="sxs-lookup"><span data-stu-id="17963-116">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="17963-117">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="17963-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

