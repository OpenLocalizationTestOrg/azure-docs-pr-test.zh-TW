---
title: "如何使用 Power BI Embedded 搭配 REST | Microsoft Docs"
description: "了解如何使用 Power BI Embedded 搭配 REST  "
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 31624b9d15772a4f08cf013ac713b3aa636acfca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-power-bi-embedded-with-rest"></a><span data-ttu-id="3ec18-103">如何使用 Power BI Embedded 搭配 REST</span><span class="sxs-lookup"><span data-stu-id="3ec18-103">How to use Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="3ec18-104">Power BI Embedded：了解功能與用途</span><span class="sxs-lookup"><span data-stu-id="3ec18-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="3ec18-105">在官方的 [Power BI Embedded 網站](https://azure.microsoft.com/services/power-bi-embedded/)中已說明 Power BI Embedded 的概觀，但在深入了解使用它來搭配 REST 的詳細資料之前，讓我們先快速了解一下。</span><span class="sxs-lookup"><span data-stu-id="3ec18-105">An overview of Power BI Embedded is described in the official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into the details about using it with REST.</span></span>

<span data-ttu-id="3ec18-106">這其實很簡單。</span><span class="sxs-lookup"><span data-stu-id="3ec18-106">It's quite simple, really.</span></span> <span data-ttu-id="3ec18-107">您可能想在自己的應用程式中使用 [Power BI](https://powerbi.microsoft.com) 的動態資料視覺效果。</span><span class="sxs-lookup"><span data-stu-id="3ec18-107">you may want to use the dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="3ec18-108">大部分的自訂應用程式需要為它們的客戶傳遞資料，那些客戶不一定是它們本身組織內的使用者。</span><span class="sxs-lookup"><span data-stu-id="3ec18-108">Most custom applications need to deliver the data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="3ec18-109">例如，如果您要同時為公司 A 和 公司 B 提供某些服務，公司 A 中的使用者應該只會看到他們公司 A 本身的資料。也就是需要透過多重租用來傳遞。</span><span class="sxs-lookup"><span data-stu-id="3ec18-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, the multi-tenancy is needed for the delivery.</span></span>

<span data-ttu-id="3ec18-110">自訂應用程式也可以提供自己的驗證方法，例如表單驗證、基本驗證等等。</span><span class="sxs-lookup"><span data-stu-id="3ec18-110">The custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="3ec18-111">接著，內嵌解決方案必須與現有的驗證方法安全地共同作業。</span><span class="sxs-lookup"><span data-stu-id="3ec18-111">Then, the embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="3ec18-112">同時，使用者也必須可以使用那些 ISV 應用程式，而不需要另外購買 Power BI 訂用帳戶或授權。</span><span class="sxs-lookup"><span data-stu-id="3ec18-112">It's also necessary for users to be able to use those ISV applications without the extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="3ec18-113">**Power BI Embedded** 正是針對這類案例所設計。</span><span class="sxs-lookup"><span data-stu-id="3ec18-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="3ec18-114">我們現在已經完成快速介紹，接著就讓我們深入了解一些詳細資料</span><span class="sxs-lookup"><span data-stu-id="3ec18-114">So, now that we have that quick introduction out of the way, let's get into some details</span></span>

<span data-ttu-id="3ec18-115">您可以使用 .NET \(C#) 或 Node.js SDK 來輕鬆建立含有 Power BI Embedded 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ec18-115">You can use the .NET \(C#) or Node.js SDK, to easily build your application with Power BI Embedded.</span></span> <span data-ttu-id="3ec18-116">但是，在本文中，我們將不使用 SDK 來說明關於 Power BI 的 HTTP 流程 \(incl. AuthN)。</span><span class="sxs-lookup"><span data-stu-id="3ec18-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="3ec18-117">了解這個流程，您就可以 **使用任何程式設計語言**建置應用程式，並深入了解 Power BI Embedded 的本質。</span><span class="sxs-lookup"><span data-stu-id="3ec18-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply the essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="3ec18-118">建立 Power BI 工作區集合，並取得存取金鑰 \(佈建)</span><span class="sxs-lookup"><span data-stu-id="3ec18-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="3ec18-119">Power BI Embedded 是其中一項 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="3ec18-119">Power BI Embedded is one of the Azure services.</span></span> <span data-ttu-id="3ec18-120">只有使用 Azure 入口網站的 ISV 要支付使用費 \(依據每小時的使用者工作階段計費)，檢視報表的使用者則不需要收費，甚至不需要 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ec18-120">Only the ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and the user who views the report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="3ec18-121">在開始開發我們的應用程式之前，我們必須使用 Azure 入口網站建立 **Power BI 工作區集合** 。</span><span class="sxs-lookup"><span data-stu-id="3ec18-121">Before starting our application development, we must create the **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="3ec18-122">每個 Power BI Embedded 的工作區是各客戶 (租用戶) 的工作區，我們可以在每個工作區集合中新增多個工作區。</span><span class="sxs-lookup"><span data-stu-id="3ec18-122">Each workspace of Power BI Embedded is the workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="3ec18-123">每個工作區集合會使用相同的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="3ec18-123">The same access key is used in each workspace collection.</span></span> <span data-ttu-id="3ec18-124">實際上，工作區集合是 Power BI Embedded 的安全性界限。</span><span class="sxs-lookup"><span data-stu-id="3ec18-124">In-effect, the workspace collection is the security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="3ec18-125">當我們完成建立工作區集合後，請從 Azure 入口網站複製存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="3ec18-125">When we finish creating the workspace collection, copy the access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="3ec18-126">我們也可以佈建工作區集合，然後透過 REST API 取得存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="3ec18-126">We can also provision the workspace collection and get access key via REST API.</span></span> <span data-ttu-id="3ec18-127">若要深入了解，請參閱 [Power BI Resource Provider APIs (Power BI 資源提供者 API)](https://msdn.microsoft.com/library/azure/mt712306.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3ec18-127">To learn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="3ec18-128">使用 Power BI Desktop 建立 .pbix 檔案</span><span class="sxs-lookup"><span data-stu-id="3ec18-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="3ec18-129">接下來，我們必須建立資料連接與要內嵌的報表。</span><span class="sxs-lookup"><span data-stu-id="3ec18-129">Next, we must create the data connection and reports to be embedded.</span></span>
<span data-ttu-id="3ec18-130">此工作中沒有任何程式設計或程式碼。</span><span class="sxs-lookup"><span data-stu-id="3ec18-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="3ec18-131">我們只使用 Power BI Desktop。</span><span class="sxs-lookup"><span data-stu-id="3ec18-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="3ec18-132">在本文中，我們不會探討如何使用 Power BI Desktop。</span><span class="sxs-lookup"><span data-stu-id="3ec18-132">In this article, we won't go through the details about how to use Power BI Desktop.</span></span> <span data-ttu-id="3ec18-133">如果您在此處需要一些說明，請參閱 [開始使用 Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)。</span><span class="sxs-lookup"><span data-stu-id="3ec18-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="3ec18-134">在我們的範例中，我們只使用 [零售分析範例](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/)。</span><span class="sxs-lookup"><span data-stu-id="3ec18-134">For our example, we'll just use the [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="3ec18-135">建立 Power BI 工作區</span><span class="sxs-lookup"><span data-stu-id="3ec18-135">Create a Power BI workspace</span></span>

<span data-ttu-id="3ec18-136">現在已經完成所有的佈建，我們可以透過 REST API 開始在工作區集合中建立客戶的工作區。</span><span class="sxs-lookup"><span data-stu-id="3ec18-136">Now that the provisioning is all done, let’s get started creating a customer’s workspace in the workspace collection via REST APIs.</span></span> <span data-ttu-id="3ec18-137">下列 HTTP POST 要求 (REST) 會在我們現有的工作區集合中建立新的工作區。</span><span class="sxs-lookup"><span data-stu-id="3ec18-137">The following HTTP POST Request (REST) is creating the new workspace in our existing workspace collection.</span></span> <span data-ttu-id="3ec18-138">這是 [POST 工作區 API](https://msdn.microsoft.com/library/azure/mt711503.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3ec18-138">This is the [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="3ec18-139">在本範例中，工作區集合名稱是 **mypbiapp**。</span><span class="sxs-lookup"><span data-stu-id="3ec18-139">In our example, the workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="3ec18-140">我們只要將先前複製的存取金鑰設定為 **AppKey**。</span><span class="sxs-lookup"><span data-stu-id="3ec18-140">We just set the access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="3ec18-141">這是非常簡單的驗證！</span><span class="sxs-lookup"><span data-stu-id="3ec18-141">It’s very simple authentication!</span></span>

<span data-ttu-id="3ec18-142">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="3ec18-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="3ec18-143">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="3ec18-143">**HTTP Response**</span></span>

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

<span data-ttu-id="3ec18-144">傳回的 **workspaceId** 會用於後續的 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="3ec18-144">The returned **workspaceId** is used for the following subsequent API calls.</span></span> <span data-ttu-id="3ec18-145">我們的應用程式必須保留這個值。</span><span class="sxs-lookup"><span data-stu-id="3ec18-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-the-workspace"></a><span data-ttu-id="3ec18-146">將 .pbix 檔案匯入工作區</span><span class="sxs-lookup"><span data-stu-id="3ec18-146">Import .pbix file into the workspace</span></span>

<span data-ttu-id="3ec18-147">工作區中的每個報表都會對應到單一 Power BI Desktop 檔案，其中含有資料集 \(包括資料來源設定)。</span><span class="sxs-lookup"><span data-stu-id="3ec18-147">Each report in a workspace corresponds to a single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="3ec18-148">我們可以將我們的 .pbix 檔案匯入工作區，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="3ec18-148">We can import our .pbix file to the workspace as shown in the code below.</span></span> <span data-ttu-id="3ec18-149">如您所見，我們可以使用 http 中的 MIME multipart 上傳 .pbix 檔案的二進位檔。</span><span class="sxs-lookup"><span data-stu-id="3ec18-149">As you can see, we can upload the binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="3ec18-150">Uri 片段 **32960a09-6366-4208-a8bb-9e0678cdbb9d** 是工作區識別碼，而查詢參數 **datasetDisplayName** 是要建立的資料集名稱。</span><span class="sxs-lookup"><span data-stu-id="3ec18-150">The uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is the workspaceId, and query parameter **datasetDisplayName** is the dataset name to create.</span></span> <span data-ttu-id="3ec18-151">建立的資料集會保存 .pbix 檔案中所有和資料相關的成品，例如匯入的資料、資料來源的指標等等。</span><span class="sxs-lookup"><span data-stu-id="3ec18-151">The created dataset holds all data related artifacts in .pbix file such as imported data, the pointer to the data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{the content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="3ec18-152">此匯入工作可能會執行一段時間。</span><span class="sxs-lookup"><span data-stu-id="3ec18-152">This import task might run for a while.</span></span> <span data-ttu-id="3ec18-153">完成時，我們的應用程式可以使用匯入識別碼要求工作狀態。</span><span class="sxs-lookup"><span data-stu-id="3ec18-153">When complete, our application can ask the task status using import id.</span></span> <span data-ttu-id="3ec18-154">在本範例中，匯入識別碼是 **4eec64dd-533b-47c3-a72c-6508ad854659**。</span><span class="sxs-lookup"><span data-stu-id="3ec18-154">In our example, the import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="3ec18-155">以下是使用此匯入識別碼要求狀態：</span><span class="sxs-lookup"><span data-stu-id="3ec18-155">The following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="3ec18-156">如果工作未完成，則 HTTP 回應可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="3ec18-156">If the task isn't complete, the HTTP response could be like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

<span data-ttu-id="3ec18-157">如果工作已完成，則 HTTP 回應比較可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="3ec18-157">If the task is complete, the HTTP response could be more like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="3ec18-158">資料來源連線 \(以及資料的多重租用)</span><span class="sxs-lookup"><span data-stu-id="3ec18-158">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="3ec18-159">即使幾乎 .pbix 檔案中的所有成品都會匯入到我們的工作區，但不會包含資料來源的認證。</span><span class="sxs-lookup"><span data-stu-id="3ec18-159">While almost all of the artifacts in .pbix file are imported into our workspace, the  credentials for data sources are not.</span></span> <span data-ttu-id="3ec18-160">如此一來，當使用 [DirectQuery 模式] 時，內嵌的報表會無法正確顯示。</span><span class="sxs-lookup"><span data-stu-id="3ec18-160">As a result, when using **DirectQuery mode**, the embedded report cannot be shown correctly.</span></span> <span data-ttu-id="3ec18-161">但是，當使用 [匯入模式] 時，我們可以使用現有的匯入資料檢視報表。</span><span class="sxs-lookup"><span data-stu-id="3ec18-161">But, when using **Import mode**, we can view the report using the existing imported data.</span></span> <span data-ttu-id="3ec18-162">在這種情況下，我們必須使用下列步驟，透過 REST 呼叫來設定認證。</span><span class="sxs-lookup"><span data-stu-id="3ec18-162">In such a case, we must set the credential using the following steps via REST calls.</span></span>

<span data-ttu-id="3ec18-163">首先，我們必須取得閘道器資料來源。</span><span class="sxs-lookup"><span data-stu-id="3ec18-163">First, we must get the gateway datasource.</span></span> <span data-ttu-id="3ec18-164">我們知道資料集 **id** 是先前傳回的識別碼。</span><span class="sxs-lookup"><span data-stu-id="3ec18-164">We know the dataset **id** is the previously returned id.</span></span>

<span data-ttu-id="3ec18-165">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="3ec18-165">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="3ec18-166">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="3ec18-166">**HTTP Response**</span></span>

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

<span data-ttu-id="3ec18-167">使用傳回的閘道器識別碼和資料來源識別碼 \(請參閱之前的 **gatewayId** 和所傳回結果的 **id**)，我們可以變更這個資料來源的認證，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3ec18-167">Using the returned gateway id and datasource id \(see the previous **gatewayId** and **id** in the returned result), we can change the credential of this datasource as follows:</span></span>

<span data-ttu-id="3ec18-168">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="3ec18-168">**HTTP Request**</span></span>

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

<span data-ttu-id="3ec18-169">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="3ec18-169">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="3ec18-170">在生產環境中，我們也可以使用 REST API 針對每個工作區設定不同的連接字串。</span><span class="sxs-lookup"><span data-stu-id="3ec18-170">In production, we can also set the different connection string for each workspace using REST API.</span></span> <span data-ttu-id="3ec18-171">\(也就是可以針對每個客戶分隔資料庫。)</span><span class="sxs-lookup"><span data-stu-id="3ec18-171">\(i.e, we can separate the database for each customers.)</span></span>

<span data-ttu-id="3ec18-172">接著透過 REST 來變更資料來源的連接字串。</span><span class="sxs-lookup"><span data-stu-id="3ec18-172">The following is changing the connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="3ec18-173">或者，我們可以使用 Power BI Embedded 中的「資料列層級安全性」，並且可以在單一報表中為每位使用者分隔資料。</span><span class="sxs-lookup"><span data-stu-id="3ec18-173">Or, we can use Row Level Security in Power BI Embedded and we can separate the data for each users in one report.</span></span> <span data-ttu-id="3ec18-174">如此一來，我們就可以使用同一個 .pbix \(UI 等等) 和不同的資料來源，來佈建每個客戶報表。</span><span class="sxs-lookup"><span data-stu-id="3ec18-174">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="3ec18-175">如果您使用 [匯入模式] 而不是 [DirectQuery 模式]，則無法透過 API 重新整理模型。</span><span class="sxs-lookup"><span data-stu-id="3ec18-175">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way to refresh models via API.</span></span> <span data-ttu-id="3ec18-176">而且，Power BI Embedded 尚未支援透過 Power BI 閘道器內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="3ec18-176">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="3ec18-177">不過，建議您持續留意 [Power BI 部落格](https://powerbi.microsoft.com/blog/) ，以了解最新消息和未來版本中將推出的新功能。</span><span class="sxs-lookup"><span data-stu-id="3ec18-177">However, you'll really want to keep an eye on the [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="3ec18-178">在我們的網頁中驗證和裝載 (內嵌) 報表</span><span class="sxs-lookup"><span data-stu-id="3ec18-178">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="3ec18-179">在先前的 REST API 中，我們可以使用存取金鑰 **AppKey** 本身作為授權標頭。</span><span class="sxs-lookup"><span data-stu-id="3ec18-179">In the previous REST API, we can use the access key **AppKey** itself as the authorization header.</span></span> <span data-ttu-id="3ec18-180">因為這類呼叫可以在後端伺服器端處理，因此非常安全。</span><span class="sxs-lookup"><span data-stu-id="3ec18-180">Because these calls can be handled on the backend server side, it's safe.</span></span>

<span data-ttu-id="3ec18-181">不過，當我們在網頁中內嵌報表時，會使用 JavaScript \(前端) 來處理這類安全性資訊。</span><span class="sxs-lookup"><span data-stu-id="3ec18-181">But, when we embed the report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="3ec18-182">接著必須保護授權標頭值。</span><span class="sxs-lookup"><span data-stu-id="3ec18-182">Then the authorization header value must be secured.</span></span> <span data-ttu-id="3ec18-183">如果我們的存取金鑰被惡意使用者或惡意程式碼發現，他們就可以使用這個金鑰呼叫任何作業。</span><span class="sxs-lookup"><span data-stu-id="3ec18-183">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="3ec18-184">當我們在網頁中內嵌報表時，我們必須改用已處理的權杖，而不使用存取金鑰 **AppKey**。</span><span class="sxs-lookup"><span data-stu-id="3ec18-184">When we embed the report in our web page, we must use the computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="3ec18-185">我們的應用程式必須建立 OAuth Json Web 權杖 \(JWT)，這是由宣告和已處理的數位簽章所組成。</span><span class="sxs-lookup"><span data-stu-id="3ec18-185">Our application must create the OAuth Json Web Token \(JWT) which consists of the claims and the computed digital signature.</span></span> <span data-ttu-id="3ec18-186">這個 OAuth JWT 是使用點分隔符號編碼的字串權杖，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="3ec18-186">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="3ec18-187">首先，我們必須準備輸入值，稍後會簽署這個值。</span><span class="sxs-lookup"><span data-stu-id="3ec18-187">First, we must prepare the input value, which is signed later.</span></span> <span data-ttu-id="3ec18-188">這個值是下列 json 的 base64 url 編碼 (rfc4648) 字串，以點 \(dot) 字元分隔。</span><span class="sxs-lookup"><span data-stu-id="3ec18-188">This value is the base64 url encoded (rfc4648) string of the following json, and these are delimited by the dot \(.) character.</span></span> <span data-ttu-id="3ec18-189">稍後，我們會說明如何取得報表識別碼。</span><span class="sxs-lookup"><span data-stu-id="3ec18-189">Later, we'll explain how to get the report id.</span></span>

> [!NOTE]
> <span data-ttu-id="3ec18-190">如果我們想要使用 Power BI Embedded 的資料列層級安全性 (RLS)，則我們在宣告中也必須指定 **username** 和 **roles**。</span><span class="sxs-lookup"><span data-stu-id="3ec18-190">If we want to use Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in the claims.</span></span>

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

<span data-ttu-id="3ec18-191">接下來，我們必須使用 SHA 256 演算法建立 HMAC \(簽章) 的 base64 編碼字串。</span><span class="sxs-lookup"><span data-stu-id="3ec18-191">Next, we must create the base64 encoded string of HMAC \(the signature) with SHA256 algorithm.</span></span> <span data-ttu-id="3ec18-192">這個經過簽署的輸入值是之前的字串。</span><span class="sxs-lookup"><span data-stu-id="3ec18-192">This signed input value is the previous string.</span></span>

<span data-ttu-id="3ec18-193">最後，我們必須使用句號 \(.) 字元結合輸入值和簽章字串。</span><span class="sxs-lookup"><span data-stu-id="3ec18-193">Last, we must combine the input value and signature string using period \(.) character.</span></span> <span data-ttu-id="3ec18-194">完整的字串是用於內嵌報表的應用程式權杖。</span><span class="sxs-lookup"><span data-stu-id="3ec18-194">The completed string is the app token for the report embedding.</span></span> <span data-ttu-id="3ec18-195">即使應用程式權杖被惡意使用者發現，他們也無法取得原始的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="3ec18-195">Even if the app token is discovered by a malicious user, they cannot get the original access key.</span></span> <span data-ttu-id="3ec18-196">此應用程式權杖很快就會到期。</span><span class="sxs-lookup"><span data-stu-id="3ec18-196">This app token will expire quickly.</span></span>

<span data-ttu-id="3ec18-197">以下是這些步驟的 PHP 範例：</span><span class="sxs-lookup"><span data-stu-id="3ec18-197">Here's a PHP example for these steps:</span></span>

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is the apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-the-report-into-the-web-page"></a><span data-ttu-id="3ec18-198">最後，將報表內嵌到網頁</span><span class="sxs-lookup"><span data-stu-id="3ec18-198">Finally, embed the report into the web page</span></span>

<span data-ttu-id="3ec18-199">如需內嵌我們的報表，我們必須使用下列 REST API 取得內嵌 URL 和報表 **id** 。</span><span class="sxs-lookup"><span data-stu-id="3ec18-199">For embedding our report, we must get the embed url and report **id** using the following REST API.</span></span>

<span data-ttu-id="3ec18-200">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="3ec18-200">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="3ec18-201">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="3ec18-201">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

<span data-ttu-id="3ec18-202">我們可以使用之前的應用程式權杖在 Web 應用程式中內嵌報表。</span><span class="sxs-lookup"><span data-stu-id="3ec18-202">We can embed the report in our web app using the previous app token.</span></span>
<span data-ttu-id="3ec18-203">如果我們查看下一個範例程式碼，會發現前半部與之前的範例相同。</span><span class="sxs-lookup"><span data-stu-id="3ec18-203">If we look at the next sample code, the former part is the same as the previous example.</span></span> <span data-ttu-id="3ec18-204">在後半部中，這個範例會在 iframe 中顯示 **embedUrl** \(請參閱之前的結果)，並將應用程式權杖張貼到 iframe 中。</span><span class="sxs-lookup"><span data-stu-id="3ec18-204">In the latter part, this sample shows the **embedUrl** \(see the previous result) in the iframe, and is posting the app token into the iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="3ec18-205">您必須將報表識別碼值變更為您擁有的其中一個。</span><span class="sxs-lookup"><span data-stu-id="3ec18-205">You'll need to change the report id value to one of your own.</span></span> <span data-ttu-id="3ec18-206">此外，由於我們內容管理系統中的錯誤，程式碼範例中的 iframe 標籤會照字面讀出。</span><span class="sxs-lookup"><span data-stu-id="3ec18-206">Also, due to a bug in our content management system, the iframe tag in the code sample is read literally.</span></span> <span data-ttu-id="3ec18-207">如果您將這個範例程式碼複製並貼上，請移除標籤中的大寫文字。</span><span class="sxs-lookup"><span data-stu-id="3ec18-207">Remove the capped text from the tag if you copy and paste this sample code.</span></span>

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

<span data-ttu-id="3ec18-208">我們的結果如下︰</span><span class="sxs-lookup"><span data-stu-id="3ec18-208">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="3ec18-209">此時，Power BI Embedded 僅會在 iframe 中顯示報表。</span><span class="sxs-lookup"><span data-stu-id="3ec18-209">At this time, Power BI Embedded only shows the report in the iframe.</span></span> <span data-ttu-id="3ec18-210">但是，請持續關注 [Power BI 部落格](https://powerbi.microsoft.com/blog/)。</span><span class="sxs-lookup"><span data-stu-id="3ec18-210">But, keep an eye on the [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="3ec18-211">未來的增強功能可能使用新的用戶端 API，讓我們可以傳送資訊到 iframe 以及取出資訊。</span><span class="sxs-lookup"><span data-stu-id="3ec18-211">Future improvements could use new client side APIs that will let us send information into the iframe as well as get information out.</span></span> <span data-ttu-id="3ec18-212">令人興奮吧！</span><span class="sxs-lookup"><span data-stu-id="3ec18-212">Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="3ec18-213">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3ec18-213">See also</span></span>
* [<span data-ttu-id="3ec18-214">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="3ec18-214">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="3ec18-215">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="3ec18-215">More questions?</span></span> [<span data-ttu-id="3ec18-216">試用 Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="3ec18-216">Try the Power BI Community</span></span>](http://community.powerbi.com/)

