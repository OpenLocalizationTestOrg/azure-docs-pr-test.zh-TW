---
title: "aaaGuide toocreating 資料服務的 hello Marketplace |Microsoft 文件"
description: "Toocreate、 認證和部署資料服務的方式的詳細的指示購買 hello Azure Marketplace 上。"
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
ms.openlocfilehash: 8917a43959834d15f70866297f98d24bb83e217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-mapping-an-existing-web-service-tooodata-through-csdls"></a>範例對應現有的 web 服務 tooOData 透過 CSDLs
> [!IMPORTANT]
> 目前我們已不再針對任何新的資料服務發行者進行上架。新的 Dataservice 將不會獲得核准以列出於清單上。 如果您有商務 una aplicación SaaS 希望 toopublish AppSource 上，您可以找到更多資訊[這裡](https://appsource.microsoft.com/partners)。 如果您的 IaaS 應用程式或開發人員服務您會像在 Azure Marketplace toopublish 中，您可以找到更多資訊[這裡](https://azure.microsoft.com/marketplace/programs/certified/)。
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a>範例：使用 "POST" 傳回 "Raw" 資料的 FunctionImport
使用 POST 原始資料 toocreate 新部屬，並傳回它的伺服器定義 URL(location) 或次級伺服器 hello hello tooupdate 部分定義 URL。  Hello 次級所在的資料流，也就是無結構，例如。 文字檔。  請注意，POST 若沒有位置則不具等冪性。

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

## <a name="example-functionimport-using-delete"></a>範例：使用 "DELETE" 的 FunctionImport
使用 DELETE tooremove 指定的 URI。

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

## <a name="example-functionimport-using-post"></a>範例：使用 "POST" 的 FunctionImport
使用 POST 原始資料 toocreate 新部屬，並傳回它的伺服器定義 URL(location) 或次級伺服器 hello hello tooupdate 部分定義 URL。  Hello 次級所在的結構。 請注意，POST 若沒有位置則不具等冪性。

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

## <a name="example-functionimport-using-put"></a>範例：使用 "PUT" 的 FunctionImport
使用 PUT toocreate 新次級或 tooupdate hello 整個次級伺服器上的定義的 URL。  PUT hello 次級是一種結構，其中是等冪，因此多個項目將導致 hello 相同狀態，也就是 x=5。  Put 應搭配 hello 的 hello 指定完整的內容資源。

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


## <a name="example-functionimport-for-raw-data-returned-using-put"></a>範例：使用 "PUT" 傳回 "Raw" 資料的 FunctionImport
使用將未經處理資料 toocreate 新次級或 tooupdate hello 整個次級伺服器上的定義的 URL。  Hello 次級所在的資料流，也就是無結構，例如。 文字檔。  PUT 為等冪，因此多個項目將導致 hello 相同狀態，也就是 x=5。  Put 應搭配 hello 的 hello 指定完整的內容資源。

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


## <a name="example-functionimport-for-raw-data-returned-using-get"></a>範例：使用 "GET" 傳回 "Raw" 資料的 FunctionImport
使用取得未經處理資料 tooreturn 從屬的非結構化，也就是文字。

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

## <a name="example-functionimport-for-paging-through-returned-data"></a>範例：「逐頁查看」所傳回資料的 FunctionImport
透過 GET 以符合 REST 限制的方式實作「逐頁查看」您的資料。  預設分頁設定 too100 資料列每個分頁的資料。

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

## <a name="see-also"></a>另請參閱
* 如果您有興趣了解 hello 整體 OData 對應程序及目的閱讀此文章[資料服務 OData 對應](marketplace-publishing-data-service-creation-odata-mapping.md)tooreview 定義、 結構和指示。
* 如果您有興趣在學習並了解 hello 特定節點和它們的參數，請閱讀此文章[資料服務 OData 對應節點](marketplace-publishing-data-service-creation-odata-mapping-nodes.md)的定義和說明、 範例和案例使用的內容。
* 規定路徑發行閱讀本文資料服務 toohello Azure Marketplace tooreturn toohello[資料服務的發行指導](marketplace-publishing-data-service-creation.md)。

