---
title: "Power BI Embedded 與其餘 aaaHow toouse |Microsoft 文件"
description: "深入了解如何 toouse Power BI Embedded 與其餘部分 "
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
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a><span data-ttu-id="7182d-103">如何 toouse Power BI Embedded 與其餘部分</span><span class="sxs-lookup"><span data-stu-id="7182d-103">How toouse Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="7182d-104">Power BI Embedded：了解功能與用途</span><span class="sxs-lookup"><span data-stu-id="7182d-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="7182d-105">Power BI Embedded 概觀述 hello 官方[Power BI Embedded 網站](https://azure.microsoft.com/services/power-bi-embedded/)，但得到 hello 詳細說明使用 REST 之前，讓我們快速瀏覽。</span><span class="sxs-lookup"><span data-stu-id="7182d-105">An overview of Power BI Embedded is described in hello official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into hello details about using it with REST.</span></span>

<span data-ttu-id="7182d-106">這其實很簡單。</span><span class="sxs-lookup"><span data-stu-id="7182d-106">It's quite simple, really.</span></span> <span data-ttu-id="7182d-107">您可能會想 toouse hello 動態資料視覺效果的[Power BI](https://powerbi.microsoft.com)自己的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="7182d-107">you may want toouse hello dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="7182d-108">大部分的自訂應用程式需要 toodeliver hello 資料他們自己的客戶，不一定是自己的組織中的使用者。</span><span class="sxs-lookup"><span data-stu-id="7182d-108">Most custom applications need toodeliver hello data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="7182d-109">比方說，如果您提供服務給公司 A 和 B 公司，公司 A 中的使用者只能看到資料為自己的公司 a。也就是說，hello 多租用戶所需的 hello 傳遞。</span><span class="sxs-lookup"><span data-stu-id="7182d-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, hello multi-tenancy is needed for hello delivery.</span></span>

<span data-ttu-id="7182d-110">hello 自訂應用程式可能也提供它自己的驗證方法，例如表單驗證、 基本驗證等等...</span><span class="sxs-lookup"><span data-stu-id="7182d-110">hello custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="7182d-111">然後，hello 內嵌方案必須共同作業以這個現有的驗證方法安全地。</span><span class="sxs-lookup"><span data-stu-id="7182d-111">Then, hello embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="7182d-112">它也是必要的使用者 toobe 無法 toouse 的 ISV 應用程式不含 hello 額外採購或授權的 Power BI 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7182d-112">It's also necessary for users toobe able toouse those ISV applications without hello extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="7182d-113">**Power BI Embedded** 正是針對這類案例所設計。</span><span class="sxs-lookup"><span data-stu-id="7182d-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="7182d-114">因此，現在，我們已經超出 hello 方式的快速簡介，讓我們先進入部分詳細資料</span><span class="sxs-lookup"><span data-stu-id="7182d-114">So, now that we have that quick introduction out of hello way, let's get into some details</span></span>

<span data-ttu-id="7182d-115">您可以使用 hello.NET \(C#) 或 Node.js SDK，tooeasily 建置使用 Power BI Embedded 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7182d-115">You can use hello .NET \(C#) or Node.js SDK, tooeasily build your application with Power BI Embedded.</span></span> <span data-ttu-id="7182d-116">但是，在本文中，我們將不使用 SDK 來說明關於 Power BI 的 HTTP 流程 \(incl. AuthN)。</span><span class="sxs-lookup"><span data-stu-id="7182d-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="7182d-117">了解此流程，您可以建置應用程式**與程式設計語言**，而且您可以了解太深的 Power BI Embedded 的 hello 本質。</span><span class="sxs-lookup"><span data-stu-id="7182d-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply hello essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="7182d-118">建立 Power BI 工作區集合，並取得存取金鑰 \(佈建)</span><span class="sxs-lookup"><span data-stu-id="7182d-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="7182d-119">Power BI Embedded 是其中一個 hello Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="7182d-119">Power BI Embedded is one of hello Azure services.</span></span> <span data-ttu-id="7182d-120">只有 hello ISV 會使用 Azure 入口網站則需支付使用費\(每個小時使用者工作階段)，而且檢視 hello 報表不充電或甚至 hello 使用者需要 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7182d-120">Only hello ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and hello user who views hello report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="7182d-121">開始之前我們的應用程式開發，我們必須建立 hello **Power BI 工作區集合**透過 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="7182d-121">Before starting our application development, we must create hello **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="7182d-122">每個工作區的 Power BI Embedded hello 工作區中的每個客戶 （租用戶），但我們可以加入多個工作區中的每個工作區集合。</span><span class="sxs-lookup"><span data-stu-id="7182d-122">Each workspace of Power BI Embedded is hello workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="7182d-123">相同的存取金鑰會用在每個工作區集合中的 hello。</span><span class="sxs-lookup"><span data-stu-id="7182d-123">hello same access key is used in each workspace collection.</span></span> <span data-ttu-id="7182d-124">事實上，hello 工作區集合是 Power BI Embedded hello 安全性界限。</span><span class="sxs-lookup"><span data-stu-id="7182d-124">In-effect, hello workspace collection is hello security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="7182d-125">當我們完成建立 hello 工作區的集合時，請從 Azure 入口網站複製 hello 存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="7182d-125">When we finish creating hello workspace collection, copy hello access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="7182d-126">我們也可以佈建 hello 工作區集合中並取得透過 REST API 的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="7182d-126">We can also provision hello workspace collection and get access key via REST API.</span></span> <span data-ttu-id="7182d-127">詳細資訊，請參閱 toolearn [Power BI 資源提供者 Api](https://msdn.microsoft.com/library/azure/mt712306.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7182d-127">toolearn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="7182d-128">使用 Power BI Desktop 建立 .pbix 檔案</span><span class="sxs-lookup"><span data-stu-id="7182d-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="7182d-129">接下來，我們必須建立 hello 資料連接和內嵌報表 toobe。</span><span class="sxs-lookup"><span data-stu-id="7182d-129">Next, we must create hello data connection and reports toobe embedded.</span></span>
<span data-ttu-id="7182d-130">此工作中沒有任何程式設計或程式碼。</span><span class="sxs-lookup"><span data-stu-id="7182d-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="7182d-131">我們只使用 Power BI Desktop。</span><span class="sxs-lookup"><span data-stu-id="7182d-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="7182d-132">在本文中，我們將不會經歷 hello 詳細瞭解 toouse Power BI Desktop。</span><span class="sxs-lookup"><span data-stu-id="7182d-132">In this article, we won't go through hello details about how toouse Power BI Desktop.</span></span> <span data-ttu-id="7182d-133">如果您在此處需要一些說明，請參閱 [開始使用 Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)。</span><span class="sxs-lookup"><span data-stu-id="7182d-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="7182d-134">此範例中，我們將只使用 hello[零售分析範例](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/)。</span><span class="sxs-lookup"><span data-stu-id="7182d-134">For our example, we'll just use hello [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="7182d-135">建立 Power BI 工作區</span><span class="sxs-lookup"><span data-stu-id="7182d-135">Create a Power BI workspace</span></span>

<span data-ttu-id="7182d-136">既然 hello 佈建所有完成，讓我們開始吧 hello 透過 REST Api 的 工作區集合中建立客戶的工作區。</span><span class="sxs-lookup"><span data-stu-id="7182d-136">Now that hello provisioning is all done, let’s get started creating a customer’s workspace in hello workspace collection via REST APIs.</span></span> <span data-ttu-id="7182d-137">hello 下列 HTTP POST 要求 (REST) 建立 hello 新的工作區中現有工作區集合。</span><span class="sxs-lookup"><span data-stu-id="7182d-137">hello following HTTP POST Request (REST) is creating hello new workspace in our existing workspace collection.</span></span> <span data-ttu-id="7182d-138">這是 hello [POST 工作區 API](https://msdn.microsoft.com/library/azure/mt711503.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7182d-138">This is hello [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="7182d-139">在本例中，為 hello 工作區集合名稱**mypbiapp**。</span><span class="sxs-lookup"><span data-stu-id="7182d-139">In our example, hello workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="7182d-140">我們只設定 hello 存取金鑰，我們先前複製為**AppKey**。</span><span class="sxs-lookup"><span data-stu-id="7182d-140">We just set hello access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="7182d-141">這是非常簡單的驗證！</span><span class="sxs-lookup"><span data-stu-id="7182d-141">It’s very simple authentication!</span></span>

<span data-ttu-id="7182d-142">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="7182d-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="7182d-143">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="7182d-143">**HTTP Response**</span></span>

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

<span data-ttu-id="7182d-144">傳回的 hello**工作區識別碼**用於 hello 遵循後續的 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="7182d-144">hello returned **workspaceId** is used for hello following subsequent API calls.</span></span> <span data-ttu-id="7182d-145">我們的應用程式必須保留這個值。</span><span class="sxs-lookup"><span data-stu-id="7182d-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-hello-workspace"></a><span data-ttu-id="7182d-146">.Pbix 檔案匯入至 hello 工作區</span><span class="sxs-lookup"><span data-stu-id="7182d-146">Import .pbix file into hello workspace</span></span>

<span data-ttu-id="7182d-147">每個工作區中的報表對應 tooa 單一 Power BI Desktop 檔案與資料集\(包括資料來源的設定)。</span><span class="sxs-lookup"><span data-stu-id="7182d-147">Each report in a workspace corresponds tooa single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="7182d-148">我們可以匯入我們.pbix 檔案 toohello 工作區中 hello 的下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="7182d-148">We can import our .pbix file toohello workspace as shown in hello code below.</span></span> <span data-ttu-id="7182d-149">您可以看到，我們可以上傳.pbix 檔案，使用 http 以 MIME 多組件的 hello 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="7182d-149">As you can see, we can upload hello binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="7182d-150">hello uri 片段**32960a09-6366-4208-a8bb-9e0678cdbb9d** hello 工作區識別碼，和查詢參數**datasetDisplayName**是 hello 資料集名稱 toocreate。</span><span class="sxs-lookup"><span data-stu-id="7182d-150">hello uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is hello workspaceId, and query parameter **datasetDisplayName** is hello dataset name toocreate.</span></span> <span data-ttu-id="7182d-151">hello 建立資料集保存所有相關資料匯入資料，例如.pbix 檔案中的成品 hello 指標 toohello 資料來源等等...</span><span class="sxs-lookup"><span data-stu-id="7182d-151">hello created dataset holds all data related artifacts in .pbix file such as imported data, hello pointer toohello data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="7182d-152">此匯入工作可能會執行一段時間。</span><span class="sxs-lookup"><span data-stu-id="7182d-152">This import task might run for a while.</span></span> <span data-ttu-id="7182d-153">完成時，我們的應用程式可以要求使用匯入識別碼 hello 工作狀態。在此範例中，hello 匯入 id 是**4eec64dd-533b-47c3-a72c-6508ad854659**。</span><span class="sxs-lookup"><span data-stu-id="7182d-153">When complete, our application can ask hello task status using import id. In our example, hello import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="7182d-154">hello 下列要求使用此匯入識別碼的狀態：</span><span class="sxs-lookup"><span data-stu-id="7182d-154">hello following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="7182d-155">如果 hello 工作未完成，HTTP 回應 hello 可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="7182d-155">If hello task isn't complete, hello HTTP response could be like this:</span></span>

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

<span data-ttu-id="7182d-156">如果 hello 工作已完成，HTTP 回應 hello 可能類似這樣：</span><span class="sxs-lookup"><span data-stu-id="7182d-156">If hello task is complete, hello HTTP response could be more like this:</span></span>

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

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="7182d-157">資料來源連線 \(以及資料的多重租用)</span><span class="sxs-lookup"><span data-stu-id="7182d-157">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="7182d-158">幾乎所有的.pbix 檔案中的 hello 成品匯入至我們的工作區中，資料來源的 hello 認證並不是。</span><span class="sxs-lookup"><span data-stu-id="7182d-158">While almost all of hello artifacts in .pbix file are imported into our workspace, hello  credentials for data sources are not.</span></span> <span data-ttu-id="7182d-159">如此一來，當使用**DirectQuery 模式**，hello 內嵌的報表無法顯示正確。</span><span class="sxs-lookup"><span data-stu-id="7182d-159">As a result, when using **DirectQuery mode**, hello embedded report cannot be shown correctly.</span></span> <span data-ttu-id="7182d-160">但是，當使用**匯入模式**，我們可以檢視 hello 報表使用 hello 現有的匯入的資料。</span><span class="sxs-lookup"><span data-stu-id="7182d-160">But, when using **Import mode**, we can view hello report using hello existing imported data.</span></span> <span data-ttu-id="7182d-161">在這種情況下，我們必須設定使用下列步驟透過 REST 呼叫的 hello hello 認證。</span><span class="sxs-lookup"><span data-stu-id="7182d-161">In such a case, we must set hello credential using hello following steps via REST calls.</span></span>

<span data-ttu-id="7182d-162">首先，我們必須取得 hello 閘道資料來源。</span><span class="sxs-lookup"><span data-stu-id="7182d-162">First, we must get hello gateway datasource.</span></span> <span data-ttu-id="7182d-163">我們知道 hello 資料集**識別碼**hello 先前傳回識別碼。</span><span class="sxs-lookup"><span data-stu-id="7182d-163">We know hello dataset **id** is hello previously returned id.</span></span>

<span data-ttu-id="7182d-164">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="7182d-164">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="7182d-165">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="7182d-165">**HTTP Response**</span></span>

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

<span data-ttu-id="7182d-166">使用 hello 傳回閘道識別碼和資料來源識別碼\(請參閱先前的 hello **gatewayId**和**識別碼**hello 中傳回的結果)，我們可以變更這個資料來源的 hello 認證，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7182d-166">Using hello returned gateway id and datasource id \(see hello previous **gatewayId** and **id** in hello returned result), we can change hello credential of this datasource as follows:</span></span>

<span data-ttu-id="7182d-167">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="7182d-167">**HTTP Request**</span></span>

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

<span data-ttu-id="7182d-168">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="7182d-168">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="7182d-169">在生產環境中，我們也可以設定每個工作區中使用 REST API 的 hello 不同的連接字串。</span><span class="sxs-lookup"><span data-stu-id="7182d-169">In production, we can also set hello different connection string for each workspace using REST API.</span></span> <span data-ttu-id="7182d-170">\(亦即，我們可以區隔 hello 資料庫的每個客戶。）</span><span class="sxs-lookup"><span data-stu-id="7182d-170">\(i.e, we can separate hello database for each customers.)</span></span>

<span data-ttu-id="7182d-171">hello 下列變更 hello 透過 REST 的資料來源的連接字串。</span><span class="sxs-lookup"><span data-stu-id="7182d-171">hello following is changing hello connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="7182d-172">或者，我們可以使用資料列層級安全性，在 Power BI Embedded，而且可以區隔每個使用者在報表中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7182d-172">Or, we can use Row Level Security in Power BI Embedded and we can separate hello data for each users in one report.</span></span> <span data-ttu-id="7182d-173">如此一來，我們就可以使用同一個 .pbix \(UI 等等) 和不同的資料來源，來佈建每個客戶報表。</span><span class="sxs-lookup"><span data-stu-id="7182d-173">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="7182d-174">如果您使用**匯入模式**而不是**DirectQuery 模式**，不沒有應用程式開發介面透過任何方式 toorefresh 模型。</span><span class="sxs-lookup"><span data-stu-id="7182d-174">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way toorefresh models via API.</span></span> <span data-ttu-id="7182d-175">而且，Power BI Embedded 尚未支援透過 Power BI 閘道器內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="7182d-175">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="7182d-176">不過，您會真的想 tookeep 落在 hello [Power BI 部落格](https://powerbi.microsoft.com/blog/)針對最新消息未來在未來發行版本。</span><span class="sxs-lookup"><span data-stu-id="7182d-176">However, you'll really want tookeep an eye on hello [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="7182d-177">在我們的網頁中驗證和裝載 (內嵌) 報表</span><span class="sxs-lookup"><span data-stu-id="7182d-177">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="7182d-178">在 hello 先前的 REST API，我們可以使用 hello 便捷鍵**AppKey**本身做為 hello 授權標頭。</span><span class="sxs-lookup"><span data-stu-id="7182d-178">In hello previous REST API, we can use hello access key **AppKey** itself as hello authorization header.</span></span> <span data-ttu-id="7182d-179">這些呼叫可以 hello 後端伺服器端處理，因為它是安全的。</span><span class="sxs-lookup"><span data-stu-id="7182d-179">Because these calls can be handled on hello backend server side, it's safe.</span></span>

<span data-ttu-id="7182d-180">但是，當我們在我們的網頁中內嵌 hello 報表時，會使用 JavaScript 處理這類安全性資訊\(前端)。</span><span class="sxs-lookup"><span data-stu-id="7182d-180">But, when we embed hello report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="7182d-181">然後您必須保護 hello 授權標頭值。</span><span class="sxs-lookup"><span data-stu-id="7182d-181">Then hello authorization header value must be secured.</span></span> <span data-ttu-id="7182d-182">如果我們的存取金鑰被惡意使用者或惡意程式碼發現，他們就可以使用這個金鑰呼叫任何作業。</span><span class="sxs-lookup"><span data-stu-id="7182d-182">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="7182d-183">當我們在我們的網頁中內嵌 hello 報表時，我們必須使用 hello 計算語彙基元，而不是存取金鑰**AppKey**。</span><span class="sxs-lookup"><span data-stu-id="7182d-183">When we embed hello report in our web page, we must use hello computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="7182d-184">我們的應用程式必須建立 hello OAuth Json Web 權杖\(JWT) 所組成 hello 宣告與 hello 計算數位簽章。</span><span class="sxs-lookup"><span data-stu-id="7182d-184">Our application must create hello OAuth Json Web Token \(JWT) which consists of hello claims and hello computed digital signature.</span></span> <span data-ttu-id="7182d-185">這個 OAuth JWT 是使用點分隔符號編碼的字串權杖，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="7182d-185">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="7182d-186">首先，我們必須準備 hello 輸入的值，稍後再簽署。</span><span class="sxs-lookup"><span data-stu-id="7182d-186">First, we must prepare hello input value, which is signed later.</span></span> <span data-ttu-id="7182d-187">此值為 hello base64 url 編碼 (rfc4648) 字串的 hello 下列 json，且這些由 hello 點分隔\(。) 字元。</span><span class="sxs-lookup"><span data-stu-id="7182d-187">This value is hello base64 url encoded (rfc4648) string of hello following json, and these are delimited by hello dot \(.) character.</span></span> <span data-ttu-id="7182d-188">更新版本中，我們將說明如何 tooget hello 報表識別碼。</span><span class="sxs-lookup"><span data-stu-id="7182d-188">Later, we'll explain how tooget hello report id.</span></span>

> [!NOTE]
> <span data-ttu-id="7182d-189">如果我們想 toouse 資料列層級安全性 (RLS) 與 Power BI Embedded，我們也必須指定**username**和**角色**hello 宣告中。</span><span class="sxs-lookup"><span data-stu-id="7182d-189">If we want toouse Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in hello claims.</span></span>

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

<span data-ttu-id="7182d-190">接下來，我們必須建立 hello base64 編碼字串的 HMAC \(hello 簽章) 使用 SHA256 演算法。</span><span class="sxs-lookup"><span data-stu-id="7182d-190">Next, we must create hello base64 encoded string of HMAC \(hello signature) with SHA256 algorithm.</span></span> <span data-ttu-id="7182d-191">此帶正負號的輸入的值為 hello 先前的字串。</span><span class="sxs-lookup"><span data-stu-id="7182d-191">This signed input value is hello previous string.</span></span>

<span data-ttu-id="7182d-192">最後，我們就必須合併 hello 輸入的值和簽章字串的使用期限\(。) 字元。</span><span class="sxs-lookup"><span data-stu-id="7182d-192">Last, we must combine hello input value and signature string using period \(.) character.</span></span> <span data-ttu-id="7182d-193">已完成的 hello 字串是 hello hello 報表內嵌的應用程式語彙基元。</span><span class="sxs-lookup"><span data-stu-id="7182d-193">hello completed string is hello app token for hello report embedding.</span></span> <span data-ttu-id="7182d-194">即使 hello 應用程式的權杖探索到的惡意使用者，他們無法取得 hello 原始的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="7182d-194">Even if hello app token is discovered by a malicious user, they cannot get hello original access key.</span></span> <span data-ttu-id="7182d-195">此應用程式權杖很快就會到期。</span><span class="sxs-lookup"><span data-stu-id="7182d-195">This app token will expire quickly.</span></span>

<span data-ttu-id="7182d-196">以下是這些步驟的 PHP 範例：</span><span class="sxs-lookup"><span data-stu-id="7182d-196">Here's a PHP example for these steps:</span></span>

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

// 4. show result (which is hello apptoken)
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

## <a name="finally-embed-hello-report-into-hello-web-page"></a><span data-ttu-id="7182d-197">最後，hello 報表內嵌到 hello web 網頁</span><span class="sxs-lookup"><span data-stu-id="7182d-197">Finally, embed hello report into hello web page</span></span>

<span data-ttu-id="7182d-198">針對內嵌報表，我們必須取得 hello 內嵌 url 和報表**識別碼**使用下列 REST API 的 hello。</span><span class="sxs-lookup"><span data-stu-id="7182d-198">For embedding our report, we must get hello embed url and report **id** using hello following REST API.</span></span>

<span data-ttu-id="7182d-199">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="7182d-199">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="7182d-200">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="7182d-200">**HTTP Response**</span></span>

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

<span data-ttu-id="7182d-201">我們使用 hello 先前的應用程式權杖的 web 應用程式中，我們可以內嵌 hello 報表。</span><span class="sxs-lookup"><span data-stu-id="7182d-201">We can embed hello report in our web app using hello previous app token.</span></span>
<span data-ttu-id="7182d-202">如果看一下 hello 下一個範例程式碼，hello 先前部分是 hello 與 hello 前一個範例相同。</span><span class="sxs-lookup"><span data-stu-id="7182d-202">If we look at hello next sample code, hello former part is hello same as hello previous example.</span></span> <span data-ttu-id="7182d-203">在 hello 第二個部分中，這個範例會顯示 hello **embedUrl** \(請參閱上述結果中 hello) 在 hello iframe，並張貼到 hello iframe hello 應用程式權杖。</span><span class="sxs-lookup"><span data-stu-id="7182d-203">In hello latter part, this sample shows hello **embedUrl** \(see hello previous result) in hello iframe, and is posting hello app token into hello iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="7182d-204">您將需要 toochange hello 報表識別碼值 tooone 您自己。</span><span class="sxs-lookup"><span data-stu-id="7182d-204">You'll need toochange hello report id value tooone of your own.</span></span> <span data-ttu-id="7182d-205">此外，因為在我們的內容管理系統 tooa bug，hello iframe hello 程式碼範例中讀取標記時常值。</span><span class="sxs-lookup"><span data-stu-id="7182d-205">Also, due tooa bug in our content management system, hello iframe tag in hello code sample is read literally.</span></span> <span data-ttu-id="7182d-206">如果您複製並貼上此範例程式碼，則請移除 hello 標記上限的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="7182d-206">Remove hello capped text from hello tag if you copy and paste this sample code.</span></span>

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

<span data-ttu-id="7182d-207">我們的結果如下︰</span><span class="sxs-lookup"><span data-stu-id="7182d-207">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="7182d-208">在這個階段中，Power BI Embedded 只會顯示 hello 報表 hello iframe 中。</span><span class="sxs-lookup"><span data-stu-id="7182d-208">At this time, Power BI Embedded only shows hello report in hello iframe.</span></span> <span data-ttu-id="7182d-209">但是，請注意 hello [Power BI 部落格](https://powerbi.microsoft.com/blog/)。</span><span class="sxs-lookup"><span data-stu-id="7182d-209">But, keep an eye on hello [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="7182d-210">未來的改良功能無法使用新的用戶端應用程式開發介面，將會讓我們傳送資訊到 hello iframe，以及取得資訊。令人興奮吧！</span><span class="sxs-lookup"><span data-stu-id="7182d-210">Future improvements could use new client side APIs that will let us send information into hello iframe as well as get information out. Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="7182d-211">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7182d-211">See also</span></span>
* [<span data-ttu-id="7182d-212">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="7182d-212">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="7182d-213">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="7182d-213">More questions?</span></span> [<span data-ttu-id="7182d-214">再試一次 hello Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="7182d-214">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

