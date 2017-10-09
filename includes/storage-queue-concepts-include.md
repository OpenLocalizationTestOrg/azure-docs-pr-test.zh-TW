## <a name="what-is-queue-storage"></a><span data-ttu-id="fc152-101">什麼是佇列儲存體？</span><span class="sxs-lookup"><span data-stu-id="fc152-101">What is Queue Storage?</span></span>
<span data-ttu-id="fc152-102">Azure 佇列儲存體是用於儲存大量訊息，可透過使用 HTTP 或 HTTPS 驗證呼叫的 hello world 中從任何地方存取服務。</span><span class="sxs-lookup"><span data-stu-id="fc152-102">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="fc152-103">單一佇列訊息可以是總 too64 KB 的大小，並佇列可以包含數百萬個訊息，向上 toohello 總容量限制的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fc152-103">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

<span data-ttu-id="fc152-104">佇列儲存體的一般用途包括：</span><span class="sxs-lookup"><span data-stu-id="fc152-104">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="fc152-105">以非同步方式建立工作 tooprocess 待辦項的目</span><span class="sxs-lookup"><span data-stu-id="fc152-105">Creating a backlog of work tooprocess asynchronously</span></span>
* <span data-ttu-id="fc152-106">從 Azure web 角色 tooan Azure 背景工作角色傳遞訊息</span><span class="sxs-lookup"><span data-stu-id="fc152-106">Passing messages from an Azure web role tooan Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="fc152-107">佇列服務概念</span><span class="sxs-lookup"><span data-stu-id="fc152-107">Queue Service Concepts</span></span>
<span data-ttu-id="fc152-108">hello 佇列服務包含下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="fc152-108">hello Queue service contains hello following components:</span></span>

![Queue1](./media/storage-queue-concepts-include/queue1.png)

* <span data-ttu-id="fc152-110">**URL 格式：**可以使用 hello 下列 URL 格式來定址佇列：</span><span class="sxs-lookup"><span data-stu-id="fc152-110">**URL format:** Queues are addressable using hello following URL format:</span></span>   
    <span data-ttu-id="fc152-111">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="fc152-111">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="fc152-112">下列 URL 的 hello 解決 hello 圖表中的佇列：</span><span class="sxs-lookup"><span data-stu-id="fc152-112">hello following URL addresses a queue in hello diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="fc152-113">**儲存體帳戶：**所有存取的 tooAzure 是儲存體透過儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fc152-113">**Storage Account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="fc152-114">如需關於儲存體帳戶容量的詳細資訊，請參閱＜ [Azure 儲存體延展性和效能目標](../articles/storage/common/storage-scalability-targets.md) ＞(英文)。</span><span class="sxs-lookup"><span data-stu-id="fc152-114">See [Azure Storage Scalability and Performance Targets](../articles/storage/common/storage-scalability-targets.md) for details about storage account capacity.</span></span>
* <span data-ttu-id="fc152-115">**佇列：** 佇列包含一組訊息。</span><span class="sxs-lookup"><span data-stu-id="fc152-115">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="fc152-116">所有訊息都必須放在佇列中。</span><span class="sxs-lookup"><span data-stu-id="fc152-116">All messages must be in a queue.</span></span> <span data-ttu-id="fc152-117">請注意該 hello 佇列名稱必須全部小寫。</span><span class="sxs-lookup"><span data-stu-id="fc152-117">Note that hello queue name must be all lowercase.</span></span> <span data-ttu-id="fc152-118">如需為佇列命名的詳細資訊，請參閱 [為佇列和中繼資料命名](https://msdn.microsoft.com/library/azure/dd179349.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fc152-118">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>
* <span data-ttu-id="fc152-119">**訊息：**的訊息，任何格式的總 too64 KB。</span><span class="sxs-lookup"><span data-stu-id="fc152-119">**Message:** A message, in any format, of up too64 KB.</span></span> <span data-ttu-id="fc152-120">hello 訊息保留在 hello 佇列中的最大時間為 7 天。</span><span class="sxs-lookup"><span data-stu-id="fc152-120">hello maximum time that a message can remain in hello queue is 7 days.</span></span>

