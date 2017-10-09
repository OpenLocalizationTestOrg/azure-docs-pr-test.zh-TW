
## <a name="start-your-powershell-session"></a>啟動 PowerShell 工作階段
首先，您必須 toohave hello 最新[Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx)安裝且正在執行。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。

> [!NOTE]
> hello 範例在這個主題使用[Azure Resource Manager 部署模型](../articles/azure-resource-manager/resource-group-overview.md)，因此範例會使用 hello [Azure 資源管理員 cmdlet](http://msdn.microsoft.com/library/azure/mt125356.aspx)。 
> 
> 

執行 hello [**新增 AzureRmAccount** ](http://msdn.microsoft.com/library/mt619267.aspx)指令程式，而且您會看到與登入畫面 tooenter 您的認證。 使用 hello 相同，您會使用 toosign toohello Azure 入口網站中的認證。

    Add-AzureRmAccount

如果您有多個訂閱使用 hello [**組 AzureRmContext** ](http://msdn.microsoft.com/library/mt619263.aspx) cmdlet tooselect 您的 PowerShell 工作階段應該使用哪一個訂用帳戶。 哪些訂閱 hello 目前 PowerShell 工作階段使用，toosee 執行[ **Get AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx)。 toosee 所有您的訂用帳戶，執行[ **Get AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx)。

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

