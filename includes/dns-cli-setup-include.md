## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="7272e-101">設定適用於 Azure DNS 的 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7272e-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="7272e-102">開始之前</span><span class="sxs-lookup"><span data-stu-id="7272e-102">Before you begin</span></span>

<span data-ttu-id="7272e-103">確認您擁有 hello 開始您的組態之前，下列項目。</span><span class="sxs-lookup"><span data-stu-id="7272e-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="7272e-104">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7272e-104">An Azure subscription.</span></span> <span data-ttu-id="7272e-105">如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="7272e-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7272e-106">安裝 hello hello Azure CLI，適用於 Windows、 Linux 或 MAC 最新版本</span><span class="sxs-lookup"><span data-stu-id="7272e-106">Install hello latest version of hello Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="7272e-107">詳細的資訊將會位於[安裝 hello Azure CLI](../articles/cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="7272e-107">More information is available at [Install hello Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="7272e-108">Azure 帳戶登入 tooyour</span><span class="sxs-lookup"><span data-stu-id="7272e-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="7272e-109">開啟主控台視窗，並驗證您的認證。</span><span class="sxs-lookup"><span data-stu-id="7272e-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="7272e-110">如需詳細資訊，請參閱[登入從 hello Azure CLI tooAzure](../articles/xplat-cli-connect.md)</span><span class="sxs-lookup"><span data-stu-id="7272e-110">For more information, see [Log in tooAzure from hello Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="7272e-111">切換 CLI 模式</span><span class="sxs-lookup"><span data-stu-id="7272e-111">Switch CLI mode</span></span>

<span data-ttu-id="7272e-112">Azure DNS 使用 Azure Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="7272e-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="7272e-113">請確定切換 CLI 模式 toouse Azure 資源管理員命令。</span><span class="sxs-lookup"><span data-stu-id="7272e-113">Make sure you switch CLI mode toouse Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a><span data-ttu-id="7272e-114">選取 hello 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7272e-114">Select hello subscription</span></span>

<span data-ttu-id="7272e-115">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7272e-115">Check hello subscriptions for hello account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="7272e-116">選擇 Azure 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="7272e-116">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="7272e-117">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="7272e-117">Create a resource group</span></span>

<span data-ttu-id="7272e-118">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="7272e-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="7272e-119">這當做 hello 預設位置，該資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="7272e-119">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="7272e-120">不過，因為所有的 DNS 資源全域，不是地區，hello 所選擇的資源群組位置沒有任何影響 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="7272e-120">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="7272e-121">如果您使用現有的資源群組，則可略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="7272e-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="7272e-122">註冊資源提供者</span><span class="sxs-lookup"><span data-stu-id="7272e-122">Register resource provider</span></span>

<span data-ttu-id="7272e-123">hello Azure DNS 服務是由 hello Microsoft.Network 資源提供者管理。</span><span class="sxs-lookup"><span data-stu-id="7272e-123">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="7272e-124">您的 Azure 訂用帳戶必須是已註冊的 toouse 這個資源提供者才能使用 Azure DNS。</span><span class="sxs-lookup"><span data-stu-id="7272e-124">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="7272e-125">每個訂用帳戶只需執行一次此作業。</span><span class="sxs-lookup"><span data-stu-id="7272e-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

