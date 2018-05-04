---
title: "Azure Service Fabric 的架構 | Microsoft Docs"
description: "Service Fabric 是一種分散式系統平台，用來建置可調整、可靠且輕鬆管理的雲端應用程式。 本文章說明 Service Fabric 的架構。"
services: service-fabric
documentationcenter: .net
author: rishirsinha
manager: timlt
editor: rishirsinha
ms.assetid: 6b554243-70cb-4c22-9b28-1a8b4703f45e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/12/2017
ms.author: rsinha
ms.openlocfilehash: 3d1f9d6136622e0e9fc1e725d8230dbedd6af24a
ms.sourcegitcommit: 804db51744e24dca10f06a89fe950ddad8b6a22d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/30/2017
---
# <a name="service-fabric-architecture"></a>Service Fabric 架構
Service Fabric 是使用分層的子系統所建置。 這些子系統可讓您撰寫的應用程式為：

* 高可用性
* 可調整
* 可管理
* 可測試

下圖顯示 Service Fabric 的主要子系統。

![Service Fabric 架構的圖表](media/service-fabric-architecture/service-fabric-architecture.png)

在分散式系統中，能夠叢集中的節點之間安全地進行通訊非常重要。 堆疊的基底為傳輸子系統，可讓您安全地在節點之間進行通訊。 傳輸子系統上方即為同盟子系統，會將不同的節點叢集成單一實體 (稱為叢集)，讓 Service Fabric 可以偵測失敗、執行前置選擇，以及提供一致的路由。 可靠性子系統，即同盟子系統的最上層，負責透過如複寫、資源管理和容錯移轉等機制，提供 Service Fabric 服務的可靠性。 同盟子系統也以主控和啟用子系統為基礎，用來管理單一節點上的應用程式生命週期。 管理子系統會管理應用程式和服務的生命週期。 可測試性子系統可協助應用程式開發人員在將應用程式和服務部署至生產環境的前後，透過模擬錯誤測試其服務。 Service Fabric 可以透過其通訊子系統解析服務位置。 公開給開發人員的應用程式設計模型與啟用工具的應用程式模型位於這些子系統的最上層。

## <a name="transport-subsystem"></a>傳輸子系統
傳輸子系統會實作點對點資料包通訊通道。 此通道用於 Service Fabric 叢集內，以及 Service Fabric 叢集與用戶端之間的通訊。 它支援單向和要求/回覆通訊模式，可在同盟層提供實作廣播和多點傳送的基礎。 傳輸子系統使用 X509 憑證或 Windows 安全性來確保通訊安全。 此子系統供 Service Fabric 內部使用，並非由應用程式設計的開發人員直接存取。

## <a name="federation-subsystem"></a>同盟子系統
為了理解分散式系統中的節點集，您需要系統的一致檢視。 同盟子系統會使用傳輸子系統所提供的通訊基本功能，並將不同節點結合至單一的整合節點以便於理解。 其提供其他子系統所需的的分散式系統基本功能，包含失敗偵測、前置選擇，以及一致的路由。 同盟子系統使用 128 位元的權杖空間建置於分散式雜湊資料表的頂端。 此子系統會在節點上建立環狀拓撲，而環中的每個節點皆會針對擁有權來配置權杖空間的子集。 為了進行失敗偵測，分層會使用根據活動訊號和仲裁的租用機制。 同盟子系統也會透過複雜的聯結和分離的通訊協定，確保在任何時間內僅存在單一權杖擁有者。 如此可提供前置選擇和一致的路由保證。

## <a name="reliability-subsystem"></a>可靠性子系統
可靠性子系統提供一種機制，可透過使用「複寫器」、「容錯移轉管理員」以及「資源平衡器」，讓 Service Fabric 服務的狀態具有高可用性。

* 複寫器可確保主要服務複本中的狀態變更會自動複寫至次要複本，以便在服務複本集中維護主要和次要複本之間的一致性。 複寫器負責在複本集中的複本之間進行仲裁管理。 其會與容錯移轉單元互動，以取得要複寫的作業清單，且重新設定代理程式會提供複本集的組態。 該組態指出需要複寫作業的複本。 Service Fabric 會提供稱為網狀架構複寫器的預設複寫器，可由程式撰寫模型 API 用來使服務狀態具有高可用性和可靠性。
* 容錯移轉管理員可確保當節點加入至叢集或從叢集移除節點時，負載會在可用的節點上自動重新分配。 如果叢集中的節點失敗，叢集會自動重新設定服務複本以維護可用性。
* Resource Manager 會將服務複本置於叢集中的失敗網域，並確保所有的容錯移轉單元正常運作。 Resource Manager 也會在叢集節點的基礎共用集區上平衡服務資源，以便達到最佳的統一負載分佈。

## <a name="management-subsystem"></a>管理子系統
管理子系統提供端對端服務和應用程式生命週期管理。 PowerShell Cmdlet 和系統管理 API 可讓您佈建、部署、修補、升級和解除佈建應用程式，而不減損可用性。 管理子系統會透過下列服務來執行此作業。

* **叢集管理員**：這是用來與容錯移轉管理員互動的主要服務，從可靠性到根據服務放置條件約束將應用程式放置在節點上。 容錯移轉子系統中的 Resource Manager 可確保永遠遵循條件約束。 叢集管理員會在從佈建到解除佈建的範圍內，管理應用程式的生命週期。 它會與健康狀態管理員整合，以便從語意上的健康狀態觀點，確保在升級期間不會減損應用程式的可用性。
* **健康狀態管理員**：此服務會啟用應用程式、服務和叢集實體的健康狀態監視。 叢集實體 (例如節點、服務分割和複本) 可以報告健康狀態資訊，然後彙總至集中式健康狀態資料存放區。 此健康狀態資訊可提供服務的整體時間點健康狀態快照和分散在叢集中多個節點的節點，可讓您採取任何需要的修正動作。 健康狀態查詢 API 可讓您查詢向健康狀態子系統報告的健康狀態事件。 健康狀態查詢 API 會傳回儲存在健康狀態資料存放區中的原始健康狀態資料，或針對特定叢集實體傳回經過彙總、解譯的健康狀態資料。
* **映像存放區**：此服務會提供應用程式二進位檔的儲存體和發佈。 此服務會提供簡易的分散式檔案存放區，應用程式可在其中進行上傳和下載。

## <a name="hosting-subsystem"></a>主控子系統
叢集管理員會通知主控子系統 (在每個節點上執行) 需要針對特定節點進行管理的服務。 主控子系統接著會管理該節點上的應用程式生命週期。 其會與可靠性和健康狀態元件互動，以確保複本放置於正確位置且健康狀態良好。

## <a name="communication-subsystem"></a>通訊子系統
此子系統會在叢集內提供可靠訊息，並透過命名服務提供服務探索。 命名服務會將服務名稱解析至叢集中的位置，並可讓使用者能夠管理服務名稱和屬性。 用戶端可以使用命名服務，與叢集中的任何節點安全地進行通訊，以便解析服務名稱和擷取服務中繼資料。 Service Fabric 的使用者可以使用簡易命名用戶端 API，開發能夠解析目前網路位置的服務和用戶端，而不受節點動態或重新調整大小的叢集的限制。

## <a name="testability-subsystem"></a>可測試性子系統
可測試性是一組工具套件，專門用來測試建置於 Service Fabric 上的服務。 這些工具可讓開發人員輕鬆誘發有意義的錯誤及執行測試案例，並使用受控制的安全方式，執行及驗證服務在其生命週期會發生的各種狀態和轉換情形。 可測試性也會提供一種機制，透過執行較長時間的測試，逐一查看各種可能的失敗，而不會減損可用性。 如此可為您提供生產環境中的測試。
