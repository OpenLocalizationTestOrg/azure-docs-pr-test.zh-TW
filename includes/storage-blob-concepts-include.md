## <a name="what-is-blob-storage"></a><span data-ttu-id="32491-101">什麼是 Blob 儲存體？</span><span class="sxs-lookup"><span data-stu-id="32491-101">What is Blob Storage?</span></span>
<span data-ttu-id="32491-102">Azure Blob 儲存體是用於儲存大量非結構化的物件的資料，例如文字或二進位資料，可以在 hello world，透過 HTTP 或 HTTPS 從任何地方存取服務。</span><span class="sxs-lookup"><span data-stu-id="32491-102">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="32491-103">您可以使用 Blob 儲存體 tooexpose 資料公開 toohello 世界中或 toostore 應用程式資料未公開。</span><span class="sxs-lookup"><span data-stu-id="32491-103">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span>

<span data-ttu-id="32491-104">Blob 儲存體的一般用途包括：</span><span class="sxs-lookup"><span data-stu-id="32491-104">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="32491-105">服務映像，或直接文 tooa 瀏覽器</span><span class="sxs-lookup"><span data-stu-id="32491-105">Serving images or documents directly tooa browser</span></span>
* <span data-ttu-id="32491-106">儲存檔案供分散式存取</span><span class="sxs-lookup"><span data-stu-id="32491-106">Storing files for distributed access</span></span>
* <span data-ttu-id="32491-107">串流傳輸視訊和音訊</span><span class="sxs-lookup"><span data-stu-id="32491-107">Streaming video and audio</span></span>
* <span data-ttu-id="32491-108">儲存備份和還原、災害復原和封存資料</span><span class="sxs-lookup"><span data-stu-id="32491-108">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="32491-109">儲存資料供內部部署或 Azure 託管服務進行分析</span><span class="sxs-lookup"><span data-stu-id="32491-109">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="32491-110">Blob 服務概念</span><span class="sxs-lookup"><span data-stu-id="32491-110">Blob service concepts</span></span>
<span data-ttu-id="32491-111">hello Blob 服務包含下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="32491-111">hello Blob service contains hello following components:</span></span>

![Blob 架構](./media/storage-blob-concepts-include/blob1.png)

* <span data-ttu-id="32491-113">**儲存體帳戶：**所有存取的 tooAzure 是儲存體透過儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="32491-113">**Storage Account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="32491-114">此儲存體帳戶可以是**一般用途的儲存體帳戶**或專門用於儲存物件/Blob 的 **Blob 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="32491-114">This storage account can be a **General-purpose storage account** or a **Blob storage account** which is specialized for storing objects/blobs.</span></span> <span data-ttu-id="32491-115">如需詳細資訊，請參閱[關於 Azure 儲存體帳戶](../articles/storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="32491-115">See [About Azure storage accounts](../articles/storage/common/storage-create-storage-account.md) for more information.</span></span>
* <span data-ttu-id="32491-116">**容器：** 容器提供一組 Blob 的群組。</span><span class="sxs-lookup"><span data-stu-id="32491-116">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="32491-117">所有 Blob 都必須放在容器中。</span><span class="sxs-lookup"><span data-stu-id="32491-117">All blobs must be in a container.</span></span> <span data-ttu-id="32491-118">一個帳戶可以包含的容器不限數量。</span><span class="sxs-lookup"><span data-stu-id="32491-118">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="32491-119">容器可以儲存無限制的 Blob。</span><span class="sxs-lookup"><span data-stu-id="32491-119">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="32491-120">請注意該 hello 容器名稱必須是小寫。</span><span class="sxs-lookup"><span data-stu-id="32491-120">Note that hello container name must be lowercase.</span></span>
* <span data-ttu-id="32491-121">**Blob：** 任何類型和大小的檔案。</span><span class="sxs-lookup"><span data-stu-id="32491-121">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="32491-122">Azure 儲存體提供三種類型的 Blob：區塊 Blob、分頁 Blob 及附加 Blob。</span><span class="sxs-lookup"><span data-stu-id="32491-122">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="32491-123">*區塊 Blob* 很適合儲存文字或二進位檔案，例如文件和媒體檔案。</span><span class="sxs-lookup"><span data-stu-id="32491-123">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="32491-124">*附加 blob*會類似 tooblock blob 的區塊，由組成，但它們會針對最佳化在所附加作業，讓它們可用於記錄的案例。</span><span class="sxs-lookup"><span data-stu-id="32491-124">*Append blobs* are similar tooblock blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="32491-125">單一區塊 blob 可包含總 too50，000 區塊 too100 MB，總稍微大於 4.75 TB (100 MB X 50000) 的總大小。</span><span class="sxs-lookup"><span data-stu-id="32491-125">A single block blob can contain up too50,000 blocks of up too100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="32491-126">單一附加 blob 可包含總 too50，000 區塊 too4 MB，總稍微超過 195 GB (4 MB X 50000) 的總大小。</span><span class="sxs-lookup"><span data-stu-id="32491-126">A single append blob can contain up too50,000 blocks of up too4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="32491-127">*分頁 blob*最長 too1 TB 的大小，可能會和更頻繁的讀取/寫入作業時很有效率。</span><span class="sxs-lookup"><span data-stu-id="32491-127">*Page blobs* can be up too1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="32491-128">Azure 虛擬機器會使用分頁 Blob 作為作業系統和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="32491-128">Azure Virtual Machines use page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="32491-129">如需有關命名容器和 Blob 的詳細資訊，請參閱 [命名和參考容器、Blob 及中繼資料](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata)。</span><span class="sxs-lookup"><span data-stu-id="32491-129">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>
