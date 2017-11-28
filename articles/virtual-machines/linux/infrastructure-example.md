---
title: "aaaExample Azure 基礎結構的逐步解說 |Microsoft 文件"
description: "深入了解 hello 金鑰設計和實作部署的指導方針在 Azure 中的範例基礎結構。"
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 281fc2c0-b533-45fa-81a3-728c0049c73d
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6b307c0112203aa83e1fada81966fc265397a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a><span data-ttu-id="9e619-103">適用於 Linux VM 的範例 Azure 基礎結構逐步解說</span><span class="sxs-lookup"><span data-stu-id="9e619-103">Example Azure infrastructure walkthrough for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="9e619-104">本文將逐步解說建置範例應用程式基礎結構的方法。</span><span class="sxs-lookup"><span data-stu-id="9e619-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="9e619-105">我們將詳細說明設計簡單的線上存放區的結合所有 hello 指導方針和命名慣例、 可用性設定組中，虛擬網路和負載平衡器、 周圍的決策基礎結構與實際部署您的虛擬機器 (Vm)。</span><span class="sxs-lookup"><span data-stu-id="9e619-105">We detail designing an infrastructure for a simple on-line store that brings together all hello guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="9e619-106">範例工作負載</span><span class="sxs-lookup"><span data-stu-id="9e619-106">Example workload</span></span>
<span data-ttu-id="9e619-107">Adventure Works Cycles 想 toobuild 線上存放區中的應用程式所組成的 Azure:</span><span class="sxs-lookup"><span data-stu-id="9e619-107">Adventure Works Cycles wants toobuild an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="9e619-108">執行用戶端 hello 前端 web 層中的兩個 nginx 伺服器</span><span class="sxs-lookup"><span data-stu-id="9e619-108">Two nginx servers running hello client front-end in a web tier</span></span>
* <span data-ttu-id="9e619-109">兩個在應用程式層級中處理資料和訂單的 nginx 伺服器</span><span class="sxs-lookup"><span data-stu-id="9e619-109">Two nginx servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="9e619-110">兩個做為在資料庫層級中儲存產品資料及訂單的共用叢集一部分的 MongoDB 伺服器</span><span class="sxs-lookup"><span data-stu-id="9e619-110">Two MongoDB servers part of a sharded cluster for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="9e619-111">兩個在驗證層級中針對客戶帳戶及供應商的 Active Directory 網域控制站</span><span class="sxs-lookup"><span data-stu-id="9e619-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="9e619-112">所有的 hello 伺服器位於兩個子網路：</span><span class="sxs-lookup"><span data-stu-id="9e619-112">All hello servers are located in two subnets:</span></span>
  * <span data-ttu-id="9e619-113">hello web 伺服器前端的子網路</span><span class="sxs-lookup"><span data-stu-id="9e619-113">a front-end subnet for hello web servers</span></span> 
  * <span data-ttu-id="9e619-114">後端子 hello 應用程式伺服器、 MongoDB 叢集和網域控制站</span><span class="sxs-lookup"><span data-stu-id="9e619-114">a back-end subnet for hello application servers, MongoDB cluster, and domain controllers</span></span>

![不同應用程式基礎結構層級的圖表](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="9e619-116">安全的連入網路流量必須在 hello web 伺服器之間進行負載平衡與客戶瀏覽 hello 線上存放區。</span><span class="sxs-lookup"><span data-stu-id="9e619-116">Incoming secure web traffic must be load-balanced among hello web servers as customers browse hello on-line store.</span></span> <span data-ttu-id="9e619-117">從伺服器必須是負載平衡 hello 應用程式伺服器之間的 hello web 要求訂單處理 hello 表單送出的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="9e619-117">Order processing traffic in hello form of HTTP requests from hello web servers must be load-balanced among hello application servers.</span></span> <span data-ttu-id="9e619-118">此外，您必須針對高可用性設計 hello 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="9e619-118">Additionally, hello infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="9e619-119">必須納入 hello 產生設計：</span><span class="sxs-lookup"><span data-stu-id="9e619-119">hello resulting design must incorporate:</span></span>

* <span data-ttu-id="9e619-120">Azure 訂用帳戶和帳戶</span><span class="sxs-lookup"><span data-stu-id="9e619-120">An Azure subscription and account</span></span>
* <span data-ttu-id="9e619-121">單一資源群組</span><span class="sxs-lookup"><span data-stu-id="9e619-121">A single resource group</span></span>
* <span data-ttu-id="9e619-122">Azure 受控磁碟</span><span class="sxs-lookup"><span data-stu-id="9e619-122">Azure Managed Disks</span></span>
* <span data-ttu-id="9e619-123">具有兩個子網路的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="9e619-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="9e619-124">Hello Vm 與角色類似的可用性設定組</span><span class="sxs-lookup"><span data-stu-id="9e619-124">Availability sets for hello VMs with a similar role</span></span>
* <span data-ttu-id="9e619-125">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9e619-125">Virtual machines</span></span>

<span data-ttu-id="9e619-126">上述所有 hello，請都遵循下列命名慣例：</span><span class="sxs-lookup"><span data-stu-id="9e619-126">All hello above follow these naming conventions:</span></span>

* <span data-ttu-id="9e619-127">Adventure Works Cycles 使用 **[IT workload]-[location]-[Azure resource]** 做為首碼</span><span class="sxs-lookup"><span data-stu-id="9e619-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="9e619-128">例如，"**azos**"（Azure 線上存放區） 是 hello IT 工作負載名稱和"**使用**"（美國東部 2） 是 hello 位置</span><span class="sxs-lookup"><span data-stu-id="9e619-128">For this example, "**azos**" (Azure On-line Store) is hello IT workload name and "**use**" (East US 2) is hello location</span></span>
* <span data-ttu-id="9e619-129">虛擬網路會使用 AZOS-USE-VN**[number]**</span><span class="sxs-lookup"><span data-stu-id="9e619-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="9e619-130">可用性設定組會使用 azos-use-as-**[role]**</span><span class="sxs-lookup"><span data-stu-id="9e619-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="9e619-131">虛擬機器名稱會使用 azos-use-vm-**[vmname]**</span><span class="sxs-lookup"><span data-stu-id="9e619-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="9e619-132">Azure 訂用帳戶與帳戶</span><span class="sxs-lookup"><span data-stu-id="9e619-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="9e619-133">Adventure Works Cycles 使用其企業訂用帳戶，名為 Adventure Works 企業訂用帳戶，tooprovide 計費這樣的 IT 工作負載。</span><span class="sxs-lookup"><span data-stu-id="9e619-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, tooprovide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="9e619-134">儲存體</span><span class="sxs-lookup"><span data-stu-id="9e619-134">Storage</span></span>
<span data-ttu-id="9e619-135">Adventure Works Cycles 決定他們應該使用 Azure 受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="9e619-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="9e619-136">建立 VM 時，會使用這兩個可用儲存體的儲存層：</span><span class="sxs-lookup"><span data-stu-id="9e619-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="9e619-137">**標準儲存體**hello 網頁伺服器、 應用程式伺服器和網域控制站和其資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="9e619-137">**Standard storage** for hello web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="9e619-138">**高階儲存體**hello MongoDB 分區化的叢集伺服器和其資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="9e619-138">**Premium storage** for hello MongoDB sharded cluster servers and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="9e619-139">虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="9e619-139">Virtual network and subnets</span></span>
<span data-ttu-id="9e619-140">Hello 虛擬網路不需要持續連線 toohello Adventure 工作週期在內部部署網路，因為它們會決定在僅限雲端的虛擬網路上。</span><span class="sxs-lookup"><span data-stu-id="9e619-140">Because hello virtual network does not need ongoing connectivity toohello Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="9e619-141">它們可以建立僅限雲端的虛擬網路以下列設定使用 hello Azure 入口網站的 hello:</span><span class="sxs-lookup"><span data-stu-id="9e619-141">They created a cloud-only virtual network with hello following settings using hello Azure portal:</span></span>

* <span data-ttu-id="9e619-142">名稱：AZOS-USE-VN01</span><span class="sxs-lookup"><span data-stu-id="9e619-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="9e619-143">位置：East US 2</span><span class="sxs-lookup"><span data-stu-id="9e619-143">Location: East US 2</span></span>
* <span data-ttu-id="9e619-144">虛擬網路位址空間：10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="9e619-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="9e619-145">第一個子網路：</span><span class="sxs-lookup"><span data-stu-id="9e619-145">First subnet:</span></span>
  * <span data-ttu-id="9e619-146">名稱：FrontEnd</span><span class="sxs-lookup"><span data-stu-id="9e619-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="9e619-147">位址空間：10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="9e619-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="9e619-148">第二個子網路：</span><span class="sxs-lookup"><span data-stu-id="9e619-148">Second subnet:</span></span>
  * <span data-ttu-id="9e619-149">名稱：BackEnd</span><span class="sxs-lookup"><span data-stu-id="9e619-149">Name: BackEnd</span></span>
  * <span data-ttu-id="9e619-150">位址空間：10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="9e619-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="9e619-151">可用性集合</span><span class="sxs-lookup"><span data-stu-id="9e619-151">Availability sets</span></span>
<span data-ttu-id="9e619-152">所有的四個層，其線上存放區決定上四個可用性設定組的 Adventure Works Cycles 的 toomaintain 高可用性：</span><span class="sxs-lookup"><span data-stu-id="9e619-152">toomaintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="9e619-153">**azos-使用-做為 web** hello 網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="9e619-153">**azos-use-as-web** for hello web servers</span></span>
* <span data-ttu-id="9e619-154">**azos 使用-做為應用程式**hello 應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="9e619-154">**azos-use-as-app** for hello application servers</span></span>
* <span data-ttu-id="9e619-155">**azos-使用-為-db** hello 叢集中的伺服器 hello MongoDB 分區化</span><span class="sxs-lookup"><span data-stu-id="9e619-155">**azos-use-as-db** for hello servers in hello MongoDB sharded cluster</span></span>
* <span data-ttu-id="9e619-156">**azos-使用-做為 dc** hello 網域控制站</span><span class="sxs-lookup"><span data-stu-id="9e619-156">**azos-use-as-dc** for hello domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="9e619-157">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9e619-157">Virtual machines</span></span>
<span data-ttu-id="9e619-158">Adventure Works Cycles 決定 hello 下列其 Azure Vm 的名稱：</span><span class="sxs-lookup"><span data-stu-id="9e619-158">Adventure Works Cycles decided on hello following names for their Azure VMs:</span></span>

* <span data-ttu-id="9e619-159">**azos 使用 vm-web01** hello 第一個網頁伺服器</span><span class="sxs-lookup"><span data-stu-id="9e619-159">**azos-use-vm-web01** for hello first web server</span></span>
* <span data-ttu-id="9e619-160">**azos 使用 vm-web02** hello 第二部 web 伺服器</span><span class="sxs-lookup"><span data-stu-id="9e619-160">**azos-use-vm-web02** for hello second web server</span></span>
* <span data-ttu-id="9e619-161">**azos 使用 vm-app01** hello 第一個應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="9e619-161">**azos-use-vm-app01** for hello first application server</span></span>
* <span data-ttu-id="9e619-162">**azos 使用 vm-app02** hello 第二個應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="9e619-162">**azos-use-vm-app02** for hello second application server</span></span>
* <span data-ttu-id="9e619-163">**azos 使用 vm-db01** hello 第一台 hello 叢集中的 MongoDB 伺服器</span><span class="sxs-lookup"><span data-stu-id="9e619-163">**azos-use-vm-db01** for hello first MongoDB server in hello cluster</span></span>
* <span data-ttu-id="9e619-164">**azos 使用 vm-db02** hello 第二部 MongoDB 伺服器 hello 叢集中</span><span class="sxs-lookup"><span data-stu-id="9e619-164">**azos-use-vm-db02** for hello second MongoDB server in hello cluster</span></span>
* <span data-ttu-id="9e619-165">**azos 使用 vm-dc01** hello 第一個網域控制站</span><span class="sxs-lookup"><span data-stu-id="9e619-165">**azos-use-vm-dc01** for hello first domain controller</span></span>
* <span data-ttu-id="9e619-166">**azos 使用 vm-dc02** hello 第二個網域控制站</span><span class="sxs-lookup"><span data-stu-id="9e619-166">**azos-use-vm-dc02** for hello second domain controller</span></span>

<span data-ttu-id="9e619-167">以下是 hello 產生的設定。</span><span class="sxs-lookup"><span data-stu-id="9e619-167">Here is hello resulting configuration.</span></span>

![在 Azure 中部署的最終應用程式基礎結構](./media/infrastructure-example/example-config.png)

<span data-ttu-id="9e619-169">這個設定包含下列各項：</span><span class="sxs-lookup"><span data-stu-id="9e619-169">This configuration incorporates:</span></span>

* <span data-ttu-id="9e619-170">含有兩個子網路 (前端和後端) 且僅限雲端的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="9e619-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="9e619-171">使用標準和進階磁碟的 Azure 受控磁碟</span><span class="sxs-lookup"><span data-stu-id="9e619-171">Azure Managed Disks using both Standard and Premium disks</span></span>
* <span data-ttu-id="9e619-172">四個可用性設定組，一個用於 hello 線上存放區的每一層</span><span class="sxs-lookup"><span data-stu-id="9e619-172">Four availability sets, one for each tier of hello on-line store</span></span>
* <span data-ttu-id="9e619-173">hello hello 四層的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9e619-173">hello virtual machines for hello four tiers</span></span>
* <span data-ttu-id="9e619-174">從 hello 網際網路 toohello 的 web 伺服器的 HTTPS 為基礎的 web 流量的外部負載平衡集</span><span class="sxs-lookup"><span data-stu-id="9e619-174">An external load balanced set for HTTPS-based web traffic from hello Internet toohello web servers</span></span>
* <span data-ttu-id="9e619-175">內部負載平衡集從 hello web 伺服器 toohello 應用程式伺服器的加密的 web 流量</span><span class="sxs-lookup"><span data-stu-id="9e619-175">An internal load balanced set for unencrypted web traffic from hello web servers toohello application servers</span></span>
* <span data-ttu-id="9e619-176">單一資源群組</span><span class="sxs-lookup"><span data-stu-id="9e619-176">A single resource group</span></span>
