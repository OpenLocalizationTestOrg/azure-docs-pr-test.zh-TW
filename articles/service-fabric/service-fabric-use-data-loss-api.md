---
title: "服務網狀架構上發生資料遺失的 aaaHow tooInvoke |Microsoft 文件"
description: "描述如何 toouse hello 資料遺失應用程式開發介面"
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
ms.openlocfilehash: 014c7ebfd2c42d79a5fe1802ecc3fa0c1f26f9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinvoke-data-loss-on-services"></a><span data-ttu-id="24a0e-103">如何 tooInvoke 遺失服務資料</span><span class="sxs-lookup"><span data-stu-id="24a0e-103">How tooInvoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="24a0e-104">本文件說明如何 toocause 資料遺失，在您的服務，應小心使用。</span><span class="sxs-lookup"><span data-stu-id="24a0e-104">This document describe how toocause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="24a0e-105">簡介</span><span class="sxs-lookup"><span data-stu-id="24a0e-105">Introduction</span></span>
<span data-ttu-id="24a0e-106">您可以在 Service Fabric 服務的分割區上，藉由呼叫 StartPartitionDataLossAsync() 來叫用資料遺失。</span><span class="sxs-lookup"><span data-stu-id="24a0e-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="24a0e-107">這個 api 會使用 hello 錯誤插入和分析服務 tooperform hello 工作 toocause 資料遺失狀況。</span><span class="sxs-lookup"><span data-stu-id="24a0e-107">This api uses hello Fault Injection and Analysis Service tooperform hello work toocause data loss conditions.</span></span>

## <a name="using-hello-fault-injection-and-analysis-service"></a><span data-ttu-id="24a0e-108">使用錯誤資料隱碼 hello 和分析服務</span><span class="sxs-lookup"><span data-stu-id="24a0e-108">Using hello Fault Injection and Analysis Service</span></span>
<span data-ttu-id="24a0e-109">hello 錯誤插入和分析服務目前支援下列 Api hello 下圖中的 hello。</span><span class="sxs-lookup"><span data-stu-id="24a0e-109">hello Fault Injection and Analysis Service currently supports hello following APIs in hello chart below.</span></span>  <span data-ttu-id="24a0e-110">hello 右邊的 hello 圖表顯示 hello 對應的 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="24a0e-110">hello right side of hello chart shows hello corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="24a0e-111">請如需有關每個，參閱每個 API 上的 toohello msdn 文件。</span><span class="sxs-lookup"><span data-stu-id="24a0e-111">Please refer toohello msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="24a0e-112">C# API</span><span class="sxs-lookup"><span data-stu-id="24a0e-112">C# API</span></span> | <span data-ttu-id="24a0e-113">PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="24a0e-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="24a0e-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="24a0e-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="24a0e-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="24a0e-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="24a0e-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="24a0e-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="24a0e-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="24a0e-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="24a0e-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="24a0e-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="24a0e-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="24a0e-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="24a0e-120">執行命令的概念概觀</span><span class="sxs-lookup"><span data-stu-id="24a0e-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="24a0e-121">hello 錯誤插入和分析服務會使用您在此處開始 hello 非同步模型的命令是使用一個 API，而參考這份文件，然後檢查 hello 進行此命令使用 「 GetProgress 」 的 API，直到它已達到終端機 tooas hello 「 開始 」 API狀態，或直到您將它取消。</span><span class="sxs-lookup"><span data-stu-id="24a0e-121">hello Fault Injection and Analysis Service uses an asynchronous model where you start hello command with one API, referred tooas hello “Start” API in this document, then checks hello progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="24a0e-122">toostart 命令，針對 hello 對應的 API 呼叫 hello 「 啟動 」 的 API。</span><span class="sxs-lookup"><span data-stu-id="24a0e-122">toostart a command, call hello “Start” API for hello corresponding API.</span></span>  <span data-ttu-id="24a0e-123">這個 API 時，傳回 hello 已接受 hello 要求錯誤插入和分析服務。</span><span class="sxs-lookup"><span data-stu-id="24a0e-123">This API returns when hello Fault Injection and Analysis Service has accepted hello request.</span></span>  <span data-ttu-id="24a0e-124">不過，它不會指出命令已執行多久時間，或者甚至尚未啟動。</span><span class="sxs-lookup"><span data-stu-id="24a0e-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="24a0e-125">在命令的訂單 toocheck 進度，呼叫 hello"GetProgress 」 對應 「 啟動 」 之前呼叫之 API 的 toohello 的 API。</span><span class="sxs-lookup"><span data-stu-id="24a0e-125">In order toocheck progress of a command, call hello “GetProgress” API that corresponds toohello “Start” API previously called.</span></span>  <span data-ttu-id="24a0e-126">hello"GetProgress 」 應用程式開發介面會傳回物件，指出 hello 的 hello 命令其狀態屬性內的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="24a0e-126">hello “GetProgress” API will return an object indicating hello current status of hello command inside its State property.</span></span>  <span data-ttu-id="24a0e-127">在符合下列條件之前，無限期執行命令：</span><span class="sxs-lookup"><span data-stu-id="24a0e-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="24a0e-128">順利完成。</span><span class="sxs-lookup"><span data-stu-id="24a0e-128">It completes successfully.</span></span>  <span data-ttu-id="24a0e-129">如果在此情況下在其上呼叫 「 GetProgress 」，將會完成 hello 進行物件的狀態。</span><span class="sxs-lookup"><span data-stu-id="24a0e-129">If you call “GetProgress” on it in this case, hello progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="24a0e-130">遇到嚴重錯誤。</span><span class="sxs-lookup"><span data-stu-id="24a0e-130">It encounters a fatal error.</span></span>  <span data-ttu-id="24a0e-131">如果您"GetProgress 」 上呼叫它在此情況下，會發生錯誤 hello 進行物件的狀態</span><span class="sxs-lookup"><span data-stu-id="24a0e-131">If you call “GetProgress” on it in this case, hello progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="24a0e-132">您取消透過 hello [CancelTestCommandAsync] [ cancel]應用程式開發介面，或[停止 ServiceFabricTestCommand] [ cancelps] PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="24a0e-132">You cancel it through hello [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="24a0e-133">如果在此情況下在其上呼叫 「 GetProgress"，hello 進行物件的狀態會是已取消或 ForceCancelled，根據引數 toothat 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="24a0e-133">If you call “GetProgress” on it in this case, hello progress object’s State will be either Cancelled or ForceCancelled, depending on an argument toothat API.</span></span>  <span data-ttu-id="24a0e-134">請參閱 hello 文件[CancelTestCommandAsync] [ cancel]如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="24a0e-134">See hello documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="24a0e-135">執行命令的詳細資料</span><span class="sxs-lookup"><span data-stu-id="24a0e-135">Details of Running a Command</span></span>
<span data-ttu-id="24a0e-136">順序 toostart 命令，在呼叫 hello 啟動應用程式開發介面與 hello 預期引數。</span><span class="sxs-lookup"><span data-stu-id="24a0e-136">In order toostart a command, call hello Start API with hello expected arguments.</span></span>  <span data-ttu-id="24a0e-137">所有的 Start API 都具有名為 operationId 的 Guid 引數。</span><span class="sxs-lookup"><span data-stu-id="24a0e-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="24a0e-138">您應該追蹤的 hello operationId 引數，因為它是使用這個命令的 tootrack 進度。</span><span class="sxs-lookup"><span data-stu-id="24a0e-138">You should keep track of hello operationId argument, since it is used tootrack progress of this command.</span></span>  <span data-ttu-id="24a0e-139">這必須傳入 hello"GetProgress 」 應用程式開發介面的 hello 命令順序 tootrack 正在進行中。</span><span class="sxs-lookup"><span data-stu-id="24a0e-139">This must be passed into hello “GetProgress” API in order tootrack progress of hello command.</span></span>  <span data-ttu-id="24a0e-140">hello operationId 必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="24a0e-140">hello operationId must be unique.</span></span>

<span data-ttu-id="24a0e-141">在成功呼叫 hello 啟動應用程式開發介面，應該在迴圈中呼叫 GetProgress API，直到 hello 傳回進度的 hello 之後完成物件的狀態屬性。</span><span class="sxs-lookup"><span data-stu-id="24a0e-141">After successfully calling hello Start API, hello GetProgress API should be called in a loop until hello returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="24a0e-142">所有的 [FabricTransientException’s][fte] 和 OperationCanceledException 都應重試。</span><span class="sxs-lookup"><span data-stu-id="24a0e-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="24a0e-143">當 hello 命令到達終止狀態 （已完成、 Faulted 或已取消） 時，hello 傳回進行物件的結果屬性會有額外的資訊。</span><span class="sxs-lookup"><span data-stu-id="24a0e-143">When hello command has reached a terminal state (Completed, Faulted, or Cancelled), hello returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="24a0e-144">如果 hello 狀態完成，Result.SelectedPartition.PartitionId 會包含所選取的 hello 分割區識別碼。</span><span class="sxs-lookup"><span data-stu-id="24a0e-144">If hello state is Completed, Result.SelectedPartition.PartitionId will contain hello partition id that was selected.</span></span>  <span data-ttu-id="24a0e-145">Result.Exception 會是 null。</span><span class="sxs-lookup"><span data-stu-id="24a0e-145">Result.Exception will be null.</span></span>  <span data-ttu-id="24a0e-146">如果 hello 狀態為 Faulted，Result.Exception 必須 hello 原因 hello 錯誤插入和分析服務發生錯誤 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="24a0e-146">If hello state is Faulted, Result.Exception will have hello reason hello Fault Injection and Analysis Service faulted hello command.</span></span>  <span data-ttu-id="24a0e-147">Result.SelectedPartition.PartitionId 必須 hello 所選取的分割區識別碼。</span><span class="sxs-lookup"><span data-stu-id="24a0e-147">Result.SelectedPartition.PartitionId will have hello partition id that was selected.</span></span>  <span data-ttu-id="24a0e-148">在某些情況下，hello 命令可能會不具有繼續進行資料分割不足 toochoose。</span><span class="sxs-lookup"><span data-stu-id="24a0e-148">In some situations, hello command may not have proceeded far enough toochoose a partition.</span></span>  <span data-ttu-id="24a0e-149">在此情況下，hello PartitionId 將會是 0。</span><span class="sxs-lookup"><span data-stu-id="24a0e-149">In that case, hello PartitionId will be 0.</span></span>  <span data-ttu-id="24a0e-150">如果取消 hello 狀態，則 Result.Exception 將為 null。</span><span class="sxs-lookup"><span data-stu-id="24a0e-150">If hello state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="24a0e-151">Hello Faulted 案例，例如 Result.SelectedPartition.PartitionId hello 分割區識別碼的選擇，但是如果 hello 命令已不繼續進行不足 toodo 因此，它將會是 0。</span><span class="sxs-lookup"><span data-stu-id="24a0e-151">Like hello Faulted case, Result.SelectedPartition.PartitionId will have hello partition id that was chosen, but if hello command has not proceeded far enough toodo so, it will be 0.</span></span>  <span data-ttu-id="24a0e-152">請參閱也 toohello 以下的範例。</span><span class="sxs-lookup"><span data-stu-id="24a0e-152">Please also refer toohello sample below.</span></span>

<span data-ttu-id="24a0e-153">下列的 hello 範例程式碼顯示如何 toostart 然後檢查特定磁碟分割上的命令 toocause 資料遺失的進度。</span><span class="sxs-lookup"><span data-stu-id="24a0e-153">hello sample code below shows how toostart then check progress on a command toocause data loss on a specific partition.</span></span>

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // hello id of hello target partition inside hello target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
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

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.        

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

                // In a terminal state .Result.SelectedPartition.PartitionId will have hello chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
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

<span data-ttu-id="24a0e-154">hello 以下範例顯示如何 toouse hello PartitionSelector toochoose 指定服務的隨機分割區：</span><span class="sxs-lookup"><span data-stu-id="24a0e-154">hello sample below shows how toouse hello PartitionSelector toochoose a random partition of a specified service:</span></span>

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have hello Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
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

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.

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
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
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

## <a name="history-and-truncation"></a><span data-ttu-id="24a0e-155">歷程記錄與截斷</span><span class="sxs-lookup"><span data-stu-id="24a0e-155">History and Truncation</span></span>
<span data-ttu-id="24a0e-156">命令已達到終止狀態之後，它的中繼資料會保留在 hello 錯誤插入和分析服務一段時間，才會移除 toosave 空間。</span><span class="sxs-lookup"><span data-stu-id="24a0e-156">After a command has reached a terminal state, its metadata will remain in hello Fault Injection and Analysis Service for a certain time, before it will be removed toosave space.</span></span>  <span data-ttu-id="24a0e-157">如果"GetProgress 「 呼叫後已移除，請使用命令的 hello operationId，它會傳回與 KeyNotFound ErrorCode FabricException。</span><span class="sxs-lookup"><span data-stu-id="24a0e-157">If “GetProgress” is called using hello operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
