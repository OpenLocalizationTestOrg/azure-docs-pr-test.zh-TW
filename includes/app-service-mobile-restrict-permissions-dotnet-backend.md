
<span data-ttu-id="8645b-101">根據預設，可以匿名方式叫用 Mobile Apps 後端中的 API。</span><span class="sxs-lookup"><span data-stu-id="8645b-101">By default, APIs in a Mobile Apps back end can be invoked anonymously.</span></span> <span data-ttu-id="8645b-102">接下來，您需要 toorestrict 存取 tooonly 驗證用戶端。</span><span class="sxs-lookup"><span data-stu-id="8645b-102">Next, you need toorestrict access tooonly authenticated clients.</span></span>  

* <span data-ttu-id="8645b-103">**Node.js 回結束 （透過 hello Azure 入口網站)** :</span><span class="sxs-lookup"><span data-stu-id="8645b-103">**Node.js back end (via hello Azure portal)** :</span></span>  

    <span data-ttu-id="8645b-104">在 Mobile Apps 的 [設定] 中，按一下 [簡單資料表]，然後選取資料表。</span><span class="sxs-lookup"><span data-stu-id="8645b-104">In your Mobile Apps settings, click **Easy Tables** and select your table.</span></span> <span data-ttu-id="8645b-105">按一下 變更權限，選取所有權限的 僅驗證存取，然後按一下儲存。</span><span class="sxs-lookup"><span data-stu-id="8645b-105">Click **Change permissions**, select **Authenticated access only** for all permissions, and then click **Save**.</span></span>
* <span data-ttu-id="8645b-106">**.NET 後端 (C#)**：</span><span class="sxs-lookup"><span data-stu-id="8645b-106">**.NET back end (C#)**:</span></span>  

    <span data-ttu-id="8645b-107">在 hello 伺服器專案中，瀏覽過**控制器** > **TodoItemController.cs**。</span><span class="sxs-lookup"><span data-stu-id="8645b-107">In hello server project, navigate too**Controllers** > **TodoItemController.cs**.</span></span> <span data-ttu-id="8645b-108">新增 hello`[Authorize]`屬性 toohello **TodoItemController**類別，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8645b-108">Add hello `[Authorize]` attribute toohello **TodoItemController** class, as follows.</span></span> <span data-ttu-id="8645b-109">toorestrict 存取只有 toospecific 方法，您也可以套用這個屬性只 toothose 方法，而不是 hello 類別。</span><span class="sxs-lookup"><span data-stu-id="8645b-109">toorestrict access only toospecific methods, you can also apply this attribute just toothose methods instead of hello class.</span></span> <span data-ttu-id="8645b-110">重新發佈 hello 伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="8645b-110">Republish hello server project.</span></span>

        [Authorize]
        public class TodoItemController : TableController<TodoItem>

* <span data-ttu-id="8645b-111">**Node.js 後端 (透過 Node.js 程式碼)** ：</span><span class="sxs-lookup"><span data-stu-id="8645b-111">**Node.js backend (via Node.js code)** :</span></span>  

    <span data-ttu-id="8645b-112">toorequire 驗證進行資料表存取，加入下列行 toohello Node.js 伺服器指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="8645b-112">toorequire authentication for table access, add hello following line toohello Node.js server script:</span></span>

        table.access = 'authenticated';

    <span data-ttu-id="8645b-113">如需詳細資訊，請參閱[How to： 需要驗證才能存取 tootables](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-auth)。</span><span class="sxs-lookup"><span data-stu-id="8645b-113">For more details, see [How to: Require authentication for access tootables](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-auth).</span></span> <span data-ttu-id="8645b-114">如何從您的網站，toodownload hello 快速入門的程式碼專案，請參閱的 toolearn [How to： 下載 hello Node.js 後端快速入門的程式碼專案使用 Git](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart)。</span><span class="sxs-lookup"><span data-stu-id="8645b-114">toolearn how toodownload hello quickstart code project from your site, see [How to: Download hello Node.js backend quickstart code project using Git](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart).</span></span>
