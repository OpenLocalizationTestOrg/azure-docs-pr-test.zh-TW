---
title: "aaaReplicate 多層式 IIS 型 web 應用程式使用 Azure Site Recovery |Microsoft 文件"
description: "本文說明如何 tooreplicate IIS web 伺服陣列使用 Azure Site Recovery 的虛擬機器。"
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
ms.openlocfilehash: 1974265b3cb05f6dc57049876306d2e08424bb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-iis-based-web-application-using-azure-site-recovery"></a><span data-ttu-id="f30e5-103">使用 Azure Site Recovery 複寫多層式 IIS 型 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="f30e5-103">Replicate a multi-tier IIS based web application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="f30e5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="f30e5-104">Overview</span></span>


<span data-ttu-id="f30e5-105">應用程式軟體是在組織中的商務產能的 hello 引擎。</span><span class="sxs-lookup"><span data-stu-id="f30e5-105">Application software is hello engine of business productivity in an organization.</span></span> <span data-ttu-id="f30e5-106">各種 web 應用程式可在組織提供不同的用途。</span><span class="sxs-lookup"><span data-stu-id="f30e5-106">Various web applications can serve different purposes in an organization.</span></span> <span data-ttu-id="f30e5-107">這些其中一部分，例如處理薪資、財務應用程式和客戶面向的網站可能對組織是最重要的。</span><span class="sxs-lookup"><span data-stu-id="f30e5-107">Some of these like payroll processing, financial applications and customer facing websites can be utmost critical for an organization.</span></span> <span data-ttu-id="f30e5-108">它對於 hello 組織 toohave 向上以及在任何時候 tooprevent 降低產能執行重要而且更重要的是防止 hello 組織的任何損害 toohello 品牌映像。</span><span class="sxs-lookup"><span data-stu-id="f30e5-108">It will be important for hello organization toohave them up and running at all times tooprevent loss of productivity and more importantly prevent any damage toohello brand image of hello organization.</span></span>

<span data-ttu-id="f30e5-109">重要的 web 應用程式通常是做為 hello web、 資料庫與應用程式在不同的層上的多層式應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="f30e5-109">Critical web applications are typically set up as multi-tier applications with hello web, database and application on different tiers.</span></span> <span data-ttu-id="f30e5-110">除了會分散在各層，hello 應用程式也可以使用多部伺服器中每個層 tooload hello 流量平衡。</span><span class="sxs-lookup"><span data-stu-id="f30e5-110">Apart from being spread across various tiers, hello applications may also be using multiple servers in each tier tooload balance hello traffic.</span></span> <span data-ttu-id="f30e5-111">此外，hello hello 網頁伺服器與各層之間的對應可能會根據靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f30e5-111">Moreover, hello mappings between various tiers and on hello web server may be based on static IP addresses.</span></span> <span data-ttu-id="f30e5-112">在容錯移轉時，部分對應必須 toobe 更新，特別是，當您擁有 hello web 伺服器上設定的多個網站。</span><span class="sxs-lookup"><span data-stu-id="f30e5-112">On failover, some of these mappings will need toobe updated, especially, if you have multiple websites configured on hello web server.</span></span> <span data-ttu-id="f30e5-113">如果使用 SSL 的 web 應用程式，需要 toobe 更新憑證繫結。</span><span class="sxs-lookup"><span data-stu-id="f30e5-113">In case of web applications using SSL, certificate bindings will need toobe updated.</span></span>

<span data-ttu-id="f30e5-114">傳統的非複寫根據的修復方法牽涉到不同的設定檔、 登錄設定、 繫結、 自訂元件 （COM 或.NET）、 內容和也憑證和復原 hello 檔案透過手動步驟一組的備份。</span><span class="sxs-lookup"><span data-stu-id="f30e5-114">Traditional non-replication based recovery methods involve backing up of various configuration files, registry settings, bindings, custom components (COM or .NET), content and also certificates and recovering hello files through a set of manual steps.</span></span> <span data-ttu-id="f30e5-115">這些技術顯然都很麻煩，很容易出錯且不可調整。</span><span class="sxs-lookup"><span data-stu-id="f30e5-115">These techniques are clearly cumbersome, error prone and not scalable.</span></span> <span data-ttu-id="f30e5-116">它是，例如，輕鬆地讓您 tooforget 備份憑證而且沒有選項但 toobuy hello 伺服器的新憑證在容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="f30e5-116">It is, for example, easily possible for you tooforget backing up certificates and be left with no choice but toobuy new certificates for hello server after failover.</span></span>

<span data-ttu-id="f30e5-117">理想的災害復原解決方案，應該上方複雜的應用程式架構允許 hello 周圍的復原方案的模型，而且也具有 hello 能力 tooadd 自訂步驟 toohandle 應用程式之間的對應因此提供的各層單鍵確定 hello 開頭 tooa 災害事件中擷取畫面方案降低 RTO。</span><span class="sxs-lookup"><span data-stu-id="f30e5-117">A good disaster recovery solution, should allow modeling of recovery plans around hello above complex application architectures and also have hello ability tooadd customized steps toohandle application mappings between various tiers hence providing a single-click sure shot solution in hello event of a disaster leading tooa lower RTO.</span></span>


<span data-ttu-id="f30e5-118">本文說明如何 tooprotect IIS 型 web 應用程式使用[Azure Site Recovery](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f30e5-118">This article describes how tooprotect an IIS based web application using a [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="f30e5-119">IIS 型 web 應用程式 tooAzure、 告訴您如何進行災害復原訓練，和如何容錯移轉 hello 應用程式 tooAzure，本文將討論複寫三層的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="f30e5-119">This article will cover best practices for replicating a three tier IIS based web application tooAzure, how you can do a disaster recovery drill, and how you can failover hello application tooAzure.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f30e5-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="f30e5-120">Prerequisites</span></span>

<span data-ttu-id="f30e5-121">開始之前，請確定您了解 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f30e5-121">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="f30e5-122">複寫虛擬機器 tooAzure</span><span class="sxs-lookup"><span data-stu-id="f30e5-122">Replicating a virtual machine tooAzure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="f30e5-123">如何太[設計與復原網路](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="f30e5-123">How too[design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="f30e5-124">執行測試容錯移轉 tooAzure</span><span class="sxs-lookup"><span data-stu-id="f30e5-124">Doing a test failover tooAzure</span></span>](./site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="f30e5-125">執行容錯移轉 tooAzure</span><span class="sxs-lookup"><span data-stu-id="f30e5-125">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="f30e5-126">如何太[複寫的網域控制站](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="f30e5-126">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="f30e5-127">如何太[複寫 SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="f30e5-127">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="f30e5-128">部署模式</span><span class="sxs-lookup"><span data-stu-id="f30e5-128">Deployment patterns</span></span>
<span data-ttu-id="f30e5-129">為基礎的 IIS web 應用程式通常會遵循 hello 下列部署模式的其中一個：</span><span class="sxs-lookup"><span data-stu-id="f30e5-129">An IIS based web application typically follows one of hello following deployment patterns:</span></span>

<span data-ttu-id="f30e5-130">**部署模式 1 ** 具有應用程式要求路由 (ARR)、IIS 伺服器與 Microsoft SQL Server 的 IIS 型 web 伺服陣列。</span><span class="sxs-lookup"><span data-stu-id="f30e5-130">**Deployment pattern 1 ** An IIS based web farm  with Application Request Routing(ARR), IIS Server and Microsoft SQL Server.</span></span>

![部署模式](./media/site-recovery-iis/deployment-pattern1.png)

<span data-ttu-id="f30e5-132">**部署模式 2** 具有應用程式要求路由 (ARR)、IIS 伺服器、應用程式伺服器與 Microsoft SQL Server 的 IIS 型 web 伺服陣列。</span><span class="sxs-lookup"><span data-stu-id="f30e5-132">**Deployment pattern 2** An IIS based web farm with Application Request Routing(ARR), IIS Server, Application Server, and Microsoft SQL Server.</span></span>


![部署模式](./media/site-recovery-iis/deployment-pattern2.png)

## <a name="site-recovery-support"></a><span data-ttu-id="f30e5-134">Site Recovery 支援</span><span class="sxs-lookup"><span data-stu-id="f30e5-134">Site Recovery support</span></span>

<span data-ttu-id="f30e5-135">Hello 目的是要使用 IIS 伺服器上 Windows Server 2012 R2 Enterprise 版本 7.5 建立此發行項的 VMware 虛擬機器所使用。</span><span class="sxs-lookup"><span data-stu-id="f30e5-135">For hello purpose of creating this article VMware virtual machines with IIS Server version 7.5 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="f30e5-136">站台復原複寫與應用程式無關，hello 建議提供以下是預期的 toohold 在下列的情況下，不同版本的 IIS。</span><span class="sxs-lookup"><span data-stu-id="f30e5-136">As site recovery replication is application agnostic, hello recommendations provided here are expected toohold on following scenarios as well and for different version of IIS.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="f30e5-137">來源與目標</span><span class="sxs-lookup"><span data-stu-id="f30e5-137">Source and target</span></span>

<span data-ttu-id="f30e5-138">**案例**</span><span class="sxs-lookup"><span data-stu-id="f30e5-138">**Scenario**</span></span> | <span data-ttu-id="f30e5-139">**tooa 次要站台**</span><span class="sxs-lookup"><span data-stu-id="f30e5-139">**tooa secondary site**</span></span> | <span data-ttu-id="f30e5-140">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="f30e5-140">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="f30e5-141">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="f30e5-141">**Hyper-V**</span></span> | <span data-ttu-id="f30e5-142">是</span><span class="sxs-lookup"><span data-stu-id="f30e5-142">Yes</span></span> | <span data-ttu-id="f30e5-143">是</span><span class="sxs-lookup"><span data-stu-id="f30e5-143">Yes</span></span>
<span data-ttu-id="f30e5-144">**VMware**</span><span class="sxs-lookup"><span data-stu-id="f30e5-144">**VMware**</span></span> | <span data-ttu-id="f30e5-145">是</span><span class="sxs-lookup"><span data-stu-id="f30e5-145">Yes</span></span> | <span data-ttu-id="f30e5-146">是</span><span class="sxs-lookup"><span data-stu-id="f30e5-146">Yes</span></span>
<span data-ttu-id="f30e5-147">**實體伺服器**</span><span class="sxs-lookup"><span data-stu-id="f30e5-147">**Physical server**</span></span> | <span data-ttu-id="f30e5-148">否</span><span class="sxs-lookup"><span data-stu-id="f30e5-148">No</span></span> | <span data-ttu-id="f30e5-149">是</span><span class="sxs-lookup"><span data-stu-id="f30e5-149">Yes</span></span>

## <a name="replicate-virtual-machines"></a><span data-ttu-id="f30e5-150">複寫虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f30e5-150">Replicate virtual machines</span></span>

<span data-ttu-id="f30e5-151">請遵循[本指南](site-recovery-vmware-to-azure.md)toostart 複寫所有 hello IIS web 伺服陣列的虛擬機器 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="f30e5-151">Follow [this guidance](site-recovery-vmware-to-azure.md) toostart replicating all hello IIS web farm virtual machines tooAzure.</span></span>

<span data-ttu-id="f30e5-152">如果您使用靜態 ip 位址，則指定您想 hello hello 中的虛擬機器 tootake hello IP [**目標 IP** ](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties)運算和網路設定中設定。</span><span class="sxs-lookup"><span data-stu-id="f30e5-152">If you are using a static IP then specify hello IP that you want hello virtual machine tootake in hello [**Target IP**](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties) setting in Compute and Network settings.</span></span>

![目標 IP](./media/site-recovery-active-directory/dns-target-ip.png)


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="f30e5-154">建立復原計劃</span><span class="sxs-lookup"><span data-stu-id="f30e5-154">Creating a recovery plan</span></span>

<span data-ttu-id="f30e5-155">復原計劃可讓您排序 hello 容錯移轉維護應用程式一致性是多層式應用程式，因此，在各層。</span><span class="sxs-lookup"><span data-stu-id="f30e5-155">A recovery plan allows sequencing hello failover of various tiers in a multi-tier application, hence, maintaining application consistency.</span></span> <span data-ttu-id="f30e5-156">建立多層式 web 應用程式的復原計劃時，請遵循下面的步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="f30e5-156">Follow hello below steps while creating a recovery plan for a multi-tier web application.</span></span>  <span data-ttu-id="f30e5-157">[深入了解如何建立復原計劃](./site-recovery-create-recovery-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="f30e5-157">[Learn more about creating a recovery plan](./site-recovery-create-recovery-plans.md).</span></span>

### <a name="adding-virtual-machines-toofailover-groups"></a><span data-ttu-id="f30e5-158">新增虛擬機器 toofailover 群組</span><span class="sxs-lookup"><span data-stu-id="f30e5-158">Adding virtual machines toofailover groups</span></span>
<span data-ttu-id="f30e5-159">SQL 虛擬機器、 hello constituted IIS 伺服器的 web 層和應用程式層的資料庫層將會包含一般的多層式 IIS web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f30e5-159">A typical multi-tier IIS web application will consist of a database tier with SQL virtual machines, hello web tier constituted by a IIS server and an application tier.</span></span> <span data-ttu-id="f30e5-160">所有這些虛擬機器 toodifferent 基礎加入群組層做為下面。</span><span class="sxs-lookup"><span data-stu-id="f30e5-160">Add all these virtual machines toodifferent group based on tier as below.</span></span> <span data-ttu-id="f30e5-161">[深入了解自訂復原方案](site-recovery-runbook-automation.md#customize-the-recovery-plan)。</span><span class="sxs-lookup"><span data-stu-id="f30e5-161">[Learn more about customising recovery plan](site-recovery-runbook-automation.md#customize-the-recovery-plan).</span></span>

1. <span data-ttu-id="f30e5-162">建立復原計畫。</span><span class="sxs-lookup"><span data-stu-id="f30e5-162">Create a recovery plan.</span></span> <span data-ttu-id="f30e5-163">新增群組 1 tooensure 它們最後會關機並帶出第一個下 hello 資料庫在階層虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f30e5-163">Add hello database tier virtual machines under Group 1 tooensure that they are shutdown last and brought up first.</span></span>

1. <span data-ttu-id="f30e5-164">它們會帶出 hello 資料庫層啟動之後，請加入 hello 應用程式層群組 2 底下的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f30e5-164">Add hello application tier virtual machines under Group 2 such that they are brought up after hello database tier has been brought up.</span></span>

1. <span data-ttu-id="f30e5-165">新增群組 3 hello web 層的虛擬機器，使得 hello 應用程式層啟動之後，它們會帶出。</span><span class="sxs-lookup"><span data-stu-id="f30e5-165">Add hello web tier virtual machines in Group 3 such that they are brought up after hello application tier has been brought up.</span></span>

1. <span data-ttu-id="f30e5-166">使 hello web 層啟動之後，它們會帶出，群組 4 中新增虛擬機器負載平衡。</span><span class="sxs-lookup"><span data-stu-id="f30e5-166">Add load balance virtual machines in Group 4 such that they are brought up after hello web tier has been brought up.</span></span>


### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="f30e5-167">加入指令碼 toohello 復原計劃</span><span class="sxs-lookup"><span data-stu-id="f30e5-167">Adding scripts toohello recovery plan</span></span>
<span data-ttu-id="f30e5-168">您可能需要 toodo hello Azure 虛擬機器後測試容錯移轉/容錯移轉 toomake IIS web 伺服陣列函式的某些作業正確。</span><span class="sxs-lookup"><span data-stu-id="f30e5-168">You may need toodo some operations on hello Azure virtual machines post failover/Test failover toomake IIS web farm function correctly.</span></span> <span data-ttu-id="f30e5-169">您可以自動化 hello post 容錯移轉作業，例如更新 DNS 項目，變更 網站繫結、 變更連接字串中加入對應的指令碼，如下所示的 hello 復原方案中。</span><span class="sxs-lookup"><span data-stu-id="f30e5-169">You can automate hello post failover operation like updating DNS entry, changing site binding, change  in connection string  by adding corresponding scripts in hello recovery plan as below.</span></span> <span data-ttu-id="f30e5-170">[深入了解新增指令碼復原計劃](./site-recovery-create-recovery-plans.md#add-scripts)。</span><span class="sxs-lookup"><span data-stu-id="f30e5-170">[Learn more about add script recovery plan](./site-recovery-create-recovery-plans.md#add-scripts).</span></span>

#### <a name="dns-update"></a><span data-ttu-id="f30e5-171">DNS 更新</span><span class="sxs-lookup"><span data-stu-id="f30e5-171">DNS Update</span></span>
<span data-ttu-id="f30e5-172">如果 hello DNS 針對動態 DNS 更新設定，然後虛擬機器通常更新 hello DNS hello 新 IP 之後啟動。</span><span class="sxs-lookup"><span data-stu-id="f30e5-172">If hello DNS is configured for dynamic DNS update then virtual machines usually update hello DNS with hello new IP once they start.</span></span> <span data-ttu-id="f30e5-173">如果您想 tooadd 以 hello 明確步驟 tooupdate DNS 新 hello 虛擬機器的 Ip 再新增這[指令碼在 DNS 中的 tooupdate IP](https://aka.ms/asr-dns-update)作為復原計畫群組後動作。</span><span class="sxs-lookup"><span data-stu-id="f30e5-173">If you want tooadd an explicit step tooupdate DNS with hello new IPs of hello virtual machines then add this [script tooupdate IP in DNS](https://aka.ms/asr-dns-update) as a post action on recovery plan groups.</span></span>  

#### <a name="connection-string-in-an-applications-webconfig"></a><span data-ttu-id="f30e5-174">在應用程式 web.config 中的連接字串</span><span class="sxs-lookup"><span data-stu-id="f30e5-174">Connection string in an application’s web.config</span></span>
<span data-ttu-id="f30e5-175">hello 連接字串會指定與 hello 網站的 hello 資料庫通訊。</span><span class="sxs-lookup"><span data-stu-id="f30e5-175">hello connection string specifies hello database that hello web site communicates with.</span></span>

<span data-ttu-id="f30e5-176">如果 hello 連接字串會帶來 hello hello 資料庫虛擬機器名稱，再執行任何步驟將會容錯移轉所需的後，hello 應用程式將無法 tooautomatically 通訊 toohello DB。</span><span class="sxs-lookup"><span data-stu-id="f30e5-176">If hello connection string carries hello name of hello database virtual machine, no further steps will be needed post failover and hello application will be able tooautomatically communicate toohello DB.</span></span> <span data-ttu-id="f30e5-177">此外，如果 hello hello 資料庫虛擬機器的 IP 位址會保留下來，它不會需要 tooupdate hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="f30e5-177">Also, if hello IP address for hello database virtual machine is retained, it will not be needed tooupdate hello connection string.</span></span> <span data-ttu-id="f30e5-178">如果 hello 連接字串是指 toohello 資料庫虛擬機器使用的 IP 位址，它將需要容錯移轉後 toobe 更新。</span><span class="sxs-lookup"><span data-stu-id="f30e5-178">If hello connection string refers toohello database virtual machine using an IP address, it will need toobe updated post failover.</span></span> <span data-ttu-id="f30e5-179">例如</span><span class="sxs-lookup"><span data-stu-id="f30e5-179">E.g.</span></span> <span data-ttu-id="f30e5-180">下列連接字串 hello 點 toohello ip 127.0.1.2 DB</span><span class="sxs-lookup"><span data-stu-id="f30e5-180">hello below connection string points toohello DB with IP 127.0.1.2</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <configuration>
        <connectionStrings>
        <add name="ConnStringDb1" connectionString="Data Source= 127.0.1.2\SqlExpress; Initial Catalog=TestDB1;Integrated Security=False;" />
        </connectionStrings>
        </configuration>

<span data-ttu-id="f30e5-181">您可以藉由新增更新 hello 連接字串中的 web 層[IIS 連接更新指令碼](https://aka.ms/asr-update-webtier-script-classic)hello 復原計劃中的群組 3 之後。</span><span class="sxs-lookup"><span data-stu-id="f30e5-181">You can update hello connection string in web tier by adding [IIS connection update script](https://aka.ms/asr-update-webtier-script-classic) after Group 3 in hello recovery plan.</span></span>

#### <a name="site-bindings-for-hello-application"></a><span data-ttu-id="f30e5-182">Hello 應用程式的站台繫結</span><span class="sxs-lookup"><span data-stu-id="f30e5-182">Site bindings for hello application</span></span>
<span data-ttu-id="f30e5-183">每個站台繫結資訊，包括 hello 繫結型別、 hello 的 hello IIS 伺服器接聽 toohello 要求 hello 站台、 hello 連接埠號碼 hello hello 網站的主機名稱的 IP 位址所組成。</span><span class="sxs-lookup"><span data-stu-id="f30e5-183">Every site consists of binding information that includes hello type of binding, hello IP address at which hello IIS server listens toohello requests for hello site, hello port number and hello host names for hello site.</span></span> <span data-ttu-id="f30e5-184">在容錯移轉的 hello 階段，這些繫結可能需要 toobe 更新 hello 與其相關聯的 IP 位址變更時。</span><span class="sxs-lookup"><span data-stu-id="f30e5-184">At hello time of a failover, these bindings might need toobe updated if there is a change in hello IP address associated with them.</span></span>

> [!NOTE]
>
> <span data-ttu-id="f30e5-185">如果您已標記為 'all unassigned' hello 站台繫結，如下列的 hello 範例所示，您將不需要 tooupdate 此繫結 post 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="f30e5-185">If you have marked ‘all unassigned’ for hello site binding as in hello example below, you will not need tooupdate this binding post failover.</span></span> <span data-ttu-id="f30e5-186">此外，如果 hello 與網站相關聯的 IP 位址不會變更 post 容錯移轉，hello 網站繫結需要不會更新 （hello 網路架構取決於保留期 hello IP 位址和子網路指派 toohello 主要和復原站台，因此可能會或可能不會將為您的組織。）</span><span class="sxs-lookup"><span data-stu-id="f30e5-186">Also, if hello IP address associated with a site is not changed post failover, hello site binding need not be updated (Retention of hello IP address depends on hello network architecture and subnets assigned toohello primary and recovery sites and hence may or may not be feasible for your organization.)</span></span>

![SSL 繫結](./media/site-recovery-iis/sslbinding.png)

<span data-ttu-id="f30e5-188">如果您擁有 hello IP 位址關聯站台，您將需要 tooupdate hello 新 IP 位址的所有站台繫結。</span><span class="sxs-lookup"><span data-stu-id="f30e5-188">If you have associated hello IP address with a site, you will need tooupdate all site bindings with hello new IP address.</span></span> <span data-ttu-id="f30e5-189">您可以加入[IIS Web 層更新指令碼](https://aka.ms/asr-web-tier-update-runbook-classic)之後復原計劃 toochange hello 站台繫結中的群組 3。</span><span class="sxs-lookup"><span data-stu-id="f30e5-189">You can add [IIS Web tier update script](https://aka.ms/asr-web-tier-update-runbook-classic) after Group 3 in recovery plan toochange hello site bindings.</span></span>


#### <a name="update-load-balancer-ip-address"></a><span data-ttu-id="f30e5-190">更新負載平衡器 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f30e5-190">Update load balancer IP address</span></span>
<span data-ttu-id="f30e5-191">如果您有應用程式要求路由的虛擬機器，新增[IIS ARR 容錯移轉指令碼](https://aka.ms/asr-iis-arrtier-failover-script-classic)群組 4 tooupdate hello IP 位址之後。</span><span class="sxs-lookup"><span data-stu-id="f30e5-191">If you have  Application Request Routing virtual machine, add [IIS ARR  failover script](https://aka.ms/asr-iis-arrtier-failover-script-classic) after Group 4 tooupdate hello IP address.</span></span>

#### <a name="hello-ssl-cert-binding-for-an-https-connection"></a><span data-ttu-id="f30e5-192">hello SSL 憑證繫結進行 https 連接</span><span class="sxs-lookup"><span data-stu-id="f30e5-192">hello SSL cert binding for an https connection</span></span>
<span data-ttu-id="f30e5-193">網站可以有相關聯的 SSL 憑證，可協助確保 hello 網頁伺服器與 hello 使用者的瀏覽器之間安全通訊。</span><span class="sxs-lookup"><span data-stu-id="f30e5-193">Websites can have an associated SSL certificate that helps in ensuring a secure communication between hello webserver and hello user’s browser.</span></span> <span data-ttu-id="f30e5-194">如果 hello 網站有一個 https 連線和相關聯的 https 網站繫結 toohello IP 位址的 SSL 憑證繫結 hello IIS 伺服器，新的站台繫結必須 toobe 加入 hello 憑證以 hello hello IIS 虛擬機器的 IP 張貼容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="f30e5-194">If hello website has an https connection and an associated https site binding toohello IP address of hello IIS server with an SSL cert binding, a new site binding will need toobe added for hello cert with hello IP of hello IIS virtual machine post failover.</span></span>

<span data-ttu-id="f30e5-195">hello SSL 憑證可以發行對-</span><span class="sxs-lookup"><span data-stu-id="f30e5-195">hello SSL cert can be issued against-</span></span>

<span data-ttu-id="f30e5-196">hello 網站 a) hello 完整的網域名稱</span><span class="sxs-lookup"><span data-stu-id="f30e5-196">a) hello fully qualified domain name of hello website</span></span><br>
<span data-ttu-id="f30e5-197">hello 伺服器 b) hello 名稱</span><span class="sxs-lookup"><span data-stu-id="f30e5-197">b) hello name of hello server</span></span><br>
<span data-ttu-id="f30e5-198">c） 萬用字元憑證 hello 網域名稱</span><span class="sxs-lookup"><span data-stu-id="f30e5-198">c) A wildcard certificate for hello domain name</span></span><br>
<span data-ttu-id="f30e5-199">d） IP 位址 – 如果 hello IIS 伺服器 hello IP 對發出 hello SSL 憑證，另一個 SSL 憑證需求 toobe hello hello IP 位址對 hello Azure 站台上的 IIS 伺服器發出額外的 SSL 繫結此憑證必須 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="f30e5-199">d) An IP address – If hello SSL cert is issued against hello IP of hello IIS server, another SSL cert needs toobe issued against hello IP address of hello IIS server on hello Azure site and an additional SSL binding for this certificate will need toobe created.</span></span> <span data-ttu-id="f30e5-200">因此，它是針對 IP 所核發的 SSL 憑證的建議 toonot 使用。</span><span class="sxs-lookup"><span data-stu-id="f30e5-200">Hence, it is advisable toonot use an SSL cert issued against IP.</span></span> <span data-ttu-id="f30e5-201">這是較不常用的選項，而且很快就會根據新的 CA/瀏覽器論壇變更而取代。</span><span class="sxs-lookup"><span data-stu-id="f30e5-201">This is a less widely used option and will soon be deprecated as per new CA/browser forum changes.</span></span>

#### <a name="update-hello-dependency-between-hello-web-and-hello-application-tier"></a><span data-ttu-id="f30e5-202">更新 hello hello web 和 hello 應用程式層之間的相依性</span><span class="sxs-lookup"><span data-stu-id="f30e5-202">Update hello dependency between hello web and hello application tier</span></span>
<span data-ttu-id="f30e5-203">如果您有根據 hello hello 虛擬機器的 IP 位址的特定相依性的應用程式，您需要 tooupdate 此相依性 post 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="f30e5-203">If you have an application specific dependency based on hello IP address of hello virtual machines, you need tooupdate this dependency post failover.</span></span>

## <a name="doing-a-test-failover"></a><span data-ttu-id="f30e5-204">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="f30e5-204">Doing a test failover</span></span>
<span data-ttu-id="f30e5-205">請遵循[本指南](site-recovery-test-failover-to-azure.md)toodo 測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="f30e5-205">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

1.  <span data-ttu-id="f30e5-206">移 tooAzure 入口網站，然後選取您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="f30e5-206">Go tooAzure portal and select your Recovery Service vault.</span></span>
1.  <span data-ttu-id="f30e5-207">按一下 建立 IIS web 伺服陣列的 hello 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="f30e5-207">Click on hello recovery plan created for IIS web farm.</span></span>
1.  <span data-ttu-id="f30e5-208">按一下 [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="f30e5-208">Click on 'Test Failover'.</span></span>
1.  <span data-ttu-id="f30e5-209">選取的復原點和 Azure 虛擬網路 toostart hello 測試容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="f30e5-209">Select recovery point and Azure virtual network toostart hello test failover process.</span></span>
1.  <span data-ttu-id="f30e5-210">一旦 hello 次要環境已啟動，您可以執行您的驗證。</span><span class="sxs-lookup"><span data-stu-id="f30e5-210">Once hello secondary environment is up, you can perform your validations.</span></span>
1.  <span data-ttu-id="f30e5-211">Hello 驗證完成後，您可以選取 '完成驗證'，並將清除 hello 測試容錯移轉環境。</span><span class="sxs-lookup"><span data-stu-id="f30e5-211">Once hello validations are complete, you can select ‘Validations complete’ and hello test failover environment will be cleaned.</span></span>

## <a name="doing-a-failover"></a><span data-ttu-id="f30e5-212">執行容錯移轉</span><span class="sxs-lookup"><span data-stu-id="f30e5-212">Doing a failover</span></span>
<span data-ttu-id="f30e5-213">當您在進行容錯移轉時，請依照[本指引](site-recovery-failover.md)。</span><span class="sxs-lookup"><span data-stu-id="f30e5-213">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

1.  <span data-ttu-id="f30e5-214">移 tooAzure 入口網站，然後選取您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="f30e5-214">Go tooAzure portal and select your Recovery Service vault.</span></span>
1.  <span data-ttu-id="f30e5-215">按一下 建立 IIS web 伺服陣列的 hello 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="f30e5-215">Click on hello recovery plan created for IIS web farm.</span></span>
1.  <span data-ttu-id="f30e5-216">按一下 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="f30e5-216">Click on 'Failover'.</span></span>
1.  <span data-ttu-id="f30e5-217">選取的復原點 toostart hello 容錯移轉程序。</span><span class="sxs-lookup"><span data-stu-id="f30e5-217">Select recovery point toostart hello failover process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f30e5-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f30e5-218">Next steps</span></span>
<span data-ttu-id="f30e5-219">您可以使用站台復原深入了解[複寫其他應用程式](site-recovery-workload.md)。</span><span class="sxs-lookup"><span data-stu-id="f30e5-219">You can learn more about [replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
