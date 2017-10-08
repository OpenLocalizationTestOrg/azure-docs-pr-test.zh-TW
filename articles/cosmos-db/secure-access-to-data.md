---
title: "aaaLearn toosecure 如何存取在 Azure Cosmos DB toodata |Microsoft 文件"
description: "深入了解 Azure Cosmos DB 中的存取控制概念，其中包括主要金鑰、唯讀金鑰、使用者和權限。"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 8641225d-e839-4ba6-a6fd-d6314ae3a51c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: fef7f8e14b488f6ceab0f2aa279a1e99d4416f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-cosmos-db-data"></a>保護存取 tooAzure Cosmos DB 的資料
本文提供的保護儲存在存取 toodata 概觀[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)。

Azure Cosmos DB 會使用兩種類型的索引鍵 tooauthenticate 使用者，並提供存取 tooits 資料和資源。 

|金鑰類型|資源|
|---|---|
|[主要金鑰](#master-keys) |用於系統管理資源︰資料庫帳戶、資料庫、使用者和權限|
|[資源權杖](#resource-tokens)|用於應用程式資源︰集合、文件、附件、預存程序、觸發程序和 UDF|

<a id="master-keys"></a>

## <a name="master-keys"></a>主要金鑰 

主要金鑰提供 hello 資料庫帳戶存取 toohello 所有 hello 管理資源。 主要金鑰：  
- 提供存取 tooaccounts、 資料庫、 使用者和權限。 
- 不能使用的 tooprovide 細微的存取權 toocollections 和文件。
- 在 hello 建立帳戶期間建立。
- 可隨時重新產生。

每個帳戶包含兩個主要金鑰︰主要金鑰和次要金鑰。 hello 雙重機碼的目的是，讓您可以重新產生，或復原金鑰，提供持續存取 tooyour 帳戶和資料。 

在加法 toohello 兩個主要金鑰的 hello Cosmos DB 帳戶，有兩個唯讀的索引鍵。 這些的唯讀機碼，僅允許 hello 帳戶上的讀取的作業。 唯讀金鑰並不提供存取 tooread 權限資源。

主要、 次要唯讀狀態，而且可以擷取讀寫主要金鑰，並且使用 hello Azure 入口網站重新產生。 相關指示請參閱[檢視、複製和重新產生存取金鑰](manage-account.md#keys)。

![在 hello Azure 入口網站-示範 NoSQL 資料庫安全性的存取控制 (IAM)](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

hello 的旋轉您的主要金鑰的程序很簡單。 瀏覽 toohello Azure 入口網站 tooretrieve 次要的索引鍵，然後以您在應用程式中的次要金鑰取代主索引鍵然後旋轉 hello hello Azure 入口網站中的主索引鍵。

![在 hello Azure 入口網站-示範 NoSQL 資料庫安全性的主要金鑰輪替](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a>程式碼範例 toouse 主要金鑰

hello 下列程式碼範例說明如何 toouse Cosmos DB 帳戶端點和服務主要金鑰 tooinstantiate DocumentClient 及建立資料庫。 

```csharp
//Read hello Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from hello Azure portal on hello Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access tooyour DocDB account.

private static readonly string endpointUrl = ConfigurationManager.AppSettings["EndPointUrl"];
private static readonly SecureString authorizationKey = ToSecureString(ConfigurationManager.AppSettings["AuthorizationKey"]);

client = new DocumentClient(new Uri(endpointUrl), authorizationKey);

// Create Database
Database database = await client.CreateDatabaseAsync(
    new Database
    {
        Id = databaseName
    });
```

<a id="resource-tokens"></a>

## <a name="resource-tokens"></a>資源權杖

資源語彙基元提供 toohello 資料庫內的應用程式資源的存取。 資源權杖：
- 提供存取 toospecific 集合、 資料分割索引鍵、 文件、 附件、 預存程序、 觸發程序和 Udf。
- 時，會建立[使用者](#users)授與[權限](#permissions)tooa 特定資源。
- 使用 POST、GET 或 PUT 呼叫處理權限資源時重新建立。
- 使用雜湊資源的語彙基元，特別是建構 hello 使用者、 資源和權限。
- 是與可自訂的有效期間繫結的時間。 hello 有效時間範圍為 1 小時。 權杖存留期，不過，可明確指定，向上 tooa 最多五個小時。
- 提供安全的替代 toogiving 出 hello 主要金鑰。 
- 啟用用戶端 tooread、 寫入和刪除資源，根據 toohello 他們已被授與的權限的 hello Cosmos DB 帳戶中。

您可以使用為資源語彙基元 （藉由建立 Cosmos DB 使用者和權限） 當您想在 Cosmos DB tooprovide 存取 tooresources 帳戶 tooa 用戶端無法信任 hello 主要金鑰。  

Cosmos DB 資源語彙基元提供安全的替代方案，可讓用戶端 tooread、 寫入和刪除資源，根據 toohello 權限已授與，Cosmos DB 帳戶中，而需要在主版，或讀取唯一索引鍵。

以下是典型的設計模式，藉此資源語彙基元可能要求、 產生，並傳遞 tooclients:

1. 中間層服務設定 tooserve 行動應用程式 tooshare 使用者相片。 
2. hello 中間層服務擁有 hello hello Cosmos 資料庫帳戶主要金鑰。
3. hello 相片應用程式會安裝在使用者的行動裝置上。 
4. 在登入時，hello 相片應用程式會建立 hello 與 hello 中間層服務的 hello 使用者識別。 這項機制的身分識別建立已完全啟動 toohello 應用程式。
5. 一旦建立 hello 身分識別，hello 中間層服務要求 hello 識別為基礎的權限。
6. hello 中間層服務會傳送為資源語彙基元後 toohello phone 應用程式。
7. hello 電話應用程式可以繼續 toouse hello 資源語彙基元 toodirectly Cosmos DB 存取的資源定義 hello 資源語彙基元和 hello 間隔 hello 資源語彙基元所允許的 hello 權限。 
8. Hello 資源權杖過期時，後續要求就會收到 401 未授權例外狀況。  此時，hello 電話應用程式會重新建立 hello 身分識別，並要求新的資源權杖。

    ![Azure Cosmos DB 資源權杖工作流程](./media/secure-access-to-data/resourcekeyworkflow.png)

資源權杖的產生和管理是由原生 Cosmos DB 用戶端程式庫 hello; 處理不過，如果您使用 REST，您必須建構 hello 要求/驗證標頭。 如需有關如何建立 REST 驗證標頭的詳細資訊，請參閱[Cosmos DB 資源的存取控制](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources)或 hello[原始程式碼我們 sdk](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js)。

中介層服務的範例使用 toogenerate 或 broker 資源語彙基元，請參閱 hello [ResourceTokenBroker 應用程式](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers)。

<a id="users"></a>

## <a name="users"></a>使用者
Cosmos DB 使用者會與 Cosmos DB 資料庫相關聯。  每個資料庫都包含零個或多個 Cosmos DB 使用者。  hello 下列程式碼範例會示範如何 toocreate Cosmos DB 使用者資源。

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> 每個的 Cosmos DB 使用者都可以是使用的 tooretrieve hello 清單 PermissionsLink 屬性[權限](#permissions)hello 使用者相關聯。
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a>權限
Cosmos DB 權限資源會與 Cosmos DB 使用者相關聯。  每位使用者都包含零個或多個 Cosmos DB 權限。  權限資源會提供 hello 使用者需求時，嘗試 tooaccess 特定應用程式資源的存取 tooa 安全性權杖。
權限資源可能提供兩種可用的存取等級：

* All: hello 使用者 hello 資源上具有完整權限。
* 請閱讀： hello 使用者只能讀取 hello hello 資源內容，但無法寫入、 更新或刪除作業 hello 資源上的執行。

> [!NOTE]
> 在訂單 toorun Cosmos DB 預存程序 hello 使用者必須具有 hello All 權限將會執行預存程序中的 hello hello 集合上。
> 
> 

### <a name="code-sample-toocreate-permission"></a>程式碼範例 toocreate 權限

hello 下列程式碼範例顯示如何 toocreate 權限資源，讀取 hello hello 權限資源，資源語彙基元和 hello 權限聯 hello[使用者](#users)上面所建立。

```csharp
// Create a permission.
Permission docPermission = new Permission
{
    PermissionMode = PermissionMode.Read,
    ResourceLink = documentCollection.SelfLink,
    Id = "readperm"
};
  
docPermission = await client.CreatePermissionAsync(UriFactory.CreateUserUri("db", "user"), docPermission);
Console.WriteLine(docPermission.Id + " has token of: " + docPermission.Token);
```

如果您已經指定您的集合，然後 hello 權限集合中，文件，而附件資源的資料分割索引鍵也必須包含 hello ResourcePartitionKey 加法 toohello ResourceLink 中。

### <a name="code-sample-tooread-permissions-for-user"></a>使用者的程式碼範例 tooread 權限

tooeasily 取得所有與特定使用者相關聯的權限資源，但是 Cosmos DB 可用權限摘要每個使用者物件。  hello 下列程式碼片段示範上述 tooretrieve hello 權限與 hello 使用者相關聯的建立方式、 建構權限清單，並具現化新 DocumentClient 代表 hello 使用者。

```csharp
//Read a permission feed.
FeedResponse<Permission> permFeed = await client.ReadPermissionFeedAsync(
  UriFactory.CreateUserUri("db", "myUser"));
 List<Permission> permList = new List<Permission>();

foreach (Permission perm in permFeed)
{
    permList.Add(perm);
}

DocumentClient userClient = new DocumentClient(new Uri(endpointUrl), permList);
```

## <a name="next-steps"></a>後續步驟
* toolearn 進一步了解 Cosmos DB 資料庫安全性，請參閱[Cosmos DB： 資料庫安全性](database-security.md)。
* toolearn 有關管理主要和唯讀索引鍵，請參閱[如何 toomanage Azure Cosmos DB 帳戶](manage-account.md#keys)。
* 如何 tooconstruct Azure Cosmos DB 授權權杖，請參閱的 toolearn [Azure Cosmos DB 資源的存取控制](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources)。
