---
title: "使用 FreeBSD 的封包篩選器在 Azure 中建立防火牆 | Microsoft Docs"
description: "了解如何使用 FreeBSD 的 PF 在 Azure 中部署 NAT 防火牆。"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/20/2017
ms.author: kyliel
ms.openlocfilehash: cd777291a1321eabf4efe0d7b9b101f932d9398b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-freebsds-packet-filter-to-create-a-secure-firewall-in-azure"></a><span data-ttu-id="8d4cd-103">如何使用 FreeBSD 的「封包篩選器」在 Azure 中建立安全防火牆</span><span class="sxs-lookup"><span data-stu-id="8d4cd-103">How to use FreeBSD's Packet Filter to create a secure firewall in Azure</span></span>
<span data-ttu-id="8d4cd-104">本文介紹如何透過 Azure Resource Manager 範本，針對常見的 Web 伺服器案例，使用 FreeBSD 的「封包篩選器」來部署 NAT 防火牆。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-104">This article introduces how to deploy a NAT firewall using FreeBSD’s Packer Filter through Azure Resource Manager template for common web server scenario.</span></span>

## <a name="what-is-pf"></a><span data-ttu-id="8d4cd-105">什麼是 PF？</span><span class="sxs-lookup"><span data-stu-id="8d4cd-105">What is PF?</span></span>
<span data-ttu-id="8d4cd-106">PF (封包篩選器，也寫成 pf) 是一個 BSD 授權的具狀態封包篩選器，是防火牆軟體的一個核心部分。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-106">PF (Packet Filter, also written pf) is a BSD licensed stateful packet filter, a central piece of software for firewalling.</span></span> <span data-ttu-id="8d4cd-107">PF 一直以來快速發展，現在已有數個超越其他可用防火牆的優點。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-107">PF has since evolved quickly and now has several advantages over other available firewalls.</span></span> <span data-ttu-id="8d4cd-108">PF 從一開始便包含「網路位址轉譯」(NAT)，接著，藉由整合 ALTQ 並將它變成可透過 PF 組態來進行設定，整合了封包排程器和作用中佇列管理。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-108">Network Address Translation (NAT) is in PF since day one, then packet scheduler and active queue management have been integrated into PF, by integrating the ALTQ and making it configurable through PF's configuration.</span></span> <span data-ttu-id="8d4cd-109">此外，一些功能也將 PF 加以延伸，例如用來進行容錯移轉和備援的 pfsync 和 CARP、用來進行工作階段驗證的 authpf，以及可輕鬆為難以設定的 FTP 通訊協定建立防火牆的 ftp-proxy 等功能。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-109">Features such as pfsync and CARP for failover and redundancy, authpf for session authentication, and ftp-proxy to ease firewalling the difficult FTP protocol, have also extended PF.</span></span> <span data-ttu-id="8d4cd-110">簡單說來，PF 就是一個強大且功能豐富的防火牆。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-110">In short, PF is a powerful and feature-rich firewall.</span></span> 

## <a name="get-started"></a><span data-ttu-id="8d4cd-111">開始使用</span><span class="sxs-lookup"><span data-stu-id="8d4cd-111">Get started</span></span>
<span data-ttu-id="8d4cd-112">如果您對於在雲端為您的 Web 伺服器設定安全的防火牆感興趣，就讓我們開始吧！</span><span class="sxs-lookup"><span data-stu-id="8d4cd-112">If you are interested in setting up a secure firewall in the cloud for your web servers, then let’s get started.</span></span> <span data-ttu-id="8d4cd-113">您也可以套用這個 Azure Resource Manager 範本中使用的指令碼來設定您的網路拓撲。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-113">You can also apply the scripts used in this Azure Resource Manager template to set up your networking topology.</span></span>
<span data-ttu-id="8d4cd-114">Azure Resource Manager 範本會設定一部 FreeBSD 虛擬機器，此虛擬機器會使用 PF 和兩部已安裝並設定 Nginx Web 伺服器的 FreeBSD 虛擬機器，來執行 NAT/重新導向。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-114">The Azure Resource Manager template set up a FreeBSD virtual machine that performs NAT /redirection using PF and two FreeBSD virtual machines with the Nginx web server installed and configured.</span></span> <span data-ttu-id="8d4cd-115">除了為兩部 Web 伺服器的輸出流量執行 NAT 之外，NAT/重新導向虛擬機器還會攔截 HTTP 要求，然後以循環方式將這些要求重新導向到兩部 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-115">In addition to performing NAT for the two web servers egress traffic, the NAT/redirection virtual machine intercepts HTTP requests and redirect them to the two web servers in round-robin fashion.</span></span> <span data-ttu-id="8d4cd-116">VNet 會使用無法經路由傳送的私人 IP 位址空間 10.0.0.2/24，而您可以修改此範本的參數。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-116">The VNet uses the private non-routable IP address space 10.0.0.2/24 and you can modify the parameters of the template.</span></span> <span data-ttu-id="8d4cd-117">Azure Resource Manager 範本也為整個 VNet 定義了路由表，此表格是個別路由的集合，可用來根據目的地 IP 位址覆寫 Azure 預設路由。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-117">The Azure Resource Manager template also defines a route table for the whole VNet, which is a collection of individual routes used to override Azure default routes based on the destination IP address.</span></span> 

![pf_topology](./media/freebsd-pf-nat/pf_topology.jpg)
    
### <a name="deploy-through-azure-cli"></a><span data-ttu-id="8d4cd-119">透過 Azure CLI 進行部署</span><span class="sxs-lookup"><span data-stu-id="8d4cd-119">Deploy through Azure CLI</span></span>
<span data-ttu-id="8d4cd-120">您需要安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2)，並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-120">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="8d4cd-121">使用 [az group create](/cli/azure/group#create) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-121">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8d4cd-122">下列範例會在 `West US` 位置建立名為 `myResourceGroup` 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-122">The following example creates a resource group name `myResourceGroup` in the `West US` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="8d4cd-123">接著，使用 [az group deployment create](/cli/azure/group/deployment#create) 來部署 [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) 範本。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-123">Next, deploy the template [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="8d4cd-124">下載相同路徑下的 [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json)，並定義您自己的資源值，例如 `adminPassword`、`networkPrefix` 及 `domainNamePrefix`。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-124">Download [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json) under the same path and define your own resource values, such as `adminPassword`, `networkPrefix`, and `domainNamePrefix`.</span></span> 

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeploymentName \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/pf-freebsd-setup/azuredeploy.json \
    --parameters '@azuredeploy.parameters.json' --verbose
```

<span data-ttu-id="8d4cd-125">在大約 5 分鐘後，您將會收到 `"provisioningState": "Succeeded"` 的資訊。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-125">After about five minutes, you will get the information of `"provisioningState": "Succeeded"`.</span></span> <span data-ttu-id="8d4cd-126">接著，您可以透過 SSH 連線到前端 VM (NAT)，或在瀏覽器中使用公用 IP 位址或前端 VM (NAT) 的 FQDN 來存取 Nginx Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-126">Then you can ssh to the frontend VM (NAT) or access Nginx web server in a browser using the public IP address or FQDN of the frontend VM (NAT).</span></span> <span data-ttu-id="8d4cd-127">下列範例會列出指派給 `myResourceGroup` 資源群組中前端 VM (NAT) 的 FQDN 和公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-127">The following example lists FQDN and public IP address that assigned to the frontend VM (NAT) in the `myResourceGroup` resource group.</span></span> 

```azurecli
az network public-ip list --resource-group myResourceGroup
```
    
## <a name="next-steps"></a><span data-ttu-id="8d4cd-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8d4cd-128">Next steps</span></span>
<span data-ttu-id="8d4cd-129">您想要在 Azure 中設定自己的 NAT 嗎？</span><span class="sxs-lookup"><span data-stu-id="8d4cd-129">Do you want to set up your own NAT in Azure?</span></span> <span data-ttu-id="8d4cd-130">需要是開放原始碼、免費但具有強大功能嗎？</span><span class="sxs-lookup"><span data-stu-id="8d4cd-130">Open Source, free but powerful?</span></span> <span data-ttu-id="8d4cd-131">那麼，PF 會是一個理想的選擇。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-131">Then PF is a good choice.</span></span> <span data-ttu-id="8d4cd-132">藉由使用 [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) 範本，您只需 5 分鐘的時間，即可使用 FreeBSD 的 PF，在 Azure 中針對常見的 Web 伺服器案例，設定具備循環配置資源負載平衡功能的 NAT 防火牆。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-132">By using the template [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup), you only need five minutes to set up a NAT firewall with round-robin load balancing using FreeBSD's PF in Azure for common web server scenario.</span></span> 

<span data-ttu-id="8d4cd-133">如果您想要了解 Azure 中的 FreeBSD 方案，請參閱[Azure 上的 FreeBSD 簡介](freebsd-intro-on-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-133">If you want to learn the offering of FreeBSD in Azure, refer to [introduction to FreeBSD on Azure](freebsd-intro-on-azure.md).</span></span>

<span data-ttu-id="8d4cd-134">如果您想要深入了解 PF，請參考 [FreeBSD 手冊 (英文)](https://www.freebsd.org/doc/handbook/firewalls-pf.html) 或 [PF 使用者指南 (英文)](https://www.freebsd.org/doc/handbook/firewalls-pf.html)。</span><span class="sxs-lookup"><span data-stu-id="8d4cd-134">If you want to know more about PF, refer to [FreeBSD handbook](https://www.freebsd.org/doc/handbook/firewalls-pf.html) or [PF-User's Guide](https://www.freebsd.org/doc/handbook/firewalls-pf.html).</span></span>
