# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="8e977-101">調整 Container Service 叢集中的代理程式節點</span><span class="sxs-lookup"><span data-stu-id="8e977-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="8e977-102">在[部署 Azure Container Service 叢集](../articles/container-service/dcos-swarm/container-service-deployment.md)之後，您可能需要變更代理程式節點的數目。</span><span class="sxs-lookup"><span data-stu-id="8e977-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need to change the number of agent nodes.</span></span> <span data-ttu-id="8e977-103">例如，您可能需要更多代理程式，以便可以執行更多的容器應用程式或執行個體。</span><span class="sxs-lookup"><span data-stu-id="8e977-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="8e977-104">您可以使用 Azure 入口網站或 Azure CLI 2.0 來變更 DC/OS、Docker Swarm 或 Kubernetes 叢集中的代理程式節點數目。</span><span class="sxs-lookup"><span data-stu-id="8e977-104">You can change the number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using the Azure portal or the Azure CLI 2.0.</span></span> 

## <a name="scale-with-the-azure-portal"></a><span data-ttu-id="8e977-105">使用 Azure 入口網站進行調整</span><span class="sxs-lookup"><span data-stu-id="8e977-105">Scale with the Azure portal</span></span>

1. <span data-ttu-id="8e977-106">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽**容器服務**，然後按一下您想要修改的容器服務。</span><span class="sxs-lookup"><span data-stu-id="8e977-106">In the [Azure portal](https://portal.azure.com), browse for **Container services**, and then click the container service that you want to modify.</span></span>
2. <span data-ttu-id="8e977-107">在 [容器服務] 刀鋒視窗中，按一下 [代理程式]。</span><span class="sxs-lookup"><span data-stu-id="8e977-107">In the **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="8e977-108">在 [VM 計數] 中，輸入所需的代理程式節點數目。</span><span class="sxs-lookup"><span data-stu-id="8e977-108">In **VM Count**, enter the desired number of agents nodes.</span></span>

    ![在入口網站中調整集區](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="8e977-110">若要儲存組態時，請按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="8e977-110">To save the configuration, click **Save**.</span></span>

## <a name="scale-with-the-azure-cli-20"></a><span data-ttu-id="8e977-111">使用 Azure CLI 2.0 進行調整</span><span class="sxs-lookup"><span data-stu-id="8e977-111">Scale with the Azure CLI 2.0</span></span>

<span data-ttu-id="8e977-112">請確定您[已安裝](/cli/azure/install-az-cli2)最新的 Azure CLI 2.0 並登入 Azure 帳戶 (`az login`)。</span><span class="sxs-lookup"><span data-stu-id="8e977-112">Make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an azure account (`az login`).</span></span>

### <a name="see-the-current-agent-count"></a><span data-ttu-id="8e977-113">查看目前的代理程式計數</span><span class="sxs-lookup"><span data-stu-id="8e977-113">See the current agent count</span></span>
<span data-ttu-id="8e977-114">若要查看叢集中目前擁有的代理程式數目，請執行 `az acs show` 命令。</span><span class="sxs-lookup"><span data-stu-id="8e977-114">To see the number of agents currently in the cluster, run the `az acs show` command.</span></span> <span data-ttu-id="8e977-115">這會顯示叢集組態。</span><span class="sxs-lookup"><span data-stu-id="8e977-115">This shows the cluster configuration.</span></span> <span data-ttu-id="8e977-116">例如，下列命令會顯示資源群組 `myResourceGroup` 中名為 `containerservice-myACSName` 之容器服務的組態：</span><span class="sxs-lookup"><span data-stu-id="8e977-116">For example, the following command shows the configuration of the container service named `containerservice-myACSName` in the resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="8e977-117">此命令會在 `AgentPoolProfiles` 底下的 `Count` 值中傳回代理程式數目。</span><span class="sxs-lookup"><span data-stu-id="8e977-117">The command returns the number of agents in the `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-the-az-acs-scale-command"></a><span data-ttu-id="8e977-118">使用 az acs scale 命令</span><span class="sxs-lookup"><span data-stu-id="8e977-118">Use the az acs scale command</span></span>
<span data-ttu-id="8e977-119">若要變更代理程式節點數目，請執行 `az acs scale` 命令，並提供**資源群組**、**容器服務名稱**及所需的**新代理程式計數**。</span><span class="sxs-lookup"><span data-stu-id="8e977-119">To change the number of agent nodes, run the `az acs scale` command and supply the **resource group**, **container service name**, and the desired **new agent count**.</span></span> <span data-ttu-id="8e977-120">藉由使用較少或更高的數字，即可分別相應減少或相應增加。</span><span class="sxs-lookup"><span data-stu-id="8e977-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="8e977-121">例如，若要將先前叢集中的代理程式數目變更為 10，請輸入下列命令︰</span><span class="sxs-lookup"><span data-stu-id="8e977-121">For example, to change the number of agents in the previous cluster to 10, type the following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="8e977-122">Azure CLI 2.0 會傳回 JSON 字串，這個字串代表容器服務的新組態，其中包括新的代理程式計數。</span><span class="sxs-lookup"><span data-stu-id="8e977-122">The Azure CLI 2.0 returns a JSON string representing the new configuration of the container service, including the new agent count.</span></span>

<span data-ttu-id="8e977-123">如需更多的命令選項，請執行 `az acs scale --help`。</span><span class="sxs-lookup"><span data-stu-id="8e977-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="8e977-124">調整考量</span><span class="sxs-lookup"><span data-stu-id="8e977-124">Scaling considerations</span></span>

* <span data-ttu-id="8e977-125">代理程式節點的數目必須介於 1 到 100 (含) 之間。</span><span class="sxs-lookup"><span data-stu-id="8e977-125">The number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="8e977-126">核心配額可以限制叢集中的代理程式節點數目。</span><span class="sxs-lookup"><span data-stu-id="8e977-126">Your cores quota can limit the number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="8e977-127">代理程式節點調整作業會套用至包含代理程式集區的 Azure 虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="8e977-127">Agent node scaling operations are applied to an Azure virtual machine scale set that contains the agent pool.</span></span> <span data-ttu-id="8e977-128">在 DC/OS 叢集中，只有私人集區中的代理程式節點會受到本文所示作業的調整。</span><span class="sxs-lookup"><span data-stu-id="8e977-128">In a DC/OS cluster, only agent nodes in the private pool are scaled by the operations shown in this article.</span></span>

* <span data-ttu-id="8e977-129">您可以根據您在叢集中部署的 Orchestrator，個別地調整在叢集上執行之容器的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="8e977-129">Depending on the orchestrator you deploy in your cluster, you can separately scale the number of instances of a container running on the cluster.</span></span> <span data-ttu-id="8e977-130">例如，在 DC/OS 叢集中，使用 [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) 來變更容器應用程式的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="8e977-130">For example, in a DC/OS cluster, use the [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) to change the number of instances of a container application.</span></span>

* <span data-ttu-id="8e977-131">目前並不支援在容器服務叢集中自動調整代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="8e977-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e977-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e977-132">Next steps</span></span>
* <span data-ttu-id="8e977-133">請參閱[更多範例](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md)，以了解如何搭配使用 Azure CLI 2.0 命令與 Azure Container Service。</span><span class="sxs-lookup"><span data-stu-id="8e977-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="8e977-134">深入了解 Azure Container Service 中的 [DC/OS 代理程式集區](../articles/container-service/dcos-swarm/container-service-dcos-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="8e977-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

