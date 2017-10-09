
您可以在這段 Azure Friday 影片中，和 Scott Hanselman 與工程總經理 Karthik Raman 一起了解 Azure Cosmos DB 全域散發。

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

如需有關 Cosmos DB 中全域資料庫複寫運作方式的詳細資訊，請參閱[使用 Cosmos DB 來全域散發資料](../articles/documentdb/documentdb-distribute-data-globally.md)。

## <a id="addregion"></a>新增使用 hello Azure 入口網站的全域資料庫區域
全球所有的 [Azure 區域][azureregions]均可使用 Azure Cosmos DB。 選取您的資料庫帳戶的 hello 預設一致性層級之後, 您可以將一或多個區域 （取決於您所選擇的預設一致性層級和全域發佈需求） 產生關聯。

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，在 hello 左的工具列中按一下**Azure Cosmos DB**。
2. 在 hello **Azure Cosmos DB**刀鋒視窗中，選取 hello 資料庫帳戶 toomodify。
3. 在 hello 帳戶刀鋒視窗中，按一下 **資料會進行全域複寫**hello 功能表。
4. 在 hello**資料會進行全域複寫**刀鋒視窗中，選取 hello 區域 tooadd 或按一下區域 hello 對應中的移除，然後按一下**儲存**。 沒有成本 tooadding 區域，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/documentdb/)或 hello[全域使用 DocumentDB 資料散發](../articles/documentdb/documentdb-distribute-data-globally.md)文件以取得詳細資訊。
   
    ![按一下 hello 對應 tooadd 中的 hello 區域，或將它們移除][1]
    
一旦您加入第二個區域，hello**手動容錯移轉**hello 上已啟用選項**資料會進行全域複寫**hello 入口網站中的刀鋒視窗。 您可以使用此選項 tootest hello 容錯移轉程序，或變更 hello 主要寫入區域。 一旦您加入第三個區域，hello**容錯移轉優先權**上啟用選項 hello 相同刀鋒視窗，因此您可以變更為讀取 hello 容錯移轉順序。  

### <a name="selecting-global-database-regions"></a>選取全球資料庫區域
設定兩個或更多區域有兩個常見案例︰

1. 傳遞低延遲存取 toodata tooend 使用者，不論它們位於周圍 hello 球體
2. 新增業務持續性和災害復原 (BCDR) 的區域性復原功能

對於提供低延遲 tooend 位使用者，建議您使用的 toodeploy 兩者 hello 應用程式，然後新增位於 Azure Cosmos DB hello 區域中，它會對應 toowhere hello 應用程式的使用者。

Bcdr，建議您使用 hello 中所述的 hello 區域配對為基礎的 tooadd 區域[業務續航力和災害復原 (BCDR): Azure 配對區域][ bcdr]發行項。

<!--

## <a id="selectwriteregion"></a>Select hello write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive hello write (insert, upsert, replace, delete) requests. tooset hello active write region, do hello following  


1. In hello **Azure Cosmos DB** blade, select hello database account toomodify.
2. In hello account blade, click **Replicate data globally** from hello menu.
3. In hello **Replicate data globally** blade, click **Manual Failover** from hello top bar.
    ![Change hello write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region toobecome hello new write region, click hello checkbox tooconfirm triggering a failover, and click OK
    ![Change hello write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
