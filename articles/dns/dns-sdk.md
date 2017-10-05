---
title: "使用 .NET SDK 在 Azure DNS 中建立 DNS 區域和記錄集 | Microsoft Docs"
description: "如何使用 .NET SDK 在 Azure DNS 中建立 DNS 區域和記錄集。"
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
ms.openlocfilehash: c0fb0be8da1c0ca48a4d43ea027d30a0bc17fe30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-dns-zones-and-record-sets-using-the-net-sdk"></a><span data-ttu-id="12e83-103">使用 .NET SDK 建立 DNS 區域和記錄集</span><span class="sxs-lookup"><span data-stu-id="12e83-103">Create DNS zones and record sets using the .NET SDK</span></span>

<span data-ttu-id="12e83-104">您可以使用 DNS SDK 搭配 .NET DNS 管理程式庫，以自動化作業來建立、刪除或更新 DNS 區域、記錄集和記錄。</span><span class="sxs-lookup"><span data-stu-id="12e83-104">You can automate operations to create, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="12e83-105">[這裡](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)提供完整的 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="12e83-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="12e83-106">建立服務主體帳戶</span><span class="sxs-lookup"><span data-stu-id="12e83-106">Create a service principal account</span></span>

<span data-ttu-id="12e83-107">一般而言，若想要獲得以程式設計方式存取 Azure 資源的權限，就必須透過專用帳戶而非您自己的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="12e83-107">Typically, programmatic access to Azure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="12e83-108">這些專用帳戶稱為「服務主體」帳戶。</span><span class="sxs-lookup"><span data-stu-id="12e83-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="12e83-109">若要使用 Azure DNS SDK 範例專案，您首先需要建立服務主體帳戶，並為其指派正確的權限。</span><span class="sxs-lookup"><span data-stu-id="12e83-109">To use the Azure DNS SDK sample project, you first need to create a service principal account and assign it the correct permissions.</span></span>

1. <span data-ttu-id="12e83-110">遵循 [這些指示](../azure-resource-manager/resource-group-authenticate-service-principal.md) 建立服務主體帳戶 (Azure DNS SDK 範例專案會採用密碼型驗證)。</span><span class="sxs-lookup"><span data-stu-id="12e83-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) to create a service principal account (the Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="12e83-111">建立資源群組 ([方法在此](../azure-resource-manager/resource-group-template-deploy-portal.md))。</span><span class="sxs-lookup"><span data-stu-id="12e83-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="12e83-112">使用 Azure RBAC 將資源群組的「DNS 區域參與者」權限授與服務主體帳戶 ([方法在此](../active-directory/role-based-access-control-configure.md))。</span><span class="sxs-lookup"><span data-stu-id="12e83-112">Use Azure RBAC to grant the service principal account 'DNS Zone Contributor' permissions to the resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="12e83-113">如果使用 Azure DNS SDK 範例專案，請如下編輯 'program.cs' 檔案︰</span><span class="sxs-lookup"><span data-stu-id="12e83-113">If using the Azure DNS SDK sample project, edit the 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="12e83-114">針對 tenantId、clientId (也稱為帳戶識別碼)、secret (服務主體帳戶密碼) 和 subscriptionId 插入步驟 1 所使用的正確值。</span><span class="sxs-lookup"><span data-stu-id="12e83-114">Insert the correct values for the tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="12e83-115">輸入在步驟 2 中選擇的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="12e83-115">Enter the resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="12e83-116">輸入您選擇的 DNS 區域名稱。</span><span class="sxs-lookup"><span data-stu-id="12e83-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="12e83-117">NuGet 封裝和命名空間宣告</span><span class="sxs-lookup"><span data-stu-id="12e83-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="12e83-118">若要使用 Azure DNS .NET SDK，您需要安裝 **Azure DNS 管理程式庫** NuGet 封裝以及其他必要的 Azure 封裝。</span><span class="sxs-lookup"><span data-stu-id="12e83-118">To use the Azure DNS .NET SDK, you need to install the **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="12e83-119">在 **Visual Studio**中，開啟專案或新專案。</span><span class="sxs-lookup"><span data-stu-id="12e83-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="12e83-120">移至 [工具]**>**[NuGet 封裝管理員]**>**[管理解決方案的 NuGet 封裝...]。</span><span class="sxs-lookup"><span data-stu-id="12e83-120">Go to **Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="12e83-121">按一下 [瀏覽]，啟用 [包括發行前版本] 核取方塊，然後在搜尋方塊中輸入 **Microsoft.Azure.Management.Dns**。</span><span class="sxs-lookup"><span data-stu-id="12e83-121">Click **Browse**, enable the **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in the search box.</span></span>
4. <span data-ttu-id="12e83-122">選取封裝，然後按一下 [安裝]  將它加入至您的 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="12e83-122">Select the package and click **Install** to add it to your Visual Studio project.</span></span>
5. <span data-ttu-id="12e83-123">重複上述程序以便一併安裝下列封裝︰**Microsoft.Rest.ClientRuntime.Azure.Authentication** 和 **Microsoft.Azure.Management.ResourceManager**。</span><span class="sxs-lookup"><span data-stu-id="12e83-123">Repeat the process above to also install the following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="12e83-124">新增命名空間宣告</span><span class="sxs-lookup"><span data-stu-id="12e83-124">Add namespace declarations</span></span>

<span data-ttu-id="12e83-125">新增下列命名空間宣告</span><span class="sxs-lookup"><span data-stu-id="12e83-125">Add the following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-the-dns-management-client"></a><span data-ttu-id="12e83-126">初始化 DNS 管理用戶端</span><span class="sxs-lookup"><span data-stu-id="12e83-126">Initialize the DNS management client</span></span>

<span data-ttu-id="12e83-127">*DnsManagementClient* 包含管理 DNS 區域和記錄集所需的方法和屬性。</span><span class="sxs-lookup"><span data-stu-id="12e83-127">The *DnsManagementClient* contains the methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="12e83-128">下列程式碼會登入服務主體帳戶，並建立 DnsManagementClient 物件。</span><span class="sxs-lookup"><span data-stu-id="12e83-128">The following code logs in to the service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build the service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="12e83-129">建立或更新 DNS 區域</span><span class="sxs-lookup"><span data-stu-id="12e83-129">Create or update a DNS zone</span></span>

<span data-ttu-id="12e83-130">若要建立 DNS 區域，首先要建立包含 DNS 區域參數的「區域」物件。</span><span class="sxs-lookup"><span data-stu-id="12e83-130">To create a DNS zone, first a "Zone" object is created to contain the DNS zone parameters.</span></span> <span data-ttu-id="12e83-131">因為 DNS 區域未連結到特定區域，所以位置設定為 'global'。</span><span class="sxs-lookup"><span data-stu-id="12e83-131">Because DNS zones are not linked to a specific region, the location is set to 'global'.</span></span> <span data-ttu-id="12e83-132">在此範例中，還會對此區域新增 [Azure Resource Manager「標籤」](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) 。</span><span class="sxs-lookup"><span data-stu-id="12e83-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added to the zone.</span></span>

<span data-ttu-id="12e83-133">若要在 Azure DNS 中實際建立或更新區域，則會將包含區域參數的區域物件傳遞至「DnsManagementClient.Zones.CreateOrUpdateAsyc」  方法。</span><span class="sxs-lookup"><span data-stu-id="12e83-133">To actually create or update the zone in Azure DNS, the zone object containing the zone parameters is passed to the *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="12e83-134">DnsManagementClient 支援三種作業模式︰同步 ('CreateOrUpdate')、非同步 ('CreateOrUpdateAsync')，或非同步並可存取 HTTP 回應 ('CreateOrUpdateWithHttpMessagesAsync')。</span><span class="sxs-lookup"><span data-stu-id="12e83-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access to the HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="12e83-135">您可以根據應用程式的需要選擇上述任何模式。</span><span class="sxs-lookup"><span data-stu-id="12e83-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="12e83-136">Azure DNS 支援開放式同步存取，稱為 [Etag](dns-getstarted-create-dnszone.md)。</span><span class="sxs-lookup"><span data-stu-id="12e83-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="12e83-137">在此範例中，為 'If-None-Match' 標頭指定 "*" 會告訴 Azure DNS 建立 DNS 區域 (如果還沒有任何區域存在)。</span><span class="sxs-lookup"><span data-stu-id="12e83-137">In this example, specifying "*" for the 'If-None-Match' header tells Azure DNS to create a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="12e83-138">如果指定的資源群組中已存在具有指定名稱的區域，呼叫就會失敗。</span><span class="sxs-lookup"><span data-stu-id="12e83-138">The call fails if a zone with the given name already exists in the given resource group.</span></span>

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create the actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if the zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting the http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="12e83-139">建立 DNS 記錄集和記錄</span><span class="sxs-lookup"><span data-stu-id="12e83-139">Create DNS record sets and records</span></span>

<span data-ttu-id="12e83-140">DNS 記錄是以記錄集形式管理。</span><span class="sxs-lookup"><span data-stu-id="12e83-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="12e83-141">記錄集是指一個區域內有相同名稱和記錄類型的一組記錄。</span><span class="sxs-lookup"><span data-stu-id="12e83-141">A record set is a set of records with the same name and record type within a zone.</span></span>  <span data-ttu-id="12e83-142">記錄集名稱會相對於區域名稱而非完整的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="12e83-142">The record set name is relative to the zone name, not the fully qualified DNS name.</span></span>

<span data-ttu-id="12e83-143">若要建立或更新記錄集，則會建立「RecordSet」參數物件並傳遞給「DnsManagementClient.RecordSets.CreateOrUpdateAsync」 。</span><span class="sxs-lookup"><span data-stu-id="12e83-143">To create or update a record set, a "RecordSet" parameters object is created and passed to *DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="12e83-144">和 DNS 區域的情況一樣，作業模式也有三種︰同步 ('CreateOrUpdate')、非同步 ('CreateOrUpdateAsync')，或非同步並可存取 HTTP 回應 ('CreateOrUpdateWithHttpMessagesAsync')。</span><span class="sxs-lookup"><span data-stu-id="12e83-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access to the HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="12e83-145">和 DNS 區域的情況一樣，記錄集上的作業包含開放式並行存取支援。</span><span class="sxs-lookup"><span data-stu-id="12e83-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="12e83-146">在此範例中，因為 'If-Match' 和 'If-None-Match' 都未指定，所以一律會建立記錄集。</span><span class="sxs-lookup"><span data-stu-id="12e83-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, the record set is always created.</span></span>  <span data-ttu-id="12e83-147">這個呼叫會覆寫此 DNS 區域中任何具有相同名稱和記錄類型的現有記錄集。</span><span class="sxs-lookup"><span data-stu-id="12e83-147">This call overwrites any existing record set with the same name and record type in this DNS zone.</span></span>

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records to the record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata to the record set.  Similar to Azure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create the actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="12e83-148">取得區域和記錄集</span><span class="sxs-lookup"><span data-stu-id="12e83-148">Get zones and record sets</span></span>

<span data-ttu-id="12e83-149">*DnsManagementClient.Zones.Get* 和 *DnsManagementClient.RecordSets.Get* 方法分別會擷取個別的區域和記錄集。</span><span class="sxs-lookup"><span data-stu-id="12e83-149">The *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="12e83-150">RecordSets 依其類型、名稱及所在的區域和資源群組來識別。</span><span class="sxs-lookup"><span data-stu-id="12e83-150">RecordSets are identified by their type, name, and the zone and resource group they exist in.</span></span> <span data-ttu-id="12e83-151">Zones 依其名稱及所在的資源群組來識別。</span><span class="sxs-lookup"><span data-stu-id="12e83-151">Zones are identified by their name and the resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="12e83-152">更新現有記錄集</span><span class="sxs-lookup"><span data-stu-id="12e83-152">Update an existing record set</span></span>

<span data-ttu-id="12e83-153">若要更新現有 DNS 記錄集，請先擷取記錄集，接著更新記錄集內容，然後提交變更。</span><span class="sxs-lookup"><span data-stu-id="12e83-153">To update an existing DNS record set, first retrieve the record set, then update the record set contents, then submit the change.</span></span>  <span data-ttu-id="12e83-154">在此範例中，我們會從 'If-Match' 參數中所擷取的記錄集指定 'Etag'。</span><span class="sxs-lookup"><span data-stu-id="12e83-154">In this example, we specify the 'Etag' from the retrieved record set in the 'If-Match' parameter.</span></span> <span data-ttu-id="12e83-155">如果並行作業在此同時也修改了記錄集，則呼叫會失敗。</span><span class="sxs-lookup"><span data-stu-id="12e83-155">The call fails if a concurrent operation has modified the record set in the meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record to the local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update the record set in Azure DNS
// Note: ETAG check specified, update will be rejected if the record set has changed in the meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="12e83-156">列出區域和記錄集</span><span class="sxs-lookup"><span data-stu-id="12e83-156">List zones and record sets</span></span>

<span data-ttu-id="12e83-157">若要列出區域，請使用*DnsManagementClient.Zones.List...* 方法，其支援列出指定資源群組中的所有區域，或是指定 Azure 訂用帳戶中的所有區域 (跨資源群組)。若要列出記錄集，請使用 *DnsManagementClient.RecordSets.List...* 方法，其支援列出指定區域中的所有記錄集，或只列出特定類型的記錄集。</span><span class="sxs-lookup"><span data-stu-id="12e83-157">To list zones, use the *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) To list record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="12e83-158">請注意，在列出區域和記錄集時，其結果可能會分頁。</span><span class="sxs-lookup"><span data-stu-id="12e83-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="12e83-159">下列範例示範如何逐一查看結果頁面 </span><span class="sxs-lookup"><span data-stu-id="12e83-159">The following example shows how to iterate through the pages of results.</span></span> <span data-ttu-id="12e83-160">(範例中使用了 '2' 的人為小型頁面大小來強制分頁；實際上應該忽略此參數並使用預設頁面大小)。</span><span class="sxs-lookup"><span data-stu-id="12e83-160">(An artificially small page size of '2' is used to force paging; in practice this parameter should be omitted and the default page size used.)</span></span>

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) to demonstrate paging
// In practice, to improve performance you would use a large page size or just use the system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a><span data-ttu-id="12e83-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="12e83-161">Next steps</span></span>

<span data-ttu-id="12e83-162">下載 [Azure DNS .NET SDK 範例專案](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)，其包括如何使用 Azure DNS .NET SDK 的其他範例，包括其他 DNS 記錄類型的範例。</span><span class="sxs-lookup"><span data-stu-id="12e83-162">Download the [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how to use the Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
