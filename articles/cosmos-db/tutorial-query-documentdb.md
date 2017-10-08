---
title: "Azure Cosmos DB 中的 SQL aaaHow tooquery 嗎？ | Microsoft Docs"
description: "了解 tooquery DocumentDB SQL Azure Cosmos DB 中的資料"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d3dc51acf92cb78d4f4d9dbac7ec54b1382431cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a>Azure Cosmos DB： 如何使用 SQL tooquery 嗎？

hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md)查詢使用 SQL 的文件的支援。 本文提供一個範例文件及兩個範例 SQL 查詢和結果。

本文涵蓋下列工作的 hello: 

> [!div class="checklist"]
> * 使用 SQL 來查詢資料

## <a name="sample-document"></a>範例文件

本文章中的 hello SQL 查詢使用 hello 遵循範例文件。

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

您可以使用執行查詢 hello hello 透過 Azure 入口網站中的 hello 資料總管[REST API 和 Sdk](documentdb-sdk-dotnet.md)，甚至 hello 和[查詢遊樂場](https://www.documentdb.com/sql/demo)，現有的範例資料集上執行查詢。

如需有關 SQL 查詢的詳細資訊，請參閱：
* [SQL 查詢和 SQL 語法](documentdb-sql-query.md)

## <a name="prerequisites"></a>必要條件

本教學課程會假設您具備 Azure Cosmos DB 帳戶和集合。 不符合上述其中任何一項條件嗎？ 完整的 hello [5 分鐘快速入門](create-mongodb-nodejs.md)或 hello[開發人員教學課程](tutorial-develop-mongodb.md)toocreate 帳戶和集合。

## <a name="example-query-1"></a>範例查詢 1

給定 hello 範例系列文件上方，下列 SQL 查詢會傳回 hello 文件符合 hello 識別碼 欄位的位置`WakefieldFamily`。 因為它是`SELECT *`陳述式，hello 查詢的 hello 輸出是 hello 完整的 JSON 文件：

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

hello 下一個查詢會傳回所有 hello 指定名稱的子系中 hello 系列，其識別碼符合`WakefieldFamily`依其等級。

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

在本教學課程中，您們 hello 下列：

> [!div class="checklist"]
> * 了解如何使用 SQL tooquery  

您現在可以如何繼續 toohello 下一個教學課程 toolearn toodistribute 資料全域。

> [!div class="nextstepaction"]
> [全域散發您的資料](tutorial-global-distribution-documentdb.md)

