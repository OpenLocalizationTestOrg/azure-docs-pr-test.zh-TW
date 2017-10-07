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
# <a name="how-tooinvoke-data-loss-on-services"></a>如何 tooInvoke 遺失服務資料
> [!WARNING]
> 本文件說明如何 toocause 資料遺失，在您的服務，應小心使用。
> 
> 

## <a name="introduction"></a>簡介
您可以在 Service Fabric 服務的分割區上，藉由呼叫 StartPartitionDataLossAsync() 來叫用資料遺失。  這個 api 會使用 hello 錯誤插入和分析服務 tooperform hello 工作 toocause 資料遺失狀況。

## <a name="using-hello-fault-injection-and-analysis-service"></a>使用錯誤資料隱碼 hello 和分析服務
hello 錯誤插入和分析服務目前支援下列 Api hello 下圖中的 hello。  hello 右邊的 hello 圖表顯示 hello 對應的 PowerShell cmdlet。  請如需有關每個，參閱每個 API 上的 toohello msdn 文件。

| C# API | PowerShell Cmdlet |
| --- | ---:|
| [StartPartitionDataLossAsync][dl] |[Start-ServiceFabricPartitionDataLoss][psdl] |
| [StartPartitionQuorumLossAsync][ql] |[Start-ServiceFabricPartitionQuorumLoss][psql] |
| [StartPartitionRestartAsync][rp] |[Start-ServiceFabricPartitionRestart][psrp] |

## <a name="conceptual-overview-of-running-a-command"></a>執行命令的概念概觀
hello 錯誤插入和分析服務會使用您在此處開始 hello 非同步模型的命令是使用一個 API，而參考這份文件，然後檢查 hello 進行此命令使用 「 GetProgress 」 的 API，直到它已達到終端機 tooas hello 「 開始 」 API狀態，或直到您將它取消。
toostart 命令，針對 hello 對應的 API 呼叫 hello 「 啟動 」 的 API。  這個 API 時，傳回 hello 已接受 hello 要求錯誤插入和分析服務。  不過，它不會指出命令已執行多久時間，或者甚至尚未啟動。  在命令的訂單 toocheck 進度，呼叫 hello"GetProgress 」 對應 「 啟動 」 之前呼叫之 API 的 toohello 的 API。  hello"GetProgress 」 應用程式開發介面會傳回物件，指出 hello 的 hello 命令其狀態屬性內的目前狀態。  在符合下列條件之前，無限期執行命令：

1. 順利完成。  如果在此情況下在其上呼叫 「 GetProgress 」，將會完成 hello 進行物件的狀態。
2. 遇到嚴重錯誤。  如果您"GetProgress 」 上呼叫它在此情況下，會發生錯誤 hello 進行物件的狀態
3. 您取消透過 hello [CancelTestCommandAsync] [ cancel]應用程式開發介面，或[停止 ServiceFabricTestCommand] [ cancelps] PowerShell cmdlet。  如果在此情況下在其上呼叫 「 GetProgress"，hello 進行物件的狀態會是已取消或 ForceCancelled，根據引數 toothat 應用程式開發介面。  請參閱 hello 文件[CancelTestCommandAsync] [ cancel]如需詳細資訊。

## <a name="details-of-running-a-command"></a>執行命令的詳細資料
順序 toostart 命令，在呼叫 hello 啟動應用程式開發介面與 hello 預期引數。  所有的 Start API 都具有名為 operationId 的 Guid 引數。  您應該追蹤的 hello operationId 引數，因為它是使用這個命令的 tootrack 進度。  這必須傳入 hello"GetProgress 」 應用程式開發介面的 hello 命令順序 tootrack 正在進行中。  hello operationId 必須是唯一的。

在成功呼叫 hello 啟動應用程式開發介面，應該在迴圈中呼叫 GetProgress API，直到 hello 傳回進度的 hello 之後完成物件的狀態屬性。  所有的 [FabricTransientException’s][fte] 和 OperationCanceledException 都應重試。
當 hello 命令到達終止狀態 （已完成、 Faulted 或已取消） 時，hello 傳回進行物件的結果屬性會有額外的資訊。  如果 hello 狀態完成，Result.SelectedPartition.PartitionId 會包含所選取的 hello 分割區識別碼。  Result.Exception 會是 null。  如果 hello 狀態為 Faulted，Result.Exception 必須 hello 原因 hello 錯誤插入和分析服務發生錯誤 hello 命令。  Result.SelectedPartition.PartitionId 必須 hello 所選取的分割區識別碼。  在某些情況下，hello 命令可能會不具有繼續進行資料分割不足 toochoose。  在此情況下，hello PartitionId 將會是 0。  如果取消 hello 狀態，則 Result.Exception 將為 null。  Hello Faulted 案例，例如 Result.SelectedPartition.PartitionId hello 分割區識別碼的選擇，但是如果 hello 命令已不繼續進行不足 toodo 因此，它將會是 0。  請參閱也 toohello 以下的範例。

下列的 hello 範例程式碼顯示如何 toostart 然後檢查特定磁碟分割上的命令 toocause 資料遺失的進度。

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

hello 以下範例顯示如何 toouse hello PartitionSelector toochoose 指定服務的隨機分割區：

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

## <a name="history-and-truncation"></a>歷程記錄與截斷
命令已達到終止狀態之後，它的中繼資料會保留在 hello 錯誤插入和分析服務一段時間，才會移除 toosave 空間。  如果"GetProgress 「 呼叫後已移除，請使用命令的 hello operationId，它會傳回與 KeyNotFound ErrorCode FabricException。

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
