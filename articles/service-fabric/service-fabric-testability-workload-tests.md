---
title: "在 Azure microservices aaaSimulate 錯誤 |Microsoft 文件"
description: "如何 tooharden 您針對非失誤性和不正常失敗的服務。"
services: service-fabric
documentationcenter: .net
author: anmolah
manager: timlt
editor: 
ms.assetid: 44af01f0-ed73-4c31-8ac0-d9d65b4ad2d6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: anmola
ms.openlocfilehash: 05467e291dfc0f12a021955f8ea540881ec10746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="simulate-failures-during-service-workloads"></a>模擬服務工作負載期間的失敗案例
Azure Service Fabric 中的 hello 可測試性案例可讓開發人員 toonot 擔心個別錯誤處理。 不過還是有些案例，可能會需要明確的用戶端工作負載和失敗交錯。 hello 交錯的用戶端工作負載和錯誤，可確保 hello 服務實際執行某些動作失敗時。 獲得 hello 層級，可測試性提供，這些可能是控制項的 hello 工作負載執行的精確時間點。 此錯誤在 hello 應用程式中的不同狀態的歸納可尋找 bug，並改善品質。

## <a name="sample-custom-scenario"></a>範例自訂案例
這項測試顯示的案例與該 interleaves hello 企業工作負載[依正常程序和不正常失敗](service-fabric-testability-actions.md#graceful-vs-ungraceful-fault-actions)。 hello 錯誤應該產生 hello 中間的服務作業，或是為了獲得最佳結果的計算。

讓我們逐步解說會顯示四個工作負載服務的範例： A、 B、 C 和 d。 每個對應 tooa 組的工作流程，且無法計算、 儲存體或混合。 為了簡化的 hello 起見，我們將會擷取 hello 工作負載在我們的範例。 在此範例中執行的 hello 不同錯誤是：

* RestartNode： 不正常錯誤 toosimulate 機器重新啟動。
* RestartDeployedCodePackage： 不正常錯誤 toosimulate 服務主機處理序損毀。
* RemoveReplica： 依正常程序錯誤 toosimulate 複本移除。
* MovePrimary： 依正常程序錯誤 toosimulate 複本移動觸發 hello Service Fabric 負載平衡器。

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll.

using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        // Replace these strings with hello actual version for your cluster and application.
        string clusterConnection = "localhost:19000";
        Uri applicationName = new Uri("fabric:/samples/PersistentToDoListApp");
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Workload Test...");
        try
        {
            RunTestAsync(clusterConnection, applicationName, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Workload Test failed: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Workload Test completed successfully.");
        return 0;
    }

    public enum ServiceWorkloads
    {
        A,
        B,
        C,
        D
    }

    public enum ServiceFabricFaults
    {
        RestartNode,
        RestartCodePackage,
        RemoveReplica,
        MovePrimary,
    }

    public static async Task RunTestAsync(string clusterConnection, Uri applicationName, Uri serviceName)
    {
        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);
        // Maximum time toowait for a service toostabilize.
        TimeSpan maxServiceStabilizationTime = TimeSpan.FromSeconds(120);

        // How many loops of faults you want tooexecute.
        uint testLoopCount = 20;
        Random random = new Random();

        for (var i = 0; i < testLoopCount; ++i)
        {
            var workload = SelectRandomValue<ServiceWorkloads>(random);
            // Start hello workload.
            var workloadTask = RunWorkloadAsync(workload);

            // While hello task is running, induce faults into hello service. They can be ungraceful faults like
            // RestartNode and RestartDeployedCodePackage or graceful faults like RemoveReplica or MovePrimary.
            var fault = SelectRandomValue<ServiceFabricFaults>(random);

            // Create a replica selector, which will select a primary replica from hello given service tootest.
            var replicaSelector = ReplicaSelector.PrimaryOf(PartitionSelector.RandomOf(serviceName));
            // Run hello selected random fault.
            await RunFaultAsync(applicationName, fault, replicaSelector, fabricClient);
            // Validate hello health and stability of hello service.
            await fabricClient.ServiceManager.ValidateServiceAsync(serviceName, maxServiceStabilizationTime);

            // Wait for hello workload toofinish successfully.
            await workloadTask;
        }
    }

    private static async Task RunFaultAsync(Uri applicationName, ServiceFabricFaults fault, ReplicaSelector selector, FabricClient client)
    {
        switch (fault)
        {
            case ServiceFabricFaults.RestartNode:
                await client.ClusterManager.RestartNodeAsync(selector, CompletionMode.Verify);
                break;
            case ServiceFabricFaults.RestartCodePackage:
                await client.ApplicationManager.RestartDeployedCodePackageAsync(applicationName, selector, CompletionMode.Verify);
                break;
            case ServiceFabricFaults.RemoveReplica:
                await client.ServiceManager.RemoveReplicaAsync(selector, CompletionMode.Verify, false);
                break;
            case ServiceFabricFaults.MovePrimary:
                await client.ServiceManager.MovePrimaryAsync(selector.PartitionSelector);
                break;
        }
    }

    private static Task RunWorkloadAsync(ServiceWorkloads workload)
    {
        throw new NotImplementedException();
        // This is where you trigger and complete your service workload.
        // Note that hello faults induced while your service workload is running will
        // fault hello primary service. Hence, you will need tooreconnect toocomplete or check
        // hello status of hello workload.
    }

    private static T SelectRandomValue<T>(Random random)
    {
        Array values = Enum.GetValues(typeof(T));
        T workload = (T)values.GetValue(random.Next(values.Length));
        return workload;
    }
}
```
