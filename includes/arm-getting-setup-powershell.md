## <a name="setting-up-powershell-for-resource-manager-templates"></a>設定資源管理員範本的 PowerShell
您可以使用 Azure PowerShell 與資源管理員之前，您需要 toohave hello 右 Windows PowerShell 和 Azure PowerShell 版本。

### <a name="verify-powershell-versions"></a>確認 PowerShell 版本
確認您有 Windows PowerShell 3.0 或 4.0 版。 toofind hello 版本的 Windows PowerShell 中，輸入這個命令在 Windows PowerShell 命令提示字元。

    $PSVersionTable

您會收到 hello 下列類型的資訊：

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


請確認的 hello 值**Register-pssessionconfiguration** 3.0 或 4.0。 如果為否，請參閱 [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) 或 [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855)。

### <a name="set-your-azure-account-and-subscription"></a>設定 Azure 帳戶和訂用帳戶
如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或申請[免費試用](https://azure.microsoft.com/pricing/free-trial/)。

開啟 Azure PowerShell 命令提示字元，並登入 tooAzure 與此命令。

    Login-AzureRmAccount

如果您有多個 Azure 訂用帳戶，則可以使用這個命令列出 Azure 訂用帳戶。

    Get-AzureRmSubscription

您會收到 hello 下列類型的資訊：

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName :
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

您可以在 hello Azure PowerShell 命令提示字元中執行這些命令來設定 hello 目前的 Azure 訂用帳戶。 Hello 括在引號，包括 hello < 和 > 字元內的所有項目取代 hello 正確的名稱。

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

如需有關 Azure 訂用帳戶和帳戶的詳細資訊，請參閱[如何： 連接 tooyour 訂閱](/powershell/azureps-cmdlets-docs#step-3-connect)。

