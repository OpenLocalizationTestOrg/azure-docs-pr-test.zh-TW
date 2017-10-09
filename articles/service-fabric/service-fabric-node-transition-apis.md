---
title: "aaaStart 和停止叢集節點 tootest Azure microservices |Microsoft 文件"
description: "了解如何 toouse 錯誤資料隱碼 tootest Service Fabric 應用程式的啟動和停止叢集節點。"
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
ms.date: 6/12/2017
ms.author: lemai
ms.openlocfilehash: 7d3f5147328e6233a67533fbfb2a525aa5fc060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a>Hello 啟動節點和停止節點 Api 取代 hello 節點轉換 API

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a>什麼執行 hello 停止節點，並開始節點 Api 執行？

hello 停止節點 API (管理： [StopNodeAsync()][stopnode]，PowerShell:[停止 ServiceFabricNode][stopnodeps]) 停止 Service Fabric 節點。  Service Fabric 節點是程序，不是 VM 或電腦 – hello VM 或電腦將仍會執行。  Hello hello 文件其餘部分 「 節點 」 表示 Service Fabric 節點。  停止節點放入*停止*狀態的不是 hello 叢集的成員，而無法裝載服務，藉此模擬*向*節點。  這可用於將 hello 系統 tootest 插入您的應用程式的錯誤。  hello 開始節點 API (管理： [StartNodeAsync()][startnode]，PowerShell:[開始 ServiceFabricNode][startnodeps]]) 反轉 hello 停止節點應用程式開發介面， 它會 hello 節點後 tooa 正常狀態。

## <a name="why-are-we-replacing-these"></a>為什麼要取代它們？

如上所述，*停止*Service Fabric 節點是刻意使用 hello 停止節點 API 的目標節點。  A*向*節點是節點因任何原因 （例如 hello VM 或電腦為關閉） 已關閉。  Hello 停止節點 API，與 hello 系統不會公開資訊 toodifferentiate 之間*停止*節點和*向*節點。

此外，這些 API 傳回的某些錯誤的描述不明確。  例如，叫用 hello 停止節點 API 上的 已*停止*節點將會傳回 hello 錯誤*InvalidAddress*。  這種經驗可以改善。

此外，節點已停止 hello 期間才開始節點 API 會叫用的 hello 是 「 無限 」。  我們發現這可能會造成問題，比較容易出錯。  例如，我們已看到使用者叫用 hello 停止節點 API 在節點上的，並接著忘記其相關的問題。  更新版本中，所以如果 hello 的節點不清楚*向*或*停止*。


## <a name="introducing-hello-node-transition-apis"></a>介紹 hello 節點轉換應用程式開發介面

我們已經用一組新的 API 解決上述問題。  新節點的轉換 API hello (管理： [StartNodeTransitionAsync()][snt]) 可能會使用的 tootransition Service Fabric 節點 tooa*停止*狀態或 tootransition 它從*停止*狀態 tooa 正常狀態。  請注意該 hello 「 開始 」 中的 hello API hello 名稱不是指 toostarting 節點。  它會參考非同步作業 hello 系統將會執行 tootransition hello 節點 tooeither toobeginning*停止*或啟動狀態。

**用法**

Hello 節點轉換應用程式開發介面不會擲回例外狀況叫用時，如果 hello 系統已接受 hello 非同步作業，並加以執行。  在成功呼叫不代表 hello 作業尚未完成。  tooget hello hello 作業時，呼叫 hello 節點轉換進行應用程式開發介面的目前狀態相關的資訊 (受管理： [GetNodeTransitionProgressAsync()][gntp]) 與 hello 叫用節點時使用的 guid這項作業的轉換 API。  hello 節點轉換進度 API 傳回 NodeTransitionProgress 物件。  此物件的狀態屬性會指定 hello hello 作業目前狀態。  如果 hello 狀態 「 執行 」 hello 作業正在執行。  如果它已完成，hello 作業完成，沒有錯誤。  如果會發生錯誤，無法執行 hello 作業。  屬性會指出哪些 hello 發出的 hello 結果屬性的例外狀況。  Https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate 的 hello 狀態屬性和 hello 」 範例使用方式 」 一節的程式碼範例的詳細資訊，請參閱。


**已停止的節點，然後關閉節點之間的區別**如果節點是*停止*使用 hello 節點轉換 API hello 查詢輸出的節點 (管理： [GetNodeListAsync()] [ nodequery]，PowerShell: [Get ServiceFabricNode][nodequeryps]) 將會顯示這個節點有*IsStopped*屬性值為 true。  請注意這點不同於 hello hello 值*NodeStatus*屬性，將假設*向*。  如果 hello *NodeStatus*屬性的值為*向*，但*IsStopped* hello 節點並未停止使用 hello 節點轉換 API，則為 false，且*向下*因其他原因。  如果 hello *IsStopped*屬性為 true，而且 hello *NodeStatus*屬性是*向*，然後停止使用 hello 節點轉換 API。

啟動*停止*節點使用 hello 節點轉換 API 會傳回它 toofunction 做為正常叢集成員的 hello 一次。  hello hello 節點查詢 API 的輸出會顯示*IsStopped*為 false，和*NodeStatus*為非項目向下 （例如上）。


**有限的持續時間**時使用 hello 節點轉換 API toostop 節點，一個 hello 的必要參數， *stopNodeDurationInSeconds*，代表 hello 秒 tookeep hello 節點中的時間量*停止*。  此值必須在允許的範圍，其中具有最小值為 600 和最多個 14400 hello。  此時間過期之後，hello 節點會自動重新啟動成本身總狀態。  如需使用方式的範例，請參閱 tooSample 下列 1。

> [!WARNING]
> 避免混用節點轉換 Api 和 hello 停止節點，然後啟動節點 Api。  hello 建議太使用 hello 只節點轉換 API。  > 如果節點已被已停止使用 hello 停止節點 API，它應該要啟動使用 hello 之前，先使用 hello 開始節點 API > 節點的轉換 Api。

> [!WARNING]
> 無法進行呼叫的多個節點的轉換 Api hello 以平行方式的相同節點。  在這種情況下，將 hello 節點轉換 API > ErrorCode 屬性值為 NodeTransitionInProgress FabricException 會擲回。  一旦節點上之轉換的特定節點擁有 > 已啟動，您應該等待 hello 作業開始之前到達終止狀態 （已完成、 Faulted 或 ForceCancelled） > new 上的轉換 hello 相同節點。  允許在不同節點上平行呼叫節點轉換。


#### <a name="sample-usage"></a>範例用法


**範例 1** -hello 下列範例會使用 hello 節點轉換 API toostop 節點。

```csharp
        // Helper function tooget information about a node
        static Node GetNodeInfo(FabricClient fc, string node)
        {
            NodeList n = null;
            while (n == null)
            {
                n = fc.QueryManager.GetNodeListAsync(node).GetAwaiter().GetResult();
                Task.Delay(TimeSpan.FromSeconds(1)).GetAwaiter();
            };

            return n.FirstOrDefault();
        }

        static async Task WaitForStateAsync(FabricClient fc, Guid operationId, TestCommandProgressState targetState)
        {
            NodeTransitionProgress progress = null;

            do
            {
                bool exceptionObserved = false;
                try
                {
                    progress = await fc.TestManager.GetNodeTransitionProgressAsync(operationId, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                    exceptionObserved = true;
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                    exceptionObserved = true;
                }

                if (!exceptionObserved)
                {
                    Console.WriteLine("Current state of operation '{0}': {1}", operationId, progress.State);

                    if (progress.State == TestCommandProgressState.Faulted)
                    {
                        // Inspect hello progress object's Result.Exception.HResult tooget hello error code.
                        Console.WriteLine("'{0}' failed with: {1}, HResult: {2}", operationId, progress.Result.Exception, progress.Result.Exception.HResult);

                        // ...additional logic as required
                    }

                    if (progress.State == targetState)
                    {
                        Console.WriteLine("Target state '{0}' has been reached", targetState);
                        break;
                    }
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (true);
        }

        static async Task StopNodeAsync(FabricClient fc, string nodeName, int durationInSeconds)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            // Create a Guid
            Guid guid = Guid.NewGuid();

            // Create a NodeStopDescription object, which will be used as a parameter into StartNodeTransition
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, durationInSeconds);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStopDescription from above, which will stop hello target node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    // This is retryable
                }
                catch (FabricTransientException fte)
                {
                    // This is retryable
                }

                // Backoff
                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

**範例 2** -hello 遵循範例啟動*停止*節點。  它會使用一些 helper 方法，從 hello 第一個範例。

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = n.NodeInstanceId;

            // Create a NodeStartDescription object, which will be used as a parameter into StartNodeTransition
            NodeStartDescription description = new NodeStartDescription(guid, n.NodeName, nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

**範例 3** -hello 下列範例顯示使用方式不正確。  這種使用方式不正確因為 hello *stopDurationInSeconds*它提供大於允許的範圍中的 hello。  由於 StartNodeTransitionAsync() 將會發生嚴重錯誤時失敗，hello 作業不被接受，而且不應該呼叫 hello 進行應用程式開發介面。  這個範例會使用一些 helper 方法，從 hello 第一個範例。

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds toodemonstrate error
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, 99999);

            try
            {
                await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
            }

            catch (FabricException e)
            {
                Console.WriteLine("Caught {0}", e);
                Console.WriteLine("ErrorCode {0}", e.ErrorCode);
                // Output:
                // Caught System.Fabric.FabricException: System.Runtime.InteropServices.COMException (-2147017629)
                // StopDurationInSeconds is out of range ---> System.Runtime.InteropServices.COMException: Exception from HRESULT: 0x80071C63
                // << Parts of exception omitted>>
                //
                // ErrorCode InvalidDuration
            }
        }
```

**範例 4** -hello 下列範例顯示 hello hello 節點轉換進度 API hello hello 節點轉換 API 所起始的作業會被接受，但無法執行時，稍後時將傳回錯誤資訊。  在 hello 情況下，它會失敗，因為 hello 節點轉換 API 嘗試 toostart 不存在的節點。  這個範例會使用一些 helper 方法，從 hello 第一個範例。

```csharp
        static async Task StartNodeWithNonexistentNodeAsync(FabricClient fc)
        {
            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = 12345;

            // Intentionally use a nonexistent node
            NodeStartDescription description = new NodeStartDescription(guid, "NonexistentNode", nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hello desired state is reached.  In this case, it will end up in hello Faulted state since hello node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect hello progress object's Result.Exception.HResult tooget hello error code.
            // In this case, it will be NodeNotFound.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Faulted).ConfigureAwait(false);
        }
```

[stopnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StopNodeAsync_System_String_System_Numerics_BigInteger_System_Fabric_CompletionMode_
[stopnodeps]: https://msdn.microsoft.com/library/mt125982.aspx
[startnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StartNodeAsync_System_String_System_Numerics_BigInteger_System_String_System_Int32_System_Fabric_CompletionMode_System_Threading_CancellationToken_
[startnodeps]: https://msdn.microsoft.com/library/mt163520.aspx
[nodequery]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient#System_Fabric_FabricClient_QueryClient_GetNodeListAsync_System_String_
[nodequeryps]: https://docs.microsoft.com/powershell/servicefabric/vlatest/Get-ServiceFabricNode?redirectedfrom=msdn
[snt]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_StartNodeTransitionAsync_System_Fabric_Description_NodeTransitionDescription_System_TimeSpan_System_Threading_CancellationToken_
[gntp]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_GetNodeTransitionProgressAsync_System_Guid_System_TimeSpan_System_Threading_CancellationToken_
