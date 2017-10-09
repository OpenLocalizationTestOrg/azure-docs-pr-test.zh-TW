### <a name="azure-storage-linked-service"></a><span data-ttu-id="aaa77-101">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="aaa77-101">Azure Storage Linked Service</span></span>
<span data-ttu-id="aaa77-102">hello **Azure 儲存體連結服務**可讓您使用 hello 的 Azure 儲存體帳戶 tooan Azure data factory toolink**帳戶金鑰**，可以提供與全域存取 toohello Azure 的 hello 資料處理站儲存體。</span><span class="sxs-lookup"><span data-stu-id="aaa77-102">hello **Azure Storage linked service** allows you toolink an Azure storage account tooan Azure data factory by using hello **account key**, which provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="aaa77-103">下表中的 hello 提供 JSON 項目特定 tooAzure 儲存體連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="aaa77-103">hello following table provides description for JSON elements specific tooAzure Storage linked service.</span></span>

| <span data-ttu-id="aaa77-104">屬性</span><span class="sxs-lookup"><span data-stu-id="aaa77-104">Property</span></span> | <span data-ttu-id="aaa77-105">說明</span><span class="sxs-lookup"><span data-stu-id="aaa77-105">Description</span></span> | <span data-ttu-id="aaa77-106">必要</span><span class="sxs-lookup"><span data-stu-id="aaa77-106">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="aaa77-107">類型</span><span class="sxs-lookup"><span data-stu-id="aaa77-107">type</span></span> |<span data-ttu-id="aaa77-108">hello 類型屬性必須設定為： **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="aaa77-108">hello type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="aaa77-109">是</span><span class="sxs-lookup"><span data-stu-id="aaa77-109">Yes</span></span> |
| <span data-ttu-id="aaa77-110">connectionString</span><span class="sxs-lookup"><span data-stu-id="aaa77-110">connectionString</span></span> |<span data-ttu-id="aaa77-111">指定所需的資訊 tooconnect tooAzure 儲存體 hello connectionString 屬性。</span><span class="sxs-lookup"><span data-stu-id="aaa77-111">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="aaa77-112">是</span><span class="sxs-lookup"><span data-stu-id="aaa77-112">Yes</span></span> |

<span data-ttu-id="aaa77-113">請參閱下列文章步驟 tooview/複製 hello 帳戶金鑰的 Azure 儲存體的 hello:[檢視、 複製和重新產生儲存體存取金鑰](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="aaa77-113">See hello following article for steps tooview/copy hello account key for an Azure Storage: [View, copy, and regenerate storage access keys](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

<span data-ttu-id="aaa77-114">**範例：**</span><span class="sxs-lookup"><span data-stu-id="aaa77-114">**Example:**</span></span>  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="aaa77-115">Azure 儲存體 SAS 連結服務</span><span class="sxs-lookup"><span data-stu-id="aaa77-115">Azure Storage Sas Linked Service</span></span>
<span data-ttu-id="aaa77-116">共用的存取簽章 (SAS) 提供儲存體帳戶中的委派的存取 tooresources。</span><span class="sxs-lookup"><span data-stu-id="aaa77-116">A shared access signature (SAS) provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="aaa77-117">它可讓 toogrant 用戶端在指定期間內的時間與一組指定的權限，在儲存體帳戶的權限 tooobjects 限制而不需要 tooshare 帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="aaa77-117">It allows you toogrant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having tooshare your account access keys.</span></span> <span data-ttu-id="aaa77-118">hello SAS 是包含在其查詢參數中所有的 hello 資訊所需的已驗證的存取 tooa 儲存體資源的 URI。</span><span class="sxs-lookup"><span data-stu-id="aaa77-118">hello SAS is a URI that encompasses in its query parameters all hello information necessary for authenticated access tooa storage resource.</span></span> <span data-ttu-id="aaa77-119">tooaccess 以 hello SAS 存放裝置資源，hello 用戶端只需要 toopass hello SAS toohello 適當建構函式或方法中。</span><span class="sxs-lookup"><span data-stu-id="aaa77-119">tooaccess storage resources with hello SAS, hello client only needs toopass in hello SAS toohello appropriate constructor or method.</span></span> <span data-ttu-id="aaa77-120">如需 SAS 的詳細資訊，請參閱[共用存取簽章： 了解 hello SAS 模型](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="aaa77-120">For detailed information about SAS, see [Shared Access Signatures: Understanding hello SAS Model](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aaa77-121">Azure Data Factory 現在僅支援 **服務 SAS**，但不支援帳戶 SAS。</span><span class="sxs-lookup"><span data-stu-id="aaa77-121">Azure Data Factory now only supports **Service SAS** but not Account SAS.</span></span> <span data-ttu-id="aaa77-122">請參閱[共用存取簽章的型別](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures)這兩種類型的詳細資料以及如何 tooconstruct。</span><span class="sxs-lookup"><span data-stu-id="aaa77-122">See [Types of Shared Access Signatures](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures) for details about these two types and how tooconstruct.</span></span> <span data-ttu-id="aaa77-123">請注意 hello generable 從 Azure 入口網站的 SAS URL，或儲存體總管是帳戶 SAS，但不支援。</span><span class="sxs-lookup"><span data-stu-id="aaa77-123">Note hello SAS URL generable from Azure portal or Storage Explorer is an Account SAS, which is not supported.</span></span>
> 

<span data-ttu-id="aaa77-124">hello Azure 儲存體 SAS 連結服務可讓您 Azure 儲存體帳戶 tooan Azure data factory toolink 使用共用存取簽章 (SAS)。</span><span class="sxs-lookup"><span data-stu-id="aaa77-124">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="aaa77-125">它提供 hello 資料 factory 限制/時間繫結存取 tooall/特定資源 （blob/容器） hello 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="aaa77-125">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="aaa77-126">下表中的 hello 提供 JSON 項目特定 tooAzure 儲存體 SAS 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="aaa77-126">hello following table provides description for JSON elements specific tooAzure Storage SAS linked service.</span></span> 

| <span data-ttu-id="aaa77-127">屬性</span><span class="sxs-lookup"><span data-stu-id="aaa77-127">Property</span></span> | <span data-ttu-id="aaa77-128">說明</span><span class="sxs-lookup"><span data-stu-id="aaa77-128">Description</span></span> | <span data-ttu-id="aaa77-129">必要</span><span class="sxs-lookup"><span data-stu-id="aaa77-129">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="aaa77-130">類型</span><span class="sxs-lookup"><span data-stu-id="aaa77-130">type</span></span> |<span data-ttu-id="aaa77-131">hello 類型屬性必須設定為： **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="aaa77-131">hello type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="aaa77-132">是</span><span class="sxs-lookup"><span data-stu-id="aaa77-132">Yes</span></span> |
| <span data-ttu-id="aaa77-133">sasUri</span><span class="sxs-lookup"><span data-stu-id="aaa77-133">sasUri</span></span> |<span data-ttu-id="aaa77-134">指定共用存取簽章 URI toohello Azure 儲存體資源，例如 blob、 容器或資料表。</span><span class="sxs-lookup"><span data-stu-id="aaa77-134">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span>  |<span data-ttu-id="aaa77-135">是</span><span class="sxs-lookup"><span data-stu-id="aaa77-135">Yes</span></span> |

<span data-ttu-id="aaa77-136">**範例：**</span><span class="sxs-lookup"><span data-stu-id="aaa77-136">**Example:**</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<Specify SAS URI of hello Azure Storage resource>"   
        }  
    }  
}  
```

<span data-ttu-id="aaa77-137">建立時**SAS URI**，考慮下列 hello:</span><span class="sxs-lookup"><span data-stu-id="aaa77-137">When creating an **SAS URI**, considering hello following:</span></span>  

* <span data-ttu-id="aaa77-138">設定適當的讀取/寫入**權限**上根據物件 hello 已連結的服務 （讀取、 寫入、 讀取/寫入） 如何用於您的 data factory。</span><span class="sxs-lookup"><span data-stu-id="aaa77-138">Set appropriate read/write **permissions** on objects based on how hello linked service (read, write, read/write) is used in your data factory.</span></span>
* <span data-ttu-id="aaa77-139">設定適當的 [過期時間]。</span><span class="sxs-lookup"><span data-stu-id="aaa77-139">Set **Expiry time** appropriately.</span></span> <span data-ttu-id="aaa77-140">請確定 hello hello 管線的作用中的期間內不會過期 hello 存取 tooAzure 儲存物件。</span><span class="sxs-lookup"><span data-stu-id="aaa77-140">Make sure that hello access tooAzure Storage objects does not expire within hello active period of hello pipeline.</span></span>
* <span data-ttu-id="aaa77-141">Uri 應建立在 hello 右 「 容器 /blob 或資料表層級根據 hello 需要。</span><span class="sxs-lookup"><span data-stu-id="aaa77-141">Uri should be created at hello right container/blob or Table level based on hello need.</span></span> <span data-ttu-id="aaa77-142">Azure blob 的 SAS Uri tooan 允許 hello Data Factory 服務 tooaccess 該特定的 blob。</span><span class="sxs-lookup"><span data-stu-id="aaa77-142">A SAS Uri tooan Azure blob allows hello Data Factory service tooaccess that particular blob.</span></span> <span data-ttu-id="aaa77-143">SAS Uri tooan Azure blob 容器可讓 hello Data Factory 服務 tooiterate 透過該容器中的 blob。</span><span class="sxs-lookup"><span data-stu-id="aaa77-143">A SAS Uri tooan Azure blob container allows hello Data Factory service tooiterate through blobs in that container.</span></span> <span data-ttu-id="aaa77-144">如果您需要更大的 tooprovide 存取/較少的更新版本中，物件或更新 hello SAS URI，請記住 tooupdate hello 連結服務與 hello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="aaa77-144">If you need tooprovide access more/fewer objects later, or update hello SAS URI, remember tooupdate hello linked service with hello new URI.</span></span>   

