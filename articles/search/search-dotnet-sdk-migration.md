---
title: "升級至 Azure 搜尋服務 .NET SDK 版本 1.1 | Microsoft Docs"
description: "升級至 Azure 搜尋服務 .NET SDK 版本 1.1"
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
ms.openlocfilehash: 9782454e3bfc697b63cde8aa28a14be0c393c36b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-net-sdk-version-3"></a><span data-ttu-id="5643a-103">升級至 Azure 搜尋服務 .NET SDK 版本 3</span><span class="sxs-lookup"><span data-stu-id="5643a-103">Upgrading to the Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="5643a-104">如果您使用版本 2.0 預覽版或更舊版本的 [Azure 搜尋服務 .NET SDK](https://aka.ms/search-sdk)，本文可協助您將應用程式升級至版本 3。</span><span class="sxs-lookup"><span data-stu-id="5643a-104">If you're using version 2.0-preview or older of the [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application to use version 3.</span></span>

<span data-ttu-id="5643a-105">如需包括範例的 SDK 一般逐步解說，請參閱 [如何從 .NET 應用程式使用 Azure 搜尋服務](search-howto-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="5643a-105">For a more general walkthrough of the SDK including examples, see [How to use Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="5643a-106">Azure 搜尋服務 .NET SDK 版本 3 包含一些從舊版所做的變更。</span><span class="sxs-lookup"><span data-stu-id="5643a-106">Version 3 of the Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="5643a-107">這些變更大部分是次要變更，所以變更程式碼應該只需要最少的工作。</span><span class="sxs-lookup"><span data-stu-id="5643a-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="5643a-108">請參閱 [升級步驟](#UpgradeSteps) 以取得如何變更您的程式碼以使用新的 SDK 版本的指示。</span><span class="sxs-lookup"><span data-stu-id="5643a-108">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="5643a-109">如果您使用 1.0.2 預覽版或更舊版本，請先升級至 1.1 版，再升級至版本 3。</span><span class="sxs-lookup"><span data-stu-id="5643a-109">If you're using version 1.0.2-preview or older, you should upgrade to version 1.1 first, and then upgrade to version 3.</span></span> <span data-ttu-id="5643a-110">如需指示，請參閱 [附錄：升級至版本 1.1 的步驟](#UpgradeStepsV1) 。</span><span class="sxs-lookup"><span data-stu-id="5643a-110">See [Appendix: Steps to upgrade to version 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="5643a-111">您的「Azure 搜尋服務」執行個體支援數個 REST API 版本，包括最新版本。</span><span class="sxs-lookup"><span data-stu-id="5643a-111">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="5643a-112">當一個版本不再是最新版本時，您仍可繼續使用該版本，但建議您將程式碼移轉成使用最新版本。</span><span class="sxs-lookup"><span data-stu-id="5643a-112">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span> <span data-ttu-id="5643a-113">使用 REST API 時，您必須每個要求中透過 api-version 參數指定 API 版本。</span><span class="sxs-lookup"><span data-stu-id="5643a-113">When using the REST API, you must specify the API version in every request via the api-version parameter.</span></span> <span data-ttu-id="5643a-114">使用 .NET SDK 時，您使用的 SDK 版本會決定對應的 REST API 版本。</span><span class="sxs-lookup"><span data-stu-id="5643a-114">When using the .NET SDK, the version of the SDK you’re using determines the corresponding version of the REST API.</span></span> <span data-ttu-id="5643a-115">如果您使用的是舊版 SDK，則即使服務已升級成支援新版 API 版本，您仍可繼續執行該程式碼而無須變更。</span><span class="sxs-lookup"><span data-stu-id="5643a-115">If you are using an older SDK, you can continue to run that code with no changes even if the service is upgraded to support a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="5643a-116">版本 3 的新功能</span><span class="sxs-lookup"><span data-stu-id="5643a-116">What's new in version 3</span></span>
<span data-ttu-id="5643a-117">Azure 搜尋服務 .NET SDK 版本 3 以最新推出的 Azure 搜尋服務 REST API 版本為目標，特別是 2016-09-01。</span><span class="sxs-lookup"><span data-stu-id="5643a-117">Version 3 of the Azure Search .NET SDK targets the latest generally available version of the Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="5643a-118">這樣可讓您從 .NET 應用程式中使用 Azure 搜尋服務的許多新功能，包括：</span><span class="sxs-lookup"><span data-stu-id="5643a-118">This makes it possible to use many new features of Azure Search from a .NET application, including the following:</span></span>

* [<span data-ttu-id="5643a-119">自訂分析器</span><span class="sxs-lookup"><span data-stu-id="5643a-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="5643a-120">[Azure Blob 儲存體](search-howto-indexing-azure-blob-storage.md)和 [Azure 表格儲存體](search-howto-indexing-azure-tables.md)索引子支援</span><span class="sxs-lookup"><span data-stu-id="5643a-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="5643a-121">透過 [欄位對應](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="5643a-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="5643a-122">可安全地並行更新索引定義、索引子和資料來源的 ETag 支援</span><span class="sxs-lookup"><span data-stu-id="5643a-122">ETags support to enable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="5643a-123">支援修飾您的模型類別和使用新的 `FieldBuilder` 類別，以宣告方式建置索引欄位定義。</span><span class="sxs-lookup"><span data-stu-id="5643a-123">Support for building index field definitions declaratively by decorating your model class and using the new `FieldBuilder` class.</span></span>
* <span data-ttu-id="5643a-124">對 .NET Core 和 .NET Portable Profile 111 的支援</span><span class="sxs-lookup"><span data-stu-id="5643a-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="5643a-125">升級步驟</span><span class="sxs-lookup"><span data-stu-id="5643a-125">Steps to upgrade</span></span>
<span data-ttu-id="5643a-126">首先，更新 `Microsoft.Azure.Search` 的 NuGet 參考，方法是使用 NuGet 封裝管理員主控台，或是在 Visual Studio 中用滑鼠右鍵按一下您的專案參考並選取 [管理 NuGet 封裝]。</span><span class="sxs-lookup"><span data-stu-id="5643a-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="5643a-127">一旦 NuGet 下載新的封裝和其相依性，請重建您的專案。</span><span class="sxs-lookup"><span data-stu-id="5643a-127">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="5643a-128">根據您的程式碼結構情況，它可能會順利重新建置。</span><span class="sxs-lookup"><span data-stu-id="5643a-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="5643a-129">如果是這樣，代表您已準備就緒！</span><span class="sxs-lookup"><span data-stu-id="5643a-129">If so, you're ready to go!</span></span>

<span data-ttu-id="5643a-130">如果建置失敗，您應該會看到如下所示的建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="5643a-130">If your build fails, you should see a build error like the following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' to 'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="5643a-131">下一個步驟是修正此建置錯誤。</span><span class="sxs-lookup"><span data-stu-id="5643a-131">The next step is to fix this build error.</span></span> <span data-ttu-id="5643a-132">如需有關造成錯誤的原因及修正方式的詳細資料，請參閱[版本 3 的重大變更](#ListOfChanges)。</span><span class="sxs-lookup"><span data-stu-id="5643a-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes the error and how to fix it.</span></span>

<span data-ttu-id="5643a-133">您可能會看到與過時的方法或屬性相關的其他建置警告。</span><span class="sxs-lookup"><span data-stu-id="5643a-133">You may see additional build warnings related to obsolete methods or properties.</span></span> <span data-ttu-id="5643a-134">警告將會包含要使用哪些內容取代過時功能的指示。</span><span class="sxs-lookup"><span data-stu-id="5643a-134">The warnings will include instructions on what to use instead of the deprecated feature.</span></span> <span data-ttu-id="5643a-135">例如，如果您的應用程式使用 `IndexingParameters.Base64EncodeKeys` 屬性，您應該會收到指出 `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="5643a-135">For example, if your application uses the `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="5643a-136">一旦您已修正任何建置錯誤，您就可以變更您的應用程式以視需要利用新的功能。</span><span class="sxs-lookup"><span data-stu-id="5643a-136">Once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span> <span data-ttu-id="5643a-137">[版本 3 的新功能](#WhatsNew)中詳述 SDK 的新功能。</span><span class="sxs-lookup"><span data-stu-id="5643a-137">New features in the SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="5643a-138">版本 3 的重大變更</span><span class="sxs-lookup"><span data-stu-id="5643a-138">Breaking changes in version 3</span></span>
<span data-ttu-id="5643a-139">除了重新建置您的應用程式，版本 3 有少數幾項重大變更可能需要變更程式碼。</span><span class="sxs-lookup"><span data-stu-id="5643a-139">There a small number of breaking changes in version 3 that may require code changes in addition to rebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="5643a-140">Indexes.GetClient 傳回類型</span><span class="sxs-lookup"><span data-stu-id="5643a-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="5643a-141">`Indexes.GetClient` 方法有新的傳回類型。</span><span class="sxs-lookup"><span data-stu-id="5643a-141">The `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="5643a-142">以往它會傳回 `SearchIndexClient`，但這在 2.0 預覽版中已變更為 `ISearchIndexClient`，該變更也延續至版本 3。</span><span class="sxs-lookup"><span data-stu-id="5643a-142">Previously, it returned `SearchIndexClient`, but this was changed to `ISearchIndexClient` in version 2.0-preview, and that change carries over to version 3.</span></span> <span data-ttu-id="5643a-143">這是為了支援想要藉由傳回 `ISearchIndexClient` 的模擬實作，針對單元測試模擬 `GetClient` 方法的客戶。</span><span class="sxs-lookup"><span data-stu-id="5643a-143">This is to support customers that wish to mock the `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="5643a-144">範例</span><span class="sxs-lookup"><span data-stu-id="5643a-144">Example</span></span>
<span data-ttu-id="5643a-145">如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="5643a-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="5643a-146">您可以將其變更如下以修正任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="5643a-146">You can change it to this to fix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-to-strings"></a><span data-ttu-id="5643a-147">AnalyzerName、DataType 及其他類型已無法再隱含地轉換成字串</span><span class="sxs-lookup"><span data-stu-id="5643a-147">AnalyzerName, DataType, and others are no longer implicitly convertible to strings</span></span>
<span data-ttu-id="5643a-148">Azure 搜尋服務 .NET SDK 中有許多類型衍生自 `ExtensibleEnum`。</span><span class="sxs-lookup"><span data-stu-id="5643a-148">There are many types in the Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="5643a-149">以往這些類型全都可隱含地轉換成 `string` 類型。</span><span class="sxs-lookup"><span data-stu-id="5643a-149">Previously these types were all implicitly convertible to type `string`.</span></span> <span data-ttu-id="5643a-150">不過，在這些類別的 `Object.Equals` 實作中已發現錯誤，為了修正錯誤，需要停用這項隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="5643a-150">However, a bug was discovered in the `Object.Equals` implementation for these classes, and fixing the bug required disabling this implicit conversion.</span></span> <span data-ttu-id="5643a-151">仍然允許明確轉換為 `string`。</span><span class="sxs-lookup"><span data-stu-id="5643a-151">Explicit conversion to `string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="5643a-152">範例</span><span class="sxs-lookup"><span data-stu-id="5643a-152">Example</span></span>
<span data-ttu-id="5643a-153">如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="5643a-153">If your code looks like this:</span></span>

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

<span data-ttu-id="5643a-154">您可以將其變更如下以修正任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="5643a-154">You can change it to this to fix any build errors:</span></span>

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

### <a name="removed-obsolete-members"></a><span data-ttu-id="5643a-155">移除過時的成員</span><span class="sxs-lookup"><span data-stu-id="5643a-155">Removed obsolete members</span></span>

<span data-ttu-id="5643a-156">您可能會看到關於方法或屬性的建置錯誤，這些已在 2.0 預覽版中標示為過時，且隨後於版本 3 中移除。</span><span class="sxs-lookup"><span data-stu-id="5643a-156">You may see build errors related to methods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="5643a-157">如果您遇到這類錯誤，解決方法如下︰</span><span class="sxs-lookup"><span data-stu-id="5643a-157">If you encounter such errors, here is how to resolve them:</span></span>

- <span data-ttu-id="5643a-158">如果您使用這個建構函式︰`ScoringParameter(string name, string value)`，請改用︰`ScoringParameter(string name, IEnumerable<string> values)`</span><span class="sxs-lookup"><span data-stu-id="5643a-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="5643a-159">如果您原本使用 `ScoringParameter.Value` 屬性，請改用 `ScoringParameter.Values` 屬性或`ToString` 方法。</span><span class="sxs-lookup"><span data-stu-id="5643a-159">If you were using the `ScoringParameter.Value` property, use the `ScoringParameter.Values` property or the `ToString` method instead.</span></span>
- <span data-ttu-id="5643a-160">如果您原本使用 `SearchRequestOptions.RequestId` 屬性，請改用 `ClientRequestId` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5643a-160">If you were using the `SearchRequestOptions.RequestId` property, use the `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="5643a-161">已移除的預覽功能</span><span class="sxs-lookup"><span data-stu-id="5643a-161">Removed preview features</span></span>

<span data-ttu-id="5643a-162">如果您從 2.0 預覽版升級至版本 3，請注意已移除 Blob 索引子的 JSON 和 CSV 剖析支援，因為這些功能仍處於預覽階段。</span><span class="sxs-lookup"><span data-stu-id="5643a-162">If you are upgrading from version 2.0-preview to version 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="5643a-163">具體而言，`IndexingParametersExtensions` 類別中已移除下列方法︰</span><span class="sxs-lookup"><span data-stu-id="5643a-163">Specifically, the following methods of the `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="5643a-164">如果您的應用程式緊密相依於這些功能，則您無法升級至 Azure 搜尋服務 .NET SDK 版本 3。</span><span class="sxs-lookup"><span data-stu-id="5643a-164">If your application has a hard dependency on these features, you will not be able to upgrade to version 3 of the Azure Search .NET SDK.</span></span> <span data-ttu-id="5643a-165">您可以繼續使用 2.0 預覽版。</span><span class="sxs-lookup"><span data-stu-id="5643a-165">You can continue to use version 2.0-preview.</span></span> <span data-ttu-id="5643a-166">但請記住，**我們不建議在實際執行應用程式中使用預覽 SDK**。</span><span class="sxs-lookup"><span data-stu-id="5643a-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="5643a-167">預覽功能僅供評估，可能會變更。</span><span class="sxs-lookup"><span data-stu-id="5643a-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="5643a-168">結論</span><span class="sxs-lookup"><span data-stu-id="5643a-168">Conclusion</span></span>
<span data-ttu-id="5643a-169">如果您需要使用 Azure 搜尋服務 .NET SDK 的更多詳細資料，請參閱我們最近更新的 [做法](search-howto-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="5643a-169">If you need more details on using the Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="5643a-170">歡迎您提供 SDK 的意見反應。</span><span class="sxs-lookup"><span data-stu-id="5643a-170">We welcome your feedback on the SDK.</span></span> <span data-ttu-id="5643a-171">如果您遇到問題，歡迎在 [Azure 搜尋服務 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch)上尋求協助。</span><span class="sxs-lookup"><span data-stu-id="5643a-171">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="5643a-172">如果您發現錯誤，您可以在 [Azure .NET SDK GitHub 儲存機制](https://github.com/Azure/azure-sdk-for-net/issues)中提出問題。</span><span class="sxs-lookup"><span data-stu-id="5643a-172">If you find a bug, you can file an issue in the [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="5643a-173">請確定在您的問題標題加上前置詞「搜尋服務 SDK：」。</span><span class="sxs-lookup"><span data-stu-id="5643a-173">Make sure to prefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="5643a-174">感謝您使用 Azure 搜尋服務！</span><span class="sxs-lookup"><span data-stu-id="5643a-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-to-upgrade-to-version-11"></a><span data-ttu-id="5643a-175">附錄：升級至版本 1.1 的步驟</span><span class="sxs-lookup"><span data-stu-id="5643a-175">Appendix: Steps to upgrade to version 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="5643a-176">本節僅適用於 Azure 搜尋服務 .NET SDK 1.0.2 預覽版和更舊版本的使用者。</span><span class="sxs-lookup"><span data-stu-id="5643a-176">This section applies only to users of the Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="5643a-177">首先，更新 `Microsoft.Azure.Search` 的 NuGet 參考，方法是使用 NuGet 封裝管理員主控台，或是在 Visual Studio 中用滑鼠右鍵按一下您的專案參考並選取 [管理 NuGet 封裝]。</span><span class="sxs-lookup"><span data-stu-id="5643a-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="5643a-178">一旦 NuGet 下載新的封裝和其相依性，請重建您的專案。</span><span class="sxs-lookup"><span data-stu-id="5643a-178">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="5643a-179">如果您之前使用版本 1.0.0 預覽版、1.0.1 預覽版，或 1.0.2 預覽版，應能夠成功建置且您已經準備就緒！</span><span class="sxs-lookup"><span data-stu-id="5643a-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, the build should succeed and you're ready to go!</span></span>

<span data-ttu-id="5643a-180">如果您之前使用版本 0.13.0 預覽版或更舊版本，您應該會看到如下所示的建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="5643a-180">If you were previously using version 0.13.0-preview or older, you should see build errors like the following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: The type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="5643a-181">下一步是逐一修正建置錯誤。</span><span class="sxs-lookup"><span data-stu-id="5643a-181">The next step is to fix the build errors one by one.</span></span> <span data-ttu-id="5643a-182">大部分錯誤需要變更 SDK 中已重新命名的某些類別和方法名稱。</span><span class="sxs-lookup"><span data-stu-id="5643a-182">Most will require changing some class and method names that have been renamed in the SDK.</span></span> <span data-ttu-id="5643a-183">[版本 1.1 的重大變更清單](#ListOfChangesV1) 一節包含這些名稱變更的清單。</span><span class="sxs-lookup"><span data-stu-id="5643a-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="5643a-184">如果您使用自訂類別來建立您文件的模型，且這些類別有不可為 Null 的基本類型屬性 (例如 C# 中的 `int` 或 `bool`)，則您應該要注意 SDK 1.1 版本中的某個錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="5643a-184">If you're using custom classes to model your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in the 1.1 version of the SDK of which you should be aware.</span></span> <span data-ttu-id="5643a-185">請參閱 [版本 1.1 的錯誤修正](#BugFixesV1) 一節以取得更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5643a-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="5643a-186">最後，一旦您已修正任何建置錯誤，您可以變更您的應用程式以視需要利用新的功能。</span><span class="sxs-lookup"><span data-stu-id="5643a-186">Finally, once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="5643a-187">版本 1.1 的重大變更清單</span><span class="sxs-lookup"><span data-stu-id="5643a-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="5643a-188">下列清單會根據變更影響應用程式程式碼的可能性排序。</span><span class="sxs-lookup"><span data-stu-id="5643a-188">The following list is ordered by the likelihood that the change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="5643a-189">IndexBatch 和 IndexAction 變更</span><span class="sxs-lookup"><span data-stu-id="5643a-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="5643a-190">`IndexBatch.Create` 已重新命名為 `IndexBatch.New` 且不再具有 `params` 引數。</span><span class="sxs-lookup"><span data-stu-id="5643a-190">`IndexBatch.Create` has been renamed to `IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="5643a-191">您可以針對混合不同類型動作 (合併、刪除等等) 的批次使用 `IndexBatch.New` 。</span><span class="sxs-lookup"><span data-stu-id="5643a-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="5643a-192">此外，還有新的靜態方法可以用來建立批次，其中所有動作都相同：`Delete`、`Merge`、`MergeOrUpload` 和 `Upload`。</span><span class="sxs-lookup"><span data-stu-id="5643a-192">In addition, there are new static methods for creating batches where all the actions are the same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="5643a-193">`IndexAction` 不再具有公用建構函式且其屬性現在固定不變。</span><span class="sxs-lookup"><span data-stu-id="5643a-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="5643a-194">您應該使用新的靜態方法來針對不同用途建立動作：`Delete`、`Merge`、`MergeOrUpload` 和 `Upload`。</span><span class="sxs-lookup"><span data-stu-id="5643a-194">You should use the new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="5643a-195">`IndexAction.Create` 已移除。</span><span class="sxs-lookup"><span data-stu-id="5643a-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="5643a-196">如果您使用僅採用文件的多載，請務必改為使用 `Upload` 。</span><span class="sxs-lookup"><span data-stu-id="5643a-196">If you used the overload that takes only a document, make sure to use `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="5643a-197">範例</span><span class="sxs-lookup"><span data-stu-id="5643a-197">Example</span></span>
<span data-ttu-id="5643a-198">如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="5643a-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="5643a-199">您可以將其變更如下以修正任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="5643a-199">You can change it to this to fix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="5643a-200">如果您想要的話，可以進一步加以簡化如下：</span><span class="sxs-lookup"><span data-stu-id="5643a-200">If you want, you can further simplify it to this:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="5643a-201">IndexBatchException 變更</span><span class="sxs-lookup"><span data-stu-id="5643a-201">IndexBatchException changes</span></span>
<span data-ttu-id="5643a-202">`IndexBatchException.IndexResponse` 屬性已重新命名為 `IndexingResults`，而其類型現在是 `IList<IndexingResult>`。</span><span class="sxs-lookup"><span data-stu-id="5643a-202">The `IndexBatchException.IndexResponse` property has been renamed to `IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="5643a-203">範例</span><span class="sxs-lookup"><span data-stu-id="5643a-203">Example</span></span>
<span data-ttu-id="5643a-204">如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="5643a-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="5643a-205">您可以將其變更如下以修正任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="5643a-205">You can change it to this to fix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="5643a-206">作業方法變更</span><span class="sxs-lookup"><span data-stu-id="5643a-206">Operation method changes</span></span>
<span data-ttu-id="5643a-207">Azure 搜尋服務 .NET SDK 中的每項作業都針對同步和非同步呼叫端公開為一組方法多載。</span><span class="sxs-lookup"><span data-stu-id="5643a-207">Each operation in the Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="5643a-208">在版本 1.1 中，這些方法多載的簽章和分解已經變更。</span><span class="sxs-lookup"><span data-stu-id="5643a-208">The signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="5643a-209">例如，較舊版本的 SDK 中的「取得索引統計資料」作業會公開這些簽章：</span><span class="sxs-lookup"><span data-stu-id="5643a-209">For example, the "Get Index Statistics" operation in older versions of the SDK exposed these signatures:</span></span>

<span data-ttu-id="5643a-210">在 `IIndexOperations`中：</span><span class="sxs-lookup"><span data-stu-id="5643a-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="5643a-211">在 `IndexOperationsExtensions`中：</span><span class="sxs-lookup"><span data-stu-id="5643a-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="5643a-212">在版本 1.1 中，相同作業的方法簽章看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="5643a-212">The method signatures for the same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="5643a-213">在 `IIndexesOperations`中：</span><span class="sxs-lookup"><span data-stu-id="5643a-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="5643a-214">在 `IndexesOperationsExtensions`中：</span><span class="sxs-lookup"><span data-stu-id="5643a-214">In `IndexesOperationsExtensions`:</span></span>

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

<span data-ttu-id="5643a-215">從版本 1.1 開始，Azure 搜尋服務 .NET SDK 會採用不同的作業方法組織方式：</span><span class="sxs-lookup"><span data-stu-id="5643a-215">Starting with version 1.1, the Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="5643a-216">選擇性參數現在模型化為預設參數，而不是其他方法多載。</span><span class="sxs-lookup"><span data-stu-id="5643a-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="5643a-217">這樣可以減少方法多載的數目，有時候減少的數量相當大。</span><span class="sxs-lookup"><span data-stu-id="5643a-217">This reduces the number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="5643a-218">擴充方法現在會隱藏許多來自呼叫端的無關 HTTP 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5643a-218">The extension methods now hide a lot of the extraneous details of HTTP from the caller.</span></span> <span data-ttu-id="5643a-219">例如，較舊版本的 SDK 會傳回具有 HTTP 狀態碼的回應物件，您通常不需要檢查，因為作業方法會針對表示發生錯誤的任何狀態碼擲回 `CloudException` 。</span><span class="sxs-lookup"><span data-stu-id="5643a-219">For example, older versions of the SDK returned a response object with an HTTP status code, which you often didn't need to check because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="5643a-220">新的擴充方法只會傳回模型物件，省卻您必須在程式碼中將它們解除包裝的麻煩。</span><span class="sxs-lookup"><span data-stu-id="5643a-220">The new extension methods just return model objects, saving you the trouble of having to unwrap them in your code.</span></span>
* <span data-ttu-id="5643a-221">相反地，核心介面現在會公開方法，在您需要時為您提供 HTTP 層級更多的控制權。</span><span class="sxs-lookup"><span data-stu-id="5643a-221">Conversely, the core interfaces now expose methods that give you more control at the HTTP level if you need it.</span></span> <span data-ttu-id="5643a-222">您現在可以傳入自訂 HTTP 標頭以包含在要求中，新的 `AzureOperationResponse<T>` 傳回類型給予您針對作業對於 `HttpRequestMessage` 和 `HttpResponseMessage` 的直接存取。</span><span class="sxs-lookup"><span data-stu-id="5643a-222">You can now pass in custom HTTP headers to be included in requests, and the new `AzureOperationResponse<T>` return type gives you direct access to the `HttpRequestMessage` and `HttpResponseMessage` for the operation.</span></span> <span data-ttu-id="5643a-223">`AzureOperationResponse` 是在 `Microsoft.Rest.Azure` 命名空間中定義，並且取代 `Hyak.Common.OperationResponse`。</span><span class="sxs-lookup"><span data-stu-id="5643a-223">`AzureOperationResponse` is defined in the `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="5643a-224">ScoringParameters 變更</span><span class="sxs-lookup"><span data-stu-id="5643a-224">ScoringParameters changes</span></span>
<span data-ttu-id="5643a-225">名為 `ScoringParameter` 的新類別已在最新的 SDK 中加入，讓您更輕鬆地提供參數給搜尋查詢中的評分設定檔。</span><span class="sxs-lookup"><span data-stu-id="5643a-225">A new class named `ScoringParameter` has been added in the latest SDK to make it easier to provide parameters to scoring profiles in a search query.</span></span> <span data-ttu-id="5643a-226">先前 `SearchParameters` 類別的 `ScoringProfiles` 屬性的類型是 `IList<string>`；現在它的類型是 `IList<ScoringParameter>`。</span><span class="sxs-lookup"><span data-stu-id="5643a-226">Previously the `ScoringProfiles` property of the `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="5643a-227">範例</span><span class="sxs-lookup"><span data-stu-id="5643a-227">Example</span></span>
<span data-ttu-id="5643a-228">如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="5643a-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="5643a-229">您可以將其變更如下以修正任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="5643a-229">You can change it to this to fix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="5643a-230">模型類別變更</span><span class="sxs-lookup"><span data-stu-id="5643a-230">Model class changes</span></span>
<span data-ttu-id="5643a-231">由於[作業方法變更](#OperationMethodChanges)中所述的簽章變更，`Microsoft.Azure.Search.Models` 命名空間中的許多類別都已重新命名或移除。</span><span class="sxs-lookup"><span data-stu-id="5643a-231">Due to the signature changes described in [Operation method changes](#OperationMethodChanges), many classes in the `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="5643a-232">例如：</span><span class="sxs-lookup"><span data-stu-id="5643a-232">For example:</span></span>

* <span data-ttu-id="5643a-233">`IndexDefinitionResponse` 已由 `AzureOperationResponse<Index>` 取代</span><span class="sxs-lookup"><span data-stu-id="5643a-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="5643a-234">`DocumentSearchResponse` 已重新命名為 `DocumentSearchResult`</span><span class="sxs-lookup"><span data-stu-id="5643a-234">`DocumentSearchResponse` has been renamed to `DocumentSearchResult`</span></span>
* <span data-ttu-id="5643a-235">`IndexResult` 已重新命名為 `IndexingResult`</span><span class="sxs-lookup"><span data-stu-id="5643a-235">`IndexResult` has been renamed to `IndexingResult`</span></span>
* <span data-ttu-id="5643a-236">`Documents.Count()` 現在會傳回 `long`，具有文件計數而不是 `DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="5643a-236">`Documents.Count()` now returns a `long` with the document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="5643a-237">`IndexGetStatisticsResponse` 已重新命名為 `IndexGetStatisticsResult`</span><span class="sxs-lookup"><span data-stu-id="5643a-237">`IndexGetStatisticsResponse` has been renamed to `IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="5643a-238">`IndexListResponse` 已重新命名為 `IndexListResult`</span><span class="sxs-lookup"><span data-stu-id="5643a-238">`IndexListResponse` has been renamed to `IndexListResult`</span></span>

<span data-ttu-id="5643a-239">總而言之，已存在的 `OperationResponse`衍生類別只是用來包裝已移除的模型物件。</span><span class="sxs-lookup"><span data-stu-id="5643a-239">To summarize, `OperationResponse`-derived classes that existed only to wrap a model object have been removed.</span></span> <span data-ttu-id="5643a-240">其餘的類別已將其尾碼從 `Response` 變更為 `Result`。</span><span class="sxs-lookup"><span data-stu-id="5643a-240">The remaining classes have had their suffix changed from `Response` to `Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="5643a-241">範例</span><span class="sxs-lookup"><span data-stu-id="5643a-241">Example</span></span>
<span data-ttu-id="5643a-242">如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="5643a-242">If your code looks like this:</span></span>

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

<span data-ttu-id="5643a-243">您可以將其變更如下以修正任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="5643a-243">You can change it to this to fix any build errors:</span></span>

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

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="5643a-244">回應類別和 IEnumerable</span><span class="sxs-lookup"><span data-stu-id="5643a-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="5643a-245">可能會影響您程式碼的其他變更，就是讓集合不再實作 `IEnumerable<T>`的回應類別。</span><span class="sxs-lookup"><span data-stu-id="5643a-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="5643a-246">您可以改為直接存取集合屬性。</span><span class="sxs-lookup"><span data-stu-id="5643a-246">Instead, you can access the collection property directly.</span></span> <span data-ttu-id="5643a-247">例如，如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="5643a-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="5643a-248">您可以將其變更如下以修正任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="5643a-248">You can change it to this to fix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="5643a-249">Web 應用程式的特殊案例</span><span class="sxs-lookup"><span data-stu-id="5643a-249">Special case for web applications</span></span>
<span data-ttu-id="5643a-250">如果您有 Web 應用程式會直接將 `DocumentSearchResponse` 序列化，以將搜尋結果傳送至瀏覽器，您將需要變更程式碼，否則結果不會正確地序列化。</span><span class="sxs-lookup"><span data-stu-id="5643a-250">If you have a web application that serializes `DocumentSearchResponse` directly to send search results to the browser, you will need to change your code or the results will not serialize correctly.</span></span> <span data-ttu-id="5643a-251">例如，如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="5643a-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="5643a-252">您可以藉由取得搜尋回應的 `.Results` 屬性以修正搜尋結果轉譯，來加以變更：</span><span class="sxs-lookup"><span data-stu-id="5643a-252">You can change it by getting the `.Results` property of the search response to fix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="5643a-253">您必須自行在您的程式碼中尋找這種情況；**編譯器不會警告您**，因為 `JsonResult.Data` 的類型是 `object`。</span><span class="sxs-lookup"><span data-stu-id="5643a-253">You will have to look for such cases in your code yourself; **The compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="5643a-254">CloudException 變更</span><span class="sxs-lookup"><span data-stu-id="5643a-254">CloudException changes</span></span>
<span data-ttu-id="5643a-255">`CloudException` 類別已經從 `Hyak.Common` 命名空間移至 `Microsoft.Rest.Azure` 命名空間。</span><span class="sxs-lookup"><span data-stu-id="5643a-255">The `CloudException` class has moved from the `Hyak.Common` namespace to the `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="5643a-256">此外，`Error` 屬性已重新命名為 `Body`。</span><span class="sxs-lookup"><span data-stu-id="5643a-256">Also, its `Error` property has been renamed to `Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="5643a-257">SearchServiceClient 和 SearchIndexClient 變更</span><span class="sxs-lookup"><span data-stu-id="5643a-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="5643a-258">`Credentials` 屬性的類型已經從 `SearchCredentials` 變更為其基底類別，`ServiceClientCredentials`。</span><span class="sxs-lookup"><span data-stu-id="5643a-258">The type of the `Credentials` property has changed from `SearchCredentials` to its base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="5643a-259">如果您需要存取 `SearchIndexClient` 或 `SearchServiceClient` 的 `SearchCredentials`，請使用新的 `SearchCredentials` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5643a-259">If you need to access the `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use the new `SearchCredentials` property.</span></span>

<span data-ttu-id="5643a-260">在舊版的 SDK 中，`SearchServiceClient` 和 `SearchIndexClient` 有建構函式，會採用 `HttpClient` 參數。</span><span class="sxs-lookup"><span data-stu-id="5643a-260">In older versions of the SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="5643a-261">這些建構函式已由使用 `HttpClientHandler` 的建構函式和 `DelegatingHandler` 物件的陣列取代。</span><span class="sxs-lookup"><span data-stu-id="5643a-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="5643a-262">如此可讓在需要時將自訂處理常式安裝至前置處理 HTTP 要求更加簡易。</span><span class="sxs-lookup"><span data-stu-id="5643a-262">This makes it easier to install custom handlers to pre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="5643a-263">最後，採用 `Uri` 和 `SearchCredentials` 的建構函式已變更。</span><span class="sxs-lookup"><span data-stu-id="5643a-263">Finally, the constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="5643a-264">例如，如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="5643a-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="5643a-265">您可以將其變更如下以修正任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="5643a-265">You can change it to this to fix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="5643a-266">另外請注意，認證參數的類型已變更為 `ServiceClientCredentials`。</span><span class="sxs-lookup"><span data-stu-id="5643a-266">Also note that the type of the credentials parameter has changed to `ServiceClientCredentials`.</span></span> <span data-ttu-id="5643a-267">這不會影響您的程式碼，因為 `SearchCredentials` 衍生自 `ServiceClientCredentials`。</span><span class="sxs-lookup"><span data-stu-id="5643a-267">This is unlikely to affect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="5643a-268">傳送要求 ID</span><span class="sxs-lookup"><span data-stu-id="5643a-268">Passing a request ID</span></span>
<span data-ttu-id="5643a-269">在較舊版本的 SDK 中，您可以在 `SearchServiceClient` 或 `SearchIndexClient` 上設定要求 ID，且它會納入 REST API 的每個要求中。</span><span class="sxs-lookup"><span data-stu-id="5643a-269">In older versions of the SDK, you could set a request ID on the `SearchServiceClient` or `SearchIndexClient` and it would be included in every request to the REST API.</span></span> <span data-ttu-id="5643a-270">如果您需要連絡支援人員，疑難排解搜尋服務的問題時，相當有用。</span><span class="sxs-lookup"><span data-stu-id="5643a-270">This is useful for troubleshooting issues with your search service if you need to contact support.</span></span> <span data-ttu-id="5643a-271">不過，為每個作業設定唯一要求 ID 更加有用，而不是對所有作業使用相同 ID。</span><span class="sxs-lookup"><span data-stu-id="5643a-271">However, it is more useful to set a unique request ID for every operation rather than to use the same ID for all operations.</span></span> <span data-ttu-id="5643a-272">基於這個原因，`SearchServiceClient` 和 `SearchIndexClient` 的 `SetClientRequestId` 方法已移除。</span><span class="sxs-lookup"><span data-stu-id="5643a-272">For this reason, the `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="5643a-273">您可以改為透過選擇性 `SearchRequestOptions` 參數將要求 ID 傳送給每個作業方法。</span><span class="sxs-lookup"><span data-stu-id="5643a-273">Instead, you can pass a request ID to each operation method via the optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="5643a-274">在未來的 SDK 版本中，我們會新增新機制，在用戶端物件上全域設定要求 ID，與其他 Azure SDK 所使用的方法一致。</span><span class="sxs-lookup"><span data-stu-id="5643a-274">In a future release of the SDK, we will add a new mechanism for setting a request ID globally on the client objects that is consistent with the approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="5643a-275">範例</span><span class="sxs-lookup"><span data-stu-id="5643a-275">Example</span></span>
<span data-ttu-id="5643a-276">如果您的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="5643a-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="5643a-277">您可以將其變更如下以修正任何建置錯誤：</span><span class="sxs-lookup"><span data-stu-id="5643a-277">You can change it to this to fix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="5643a-278">介面名稱變更</span><span class="sxs-lookup"><span data-stu-id="5643a-278">Interface name changes</span></span>
<span data-ttu-id="5643a-279">作業群組介面名稱皆已變更，與其對應的屬性名稱一致：</span><span class="sxs-lookup"><span data-stu-id="5643a-279">The operation group interface names have all changed to be consistent with their corresponding property names:</span></span>

* <span data-ttu-id="5643a-280">`ISearchServiceClient.Indexes` 的類型已從 `IIndexOperations` 重新命名為 `IIndexesOperations`。</span><span class="sxs-lookup"><span data-stu-id="5643a-280">The type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` to `IIndexesOperations`.</span></span>
* <span data-ttu-id="5643a-281">`ISearchServiceClient.Indexers` 的類型已從 `IIndexerOperations` 重新命名為 `IIndexersOperations`。</span><span class="sxs-lookup"><span data-stu-id="5643a-281">The type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` to `IIndexersOperations`.</span></span>
* <span data-ttu-id="5643a-282">`ISearchServiceClient.DataSources` 的類型已從 `IDataSourceOperations` 重新命名為 `IDataSourcesOperations`。</span><span class="sxs-lookup"><span data-stu-id="5643a-282">The type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` to `IDataSourcesOperations`.</span></span>
* <span data-ttu-id="5643a-283">`ISearchIndexClient.Documents` 的類型已從 `IDocumentOperations` 重新命名為 `IDocumentsOperations`。</span><span class="sxs-lookup"><span data-stu-id="5643a-283">The type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` to `IDocumentsOperations`.</span></span>

<span data-ttu-id="5643a-284">這項變更不會影響您的程式碼，除非您針對測試目的建立這些介面的模擬。</span><span class="sxs-lookup"><span data-stu-id="5643a-284">This change is unlikely to affect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="5643a-285">版本 1.1 的錯誤修正</span><span class="sxs-lookup"><span data-stu-id="5643a-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="5643a-286">在舊版的 Azure 搜尋服務 .NET SDK 中，有與自訂模型類別的序列化相關的錯誤。</span><span class="sxs-lookup"><span data-stu-id="5643a-286">There was a bug in older versions of the Azure Search .NET SDK relating to serialization of custom model classes.</span></span> <span data-ttu-id="5643a-287">如果您建立具有不可為 null 值類型的屬性的自訂模型類別，可能會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="5643a-287">The bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-to-reproduce"></a><span data-ttu-id="5643a-288">重現的步驟</span><span class="sxs-lookup"><span data-stu-id="5643a-288">Steps to reproduce</span></span>
<span data-ttu-id="5643a-289">建立具有不可為 null 值類型的屬性的自訂模型類別。</span><span class="sxs-lookup"><span data-stu-id="5643a-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="5643a-290">例如，加入類型 `int` 而不是 `int?` 的公用 `UnitCount` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5643a-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="5643a-291">如果要使用該類型的預設值編製文件的索引 (例如， `int`的 0)，欄位在 Azure 搜尋服務中將會是 null。</span><span class="sxs-lookup"><span data-stu-id="5643a-291">If you index a document with the default value of that type (for example, 0 for `int`), the field will be null in Azure Search.</span></span> <span data-ttu-id="5643a-292">如果您後續搜尋該文件，`Search` 呼叫將會擲回 `JsonSerializationException`，提報它無法將 `null` 轉換為 `int`。</span><span class="sxs-lookup"><span data-stu-id="5643a-292">If you subsequently search for that document, the `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` to `int`.</span></span>

<span data-ttu-id="5643a-293">此外，篩選可能無法如預期般執行，因為 null 被寫入索引，而不是預期的值。</span><span class="sxs-lookup"><span data-stu-id="5643a-293">Also, filters may not work as expected since null was written to the index instead of the intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="5643a-294">修正詳細資料</span><span class="sxs-lookup"><span data-stu-id="5643a-294">Fix details</span></span>
<span data-ttu-id="5643a-295">我們已在 SDK 的版本 1.1 中修正此問題。</span><span class="sxs-lookup"><span data-stu-id="5643a-295">We have fixed this issue in version 1.1 of the SDK.</span></span> <span data-ttu-id="5643a-296">現在，如果您有一個如下的模型類別：</span><span class="sxs-lookup"><span data-stu-id="5643a-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="5643a-297">而且您將 `IntValue` 設定為 0，該值現在會在線路上正確序列化為 0，並且在索引中儲存為 0。</span><span class="sxs-lookup"><span data-stu-id="5643a-297">and you set `IntValue` to 0, that value is now correctly serialized as 0 on the wire and stored as 0 in the index.</span></span> <span data-ttu-id="5643a-298">來回行程也如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="5643a-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="5643a-299">這種方法有一個需要注意的可能問題：如果您使用具有不可為 null 屬性的模型類型，您必須保證  索引中沒有任何文件對於對應欄位包含 null 值。</span><span class="sxs-lookup"><span data-stu-id="5643a-299">There is one potential issue to be aware of with this approach: If you use a model type with a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="5643a-300">SDK 和 Azure 搜尋服務 REST API 都不會協助您強制執行。</span><span class="sxs-lookup"><span data-stu-id="5643a-300">Neither the SDK nor the Azure Search REST API will help you to enforce this.</span></span>

<span data-ttu-id="5643a-301">這不只是假設性的問題：如果您在類型為 `Edm.Int32` 的現有索引中新增欄位，</span><span class="sxs-lookup"><span data-stu-id="5643a-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="5643a-302">更新索引定義之後，所有文件對於該新的欄位具有 null 值 (因為所有類型在 Azure 搜尋服務中都可為 null)。</span><span class="sxs-lookup"><span data-stu-id="5643a-302">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="5643a-303">如果您接著對該欄位使用 `int` 屬性不可為 Null 的模型類別，就會在嘗試擷取文件時得到類似這樣的 `JsonSerializationException`：</span><span class="sxs-lookup"><span data-stu-id="5643a-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="5643a-304">基於這個原因，我們仍然建議您在模型類別中使用可為 null 的類型做為最佳作法。</span><span class="sxs-lookup"><span data-stu-id="5643a-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="5643a-305">如需有關此錯誤和修正的詳細資訊，請參閱 [GitHub 上的這個問題](https://github.com/Azure/azure-sdk-for-net/issues/1063)。</span><span class="sxs-lookup"><span data-stu-id="5643a-305">For more details on this bug and the fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

