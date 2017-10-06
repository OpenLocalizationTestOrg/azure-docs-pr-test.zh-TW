---
title: "aaaCreate DNS 區域與使用 Azure DNS 中的資料錄集 hello.NET SDK |Microsoft 文件"
description: "如何 toocreate DNS 區域與記錄設定中 Azure DNS 使用 hello.NET SDK。"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: e3bab98b13b787427219acb7ec55e53490512fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a>建立 DNS 區域和資料錄集使用 hello.NET SDK

您可以自動化作業 toocreate、 刪除或更新 DNS 區域，資料錄集，而且記錄透過 DNS SDK 與.NET DNS 管理程式庫。 [這裡](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)提供完整的 Visual Studio 專案。

## <a name="create-a-service-principal-account"></a>建立服務主體帳戶

一般而言，以程式設計方式存取 tooAzure 資源是透過專用的帳戶，而不是您自己的使用者認證授與。 這些專用帳戶稱為「服務主體」帳戶。 toouse hello Azure DNS SDK 範例專案，您首先需要 toocreate 服務主體帳戶，並將它指派 hello 正確的權限。

1. 請遵循[這些指示](../azure-resource-manager/resource-group-authenticate-service-principal.md)toocreate 服務主體帳戶 （hello Azure DNS SDK 範例專案會假設密碼為基礎的驗證）。
2. 建立資源群組 ([方法在此](../azure-resource-manager/resource-group-template-deploy-portal.md))。
3. 使用 Azure rbac 進行 toogrant hello 服務主體帳戶 DNS 區域參與者 ' 權限 toohello 資源群組 ([以下是如何](../active-directory/role-based-access-control-configure.md)。)
4. 如果使用 hello Azure DNS SDK 範例專案，請編輯 hello 'program.cs' 檔案，如下所示：

   * 插入 hello hello tenantId、 clientId （也稱為帳戶識別碼）、 秘密 （服務主體帳戶密碼） 和訂用帳戶 Id 為步驟 1 中所使用的正確值。
   * 輸入在步驟 2 中選擇 hello 資源群組名稱。
   * 輸入您選擇的 DNS 區域名稱。

## <a name="nuget-packages-and-namespace-declarations"></a>NuGet 封裝和命名空間宣告

toouse hello Azure DNS.NET SDK，您需要 tooinstall hello **Azure DNS 管理程式庫**NuGet 套件和其他需要 Azure 的封裝。

1. 在 **Visual Studio**中，開啟專案或新專案。
2. 跳過**工具**  **>**  **NuGet 套件管理員**  **>**  **Manage NuGet Packages for方案...**.
3. 按一下**瀏覽**，啟用 hello**包含發行前版本**核取方塊，然後輸入**Microsoft.Azure.Management.Dns** hello [搜尋] 方塊中。
4. 選取 hello 封裝，然後按一下 **安裝**tooadd 它 tooyour Visual Studio 專案。
5. 重複上述 tooalso 安裝 hello 下列套件 hello 程序： **Microsoft.Rest.ClientRuntime.Azure.Authentication**和**Microsoft.Azure.Management.ResourceManager**。

## <a name="add-namespace-declarations"></a>新增命名空間宣告

新增下列命名空間宣告的 hello

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a>初始化 hello DNS 管理用戶端

hello *DnsManagementClient*包含 hello 方法和屬性所需的 DNS 區域和資料錄集。  hello 下列程式碼登入 toohello 服務主體帳戶並建立 DnsManagementClient 物件。

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a>建立或更新 DNS 區域

toocreate DNS 區域中，第一次 「 區域 」 會建立一個物件 toocontain hello DNS 區域的參數。 因為 DNS 區域不是連結的 tooa 特定區域，設定 hello 位置 too'global'。 在此範例中， [Azure 資源管理員 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/)也會加入 toohello 區域。

tooactually 建立或更新 Azure DNS，hello 區域物件，其中包含 hello 區域參數中的 hello 區域傳遞 toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc*方法。

> [!NOTE]
> DnsManagementClient 支援三種作業模式： 同步 ('CreateOrUpdate')、 非同步 ('CreateOrUpdateAsync')，或非同步存取 toohello HTTP 回應 ('CreateOrUpdateWithHttpMessagesAsync')。  您可以根據應用程式的需要選擇上述任何模式。

Azure DNS 支援開放式同步存取，稱為 [Etag](dns-getstarted-create-dnszone.md)。 在此範例中，指定"*"的 hello '無-If-match' 標頭會告訴 Azure DNS toocreate DNS 區域如果不存在。  如果 hello 指定資源群組中已存在具有 hello 指定名稱的區域，hello 呼叫將會失敗。

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create hello actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if hello zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting hello http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a>建立 DNS 記錄集和記錄

DNS 記錄是以記錄集形式管理。 資料錄集是一組具有相同名稱，並記錄的 hello 記錄的區域內的類型。  hello 記錄集名稱是相對 toohello 區域名稱，不 hello 完整的 DNS 名稱。

toocreate 或更新的記錄集，「 資料錄集 」 參數物件建立，並傳遞太*DnsManagementClient.RecordSets.CreateOrUpdateAsync*。 為使用 DNS 區域中，有三種作業模式： 同步 ('CreateOrUpdate')、 非同步 ('CreateOrUpdateAsync')，或非同步存取 toohello HTTP 回應 ('CreateOrUpdateWithHttpMessagesAsync')。

和 DNS 區域的情況一樣，記錄集上的作業包含開放式並行存取支援。  在此範例中，因為 'If-match' 和 ' 如果 If-none-Match' 都未指定，也會一律建立 hello 記錄集。  此呼叫會覆寫任何現有的記錄集的 hello 相同的名稱和記錄此 DNS 區域中的型別。

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records toohello record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata toohello record set.  Similar tooAzure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create hello actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a>取得區域和記錄集

hello *DnsManagementClient.Zones.Get*和*DnsManagementClient.RecordSets.Get*方法會擷取個別的區域和資料錄集，分別。 由其類型、 名稱和 hello 區域或資源群組存在於識別資料錄集。 存在於其名稱和 hello 資源群組來識別區域。

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a>更新現有記錄集

tooupdate 現有的 DNS 記錄設定，先擷取 hello 資料錄集，然後更新 hello 記錄設定的內容，然後送出 hello 變更。  在此範例中，我們可以指定 'Etag' hello 從擷取記錄集 hello 'If-match' 參數中的 hello。 如果並行作業已經修改，同時設定在 hello hello 記錄，hello 呼叫將會失敗。

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a>列出區域和記錄集

toolist 區域使用 hello *DnsManagementClient.Zones.List...*方法，支援清單中指定的資源群組的所有區域，或是中指定 Azure 訂用帳戶 （跨越資源群組。） toolist 資料錄集的所有區域，使用*DnsManagementClient.RecordSets.List...*支援列出給定的區域中的所有資料錄集或特定類型的資料錄集的方法。

請注意，在列出區域和記錄集時，其結果可能會分頁。  下列範例會示範如何 hello tooiterate 透過 hello 頁面的結果。 （'2' 的人工小型的頁面大小就是使用的 tooforce 分頁，實際上，這個參數應該省略和 hello 使用的預設頁面大小）。

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) toodemonstrate paging
// In practice, tooimprove performance you would use a large page size or just use hello system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a>後續步驟

下載 hello [Azure DNS.NET SDK 範例專案](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)，其中包括屬於 toouse 如何 hello Azure DNS.NET SDK，包括其他 DNS 記錄類型的範例。
