---
title: "部署 3 個節點的 Deis 叢集 | Microsoft Docs"
description: "本文說明如何使用 Azure 資源管理員，在 Azure 上建立 3 個節點的 Deis 叢集。"
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
ms.openlocfilehash: 9a0c3dd7562dfb5ce54c2ebfd4665109f59cd8fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="ffaad-103">在 Azure 中部署和設定 3 個節點的 Deis 叢集</span><span class="sxs-lookup"><span data-stu-id="ffaad-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="ffaad-104">本文將指導您逐步完成在 Azure 上佈建 [Deis](http://deis.io/) 叢集。</span><span class="sxs-lookup"><span data-stu-id="ffaad-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="ffaad-105">它涵蓋建立必要的憑證，以及在新佈建的叢集上部署及調整 **Go** 應用程式範例的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="ffaad-105">It covers all the steps from creating the necessary certificates to deploying and scaling a sample **Go** application on the newly provisioned cluster.</span></span>

<span data-ttu-id="ffaad-106">下圖顯示已部署的系統之架構。</span><span class="sxs-lookup"><span data-stu-id="ffaad-106">The following diagram shows the architecture of the deployed system.</span></span> <span data-ttu-id="ffaad-107">系統管理員會使用 Deis 工具 (如 **deis** 和 **deisctl**) 來管理叢集。</span><span class="sxs-lookup"><span data-stu-id="ffaad-107">A system administrator manages the cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="ffaad-108">連線是透過會將連線轉送到叢集上其中一個節點的 Azure 負載平衡器而建立。</span><span class="sxs-lookup"><span data-stu-id="ffaad-108">Connections are established through an Azure load balancer, which forwards the connections to one of the member nodes on the cluster.</span></span> <span data-ttu-id="ffaad-109">用戶端也是透過負載平衡器存取部署的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ffaad-109">The clients access deployed applications through the load balancer as well.</span></span> <span data-ttu-id="ffaad-110">在此情況下，負載平衡器將流量轉送到 Deis 路由器網狀結構，進一步將流量路由至裝載於叢集上且相對應的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="ffaad-110">In this case, the load balancer forwards the traffic to a Deis router mesh, which further routs traffic to corresponding Docker containers hosted on the cluster.</span></span>

  ![已部署之 Desis 叢集的架構圖](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="ffaad-112">若要完成下列步驟，您需要：</span><span class="sxs-lookup"><span data-stu-id="ffaad-112">In order to run through the following steps, you'll need:</span></span>

* <span data-ttu-id="ffaad-113">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ffaad-113">An active Azure subscription.</span></span> <span data-ttu-id="ffaad-114">如果沒有，您可以在 [azure.com](https://azure.microsoft.com/)免費取得一個。</span><span class="sxs-lookup"><span data-stu-id="ffaad-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="ffaad-115">用於 Azure 資源群組的工作或學校識別碼。</span><span class="sxs-lookup"><span data-stu-id="ffaad-115">A work or school id to use Azure resource groups.</span></span> <span data-ttu-id="ffaad-116">如果您有個人帳戶且使用 Microsoft ID 登入，則您需要 [以您的個人識別碼建立一個工作識別碼](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ffaad-116">If you have a personal account and log in with a Microsoft id, you need to [create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="ffaad-117">依您的用戶端作業系統而定 -- [Azure PowerShell](/powershell/azureps-cmdlets-docs) 或[適用於 Mac、Linux 和 Windows 的 Azure CLI](../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="ffaad-117">Either -- depending on your client operating system -- the [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="ffaad-118">[OpenSSL](https://www.openssl.org/)。</span><span class="sxs-lookup"><span data-stu-id="ffaad-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="ffaad-119">OpenSSL 是用來產生必要的憑證。</span><span class="sxs-lookup"><span data-stu-id="ffaad-119">OpenSSL is used to generate the necessary certificates.</span></span>
* <span data-ttu-id="ffaad-120">Git 用戶端，例如 [Git Bash](https://git-scm.com/)。</span><span class="sxs-lookup"><span data-stu-id="ffaad-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="ffaad-121">若要測試範例應用程式，您也需要 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ffaad-121">To test the sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="ffaad-122">您也可以使用任何 DNS 伺服器或 支援萬用字元 A 記錄的服務。</span><span class="sxs-lookup"><span data-stu-id="ffaad-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="ffaad-123">執行 Deis 用戶端工具的電腦。</span><span class="sxs-lookup"><span data-stu-id="ffaad-123">A computer to run Deis client tools.</span></span> <span data-ttu-id="ffaad-124">您可以使用本機電腦或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ffaad-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="ffaad-125">您可以在幾乎所有 Linux 散發套件執行這些工具，但是以下指示使用的是 Ubuntu。</span><span class="sxs-lookup"><span data-stu-id="ffaad-125">You can run these tools on almost any Linux distribution, but the following instructions use Ubuntu.</span></span>

## <a name="provision-the-cluster"></a><span data-ttu-id="ffaad-126">佈建叢集</span><span class="sxs-lookup"><span data-stu-id="ffaad-126">Provision the cluster</span></span>
<span data-ttu-id="ffaad-127">在本節中，您將使用開放原始碼儲存機制 [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) 中的 [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) 範本。</span><span class="sxs-lookup"><span data-stu-id="ffaad-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from the open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="ffaad-128">首先，您會複製範本。</span><span class="sxs-lookup"><span data-stu-id="ffaad-128">First, you'll copy down the template.</span></span> <span data-ttu-id="ffaad-129">然後，您會建立用於驗證的新 SSH 金鑰組。</span><span class="sxs-lookup"><span data-stu-id="ffaad-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="ffaad-130">接下來，您會為叢集設定新的識別碼。</span><span class="sxs-lookup"><span data-stu-id="ffaad-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="ffaad-131">最後，您會使用 Shell 指令碼或 PowerShell 指令碼佈建叢集。</span><span class="sxs-lookup"><span data-stu-id="ffaad-131">And finally, you'll use either the Shell script or the PowerShell script to provision the cluster.</span></span>

1. <span data-ttu-id="ffaad-132">複製儲存機制： [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="ffaad-132">Clone the repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="ffaad-133">移至範本資料夾：</span><span class="sxs-lookup"><span data-stu-id="ffaad-133">Go to the template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="ffaad-134">使用 ssh-keygen 建立新的 SSH 金鑰組：</span><span class="sxs-lookup"><span data-stu-id="ffaad-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="ffaad-135">使用上一步的私密金鑰產生憑證：</span><span class="sxs-lookup"><span data-stu-id="ffaad-135">Generate a certificate using the above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file to be generated]
5. <span data-ttu-id="ffaad-136">移至 [https://discovery.etcd.io/new](https://discovery.etcd.io/new) 來產生新的叢集權杖，看起來會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="ffaad-136">Go to [https://discovery.etcd.io/new](https://discovery.etcd.io/new) to generate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="ffaad-137">每個 CoreOS 叢集都必須有這項免費服務提供的唯一權杖。</span><span class="sxs-lookup"><span data-stu-id="ffaad-137">Each CoreOS cluster needs to have a unique token from this free service.</span></span> <span data-ttu-id="ffaad-138">如需詳細資訊，請參閱 [CoreOS 文件](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) 。</span><span class="sxs-lookup"><span data-stu-id="ffaad-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="ffaad-139">修改 **cloud-config.yaml**檔案，以新權杖取代現有的 **discovery** 權杖：</span><span class="sxs-lookup"><span data-stu-id="ffaad-139">Modify the **cloud-config.yaml** file to replace the existing  **discovery** token with the new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment the following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="ffaad-140">修改 **azuredeploy parameters.json** 檔案：開啟您在步驟 4 中，於文字編輯器內建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="ffaad-140">Modify the **azuredeploy-parameters.json** file: Open the certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="ffaad-141">將 `----BEGIN CERTIFICATE-----` 和 `-----END CERTIFICATE-----` 之間的所有文字複製到 **sshKeyData** 參數中 (您必須移除所有新行字元)。</span><span class="sxs-lookup"><span data-stu-id="ffaad-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into the **sshKeyData** parameter (you'll need to remove all newline characters).</span></span>
8. <span data-ttu-id="ffaad-142">修改 **newStorageAccountName** 參數。</span><span class="sxs-lookup"><span data-stu-id="ffaad-142">Modify the **newStorageAccountName** parameter.</span></span> <span data-ttu-id="ffaad-143">這是 VM OS 磁碟的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ffaad-143">This is the storage account for VM OS disks.</span></span> <span data-ttu-id="ffaad-144">此帳戶名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="ffaad-144">This account name has to be globally unique.</span></span>
9. <span data-ttu-id="ffaad-145">修改 **publicDomainName** 參數。</span><span class="sxs-lookup"><span data-stu-id="ffaad-145">Modify the **publicDomainName** parameter.</span></span> <span data-ttu-id="ffaad-146">這會成為 DNS 名稱與負載平衡器公用 IP 相關聯的一部分。</span><span class="sxs-lookup"><span data-stu-id="ffaad-146">This will become part of the DNS name associated with the load balancer public IP.</span></span> <span data-ttu-id="ffaad-147">最終的 FQDN 格式會是 *[此參數的值]*.*[區域]*.cloudapp.azure.com。</span><span class="sxs-lookup"><span data-stu-id="ffaad-147">The final FQDN will have the format of *[value of this parameter]*.*[region]*.cloudapp.azure.com.</span></span> <span data-ttu-id="ffaad-148">例如，如果名稱指定為 deishbai32，且資源群組部署至美國西部地區，則您負載平衡器會最終的 FQDN 會是 deishbai32.westus.cloudapp.azure.com。</span><span class="sxs-lookup"><span data-stu-id="ffaad-148">For example, if you specify the name as deishbai32, and the resource group is deployed to the West US region, then the final FQDN to your load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="ffaad-149">儲存參數檔案。</span><span class="sxs-lookup"><span data-stu-id="ffaad-149">Save the parameter file.</span></span> <span data-ttu-id="ffaad-150">然後您可以使用 Azure PowerShell 佈建叢集：</span><span class="sxs-lookup"><span data-stu-id="ffaad-150">And then you can provision the cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="ffaad-151">或 Azure CLI：</span><span class="sxs-lookup"><span data-stu-id="ffaad-151">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="ffaad-152">資源群組佈建之後，您可以在 Azure 傳統入口網站上看到群組中的所有資源。</span><span class="sxs-lookup"><span data-stu-id="ffaad-152">Once the resource group is provisioned, you can see all the resources in the group on Azure classic portal.</span></span> <span data-ttu-id="ffaad-153">如以下螢幕擷取畫面所示，資源群組內有包含三個 VM 的虛擬網路，這些 VM 加入同一個可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="ffaad-153">As shown in the following screenshot, the resource group contains a virtual network with three VMs, which are joined to the same availability set.</span></span> <span data-ttu-id="ffaad-154">該群組也包含負載平衡器，其具有關聯的公用 IP。</span><span class="sxs-lookup"><span data-stu-id="ffaad-154">The group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![在 Azure 傳統入口網站佈建的資源群組](./media/deis-cluster/resource-group.png)

## <a name="install-the-client"></a><span data-ttu-id="ffaad-156">安裝用戶端</span><span class="sxs-lookup"><span data-stu-id="ffaad-156">Install the client</span></span>
<span data-ttu-id="ffaad-157">您需要 **deisctl** 來控制 Deis 叢集。</span><span class="sxs-lookup"><span data-stu-id="ffaad-157">You need **deisctl** to control your Deis cluster.</span></span> <span data-ttu-id="ffaad-158">雖然 deisctl 會自動安裝在所有叢集節點中，但較佳做法是在個別的系統管理電腦上使用 deisctl。</span><span class="sxs-lookup"><span data-stu-id="ffaad-158">Although deisctl is automatically installed in all the cluster nodes, it's a good practice to use deisctl on a separate administrative machine.</span></span> <span data-ttu-id="ffaad-159">此外，因為所有節點都只設定私用 IP 位址，所以您會需要使用 SSH 在負載平衡器 (有公用 IP) 建立通道，以連線到節點電腦。</span><span class="sxs-lookup"><span data-stu-id="ffaad-159">Furthermore, because all nodes are configured with only private IP addresses, you'll need to use SSH tunneling through the load balancer, which has a public IP, to connect to the node machines.</span></span> <span data-ttu-id="ffaad-160">以下是在各別的 Ubuntu 實體或虛擬機器上設定 deisctl 的步驟。</span><span class="sxs-lookup"><span data-stu-id="ffaad-160">The following are the steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="ffaad-161">安裝 deisctl：mkdir deis</span><span class="sxs-lookup"><span data-stu-id="ffaad-161">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="ffaad-162">將您的私用金鑰加入 SSH 代理程式：</span><span class="sxs-lookup"><span data-stu-id="ffaad-162">Add your private key to ssh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path to the private key file, see step 1 in the previous section]
3. <span data-ttu-id="ffaad-163">設定 deisctl：</span><span class="sxs-lookup"><span data-stu-id="ffaad-163">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of the load balancer]:2223

<span data-ttu-id="ffaad-164">範本會定義傳入的 NAT 規則，將 2223 對應到執行個體 1、2224 對應到執行個體 2、2225 對應到執行個體 3。</span><span class="sxs-lookup"><span data-stu-id="ffaad-164">The template defines inbound NAT rules that map 2223 to instance 1, 2224 to instance 2, and 2225 to instance 3.</span></span> <span data-ttu-id="ffaad-165">這會提供使用 deisctl 工具的備援。</span><span class="sxs-lookup"><span data-stu-id="ffaad-165">This provides redundancy for using the deisctl tool.</span></span> <span data-ttu-id="ffaad-166">您可以在 Azure 傳統入口網站檢查這些規則：</span><span class="sxs-lookup"><span data-stu-id="ffaad-166">You can examine these rules on Azure classic portal:</span></span>

![負載平衡器上的 NAT 規則](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="ffaad-168">範本目前僅支援 3 個節點的叢集。</span><span class="sxs-lookup"><span data-stu-id="ffaad-168">Currently the template only supports 3-node clusters.</span></span> <span data-ttu-id="ffaad-169">這是因為 Azure 資源管理員範本 NAT 規則定義不支援迴圈與法的限制。</span><span class="sxs-lookup"><span data-stu-id="ffaad-169">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-the-deis-platform"></a><span data-ttu-id="ffaad-170">安裝並啟動 Deis 平台</span><span class="sxs-lookup"><span data-stu-id="ffaad-170">Install and start the Deis platform</span></span>
<span data-ttu-id="ffaad-171">您現在可以使用 deisctl 來安裝和啟動 Deis 平台：</span><span class="sxs-lookup"><span data-stu-id="ffaad-171">Now you can use deisctl to install and start the Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path to the private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="ffaad-172">啟動平台需要一些時間 (最多 10 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="ffaad-172">Starting the platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="ffaad-173">尤其啟動建立器服務需要較長的時間。</span><span class="sxs-lookup"><span data-stu-id="ffaad-173">Especially, starting the builder service can take a long time.</span></span> <span data-ttu-id="ffaad-174">而且有時要嘗試幾次才會成功：如果作業似乎無回應，請嘗試輸入 `ctrl+c` 來中斷命令的執行，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="ffaad-174">And sometimes it takes a few tries to succeed: If the operation seems to hang, try typing `ctrl+c` to break execution of the command and retry.</span></span>
> 
> 

<span data-ttu-id="ffaad-175">您可以使用 `deisctl list` 確認是否所有服務都在執行：</span><span class="sxs-lookup"><span data-stu-id="ffaad-175">You can use `deisctl list` to verify if all services are running:</span></span>

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

<span data-ttu-id="ffaad-176">恭喜！</span><span class="sxs-lookup"><span data-stu-id="ffaad-176">Congratulations!</span></span> <span data-ttu-id="ffaad-177">您現在有在 Azure 上執行的 Deis 了！</span><span class="sxs-lookup"><span data-stu-id="ffaad-177">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="ffaad-178">接下來，讓我們部署一個簡單的 Go 應用程式，看看叢集實際運作。</span><span class="sxs-lookup"><span data-stu-id="ffaad-178">Next, let's deploy a sample Go application to see the cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="ffaad-179">部署及調整 Hello World 應用程式</span><span class="sxs-lookup"><span data-stu-id="ffaad-179">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="ffaad-180">以下步驟說明如何將 Go 應用程式「Hello World」部署到叢集。</span><span class="sxs-lookup"><span data-stu-id="ffaad-180">The following steps show how to deploy a "Hello World" Go application to the cluster.</span></span> <span data-ttu-id="ffaad-181">這些步驟皆是以 [Deis 文件](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles)(英文) 為基礎。</span><span class="sxs-lookup"><span data-stu-id="ffaad-181">The steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="ffaad-182">為了讓路由網狀結構正確運作，您指向負載平衡器公用 IP 的網域必須有萬用字元 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="ffaad-182">For the routing mesh to work properly, you’ll need to have a wildcard A record for your domain pointing to the public IP of the load balancer.</span></span> <span data-ttu-id="ffaad-183">以下螢幕擷取畫面顯示在 GoDaddy 上註冊之範例網域的 A 記錄：</span><span class="sxs-lookup"><span data-stu-id="ffaad-183">The following screenshot shows the A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Godaddy A 記錄](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="ffaad-185">安裝 deis：</span><span class="sxs-lookup"><span data-stu-id="ffaad-185">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="ffaad-186">建立新的 SSH 金鑰，然後將公用金鑰加入 GitHub (當然，您也可以使用您現有的金鑰)。</span><span class="sxs-lookup"><span data-stu-id="ffaad-186">Create a new SSH key, and then add the public key to GitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="ffaad-187">若要建立新的 SSH 金鑰組，請使用：</span><span class="sxs-lookup"><span data-stu-id="ffaad-187">To create a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s to use default file names and empty passcode)
4. <span data-ttu-id="ffaad-188">在 GitHub 加入 id_rsa.pub，或您自行選擇的公用金鑰。</span><span class="sxs-lookup"><span data-stu-id="ffaad-188">Add id_rsa.pub, or the public key of your choice, to GitHub.</span></span> <span data-ttu-id="ffaad-189">您可以使用 SSH 金鑰設定畫面上的 [Add SSH key] 按鈕來加入。</span><span class="sxs-lookup"><span data-stu-id="ffaad-189">You can do this by using the Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![GitHub 金鑰](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="ffaad-191">註冊新的使用者：</span><span class="sxs-lookup"><span data-stu-id="ffaad-191">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="ffaad-192">加入 SSH 金鑰：</span><span class="sxs-lookup"><span data-stu-id="ffaad-192">Add the SSH key:</span></span>
   
        deis keys:add [path to your SSH public key]
   <p />      
7. <span data-ttu-id="ffaad-193">建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="ffaad-193">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="ffaad-194">
8. git push 會觸發建置及部署 Docker 映像，這需要幾分鐘來完成。</span><span class="sxs-lookup"><span data-stu-id="ffaad-194">
8. The git push will trigger Docker images to be built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="ffaad-195">根據我的經驗，第 10 步驟 (將映像推送到私用儲存機制) 通常會無回應。</span><span class="sxs-lookup"><span data-stu-id="ffaad-195">From my experience, occasionally, Step 10 (Pushing image to private repository) may hang.</span></span> <span data-ttu-id="ffaad-196">當發生這種情況時，您可以停止程序，使用 `deis apps:destroy –a <application name>` to remove the application and try again. You can use `deis apps:list` 移除應用程式，找出應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="ffaad-196">When this happens, you can stop the process, remove the application using `deis apps:destroy –a <application name>` to remove the application and try again. You can use `deis apps:list` to find out the name of your application.</span></span> <span data-ttu-id="ffaad-197">如果一切都正常運作，您會在命令輸出的結尾看到訊息如下：</span><span class="sxs-lookup"><span data-stu-id="ffaad-197">If everything works out, you should see something like the following at the end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed to Deis
               http://lambda-underdog.artitrack.com
               To learn more, use `deis help` or visit http://deis.io
        To ssh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="ffaad-198">確認應用程式是否正在運作：</span><span class="sxs-lookup"><span data-stu-id="ffaad-198">Verify if the application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="ffaad-199">您應該會看到：</span><span class="sxs-lookup"><span data-stu-id="ffaad-199">You should see:</span></span>
   
        Welcome to Deis!
        See the documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list to get the name of your application).
   <p />
10. <span data-ttu-id="ffaad-200">將應用程式調整為 3 個執行個體：</span><span class="sxs-lookup"><span data-stu-id="ffaad-200">Scale the application to 3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="ffaad-201">或者，您可以使用 deis info 來檢查應用程式的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ffaad-201">Optionally, you can use deis info to examine details of your application.</span></span> <span data-ttu-id="ffaad-202">以下是我的應用程式部署的輸出結果：</span><span class="sxs-lookup"><span data-stu-id="ffaad-202">The following outputs are from my application deployment:</span></span>
    
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

## <a name="next-steps"></a><span data-ttu-id="ffaad-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ffaad-203">Next Steps</span></span>
<span data-ttu-id="ffaad-204">本文章會引導您使用 Azure 資源管理員範本，完成所有佈建新 Deis 叢集的步驟。</span><span class="sxs-lookup"><span data-stu-id="ffaad-204">This article walked you through all the steps to provision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="ffaad-205">範本支援工具連線的備援，以及已部署應用程式的負載平衡。</span><span class="sxs-lookup"><span data-stu-id="ffaad-205">The template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="ffaad-206">該範本也避免在成員節點使用公用 IP，這可以節省寶貴的公用 IP 資源，並提供主機應用程式更安全的環境。</span><span class="sxs-lookup"><span data-stu-id="ffaad-206">The template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment to host applications.</span></span> <span data-ttu-id="ffaad-207">若要深入了解，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="ffaad-207">To learn more, see the following articles:</span></span>

<span data-ttu-id="ffaad-208">[Azure Resource Manager 概觀][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="ffaad-208">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="ffaad-209">[如何使用 Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="ffaad-209">[How to use the Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="ffaad-210">[搭配使用 Azure PowerShell 與 Azure Resource Manager][powershell-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="ffaad-210">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
