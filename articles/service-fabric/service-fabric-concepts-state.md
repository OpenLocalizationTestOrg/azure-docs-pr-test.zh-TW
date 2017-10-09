---
title: "aaaDefinine 和管理 Azure microservices 狀態 |Microsoft 文件"
description: "如何 toodefine 和管理服務的網狀架構中的服務狀態"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a>服務狀態
**服務狀態**參考 toohello 記憶體或磁碟資料服務需要 toofunction。 它包含，例如 hello 資料結構和成員變數 hello 服務讀取和寫入 toodo 工作。 根據如何 hello 服務的架構，它也可能包括檔案或儲存在磁碟的其他資源。 Hello，例如檔案的資料庫會使用 toostore 資料和交易記錄。

作為範例服務，讓我們考慮計算機。 基本計算機服務會採用兩個數字並傳回其總和。 執行這項計算不會牽涉任何成員變數或其他資訊。

現在請思考一下 hello 相同的計算機，但已經使用其他方法來儲存及傳回 hello 最後一個加總計算。 此服務現在為具狀態。 可設定狀態，表示它包含寫入的 toowhen，它會計算新的總和，並讀取時詢問 tooreturn hello 的最後一個計算的總和的某種狀態。

在 Azure Service Fabric，hello 第一個服務稱為無狀態的服務。 hello 第二個服務會呼叫可設定狀態的服務。

## <a name="storing-service-state"></a>儲存服務狀態
狀態可以外部化或共置 hello 程式碼，它會處理 hello 狀態。 外部化的狀態通常是使用外部資料庫或其他資料存放區 hello 網路上或跨處理序上的不同電腦上執行 hello 同一部電腦。 在計算機範例中，SQL database 或 Azure 資料表存放區執行個體，可能是 hello 資料存放區。 每個要求 toocompute hello 加總這個資料中，執行更新，並要求 toohello 服務 tooreturn hello 值導致 hello 提取從 hello 存放區的目前值。 

狀態也可以共置於 hello 操作 hello 狀態的程式碼。 Service Fabric 中的具狀態服務通常是使用此模型來建置。 Service Fabric 提供 hello 基礎結構 tooensure 此狀態是高度可用、 一致且持久，，和 hello services 內建這種方式可以輕鬆地調整。

## <a name="next-steps"></a>後續步驟
如需有關 Service Fabric 概念的詳細資訊，請參閱下列文章 hello:

* [Service Fabric 服務的可用性](service-fabric-availability-services.md)
* [Service Fabric 服務的延展性](service-fabric-concepts-scalability.md)
* [分割 Service Fabric 服務](service-fabric-concepts-partitioning.md)
* [Service Fabric Reliable Services](service-fabric-reliable-services-introduction.md)
