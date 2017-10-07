---
title: "Testability：服務通訊 | Microsoft Docs"
description: "服務之間的通訊是整合 Service Fabric 應用程式的重要環節。 本文討論設計考量及測試技巧。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 017557df-fb59-4e4a-a65d-2732f29255b8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4a8f941c1e8e641384a9ee3a1149dabaaf9983cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-testability-scenarios-service-communication"></a>Service Fabric Testability 案例：服務通訊
微服務及服務導向的架構樣式會在 Azure Service Fabric 中自然出現。 在這些類型的分散式架構中，通常被組成需要 tootalk tooeach 其他的多個服務的元件化的微服務應用程式。 在即使 hello 最簡單的情況下，您通常具有最少的無狀態 web 服務和需要 toocommunicate 可設定狀態的資料儲存體服務。

服務對服務通訊是應用程式中，重要的整合點，因為每個服務會公開一種遠端 API tooother 服務。 與 I/O 相關的一組 API 界限通常需要謹慎處理，且需經過大量測試和驗證。

這些服務界限在分散式系統連接在一起時，有許多考量 toomake:

* 傳輸通訊協定。 您要使用 HTTP 以提供更優異的互通性，還是自訂的二進位通訊協定，以應付最大的輸送量？
* 錯誤處理。 如何處理永久性和暫時性錯誤？ 當服務移 tooa 另一個節點時，會發生什麼事？
* 逾時與延遲。 在多層式應用程式如何將每個服務層處理 hello 堆疊和 toohello 使用者透過延遲？

無論您使用其中一個 hello Service Fabric 所提供的內建的服務通訊元件，或是您建立您自己，測試您的服務之間的 hello 互動是您的應用程式中的重大 tooensuring 恢復功能。

## <a name="prepare-for-services-toomove"></a>準備服務 toomove
服務執行個體經過一段時間後可能會移動。 尤其在它們設有負載度量，以自訂最佳資源平衡時更是如此。 Service Fabric 移動期間升級、 容錯移轉、 向外延展和其他透過分散式系統的 hello 存留期間發生的情況下，即使您的服務執行個體 toomaximize 其可用性。

服務移動 hello 叢集中，您的用戶端和其他服務時，應該已備妥的 toohandle 兩個案例進行討論 tooa 服務：

* hello 服務執行個體或資料分割複本已經因為 hello 討論 tooit 的最後一次。 這是服務生命週期的一部分，且應預期的 toohappen hello 應用程式的存留期間。
* hello 服務執行個體或資料分割複本處於移動的 hello 程序。 服務網狀架構中發生非常快速地從一個節點 tooanother 服務的容錯移轉，雖然可能會延遲可用性緩慢 toostart hello 通訊元件，您的服務時。

妥善處理這些案例，對於系統流暢運作至關重要。 toodo 因此，請記住，：

* 每項服務可以連線的 toohas*位址*，它會接聽程式 （例如，HTTP 或 Websocket）。 當服務執行個體或分割移動時，其位址端點會變更。 （它會移動 tooa 不同的節點，請使用不同的 IP 位址。）如果您使用 hello 的內建通訊的元件，將為您處理重新解決服務位址。
* 可能有其接聽程式 hello 服務執行個體啟動為服務延遲暫時增加一次。 這取決於 hello 服務執行個體已經移動後 hello 服務開啟 hello 接聽程式的速度。
* 任何現有的連線需要 toobe 關閉並重新開啟 hello 服務開啟新的節點之後。 依正常程序中的節點關機或重新啟動允許正常關閉現有連接 toobe 的時間。

### <a name="test-it-move-service-instances"></a>測試：移動服務執行個體
使用 Service Fabric 可測試性工具，您可以撰寫測試案例 tootest 這些情況下以不同的方式：

1. 移動具狀態服務的主要複本。
   
    hello 可設定狀態的服務資料分割的主要複本可以移動的原因有許多。 使用您的服務 react toohello 如何在受控制的方式移動特定資料分割 toosee 此 tootarget hello 主要複本。
   
    ```powershell
   
    PS > Move-ServiceFabricPrimaryReplica -PartitionId 6faa4ffa-521a-44e9-8351-dfca0f7e0466 -ServiceName fabric:/MyApplication/MyService
   
    ```
2. 停止節點。
   
    在停止節點時，Service Fabric 移 hello 的所有服務執行個體或資料分割上的該節點 tooone hello hello 叢集中的其他可用節點。 使用此 tootest 節點是從您的叢集遺失，和所有 hello 服務執行個體和該節點上的複本有 toomove 的情況。
   
    您可以藉由使用 hello PowerShell 停止節點**停止 ServiceFabricNode** cmdlet:
   
    ```powershell
   
    PS > Restart-ServiceFabricNode -NodeName Node_1
   
    ```

## <a name="maintain-service-availability"></a>維護服務可用性
做為平台，Service Fabric 這項設計的 tooprovide 高可用性，您的服務。 但是在極端情況下，基礎結構的基礎問題仍可能導致無法使用服務。 太重要 tootest 針對這些案例。

可設定狀態的服務會使用以仲裁為基礎的系統 tooreplicate 狀態的高可用性。 這表示複本的仲裁必須 toobe 可用 tooperform 寫入作業。 在極罕見情況下，例如大規模的硬體故障，有可能無法使用複本仲裁。 在這些情況下，您將不會無法 tooperform 寫入作業，但是您仍然可以無法 tooperform 讀取的作業。

### <a name="test-it-write-operation-unavailability"></a>測試：撰寫作業無法使用
使用 Service Fabric 中 hello 可測試性工具，您可以將插入其仲裁遺失，做為測試會引發錯誤。 雖然這類案例中很少發生，請務必用戶端和服務可設定狀態服務所依賴的準備，它們無法做出寫入要求 tooit toohandle 情況。 也很重要，hello 可設定狀態服務本身是留意這個可能性，可以依正常程序進行通訊它 toocallers。

您可以使用 hello PowerShell 誘使仲裁遺失**Invoke ServiceFabricPartitionQuorumLoss** cmdlet:

```powershell

PS > Invoke-ServiceFabricPartitionQuorumLoss -ServiceName fabric:/Myapplication/MyService -QuorumLossMode QuorumReplicas -QuorumLossDurationInSeconds 20

```

在此範例中，我們設定`QuorumLossMode`太`QuorumReplicas`tooindicate 我們想 tooinduce 仲裁遺失而不需讓下所有複本。 如此才能正常執行讀取作業。 tootest 案例，其中整個磁碟分割是無法使用，您可以設定此參數太`AllReplicas`。

## <a name="next-steps"></a>後續步驟
[深入了解 Testability 動作](service-fabric-testability-actions.md)

[深入了解 Testability 案例](service-fabric-testability-scenarios.md)

