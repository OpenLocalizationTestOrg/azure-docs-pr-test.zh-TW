
根據預設，可以匿名方式叫用 Mobile Apps 後端中的 API。 接下來，您需要 toorestrict 存取 tooonly 驗證用戶端。  

* **Node.js 回結束 （透過 hello Azure 入口網站)** :  

    在 Mobile Apps 的 [設定] 中，按一下 [簡單資料表]，然後選取資料表。 按一下 變更權限，選取所有權限的 僅驗證存取，然後按一下儲存。
* **.NET 後端 (C#)**：  

    在 hello 伺服器專案中，瀏覽過**控制器** > **TodoItemController.cs**。 新增 hello`[Authorize]`屬性 toohello **TodoItemController**類別，如下所示。 toorestrict 存取只有 toospecific 方法，您也可以套用這個屬性只 toothose 方法，而不是 hello 類別。 重新發佈 hello 伺服器專案。

        [Authorize]
        public class TodoItemController : TableController<TodoItem>

* **Node.js 後端 (透過 Node.js 程式碼)** ：  

    toorequire 驗證進行資料表存取，加入下列行 toohello Node.js 伺服器指令碼的 hello:

        table.access = 'authenticated';

    如需詳細資訊，請參閱[How to： 需要驗證才能存取 tootables](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-auth)。 如何從您的網站，toodownload hello 快速入門的程式碼專案，請參閱的 toolearn [How to： 下載 hello Node.js 後端快速入門的程式碼專案使用 Git](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart)。
