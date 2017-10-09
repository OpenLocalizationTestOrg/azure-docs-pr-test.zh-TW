
<br>

> [!NOTE]
> 如果系統管理員已提供給您使用者名稱與密碼，很有可能您已經有工作或學校識別碼 (有時也稱做「組織識別碼」)。 如果是這樣，您可以立即開始 toouse 您的 Azure 帳戶 tooaccess 需要其中一個的 Azure 資源。 如果您發現您無法使用這些資源，您可能需要 tooreturn toothis 發行項的說明。 如需詳細資訊，請參閱[您可以使用的帳戶登入](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts)和[如何為 Azure 訂用帳戶已相關的 tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir)。
> 
> 

hello 步驟很簡單。 您需要 toolocate 您帶正負號上 hello Azure 傳統入口網站中的身分識別，探索您的預設 Azure Active Directory 網域，並加入新的使用者 tooit 為 Azure 的共同管理員。

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a>在 hello Azure 傳統入口網站中尋找您的預設目錄
開始登入以 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)與您個人的 Microsoft 帳戶識別碼。 在登入後，捲動 hello 左邊的藍色 hello 面板，並按一下**ACTIVE DIRECTORY**。

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

讓我們開始在 Azure 中找出您身分識別的部分資訊。 您應該會看到類似下 hello 遵循 hello 主窗格中，顯示您有一個預設目錄。

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

讓我們找到更多的相關資訊。 按一下 hello 預設目錄資料列，讓您回到成 hello 預設目錄屬性。  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

tooview hello 預設網域名稱，按一下 **網域**。

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

這裡您應該要建立 hello Azure 帳戶後，Azure Active Directory 建立個人的預設網域的雜湊值 （從文字字串所產生的數字） 可以 toosee 您個人的 id 做為 onmicrosoft.com 的子網域。這是 hello 網域 toowhich 現在要加入新的使用者。

## <a name="creating-a-new-user-in-hello-default-domain"></a>Hello 預設網域中建立新的使用者
按一下 [使用者]，然後尋找您的單一個人帳戶。 您應該會看到在 hello**源自**資料行，它是**Microsoft 帳戶**。 我們希望 toocreate 中預設的使用者。 Azure Active Directory 的 onmicrosoft.com 網域。

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

我們會 toofollow[這些指示](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1)在 hello 接下來的步驟，但使用特定的範例。

在 hello hello 頁面底部，按一下**+ 新增使用者**。 在出現的 hello 頁面上，輸入 hello 新的使用者名稱，並讓 hello**使用者類型****您組織中的新使用者**。 此範例中的 hello 新的使用者名稱是`ahmet`。 選取您所探索的 hello 預設網域先前做為 hello ahmet 的電子郵件地址的網域。 按一下 完成 hello 下一步箭頭。

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

Ahmet，加入更多詳細資料，但請確定 tooselect hello 適當**角色**值。 它是簡單 toouse**全域管理員**正在 toomake 確定項目，但如果您可以使用較小者的角色，這是個不錯的主意。 這個範例會使用 hello**使用者**角色。 (在[依據角色的系統管理員權限](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1)中取得更多資訊。)請勿啟用多重要素驗證，除非您想 toouse 多重要素驗證每個記錄檔中作業。 當您完成時，請按一下 hello 下一步箭頭。

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

按一下 hello**建立**按鈕 toogenerate 和 Ahmet 顯示暫時密碼。

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

複製 hello 使用者名稱的電子郵件地址，或使用**傳送密碼在電子郵件**。 您稍後將需要 hello 資訊 toolog 上。

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

現在您應該會看到新的使用者，hello **Ahmet hello 開發人員**、 從 Azure Active Directory 來源。 您已建立 hello 新的工作或學校身分識別與 Azure Active Directory。 不過，這個身分識別還沒有權限 toouse Azure 資源。

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

如果您使用**傳送密碼在電子郵件**，會傳送 hello 下列種類的電子郵件。

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a>為訂用帳戶新增 Azure 的共同管理員權限
現在您需要 tooadd hello 新使用者訂用帳戶的共同管理員身分讓 hello 新的使用者可以登入 toohello 管理入口網站。 在 [hello] 面板左下方按一下的 toodo**設定**。

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

在 hello 主要設定 區域中，按一下 **管理員**在 hello 頂端，而且您應該會看到只有您個人 Microsoft 帳戶的身分識別。 在 hello hello 頁面底部，按一下**+ 加入**toospecify 共同管理員。 在這裡，輸入 hello hello 您建立，包括您的預設網域的新使用者的電子郵件地址。 Hello 的下一個螢幕擷取畫面所示，綠色的核取記號會出現 下一步 toohello 使用者 hello 預設目錄。 請記住 tooselect 所有您想要此使用者 toobe 無法 tooadminister hello 訂用帳戶。

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

完成後，您現在應會看到兩個使用者，包括新的共同管理員身分識別。 登出 hello 入口網站。

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a>登入並變更 hello 新使用者的密碼
Hello 建立新的使用者身分登入。

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

您會立即提示的 toocreate 新密碼。

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

您應該看起來像下列 hello 的成功報償。

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a>後續步驟
您現在可以使用您新的 Azure Active Directory 身分識別 toouse [Azure 資源群組範本](../articles/xplat-cli-azure-resource-manager.md)。

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how tooset them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@aztrainpassxxxxxoutlook.onmicrosoft.com
    Password: *********
    /info:    Added subscription Azure Pass
    info:    Setting subscription Azure Pass as default
    +
    info:    login command OK
    ralph@local:~$ azure config mode arm
    info:    New mode is arm
    ralph@local:~$ azure group list
    info:    Executing command group list
    + Listing resource groups
    info:    No matched resource groups were found
    info:    group list command OK
    ralph@local:~$ azure group create newgroup westus
    info:    Executing command group create
    + Getting resource group newgroup
    + Creating resource group newgroup
    info:    Created resource group newgroup
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/newgroup
    data:    Name:                newgroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags:
    data:
    info:    group create command OK
