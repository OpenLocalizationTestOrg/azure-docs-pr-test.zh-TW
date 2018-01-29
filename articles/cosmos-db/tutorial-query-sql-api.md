---
title: "如何在 Azure Cosmos DB 中使用 SQL 進行查詢？ | Microsoft Docs"
description: "了解如何使用 Azure Cosmos DB 中的 SQL 查詢"
services: cosmos-db
documentationcenter: 
author: rafats
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: tutorial-develop, mvc
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: rafats
ms.openlocfilehash: ffef6ec2120a80d907449470efb7b4ab6dca8037
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="azure-cosmos-db-how-to-query-using-sql"></a>Azure Cosmos DB：如何使用 SQL 來進行查詢？

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

Azure Cosmos DB [SQL API](documentdb-introduction.md)查詢使用 SQL 的文件的支援。 本文提供一個範例文件及兩個範例 SQL 查詢和結果。

本文涵蓋下列工作： 

> [!div class="checklist"]
> * 使用 SQL 來查詢資料

## <a name="sample-document"></a>範例文件

本文中的 SQL 查詢使用下列範例文件。

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```
## <a name="where-can-i-run-sql-queries"></a>我可以在哪裡執行 SQL 查詢？

您可以使用 Azure 入口網站中的 [資料總管]、透過 [REST API 和 SDK](sql-api-sdk-dotnet.md)，甚至是 [Query Playground](https://www.documentdb.com/sql/demo) (在一組現有的範例資料上執行查詢)，來執行查詢。

如需有關 SQL 查詢的詳細資訊，請參閱：
* [SQL 查詢和 SQL 語法](sql-api-sql-query.md)

## <a name="prerequisites"></a>必要條件

本教學課程會假設您具備 Azure Cosmos DB 帳戶和集合。 不符合上述其中任何一項條件嗎？ 請完成 [5 分鐘快速入門](create-mongodb-nodejs.md)或[開發人員教學課程](tutorial-develop-mongodb.md)，以建立帳戶和集合。

## <a name="example-query-1"></a>範例查詢 1

在提供上述範例家族文件的情況下，下列 SQL 查詢會傳回識別碼欄位符合 `WakefieldFamily` 的文件。 由於它是一個 `SELECT *` 陳述式，因為查詢的輸出是完整的 JSON 文件：

**查詢**

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

**結果**

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

## <a name="example-query-2"></a>範例查詢 2

下一個查詢會傳回家族中識別碼符合 `WakefieldFamily` 的小孩名字，並依年級排序。

**查詢**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

**結果**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a>後續步驟

在本教學課程中，您已完成下列操作：

> [!div class="checklist"]
> * 了解如何使用 SQL 來進行查詢  

您現在可以繼續進行到下一個教學課程，以了解如何全域散發您的資料。

> [!div class="nextstepaction"]
> [全域散發您的資料](tutorial-global-distribution-sql-api.md)

