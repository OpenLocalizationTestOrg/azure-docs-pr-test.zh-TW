<span data-ttu-id="f6541-101">hello 儲存體模擬器的共用金鑰驗證支援單一固定的帳戶及已知的驗證金鑰。</span><span class="sxs-lookup"><span data-stu-id="f6541-101">hello storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="f6541-102">此帳戶和金鑰是 hello hello 儲存體模擬器搭配允許只共用金鑰認證。</span><span class="sxs-lookup"><span data-stu-id="f6541-102">This account and key are hello only Shared Key credentials permitted for use with hello storage emulator.</span></span> <span data-ttu-id="f6541-103">如下：</span><span class="sxs-lookup"><span data-stu-id="f6541-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="f6541-104">hello hello 儲存體模擬器所支援的驗證金鑰僅供測試用戶端的驗證程式碼的 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="f6541-104">hello authentication key supported by hello storage emulator is intended only for testing hello functionality of your client authentication code.</span></span> <span data-ttu-id="f6541-105">它不提供任何安全性用途。</span><span class="sxs-lookup"><span data-stu-id="f6541-105">It does not serve any security purpose.</span></span> <span data-ttu-id="f6541-106">您不能使用您的生產儲存體帳戶與金鑰 hello 儲存體模擬器。</span><span class="sxs-lookup"><span data-stu-id="f6541-106">You cannot use your production storage account and key with hello storage emulator.</span></span> <span data-ttu-id="f6541-107">您不應該使用 hello 開發帳戶使用生產資料。</span><span class="sxs-lookup"><span data-stu-id="f6541-107">You should not use hello development account with production data.</span></span>
> 
> <span data-ttu-id="f6541-108">hello 儲存體模擬器支援僅透過 HTTP 連接。</span><span class="sxs-lookup"><span data-stu-id="f6541-108">hello storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="f6541-109">不過，HTTPS 為建議用來存取 Azure 儲存體帳戶的生產環境中資源的通訊協定的 hello。</span><span class="sxs-lookup"><span data-stu-id="f6541-109">However, HTTPS is hello recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a><span data-ttu-id="f6541-110">使用快速鍵 toohello 模擬器帳戶連線</span><span class="sxs-lookup"><span data-stu-id="f6541-110">Connect toohello emulator account using a shortcut</span></span>
<span data-ttu-id="f6541-111">hello 最簡單方式 tooconnect toohello 儲存體模擬器從您的應用程式是 tooconfigure 參考 hello 快顯的應用程式組態檔中的連接字串`UseDevelopmentStorage=true`。</span><span class="sxs-lookup"><span data-stu-id="f6541-111">hello easiest way tooconnect toohello storage emulator from your application is tooconfigure a connection string in your application's configuration file that references hello shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="f6541-112">以下是範例連接字串 toohello 儲存體模擬器中*app.config*檔案：</span><span class="sxs-lookup"><span data-stu-id="f6541-112">Here's an example of a connection string toohello storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a><span data-ttu-id="f6541-113">使用 hello 已知帳戶名稱和金鑰 toohello 模擬器帳戶連線</span><span class="sxs-lookup"><span data-stu-id="f6541-113">Connect toohello emulator account using hello well-known account name and key</span></span>
<span data-ttu-id="f6541-114">toocreate 參考 hello 模擬器帳戶名稱，以及索引鍵，您必須指定 hello 端點，每個 hello 服務您的連接字串會希望 toouse hello 連接字串中的 hello 模擬器。</span><span class="sxs-lookup"><span data-stu-id="f6541-114">toocreate a connection string that references hello emulator account name and key, you must specify hello endpoints for each of hello services you wish toouse from hello emulator in hello connection string.</span></span> <span data-ttu-id="f6541-115">這是必要的如此 hello 連接字串將參考 hello 模擬器端點，不同於生產儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f6541-115">This is necessary so that hello connection string will reference hello emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="f6541-116">例如，您的連接字串 hello 值看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="f6541-116">For example, hello value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="f6541-117">這個值是相同的 toohello 捷徑如上所示， `UseDevelopmentStorage=true`。</span><span class="sxs-lookup"><span data-stu-id="f6541-117">This value is identical toohello shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="f6541-118">指定 HTTP proxy</span><span class="sxs-lookup"><span data-stu-id="f6541-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="f6541-119">當您要測試您的服務與 hello 儲存體模擬器，您也可以指定 HTTP proxy toouse。</span><span class="sxs-lookup"><span data-stu-id="f6541-119">You can also specify an HTTP proxy toouse when you're testing your service against hello storage emulator.</span></span> <span data-ttu-id="f6541-120">這可用於偵錯對 hello 儲存體服務的作業時，觀察 HTTP 要求和回應。</span><span class="sxs-lookup"><span data-stu-id="f6541-120">This can be useful for observing HTTP requests and responses while you're debugging operations against hello storage services.</span></span> <span data-ttu-id="f6541-121">toospecify proxy、 新增 hello`DevelopmentStorageProxyUri`選項 toohello 連接字串，並設定其值 toohello proxy 的 URI。</span><span class="sxs-lookup"><span data-stu-id="f6541-121">toospecify a proxy, add hello `DevelopmentStorageProxyUri` option toohello connection string, and set its value toohello proxy URI.</span></span> <span data-ttu-id="f6541-122">例如，以下是指向 toohello 儲存體模擬器，並且設定 HTTP proxy 的連接字串：</span><span class="sxs-lookup"><span data-stu-id="f6541-122">For example, here is a connection string that points toohello storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

