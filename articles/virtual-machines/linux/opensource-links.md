---
title: "Azure 上的 Linux 和開放原始碼運算 | Microsoft Docs"
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
ms.openlocfilehash: 1cdd0e68368d2dc376ee45df67bf5e75288d4ca3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="linux-and-open-source-computing-on-azure"></a><span data-ttu-id="0a957-103">Azure 上的 Linux 和開放原始碼運算</span><span class="sxs-lookup"><span data-stu-id="0a957-103">Linux and open-source computing on Azure</span></span>
<span data-ttu-id="0a957-104">尋找在傳統部署模型中建立和管理以 Linux 為基礎的虛擬機器所需的所有說明文件。</span><span class="sxs-lookup"><span data-stu-id="0a957-104">Find all the documentation you need to create and manage Linux-based virtual machines in the classic deployment model.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="0a957-105">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="0a957-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0a957-106">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="0a957-106">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="0a957-107">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="0a957-107">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

## <a name="get-started"></a><span data-ttu-id="0a957-108">開始使用</span><span class="sxs-lookup"><span data-stu-id="0a957-108">Get Started</span></span>
* [<span data-ttu-id="0a957-109">Azure 上的 Linux 簡介</span><span class="sxs-lookup"><span data-stu-id="0a957-109">Introduction for Linux on Azure</span></span>](intro-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0a957-110">關於以傳統部署模型建立之 Azure 虛擬機器的常見問題集</span><span class="sxs-lookup"><span data-stu-id="0a957-110">Frequently asked question about Azure Virtual Machines created with the classic deployment model</span></span>](classic/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-111">關於虛擬機器的映像</span><span class="sxs-lookup"><span data-stu-id="0a957-111">About images for virtual machines</span></span>](../windows/classic/about-images.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* <span data-ttu-id="0a957-112">[上傳您自己的 Distro 映像](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) (以及使用 [Azure 背書散發版本](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)的指示)</span><span class="sxs-lookup"><span data-stu-id="0a957-112">[Uploading your own Distro Image](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) (and also instructions using an [Azure-Endorsed Distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))</span></span>
* [<span data-ttu-id="0a957-113">使用 Azure 傳統入口網站登入 Linux VM</span><span class="sxs-lookup"><span data-stu-id="0a957-113">Log on to a Linux VM Using the Azure classic portal</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="set-up"></a><span data-ttu-id="0a957-114">設定</span><span class="sxs-lookup"><span data-stu-id="0a957-114">Set up</span></span>
* [<span data-ttu-id="0a957-115">安裝 Azure 命令列介面 (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="0a957-115">Install Azure Command-Line Interface (Azure CLI)</span></span>](../../cli-install-nodejs.md)

## <a name="tutorials"></a><span data-ttu-id="0a957-116">教學課程</span><span class="sxs-lookup"><span data-stu-id="0a957-116">Tutorials</span></span>
* [<span data-ttu-id="0a957-117">在 Azure 中的 Linux 虛擬機器上安裝 LAMP 堆疊</span><span class="sxs-lookup"><span data-stu-id="0a957-117">Install the LAMP Stack on a Linux virtual machine in Azure</span></span>](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0a957-118">Azure VM 上的 Ruby on Rails Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0a957-118">Ruby on Rails Web application on an Azure VM</span></span>](classic/virtual-machines-linux-classic-ruby-rails-web-app.md)
* [<span data-ttu-id="0a957-119">做法：安裝 Apache Qpid Proton-C for AMQP 和服務匯流排</span><span class="sxs-lookup"><span data-stu-id="0a957-119">How to: Install Apache Qpid Proton-C for AMQP and Service Bus</span></span>](../../service-bus-messaging/service-bus-amqp-apache.md)

### <a name="databases"></a><span data-ttu-id="0a957-120">資料庫</span><span class="sxs-lookup"><span data-stu-id="0a957-120">Databases</span></span>
* [<span data-ttu-id="0a957-121">在 Azure 上最佳化 MySQL 的效能</span><span class="sxs-lookup"><span data-stu-id="0a957-121">Optimize Performance of MySQL on Azure</span></span>](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-122">MySQL 叢集</span><span class="sxs-lookup"><span data-stu-id="0a957-122">MySQL Clusters</span></span>](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-123">在 Azure 上執行 Cassandra 搭配 Linux 並透過 Node.js 進行存取</span><span class="sxs-lookup"><span data-stu-id="0a957-123">Running Cassandra with Linux on Azure and Accessing it from Node.js</span></span>](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-124">建立 MariaDbs 的多重主機叢集</span><span class="sxs-lookup"><span data-stu-id="0a957-124">Create a Multi-Master cluster of MariaDbs</span></span>](classic/mariadb-mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="hpc"></a><span data-ttu-id="0a957-125">HPC</span><span class="sxs-lookup"><span data-stu-id="0a957-125">HPC</span></span>
* [<span data-ttu-id="0a957-126">開始在 Azure 中的 HPC Pack 叢集使用 Linux 運算節點</span><span class="sxs-lookup"><span data-stu-id="0a957-126">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-127">在 Azure 中的 Linux 運算節點以 Microsoft HPC Pack 執行 NAMD</span><span class="sxs-lookup"><span data-stu-id="0a957-127">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-128">設定 Linux RDMA 叢集以執行 MPI 應用程式</span><span class="sxs-lookup"><span data-stu-id="0a957-128">Set up a Linux RDMA cluster to run MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="docker"></a><span data-ttu-id="0a957-129">Docker</span><span class="sxs-lookup"><span data-stu-id="0a957-129">Docker</span></span>
* [<span data-ttu-id="0a957-130">透過 Azure 命令列介面 (Azure CL) 使用 Docker VM 延伸模組</span><span class="sxs-lookup"><span data-stu-id="0a957-130">Using the Docker VM Extension from the Azure Command-line Interface (Azure CLI)</span></span>](classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-131">使用 Azure 入口網站中的Docker VM 擴充程式</span><span class="sxs-lookup"><span data-stu-id="0a957-131">Using the Docker VM Extension from the Azure portal</span></span>](classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-132">如何在 Azure 上使用 docker-machine</span><span class="sxs-lookup"><span data-stu-id="0a957-132">How to use docker-machine on Azure</span></span>](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="ubuntu"></a><span data-ttu-id="0a957-133">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="0a957-133">Ubuntu</span></span>
* [<span data-ttu-id="0a957-134">做法：MySQL 叢集</span><span class="sxs-lookup"><span data-stu-id="0a957-134">How to: MySQL Clusters</span></span>](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-135">做法：Node.js 和 Cassandra</span><span class="sxs-lookup"><span data-stu-id="0a957-135">How to: Node.js and Cassandra</span></span>](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="opensuse"></a><span data-ttu-id="0a957-136">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="0a957-136">OpenSUSE</span></span>
* [<span data-ttu-id="0a957-137">做法：安裝和執行 MySQL</span><span class="sxs-lookup"><span data-stu-id="0a957-137">How to: Install and Run MySQL</span></span>](classic/mysql-on-opensuse.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="coreos"></a><span data-ttu-id="0a957-138">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0a957-138">CoreOS</span></span>
* [<span data-ttu-id="0a957-139">做法：在 Azure 上使用 CoreOS</span><span class="sxs-lookup"><span data-stu-id="0a957-139">How to: Use CoreOS on Azure</span></span>](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="planning"></a><span data-ttu-id="0a957-140">規劃</span><span class="sxs-lookup"><span data-stu-id="0a957-140">Planning</span></span>
* [<span data-ttu-id="0a957-141">Azure 基礎結構服務實作指導方針</span><span class="sxs-lookup"><span data-stu-id="0a957-141">Azure infrastructure services implementation guidelines</span></span>](../windows/infrastructure-subscription-accounts-guidelines.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0a957-142">選取 Linux 使用者名稱</span><span class="sxs-lookup"><span data-stu-id="0a957-142">Selecting Linux Usernames</span></span>](usernames.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0a957-143">如何以傳統部署模型設定虛擬機器的可用性設定組</span><span class="sxs-lookup"><span data-stu-id="0a957-143">How to configure an availability set for virtual machines in the classic deployment model</span></span>](../windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-144">如何排定在 Azure VM 上的計劃性維護</span><span class="sxs-lookup"><span data-stu-id="0a957-144">How to Schedule Planned Maintenance on Azure VMs</span></span>](classic/planned-maintenance-schedule.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-145">管理虛擬機器的可用性</span><span class="sxs-lookup"><span data-stu-id="0a957-145">Manage the availability of virtual machines</span></span>](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0a957-146">Azure 中 Linux 虛擬機器預定進行的維修</span><span class="sxs-lookup"><span data-stu-id="0a957-146">Planned maintenance for Linux virtual machines in Azure</span></span>](planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="deployment"></a><span data-ttu-id="0a957-147">部署</span><span class="sxs-lookup"><span data-stu-id="0a957-147">Deployment</span></span>
* [<span data-ttu-id="0a957-148">建立執行 Linux 的自訂虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0a957-148">Create a custom virtual machine running Linux</span></span>](../windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-149">基本概念：擷取 Linux VM 來製作範本</span><span class="sxs-lookup"><span data-stu-id="0a957-149">The basics: Capturing a Linux VM to Make a Template</span></span>](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-150">非背書散發套件的資訊</span><span class="sxs-lookup"><span data-stu-id="0a957-150">Information for Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="management"></a><span data-ttu-id="0a957-151">管理</span><span class="sxs-lookup"><span data-stu-id="0a957-151">Management</span></span>
* [<span data-ttu-id="0a957-152">SSH</span><span class="sxs-lookup"><span data-stu-id="0a957-152">SSH</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0a957-153">如何重設 Linux 的密碼或 SSH 屬性</span><span class="sxs-lookup"><span data-stu-id="0a957-153">How to Reset a Password or SSH Properties for Linux</span></span>](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-154">使用 Root</span><span class="sxs-lookup"><span data-stu-id="0a957-154">Using Root</span></span>](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="azure-resources"></a><span data-ttu-id="0a957-155">Azure 資源</span><span class="sxs-lookup"><span data-stu-id="0a957-155">Azure Resources</span></span>
* [<span data-ttu-id="0a957-156">Azure Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="0a957-156">The Azure Linux Agent</span></span>](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0a957-157">Azure VM 延伸模組與功能</span><span class="sxs-lookup"><span data-stu-id="0a957-157">Azure VM Extensions and Features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="0a957-158">將自訂資料插入 VM 中以搭配 Cloud-init 使用</span><span class="sxs-lookup"><span data-stu-id="0a957-158">Injecting Custom Data into a VM to use with Cloud-init</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="storage"></a><span data-ttu-id="0a957-159">儲存體</span><span class="sxs-lookup"><span data-stu-id="0a957-159">Storage</span></span>
* [<span data-ttu-id="0a957-160">將資料磁碟連接至 Linux VM</span><span class="sxs-lookup"><span data-stu-id="0a957-160">Attaching a Data Disk to a Linux VM</span></span>](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-161">從 Linux VM 卸離資料磁碟</span><span class="sxs-lookup"><span data-stu-id="0a957-161">Detaching a Data Disk from a Linux VM</span></span>](classic/detach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="0a957-162">RAID</span><span class="sxs-lookup"><span data-stu-id="0a957-162">RAID</span></span>](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a><span data-ttu-id="0a957-163">網路</span><span class="sxs-lookup"><span data-stu-id="0a957-163">Networking</span></span>
* [<span data-ttu-id="0a957-164">如何在 Azure 中的傳統虛擬機器上設定端點</span><span class="sxs-lookup"><span data-stu-id="0a957-164">How to set up endpoints on a classic virtual machine in Azure</span></span>](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="troubleshooting"></a><span data-ttu-id="0a957-165">疑難排解</span><span class="sxs-lookup"><span data-stu-id="0a957-165">Troubleshooting</span></span>
* [<span data-ttu-id="0a957-166">疑難排解以 Linux 為基礎之 Azure 虛擬機器的安全殼層 (SSH) 連線</span><span class="sxs-lookup"><span data-stu-id="0a957-166">Troubleshoot Secure Shell (SSH) connections to a Linux-based Azure virtual machine</span></span>](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0a957-167">針對在 Azure 中建立新 Linux 虛擬機器的傳統部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0a957-167">Troubleshoot classic deployment issues with creating a new Linux virtual machine in Azure</span></span>](classic/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)  
* [<span data-ttu-id="0a957-168">針對在 Azure 中重新啟動或調整現有 Linux 虛擬機器的傳統部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0a957-168">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>](../windows/restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 

## <a name="reference"></a><span data-ttu-id="0a957-169">參考</span><span class="sxs-lookup"><span data-stu-id="0a957-169">Reference</span></span>
* [<span data-ttu-id="0a957-170">Azure 服務管理 (asm) 模式中的 Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="0a957-170">Azure CLI commands in Azure Service Management (asm) mode</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="0a957-171">Azure 服務管理 REST API</span><span class="sxs-lookup"><span data-stu-id="0a957-171">Azure Service Management REST API</span></span>](https://msdn.microsoft.com/library/azure/ee460799.aspx)

## <a name="general-links"></a><span data-ttu-id="0a957-172">一般連結</span><span class="sxs-lookup"><span data-stu-id="0a957-172">General Links</span></span>
<span data-ttu-id="0a957-173">下列連結是上述 Azure.com 文件之外的 Microsoft 部落格、Technet 頁面和外部網站。</span><span class="sxs-lookup"><span data-stu-id="0a957-173">The following links are for Microsoft blogs, Technet pages, and external sites rather than Azure.com documentation as above.</span></span> <span data-ttu-id="0a957-174">由於 Azure 和開放原始碼運算的世界都是變動迅速的目標，因此「儘管」  我們會盡全力持續加入較新的主題並移除過期的主題，但我們也幾乎可以肯定下列連結已經過時了。</span><span class="sxs-lookup"><span data-stu-id="0a957-174">As both Azure and the open-source computing world are fast-moving targets, it is almost certain that the following links are out of date, *despite* the fact that we shall do our best to continually add newer topics and remove out-of-date ones.</span></span> <span data-ttu-id="0a957-175">如果我們遺漏了什麼，請在註解中讓我們知道，或將提取要求提交至我們的 [Github 儲存機制](https://github.com/Azure/azure-content/)。</span><span class="sxs-lookup"><span data-stu-id="0a957-175">If we've missed one, please let us know in the comments, or submit a pull request to our [GitHub repo](https://github.com/Azure/azure-content/).</span></span>

* [<span data-ttu-id="0a957-176">在 Linux 上使用 Docker 容器執行 ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="0a957-176">Running ASP.NET 5 on Linux using Docker Containers</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/01/14/running-asp-net-5-applications-in-linux-containers-with-docker.aspx)
* [<span data-ttu-id="0a957-177">如何部署 OpenLogic 提供的 CentOS VM 映像</span><span class="sxs-lookup"><span data-stu-id="0a957-177">How to Deploy a CentOS VM Image from OpenLogic</span></span>](https://azure.microsoft.com/blog/2013/01/11/deploying-openlogic-centos-images-on-windows-azure-virtual-machines/)
* [<span data-ttu-id="0a957-178">SUSE 更新基礎結構</span><span class="sxs-lookup"><span data-stu-id="0a957-178">SUSE Update Infrastructure</span></span>](https://forums.suse.com/showthread.php?5622-New-Update-Infrastructure)
* [<span data-ttu-id="0a957-179">SUSE Linux Enterprise Server for SAP 雲端應用裝置程式庫</span><span class="sxs-lookup"><span data-stu-id="0a957-179">SUSE Linux Enterprise Server for SAP Cloud Appliance  Library</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver11sp3forsapcloudappliance/)
* [<span data-ttu-id="0a957-180">以 12 個步驟在 Azure 上建置高可用性的 Linux</span><span class="sxs-lookup"><span data-stu-id="0a957-180">Building Highly Available Linux on Azure in 12 Steps</span></span>](http://blogs.technet.com/b/keithmayer/archive/2014/10/03/quick-start-guide-building-highly-available-linux-servers-in-the-cloud-on-microsoft-azure.aspx)
* [<span data-ttu-id="0a957-181">透過 Azure CLI、node.js、jhawk 在 Azure 上自動佈建 Linux</span><span class="sxs-lookup"><span data-stu-id="0a957-181">Automate Provisioning Linux on Azure with Azure CLI, node.js, jhawk</span></span>](http://blogs.technet.com/b/keithmayer/archive/2014/11/24/step-by-step-automated-provisioning-for-linux-in-the-cloud-with-microsoft-azure-xplat-cli-json-and-node-js-part-1.aspx)
* [<span data-ttu-id="0a957-182">Azure 上的 GlusterFS</span><span class="sxs-lookup"><span data-stu-id="0a957-182">GlusterFS on Azure</span></span>](http://dastouri.azurewebsites.net/gluster-on-azure-part-1/)

### <a name="freebsd"></a><span data-ttu-id="0a957-183">FreeBSD</span><span class="sxs-lookup"><span data-stu-id="0a957-183">FreeBSD</span></span>
* [<span data-ttu-id="0a957-184">在 Azure 中執行 FreeBSD</span><span class="sxs-lookup"><span data-stu-id="0a957-184">Running FreeBSD in Azure</span></span>](https://azure.microsoft.com/blog/2014/05/22/running-freebsd-in-azure/)
* [<span data-ttu-id="0a957-185">輕鬆部署 FreeBSD</span><span class="sxs-lookup"><span data-stu-id="0a957-185">Easy Deploy FreeBSD</span></span>](http://msopentech.com/blog/2014/10/24/easy-deploy-freebsd-microsoft-azure-vm-depot/)
* [<span data-ttu-id="0a957-186">部署自訂的 FreeBSD 映像</span><span class="sxs-lookup"><span data-stu-id="0a957-186">Deploying a Customized FreeBSD Image</span></span>](http://msopentech.com/blog/2014/05/14/deploy-customize-freebsd-virtual-machine-image-microsoft-azure/)
* [<span data-ttu-id="0a957-187">適用於 Linux 檔案伺服器的 Kaspersky AV</span><span class="sxs-lookup"><span data-stu-id="0a957-187">Kaspersky AV for Linux File Server</span></span>](https://azure.microsoft.com/marketplace/partners/kaspersky-lab/kav-for-lfs-kav-for-lfs/)

### <a name="nosql"></a><span data-ttu-id="0a957-188">NoSQL</span><span class="sxs-lookup"><span data-stu-id="0a957-188">NoSQL</span></span>
* [<span data-ttu-id="0a957-189">Azure 的 8 個開放原始碼 NoSql 資料庫</span><span class="sxs-lookup"><span data-stu-id="0a957-189">8 Open-source NoSql Databases for Azure</span></span>](http://openness.microsoft.com/blog/2014/11/03/open-source-nosql-databases-microsoft-azure/)
* [<span data-ttu-id="0a957-190">Slideshare (MSOpenTech)︰Azure 上的 CouchDb 經驗</span><span class="sxs-lookup"><span data-stu-id="0a957-190">Slideshare (MSOpenTech): Experiences with CouchDb on Azure</span></span>](http://www.slideshare.net/brianbenz/experiences-using-couchdb-inside-microsofts-azure-team)
* [<span data-ttu-id="0a957-191">透過 node.js、CORS 和 Grunt 執行 CouchDB 即服務</span><span class="sxs-lookup"><span data-stu-id="0a957-191">Running CouchDB-as-a-Service with node.js, CORS, and Grunt</span></span>](http://msopentech.com/blog/2013/12/19/tutorial-building-multi-tier-windows-azure-web-application-use-cloudants-couchdb-service-node-js-cors-grunt-2/)
* [<span data-ttu-id="0a957-192">Azure Redis 快取服務中的 Redis on Windows</span><span class="sxs-lookup"><span data-stu-id="0a957-192">Redis on Windows in the Azure Redis Cache Service</span></span>](http://msopentech.com/blog/2014/05/12/redis-on-windows/)
* [<span data-ttu-id="0a957-193">宣佈 Redis 預覽版本的 ASP.NET 工作階段狀態提供者</span><span class="sxs-lookup"><span data-stu-id="0a957-193">Announcing ASP.NET Session State Provider for Redis Preview Release</span></span>](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)
* [<span data-ttu-id="0a957-194">部落格：Azure Marketplace 現已提供 RavenHQ</span><span class="sxs-lookup"><span data-stu-id="0a957-194">Blog: RavenHQ Now Available in the Azure Marketplace</span></span>](https://azure.microsoft.com/blog/2014/08/12/ravenhq-now-available-in-the-azure-store/)

### <a name="big-data"></a><span data-ttu-id="0a957-195">巨量資料</span><span class="sxs-lookup"><span data-stu-id="0a957-195">Big Data</span></span>
* [<span data-ttu-id="0a957-196">在 Azure Linux VM 上安裝 Hadoop</span><span class="sxs-lookup"><span data-stu-id="0a957-196">Installing Hadoop on Azure Linux VMs</span></span>](http://blogs.msdn.com/b/benjguin/archive/2013/04/05/how-to-install-hadoop-on-windows-azure-linux-virtual-machines.aspx)
* [<span data-ttu-id="0a957-197">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a957-197">Azure HDInsight</span></span>](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/)

### <a name="relational-database"></a><span data-ttu-id="0a957-198">關聯式資料庫</span><span class="sxs-lookup"><span data-stu-id="0a957-198">Relational database</span></span>
* [<span data-ttu-id="0a957-199">Microsoft Azure 中的 MySQL 高可用性架構</span><span class="sxs-lookup"><span data-stu-id="0a957-199">MySQL High Availability Architecture in Microsoft Azure</span></span>](http://download.microsoft.com/download/6/1/C/61C0E37C-F252-4B33-9557-42B90BA3E472/MySQL_HADR_solution_in_Azure.pdf)
* [<span data-ttu-id="0a957-200">使用 corosync 安裝 Postgres，使用 ILB 安裝 pg_bouncer</span><span class="sxs-lookup"><span data-stu-id="0a957-200">Installing Postgres with corosync, pg_bouncer using ILB</span></span>](https://github.com/chgeuer/postgres-azure)

### <a name="linux-high-performance-computing-hpc"></a><span data-ttu-id="0a957-201">Linux 高效能運算 (HPC)</span><span class="sxs-lookup"><span data-stu-id="0a957-201">Linux high performance computing (HPC)</span></span>
* <span data-ttu-id="0a957-202">[快速入門範本：加速 SLURM 叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (以及[部落格文章](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))</span><span class="sxs-lookup"><span data-stu-id="0a957-202">[Quickstart template: Spin up a SLURM cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))</span></span>
* [<span data-ttu-id="0a957-203">快速入門範本：建立 Linux 計算節點的 HPC 叢集</span><span class="sxs-lookup"><span data-stu-id="0a957-203">Quickstart template: Create an HPC cluster with Linux compute nodes</span></span>](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)

### <a name="devops-management-and-optimization"></a><span data-ttu-id="0a957-204">開發、管理和最佳化</span><span class="sxs-lookup"><span data-stu-id="0a957-204">Devops, management, and optimization</span></span>
<span data-ttu-id="0a957-205">由於開發、管理和最佳化的領域相當廣泛、瞬息萬變，您應考慮從下列清單著手。</span><span class="sxs-lookup"><span data-stu-id="0a957-205">As the world of devops, management, and optimization is quite expansive and changing very quickly, you should consider the list below a starting point.</span></span>

* [<span data-ttu-id="0a957-206">影片：Azure CLI 虛擬機器：使用 Chef、Puppet 和 Docker 管理 Linux VM</span><span class="sxs-lookup"><span data-stu-id="0a957-206">Video: Azure Virtual Machines : Using Chef, Puppet and Docker for managing Linux VMs</span></span>](https://azure.microsoft.com/blog/2014/12/15/azure-virtual-machines-using-chef-puppet-and-docker-for-managing-linux-vms/)
* [<span data-ttu-id="0a957-207">使用 CoreOS 和 Weave 自動部署 Kubernetes 叢集的完整指南</span><span class="sxs-lookup"><span data-stu-id="0a957-207">Complete guide to automated Kubernetes cluster deployment with CoreOS and Weave</span></span>](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
* [<span data-ttu-id="0a957-208">Kubernetes Visualizer</span><span class="sxs-lookup"><span data-stu-id="0a957-208">Kubernetes Visualizer</span></span>](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [<span data-ttu-id="0a957-209">適用於 Azure 的 Jenkins 從屬外掛程式</span><span class="sxs-lookup"><span data-stu-id="0a957-209">Jenkins Slave Plug-in for Azure</span></span>](http://msopentech.com/blog/2014/09/23/announcing-jenkins-slave-plugin-azure/)
* [<span data-ttu-id="0a957-210">GitHub 儲存機制︰適用於 Azure 的 Jenkins 儲存體外掛程式</span><span class="sxs-lookup"><span data-stu-id="0a957-210">GitHub repo: Jenkins Storage Plug-in for Azure</span></span>](https://github.com/jenkinsci/windows-azure-storage-plugin)
* [<span data-ttu-id="0a957-211">協力廠商︰適用於 Azure 的 Hudson 從屬外掛程式</span><span class="sxs-lookup"><span data-stu-id="0a957-211">Third Party: Hudson Slave Plug-in for Azure</span></span>](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
* [<span data-ttu-id="0a957-212">協力廠商︰適用於 Azure 的 Hudson 儲存體外掛程式</span><span class="sxs-lookup"><span data-stu-id="0a957-212">Third Party: Hudson Storage Plug-in for Azure</span></span>](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [<span data-ttu-id="0a957-213">影片：Chef 是什麼，以及如何運作？</span><span class="sxs-lookup"><span data-stu-id="0a957-213">Video: What is Chef and How does it Work?</span></span>](https://msopentech.com/blog/2014/03/31/using-chef-to-manage-azure-resources/)
* [<span data-ttu-id="0a957-214">影片：如何在 Linux VM 上使用 Azure 自動化</span><span class="sxs-lookup"><span data-stu-id="0a957-214">Video: How to Use Azure Automation with Linux VMs</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* [<span data-ttu-id="0a957-215">部落格：如何使用 Powershell DSC for Linux</span><span class="sxs-lookup"><span data-stu-id="0a957-215">Blog: How to do Powershell DSC for Linux</span></span>](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
* [<span data-ttu-id="0a957-216">GitHub：Docker 用戶端 DSC</span><span class="sxs-lookup"><span data-stu-id="0a957-216">GitHub: Docker Client DSC</span></span>](https://github.com/anweiss/DockerClientDSC)
* [<span data-ttu-id="0a957-217">Azure 的 Packer 外掛程式</span><span class="sxs-lookup"><span data-stu-id="0a957-217">Packer plugin for Azure</span></span>](https://github.com/msopentech/packer-azure)

