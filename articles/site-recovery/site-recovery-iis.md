---
title: "使用 Azure Site Recovery 複寫多層式 IIS 型 web 應用程式 | Microsoft Docs"
description: "本文說明如何使用 Azure Site Recovery 複寫 IIS web 伺服陣列虛擬機器。"
services: site-recovery
documentationcenter: 
author: nsoneji
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 4ac79df703de00ac009d9845772d8be740e74f29
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="replicate-a-multi-tier-iis-based-web-application-using-azure-site-recovery"></a><span data-ttu-id="21ca5-103">使用 Azure Site Recovery 複寫多層式 IIS 型 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="21ca5-103">Replicate a multi-tier IIS based web application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="21ca5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="21ca5-104">Overview</span></span>


<span data-ttu-id="21ca5-105">應用程式軟體是組織中商務產能的引擎。</span><span class="sxs-lookup"><span data-stu-id="21ca5-105">Application software is the engine of business productivity in an organization.</span></span> <span data-ttu-id="21ca5-106">各種 web 應用程式可在組織提供不同的用途。</span><span class="sxs-lookup"><span data-stu-id="21ca5-106">Various web applications can serve different purposes in an organization.</span></span> <span data-ttu-id="21ca5-107">這些其中一部分，例如處理薪資、財務應用程式和客戶面向的網站可能對組織是最重要的。</span><span class="sxs-lookup"><span data-stu-id="21ca5-107">Some of these like payroll processing, financial applications and customer facing websites can be utmost critical for an organization.</span></span> <span data-ttu-id="21ca5-108">對於組織而言維持隨時運作以避免損失產能很重要，更重要的是避免公司品牌形象的任何損壞。</span><span class="sxs-lookup"><span data-stu-id="21ca5-108">It will be important for the organization to have them up and running at all times to prevent loss of productivity and more importantly prevent any damage to the brand image of the organization.</span></span>

<span data-ttu-id="21ca5-109">重要的 web 應用程式通常會設定為多層式應用程式，在不同層上使用 web、資料庫和應用程式。</span><span class="sxs-lookup"><span data-stu-id="21ca5-109">Critical web applications are typically set up as multi-tier applications with the web, database and application on different tiers.</span></span> <span data-ttu-id="21ca5-110">除了會分散在各層外，應用程式也可在每一層中使用多部伺服器中以負載平衡流量。</span><span class="sxs-lookup"><span data-stu-id="21ca5-110">Apart from being spread across various tiers, the applications may also be using multiple servers in each tier to load balance the traffic.</span></span> <span data-ttu-id="21ca5-111">此外，各層之間和 web 伺服器上的對應可能會根據靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="21ca5-111">Moreover, the mappings between various tiers and on the web server may be based on static IP addresses.</span></span> <span data-ttu-id="21ca5-112">在容錯移轉時，部分對應將需要更新，尤其是如果您在 web 伺服器上設定了多個網站。</span><span class="sxs-lookup"><span data-stu-id="21ca5-112">On failover, some of these mappings will need to be updated, especially, if you have multiple websites configured on the web server.</span></span> <span data-ttu-id="21ca5-113">如果 web 應用程式使用 SSL，則憑證繫結需要更新。</span><span class="sxs-lookup"><span data-stu-id="21ca5-113">In case of web applications using SSL, certificate bindings will need to be updated.</span></span>

<span data-ttu-id="21ca5-114">傳統的非複寫型復原方法牽涉到不同的組態檔、登錄設定、繫結、自訂元件 (COM 或 .NET)、內容和憑證的備份，以及透過一組手動步驟復原檔案。</span><span class="sxs-lookup"><span data-stu-id="21ca5-114">Traditional non-replication based recovery methods involve backing up of various configuration files, registry settings, bindings, custom components (COM or .NET), content and also certificates and recovering the files through a set of manual steps.</span></span> <span data-ttu-id="21ca5-115">這些技術顯然都很麻煩，很容易出錯且不可調整。</span><span class="sxs-lookup"><span data-stu-id="21ca5-115">These techniques are clearly cumbersome, error prone and not scalable.</span></span> <span data-ttu-id="21ca5-116">例如，您很容易忘了備份憑證，且在容錯移轉之後不得不購買伺服器的新憑證。</span><span class="sxs-lookup"><span data-stu-id="21ca5-116">It is, for example, easily possible for you to forget backing up certificates and be left with no choice but to buy new certificates for the server after failover.</span></span>

<span data-ttu-id="21ca5-117">理想的災害復原解決方案應該允許上述複雜應用程式架構的相關復原計劃模型化，並且也能夠新增自訂步驟以處理各層之間的應用程式對應，因此在導致較低 RTO 的災難發生時能提供單鍵擷取方案。</span><span class="sxs-lookup"><span data-stu-id="21ca5-117">A good disaster recovery solution, should allow modeling of recovery plans around the above complex application architectures and also have the ability to add customized steps to handle application mappings between various tiers hence providing a single-click sure shot solution in the event of a disaster leading to a lower RTO.</span></span>


<span data-ttu-id="21ca5-118">本文說明如何使用 [Azure Site Recovery](site-recovery-overview.md)保護 IIS 型 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="21ca5-118">This article describes how to protect an IIS based web application using a [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="21ca5-119">本文將介紹最佳作法來將三層 IIS 型 web 應用程式複寫至 Azure、如何進行災害復原訓練，以及如何將應用程式容錯移轉至 Azure。</span><span class="sxs-lookup"><span data-stu-id="21ca5-119">This article will cover best practices for replicating a three tier IIS based web application to Azure, how you can do a disaster recovery drill, and how you can failover the application to Azure.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="21ca5-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="21ca5-120">Prerequisites</span></span>

<span data-ttu-id="21ca5-121">開始之前，請確定您瞭解下列項目︰</span><span class="sxs-lookup"><span data-stu-id="21ca5-121">Before you start, make sure you understand the following:</span></span>

1. [<span data-ttu-id="21ca5-122">將虛擬機器複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="21ca5-122">Replicating a virtual machine to Azure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="21ca5-123">如何[設計修復網路](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="21ca5-123">How to [design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="21ca5-124">執行測試容錯移轉至 Azure</span><span class="sxs-lookup"><span data-stu-id="21ca5-124">Doing a test failover to Azure</span></span>](./site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="21ca5-125">執行容錯移轉至 Azure</span><span class="sxs-lookup"><span data-stu-id="21ca5-125">Doing a failover to Azure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="21ca5-126">如何[複寫網域控制站](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="21ca5-126">How to [replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="21ca5-127">如何[複寫 SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="21ca5-127">How to [replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="21ca5-128">部署模式</span><span class="sxs-lookup"><span data-stu-id="21ca5-128">Deployment patterns</span></span>
<span data-ttu-id="21ca5-129">IIS 型 web 應用程式通常會遵循下列其中一個部署模式︰</span><span class="sxs-lookup"><span data-stu-id="21ca5-129">An IIS based web application typically follows one of the following deployment patterns:</span></span>

<span data-ttu-id="21ca5-130">**部署模式 1 ** 具有應用程式要求路由 (ARR)、IIS 伺服器與 Microsoft SQL Server 的 IIS 型 web 伺服陣列。</span><span class="sxs-lookup"><span data-stu-id="21ca5-130">**Deployment pattern 1 ** An IIS based web farm  with Application Request Routing(ARR), IIS Server and Microsoft SQL Server.</span></span>

![部署模式](./media/site-recovery-iis/deployment-pattern1.png)

<span data-ttu-id="21ca5-132">**部署模式 2** 具有應用程式要求路由 (ARR)、IIS 伺服器、應用程式伺服器與 Microsoft SQL Server 的 IIS 型 web 伺服陣列。</span><span class="sxs-lookup"><span data-stu-id="21ca5-132">**Deployment pattern 2** An IIS based web farm with Application Request Routing(ARR), IIS Server, Application Server, and Microsoft SQL Server.</span></span>


![部署模式](./media/site-recovery-iis/deployment-pattern2.png)

## <a name="site-recovery-support"></a><span data-ttu-id="21ca5-134">Site Recovery 支援</span><span class="sxs-lookup"><span data-stu-id="21ca5-134">Site Recovery support</span></span>

<span data-ttu-id="21ca5-135">為建立這篇文章，會使用 Windows Server 2012 R2 Enterprise 上的 VMware 虛擬機器與 IIS Server 7.5 版。</span><span class="sxs-lookup"><span data-stu-id="21ca5-135">For the purpose of creating this article VMware virtual machines with IIS Server version 7.5 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="21ca5-136">因為站台復原複寫應用程式無從驗證，此處提供的建議也都必須保留下列案例，以及其他版本的 IIS。</span><span class="sxs-lookup"><span data-stu-id="21ca5-136">As site recovery replication is application agnostic, the recommendations provided here are expected to hold on following scenarios as well and for different version of IIS.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="21ca5-137">來源與目標</span><span class="sxs-lookup"><span data-stu-id="21ca5-137">Source and target</span></span>

<span data-ttu-id="21ca5-138">**案例**</span><span class="sxs-lookup"><span data-stu-id="21ca5-138">**Scenario**</span></span> | <span data-ttu-id="21ca5-139">**至次要網站**</span><span class="sxs-lookup"><span data-stu-id="21ca5-139">**To a secondary site**</span></span> | <span data-ttu-id="21ca5-140">**至 Azure**</span><span class="sxs-lookup"><span data-stu-id="21ca5-140">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="21ca5-141">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="21ca5-141">**Hyper-V**</span></span> | <span data-ttu-id="21ca5-142">是</span><span class="sxs-lookup"><span data-stu-id="21ca5-142">Yes</span></span> | <span data-ttu-id="21ca5-143">是</span><span class="sxs-lookup"><span data-stu-id="21ca5-143">Yes</span></span>
<span data-ttu-id="21ca5-144">**VMware**</span><span class="sxs-lookup"><span data-stu-id="21ca5-144">**VMware**</span></span> | <span data-ttu-id="21ca5-145">是</span><span class="sxs-lookup"><span data-stu-id="21ca5-145">Yes</span></span> | <span data-ttu-id="21ca5-146">是</span><span class="sxs-lookup"><span data-stu-id="21ca5-146">Yes</span></span>
<span data-ttu-id="21ca5-147">**實體伺服器**</span><span class="sxs-lookup"><span data-stu-id="21ca5-147">**Physical server**</span></span> | <span data-ttu-id="21ca5-148">否</span><span class="sxs-lookup"><span data-stu-id="21ca5-148">No</span></span> | <span data-ttu-id="21ca5-149">是</span><span class="sxs-lookup"><span data-stu-id="21ca5-149">Yes</span></span>

## <a name="replicate-virtual-machines"></a><span data-ttu-id="21ca5-150">複寫虛擬機器</span><span class="sxs-lookup"><span data-stu-id="21ca5-150">Replicate virtual machines</span></span>

<span data-ttu-id="21ca5-151">請依照[本指引](site-recovery-vmware-to-azure.md)開始將所有 IIS web 伺服陣列虛擬機器複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="21ca5-151">Follow [this guidance](site-recovery-vmware-to-azure.md) to start replicating all the IIS web farm virtual machines to Azure.</span></span>

<span data-ttu-id="21ca5-152">如果您是使用靜態 IP 位址，請在計算和網路設定中指定您希望虛擬機器在 [**目標 IP** ](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties)設定中採用的 IP。</span><span class="sxs-lookup"><span data-stu-id="21ca5-152">If you are using a static IP then specify the IP that you want the virtual machine to take in the [**Target IP**](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties) setting in Compute and Network settings.</span></span>

![目標 IP](./media/site-recovery-active-directory/dns-target-ip.png)


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="21ca5-154">建立復原計劃</span><span class="sxs-lookup"><span data-stu-id="21ca5-154">Creating a recovery plan</span></span>

<span data-ttu-id="21ca5-155">復原計劃可讓您在多層式應用程式中排序各層的容錯移轉，因此可維護應用程式一致性。</span><span class="sxs-lookup"><span data-stu-id="21ca5-155">A recovery plan allows sequencing the failover of various tiers in a multi-tier application, hence, maintaining application consistency.</span></span> <span data-ttu-id="21ca5-156">建立多層式 web 應用程式的復原計畫時請，遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="21ca5-156">Follow the below steps while creating a recovery plan for a multi-tier web application.</span></span>  <span data-ttu-id="21ca5-157">[深入了解如何建立復原計劃](./site-recovery-create-recovery-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="21ca5-157">[Learn more about creating a recovery plan](./site-recovery-create-recovery-plans.md).</span></span>

### <a name="adding-virtual-machines-to-failover-groups"></a><span data-ttu-id="21ca5-158">將虛擬機器新增至容錯移轉群組</span><span class="sxs-lookup"><span data-stu-id="21ca5-158">Adding virtual machines to failover groups</span></span>
<span data-ttu-id="21ca5-159">一般的多層式 IIS web 應用程式將包含資料庫層與 SQL 虛擬機器，web 層由 IIS 伺服器和應用程式層所構成。</span><span class="sxs-lookup"><span data-stu-id="21ca5-159">A typical multi-tier IIS web application will consist of a database tier with SQL virtual machines, the web tier constituted by a IIS server and an application tier.</span></span> <span data-ttu-id="21ca5-160">根據如下層將所有這些虛擬機器新增至不同的群組。</span><span class="sxs-lookup"><span data-stu-id="21ca5-160">Add all these virtual machines to different group based on tier as below.</span></span> <span data-ttu-id="21ca5-161">[深入了解自訂復原方案](site-recovery-runbook-automation.md#customize-the-recovery-plan)。</span><span class="sxs-lookup"><span data-stu-id="21ca5-161">[Learn more about customising recovery plan](site-recovery-runbook-automation.md#customize-the-recovery-plan).</span></span>

1. <span data-ttu-id="21ca5-162">建立復原計畫。</span><span class="sxs-lookup"><span data-stu-id="21ca5-162">Create a recovery plan.</span></span> <span data-ttu-id="21ca5-163">在群組 1 下新增資料庫層虛擬機器以確保它們都後關閉並先提供。</span><span class="sxs-lookup"><span data-stu-id="21ca5-163">Add the database tier virtual machines under Group 1 to ensure that they are shutdown last and brought up first.</span></span>

1. <span data-ttu-id="21ca5-164">在群組 2 下新增應用程式層虛擬機器，以致於提供資料庫層之後，它們會予以提供。</span><span class="sxs-lookup"><span data-stu-id="21ca5-164">Add the application tier virtual machines under Group 2 such that they are brought up after the database tier has been brought up.</span></span>

1. <span data-ttu-id="21ca5-165">在群組 3 中新增 web 層虛擬機器，以致於提供應用程式層之後，它們會予以提供。</span><span class="sxs-lookup"><span data-stu-id="21ca5-165">Add the web tier virtual machines in Group 3 such that they are brought up after the application tier has been brought up.</span></span>

1. <span data-ttu-id="21ca5-166">在群組 4 中新增虛擬機器負載平衡，以致於提供 web 層之後，它們會予以提供。</span><span class="sxs-lookup"><span data-stu-id="21ca5-166">Add load balance virtual machines in Group 4 such that they are brought up after the web tier has been brought up.</span></span>


### <a name="adding-scripts-to-the-recovery-plan"></a><span data-ttu-id="21ca5-167">將指令碼新增至復原計畫</span><span class="sxs-lookup"><span data-stu-id="21ca5-167">Adding scripts to the recovery plan</span></span>
<span data-ttu-id="21ca5-168">您可能需要在容錯移轉/測試容錯移轉後於 Azure 虛擬機器上執行某些作業以讓 IIS web 伺服陣列正確運作。</span><span class="sxs-lookup"><span data-stu-id="21ca5-168">You may need to do some operations on the Azure virtual machines post failover/Test failover to make IIS web farm function correctly.</span></span> <span data-ttu-id="21ca5-169">您可以自動化後置容錯移轉作業，例如更新 DNS 項目、變更網站繫結、在如下所示的復原方案中新增對應指令碼在連接字串中進行變更。</span><span class="sxs-lookup"><span data-stu-id="21ca5-169">You can automate the post failover operation like updating DNS entry, changing site binding, change  in connection string  by adding corresponding scripts in the recovery plan as below.</span></span> <span data-ttu-id="21ca5-170">[深入了解新增指令碼復原計劃](./site-recovery-create-recovery-plans.md#add-scripts)。</span><span class="sxs-lookup"><span data-stu-id="21ca5-170">[Learn more about add script recovery plan](./site-recovery-create-recovery-plans.md#add-scripts).</span></span>

#### <a name="dns-update"></a><span data-ttu-id="21ca5-171">DNS 更新</span><span class="sxs-lookup"><span data-stu-id="21ca5-171">DNS Update</span></span>
<span data-ttu-id="21ca5-172">如果已設定動態 DNS 更新的 DNS，則虛擬機器通常會在啟動之後使用新的 IP 更新 DNS。</span><span class="sxs-lookup"><span data-stu-id="21ca5-172">If the DNS is configured for dynamic DNS update then virtual machines usually update the DNS with the new IP once they start.</span></span> <span data-ttu-id="21ca5-173">如果您想要使用虛擬機器的新 IP 新增更新 DNS 的明確步驟，則請新增此[指令碼來更新 DNS 中的 IP](https://aka.ms/asr-dns-update) 做為復原方案群組上的後置動作。</span><span class="sxs-lookup"><span data-stu-id="21ca5-173">If you want to add an explicit step to update DNS with the new IPs of the virtual machines then add this [script to update IP in DNS](https://aka.ms/asr-dns-update) as a post action on recovery plan groups.</span></span>  

#### <a name="connection-string-in-an-applications-webconfig"></a><span data-ttu-id="21ca5-174">在應用程式 web.config 中的連接字串</span><span class="sxs-lookup"><span data-stu-id="21ca5-174">Connection string in an application’s web.config</span></span>
<span data-ttu-id="21ca5-175">連接字串會指定與網站進行通訊的資料庫。</span><span class="sxs-lookup"><span data-stu-id="21ca5-175">The connection string specifies the database that the web site communicates with.</span></span>

<span data-ttu-id="21ca5-176">如果連接字串執行資料庫虛擬機器的名稱，則容錯移轉後無需進一步的步驟，應用程式都能夠自動對 DB 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="21ca5-176">If the connection string carries the name of the database virtual machine, no further steps will be needed post failover and the application will be able to automatically communicate to the DB.</span></span> <span data-ttu-id="21ca5-177">此外，如果保留資料庫虛擬機器的 IP 位址，則它不需要更新連接字串。</span><span class="sxs-lookup"><span data-stu-id="21ca5-177">Also, if the IP address for the database virtual machine is retained, it will not be needed to update the connection string.</span></span> <span data-ttu-id="21ca5-178">如果連接字串是使用 IP 位址指資料庫虛擬機器，它必須在容錯移轉後更新。</span><span class="sxs-lookup"><span data-stu-id="21ca5-178">If the connection string refers to the database virtual machine using an IP address, it will need to be updated post failover.</span></span> <span data-ttu-id="21ca5-179">例如</span><span class="sxs-lookup"><span data-stu-id="21ca5-179">E.g.</span></span> <span data-ttu-id="21ca5-180">下列連接字串指向 DB，IP 為 127.0.1.2</span><span class="sxs-lookup"><span data-stu-id="21ca5-180">the below connection string points to the DB with IP 127.0.1.2</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <configuration>
        <connectionStrings>
        <add name="ConnStringDb1" connectionString="Data Source= 127.0.1.2\SqlExpress; Initial Catalog=TestDB1;Integrated Security=False;" />
        </connectionStrings>
        </configuration>

<span data-ttu-id="21ca5-181">您可以更新 web 層中的連接字串，方法為在復原計劃中的群組 3 之後新增 [IIS 連線更新指令碼](https://aka.ms/asr-update-webtier-script-classic)。</span><span class="sxs-lookup"><span data-stu-id="21ca5-181">You can update the connection string in web tier by adding [IIS connection update script](https://aka.ms/asr-update-webtier-script-classic) after Group 3 in the recovery plan.</span></span>

#### <a name="site-bindings-for-the-application"></a><span data-ttu-id="21ca5-182">應用程式的網站繫結</span><span class="sxs-lookup"><span data-stu-id="21ca5-182">Site bindings for the application</span></span>
<span data-ttu-id="21ca5-183">每個網站所包含的繫結資訊包括繫結的類型、IIS 伺服器接聽要求之網站的 IP 位址、連接埠號碼和網站的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="21ca5-183">Every site consists of binding information that includes the type of binding, the IP address at which the IIS server listens to the requests for the site, the port number and the host names for the site.</span></span> <span data-ttu-id="21ca5-184">在容錯移轉期間，如果與這些繫結相關聯的 IP 位址中有變更時，可能需要更新這些繫結。</span><span class="sxs-lookup"><span data-stu-id="21ca5-184">At the time of a failover, these bindings might need to be updated if there is a change in the IP address associated with them.</span></span>

> [!NOTE]
>
> <span data-ttu-id="21ca5-185">如果您已對網站繫結標記「全部未指派」，如下列範例所示，您將不需要在容錯移轉後更新此繫結。</span><span class="sxs-lookup"><span data-stu-id="21ca5-185">If you have marked ‘all unassigned’ for the site binding as in the example below, you will not need to update this binding post failover.</span></span> <span data-ttu-id="21ca5-186">此外，如果與網站相關聯的 IP 位址在容錯移轉後未變更，則網站繫結不需要更新 (IP 位址保留取決於指派至主要和復原網站的網路架構和子網路，因此對您的組織可能可行或可能不可行。)</span><span class="sxs-lookup"><span data-stu-id="21ca5-186">Also, if the IP address associated with a site is not changed post failover, the site binding need not be updated (Retention of the IP address depends on the network architecture and subnets assigned to the primary and recovery sites and hence may or may not be feasible for your organization.)</span></span>

![SSL 繫結](./media/site-recovery-iis/sslbinding.png)

<span data-ttu-id="21ca5-188">如果您已將 IP 位址與網站相關聯，必須使用新的 IP 位址更新所有網站繫結。</span><span class="sxs-lookup"><span data-stu-id="21ca5-188">If you have associated the IP address with a site, you will need to update all site bindings with the new IP address.</span></span> <span data-ttu-id="21ca5-189">您可以在復原計劃中的群組 3 之後新增 [IIS Web 層更新指令碼](https://aka.ms/asr-web-tier-update-runbook-classic)以變更網站繫結。</span><span class="sxs-lookup"><span data-stu-id="21ca5-189">You can add [IIS Web tier update script](https://aka.ms/asr-web-tier-update-runbook-classic) after Group 3 in recovery plan to change the site bindings.</span></span>


#### <a name="update-load-balancer-ip-address"></a><span data-ttu-id="21ca5-190">更新負載平衡器 IP 位址</span><span class="sxs-lookup"><span data-stu-id="21ca5-190">Update load balancer IP address</span></span>
<span data-ttu-id="21ca5-191">如果您有應用程式要求路由虛擬機器，請在群組 4 之後新增 [IIS ARR 容錯移轉指令碼](https://aka.ms/asr-iis-arrtier-failover-script-classic)以更新 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="21ca5-191">If you have  Application Request Routing virtual machine, add [IIS ARR  failover script](https://aka.ms/asr-iis-arrtier-failover-script-classic) after Group 4 to update the IP address.</span></span>

#### <a name="the-ssl-cert-binding-for-an-https-connection"></a><span data-ttu-id="21ca5-192">Https 連線的 SSL 憑證繫結</span><span class="sxs-lookup"><span data-stu-id="21ca5-192">The SSL cert binding for an https connection</span></span>
<span data-ttu-id="21ca5-193">網站可擁有相關聯的 SSL 憑證，以協助確保 web 伺服器與使用者瀏覽器之間的安全通訊。</span><span class="sxs-lookup"><span data-stu-id="21ca5-193">Websites can have an associated SSL certificate that helps in ensuring a secure communication between the webserver and the user’s browser.</span></span> <span data-ttu-id="21ca5-194">如果網站具有 https 連線，且相關聯的 https 網站使用 SSL 憑證繫結繫結至 IIS 伺服器的 IP 位址，必須使用容錯移轉後的 IIS 虛擬機器之 IP 為憑證新增新的網站繫結。</span><span class="sxs-lookup"><span data-stu-id="21ca5-194">If the website has an https connection and an associated https site binding to the IP address of the IIS server with an SSL cert binding, a new site binding will need to be added for the cert with the IP of the IIS virtual machine post failover.</span></span>

<span data-ttu-id="21ca5-195">可以發出 SSL 憑證，針對-</span><span class="sxs-lookup"><span data-stu-id="21ca5-195">The SSL cert can be issued against-</span></span>

<span data-ttu-id="21ca5-196">a) 網站的完整網域名稱</span><span class="sxs-lookup"><span data-stu-id="21ca5-196">a) The fully qualified domain name of the website</span></span><br>
<span data-ttu-id="21ca5-197">b) 伺服器的名稱</span><span class="sxs-lookup"><span data-stu-id="21ca5-197">b) The name of the server</span></span><br>
<span data-ttu-id="21ca5-198">c) 網域名稱的萬用字元憑證</span><span class="sxs-lookup"><span data-stu-id="21ca5-198">c) A wildcard certificate for the domain name</span></span><br>
<span data-ttu-id="21ca5-199">d) IP 位址 – 如果針對 IIS 伺服器的 IP 發行 SSL 憑證，需要對 Azure 網站上 IIS 伺服器的 IP 位址發出另一個 SSL 憑證，且必須建立此憑證的額外 SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="21ca5-199">d) An IP address – If the SSL cert is issued against the IP of the IIS server, another SSL cert needs to be issued against the IP address of the IIS server on the Azure site and an additional SSL binding for this certificate will need to be created.</span></span> <span data-ttu-id="21ca5-200">因此，建議您不要使用對 IP 發出的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="21ca5-200">Hence, it is advisable to not use an SSL cert issued against IP.</span></span> <span data-ttu-id="21ca5-201">這是較不常用的選項，而且很快就會根據新的 CA/瀏覽器論壇變更而取代。</span><span class="sxs-lookup"><span data-stu-id="21ca5-201">This is a less widely used option and will soon be deprecated as per new CA/browser forum changes.</span></span>

#### <a name="update-the-dependency-between-the-web-and-the-application-tier"></a><span data-ttu-id="21ca5-202">更新 web 和應用程式層之間的相依性</span><span class="sxs-lookup"><span data-stu-id="21ca5-202">Update the dependency between the web and the application tier</span></span>
<span data-ttu-id="21ca5-203">如果您根據虛擬機器的 IP 位址有特定相依性的應用程式，則需要在容錯移轉後更新此相依性。</span><span class="sxs-lookup"><span data-stu-id="21ca5-203">If you have an application specific dependency based on the IP address of the virtual machines, you need to update this dependency post failover.</span></span>

## <a name="doing-a-test-failover"></a><span data-ttu-id="21ca5-204">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="21ca5-204">Doing a test failover</span></span>
<span data-ttu-id="21ca5-205">請依照[本指引](site-recovery-test-failover-to-azure.md)來執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="21ca5-205">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

1.  <span data-ttu-id="21ca5-206">請移至 Azure 入口網站，然後選取您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="21ca5-206">Go to Azure portal and select your Recovery Service vault.</span></span>
1.  <span data-ttu-id="21ca5-207">按一下為 IIS web 伺服器陣列建立的復原計劃。</span><span class="sxs-lookup"><span data-stu-id="21ca5-207">Click on the recovery plan created for IIS web farm.</span></span>
1.  <span data-ttu-id="21ca5-208">按一下 [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="21ca5-208">Click on 'Test Failover'.</span></span>
1.  <span data-ttu-id="21ca5-209">選取復原點和 Azure 虛擬網路來開始測試容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="21ca5-209">Select recovery point and Azure virtual network to start the test failover process.</span></span>
1.  <span data-ttu-id="21ca5-210">次要環境啟動後，您就可以執行您的驗證。</span><span class="sxs-lookup"><span data-stu-id="21ca5-210">Once the secondary environment is up, you can perform your validations.</span></span>
1.  <span data-ttu-id="21ca5-211">驗證完成後，您可以選取 [完成驗證]，並會清除測試容錯移轉環境。</span><span class="sxs-lookup"><span data-stu-id="21ca5-211">Once the validations are complete, you can select ‘Validations complete’ and the test failover environment will be cleaned.</span></span>

## <a name="doing-a-failover"></a><span data-ttu-id="21ca5-212">執行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="21ca5-212">Doing a failover</span></span>
<span data-ttu-id="21ca5-213">當您在進行容錯移轉時，請依照[本指引](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="21ca5-213">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

1.  <span data-ttu-id="21ca5-214">請移至 Azure 入口網站，然後選取您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="21ca5-214">Go to Azure portal and select your Recovery Service vault.</span></span>
1.  <span data-ttu-id="21ca5-215">按一下為 IIS web 伺服器陣列建立的復原計劃。</span><span class="sxs-lookup"><span data-stu-id="21ca5-215">Click on the recovery plan created for IIS web farm.</span></span>
1.  <span data-ttu-id="21ca5-216">按一下 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="21ca5-216">Click on 'Failover'.</span></span>
1.  <span data-ttu-id="21ca5-217">選取復原點以啟動容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="21ca5-217">Select recovery point to start the failover process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21ca5-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21ca5-218">Next steps</span></span>
<span data-ttu-id="21ca5-219">您可以使用站台復原深入了解[複寫其他應用程式](site-recovery-workload.md)。</span><span class="sxs-lookup"><span data-stu-id="21ca5-219">You can learn more about [replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
