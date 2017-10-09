## <a name="prepare-for-akv-integration"></a>準備進行 AKV 整合
toouse Azure 金鑰保存庫整合 tooconfigure SQL Server VM，有數個先決條件： 

1. [安裝 Azure PowerShell](#install-azure-powershell)
2. [建立 Azure Active Directory](#create-an-azure-active-directory)
3. [建立金鑰保存庫](#create-a-key-vault)

hello 下列各節說明這些先決條件和 hello 需要 toocollect toolater 執行 hello PowerShell cmdlet 的資訊。

### <a name="install-azure-powershell"></a>安裝 Azure PowerShell
請確定您已安裝 hello 最新的 Azure PowerShell SDK。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。

### <a name="create-an-azure-active-directory"></a>建立 Azure Active Directory
首先，您需要 toohave [Azure Active Directory](https://azure.microsoft.com/trial/get-started-active-directory/) (AAD) 您的訂用帳戶中。 許多優點，這可讓您 toogrant 權限 tooyour 金鑰保存庫特定的使用者和應用程式。

接下來，向 AAD 註冊應用程式。 如此可讓您的服務主體帳戶具有存取 tooyour 金鑰保存庫必須在您的 VM。 本文 hello Azure 金鑰保存庫，您可以在 hello 中找到這些步驟[與 Azure Active Directory 註冊應用程式](../articles/key-vault/key-vault-get-started.md#register) 區段中，或者您可以看到在 hello 螢幕擷取畫面和步驟，hello **hello 應用程式取得身分識別區段**的[此部落格文章](http://blogs.technet.com/b/kv/archive/2015/01/09/azure-key-vault-step-by-step.aspx)。 在之前完成這些步驟，請注意，您需要下列資訊，當您啟用 SQL VM 上的 Azure 金鑰保存庫整合之後需要這個註冊期間 toocollect hello。

* Hello 應用程式會加入後，會發現 hello**用戶端識別碼**上 hello**設定** 索引標籤。 ![Azure Active Directory 用戶端識別碼](./media/virtual-machines-sql-server-akv-prepare/aad-client-id.png)
  
    hello 用戶端識別碼指派更新 toohello **$spName** hello PowerShell 指令碼 tooenable Azure 金鑰保存庫整合在 （服務主體名稱） 參數。 
* 此外，在這些步驟當您建立您的金鑰，複製您金鑰的 hello 密碼 hello 下列螢幕擷取畫面所示。 此金鑰的密碼指派更新 toohello **$spSecret** hello PowerShell 指令碼中的 （服務主體機密） 參數。  
    ![Azure Active Directory 密碼](./media/virtual-machines-sql-server-akv-prepare/aad-sp-secret.png)
* 您必須授權下列存取權限這個新用戶端識別碼 toohave hello:**加密**，**解密**， **wrapKey**， **unwrapKey**，**登**，和**確認**。 這是以 hello [Set-azurermkeyvaultaccesspolicy](https://msdn.microsoft.com/library/azure/mt603625.aspx) cmdlet。 如需詳細資訊，請參閱[授權 hello 應用程式 toouse hello 金鑰或密碼](../articles/key-vault/key-vault-get-started.md#authorize)。

### <a name="create-a-key-vault"></a>建立金鑰保存庫
在訂單 toouse Azure 金鑰保存庫 toostore hello 金鑰，您會在 VM 中使用加密，您會需要存取 tooa 金鑰保存庫。 如果尚未設定金鑰保存庫，建立一個 hello 中的 hello 步驟[開始使用 Azure 金鑰保存庫](../articles/key-vault/key-vault-get-started.md)主題。 之前完成這些步驟，請注意，當您啟用 SQL VM 上的 Azure 金鑰保存庫整合之後需要一些資訊，您需要 toocollect 期間，此設定。

當您取得 toohello 建立金鑰保存庫的步驟中，注意 hello 傳回**vaultUri**屬性，這是 hello 金鑰保存庫 URL。 在該，如下所示的步驟中所提供的 hello 範例 hello 金鑰保存庫名稱為 ContosoKeyVault，因此 hello 金鑰保存庫 URL 會是 https://contosokeyvault.vault.azure.net/。

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

hello 金鑰保存庫 URL 指派更新 toohello **$akvURL** hello PowerShell 指令碼 tooenable Azure 金鑰保存庫整合中的參數。

