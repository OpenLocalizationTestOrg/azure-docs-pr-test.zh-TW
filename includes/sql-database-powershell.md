
## <a name="start-your-powershell-session"></a>啟動 PowerShell 工作階段
首先，您應該 hello 最新的 Azure PowerShell 安裝和執行。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。

> [!NOTE]
> 您使用 hello 時，才支援許多新的 SQL Database 功能[Azure Resource Manager 部署模型](../articles/azure-resource-manager/resource-group-overview.md)，因此範例會使用 hello [Azure SQL Database 的 PowerShell cmdlet](https://msdn.microsoft.com/library/azure/mt574084\(v=azure.300\).aspx)讓資源管理員. hello 服務管理 （傳統） 部署模型[Azure SQL Database 服務管理 cmdlet](https://msdn.microsoft.com/library/azure/dn546723\(v=azure.300\).aspx)皆支援回溯相容性，但我們建議您改用 hello 資源管理員 cmdlet。
> 
> 

執行 hello [**新增 AzureRmAccount** ](https://msdn.microsoft.com/library/azure/mt619267\(v=azure.300\).aspx) cmdlet，而且您會看到登入畫面 tooenter 您的認證。 使用 hello 相同，您會使用 toosign toohello Azure 入口網站中的認證。

```PowerShell
Add-AzureRmAccount
```

如果您有多個訂閱，使用 hello [**組 AzureRmContext** ](https://msdn.microsoft.com/library/azure/mt619263\(v=azure.300\).aspx) cmdlet tooselect 您的 PowerShell 工作階段應該使用哪一個訂用帳戶。 哪些訂閱 hello 目前 PowerShell 工作階段使用，toosee 執行[ **Get AzureRmContext**](https://msdn.microsoft.com/library/azure/mt619265\(v=azure.300\).aspx)。 toosee 所有您的訂用帳戶，執行[ **Get AzureRmSubscription**](https://msdn.microsoft.com/library/azure/mt619284\(v=azure.300\).aspx)。

```PowerShell
Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'
```
