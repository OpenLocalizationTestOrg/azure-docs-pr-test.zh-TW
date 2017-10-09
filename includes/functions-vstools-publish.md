1. 在**方案總管 中**，hello 專案上按一下滑鼠右鍵，然後選取**發行**。 選擇 新建，然後按一下發佈。 

    ![發佈新建的函式應用程式](./media/functions-vstools-publish/functions-vstools-publish-new-function-app.png)

2. 如果您已經沒有連接 Visual Studio tooyour Azure 帳戶，按一下**新增帳戶...**.  

3. 在 hello**建立 App Service**對話方塊中，使用 hello**主控**設定為下表中所指定的 hello: 

    ![Azure 本機執行階段](./media/functions-vstools-publish/functions-vstools-publish.png)

    | 設定      | 建議的值  | 說明                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **應用程式名稱** | 全域唯一的名稱 | 用以唯一識別新函式應用程式的名稱。 |
    | **訂用帳戶** | 選擇您的訂用帳戶 | hello Azure 訂用帳戶 toouse。 |
    | **[資源群組](../articles/azure-resource-manager/resource-group-overview.md)** | myResourceGroup |  函式應用程式的群組哪些 toocreate hello 資源的名稱。 |
    | **[App Service 方案](../articles/azure-functions/functions-scale.md)** | 取用方案 | 請確定 toochoose hello**耗用量**下**大小**當您建立新的計畫。  |
    | **[儲存體帳戶](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)** | 全域唯一的名稱 | 使用現有的儲存體帳戶或建立新帳戶。   |

4. 按一下**建立**toocreate 函式的應用程式在 Azure 中使用這些設定。 Hello 佈建完成之後，請記下 hello**網站 URL**值，這是應用程式函式，在 Azure 中的 hello 位址。 

    ![Azure 本機執行階段](./media/functions-vstools-publish/functions-vstools-publish-profile.png)
