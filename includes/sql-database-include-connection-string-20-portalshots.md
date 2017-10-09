
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-hello-connection-string-from-hello-azure-portal"></a>從 hello Azure 入口網站取得 hello 連接字串
使用 hello [Azure 入口網站](https://portal.azure.com/)tooobtain hello 連接字串需要您使用 Azure SQL Database 的用戶端程式 toointeract: 

1. 按一下 [瀏覽] >  [SQL Database]。
2. Hello 您資料庫的名稱在 hello 篩選文字方塊輸入 hello 左上角附近的 hello **SQL 資料庫**刀鋒視窗。
3. 按一下您的資料庫 hello 資料列。
4. Hello 刀鋒視窗中出現為您的資料庫之後，請針對視覺上的方便性，您可以按一下 hello 標準最小化您用來瀏覽和資料庫篩選控制項 toocollapse hello 刀鋒。 
   
    ![篩選 tooisolate 您的資料庫][10-FilterDatabase]
5. 在 hello 刀鋒視窗中為您的資料庫，按一下 **顯示資料庫的連接字串**。
6. 如果您想 toouse hello ADO.NET 連線庫，複製 hello 字串標示為**ADO**。 
   
    ![複製資料庫的 hello ADO 連接字串][20-CopyAdoConnectionString]
7. 在一種格式或另一個，貼入您的用戶端程式碼中的 hello 連接字串資訊。

如需詳細資訊，請參閱：<br/>[連接字串與組態檔](http://msdn.microsoft.com/library/ms254494.aspx)。

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
