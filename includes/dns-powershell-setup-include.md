## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="dba94-101">針對 Azure DNS 設定 Azure PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="dba94-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="dba94-102">開始之前</span><span class="sxs-lookup"><span data-stu-id="dba94-102">Before you begin</span></span>

<span data-ttu-id="dba94-103">確認您擁有 hello 開始您的組態之前，下列項目。</span><span class="sxs-lookup"><span data-stu-id="dba94-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="dba94-104">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dba94-104">An Azure subscription.</span></span> <span data-ttu-id="dba94-105">如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="dba94-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="dba94-106">您需要 tooinstall hello 最新版本的 hello Azure 資源管理員 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="dba94-106">You need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="dba94-107">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="dba94-107">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="dba94-108">Azure 帳戶登入 tooyour</span><span class="sxs-lookup"><span data-stu-id="dba94-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="dba94-109">開啟 PowerShell 主控台並連接 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="dba94-109">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="dba94-110">如需詳細資訊，請參閱[搭配使用 PowerShell 與 Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="dba94-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a><span data-ttu-id="dba94-111">選取 hello 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dba94-111">Select hello subscription</span></span>
 
<span data-ttu-id="dba94-112">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dba94-112">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="dba94-113">選擇 Azure 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="dba94-113">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="dba94-114">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="dba94-114">Create a resource group</span></span>

<span data-ttu-id="dba94-115">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="dba94-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="dba94-116">此位置用於 hello 預設位置為該資源群組。</span><span class="sxs-lookup"><span data-stu-id="dba94-116">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="dba94-117">不過，因為所有的 DNS 資源全域，不是地區，hello 所選擇的資源群組位置沒有任何影響 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="dba94-117">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="dba94-118">如果您使用現有的資源群組，則可略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="dba94-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="dba94-119">註冊資源提供者</span><span class="sxs-lookup"><span data-stu-id="dba94-119">Register resource provider</span></span>

<span data-ttu-id="dba94-120">hello Azure DNS 服務是由 hello Microsoft.Network 資源提供者管理。</span><span class="sxs-lookup"><span data-stu-id="dba94-120">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="dba94-121">您的 Azure 訂用帳戶必須是已註冊的 toouse 這個資源提供者才能使用 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="dba94-121">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="dba94-122">每個訂用帳戶只需執行一次此作業。</span><span class="sxs-lookup"><span data-stu-id="dba94-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```