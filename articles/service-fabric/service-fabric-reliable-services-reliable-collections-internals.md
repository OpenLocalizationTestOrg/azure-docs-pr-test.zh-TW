---
title: "服務網狀架構可靠狀態管理員和可靠的集合內部 aaaAzure |Microsoft 文件"
description: "深入了解 Reliable Collection 概念和 Azure Service Fabric 設計。"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a>Azure Service Fabric Reliable State Manager 與 Reliable Collection 內部
這份文件是可靠的狀態管理員和可靠的集合 toosee 內探索核心元件 hello 幕後的運作方式。

> [!NOTE]
> 這份文件仍在處理中。 加入註解 toothis 文章 tootell 我們主題，您想要深入了解 toolearn。
>

##  <a name="local-persistence-model-log-and-checkpoint"></a>本機持續性模型︰記錄和檢查點
hello 可靠狀態管理員和可靠的集合，請遵循稱為記錄檔和檢查點的持續性模型。
在此模型中，每個狀態變更會先記錄在磁碟上，然後套用在記憶體中。
hello 完成本身被保存的狀態只是偶爾 （也稱為 檢查點)。
hello 好處是差異會轉換成循序附加專用寫入磁碟上改善效能。

toobetter 了解 hello 記錄和檢查點模型，讓我們先來看 hello 無限磁碟案例。
hello 可靠狀態管理員會記錄每項作業之前它會複寫。
記錄允許 hello 可靠集合 tooapply hello 作業只能在記憶體中。
因為記錄檔會保存，即使 hello 複本失敗且需要重新啟動，toobe hello 可靠狀態管理員有足夠的資訊在其記錄 tooreplay 所有 hello 作業 hello 複本都已遺失。
Hello 磁碟是無限的因為記錄檔記錄永遠不需要移除 toobe 且 hello 可靠集合必須 toomanage 唯一 hello 記憶體中狀態。

現在讓我們看看 hello 有限磁碟案例。
因為記錄檔記錄會累積，hello 可靠狀態管理員將會用完磁碟空間。
發生這種情況，hello 可靠狀態管理員必須 tootruncate 其記錄 toomake 出空間給 hello 較新記錄。
Reliable 狀態管理員要求在其記憶體中狀態 toodisk hello toocheckpoint 可靠的集合。
此時，hello 可靠的集合' 會保存其記憶體中狀態。
Hello 可靠集合完成後的檢查點，hello 可靠狀態管理員可以截斷 hello 記錄 toofree 出磁碟空間。
當 hello 複本需要重新啟動 toobe 時，可靠的集合會復原檢查點狀態，而且 hello 可靠狀態管理員復原播放 hello 最後一個檢查點之後發生的所有 hello 狀態變更。

檢查點新增另一個值可改善一般情況下的復原時間。 記錄檔包含 hello 最後一個檢查點之後發生的所有作業。
因此它可能包含某個項目的多個版本，如 Reliable Dictionary 中特定資料列的多個值。
相反地，可靠的集合檢查點僅 hello 最新版本的每個索引鍵的值。

## <a name="next-steps"></a>後續步驟
* [交易和鎖定](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

