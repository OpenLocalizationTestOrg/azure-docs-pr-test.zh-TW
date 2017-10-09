## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a>準備 Azure 資源管理員要求的 tooauthenticate
您必須驗證您在使用 hello 的資源執行的所有 hello 作業[Azure Resource Manager] [ lnk-authenticate-arm]與 Azure Active Directory (AD)。 hello 最簡單的方式 tooconfigure 這是 toouse PowerShell 或 Azure CLI。

安裝 hello [Azure PowerShell cmdlet] [ lnk-powershell-install]繼續進行之前。

hello 下列步驟顯示如何使用 PowerShell 建立 AD 應用程式的密碼驗證設定 tooset。 您可以在標準 PowerShell 工作階段中執行這些命令。

1. 登入 tooyour Azure 訂用帳戶使用 hello 下列命令：

    ```powershell
    Login-AzureRmAccount
    ```

1. 如果您有多個 Azure 訂用帳戶，授與存取 tooall 登入 tooAzure hello 與認證相關聯的 Azure 訂用帳戶。 使用下列命令 toolist hello Azure 訂用帳戶可讓您 toouse hello:

    ```powershell
    Get-AzureRMSubscription
    ```

    使用下列命令 tooselect 訂用帳戶的 toouse toorun hello 命令 toomanage IoT 中樞的 hello。 您可以使用 hello 訂用帳戶名稱或識別碼，從 hello 輸出 hello 前一個命令：

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. 請記下您的 **TenantId** 和 **SubscriptionId**。 您稍後需要這些資訊。
3. 建立新的 Azure Active Directory 應用程式，使用下列命令、 取代 hello 預留位置 hello:
   
   * **{Display name}：**應用程式的顯示名稱，如 **MySampleApp**
   * **{首頁 URL}:** hello hello 首頁，應用程式的 URL，例如**http://mysampleapp/home**。 此 URL 不需要 toopoint tooa 實際的應用程式。
   * **{Application identifier}：**唯一識別碼，如 **http://mysampleapp**。 此 URL 不需要 toopoint tooa 實際的應用程式。
   * **{Password}:** tooauthenticate 搭配您的應用程式密碼。
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. 請記下 hello **ApplicationId** hello 應用程式所建立。 您稍後需要此資訊。
5. 建立新的服務主體使用下列命令、 取代 hello **{MyApplicationId}**以 hello **ApplicationId** hello 上一個步驟：
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. 設定角色指派，使用下列命令、 取代 hello **{MyApplicationId}**與您**ApplicationId**。
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

您現在已經完成建立 hello Azure AD 應用程式，可讓您 tooauthenticate 從您自訂的 C# 應用程式。 您需要下列值稍後在本教學課程中的 hello:

* TenantId
* SubscriptionId
* ApplicationId
* 密碼

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
