---
title: "資料表 api aaaAzure Cosmos DB 全域發佈教學課程 |Microsoft 文件"
description: "了解如何使用全域發佈 toosetup Azure Cosmos DB hello 表格 API。"
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
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a>如何使用全域發佈 toosetup Azure Cosmos DB hello 表格 API

在本文中，我們會示範如何 toouse hello Azure 入口網站 toosetup Azure Cosmos DB 全域發佈，然後使用 hello 表格 API （預覽） 連接。

本文涵蓋下列工作的 hello: 

> [!div class="checklist"]
> * 設定全域發佈使用 hello Azure 入口網站
> * 設定全域發佈使用 hello[表格 API](table-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a>連接使用 hello 表格 API tooa 慣用的區域

中的順序 tootake 優點[全域發佈](distribute-data-globally.md)，用戶端應用程式可以指定 hello 排序喜好設定清單中的區域 toobe 用 tooperform 文件的作業。 這可藉由設定 hello `TablePreferredLocations` hello hello 預覽 Azure 儲存體 SDK 的應用程式組態中的組態值。 根據 hello Azure Cosmos DB 帳戶設定，目前的地區可用性與 hello 喜好設定指定的清單，大部分的最佳端點將會選擇的 hello Azure 儲存體 SDK tooperform hello 寫入和讀取作業。

hello`TablePreferredLocations`應包含以逗號分隔清單的慣用 （多路連接） 的位置供讀取。 每個用戶端執行個體可以針對低度延遲讀取 hello 慣用順序指定這些區域的子集。 必須使用命名 hello 區及其[顯示名稱](https://msdn.microsoft.com/library/azure/gg441293.aspx)，例如`West US`。

所有的讀取將會傳送 toohello 第一個可用的地區中 hello`TablePreferredLocations`清單。 如果 hello 要求失敗，hello 用戶端會向 hello 清單 toohello 下一個區域，失敗等等。

hello SDK 只會嘗試從 hello 區域中指定 tooread `TablePreferredLocations`。 因此，比方說，如果 hello 資料庫帳戶有三個區域，但是 hello 用戶端只會指定兩個 hello 非寫入區域`TablePreferredLocations`，然後讀取將會由 hello 寫入區域，即使在 hello 的容錯移轉的情況下提供服務。

hello SDK 都會自動傳送所有寫入 toohello 目前寫入的區域。

如果 hello`TablePreferredLocations`屬性未設定，所有的要求將由 hello 目前寫入區域。

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

就這麼簡單，這樣便已完成本教學課程。 您可以了解如何 toomanage hello 所讀取的一致性，您的全球複寫帳戶[Azure Cosmos DB 中的一致性層級](consistency-levels.md)。 如需有關 Azure Cosmos DB 中全域資料庫複寫運作方式的詳細資訊，請參閱[使用 Azure Cosmos DB 來全域散發資料](distribute-data-globally.md)。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您們 hello 下列：

> [!div class="checklist"]
> * 設定全域發佈使用 hello Azure 入口網站
> * 設定全域發佈使用 hello DocumentDB Api

您可以現在繼續 toohello 下一個教學課程 toolearn 如何使用在本機的 toodevelop hello Azure Cosmos DB 本機模擬器。

> [!div class="nextstepaction"]
> [與 hello 模擬器在本機開發](local-emulator.md)
