
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-hello-connection-string-from-hello-azure-portal"></a><span data-ttu-id="0a02e-101">從 hello Azure 入口網站取得 hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="0a02e-101">Obtain hello connection string from hello Azure portal</span></span>
<span data-ttu-id="0a02e-102">使用 hello [Azure 入口網站](https://portal.azure.com/)tooobtain hello 連接字串需要您使用 Azure SQL Database 的用戶端程式 toointeract:</span><span class="sxs-lookup"><span data-stu-id="0a02e-102">Use hello [Azure portal](https://portal.azure.com/) tooobtain hello connection string necessary for your client program toointeract with Azure SQL Database:</span></span> 

1. <span data-ttu-id="0a02e-103">按一下 [瀏覽] >  [SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="0a02e-103">Click **BROWSE** > **SQL databases**.</span></span>
2. <span data-ttu-id="0a02e-104">Hello 您資料庫的名稱在 hello 篩選文字方塊輸入 hello 左上角附近的 hello **SQL 資料庫**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0a02e-104">Enter hello name of your database into hello filter text box near hello upper-left of hello **SQL databases** blade.</span></span>
3. <span data-ttu-id="0a02e-105">按一下您的資料庫 hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="0a02e-105">Click hello row for your database.</span></span>
4. <span data-ttu-id="0a02e-106">Hello 刀鋒視窗中出現為您的資料庫之後，請針對視覺上的方便性，您可以按一下 hello 標準最小化您用來瀏覽和資料庫篩選控制項 toocollapse hello 刀鋒。</span><span class="sxs-lookup"><span data-stu-id="0a02e-106">After hello blade appears for your database, for visual convenience you can click hello standard minimize controls toocollapse hello blades  you used for browsing and database filtering.</span></span> 
   
    ![篩選 tooisolate 您的資料庫][10-FilterDatabase]
5. <span data-ttu-id="0a02e-108">在 hello 刀鋒視窗中為您的資料庫，按一下 **顯示資料庫的連接字串**。</span><span class="sxs-lookup"><span data-stu-id="0a02e-108">On hello blade for your database, click **Show database connection strings**.</span></span>
6. <span data-ttu-id="0a02e-109">如果您想 toouse hello ADO.NET 連線庫，複製 hello 字串標示為**ADO**。</span><span class="sxs-lookup"><span data-stu-id="0a02e-109">If you intend toouse hello ADO.NET connection library, copy hello string labeled **ADO**.</span></span> 
   
    ![複製資料庫的 hello ADO 連接字串][20-CopyAdoConnectionString]
7. <span data-ttu-id="0a02e-111">在一種格式或另一個，貼入您的用戶端程式碼中的 hello 連接字串資訊。</span><span class="sxs-lookup"><span data-stu-id="0a02e-111">In one format or another, paste hello connection string information into your client program code.</span></span>

<span data-ttu-id="0a02e-112">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="0a02e-112">For more information, see:</span></span><br/><span data-ttu-id="0a02e-113">[連接字串與組態檔](http://msdn.microsoft.com/library/ms254494.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0a02e-113">[Connection Strings and Configuration Files](http://msdn.microsoft.com/library/ms254494.aspx).</span></span>

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
