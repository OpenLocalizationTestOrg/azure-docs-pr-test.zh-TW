---
title: "aaaLinux，並在 Azure 上的開放原始碼計算 |Microsoft 文件"
description: "列出 Azure 上的 Linux 和開放原始碼運算文章，其中包括基本的 Linux 使用方式、有關在 Azure 上執行或上傳 Linux 映像的一些基本概念，以及其他有關特定技術與最佳化的內容。"
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: a7e608b5-26ea-41e0-b46b-1a483a257754
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/27/2016
ms.author: rasquill
ms.openlocfilehash: 3ce0dcc65f28d0dddb29f654409f6dae56213bc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="linux-and-open-source-computing-on-azure"></a><span data-ttu-id="b5631-103">Azure 上的 Linux 和開放原始碼運算</span><span class="sxs-lookup"><span data-stu-id="b5631-103">Linux and open-source computing on Azure</span></span>
<span data-ttu-id="b5631-104">找到您需要 toocreate 並管理 Linux 型虛擬機器 hello 傳統部署模型中所有的 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="b5631-104">Find all hello documentation you need toocreate and manage Linux-based virtual machines in hello classic deployment model.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b5631-105">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="b5631-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b5631-106">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="b5631-106">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b5631-107">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="b5631-107">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

## <a name="get-started"></a><span data-ttu-id="b5631-108">開始使用</span><span class="sxs-lookup"><span data-stu-id="b5631-108">Get Started</span></span>
* [<span data-ttu-id="b5631-109">Azure 上的 Linux 簡介</span><span class="sxs-lookup"><span data-stu-id="b5631-109">Introduction for Linux on Azure</span></span>](intro-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b5631-110">常見問題集的問題有關 Azure 虛擬機器建立 hello 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="b5631-110">Frequently asked question about Azure Virtual Machines created with hello classic deployment model</span></span>](classic/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-111">關於虛擬機器的映像</span><span class="sxs-lookup"><span data-stu-id="b5631-111">About images for virtual machines</span></span>](../windows/classic/about-images.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* <span data-ttu-id="b5631-112">[上傳您自己的 Distro 映像](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) (以及使用 [Azure 背書散發版本](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)的指示)</span><span class="sxs-lookup"><span data-stu-id="b5631-112">[Uploading your own Distro Image](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) (and also instructions using an [Azure-Endorsed Distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))</span></span>
* [<span data-ttu-id="b5631-113">登入 tooa Linux VM 使用 hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="b5631-113">Log on tooa Linux VM Using hello Azure classic portal</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="set-up"></a><span data-ttu-id="b5631-114">設定</span><span class="sxs-lookup"><span data-stu-id="b5631-114">Set up</span></span>
* [<span data-ttu-id="b5631-115">安裝 Azure 命令列介面 (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="b5631-115">Install Azure Command-Line Interface (Azure CLI)</span></span>](../../cli-install-nodejs.md)

## <a name="tutorials"></a><span data-ttu-id="b5631-116">教學課程</span><span class="sxs-lookup"><span data-stu-id="b5631-116">Tutorials</span></span>
* [<span data-ttu-id="b5631-117">在 Azure 中的 Linux 虛擬機器上安裝 hello LAMP 堆疊</span><span class="sxs-lookup"><span data-stu-id="b5631-117">Install hello LAMP Stack on a Linux virtual machine in Azure</span></span>](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b5631-118">Azure VM 上的 Ruby on Rails Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="b5631-118">Ruby on Rails Web application on an Azure VM</span></span>](classic/virtual-machines-linux-classic-ruby-rails-web-app.md)
* [<span data-ttu-id="b5631-119">做法：安裝 Apache Qpid Proton-C for AMQP 和服務匯流排</span><span class="sxs-lookup"><span data-stu-id="b5631-119">How to: Install Apache Qpid Proton-C for AMQP and Service Bus</span></span>](../../service-bus-messaging/service-bus-amqp-apache.md)

### <a name="databases"></a><span data-ttu-id="b5631-120">資料庫</span><span class="sxs-lookup"><span data-stu-id="b5631-120">Databases</span></span>
* [<span data-ttu-id="b5631-121">在 Azure 上最佳化 MySQL 的效能</span><span class="sxs-lookup"><span data-stu-id="b5631-121">Optimize Performance of MySQL on Azure</span></span>](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-122">MySQL 叢集</span><span class="sxs-lookup"><span data-stu-id="b5631-122">MySQL Clusters</span></span>](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-123">在 Azure 上執行 Cassandra 搭配 Linux 並透過 Node.js 進行存取</span><span class="sxs-lookup"><span data-stu-id="b5631-123">Running Cassandra with Linux on Azure and Accessing it from Node.js</span></span>](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-124">建立 MariaDbs 的多重主機叢集</span><span class="sxs-lookup"><span data-stu-id="b5631-124">Create a Multi-Master cluster of MariaDbs</span></span>](classic/mariadb-mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="hpc"></a><span data-ttu-id="b5631-125">HPC</span><span class="sxs-lookup"><span data-stu-id="b5631-125">HPC</span></span>
* [<span data-ttu-id="b5631-126">開始在 Azure 中的 HPC Pack 叢集使用 Linux 運算節點</span><span class="sxs-lookup"><span data-stu-id="b5631-126">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-127">在 Azure 中的 Linux 運算節點以 Microsoft HPC Pack 執行 NAMD</span><span class="sxs-lookup"><span data-stu-id="b5631-127">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-128">設定 Linux RDMA 叢集 toorun MPI 應用程式</span><span class="sxs-lookup"><span data-stu-id="b5631-128">Set up a Linux RDMA cluster toorun MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="docker"></a><span data-ttu-id="b5631-129">Docker</span><span class="sxs-lookup"><span data-stu-id="b5631-129">Docker</span></span>
* [<span data-ttu-id="b5631-130">使用從 hello Azure 命令列介面 (Azure CLI) hello Docker VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="b5631-130">Using hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)</span></span>](classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-131">使用從 hello Azure 入口網站的 hello Docker VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="b5631-131">Using hello Docker VM Extension from hello Azure portal</span></span>](classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-132">如何 toouse docker 電腦在 Azure 上</span><span class="sxs-lookup"><span data-stu-id="b5631-132">How toouse docker-machine on Azure</span></span>](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="ubuntu"></a><span data-ttu-id="b5631-133">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b5631-133">Ubuntu</span></span>
* [<span data-ttu-id="b5631-134">做法：MySQL 叢集</span><span class="sxs-lookup"><span data-stu-id="b5631-134">How to: MySQL Clusters</span></span>](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-135">做法：Node.js 和 Cassandra</span><span class="sxs-lookup"><span data-stu-id="b5631-135">How to: Node.js and Cassandra</span></span>](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="opensuse"></a><span data-ttu-id="b5631-136">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="b5631-136">OpenSUSE</span></span>
* [<span data-ttu-id="b5631-137">做法：安裝和執行 MySQL</span><span class="sxs-lookup"><span data-stu-id="b5631-137">How to: Install and Run MySQL</span></span>](classic/mysql-on-opensuse.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="coreos"></a><span data-ttu-id="b5631-138">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b5631-138">CoreOS</span></span>
* [<span data-ttu-id="b5631-139">做法：在 Azure 上使用 CoreOS</span><span class="sxs-lookup"><span data-stu-id="b5631-139">How to: Use CoreOS on Azure</span></span>](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="planning"></a><span data-ttu-id="b5631-140">規劃</span><span class="sxs-lookup"><span data-stu-id="b5631-140">Planning</span></span>
* [<span data-ttu-id="b5631-141">Azure 基礎結構服務實作指導方針</span><span class="sxs-lookup"><span data-stu-id="b5631-141">Azure infrastructure services implementation guidelines</span></span>](../windows/infrastructure-subscription-accounts-guidelines.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b5631-142">選取 Linux 使用者名稱</span><span class="sxs-lookup"><span data-stu-id="b5631-142">Selecting Linux Usernames</span></span>](usernames.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b5631-143">如何 tooconfigure 可用性設定組 hello 傳統部署模型中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b5631-143">How tooconfigure an availability set for virtual machines in hello classic deployment model</span></span>](../windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-144">如何在 Azure Vm 上的計劃中維護 tooSchedule</span><span class="sxs-lookup"><span data-stu-id="b5631-144">How tooSchedule Planned Maintenance on Azure VMs</span></span>](classic/planned-maintenance-schedule.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-145">管理虛擬機器 hello 可用性</span><span class="sxs-lookup"><span data-stu-id="b5631-145">Manage hello availability of virtual machines</span></span>](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b5631-146">Azure 中 Linux 虛擬機器預定進行的維修</span><span class="sxs-lookup"><span data-stu-id="b5631-146">Planned maintenance for Linux virtual machines in Azure</span></span>](planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="deployment"></a><span data-ttu-id="b5631-147">部署</span><span class="sxs-lookup"><span data-stu-id="b5631-147">Deployment</span></span>
* [<span data-ttu-id="b5631-148">建立執行 Linux 的自訂虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b5631-148">Create a custom virtual machine running Linux</span></span>](../windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-149">hello 基本概念： 擷取 Linux VM tooMake 範本</span><span class="sxs-lookup"><span data-stu-id="b5631-149">hello basics: Capturing a Linux VM tooMake a Template</span></span>](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-150">非背書散發套件的資訊</span><span class="sxs-lookup"><span data-stu-id="b5631-150">Information for Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="management"></a><span data-ttu-id="b5631-151">管理</span><span class="sxs-lookup"><span data-stu-id="b5631-151">Management</span></span>
* [<span data-ttu-id="b5631-152">SSH</span><span class="sxs-lookup"><span data-stu-id="b5631-152">SSH</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b5631-153">如何 tooReset 密碼或 SSH 屬性適用於 Linux</span><span class="sxs-lookup"><span data-stu-id="b5631-153">How tooReset a Password or SSH Properties for Linux</span></span>](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-154">使用 Root</span><span class="sxs-lookup"><span data-stu-id="b5631-154">Using Root</span></span>](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="azure-resources"></a><span data-ttu-id="b5631-155">Azure 資源</span><span class="sxs-lookup"><span data-stu-id="b5631-155">Azure Resources</span></span>
* [<span data-ttu-id="b5631-156">hello Azure Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="b5631-156">hello Azure Linux Agent</span></span>](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b5631-157">Azure VM 延伸模組與功能</span><span class="sxs-lookup"><span data-stu-id="b5631-157">Azure VM Extensions and Features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="b5631-158">將自訂資料插入 VM toouse 以便與雲端初始化</span><span class="sxs-lookup"><span data-stu-id="b5631-158">Injecting Custom Data into a VM toouse with Cloud-init</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="storage"></a><span data-ttu-id="b5631-159">儲存體</span><span class="sxs-lookup"><span data-stu-id="b5631-159">Storage</span></span>
* [<span data-ttu-id="b5631-160">附加資料磁碟 tooa Linux VM</span><span class="sxs-lookup"><span data-stu-id="b5631-160">Attaching a Data Disk tooa Linux VM</span></span>](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-161">從 Linux VM 卸離資料磁碟</span><span class="sxs-lookup"><span data-stu-id="b5631-161">Detaching a Data Disk from a Linux VM</span></span>](classic/detach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b5631-162">RAID</span><span class="sxs-lookup"><span data-stu-id="b5631-162">RAID</span></span>](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a><span data-ttu-id="b5631-163">網路</span><span class="sxs-lookup"><span data-stu-id="b5631-163">Networking</span></span>
* [<span data-ttu-id="b5631-164">如何 tooset 個端點在 Azure 中的傳統虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b5631-164">How tooset up endpoints on a classic virtual machine in Azure</span></span>](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="troubleshooting"></a><span data-ttu-id="b5631-165">疑難排解</span><span class="sxs-lookup"><span data-stu-id="b5631-165">Troubleshooting</span></span>
* [<span data-ttu-id="b5631-166">疑難排解安全殼層 (SSH) 連線 tooa Linux 型 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b5631-166">Troubleshoot Secure Shell (SSH) connections tooa Linux-based Azure virtual machine</span></span>](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b5631-167">針對在 Azure 中建立新 Linux 虛擬機器的傳統部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="b5631-167">Troubleshoot classic deployment issues with creating a new Linux virtual machine in Azure</span></span>](classic/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)  
* [<span data-ttu-id="b5631-168">針對在 Azure 中重新啟動或調整現有 Linux 虛擬機器的傳統部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="b5631-168">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>](../windows/restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 

## <a name="reference"></a><span data-ttu-id="b5631-169">參考</span><span class="sxs-lookup"><span data-stu-id="b5631-169">Reference</span></span>
* [<span data-ttu-id="b5631-170">Azure 服務管理 (asm) 模式中的 Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="b5631-170">Azure CLI commands in Azure Service Management (asm) mode</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="b5631-171">Azure 服務管理 REST API</span><span class="sxs-lookup"><span data-stu-id="b5631-171">Azure Service Management REST API</span></span>](https://msdn.microsoft.com/library/azure/ee460799.aspx)

## <a name="general-links"></a><span data-ttu-id="b5631-172">一般連結</span><span class="sxs-lookup"><span data-stu-id="b5631-172">General Links</span></span>
<span data-ttu-id="b5631-173">下列連結查看 hello 適用於 Microsoft 部落格、 Technet 網頁和外部網站，而上述 Azure.com 文件。</span><span class="sxs-lookup"><span data-stu-id="b5631-173">hello following links are for Microsoft blogs, Technet pages, and external sites rather than Azure.com documentation as above.</span></span> <span data-ttu-id="b5631-174">為 Azure 與 hello 的開放原始碼電腦世界會快速移動目標，它是幾乎某些 hello 下列連結已過期，*儘管*我們應該執行我們的最佳 toocontinually hello 事實加入較新的主題和移除過時的項目。</span><span class="sxs-lookup"><span data-stu-id="b5631-174">As both Azure and hello open-source computing world are fast-moving targets, it is almost certain that hello following links are out of date, *despite* hello fact that we shall do our best toocontinually add newer topics and remove out-of-date ones.</span></span> <span data-ttu-id="b5631-175">如果我們已遺失其中一個，請讓我們知道 hello 的註解或提交提取要求 tooour [GitHub 儲存機制](https://github.com/Azure/azure-content/)。</span><span class="sxs-lookup"><span data-stu-id="b5631-175">If we've missed one, please let us know in hello comments, or submit a pull request tooour [GitHub repo](https://github.com/Azure/azure-content/).</span></span>

* [<span data-ttu-id="b5631-176">在 Linux 上使用 Docker 容器執行 ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="b5631-176">Running ASP.NET 5 on Linux using Docker Containers</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/01/14/running-asp-net-5-applications-in-linux-containers-with-docker.aspx)
* [<span data-ttu-id="b5631-177">如何 tooDeploy CentOS VM 映像來自 OpenLogic，</span><span class="sxs-lookup"><span data-stu-id="b5631-177">How tooDeploy a CentOS VM Image from OpenLogic</span></span>](https://azure.microsoft.com/blog/2013/01/11/deploying-openlogic-centos-images-on-windows-azure-virtual-machines/)
* [<span data-ttu-id="b5631-178">SUSE 更新基礎結構</span><span class="sxs-lookup"><span data-stu-id="b5631-178">SUSE Update Infrastructure</span></span>](https://forums.suse.com/showthread.php?5622-New-Update-Infrastructure)
* [<span data-ttu-id="b5631-179">SUSE Linux Enterprise Server for SAP 雲端應用裝置程式庫</span><span class="sxs-lookup"><span data-stu-id="b5631-179">SUSE Linux Enterprise Server for SAP Cloud Appliance  Library</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver11sp3forsapcloudappliance/)
* [<span data-ttu-id="b5631-180">以 12 個步驟在 Azure 上建置高可用性的 Linux</span><span class="sxs-lookup"><span data-stu-id="b5631-180">Building Highly Available Linux on Azure in 12 Steps</span></span>](http://blogs.technet.com/b/keithmayer/archive/2014/10/03/quick-start-guide-building-highly-available-linux-servers-in-the-cloud-on-microsoft-azure.aspx)
* [<span data-ttu-id="b5631-181">透過 Azure CLI、node.js、jhawk 在 Azure 上自動佈建 Linux</span><span class="sxs-lookup"><span data-stu-id="b5631-181">Automate Provisioning Linux on Azure with Azure CLI, node.js, jhawk</span></span>](http://blogs.technet.com/b/keithmayer/archive/2014/11/24/step-by-step-automated-provisioning-for-linux-in-the-cloud-with-microsoft-azure-xplat-cli-json-and-node-js-part-1.aspx)
* [<span data-ttu-id="b5631-182">Azure 上的 GlusterFS</span><span class="sxs-lookup"><span data-stu-id="b5631-182">GlusterFS on Azure</span></span>](http://dastouri.azurewebsites.net/gluster-on-azure-part-1/)

### <a name="freebsd"></a><span data-ttu-id="b5631-183">FreeBSD</span><span class="sxs-lookup"><span data-stu-id="b5631-183">FreeBSD</span></span>
* [<span data-ttu-id="b5631-184">在 Azure 中執行 FreeBSD</span><span class="sxs-lookup"><span data-stu-id="b5631-184">Running FreeBSD in Azure</span></span>](https://azure.microsoft.com/blog/2014/05/22/running-freebsd-in-azure/)
* [<span data-ttu-id="b5631-185">輕鬆部署 FreeBSD</span><span class="sxs-lookup"><span data-stu-id="b5631-185">Easy Deploy FreeBSD</span></span>](http://msopentech.com/blog/2014/10/24/easy-deploy-freebsd-microsoft-azure-vm-depot/)
* [<span data-ttu-id="b5631-186">部署自訂的 FreeBSD 映像</span><span class="sxs-lookup"><span data-stu-id="b5631-186">Deploying a Customized FreeBSD Image</span></span>](http://msopentech.com/blog/2014/05/14/deploy-customize-freebsd-virtual-machine-image-microsoft-azure/)
* [<span data-ttu-id="b5631-187">適用於 Linux 檔案伺服器的 Kaspersky AV</span><span class="sxs-lookup"><span data-stu-id="b5631-187">Kaspersky AV for Linux File Server</span></span>](https://azure.microsoft.com/marketplace/partners/kaspersky-lab/kav-for-lfs-kav-for-lfs/)

### <a name="nosql"></a><span data-ttu-id="b5631-188">NoSQL</span><span class="sxs-lookup"><span data-stu-id="b5631-188">NoSQL</span></span>
* [<span data-ttu-id="b5631-189">Azure 的 8 個開放原始碼 NoSql 資料庫</span><span class="sxs-lookup"><span data-stu-id="b5631-189">8 Open-source NoSql Databases for Azure</span></span>](http://openness.microsoft.com/blog/2014/11/03/open-source-nosql-databases-microsoft-azure/)
* [<span data-ttu-id="b5631-190">Slideshare (MSOpenTech)︰Azure 上的 CouchDb 經驗</span><span class="sxs-lookup"><span data-stu-id="b5631-190">Slideshare (MSOpenTech): Experiences with CouchDb on Azure</span></span>](http://www.slideshare.net/brianbenz/experiences-using-couchdb-inside-microsofts-azure-team)
* [<span data-ttu-id="b5631-191">透過 node.js、CORS 和 Grunt 執行 CouchDB 即服務</span><span class="sxs-lookup"><span data-stu-id="b5631-191">Running CouchDB-as-a-Service with node.js, CORS, and Grunt</span></span>](http://msopentech.com/blog/2013/12/19/tutorial-building-multi-tier-windows-azure-web-application-use-cloudants-couchdb-service-node-js-cors-grunt-2/)
* [<span data-ttu-id="b5631-192">在 Windows 上 redis 在 hello Azure Redis 快取服務</span><span class="sxs-lookup"><span data-stu-id="b5631-192">Redis on Windows in hello Azure Redis Cache Service</span></span>](http://msopentech.com/blog/2014/05/12/redis-on-windows/)
* [<span data-ttu-id="b5631-193">宣佈 Redis 預覽版本的 ASP.NET 工作階段狀態提供者</span><span class="sxs-lookup"><span data-stu-id="b5631-193">Announcing ASP.NET Session State Provider for Redis Preview Release</span></span>](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)
* [<span data-ttu-id="b5631-194">部落格： RavenHQ 目前可在 hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="b5631-194">Blog: RavenHQ Now Available in hello Azure Marketplace</span></span>](https://azure.microsoft.com/blog/2014/08/12/ravenhq-now-available-in-the-azure-store/)

### <a name="big-data"></a><span data-ttu-id="b5631-195">巨量資料</span><span class="sxs-lookup"><span data-stu-id="b5631-195">Big Data</span></span>
* [<span data-ttu-id="b5631-196">在 Azure Linux VM 上安裝 Hadoop</span><span class="sxs-lookup"><span data-stu-id="b5631-196">Installing Hadoop on Azure Linux VMs</span></span>](http://blogs.msdn.com/b/benjguin/archive/2013/04/05/how-to-install-hadoop-on-windows-azure-linux-virtual-machines.aspx)
* [<span data-ttu-id="b5631-197">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5631-197">Azure HDInsight</span></span>](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/)

### <a name="relational-database"></a><span data-ttu-id="b5631-198">關聯式資料庫</span><span class="sxs-lookup"><span data-stu-id="b5631-198">Relational database</span></span>
* [<span data-ttu-id="b5631-199">Microsoft Azure 中的 MySQL 高可用性架構</span><span class="sxs-lookup"><span data-stu-id="b5631-199">MySQL High Availability Architecture in Microsoft Azure</span></span>](http://download.microsoft.com/download/6/1/C/61C0E37C-F252-4B33-9557-42B90BA3E472/MySQL_HADR_solution_in_Azure.pdf)
* [<span data-ttu-id="b5631-200">使用 corosync 安裝 Postgres，使用 ILB 安裝 pg_bouncer</span><span class="sxs-lookup"><span data-stu-id="b5631-200">Installing Postgres with corosync, pg_bouncer using ILB</span></span>](https://github.com/chgeuer/postgres-azure)

### <a name="linux-high-performance-computing-hpc"></a><span data-ttu-id="b5631-201">Linux 高效能運算 (HPC)</span><span class="sxs-lookup"><span data-stu-id="b5631-201">Linux high performance computing (HPC)</span></span>
* <span data-ttu-id="b5631-202">[快速入門範本：加速 SLURM 叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (以及[部落格文章](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))</span><span class="sxs-lookup"><span data-stu-id="b5631-202">[Quickstart template: Spin up a SLURM cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))</span></span>
* [<span data-ttu-id="b5631-203">快速入門範本：建立 Linux 計算節點的 HPC 叢集</span><span class="sxs-lookup"><span data-stu-id="b5631-203">Quickstart template: Create an HPC cluster with Linux compute nodes</span></span>](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)

### <a name="devops-management-and-optimization"></a><span data-ttu-id="b5631-204">開發、管理和最佳化</span><span class="sxs-lookup"><span data-stu-id="b5631-204">Devops, management, and optimization</span></span>
<span data-ttu-id="b5631-205">Hello world 的 devops、 管理及最佳化是相當以免受到擴充和非常快速地變更，您應該考慮 hello 清單下方的起始點。</span><span class="sxs-lookup"><span data-stu-id="b5631-205">As hello world of devops, management, and optimization is quite expansive and changing very quickly, you should consider hello list below a starting point.</span></span>

* [<span data-ttu-id="b5631-206">影片：Azure CLI 虛擬機器：使用 Chef、Puppet 和 Docker 管理 Linux VM</span><span class="sxs-lookup"><span data-stu-id="b5631-206">Video: Azure Virtual Machines : Using Chef, Puppet and Docker for managing Linux VMs</span></span>](https://azure.microsoft.com/blog/2014/12/15/azure-virtual-machines-using-chef-puppet-and-docker-for-managing-linux-vms/)
* [<span data-ttu-id="b5631-207">完成 CoreOS 與針織紋指南 tooautomated Kubernetes 叢集部署</span><span class="sxs-lookup"><span data-stu-id="b5631-207">Complete guide tooautomated Kubernetes cluster deployment with CoreOS and Weave</span></span>](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
* [<span data-ttu-id="b5631-208">Kubernetes Visualizer</span><span class="sxs-lookup"><span data-stu-id="b5631-208">Kubernetes Visualizer</span></span>](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [<span data-ttu-id="b5631-209">適用於 Azure 的 Jenkins 從屬外掛程式</span><span class="sxs-lookup"><span data-stu-id="b5631-209">Jenkins Slave Plug-in for Azure</span></span>](http://msopentech.com/blog/2014/09/23/announcing-jenkins-slave-plugin-azure/)
* [<span data-ttu-id="b5631-210">GitHub 儲存機制︰適用於 Azure 的 Jenkins 儲存體外掛程式</span><span class="sxs-lookup"><span data-stu-id="b5631-210">GitHub repo: Jenkins Storage Plug-in for Azure</span></span>](https://github.com/jenkinsci/windows-azure-storage-plugin)
* [<span data-ttu-id="b5631-211">協力廠商︰適用於 Azure 的 Hudson 從屬外掛程式</span><span class="sxs-lookup"><span data-stu-id="b5631-211">Third Party: Hudson Slave Plug-in for Azure</span></span>](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
* [<span data-ttu-id="b5631-212">協力廠商︰適用於 Azure 的 Hudson 儲存體外掛程式</span><span class="sxs-lookup"><span data-stu-id="b5631-212">Third Party: Hudson Storage Plug-in for Azure</span></span>](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [<span data-ttu-id="b5631-213">影片：Chef 是什麼，以及如何運作？</span><span class="sxs-lookup"><span data-stu-id="b5631-213">Video: What is Chef and How does it Work?</span></span>](https://msopentech.com/blog/2014/03/31/using-chef-to-manage-azure-resources/)
* [<span data-ttu-id="b5631-214">影片： 如何 tooUse 使用 Linux Vm 的 Azure 自動化</span><span class="sxs-lookup"><span data-stu-id="b5631-214">Video: How tooUse Azure Automation with Linux VMs</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* [<span data-ttu-id="b5631-215">部落格： 如何 toodo Powershell DSC for Linux</span><span class="sxs-lookup"><span data-stu-id="b5631-215">Blog: How toodo Powershell DSC for Linux</span></span>](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
* [<span data-ttu-id="b5631-216">GitHub：Docker 用戶端 DSC</span><span class="sxs-lookup"><span data-stu-id="b5631-216">GitHub: Docker Client DSC</span></span>](https://github.com/anweiss/DockerClientDSC)
* [<span data-ttu-id="b5631-217">Azure 的 Packer 外掛程式</span><span class="sxs-lookup"><span data-stu-id="b5631-217">Packer plugin for Azure</span></span>](https://github.com/msopentech/packer-azure)

