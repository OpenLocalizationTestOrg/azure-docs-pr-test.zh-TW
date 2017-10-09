---
title: "Service Fabric 服務的 aaaAvailability |Microsoft 文件"
description: "描述錯誤偵測、容錯移轉與服務復原"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c443aadfe31a1413359b08d34c4b7dd5db4edd16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="availability-of-service-fabric-services"></a>Service Fabric 服務的可用性
本文章概述 Service Fabric 如何維護服務的可用性。

## <a name="availability-of-service-fabric-stateless-services"></a>Service Fabric 無狀態服務的可用性
Azure Service Fabric 服務可能是具狀態或無狀態。 無狀態服務是沒有任何應用程式服務[本機狀態](service-fabric-concepts-state.md)需要 toobe 高度可用或可靠。

建立無狀態服務需要定義 `InstanceCount`。 hello 執行個體計數定義 hello hello 無狀態服務的應用程式邏輯，應該在 hello 叢集中執行的執行個體數目。 執行個體的 hello 數目增加為 hello 建議的向外延展無狀態服務的方式。

無狀態的名為 service 執行個體失敗時，某些合格 hello 叢集中節點上建立的新執行個體。 例如，無狀態服務執行個體可能會在 Node1 上失敗並在 Node5 上重新建立。

## <a name="availability-of-service-fabric-stateful-services"></a>Service Fabric 可設定狀態服務的可用性
具狀態服務具有某些與其相關聯的狀態。 在 Service Fabric 中，可設定狀態服務會模型化為複本集。 每個複本是 hello hello 服務也有一份該服務的 hello 狀態碼的執行個體。 讀取和寫入作業會執行一個複本 （稱為 hello 主要）。 會從寫入作業變更 toostate*複寫*toohello hello 複本設定 （稱為作用中次要資料庫） 中的其他複本及套用。 

只能有一個「主要複本」，但可以有多個「作用中次要複本」。 作用中次要複本的 hello 數目可設定，而有較多的複本可容許更多並行的軟體和硬體故障。

如果 hello 主要複本已關閉時，Service Fabric，使其中一個 hello 作用中次要複本 hello 新的主要複本。 這個作用中次要複本已有更新的 hello 版本 hello 狀態 (透過*複寫*)，以及它可以繼續處理其他的讀取和寫入作業。

主要或作用中次要複本的這個概念，稱為 hello 複本角色。

### <a name="replica-roles"></a>複本角色
hello 複本的角色是狀態的使用的 toomanage hello 生命週期的 hello 受該複本。 扮演「主要」角色的複本會為讀取要求提供服務。 hello 主要也可以更新其狀態，並複寫 hello 變更處理所有寫入要求。 這些變更會套用的 toohello hello 複本集中作用中次要資料庫。 作用中次要的 hello 作業是 tooreceive hello 主要複本的狀態變更已複寫，並更新其 hello 狀態的檢視。

> [!NOTE]
> 較高層級的程式設計模型例如[Reliable Actors](service-fabric-reliable-actors-introduction.md)和[可靠服務](service-fabric-reliable-services-introduction.md)隱藏 hello 概念 hello 位開發人員的複本角色。 動作項目，在 hello 概念的角色中不需要，同時它主要簡化在大部分情況下的服務。
>

## <a name="next-steps"></a>後續步驟
如需有關 Service Fabric 概念的詳細資訊，請參閱下列文章 hello:

- [調整 Service Fabric 服務](service-fabric-concepts-scalability.md)
- [分割 Service Fabric 服務](service-fabric-concepts-partitioning.md)
- [定義和管理狀態](service-fabric-concepts-state.md)
- [Reliable Services](service-fabric-reliable-services-introduction.md)
