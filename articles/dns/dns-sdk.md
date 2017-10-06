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
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a><span data-ttu-id="8a2c1-103">建立 DNS 區域和資料錄集使用 hello.NET SDK</span><span class="sxs-lookup"><span data-stu-id="8a2c1-103">Create DNS zones and record sets using hello .NET SDK</span></span>

<span data-ttu-id="8a2c1-104">您可以自動化作業 toocreate、 刪除或更新 DNS 區域，資料錄集，而且記錄透過 DNS SDK 與.NET DNS 管理程式庫。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-104">You can automate operations toocreate, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="8a2c1-105">[這裡](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)提供完整的 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="8a2c1-106">建立服務主體帳戶</span><span class="sxs-lookup"><span data-stu-id="8a2c1-106">Create a service principal account</span></span>

<span data-ttu-id="8a2c1-107">一般而言，以程式設計方式存取 tooAzure 資源是透過專用的帳戶，而不是您自己的使用者認證授與。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-107">Typically, programmatic access tooAzure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="8a2c1-108">這些專用帳戶稱為「服務主體」帳戶。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="8a2c1-109">toouse hello Azure DNS SDK 範例專案，您首先需要 toocreate 服務主體帳戶，並將它指派 hello 正確的權限。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-109">toouse hello Azure DNS SDK sample project, you first need toocreate a service principal account and assign it hello correct permissions.</span></span>

1. <span data-ttu-id="8a2c1-110">請遵循[這些指示](../azure-resource-manager/resource-group-authenticate-service-principal.md)toocreate 服務主體帳戶 （hello Azure DNS SDK 範例專案會假設密碼為基礎的驗證）。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate a service principal account (hello Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="8a2c1-111">建立資源群組 ([方法在此](../azure-resource-manager/resource-group-template-deploy-portal.md))。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="8a2c1-112">使用 Azure rbac 進行 toogrant hello 服務主體帳戶 DNS 區域參與者 ' 權限 toohello 資源群組 ([以下是如何](../active-directory/role-based-access-control-configure.md)。)</span><span class="sxs-lookup"><span data-stu-id="8a2c1-112">Use Azure RBAC toogrant hello service principal account 'DNS Zone Contributor' permissions toohello resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="8a2c1-113">如果使用 hello Azure DNS SDK 範例專案，請編輯 hello 'program.cs' 檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a2c1-113">If using hello Azure DNS SDK sample project, edit hello 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="8a2c1-114">插入 hello hello tenantId、 clientId （也稱為帳戶識別碼）、 秘密 （服務主體帳戶密碼） 和訂用帳戶 Id 為步驟 1 中所使用的正確值。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-114">Insert hello correct values for hello tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="8a2c1-115">輸入在步驟 2 中選擇 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-115">Enter hello resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="8a2c1-116">輸入您選擇的 DNS 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="8a2c1-117">NuGet 封裝和命名空間宣告</span><span class="sxs-lookup"><span data-stu-id="8a2c1-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="8a2c1-118">toouse hello Azure DNS.NET SDK，您需要 tooinstall hello **Azure DNS 管理程式庫**NuGet 套件和其他需要 Azure 的封裝。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-118">toouse hello Azure DNS .NET SDK, you need tooinstall hello **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="8a2c1-119">在 **Visual Studio**中，開啟專案或新專案。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="8a2c1-120">跳過**工具**  **>**  **NuGet 套件管理員**  **>**  **Manage NuGet Packages for方案...**.</span><span class="sxs-lookup"><span data-stu-id="8a2c1-120">Go too**Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="8a2c1-121">按一下**瀏覽**，啟用 hello**包含發行前版本**核取方塊，然後輸入**Microsoft.Azure.Management.Dns** hello [搜尋] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-121">Click **Browse**, enable hello **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in hello search box.</span></span>
4. <span data-ttu-id="8a2c1-122">選取 hello 封裝，然後按一下 **安裝**tooadd 它 tooyour Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-122">Select hello package and click **Install** tooadd it tooyour Visual Studio project.</span></span>
5. <span data-ttu-id="8a2c1-123">重複上述 tooalso 安裝 hello 下列套件 hello 程序： **Microsoft.Rest.ClientRuntime.Azure.Authentication**和**Microsoft.Azure.Management.ResourceManager**。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-123">Repeat hello process above tooalso install hello following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="8a2c1-124">新增命名空間宣告</span><span class="sxs-lookup"><span data-stu-id="8a2c1-124">Add namespace declarations</span></span>

<span data-ttu-id="8a2c1-125">新增下列命名空間宣告的 hello</span><span class="sxs-lookup"><span data-stu-id="8a2c1-125">Add hello following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a><span data-ttu-id="8a2c1-126">初始化 hello DNS 管理用戶端</span><span class="sxs-lookup"><span data-stu-id="8a2c1-126">Initialize hello DNS management client</span></span>

<span data-ttu-id="8a2c1-127">hello *DnsManagementClient*包含 hello 方法和屬性所需的 DNS 區域和資料錄集。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-127">hello *DnsManagementClient* contains hello methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="8a2c1-128">hello 下列程式碼登入 toohello 服務主體帳戶並建立 DnsManagementClient 物件。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-128">hello following code logs in toohello service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="8a2c1-129">建立或更新 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="8a2c1-129">Create or update a DNS zone</span></span>

<span data-ttu-id="8a2c1-130">toocreate DNS 區域中，第一次 「 區域 」 會建立一個物件 toocontain hello DNS 區域的參數。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-130">toocreate a DNS zone, first a "Zone" object is created toocontain hello DNS zone parameters.</span></span> <span data-ttu-id="8a2c1-131">因為 DNS 區域不是連結的 tooa 特定區域，設定 hello 位置 too'global'。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-131">Because DNS zones are not linked tooa specific region, hello location is set too'global'.</span></span> <span data-ttu-id="8a2c1-132">在此範例中， [Azure 資源管理員 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/)也會加入 toohello 區域。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added toohello zone.</span></span>

<span data-ttu-id="8a2c1-133">tooactually 建立或更新 Azure DNS，hello 區域物件，其中包含 hello 區域參數中的 hello 區域傳遞 toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc*方法。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-133">tooactually create or update hello zone in Azure DNS, hello zone object containing hello zone parameters is passed toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="8a2c1-134">DnsManagementClient 支援三種作業模式： 同步 ('CreateOrUpdate')、 非同步 ('CreateOrUpdateAsync')，或非同步存取 toohello HTTP 回應 ('CreateOrUpdateWithHttpMessagesAsync')。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="8a2c1-135">您可以根據應用程式的需要選擇上述任何模式。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="8a2c1-136">Azure DNS 支援開放式同步存取，稱為 [Etag](dns-getstarted-create-dnszone.md)。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="8a2c1-137">在此範例中，指定"*"的 hello '無-If-match' 標頭會告訴 Azure DNS toocreate DNS 區域如果不存在。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-137">In this example, specifying "*" for hello 'If-None-Match' header tells Azure DNS toocreate a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="8a2c1-138">如果 hello 指定資源群組中已存在具有 hello 指定名稱的區域，hello 呼叫將會失敗。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-138">hello call fails if a zone with hello given name already exists in hello given resource group.</span></span>

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

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="8a2c1-139">建立 DNS 記錄集和記錄</span><span class="sxs-lookup"><span data-stu-id="8a2c1-139">Create DNS record sets and records</span></span>

<span data-ttu-id="8a2c1-140">DNS 記錄是以記錄集形式管理。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="8a2c1-141">資料錄集是一組具有相同名稱，並記錄的 hello 記錄的區域內的類型。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-141">A record set is a set of records with hello same name and record type within a zone.</span></span>  <span data-ttu-id="8a2c1-142">hello 記錄集名稱是相對 toohello 區域名稱，不 hello 完整的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-142">hello record set name is relative toohello zone name, not hello fully qualified DNS name.</span></span>

<span data-ttu-id="8a2c1-143">toocreate 或更新的記錄集，「 資料錄集 」 參數物件建立，並傳遞太*DnsManagementClient.RecordSets.CreateOrUpdateAsync*。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-143">toocreate or update a record set, a "RecordSet" parameters object is created and passed too*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="8a2c1-144">為使用 DNS 區域中，有三種作業模式： 同步 ('CreateOrUpdate')、 非同步 ('CreateOrUpdateAsync')，或非同步存取 toohello HTTP 回應 ('CreateOrUpdateWithHttpMessagesAsync')。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="8a2c1-145">和 DNS 區域的情況一樣，記錄集上的作業包含開放式並行存取支援。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="8a2c1-146">在此範例中，因為 'If-match' 和 ' 如果 If-none-Match' 都未指定，也會一律建立 hello 記錄集。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, hello record set is always created.</span></span>  <span data-ttu-id="8a2c1-147">此呼叫會覆寫任何現有的記錄集的 hello 相同的名稱和記錄此 DNS 區域中的型別。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-147">This call overwrites any existing record set with hello same name and record type in this DNS zone.</span></span>

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

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="8a2c1-148">取得區域和記錄集</span><span class="sxs-lookup"><span data-stu-id="8a2c1-148">Get zones and record sets</span></span>

<span data-ttu-id="8a2c1-149">hello *DnsManagementClient.Zones.Get*和*DnsManagementClient.RecordSets.Get*方法會擷取個別的區域和資料錄集，分別。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-149">hello *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="8a2c1-150">由其類型、 名稱和 hello 區域或資源群組存在於識別資料錄集。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-150">RecordSets are identified by their type, name, and hello zone and resource group they exist in.</span></span> <span data-ttu-id="8a2c1-151">存在於其名稱和 hello 資源群組來識別區域。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-151">Zones are identified by their name and hello resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="8a2c1-152">更新現有記錄集</span><span class="sxs-lookup"><span data-stu-id="8a2c1-152">Update an existing record set</span></span>

<span data-ttu-id="8a2c1-153">tooupdate 現有的 DNS 記錄設定，先擷取 hello 資料錄集，然後更新 hello 記錄設定的內容，然後送出 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-153">tooupdate an existing DNS record set, first retrieve hello record set, then update hello record set contents, then submit hello change.</span></span>  <span data-ttu-id="8a2c1-154">在此範例中，我們可以指定 'Etag' hello 從擷取記錄集 hello 'If-match' 參數中的 hello。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-154">In this example, we specify hello 'Etag' from hello retrieved record set in hello 'If-Match' parameter.</span></span> <span data-ttu-id="8a2c1-155">如果並行作業已經修改，同時設定在 hello hello 記錄，hello 呼叫將會失敗。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-155">hello call fails if a concurrent operation has modified hello record set in hello meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="8a2c1-156">列出區域和記錄集</span><span class="sxs-lookup"><span data-stu-id="8a2c1-156">List zones and record sets</span></span>

<span data-ttu-id="8a2c1-157">toolist 區域使用 hello *DnsManagementClient.Zones.List...*方法，支援清單中指定的資源群組的所有區域，或是中指定 Azure 訂用帳戶 （跨越資源群組。） toolist 資料錄集的所有區域，使用*DnsManagementClient.RecordSets.List...*支援列出給定的區域中的所有資料錄集或特定類型的資料錄集的方法。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-157">toolist zones, use hello *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) toolist record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="8a2c1-158">請注意，在列出區域和記錄集時，其結果可能會分頁。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="8a2c1-159">下列範例會示範如何 hello tooiterate 透過 hello 頁面的結果。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-159">hello following example shows how tooiterate through hello pages of results.</span></span> <span data-ttu-id="8a2c1-160">（'2' 的人工小型的頁面大小就是使用的 tooforce 分頁，實際上，這個參數應該省略和 hello 使用的預設頁面大小）。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-160">(An artificially small page size of '2' is used tooforce paging; in practice this parameter should be omitted and hello default page size used.)</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8a2c1-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8a2c1-161">Next steps</span></span>

<span data-ttu-id="8a2c1-162">下載 hello [Azure DNS.NET SDK 範例專案](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)，其中包括屬於 toouse 如何 hello Azure DNS.NET SDK，包括其他 DNS 記錄類型的範例。</span><span class="sxs-lookup"><span data-stu-id="8a2c1-162">Download hello [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how toouse hello Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
