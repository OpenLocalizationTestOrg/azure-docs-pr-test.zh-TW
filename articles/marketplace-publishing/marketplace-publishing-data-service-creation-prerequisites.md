---
title: "建立要發行到 Marketplace 之資料服務的技術必要條件 | Microsoft Docs"
description: "了解建立資料服務，以在 Azure Marketplace 中部署及銷售的的需求"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: aaff609a-1cd1-4146-98f4-d04166b0fce0
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 52827723477677bc292c645e2390c435fbad3ee4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="technical-pre-requisites-for-creating-a-data-service-offer-for-the-azure-marketplace"></a><span data-ttu-id="378b7-103">建立 Azure Marketplace 之資料服務產品的技術必要條件</span><span class="sxs-lookup"><span data-stu-id="378b7-103">Technical Pre-requisites for creating a Data Service offer for the Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="378b7-104">目前我們已不再針對任何新的資料服務發行者進行上架。新的 Dataservice 將不會獲得核准以列出於清單上。</span><span class="sxs-lookup"><span data-stu-id="378b7-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="378b7-105">如果您有想要在 AppSource 上發佈的 SaaS 商務應用程式，您可以在[這裡](https://appsource.microsoft.com/partners)找到詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="378b7-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="378b7-106">如果您有想要在 Azure Marketplace 發佈的 IaaS 應用程式或開發人員服務，您可以在[這裡](https://azure.microsoft.com/marketplace/programs/certified/)找到詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="378b7-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="378b7-107">開始之前，請先徹底閱讀程序，並且了解每個步驟執行的位置及原因。</span><span class="sxs-lookup"><span data-stu-id="378b7-107">Read the process thoroughly before beginning and understand where and why each step is performed.</span></span> <span data-ttu-id="378b7-108">在供應項目建立程序之前，您應該盡可能準備您的公司資訊和其他資料、下載必要的工具，和/或建立技術元件。</span><span class="sxs-lookup"><span data-stu-id="378b7-108">As much as possible, you should prepare your company information and other data, download necessary tools, and/or create technical components before beginning the offer creation process.</span></span>

<span data-ttu-id="378b7-109">開始程序之前，您應該先準備好下列項目：</span><span class="sxs-lookup"><span data-stu-id="378b7-109">You should have the following items ready before beginning the process:</span></span>

## <a name="make-a-decision-on-what-technology-will-be-used-to-publish-your-data-service-offer"></a><span data-ttu-id="378b7-110">決定要使用何種技術發行您的資料服務產品</span><span class="sxs-lookup"><span data-stu-id="378b7-110">Make a decision on what technology will be used to publish your Data Service offer</span></span>
<span data-ttu-id="378b7-111">在 Azure Marketplace 中發行資料服務時，發行者可以從多種技術中選擇所要使用的技術。</span><span class="sxs-lookup"><span data-stu-id="378b7-111">A Publisher can decide between multiple technologies when publishing Data Service in Azure Marketplace.</span></span> <span data-ttu-id="378b7-112">主要技術支援如下所述。</span><span class="sxs-lookup"><span data-stu-id="378b7-112">The main technologies that are supported described below.</span></span> <span data-ttu-id="378b7-113">無論使用何種技術發行資料服務，使用者都會透過 Azure Marketplace 服務所公開的 **OData 摘要** 使用服務。</span><span class="sxs-lookup"><span data-stu-id="378b7-113">Regardless what technology is used to publish the Data Service, the end-user consumes the data through the **OData feed** exposed by Azure Marketplace Service.</span></span> <span data-ttu-id="378b7-114">如需 OData 服務的完整資訊，請前往 [http://www.odata.org/](http://www.odata.org/)</span><span class="sxs-lookup"><span data-stu-id="378b7-114">Full information about OData service you can find on [http://www.odata.org/](http://www.odata.org/)</span></span>

## <a name="sql-azure-database"></a><span data-ttu-id="378b7-115">SQL Azure Database</span><span class="sxs-lookup"><span data-stu-id="378b7-115">SQL Azure Database</span></span>
<span data-ttu-id="378b7-116">發行者必須負責在 SQL Azure 中備妥資料集。</span><span class="sxs-lookup"><span data-stu-id="378b7-116">Having dataset ready in SQL Azure is Publisher’s responsibility.</span></span> <span data-ttu-id="378b7-117">您必須訂閱 Azure、佈建適當大小的資料庫，以及將您的資料上傳到 SQL Azure DB。</span><span class="sxs-lookup"><span data-stu-id="378b7-117">You’ll need to subscribe to Azure, provision appropriate size of Database and upload your Data into SQL Azure DB.</span></span> <span data-ttu-id="378b7-118">發行者也必須負責將自己的資料保持在最新的狀態。</span><span class="sxs-lookup"><span data-stu-id="378b7-118">Publisher is also responsible to keep his/her data always up-to-date.</span></span> <span data-ttu-id="378b7-119">如需訂閱各種 Azure 服務的詳細資訊，請參閱 [https://azure.microsoft.com/services/sql-database/](https://azure.microsoft.com/services/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="378b7-119">More information about subscribing to Azure Services you can find on [https://azure.microsoft.com/services/sql-database/](https://azure.microsoft.com/services/sql-database/)</span></span>

<span data-ttu-id="378b7-120">當將資料移至 SQL Azure 時，Azure Marketplace 可以公開資料表與檢視表。</span><span class="sxs-lookup"><span data-stu-id="378b7-120">When moving the data into SQL Azure, the Azure Marketplace can expose tables and views.</span></span> <span data-ttu-id="378b7-121">發行者可以要指定要對使用者公開的資料表/檢視表與資料行。</span><span class="sxs-lookup"><span data-stu-id="378b7-121">The Publisher can specify which tables/views and columns are exposed to the end-user.</span></span> <span data-ttu-id="378b7-122">內容提供者更可以指定使用者所能查詢的資料行，以及只有承載才會傳回的資料行。</span><span class="sxs-lookup"><span data-stu-id="378b7-122">Further the content provider can also specify which columns can be queried by the end-user and which ones are only returned in the payload.</span></span> <span data-ttu-id="378b7-123">這為所要公開的資料庫資料提供高度的靈活性。</span><span class="sxs-lookup"><span data-stu-id="378b7-123">This gives a high level of flexibility about which data in the database should be exposed.</span></span> <span data-ttu-id="378b7-124">可查詢的資料行必須由一或多個資料庫的索引所支援。</span><span class="sxs-lookup"><span data-stu-id="378b7-124">Columns that can be queried need to be backed by one or more database indices.</span></span>

## <a name="rest-based-web-service"></a><span data-ttu-id="378b7-125">採用 REST 的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="378b7-125">REST based web service</span></span>
<span data-ttu-id="378b7-126">支援通訊協定： **僅 HTTPS**</span><span class="sxs-lookup"><span data-stu-id="378b7-126">Supported protocol: **HTTPS only**</span></span>

<span data-ttu-id="378b7-127">現有 REST 服務可以透過 Azure Marketplace 公開。</span><span class="sxs-lookup"><span data-stu-id="378b7-127">Existing REST based services can be exposed through the Azure Marketplace.</span></span> <span data-ttu-id="378b7-128">因為資料集一律會透過 OData 摘要公開給使用者，所以 Azure Marketplace 服務必須能夠將服務對應到 OData 服務。</span><span class="sxs-lookup"><span data-stu-id="378b7-128">Because the dataset is always exposed to the end-user as an OData feed, the Azure Marketplace service needs to be able to map the service to a OData based service.</span></span> <span data-ttu-id="378b7-129">為達成此目的，REST 端點必須透過 HTTP 參數公開所有參數。</span><span class="sxs-lookup"><span data-stu-id="378b7-129">To do so the REST based endpoints need to expose all parameters as HTTP parameters.</span></span>

<span data-ttu-id="378b7-130">承載的格式必須能夠對應到 ATOM 回應。</span><span class="sxs-lookup"><span data-stu-id="378b7-130">The payload needs to be in a form that can be mapped into an ATOM response.</span></span> <span data-ttu-id="378b7-131">因此，服務的回應必須是 XML 格式，而且只可包含一個重複的元素 (內含記錄集一類的承載值)。</span><span class="sxs-lookup"><span data-stu-id="378b7-131">Hence the response from the services needs to be in XML format and can only contain one repeating element that contains the payload values (like record set).</span></span> <span data-ttu-id="378b7-132">Azure Marketplace 服務會將重複的節點對應到 ATOM 中的的項目節點，再將承載值對應用到該項目節點中的屬性節點。</span><span class="sxs-lookup"><span data-stu-id="378b7-132">The Azure Marketplace service will map the repeating node to the entry node in ATOM and the payload values into property nodes within the entry node.</span></span>

<span data-ttu-id="378b7-133">授權資訊 (例如 API 金鑰、驗證權杖等等) 必須透過 HTTP 參數或在 HTTP 標頭 (機碼值組) 中提供，而基本驗證也可使用此法。</span><span class="sxs-lookup"><span data-stu-id="378b7-133">Authorization information (such as API key, authentication token, etc.) needs to be provided as an HTTP parameter or in the HTTP header (key value pair) – basic authentication is also supported.</span></span> <span data-ttu-id="378b7-134">必須提供有效的金鑰，而所有經由 Azure Marketplace 的要求都會由該金鑰發出。</span><span class="sxs-lookup"><span data-stu-id="378b7-134">A valid key needs to be provided and all requests through Azure Marketplace are being made through that key.</span></span> <span data-ttu-id="378b7-135">使用者監視與帳單會在 Azure Marketplace 層發生。</span><span class="sxs-lookup"><span data-stu-id="378b7-135">User monitoring and billing happens at the Azure Marketplace layer.</span></span>

<span data-ttu-id="378b7-136">服務傳回的錯誤必須對應到 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="378b7-136">Errors returned by the service need to be mapped into HTTP status codes.</span></span> <span data-ttu-id="378b7-137">若服務傳回的 XML 包含了錯誤，Azure Marketplace 服務會將其對應到 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="378b7-137">In case the service returns a XML that contains the error these are going to be mapped by the Azure Marketplace service to HTTP status codes.</span></span>

## <a name="soap-based-web-services"></a><span data-ttu-id="378b7-138">採用 SOAP 的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="378b7-138">SOAP based web services</span></span>
<span data-ttu-id="378b7-139">通訊協定： **僅 HTTPS**</span><span class="sxs-lookup"><span data-stu-id="378b7-139">Protocol: **HTTPS only**</span></span>

<span data-ttu-id="378b7-140">這類服務的需求與 REST 服務一節所述相同。</span><span class="sxs-lookup"><span data-stu-id="378b7-140">The requirements are the same as in the REST based service section.</span></span> <span data-ttu-id="378b7-141">唯一差別是每一個透過 Azure Marketplace 所發出的要求，也可在要張貼到發行者服務的 XML 主體中提供參數。</span><span class="sxs-lookup"><span data-stu-id="378b7-141">The only difference is that parameters can also be provided in an XML body that’s being posted to the Publisher’s service with every request made through Azure Marketplace.</span></span> <span data-ttu-id="378b7-142">這表示使用者在前端提供的 HTTP 參數，將會在對內容提供者 Web 服務發出要求時，轉譯成所要張貼之 XML 文件的 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="378b7-142">This means that HTTP parameters the user provides at the front-end are being translated into XML elements of an XML document that’s being posted with the request to the content provider’s web service.</span></span>

## <a name="odata-based-web-services"></a><span data-ttu-id="378b7-143">採用 OData 的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="378b7-143">OData based web services</span></span>
<span data-ttu-id="378b7-144">通訊協定： **僅 HTTPS**</span><span class="sxs-lookup"><span data-stu-id="378b7-144">Protocol: **HTTPS only**</span></span>

<span data-ttu-id="378b7-145">資料可以在 Azure Marketplace 以OData 服務公開。</span><span class="sxs-lookup"><span data-stu-id="378b7-145">Data can be exposed as an OData service to Azure Marketplace.</span></span> <span data-ttu-id="378b7-146">系統會透過服務連接，並以 Azure Marketplace 服務的根目錄取代服務的根目錄，以確保後續的所有呼叫皆會透過 Azure Marketplace 服務的根目錄。</span><span class="sxs-lookup"><span data-stu-id="378b7-146">The system is going to pass the service through and replaces the root of the service with the Azure Marketplace service root – to ensure all subsequent calls go through Azure Marketplace.</span></span>

<span data-ttu-id="378b7-147">OData 服務不再只是需要仰賴後端的資料庫。</span><span class="sxs-lookup"><span data-stu-id="378b7-147">OData services don’t only need to go against a database in the backend.</span></span> <span data-ttu-id="378b7-148">OData 支援各種儲存體或商務邏輯，讓服務能夠順利運行。</span><span class="sxs-lookup"><span data-stu-id="378b7-148">OData supports any kind of storage or business logic to drive the service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="378b7-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="378b7-149">Next Steps</span></span>
<span data-ttu-id="378b7-150">至此，您已經檢閱了各項必要條件，而且也完成了各項必要工作，您可以依照 [資料服務的發行指導](marketplace-publishing-data-service-creation.md)所述，繼續建立您的資料服務產品。</span><span class="sxs-lookup"><span data-stu-id="378b7-150">Now that you reviewed the pre-requisites and completed the necessary tasks, you can move forward with the creating your Data Service offer as detailed in the [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

<span data-ttu-id="378b7-151">若您想要重新檢閱整個流程，以及每個發行階段的各篇文章，請參閱 [快速入門：如何將產品發行到 Azure Marketplace](marketplace-publishing-getting-started.md)一文。</span><span class="sxs-lookup"><span data-stu-id="378b7-151">Or, if you would like to review the overall process and the respective articles for each of the publishing phases, please visit the article [Getting Started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

[link-acct]:marketplace-publishing-accounts-creation-registration.md
