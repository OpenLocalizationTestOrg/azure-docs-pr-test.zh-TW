---
<span data-ttu-id="22d82-101">標題： aaa 」 教學課程： hello 入口網站中建立第一個的 Azure 搜尋索引 |Microsoft 文件"描述： hello Azure 入口網站，在使用預先定義的範例資料 toogenerate 索引。</span><span class="sxs-lookup"><span data-stu-id="22d82-101">title: aaa"Tutorial: Create your first Azure Search index in hello portal | Microsoft Docs" description: In hello Azure portal, use predefined sample data toogenerate an index.</span></span> <span data-ttu-id="22d82-102">探索全文檢索搜尋、篩選器、面向、模糊搜尋、地理搜尋功能等等。</span><span class="sxs-lookup"><span data-stu-id="22d82-102">Explore full text search, filters, facets, fuzzy search, geosearch, and more.</span></span>
<span data-ttu-id="22d82-103">服務： 搜尋 documentationcenter: '作者： HeidiSteen 管理員： jhubbard 編輯器:' 標記： azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="22d82-103">services: search documentationcenter: '' author: HeidiSteen manager: jhubbard editor: '' tags: azure-portal</span></span>

<span data-ttu-id="22d82-104">ms.assetid: 21adc351-69bb-4a39-bc59-598c60c8f958 ms.service： 搜尋 ms.devlang: na ms.workload： 搜尋 ms.topic： 英雄文章 ms.tgt_pltfrm: na ms.date: 06/26/2017 ms.author: heidist</span><span class="sxs-lookup"><span data-stu-id="22d82-104">ms.assetid: 21adc351-69bb-4a39-bc59-598c60c8f958 ms.service: search ms.devlang: na ms.workload: search ms.topic: hero-article ms.tgt_pltfrm: na ms.date: 06/26/2017 ms.author: heidist</span></span>

---
# <a name="tutorial-create-your-first-azure-search-index-in-hello-portal"></a><span data-ttu-id="22d82-105">教學課程： Hello 入口網站中建立第一個的 Azure 搜尋索引</span><span class="sxs-lookup"><span data-stu-id="22d82-105">Tutorial: Create your first Azure Search index in hello portal</span></span>

<span data-ttu-id="22d82-106">在 hello Azure 入口網站，開始使用預先定義的範例資料集 tooquickly 產生使用 hello 索引**匯入資料**精靈。</span><span class="sxs-lookup"><span data-stu-id="22d82-106">In hello Azure portal, start with a predefined sample dataset tooquickly generate an index using hello **Import data** wizard.</span></span> <span data-ttu-id="22d82-107">使用**搜尋總管**探索全文檢索搜尋、篩選器、面向、模糊搜尋和地理搜尋功能。</span><span class="sxs-lookup"><span data-stu-id="22d82-107">Explore full text search, filters, facets, fuzzy search, and geosearch with **Search explorer**.</span></span>  

<span data-ttu-id="22d82-108">此無程式碼的簡介，讓您從預先定義的資料著手，以便立即撰寫有趣的查詢。</span><span class="sxs-lookup"><span data-stu-id="22d82-108">This code-free introduction gets you started with predefined data so that you can write interesting queries right away.</span></span> <span data-ttu-id="22d82-109">雖然入口網站工具無法取代程式碼，但很適合用於下列工作︰</span><span class="sxs-lookup"><span data-stu-id="22d82-109">While portal tools are not a substitute for code, tools are useful for these tasks:</span></span>

+ <span data-ttu-id="22d82-110">產品量產時間最短的實際操作學習</span><span class="sxs-lookup"><span data-stu-id="22d82-110">Hands on learning with minimal ramp-up</span></span>
+ <span data-ttu-id="22d82-111">在 [匯入資料] 中撰寫程式碼前，先設定索引的原型</span><span class="sxs-lookup"><span data-stu-id="22d82-111">Prototype an index before you write code in **Import data**</span></span>
+ <span data-ttu-id="22d82-112">在 [搜尋總管] 中測試查詢和剖析器語法</span><span class="sxs-lookup"><span data-stu-id="22d82-112">Test queries and parser syntax in **Search explorer**</span></span>
+ <span data-ttu-id="22d82-113">檢視現有的索引已發行的 tooyour 服務並尋找其屬性</span><span class="sxs-lookup"><span data-stu-id="22d82-113">View an existing index published tooyour service and look up its attributes</span></span>

<span data-ttu-id="22d82-114">**估計時間︰**大約 15 分鐘，但如果還需要註冊帳戶或服務，則時間較長。</span><span class="sxs-lookup"><span data-stu-id="22d82-114">**Time Estimate:** About 15 minutes, but longer if account or service sign-up is also required.</span></span> 

<span data-ttu-id="22d82-115">或者，使用專業[Azure 搜尋.NET 中的程式碼為基礎的簡介 tooprogramming](search-howto-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="22d82-115">Alternatively, ramp up using a [code-based introduction tooprogramming Azure Search in .NET](search-howto-dotnet-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22d82-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="22d82-116">Prerequisites</span></span>

<span data-ttu-id="22d82-117">本教學課程會採用 [Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)和 [Azure 搜尋服務](search-create-service-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="22d82-117">This tutorial assumes an [Azure subscription](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) and [Azure Search service](search-create-service-portal.md).</span></span> 

<span data-ttu-id="22d82-118">如果您不立即想 tooprovision 服務，您可以觀看的 hello 6 分鐘示範的步驟在本教學課程中，開始三分鐘到這個[Azure Search 概觀影片](https://channel9.msdn.com/Events/Connect/2016/138)。</span><span class="sxs-lookup"><span data-stu-id="22d82-118">If you don't want tooprovision a service immediately, you can watch a 6-minute demonstration of hello steps in this tutorial, starting at about three minutes into this [Azure Search Overview video](https://channel9.msdn.com/Events/Connect/2016/138).</span></span>

## <a name="find-your-service"></a><span data-ttu-id="22d82-119">尋找您的服務</span><span class="sxs-lookup"><span data-stu-id="22d82-119">Find your service</span></span>
1. <span data-ttu-id="22d82-120">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="22d82-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="22d82-121">開啟您的 Azure 搜尋服務的 hello 服務儀表板。</span><span class="sxs-lookup"><span data-stu-id="22d82-121">Open hello service dashboard of your Azure Search service.</span></span> <span data-ttu-id="22d82-122">如果您未釘選 hello 服務磚 tooyour 儀表板，您可以找到您的服務在這種方式：</span><span class="sxs-lookup"><span data-stu-id="22d82-122">If you didn't pin hello service tile tooyour dashboard, you can find your service this way:</span></span> 
   
   * <span data-ttu-id="22d82-123">在 hello Jumpbar，按一下 **更多服務**在 hello hello 左側瀏覽窗格的底部。</span><span class="sxs-lookup"><span data-stu-id="22d82-123">In hello Jumpbar, click **More services** at hello bottom of hello left navigation pane.</span></span>
   * <span data-ttu-id="22d82-124">在 [hello] 搜尋方塊中，輸入*搜尋*tooget 訂用帳戶服務的搜尋清單。</span><span class="sxs-lookup"><span data-stu-id="22d82-124">In hello search box, type *search* tooget a list of search services for your subscription.</span></span> <span data-ttu-id="22d82-125">Hello 清單應會顯示您的服務。</span><span class="sxs-lookup"><span data-stu-id="22d82-125">Your service should appear in hello list.</span></span> 

## <a name="check-for-space"></a><span data-ttu-id="22d82-126">檢查空間</span><span class="sxs-lookup"><span data-stu-id="22d82-126">Check for space</span></span>
<span data-ttu-id="22d82-127">許多客戶開始 hello 免費服務。</span><span class="sxs-lookup"><span data-stu-id="22d82-127">Many customers start with hello free service.</span></span> <span data-ttu-id="22d82-128">這個版本是有限的 toothree 索引、 三個資料來源，以及三個索引子。</span><span class="sxs-lookup"><span data-stu-id="22d82-128">This version is limited toothree indexes, three data sources, and three indexers.</span></span> <span data-ttu-id="22d82-129">開始之前，請先確定您有空間可容納額外的項目。</span><span class="sxs-lookup"><span data-stu-id="22d82-129">Make sure you have room for extra items before you begin.</span></span> <span data-ttu-id="22d82-130">本教學課程會建立各一個物件。</span><span class="sxs-lookup"><span data-stu-id="22d82-130">This tutorial creates one of each object.</span></span> 

> [!TIP] 
> <span data-ttu-id="22d82-131">Hello 服務儀表板上的磚會顯示多少索引、 索引子和資料來源您已經有。</span><span class="sxs-lookup"><span data-stu-id="22d82-131">Tiles on hello service dashboard show how many indexes, indexers, and data sources you already have.</span></span> <span data-ttu-id="22d82-132">hello 索引子的磚會顯示成功和失敗的指標。</span><span class="sxs-lookup"><span data-stu-id="22d82-132">hello Indexer tile shows success and failure indicators.</span></span> <span data-ttu-id="22d82-133">按一下 hello 磚 tooview hello 索引子計數。</span><span class="sxs-lookup"><span data-stu-id="22d82-133">Click hello tile tooview hello indexer count.</span></span> 
>
> ![索引子和資料來源的圖格][1]
>

## <span data-ttu-id="22d82-135"><a name="create-index"></a> 建立索引和載入資料</span><span class="sxs-lookup"><span data-stu-id="22d82-135"><a name="create-index"></a> Create an index and load data</span></span>
<span data-ttu-id="22d82-136">搜尋查詢會逐一查看索引  ，其中包含用來最佳化特定搜尋行為的可搜尋資料、中繼資料及建構。</span><span class="sxs-lookup"><span data-stu-id="22d82-136">Search queries iterate over an *index* containing searchable data, metadata, and constructs used for optimizing certain search behaviors.</span></span>

<span data-ttu-id="22d82-137">tookeep 這個入口網站為基礎的工作中，我們會使用內建的範例資料集可以使用索引子透過 hello 編目**匯入資料**精靈。</span><span class="sxs-lookup"><span data-stu-id="22d82-137">tookeep this task portal-based, we use a built-in sample dataset that can be crawled using an indexer via hello **Import data** wizard.</span></span> 

#### <a name="step-1-start-hello-import-data-wizard"></a><span data-ttu-id="22d82-138">步驟 1： 啟動 hello 匯入資料精靈</span><span class="sxs-lookup"><span data-stu-id="22d82-138">Step 1: Start hello Import data wizard</span></span>
1. <span data-ttu-id="22d82-139">Azure 搜尋服務儀表板上，按一下 **匯入資料**hello 命令列 toostart 精靈，同時建立並填入索引中。</span><span class="sxs-lookup"><span data-stu-id="22d82-139">On your Azure Search service dashboard, click **Import data** in hello command bar toostart a wizard that both creates and populates an index.</span></span>
   
    ![匯入資料命令][2]

2. <span data-ttu-id="22d82-141">在 hello 精靈 中，按一下 **資料來源** > **範例** > **realestate-我們為範例**。</span><span class="sxs-lookup"><span data-stu-id="22d82-141">In hello wizard, click **Data Source** > **Samples** > **realestate-us-sample**.</span></span> <span data-ttu-id="22d82-142">此資料來源已預先設定名稱、類型和連線資訊。</span><span class="sxs-lookup"><span data-stu-id="22d82-142">This data source is preconfigured with a name, type, and connection information.</span></span> <span data-ttu-id="22d82-143">一旦建立，就會變成可在其他匯入作業中重複使用的「現有資料來源」。</span><span class="sxs-lookup"><span data-stu-id="22d82-143">Once created, it becomes an "existing data source" that can be reused in other import operations.</span></span>

    ![選取範例資料集][9]

3. <span data-ttu-id="22d82-145">按一下**確定**toouse 它。</span><span class="sxs-lookup"><span data-stu-id="22d82-145">Click **OK** toouse it.</span></span>

#### <a name="step-2-define-hello-index"></a><span data-ttu-id="22d82-146">步驟 2： 定義 hello 索引</span><span class="sxs-lookup"><span data-stu-id="22d82-146">Step 2: Define hello index</span></span>
<span data-ttu-id="22d82-147">建立索引通常會是手動和程式碼為基礎，但 hello 精靈可能會產生任何資料來源，它可以搜耙的索引。</span><span class="sxs-lookup"><span data-stu-id="22d82-147">Creating an index is typically manual and code-based, but hello wizard can generate an index for any data source it can crawl.</span></span> <span data-ttu-id="22d82-148">至少具有一個欄位標示為 hello 文件索引鍵 toouniquely 識別每個文件，索引需要名稱和欄位集合。</span><span class="sxs-lookup"><span data-stu-id="22d82-148">Minimally, an index requires a name, and a fields collection, with one field marked as hello document key toouniquely identify each document.</span></span>

<span data-ttu-id="22d82-149">欄位具有資料類型和屬性。</span><span class="sxs-lookup"><span data-stu-id="22d82-149">Fields have data types and attributes.</span></span> <span data-ttu-id="22d82-150">hello hello 頂端的核取方塊是*屬性索引*控制 hello 欄位的使用方式。</span><span class="sxs-lookup"><span data-stu-id="22d82-150">hello check boxes across hello top are *index attributes* controlling how hello field is used.</span></span> 

* <span data-ttu-id="22d82-151"> 表示它會出現在搜尋結果清單中。</span><span class="sxs-lookup"><span data-stu-id="22d82-151">**Retrievable** means that it shows up in search results list.</span></span> <span data-ttu-id="22d82-152">例如當欄位僅使用於篩選運算式時，您可以清除此核取方塊，將個別欄位標記為關閉搜尋結果的限制。</span><span class="sxs-lookup"><span data-stu-id="22d82-152">You can mark individual fields as off limits for search results by clearing this checkbox, for example when fields used only in filter expressions.</span></span> 
* <span data-ttu-id="22d82-153">[可篩選]、[可排序] 和 [可面向化] 判斷欄位是否可以用於篩選、排序或多面向導覽結構。</span><span class="sxs-lookup"><span data-stu-id="22d82-153">**Filterable**, **Sortable**, and **Facetable** determine whether a field can be used in a filter, a sort, or a facet navigation structure.</span></span> 
* <span data-ttu-id="22d82-154"> 表示欄位包含在全文檢索搜尋中。</span><span class="sxs-lookup"><span data-stu-id="22d82-154">**Searchable** means that a field is included in full text search.</span></span> <span data-ttu-id="22d82-155">字串可以搜尋。</span><span class="sxs-lookup"><span data-stu-id="22d82-155">Strings are searchable.</span></span> <span data-ttu-id="22d82-156">數字欄位和布林值欄位通常會標示為不可搜尋。</span><span class="sxs-lookup"><span data-stu-id="22d82-156">Numeric fields and Boolean fields are often marked as not searchable.</span></span> 

<span data-ttu-id="22d82-157">根據預設，hello 精靈會掃描為 hello 索引鍵欄位的 hello 基礎 hello 資料來源的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="22d82-157">By default, hello wizard scans hello data source for unique identifiers as hello basis for hello key field.</span></span> <span data-ttu-id="22d82-158">字串具有可擷取和可搜尋的特性。</span><span class="sxs-lookup"><span data-stu-id="22d82-158">Strings are attributed as retrievable and searchable.</span></span> <span data-ttu-id="22d82-159">整數具有可擷取、可篩選、可排序和可 Fact 處理的特性。</span><span class="sxs-lookup"><span data-stu-id="22d82-159">Integers are attributed as retrievable, filterable, sortable, and facetable.</span></span>

  ![產生的 realestate 索引][3]

<span data-ttu-id="22d82-161">按一下**確定**toocreate hello 索引。</span><span class="sxs-lookup"><span data-stu-id="22d82-161">Click **OK** toocreate hello index.</span></span>

#### <a name="step-3-define-hello-indexer"></a><span data-ttu-id="22d82-162">步驟 3： 定義 hello 索引子</span><span class="sxs-lookup"><span data-stu-id="22d82-162">Step 3: Define hello indexer</span></span>
<span data-ttu-id="22d82-163">仍在 hello**匯入資料**精靈] 中，按一下 [**索引子** > **名稱**，然後輸入 hello 索引子的名稱。</span><span class="sxs-lookup"><span data-stu-id="22d82-163">Still in hello **Import data** wizard, click **Indexer** > **Name**, and type a name for hello indexer.</span></span> 

<span data-ttu-id="22d82-164">此物件定義可執行的程序。</span><span class="sxs-lookup"><span data-stu-id="22d82-164">This object defines an executable process.</span></span> <span data-ttu-id="22d82-165">您無法將它放循環的排程，但現在使用 hello 預設選項 toorun hello 索引子之後立即，當您按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="22d82-165">You could put it on recurring schedule, but for now use hello default option toorun hello indexer once, immediately, when you click **OK**.</span></span>  

  ![realestate 索引子][8]

## <a name="check-progress"></a><span data-ttu-id="22d82-167">檢查進度</span><span class="sxs-lookup"><span data-stu-id="22d82-167">Check progress</span></span>
<span data-ttu-id="22d82-168">toomonitor 資料匯入，請返回 toohello 服務儀表板、 向下捲動並按兩下 hello**索引子**並排 tooopen hello 索引子清單。</span><span class="sxs-lookup"><span data-stu-id="22d82-168">toomonitor data import, go back toohello service dashboard, scroll down, and double-click hello **Indexers** tile tooopen hello indexers list.</span></span> <span data-ttu-id="22d82-169">您應該會看見 hello 新建立的索引子，在 [hello] 清單中，並提供狀態，指出 「 進行中 」 或成功的原因，以及 hello 編製索引的文件的數目。</span><span class="sxs-lookup"><span data-stu-id="22d82-169">You should see hello newly created indexer in hello list, with status indicating "in progress" or success, along with hello number of documents indexed.</span></span>

   ![索引子進度訊息][4]

## <span data-ttu-id="22d82-171"><a name="query-index"></a>查詢 hello 索引</span><span class="sxs-lookup"><span data-stu-id="22d82-171"><a name="query-index"></a> Query hello index</span></span>
<span data-ttu-id="22d82-172">您現在可以準備 tooquery 搜尋索引。</span><span class="sxs-lookup"><span data-stu-id="22d82-172">You now have a search index that's ready tooquery.</span></span> <span data-ttu-id="22d82-173">**搜尋總管**是 hello 入口網站內建查詢工具。</span><span class="sxs-lookup"><span data-stu-id="22d82-173">**Search explorer** is a query tool built into hello portal.</span></span> <span data-ttu-id="22d82-174">它會提供搜尋方塊，以便確認搜尋結果是否如您所預期。</span><span class="sxs-lookup"><span data-stu-id="22d82-174">It provides a search box so that you can verify whether search results are what you expect.</span></span> 

> [!TIP]
> <span data-ttu-id="22d82-175">在 hello [Azure Search 概觀影片](https://channel9.msdn.com/Events/Connect/2016/138)，hello 步驟會示範在 6m08s hello 影片。</span><span class="sxs-lookup"><span data-stu-id="22d82-175">In hello [Azure Search Overview video](https://channel9.msdn.com/Events/Connect/2016/138), hello following steps are demonstrated at 6m08s into hello video.</span></span>
>

1. <span data-ttu-id="22d82-176">按一下**搜尋總管**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="22d82-176">Click **Search explorer** on hello command bar.</span></span>

   ![搜尋總管命令][5]

2. <span data-ttu-id="22d82-178">按一下**變更索引**上 hello 命令列 tooswitch 太*realestate-我們為範例*。</span><span class="sxs-lookup"><span data-stu-id="22d82-178">Click **Change index** on hello command bar tooswitch too*realestate-us-sample*.</span></span>

   ![索引和 API 命令][6]

3. <span data-ttu-id="22d82-180">按一下**設定 API 版本**hello REST Api 可用的命令列 toosee 上。</span><span class="sxs-lookup"><span data-stu-id="22d82-180">Click **Set API version** on hello command bar toosee which REST APIs are available.</span></span> <span data-ttu-id="22d82-181">預覽應用程式開發介面可讓您存取 toonew 功能通常尚未發行。</span><span class="sxs-lookup"><span data-stu-id="22d82-181">Preview APIs give you access toonew features not yet generally released.</span></span> <span data-ttu-id="22d82-182">除非另有指示 hello 查詢下方，使用 hello 上市版 (2016年-09-01)。</span><span class="sxs-lookup"><span data-stu-id="22d82-182">For hello queries below, use hello generally available version (2016-09-01) unless directed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="22d82-183">[Azure 搜尋 REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents)和 hello [.NET 程式庫](search-howto-dotnet-sdk.md#core-scenarios)完全相同，但**搜尋總管**是配備的 toohandle REST 呼叫。</span><span class="sxs-lookup"><span data-stu-id="22d82-183">[Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents) and hello [.NET library](search-howto-dotnet-sdk.md#core-scenarios) are fully equivalent, but **Search explorer** is only equipped toohandle REST calls.</span></span> <span data-ttu-id="22d82-184">它可接受兩個語法[簡單查詢語法](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)和[完整 Lucene 查詢剖析器](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)，加上所有 hello 中可用的搜尋參數[搜尋文件](https://docs.microsoft.com/rest/api/searchservice/search-documents)作業。</span><span class="sxs-lookup"><span data-stu-id="22d82-184">It accepts syntax for both [simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) and [full Lucene query parser](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), plus all hello search parameters available in [Search Document](https://docs.microsoft.com/rest/api/searchservice/search-documents) operations.</span></span>
    > 

4. <span data-ttu-id="22d82-185">在 hello 搜尋列中，輸入以下的 hello 查詢字串，然後按一下**搜尋**。</span><span class="sxs-lookup"><span data-stu-id="22d82-185">In hello search bar, enter hello query strings below and click **Search**.</span></span>

  ![搜尋查詢範例][7]

**`search=seattle`**

+ <span data-ttu-id="22d82-187">hello`search`參數是使用的 tooinput 關鍵字搜尋的全文檢索搜尋，在此情況下，傳回在國王郡，華盛頓州的清單，其中包含*西雅圖*hello 文件中任何可搜尋的欄位。</span><span class="sxs-lookup"><span data-stu-id="22d82-187">hello `search` parameter is used tooinput a keyword search for full text search, in this case, returning listings in King County, Washington state, containing *Seattle* in any searchable field in hello document.</span></span> 

+ <span data-ttu-id="22d82-188">**搜尋總管**會傳回結果在 JSON 中，這是詳細資訊和固定 tooread 文件有密集的結構。</span><span class="sxs-lookup"><span data-stu-id="22d82-188">**Search explorer** returns results in JSON, which is verbose and hard tooread if documents have a dense structure.</span></span> <span data-ttu-id="22d82-189">根據您的文件，您可能需要 toowrite 程式碼控制代碼搜尋結果 tooextract 重要的項目。</span><span class="sxs-lookup"><span data-stu-id="22d82-189">Depending on your documents, you might need toowrite code that handles search results tooextract important elements.</span></span> 

+ <span data-ttu-id="22d82-190">文件所組成標示為可擷取 hello 索引中的所有欄位。</span><span class="sxs-lookup"><span data-stu-id="22d82-190">Documents are composed of all fields marked as retrievable in hello index.</span></span> <span data-ttu-id="22d82-191">tooview 索引屬性，在 hello 入口網站按一下*realestate-我們為範例*在 hello**索引**磚。</span><span class="sxs-lookup"><span data-stu-id="22d82-191">tooview index attributes in hello portal, click *realestate-us-sample* in hello **Indexes** tile.</span></span>

**`search=seattle&$count=true&$top=100`**

+ <span data-ttu-id="22d82-192">hello`&`符號就是使用的 tooappend 搜尋參數，可以依照任何順序指定。</span><span class="sxs-lookup"><span data-stu-id="22d82-192">hello `&` symbol is used tooappend search parameters, which can be specified in any order.</span></span> 

+  <span data-ttu-id="22d82-193">hello`$count=true`參數會傳回所有傳回的文件的 hello 總和的計數。</span><span class="sxs-lookup"><span data-stu-id="22d82-193">hello `$count=true` parameter returns a count for hello sum of all documents returned.</span></span> <span data-ttu-id="22d82-194">您可以藉由監視 `$count=true` 所報告的變更來驗證篩選查詢。</span><span class="sxs-lookup"><span data-stu-id="22d82-194">You can verify filter queries by monitoring changes reported by `$count=true`.</span></span> 

+ <span data-ttu-id="22d82-195">hello`$top=100`傳回 hello 最高排名 hello 總計超出 100 文件。</span><span class="sxs-lookup"><span data-stu-id="22d82-195">hello `$top=100` returns hello highest ranked 100 documents out of hello total.</span></span> <span data-ttu-id="22d82-196">根據預設，Azure 搜尋會傳回 hello 前 50 個最符合項目。</span><span class="sxs-lookup"><span data-stu-id="22d82-196">By default, Azure Search returns hello first 50 best matches.</span></span> <span data-ttu-id="22d82-197">您可以增加或減少從傳送嗨量`$top`。</span><span class="sxs-lookup"><span data-stu-id="22d82-197">You can increase or decrease hello amount via `$top`.</span></span>

**`search=*&facet=city&$top=2`**

+ <span data-ttu-id="22d82-198">`search=*` 是空的搜尋。</span><span class="sxs-lookup"><span data-stu-id="22d82-198">`search=*` is an empty search.</span></span> <span data-ttu-id="22d82-199">空的搜尋會搜尋所有一切。</span><span class="sxs-lookup"><span data-stu-id="22d82-199">Empty searches search over everything.</span></span> <span data-ttu-id="22d82-200">送出空的查詢太篩選器或 facet hello 完整資料集的文件的其中一個原因。</span><span class="sxs-lookup"><span data-stu-id="22d82-200">One reason for submitting an empty query is too filter or facet over hello complete set of documents.</span></span> <span data-ttu-id="22d82-201">例如，您會想 hello 索引中的所有城市 faceting 導覽結構 tooconsist。</span><span class="sxs-lookup"><span data-stu-id="22d82-201">For example, you want a faceting navigation structure tooconsist of all cities in hello index.</span></span>

+  <span data-ttu-id="22d82-202">`facet`瀏覽傳回結構，您可以將 tooa UI 控制項。</span><span class="sxs-lookup"><span data-stu-id="22d82-202">`facet` returns a navigation structure that you can pass tooa UI control.</span></span> <span data-ttu-id="22d82-203">它會傳回一些類別和一個計數。</span><span class="sxs-lookup"><span data-stu-id="22d82-203">It returns categories and a count.</span></span> <span data-ttu-id="22d82-204">在此情況下，類別根據 hello 數字的城市。</span><span class="sxs-lookup"><span data-stu-id="22d82-204">In this case, categories are based on hello number of cities.</span></span> <span data-ttu-id="22d82-205">在 Azure 搜尋服務中沒有彙總功能，但您可以透過 `facet` 模擬彙總，其可提供各類別中的文件計數。</span><span class="sxs-lookup"><span data-stu-id="22d82-205">There is no aggregation in Azure Search, but you can approximate aggregation via `facet`, which gives a count of documents in each category.</span></span>

+ <span data-ttu-id="22d82-206">`$top=2`取回兩份文件，說明您可以使用`top`tooboth 減少或增加結果。</span><span class="sxs-lookup"><span data-stu-id="22d82-206">`$top=2` brings back two documents, illustrating that you can use `top` tooboth reduce or increase results.</span></span>

**`search=seattle&facet=beds`**

+ <span data-ttu-id="22d82-207">此查詢是 beds 的面向，以 Seattle 的文字搜尋為基礎。</span><span class="sxs-lookup"><span data-stu-id="22d82-207">This query is facet for beds, on a text search for *Seattle*.</span></span> <span data-ttu-id="22d82-208">`"beds"`指定 facet hello 欄位會標示為可擷取、 可篩選，因此可進行 facet 處理 hello 索引和 hello 值它包含 （數字，1 到 5）、 適用於分類成群組 （3 房間，4 個房間的清單） 的清單。</span><span class="sxs-lookup"><span data-stu-id="22d82-208">`"beds"` can be specified as a facet because hello field is marked as retrievable, filterable, and facetable in hello index, and hello values it contains (numeric, 1 through 5), are suitable for categorizing listings into groups (listings with 3 bedrooms, 4 bedrooms).</span></span> 

+ <span data-ttu-id="22d82-209">只有可篩選的欄位可以面向化。</span><span class="sxs-lookup"><span data-stu-id="22d82-209">Only filterable fields can be faceted.</span></span> <span data-ttu-id="22d82-210">只有可擷取的欄位可以傳回 hello 結果中。</span><span class="sxs-lookup"><span data-stu-id="22d82-210">Only retrievable fields can be returned in hello results.</span></span>

**`search=seattle&$filter=beds gt 3`**

+ <span data-ttu-id="22d82-211">hello`filter`參數會傳回符合您所提供的 hello 準則的結果。</span><span class="sxs-lookup"><span data-stu-id="22d82-211">hello `filter` parameter returns results matching hello criteria you provided.</span></span> <span data-ttu-id="22d82-212">在此情況下，房間大於 3 間。</span><span class="sxs-lookup"><span data-stu-id="22d82-212">In this case, bedrooms greater than 3.</span></span> 

+ <span data-ttu-id="22d82-213">篩選語法是 OData 建構。</span><span class="sxs-lookup"><span data-stu-id="22d82-213">Filter syntax is an OData construction.</span></span> <span data-ttu-id="22d82-214">如需詳細資訊，請參閱[篩選 OData 語法](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search)。</span><span class="sxs-lookup"><span data-stu-id="22d82-214">For more information, see [Filter OData syntax](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search).</span></span>

**`search=granite countertops&highlight=description`**

+ <span data-ttu-id="22d82-215">叫用的反白顯示參考 tooformatting 文字上比對 hello 關鍵字指定相符項目中找到特定的欄位。</span><span class="sxs-lookup"><span data-stu-id="22d82-215">Hit highlighting refers tooformatting on text matching hello keyword, given matches are found in a specific field.</span></span> <span data-ttu-id="22d82-216">如果您的搜尋字詞深埋在描述中，您可以加入叫用的反白顯示 toomake 它更容易 toospot。</span><span class="sxs-lookup"><span data-stu-id="22d82-216">If your search term is deeply buried in a description, you can add hit highlighting toomake it easier toospot.</span></span> <span data-ttu-id="22d82-217">在此情況下，hello 格式化片語`"granite countertops"`是更容易 toosee hello 描述欄位中的。</span><span class="sxs-lookup"><span data-stu-id="22d82-217">In this case, hello formatted phrase `"granite countertops"` is easier toosee in hello description field.</span></span>

**`search=mice&highlight=description`**

+ <span data-ttu-id="22d82-218">全文檢索搜尋會尋找具有類似語意的文字形式。</span><span class="sxs-lookup"><span data-stu-id="22d82-218">Full text search finds word forms with similar semantics.</span></span> <span data-ttu-id="22d82-219">在此情況下，搜尋結果會包含"mouse"，"mice"的回應 tooa 關鍵字搜尋中的滑鼠侵擾家庭的反白顯示的文字。</span><span class="sxs-lookup"><span data-stu-id="22d82-219">In this case, search results contain highlighted text for "mouse", for homes that have mouse infestation, in response tooa keyword search on "mice".</span></span> <span data-ttu-id="22d82-220">不同的形式的 hello 相同字組可以出現在結果，因為語言分析。</span><span class="sxs-lookup"><span data-stu-id="22d82-220">Different forms of hello same word can appear in results because of linguistic analysis.</span></span> 

+ <span data-ttu-id="22d82-221">Azure 搜尋服務支援 Microsoft 和 Lucene 所提供的 56 個分析器。</span><span class="sxs-lookup"><span data-stu-id="22d82-221">Azure Search supports 56 analyzers from both Lucene and Microsoft.</span></span> <span data-ttu-id="22d82-222">使用 Azure 搜尋的 hello 預設值為 hello 標準 Lucene 分析器。</span><span class="sxs-lookup"><span data-stu-id="22d82-222">hello default used by Azure Search is hello standard Lucene analyzer.</span></span> 

**`search=samamish`**

+ <span data-ttu-id="22d82-223">拼錯的字，例如 'samamish' hello Samammish 高原 hello 西雅圖地區的失敗 tooreturn 符合項目在一般搜尋。</span><span class="sxs-lookup"><span data-stu-id="22d82-223">Misspelled words, like 'samamish' for hello Samammish plateau in hello Seattle area, fail tooreturn matches in typical search.</span></span> <span data-ttu-id="22d82-224">toohandle 拼字錯誤，您可以使用模糊的搜尋，hello 下一個範例中所述。</span><span class="sxs-lookup"><span data-stu-id="22d82-224">toohandle misspellings, you can use fuzzy search, described in hello next example.</span></span>

**`search=samamish~&queryType=full`**

+ <span data-ttu-id="22d82-225">當您指定 hello 啟用模糊搜尋`~`符號，然後使用 hello 完整查詢剖析器，它會解譯及正確剖析 hello`~`語法。</span><span class="sxs-lookup"><span data-stu-id="22d82-225">Fuzzy search is enabled when you specify hello `~` symbol and use hello full query parser, which interprets and correctly parses hello `~` syntax.</span></span> 

+ <span data-ttu-id="22d82-226">模糊的搜尋時，使用您選擇進行設定時，就會發生的 hello 完整查詢剖析器`queryType=full`。</span><span class="sxs-lookup"><span data-stu-id="22d82-226">Fuzzy search is available when you opt in for hello full query parser, which occurs when you set `queryType=full`.</span></span> <span data-ttu-id="22d82-227">如需啟用 hello 完整查詢剖析器查詢案例的詳細資訊，請參閱[Lucene 的查詢語法，在 Azure 搜尋](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)。</span><span class="sxs-lookup"><span data-stu-id="22d82-227">For more information about query scenarios enabled by hello full query parser, see [Lucene query syntax in Azure Search](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search).</span></span>

+ <span data-ttu-id="22d82-228">當`queryType`是未指定，會使用 hello 預設簡單查詢剖析器。</span><span class="sxs-lookup"><span data-stu-id="22d82-228">When `queryType` is unspecified, hello default simple query parser is used.</span></span> <span data-ttu-id="22d82-229">hello 簡單查詢剖析器還快，但是如果您需要模糊的搜尋、 規則運算式、 鄰近搜尋或其他進階的查詢類型，您將需要 hello 完整的語法。</span><span class="sxs-lookup"><span data-stu-id="22d82-229">hello simple query parser is faster, but if you require fuzzy search, regular expressions, proximity search, or other advanced query types, you will need hello full syntax.</span></span> 

**`search=*&$count=true&$filter=geo.distance(location,geography'POINT(-122.121513 47.673988)') le 5`**

+ <span data-ttu-id="22d82-230">透過 hello 支援地理空間搜尋[edm。GeographyPoint 資料型別](https://docs.microsoft.com/rest/api/searchservice/supported-data-types)上包含座標的欄位。</span><span class="sxs-lookup"><span data-stu-id="22d82-230">Geospatial search is supported through hello [edm.GeographyPoint data type](https://docs.microsoft.com/rest/api/searchservice/supported-data-types) on a field containing coordinates.</span></span> <span data-ttu-id="22d82-231">地理搜尋是在[篩選 OData 語法](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search)中指定的一種篩選器。</span><span class="sxs-lookup"><span data-stu-id="22d82-231">Geosearch is a type of filter, specified in [Filter OData syntax](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search).</span></span> 

+ <span data-ttu-id="22d82-232">hello 範例查詢會篩選其中結果是少於 5 公里從指定的點 （指定為緯度和經度座標） 位置的資料的所有結果。</span><span class="sxs-lookup"><span data-stu-id="22d82-232">hello example query filters all results for positional data, where results are less than 5 kilometers from a given point (specified as latitude and longitude coordinates).</span></span> <span data-ttu-id="22d82-233">藉由新增`$count`，您可以查看變更 hello 距離或 hello 座標時，會傳回多少的結果。</span><span class="sxs-lookup"><span data-stu-id="22d82-233">By adding `$count`, you can see how many results are returned when you change either hello distance or hello coordinates.</span></span> 

+ <span data-ttu-id="22d82-234">如果搜尋應用程式有「尋找附近地點」功能或使用地圖導航功能，地理空間搜尋便很實用。</span><span class="sxs-lookup"><span data-stu-id="22d82-234">Geospatial search is useful if your search application has a 'find near me' feature or uses map navigation.</span></span> <span data-ttu-id="22d82-235">不過，並不是全文檢索搜尋。</span><span class="sxs-lookup"><span data-stu-id="22d82-235">It is not full text search, however.</span></span> <span data-ttu-id="22d82-236">如果您有依名稱搜尋上縣市或國家/地區的使用者需求，加入包含縣市或國家/地區中的名稱，加法 toocoordinates 欄位。</span><span class="sxs-lookup"><span data-stu-id="22d82-236">If you have user requirements for searching on a city or country by name, add fields containing city or country names, in addition toocoordinates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22d82-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22d82-237">Next steps</span></span>

+ <span data-ttu-id="22d82-238">修改任何 hello 您剛才建立的物件。</span><span class="sxs-lookup"><span data-stu-id="22d82-238">Modify any of hello objects you just created.</span></span> <span data-ttu-id="22d82-239">您一次執行 hello 精靈之後，您可以返回並檢視或修改個別元件： 索引、 索引子或資料來源。</span><span class="sxs-lookup"><span data-stu-id="22d82-239">After you run hello wizard once, you can go back and view or modify individual components: index, indexer, or data source.</span></span> <span data-ttu-id="22d82-240">Hello 索引上不允許某些編輯，例如 hello 變更 hello 欄位資料型別，但大部分的屬性和設定是可修改。</span><span class="sxs-lookup"><span data-stu-id="22d82-240">Some edits, such as hello changing hello field data type, are not allowed on hello index, but most properties and settings are modifiable.</span></span>

  <span data-ttu-id="22d82-241">tooview 個別元件，按一下 hello**索引**，**索引子**，或**資料來源**磚的儀表板 toodisplay 上現有的物件清單。</span><span class="sxs-lookup"><span data-stu-id="22d82-241">tooview individual components, click hello **Index**, **Indexer**, or **Data Sources** tiles on your dashboard toodisplay a list of existing objects.</span></span> <span data-ttu-id="22d82-242">toolearn 深入了解索引編輯不需要重建，請參閱[更新索引 (Azure 搜尋 REST API)](https://docs.microsoft.com/rest/api/searchservice/update-index)。</span><span class="sxs-lookup"><span data-stu-id="22d82-242">toolearn more about index edits that do not require a rebuild, see [Update Index (Azure Search REST API)](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

+ <span data-ttu-id="22d82-243">Hello 工具和其他資料來源的步驟，再試一次。</span><span class="sxs-lookup"><span data-stu-id="22d82-243">Try hello tools and steps with other data sources.</span></span> <span data-ttu-id="22d82-244">hello 範例資料集， `realestate-us-sample`，是從 Azure SQL Database 的 Azure 搜尋可以搜耙。</span><span class="sxs-lookup"><span data-stu-id="22d82-244">hello sample dataset, `realestate-us-sample`, is from an Azure SQL Database that Azure Search can crawl.</span></span> <span data-ttu-id="22d82-245">除了 Azure SQL Database，Azure 搜尋服務可以從 Azure 表格儲存體、Blob 儲存體、Azure VM 上的 SQL Server 及 Azure Cosmos DB 中的一般資料結構搜耙及推斷索引。</span><span class="sxs-lookup"><span data-stu-id="22d82-245">Besides Azure SQL Database, Azure Search can crawl and infer an index from flat data structures in Azure Table storage, Blob storage, SQL Server on an Azure VM, and Azure Cosmos DB.</span></span> <span data-ttu-id="22d82-246">Hello 精靈 中，都支援所有的這些資料來源。</span><span class="sxs-lookup"><span data-stu-id="22d82-246">All of these data sources are supported in hello wizard.</span></span> <span data-ttu-id="22d82-247">在程式碼中，您可以使用「索引子」輕鬆地填入索引。</span><span class="sxs-lookup"><span data-stu-id="22d82-247">In code, you can populate an index easily using an *indexer*.</span></span>

+ <span data-ttu-id="22d82-248">透過推入模型，您程式碼將推入新的位置，並變更 JSON tooyour 索引中的資料列集支援的所有其他非索引子資料來源。</span><span class="sxs-lookup"><span data-stu-id="22d82-248">All other non-indexer data sources are supported via a push model, where your code pushes new and changed rowsets in JSON tooyour index.</span></span> <span data-ttu-id="22d82-249">如需詳細資訊，請參閱[在 Azure 搜尋服務中新增、更新或刪除文件](https://docs.microsoft.com/rest/api/searchservice/addupdate-or-delete-documents)。</span><span class="sxs-lookup"><span data-stu-id="22d82-249">For more information, see [Add, update, or delete documents in Azure Search](https://docs.microsoft.com/rest/api/searchservice/addupdate-or-delete-documents).</span></span>

<span data-ttu-id="22d82-250">若要深入了解本文提到的其他功能，請造訪下列連結︰</span><span class="sxs-lookup"><span data-stu-id="22d82-250">Learn more about other features mentioned in this article by visiting these links:</span></span>

* [<span data-ttu-id="22d82-251">索引子概觀</span><span class="sxs-lookup"><span data-stu-id="22d82-251">Indexers overview</span></span>](search-indexer-overview.md)
* [<span data-ttu-id="22d82-252">建立的索引 （包括 hello 索引屬性的詳細的說明）</span><span class="sxs-lookup"><span data-stu-id="22d82-252">Create Index (includes a detailed explanation of hello index attributes)</span></span>](https://docs.microsoft.com/rest/api/searchservice/create-index)
* [<span data-ttu-id="22d82-253">搜尋總管</span><span class="sxs-lookup"><span data-stu-id="22d82-253">Search Explorer</span></span>](search-explorer.md)
* [<span data-ttu-id="22d82-254">搜尋文件 (包含查詢語法範例)</span><span class="sxs-lookup"><span data-stu-id="22d82-254">Search Documents (includes examples of query syntax)</span></span>](https://docs.microsoft.com/rest/api/searchservice/search-documents)


<!--Image references-->
[1]: ./media/search-get-started-portal/tiles-indexers-datasources2.png
[2]: ./media/search-get-started-portal/import-data-cmd2.png
[3]: ./media/search-get-started-portal/realestateindex2.png
[4]: ./media/search-get-started-portal/indexers-inprogress2.png
[5]: ./media/search-get-started-portal/search-explorer-cmd2.png
[6]: ./media/search-get-started-portal/search-explorer-changeindex-se2.png
[7]: ./media/search-get-started-portal/search-explorer-query2.png
[8]: ./media/search-get-started-portal/realestate-indexer2.png
[9]: ./media/search-get-started-portal/import-datasource-sample2.png