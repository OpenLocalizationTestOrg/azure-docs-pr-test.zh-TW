---
title: "具有 for.NET-Azure hello 用戶端程式庫的 aaaManage 批次帳戶資源 |Microsoft 文件"
description: "建立、 刪除和修改 Azure Batch 帳戶資源 hello Batch Management.NET 程式庫。"
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
ms.openlocfilehash: 638d8129f3841ffcfb2e10f5d531a319bcbb7701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a>管理適用於.NET 的 Batch 帳戶與配額與 hello 批次管理用戶端程式庫

> [!div class="op_single_selector"]
> * [Azure 入口網站](batch-account-create-portal.md)
> * [Batch Management .NET](batch-management-dotnet.md)
> 
> 

您可以降低維護負擔 Azure Batch 應用程式中使用 hello [Batch Management.NET] [ api_mgmt_net]文件庫 tooautomate 批次帳戶的建立、 刪除、 金鑰管理和配額的探索。

* **建立和刪除 Batch 帳戶** 。 如果您是獨立軟體廠商 (ISV)，例如您提供您在其中每個指派不同的批次帳戶進行計費的用戶端的服務，您可以加入帳戶建立和刪除功能 tooyour 客戶入口網站。
* **擷取和重新產生帳戶金鑰** 。 這可協助您符合強制定期變換帳戶金鑰或讓帳戶金鑰過期的安全性原則。 當您在各種不同的 Azure 區域中有數個 Batch 帳戶時，將此變換程序自動化可增加解決方案的效率。
* **檢查帳戶配額**並採取 hello 試用錯誤猜測超出判斷哪些批次帳戶有何限制。 藉由在開始作業、建立集區或新增計算節點之前檢查您的帳戶配額，您可以主動地調整建立計算資源的位置或時機。 您可以決定在帳戶中配置其他資源之前，哪些帳戶需要增加配額。
* **將其他 Azure 服務的功能結合**的全功能的管理體驗--使用 Batch Management.NET， [Azure Active Directory][aad_about]，和 hello [Azure資源管理員][ resman_overview]一起放在 hello 相同的應用程式。 您可以使用這些功能和其應用程式開發介面，提供格局的無耗損驗證體驗、 hello 能力 toocreate 和刪除資源群組和上述的端對端管理解決方案的 hello 功能。

> [!NOTE]
> 本文著重在批次帳戶、 金鑰和配額的 hello 以程式設計方式管理，您可以執行許多活動使用 hello [Azure 入口網站][azure_portal]。 如需詳細資訊，請參閱[建立 Azure 批次帳戶使用 Azure 入口網站 hello](batch-account-create-portal.md)和[hello Azure 批次服務的配額與限制](batch-quota-limit.md)。
> 
> 

## <a name="create-and-delete-batch-accounts"></a>建立和刪除 Batch 帳戶
如所述，其中一項 hello 的 hello 批次管理 API 的主要功能是 toocreate 並刪除 Batch 帳戶的 Azure 區域中。 因此，使用 toodo [BatchManagementClient.Account.CreateAsync] [ net_create]和[DeleteAsync][net_delete]，或與其同步對應項目。

hello 下列程式碼片段會建立一個帳戶，會取得新建立的帳戶從 hello 批次服務的 hello，然後刪除它。 在此程式碼片段和其他人 hello 在本文中`batchManagementClient`完整初始化的執行個體[BatchManagementClient][net_mgmt_client]。

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get hello new account from hello Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete hello account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> 使用 hello Batch Management.NET 程式庫和其 BatchManagementClient 類別的應用程式需要**服務系統管理員**或**coadministrator**存取 toohello 訂用帳戶擁有 hello批次帳戶 toobe 管理。 如需詳細資訊，請參閱 hello [Azure Active Directory](#azure-active-directory)區段和 hello [AccountManagement] [ acct_mgmt_sample]程式碼範例。
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a>擷取和重新產生帳戶金鑰
使用 [ListKeysAsync][net_list_keys] 從您的訂用帳戶內的任何 Batch 帳戶取得主要和次要帳戶金鑰。 您可以使用 [RegenerateKeyAsync][net_regenerate_keys] 重新產生這些金鑰。

```csharp
// Get and print hello primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate hello primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> 您可以為您的管理應用程式建立簡化的連線工作流程。 首先，以取得您想使用 toomanage hello 批次帳戶的帳戶金鑰[ListKeysAsync][net_list_keys]。 接著，使用此金鑰，初始化 hello 批次.NET 程式庫的時[BatchSharedKeyCredentials] [ net_sharedkeycred]類別初始化時所用[BatchClient] [net_batch_client].
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a>檢查 Azure 訂用帳戶和 Batch 帳戶配額
Azure 訂用帳戶和 hello 個別 Azure 服務像所有的批次有預設的特定實體中的 hello 數目限制的配額。 Hello Azure 訂用帳戶的預設配額，請參閱[Azure 訂用帳戶和服務限制、 配額和條件約束](../azure-subscription-service-limits.md)。 Hello hello 批次服務的預設配額，請參閱[hello Azure 批次服務的配額與限制](batch-quota-limit.md)。 藉由使用 hello Batch Management.NET 程式庫，您可以檢查這些配額在應用程式中。 這可讓您 toomake 配置決策之前新增帳戶或計算資源，例如集區和計算節點。

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a>檢查 Azure 訂用帳戶和 Batch 帳戶配額
建立之前的批次帳戶在區域中，您可以檢查您的 Azure 訂用帳戶 toosee 是否能 tooadd 該區域中的帳戶。

在 hello 下列程式碼片段，我們會先使用[BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget 訂用帳戶內的所有批次帳戶的集合。 一旦我們已取得此集合，我們判斷多少的帳戶位於 hello 目標區域。 然後我們使用[BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain hello 批次帳戶的配額，並判斷該區域中可建立多少帳戶 （如果有的話）。

```csharp
// Get a collection of all Batch accounts within hello subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within hello target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get hello account quota for hello specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in hello target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in hello {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

在 hello 程式碼片段上方，`creds`的執行個體[TokenCloudCredentials][azure_tokencreds]。 toosee 建立此物件的範例，請參閱 「 hello [AccountManagement] [ acct_mgmt_sample] GitHub 上的程式碼範例。

### <a name="check-a-batch-account-for-compute-resource-quotas"></a>檢查 Batch 帳戶的計算資源配額
之前增加批次方案中的計算資源，您可以檢查您想 tooallocate 將不會超過 hello 帳戶配額的 tooensure hello 資源。 在 hello 下列程式碼片段，我們會列印 hello hello 名為批次帳戶的配額資訊`mybatchaccount`。 在自己的應用程式中，您可以使用這類資訊 toodetermine 是否 hello 帳戶可以處理 hello 其他資源 toobe 建立。

```csharp
// First obtain hello Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print hello compute resource quotas for hello account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> Azure 訂用帳戶和服務的預設配額時，許多這些限制可能會引發透過發出要求，以在 hello [Azure 入口網站][azure_portal]。 例如，請參閱[hello Azure 批次服務的配額與限制](batch-quota-limit.md)如需增加您的批次帳戶配額的指示。
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a>搭配 Batch Management .NET 使用 Azure AD

hello Batch Management.NET 程式庫是 Azure 資源提供者用戶端，並會搭配[Azure Resource Manager] [ resman_overview] toomanage 帳戶資源以程式設計的方式。 Azure AD 會透過任何 Azure 資源提供者用戶端，包括 hello Batch Management.NET 程式庫，以及透過需要的 tooauthenticate 要求[Azure Resource Manager][resman_overview]。 使用 Azure AD 與 hello Batch Management.NET 程式庫的相關資訊，請參閱[使用 Azure Active Directory tooauthenticate 批次方案](batch-aad-auth.md)。 

## <a name="sample-project-on-github"></a>GitHub 上的範例專案

toosee Batch Management.NET 中的動作，請參閱 hello [AccountManagment] [ acct_mgmt_sample] GitHub 上的範例專案。 hello AccountManagment 範例應用程式將示範下列作業的 hello:

1. 使用 [ADAL][aad_adal] 向 Azure AD 取得安全性權杖。 如果 hello 使用者沒有已登入，系統會提示他們輸入其 Azure 認證。
2. 從 Azure AD 取得 hello 安全性權杖，以建立[SubscriptionClient] [ resman_subclient] tooquery Azure hello 帳戶相關聯的訂用帳戶的清單。 hello 使用者可以從 hello 清單中選取訂用帳戶，如果它包含一個以上的訂用帳戶。
3. 取得與 hello 選取訂用帳戶相關聯的認證。
4. 建立[ResourceManagementClient] [ resman_client]使用 hello 認證物件。
5. 使用[ResourceManagementClient] [ resman_client] toocreate 資源群組的物件。
6. 使用[BatchManagementClient] [ net_mgmt_client]物件 tooperform 幾個批次帳戶的作業：
   * 建立批次帳戶 hello 新資源群組中。
   * 取得新建立的帳戶從 hello 批次服務的 hello。
   * 列印 hello hello 新帳戶的帳戶金鑰。
   * 重新產生 hello 帳戶的新主索引鍵。
   * 列印 hello hello 帳戶的配額資訊。
   * 列印 hello hello 訂用帳戶的配額資訊。
   * 列印 hello 訂用帳戶內的所有帳戶。
   * 刪除新建立的帳戶。
7. 刪除 hello 資源群組。

在刪除之前 hello 新建立的批次帳戶和資源群組，您可以檢視它們 hello [Azure 入口網站][azure_portal]:

toorun hello 範例應用程式成功，您必須先向 Azure AD 租用戶的 hello Azure 入口網站並授與權限 toohello Azure 資源管理員 API。 遵循所提供的 hello 步驟[與 Active Directory 驗證批次管理解決方案](batch-aad-auth-management.md)。


[aad_about]: ../active-directory/active-directory-whatis.md "什麼是 Azure Active Directory？"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD 的驗證案例"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "整合應用程式與 Azure Active Directory"
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
