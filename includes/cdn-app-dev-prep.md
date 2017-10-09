## <a name="prerequisites"></a>必要條件
我們可以撰寫 CDN 管理程式碼之前，我們需要 toodo 某些準備 tooenable 我們的程式碼 toointeract 以 hello Azure 資源管理員。  toodo，您將需要：

* 建立資源群組 toocontain hello 我們在本教學課程中建立的 CDN 設定檔
* 設定 Azure Active Directory tooprovide 驗證應用程式
* 套用 toohello 資源群組，以便只有授權的使用者從我們的 Azure AD 租用戶可以互動與我們的 CDN 設定檔的權限

### <a name="creating-hello-resource-group"></a>建立 hello 資源群組
1. 登入 hello [Azure 入口網站](https://portal.azure.com)。
2. 按一下 hello**新增**中 hello 左上方的按鈕，然後**管理**，和**資源群組**。

    ![建立新的資源群組](./media/cdn-app-dev-prep/cdn-new-rg-1-include.png)
3. 呼叫您的資源群組 CdnConsoleTutorial 。  選取您的訂用帳戶，並選擇離您最近的位置。  如果您希望，您可以按一下 hello **Pin toodashboard**核取方塊 toopin hello 資源群組 toohello 儀表板 hello 入口網站中的。  這會讓它更容易 toofind 更新版本。  進行選擇之後，按一下 [建立] 。

    ![命名 hello 資源群組](./media/cdn-app-dev-prep/cdn-new-rg-2-include.png)
4. 建立 hello 資源群組時，如果您未將其釘選 tooyour 儀表板之後，可以找到按一下**瀏覽**，然後**資源群組**。  按一下 hello 資源群組 tooopen 它。  請記下您的**訂用帳戶 ID**。  我們稍後將會用到此資訊。

    ![命名 hello 資源群組](./media/cdn-app-dev-prep/cdn-subscription-id-include.png)

### <a name="creating-hello-azure-ad-application-and-applying-permissions"></a>建立 hello Azure AD 應用程式，並套用權限
有兩種方式與 Azure Active Directory tooapp 驗證： 個別使用者或服務主體。 服務主體是在 Windows 中的類似 tooa 服務帳戶。  而不是授與特定使用者權限 toointeract hello CDN 設定檔，我們改為授權 hello toohello 服務主體。  服務主體通常用於自動化的非互動式處理程序。  雖然本教學課程撰寫互動式主控台應用程式，我們將焦點放在 hello 服務主體的方法。

建立服務主體包含數個步驟，其中包括建立 Azure Active Directory 應用程式。  toodo，我們會太[遵循本教學課程](../articles/resource-group-create-service-principal-portal.md)。

> [!IMPORTANT]
> Hello 中的所有 hello 步驟都是確定 toofollow[連結教學課程](../articles/resource-group-create-service-principal-portal.md)。  您必須如所述方式確實完成，這點「極為重要」。  請確定 toonote 您**租用戶識別碼**，**租用戶網域名稱**(通常*。 onmicrosoft.com*網域除非您指定自訂的網域)，**用戶端識別碼**，和**用戶端驗證金鑰**，因為我們將需要這些更新。  要非常小心 tooguard 您**用戶端識別碼**和**用戶端驗證金鑰**，如這些認證可以是任何人使用 tooexecute 作業以 hello 服務主體。
>
> 當您設定多租用戶應用程式命名為 toohello 步驟，選取**否**。
>
> 當您取得 toohello 步驟[指派應用程式 toorole](../articles/azure-resource-manager/resource-group-create-service-principal-portal.md#assign-application-to-role)，使用我們稍早建立的 hello 資源群組*CdnConsoleTutorial*，但不 hello**讀取器**角色，指派hello **CDN 設定檔參與者**角色。  指派 hello 應用程式 hello 之後**CDN 設定檔參與者**上資源群組中，傳回 toothis 教學課程中的角色。 
>
>

一旦您已建立服務主體，並已指派 hello **CDN 設定檔參與者**角色、 hello**使用者**刀鋒視窗中的資源群組應該看起來類似 toothis。

![[使用者] 刀鋒視窗](./media/cdn-app-dev-prep/cdn-service-principal-include.png)

### <a name="interactive-user-authentication"></a>互動式使用者驗證
如果，而不是服務主體，而不是互動式的個別使用者驗證，hello 程序就會是非常類似 toothat 服務主體。  事實上，您將需要 toofollow hello 相同的程序，但進行一些微幅變更。

> [!IMPORTANT]
> 如果您選擇 toouse 個別使用者驗證，而不是服務主體僅請遵循下列步驟。
>
>

1. 當您建立應用程式，而不是 **Web 應用程式**時，請選擇 [原生應用程式]。

    ![原生應用程式](./media/cdn-app-dev-prep/cdn-native-application-include.png)
2. 在 hello 下一個頁面上，系統會提示**重新導向 URI**。  hello URI 將不會進行驗證，但是請記住您的輸入。  稍後您將會用到此資訊。
3. 沒有任何需要 toocreate**用戶端驗證金鑰**。
4. 而不是指派服務主體的 toohello **CDN 設定檔參與者**角色中，我們會 tooassign 個別使用者或群組。  在此範例中，您可以看到，我指派*CDN 示範使用者*toohello **CDN 設定檔參與者**角色。  

    ![個別使用者存取](./media/cdn-app-dev-prep/cdn-aad-user-include.png)
