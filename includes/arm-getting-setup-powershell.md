## <a name="setting-up-powershell-for-resource-manager-templates"></a><span data-ttu-id="69b1e-101">設定資源管理員範本的 PowerShell</span><span class="sxs-lookup"><span data-stu-id="69b1e-101">Setting up PowerShell for Resource Manager templates</span></span>
<span data-ttu-id="69b1e-102">您可以使用 Azure PowerShell 與資源管理員之前，您需要 toohave hello 右 Windows PowerShell 和 Azure PowerShell 版本。</span><span class="sxs-lookup"><span data-stu-id="69b1e-102">Before you can use Azure PowerShell with Resource Manager, you will need toohave hello right Windows PowerShell and Azure PowerShell versions.</span></span>

### <a name="verify-powershell-versions"></a><span data-ttu-id="69b1e-103">確認 PowerShell 版本</span><span class="sxs-lookup"><span data-stu-id="69b1e-103">Verify PowerShell versions</span></span>
<span data-ttu-id="69b1e-104">確認您有 Windows PowerShell 3.0 或 4.0 版。</span><span class="sxs-lookup"><span data-stu-id="69b1e-104">Verify you have Windows PowerShell version 3.0 or 4.0.</span></span> <span data-ttu-id="69b1e-105">toofind hello 版本的 Windows PowerShell 中，輸入這個命令在 Windows PowerShell 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="69b1e-105">toofind hello version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span></span>

    $PSVersionTable

<span data-ttu-id="69b1e-106">您會收到 hello 下列類型的資訊：</span><span class="sxs-lookup"><span data-stu-id="69b1e-106">You will receive hello following type of information:</span></span>

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


<span data-ttu-id="69b1e-107">請確認的 hello 值**Register-pssessionconfiguration** 3.0 或 4.0。</span><span class="sxs-lookup"><span data-stu-id="69b1e-107">Verify that hello value of **PSVersion** is 3.0 or 4.0.</span></span> <span data-ttu-id="69b1e-108">如果為否，請參閱 [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) 或 [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855)。</span><span class="sxs-lookup"><span data-stu-id="69b1e-108">If not, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="69b1e-109">設定 Azure 帳戶和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="69b1e-109">Set your Azure account and subscription</span></span>
<span data-ttu-id="69b1e-110">如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或申請[免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="69b1e-110">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="69b1e-111">開啟 Azure PowerShell 命令提示字元，並登入 tooAzure 與此命令。</span><span class="sxs-lookup"><span data-stu-id="69b1e-111">Open an Azure PowerShell command prompt and log on tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="69b1e-112">如果您有多個 Azure 訂用帳戶，則可以使用這個命令列出 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="69b1e-112">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="69b1e-113">您會收到 hello 下列類型的資訊：</span><span class="sxs-lookup"><span data-stu-id="69b1e-113">You will receive hello following type of information:</span></span>

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

<span data-ttu-id="69b1e-114">您可以在 hello Azure PowerShell 命令提示字元中執行這些命令來設定 hello 目前的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="69b1e-114">You can set hello current Azure subscription by running these commands at hello Azure PowerShell command prompt.</span></span> <span data-ttu-id="69b1e-115">Hello 括在引號，包括 hello < 和 > 字元內的所有項目取代 hello 正確的名稱。</span><span class="sxs-lookup"><span data-stu-id="69b1e-115">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

<span data-ttu-id="69b1e-116">如需有關 Azure 訂用帳戶和帳戶的詳細資訊，請參閱[如何： 連接 tooyour 訂閱](/powershell/azureps-cmdlets-docs#step-3-connect)。</span><span class="sxs-lookup"><span data-stu-id="69b1e-116">For more information about Azure subscriptions and accounts, see [How to: Connect tooyour subscription](/powershell/azureps-cmdlets-docs#step-3-connect).</span></span>

