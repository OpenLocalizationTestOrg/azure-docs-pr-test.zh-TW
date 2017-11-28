<span data-ttu-id="9bae7-101">.NET 應用程式可以使用 **StackExchange.Redis** 快取用戶端，該用戶端可在 Visual Studio 中使用能簡化快取用戶端應用程式組態的 NuGet 套件來加以設定。</span><span class="sxs-lookup"><span data-stu-id="9bae7-101">.NET applications can use the **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies the configuration of cache client applications.</span></span> 

> [!NOTE]
> <span data-ttu-id="9bae7-102">如需詳細資訊，請參閱 [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github 頁面和 [StackExchange.Redis 快取用戶端文件](http://github.com/StackExchange/StackExchange.Redis#documentation)。</span><span class="sxs-lookup"><span data-stu-id="9bae7-102">For more information, see the [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  the [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span></span>
> 
> 

<span data-ttu-id="9bae7-103">若要在 Visual Studio 中使用 StackExchange.Redis NuGet 套件來設定用戶端應用程式，請在 [方案總管] 中的專案上按一下滑鼠右鍵，然後選擇 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="9bae7-103">To configure a client application in Visual Studio using the StackExchange.Redis NuGet package, right-click the project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![Manage NuGet packages](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

<span data-ttu-id="9bae7-105">在搜尋文字方塊中輸入 **StackExchange.Redis** 或 **StackExchange.Redis.StrongName**、從結果選取需要的版本，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="9bae7-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into the search text box, select the desired version from the results, and click **Install**.</span></span>

> [!NOTE]
> <span data-ttu-id="9bae7-106">如果您偏好使用強式名稱版本的 **StackExchange.Redis** 用戶端程式庫，請選取 **StackExchange.Redis.StrongName**；否則選取 **StackExchange.Redis**。</span><span class="sxs-lookup"><span data-stu-id="9bae7-106">If you prefer to use a strong-named version of the **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span></span>
> 
> 

![StackExchange.Redis NuGet package](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

<span data-ttu-id="9bae7-108">NuGet 套件會為您的用戶端應用程式下載並新增必要的組件參考，以利用 StackExchange.Redis 快取用戶端來存取 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="9bae7-108">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span></span>

> [!NOTE]
> <span data-ttu-id="9bae7-109">如果您先前已經設定專案以使用 StackExchange.Redis，您就可以從 **NuGet 套件管理員**檢查套件更新。</span><span class="sxs-lookup"><span data-stu-id="9bae7-109">If you have previously configured your project to use StackExchange.Redis, you can check for updates to the package from the **NuGet Package Manager**.</span></span> <span data-ttu-id="9bae7-110">若要檢查及安裝 StackExchange.Redis NuGet 套件的已更新版本，請按一下 [NuGet 套件管理員] 視窗中的 [更新]。</span><span class="sxs-lookup"><span data-stu-id="9bae7-110">To check for and install updated versions of the StackExchange.Redis NuGet package, click **Updates** in the the **NuGet Package Manager** window.</span></span> <span data-ttu-id="9bae7-111">如果 StackExchange.Redis NuGet 套件有更新可用，您可以更新您的專案來使用已更新版本。</span><span class="sxs-lookup"><span data-stu-id="9bae7-111">If an update to the StackExchange.Redis NuGet package is available, you can update your project to use the updated version.</span></span>
> 
> 

<span data-ttu-id="9bae7-112">從 [工具] 功能表按一下 [NuGet 套用管理員]、[套件管理員主控台]，然後從 [Package Manager Console] 視窗執行下列命令，也可以安裝 StackExchange.Redis NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="9bae7-112">You can also install the StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu, and running the following command from the **Package Manager Console** window.</span></span>
    
```
Install-Package StackExchange.Redis
```
