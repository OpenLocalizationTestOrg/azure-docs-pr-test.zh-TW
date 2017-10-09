# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="b3762-101">調整 Container Service 叢集中的代理程式節點</span><span class="sxs-lookup"><span data-stu-id="b3762-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="b3762-102">之後[部署 Azure 容器服務叢集](../articles/container-service/dcos-swarm/container-service-deployment.md)，您可能需要的代理程式節點的 toochange hello 數目。</span><span class="sxs-lookup"><span data-stu-id="b3762-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need toochange hello number of agent nodes.</span></span> <span data-ttu-id="b3762-103">例如，您可能需要更多代理程式，以便可以執行更多的容器應用程式或執行個體。</span><span class="sxs-lookup"><span data-stu-id="b3762-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="b3762-104">您可以使用 hello Azure 入口網站來變更 hello DC/OS、 Docker Swarm，或 Kubernetes 叢集中的代理程式節點的數目或 hello Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="b3762-104">You can change hello number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using hello Azure portal or hello Azure CLI 2.0.</span></span> 

## <a name="scale-with-hello-azure-portal"></a><span data-ttu-id="b3762-105">調整以 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b3762-105">Scale with hello Azure portal</span></span>

1. <span data-ttu-id="b3762-106">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽**容器服務**，然後按一下您想 toomodify hello 容器服務。</span><span class="sxs-lookup"><span data-stu-id="b3762-106">In hello [Azure portal](https://portal.azure.com), browse for **Container services**, and then click hello container service that you want toomodify.</span></span>
2. <span data-ttu-id="b3762-107">在 hello**容器服務**刀鋒視窗中，按一下 **代理程式**。</span><span class="sxs-lookup"><span data-stu-id="b3762-107">In hello **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="b3762-108">在**VM 計數**，輸入想要的 hello 代理程式節點的數目。</span><span class="sxs-lookup"><span data-stu-id="b3762-108">In **VM Count**, enter hello desired number of agents nodes.</span></span>

    ![調整 hello 入口網站中的集區](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="b3762-110">toosave hello 組態中，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="b3762-110">toosave hello configuration, click **Save**.</span></span>

## <a name="scale-with-hello-azure-cli-20"></a><span data-ttu-id="b3762-111">調整以 hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b3762-111">Scale with hello Azure CLI 2.0</span></span>

<span data-ttu-id="b3762-112">請確定您[安裝](/cli/azure/install-az-cli2)hello 最新的 Azure CLI 2.0 和登入 tooan azure 帳戶 (`az login`)。</span><span class="sxs-lookup"><span data-stu-id="b3762-112">Make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan azure account (`az login`).</span></span>

### <a name="see-hello-current-agent-count"></a><span data-ttu-id="b3762-113">請參閱 hello 目前的代理程式計數</span><span class="sxs-lookup"><span data-stu-id="b3762-113">See hello current agent count</span></span>
<span data-ttu-id="b3762-114">代理程式目前的 toosee hello 數目 hello 叢集中執行 hello`az acs show`命令。</span><span class="sxs-lookup"><span data-stu-id="b3762-114">toosee hello number of agents currently in hello cluster, run hello `az acs show` command.</span></span> <span data-ttu-id="b3762-115">這會顯示 hello 叢集設定。</span><span class="sxs-lookup"><span data-stu-id="b3762-115">This shows hello cluster configuration.</span></span> <span data-ttu-id="b3762-116">例如，下列命令會顯示 hello 名為 hello 容器服務的組態來 hello `containerservice-myACSName` hello 資源群組中`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b3762-116">For example, hello following command shows hello configuration of hello container service named `containerservice-myACSName` in hello resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="b3762-117">hello 命令會傳回 hello 代理程式數目的 hello`Count`值下`AgentPoolProfiles`。</span><span class="sxs-lookup"><span data-stu-id="b3762-117">hello command returns hello number of agents in hello `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-hello-az-acs-scale-command"></a><span data-ttu-id="b3762-118">使用 hello az acs 小數位數的命令</span><span class="sxs-lookup"><span data-stu-id="b3762-118">Use hello az acs scale command</span></span>
<span data-ttu-id="b3762-119">toochange hello 代理程式節點數目，執行 hello`az acs scale`命令和提供 hello**資源群組**，**容器服務名稱**，並想要的 hello**新代理程式計數**.</span><span class="sxs-lookup"><span data-stu-id="b3762-119">toochange hello number of agent nodes, run hello `az acs scale` command and supply hello **resource group**, **container service name**, and hello desired **new agent count**.</span></span> <span data-ttu-id="b3762-120">藉由使用較少或更高的數字，即可分別相應減少或相應增加。</span><span class="sxs-lookup"><span data-stu-id="b3762-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="b3762-121">例如，在上一個叢集 too10 hello，代理程式的 toochange hello 數目輸入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="b3762-121">For example, toochange hello number of agents in hello previous cluster too10, type hello following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="b3762-122">hello Azure CLI 2.0 傳回 JSON 字串，代表 hello 新服務的組態 hello 容器，包括 hello 新代理程式計數。</span><span class="sxs-lookup"><span data-stu-id="b3762-122">hello Azure CLI 2.0 returns a JSON string representing hello new configuration of hello container service, including hello new agent count.</span></span>

<span data-ttu-id="b3762-123">如需更多的命令選項，請執行 `az acs scale --help`。</span><span class="sxs-lookup"><span data-stu-id="b3762-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="b3762-124">調整考量</span><span class="sxs-lookup"><span data-stu-id="b3762-124">Scaling considerations</span></span>

* <span data-ttu-id="b3762-125">hello 代理程式節點的數目必須是介於 1 到 100 (含) 之間。</span><span class="sxs-lookup"><span data-stu-id="b3762-125">hello number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="b3762-126">核心配額可以限制 hello 叢集中的代理程式節點的數目。</span><span class="sxs-lookup"><span data-stu-id="b3762-126">Your cores quota can limit hello number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="b3762-127">代理程式節點的縮放作業是套用的 tooan Azure 虛擬機器規模集包含 hello 代理程式集區。</span><span class="sxs-lookup"><span data-stu-id="b3762-127">Agent node scaling operations are applied tooan Azure virtual machine scale set that contains hello agent pool.</span></span> <span data-ttu-id="b3762-128">在 DC/OS 叢集中，只有代理程式節點 hello 私用的集區中縮放 hello 本文中所顯示的作業。</span><span class="sxs-lookup"><span data-stu-id="b3762-128">In a DC/OS cluster, only agent nodes in hello private pool are scaled by hello operations shown in this article.</span></span>

* <span data-ttu-id="b3762-129">根據您在叢集中部署的 hello orchestrator，您可以分開調整 hello hello 叢集上執行的容器的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="b3762-129">Depending on hello orchestrator you deploy in your cluster, you can separately scale hello number of instances of a container running on hello cluster.</span></span> <span data-ttu-id="b3762-130">例如，在 DC/OS 叢集中，使用 hello[馬拉松 UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello 數目的容器應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="b3762-130">For example, in a DC/OS cluster, use hello [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello number of instances of a container application.</span></span>

* <span data-ttu-id="b3762-131">目前並不支援在容器服務叢集中自動調整代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="b3762-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3762-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3762-132">Next steps</span></span>
* <span data-ttu-id="b3762-133">請參閱[更多範例](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md)，以了解如何搭配使用 Azure CLI 2.0 命令與 Azure Container Service。</span><span class="sxs-lookup"><span data-stu-id="b3762-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="b3762-134">深入了解 Azure Container Service 中的 [DC/OS 代理程式集區](../articles/container-service/dcos-swarm/container-service-dcos-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="b3762-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

