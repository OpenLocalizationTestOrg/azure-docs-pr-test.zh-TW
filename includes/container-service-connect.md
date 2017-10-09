# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="24fba-101">進行遠端連線 tooa Kubernetes、 DC/作業系統，或 Docker Swarm 叢集</span><span class="sxs-lookup"><span data-stu-id="24fba-101">Make a remote connection tooa Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="24fba-102">建立 Azure 容器服務叢集之後, 您會需要 tooconnect toohello 叢集 toodeploy 和管理工作負載。</span><span class="sxs-lookup"><span data-stu-id="24fba-102">After creating an Azure Container Service cluster, you need tooconnect toohello cluster toodeploy and manage workloads.</span></span> <span data-ttu-id="24fba-103">本文說明 tooconnect toohello 主要 VM 的 hello 從遠端電腦的叢集化。</span><span class="sxs-lookup"><span data-stu-id="24fba-103">This article describes how tooconnect toohello master VM of hello cluster from a remote computer.</span></span> 

<span data-ttu-id="24fba-104">hello Kubernetes、 DC/OS，和 Docker Swarm 叢集提供本機 HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="24fba-104">hello Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="24fba-105">如 Kubernetes，此端點安全地公開所在 hello 網際網路，而且您可以藉由執行 hello 存取`kubectl`命令列工具，從任何連線網際網路的電腦。</span><span class="sxs-lookup"><span data-stu-id="24fba-105">For Kubernetes, this endpoint is securely exposed on hello internet, and you can access it by running hello `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="24fba-106">DC/OS 和 Docker Swarm，我們建議您從本機電腦 toohello 叢集管理系統建立安全殼層 (SSH) 通道。</span><span class="sxs-lookup"><span data-stu-id="24fba-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer toohello cluster management system.</span></span> <span data-ttu-id="24fba-107">建立 hello 通道之後，您可以執行使用 hello HTTP 端點和檢視 hello orchestrator 的 web 介面 （如果有的話） 從您的本機系統的命令。</span><span class="sxs-lookup"><span data-stu-id="24fba-107">After hello tunnel is established, you can run commands which use hello HTTP endpoints and view hello orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="24fba-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="24fba-108">Prerequisites</span></span>

* <span data-ttu-id="24fba-109">[在 Azure Container Service 中部署](../articles/container-service/dcos-swarm/container-service-deployment.md)的 Kubernetes、DC/OS 或 Docker Swarm 叢集。</span><span class="sxs-lookup"><span data-stu-id="24fba-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="24fba-110">SSH RSA 私密金鑰檔案，在部署期間對應 toohello 公用金鑰加入的 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="24fba-110">SSH RSA private key file, corresponding toohello public key added toohello cluster during deployment.</span></span> <span data-ttu-id="24fba-111">這些命令會假設該 hello SSH 私密金鑰是在`$HOME/.ssh/id_rsa`您電腦上。</span><span class="sxs-lookup"><span data-stu-id="24fba-111">These commands assume that hello private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="24fba-112">如需詳細資訊，請參閱 [macOS 及 Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) 或 [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) 的相關指示。</span><span class="sxs-lookup"><span data-stu-id="24fba-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="24fba-113">如果 hello SSH 連線沒有運作，您可能需要過[重設 SSH 金鑰](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="24fba-113">If hello SSH connection isn't working, you may need too [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-tooa-kubernetes-cluster"></a><span data-ttu-id="24fba-114">Tooa Kubernetes 叢集連線</span><span class="sxs-lookup"><span data-stu-id="24fba-114">Connect tooa Kubernetes cluster</span></span>

<span data-ttu-id="24fba-115">請遵循這些步驟 tooinstall 及設定`kubectl`您電腦上。</span><span class="sxs-lookup"><span data-stu-id="24fba-115">Follow these steps tooinstall and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="24fba-116">在 Linux 或 macOS，您可能需要 toorun hello 命令中使用此區段`sudo`。</span><span class="sxs-lookup"><span data-stu-id="24fba-116">On Linux or macOS, you might need toorun hello commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="24fba-117">安裝 kubectl</span><span class="sxs-lookup"><span data-stu-id="24fba-117">Install kubectl</span></span>
<span data-ttu-id="24fba-118">其中一種方式 tooinstall 此工具為 toouse hello `az acs kubernetes install-cli` Azure CLI 2.0 命令。</span><span class="sxs-lookup"><span data-stu-id="24fba-118">One way tooinstall this tool is toouse hello `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="24fba-119">此命令時，請確定 toorun 您[安裝](/cli/azure/install-az-cli2)hello 最新的 Azure CLI 2.0 和登入 Azure 帳戶 tooan (`az login`)。</span><span class="sxs-lookup"><span data-stu-id="24fba-119">toorun this command, make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="24fba-120">或者，您可以最新版本下載 hello`kubectl`用戶端直接從 hello [Kubernetes 釋放頁面](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md)。</span><span class="sxs-lookup"><span data-stu-id="24fba-120">Alternatively, you can download hello latest `kubectl` client directly from hello [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="24fba-121">如需詳細資訊，請參閱[安裝和設定 kubectl](https://kubernetes.io/docs/tasks/kubectl/install/)。</span><span class="sxs-lookup"><span data-stu-id="24fba-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="24fba-122">下載叢集認證</span><span class="sxs-lookup"><span data-stu-id="24fba-122">Download cluster credentials</span></span>
<span data-ttu-id="24fba-123">一旦`kubectl`安裝，您需要 toocopy hello 叢集認證 tooyour 機器。</span><span class="sxs-lookup"><span data-stu-id="24fba-123">Once you have `kubectl` installed, you need toocopy hello cluster credentials tooyour machine.</span></span> <span data-ttu-id="24fba-124">其中一種方式 toodo get hello 認證是以 hello`az acs kubernetes get-credentials`命令。</span><span class="sxs-lookup"><span data-stu-id="24fba-124">One way toodo get hello credentials is with hello `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="24fba-125">傳遞 hello hello 資源群組名稱和 hello hello 容器服務資源名稱：</span><span class="sxs-lookup"><span data-stu-id="24fba-125">Pass hello name of hello resource group and hello name of hello container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="24fba-126">這個命令會下載太 hello 叢集認證`$HOME/.kube/config`，其中`kubectl`toobe 位於也需要它。</span><span class="sxs-lookup"><span data-stu-id="24fba-126">This command downloads hello cluster credentials too`$HOME/.kube/config`, where `kubectl` expects it toobe located.</span></span>

<span data-ttu-id="24fba-127">或者，您可以使用`scp`toosecurely 複製 hello 檔案從`$HOME/.kube/config`hello 主要 VM tooyour 本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="24fba-127">Alternatively, you can use `scp` toosecurely copy hello file from `$HOME/.kube/config` on hello master VM tooyour local machine.</span></span> <span data-ttu-id="24fba-128">例如：</span><span class="sxs-lookup"><span data-stu-id="24fba-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="24fba-129">如果您是在 Windows 上，您可以在 Windows、 hello PuTTy 安全的檔案複製用戶端或類似的工具上的 Ubuntu 上使用 Bash。</span><span class="sxs-lookup"><span data-stu-id="24fba-129">If you are on Windows, you can use Bash on Ubuntu on Windows, hello PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="24fba-130">使用 kubectl</span><span class="sxs-lookup"><span data-stu-id="24fba-130">Use kubectl</span></span>

<span data-ttu-id="24fba-131">一旦`kubectl`設定，藉由列出 hello 叢集中的節點測試 hello 連線：</span><span class="sxs-lookup"><span data-stu-id="24fba-131">Once you have `kubectl` configured, test hello connection by listing hello nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="24fba-132">您可以嘗試其他 `kubectl` 命令。</span><span class="sxs-lookup"><span data-stu-id="24fba-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="24fba-133">例如，您可以檢視 hello Kubernetes 儀表板。</span><span class="sxs-lookup"><span data-stu-id="24fba-133">For example, you can view hello Kubernetes Dashboard.</span></span> <span data-ttu-id="24fba-134">首先，執行 proxy toohello Kubernetes API 伺服器：</span><span class="sxs-lookup"><span data-stu-id="24fba-134">First, run a proxy toohello Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="24fba-135">hello Kubernetes UI 現在已經提供： `http://localhost:8001/ui`。</span><span class="sxs-lookup"><span data-stu-id="24fba-135">hello Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="24fba-136">如需詳細資訊，請參閱 hello [Kubernetes 快速入門](http://kubernetes.io/docs/user-guide/quick-start/)。</span><span class="sxs-lookup"><span data-stu-id="24fba-136">For more information, see hello [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-tooa-dcos-or-swarm-cluster"></a><span data-ttu-id="24fba-137">Tooa DC/OS 或群集叢集連線</span><span class="sxs-lookup"><span data-stu-id="24fba-137">Connect tooa DC/OS or Swarm cluster</span></span>

<span data-ttu-id="24fba-138">toouse hello DC/OS 和 Docker Swarm 叢集部署 Azure 容器服務，請遵循這些指示 toocreate SSH 通道，從本機 Linux、 macOS、 或 Windows 系統。</span><span class="sxs-lookup"><span data-stu-id="24fba-138">toouse hello DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions toocreate a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="24fba-139">這些是透過 SSH 通道傳送 TCP 流量的指示。</span><span class="sxs-lookup"><span data-stu-id="24fba-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="24fba-140">您也可以使用其中一個 hello 內部叢集管理系統，開始的互動式的 SSH 工作階段，但我們不建議您這樣做。</span><span class="sxs-lookup"><span data-stu-id="24fba-140">You can also start an interactive SSH session with one of hello internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="24fba-141">直接使用內部系統可能會不小心變更設定。</span><span class="sxs-lookup"><span data-stu-id="24fba-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="24fba-142">在 Linux 或 macOS 上建立 SSH 通道</span><span class="sxs-lookup"><span data-stu-id="24fba-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="24fba-143">您在執行 Linux 或 macOS 上建立的 SSH 通道時的 hello 第一件事是 toolocate hello 公開 DNS 名稱的 hello 負載平衡的主機。</span><span class="sxs-lookup"><span data-stu-id="24fba-143">hello first thing that you do when you create an SSH tunnel on Linux or macOS is toolocate hello public DNS name of hello load-balanced masters.</span></span> <span data-ttu-id="24fba-144">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="24fba-144">Follow these steps:</span></span>


1. <span data-ttu-id="24fba-145">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽包含您的容器服務叢集 toohello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="24fba-145">In hello [Azure portal](https://portal.azure.com), browse toohello resource group containing your container service cluster.</span></span> <span data-ttu-id="24fba-146">展開 hello 資源群組，會顯示每個資源。</span><span class="sxs-lookup"><span data-stu-id="24fba-146">Expand hello resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="24fba-147">按一下 hello**容器服務**資源，然後按一下**概觀**。</span><span class="sxs-lookup"><span data-stu-id="24fba-147">Click hello **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="24fba-148">hello**主要 FQDN**叢集出現在下方的 hello **Essentials**。</span><span class="sxs-lookup"><span data-stu-id="24fba-148">hello **Master FQDN** of hello cluster appears under **Essentials**.</span></span> <span data-ttu-id="24fba-149">儲存這個名稱供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="24fba-149">Save this name for later use.</span></span> 

    ![公用 DNS 名稱](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="24fba-151">或者，執行 hello`az acs show`容器服務命令。</span><span class="sxs-lookup"><span data-stu-id="24fba-151">Alternatively, run hello `az acs show` command on your container service.</span></span> <span data-ttu-id="24fba-152">尋找 hello**主要設定檔： fqdn** hello 命令輸出中的屬性。</span><span class="sxs-lookup"><span data-stu-id="24fba-152">Look for hello **Master Profile:fqdn** property in hello command output.</span></span>

3. <span data-ttu-id="24fba-153">現在開啟 shell，並執行 hello`ssh`命令藉由指定下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="24fba-153">Now open a shell and run hello `ssh` command by specifying hello following values:</span></span> 

    <span data-ttu-id="24fba-154">**LOCAL_PORT**為 hello 以 hello 通道 tooconnect hello 服務端上的 TCP 通訊埠。</span><span class="sxs-lookup"><span data-stu-id="24fba-154">**LOCAL_PORT** is hello TCP port on hello service side of hello tunnel tooconnect to.</span></span> <span data-ttu-id="24fba-155">對於群集，來設定此 too2375。</span><span class="sxs-lookup"><span data-stu-id="24fba-155">For Swarm, set this too2375.</span></span> <span data-ttu-id="24fba-156">DC/OS，設定此 too80。</span><span class="sxs-lookup"><span data-stu-id="24fba-156">For DC/OS, set this too80.</span></span> 
    <span data-ttu-id="24fba-157">**REMOTE_PORT**是您想 tooexpose hello 端點的 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="24fba-157">**REMOTE_PORT** is hello port of hello endpoint that you want tooexpose.</span></span> <span data-ttu-id="24fba-158">針對 Swarm，使用連接埠 2375。</span><span class="sxs-lookup"><span data-stu-id="24fba-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="24fba-159">若為 DC/OS，則使用連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="24fba-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="24fba-160">**使用者名稱**是當您部署的 hello 叢集時所提供的 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="24fba-160">**USERNAME** is hello user name that was provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="24fba-161">**DNSPREFIX**是您部署 hello 叢集時，您所提供的 hello DNS 前置詞。</span><span class="sxs-lookup"><span data-stu-id="24fba-161">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="24fba-162">**區域**是資源群組所在的 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="24fba-162">**REGION** is hello region in which your resource group is located.</span></span>  
    <span data-ttu-id="24fba-163">**PATH_TO_PRIVATE_KEY** [選擇性] 是 hello 路徑 toohello 對應私密金鑰 toohello 建立 hello 叢集時所提供的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="24fba-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is hello path toohello private key that corresponds toohello public key you provided when you created hello cluster.</span></span> <span data-ttu-id="24fba-164">使用此選項以 hello`-i`旗標。</span><span class="sxs-lookup"><span data-stu-id="24fba-164">Use this option with hello `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="24fba-165">hello SSH 連接埠是 2200年，而且不 hello 標準通訊埠 22。</span><span class="sxs-lookup"><span data-stu-id="24fba-165">hello SSH connection port is 2200 and not hello standard port 22.</span></span> <span data-ttu-id="24fba-166">在具有一個以上的主要 VM 的叢集中，這會是 hello 連接埠 toohello 第一個主要 VM。</span><span class="sxs-lookup"><span data-stu-id="24fba-166">In a cluster with more than one master VM, this is hello connection port toohello first master VM.</span></span>
  > 

  <span data-ttu-id="24fba-167">hello 命令會傳回沒有輸出。</span><span class="sxs-lookup"><span data-stu-id="24fba-167">hello command returns without output.</span></span>

<span data-ttu-id="24fba-168">請參閱 DC/OS 和群集 hello 下列各節中的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="24fba-168">See hello examples for DC/OS and Swarm in hello following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="24fba-169">DC/OS 通道</span><span class="sxs-lookup"><span data-stu-id="24fba-169">DC/OS tunnel</span></span>
<span data-ttu-id="24fba-170">tooopen DC/OS 端點通道執行 hello 下列類似的命令：</span><span class="sxs-lookup"><span data-stu-id="24fba-170">tooopen a tunnel for DC/OS endpoints, run a command like hello following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="24fba-171">確定您沒有另一個繫結連接埠 80 的本機處理序。</span><span class="sxs-lookup"><span data-stu-id="24fba-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="24fba-172">如有需要，您可以指定連接埠 80 以外的本機連接埠 (例如連接埠 8080)。</span><span class="sxs-lookup"><span data-stu-id="24fba-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="24fba-173">不過，當您使用此連接埠時，某些網頁 UI 連結可能無法運作。</span><span class="sxs-lookup"><span data-stu-id="24fba-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="24fba-174">您現在可以從您的本機系統，透過 hello 下列 Url （假設本機連接埠 80） 存取 hello DC/OS 端點：</span><span class="sxs-lookup"><span data-stu-id="24fba-174">You can now access hello DC/OS endpoints from your local system through hello following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="24fba-175">DC/OS： `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="24fba-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="24fba-176">Marathon： `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="24fba-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="24fba-177">Mesos： `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="24fba-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="24fba-178">同樣地，您可能會達到每個應用程式，透過這個通道的 hello rest Api。</span><span class="sxs-lookup"><span data-stu-id="24fba-178">Similarly, you can reach hello rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="24fba-179">Swarm 通道</span><span class="sxs-lookup"><span data-stu-id="24fba-179">Swarm tunnel</span></span>
<span data-ttu-id="24fba-180">tooopen 通道 toohello 群集結束點執行類似 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="24fba-180">tooopen a tunnel toohello Swarm endpoint, run a command like hello following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="24fba-181">確定您沒有另一個繫結連接埠 2375 的本機處理序。</span><span class="sxs-lookup"><span data-stu-id="24fba-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="24fba-182">例如，如果您在本機執行 hello Docker 精靈，它會設定預設 toouse 連接埠 2375年。</span><span class="sxs-lookup"><span data-stu-id="24fba-182">For example, if you are running hello Docker daemon locally, it's set by default toouse port 2375.</span></span> <span data-ttu-id="24fba-183">如有需要，您可以指定連接埠 2375 以外的本機連接埠。</span><span class="sxs-lookup"><span data-stu-id="24fba-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="24fba-184">現在您可以存取您的本機系統上使用 hello Docker 命令列介面 (Docker CLI) 的 hello Docker Swarm 叢集。</span><span class="sxs-lookup"><span data-stu-id="24fba-184">Now you can access hello Docker Swarm cluster using hello Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="24fba-185">如需安裝指示，請參閱[安裝 Docker](https://docs.docker.com/engine/installation/)。</span><span class="sxs-lookup"><span data-stu-id="24fba-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="24fba-186">設定您 DOCKER_HOST 環境變數 toohello 您設定 hello 通道的本機連接埠。</span><span class="sxs-lookup"><span data-stu-id="24fba-186">Set your DOCKER_HOST environment variable toohello local port you configured for hello tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="24fba-187">該通道 toohello Docker Swarm 叢集中執行 Docker 命令。</span><span class="sxs-lookup"><span data-stu-id="24fba-187">Run Docker commands that tunnel toohello Docker Swarm cluster.</span></span> <span data-ttu-id="24fba-188">例如：</span><span class="sxs-lookup"><span data-stu-id="24fba-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="24fba-189">在 Windows 上建立 SSH 通道</span><span class="sxs-lookup"><span data-stu-id="24fba-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="24fba-190">在 Windows 上建立 SSH 通道有很多選項。</span><span class="sxs-lookup"><span data-stu-id="24fba-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="24fba-191">如果您在 Ubuntu 上執行 Bash Windows 或類似的工具上，您可以遵循 hello SSH 通道指示 macOS 和 Linux 適用的本文稍早所示。</span><span class="sxs-lookup"><span data-stu-id="24fba-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow hello SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="24fba-192">或者在 Windows 上，本章節描述如何 toouse PuTTY toocreate hello 通道。</span><span class="sxs-lookup"><span data-stu-id="24fba-192">As an alternative on Windows, this section describes how toouse PuTTY toocreate hello tunnel.</span></span>

1. <span data-ttu-id="24fba-193">[下載 PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows 系統。</span><span class="sxs-lookup"><span data-stu-id="24fba-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows system.</span></span>

2. <span data-ttu-id="24fba-194">執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24fba-194">Run hello application.</span></span>

3. <span data-ttu-id="24fba-195">輸入主機名稱所組成的 hello 叢集系統管理員使用者名稱和 hello hello 叢集中的第一個主要的 hello 公開 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="24fba-195">Enter a host name that is comprised of hello cluster admin user name and hello public DNS name of hello first master in hello cluster.</span></span> <span data-ttu-id="24fba-196">hello**主機名稱**看起來太`azureuser@PublicDNSName`。</span><span class="sxs-lookup"><span data-stu-id="24fba-196">hello **Host Name** looks similar too`azureuser@PublicDNSName`.</span></span> <span data-ttu-id="24fba-197">輸入 hello 2200**連接埠**。</span><span class="sxs-lookup"><span data-stu-id="24fba-197">Enter 2200 for hello **Port**.</span></span>

    ![PuTTY 組態 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="24fba-199">選取 [SSH] > [Auth]。新增路徑 tooyour 私密金鑰檔 （.ppk 格式） 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="24fba-199">Select **SSH > Auth**. Add a path tooyour private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="24fba-200">您可以使用一種工具，例如[Ssh-keygen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate 這個檔案從 hello SSH 金鑰的使用的 toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="24fba-200">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate this file from hello SSH key used toocreate hello cluster.</span></span>

    ![PuTTY 組態 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="24fba-202">選取**SSH > 通道**和設定轉送連接埠的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="24fba-202">Select **SSH > Tunnels** and configure hello following forwarded ports:</span></span>

    * <span data-ttu-id="24fba-203">**來源連接埠：**DC/OS 使用 80 或 Swarm 使用 2375。</span><span class="sxs-lookup"><span data-stu-id="24fba-203">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="24fba-204">**目的地：** DC/OS 使用 localhost:80 或 Swarm 使用 localhost:2375。</span><span class="sxs-lookup"><span data-stu-id="24fba-204">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="24fba-205">下列範例中的 hello 已針對 DC/OS，，但看起來類似的 Docker Swarm。</span><span class="sxs-lookup"><span data-stu-id="24fba-205">hello following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="24fba-206">建立此通道時，連接埠 80 不得使用中。</span><span class="sxs-lookup"><span data-stu-id="24fba-206">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![PuTTY 組態 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="24fba-208">當您完成時，按一下 **工作階段 > 儲存**toosave hello 連接組態。</span><span class="sxs-lookup"><span data-stu-id="24fba-208">When you're finished, click **Session > Save** toosave hello connection configuration.</span></span>

7. <span data-ttu-id="24fba-209">tooconnect toohello PuTTY 工作階段中，按一下**開啟**。</span><span class="sxs-lookup"><span data-stu-id="24fba-209">tooconnect toohello PuTTY session, click **Open**.</span></span> <span data-ttu-id="24fba-210">當您連線時，您可以看到 hello hello PuTTY 事件記錄檔中的連接埠設定。</span><span class="sxs-lookup"><span data-stu-id="24fba-210">When you connect, you can see hello port configuration in hello PuTTY event log.</span></span>

    ![PuTTY 事件記錄檔](./media/container-service-connect/putty4.png)

<span data-ttu-id="24fba-212">您設定 DC/OS hello 通道之後，您可以存取 hello 相關上的端點：</span><span class="sxs-lookup"><span data-stu-id="24fba-212">After you've configured hello tunnel for DC/OS, you can access hello related endpoints at:</span></span>

* <span data-ttu-id="24fba-213">DC/OS： `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="24fba-213">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="24fba-214">Marathon： `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="24fba-214">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="24fba-215">Mesos： `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="24fba-215">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="24fba-216">您的 Docker Swarm 設定 hello 通道之後，開啟您的 Windows 設定 tooconfigure 系統環境變數，名為`DOCKER_HOST`值是`:2375`。</span><span class="sxs-lookup"><span data-stu-id="24fba-216">After you've configured hello tunnel for Docker Swarm, open your Windows settings tooconfigure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="24fba-217">然後，您可以透過 Docker CLI hello 存取 hello 群集叢集。</span><span class="sxs-lookup"><span data-stu-id="24fba-217">Then, you can access hello Swarm cluster through hello Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24fba-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="24fba-218">Next steps</span></span>
<span data-ttu-id="24fba-219">部署及管理叢集中的容器：</span><span class="sxs-lookup"><span data-stu-id="24fba-219">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="24fba-220">使用 Azure Container Service 和 Kubernetes</span><span class="sxs-lookup"><span data-stu-id="24fba-220">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="24fba-221">使用 Azure Container Service 和 DC/OS</span><span class="sxs-lookup"><span data-stu-id="24fba-221">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="24fba-222">使用 hello Azure 容器服務和 Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="24fba-222">Work with hello Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

