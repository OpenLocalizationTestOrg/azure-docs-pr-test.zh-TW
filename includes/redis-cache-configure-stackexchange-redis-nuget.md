<span data-ttu-id="e2ab2-101">.NET 應用程式可以使用 hello **StackExchange.Redis**快取用戶端，可以使用 NuGet 封裝，它可簡化 hello 設定快取的用戶端應用程式的 Visual Studio 中設定。</span><span class="sxs-lookup"><span data-stu-id="e2ab2-101">.NET applications can use hello **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies hello configuration of cache client applications.</span></span> 

> [!NOTE]
> <span data-ttu-id="e2ab2-102">如需詳細資訊，請參閱 hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github 頁面和 hello [StackExchange.Redis 快取的用戶端文件](http://github.com/StackExchange/StackExchange.Redis#documentation)。</span><span class="sxs-lookup"><span data-stu-id="e2ab2-102">For more information, see hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  hello [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span></span>
> 
> 

<span data-ttu-id="e2ab2-103">tooconfigure 用戶端應用程式，在 Visual Studio 中使用 hello StackExchange.Redis NuGet 封裝，以滑鼠右鍵按一下中的 hello 專案**方案總管 中**選擇**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="e2ab2-103">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, right-click hello project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![Manage NuGet packages](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

<span data-ttu-id="e2ab2-105">型別**StackExchange.Redis**或**StackExchange.Redis.StrongName** hello 搜尋文字方塊中，從 hello 結果中，選取 hello 所需的版本，然後按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="e2ab2-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into hello search text box, select hello desired version from hello results, and click **Install**.</span></span>

> [!NOTE]
> <span data-ttu-id="e2ab2-106">如果您偏好 toouse hello 的強式名稱版本**StackExchange.Redis**用戶端程式庫中，選擇**StackExchange.Redis.StrongName**; 否則選擇**StackExchange.Redis**.</span><span class="sxs-lookup"><span data-stu-id="e2ab2-106">If you prefer toouse a strong-named version of hello **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span></span>
> 
> 

![StackExchange.Redis NuGet package](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

<span data-ttu-id="e2ab2-108">hello NuGet 封裝下載並新增 hello hello StackExchange.Redis 快取用戶端與您用戶端應用程式 tooaccess Azure Redis 快取所需的組件參考。</span><span class="sxs-lookup"><span data-stu-id="e2ab2-108">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span>

> [!NOTE]
> <span data-ttu-id="e2ab2-109">如果您先前已設定您的專案 toouse StackExchange.Redis，您可以檢查更新 toohello 封裝從 hello **NuGet 套件管理員**。</span><span class="sxs-lookup"><span data-stu-id="e2ab2-109">If you have previously configured your project toouse StackExchange.Redis, you can check for updates toohello package from hello **NuGet Package Manager**.</span></span> <span data-ttu-id="e2ab2-110">如 toocheck 和安裝更新版本的 hello StackExchange.Redis NuGet 封裝，按一下**更新**在 hello hello **NuGet 套件管理員**視窗。</span><span class="sxs-lookup"><span data-stu-id="e2ab2-110">toocheck for and install updated versions of hello StackExchange.Redis NuGet package, click **Updates** in hello hello **NuGet Package Manager** window.</span></span> <span data-ttu-id="e2ab2-111">如果更新 toohello StackExchange.Redis NuGet 封裝功能，您可以更新您的專案 toouse hello 更新版本。</span><span class="sxs-lookup"><span data-stu-id="e2ab2-111">If an update toohello StackExchange.Redis NuGet package is available, you can update your project toouse hello updated version.</span></span>
> 
> 

<span data-ttu-id="e2ab2-112">您也可以按一下 安裝 hello StackExchange.Redis NuGet 封裝**NuGet 套件管理員**， **Package Manager Console**從 hello**工具**功能表，然後執行 hello下列命令從 hello **Package Manager Console**視窗。</span><span class="sxs-lookup"><span data-stu-id="e2ab2-112">You can also install hello StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu, and running hello following command from hello **Package Manager Console** window.</span></span>
    
```
Install-Package StackExchange.Redis
```
