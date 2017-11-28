
## <a name="start-your-powershell-session"></a><span data-ttu-id="f8695-101">啟動 PowerShell 工作階段</span><span class="sxs-lookup"><span data-stu-id="f8695-101">Start your PowerShell session</span></span>
<span data-ttu-id="f8695-102">首先，您必須安裝並執行最新的 [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="f8695-102">First you need to have the latest [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) installed and running.</span></span> <span data-ttu-id="f8695-103">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="f8695-103">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

> [!NOTE]
> <span data-ttu-id="f8695-104">本主題中的範例會使用 [Azure Resource Manager 部署模型](../articles/azure-resource-manager/resource-group-overview.md)，因此範例使用 [Azure Resource Manager Cmdlet](http://msdn.microsoft.com/library/azure/mt125356.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f8695-104">The examples in this topic use [Azure Resource Manager deployment model](../articles/azure-resource-manager/resource-group-overview.md), so examples use the [Azure Resource Manager cmdlets](http://msdn.microsoft.com/library/azure/mt125356.aspx).</span></span> 
> 
> 

<span data-ttu-id="f8695-105">執行 [**Add-AzureRmAccount**](http://msdn.microsoft.com/library/mt619267.aspx) Cmdlet，您會看到要輸入認證的登入畫面。</span><span class="sxs-lookup"><span data-stu-id="f8695-105">Run the [**Add-AzureRmAccount**](http://msdn.microsoft.com/library/mt619267.aspx) cmdlet and you will be presented with a sign in screen to enter your credentials.</span></span> <span data-ttu-id="f8695-106">使用您用來登入 Azure 入口網站的相同認證。</span><span class="sxs-lookup"><span data-stu-id="f8695-106">Use the same credentials that you use to sign in to the Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="f8695-107">如果您有多個訂用帳戶，請使用 Set-[**AzureRmContext**](http://msdn.microsoft.com/library/mt619263.aspx) Cmdlet 選取您的 PowerShell 工作階段應該使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f8695-107">If you have multiple subscriptions use the [**Set-AzureRmContext**](http://msdn.microsoft.com/library/mt619263.aspx) cmdlet to select which subscription your PowerShell session should use.</span></span> <span data-ttu-id="f8695-108">若要查看目前的 PowerShell 工作階段正在使用哪個訂用帳戶，請執行 [**Get-AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f8695-108">To see what subscription the current PowerShell session is using, run [**Get-AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx).</span></span> <span data-ttu-id="f8695-109">若要查看所有訂用帳戶，請執行 [**Get-AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f8695-109">To see all your subscriptions, run [**Get-AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx).</span></span>

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

