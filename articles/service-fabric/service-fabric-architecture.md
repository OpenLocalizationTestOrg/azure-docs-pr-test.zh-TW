---
title: "Azure Service Fabric 的 aaaArchitecture |Microsoft 文件"
description: "Service Fabric 是分散式的系統平台使用 hello 雲端 toobuild 可擴充、 可靠且和輕鬆管理應用程式。 這篇文章會顯示 Service Fabric hello 架構。"
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
ms.date: 04/19/2017
ms.author: rsinha
ms.openlocfilehash: 0268578094ad1a0010ef44ed940f828b985f6c40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-architecture"></a>Service Fabric 架構
Service Fabric 是使用分層的子系統所建置。 這些子系統將啟用 toowrite 的應用程式：

* 高可用性
* 可調整
* 可管理
* 可測試

hello 下列圖表顯示 hello Service Fabric 主要子系統。

![Service Fabric 架構的圖表](media/service-fabric-architecture/service-fabric-architecture.png)

在分散式系統中，在節點之間的通訊 hello 能力 toosecurely 叢集是非常重要。 Hello hello 堆疊的基底是 hello 傳輸子系統，提供節點之間的通訊安全。 上述 hello 傳輸子系統會位於 hello 同盟子系統，哪些群集會 hello 單一實體 （稱為 「 叢集 」） 到不同的節點，因此 Service Fabric 偵測失敗，執行前置選擇，且提供一致的路由。 hello 同盟子系統的最上層的 hello 可靠性子系統負責的機制，例如複寫、 資源管理和容錯移轉到 Service Fabric 服務的 hello 可靠性。 hello 同盟子系統也做為 hello 裝載和啟動子系統，可管理 hello 單一節點上的應用程式生命週期。 hello 管理子系統管理應用程式和服務的 hello 生命的週期。 hello 可測試性子系統可協助應用程式開發人員在部署應用程式和服務 tooproduction 環境前後測試他們的服務，透過模擬的錯誤。 Service Fabric 提供 hello 能力 tooresolve 透過其通訊子系統的服務位置。 hello 公開的 toodevelopers 上層 hello 應用程式模型 tooenable 工具以及這些子系統的應用程式撰寫模型。

## <a name="transport-subsystem"></a>傳輸子系統
hello 傳輸子系統實作點對點資料包通訊通道。 此管道用於 service fabric 叢集內的通訊和 hello service fabric 叢集和用戶端之間的通訊。 它支援單向和要求-回覆通訊模式，提供 hello 基礎實作廣播 」 與 「 在多點傳送 hello 同盟層。 hello 傳輸子系統以便保護通訊安全使用 X509 憑證或 Windows 安全性。 這個子系統由服務網狀架構內部使用，並不是直接存取 toodevelopers 應用程式設計。

## <a name="federation-subsystem"></a>同盟子系統
在順序 tooreason 相關的一組在分散式系統中的節點，您會需要 toohave hello 系統的一致檢視。 hello 同盟子系統使用 hello 傳輸子系統所提供的 hello 通訊原始和 gallery< hello 到可以理解的單一統一叢集中不同節點。 它提供 hello 分散式系統的基本項目所需的 hello 其他子系統-失敗偵測、 前置選擇以及一致的路由。 分散式的雜湊表具有 128 位元的語彙基元空間乃是建立 hello 同盟子系統。 hello 子系統會透過 hello 節點，每個節點中所配置的 hello 語彙基元空間子集的擁有權的 hello 信號建立環狀拓撲。 用於失敗偵測 hello 層會使用租用機制根據核心打和仲裁。 hello 同盟子系統也可保證，透過複雜聯結和出發，隨時都有單一擁有者的語彙基元的通訊協定。 如此可提供前置選擇和一致的路由保證。

## <a name="reliability-subsystem"></a>可靠性子系統
hello 可靠性子系統提供透過 hello hello 使用高可用性的 Service Fabric 服務的 hello 機制 toomake hello 狀態*複寫器*，*容錯移轉管理員*，和*Resource Balancer*。

* hello 複寫器可確保在 hello 主要服務複本的狀態變更會自動複寫的 toosecondary 複本維護服務複本集的 hello 主要和次要複本之間的一致性。 hello 複寫器負責在 hello 複本組中的 hello 複本之間的仲裁管理。 它與 hello 容錯移轉單元 tooget hello 的清單作業 tooreplicate 互動和 hello 重新設定代理程式會將其提供 hello 複本集的 hello 組態。 該設定會指出哪些複本 hello 作業需要 toobe 複寫。 Service Fabric 提供稱為網狀架構複寫器，可供程式設計模型 API toomake hello 服務狀態高度可用且可靠的 hello 預設複寫器。
* hello 容錯移轉管理員可確保，當加入 tooor 從 hello 叢集中移除節點，hello 負載自動重新分配跨 hello 可用的節點。 如果 hello 叢集中的節點失敗，則 hello 叢集會自動重新設定 hello 服務複本 toomaintain 可用性。
* hello 資源管理員將服務複本放在 hello 叢集中的錯誤網域，並確保所有的容錯移轉單元運作正常。 hello 資源管理員也會在服務資源 hello 基礎的叢集節點 tooachieve 最佳統一的負載分配的共用集區之間取得平衡。

## <a name="management-subsystem"></a>管理子系統
hello 管理子系統提供端對端服務和應用程式生命週期管理。 PowerShell cmdlet 和系統管理 Api tooprovision 可讓您、 部署修補程式，升級和解除佈建應用程式不會遺失的可用性。 hello 管理子系統會執行這透過下列服務的 hello。

* **叢集管理員**： 這是 hello 與 hello 容錯移轉管理員從依據 hello 服務位置條件約束的 hello 節點上的可靠性 tooplace hello 應用程式互動的主要服務。 在容錯移轉子系統中的 hello 資源管理員可確保 hello 條件約束是永遠不會中斷。 hello 叢集管理員會管理 hello hello 應用程式生命週期，從佈建 toode 佈建。 它會與 hello 健全狀況管理員 tooensure，應用程式的可用性不會遺失語意的健全狀況的觀點在升級期間進行整合。
* **健康狀態管理員**：此服務會啟用應用程式、服務和叢集實體的健康狀態監視。 （例如節點、 服務分割和複本） 的叢集實體可以報告健全狀況資訊，然後彙總成 hello 集中式的健全狀況存放區。 此健全狀況資訊提供任何所需的修正動作的整體中時間點健全狀況的快照集服務 hello 和分散到多個節點在 hello 叢集中，讓您 tootake 的節點。 健全狀況查詢 Api 可讓您 tooquery hello 健全狀況事件會報告 toohello 健全狀況子系統。 hello 健全狀況查詢 Api 會傳回儲存在 hello 健全狀況的 hello 未經處理的健全狀況資料存放區或 hello 彙總，解譯指定的叢集實體健全狀況資料。
* **映像存放區**： 此服務會提供儲存體和 hello 發佈應用程式二進位檔。 此服務會提供簡單的分散式的檔案存放 hello 應用程式上傳的 tooand 從下載。

## <a name="hosting-subsystem"></a>主控子系統
hello 叢集管理員會通知 hello 裝載子系統 （每個節點上執行） 服務它需要 toomanage 特定節點。 然後裝載子系統的 hello 管理 hello hello 該節點上的應用程式生命週期。 它會與 hello 可靠性及健康情況元件 tooensure hello 複本位置是正確和狀況良好互動。

## <a name="communication-subsystem"></a>通訊子系統
這個子系統提供 hello 叢集服務探索透過 hello 命名服務內的可信賴傳訊。 hello 命名服務解析 hello 叢集中的服務名稱 tooa 位置，並可讓使用者 toomanage 服務名稱和屬性。 使用 hello 命名服務，用戶端可以安全地與 hello 叢集 tooresolve 中的任何節點，進行通訊的服務名稱，擷取服務中繼資料。 使用簡單的命名用戶端應用程式開發介面，Service Fabric 的使用者可以開發服務和用戶端能夠解析不管節點了，還是 hello 重新調整大小的 hello 叢集 hello 目前網路位置。

## <a name="testability-subsystem"></a>可測試性子系統
可測試性是一組工具套件，專門用來測試建置於 Service Fabric 上的服務。 hello 工具可讓開發人員輕鬆地產生有意義的錯誤和執行測試案例 tooexercise 和驗證 hello 許多狀態和轉換，服務會在其存留期，發生在受控制且安全的方式。 可測試性也會提供機制 toorun 較長的測試，可逐一各種可能發生的失敗不會遺失可用性。 如此可為您提供生產環境中的測試。

