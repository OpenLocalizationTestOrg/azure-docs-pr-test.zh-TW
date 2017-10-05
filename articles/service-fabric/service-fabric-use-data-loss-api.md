---
title: "如何在 Service Fabric 服務上叫用資料遺失 | Microsoft Docs"
description: "說明如何使用資料遺失 API"
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/19/2016
ms.author: lemai
redirect_url: /azure/service-fabric/service-fabric-testability-overview
ms.openlocfilehash: 0c4791e56f84d0df38783a13c8d8c564fd25f55f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-invoke-data-loss-on-services"></a><span data-ttu-id="23b8d-103">如何在服務上叫用資料遺失</span><span class="sxs-lookup"><span data-stu-id="23b8d-103">How to Invoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="23b8d-104">本文件說明如何在您的服務中造成資料遺失，而且應小心使用。</span><span class="sxs-lookup"><span data-stu-id="23b8d-104">This document describe how to cause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="23b8d-105">簡介</span><span class="sxs-lookup"><span data-stu-id="23b8d-105">Introduction</span></span>
<span data-ttu-id="23b8d-106">您可以在 Service Fabric 服務的分割區上，藉由呼叫 StartPartitionDataLossAsync() 來叫用資料遺失。</span><span class="sxs-lookup"><span data-stu-id="23b8d-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="23b8d-107">這個 API 會使用錯誤插入和分析服務來執行工作以造成資料遺失的狀況。</span><span class="sxs-lookup"><span data-stu-id="23b8d-107">This api uses the Fault Injection and Analysis Service to perform the work to cause data loss conditions.</span></span>

## <a name="using-the-fault-injection-and-analysis-service"></a><span data-ttu-id="23b8d-108">使用錯誤插入和分析服務</span><span class="sxs-lookup"><span data-stu-id="23b8d-108">Using the Fault Injection and Analysis Service</span></span>
<span data-ttu-id="23b8d-109">錯誤插入和分析服務目前支援下列圖表中的 API。</span><span class="sxs-lookup"><span data-stu-id="23b8d-109">The Fault Injection and Analysis Service currently supports the following APIs in the chart below.</span></span>  <span data-ttu-id="23b8d-110">圖表右側顯示對應的 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="23b8d-110">The right side of the chart shows the corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="23b8d-111">如需每個 API 的詳細資訊，請參閱關於每個 API 的 MSDN 文件。</span><span class="sxs-lookup"><span data-stu-id="23b8d-111">Please refer to the msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="23b8d-112">C# API</span><span class="sxs-lookup"><span data-stu-id="23b8d-112">C# API</span></span> | <span data-ttu-id="23b8d-113">PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="23b8d-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="23b8d-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="23b8d-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="23b8d-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="23b8d-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="23b8d-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="23b8d-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="23b8d-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="23b8d-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="23b8d-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="23b8d-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="23b8d-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="23b8d-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="23b8d-120">執行命令的概念概觀</span><span class="sxs-lookup"><span data-stu-id="23b8d-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="23b8d-121">錯誤插入和分析服務會使用非同步模型，您會在其中使用一個本文件中稱為 “Start” API 的 API 來啟動命令，然後使用 “GetProgress” API 檢查此命令的進度，直到其觸達終止狀態或您取消該命令為止。</span><span class="sxs-lookup"><span data-stu-id="23b8d-121">The Fault Injection and Analysis Service uses an asynchronous model where you start the command with one API, referred to as the “Start” API in this document, then checks the progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="23b8d-122">若要啟動命令，請針對對應的 API 呼叫 “Start” API。</span><span class="sxs-lookup"><span data-stu-id="23b8d-122">To start a command, call the “Start” API for the corresponding API.</span></span>  <span data-ttu-id="23b8d-123">這個 API 會在錯誤插入和分析服務已接受要求時傳回。</span><span class="sxs-lookup"><span data-stu-id="23b8d-123">This API returns when the Fault Injection and Analysis Service has accepted the request.</span></span>  <span data-ttu-id="23b8d-124">不過，它不會指出命令已執行多久時間，或者甚至尚未啟動。</span><span class="sxs-lookup"><span data-stu-id="23b8d-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="23b8d-125">若要檢查命令的進度，可呼叫對應到先前呼叫的 “Start” API 的 “GetProgress” API。</span><span class="sxs-lookup"><span data-stu-id="23b8d-125">In order to check progress of a command, call the “GetProgress” API that corresponds to the “Start” API previously called.</span></span>  <span data-ttu-id="23b8d-126">“GetProgress” API 將傳回物件，指出命令在其 State 屬性內目前的狀態。</span><span class="sxs-lookup"><span data-stu-id="23b8d-126">The “GetProgress” API will return an object indicating the current status of the command inside its State property.</span></span>  <span data-ttu-id="23b8d-127">在符合下列條件之前，無限期執行命令：</span><span class="sxs-lookup"><span data-stu-id="23b8d-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="23b8d-128">順利完成。</span><span class="sxs-lookup"><span data-stu-id="23b8d-128">It completes successfully.</span></span>  <span data-ttu-id="23b8d-129">如果您在此情況下於其上呼叫 “GetProgress”，進度物件的 State 會是 Completed。</span><span class="sxs-lookup"><span data-stu-id="23b8d-129">If you call “GetProgress” on it in this case, the progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="23b8d-130">遇到嚴重錯誤。</span><span class="sxs-lookup"><span data-stu-id="23b8d-130">It encounters a fatal error.</span></span>  <span data-ttu-id="23b8d-131">如果您在此情況下於其上呼叫 “GetProgress”，進度物件的 State 會是 Faulted</span><span class="sxs-lookup"><span data-stu-id="23b8d-131">If you call “GetProgress” on it in this case, the progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="23b8d-132">您可以透過 [CancelTestCommandAsync][cancel] API 或 [Stop-ServiceFabricTestCommand][cancelps] PowerShell Cmdlet 來取消它。</span><span class="sxs-lookup"><span data-stu-id="23b8d-132">You cancel it through the [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="23b8d-133">如果您在此情況下於其上呼叫 “GetProgress”，根據該 API 的引數而定，進度物件的狀態會是 Cancelled 或 ForceCancelled。</span><span class="sxs-lookup"><span data-stu-id="23b8d-133">If you call “GetProgress” on it in this case, the progress object’s State will be either Cancelled or ForceCancelled, depending on an argument to that API.</span></span>  <span data-ttu-id="23b8d-134">如需詳細資訊，請參閱適用於 [CancelTestCommandAsync][cancel] 的文件。</span><span class="sxs-lookup"><span data-stu-id="23b8d-134">See the documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="23b8d-135">執行命令的詳細資料</span><span class="sxs-lookup"><span data-stu-id="23b8d-135">Details of Running a Command</span></span>
<span data-ttu-id="23b8d-136">若要啟動命令，可搭配預期的引數呼叫 Start API。</span><span class="sxs-lookup"><span data-stu-id="23b8d-136">In order to start a command, call the Start API with the expected arguments.</span></span>  <span data-ttu-id="23b8d-137">所有的 Start API 都具有名為 operationId 的 Guid 引數。</span><span class="sxs-lookup"><span data-stu-id="23b8d-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="23b8d-138">您應該持續追蹤 operationId 引數，因為它可用來追蹤此命令的進度。</span><span class="sxs-lookup"><span data-stu-id="23b8d-138">You should keep track of the operationId argument, since it is used to track progress of this command.</span></span>  <span data-ttu-id="23b8d-139">這必須傳遞至 “GetProgress” API，以便追蹤命令的進度。</span><span class="sxs-lookup"><span data-stu-id="23b8d-139">This must be passed into the “GetProgress” API in order to track progress of the command.</span></span>  <span data-ttu-id="23b8d-140">OperationId 必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="23b8d-140">The operationId must be unique.</span></span>

<span data-ttu-id="23b8d-141">成功呼叫 Start API 之後，應該在迴圈中呼叫 GetProgress API，直到所傳回進度物件的 State 屬性為 Completed 為止。</span><span class="sxs-lookup"><span data-stu-id="23b8d-141">After successfully calling the Start API, the GetProgress API should be called in a loop until the returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="23b8d-142">所有的 [FabricTransientException’s][fte] 和 OperationCanceledException 都應重試。</span><span class="sxs-lookup"><span data-stu-id="23b8d-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="23b8d-143">當命令觸達終止狀態 (Completed、Faulted 或 Cancelled) 時，所傳回進度物件的 Result 屬性將具有額外的資訊。</span><span class="sxs-lookup"><span data-stu-id="23b8d-143">When the command has reached a terminal state (Completed, Faulted, or Cancelled), the returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="23b8d-144">如果狀態為 Completed，Result.SelectedPartition.PartitionId 將包含所選取的分割識別碼。</span><span class="sxs-lookup"><span data-stu-id="23b8d-144">If the state is Completed, Result.SelectedPartition.PartitionId will contain the partition id that was selected.</span></span>  <span data-ttu-id="23b8d-145">Result.Exception 會是 null。</span><span class="sxs-lookup"><span data-stu-id="23b8d-145">Result.Exception will be null.</span></span>  <span data-ttu-id="23b8d-146">如果狀態為 Faulted，Result.Exception 將產生錯誤插入和分析服務無法執行該命令的理由。</span><span class="sxs-lookup"><span data-stu-id="23b8d-146">If the state is Faulted, Result.Exception will have the reason the Fault Injection and Analysis Service faulted the command.</span></span>  <span data-ttu-id="23b8d-147">Result.SelectedPartition.PartitionId 將具有所選取的分割識別碼。</span><span class="sxs-lookup"><span data-stu-id="23b8d-147">Result.SelectedPartition.PartitionId will have the partition id that was selected.</span></span>  <span data-ttu-id="23b8d-148">在某些情況下，會因為命令執行的程度還不夠而無法選擇分割區。</span><span class="sxs-lookup"><span data-stu-id="23b8d-148">In some situations, the command may not have proceeded far enough to choose a partition.</span></span>  <span data-ttu-id="23b8d-149">在此情況下，PartitionId 會是 0。</span><span class="sxs-lookup"><span data-stu-id="23b8d-149">In that case, the PartitionId will be 0.</span></span>  <span data-ttu-id="23b8d-150">如果狀態為 Cancelled，則 Result.Exception 會是 null。</span><span class="sxs-lookup"><span data-stu-id="23b8d-150">If the state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="23b8d-151">與 Faulted 情況類似，Result.SelectedPartition.PartitionId 將具有所選擇的分割識別碼，但是如果因為命令執行的程度還不夠而無法執行此動作，則為 0。</span><span class="sxs-lookup"><span data-stu-id="23b8d-151">Like the Faulted case, Result.SelectedPartition.PartitionId will have the partition id that was chosen, but if the command has not proceeded far enough to do so, it will be 0.</span></span>  <span data-ttu-id="23b8d-152">另請參閱下面的範例。</span><span class="sxs-lookup"><span data-stu-id="23b8d-152">Please also refer to the sample below.</span></span>

<span data-ttu-id="23b8d-153">下列範例程式碼示範如何啟動然後檢查命令上的進度以造成特定分割區遺失資料。</span><span class="sxs-lookup"><span data-stu-id="23b8d-153">The sample code below shows how to start then check progress on a command to cause data loss on a specific partition.</span></span>

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // The id of the target partition inside the target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.        

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                // In a terminal state .Result.SelectedPartition.PartitionId will have the chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
                Console.WriteLine("Command '{0}' failed with '{1}'", operationId, progress.Result.Exception);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(5.0d)).ConfigureAwait(false);
        }
    }
```

<span data-ttu-id="23b8d-154">下列範例示範如何使用 PartitionSelector 來選擇指定服務的隨機分割區：</span><span class="sxs-lookup"><span data-stu-id="23b8d-154">The sample below shows how to use the PartitionSelector to choose a random partition of a specified service:</span></span>

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have the Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }
            catch (Exception e)
            {
                Console.WriteLine("Unexpected exception '{0}'", e);
                throw;
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                Console.WriteLine("Printing progress.Result:");
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);

                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
                Console.WriteLine("Command '{0}' failed with '{1}', SelectedPartition {2}", operationId, progress.Result.Exception, progress.Result.SelectedPartition);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }
    }
```

## <a name="history-and-truncation"></a><span data-ttu-id="23b8d-155">歷程記錄與截斷</span><span class="sxs-lookup"><span data-stu-id="23b8d-155">History and Truncation</span></span>
<span data-ttu-id="23b8d-156">當命令已觸達終止狀態之後，它的中繼資料將會在錯誤插入和分析服務中保留一段時間，之後才會將它移除以節省空間。</span><span class="sxs-lookup"><span data-stu-id="23b8d-156">After a command has reached a terminal state, its metadata will remain in the Fault Injection and Analysis Service for a certain time, before it will be removed to save space.</span></span>  <span data-ttu-id="23b8d-157">如果在移除命令之後使用該命令的 operationId 來呼叫 “GetProgress”，將會傳回 FabricException 且 ErrorCode 為 KeyNotFound。</span><span class="sxs-lookup"><span data-stu-id="23b8d-157">If “GetProgress” is called using the operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
