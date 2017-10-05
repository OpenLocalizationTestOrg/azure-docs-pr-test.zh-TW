---
title: "建立 Marketplace 資料服務的指南 | Microsoft Docs"
description: "如何建立、認證和部署資料服務供他人在 Azure Marketplace 上購買的詳細指示。"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 148f8638-ee80-4100-8d63-5afa4167ca1b
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2ab624941fc385f14b62bb5d743927f157955845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="examples-of-mapping-an-existing-web-service-to-odata-through-csdls"></a><span data-ttu-id="c014d-103">透過 CSDL 將現有的 Web 服務對應至 OData 的範例</span><span class="sxs-lookup"><span data-stu-id="c014d-103">Examples of mapping an existing web service to OData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c014d-104">目前我們已不再針對任何新的資料服務發行者進行上架。新的 Dataservice 將不會獲得核准以列出於清單上。</span><span class="sxs-lookup"><span data-stu-id="c014d-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="c014d-105">如果您有想要在 AppSource 上發佈的 SaaS 商務應用程式，您可以在[這裡](https://appsource.microsoft.com/partners)找到詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c014d-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="c014d-106">如果您有想要在 Azure Marketplace 發佈的 IaaS 應用程式或開發人員服務，您可以在[這裡](https://azure.microsoft.com/marketplace/programs/certified/)找到詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c014d-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="c014d-107">範例：使用 "POST" 傳回 "Raw" 資料的 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="c014d-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="c014d-108">使用 POST Raw 資料建立新的部屬並傳回其伺服器定義的 URL(location)，或更新伺服器所定義 URL 處的部分部屬。</span><span class="sxs-lookup"><span data-stu-id="c014d-108">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="c014d-109">其中的部屬是串流，即</span><span class="sxs-lookup"><span data-stu-id="c014d-109">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="c014d-110">非結構化，例如</span><span class="sxs-lookup"><span data-stu-id="c014d-110">unstructured, ex.</span></span> <span data-ttu-id="c014d-111">文字檔。</span><span class="sxs-lookup"><span data-stu-id="c014d-111">a text file.</span></span>  <span data-ttu-id="c014d-112">請注意，POST 若沒有位置則不具等冪性。</span><span class="sxs-lookup"><span data-stu-id="c014d-112">Beware POST in not idempotent without a location.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="AddUsageEvent" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Add usage event (data acquisition)</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="c014d-113">範例：使用 "DELETE" 的 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="c014d-113">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="c014d-114">使用 DELETE 移除指定的 URI。</span><span class="sxs-lookup"><span data-stu-id="c014d-114">Use DELETE to remove a specified URI.</span></span>

        <EntitySet Name="DeleteUsageFileEntitySet" EntityType="MyOffer.DeleteUsageFileEntity" />
        <FunctionImport Name="DeleteUsageFile" EntitySet="DeleteUsageFileEntitySet" ReturnType="Collection(MyOffer.DeleteUsageFileEntity)"  d:AllowedHttpMethods="DELETE" d:EncodeParameterValues="true” d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643" >
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Delete usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="DeleteUsageFileEntity" d:Map="//boolean">
        <Property Name="boolean" Type="String" Nullable="true" d:Map="./boolean" />
        </EntityType>

## <a name="example-functionimport-using-post"></a><span data-ttu-id="c014d-115">範例：使用 "POST" 的 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="c014d-115">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="c014d-116">使用 POST Raw 資料建立新的部屬並傳回其伺服器定義的 URL(location)，或更新伺服器所定義 URL 處的部分部屬。</span><span class="sxs-lookup"><span data-stu-id="c014d-116">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="c014d-117">其中的部屬是結構。</span><span class="sxs-lookup"><span data-stu-id="c014d-117">Where the subordinate is a structure.</span></span> <span data-ttu-id="c014d-118">請注意，POST 若沒有位置則不具等冪性。</span><span class="sxs-lookup"><span data-stu-id="c014d-118">Beware POST is not idempotent without a location.</span></span>

        <EntitySet Name="CreateANewModelEntitySet2" EntityType=" MyOffer.CreateANewModelEntity2" />
        <FunctionImport Name="CreateModel" EntitySet="CreateANewModelEntitySet2" ReturnType="Collection(MyOffer.CreateANewModelEntity2)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Create A New Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-put"></a><span data-ttu-id="c014d-119">範例：使用 "PUT" 的 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="c014d-119">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="c014d-120">使用 PUT 建立新的部屬，或更新伺服器所定義 URL 處的整個部屬。</span><span class="sxs-lookup"><span data-stu-id="c014d-120">Use PUT to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="c014d-121">其中的部屬是結構，PUT 具有等冪性，因此即使出現多次也將產生相同的狀態，即</span><span class="sxs-lookup"><span data-stu-id="c014d-121">Where the subordinate is a structure, PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="c014d-122">x=5。</span><span class="sxs-lookup"><span data-stu-id="c014d-122">x=5.</span></span>  <span data-ttu-id="c014d-123">Put 應與指定資源的完整內容搭配使用。</span><span class="sxs-lookup"><span data-stu-id="c014d-123">Put should be used with the full content of the specified resource.</span></span>

        <EntitySet Name="UpdateAnExistingModelEntitySet" EntityType="MyOffer.UpdateAnExistingModelEntity" />
        <FunctionImport Name="UpdateModel" EntitySet="UpdateAnExistingModelEntitySet" ReturnType="Collection(MyOffer.UpdateAnExistingModelEntity)" d:EncodeParameterValues="true" d:AllowedHttpMethods="PUT" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Update an Existing Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="UpdateAnExistingModelEntity" d:Map="//string">
        <Property Name="string"     Type="String" Nullable="true" d:Map="./string" />
        </EntityType>


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="c014d-124">範例：使用 "PUT" 傳回 "Raw" 資料的 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="c014d-124">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="c014d-125">使用 PUT Raw 資料建立新的部屬，或更新伺服器所定義 URL 處的整個部屬。</span><span class="sxs-lookup"><span data-stu-id="c014d-125">Use PUT Raw data to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="c014d-126">其中的部屬是串流，即</span><span class="sxs-lookup"><span data-stu-id="c014d-126">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="c014d-127">非結構化，例如</span><span class="sxs-lookup"><span data-stu-id="c014d-127">unstructured, ex.</span></span> <span data-ttu-id="c014d-128">文字檔。</span><span class="sxs-lookup"><span data-stu-id="c014d-128">a text file.</span></span>  <span data-ttu-id="c014d-129">PUT 具有等冪性，因此即使出現多次也將產生相同的狀態，即</span><span class="sxs-lookup"><span data-stu-id="c014d-129">PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="c014d-130">x=5。</span><span class="sxs-lookup"><span data-stu-id="c014d-130">x=5.</span></span>  <span data-ttu-id="c014d-131">Put 應與指定資源的完整內容搭配使用。</span><span class="sxs-lookup"><span data-stu-id="c014d-131">Put should be used with the full content of the specified resource.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="CancelBuild” ReturnType="Raw(text/plain)" d:AllowedHttpMethods="PUT" d:EncodeParameterValues="true" d:BaseUri=” http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Cancel Build</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="c014d-132">範例：使用 "GET" 傳回 "Raw" 資料的 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="c014d-132">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="c014d-133">使用 GET Raw 資料傳回非結構化的部屬，即文字。</span><span class="sxs-lookup"><span data-stu-id="c014d-133">Use GET Raw data to return a subordinate that is unstructured, i.e. text.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="GetModelUsageFile" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="GET" d:BaseUri="https://cmla.cloudapp.net/api2/model/builder/build?buildId={buildId}&amp;apiVersion={apiVersion}">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Download A Models Usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Accept" d:Value="application/xml,application/xhtml+xml,text/html;" />
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="c014d-134">範例：「逐頁查看」所傳回資料的 FunctionImport</span><span class="sxs-lookup"><span data-stu-id="c014d-134">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="c014d-135">透過 GET 以符合 REST 限制的方式實作「逐頁查看」您的資料。</span><span class="sxs-lookup"><span data-stu-id="c014d-135">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="c014d-136">預設的分頁設為每頁 100 列的資料。</span><span class="sxs-lookup"><span data-stu-id="c014d-136">Default paging is set to 100 row per page of data.</span></span>

        <EntitySet Name=”CropEntitySet" EntityType="MyOffer.CropEntity" />
        <FunctionImport    Name="GetCropReport" EntitySet="CropEntitySet” ReturnType="Collection(MyOffer.CropEntity)" d:EmitSelfLink="false" d:EncodeParameterValues="true" d:Paging="SkipTake" d:MaxPageSize="100" d:BaseUri="http://api.mydata.org/Crop? report={report}&amp;series={series}&amp;start={$skip}&amp;size=100">
        <Parameter Name="report" Type="Int32" Mode="In" Nullable="false" d:SampleValues="4"  d:enum="1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19"  />
        <Parameter Name="series"    Type="String"    Mode="In" Nullable="false" d:SampleValues="FARM" />
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="text/xml;charset=UTF-8" />
        </d:Headers>
        <d:Namespaces>
        <d:Namespace d:Prefix="diffgr" d:Uri="urn:schemas-microsoft-com:xml-diffgram-v1" />
        </d:Namespaces>
        </FunctionImport>

## <a name="see-also"></a><span data-ttu-id="c014d-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c014d-137">See Also</span></span>
* <span data-ttu-id="c014d-138">如果您有興趣全面了解 OData 對應程序和用途，請閱讀 [資料服務 OData 對應](marketplace-publishing-data-service-creation-odata-mapping.md) 一文來檢閱定義、結構和指示。</span><span class="sxs-lookup"><span data-stu-id="c014d-138">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="c014d-139">如果您有興趣學習和了解特定節點及其參數，請閱讀 [資料服務 OData 對應節點](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) 一文，來了解定義和說明、範例，以及使用案例內容。</span><span class="sxs-lookup"><span data-stu-id="c014d-139">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="c014d-140">若要返回用於將資料服務發佈至 Azure Marketplace 的指定路徑，請閱讀 [資料服務發佈指南](marketplace-publishing-data-service-creation.md)一文。</span><span class="sxs-lookup"><span data-stu-id="c014d-140">To return to the prescribed path for publishing a Data Service to the Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

