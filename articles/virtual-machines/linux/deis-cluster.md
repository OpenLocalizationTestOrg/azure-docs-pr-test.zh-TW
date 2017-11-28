---
title: "3 個節點 Deis 的 aaaDeploy 叢集 |Microsoft 文件"
description: "本文說明如何 toocreate 3 節點 Deis 在 Azure 中使用 Azure Resource Manager 範本上的叢集"
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="1ea13-103">在 Azure 中部署和設定 3 個節點的 Deis 叢集</span><span class="sxs-lookup"><span data-stu-id="1ea13-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="1ea13-104">本文將指導您逐步完成在 Azure 上佈建 [Deis](http://deis.io/) 叢集。</span><span class="sxs-lookup"><span data-stu-id="1ea13-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="1ea13-105">它涵蓋了所有 hello 步驟建立 hello 必要的憑證 toodeploying 和縮放範例**移**hello 新佈建叢集上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ea13-105">It covers all hello steps from creating hello necessary certificates toodeploying and scaling a sample **Go** application on hello newly provisioned cluster.</span></span>

<span data-ttu-id="1ea13-106">hello 下列圖表顯示 hello 部署的 hello 系統架構。</span><span class="sxs-lookup"><span data-stu-id="1ea13-106">hello following diagram shows hello architecture of hello deployed system.</span></span> <span data-ttu-id="1ea13-107">系統管理員管理 hello 叢集使用例如 Deis 工具**deis**和**deisctl**。</span><span class="sxs-lookup"><span data-stu-id="1ea13-107">A system administrator manages hello cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="1ea13-108">透過 Azure 負載平衡器會將轉送 hello 連線 tooone hello 成員的 hello 叢集上的節點建立連線。</span><span class="sxs-lookup"><span data-stu-id="1ea13-108">Connections are established through an Azure load balancer, which forwards hello connections tooone of hello member nodes on hello cluster.</span></span> <span data-ttu-id="1ea13-109">hello 用戶端存取部署的應用程式透過以及 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="1ea13-109">hello clients access deployed applications through hello load balancer as well.</span></span> <span data-ttu-id="1ea13-110">在此情況下，hello 負載平衡器轉送 hello 流量 tooa Deis 路由器網狀結構，進一步 routs hello 叢集上裝載的流量 toocorresponding Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="1ea13-110">In this case, hello load balancer forwards hello traffic tooa Deis router mesh, which further routs traffic toocorresponding Docker containers hosted on hello cluster.</span></span>

  ![已部署之 Desis 叢集的架構圖](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="1ea13-112">在透過 hello 步驟順序 toorun，您將需要：</span><span class="sxs-lookup"><span data-stu-id="1ea13-112">In order toorun through hello following steps, you'll need:</span></span>

* <span data-ttu-id="1ea13-113">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ea13-113">An active Azure subscription.</span></span> <span data-ttu-id="1ea13-114">如果沒有，您可以在 [azure.com](https://azure.microsoft.com/)免費取得一個。</span><span class="sxs-lookup"><span data-stu-id="1ea13-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="1ea13-115">工作或學校識別碼 toouse Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="1ea13-115">A work or school id toouse Azure resource groups.</span></span> <span data-ttu-id="1ea13-116">如果您有個人帳戶和登入 Microsoft id，您需要太[從個人所建立的工作識別碼](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1ea13-116">If you have a personal account and log in with a Microsoft id, you need too[create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="1ea13-117">-根據用戶端作業系統-hello [Azure PowerShell](/powershell/azureps-cmdlets-docs)或 hello [Mac、 Linux 和 Windows Azure CLI](../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="1ea13-117">Either -- depending on your client operating system -- hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="1ea13-118">[OpenSSL](https://www.openssl.org/)。</span><span class="sxs-lookup"><span data-stu-id="1ea13-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="1ea13-119">OpenSSL 是使用的 toogenerate hello 必要的憑證。</span><span class="sxs-lookup"><span data-stu-id="1ea13-119">OpenSSL is used toogenerate hello necessary certificates.</span></span>
* <span data-ttu-id="1ea13-120">Git 用戶端，例如 [Git Bash](https://git-scm.com/)。</span><span class="sxs-lookup"><span data-stu-id="1ea13-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="1ea13-121">tootest hello 範例應用程式，您還需要 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1ea13-121">tootest hello sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="1ea13-122">您也可以使用任何 DNS 伺服器或 支援萬用字元 A 記錄的服務。</span><span class="sxs-lookup"><span data-stu-id="1ea13-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="1ea13-123">電腦 toorun Deis 用戶端工具。</span><span class="sxs-lookup"><span data-stu-id="1ea13-123">A computer toorun Deis client tools.</span></span> <span data-ttu-id="1ea13-124">您可以使用本機電腦或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1ea13-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="1ea13-125">您可以執行這些工具在幾乎所有 Linux 散發套件，但是 hello 下列指示使用 Ubuntu。</span><span class="sxs-lookup"><span data-stu-id="1ea13-125">You can run these tools on almost any Linux distribution, but hello following instructions use Ubuntu.</span></span>

## <a name="provision-hello-cluster"></a><span data-ttu-id="1ea13-126">佈建 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="1ea13-126">Provision hello cluster</span></span>
<span data-ttu-id="1ea13-127">在本節中，您將使用[Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) hello 開放原始碼儲存機制中的範本[azure-快速入門範本](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="1ea13-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from hello open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="1ea13-128">首先，您將會複製下 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="1ea13-128">First, you'll copy down hello template.</span></span> <span data-ttu-id="1ea13-129">然後，您會建立用於驗證的新 SSH 金鑰組。</span><span class="sxs-lookup"><span data-stu-id="1ea13-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="1ea13-130">接下來，您會為叢集設定新的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1ea13-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="1ea13-131">最後，您會使用 hello 殼層指令碼或 hello PowerShell 指令碼 tooprovision hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="1ea13-131">And finally, you'll use either hello Shell script or hello PowerShell script tooprovision hello cluster.</span></span>

1. <span data-ttu-id="1ea13-132">複製 hello 儲存機制： [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="1ea13-132">Clone hello repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="1ea13-133">請移 toohello 範本資料夾：</span><span class="sxs-lookup"><span data-stu-id="1ea13-133">Go toohello template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="1ea13-134">使用 ssh-keygen 建立新的 SSH 金鑰組：</span><span class="sxs-lookup"><span data-stu-id="1ea13-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="1ea13-135">產生使用 hello 上方私密金鑰的憑證：</span><span class="sxs-lookup"><span data-stu-id="1ea13-135">Generate a certificate using hello above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. <span data-ttu-id="1ea13-136">跳過[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate 新叢集的權杖，看起來類似：</span><span class="sxs-lookup"><span data-stu-id="1ea13-136">Go too[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="1ea13-137">每個 CoreOS 叢集中需要 toohave 來自這項免費服務的唯一權杖。</span><span class="sxs-lookup"><span data-stu-id="1ea13-137">Each CoreOS cluster needs toohave a unique token from this free service.</span></span> <span data-ttu-id="1ea13-138">如需詳細資訊，請參閱 [CoreOS 文件](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) 。</span><span class="sxs-lookup"><span data-stu-id="1ea13-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="1ea13-139">修改 hello**雲端 config.yaml**檔案 tooreplace hello 現有**探索**權杖與 hello 新權杖：</span><span class="sxs-lookup"><span data-stu-id="1ea13-139">Modify hello **cloud-config.yaml** file tooreplace hello existing  **discovery** token with hello new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="1ea13-140">修改 hello **azuredeploy parameters.json**檔案： hello 開啟您在文字編輯器中的步驟 4 中建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="1ea13-140">Modify hello **azuredeploy-parameters.json** file: Open hello certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="1ea13-141">複製之間的所有文字`----BEGIN CERTIFICATE-----`和`-----END CERTIFICATE-----`到 hello **sshKeyData** （您將需要 tooremove 所有新行字元） 的參數。</span><span class="sxs-lookup"><span data-stu-id="1ea13-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into hello **sshKeyData** parameter (you'll need tooremove all newline characters).</span></span>
8. <span data-ttu-id="1ea13-142">修改 hello **newStorageAccountName**參數。</span><span class="sxs-lookup"><span data-stu-id="1ea13-142">Modify hello **newStorageAccountName** parameter.</span></span> <span data-ttu-id="1ea13-143">這是 hello VM OS 磁碟的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ea13-143">This is hello storage account for VM OS disks.</span></span> <span data-ttu-id="1ea13-144">此帳戶名稱中有全域唯一 toobe。</span><span class="sxs-lookup"><span data-stu-id="1ea13-144">This account name has toobe globally unique.</span></span>
9. <span data-ttu-id="1ea13-145">修改 hello **publicDomainName**參數。</span><span class="sxs-lookup"><span data-stu-id="1ea13-145">Modify hello **publicDomainName** parameter.</span></span> <span data-ttu-id="1ea13-146">這會成為 hello 與 hello 負載平衡器的公用 IP 相關聯的 DNS 名稱的一部分。</span><span class="sxs-lookup"><span data-stu-id="1ea13-146">This will become part of hello DNS name associated with hello load balancer public IP.</span></span> <span data-ttu-id="1ea13-147">hello 最終的 FQDN 必須 hello 格式*此參數值*。*[地區]*。 cloudapp.azure.com。例如，如果您 hello 名稱指定為 deishbai32，和 hello 資源群組是已部署的 toohello 美國西部地區，則最後的 hello FQDN tooyour 負載平衡器會 deishbai32.westus.cloudapp.azure.com。</span><span class="sxs-lookup"><span data-stu-id="1ea13-147">hello final FQDN will have hello format of *[value of this parameter]*.*[region]*.cloudapp.azure.com. For example, if you specify hello name as deishbai32, and hello resource group is deployed toohello West US region, then hello final FQDN tooyour load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="1ea13-148">儲存 hello 參數檔案。</span><span class="sxs-lookup"><span data-stu-id="1ea13-148">Save hello parameter file.</span></span> <span data-ttu-id="1ea13-149">然後佈建使用 Azure PowerShell hello 叢集：</span><span class="sxs-lookup"><span data-stu-id="1ea13-149">And then you can provision hello cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="1ea13-150">或 Azure CLI：</span><span class="sxs-lookup"><span data-stu-id="1ea13-150">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="1ea13-151">Hello 資源群組已佈建之後，您可以在 Azure 傳統入口網站中看到 hello 群組中的所有 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="1ea13-151">Once hello resource group is provisioned, you can see all hello resources in hello group on Azure classic portal.</span></span> <span data-ttu-id="1ea13-152">中所示 hello 下列螢幕擷取畫面，hello 資源群組包含具有三個 Vm 的虛擬網路，這是加入 toohello 相同可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="1ea13-152">As shown in hello following screenshot, hello resource group contains a virtual network with three VMs, which are joined toohello same availability set.</span></span> <span data-ttu-id="1ea13-153">hello 群組也包含負載平衡器，其具有相關聯的公用 IP。</span><span class="sxs-lookup"><span data-stu-id="1ea13-153">hello group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![hello 佈建在 Azure 傳統入口網站上的資源群組](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a><span data-ttu-id="1ea13-155">Hello 用戶端安裝</span><span class="sxs-lookup"><span data-stu-id="1ea13-155">Install hello client</span></span>
<span data-ttu-id="1ea13-156">您需要**deisctl** toocontrol 您 Deis 叢集。</span><span class="sxs-lookup"><span data-stu-id="1ea13-156">You need **deisctl** toocontrol your Deis cluster.</span></span> <span data-ttu-id="1ea13-157">雖然 deisctl 自動安裝在所有 hello 叢集節點中，是很好的作法 toouse deisctl 在不同的系統管理電腦上。</span><span class="sxs-lookup"><span data-stu-id="1ea13-157">Although deisctl is automatically installed in all hello cluster nodes, it's a good practice toouse deisctl on a separate administrative machine.</span></span> <span data-ttu-id="1ea13-158">此外，因為所有節點，都皆只有私用 IP 位址，您將需要 toouse 透過 hello 負載平衡器，其具有公用 IP，tooconnect toohello 節點機器的 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="1ea13-158">Furthermore, because all nodes are configured with only private IP addresses, you'll need toouse SSH tunneling through hello load balancer, which has a public IP, tooconnect toohello node machines.</span></span> <span data-ttu-id="1ea13-159">hello 下面是 hello deisctl 個別 Ubuntu 實體或虛擬機器上所設定的步驟。</span><span class="sxs-lookup"><span data-stu-id="1ea13-159">hello following are hello steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="1ea13-160">安裝 deisctl：mkdir deis</span><span class="sxs-lookup"><span data-stu-id="1ea13-160">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="1ea13-161">加入私用金鑰 toossh 代理程式：</span><span class="sxs-lookup"><span data-stu-id="1ea13-161">Add your private key toossh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. <span data-ttu-id="1ea13-162">設定 deisctl：</span><span class="sxs-lookup"><span data-stu-id="1ea13-162">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

<span data-ttu-id="1ea13-163">hello 範本會定義將 2223 tooinstance 1，對應的輸入的 NAT 規則 2224 tooinstance 2 和 2225 tooinstance 3。</span><span class="sxs-lookup"><span data-stu-id="1ea13-163">hello template defines inbound NAT rules that map 2223 tooinstance 1, 2224 tooinstance 2, and 2225 tooinstance 3.</span></span> <span data-ttu-id="1ea13-164">這是使用 hello deisctl 工具提供備援性。</span><span class="sxs-lookup"><span data-stu-id="1ea13-164">This provides redundancy for using hello deisctl tool.</span></span> <span data-ttu-id="1ea13-165">您可以在 Azure 傳統入口網站檢查這些規則：</span><span class="sxs-lookup"><span data-stu-id="1ea13-165">You can examine these rules on Azure classic portal:</span></span>

![Hello 負載平衡器上的 NAT 規則](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="1ea13-167">目前 hello 範本只支援 3 個節點的叢集。</span><span class="sxs-lookup"><span data-stu-id="1ea13-167">Currently hello template only supports 3-node clusters.</span></span> <span data-ttu-id="1ea13-168">這是因為 Azure 資源管理員範本 NAT 規則定義不支援迴圈與法的限制。</span><span class="sxs-lookup"><span data-stu-id="1ea13-168">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-hello-deis-platform"></a><span data-ttu-id="1ea13-169">安裝並啟動 hello Deis 平台</span><span class="sxs-lookup"><span data-stu-id="1ea13-169">Install and start hello Deis platform</span></span>
<span data-ttu-id="1ea13-170">現在您可以使用 deisctl tooinstall 並啟動 hello Deis 平台：</span><span class="sxs-lookup"><span data-stu-id="1ea13-170">Now you can use deisctl tooinstall and start hello Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="1ea13-171">起始 hello 平台需要一些時間 （最多可達 10 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="1ea13-171">Starting hello platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="1ea13-172">特別是，啟動 hello builder 服務可能需要很長的時間。</span><span class="sxs-lookup"><span data-stu-id="1ea13-172">Especially, starting hello builder service can take a long time.</span></span> <span data-ttu-id="1ea13-173">有時需要花幾次嘗試 toosucceed: hello 作業看起來 toohang，如果嘗試輸入`ctrl+c`toobreak 執行 hello 命令和重試。</span><span class="sxs-lookup"><span data-stu-id="1ea13-173">And sometimes it takes a few tries toosucceed: If hello operation seems toohang, try typing `ctrl+c` toobreak execution of hello command and retry.</span></span>
> 
> 

<span data-ttu-id="1ea13-174">您可以使用`deisctl list`tooverify 如果所有服務都執行：</span><span class="sxs-lookup"><span data-stu-id="1ea13-174">You can use `deisctl list` tooverify if all services are running:</span></span>

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

<span data-ttu-id="1ea13-175">恭喜！</span><span class="sxs-lookup"><span data-stu-id="1ea13-175">Congratulations!</span></span> <span data-ttu-id="1ea13-176">您現在有在 Azure 上執行的 Deis 了！</span><span class="sxs-lookup"><span data-stu-id="1ea13-176">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="1ea13-177">接下來，讓我們來部署到應用程式 toosee hello 叢集動作中的範例。</span><span class="sxs-lookup"><span data-stu-id="1ea13-177">Next, let's deploy a sample Go application toosee hello cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="1ea13-178">部署及調整 Hello World 應用程式</span><span class="sxs-lookup"><span data-stu-id="1ea13-178">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="1ea13-179">hello 下列步驟顯示如何 toodeploy"Hello World"到應用程式 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="1ea13-179">hello following steps show how toodeploy a "Hello World" Go application toohello cluster.</span></span> <span data-ttu-id="1ea13-180">hello 步驟為基礎[Deis 文件](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles)。</span><span class="sxs-lookup"><span data-stu-id="1ea13-180">hello steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="1ea13-181">Hello 路由網狀結構 toowork 正常運作，您將需要 toohave 萬用字元的記錄為指向 toohello 公用 IP hello 負載平衡器的網域。</span><span class="sxs-lookup"><span data-stu-id="1ea13-181">For hello routing mesh toowork properly, you’ll need toohave a wildcard A record for your domain pointing toohello public IP of hello load balancer.</span></span> <span data-ttu-id="1ea13-182">hello 下列螢幕擷取畫面顯示 hello A 記錄，如範例的網域註冊 GoDaddy 上：</span><span class="sxs-lookup"><span data-stu-id="1ea13-182">hello following screenshot shows hello A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Godaddy A 記錄](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="1ea13-184">安裝 deis：</span><span class="sxs-lookup"><span data-stu-id="1ea13-184">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="1ea13-185">建立新的 SSH 金鑰，然後加入 hello 公用金鑰 tooGitHub （當然，您也可以重複使用現有的金鑰）。</span><span class="sxs-lookup"><span data-stu-id="1ea13-185">Create a new SSH key, and then add hello public key tooGitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="1ea13-186">toocreate 新的 SSH 金鑰組，使用：</span><span class="sxs-lookup"><span data-stu-id="1ea13-186">toocreate a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. <span data-ttu-id="1ea13-187">加入 id_rsa.pub 或您的選擇 tooGitHub 的 hello 公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="1ea13-187">Add id_rsa.pub, or hello public key of your choice, tooGitHub.</span></span> <span data-ttu-id="1ea13-188">您可以使用 SSH 金鑰組態畫面中的 hello 加入 SSH 金鑰 按鈕：</span><span class="sxs-lookup"><span data-stu-id="1ea13-188">You can do this by using hello Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![GitHub 金鑰](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="1ea13-190">註冊新的使用者：</span><span class="sxs-lookup"><span data-stu-id="1ea13-190">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="1ea13-191">新增 hello SSH 金鑰：</span><span class="sxs-lookup"><span data-stu-id="1ea13-191">Add hello SSH key:</span></span>
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. <span data-ttu-id="1ea13-192">建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ea13-192">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="1ea13-193">
8.hello git 推送將會觸發將需要花幾分鐘的時間 Docker 映像 toobe 建置與部署。</span><span class="sxs-lookup"><span data-stu-id="1ea13-193">
8. hello git push will trigger Docker images toobe built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="1ea13-194">我的經驗，有時候，步驟 10 （Pushing 映像 tooprivate 儲存機制） 可能會停止回應。</span><span class="sxs-lookup"><span data-stu-id="1ea13-194">From my experience, occasionally, Step 10 (Pushing image tooprivate repository) may hang.</span></span> <span data-ttu-id="1ea13-195">當發生這種情況時，您可以停止 hello 程序，移除 hello 應用程式使用 ' deis 應用程式： 終結 – <application name> ` tooremove hello application and try again. You can use `deis apps:list' toofind 出 hello 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="1ea13-195">When this happens, you can stop hello process, remove hello application using `deis apps:destroy –a <application name>` tooremove hello application and try again. You can use `deis apps:list` toofind out hello name of your application.</span></span> <span data-ttu-id="1ea13-196">如果一切運作，您應該會看到在命令輸出的 hello 結尾 hello 下列類似：</span><span class="sxs-lookup"><span data-stu-id="1ea13-196">If everything works out, you should see something like hello following at hello end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="1ea13-197">請確認 hello 應用程式是否正在運作：</span><span class="sxs-lookup"><span data-stu-id="1ea13-197">Verify if hello application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="1ea13-198">您應該會看到：</span><span class="sxs-lookup"><span data-stu-id="1ea13-198">You should see:</span></span>
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. <span data-ttu-id="1ea13-199">標尺 hello 應用程式 too3 執行個體：</span><span class="sxs-lookup"><span data-stu-id="1ea13-199">Scale hello application too3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="1ea13-200">或者，您可以使用 deis 資訊 tooexamine 詳細資料，您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ea13-200">Optionally, you can use deis info tooexamine details of your application.</span></span> <span data-ttu-id="1ea13-201">hello 下列輸出會從我的應用程式部署：</span><span class="sxs-lookup"><span data-stu-id="1ea13-201">hello following outputs are from my application deployment:</span></span>
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a><span data-ttu-id="1ea13-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1ea13-202">Next Steps</span></span>
<span data-ttu-id="1ea13-203">本文逐步進行所有 hello 步驟 tooprovision 新 Deis 作業您在 Azure 中使用 Azure Resource Manager 範本上的叢集。</span><span class="sxs-lookup"><span data-stu-id="1ea13-203">This article walked you through all hello steps tooprovision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="1ea13-204">hello 範本支援備援連線，以及負載平衡提供部署應用程式的工具。</span><span class="sxs-lookup"><span data-stu-id="1ea13-204">hello template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="1ea13-205">hello 範本也可避免成員在節點上，這可以節省寶貴的公用 IP 資源，並提供更安全的環境 toohost 應用程式中使用公用 Ip。</span><span class="sxs-lookup"><span data-stu-id="1ea13-205">hello template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment toohost applications.</span></span> <span data-ttu-id="1ea13-206">toolearn 詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="1ea13-206">toolearn more, see hello following articles:</span></span>

<span data-ttu-id="1ea13-207">[Azure Resource Manager 概觀][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="1ea13-207">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="1ea13-208">[如何 toouse hello Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="1ea13-208">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="1ea13-209">[搭配使用 Azure PowerShell 與 Azure Resource Manager][powershell-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="1ea13-209">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
