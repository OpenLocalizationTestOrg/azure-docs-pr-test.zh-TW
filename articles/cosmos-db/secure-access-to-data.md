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
# <a name="securing-access-tooazure-cosmos-db-data"></a><span data-ttu-id="5c668-103">保護存取 tooAzure Cosmos DB 的資料</span><span class="sxs-lookup"><span data-stu-id="5c668-103">Securing access tooAzure Cosmos DB data</span></span>
<span data-ttu-id="5c668-104">本文提供的保護儲存在存取 toodata 概觀[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="5c668-104">This article provides an overview of securing access toodata stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="5c668-105">Azure Cosmos DB 會使用兩種類型的索引鍵 tooauthenticate 使用者，並提供存取 tooits 資料和資源。</span><span class="sxs-lookup"><span data-stu-id="5c668-105">Azure Cosmos DB uses two types of keys tooauthenticate users and provide access tooits data and resources.</span></span> 

|<span data-ttu-id="5c668-106">金鑰類型</span><span class="sxs-lookup"><span data-stu-id="5c668-106">Key type</span></span>|<span data-ttu-id="5c668-107">資源</span><span class="sxs-lookup"><span data-stu-id="5c668-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="5c668-108">主要金鑰</span><span class="sxs-lookup"><span data-stu-id="5c668-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="5c668-109">用於系統管理資源︰資料庫帳戶、資料庫、使用者和權限</span><span class="sxs-lookup"><span data-stu-id="5c668-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="5c668-110">資源權杖</span><span class="sxs-lookup"><span data-stu-id="5c668-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="5c668-111">用於應用程式資源︰集合、文件、附件、預存程序、觸發程序和 UDF</span><span class="sxs-lookup"><span data-stu-id="5c668-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="5c668-112">主要金鑰</span><span class="sxs-lookup"><span data-stu-id="5c668-112">Master keys</span></span> 

<span data-ttu-id="5c668-113">主要金鑰提供 hello 資料庫帳戶存取 toohello 所有 hello 管理資源。</span><span class="sxs-lookup"><span data-stu-id="5c668-113">Master keys provide access toohello all hello administrative resources for hello database account.</span></span> <span data-ttu-id="5c668-114">主要金鑰：</span><span class="sxs-lookup"><span data-stu-id="5c668-114">Master keys:</span></span>  
- <span data-ttu-id="5c668-115">提供存取 tooaccounts、 資料庫、 使用者和權限。</span><span class="sxs-lookup"><span data-stu-id="5c668-115">Provide access tooaccounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="5c668-116">不能使用的 tooprovide 細微的存取權 toocollections 和文件。</span><span class="sxs-lookup"><span data-stu-id="5c668-116">Cannot be used tooprovide granular access toocollections and documents.</span></span>
- <span data-ttu-id="5c668-117">在 hello 建立帳戶期間建立。</span><span class="sxs-lookup"><span data-stu-id="5c668-117">Are created during hello creation of an account.</span></span>
- <span data-ttu-id="5c668-118">可隨時重新產生。</span><span class="sxs-lookup"><span data-stu-id="5c668-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="5c668-119">每個帳戶包含兩個主要金鑰︰主要金鑰和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="5c668-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="5c668-120">hello 雙重機碼的目的是，讓您可以重新產生，或復原金鑰，提供持續存取 tooyour 帳戶和資料。</span><span class="sxs-lookup"><span data-stu-id="5c668-120">hello purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access tooyour account and data.</span></span> 

<span data-ttu-id="5c668-121">在加法 toohello 兩個主要金鑰的 hello Cosmos DB 帳戶，有兩個唯讀的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5c668-121">In addition toohello two master keys for hello Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="5c668-122">這些的唯讀機碼，僅允許 hello 帳戶上的讀取的作業。</span><span class="sxs-lookup"><span data-stu-id="5c668-122">These read-only keys only allow read operations on hello account.</span></span> <span data-ttu-id="5c668-123">唯讀金鑰並不提供存取 tooread 權限資源。</span><span class="sxs-lookup"><span data-stu-id="5c668-123">Read-only keys do not provide access tooread permissions resources.</span></span>

<span data-ttu-id="5c668-124">主要、 次要唯讀狀態，而且可以擷取讀寫主要金鑰，並且使用 hello Azure 入口網站重新產生。</span><span class="sxs-lookup"><span data-stu-id="5c668-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using hello Azure portal.</span></span> <span data-ttu-id="5c668-125">相關指示請參閱[檢視、複製和重新產生存取金鑰](manage-account.md#keys)。</span><span class="sxs-lookup"><span data-stu-id="5c668-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![在 hello Azure 入口網站-示範 NoSQL 資料庫安全性的存取控制 (IAM)](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="5c668-127">hello 的旋轉您的主要金鑰的程序很簡單。</span><span class="sxs-lookup"><span data-stu-id="5c668-127">hello process of rotating your master key is simple.</span></span> <span data-ttu-id="5c668-128">瀏覽 toohello Azure 入口網站 tooretrieve 次要的索引鍵，然後以您在應用程式中的次要金鑰取代主索引鍵然後旋轉 hello hello Azure 入口網站中的主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5c668-128">Navigate toohello Azure portal tooretrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate hello primary key in hello Azure portal.</span></span>

![在 hello Azure 入口網站-示範 NoSQL 資料庫安全性的主要金鑰輪替](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a><span data-ttu-id="5c668-130">程式碼範例 toouse 主要金鑰</span><span class="sxs-lookup"><span data-stu-id="5c668-130">Code sample toouse a master key</span></span>

<span data-ttu-id="5c668-131">hello 下列程式碼範例說明如何 toouse Cosmos DB 帳戶端點和服務主要金鑰 tooinstantiate DocumentClient 及建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="5c668-131">hello following code sample illustrates how toouse a Cosmos DB account endpoint and master key tooinstantiate a DocumentClient and create a database.</span></span> 

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

## <a name="resource-tokens"></a><span data-ttu-id="5c668-132">資源權杖</span><span class="sxs-lookup"><span data-stu-id="5c668-132">Resource tokens</span></span>

<span data-ttu-id="5c668-133">資源語彙基元提供 toohello 資料庫內的應用程式資源的存取。</span><span class="sxs-lookup"><span data-stu-id="5c668-133">Resource tokens provide access toohello application resources within a database.</span></span> <span data-ttu-id="5c668-134">資源權杖：</span><span class="sxs-lookup"><span data-stu-id="5c668-134">Resource tokens:</span></span>
- <span data-ttu-id="5c668-135">提供存取 toospecific 集合、 資料分割索引鍵、 文件、 附件、 預存程序、 觸發程序和 Udf。</span><span class="sxs-lookup"><span data-stu-id="5c668-135">Provide access toospecific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="5c668-136">時，會建立[使用者](#users)授與[權限](#permissions)tooa 特定資源。</span><span class="sxs-lookup"><span data-stu-id="5c668-136">Are created when a [user](#users) is granted [permissions](#permissions) tooa specific resource.</span></span>
- <span data-ttu-id="5c668-137">使用 POST、GET 或 PUT 呼叫處理權限資源時重新建立。</span><span class="sxs-lookup"><span data-stu-id="5c668-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="5c668-138">使用雜湊資源的語彙基元，特別是建構 hello 使用者、 資源和權限。</span><span class="sxs-lookup"><span data-stu-id="5c668-138">Use a hash resource token specifically constructed for hello user, resource, and permission.</span></span>
- <span data-ttu-id="5c668-139">是與可自訂的有效期間繫結的時間。</span><span class="sxs-lookup"><span data-stu-id="5c668-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="5c668-140">hello 有效時間範圍為 1 小時。</span><span class="sxs-lookup"><span data-stu-id="5c668-140">hello default valid timespan is one hour.</span></span> <span data-ttu-id="5c668-141">權杖存留期，不過，可明確指定，向上 tooa 最多五個小時。</span><span class="sxs-lookup"><span data-stu-id="5c668-141">Token lifetime, however, may be explicitly specified, up tooa maximum of five hours.</span></span>
- <span data-ttu-id="5c668-142">提供安全的替代 toogiving 出 hello 主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="5c668-142">Provide a safe alternative toogiving out hello master key.</span></span> 
- <span data-ttu-id="5c668-143">啟用用戶端 tooread、 寫入和刪除資源，根據 toohello 他們已被授與的權限的 hello Cosmos DB 帳戶中。</span><span class="sxs-lookup"><span data-stu-id="5c668-143">Enable clients tooread, write, and delete resources in hello Cosmos DB account according toohello permissions they've been granted.</span></span>

<span data-ttu-id="5c668-144">您可以使用為資源語彙基元 （藉由建立 Cosmos DB 使用者和權限） 當您想在 Cosmos DB tooprovide 存取 tooresources 帳戶 tooa 用戶端無法信任 hello 主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="5c668-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want tooprovide access tooresources in your Cosmos DB account tooa client that cannot be trusted with hello master key.</span></span>  

<span data-ttu-id="5c668-145">Cosmos DB 資源語彙基元提供安全的替代方案，可讓用戶端 tooread、 寫入和刪除資源，根據 toohello 權限已授與，Cosmos DB 帳戶中，而需要在主版，或讀取唯一索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5c668-145">Cosmos DB resource tokens provide a safe alternative that enables clients tooread, write, and delete resources in your Cosmos DB account according toohello permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="5c668-146">以下是典型的設計模式，藉此資源語彙基元可能要求、 產生，並傳遞 tooclients:</span><span class="sxs-lookup"><span data-stu-id="5c668-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered tooclients:</span></span>

1. <span data-ttu-id="5c668-147">中間層服務設定 tooserve 行動應用程式 tooshare 使用者相片。</span><span class="sxs-lookup"><span data-stu-id="5c668-147">A mid-tier service is set up tooserve a mobile application tooshare user photos.</span></span> 
2. <span data-ttu-id="5c668-148">hello 中間層服務擁有 hello hello Cosmos 資料庫帳戶主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="5c668-148">hello mid-tier service possesses hello master key of hello Cosmos DB account.</span></span>
3. <span data-ttu-id="5c668-149">hello 相片應用程式會安裝在使用者的行動裝置上。</span><span class="sxs-lookup"><span data-stu-id="5c668-149">hello photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="5c668-150">在登入時，hello 相片應用程式會建立 hello 與 hello 中間層服務的 hello 使用者識別。</span><span class="sxs-lookup"><span data-stu-id="5c668-150">On login, hello photo app establishes hello identity of hello user with hello mid-tier service.</span></span> <span data-ttu-id="5c668-151">這項機制的身分識別建立已完全啟動 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c668-151">This mechanism of identity establishment is purely up toohello application.</span></span>
5. <span data-ttu-id="5c668-152">一旦建立 hello 身分識別，hello 中間層服務要求 hello 識別為基礎的權限。</span><span class="sxs-lookup"><span data-stu-id="5c668-152">Once hello identity is established, hello mid-tier service requests permissions based on hello identity.</span></span>
6. <span data-ttu-id="5c668-153">hello 中間層服務會傳送為資源語彙基元後 toohello phone 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c668-153">hello mid-tier service sends a resource token back toohello phone app.</span></span>
7. <span data-ttu-id="5c668-154">hello 電話應用程式可以繼續 toouse hello 資源語彙基元 toodirectly Cosmos DB 存取的資源定義 hello 資源語彙基元和 hello 間隔 hello 資源語彙基元所允許的 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="5c668-154">hello phone app can continue toouse hello resource token toodirectly access Cosmos DB resources with hello permissions defined by hello resource token and for hello interval allowed by hello resource token.</span></span> 
8. <span data-ttu-id="5c668-155">Hello 資源權杖過期時，後續要求就會收到 401 未授權例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5c668-155">When hello resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="5c668-156">此時，hello 電話應用程式會重新建立 hello 身分識別，並要求新的資源權杖。</span><span class="sxs-lookup"><span data-stu-id="5c668-156">At this point, hello phone app re-establishes hello identity and requests a new resource token.</span></span>

    ![Azure Cosmos DB 資源權杖工作流程](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="5c668-158">資源權杖的產生和管理是由原生 Cosmos DB 用戶端程式庫 hello; 處理不過，如果您使用 REST，您必須建構 hello 要求/驗證標頭。</span><span class="sxs-lookup"><span data-stu-id="5c668-158">Resource token generation and management is handled by hello native Cosmos DB client libraries; however, if you use REST you must construct hello request/authentication headers.</span></span> <span data-ttu-id="5c668-159">如需有關如何建立 REST 驗證標頭的詳細資訊，請參閱[Cosmos DB 資源的存取控制](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources)或 hello[原始程式碼我們 sdk](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js)。</span><span class="sxs-lookup"><span data-stu-id="5c668-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or hello [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="5c668-160">中介層服務的範例使用 toogenerate 或 broker 資源語彙基元，請參閱 hello [ResourceTokenBroker 應用程式](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers)。</span><span class="sxs-lookup"><span data-stu-id="5c668-160">For an example of a middle tier service used toogenerate or broker resource tokens, see hello [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="5c668-161">使用者</span><span class="sxs-lookup"><span data-stu-id="5c668-161">Users</span></span>
<span data-ttu-id="5c668-162">Cosmos DB 使用者會與 Cosmos DB 資料庫相關聯。</span><span class="sxs-lookup"><span data-stu-id="5c668-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="5c668-163">每個資料庫都包含零個或多個 Cosmos DB 使用者。</span><span class="sxs-lookup"><span data-stu-id="5c668-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="5c668-164">hello 下列程式碼範例會示範如何 toocreate Cosmos DB 使用者資源。</span><span class="sxs-lookup"><span data-stu-id="5c668-164">hello following code sample shows how toocreate a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="5c668-165">每個的 Cosmos DB 使用者都可以是使用的 tooretrieve hello 清單 PermissionsLink 屬性[權限](#permissions)hello 使用者相關聯。</span><span class="sxs-lookup"><span data-stu-id="5c668-165">Each Cosmos DB user has a PermissionsLink property that can be used tooretrieve hello list of [permissions](#permissions) associated with hello user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="5c668-166">權限</span><span class="sxs-lookup"><span data-stu-id="5c668-166">Permissions</span></span>
<span data-ttu-id="5c668-167">Cosmos DB 權限資源會與 Cosmos DB 使用者相關聯。</span><span class="sxs-lookup"><span data-stu-id="5c668-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="5c668-168">每位使用者都包含零個或多個 Cosmos DB 權限。</span><span class="sxs-lookup"><span data-stu-id="5c668-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="5c668-169">權限資源會提供 hello 使用者需求時，嘗試 tooaccess 特定應用程式資源的存取 tooa 安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="5c668-169">A permission resource provides access tooa security token that hello user needs when trying tooaccess a specific application resource.</span></span>
<span data-ttu-id="5c668-170">權限資源可能提供兩種可用的存取等級：</span><span class="sxs-lookup"><span data-stu-id="5c668-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="5c668-171">All: hello 使用者 hello 資源上具有完整權限。</span><span class="sxs-lookup"><span data-stu-id="5c668-171">All: hello user has full permission on hello resource.</span></span>
* <span data-ttu-id="5c668-172">請閱讀： hello 使用者只能讀取 hello hello 資源內容，但無法寫入、 更新或刪除作業 hello 資源上的執行。</span><span class="sxs-lookup"><span data-stu-id="5c668-172">Read: hello user can only read hello contents of hello resource but cannot perform write, update, or delete operations on hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="5c668-173">在訂單 toorun Cosmos DB 預存程序 hello 使用者必須具有 hello All 權限將會執行預存程序中的 hello hello 集合上。</span><span class="sxs-lookup"><span data-stu-id="5c668-173">In order toorun Cosmos DB stored procedures hello user must have hello All permission on hello collection in which hello stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-toocreate-permission"></a><span data-ttu-id="5c668-174">程式碼範例 toocreate 權限</span><span class="sxs-lookup"><span data-stu-id="5c668-174">Code sample toocreate permission</span></span>

<span data-ttu-id="5c668-175">hello 下列程式碼範例顯示如何 toocreate 權限資源，讀取 hello hello 權限資源，資源語彙基元和 hello 權限聯 hello[使用者](#users)上面所建立。</span><span class="sxs-lookup"><span data-stu-id="5c668-175">hello following code sample shows how toocreate a permission resource, read hello resource token of hello permission resource, and associate hello permissions with hello [user](#users) created above.</span></span>

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

<span data-ttu-id="5c668-176">如果您已經指定您的集合，然後 hello 權限集合中，文件，而附件資源的資料分割索引鍵也必須包含 hello ResourcePartitionKey 加法 toohello ResourceLink 中。</span><span class="sxs-lookup"><span data-stu-id="5c668-176">If you have specified a partition key for your collection, then hello permission for collection, document, and attachment resources must also include hello ResourcePartitionKey in addition toohello ResourceLink.</span></span>

### <a name="code-sample-tooread-permissions-for-user"></a><span data-ttu-id="5c668-177">使用者的程式碼範例 tooread 權限</span><span class="sxs-lookup"><span data-stu-id="5c668-177">Code sample tooread permissions for user</span></span>

<span data-ttu-id="5c668-178">tooeasily 取得所有與特定使用者相關聯的權限資源，但是 Cosmos DB 可用權限摘要每個使用者物件。</span><span class="sxs-lookup"><span data-stu-id="5c668-178">tooeasily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="5c668-179">hello 下列程式碼片段示範上述 tooretrieve hello 權限與 hello 使用者相關聯的建立方式、 建構權限清單，並具現化新 DocumentClient 代表 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="5c668-179">hello following code snippet shows how tooretrieve hello permission associated with hello user created above, construct a permission list, and instantiate a new DocumentClient on behalf of hello user.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5c668-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5c668-180">Next steps</span></span>
* <span data-ttu-id="5c668-181">toolearn 進一步了解 Cosmos DB 資料庫安全性，請參閱[Cosmos DB： 資料庫安全性](database-security.md)。</span><span class="sxs-lookup"><span data-stu-id="5c668-181">toolearn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="5c668-182">toolearn 有關管理主要和唯讀索引鍵，請參閱[如何 toomanage Azure Cosmos DB 帳戶](manage-account.md#keys)。</span><span class="sxs-lookup"><span data-stu-id="5c668-182">toolearn about managing master and read-only keys, see [How toomanage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="5c668-183">如何 tooconstruct Azure Cosmos DB 授權權杖，請參閱的 toolearn [Azure Cosmos DB 資源的存取控制](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources)。</span><span class="sxs-lookup"><span data-stu-id="5c668-183">toolearn how tooconstruct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
