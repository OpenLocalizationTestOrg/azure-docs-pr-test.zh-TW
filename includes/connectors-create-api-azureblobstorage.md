### <a name="prerequisites"></a>必要條件
* Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)
* [Azure Blob 儲存體帳戶](../articles/storage/common/storage-create-storage-account.md)包括 hello 儲存體帳戶名稱和其存取金鑰。 這項資訊會列在 hello hello hello Azure 入口網站中的儲存體帳戶的屬性。 深入了解 [Azure 儲存體](../articles/storage/common/storage-introduction.md)。

邏輯應用程式中使用 Azure Blob 儲存體帳戶前, 請 tooyour Azure Blob 儲存體帳戶連接。 您可以輕鬆地在 hello Azure 入口網站應用程式邏輯中。  

連線使用下列步驟的 hello tooyour Azure Blob 儲存體帳戶：  

1. 建立邏輯應用程式。 在 hello Logic Apps 設計工具加入觸發程序，然後再加入動作。 選取**顯示 Microsoft managed Api**在 hello 下拉式清單中，然後輸入"blob"hello [搜尋] 方塊中。 選取其中一個 hello 動作：  
   
    ![Azure Blob 儲存體連接的建立步驟](./media/connectors-create-api-azureblobstorage/azureblobstorage-1.png)  
2. 如果您先前尚未建立任何連線 tooAzure 存放裝置，會提示您輸入 hello 連接詳細資料：   
   
    ![Azure Blob 儲存體連接的建立步驟](./media/connectors-create-api-azureblobstorage/connection-details.png)  
3. 輸入 hello 儲存體帳戶詳細資料。 具有星號的屬性為必要項目。
   
   | 屬性 | 詳細資料 |
   | --- | --- |
   | 連線名稱 * |為連接器輸入任何名稱。 |
   | Azure 儲存體帳戶名稱 * |輸入 hello 儲存體帳戶名稱。 hello 儲存體帳戶名稱會顯示在 hello hello Azure 入口網站中的儲存體屬性。 |
   | Azure 儲存體帳戶存取金鑰 * |輸入 hello 儲存體帳戶金鑰。 hello 存取金鑰會顯示在 hello hello Azure 入口網站中的儲存體屬性。 |
   
    這些認證是使用的 tooauthorize 您邏輯應用程式 tooconnect，並存取您的資料。 
4. 選取 [ **建立**]。
5. 請注意 hello 連線已建立。 現在，繼續進行其他 hello 邏輯應用程式中的步驟： 
   
    ![Azure Blob 儲存體連接的建立步驟](./media/connectors-create-api-azureblobstorage/azureblobstorage-3.png)  

