
您可以在這段 Azure Friday 影片中，和 Scott Hanselman 與工程總經理 Karthik Raman 一起了解 Azure Cosmos DB 全域散發。

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

如需有關 Cosmos DB 中全域資料庫複寫運作方式的詳細資訊，請參閱[使用 Cosmos DB 來全域散發資料](../articles/documentdb/documentdb-distribute-data-globally.md)。

## <a id="addregion"></a>使用 Azure 入口網站新增全球資料庫區域
全球所有的 [Azure 區域][azureregions]均可使用 Azure Cosmos DB。 選取資料庫帳戶的預設一致性層級之後，您可以關聯一或多個區域 (取決於您對於預設一致性層級和全球發佈需求的選擇)。

1. 在 [Azure 入口網站](https://portal.azure.com/)的左列中，按一下 [Azure Cosmos DB]。
2. 在 [Azure Cosmos DB] 刀鋒視窗中，選取要修改的資料庫帳戶。
3. 在帳戶刀鋒視窗中，從功能表中按一下 [全域複寫資料]。
4. 在 [全域複寫資料] 刀鋒視窗中，按一下地圖中的區域以選取要新增或移除的區域，然後按一下 [儲存]。 新增區域需要費用，如需詳細資訊，請參閱[定價頁面](https://azure.microsoft.com/pricing/details/documentdb/)或[使用 DocumentDB 全球發佈資料](../articles/documentdb/documentdb-distribute-data-globally.md)一文。
   
    ![按一下地圖中的區域以新增或移除它們][1]
    
一旦您加入第二個區域，就會在入口網站中的 [全域複寫資料] 刀鋒視窗上啟用 [手動容錯移轉] 選項。 您可以使用此選項來測試容錯移轉程序，或變更主要寫入區域。 一旦您加入第三個區域，會在相同的刀鋒視窗上啟用 [容錯移轉優先順序] 選項，因此您可以變更讀取的容錯移轉順序。  

### <a name="selecting-global-database-regions"></a>選取全球資料庫區域
設定兩個或更多區域有兩個常見案例︰

1. 為使用者提供低延遲的資料存取 (無論使用者位於世界何處)
2. 新增業務持續性和災害復原 (BCDR) 的區域性復原功能

若要為使用者提供低延遲，建議部署應用程式，並且在應用程式使用者所在位置的對應區域中新增 Azure Cosmos DB。

對於 BCDR，建議根據[業務持續性和災害復原 (BCDR)：Azure 配對區域][bcdr]一文中所述的區域配對來新增區域。

<!--

## <a id="selectwriteregion"></a>Select the write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive the write (insert, upsert, replace, delete) requests. To set the active write region, do the following  


1. In the **Azure Cosmos DB** blade, select the database account to modify.
2. In the account blade, click **Replicate data globally** from the menu.
3. In the **Replicate data globally** blade, click **Manual Failover** from the top bar.
    ![Change the write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region to become the new write region, click the checkbox to confirm triggering a failover, and click OK
    ![Change the write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
