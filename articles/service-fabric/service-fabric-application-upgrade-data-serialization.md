---
title: "應用程式升級：資料序列化 | Microsoft Docs"
description: "資料序列化的最佳作法，以及它如何影響應用程式輪流升級。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: a5f36366-a2ab-4ae3-bb08-bc2f9533bc5a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 1b65dfd3813423550631490640a81953864f58e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-data-serialization-affects-an-application-upgrade"></a>資料序列化如何影響應用程式升級
在[復原應用程式升級](service-fabric-application-upgrade.md)，hello 升級已套用的 tooa 節點的子集，一次一個升級網域。 在此過程中，某些升級網域 hello 較新版本的應用程式，而某些升級網域上 hello 較舊版本的應用程式。 Hello 首展期間 hello 新版本的應用程式必須是能夠 tooread hello 舊版本的資料，而且 hello 舊版本的應用程式必須能夠 tooread hello 新版本的資料。 如果 hello 資料格式不是向前和向後相容，hello 升級可能會失敗，或更糟的是，資料可能遺失或損毀。 本文將討論您資料格式的構成項目並提供最佳作法，以確保您的資料向前及向後相容。

## <a name="what-makes-up-your-data-format"></a>資料格式的構成項目？
在 Azure Service Fabric，hello 資料，可保存和複寫來自 C# 類別。 使用的應用程式[可靠集合](service-fabric-reliable-services-reliable-collections.md)，資料是 hello hello 可靠字典與佇列中的物件。 使用的應用程式[Reliable Actors](service-fabric-reliable-actors-introduction.md)，也就是支援的 hello 動作項目狀態的 hello。 下列 C# 類別必須是可序列化 toobe 保存和複寫。 因此，由 hello 欄位和屬性進行序列化，以及如何它們會序列化定義 hello 資料格式。 例如，在`IReliableDictionary<int, MyClass>`hello 資料會序列化`int`和序列化`MyClass`。

### <a name="code-changes-that-result-in-a-data-format-change"></a>程式碼變更造成資料格式變更
Hello 資料格式由 C# 類別，因為變更 toohello 類別可能會導致資料格式變更。 必須小心，輪流升級可處理 tooensure hello 資料格式變更。 可能會造成資料格式變更的範例：

* 新增或移除欄位或屬性
* 重新命名欄位或屬性
* 變更 hello 類型的欄位或屬性
* 變更 hello 類別名稱或命名空間

### <a name="data-contract-as-hello-default-serializer"></a>資料合約，如 hello 預設序列化程式
hello 序列化程式通常需負責讀取 hello 資料和還原序列化成 hello 新版本，即使 hello 資料是在較舊或*較新*版本。 hello 預設序列化程式為 hello[資料合約序列化程式](https://msdn.microsoft.com/library/ms733127.aspx)，其具有妥善定義的版本控制規則。 集合允許 hello 序列化程式 toobe 覆寫，但 Reliable Actors 目前並不可靠。 hello 資料序列化程式扮演重要角色啟用輪流升級。 hello 資料合約序列化程式是我們建議您針對 Service Fabric 應用程式的 hello 序列化程式。

## <a name="how-hello-data-format-affects-a-rolling-upgrade"></a>Hello 資料格式會輪流升級的影響
輪流升級時，有兩個 hello 序列化程式可能會遇到較舊的主要案例或*較新*資料的版本：

1. 節點會升級，並重新啟動之後，hello 新的序列化程式會載入已保存的 toodisk hello 舊版本的 hello 資料。
2. 期間 hello 輪流升級，hello 叢集會包含程式碼的 hello 舊的和新版本的混合。 因為複本可能會放置於不同的升級網域，而且複本會將傳送資料 tooeach 其他 hello 新及/或舊版本的資料可能會遇到 hello 新及/或舊版本的序列化程式。

> [!NOTE]
> 「 新的版本 」 和 「 舊的版本 」 hello 這裡參照 toohello 版本您正在執行的程式碼。 hello 「 新的序列化程式 」 是指在 hello 新版本的應用程式正在執行的 toohello 序列化程式程式碼。 hello 「 新的資料 」 指的是應用的序列化 toohello C# 類別從 hello 新版本程式。
> 
> 

hello 兩個版本的程式碼和資料格式必須是向前和向後相容。 如果不相容，hello 輪流升級可能會失敗，或可能會遺失資料。 hello 輪流升級可能會失敗，因為 hello 程式碼或序列化程式可能會擲回例外狀況或錯誤時遇到 hello 另一個版本。 如果，例如，已加入新屬性，但 hello 舊的序列化程式會捨棄它在還原序列化期間，可能會遺失資料。

資料合約為建議的解決方案，可確保您的資料相容的 hello。 它有新增、移除及變更欄位的定義完善版本控制規則。 它也有支援處理具有未知的欄位、 攔截到 hello 序列化和還原序列化程序，和處理的類別繼承。 如需詳細資訊，請參閱 [使用資料合約](https://msdn.microsoft.com/library/ms733127.aspx)。

## <a name="next-steps"></a>後續步驟
[使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md) 將引導您完成使用 Visual Studio 進行應用程式升級的步驟。

[使用 PowerShell 升級您的應用程式](service-fabric-application-upgrade-tutorial-powershell.md) 將引導您完成使用 PowerShell 進行應用程式升級的步驟。

使用 [升級參數](service-fabric-application-upgrade-parameters.md)來控制您應用程式的升級方式。

了解 toouse 把太升級您的應用程式時所進階的功能[進階主題](service-fabric-application-upgrade-advanced.md)。

藉由參考 toohello 步驟中的修正應用程式升級的一般問題[疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)。

