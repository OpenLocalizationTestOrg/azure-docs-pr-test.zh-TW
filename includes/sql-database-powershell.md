
## <a name="start-your-powershell-session"></a><span data-ttu-id="d0fd5-101">啟動 PowerShell 工作階段</span><span class="sxs-lookup"><span data-stu-id="d0fd5-101">Start your PowerShell session</span></span>
<span data-ttu-id="d0fd5-102">首先，您需安裝並執行最新的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d0fd5-102">First, you should have the latest Azure PowerShell installed and running.</span></span> <span data-ttu-id="d0fd5-103">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="d0fd5-103">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

> [!NOTE]
> <span data-ttu-id="d0fd5-104">SQL Database 的許多新功能只有在使用 [Azure Resource Manager 部署模型](../articles/azure-resource-manager/resource-group-overview.md)時才支援，所以範例會使用適用於 Resource Manager 的 [Azure SQL Database PowerShell Cmdlet](https://msdn.microsoft.com/library/azure/mt574084\(v=azure.300\).aspx)。</span><span class="sxs-lookup"><span data-stu-id="d0fd5-104">Many new features of SQL Database are only supported when you are using the [Azure Resource Manager deployment model](../articles/azure-resource-manager/resource-group-overview.md), so examples use the [Azure SQL Database PowerShell cmdlets](https://msdn.microsoft.com/library/azure/mt574084\(v=azure.300\).aspx) for Resource Manager.</span></span> <span data-ttu-id="d0fd5-105">服務管理 (傳統) 部署模型 [Azure SQL Database 服務管理 Cmdlet](https://msdn.microsoft.com/library/azure/dn546723\(v=azure.300\).aspx) 支援回溯相容性，但是建議使用 Resource Manager Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d0fd5-105">The service management (classic) deployment model [Azure SQL Database Service Management cmdlets](https://msdn.microsoft.com/library/azure/dn546723\(v=azure.300\).aspx) are supported for backward compatibility, but we recommend you use the Resource Manager cmdlets.</span></span>
> 
> 

<span data-ttu-id="d0fd5-106">執行 [**Add-AzureRmAccount**](https://msdn.microsoft.com/library/azure/mt619267\(v=azure.300\).aspx) Cmdlet，您會看到要輸入認證的登入畫面。</span><span class="sxs-lookup"><span data-stu-id="d0fd5-106">Run the [**Add-AzureRmAccount**](https://msdn.microsoft.com/library/azure/mt619267\(v=azure.300\).aspx) cmdlet, and you will be presented with a sign-in screen to enter your credentials.</span></span> <span data-ttu-id="d0fd5-107">使用您用來登入 Azure 入口網站的相同認證。</span><span class="sxs-lookup"><span data-stu-id="d0fd5-107">Use the same credentials that you use to sign in to the Azure portal.</span></span>

```PowerShell
Add-AzureRmAccount
```

<span data-ttu-id="d0fd5-108">如果您有多個訂用帳戶，請使用 [**Set-AzureRmContext**](https://msdn.microsoft.com/library/azure/mt619263\(v=azure.300\).aspx) Cmdlet 選取您的 PowerShell 工作階段應該使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d0fd5-108">If you have multiple subscriptions, use the [**Set-AzureRmContext**](https://msdn.microsoft.com/library/azure/mt619263\(v=azure.300\).aspx) cmdlet to select which subscription your PowerShell session should use.</span></span> <span data-ttu-id="d0fd5-109">若要查看目前的 PowerShell 工作階段正在使用哪個訂用帳戶，請執行 [**Get-AzureRmContext**](https://msdn.microsoft.com/library/azure/mt619265\(v=azure.300\).aspx)。</span><span class="sxs-lookup"><span data-stu-id="d0fd5-109">To see what subscription the current PowerShell session is using, run [**Get-AzureRmContext**](https://msdn.microsoft.com/library/azure/mt619265\(v=azure.300\).aspx).</span></span> <span data-ttu-id="d0fd5-110">若要查看所有訂用帳戶，請執行 [**Get-AzureRmSubscription**](https://msdn.microsoft.com/library/azure/mt619284\(v=azure.300\).aspx)。</span><span class="sxs-lookup"><span data-stu-id="d0fd5-110">To see all your subscriptions, run [**Get-AzureRmSubscription**](https://msdn.microsoft.com/library/azure/mt619284\(v=azure.300\).aspx).</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'
```
