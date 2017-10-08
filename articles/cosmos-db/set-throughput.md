---
title: "Azure Cosmos DB aaaProvision 輸送量 |Microsoft 文件"
description: "了解如何 tooset 佈建 Azure Cosmos DB containsers、 集合、 圖表和資料表的輸送量。"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a>設定 Azure Cosmos DB 容器的輸送量

您可以為您的 Azure Cosmos DB 容器 hello Azure 入口網站中設定輸送量或使用 hello 的用戶端 Sdk。 

hello 下表列出適用於容器的 hello 輸送量：

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><strong>單一資料分割容器</strong></p></td>
            <td valign="top"><p><strong>已資料分割的容器</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>輸送量下限</p></td>
            <td valign="top"><p>每秒 400 個要求單位</p></td>
            <td valign="top"><p>每秒 2,500 個要求單位</p></td>
        </tr>
        <tr>
            <td valign="top"><p>輸送量上限</p></td>
            <td valign="top"><p>每秒 10,000 個要求單位</p></td>
            <td valign="top"><p>無限</p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a>使用 Azure 入口網站 hello tooset hello 輸送量

1. 在新視窗中，開啟 hello [Azure 入口網站](https://portal.azure.com)。
2. Hello 左列上，按一下**Azure Cosmos DB**，或按一下**更服務**hello 底部，然後捲動太**資料庫**，然後按一下 **Azure Cosmos DB**.
3. 選取您的 Cosmos DB 帳戶。
4. 在 hello 新視窗中，按一下 **資料總管 （預覽）** hello 瀏覽功能表中。
5. 在 hello 新視窗中，展開您的資料庫和容器，然後按一下**小數位數 （& s) 設定**。
6. 在 hello 新視窗中，輸入 hello 新處理量值在 hello**輸送量**方塊，然後再按一下**儲存**。

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a>使用適用於.NET 的 hello DocumentDB API tooset hello 輸送量

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a>輸送量常見問題集

**可以設定我比 400 RU/秒的輸送量 tooless 嗎？**

400 RU/秒是 hello Cosmos DB 單一資料分割的集合 （2500 RU/秒 hello 的分割區集合最小值） 上可用的最小輸送量。 要求單位設定以 100 RU/秒間隔，但輸送量無法設定 too100 RU/秒或任何值小於 400 RU/秒。 如果您要尋找符合成本效益的方法 toodevelop 和測試 Cosmos DB 時，您可以使用可用的 hello [Azure Cosmos DB 模擬器](local-emulator.md)，其中您可以在本機部署不花一毛錢。 

**如何設定使用 hello MongoDB API througput？**

沒有任何 MongoDB API 延伸模組 tooset 輸送量。 hello 建議 toouse hello DocumentDB API 中所示[hello DocumentDB API 使用適用於.NET 的 tooset hello 輸送量](#set-throughput-sdk)。

## <a name="next-steps"></a>後續步驟

請參閱深入了解佈建和持續地球位小數位數以 Cosmos DB toolearn[資料分割和調整以 Cosmos DB](partition-data.md)。
