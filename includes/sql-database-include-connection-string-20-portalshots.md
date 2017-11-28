
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-the-connection-string-from-the-azure-portal"></a><span data-ttu-id="28ec5-101">從 Azure 入口網站取得連接字串</span><span class="sxs-lookup"><span data-stu-id="28ec5-101">Obtain the connection string from the Azure portal</span></span>
<span data-ttu-id="28ec5-102">使用 [Azure 入口網站](https://portal.azure.com/) 來取得用戶端程式與 Azure SQL Database 進行互動所需的連接字串：</span><span class="sxs-lookup"><span data-stu-id="28ec5-102">Use the [Azure portal](https://portal.azure.com/) to obtain the connection string necessary for your client program to interact with Azure SQL Database:</span></span> 

1. <span data-ttu-id="28ec5-103">按一下 [瀏覽] >  [SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="28ec5-103">Click **BROWSE** > **SQL databases**.</span></span>
2. <span data-ttu-id="28ec5-104">在 [SQL 資料庫]  刀鋒視窗左上角附近的篩選文字方塊中輸入您的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="28ec5-104">Enter the name of your database into the filter text box near the upper-left of the **SQL databases** blade.</span></span>
3. <span data-ttu-id="28ec5-105">按一下資料庫的資料列。</span><span class="sxs-lookup"><span data-stu-id="28ec5-105">Click the row for your database.</span></span>
4. <span data-ttu-id="28ec5-106">在刀鋒視窗顯示您的資料庫之後，為了閱讀方便您可以按一下標準最小化控制項來摺疊用於瀏覽和資料庫篩選的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="28ec5-106">After the blade appears for your database, for visual convenience you can click the standard minimize controls to collapse the blades  you used for browsing and database filtering.</span></span> 
   
    ![篩選以隔離您的資料庫][10-FilterDatabase]
5. <span data-ttu-id="28ec5-108">在您資料庫的刀鋒視窗上，按一下 [顯示資料庫連接字串] 。</span><span class="sxs-lookup"><span data-stu-id="28ec5-108">On the blade for your database, click **Show database connection strings**.</span></span>
6. <span data-ttu-id="28ec5-109">如果您想要使用 ADO.NET 連線庫，請複製標示為 **ADO**的字串。</span><span class="sxs-lookup"><span data-stu-id="28ec5-109">If you intend to use the ADO.NET connection library, copy the string labeled **ADO**.</span></span> 
   
    ![複製資料庫的 ADO 連接字串][20-CopyAdoConnectionString]
7. <span data-ttu-id="28ec5-111">以其中一種格式，將連接字串資訊貼入您的用戶端程式碼中。</span><span class="sxs-lookup"><span data-stu-id="28ec5-111">In one format or another, paste the connection string information into your client program code.</span></span>

<span data-ttu-id="28ec5-112">如需詳細資訊，請參閱</span><span class="sxs-lookup"><span data-stu-id="28ec5-112">For more information, see:</span></span><br/><span data-ttu-id="28ec5-113">[連接字串與組態檔](http://msdn.microsoft.com/library/ms254494.aspx)。</span><span class="sxs-lookup"><span data-stu-id="28ec5-113">[Connection Strings and Configuration Files](http://msdn.microsoft.com/library/ms254494.aspx).</span></span>

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
