---
title: "適用於資料表 API 的 Azure Cosmos DB 全域散發教學課程 | Microsoft Docs"
description: "了解如何使用「資料表 API」來設定 Azure Cosmos DB 全域散發。"
services: cosmos-db
keywords: "全域散發, 資料表"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 63c9e530a4982e2e6e478fea56e015fc77851e1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-table-api"></a>如何使用資料表 API 來設定 Azure Cosmos DB 全域散發

在本文中，我們會說明如何使用 Azure 入口網站來設定 Azure Cosmos DB 全域散發，然後使用「資料表 API」(預覽) 來進行連線。

本文涵蓋下列工作： 

> [!div class="checklist"]
> * 使用 Azure 入口網站來設定全域散發
> * 使用[資料表 API](table-introduction.md) 來設定全域散發

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-table-api"></a>使用資料表 API 來連線到慣用的區域

為了充分運用 [全球發佈](distribute-data-globally.md)，用戶端應用程式可以指定已排序的區域喜好設定清單，以用來執行文件作業。 透過在預覽版「Azure 儲存體 SDK」的應用程式設定中設定 `TablePreferredLocations` 組態值，即可達到此目的。 「Azure 儲存體 SDK」將會根據 Azure Cosmos DB 帳戶組態、目前的區域可用性及所指定的喜好設定清單，選擇最適合的端點來執行寫入和讀取作業。

`TablePreferredLocations` 應該包含一個供讀取使用的慣用 (多路連接) 位置逗號分隔清單。 每個用戶端執行個體可以依慣用順序指定這些區域的子集，供低延遲讀取使用。 指定這些區域時，必須使用其[顯示名稱](https://msdn.microsoft.com/library/azure/gg441293.aspx)，例如 `West US`。

所有讀取都會傳送到 `TablePreferredLocations` 清單中的第一個可用區域。 如果要求失敗，用戶端將無法往下到清單中的下一個區域，依此類推。

SDK 只會嘗試從 `TablePreferredLocations` 中指定的區域讀取。 因此，舉例來說，如果在三個區域中有「資料庫帳戶」可供使用，但用戶端只為 `TablePreferredLocations` 指定其中兩個非寫入區域，這樣就不會從寫入區域為任何讀取提供服務，即使發生容錯移轉時也一樣。

SDK 會自動將所有寫入傳送至目前的寫入區域。

如果未設定 `TablePreferredLocations` 屬性，將會從目前的寫入區域為所有要求提供服務。

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

就這麼簡單，這樣便已完成本教學課程。 您可以透過閱讀 [Azure Cosmos DB 中的一致性層級](consistency-levels.md)，來了解如何管理全域複寫帳戶的一致性。 如需有關 Azure Cosmos DB 中全域資料庫複寫運作方式的詳細資訊，請參閱[使用 Azure Cosmos DB 來全域散發資料](distribute-data-globally.md)。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已完成下列操作：

> [!div class="checklist"]
> * 使用 Azure 入口網站來設定全域散發
> * 使用 DocumentDB API 來設定全域散發

您現在可以繼續進行到下一個教學課程，以了解如何使用 Azure Cosmos DB 本機模擬器在本機進行開發。

> [!div class="nextstepaction"]
> [使用模擬器在本機進行開發](local-emulator.md)