---
title: "aaaUpgrading toohello Azure 搜尋.NET SDK 1.1 版 |Microsoft 文件"
description: "升級 toohello Azure 搜尋.NET SDK 1.1 版"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a><span data-ttu-id="72f9f-103">升級 toohello Azure 搜尋.NET SDK 版本 3</span><span class="sxs-lookup"><span data-stu-id="72f9f-103">Upgrading toohello Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="72f9f-104">如果您使用版本 2.0 preview 或舊版的 hello [Azure 搜尋.NET SDK](https://aka.ms/search-sdk)，本文將協助您升級您的應用程式 toouse 第 3 版。</span><span class="sxs-lookup"><span data-stu-id="72f9f-104">If you're using version 2.0-preview or older of hello [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application toouse version 3.</span></span>

<span data-ttu-id="72f9f-105">多個一般逐步解說中的 hello SDK 包括範例，請參閱[toouse Azure 搜尋.NET 應用程式如何](search-howto-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="72f9f-105">For a more general walkthrough of hello SDK including examples, see [How toouse Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="72f9f-106">第 3 版的 hello Azure 搜尋.NET SDK 包含從舊版的某些變更。</span><span class="sxs-lookup"><span data-stu-id="72f9f-106">Version 3 of hello Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="72f9f-107">這些變更大部分是次要變更，所以變更程式碼應該只需要最少的工作。</span><span class="sxs-lookup"><span data-stu-id="72f9f-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="72f9f-108">請參閱[步驟 tooupgrade](#UpgradeSteps)如需有關指示 toochange 您程式碼 toouse hello 新的 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="72f9f-108">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="72f9f-109">如果您使用版本 1.0.2-preview 或更舊版本，您應該先升級 tooversion 1.1，然後再升級 tooversion 3。</span><span class="sxs-lookup"><span data-stu-id="72f9f-109">If you're using version 1.0.2-preview or older, you should upgrade tooversion 1.1 first, and then upgrade tooversion 3.</span></span> <span data-ttu-id="72f9f-110">請參閱[附錄： 步驟 tooupgrade tooversion 1.1](#UpgradeStepsV1)如需相關指示。</span><span class="sxs-lookup"><span data-stu-id="72f9f-110">See [Appendix: Steps tooupgrade tooversion 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="72f9f-111">您的 Azure 搜尋服務執行個體支援多個 REST API 版本，包括 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="72f9f-111">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="72f9f-112">您可以繼續 toouse 版本時，它不會再 hello 最新的其中一個，但我們建議您移轉您的程式碼 toouse hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="72f9f-112">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span> <span data-ttu-id="72f9f-113">當使用 hello REST API，您必須指定 hello API 版本 hello api-version 參數透過每個要求中。</span><span class="sxs-lookup"><span data-stu-id="72f9f-113">When using hello REST API, you must specify hello API version in every request via hello api-version parameter.</span></span> <span data-ttu-id="72f9f-114">當使用 hello.NET SDK，hello 您所使用的 SDK hello 版本會決定 hello 對應 hello REST API 的版本。</span><span class="sxs-lookup"><span data-stu-id="72f9f-114">When using hello .NET SDK, hello version of hello SDK you’re using determines hello corresponding version of hello REST API.</span></span> <span data-ttu-id="72f9f-115">如果您使用較舊的 SDK，您可以繼續 toorun 未變更該程式碼即使 hello 服務升級的 toosupport 較新的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="72f9f-115">If you are using an older SDK, you can continue toorun that code with no changes even if hello service is upgraded toosupport a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="72f9f-116">版本 3 的新功能</span><span class="sxs-lookup"><span data-stu-id="72f9f-116">What's new in version 3</span></span>
<span data-ttu-id="72f9f-117">Hello Azure 搜尋.NET SDK 目標 hello 最新第 3 版上市 hello Azure 搜尋 REST API，特別是 2016年-09-01 版本。</span><span class="sxs-lookup"><span data-stu-id="72f9f-117">Version 3 of hello Azure Search .NET SDK targets hello latest generally available version of hello Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="72f9f-118">這使得可能 toouse 許多新的 Azure 搜尋.NET 應用程式，包括 hello 下列功能：</span><span class="sxs-lookup"><span data-stu-id="72f9f-118">This makes it possible toouse many new features of Azure Search from a .NET application, including hello following:</span></span>

* [<span data-ttu-id="72f9f-119">自訂分析器</span><span class="sxs-lookup"><span data-stu-id="72f9f-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="72f9f-120">[Azure Blob 儲存體](search-howto-indexing-azure-blob-storage.md)和 [Azure 表格儲存體](search-howto-indexing-azure-tables.md)索引子支援</span><span class="sxs-lookup"><span data-stu-id="72f9f-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="72f9f-121">透過 [欄位對應](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="72f9f-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="72f9f-122">Etag 支援 tooenable 安全並行更新的索引定義、 索引子和資料來源</span><span class="sxs-lookup"><span data-stu-id="72f9f-122">ETags support tooenable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="72f9f-123">支援以宣告方式建立索引欄位定義，而將模型類別，並使用新的 hello`FieldBuilder`類別。</span><span class="sxs-lookup"><span data-stu-id="72f9f-123">Support for building index field definitions declaratively by decorating your model class and using hello new `FieldBuilder` class.</span></span>
* <span data-ttu-id="72f9f-124">對 .NET Core 和 .NET Portable Profile 111 的支援</span><span class="sxs-lookup"><span data-stu-id="72f9f-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="72f9f-125">步驟 tooupgrade</span><span class="sxs-lookup"><span data-stu-id="72f9f-125">Steps tooupgrade</span></span>
<span data-ttu-id="72f9f-126">首先，更新您 NuGet 參考`Microsoft.Azure.Search`使用任一 hello NuGet 封裝管理員主控台或藉由以滑鼠右鍵按一下您的專案參考和 Visual Studio 中選取 [管理 NuGet 封裝...]。</span><span class="sxs-lookup"><span data-stu-id="72f9f-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="72f9f-127">一旦 hello 新的封裝和其相依性，已下載 NuGet，請重建您的專案。</span><span class="sxs-lookup"><span data-stu-id="72f9f-127">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="72f9f-128">根據您的程式碼結構情況，它可能會順利重新建置。</span><span class="sxs-lookup"><span data-stu-id="72f9f-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="72f9f-129">如果是這樣，您已準備好 toogo ！</span><span class="sxs-lookup"><span data-stu-id="72f9f-129">If so, you're ready toogo!</span></span>

<span data-ttu-id="72f9f-130">如果您的組建失敗，您應該會看到建置錯誤 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="72f9f-130">If your build fails, you should see a build error like hello following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="72f9f-131">hello 下一個步驟是 toofix 這個組建錯誤。</span><span class="sxs-lookup"><span data-stu-id="72f9f-131">hello next step is toofix this build error.</span></span> <span data-ttu-id="72f9f-132">請參閱[第 3 版中的重大變更](#ListOfChanges)如什麼情況會讓 hello 錯誤的詳細資訊及如何 toofix 它。</span><span class="sxs-lookup"><span data-stu-id="72f9f-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes hello error and how toofix it.</span></span>

<span data-ttu-id="72f9f-133">您可能會看到其他建置警告相關 tooobsolete 方法或屬性。</span><span class="sxs-lookup"><span data-stu-id="72f9f-133">You may see additional build warnings related tooobsolete methods or properties.</span></span> <span data-ttu-id="72f9f-134">hello 警告將會包含在何種 toouse 改為 hello 的已被取代功能的指示。</span><span class="sxs-lookup"><span data-stu-id="72f9f-134">hello warnings will include instructions on what toouse instead of hello deprecated feature.</span></span> <span data-ttu-id="72f9f-135">例如，如果您的應用程式使用 hello`IndexingParameters.Base64EncodeKeys`屬性，您應該取得說明的警告`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="72f9f-135">For example, if your application uses hello `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="72f9f-136">一旦您已修正任何建置錯誤，您可以變更 tooyour 應用程式 tootake 利用新的功能視。</span><span class="sxs-lookup"><span data-stu-id="72f9f-136">Once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span> <span data-ttu-id="72f9f-137">Hello SDK 中的新功能的詳細[第 3 版的新](#WhatsNew)。</span><span class="sxs-lookup"><span data-stu-id="72f9f-137">New features in hello SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="72f9f-138">版本 3 的重大變更</span><span class="sxs-lookup"><span data-stu-id="72f9f-138">Breaking changes in version 3</span></span>
<span data-ttu-id="72f9f-139">那里少量第 3 版中的重大變更，可能需要的程式碼變更此外 toorebuilding 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="72f9f-139">There a small number of breaking changes in version 3 that may require code changes in addition toorebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="72f9f-140">Indexes.GetClient 傳回類型</span><span class="sxs-lookup"><span data-stu-id="72f9f-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="72f9f-141">hello`Indexes.GetClient`方法有新的傳回型別。</span><span class="sxs-lookup"><span data-stu-id="72f9f-141">hello `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="72f9f-142">以往它會傳回`SearchIndexClient`，但這已經過`ISearchIndexClient`版本 2.0-預覽，以及變更會有透過 tooversion 3。</span><span class="sxs-lookup"><span data-stu-id="72f9f-142">Previously, it returned `SearchIndexClient`, but this was changed too`ISearchIndexClient` in version 2.0-preview, and that change carries over tooversion 3.</span></span> <span data-ttu-id="72f9f-143">這是 toosupport 客戶想 toomock hello`GetClient`方法所傳回的模擬實作的單元測試`ISearchIndexClient`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-143">This is toosupport customers that wish toomock hello `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="72f9f-144">範例</span><span class="sxs-lookup"><span data-stu-id="72f9f-144">Example</span></span>
<span data-ttu-id="72f9f-145">如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="72f9f-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="72f9f-146">您可以將它變更 toothis toofix 任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="72f9f-146">You can change it toothis toofix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a><span data-ttu-id="72f9f-147">AnalyzerName、 資料類型和其他人已不再隱含地轉換 toostrings</span><span class="sxs-lookup"><span data-stu-id="72f9f-147">AnalyzerName, DataType, and others are no longer implicitly convertible toostrings</span></span>
<span data-ttu-id="72f9f-148">Hello 衍生自的 Azure 搜尋.NET SDK 中的許多類型`ExtensibleEnum`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-148">There are many types in hello Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="72f9f-149">這些型別先前所有隱含地轉換 tootype `string`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-149">Previously these types were all implicitly convertible tootype `string`.</span></span> <span data-ttu-id="72f9f-150">不過，在 hello 發現 bug`Object.Equals`實作這些類別，以及修正 hello bug 所需停用這項隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="72f9f-150">However, a bug was discovered in hello `Object.Equals` implementation for these classes, and fixing hello bug required disabling this implicit conversion.</span></span> <span data-ttu-id="72f9f-151">明確轉換太`string`仍然允許。</span><span class="sxs-lookup"><span data-stu-id="72f9f-151">Explicit conversion too`string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="72f9f-152">範例</span><span class="sxs-lookup"><span data-stu-id="72f9f-152">Example</span></span>
<span data-ttu-id="72f9f-153">如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="72f9f-153">If your code looks like this:</span></span>

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

<span data-ttu-id="72f9f-154">您可以將它變更 toothis toofix 任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="72f9f-154">You can change it toothis toofix any build errors:</span></span>

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a><span data-ttu-id="72f9f-155">移除過時的成員</span><span class="sxs-lookup"><span data-stu-id="72f9f-155">Removed obsolete members</span></span>

<span data-ttu-id="72f9f-156">您可能會看到建置錯誤相關的 toomethods 或內容所標示為版本 2.0 preview 中的過時並接著在第 3 版中移除。</span><span class="sxs-lookup"><span data-stu-id="72f9f-156">You may see build errors related toomethods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="72f9f-157">如果您遇到此類錯誤時，以下是如何 tooresolve 它們：</span><span class="sxs-lookup"><span data-stu-id="72f9f-157">If you encounter such errors, here is how tooresolve them:</span></span>

- <span data-ttu-id="72f9f-158">如果您使用這個建構函式︰`ScoringParameter(string name, string value)`，請改用︰`ScoringParameter(string name, IEnumerable<string> values)`</span><span class="sxs-lookup"><span data-stu-id="72f9f-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="72f9f-159">如果您使用 hello`ScoringParameter.Value`屬性，使用 hello`ScoringParameter.Values`屬性或 hello`ToString`方法改為。</span><span class="sxs-lookup"><span data-stu-id="72f9f-159">If you were using hello `ScoringParameter.Value` property, use hello `ScoringParameter.Values` property or hello `ToString` method instead.</span></span>
- <span data-ttu-id="72f9f-160">如果您使用 hello`SearchRequestOptions.RequestId`屬性，使用 hello`ClientRequestId`屬性改為。</span><span class="sxs-lookup"><span data-stu-id="72f9f-160">If you were using hello `SearchRequestOptions.RequestId` property, use hello `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="72f9f-161">已移除的預覽功能</span><span class="sxs-lookup"><span data-stu-id="72f9f-161">Removed preview features</span></span>

<span data-ttu-id="72f9f-162">如果您要從版本 2.0 preview tooversion 3 升級，請注意，JSON 和 CSV 剖析 Blob 的索引子的支援已經已移除，因為這些功能仍處於 preview。</span><span class="sxs-lookup"><span data-stu-id="72f9f-162">If you are upgrading from version 2.0-preview tooversion 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="72f9f-163">具體來說，hello 遵循方法 hello`IndexingParametersExtensions`類別已被移除：</span><span class="sxs-lookup"><span data-stu-id="72f9f-163">Specifically, hello following methods of hello `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="72f9f-164">如果您的應用程式具有的硬式相依於這些功能，就能 tooupgrade tooversion 3 的 hello Azure 搜尋.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="72f9f-164">If your application has a hard dependency on these features, you will not be able tooupgrade tooversion 3 of hello Azure Search .NET SDK.</span></span> <span data-ttu-id="72f9f-165">您可以繼續 toouse 版本 2.0 preview。</span><span class="sxs-lookup"><span data-stu-id="72f9f-165">You can continue toouse version 2.0-preview.</span></span> <span data-ttu-id="72f9f-166">但請記住，**我們不建議在實際執行應用程式中使用預覽 SDK**。</span><span class="sxs-lookup"><span data-stu-id="72f9f-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="72f9f-167">預覽功能僅供評估，可能會變更。</span><span class="sxs-lookup"><span data-stu-id="72f9f-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="72f9f-168">結論</span><span class="sxs-lookup"><span data-stu-id="72f9f-168">Conclusion</span></span>
<span data-ttu-id="72f9f-169">如果您需要更多詳細資料上使用 hello Azure 搜尋.NET SDK，請參閱我們最近更新[How-to](search-howto-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="72f9f-169">If you need more details on using hello Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="72f9f-170">我們歡迎您的意見反應 hello SDK 上。</span><span class="sxs-lookup"><span data-stu-id="72f9f-170">We welcome your feedback on hello SDK.</span></span> <span data-ttu-id="72f9f-171">如果您遇到問題，則可以免費 tooask 我們 hello 的說明[Azure 搜尋 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch)。</span><span class="sxs-lookup"><span data-stu-id="72f9f-171">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="72f9f-172">如果您發現 bug 時，您可以在 hello 提出問題[Azure.NET SDK GitHub 儲存機制](https://github.com/Azure/azure-sdk-for-net/issues)。</span><span class="sxs-lookup"><span data-stu-id="72f9f-172">If you find a bug, you can file an issue in hello [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="72f9f-173">請確定 tooprefix 您問題的標題與 「 搜尋 SDK:"。</span><span class="sxs-lookup"><span data-stu-id="72f9f-173">Make sure tooprefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="72f9f-174">感謝您使用 Azure 搜尋服務！</span><span class="sxs-lookup"><span data-stu-id="72f9f-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a><span data-ttu-id="72f9f-175">附錄： 步驟 tooupgrade tooversion 1.1</span><span class="sxs-lookup"><span data-stu-id="72f9f-175">Appendix: Steps tooupgrade tooversion 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="72f9f-176">本節適用於僅 toousers hello Azure 搜尋.NET SDK 版本 1.0.2-preview 和較舊。</span><span class="sxs-lookup"><span data-stu-id="72f9f-176">This section applies only toousers of hello Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="72f9f-177">首先，更新您 NuGet 參考`Microsoft.Azure.Search`使用任一 hello NuGet 封裝管理員主控台或藉由以滑鼠右鍵按一下您的專案參考和 Visual Studio 中選取 [管理 NuGet 封裝...]。</span><span class="sxs-lookup"><span data-stu-id="72f9f-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="72f9f-178">一旦 hello 新的封裝和其相依性，已下載 NuGet，請重建您的專案。</span><span class="sxs-lookup"><span data-stu-id="72f9f-178">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="72f9f-179">如果您先前使用版本 1.0.0-preview、 1.0.1-preview 或 1.0.2-preview，hello 組建應該成功，而且您已準備好 toogo ！</span><span class="sxs-lookup"><span data-stu-id="72f9f-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, hello build should succeed and you're ready toogo!</span></span>

<span data-ttu-id="72f9f-180">如果您先前使用版本 0.13.0-preview 或更舊版本，您應該會看到建置錯誤 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="72f9f-180">If you were previously using version 0.13.0-preview or older, you should see build errors like hello following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="72f9f-181">hello 下一個步驟是一個 toofix hello 建置錯誤。</span><span class="sxs-lookup"><span data-stu-id="72f9f-181">hello next step is toofix hello build errors one by one.</span></span> <span data-ttu-id="72f9f-182">大部分都需要變更 hello SDK 中已重新命名某些類別和方法名稱。</span><span class="sxs-lookup"><span data-stu-id="72f9f-182">Most will require changing some class and method names that have been renamed in hello SDK.</span></span> <span data-ttu-id="72f9f-183">[版本 1.1 的重大變更清單](#ListOfChangesV1) 一節包含這些名稱變更的清單。</span><span class="sxs-lookup"><span data-stu-id="72f9f-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="72f9f-184">如果您正在使用自訂類別 toomodel 文件中，且這些類別有不可為 null 的基本類型的屬性 (例如，`int`或`bool`C# 中)，其中您應該注意的 hello SDK hello 1.1 版本中沒有 bug 修正。</span><span class="sxs-lookup"><span data-stu-id="72f9f-184">If you're using custom classes toomodel your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in hello 1.1 version of hello SDK of which you should be aware.</span></span> <span data-ttu-id="72f9f-185">請參閱 [版本 1.1 的錯誤修正](#BugFixesV1) 一節以取得更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="72f9f-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="72f9f-186">最後，一旦您已修正任何建置錯誤，您可以變更 tooyour 應用程式 tootake 利用新的功能視。</span><span class="sxs-lookup"><span data-stu-id="72f9f-186">Finally, once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="72f9f-187">版本 1.1 的重大變更清單</span><span class="sxs-lookup"><span data-stu-id="72f9f-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="72f9f-188">hello 下列清單會依據排序 hello 可能性 hello 項變更會影響應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="72f9f-188">hello following list is ordered by hello likelihood that hello change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="72f9f-189">IndexBatch 和 IndexAction 變更</span><span class="sxs-lookup"><span data-stu-id="72f9f-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="72f9f-190">`IndexBatch.Create`已重新命名過`IndexBatch.New`且不再具有`params`引數。</span><span class="sxs-lookup"><span data-stu-id="72f9f-190">`IndexBatch.Create` has been renamed too`IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="72f9f-191">您可以針對混合不同類型動作 (合併、刪除等等) 的批次使用 `IndexBatch.New` 。</span><span class="sxs-lookup"><span data-stu-id="72f9f-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="72f9f-192">此外，還有新的靜態方法，建立批次的其中所有都 hello 動作是都 hello 相同： `Delete`， `Merge`， `MergeOrUpload`，和`Upload`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-192">In addition, there are new static methods for creating batches where all hello actions are hello same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="72f9f-193">`IndexAction` 不再具有公用建構函式且其屬性現在固定不變。</span><span class="sxs-lookup"><span data-stu-id="72f9f-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="72f9f-194">您應該用於不同用途建立動作 hello 新的靜態方法： `Delete`， `Merge`， `MergeOrUpload`，和`Upload`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-194">You should use hello new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="72f9f-195">`IndexAction.Create` 已移除。</span><span class="sxs-lookup"><span data-stu-id="72f9f-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="72f9f-196">如果您使用可接受的文件 hello 多載時，請確定 toouse`Upload`改為。</span><span class="sxs-lookup"><span data-stu-id="72f9f-196">If you used hello overload that takes only a document, make sure toouse `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="72f9f-197">範例</span><span class="sxs-lookup"><span data-stu-id="72f9f-197">Example</span></span>
<span data-ttu-id="72f9f-198">如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="72f9f-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="72f9f-199">您可以將它變更 toothis toofix 任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="72f9f-199">You can change it toothis toofix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="72f9f-200">如果您想，您可以進一步加以簡化 toothis:</span><span class="sxs-lookup"><span data-stu-id="72f9f-200">If you want, you can further simplify it toothis:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="72f9f-201">IndexBatchException 變更</span><span class="sxs-lookup"><span data-stu-id="72f9f-201">IndexBatchException changes</span></span>
<span data-ttu-id="72f9f-202">hello`IndexBatchException.IndexResponse`屬性已重新命名過`IndexingResults`，且其類型為現在`IList<IndexingResult>`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-202">hello `IndexBatchException.IndexResponse` property has been renamed too`IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="72f9f-203">範例</span><span class="sxs-lookup"><span data-stu-id="72f9f-203">Example</span></span>
<span data-ttu-id="72f9f-204">如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="72f9f-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="72f9f-205">您可以將它變更 toothis toofix 任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="72f9f-205">You can change it toothis toofix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="72f9f-206">作業方法變更</span><span class="sxs-lookup"><span data-stu-id="72f9f-206">Operation method changes</span></span>
<span data-ttu-id="72f9f-207">同步和非同步呼叫端，hello Azure 搜尋.NET SDK 中的每項作業會公開為一組方法多載。</span><span class="sxs-lookup"><span data-stu-id="72f9f-207">Each operation in hello Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="72f9f-208">hello 簽章與建構的這些方法多載版本中已經變更 1.1。</span><span class="sxs-lookup"><span data-stu-id="72f9f-208">hello signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="72f9f-209">例如，hello hello SDK 的舊版本中的 < 取得索引統計資料 」 作業會公開這些簽章：</span><span class="sxs-lookup"><span data-stu-id="72f9f-209">For example, hello "Get Index Statistics" operation in older versions of hello SDK exposed these signatures:</span></span>

<span data-ttu-id="72f9f-210">在 `IIndexOperations`中：</span><span class="sxs-lookup"><span data-stu-id="72f9f-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="72f9f-211">在 `IndexOperationsExtensions`中：</span><span class="sxs-lookup"><span data-stu-id="72f9f-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="72f9f-212">hello 方法簽章的 hello 相同的作業在 1.1 版看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="72f9f-212">hello method signatures for hello same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="72f9f-213">在 `IIndexesOperations`中：</span><span class="sxs-lookup"><span data-stu-id="72f9f-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="72f9f-214">在 `IndexesOperationsExtensions`中：</span><span class="sxs-lookup"><span data-stu-id="72f9f-214">In `IndexesOperationsExtensions`:</span></span>

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

<span data-ttu-id="72f9f-215">從 1.1 版開始，hello Azure 搜尋.NET SDK 會將組織作業方法以不同的方式：</span><span class="sxs-lookup"><span data-stu-id="72f9f-215">Starting with version 1.1, hello Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="72f9f-216">選擇性參數現在模型化為預設參數，而不是其他方法多載。</span><span class="sxs-lookup"><span data-stu-id="72f9f-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="72f9f-217">這有時會大幅減少 hello 方法多載，數目。</span><span class="sxs-lookup"><span data-stu-id="72f9f-217">This reduces hello number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="72f9f-218">hello 擴充方法現在會隱藏許多 hello 多餘的詳細資料的 HTTP hello 呼叫端。</span><span class="sxs-lookup"><span data-stu-id="72f9f-218">hello extension methods now hide a lot of hello extraneous details of HTTP from hello caller.</span></span> <span data-ttu-id="72f9f-219">例如，較舊版本的 hello SDK 傳回的回應物件，與 HTTP 狀態碼，您通常不需要 toocheck 因為作業的方法擲回`CloudException`任何表示錯誤的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="72f9f-219">For example, older versions of hello SDK returned a response object with an HTTP status code, which you often didn't need toocheck because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="72f9f-220">hello 新的擴充方法僅以傳回模型物件，儲存您 hello 麻煩 toounwrap 您的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="72f9f-220">hello new extension methods just return model objects, saving you hello trouble of having toounwrap them in your code.</span></span>
* <span data-ttu-id="72f9f-221">相反地，hello 核心介面現在會公開方法可讓您有更多的控制層級 hello HTTP 如有需要。</span><span class="sxs-lookup"><span data-stu-id="72f9f-221">Conversely, hello core interfaces now expose methods that give you more control at hello HTTP level if you need it.</span></span> <span data-ttu-id="72f9f-222">您現在可以傳入要求，以及新的 hello 中包含的自訂 HTTP 標頭 toobe`AzureOperationResponse<T>`傳回類型可讓您直接存取 toohello`HttpRequestMessage`和`HttpResponseMessage`hello 作業。</span><span class="sxs-lookup"><span data-stu-id="72f9f-222">You can now pass in custom HTTP headers toobe included in requests, and hello new `AzureOperationResponse<T>` return type gives you direct access toohello `HttpRequestMessage` and `HttpResponseMessage` for hello operation.</span></span> <span data-ttu-id="72f9f-223">`AzureOperationResponse`定義在 hello`Microsoft.Rest.Azure`命名空間，並取代`Hyak.Common.OperationResponse`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-223">`AzureOperationResponse` is defined in hello `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="72f9f-224">ScoringParameters 變更</span><span class="sxs-lookup"><span data-stu-id="72f9f-224">ScoringParameters changes</span></span>
<span data-ttu-id="72f9f-225">新的類別，名為`ScoringParameter`已加入在最新 SDK toomake hello 它更容易 tooprovide 參數 tooscoring 設定檔中搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="72f9f-225">A new class named `ScoringParameter` has been added in hello latest SDK toomake it easier tooprovide parameters tooscoring profiles in a search query.</span></span> <span data-ttu-id="72f9f-226">先前 hello`ScoringProfiles`屬性 hello`SearchParameters`類別的型別是`IList<string>`;現在型別為`IList<ScoringParameter>`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-226">Previously hello `ScoringProfiles` property of hello `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="72f9f-227">範例</span><span class="sxs-lookup"><span data-stu-id="72f9f-227">Example</span></span>
<span data-ttu-id="72f9f-228">如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="72f9f-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="72f9f-229">您可以將它變更 toothis toofix 任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="72f9f-229">You can change it toothis toofix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="72f9f-230">模型類別變更</span><span class="sxs-lookup"><span data-stu-id="72f9f-230">Model class changes</span></span>
<span data-ttu-id="72f9f-231">因為 toohello 中所述的簽章變更[作業方法變更](#OperationMethodChanges)，許多類別在 hello`Microsoft.Azure.Search.Models`已重新命名或移除命名空間。</span><span class="sxs-lookup"><span data-stu-id="72f9f-231">Due toohello signature changes described in [Operation method changes](#OperationMethodChanges), many classes in hello `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="72f9f-232">例如：</span><span class="sxs-lookup"><span data-stu-id="72f9f-232">For example:</span></span>

* <span data-ttu-id="72f9f-233">`IndexDefinitionResponse` 已由 `AzureOperationResponse<Index>` 取代</span><span class="sxs-lookup"><span data-stu-id="72f9f-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="72f9f-234">`DocumentSearchResponse`已重新命名過`DocumentSearchResult`</span><span class="sxs-lookup"><span data-stu-id="72f9f-234">`DocumentSearchResponse` has been renamed too`DocumentSearchResult`</span></span>
* <span data-ttu-id="72f9f-235">`IndexResult`已重新命名過`IndexingResult`</span><span class="sxs-lookup"><span data-stu-id="72f9f-235">`IndexResult` has been renamed too`IndexingResult`</span></span>
* <span data-ttu-id="72f9f-236">`Documents.Count()`現在會傳回`long`hello 文件計數，而不是`DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="72f9f-236">`Documents.Count()` now returns a `long` with hello document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="72f9f-237">`IndexGetStatisticsResponse`已重新命名過`IndexGetStatisticsResult`</span><span class="sxs-lookup"><span data-stu-id="72f9f-237">`IndexGetStatisticsResponse` has been renamed too`IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="72f9f-238">`IndexListResponse`已重新命名過`IndexListResult`</span><span class="sxs-lookup"><span data-stu-id="72f9f-238">`IndexListResponse` has been renamed too`IndexListResult`</span></span>

<span data-ttu-id="72f9f-239">toosummarize， `OperationResponse`-衍生存在於的 toowrap 已移除模型物件的類別。</span><span class="sxs-lookup"><span data-stu-id="72f9f-239">toosummarize, `OperationResponse`-derived classes that existed only toowrap a model object have been removed.</span></span> <span data-ttu-id="72f9f-240">hello 其餘的類別都已經將其從變更的後置詞`Response`太`Result`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-240">hello remaining classes have had their suffix changed from `Response` too`Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="72f9f-241">範例</span><span class="sxs-lookup"><span data-stu-id="72f9f-241">Example</span></span>
<span data-ttu-id="72f9f-242">如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="72f9f-242">If your code looks like this:</span></span>

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

<span data-ttu-id="72f9f-243">您可以將它變更 toothis toofix 任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="72f9f-243">You can change it toothis toofix any build errors:</span></span>

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="72f9f-244">回應類別和 IEnumerable</span><span class="sxs-lookup"><span data-stu-id="72f9f-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="72f9f-245">可能會影響您程式碼的其他變更，就是讓集合不再實作 `IEnumerable<T>`的回應類別。</span><span class="sxs-lookup"><span data-stu-id="72f9f-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="72f9f-246">相反地，您也可以直接存取 hello 集合屬性。</span><span class="sxs-lookup"><span data-stu-id="72f9f-246">Instead, you can access hello collection property directly.</span></span> <span data-ttu-id="72f9f-247">例如，如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="72f9f-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="72f9f-248">您可以將它變更 toothis toofix 任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="72f9f-248">You can change it toothis toofix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="72f9f-249">Web 應用程式的特殊案例</span><span class="sxs-lookup"><span data-stu-id="72f9f-249">Special case for web applications</span></span>
<span data-ttu-id="72f9f-250">如果您有 web 應用程式，會將序列化`DocumentSearchResponse`直接 toosend 搜尋結果 toohello 瀏覽器，您將需要 toochange 程式碼或 hello 結果不會正確序列化。</span><span class="sxs-lookup"><span data-stu-id="72f9f-250">If you have a web application that serializes `DocumentSearchResponse` directly toosend search results toohello browser, you will need toochange your code or hello results will not serialize correctly.</span></span> <span data-ttu-id="72f9f-251">例如，如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="72f9f-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="72f9f-252">您可以變更它藉由取得 hello `.Results` hello 搜尋回應 toofix 搜尋結果呈現的屬性：</span><span class="sxs-lookup"><span data-stu-id="72f9f-252">You can change it by getting hello `.Results` property of hello search response toofix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="72f9f-253">您必須 toolook 這種情況下的在程式碼中自行;**hello 編譯器不會警告您**因為`JsonResult.Data`的型別`object`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-253">You will have toolook for such cases in your code yourself; **hello compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="72f9f-254">CloudException 變更</span><span class="sxs-lookup"><span data-stu-id="72f9f-254">CloudException changes</span></span>
<span data-ttu-id="72f9f-255">hello`CloudException`類別已經從 hello`Hyak.Common`命名空間 toohello`Microsoft.Rest.Azure`命名空間。</span><span class="sxs-lookup"><span data-stu-id="72f9f-255">hello `CloudException` class has moved from hello `Hyak.Common` namespace toohello `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="72f9f-256">此外，其`Error`屬性已重新命名過`Body`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-256">Also, its `Error` property has been renamed too`Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="72f9f-257">SearchServiceClient 和 SearchIndexClient 變更</span><span class="sxs-lookup"><span data-stu-id="72f9f-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="72f9f-258">hello hello 的型別`Credentials`屬性已經從`SearchCredentials`tooits 基底類別， `ServiceClientCredentials`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-258">hello type of hello `Credentials` property has changed from `SearchCredentials` tooits base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="72f9f-259">如果您需要 tooaccess hello`SearchCredentials`的`SearchIndexClient`或`SearchServiceClient`，請使用新 hello`SearchCredentials`屬性。</span><span class="sxs-lookup"><span data-stu-id="72f9f-259">If you need tooaccess hello `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use hello new `SearchCredentials` property.</span></span>

<span data-ttu-id="72f9f-260">在舊版的 hello SDK，`SearchServiceClient`和`SearchIndexClient`具有建構函式所花費`HttpClient`參數。</span><span class="sxs-lookup"><span data-stu-id="72f9f-260">In older versions of hello SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="72f9f-261">這些建構函式已由使用 `HttpClientHandler` 的建構函式和 `DelegatingHandler` 物件的陣列取代。</span><span class="sxs-lookup"><span data-stu-id="72f9f-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="72f9f-262">這使得更容易 tooinstall 自訂處理常式 toopre 處理 HTTP 要求如有必要。</span><span class="sxs-lookup"><span data-stu-id="72f9f-262">This makes it easier tooinstall custom handlers toopre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="72f9f-263">最後，hello 建構函式所花費`Uri`和`SearchCredentials`已變更。</span><span class="sxs-lookup"><span data-stu-id="72f9f-263">Finally, hello constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="72f9f-264">例如，如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="72f9f-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="72f9f-265">您可以將它變更 toothis toofix 任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="72f9f-265">You can change it toothis toofix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="72f9f-266">也請注意 hello 類型 hello 認證參數已太變更`ServiceClientCredentials`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-266">Also note that hello type of hello credentials parameter has changed too`ServiceClientCredentials`.</span></span> <span data-ttu-id="72f9f-267">這是您的程式碼，因為不太可能 tooaffect`SearchCredentials`衍生自`ServiceClientCredentials`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-267">This is unlikely tooaffect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="72f9f-268">傳送要求 ID</span><span class="sxs-lookup"><span data-stu-id="72f9f-268">Passing a request ID</span></span>
<span data-ttu-id="72f9f-269">在舊版的 hello SDK 中，您可以設定要求識別碼 hello 上`SearchServiceClient`或`SearchIndexClient`而且它會包含在每個要求 toohello REST API。</span><span class="sxs-lookup"><span data-stu-id="72f9f-269">In older versions of hello SDK, you could set a request ID on hello `SearchServiceClient` or `SearchIndexClient` and it would be included in every request toohello REST API.</span></span> <span data-ttu-id="72f9f-270">這是用於疑難排解問題與您的搜尋服務，如果您需要 toocontact 支援。</span><span class="sxs-lookup"><span data-stu-id="72f9f-270">This is useful for troubleshooting issues with your search service if you need toocontact support.</span></span> <span data-ttu-id="72f9f-271">不過，它會針對每個作業更實用的 tooset 的唯一要求 ID，而不是不是 toouse hello 相同識別碼的所有作業。</span><span class="sxs-lookup"><span data-stu-id="72f9f-271">However, it is more useful tooset a unique request ID for every operation rather than toouse hello same ID for all operations.</span></span> <span data-ttu-id="72f9f-272">基於這個理由，hello`SetClientRequestId`方法`SearchServiceClient`和`SearchIndexClient`已移除。</span><span class="sxs-lookup"><span data-stu-id="72f9f-272">For this reason, hello `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="72f9f-273">相反地，您可以將傳遞的要求識別碼 tooeach 作業方法 hello 透過選擇性`SearchRequestOptions`參數。</span><span class="sxs-lookup"><span data-stu-id="72f9f-273">Instead, you can pass a request ID tooeach operation method via hello optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="72f9f-274">在 hello SDK 未來版本中，我們將加入新 hello 用戶端上的物件，全域設定要求識別碼的機制，與其他 Azure Sdk 所使用的 hello 方法一致。</span><span class="sxs-lookup"><span data-stu-id="72f9f-274">In a future release of hello SDK, we will add a new mechanism for setting a request ID globally on hello client objects that is consistent with hello approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="72f9f-275">範例</span><span class="sxs-lookup"><span data-stu-id="72f9f-275">Example</span></span>
<span data-ttu-id="72f9f-276">如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="72f9f-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="72f9f-277">您可以將它變更 toothis toofix 任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="72f9f-277">You can change it toothis toofix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="72f9f-278">介面名稱變更</span><span class="sxs-lookup"><span data-stu-id="72f9f-278">Interface name changes</span></span>
<span data-ttu-id="72f9f-279">hello 作業群組介面名稱具有所有已變更的 toobe 及其對應的屬性名稱與一致：</span><span class="sxs-lookup"><span data-stu-id="72f9f-279">hello operation group interface names have all changed toobe consistent with their corresponding property names:</span></span>

* <span data-ttu-id="72f9f-280">hello 的型別`ISearchServiceClient.Indexes`從重新命名`IIndexOperations`太`IIndexesOperations`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-280">hello type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` too`IIndexesOperations`.</span></span>
* <span data-ttu-id="72f9f-281">hello 的型別`ISearchServiceClient.Indexers`從重新命名`IIndexerOperations`太`IIndexersOperations`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-281">hello type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` too`IIndexersOperations`.</span></span>
* <span data-ttu-id="72f9f-282">hello 的型別`ISearchServiceClient.DataSources`從重新命名`IDataSourceOperations`太`IDataSourcesOperations`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-282">hello type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` too`IDataSourcesOperations`.</span></span>
* <span data-ttu-id="72f9f-283">hello 的型別`ISearchIndexClient.Documents`從重新命名`IDocumentOperations`太`IDocumentsOperations`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-283">hello type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` too`IDocumentsOperations`.</span></span>

<span data-ttu-id="72f9f-284">這項變更是不太可能 tooaffect 您程式碼，除非您建立這些介面用於測試目的模擬。</span><span class="sxs-lookup"><span data-stu-id="72f9f-284">This change is unlikely tooaffect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="72f9f-285">版本 1.1 的錯誤修正</span><span class="sxs-lookup"><span data-stu-id="72f9f-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="72f9f-286">在舊版的自訂模型類別 hello Azure 搜尋.NET SDK 相關 tooserialization 時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="72f9f-286">There was a bug in older versions of hello Azure Search .NET SDK relating tooserialization of custom model classes.</span></span> <span data-ttu-id="72f9f-287">當您建立自訂模型類別與不可為 null 的實值類型的屬性，可能會發生 hello bug。</span><span class="sxs-lookup"><span data-stu-id="72f9f-287">hello bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-tooreproduce"></a><span data-ttu-id="72f9f-288">步驟 tooreproduce</span><span class="sxs-lookup"><span data-stu-id="72f9f-288">Steps tooreproduce</span></span>
<span data-ttu-id="72f9f-289">建立具有不可為 null 值類型的屬性的自訂模型類別。</span><span class="sxs-lookup"><span data-stu-id="72f9f-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="72f9f-290">例如，加入類型 `int` 而不是 `int?` 的公用 `UnitCount` 屬性。</span><span class="sxs-lookup"><span data-stu-id="72f9f-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="72f9f-291">如果索引文件以 hello 該類型的預設值 (例如，0 代表`int`)，hello 欄位將 Azure 搜尋中傳回 null。</span><span class="sxs-lookup"><span data-stu-id="72f9f-291">If you index a document with hello default value of that type (for example, 0 for `int`), hello field will be null in Azure Search.</span></span> <span data-ttu-id="72f9f-292">如果您後續搜尋該文件，hello`Search`呼叫會擲回`JsonSerializationException`抱怨不能轉換`null`太`int`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-292">If you subsequently search for that document, hello `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` too`int`.</span></span>

<span data-ttu-id="72f9f-293">此外，如預期般自從 null 寫入 toohello 索引，而不是預期的 hello 值後，篩選器可能無法運作。</span><span class="sxs-lookup"><span data-stu-id="72f9f-293">Also, filters may not work as expected since null was written toohello index instead of hello intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="72f9f-294">修正詳細資料</span><span class="sxs-lookup"><span data-stu-id="72f9f-294">Fix details</span></span>
<span data-ttu-id="72f9f-295">Hello SDK 1.1 版中，我們已修正此問題。</span><span class="sxs-lookup"><span data-stu-id="72f9f-295">We have fixed this issue in version 1.1 of hello SDK.</span></span> <span data-ttu-id="72f9f-296">現在，如果您有一個如下的模型類別：</span><span class="sxs-lookup"><span data-stu-id="72f9f-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="72f9f-297">您設定和`IntValue`too0 的值現在正確序列化為 0 hello 網路上及儲存為 hello 索引中為 0。</span><span class="sxs-lookup"><span data-stu-id="72f9f-297">and you set `IntValue` too0, that value is now correctly serialized as 0 on hello wire and stored as 0 in hello index.</span></span> <span data-ttu-id="72f9f-298">來回行程也如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="72f9f-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="72f9f-299">沒有一個潛在的問題 toobe 留意這種方法： 如果您使用的模型型別不可為 null 的屬性時，您有太**保證**沒有文件索引中的包含 hello 對應欄位的 null 值。</span><span class="sxs-lookup"><span data-stu-id="72f9f-299">There is one potential issue toobe aware of with this approach: If you use a model type with a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="72f9f-300">Hello SDK 都 hello Azure 搜尋 REST API 將協助您 tooenforce 這。</span><span class="sxs-lookup"><span data-stu-id="72f9f-300">Neither hello SDK nor hello Azure Search REST API will help you tooenforce this.</span></span>

<span data-ttu-id="72f9f-301">這不只是假設性的問題： 想像一下，讓您加入新欄位 tooan 現有索引型別的`Edm.Int32`。</span><span class="sxs-lookup"><span data-stu-id="72f9f-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="72f9f-302">在更新之後 hello 索引定義，所有文件必須針對該新欄位的 null 值 （因為所有類型都是可為 null 的 Azure 搜尋）。</span><span class="sxs-lookup"><span data-stu-id="72f9f-302">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="72f9f-303">若您搭配不可為 null，然後使用模型類別`int`該欄位的屬性，您會收到`JsonSerializationException`tooretrieve 文件時，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="72f9f-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="72f9f-304">基於這個原因，我們仍然建議您在模型類別中使用可為 null 的類型做為最佳作法。</span><span class="sxs-lookup"><span data-stu-id="72f9f-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="72f9f-305">如需有關這個 bug 及 hello 修正程式的詳細資訊，請參閱[此問題在 GitHub 上的](https://github.com/Azure/azure-sdk-for-net/issues/1063)。</span><span class="sxs-lookup"><span data-stu-id="72f9f-305">For more details on this bug and hello fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

