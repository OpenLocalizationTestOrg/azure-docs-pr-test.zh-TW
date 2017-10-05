---
title: "使用適用於 .NET 的用戶端程式庫管理 Batch 帳戶資源 - Azure | Microsoft Docs"
description: "使用 Batch Management .NET 程式庫建立、刪除和修改 Azure Batch 帳戶資源。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 16279b23-60ff-4b16-b308-5de000e4c028
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/24/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eafde9258222a2ab09ade2e366f9cc595a303dec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-batch-accounts-and-quotas-with-the-batch-management-client-library-for-net"></a><span data-ttu-id="9e9ae-103">使用適用於 .NET 的 Batch 管理用戶端程式庫來管理 Batch 帳戶和配額</span><span class="sxs-lookup"><span data-stu-id="9e9ae-103">Manage Batch accounts and quotas with the Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e9ae-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9e9ae-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="9e9ae-105">Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="9e9ae-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="9e9ae-106">您可以透過使用 [Batch Management .NET][api_mgmt_net] 程式庫來自動化 Batch 帳戶的建立、刪除、金鑰管理和配額探索，可降低 Azure Batch 應用程式中的維護負擔。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-106">You can lower maintenance overhead in your Azure Batch applications by using the [Batch Management .NET][api_mgmt_net] library to automate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="9e9ae-107">**建立和刪除 Batch 帳戶** 。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="9e9ae-108">比方說，身為獨立軟體廠商 (ISV)，您為每個獲派不同 Batch 帳戶的客戶針對計費目的提供服務，您可以將帳戶建立和刪除功能加入至客戶入口網站。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities to your customer portal.</span></span>
* <span data-ttu-id="9e9ae-109">**擷取和重新產生帳戶金鑰** 。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="9e9ae-110">這可協助您符合強制定期變換帳戶金鑰或讓帳戶金鑰過期的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="9e9ae-111">當您在各種不同的 Azure 區域中有數個 Batch 帳戶時，將此變換程序自動化可增加解決方案的效率。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="9e9ae-112">**檢查帳戶配額** 並採取反復試驗的猜測，判斷哪一個 Batch 帳戶有哪些限制。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-112">**Check account quotas** and take the trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="9e9ae-113">藉由在開始作業、建立集區或新增計算節點之前檢查您的帳戶配額，您可以主動地調整建立計算資源的位置或時機。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="9e9ae-114">您可以決定在帳戶中配置其他資源之前，哪些帳戶需要增加配額。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="9e9ae-115">藉由在同一個應用程式中使用 Batch Management .NET、[Azure Active Directory][aad_about] 和 [Azure Resource Manager][resman_overview]，**結合其他 Azure 服務的功能**可獲得完整功能的管理體驗。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and the [Azure Resource Manager][resman_overview] together in the same application.</span></span> <span data-ttu-id="9e9ae-116">透過使用這些功能和其 API，您可以提供順暢的驗證體驗、建立和刪除資源群組的能力，以及上面所述的功能，以獲得端對端管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-116">By using these features and their APIs, you can provide a frictionless authentication experience, the ability to create and delete resource groups, and the capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="9e9ae-117">雖然這篇文章著重在以程式設計方式管理 Batch 帳戶、金鑰和配額，您可以使用 [Azure 入口網站][azure_portal]執行許多活動。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-117">While this article focuses on the programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using the [Azure portal][azure_portal].</span></span> <span data-ttu-id="9e9ae-118">如需詳細資訊，請參閱[使用 Azure 入口網站建立 Azure Batch 帳戶](batch-account-create-portal.md)和 [Azure Batch 服務的配額和限制](batch-quota-limit.md)。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-118">For more information, see [Create an Azure Batch account using the Azure portal](batch-account-create-portal.md) and [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="9e9ae-119">建立和刪除 Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="9e9ae-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="9e9ae-120">如上所述，Batch Management API 的主要功能之一就是在 Azure 區域內建立和刪除 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-120">As mentioned, one of the primary features of the Batch Management API is to create and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="9e9ae-121">若要這樣做，您將使用 [BatchManagementClient.Account.CreateAsync][net_create] 和 [DeleteAsync][net_delete]，或其同步對應項目。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-121">To do so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="9e9ae-122">下列程式碼片段會建立一個帳戶、從 Batch 服務取得新建立的帳戶，然後將它刪除。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-122">The following code snippet creates an account, obtains the newly created account from the Batch service, and then deletes it.</span></span> <span data-ttu-id="9e9ae-123">在本文的此程式碼片段與其他程式碼片段中，`batchManagementClient` 是 [BatchManagementClient][net_mgmt_client] 完整初始化的執行個體。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-123">In this snippet and the others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get the new account from the Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete the account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="9e9ae-124">使用 Batch Management .NET 程式庫和其 BatchManagementClient 類別的應用程式需要**服務管理員**或**共同管理員**存取權，以使用擁有要管理的 Batch 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-124">Applications that use the Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access to the subscription that owns the Batch account to be managed.</span></span> <span data-ttu-id="9e9ae-125">如需詳細資訊，請參閱以 [Azure Active Directory](#azure-active-directory) 一節和 [AccountManagement][acct_mgmt_sample] 程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-125">For more information, see the [Azure Active Directory](#azure-active-directory) section and the [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="9e9ae-126">擷取和重新產生帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="9e9ae-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="9e9ae-127">使用 [ListKeysAsync][net_list_keys] 從您的訂用帳戶內的任何 Batch 帳戶取得主要和次要帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="9e9ae-128">您可以使用 [RegenerateKeyAsync][net_regenerate_keys] 重新產生這些金鑰。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print the primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate the primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="9e9ae-129">您可以為您的管理應用程式建立簡化的連線工作流程。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="9e9ae-130">首先，取得您想要使用 [ListKeysAsync][net_list_keys] 管理的 Batch 帳戶的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-130">First, obtain an account key for the Batch account you wish to manage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="9e9ae-131">接著，在初始化 Batch .NET 程式庫的 [BatchSharedKeyCredentials][net_sharedkeycred] 類別 (初始化時 [BatchClient][net_batch_client] 時使用) 時使用此金鑰。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-131">Then, use this key when initializing the Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="9e9ae-132">檢查 Azure 訂用帳戶和 Batch 帳戶配額</span><span class="sxs-lookup"><span data-stu-id="9e9ae-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="9e9ae-133">Azure 訂用帳戶和 Batch 之類的個別 Azure 服務均具有預設配額，限制其中特定實體的數目。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-133">Azure subscriptions and the individual Azure services like Batch all have default quotas that limit the number of certain entities within them.</span></span> <span data-ttu-id="9e9ae-134">如需 Azure 訂用帳戶的預設配額，請參閱 [Azure 訂用帳戶和服務限制、配額及條件約束](../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-134">For the default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="9e9ae-135">如需 Batch 服務的預設配額，請參閱 [Azure Batch 服務的配額和限制](batch-quota-limit.md)。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-135">For the default quotas of the Batch service, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="9e9ae-136">藉由使用 Batch Management .NET 程式庫，您可以檢查您的應用程式中的這些配額。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-136">By using the Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="9e9ae-137">這可讓您在加入帳戶或計算資源 (如集區和計算節點) 之前進行配置決策。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-137">This enables you to make allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="9e9ae-138">檢查 Azure 訂用帳戶和 Batch 帳戶配額</span><span class="sxs-lookup"><span data-stu-id="9e9ae-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="9e9ae-139">在區域中建立 Batch 帳戶之前，您可以檢查您的 Azure 訂用帳戶，以查看您是否能夠將帳戶加入該區域中。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-139">Before creating a Batch account in a region, you can check your Azure subscription to see whether you are able to add an account in that region.</span></span>

<span data-ttu-id="9e9ae-140">在以下的程式碼片段中，我們先使用 [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] 來取得訂用帳戶內所有 Batch 帳戶的集合。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-140">In the code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] to get a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="9e9ae-141">在我們取得此集合後，我們會判斷目標區域中有多少個帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-141">Once we've obtained this collection, we determine how many accounts are in the target region.</span></span> <span data-ttu-id="9e9ae-142">接著，我們使用 [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] 來取得 Batch 帳戶配額，並判斷該區域中可以建立多少個帳戶 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] to obtain the Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within the subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within the target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get the account quota for the specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in the target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in the {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="9e9ae-143">在上述程式碼片段中，`creds` 是 [TokenCloudCredentials][azure_tokencreds] 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-143">In the snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="9e9ae-144">若要查看建立此物件的範例，請參閱 GitHub 上的 [AccountManagement][acct_mgmt_sample] 程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-144">To see an example of creating this object, see the [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="9e9ae-145">檢查 Batch 帳戶的計算資源配額</span><span class="sxs-lookup"><span data-stu-id="9e9ae-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="9e9ae-146">在 Batch 方案中增加計算資源之前，您可以檢查以確定您要配置的資源不會超過帳戶的配額。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-146">Before increasing compute resources in your Batch solution, you can check to ensure the resources you want to allocate won't exceed the account's quotas.</span></span> <span data-ttu-id="9e9ae-147">在下列程式碼片段中，我們會列印名為 `mybatchaccount` 的 Batch 帳戶配額資訊。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-147">In the code snippet below, we print the quota information for the Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="9e9ae-148">在您自己的應用程式中，您可以使用這類資訊來判斷帳戶是否可以處理要建立的其他資源。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-148">In your own application, you could use such information to determine whether the account can handle the additional resources to be created.</span></span>

```csharp
// First obtain the Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print the compute resource quotas for the account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="9e9ae-149">雖然 Azure 訂用帳戶和服務有預設配額，這許多限制都可以透過在 [Azure 入口網站][azure_portal]中提出要求來提高。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in the [Azure portal][azure_portal].</span></span> <span data-ttu-id="9e9ae-150">例如，請參閱 [Azure Batch 服務的配額和限制](batch-quota-limit.md) 以取得增加您的 Batch 帳戶配額的指示。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-150">For example, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="9e9ae-151">搭配 Batch Management .NET 使用 Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e9ae-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="9e9ae-152">Batch Management .NET 程式庫是 Azure 資源提供者用戶端，並與 [Azure Resource Manager][resman_overview] 搭配使用，以程式設計方式管理帳戶資源。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-152">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage account resources programmatically.</span></span> <span data-ttu-id="9e9ae-153">驗證透過任何 Azure 資源提供者用戶端 (包括 Batch Management .NET 程式庫)，以及透過 [Azure Resource Manager][resman_overview] 所提出的要求時，都需要 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-153">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="9e9ae-154">如需搭配 Batch Management .NET 程式庫使用 Azure AD 的詳細資訊，請參閱[使用 Azure Active Directory 驗證 Batch 方案](batch-aad-auth.md)。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-154">For information about using Azure AD with the Batch Management .NET library, see [Use Azure Active Directory to authenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="9e9ae-155">GitHub 上的範例專案</span><span class="sxs-lookup"><span data-stu-id="9e9ae-155">Sample project on GitHub</span></span>

<span data-ttu-id="9e9ae-156">若要查看 Batch Management .NET 的實際運作，請查看 GitHub 上的 [AccountManagment][acct_mgmt_sample] 範例專案。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-156">To see Batch Management .NET in action, check out the [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="9e9ae-157">AccountManagment 範例應用程式會示範下列作業：</span><span class="sxs-lookup"><span data-stu-id="9e9ae-157">The AccountManagment sample application demonstrates the following operations:</span></span>

1. <span data-ttu-id="9e9ae-158">使用 [ADAL][aad_adal] 向 Azure AD 取得安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="9e9ae-159">如果使用者尚未登入，系統會提示使用者輸入其 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-159">If the user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="9e9ae-160">使用從 Azure AD 取得的安全性權杖，建立 [SubscriptionClient][resman_subclient] 以查詢 Azure 來取得與帳戶相關聯的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-160">With the security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] to query Azure for a list of subscriptions associated with the account.</span></span> <span data-ttu-id="9e9ae-161">如果清單包含多個訂用帳戶，使用者可以從清單中選取一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-161">The user can select a subscription from the list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="9e9ae-162">取得與所選訂用帳戶相關聯的認證。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-162">Get credentials associated with the selected subscription.</span></span>
4. <span data-ttu-id="9e9ae-163">使用認證來建立 [ResourceManagementClient][resman_client] 物件。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-163">Create a [ResourceManagementClient][resman_client] object by using the credentials.</span></span>
5. <span data-ttu-id="9e9ae-164">使用 [ResourceManagementClient][resman_client] 物件來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-164">Use a [ResourceManagementClient][resman_client] object to create a resource group.</span></span>
6. <span data-ttu-id="9e9ae-165">使用 [BatchManagementClient][net_mgmt_client] 物件來執行數個 Batch 帳戶作業：</span><span class="sxs-lookup"><span data-stu-id="9e9ae-165">Use a [BatchManagementClient][net_mgmt_client] object to perform several Batch account operations:</span></span>
   * <span data-ttu-id="9e9ae-166">在新的資源群組中建立 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-166">Create a Batch account in the new resource group.</span></span>
   * <span data-ttu-id="9e9ae-167">從 Batch 服務取得新建立的帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-167">Get the newly created account from the Batch service.</span></span>
   * <span data-ttu-id="9e9ae-168">列印新帳戶的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-168">Print the account keys for the new account.</span></span>
   * <span data-ttu-id="9e9ae-169">重新產生帳戶的新主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-169">Regenerate a new primary key for the account.</span></span>
   * <span data-ttu-id="9e9ae-170">列印帳戶的配額資訊。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-170">Print the quota information for the account.</span></span>
   * <span data-ttu-id="9e9ae-171">列印訂用帳戶的配額資訊。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-171">Print the quota information for the subscription.</span></span>
   * <span data-ttu-id="9e9ae-172">列印訂用帳戶內的所有帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-172">Print all accounts within the subscription.</span></span>
   * <span data-ttu-id="9e9ae-173">刪除新建立的帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-173">Delete newly created account.</span></span>
7. <span data-ttu-id="9e9ae-174">刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-174">Delete the resource group.</span></span>

<span data-ttu-id="9e9ae-175">刪除新建立的 Batch 帳戶和資源群組之前，您可以在 [Azure 入口網站][azure_portal]中檢視它們：</span><span class="sxs-lookup"><span data-stu-id="9e9ae-175">Before deleting the newly created Batch account and resource group, you can view them in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="9e9ae-176">若要成功執行範例應用程式，必須先向 Azure 入口網站中的 Azure AD 租用戶註冊範例應用程式，並將權限授與 Azure Resource Manager API。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-176">To run the sample application successfully, you must first register it with your Azure AD tenant in the Azure portal and grant permissions to the Azure Resource Manager API.</span></span> <span data-ttu-id="9e9ae-177">請依照[使用 Active Directory 驗證 Batch Management 解決方案](batch-aad-auth-management.md)中所提供的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="9e9ae-177">Follow the steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


<span data-ttu-id="9e9ae-178">[aad_about]: ../active-directory/active-directory-whatis.md "什麼是 Azure Active Directory？"</span><span class="sxs-lookup"><span data-stu-id="9e9ae-178">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="9e9ae-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD 的驗證案例"</span><span class="sxs-lookup"><span data-stu-id="9e9ae-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="9e9ae-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "整合應用程式與 Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="9e9ae-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_mgmt_net]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[azure_portal]: http://portal.azure.com
[azure_storage]: https://azure.microsoft.com/services/storage/
[azure_tokencreds]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.tokencloudcredentials.aspx
[batch_explorer_project]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_list_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.listkeysasync.aspx
[net_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.createasync.aspx
[net_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.deleteasync.aspx
[net_regenerate_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.regeneratekeyasync.aspx
[net_sharedkeycred]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.auth.batchsharedkeycredentials.aspx
[net_mgmt_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.aspx
[net_mgmt_subscriptions]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.subscriptions.aspx
[net_mgmt_listaccounts]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.iaccountoperations.listasync.aspx
[resman_api]: https://msdn.microsoft.com/library/azure/mt418626.aspx
[resman_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.resourcemanagementclient.aspx
[resman_subclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.subscriptions.subscriptionclient.aspx
[resman_overview]: ../azure-resource-manager/resource-group-overview.md

[1]: ./media/batch-management-dotnet/portal-01.png
[2]: ./media/batch-management-dotnet/portal-02.png
[3]: ./media/batch-management-dotnet/portal-03.png
