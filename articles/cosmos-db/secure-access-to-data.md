---
title: "了解如何安全存取 Azure Cosmos DB 中的資料 | Microsoft Docs"
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
ms.openlocfilehash: 383e04f91eec2f465b381ce30f2d6d24c488b731
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="securing-access-to-azure-cosmos-db-data"></a><span data-ttu-id="6e38f-103">安全存取 Azure Cosmos DB 資料</span><span class="sxs-lookup"><span data-stu-id="6e38f-103">Securing access to Azure Cosmos DB data</span></span>
<span data-ttu-id="6e38f-104">本文提供儲存於 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)中資料的安全存取概觀。</span><span class="sxs-lookup"><span data-stu-id="6e38f-104">This article provides an overview of securing access to data stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="6e38f-105">Azure Cosmos DB 會使用兩種類型的金鑰來驗證使用者，以允許存取其資料和資源。</span><span class="sxs-lookup"><span data-stu-id="6e38f-105">Azure Cosmos DB uses two types of keys to authenticate users and provide access to its data and resources.</span></span> 

|<span data-ttu-id="6e38f-106">金鑰類型</span><span class="sxs-lookup"><span data-stu-id="6e38f-106">Key type</span></span>|<span data-ttu-id="6e38f-107">資源</span><span class="sxs-lookup"><span data-stu-id="6e38f-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="6e38f-108">主要金鑰</span><span class="sxs-lookup"><span data-stu-id="6e38f-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="6e38f-109">用於系統管理資源︰資料庫帳戶、資料庫、使用者和權限</span><span class="sxs-lookup"><span data-stu-id="6e38f-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="6e38f-110">資源權杖</span><span class="sxs-lookup"><span data-stu-id="6e38f-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="6e38f-111">用於應用程式資源︰集合、文件、附件、預存程序、觸發程序和 UDF</span><span class="sxs-lookup"><span data-stu-id="6e38f-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="6e38f-112">主要金鑰</span><span class="sxs-lookup"><span data-stu-id="6e38f-112">Master keys</span></span> 

<span data-ttu-id="6e38f-113">主要金鑰可讓資料庫帳戶存取所有系統管理資源。</span><span class="sxs-lookup"><span data-stu-id="6e38f-113">Master keys provide access to the all the administrative resources for the database account.</span></span> <span data-ttu-id="6e38f-114">主要金鑰：</span><span class="sxs-lookup"><span data-stu-id="6e38f-114">Master keys:</span></span>  
- <span data-ttu-id="6e38f-115">允許存取帳戶、資料庫、使用者和權限。</span><span class="sxs-lookup"><span data-stu-id="6e38f-115">Provide access to accounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="6e38f-116">無法用來提供集合和文件的更細微存取權。</span><span class="sxs-lookup"><span data-stu-id="6e38f-116">Cannot be used to provide granular access to collections and documents.</span></span>
- <span data-ttu-id="6e38f-117">在帳戶建立期間建立。</span><span class="sxs-lookup"><span data-stu-id="6e38f-117">Are created during the creation of an account.</span></span>
- <span data-ttu-id="6e38f-118">可隨時重新產生。</span><span class="sxs-lookup"><span data-stu-id="6e38f-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="6e38f-119">每個帳戶包含兩個主要金鑰︰主要金鑰和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e38f-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="6e38f-120">雙重金鑰的目的是讓您可以重新產生或輸替金鑰，以持續存取您的帳戶和資料。</span><span class="sxs-lookup"><span data-stu-id="6e38f-120">The purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access to your account and data.</span></span> 

<span data-ttu-id="6e38f-121">除了 Cosmos DB 帳戶的兩個主要金鑰，還有兩個唯讀金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e38f-121">In addition to the two master keys for the Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="6e38f-122">這些唯讀金鑰只允許帳戶上的讀取作業。</span><span class="sxs-lookup"><span data-stu-id="6e38f-122">These read-only keys only allow read operations on the account.</span></span> <span data-ttu-id="6e38f-123">唯讀金鑰不提供存取權來讀取權限資源。</span><span class="sxs-lookup"><span data-stu-id="6e38f-123">Read-only keys do not provide access to read permissions resources.</span></span>

<span data-ttu-id="6e38f-124">您可以使用 Azure 入口網站來擷取和重新產生主要、次要、唯讀和讀寫主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e38f-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using the Azure portal.</span></span> <span data-ttu-id="6e38f-125">相關指示請參閱[檢視、複製和重新產生存取金鑰](manage-account.md#keys)。</span><span class="sxs-lookup"><span data-stu-id="6e38f-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Azure 入口網站中的存取控制 (IAM) - 示範 NoSQL 資料庫安全性](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="6e38f-127">輸替主要金鑰的程序很簡單。</span><span class="sxs-lookup"><span data-stu-id="6e38f-127">The process of rotating your master key is simple.</span></span> <span data-ttu-id="6e38f-128">瀏覽至 Azure 入口網站來擷取次要金鑰，在您的應用程式中以次要金鑰取代主要金鑰，然後在 Azure 入口網站中輸替主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e38f-128">Navigate to the Azure portal to retrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate the primary key in the Azure portal.</span></span>

![Azure 入口網站中的主要金鑰輪替 - 示範 NoSQL 資料庫安全性](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-to-use-a-master-key"></a><span data-ttu-id="6e38f-130">使用主要金鑰的程式碼範例</span><span class="sxs-lookup"><span data-stu-id="6e38f-130">Code sample to use a master key</span></span>

<span data-ttu-id="6e38f-131">下列程式碼範例說明如何使用 Cosmos DB 帳戶端點和主要金鑰，以具現化 DocumentClient 並建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="6e38f-131">The following code sample illustrates how to use a Cosmos DB account endpoint and master key to instantiate a DocumentClient and create a database.</span></span> 

```csharp
//Read the Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from the Azure portal on the Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access to your DocDB account.

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

## <a name="resource-tokens"></a><span data-ttu-id="6e38f-132">資源權杖</span><span class="sxs-lookup"><span data-stu-id="6e38f-132">Resource tokens</span></span>

<span data-ttu-id="6e38f-133">資源權杖允許存取資料庫內的應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="6e38f-133">Resource tokens provide access to the application resources within a database.</span></span> <span data-ttu-id="6e38f-134">資源權杖：</span><span class="sxs-lookup"><span data-stu-id="6e38f-134">Resource tokens:</span></span>
- <span data-ttu-id="6e38f-135">允許存取特定的集合、分割索引鍵、文件、附件、預存程序、觸發程序和 UDF。</span><span class="sxs-lookup"><span data-stu-id="6e38f-135">Provide access to specific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="6e38f-136">在[使用者](#users)被授與特定資源的[權限](#permissions)時建立。</span><span class="sxs-lookup"><span data-stu-id="6e38f-136">Are created when a [user](#users) is granted [permissions](#permissions) to a specific resource.</span></span>
- <span data-ttu-id="6e38f-137">使用 POST、GET 或 PUT 呼叫處理權限資源時重新建立。</span><span class="sxs-lookup"><span data-stu-id="6e38f-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="6e38f-138">使用特別為使用者、資源和權限建構的雜湊資源權杖。</span><span class="sxs-lookup"><span data-stu-id="6e38f-138">Use a hash resource token specifically constructed for the user, resource, and permission.</span></span>
- <span data-ttu-id="6e38f-139">是與可自訂的有效期間繫結的時間。</span><span class="sxs-lookup"><span data-stu-id="6e38f-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="6e38f-140">預設有效時間範圍是一小時。</span><span class="sxs-lookup"><span data-stu-id="6e38f-140">The default valid timespan is one hour.</span></span> <span data-ttu-id="6e38f-141">但可以明確指定權杖存留期，最多五小時。</span><span class="sxs-lookup"><span data-stu-id="6e38f-141">Token lifetime, however, may be explicitly specified, up to a maximum of five hours.</span></span>
- <span data-ttu-id="6e38f-142">提供安全的替代方式來分發主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e38f-142">Provide a safe alternative to giving out the master key.</span></span> 
- <span data-ttu-id="6e38f-143">可讓用戶端根據所授與的權限，讀取、寫入和刪除 Cosmos DB 帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="6e38f-143">Enable clients to read, write, and delete resources in the Cosmos DB account according to the permissions they've been granted.</span></span>

<span data-ttu-id="6e38f-144">若要對無法託付主要金鑰的用戶端提供 Cosmos DB 帳戶內資源的存取權，您可以使用資源權杖 (方法是建立 Cosmos DB 使用者和權限)。</span><span class="sxs-lookup"><span data-stu-id="6e38f-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want to provide access to resources in your Cosmos DB account to a client that cannot be trusted with the master key.</span></span>  

<span data-ttu-id="6e38f-145">Cosmos DB 資源權杖提供一個安全的替代方式，無需主要或唯讀金鑰，便可讓用戶端根據授與他們的權限，以讀取、寫入和刪除 Cosmos DB 帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="6e38f-145">Cosmos DB resource tokens provide a safe alternative that enables clients to read, write, and delete resources in your Cosmos DB account according to the permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="6e38f-146">以下是典型的設計模式，其中資源權杖可能會被要求、產生和傳遞給用戶端：</span><span class="sxs-lookup"><span data-stu-id="6e38f-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered to clients:</span></span>

1. <span data-ttu-id="6e38f-147">設定中間層服務，以協助行動應用程式分享使用者相片。</span><span class="sxs-lookup"><span data-stu-id="6e38f-147">A mid-tier service is set up to serve a mobile application to share user photos.</span></span> 
2. <span data-ttu-id="6e38f-148">中間層服務擁有 Cosmos DB 帳戶的主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="6e38f-148">The mid-tier service possesses the master key of the Cosmos DB account.</span></span>
3. <span data-ttu-id="6e38f-149">使用者的行動裝置上安裝相片應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e38f-149">The photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="6e38f-150">登入時，相片應用程式會建立中間層服務的使用者身分識別。</span><span class="sxs-lookup"><span data-stu-id="6e38f-150">On login, the photo app establishes the identity of the user with the mid-tier service.</span></span> <span data-ttu-id="6e38f-151">這項身分識別建立的機制完全取決於應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e38f-151">This mechanism of identity establishment is purely up to the application.</span></span>
5. <span data-ttu-id="6e38f-152">建立身分識別後，中間層服務會根據身分識別要求權限。</span><span class="sxs-lookup"><span data-stu-id="6e38f-152">Once the identity is established, the mid-tier service requests permissions based on the identity.</span></span>
6. <span data-ttu-id="6e38f-153">中間層服務會將資源權杖送回電話應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e38f-153">The mid-tier service sends a resource token back to the phone app.</span></span>
7. <span data-ttu-id="6e38f-154">電話應用程式可以繼續使用資源權杖，利用資源權杖所定義的權限並在資源權杖所允許的間隔內，直接存取 Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="6e38f-154">The phone app can continue to use the resource token to directly access Cosmos DB resources with the permissions defined by the resource token and for the interval allowed by the resource token.</span></span> 
8. <span data-ttu-id="6e38f-155">資源權杖過期時，後續要求會收到 401 未經授權的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6e38f-155">When the resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="6e38f-156">此時，電話應用程式會重新建立身分識別，並要求新的資源權杖。</span><span class="sxs-lookup"><span data-stu-id="6e38f-156">At this point, the phone app re-establishes the identity and requests a new resource token.</span></span>

    ![Azure Cosmos DB 資源權杖工作流程](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="6e38f-158">資源權杖的產生和管理由原生 Cosmos DB 用戶端程式庫處理。不過，如果您使用 REST，您必須建構要求/驗證標頭。</span><span class="sxs-lookup"><span data-stu-id="6e38f-158">Resource token generation and management is handled by the native Cosmos DB client libraries; however, if you use REST you must construct the request/authentication headers.</span></span> <span data-ttu-id="6e38f-159">如需有關建立 REST 驗證標頭的詳細資訊，請參閱 [Cosmos DB 資源的存取控制 (英文)](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) 或 [SDK 的原始程式碼](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js)。</span><span class="sxs-lookup"><span data-stu-id="6e38f-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or the [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="6e38f-160">如需用來產生或代理資源權杖的中間層服務的範例，請參閱 [ResourceTokenBroker 應用程式](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers)。</span><span class="sxs-lookup"><span data-stu-id="6e38f-160">For an example of a middle tier service used to generate or broker resource tokens, see the [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="6e38f-161">使用者</span><span class="sxs-lookup"><span data-stu-id="6e38f-161">Users</span></span>
<span data-ttu-id="6e38f-162">Cosmos DB 使用者會與 Cosmos DB 資料庫相關聯。</span><span class="sxs-lookup"><span data-stu-id="6e38f-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="6e38f-163">每個資料庫都包含零個或多個 Cosmos DB 使用者。</span><span class="sxs-lookup"><span data-stu-id="6e38f-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="6e38f-164">下列程式碼範例示範如何建立 Cosmos DB 使用者資源。</span><span class="sxs-lookup"><span data-stu-id="6e38f-164">The following code sample shows how to create a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="6e38f-165">每個 Cosmos DB 使用者都具有 PermissionsLink 屬性，可用來擷取與使用者相關聯的[權限](#permissions)清單。</span><span class="sxs-lookup"><span data-stu-id="6e38f-165">Each Cosmos DB user has a PermissionsLink property that can be used to retrieve the list of [permissions](#permissions) associated with the user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="6e38f-166">權限</span><span class="sxs-lookup"><span data-stu-id="6e38f-166">Permissions</span></span>
<span data-ttu-id="6e38f-167">Cosmos DB 權限資源會與 Cosmos DB 使用者相關聯。</span><span class="sxs-lookup"><span data-stu-id="6e38f-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="6e38f-168">每位使用者都包含零個或多個 Cosmos DB 權限。</span><span class="sxs-lookup"><span data-stu-id="6e38f-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="6e38f-169">當使用者嘗試存取特定的應用程式資源時，權限資源會提供使用者所需的安全性權杖存取權。</span><span class="sxs-lookup"><span data-stu-id="6e38f-169">A permission resource provides access to a security token that the user needs when trying to access a specific application resource.</span></span>
<span data-ttu-id="6e38f-170">權限資源可能提供兩種可用的存取等級：</span><span class="sxs-lookup"><span data-stu-id="6e38f-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="6e38f-171">全部：使用者具有資源的完整權限。</span><span class="sxs-lookup"><span data-stu-id="6e38f-171">All: The user has full permission on the resource.</span></span>
* <span data-ttu-id="6e38f-172">讀取：使用者只能讀取資源的內容，但無法執行資源的寫入、更新或刪除作業。</span><span class="sxs-lookup"><span data-stu-id="6e38f-172">Read: The user can only read the contents of the resource but cannot perform write, update, or delete operations on the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="6e38f-173">為執行 Cosmos DB 預存程序，使用者必須具備即將執行預存程序之集合的「所有」權限。</span><span class="sxs-lookup"><span data-stu-id="6e38f-173">In order to run Cosmos DB stored procedures the user must have the All permission on the collection in which the stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-to-create-permission"></a><span data-ttu-id="6e38f-174">建立權限的程式碼範例</span><span class="sxs-lookup"><span data-stu-id="6e38f-174">Code sample to create permission</span></span>

<span data-ttu-id="6e38f-175">下列程式碼範例示範如何建立權限資源，讀取權限資源的資源權杖，並將權限與先前所建立的[使用者](#users)產生關聯。</span><span class="sxs-lookup"><span data-stu-id="6e38f-175">The following code sample shows how to create a permission resource, read the resource token of the permission resource, and associate the permissions with the [user](#users) created above.</span></span>

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

<span data-ttu-id="6e38f-176">如果您已指定集合的分割索引鍵，則集合的權限、文件和附件資源也必須包含 ResourceLink 以外的 ResourcePartitionKey。</span><span class="sxs-lookup"><span data-stu-id="6e38f-176">If you have specified a partition key for your collection, then the permission for collection, document, and attachment resources must also include the ResourcePartitionKey in addition to the ResourceLink.</span></span>

### <a name="code-sample-to-read-permissions-for-user"></a><span data-ttu-id="6e38f-177">讀取使用者權限的程式碼範例</span><span class="sxs-lookup"><span data-stu-id="6e38f-177">Code sample to read permissions for user</span></span>

<span data-ttu-id="6e38f-178">為了輕鬆取得所有與特定使用者相關聯的權限資源，Cosmos DB 會為每個使用者物件提供權限摘要。</span><span class="sxs-lookup"><span data-stu-id="6e38f-178">To easily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="6e38f-179">下列程式碼片段示範如何擷取與先前所建立的使用者相關聯的權限、建構權限清單，並代表使用者具現化新的 DocumentClient。</span><span class="sxs-lookup"><span data-stu-id="6e38f-179">The following code snippet shows how to retrieve the permission associated with the user created above, construct a permission list, and instantiate a new DocumentClient on behalf of the user.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6e38f-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6e38f-180">Next steps</span></span>
* <span data-ttu-id="6e38f-181">若要深入了解 Cosmos DB 資料庫安全性，請參閱 [Cosmos DB 資料庫安全性](database-security.md)。</span><span class="sxs-lookup"><span data-stu-id="6e38f-181">To learn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="6e38f-182">若要了解如何管理主要和唯讀金鑰，請參閱[如何管理 Azure Cosmos DB 帳戶](manage-account.md#keys)。</span><span class="sxs-lookup"><span data-stu-id="6e38f-182">To learn about managing master and read-only keys, see [How to manage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="6e38f-183">若要了解如何建構 Cosmos DB 授權權杖，請參閱 [Cosmos DB 資源的存取控制 (英文)](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources)。</span><span class="sxs-lookup"><span data-stu-id="6e38f-183">To learn how to construct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
