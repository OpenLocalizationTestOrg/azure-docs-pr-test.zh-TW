## <a name="specifying-structure-definition-for-rectangular-datasets"></a><span data-ttu-id="abc01-101">指定矩形資料集的結構定義</span><span class="sxs-lookup"><span data-stu-id="abc01-101">Specifying structure definition for rectangular datasets</span></span>
<span data-ttu-id="abc01-102">hello hello 資料集 JSON 結構區段是**選擇性**矩形的資料表 （資料列和資料行） 區段，並包含 hello 資料表的資料行集合。</span><span class="sxs-lookup"><span data-stu-id="abc01-102">hello structure section in hello datasets JSON is an **optional** section for rectangular tables (with rows & columns) and contains a collection of columns for hello table.</span></span> <span data-ttu-id="abc01-103">您將使用類型轉換的其中一個提供的類型資訊或執行資料行對應 hello 結構 > 一節。</span><span class="sxs-lookup"><span data-stu-id="abc01-103">You will use hello structure section for either providing type information for type conversions or doing column mappings.</span></span> <span data-ttu-id="abc01-104">hello 下列各節說明這些功能的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="abc01-104">hello following sections describe these features in detail.</span></span> 

<span data-ttu-id="abc01-105">每個資料行包含下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="abc01-105">Each column contains hello following properties:</span></span>

| <span data-ttu-id="abc01-106">屬性</span><span class="sxs-lookup"><span data-stu-id="abc01-106">Property</span></span> | <span data-ttu-id="abc01-107">說明</span><span class="sxs-lookup"><span data-stu-id="abc01-107">Description</span></span> | <span data-ttu-id="abc01-108">必要</span><span class="sxs-lookup"><span data-stu-id="abc01-108">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="abc01-109">名稱</span><span class="sxs-lookup"><span data-stu-id="abc01-109">name</span></span> |<span data-ttu-id="abc01-110">Hello 資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="abc01-110">Name of hello column.</span></span> |<span data-ttu-id="abc01-111">是</span><span class="sxs-lookup"><span data-stu-id="abc01-111">Yes</span></span> |
| <span data-ttu-id="abc01-112">類型</span><span class="sxs-lookup"><span data-stu-id="abc01-112">type</span></span> |<span data-ttu-id="abc01-113">Hello 資料行資料類型。</span><span class="sxs-lookup"><span data-stu-id="abc01-113">Data type of hello column.</span></span> <span data-ttu-id="abc01-114">有關何時應指定類型資訊的詳細資訊，請參閱下文類型轉換的部份</span><span class="sxs-lookup"><span data-stu-id="abc01-114">See type conversions section below for more details regarding when should you specify type information</span></span> |<span data-ttu-id="abc01-115">否</span><span class="sxs-lookup"><span data-stu-id="abc01-115">No</span></span> |
| <span data-ttu-id="abc01-116">culture</span><span class="sxs-lookup"><span data-stu-id="abc01-116">culture</span></span> |<span data-ttu-id="abc01-117">.NET 基礎類型指定且為.NET 型別 Datetime 或 Datetimeoffset 時使用的文化特性 toobe。</span><span class="sxs-lookup"><span data-stu-id="abc01-117">.NET based culture toobe used when type is specified and is .NET type Datetime or Datetimeoffset.</span></span> <span data-ttu-id="abc01-118">預設值為 “en-us”。</span><span class="sxs-lookup"><span data-stu-id="abc01-118">Default is “en-us”.</span></span> |<span data-ttu-id="abc01-119">否</span><span class="sxs-lookup"><span data-stu-id="abc01-119">No</span></span> |
| <span data-ttu-id="abc01-120">format</span><span class="sxs-lookup"><span data-stu-id="abc01-120">format</span></span> |<span data-ttu-id="abc01-121">格式化字串 toobe 時指定了型別，且是 Datetime 或 Datetimeoffset 的.NET 類型使用。</span><span class="sxs-lookup"><span data-stu-id="abc01-121">Format string toobe used when type is specified and is .NET type Datetime or Datetimeoffset.</span></span> |<span data-ttu-id="abc01-122">否</span><span class="sxs-lookup"><span data-stu-id="abc01-122">No</span></span> |

<span data-ttu-id="abc01-123">hello 下列範例顯示一份含有三個資料行的使用者識別碼、 名稱和 lastlogindate 的 hello 結構區段 JSON。</span><span class="sxs-lookup"><span data-stu-id="abc01-123">hello following sample shows hello structure section JSON for a table that has three columns userid, name, and lastlogindate.</span></span>

```json
"structure": 
[
    { "name": "userid"},
    { "name": "name"},
    { "name": "lastlogindate"}
],
```

<span data-ttu-id="abc01-124">請使用下列指導方針時 hello tooinclude 「 結構 」 資訊和 hello 中的哪些 tooinclude**結構**> 一節。</span><span class="sxs-lookup"><span data-stu-id="abc01-124">Please use hello following guidelines for when tooinclude “structure” information and what tooinclude in hello **structure** section.</span></span>

* <span data-ttu-id="abc01-125">**結構化的資料來源的**商店以及 hello 資料本身 （SQL Server、 Oracle、 Azure 資料表等這類來源），您應該指定 hello 「 結構 」 一節，只有當您想執行的特定的資料行對應的資料結構描述和類型資訊toospecific 中接收和其名稱的資料行的來源資料行不 hello 相同 （請參閱以下的資料行對應一節中的詳細資料）。</span><span class="sxs-lookup"><span data-stu-id="abc01-125">**For structured data sources** that store data schema and type information along with hello data itself (sources like SQL Server, Oracle, Azure table etc.), you should specify hello “structure” section only if you want do column mapping of specific source columns toospecific columns in sink and their names are not hello same (see details in column mapping section below).</span></span> 
  
    <span data-ttu-id="abc01-126">如上面所述，hello 類型資訊是選擇性的 「 結構 」 一節。</span><span class="sxs-lookup"><span data-stu-id="abc01-126">As mentioned above, hello type information is optional in “structure” section.</span></span> <span data-ttu-id="abc01-127">結構化的來源類型資訊已可使用 hello 資料存放區中的資料集定義的一部分，因此您不應該包含型別資訊包括 hello 「 結構 」 一節時。</span><span class="sxs-lookup"><span data-stu-id="abc01-127">For structured sources, type information is already available as part of dataset definition in hello data store, so you should not include type information when you do include hello “structure” section.</span></span>
* <span data-ttu-id="abc01-128">**讀取的資料來源 (特別是 Azure blob) 的結構描述**您可以選擇 toostore 資料，而不儲存任何結構描述或型別資訊與 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="abc01-128">**For schema on read data sources (specifically Azure blob)**  you can choose toostore data without storing any schema or type information with hello data.</span></span> <span data-ttu-id="abc01-129">這些類型的資料來源中 hello 遵循 2 的情況下應包含 「 結構 」:</span><span class="sxs-lookup"><span data-stu-id="abc01-129">For these types of data sources you should include “structure” in hello following 2 cases:</span></span>
  * <span data-ttu-id="abc01-130">您想 toodo 資料行對應。</span><span class="sxs-lookup"><span data-stu-id="abc01-130">You want toodo column mapping.</span></span>
  * <span data-ttu-id="abc01-131">複製活動中的來源 hello 資料集時，您可以提供 「 結構 」 中的類型資訊和資料處理站將用於轉換 toonative 類型 hello 接收的此類型資訊。</span><span class="sxs-lookup"><span data-stu-id="abc01-131">When hello dataset is a source in a Copy activity, you can provide type information in “structure” and data factory will use this type information for conversion toonative types for hello sink.</span></span> <span data-ttu-id="abc01-132">請參閱[從 Azure Blob 中移動資料 tooand](../articles/data-factory/data-factory-azure-blob-connector.md)文件以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="abc01-132">See [Move data tooand from Azure Blob](../articles/data-factory/data-factory-azure-blob-connector.md) article for more information.</span></span>

### <a name="supported-net-based-types"></a><span data-ttu-id="abc01-133">支援 .NET 型的類型</span><span class="sxs-lookup"><span data-stu-id="abc01-133">Supported .NET-based types</span></span>
<span data-ttu-id="abc01-134">資料處理站支援 hello 遵循符合 CLS 標準的.NET 為基礎來讀取的資料來源，例如 Azure blob 上的結構描述提供 「 結構 」 中的類型資訊的型別值。</span><span class="sxs-lookup"><span data-stu-id="abc01-134">Data factory supports hello following CLS compliant .NET based type values for providing type information in “structure” for schema on read data sources like Azure blob.</span></span>

* <span data-ttu-id="abc01-135">Int16</span><span class="sxs-lookup"><span data-stu-id="abc01-135">Int16</span></span>
* <span data-ttu-id="abc01-136">Int32</span><span class="sxs-lookup"><span data-stu-id="abc01-136">Int32</span></span> 
* <span data-ttu-id="abc01-137">Int64</span><span class="sxs-lookup"><span data-stu-id="abc01-137">Int64</span></span>
* <span data-ttu-id="abc01-138">單一</span><span class="sxs-lookup"><span data-stu-id="abc01-138">Single</span></span>
* <span data-ttu-id="abc01-139">兩倍</span><span class="sxs-lookup"><span data-stu-id="abc01-139">Double</span></span>
* <span data-ttu-id="abc01-140">十進位</span><span class="sxs-lookup"><span data-stu-id="abc01-140">Decimal</span></span>
* <span data-ttu-id="abc01-141">Byte[]</span><span class="sxs-lookup"><span data-stu-id="abc01-141">Byte[]</span></span>
* <span data-ttu-id="abc01-142">Bool</span><span class="sxs-lookup"><span data-stu-id="abc01-142">Bool</span></span>
* <span data-ttu-id="abc01-143">String</span><span class="sxs-lookup"><span data-stu-id="abc01-143">String</span></span> 
* <span data-ttu-id="abc01-144">Guid</span><span class="sxs-lookup"><span data-stu-id="abc01-144">Guid</span></span>
* <span data-ttu-id="abc01-145">Datetime</span><span class="sxs-lookup"><span data-stu-id="abc01-145">Datetime</span></span>
* <span data-ttu-id="abc01-146">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="abc01-146">Datetimeoffset</span></span>
* <span data-ttu-id="abc01-147">Timespan</span><span class="sxs-lookup"><span data-stu-id="abc01-147">Timespan</span></span> 

<span data-ttu-id="abc01-148">Datetime 和 Datetimeoffset 您也可以選擇指定"culture"&"format"字串 toofacilitate 剖析自訂的日期時間字串。</span><span class="sxs-lookup"><span data-stu-id="abc01-148">For Datetime & Datetimeoffset you can also optionally specify “culture” & “format” string toofacilitate parsing of your custom Datetime string.</span></span> <span data-ttu-id="abc01-149">請參閱下方的類型轉換範例。</span><span class="sxs-lookup"><span data-stu-id="abc01-149">See sample for type conversion below.</span></span>

