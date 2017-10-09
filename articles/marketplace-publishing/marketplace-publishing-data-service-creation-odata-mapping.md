---
title: "aaaGuide toocreating 資料服務的 hello Marketplace |Microsoft 文件"
description: "Toocreate、 認證和部署資料服務的方式的詳細的指示購買 hello Azure Marketplace 上。"
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
ms.openlocfilehash: deb2e52dd03f5beb2ad6a927bd2d03e47d20b691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a>對應現有 web 服務 tooOData 透過 CSDL
> [!IMPORTANT]
> 目前我們已不再針對任何新的資料服務發行者進行上架。新的 Dataservice 將不會獲得核准以列出於清單上。 如果您有商務 una aplicación SaaS 希望 toopublish AppSource 上，您可以找到更多資訊[這裡](https://appsource.microsoft.com/partners)。 如果您的 IaaS 應用程式或開發人員服務您會像在 Azure Marketplace toopublish 中，您可以找到更多資訊[這裡](https://azure.microsoft.com/marketplace/programs/certified/)。
> 
> 

這篇文章概要說明如何 toouse CSDL toomap 現有服務 tooan OData 相容的服務。 它會說明如何 toocreate hello 對應文件 (CSDL) 將轉換從透過服務呼叫和 hello hello 用戶端 hello 輸入的要求輸出 （資料） 回 toohello 用戶端透過 OData 相容摘要。 Microsoft Azure Marketplace 使用 hello OData 通訊協定公開服務 toohello 使用者。 內容提供者 (資料擁有者) 所公開的服務會以各種不同形式 (例如 REST、 SOAP 等) 來公開。

## <a name="what-is-a-csdl-and-its-structure"></a>什麼是 CSDL 及其結構？
在 CSDL （概念結構定義語言） 是定義如何 toodescribe web 服務或資料庫服務在一般 XML 用語 toohello Azure Marketplace 的規格。

簡單概觀 hello**要求流程：**

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

hello**資料流程**處於 hello 相反的方向：

  `Client <- Azure Marketplace <- Content Provider’s WebService`

**圖 1**圖表如何在用戶端會從取得資料內容的提供者 （服務） 進行 hello Azure Marketplace。  hello CSDL 由 hello 對應/轉換元件 toohandle hello 要求和 hello 內容提供者的服務和 hello 要求用戶端之間傳遞的資料。

*圖 1： 從要求用戶端透過 Azure Marketplace 的 toocontent 提供者的詳細的流程*

  ![繪圖](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

如需有關 Atom、 Atom Pub 和 hello OData 通訊協定的 hello Azure Marketplace 延伸模組建置時的背景，請檢閱： [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)

連結 corresponding 摘錄： *"hello hello 開放式資料通訊協定 (以下參照 tooas OData) 的目的是樣式 CRUD 作業 （建立、 讀取、 更新和刪除） 對公開為資料服務資源的 tooprovide REST 式通訊協定。「資料服務」是一個端點，其中含有公開自一或多個「集合」的資料，每個集合均包含零到多個「項目」，這些項目是由具類型的具名值組所組成。OData 會發佈在 OASIS （hello 先進的結構化資訊標準組織） 標準的 microsoft 好讓任何人都想 toocan 建置伺服器、 用戶端或權利金或限制沒有工具 」。*

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a>具有 toobe hello CSDL 所定義的三個重要部分是：
* hello**端點**hello 服務提供者的 hello Web 位址 (URI) 的 hello 服務
* hello**資料參數**hello hello 參數傳送 toohello 內容提供者的服務，關閉 toohello 資料型別定義為輸入 toohello 服務提供者正在傳遞。
* **結構描述**傳回 toohello 要求服務 hello 資料結構描述 hello hello 內容提供者的服務所傳送的 hello 資料，包括容器、 集合/資料表、 變數/資料行和資料類型。

hello 下列圖表顯示從何處 hello 用戶端輸入 hello OData 陳述式 （呼叫 toohello 內容提供者的 web 服務） toogetting hello 結果/資料回 hello 流程的概觀。

  ![繪圖](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a>步驟：
1. 用戶端傳送要求，透過服務呼叫完成，但在 XML toohello Azure Marketplace 中定義的輸入參數
2. CSDL 是使用的 toovalidate hello 服務呼叫。
   * hello 格式化服務呼叫然後 toohello 內容提供者服務所傳送 hello Azure Marketplace
3. hello Webservice 執行並 preforms hello 動作的 hello Http 動詞命令 (亦即 GET) tooAzure Marketplace 其中 hello 要求資料 （如果有的話） 在 XML 格式 toohello 用戶端的公開會傳回 hello 資料使用的 hello hello CSDL 中定義的對應。
4. hello 用戶端會傳送 hello 資料 （如果有的話） 以 XML 或 JSON 格式

## <a name="definitions"></a>定義
### <a name="odata-atom-pub"></a>OData ATOM Pub
其中每個項目代表結果的一個資料列延伸 toohello ATOM pub 設定。 hello hello 項目的內容組件是 hello 資料列 – 增強的 toocontain hello 值做為索引鍵值組。 您可以在此處找到詳細資訊： [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)

### <a name="csdl---conceptual-schema-definition-language"></a>CSDL - 概念結構定義語言
允許定義透過資料庫公開的函式 (SPROC) 和實體。 您可以在此處找到詳細資訊： [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)  

> [!TIP]
> 按一下 hello**其他版本**下拉式清單中選取版本，如果您沒有看見 hello 發行項。
> 
> 

### <a name="edm---entry-data-model"></a>EDM - 項目資料模型
* 概觀︰[http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* 預覽︰[http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* 資料類型：[http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

hello 下列範例示範 hello 詳細左的 tooRight 流程其中 hello 用戶端輸入 hello OData 陳述式 （呼叫 toohello 內容提供者的 web 服務） toogetting hello 結果/資料回：

  ![繪圖](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a>CSDL 基本概念
在 CSDL （概念結構定義語言） 是定義如何 toodescribe web 服務或資料庫服務在一般 XML 用語 toohello Azure Marketplace 的規格。 CSDL 描述重要的 hello pieces，**讓 hello 從 hello Azure Marketplace 的資料來源 toohello 傳遞的資料。** 此處所述 hello 主要部分：

* 說明所有對外公開使用之函式 (FunctionImport 節點) 的介面資訊
* 適用於所有訊息要求 (輸入) 和訊息回應 (輸出) (EntityContainer/EntitySet/EntityType 節點) 的資料類型資訊
* 繫結 hello 傳輸通訊協定 toobe 資訊使用 （標頭節點）
* 指定服務 （BaseURI 屬性） 以找出 hello 的位址資訊。

簡而言之，hello CSDL 表示平台和語言無關之間的合約 hello 服務要求者和 hello 服務提供者。 使用 hello CSDL，用戶端可以找到 web 服務/資料庫服務，並叫用任何其公開可用的函式。

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a>關於 CSDL tooa 資料庫或集合
**hello CSDL 規格**

CSDL 是說明 Web 服務的 XML 文法。 hello 規格本身就會劃分為 4 個主要元素： EntitySet、 FunctionImport;命名空間和 EntityType。

toomake 這個抽象概念更容易 toounderstand 讓 CSDL tooa 資料表關聯。

請記住；

  CSDL 表示平台和語言無關之間的合約 hello**服務要求者**和 hello**服務提供者**。 使用 CSDL，**用戶端**可以找到 **Web 服務/資料庫服務**，並叫用任何其公開可用的**函式**。

資料服務 hello CSDL 的四個部分可視為資料庫、 資料表、 資料行及預存程序。

針對資料服務，可使用如下方式來關聯這些項目：

* EntityContainer  ~=  資料庫
* EntitySet  ~=  資料表
* EntityType  ~=  資料行
* FunctionImport  ~=  預存程序

**允許的 HTTP 動詞命令**

* 取得 – 從 hello db （傳回的集合） 的傳回值
* POST – 使用 toopass tooand 選擇性傳回的資料值 hello db （建立新的項目在 hello 集合中，傳回的識別碼 URI）
* 刪除 – 刪除資料，從 hello DB （刪除集合）
* PUT – 更新資料到 DB (取代集合或建立一個集合)

## <a name="metadatamapping-document"></a>中繼資料/對應文件
hello/對應的中繼資料文件是使用的 toomap 內容提供者的現有 web 服務，使它可以 hello Azure Marketplace 系統公開為 OData web 服務。 它為 CSDL 為基礎，實作幾個擴充功能 tooCSDL tooaccommodate hello 需求的 REST 型 web 服務透過 Azure Marketplace 公開。 hello 延伸模組位於 hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04)命名空間。

Hello CSDL 的範例如下: （複製與貼上下列 XML 編輯器中的範例 CSDL hello 和變更 toomatch 您的服務。  貼上到 CSDL 對應 DataService 索引標籤下 hello 中建立您的服務時[Azure Marketplace 發佈入口網站](https://publish.windowsazure.com))。

**詞彙：** Relating hello CSDL 條款 toohello[發佈入口網站](https://publish.windowsazure.com)UI (PPUI) 條款。

* 提供"Title"hello PPUI 中的相關 tooMyWebOffer
* 在 hello PPUI MyCompany 太相關**發行者顯示名稱**在 hello [Microsoft 開發人員中心](http://dev.windows.com/registration?accountprogram=azure)UI
* 您的 API 相關 tooa Web 或資料服務 （在 hello PPUI 計畫）

**階層：** 公司 (內容提供者) 擁有具有方案 (即服務) 的優惠，可利用 API 來排列。

### <a name="webservice-csdl-example"></a>WebService CSDL 範例
連接所公開的 web 應用程式端點 （例如 C# 應用程式） 的 tooa 服務

        <?xml version="1.0" encoding="utf-8"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all hello web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition near hello bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is hello entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines hello service call, replace & with hello encode value (&amp;).
        In hello input name value pairs {param} represents passed in value.
        Or hello value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows hello CSDL toospecifically specify hello verb of hello service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes hello parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how hello web service call is exposed toomarketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, hello {...} point toohello parameters defined below.
        Marketplace will read hello parameters from this URITemplate and fill hello values into hello corresponding parameters of hello BaseUri or RequestBody (below) during calls tooyour service.  
        It is okay for @d:BaseUri tooinclude information only for Marketplace consumption, it will not be exposed tooend users. i.e. hello hardcoded AccountKey in hello above BaseURI does not show up in hello client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of hello RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders tooinsert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how toopass userid and password via hello header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed tooend users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with hello value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited tooappearing as hello value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used toospecify values tooinsert into hello ATOM feed returned toohello end user.  You can specify hello element toocontain a fixed message by providing a value for hello element (this is hello default value).  @d:Map is an XPath expression that points into hello response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay tooalso add a d:Map attribute toooverride this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of hello web service call:
        @Name should match exactly (case sensitive) hello {…} placeholders in hello @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether hello parameter is required.
        @d:Regex - optional, attribute toodescribe hello string, limiting unwanted input at hello entry of hello system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in hello Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating hello service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in hello order listed.
        @d:Match is an Xpath query on hello service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is hello error code tooreturn if an response matches hello error.
        @d:errorMessage is hello user friendly message tooreturn when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect toohello service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- hello EntityContainer defines hello output data schema -->
        </EntityContainer>
        <!-- hello EntityType @d:Map defines hello repeating node (an XPath query) in hello response (output data schema). -->
        <!-- If these nodes are outside a namespace, add hello prefix in hello xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in hello ATOM feed, so comply with hello XML element naming restrictions (no spaces or other illegal characters).
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query toopoint at hello location tooextract hello content from your services response.
        hello "." is relative toohello repeating node in hello EntityType @d:Map Xpath expression.
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
> Hello 文件中檢視更多的 CSDL Web 服務範例[範例對應現有的 web 服務 tooOData 透過 CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)
> 
> 

### <a name="dataservice-csdl-example"></a>DataService CSDL 範例
會公開 (expose) 的資料庫資料表或檢視時的端點，下列範例示範兩個應用程式開發介面的基底資料型應用程式開發介面 （可以使用檢視，而不是資料表） 的 CSDL 的 tooa 服務的連接。

        <?xml version="1.0"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all hello data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of hello EntitySet as a Service
        @Name is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); hello table (or view) and columns toobe returned by hello data service.)
            Map is hello schema.tabel or schema.view
            dals.TableName is hello table Name
            Name is hello name identifier for hello EntityType and hello Name of hello service exposed toohello client via hello UI.
            dals:IsExposed determines if hello table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is hello schema name of hello table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines hello column properties and hello output of hello service.
            dals:ColumnName is hello name of hello column in hello table /view.
            Type is hello emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is hello maximum length of hello output value
            Name is hello name of hello Property and is exposed toohello client facing UI
            dals:IsReturned is hello Boolean that determines if hello Service exposes this value toohello client.
            IsQueryable is hello Boolean that determines if hello column can be used in a database query
            (For data Services: tooimprove Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is hello numerical position x in hello table or hello View, where x is from 1 toohello number of columns in hello table.
            dals:DatabaseDataType is hello data type of hello column in hello database, i.e. SQL data type dals:IsPrimaryKey indicates if hello column is hello Primary key in hello table/view.  (hello columns marked ISPrimaryKey are used in hello Order by clause when returning data.)
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

## <a name="see-also"></a>另請參閱
* 如果您有興趣在學習並了解 hello 特定節點和它們的參數，請閱讀此文章[資料服務 OData 對應節點](marketplace-publishing-data-service-creation-odata-mapping-nodes.md)的定義和說明、 範例和案例使用的內容。
* 如果您有興趣檢視範例，請閱讀這篇文章[資料服務 OData 對應範例](marketplace-publishing-data-service-creation-odata-mapping-examples.md)toosee 範例程式碼，並了解程式碼語法和內容。
* 規定路徑發行閱讀本文資料服務 toohello Azure Marketplace tooreturn toohello[資料服務的發行指導](marketplace-publishing-data-service-creation.md)。

