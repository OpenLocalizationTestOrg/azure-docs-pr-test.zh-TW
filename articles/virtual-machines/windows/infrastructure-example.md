---
title: "範例 Azure 基礎結構逐步解說 | Microsoft Docs"
description: "了解適合用來在 Azure 中部署範例基礎結構的關鍵設計和實作指導方針。"
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7032b586-e4e5-4954-952f-fdfc03fc1980
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 84cefcdb85f1a3c753027e827abde010b461cda7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a><span data-ttu-id="b7278-103">適用於 Windows VM 的範例 Azure 基礎結構逐步解說</span><span class="sxs-lookup"><span data-stu-id="b7278-103">Example Azure infrastructure walkthrough for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="b7278-104">本文將逐步解說建置範例應用程式基礎結構的方法。</span><span class="sxs-lookup"><span data-stu-id="b7278-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="b7278-105">我們會詳述設計簡單線上商店基礎結構的方式，此線上商店能將所有命名慣例、可用性設定組、虛擬網路及負載平衡器的指導方針和決定集合在一起，並實際部署您的虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="b7278-105">We detail designing an infrastructure for a simple on-line store that brings together all the guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="b7278-106">範例工作負載</span><span class="sxs-lookup"><span data-stu-id="b7278-106">Example workload</span></span>
<span data-ttu-id="b7278-107">Adventure Works Cycles 想要在 Azure 中建置一個線上商店，該商店將包含：</span><span class="sxs-lookup"><span data-stu-id="b7278-107">Adventure Works Cycles wants to build an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="b7278-108">兩個在 Web 層級中執行用戶端前端的 IIS 伺服器</span><span class="sxs-lookup"><span data-stu-id="b7278-108">Two IIS servers running the client front-end in a web tier</span></span>
* <span data-ttu-id="b7278-109">兩個在應用程式層級中處理資料和訂單的 IIS 伺服器</span><span class="sxs-lookup"><span data-stu-id="b7278-109">Two IIS servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="b7278-110">含有 AlwaysOn 可用性群組的兩個 Microsoft SQL Server 執行個體 (有兩部 SQL Server 和一個多數節點見證)，負責在資料庫層級中儲存產品資料和訂單</span><span class="sxs-lookup"><span data-stu-id="b7278-110">Two Microsoft SQL Server instances with AlwaysOn availability groups (two SQL Servers and a majority node witness) for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="b7278-111">兩個在驗證層級中針對客戶帳戶及供應商的 Active Directory 網域控制站</span><span class="sxs-lookup"><span data-stu-id="b7278-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="b7278-112">所有伺服器皆位於兩個子網路中：</span><span class="sxs-lookup"><span data-stu-id="b7278-112">All the servers are located in two subnets:</span></span>
  * <span data-ttu-id="b7278-113">一個適用於網頁伺服器的前端子網路</span><span class="sxs-lookup"><span data-stu-id="b7278-113">a front-end subnet for the web servers</span></span> 
  * <span data-ttu-id="b7278-114">一個適用於應用程式伺服器、SQL 叢集及網域控制站的後端子網路</span><span class="sxs-lookup"><span data-stu-id="b7278-114">a back-end subnet for the application servers, SQL cluster, and domain controllers</span></span>

![不同應用程式基礎結構層級的圖表](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="b7278-116">連入的安全網路流量必須在客戶瀏覽線上商店時，於網頁伺服器之間達成負載平衡。</span><span class="sxs-lookup"><span data-stu-id="b7278-116">Incoming secure web traffic must be load-balanced among the web servers as customers browse the on-line store.</span></span> <span data-ttu-id="b7278-117">以來自網頁伺服器的 HTTP 要求形式處理訂單流量，必須在應用程式伺服器之間達成平衡。</span><span class="sxs-lookup"><span data-stu-id="b7278-117">Order processing traffic in the form of HTTP requests from the web servers must be balanced among the application servers.</span></span> <span data-ttu-id="b7278-118">此外，基礎結構必須設計為高可用性。</span><span class="sxs-lookup"><span data-stu-id="b7278-118">Additionally, the infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="b7278-119">所產生的設計必須包含下列各項：</span><span class="sxs-lookup"><span data-stu-id="b7278-119">The resulting design must incorporate:</span></span>

* <span data-ttu-id="b7278-120">Azure 訂用帳戶和帳戶</span><span class="sxs-lookup"><span data-stu-id="b7278-120">An Azure subscription and account</span></span>
* <span data-ttu-id="b7278-121">單一資源群組</span><span class="sxs-lookup"><span data-stu-id="b7278-121">A single resource group</span></span>
* <span data-ttu-id="b7278-122">Azure 受控磁碟</span><span class="sxs-lookup"><span data-stu-id="b7278-122">Azure Managed Disks</span></span>
* <span data-ttu-id="b7278-123">具有兩個子網路的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b7278-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="b7278-124">適用於具備類似角色之 VM 的可用性設定組</span><span class="sxs-lookup"><span data-stu-id="b7278-124">Availability sets for the VMs with a similar role</span></span>
* <span data-ttu-id="b7278-125">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b7278-125">Virtual machines</span></span>

<span data-ttu-id="b7278-126">以上各項會遵循下列命名慣例：</span><span class="sxs-lookup"><span data-stu-id="b7278-126">All the above follow these naming conventions:</span></span>

* <span data-ttu-id="b7278-127">Adventure Works Cycles 使用 **[IT workload]-[location]-[Azure resource]** 做為首碼</span><span class="sxs-lookup"><span data-stu-id="b7278-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="b7278-128">針對此範例，"**azos**" (Azure 線上商店) 是 IT 工作負載名稱，而 "**use**" (美國東部 2) 是位置</span><span class="sxs-lookup"><span data-stu-id="b7278-128">For this example, "**azos**" (Azure On-line Store) is the IT workload name and "**use**" (East US 2) is the location</span></span>
* <span data-ttu-id="b7278-129">虛擬網路會使用 AZOS-USE-VN**[number]**</span><span class="sxs-lookup"><span data-stu-id="b7278-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="b7278-130">可用性設定組會使用 azos-use-as-**[role]**</span><span class="sxs-lookup"><span data-stu-id="b7278-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="b7278-131">虛擬機器名稱會使用 azos-use-vm-**[vmname]**</span><span class="sxs-lookup"><span data-stu-id="b7278-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="b7278-132">Azure 訂用帳戶與帳戶</span><span class="sxs-lookup"><span data-stu-id="b7278-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="b7278-133">Adventure Works Cycles 正在使用名稱為 Adventure Works Enterprise Subscription 的企業訂用帳戶，來提供這個 IT 工作負載的計費。</span><span class="sxs-lookup"><span data-stu-id="b7278-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, to provide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="b7278-134">儲存體</span><span class="sxs-lookup"><span data-stu-id="b7278-134">Storage</span></span>
<span data-ttu-id="b7278-135">Adventure Works Cycles 決定他們應該使用 Azure 受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="b7278-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="b7278-136">建立 VM 時，會使用這兩個可用儲存體的儲存層：</span><span class="sxs-lookup"><span data-stu-id="b7278-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="b7278-137">**標準儲存體**，適用於 Web 伺服器、應用程式伺服器，以及網域控制站及其資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="b7278-137">**Standard storage** for the web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="b7278-138">**進階儲存體**，適用於 SQL Server VM 及其資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="b7278-138">**Premium storage** for the SQL Server VMs and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="b7278-139">虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="b7278-139">Virtual network and subnets</span></span>
<span data-ttu-id="b7278-140">由於虛擬網路不需要持續連線到 Adventure Work Cycles 內部部署網路，因此他們決定使用僅限雲端的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b7278-140">Because the virtual network does not need ongoing connectivity to the Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="b7278-141">他們透過 Azure 入口網站，使用下列設定來建立僅限雲端的虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="b7278-141">They created a cloud-only virtual network with the following settings using the Azure portal:</span></span>

* <span data-ttu-id="b7278-142">名稱：AZOS-USE-VN01</span><span class="sxs-lookup"><span data-stu-id="b7278-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="b7278-143">位置：East US 2</span><span class="sxs-lookup"><span data-stu-id="b7278-143">Location: East US 2</span></span>
* <span data-ttu-id="b7278-144">虛擬網路位址空間：10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="b7278-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="b7278-145">第一個子網路：</span><span class="sxs-lookup"><span data-stu-id="b7278-145">First subnet:</span></span>
  * <span data-ttu-id="b7278-146">名稱：FrontEnd</span><span class="sxs-lookup"><span data-stu-id="b7278-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="b7278-147">位址空間：10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="b7278-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="b7278-148">第二個子網路：</span><span class="sxs-lookup"><span data-stu-id="b7278-148">Second subnet:</span></span>
  * <span data-ttu-id="b7278-149">名稱：BackEnd</span><span class="sxs-lookup"><span data-stu-id="b7278-149">Name: BackEnd</span></span>
  * <span data-ttu-id="b7278-150">位址空間：10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="b7278-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="b7278-151">可用性集合</span><span class="sxs-lookup"><span data-stu-id="b7278-151">Availability sets</span></span>
<span data-ttu-id="b7278-152">為了維持這四個線上商店層級的高可用性，Adventure Works Cycles 決定使用四個可用性設定組：</span><span class="sxs-lookup"><span data-stu-id="b7278-152">To maintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="b7278-153">**azos-use-as-web** ，適用於網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="b7278-153">**azos-use-as-web** for the web servers</span></span>
* <span data-ttu-id="b7278-154">**azosuse-as-app** ，適用於應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="b7278-154">**azos-use-as-app** for the application servers</span></span>
* <span data-ttu-id="b7278-155">**azos-use-as-sql** ，適用於 SQL Server</span><span class="sxs-lookup"><span data-stu-id="b7278-155">**azos-use-as-sql** for the SQL Servers</span></span>
* <span data-ttu-id="b7278-156">**azos-use-as-dc** ，適用於網域控制站</span><span class="sxs-lookup"><span data-stu-id="b7278-156">**azos-use-as-dc** for the domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="b7278-157">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b7278-157">Virtual machines</span></span>
<span data-ttu-id="b7278-158">Adventure Works Cycles 決定為其 Azure VM 使用下列名稱：</span><span class="sxs-lookup"><span data-stu-id="b7278-158">Adventure Works Cycles decided on the following names for their Azure VMs:</span></span>

* <span data-ttu-id="b7278-159">**azos-use-vm-web01** ，適用於第一部網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="b7278-159">**azos-use-vm-web01** for the first web server</span></span>
* <span data-ttu-id="b7278-160">**azos-use-vm-web02** ，適用於第二部網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="b7278-160">**azos-use-vm-web02** for the second web server</span></span>
* <span data-ttu-id="b7278-161">**azos-use-vm-app01** ，適用於第一部應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="b7278-161">**azos-use-vm-app01** for the first application server</span></span>
* <span data-ttu-id="b7278-162">**azos-use-vm-app02** ，適用於第二部應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="b7278-162">**azos-use-vm-app02** for the second application server</span></span>
* <span data-ttu-id="b7278-163">**azos-use-vm-sql01** ，適用於叢集中的第一部 SQL Server 伺服器</span><span class="sxs-lookup"><span data-stu-id="b7278-163">**azos-use-vm-sql01** for the first SQL Server server in the cluster</span></span>
* <span data-ttu-id="b7278-164">**azos-use-vm-sql02** ，適用於叢集中的第二部 SQL Server 伺服器</span><span class="sxs-lookup"><span data-stu-id="b7278-164">**azos-use-vm-sql02** for the second SQL Server server in the cluster</span></span>
* <span data-ttu-id="b7278-165">**azos-use-vm-dc01** ，適用於第一個網域控制站</span><span class="sxs-lookup"><span data-stu-id="b7278-165">**azos-use-vm-dc01** for the first domain controller</span></span>
* <span data-ttu-id="b7278-166">**azos-use-vm-dc02** ，適用於第二個網域控制站</span><span class="sxs-lookup"><span data-stu-id="b7278-166">**azos-use-vm-dc02** for the second domain controller</span></span>

<span data-ttu-id="b7278-167">以下是產生的組態。</span><span class="sxs-lookup"><span data-stu-id="b7278-167">Here is the resulting configuration.</span></span>

![在 Azure 中部署的最終應用程式基礎結構](./media/infrastructure-example/example-config.png)

<span data-ttu-id="b7278-169">這個設定包含下列各項：</span><span class="sxs-lookup"><span data-stu-id="b7278-169">This configuration incorporates:</span></span>

* <span data-ttu-id="b7278-170">含有兩個子網路 (前端和後端) 且僅限雲端的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b7278-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="b7278-171">含有標準和進階磁碟的 Azure 受控磁碟</span><span class="sxs-lookup"><span data-stu-id="b7278-171">Azure Managed Disks with both Standard and Premium disks</span></span>
* <span data-ttu-id="b7278-172">四個可用性設定組，每個層級的線上商店都有一組</span><span class="sxs-lookup"><span data-stu-id="b7278-172">Four availability sets, one for each tier of the on-line store</span></span>
* <span data-ttu-id="b7278-173">適用於四個層級的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b7278-173">The virtual machines for the four tiers</span></span>
* <span data-ttu-id="b7278-174">適用於以 HTTPS 為基礎之 Web 流量 (從網際網路到 Web 伺服器) 的外部負載平衡組</span><span class="sxs-lookup"><span data-stu-id="b7278-174">An external load balanced set for HTTPS-based web traffic from the Internet to the web servers</span></span>
* <span data-ttu-id="b7278-175">適用於未加密之 Web 流量 (從 Web 伺服器到應用程式伺服器) 的內部負載平衡組</span><span class="sxs-lookup"><span data-stu-id="b7278-175">An internal load balanced set for unencrypted web traffic from the web servers to the application servers</span></span>
* <span data-ttu-id="b7278-176">單一資源群組</span><span class="sxs-lookup"><span data-stu-id="b7278-176">A single resource group</span></span>