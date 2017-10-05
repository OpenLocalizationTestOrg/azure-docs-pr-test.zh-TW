---
title: "建立 Marketplace 資料服務的指南 | Microsoft Docs"
description: "如何建立、認證和部署資料服務供他人在 Azure Marketplace 上購買的詳細指示。"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3a632825-db5b-49ec-98bd-887138798bc4
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: a853b4dbd1952ba4ea8ee68ea3ca98f588bb71a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="mapping-an-existing-web-service-to-odata-through-csdl"></a><span data-ttu-id="a6968-103">透過 CSDL 將現有的 Web 服務對應至 OData</span><span class="sxs-lookup"><span data-stu-id="a6968-103">Mapping an existing web service to OData through CSDL</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a6968-104">目前我們已不再針對任何新的資料服務發行者進行上架。新的 Dataservice 將不會獲得核准以列出於清單上。</span><span class="sxs-lookup"><span data-stu-id="a6968-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="a6968-105">如果您有想要在 AppSource 上發佈的 SaaS 商務應用程式，您可以在[這裡](https://appsource.microsoft.com/partners)找到詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a6968-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="a6968-106">如果您有想要在 Azure Marketplace 發佈的 IaaS 應用程式或開發人員服務，您可以在[這裡](https://azure.microsoft.com/marketplace/programs/certified/)找到詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a6968-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="a6968-107">本文提供如何使用 CSDL 來將現有的服務對應至 OData 相容服務的概觀。</span><span class="sxs-lookup"><span data-stu-id="a6968-107">This article gives an overview on how to use a CSDL to map an existing service to an OData compatible service.</span></span> <span data-ttu-id="a6968-108">其中將說明如何建立對應文件 (CSDL)，透過服務呼叫轉換來自用戶端的輸入要求，並透過 OData 相容的摘要將輸出 (資料) 傳輸回用戶端。</span><span class="sxs-lookup"><span data-stu-id="a6968-108">It explains how to create the mapping document (CSDL) that transforms the input request from the client via a service call and the output (data) back to the client via an OData compatible feed.</span></span> <span data-ttu-id="a6968-109">Microsoft Azure Marketplace 會使用 OData 通訊協定，向使用者公開服務。</span><span class="sxs-lookup"><span data-stu-id="a6968-109">Microsoft’s Azure Marketplace exposes services to the end-users by using the OData protocol.</span></span> <span data-ttu-id="a6968-110">內容提供者 (資料擁有者) 所公開的服務會以各種不同形式 (例如 REST、 SOAP 等) 來公開。</span><span class="sxs-lookup"><span data-stu-id="a6968-110">Services that are exposed by content providers (Data Owners) are exposed in a variety of forms, such as REST, SOAP, etc.</span></span>

## <a name="what-is-a-csdl-and-its-structure"></a><span data-ttu-id="a6968-111">什麼是 CSDL 及其結構？</span><span class="sxs-lookup"><span data-stu-id="a6968-111">What is a CSDL and its structure?</span></span>
<span data-ttu-id="a6968-112">CSDL (概念結構定義語言) 是一項規格，會定義如何使用常見的 XML 用語來說明對於 Azure Marketplace 的 Web 服務或資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="a6968-112">A CSDL (Conceptual Schema Definition Language) is a specification defining how to describe web service or database service in common XML verbiage to the Azure Marketplace.</span></span>

<span data-ttu-id="a6968-113">**要求流程**</span><span class="sxs-lookup"><span data-stu-id="a6968-113">Simple overview of the **request flow:**</span></span>

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

<span data-ttu-id="a6968-114">**資料流程** 的方向相反：</span><span class="sxs-lookup"><span data-stu-id="a6968-114">The **data flow** is in the opposite direction:</span></span>

  `Client <- Azure Marketplace <- Content Provider’s WebService`

<span data-ttu-id="a6968-115">**圖 1** 圖解說明用戶端如何透過 Azure Marketplace，從內容提供者 (您的服務) 取得資料。</span><span class="sxs-lookup"><span data-stu-id="a6968-115">**Figure 1** diagrams how a client would obtain data from a content provider (your service) by going through the Azure Marketplace.</span></span>  <span data-ttu-id="a6968-116">對應/轉換元件會使用 CSDL 來處理內容提供者的服務和要求用戶端之間的要求和資料傳遞。</span><span class="sxs-lookup"><span data-stu-id="a6968-116">The CSDL is used by the Mapping/Transformation component to handle the request and data pass between the content provider’s service(s) and the requesting client.</span></span>

<span data-ttu-id="a6968-117">*圖 1：透過 Azure Marketplace，從要求用戶端到內容提供者的詳細流程*</span><span class="sxs-lookup"><span data-stu-id="a6968-117">*Figure 1: Detailed flow from requesting client to content provider via Azure Marketplace*</span></span>

  ![繪圖](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

<span data-ttu-id="a6968-119">如需 Atom、Atom Pub 和 OData 通訊協定 (Azure Marketplace 延伸模組會據以建置) 的背景，請檢閱： [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span><span class="sxs-lookup"><span data-stu-id="a6968-119">For background on Atom, Atom Pub, and the OData protocol upon which the Azure Marketplace extensions build, please review: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span></span>

<span data-ttu-id="a6968-120">摘錄自上述連結：*「開放式資料通訊協定 (以下稱為 OData) 的目的是根據公開為資料服務的資源，為 CRUD 樣式的操作 (建立、讀取、更新及刪除) 提供以 REST 為基礎的通訊協定。「資料服務」是一個端點，其中含有公開自一或多個「集合」的資料，每個集合均包含零到多個「項目」，這些項目是由具類型的具名值組所組成。OData 是 Microsoft 基於 OASIS (Organization for the Advancement of Structured Information Standards) 標準所發佈，因此，任何有需要的人都能建置伺服器、用戶端或工具，而沒有任何權利金或限制。」*</span><span class="sxs-lookup"><span data-stu-id="a6968-120">Excerpt from above link: *“The purpose of the Open Data protocol (hereafter referred to as OData) is to provide a REST-based protocol for CRUD-style operations (Create, Read, Update and Delete) against resources exposed as data services. A “data service” is an endpoint where there is data exposed from one or more “collections” each with zero or more “entries”, which consist of typed named-value pairs. OData is published by Microsoft under OASIS (Organization for the Advancement of Structured Information Standards) Standards so that anyone that wants to can build servers, clients or tools without royalties or restrictions.”*</span></span>

### <a name="three-critical-pieces-that-have-to-be-defined-by-the-csdl-are"></a><span data-ttu-id="a6968-121">以下是三個必須由 CSDL 定義的關鍵部分：</span><span class="sxs-lookup"><span data-stu-id="a6968-121">Three Critical Pieces that have to be defined by the CSDL are:</span></span>
* <span data-ttu-id="a6968-122">服務提供者的**端點**。服務的 Web 位址 (URI)</span><span class="sxs-lookup"><span data-stu-id="a6968-122">The **endpoint** of the Service Provider The Web Address (URI) of the Service</span></span>
* <span data-ttu-id="a6968-123">當成輸入傳遞至服務提供者**資料參數**。傳送至內容提供者服務 (向下至資料類型) 的參數定義。</span><span class="sxs-lookup"><span data-stu-id="a6968-123">The **data parameters** being passed as input to the Service Provider The definitions of the parameters being sent to the Content Provider’s service down to the data type.</span></span>
* <span data-ttu-id="a6968-124">傳回要求服務之資料的**結構描述**。內容提供者服務所傳遞之資料的結構描述，包括容器、集合/資料表、變數/資料行，以及資料類型。</span><span class="sxs-lookup"><span data-stu-id="a6968-124">**Schema** of the data being returned to the Requesting Service The schema of the data being delivered by the Content Provider’s service, including Container, collections/tables, variables/columns, and data types.</span></span>

<span data-ttu-id="a6968-125">下圖顯示從用戶端輸入 OData 陳述式 (呼叫內容提供者的 Web 服務) 到取回結果/資料的流程概觀。</span><span class="sxs-lookup"><span data-stu-id="a6968-125">The following diagram shows an overview of the flow from where the client enters the OData statement (call to the content provider’s web service) to getting the results/data back.</span></span>

  ![繪圖](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a><span data-ttu-id="a6968-127">步驟：</span><span class="sxs-lookup"><span data-stu-id="a6968-127">Steps:</span></span>
1. <span data-ttu-id="a6968-128">用戶端透過使用 XML 中定義的輸入參數填入的服務呼叫，將要求傳送到 Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="a6968-128">Client sends request via Service call complete with Input Parameters defined in XML to the Azure Marketplace</span></span>
2. <span data-ttu-id="a6968-129">CSDL 可用來驗證服務呼叫。</span><span class="sxs-lookup"><span data-stu-id="a6968-129">CSDL is used to validate the Service call.</span></span>
   * <span data-ttu-id="a6968-130">格式化的服務呼叫接著會由 Azure Marketplace 傳送到內容提供者服務</span><span class="sxs-lookup"><span data-stu-id="a6968-130">The Formatted Service Call is then sent to the Content Providers Service by the Azure Marketplace</span></span>
3. <span data-ttu-id="a6968-131">WebService 會執行，並執行 Http 指令動詞 (例如 GET) 的動作。資料會傳回 Azure Marketplace，其中的要求資料 (如果有的話) 會使用 CSDL 中定義的對應，以 XML 格式公開至用戶端。</span><span class="sxs-lookup"><span data-stu-id="a6968-131">The Webservice executes and preforms the action of the Http Verb (i.e. GET) The data is returned to Azure Marketplace where the requested data (if any) is exposes in XML Format to the Client using the Mapping defined in the CSDL.</span></span>
4. <span data-ttu-id="a6968-132">用戶端會以 XML 或 JSON 格式傳送資料 (如果有的話)</span><span class="sxs-lookup"><span data-stu-id="a6968-132">The Client is sent the data (if any) in XML or JSON format</span></span>

## <a name="definitions"></a><span data-ttu-id="a6968-133">定義</span><span class="sxs-lookup"><span data-stu-id="a6968-133">Definitions</span></span>
### <a name="odata-atom-pub"></a><span data-ttu-id="a6968-134">OData ATOM Pub</span><span class="sxs-lookup"><span data-stu-id="a6968-134">OData ATOM pub</span></span>
<span data-ttu-id="a6968-135">ATOM Pub 的延伸模組，其中每個項目代表結果集的一個資料列。</span><span class="sxs-lookup"><span data-stu-id="a6968-135">An extension to the ATOM pub where each entry represents one row of a result set.</span></span> <span data-ttu-id="a6968-136">項目的內容部分已增強來包含資料列的值 - 做為索引鍵值組。</span><span class="sxs-lookup"><span data-stu-id="a6968-136">The content part of the entry is enhanced to contain the values of the row – as key value pairs.</span></span> <span data-ttu-id="a6968-137">您可以在此處找到詳細資訊： [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span><span class="sxs-lookup"><span data-stu-id="a6968-137">More information is found here: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span></span>

### <a name="csdl---conceptual-schema-definition-language"></a><span data-ttu-id="a6968-138">CSDL - 概念結構定義語言</span><span class="sxs-lookup"><span data-stu-id="a6968-138">CSDL - Conceptual Schema Definition Language</span></span>
<span data-ttu-id="a6968-139">允許定義透過資料庫公開的函式 (SPROC) 和實體。</span><span class="sxs-lookup"><span data-stu-id="a6968-139">Allows defining functions (SPROCs) and entities that are exposed through a database.</span></span> <span data-ttu-id="a6968-140">您可以在此處找到詳細資訊： [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span><span class="sxs-lookup"><span data-stu-id="a6968-140">More information found here: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span></span>  

> [!TIP]
> <span data-ttu-id="a6968-141">如果您看不到該篇文章，請按一下 [其他版本] 下拉式清單並選取一個版本。</span><span class="sxs-lookup"><span data-stu-id="a6968-141">Click the **other versions** dropdown and select a version if you don’t see the article.</span></span>
> 
> 

### <a name="edm---entry-data-model"></a><span data-ttu-id="a6968-142">EDM - 項目資料模型</span><span class="sxs-lookup"><span data-stu-id="a6968-142">EDM - Entry Data Model</span></span>
* <span data-ttu-id="a6968-143">概觀︰[http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span><span class="sxs-lookup"><span data-stu-id="a6968-143">Overview: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span></span>

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* <span data-ttu-id="a6968-144">預覽︰[http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span><span class="sxs-lookup"><span data-stu-id="a6968-144">Preview: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span></span>

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* <span data-ttu-id="a6968-145">資料類型：[http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span><span class="sxs-lookup"><span data-stu-id="a6968-145">Data types: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span></span>

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

<span data-ttu-id="a6968-146">下圖顯示從用戶端輸入 OData 陳述式 (呼叫內容提供者的 Web 服務) 到取回結果/資料的詳細流程 (從左至右)：</span><span class="sxs-lookup"><span data-stu-id="a6968-146">The following shows the detailed Left to Right flow from where the client enters the OData statement (call to the content provider’s web service) to getting the results/data back:</span></span>

  ![繪圖](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a><span data-ttu-id="a6968-148">CSDL 基本概念</span><span class="sxs-lookup"><span data-stu-id="a6968-148">CSDL Basics</span></span>
<span data-ttu-id="a6968-149">CSDL (概念結構定義語言) 是一項規格，會定義如何使用常見的 XML 用語來說明對於 Azure Marketplace 的 Web 服務或資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="a6968-149">A CSDL (Conceptual Schema Definition Language) is a specification defining how to describe web service or database service in common XML verbiage to the Azure Marketplace.</span></span> <span data-ttu-id="a6968-150">CSDL 說明**盡可能將資料從資料來源傳遞至 Azure Marketplace** 的重要部分。</span><span class="sxs-lookup"><span data-stu-id="a6968-150">CSDL describes the critical pieces that **makes the passing of data from the Data Source to the Azure Marketplace possible.**</span></span> <span data-ttu-id="a6968-151">主要部分如下所示：</span><span class="sxs-lookup"><span data-stu-id="a6968-151">The main pieces are described here:</span></span>

* <span data-ttu-id="a6968-152">說明所有對外公開使用之函式 (FunctionImport 節點) 的介面資訊</span><span class="sxs-lookup"><span data-stu-id="a6968-152">Interface information describing all publicly available functions (FunctionImport Node)</span></span>
* <span data-ttu-id="a6968-153">適用於所有訊息要求 (輸入) 和訊息回應 (輸出) (EntityContainer/EntitySet/EntityType 節點) 的資料類型資訊</span><span class="sxs-lookup"><span data-stu-id="a6968-153">Data type information for all message requests(input) and message responses(outputs) (EntityContainer/EntitySet/EntityType Nodes)</span></span>
* <span data-ttu-id="a6968-154">關於要使用之傳輸通訊協定 (標頭節點) 的繫結資訊</span><span class="sxs-lookup"><span data-stu-id="a6968-154">Binding information about the transport protocol to be used (Header Node)</span></span>
* <span data-ttu-id="a6968-155">可用以尋找指定服務 (BaseURI 屬性) 的位址資訊</span><span class="sxs-lookup"><span data-stu-id="a6968-155">Address information for locating the specified service (BaseURI attribute)</span></span>

<span data-ttu-id="a6968-156">簡單來說，CSDL 表示在服務要求者和服務提供者之間與平台及語言無關的合約。</span><span class="sxs-lookup"><span data-stu-id="a6968-156">In a nutshell, the CSDL represents a platform- and language-independent contract between the service requestor and the service provider.</span></span> <span data-ttu-id="a6968-157">使用 CSDL，用戶端可以找到 Web 服務/資料庫服務，並叫用任何其公開可用的函式。</span><span class="sxs-lookup"><span data-stu-id="a6968-157">Using the CSDL, a client can locate a web service/database service and invoke any of its publicly available functions.</span></span>

### <a name="relating-a-csdl-to-a-database-or-a-collection"></a><span data-ttu-id="a6968-158">將 CSDL 關聯至資料庫或集合</span><span class="sxs-lookup"><span data-stu-id="a6968-158">Relating a CSDL to a Database or a Collection</span></span>
<span data-ttu-id="a6968-159">**CSDL 規格**</span><span class="sxs-lookup"><span data-stu-id="a6968-159">**The CSDL Specification**</span></span>

<span data-ttu-id="a6968-160">CSDL 是說明 Web 服務的 XML 文法。</span><span class="sxs-lookup"><span data-stu-id="a6968-160">CSDL is XML grammar for describing a web service.</span></span> <span data-ttu-id="a6968-161">規格本身分成 4 個主要元素：EntitySet、FunctionImport、NameSpace 和 EntityType。</span><span class="sxs-lookup"><span data-stu-id="a6968-161">The specification itself is divided into 4 major elements:  EntitySet, FunctionImport; NameSpace, and EntityType.</span></span>

<span data-ttu-id="a6968-162">若要讓這個抽象層更容易了解，可讓 CSDL 關聯至資料表。</span><span class="sxs-lookup"><span data-stu-id="a6968-162">To make this abstraction easier to understand lets relate a CSDL to a table.</span></span>

<span data-ttu-id="a6968-163">請記住；</span><span class="sxs-lookup"><span data-stu-id="a6968-163">Remember;</span></span>

  <span data-ttu-id="a6968-164">CSDL 表示在**服務要求者**和**服務提供者**之間與平台及語言無關的合約。</span><span class="sxs-lookup"><span data-stu-id="a6968-164">CSDL represents a platform- and language-independent contract between the **service requestor** and the **service provider**.</span></span> <span data-ttu-id="a6968-165">使用 CSDL，**用戶端**可以找到 **Web 服務/資料庫服務**，並叫用任何其公開可用的**函式**。</span><span class="sxs-lookup"><span data-stu-id="a6968-165">Using CSDL, a **client** can locate a **web service/database service** and invoke any of its publicly available **functions.**</span></span>

<span data-ttu-id="a6968-166">針對資料服務，可從資料庫、資料表、資料行及預存程序等方面來理解 CSDL 的四個部分。</span><span class="sxs-lookup"><span data-stu-id="a6968-166">For a Data Service the four parts of a CSDL can be thought of in terms of a Database, Table, Column, and Store Procedure.</span></span>

<span data-ttu-id="a6968-167">針對資料服務，可使用如下方式來關聯這些項目：</span><span class="sxs-lookup"><span data-stu-id="a6968-167">Relating these as follows for a Data Service:</span></span>

* <span data-ttu-id="a6968-168">EntityContainer  ~=  資料庫</span><span class="sxs-lookup"><span data-stu-id="a6968-168">EntityContainer  ~=  Database</span></span>
* <span data-ttu-id="a6968-169">EntitySet  ~=  資料表</span><span class="sxs-lookup"><span data-stu-id="a6968-169">EntitySet  ~=  Table</span></span>
* <span data-ttu-id="a6968-170">EntityType  ~=  資料行</span><span class="sxs-lookup"><span data-stu-id="a6968-170">EntityType  ~= Columns</span></span>
* <span data-ttu-id="a6968-171">FunctionImport  ~=  預存程序</span><span class="sxs-lookup"><span data-stu-id="a6968-171">FunctionImport  ~=  Stored Procedure</span></span>

<span data-ttu-id="a6968-172">**允許的 HTTP 動詞命令**</span><span class="sxs-lookup"><span data-stu-id="a6968-172">**HTTP Verbs allowed**</span></span>

* <span data-ttu-id="a6968-173">GET – 從 db 傳回值 (傳回集合)</span><span class="sxs-lookup"><span data-stu-id="a6968-173">GET – returns values from the db (returns a Collection)</span></span>
* <span data-ttu-id="a6968-174">POST – 用來傳送資料到 db 和選擇性從 db 傳回值 (在集合中建立新項目，傳回 id/URI)</span><span class="sxs-lookup"><span data-stu-id="a6968-174">POST – used to pass data to and optional return values from the db (Create a new entry in the collection, return id/URI)</span></span>
* <span data-ttu-id="a6968-175">DELETE – 從 DB 刪除資料 (刪除集合)</span><span class="sxs-lookup"><span data-stu-id="a6968-175">DELETE – Deletes data from the DB (Deletes a collection)</span></span>
* <span data-ttu-id="a6968-176">PUT – 更新資料到 DB (取代集合或建立一個集合)</span><span class="sxs-lookup"><span data-stu-id="a6968-176">PUT – Update data into a DB (replace a collection or create one)</span></span>

## <a name="metadatamapping-document"></a><span data-ttu-id="a6968-177">中繼資料/對應文件</span><span class="sxs-lookup"><span data-stu-id="a6968-177">Metadata/Mapping Document</span></span>
<span data-ttu-id="a6968-178">中繼資料/對應文件可用來對應內容提供者的現有 Web 服務，讓它能夠透過 Azure Marketplace 系統公開為 OData Web 服務。</span><span class="sxs-lookup"><span data-stu-id="a6968-178">The metadata/mapping document is used to map a content provider’s existing web services so that it can be exposed as an OData web service by the Azure Marketplace system.</span></span> <span data-ttu-id="a6968-179">它會以 CSDL 為基礎，並實作數個 CSDL 延伸模組，以滿足透過 Azure Marketplace 公開之以 REST 為基礎的 Web 服務需求。</span><span class="sxs-lookup"><span data-stu-id="a6968-179">It is based on CSDL and implements a few extensions to CSDL to accommodate the needs of REST based web services exposed through Azure Marketplace.</span></span> <span data-ttu-id="a6968-180">您可以在 [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) 命名空間中找到延伸模組。</span><span class="sxs-lookup"><span data-stu-id="a6968-180">The extensions are found in the [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) namespace.</span></span>

<span data-ttu-id="a6968-181">CSDL 的範例如下：(複製下列範例 CSDL 並貼至 XML 編輯器，然後進行變更以符合您的服務。</span><span class="sxs-lookup"><span data-stu-id="a6968-181">An example of the CSDL follows:  (Copy and paste the below example CSDL into an XML editor and change to match your Service.</span></span>  <span data-ttu-id="a6968-182">然後在 [Azure Marketplace 發佈入口網站](https://publish.windowsazure.com)) 中建立您的服務時，貼至 [DataService] 索引標籤底下的 CSDL 對應。</span><span class="sxs-lookup"><span data-stu-id="a6968-182">Then paste into CSDL Mapping under DataService tab when creating your service in the  [Azure Marketplace Publishing Portal](https://publish.windowsazure.com)).</span></span>

<span data-ttu-id="a6968-183">**詞彙：** 將 CSDL 詞彙與 [發佈入口網站](https://publish.windowsazure.com) UI (PPUI) 詞彙建立關聯。</span><span class="sxs-lookup"><span data-stu-id="a6968-183">**Terms:** Relating the CSDL terms to the [Publishing Portal](https://publish.windowsazure.com) UI (PPUI) terms.</span></span>

* <span data-ttu-id="a6968-184">PPUI 中的供應項目「標題」與 MyWebOffer 相關聯</span><span class="sxs-lookup"><span data-stu-id="a6968-184">Offer “Title” in the PPUI relates to MyWebOffer</span></span>
* <span data-ttu-id="a6968-185">PPUI 中的 MyCompany 與 [Microsoft 開發人員中心](http://dev.windows.com/registration?accountprogram=azure) UI 中的 [發行者顯示名稱] 相關聯</span><span class="sxs-lookup"><span data-stu-id="a6968-185">MyCompany in the PPUI relates to **Publisher Display Name** in the [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) UI</span></span>
* <span data-ttu-id="a6968-186">您的 API 與 Web 或資料服務相關聯 (在 PPUI 中的計畫)</span><span class="sxs-lookup"><span data-stu-id="a6968-186">Your API relates to a Web or Data Service (a Plan in the PPUI)</span></span>

<span data-ttu-id="a6968-187">**階層：** 公司 (內容提供者) 擁有具有方案 (即服務) 的優惠，可利用 API 來排列。</span><span class="sxs-lookup"><span data-stu-id="a6968-187">**Hierarchy:** A Company (Content Provider) owns Offer(s) which have Plan(s), namely service(s), which line up with an API.</span></span>

### <a name="webservice-csdl-example"></a><span data-ttu-id="a6968-188">WebService CSDL 範例</span><span class="sxs-lookup"><span data-stu-id="a6968-188">WebService CSDL Example</span></span>
<span data-ttu-id="a6968-189">連接至公開 Web 應用程式端點 (例如 C# 應用程式) 的服務</span><span class="sxs-lookup"><span data-stu-id="a6968-189">Connects to a service that is exposing an web application endpoint (like a C# application)</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <!-- The namespace attribute below is used by our system to generate C#. You can change “MyCompany.MyOffer” to something that makes sense for you, but change “MyOffer” consistently throughout the document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all the web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in the customer facing UI as name of the Service.
        @EntityType is used to point at the type definition near the bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is the entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines the service call, replace & with the encode value (&amp;).
        In the input name value pairs {param} represents passed in value.
        Or the value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows the CSDL to specifically specify the verb of the service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes the parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how the web service call is exposed to marketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, the {...} point to the parameters defined below.
        Marketplace will read the parameters from this URITemplate and fill the values into the corresponding parameters of the BaseUri or RequestBody (below) during calls to your service.  
        It is okay for @d:BaseUri to include information only for Marketplace consumption, it will not be exposed to end users. i.e. the hardcoded AccountKey in the above BaseURI does not show up in the client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of the RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders to insert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how to pass userid and password via the header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed to end users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with the value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited to appearing as the value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used to specify values to insert into the ATOM feed returned to the end user.  You can specify the element to contain a fixed message by providing a value for the element (this is the default value).  @d:Map is an XPath expression that points into the response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay to also add a d:Map attribute to override this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of the web service call:
        @Name should match exactly (case sensitive) the {…} placeholders in the @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is the EDM.SimpleType of the parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether the parameter is required.
        @d:Regex - optional, attribute to describe the string, limiting unwanted input at the entry of the system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in the Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating the service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in the order listed.
        @d:Match is an Xpath query on the service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is the error code to return if an response matches the error.
        @d:errorMessage is the user friendly message to return when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect to the service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- The EntityContainer defines the output data schema -->
        </EntityContainer>
        <!-- The EntityType @d:Map defines the repeating node (an XPath query) in the response (output data schema). -->
        <!-- If these nodes are outside a namespace, add the prefix in the xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in the ATOM feed, so comply with the XML element naming restrictions (no spaces or other illegal characters).
        @Type is the EDM.SimpleType of the parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query to point at the location to extract the content from your services response.
        The "." is relative to the repeating node in the EntityType @d:Map Xpath expression.
        -->
            <EntityType Name="MyEntityType" d:Map="/MyResponse/MyEntities">
        <Property Name="ID"    d:IsPrimaryKey="True" Type="Int32"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="Amount"    Type="Double"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="City"    Type="String"    Nullable="false" d:Map="./City"/>
        <Property Name="State"    Type="String"    Nullable="false" d:Map="./State"/>
        <Property Name="Zip"    Type="Int32"    Nullable="false" d:Map="./Zip"/>
        <Property Name="Updated"    Type="DateTime"    Nullable="false" d:Map="./Updated"/>
        <Property Name="AdditionalInfo" Type="String" Nullable="true"
        d:Map="./Info/More[1]"/>
            </EntityType>
        </Schema>

> [!TIP]
> <span data-ttu-id="a6968-190">在 [透過 CSDL 將現有的 Web 服務對應至 OData 的範例](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span><span class="sxs-lookup"><span data-stu-id="a6968-190">View more CSDL Web Service examples in the article [Examples of mapping an existing web service to OData through CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span></span>
> 
> 

### <a name="dataservice-csdl-example"></a><span data-ttu-id="a6968-191">DataService CSDL 範例</span><span class="sxs-lookup"><span data-stu-id="a6968-191">DataService CSDL Example</span></span>
<span data-ttu-id="a6968-192">連接到將資料庫資料表或檢視公開為端點的服務。以下範例顯示兩個以資料庫為基礎之 API CSDL 的 API (可以使用檢視，而不是資料表)。</span><span class="sxs-lookup"><span data-stu-id="a6968-192">Connects to a service that is exposing a database table or view as an endpoint Below example shows two APIs for Data base based API CSDL (can use views rather than tables).</span></span>

        <?xml version="1.0"?>
        <!-- The namespace attribute below is used by our system to generate C#. You can change “MyCompany.MyOffer” to something that makes sense for you, but change “MyOffer” consistently throughout the document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all the data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of the EntitySet as a Service
        @Name is used in the customer facing UI as name of the Service.
        @EntityType is used to point at the type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); the table (or view) and columns to be returned by the data service.)
            Map is the schema.tabel or schema.view
            dals.TableName is the table Name
            Name is the name identifier for the EntityType and the Name of the service exposed to the client via the UI.
            dals:IsExposed determines if the table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is the schema name of the table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines the column properties and the output of the service.
            dals:ColumnName is the name of the column in the table /view.
            Type is the emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is the maximum length of the output value
            Name is the name of the Property and is exposed to the client facing UI
            dals:IsReturned is the Boolean that determines if the Service exposes this value to the client.
            IsQueryable is the Boolean that determines if the column can be used in a database query
            (For data Services: To improve Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is the numerical position x in the table or the View, where x is from 1 to the number of columns in the table.
            dals:DatabaseDataType is the data type of the column in the database, i.e. SQL data type dals:IsPrimaryKey indicates if the column is the Primary key in the table/view.  (The columns marked ISPrimaryKey are used in the Order by clause when returning data.)
        -->
        <Property dals:ColumnName="data" Type="String" Nullable="true" dals:CharMaxLength="-1" Name="data" dals:IsReturned="true" dals:IsQueryable="false" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="ticker" Type="String" Nullable="true" dals:CharMaxLength="10" Name="ticker" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        <EntityType Map="[dbo].[ProductInfo]" dals:TableName="ProductInfo" Name="ProductInfo" dals:IsExposed="true" dals:IsView="false" dals:TableSchema="dbo" xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <Property dals:ColumnName="companyid" Type="Int32" Nullable="true" Name="companyid" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="product" Type="String" Nullable="true" dals:CharMaxLength="50" Name="product" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        </Schema>

## <a name="see-also"></a><span data-ttu-id="a6968-193">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a6968-193">See Also</span></span>
* <span data-ttu-id="a6968-194">如果您有興趣學習和了解特定節點及其參數，請閱讀 [資料服務 OData 對應節點](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) 一文，來了解定義和說明、範例，以及使用案例內容。</span><span class="sxs-lookup"><span data-stu-id="a6968-194">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="a6968-195">如果您有興趣檢閱範例，請閱讀 [資料服務 OData 對應範例](marketplace-publishing-data-service-creation-odata-mapping-examples.md) 一文，來查看範例程式碼，並了解程式碼語法與內容。</span><span class="sxs-lookup"><span data-stu-id="a6968-195">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) to see sample code and understand code syntax and context.</span></span>
* <span data-ttu-id="a6968-196">若要返回用於將資料服務發佈至 Azure Marketplace 的指定路徑，請閱讀 [資料服務發佈指南](marketplace-publishing-data-service-creation.md)一文。</span><span class="sxs-lookup"><span data-stu-id="a6968-196">To return to the prescribed path for publishing a Data Service to the Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

