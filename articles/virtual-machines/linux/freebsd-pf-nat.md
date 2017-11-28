---
title: "aaaUse FreeBSD 封包篩選器 toocreate 在 Azure 中的防火牆 |Microsoft 文件"
description: "深入了解如何 toodeploy NAT 防火牆使用 FreeBSD 的 PF 在 Azure 中的。"
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
ms.openlocfilehash: 3d3a5dde2ca03ba6fc384581c786f5eb746e6d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-freebsds-packet-filter-toocreate-a-secure-firewall-in-azure"></a><span data-ttu-id="62f04-103">如何 toouse FreeBSD 封包篩選器 toocreate 安全的防火牆，在 Azure 中</span><span class="sxs-lookup"><span data-stu-id="62f04-103">How toouse FreeBSD's Packet Filter toocreate a secure firewall in Azure</span></span>
<span data-ttu-id="62f04-104">本文介紹如何 toodeploy NAT 防火牆 FreeBSD 的 Packer 篩選器，透過 Azure Resource Manager 範本使用常見的 web 伺服器案例。</span><span class="sxs-lookup"><span data-stu-id="62f04-104">This article introduces how toodeploy a NAT firewall using FreeBSD’s Packer Filter through Azure Resource Manager template for common web server scenario.</span></span>

## <a name="what-is-pf"></a><span data-ttu-id="62f04-105">什麼是 PF？</span><span class="sxs-lookup"><span data-stu-id="62f04-105">What is PF?</span></span>
<span data-ttu-id="62f04-106">PF (封包篩選器，也寫成 pf) 是一個 BSD 授權的具狀態封包篩選器，是防火牆軟體的一個核心部分。</span><span class="sxs-lookup"><span data-stu-id="62f04-106">PF (Packet Filter, also written pf) is a BSD licensed stateful packet filter, a central piece of software for firewalling.</span></span> <span data-ttu-id="62f04-107">PF 一直以來快速發展，現在已有數個超越其他可用防火牆的優點。</span><span class="sxs-lookup"><span data-stu-id="62f04-107">PF has since evolved quickly and now has several advantages over other available firewalls.</span></span> <span data-ttu-id="62f04-108">網路位址轉譯 (NAT) 為 PF 自第一天，然後封包排程器，並使用中佇列管理已經整合至 PF，透過整合 hello ALTQ，並且讓它成為可透過 PF 的組態設定。</span><span class="sxs-lookup"><span data-stu-id="62f04-108">Network Address Translation (NAT) is in PF since day one, then packet scheduler and active queue management have been integrated into PF, by integrating hello ALTQ and making it configurable through PF's configuration.</span></span> <span data-ttu-id="62f04-109">容錯移轉與備援、 authpf 工作階段驗證以及 ftp proxy tooease 防火牆 hello 困難 FTP 通訊協定，例如 pfsync 和 CARP 功能也有擴充 PF.</span><span class="sxs-lookup"><span data-stu-id="62f04-109">Features such as pfsync and CARP for failover and redundancy, authpf for session authentication, and ftp-proxy tooease firewalling hello difficult FTP protocol, have also extended PF.</span></span> <span data-ttu-id="62f04-110">簡單說來，PF 就是一個強大且功能豐富的防火牆。</span><span class="sxs-lookup"><span data-stu-id="62f04-110">In short, PF is a powerful and feature-rich firewall.</span></span> 

## <a name="get-started"></a><span data-ttu-id="62f04-111">開始使用</span><span class="sxs-lookup"><span data-stu-id="62f04-111">Get started</span></span>
<span data-ttu-id="62f04-112">如果您想要在您的 web 伺服器的 hello 雲端中設定安全的防火牆，請讓我們開始吧。</span><span class="sxs-lookup"><span data-stu-id="62f04-112">If you are interested in setting up a secure firewall in hello cloud for your web servers, then let’s get started.</span></span> <span data-ttu-id="62f04-113">您也可以套用這個 Azure Resource Manager 範本 tooset，註冊您的網路拓撲中使用的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="62f04-113">You can also apply hello scripts used in this Azure Resource Manager template tooset up your networking topology.</span></span>
<span data-ttu-id="62f04-114">hello Azure Resource Manager 範本設定 FreeBSD 虛擬機器執行之 NAT /redirection hello Nginx 網頁伺服器安裝並設定搭配使用 PF 和兩個 FreeBSD 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="62f04-114">hello Azure Resource Manager template set up a FreeBSD virtual machine that performs NAT /redirection using PF and two FreeBSD virtual machines with hello Nginx web server installed and configured.</span></span> <span data-ttu-id="62f04-115">此外 tooperforming NAT hello 兩部 web 伺服器的輸出流量，hello NAT/重新導向虛擬機器會攔截 HTTP 要求，並將他們重新導向以循環配置資源方式 toohello 兩部 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="62f04-115">In addition tooperforming NAT for hello two web servers egress traffic, hello NAT/redirection virtual machine intercepts HTTP requests and redirect them toohello two web servers in round-robin fashion.</span></span> <span data-ttu-id="62f04-116">hello VNet 使用 hello 私用路由的內部 IP 位址空間 10.0.0.2/24，而且您可以修改 hello 樣板的 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="62f04-116">hello VNet uses hello private non-routable IP address space 10.0.0.2/24 and you can modify hello parameters of hello template.</span></span> <span data-ttu-id="62f04-117">hello Azure Resource Manager 範本也會定義的 hello 是個別的路由集合中的整個 VNet 使用 toooverride Azure 的預設路由 hello 目的地 IP 位址為基礎的路由表。</span><span class="sxs-lookup"><span data-stu-id="62f04-117">hello Azure Resource Manager template also defines a route table for hello whole VNet, which is a collection of individual routes used toooverride Azure default routes based on hello destination IP address.</span></span> 

![pf_topology](./media/freebsd-pf-nat/pf_topology.jpg)
    
### <a name="deploy-through-azure-cli"></a><span data-ttu-id="62f04-119">透過 Azure CLI 進行部署</span><span class="sxs-lookup"><span data-stu-id="62f04-119">Deploy through Azure CLI</span></span>
<span data-ttu-id="62f04-120">您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="62f04-120">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="62f04-121">使用 [az group create](/cli/azure/group#create) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="62f04-121">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="62f04-122">hello 下列範例會建立資源群組名稱`myResourceGroup`在 hello`West US`位置。</span><span class="sxs-lookup"><span data-stu-id="62f04-122">hello following example creates a resource group name `myResourceGroup` in hello `West US` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="62f04-123">接下來，部署 hello 範本[pf freebsd 設定](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup)與[az 群組部署建立](/cli/azure/group/deployment#create)。</span><span class="sxs-lookup"><span data-stu-id="62f04-123">Next, deploy hello template [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="62f04-124">下載[azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json)底下 hello 相同的路徑，以及定義您自己的資源值，例如`adminPassword`， `networkPrefix`，和`domainNamePrefix`。</span><span class="sxs-lookup"><span data-stu-id="62f04-124">Download [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json) under hello same path and define your own resource values, such as `adminPassword`, `networkPrefix`, and `domainNamePrefix`.</span></span> 

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeploymentName \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/pf-freebsd-setup/azuredeploy.json \
    --parameters '@azuredeploy.parameters.json' --verbose
```

<span data-ttu-id="62f04-125">約五分鐘之後, 您會收到 hello 資訊的`"provisioningState": "Succeeded"`。</span><span class="sxs-lookup"><span data-stu-id="62f04-125">After about five minutes, you will get hello information of `"provisioningState": "Succeeded"`.</span></span> <span data-ttu-id="62f04-126">然後您可以 ssh toohello 前端 VM (NAT) 或存取 Nginx 網頁伺服器，在瀏覽器中的 hello 前端 VM (NAT) hello 公用 IP 位址或者 FQDN。</span><span class="sxs-lookup"><span data-stu-id="62f04-126">Then you can ssh toohello frontend VM (NAT) or access Nginx web server in a browser using hello public IP address or FQDN of hello frontend VM (NAT).</span></span> <span data-ttu-id="62f04-127">hello 下列範例會列出 FQDN 和公用 IP 位址指派 toohello 前端 VM (NAT) 在 hello`myResourceGroup`資源群組。</span><span class="sxs-lookup"><span data-stu-id="62f04-127">hello following example lists FQDN and public IP address that assigned toohello frontend VM (NAT) in hello `myResourceGroup` resource group.</span></span> 

```azurecli
az network public-ip list --resource-group myResourceGroup
```
    
## <a name="next-steps"></a><span data-ttu-id="62f04-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="62f04-128">Next steps</span></span>
<span data-ttu-id="62f04-129">您想 tooset 註冊您自己在 Azure 中的 NAT？</span><span class="sxs-lookup"><span data-stu-id="62f04-129">Do you want tooset up your own NAT in Azure?</span></span> <span data-ttu-id="62f04-130">需要是開放原始碼、免費但具有強大功能嗎？</span><span class="sxs-lookup"><span data-stu-id="62f04-130">Open Source, free but powerful?</span></span> <span data-ttu-id="62f04-131">那麼，PF 會是一個理想的選擇。</span><span class="sxs-lookup"><span data-stu-id="62f04-131">Then PF is a good choice.</span></span> <span data-ttu-id="62f04-132">使用 hello 範本[pf freebsd 設定](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup)，您只需要五分鐘 tooset NAT 防火牆設定具有循環配置資源負載平衡使用 FreeBSD 的 PF 在 Azure 中常見的 web 伺服器案例。</span><span class="sxs-lookup"><span data-stu-id="62f04-132">By using hello template [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup), you only need five minutes tooset up a NAT firewall with round-robin load balancing using FreeBSD's PF in Azure for common web server scenario.</span></span> 

<span data-ttu-id="62f04-133">如果您想在 Azure 中的 FreeBSD toolearn hello 供應項目，請參閱太[在 Azure 上的簡介 tooFreeBSD](freebsd-intro-on-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="62f04-133">If you want toolearn hello offering of FreeBSD in Azure, refer too[introduction tooFreeBSD on Azure](freebsd-intro-on-azure.md).</span></span>

<span data-ttu-id="62f04-134">如果您想深入了解 PF tooknow，請參閱太[FreeBSD 手冊](https://www.freebsd.org/doc/handbook/firewalls-pf.html)或[PF 使用者的指南](https://www.freebsd.org/doc/handbook/firewalls-pf.html)。</span><span class="sxs-lookup"><span data-stu-id="62f04-134">If you want tooknow more about PF, refer too[FreeBSD handbook](https://www.freebsd.org/doc/handbook/firewalls-pf.html) or [PF-User's Guide](https://www.freebsd.org/doc/handbook/firewalls-pf.html).</span></span>
