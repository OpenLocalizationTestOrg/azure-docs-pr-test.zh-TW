
## <a name="start-your-powershell-session"></a><span data-ttu-id="0b2da-101">啟動 PowerShell 工作階段</span><span class="sxs-lookup"><span data-stu-id="0b2da-101">Start your PowerShell session</span></span>
<span data-ttu-id="0b2da-102">首先，您必須 toohave hello 最新[Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx)安裝且正在執行。</span><span class="sxs-lookup"><span data-stu-id="0b2da-102">First you need toohave hello latest [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) installed and running.</span></span> <span data-ttu-id="0b2da-103">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="0b2da-103">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

> [!NOTE]
> <span data-ttu-id="0b2da-104">hello 範例在這個主題使用[Azure Resource Manager 部署模型](../articles/azure-resource-manager/resource-group-overview.md)，因此範例會使用 hello [Azure 資源管理員 cmdlet](http://msdn.microsoft.com/library/azure/mt125356.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0b2da-104">hello examples in this topic use [Azure Resource Manager deployment model](../articles/azure-resource-manager/resource-group-overview.md), so examples use hello [Azure Resource Manager cmdlets](http://msdn.microsoft.com/library/azure/mt125356.aspx).</span></span> 
> 
> 

<span data-ttu-id="0b2da-105">執行 hello [**新增 AzureRmAccount** ](http://msdn.microsoft.com/library/mt619267.aspx)指令程式，而且您會看到與登入畫面 tooenter 您的認證。</span><span class="sxs-lookup"><span data-stu-id="0b2da-105">Run hello [**Add-AzureRmAccount**](http://msdn.microsoft.com/library/mt619267.aspx) cmdlet and you will be presented with a sign in screen tooenter your credentials.</span></span> <span data-ttu-id="0b2da-106">使用 hello 相同，您會使用 toosign toohello Azure 入口網站中的認證。</span><span class="sxs-lookup"><span data-stu-id="0b2da-106">Use hello same credentials that you use toosign in toohello Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="0b2da-107">如果您有多個訂閱使用 hello [**組 AzureRmContext** ](http://msdn.microsoft.com/library/mt619263.aspx) cmdlet tooselect 您的 PowerShell 工作階段應該使用哪一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0b2da-107">If you have multiple subscriptions use hello [**Set-AzureRmContext**](http://msdn.microsoft.com/library/mt619263.aspx) cmdlet tooselect which subscription your PowerShell session should use.</span></span> <span data-ttu-id="0b2da-108">哪些訂閱 hello 目前 PowerShell 工作階段使用，toosee 執行[ **Get AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0b2da-108">toosee what subscription hello current PowerShell session is using, run [**Get-AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx).</span></span> <span data-ttu-id="0b2da-109">toosee 所有您的訂用帳戶，執行[ **Get AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0b2da-109">toosee all your subscriptions, run [**Get-AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx).</span></span>

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

