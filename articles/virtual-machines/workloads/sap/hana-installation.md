---
title: "在 Azure （大型執行個體） 上的 SAP HANA 的 SAP HANA aaaInstall |Microsoft 文件"
description: "如何在 Azure （大型執行個體） 上的 SAP HANA 的 SAP HANA tooinstall。"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b2fe242270a1166cabcfae2f9249a8dd70ff3b93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-sap-hana-large-instances-on-azure"></a><span data-ttu-id="95795-103">如何 tooinstall 及設定 Azure 上 SAP HANA （大型執行個體）</span><span class="sxs-lookup"><span data-stu-id="95795-103">How tooinstall and configure SAP HANA (large instances) on Azure</span></span>

<span data-ttu-id="95795-104">以下是一些重要定義 tooknow 先閱讀本指南。</span><span class="sxs-lookup"><span data-stu-id="95795-104">Following are some important definitions tooknow before you read this guide.</span></span> <span data-ttu-id="95795-105">我們在 [Azure 上 SAP HANA (大型執行個體) 的概觀和架構](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)中引進了兩種不同類別的 HANA 大型執行個體單位：</span><span class="sxs-lookup"><span data-stu-id="95795-105">In [SAP HANA (large instances) overview and architecture on Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) we introduced two different classes of HANA Large Instance units with:</span></span>

- <span data-ttu-id="95795-106">S72、 S72m、 S144、 S144m、 S192 和 S192m 我們 tooas hello '我類別的 Type' 的 Sku。</span><span class="sxs-lookup"><span data-stu-id="95795-106">S72, S72m, S144, S144m, S192, and S192m, which we refer tooas hello 'Type I class' of SKUs.</span></span>
- <span data-ttu-id="95795-107">S384、 S384m、 S384xm、 S576、 S768 及我們的 S960 tooas hello 'Type II class' 的 Sku。</span><span class="sxs-lookup"><span data-stu-id="95795-107">S384, S384m, S384xm, S576, S768, and S960, which we refer tooas hello 'Type II class' of SKUs.</span></span>

<span data-ttu-id="95795-108">hello 類別規範是進行 toobe 整個 hello toodifferent 功能與根據 HANA 大型執行個體 Sku 的需求，請參閱文件 tooeventually HANA 大型執行個體使用。</span><span class="sxs-lookup"><span data-stu-id="95795-108">hello class specifier is going toobe used throughout hello HANA Large Instance documentation tooeventually refer toodifferent capabilities and requirements based on HANA Large Instance SKUs.</span></span>

<span data-ttu-id="95795-109">其他常用定義包括：</span><span class="sxs-lookup"><span data-stu-id="95795-109">Other definitions we use frequently are:</span></span>
- <span data-ttu-id="95795-110">**大型執行個體戳記：**硬體基礎結構堆疊是 SAP HANA TDI 認證和專用 toorun SAP HANA 的執行個體在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="95795-110">**Large Instance stamp:** A hardware infrastructure stack that is SAP HANA TDI certified and dedicated toorun SAP HANA instances within Azure.</span></span>
- <span data-ttu-id="95795-111">**在 Azure （大型執行個體） 上的 SAP HANA:** Azure toorun HANA 中的執行個體上 SAP HANA TDI 認證的硬體，部署在不同的 Azure 區域中的大型執行個體戳記中的 hello 優惠的正式名稱。</span><span class="sxs-lookup"><span data-stu-id="95795-111">**SAP HANA on Azure (Large Instances):** Official name for hello offer in Azure toorun HANA instances in on SAP HANA TDI certified hardware that is deployed in Large Instance stamps in different Azure regions.</span></span> <span data-ttu-id="95795-112">hello 相關詞彙**HANA 大型執行個體**是短的 Azure （大型執行個體） 上的 SAP HANA，廣泛使用此技術的部署指南。</span><span class="sxs-lookup"><span data-stu-id="95795-112">hello related term **HANA Large Instance** is short for SAP HANA on Azure (Large Instances) and is widely used this technical deployment guide.</span></span>


<span data-ttu-id="95795-113">hello SAP HANA 已安裝，您必須負責且 hello 活動接續的 Azure （大型執行個體） 的伺服器上新的 SAP HANA 遞交。</span><span class="sxs-lookup"><span data-stu-id="95795-113">hello installation of SAP HANA is your responsibility and you can start hello activity after handoff of a new SAP HANA on Azure (Large Instances) server.</span></span> <span data-ttu-id="95795-114">和您的 Azure VNet(s) 與 hello HANA 大型執行個體單位之間的 hello 連線已建立之後。</span><span class="sxs-lookup"><span data-stu-id="95795-114">And after hello connectivity between your Azure VNet(s) and hello HANA Large Instance unit(s) got established.</span></span> 

> [!Note]
> <span data-ttu-id="95795-115">根據 SAP 原則，必須由個人認證 tooperform SAP HANA 安裝執行的 SAP HANA hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="95795-115">Per SAP policy, hello installation of SAP HANA must be performed by a person certified tooperform SAP HANA installations.</span></span> <span data-ttu-id="95795-116">人員，已通過 hello 認證 SAP 技術關聯測驗，SAP HANA 安裝認證測驗，或 SAP 認證的系統整合者 (SI)。</span><span class="sxs-lookup"><span data-stu-id="95795-116">A person, who has passed hello Certified SAP Technology Associate exam, SAP HANA Installation certification exam, or by an SAP-certified system integrator (SI).</span></span>

<span data-ttu-id="95795-117">再次檢查，特別是在規劃 tooinstall HANA 2.0 [SAP 支援附註 #2235581 SAP HANA: Supported Operating Systems](https://launchpad.support.sap.com/#/notes/2235581/E)順序 toomake 確定作業系統支援該 hello 以 hello SAP HANA 釋放您決定 tooinstall。</span><span class="sxs-lookup"><span data-stu-id="95795-117">Check again, especially when planning tooinstall HANA 2.0, [SAP Support Note #2235581 - SAP HANA: Supported Operating Systems](https://launchpad.support.sap.com/#/notes/2235581/E) in order toomake sure that hello OS is supported with hello SAP HANA release you decided tooinstall.</span></span> <span data-ttu-id="95795-118">您了解支援的作業系統的限制多於 HANA 2.0 hello 作業系統支援 HANA 1.0 該 hello。</span><span class="sxs-lookup"><span data-stu-id="95795-118">You realize that hello supported OS for HANA 2.0 is more restricted than hello OS supported for HANA 1.0.</span></span> 

## <a name="first-steps-after-receiving-hello-hana-large-instance-units"></a><span data-ttu-id="95795-119">收到 hello HANA 大型執行個體單元後的第一個步驟</span><span class="sxs-lookup"><span data-stu-id="95795-119">First steps after receiving hello HANA Large Instance Unit(s)</span></span>

<span data-ttu-id="95795-120">**第一步**在收到後 hello HANA 大型執行個體，且需建立存取和連線 toohello 執行個體，tooregister hello OS hello 與作業系統提供者的執行個體。</span><span class="sxs-lookup"><span data-stu-id="95795-120">**First Step** after receiving hello HANA Large Instance and having established access and connectivity toohello instances, is tooregister hello OS of hello instance with your OS provider.</span></span> <span data-ttu-id="95795-121">這個步驟包括 SUSE SMT 需要 toohave 部署在 Azure 中的 VM 中的執行個體中註冊您的 SUSE Linux 作業系統。</span><span class="sxs-lookup"><span data-stu-id="95795-121">This step would include registering your SUSE Linux OS in an instance of SUSE SMT that you need toohave deployed in a VM in Azure.</span></span> <span data-ttu-id="95795-122">hello HANA 大型執行個體單位可以連接 toothis SMT 執行個體 （請參閱本文件中的更新版本）。</span><span class="sxs-lookup"><span data-stu-id="95795-122">hello HANA Large Instance unit can connect toothis SMT instance (see later in this documentation).</span></span> <span data-ttu-id="95795-123">或 RedHat OS 必須向 hello Red Hat 訂用帳戶管理員，您需要以 tooconnect toobe。</span><span class="sxs-lookup"><span data-stu-id="95795-123">Or your RedHat OS needs toobe registered with hello Red Hat Subscription Manager you need tooconnect to.</span></span> <span data-ttu-id="95795-124">另請參閱這份[文件](https://docs.microsoft.com/azure/virtual-machines/linux/sap-hana-overview-architecture?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中的備註。</span><span class="sxs-lookup"><span data-stu-id="95795-124">See also remarks in this [document](https://docs.microsoft.com/azure/virtual-machines/linux/sap-hana-overview-architecture?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="95795-125">這個步驟也是必要 toobe 無法 toopatch hello OS。</span><span class="sxs-lookup"><span data-stu-id="95795-125">This step also is necessary toobe able toopatch hello OS.</span></span> <span data-ttu-id="95795-126">工作中的 hello 客戶的 hello 責任。</span><span class="sxs-lookup"><span data-stu-id="95795-126">A task that is in hello responsibility of hello customer.</span></span> <span data-ttu-id="95795-127">SUSE，尋找文件 tooinstall 並設定 SMT[這裡](https://www.suse.com/documentation/sles-12/book_smt/data/smt_installation.html)。</span><span class="sxs-lookup"><span data-stu-id="95795-127">For SUSE, find documentation tooinstall and configure SMT [here](https://www.suse.com/documentation/sles-12/book_smt/data/smt_installation.html).</span></span>

<span data-ttu-id="95795-128">**第二個步驟**是新的更新和修正的 hello 特定作業系統版本/版本 toocheck。</span><span class="sxs-lookup"><span data-stu-id="95795-128">**Second Step** is toocheck for new patches and fixes of hello specific OS release/version.</span></span> <span data-ttu-id="95795-129">檢查 hello HANA 大型執行個體的 hello 修補程式等級是否在 hello 最新狀態。</span><span class="sxs-lookup"><span data-stu-id="95795-129">Check whether hello patch level of hello HANA Large Instance is on hello latest state.</span></span> <span data-ttu-id="95795-130">根據 OS 修補程式/版本與變更 toohello 映像可以部署 Microsoft 上的時間，可能會有情況下，hello 最新修補程式可能不會包含在內。</span><span class="sxs-lookup"><span data-stu-id="95795-130">Based on timing on OS patch/releases and changes toohello image Microsoft can deploy, there might be cases where hello latest patches may not be included.</span></span> <span data-ttu-id="95795-131">因此它是之後接管 HANA 大型執行個體單位，toocheck 是否同時發行特定 Linux 廠商 hello 修補程式的安全性、 功能、 可用性和效能相關，而且需要 toobe 套用必要的步驟。</span><span class="sxs-lookup"><span data-stu-id="95795-131">Hence it is a mandatory step after taking over a HANA Large Instance unit, toocheck whether patches relevant for security, functionality, availability, and performance were released meanwhile by hello particular Linux vendor and need toobe applied.</span></span>

<span data-ttu-id="95795-132">**第三個步驟**是出 hello toocheck 上安裝和設定 SAP HANA hello 特定作業系統版本/版本相關的 SAP 附註。</span><span class="sxs-lookup"><span data-stu-id="95795-132">**Third Step** is toocheck out hello relevant SAP Notes for installing and configuring SAP HANA on hello specific OS release/version.</span></span> <span data-ttu-id="95795-133">由於 toochanging 建議或變更 tooSAP 附註或相依於個別的安裝案例的組態，Microsoft 不一定能 toohave HANA 大型執行個體單位完全設定。</span><span class="sxs-lookup"><span data-stu-id="95795-133">Due toochanging recommendations or changes tooSAP Notes or configurations that are dependent on individual installation scenarios, Microsoft will not always be able toohave a HANA Large Instance unit configured perfectly.</span></span> <span data-ttu-id="95795-134">因此，它會強制您為客戶、 tooread hello SAP 附註相關 tooSAP HANA 確切的 Linux 版本上。</span><span class="sxs-lookup"><span data-stu-id="95795-134">Hence it is mandatory for you as a customer, tooread hello SAP Notes related tooSAP HANA on your exact Linux release.</span></span> <span data-ttu-id="95795-135">也請檢查 hello OS 版本/版本所需的 hello 設定並套用 hello 組態設定其中尚未完成。</span><span class="sxs-lookup"><span data-stu-id="95795-135">Also check hello configurations of hello OS release/version necessary and apply hello configuration settings where not done already.</span></span>

<span data-ttu-id="95795-136">在特定，檢查下列參數，且最後會調整成 hello:</span><span class="sxs-lookup"><span data-stu-id="95795-136">In specific, check hello following parameters and eventually adjusted to:</span></span>

- <span data-ttu-id="95795-137">net.core.rmem_max = 16777216</span><span class="sxs-lookup"><span data-stu-id="95795-137">net.core.rmem_max = 16777216</span></span>
- <span data-ttu-id="95795-138">net.core.wmem_max = 16777216</span><span class="sxs-lookup"><span data-stu-id="95795-138">net.core.wmem_max = 16777216</span></span>
- <span data-ttu-id="95795-139">net.core.rmem_default = 16777216</span><span class="sxs-lookup"><span data-stu-id="95795-139">net.core.rmem_default = 16777216</span></span>
- <span data-ttu-id="95795-140">net.core.wmem_default = 16777216</span><span class="sxs-lookup"><span data-stu-id="95795-140">net.core.wmem_default = 16777216</span></span>
- <span data-ttu-id="95795-141">net.core.optmem_max = 16777216</span><span class="sxs-lookup"><span data-stu-id="95795-141">net.core.optmem_max = 16777216</span></span>
- <span data-ttu-id="95795-142">net.ipv4.tcp_rmem = 65536 16777216 16777216</span><span class="sxs-lookup"><span data-stu-id="95795-142">net.ipv4.tcp_rmem = 65536 16777216 16777216</span></span>
- <span data-ttu-id="95795-143">net.ipv4.tcp_wmem = 65536 16777216 16777216</span><span class="sxs-lookup"><span data-stu-id="95795-143">net.ipv4.tcp_wmem = 65536 16777216 16777216</span></span>

<span data-ttu-id="95795-144">從 SLES12 SP1 和 RHEL 7.2，必須在 hello /etc/sysctl.d 目錄中的組態檔中設定這些參數。</span><span class="sxs-lookup"><span data-stu-id="95795-144">Starting with SLES12 SP1 and RHEL 7.2, these parameters must be set in a configuration file in hello /etc/sysctl.d directory.</span></span> <span data-ttu-id="95795-145">例如，您必須建立含有 hello 名稱 91 NetApp HANA.conf 組態檔。</span><span class="sxs-lookup"><span data-stu-id="95795-145">For example, a configuration file with hello name 91-NetApp-HANA.conf must be created.</span></span> <span data-ttu-id="95795-146">如果是舊版 SLES 和 RHEL，則必須 /etc/sysctl.conf 中設定這些參數。</span><span class="sxs-lookup"><span data-stu-id="95795-146">For older SLES and RHEL releases, these parameters must be set in/etc/sysctl.conf.</span></span>

<span data-ttu-id="95795-147">針對所有 RHEL 發行版本和起 SLES12 hello</span><span class="sxs-lookup"><span data-stu-id="95795-147">For all RHEL releases and starting with SLES12, hello</span></span> 
- <span data-ttu-id="95795-148">sunrpc.tcp_slot_table_entries = 128</span><span class="sxs-lookup"><span data-stu-id="95795-148">sunrpc.tcp_slot_table_entries = 128</span></span>

<span data-ttu-id="95795-149">參數必須在 /etc/modprobe.d/sunrpc-local.conf 中設定。</span><span class="sxs-lookup"><span data-stu-id="95795-149">parameter must be set in/etc/modprobe.d/sunrpc-local.conf.</span></span> <span data-ttu-id="95795-150">如果 hello 檔案不存在，它必須先建立藉由新增下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="95795-150">If hello file does not exist, it must first be created by adding hello following entry:</span></span> 
- <span data-ttu-id="95795-151">options sunrpc tcp_max_slot_table_entries=128</span><span class="sxs-lookup"><span data-stu-id="95795-151">options sunrpc tcp_max_slot_table_entries=128</span></span>

<span data-ttu-id="95795-152">**第四個步驟**HANA 大型執行個體單位的 toocheck hello 系統時間。</span><span class="sxs-lookup"><span data-stu-id="95795-152">**Fourth Step** is toocheck hello system time of your HANA Large Instance Unit.</span></span> <span data-ttu-id="95795-153">代表 hello Azure 地區 hello HANA 大型執行個體戳記位於 hello 位置的系統時區部署 hello 執行個體。</span><span class="sxs-lookup"><span data-stu-id="95795-153">hello instances are deployed with a system time zone that represent hello location of hello Azure region hello HANA Large Instance Stamp is located in.</span></span> <span data-ttu-id="95795-154">您是免費 toochange hello 系統時間或您擁有 hello 執行個體的時區時間。</span><span class="sxs-lookup"><span data-stu-id="95795-154">You are free toochange hello system time or time zone of hello instances you own.</span></span> <span data-ttu-id="95795-155">這樣做並排序成您的租用戶的多個執行個體，您需要 tooadapt hello 的時區時間 hello 新傳遞執行個體備妥。</span><span class="sxs-lookup"><span data-stu-id="95795-155">Doing so and ordering more instances into your tenant, be prepared that you need tooadapt hello time zone of hello newly delivered instances.</span></span> <span data-ttu-id="95795-156">Microsoft 作業會有任何深入了解系統時區 hello 您 hello 執行個體之後設定 hello 移。</span><span class="sxs-lookup"><span data-stu-id="95795-156">Microsoft operations have no insights into hello system time zone you set up with hello instances after hello handover.</span></span> <span data-ttu-id="95795-157">因此新部署的執行個體可能會在未設定 hello 相同時區為 hello 變更為一。</span><span class="sxs-lookup"><span data-stu-id="95795-157">Hence newly deployed instances might not be set in hello same time zone as hello one you changed to.</span></span> <span data-ttu-id="95795-158">如此一來，您必須負責為客戶 toocheck，如有必要調整 hello hello 執行個體上的時區時間。</span><span class="sxs-lookup"><span data-stu-id="95795-158">As a result, it is your responsibility as customer toocheck and if necessary adapt hello time zone of hello instance(s) handed over.</span></span> 

<span data-ttu-id="95795-159">**第五個步驟**toocheck 等/裝載。</span><span class="sxs-lookup"><span data-stu-id="95795-159">**Fifth Step** is toocheck etc/hosts.</span></span> <span data-ttu-id="95795-160">隨著 hello 刀鋒視窗取得移交時，它們就會有不同的 IP 位址指派不同的用途，（請參閱下一節）。</span><span class="sxs-lookup"><span data-stu-id="95795-160">As hello blades get handed over, they have different IP addresses assigned for different purposes (see next section).</span></span> <span data-ttu-id="95795-161">請檢查 hello 等/主機檔案。</span><span class="sxs-lookup"><span data-stu-id="95795-161">Check hello etc/hosts file.</span></span> <span data-ttu-id="95795-162">在其中單位會加入到現有的租用戶的情況下，不預期 toohave 等/新部署的 hello 系統正確維護 hello 的稍早傳遞系統的 IP 位址的主機。</span><span class="sxs-lookup"><span data-stu-id="95795-162">In cases where units are added into an existing tenant, don't expect toohave etc/hosts of hello newly deployed systems maintained correctly with hello IP addresses of earlier delivered systems.</span></span> <span data-ttu-id="95795-163">因此它是您在客戶 toocheck hello 正確設定，可以互動的新部署的執行個體，並解析 hello 租用戶中先前已部署的單位名稱。</span><span class="sxs-lookup"><span data-stu-id="95795-163">Hence it is on you as customer toocheck hello correct settings so, that a newly deployed instance can interact and resolve hello names of earlier deployed units in your tenant.</span></span> 

## <a name="networking"></a><span data-ttu-id="95795-164">網路</span><span class="sxs-lookup"><span data-stu-id="95795-164">Networking</span></span>
<span data-ttu-id="95795-165">我們假設您已遵循 hello 建議設計 Azure Vnet 和連接這些 Vnet toohello HANA 大型執行個體，這些文件中所述：</span><span class="sxs-lookup"><span data-stu-id="95795-165">We assume that you followed hello recommendations in designing your Azure VNets and connecting those VNets toohello HANA Large Instances as described in these documents:</span></span>

- [<span data-ttu-id="95795-166">Azure 上 SAP HANA (大型執行個體) 的概觀和架構</span><span class="sxs-lookup"><span data-stu-id="95795-166">SAP HANA (large Instance) Overview and Architecture on Azure</span></span>](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)
- [<span data-ttu-id="95795-167">Azure 上 SAP HANA (大型執行個體) 的基礎結構和連接</span><span class="sxs-lookup"><span data-stu-id="95795-167">SAP HANA (large instances) Infrastructure and connectivity on Azure</span></span>](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="95795-168">有一些不 toomention 有關 hello 網路的 hello 單一單位的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="95795-168">There are some details worth toomention about hello networking of hello single units.</span></span> <span data-ttu-id="95795-169">每個大型執行個體 HANA 單位隨附兩個或三個 tootwo 或 hello 單位的 3 個 NIC 連接埠指派的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="95795-169">Every HANA Large Instance unit comes with two or three IP addresses that are assigned tootwo or three NIC ports of hello unit.</span></span> <span data-ttu-id="95795-170">HANA 向外延展組態和 hello HANA 系統複寫案例中使用三個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="95795-170">Three IP addresses are used in HANA scale-out configurations and hello HANA System Replication scenario.</span></span> <span data-ttu-id="95795-171">其中一個 hello IP 位址指派的 toohello hello 單位的 NIC 超出 hello hello 所述的伺服器的 IP 集區[SAP HANA （大型執行個體） 的概觀和架構，在 Azure 上的](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)。</span><span class="sxs-lookup"><span data-stu-id="95795-171">One of hello IP addresses assigned toohello NIC of hello unit is out of hello Server IP pool that was described in hello [SAP HANA (large Instance) Overview and Architecture on Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture).</span></span>

<span data-ttu-id="95795-172">兩個 IP 位址指派單位的 hello 發佈看起來應該像：</span><span class="sxs-lookup"><span data-stu-id="95795-172">hello distribution for units with two IP addresses assigned should look like:</span></span>

- <span data-ttu-id="95795-173">eth0.xx 應該有指派的 IP 位址超出 hello 送出 tooMicrosoft 伺服器的 IP 集區位址範圍。</span><span class="sxs-lookup"><span data-stu-id="95795-173">eth0.xx should have an IP address assigned that is out of hello Server IP Pool address range that you submitted tooMicrosoft.</span></span> <span data-ttu-id="95795-174">此 IP 位址應該用於 hello OS 的 /etc/hosts 中維護。</span><span class="sxs-lookup"><span data-stu-id="95795-174">This IP address shall be used for maintaining in /etc/hosts of hello OS.</span></span>
- <span data-ttu-id="95795-175">eth1.xx 應該有 IP 位址指派用於通訊 tooNFS。</span><span class="sxs-lookup"><span data-stu-id="95795-175">eth1.xx should have an IP address assigned that is used for communication tooNFS.</span></span> <span data-ttu-id="95795-176">因此，這些位址進行**不**需要 toobe 等/主機順序 tooallow 執行個體 tooinstance 流量 hello 租用戶內維護。</span><span class="sxs-lookup"><span data-stu-id="95795-176">Therefore, these addresses do **NOT** need toobe maintained in etc/hosts in order tooallow instance tooinstance traffic within hello tenant.</span></span>

<span data-ttu-id="95795-177">就 HANA 系統複寫或 HANA 向外延展部署案例而言，並不適合使用有兩個指派之 IP 位址的刀鋒伺服器組態。</span><span class="sxs-lookup"><span data-stu-id="95795-177">For deployment cases of HANA System Replication or HANA scale-out, a blade configuration with two IP addresses assigned is not suitable.</span></span> <span data-ttu-id="95795-178">如果只指派兩個 IP 位址以及由 toodeploy 這種組態中，與 SAP HANA Azure 服務管理 tooget 第三個 IP 位址第三個指派的 VLAN。</span><span class="sxs-lookup"><span data-stu-id="95795-178">If having two IP addresses assigned only and wanting toodeploy such a configuration, contact SAP HANA on Azure Service Management tooget a third IP address in a third VLAN assigned.</span></span> <span data-ttu-id="95795-179">有三個 IP 位址指派上 3 個 NIC 的連接埠 HANA 大型執行個體單位，hello 使用量適用下列規則：</span><span class="sxs-lookup"><span data-stu-id="95795-179">For HANA Large Instance units having three IP addresses assigned on three NIC ports, hello following usage rules apply:</span></span>

- <span data-ttu-id="95795-180">eth0.xx 應該有指派的 IP 位址超出 hello 送出 tooMicrosoft 伺服器的 IP 集區位址範圍。</span><span class="sxs-lookup"><span data-stu-id="95795-180">eth0.xx should have an IP address assigned that is out of hello Server IP Pool address range that you submitted tooMicrosoft.</span></span> <span data-ttu-id="95795-181">因此這個 IP 位址不應該使用的 hello OS /etc/hosts 中維護。</span><span class="sxs-lookup"><span data-stu-id="95795-181">Hence this IP address shall not be used for maintaining in /etc/hosts of hello OS.</span></span>
- <span data-ttu-id="95795-182">eth1.xx 應該用於通訊 tooNFS 存放裝置的 IP 位址指派。</span><span class="sxs-lookup"><span data-stu-id="95795-182">eth1.xx should have an IP address assigned that is used for communication tooNFS storage.</span></span> <span data-ttu-id="95795-183">因此，不應該在 etc/hosts 中維護此類型的位址。</span><span class="sxs-lookup"><span data-stu-id="95795-183">Hence this type of addresses should not be maintained in etc/hosts.</span></span>
- <span data-ttu-id="95795-184">eth2.xx 應該以獨佔方式使用的 toobe 維護等/主控件 hello 不同執行個體之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="95795-184">eth2.xx should be exclusively used toobe maintained in etc/hosts for communication between hello different instances.</span></span> <span data-ttu-id="95795-185">這些位址也會需要 toobe HANA hello 節點間組態所使用的 IP 位址保持在向外延展 HANA 組態中的 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="95795-185">These addresses would also be hello IP addresses that need toobe maintained in scale-out HANA configurations as IP addresses HANA uses for hello inter-node configuration.</span></span>



## <a name="storage"></a><span data-ttu-id="95795-186">儲存體</span><span class="sxs-lookup"><span data-stu-id="95795-186">Storage</span></span>

<span data-ttu-id="95795-187">hello Azure （大型執行個體） 上的 SAP hana 的儲存配置設定上透過建議輔助線，如中所述的 SAP 的 Azure 服務管理的 SAP HANA [SAP HANA 存放裝置需求](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html)技術白皮書。</span><span class="sxs-lookup"><span data-stu-id="95795-187">hello storage layout for SAP HANA on Azure (Large Instances) is configured by SAP HANA on Azure Service Management through SAP recommended guide lines as documented in [SAP HANA Storage Requirements](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) white paper.</span></span> <span data-ttu-id="95795-188">hello hello 不同磁碟區的約略大小以詳加說明不同 HANA 大型執行個體 Sku 收到的 hello [SAP HANA （大型執行個體） 的概觀和架構，在 Azure 上的](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="95795-188">hello rough sizes of hello different volumes with hello different HANA Large Instances SKUs got documented in [SAP HANA (large Instance) Overview and Architecture on Azure](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="95795-189">hello hello 存放磁碟區的命名慣例已列於下表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="95795-189">hello naming conventions of hello storage volumes are listed in hello following table:</span></span>

| <span data-ttu-id="95795-190">儲存體使用量</span><span class="sxs-lookup"><span data-stu-id="95795-190">Storage usage</span></span> | <span data-ttu-id="95795-191">掛接名稱</span><span class="sxs-lookup"><span data-stu-id="95795-191">Mount Name</span></span> | <span data-ttu-id="95795-192">磁碟區名稱</span><span class="sxs-lookup"><span data-stu-id="95795-192">Volume Name</span></span> | 
| --- | --- | ---|
| <span data-ttu-id="95795-193">HANA 資料</span><span class="sxs-lookup"><span data-stu-id="95795-193">HANA data</span></span> | <span data-ttu-id="95795-194">/hana/data/SID/mnt0000<m></span><span class="sxs-lookup"><span data-stu-id="95795-194">/hana/data/SID/mnt0000<m></span></span> | <span data-ttu-id="95795-195">儲存體 IP：/hana_data_SID_mnt00001_tenant_vol</span><span class="sxs-lookup"><span data-stu-id="95795-195">Storage IP:/hana_data_SID_mnt00001_tenant_vol</span></span> |
| <span data-ttu-id="95795-196">HANA 記錄檔</span><span class="sxs-lookup"><span data-stu-id="95795-196">HANA log</span></span> | <span data-ttu-id="95795-197">/hana/log/SID/mnt0000<m></span><span class="sxs-lookup"><span data-stu-id="95795-197">/hana/log/SID/mnt0000<m></span></span> | <span data-ttu-id="95795-198">儲存體 IP：/hana_log_SID_mnt00001_tenant_vol</span><span class="sxs-lookup"><span data-stu-id="95795-198">Storage IP:/hana_log_SID_mnt00001_tenant_vol</span></span> |
| <span data-ttu-id="95795-199">HANA 記錄備份</span><span class="sxs-lookup"><span data-stu-id="95795-199">HANA log backup</span></span> | <span data-ttu-id="95795-200">/hana/log/backups</span><span class="sxs-lookup"><span data-stu-id="95795-200">/hana/log/backups</span></span> | <span data-ttu-id="95795-201">儲存體 IP：/hana_log_backups_SID_mnt00001_tenant_vol</span><span class="sxs-lookup"><span data-stu-id="95795-201">Storage IP:/hana_log_backups_SID_mnt00001_tenant_vol</span></span> |
| <span data-ttu-id="95795-202">HANA 共用</span><span class="sxs-lookup"><span data-stu-id="95795-202">HANA shared</span></span> | <span data-ttu-id="95795-203">/hana/shared/SID</span><span class="sxs-lookup"><span data-stu-id="95795-203">/hana/shared/SID</span></span> | <span data-ttu-id="95795-204">儲存體 IP：/hana_shared_SID_mnt00001_tenant_vol/shared</span><span class="sxs-lookup"><span data-stu-id="95795-204">Storage IP:/hana_shared_SID_mnt00001_tenant_vol/shared</span></span> |
| <span data-ttu-id="95795-205">usr/sap</span><span class="sxs-lookup"><span data-stu-id="95795-205">usr/sap</span></span> | <span data-ttu-id="95795-206">/usr/sap/SID</span><span class="sxs-lookup"><span data-stu-id="95795-206">/usr/sap/SID</span></span> | <span data-ttu-id="95795-207">儲存體 IP：/hana_shared_SID_mnt00001_tenant_vol/usr_sap</span><span class="sxs-lookup"><span data-stu-id="95795-207">Storage IP:/hana_shared_SID_mnt00001_tenant_vol/usr_sap</span></span> |

<span data-ttu-id="95795-208">其中 SID = hello HANA 執行個體的系統識別碼</span><span class="sxs-lookup"><span data-stu-id="95795-208">Where SID = hello HANA instance System ID</span></span> 

<span data-ttu-id="95795-209">tenant = 部署租用戶時的內部作業列舉。</span><span class="sxs-lookup"><span data-stu-id="95795-209">And tenant = an internal enumeration of operations when deploying a tenant.</span></span>

<span data-ttu-id="95795-210">如您所見，共用 HANA 共用和 usr/sap hello 相同的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="95795-210">As you can see, HANA shared and usr/sap are sharing hello same volume.</span></span> <span data-ttu-id="95795-211">hello 命名法的 hello mountpoints 並包含 hello 的 hello HANA 執行個體，以及 hello 掛接編號系統識別碼。</span><span class="sxs-lookup"><span data-stu-id="95795-211">hello nomenclature of hello mountpoints does include hello System ID of hello HANA instances as well as hello mount number.</span></span> <span data-ttu-id="95795-212">在相應增加部署中，只有一個掛接，像是 mnt00001。</span><span class="sxs-lookup"><span data-stu-id="95795-212">In scale-up deployments there only is one mount, like mnt00001.</span></span> <span data-ttu-id="95795-213">而在向外延展部署中，您會看到許多掛接，因為有背景工作角色和主要節點。</span><span class="sxs-lookup"><span data-stu-id="95795-213">Whereas in scale-out deployment you would see as many mounts, as, you have worker and master nodes.</span></span> <span data-ttu-id="95795-214">Hello 向外延展環境、 資料、 記錄檔，記錄備份的磁碟區會共用並附加 tooeach hello 向外延展組態中的節點。</span><span class="sxs-lookup"><span data-stu-id="95795-214">For hello scale-out environment, data, log, log backup volumes are shared and attached tooeach node in hello scale-out configuration.</span></span> <span data-ttu-id="95795-215">執行多個 SAP 執行個體的設定，一組不同的磁碟區會是已建立並附加 toohello 韓文大型執行個體的單位。</span><span class="sxs-lookup"><span data-stu-id="95795-215">For configurations running multiple SAP instances, a different set of volumes is created and attached toohello HAN Large Instance unit.</span></span>

<span data-ttu-id="95795-216">當您讀取 hello 紙張，並尋找 HANA 大型執行個體單元，您將了解 hello 單位有相當多的磁碟區與 HANA/資料，而且我們有 HANA/記錄檔備份的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="95795-216">As you read hello paper and look a HANA Large Instance unit, you realize that hello units come with rather generous disk volume for HANA/data and that we have a volume HANA/log/backup.</span></span> <span data-ttu-id="95795-217">為什麼我們大小 hello HANA/資料很大的 hello 原因是 hello 儲存快照集，我們提供您的客戶使用 hello 相同的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="95795-217">hello reason why we sized hello HANA/data so large is that hello storage snapshots we offer for you as a customer are using hello same disk volume.</span></span> <span data-ttu-id="95795-218">這表示 hello 多個儲存體快照在執行時，hello 更多的空間供您指定的存放磁碟區中的快照集。</span><span class="sxs-lookup"><span data-stu-id="95795-218">It means hello more storage snapshots you perform, hello more space is consumed by snapshots in your assigned storage volumes.</span></span> <span data-ttu-id="95795-219">hello HANA/記錄檔備份磁碟區不是思考 toobe hello 磁碟區中的 tooput 資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="95795-219">hello HANA/log/backup volume is not thought toobe hello volume tooput database backups in.</span></span> <span data-ttu-id="95795-220">它是可調整大小的 toobe 作為 hello HANA 交易記錄備份備份磁碟區。</span><span class="sxs-lookup"><span data-stu-id="95795-220">It is sized toobe used as backup volume for hello HANA transaction log backups.</span></span> <span data-ttu-id="95795-221">在未來版本的 hello 儲存快照集自助服務，我們將為目標多個此特定磁碟區 toohave 頻繁的快照集。</span><span class="sxs-lookup"><span data-stu-id="95795-221">In future versions of hello storage snapshot self service, we will target this specific volume toohave more frequent snapshots.</span></span> <span data-ttu-id="95795-222">與更頻繁的複寫 toohello 災害復原站台有 toooption 單元 hello hello HANA 大型執行個體的基礎結構所提供的災害復原功能。</span><span class="sxs-lookup"><span data-stu-id="95795-222">And with that more frequent replications toohello disaster recovery site if you desire toooption-in for hello disaster recovery functionality provided by hello HANA Large Instance infrastructure.</span></span> <span data-ttu-id="95795-223">詳細資訊請參閱 [Azure 上 SAP Hana (大型執行個體) 的高可用性和災害復原](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="95795-223">See details in [SAP HANA (large instances) High Availability and Disaster Recovery on Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> 

<span data-ttu-id="95795-224">除了提供 toohello 儲存體，您就可以購買額外的儲存體容量，以 1 TB 為增量單位。</span><span class="sxs-lookup"><span data-stu-id="95795-224">In addition toohello storage provided, you can purchase additional storage capacity in 1 TB increments.</span></span> <span data-ttu-id="95795-225">此額外的存放裝置可新增為新的磁碟區 tooa HANA 大型執行個體。</span><span class="sxs-lookup"><span data-stu-id="95795-225">This additional storage can be added as new volumes tooa HANA Large Instances.</span></span>

<span data-ttu-id="95795-226">在上線期間與 Azure 服務管理上的 SAP HANA，hello 客戶指定的使用者識別碼 (UID) 與群組識別碼 (GID) hello sidadm 使用者和 sapsys 群組 (例如： 1000,500) 則需要在安裝期間的 hello SAP HANA 系統，會使用這些相同的值。</span><span class="sxs-lookup"><span data-stu-id="95795-226">During onboarding with SAP HANA on Azure Service Management, hello customer specifies a User ID (UID) and Group ID (GID) for hello sidadm user and sapsys group (ex: 1000,500) It is necessary that during installation of hello SAP HANA system, these same values are used.</span></span> <span data-ttu-id="95795-227">您想要 toodeploy 單元上的多個 HANA 執行個體，您會取得多個磁碟區 （每個執行個體的一組） 集。</span><span class="sxs-lookup"><span data-stu-id="95795-227">As you want toodeploy multiple HANA instances on a unit, you get multiple sets of volumes (one set for each instance).</span></span> <span data-ttu-id="95795-228">如此一來，在部署期間您會需要 toodefine:</span><span class="sxs-lookup"><span data-stu-id="95795-228">As a result, at deployment time you need toodefine:</span></span>

- <span data-ttu-id="95795-229">hello hello 不同 HANA 的執行個體 （sidadm 衍生不使用） 的 SID。</span><span class="sxs-lookup"><span data-stu-id="95795-229">hello SID of hello different HANA instances (sidadm is derived out of it).</span></span>
- <span data-ttu-id="95795-230">Hello 不同 HANA 執行個體的記憶體大小。</span><span class="sxs-lookup"><span data-stu-id="95795-230">Memory sizes of hello different HANA instances.</span></span> <span data-ttu-id="95795-231">因為 hello 記憶體大小，每個執行個體中每個個別的磁碟區組定義 hello hello 磁碟區大小。</span><span class="sxs-lookup"><span data-stu-id="95795-231">Since hello memory size per instances defines hello size of hello volumes in each individual volume set.</span></span>

<span data-ttu-id="95795-232">根據存放裝置提供者建議 hello 下列掛接選項已針對所有掛接的磁碟區 （不包括開機 LUN）：</span><span class="sxs-lookup"><span data-stu-id="95795-232">Based on storage provider recommendations hello following mount options are configured for all mounted volumes (excludes boot LUN):</span></span>

- <span data-ttu-id="95795-233">nfs    rw, vers=4, hard, timeo=600, rsize=1048576, wsize=1048576, intr, noatime, lock 0 0</span><span class="sxs-lookup"><span data-stu-id="95795-233">nfs    rw, vers=4, hard, timeo=600, rsize=1048576, wsize=1048576, intr, noatime, lock 0 0</span></span>

<span data-ttu-id="95795-234">這些掛接點設定在 /etc/hosts fstab 像下列圖形中顯示 hello:</span><span class="sxs-lookup"><span data-stu-id="95795-234">These mount points are configured in /etc/fstab like shown in hello following graphics:</span></span>

![HANA 大型執行個體單位中掛接磁碟區的 fstab](./media/hana-installation/image1_fstab.PNG)

<span data-ttu-id="95795-236">hello 的 hello 命令 df-h S72m HANA 大型執行個體單元上的輸出應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="95795-236">hello output of hello command df -h on a S72m HANA Large Instance unit would look like:</span></span>

![HANA 大型執行個體單位中掛接磁碟區的 fstab](./media/hana-installation/image2_df_output.PNG)


<span data-ttu-id="95795-238">hello 存放裝置控制器和 hello 大型執行個體戳記中的節點是同步的 tooNTP 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="95795-238">hello storage controller and nodes in hello Large Instance stamps are synchronized tooNTP servers.</span></span> <span data-ttu-id="95795-239">與您 hello SAP HANA Azure （大型執行個體） 單位和 Azure Vm 上的對 NTP 伺服器同步處理應該 hello 基礎結構與 Azure 或大型執行個體戳記中的 hello 計算單位之間沒有很多時間漂移現象。</span><span class="sxs-lookup"><span data-stu-id="95795-239">With you synchronizing hello SAP HANA on Azure (Large Instances) units and Azure VMs against an NTP server, there should be no significant time drift happening between hello infrastructure and hello compute units in Azure or Large Instance stamps.</span></span>

<span data-ttu-id="95795-240">順序 toooptimize 之下使用的 SAP HANA toohello 儲存區，您也應該設定 hello 遵循 SAP HANA 組態參數：</span><span class="sxs-lookup"><span data-stu-id="95795-240">In order toooptimize SAP HANA toohello storage used underneath, you should also set hello following SAP HANA configuration parameters:</span></span>

- <span data-ttu-id="95795-241">max_parallel_io_requests 128</span><span class="sxs-lookup"><span data-stu-id="95795-241">max_parallel_io_requests 128</span></span>
- <span data-ttu-id="95795-242">async_read_submit on</span><span class="sxs-lookup"><span data-stu-id="95795-242">async_read_submit on</span></span>
- <span data-ttu-id="95795-243">async_write_submit_active on</span><span class="sxs-lookup"><span data-stu-id="95795-243">async_write_submit_active on</span></span>
- <span data-ttu-id="95795-244">async_write_submit_blocks all</span><span class="sxs-lookup"><span data-stu-id="95795-244">async_write_submit_blocks all</span></span>
 
<span data-ttu-id="95795-245">向上 tooSPS12 SAP HANA 1.0 版本，這些參數可以中所述的 hello hello SAP HANA 資料庫，安裝期間設定[SAP 附註 #2267798 hello SAP HANA 資料庫的組態](https://launchpad.support.sap.com/#/notes/2267798)</span><span class="sxs-lookup"><span data-stu-id="95795-245">For SAP HANA 1.0 versions up tooSPS12, these parameters can be set during hello installation of hello SAP HANA database, as described in [SAP Note #2267798 - Configuration of hello SAP HANA Database](https://launchpad.support.sap.com/#/notes/2267798)</span></span>

<span data-ttu-id="95795-246">您也可以設定 hello 參數 hello SAP HANA 資料庫安裝後，使用 hello hdbparam 架構。</span><span class="sxs-lookup"><span data-stu-id="95795-246">You also can configure hello parameters after hello SAP HANA database installation by using hello hdbparam framework.</span></span> 

<span data-ttu-id="95795-247">SAP HANA 2.0，hello hdbparam framework 已被取代。</span><span class="sxs-lookup"><span data-stu-id="95795-247">With SAP HANA 2.0, hello hdbparam framework has been deprecated.</span></span> <span data-ttu-id="95795-248">因此您必須使用 SQL 命令來設定 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="95795-248">As a result hello parameters must be set using SQL commands.</span></span> <span data-ttu-id="95795-249">如需詳細資料，請參閱 [SAP 附註 #2399079：在 HANA 2 中已刪除 hdbparam (英文)](https://launchpad.support.sap.com/#/notes/2399079)。</span><span class="sxs-lookup"><span data-stu-id="95795-249">For details, see [SAP Note #2399079: Elimination of hdbparam in HANA 2](https://launchpad.support.sap.com/#/notes/2399079).</span></span>


## <a name="operating-system"></a><span data-ttu-id="95795-250">作業系統</span><span class="sxs-lookup"><span data-stu-id="95795-250">Operating system</span></span>

<span data-ttu-id="95795-251">交換空間的 hello 傳遞 OS 映像設定根據 toohello too2 GB [SAP 支援附註 #1999997 常見問題集： SAP HANA 記憶體](https://launchpad.support.sap.com/#/notes/1999997/E)。</span><span class="sxs-lookup"><span data-stu-id="95795-251">Swap space of hello delivered OS image is set too2 GB according toohello [SAP Support Note #1999997 - FAQ: SAP HANA Memory](https://launchpad.support.sap.com/#/notes/1999997/E).</span></span> <span data-ttu-id="95795-252">任何不同設定所需需要 toobe 設定由您的客戶。</span><span class="sxs-lookup"><span data-stu-id="95795-252">Any different setting desired needs toobe set by you as a customer.</span></span>

<span data-ttu-id="95795-253">[SUSE Linux Enterprise Server 12 SP1 針對 SAP 應用程式](https://www.suse.com/products/sles-for-sap/hana)是 Linux 安裝在 Azure （大型執行個體） 上的 SAP hana 的 hello 分佈。</span><span class="sxs-lookup"><span data-stu-id="95795-253">[SUSE Linux Enterprise Server 12 SP1 for SAP Applications](https://www.suse.com/products/sles-for-sap/hana) is hello distribution of Linux installed for SAP HANA on Azure (Large Instances).</span></span> <span data-ttu-id="95795-254">這個特定的分佈提供 SAP 特定功能&quot;hello 現成&quot;（包括預先設定的參數，有效地執行 SAP SLES 上）。</span><span class="sxs-lookup"><span data-stu-id="95795-254">This particular distribution provides SAP-specific capabilities &quot;out of hello box&quot; (including pre-set parameters for running SAP on SLES effectively).</span></span>

<span data-ttu-id="95795-255">請參閱[資源程式庫/白皮書](https://www.suse.com/products/sles-for-sap/resource-library#white-papers)hello SUSE 網站上和[SAP on SUSE](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE)上 hello SAP 社群網路 (SCN) 是否有數個實用的資源相關 toodeploying SLES （包括 hello 安裝上的 SAP HANA高可用性、 安全性強化特定 tooSAP 作業等等）。</span><span class="sxs-lookup"><span data-stu-id="95795-255">See [Resource Library/White Papers](https://www.suse.com/products/sles-for-sap/resource-library#white-papers) on hello SUSE website and [SAP on SUSE](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE) on hello SAP Community Network (SCN) for several useful resources related toodeploying SAP HANA on SLES (including hello set-up of High Availability, security hardening specific tooSAP operations, and more).</span></span>

<span data-ttu-id="95795-256">額外和有用的 SAP on SUSE 相關連結︰</span><span class="sxs-lookup"><span data-stu-id="95795-256">Additional and useful SAP on SUSE-related links:</span></span>

- [<span data-ttu-id="95795-257">SUSE Linux 網站上的 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="95795-257">SAP HANA on SUSE Linux Site</span></span>](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE)
- <span data-ttu-id="95795-258">[SAP 的最佳做法：加入佇列複寫 – SAP NetWeaver on SUSE Linux Enterprise 12](https://www.suse.com/docrepcontent/container.jsp?containerId=9113)。</span><span class="sxs-lookup"><span data-stu-id="95795-258">[Best Practice for SAP: Enqueue Replication – SAP NetWeaver on SUSE Linux Enterprise 12](https://www.suse.com/docrepcontent/container.jsp?containerId=9113).</span></span>
- <span data-ttu-id="95795-259">[ClamSAP – SLES Virus Protection for SAP](http://scn.sap.com/community/linux/blog/2014/04/14/clamsap--suse-linux-enterprise-server-integrates-virus-protection-for-sap) (包括 SLES 12 for SAP 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="95795-259">[ClamSAP – SLES Virus Protection for SAP](http://scn.sap.com/community/linux/blog/2014/04/14/clamsap--suse-linux-enterprise-server-integrates-virus-protection-for-sap) (including SLES 12 for SAP Applications).</span></span>

<span data-ttu-id="95795-260">SAP 支援附註適用於 tooimplementing SLES 12 上的 SAP HANA:</span><span class="sxs-lookup"><span data-stu-id="95795-260">SAP Support Notes applicable tooimplementing SAP HANA on SLES 12:</span></span>

- <span data-ttu-id="95795-261">[SAP 支援附註 #1944799 – SLES 作業系統安裝的 SAP HANA 指南](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)。</span><span class="sxs-lookup"><span data-stu-id="95795-261">[SAP Support Note #1944799 – SAP HANA Guidelines for SLES Operating System Installation](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html).</span></span>
- <span data-ttu-id="95795-262">[SAP 支援附註 #2205917 – 針對 SLES 12 for SAP 應用程式的 SAP HANA DB 建議作業系統設定](https://launchpad.support.sap.com/#/notes/2205917/E)。</span><span class="sxs-lookup"><span data-stu-id="95795-262">[SAP Support Note #2205917 – SAP HANA DB Recommended OS Settings for SLES 12 for SAP Applications](https://launchpad.support.sap.com/#/notes/2205917/E).</span></span>
- <span data-ttu-id="95795-263">[SAP 支援附註 #1984787 – SUSE Linux Enterprise Server 12：安裝注意事項](https://launchpad.support.sap.com/#/notes/1984787)。</span><span class="sxs-lookup"><span data-stu-id="95795-263">[SAP Support Note #1984787 – SUSE Linux Enterprise Server 12:  Installation Notes](https://launchpad.support.sap.com/#/notes/1984787).</span></span>
- <span data-ttu-id="95795-264">[SAP 支援附註 #171356 – 在 Linux 上的 SAP 軟體︰一般資訊](https://launchpad.support.sap.com/#/notes/1984787)。</span><span class="sxs-lookup"><span data-stu-id="95795-264">[SAP Support Note #171356 – SAP Software on Linux:  General Information](https://launchpad.support.sap.com/#/notes/1984787).</span></span>
- <span data-ttu-id="95795-265">[SAP 支援附註 #1391070 – Linux UUID 解決方案](https://launchpad.support.sap.com/#/notes/1391070)。</span><span class="sxs-lookup"><span data-stu-id="95795-265">[SAP Support Note #1391070 – Linux UUID Solutions](https://launchpad.support.sap.com/#/notes/1391070).</span></span>

<span data-ttu-id="95795-266">[Red Hat Enterprise Linux for SAP HANA](https://www.redhat.com/en/resources/red-hat-enterprise-linux-sap-hana) 是可供在 HANA Large Instances 上執行 SAP HANA 的另一個供應項目。</span><span class="sxs-lookup"><span data-stu-id="95795-266">[Red Hat Enterprise Linux for SAP HANA](https://www.redhat.com/en/resources/red-hat-enterprise-linux-sap-hana) is another offer for running SAP HANA on HANA Large Instances.</span></span> <span data-ttu-id="95795-267">版本 RHEL 6.7 和 7.2 均可使用。</span><span class="sxs-lookup"><span data-stu-id="95795-267">Releases of RHEL 6.7 and 7.2 are available.</span></span> 

<span data-ttu-id="95795-268">額外和有用的 SAP on Red Hat 相關連結︰</span><span class="sxs-lookup"><span data-stu-id="95795-268">Additional and useful SAP on Red Hat related links:</span></span>
- <span data-ttu-id="95795-269">[Red Hat Linux 網站上的 SAP HANA](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+Red+Hat)。</span><span class="sxs-lookup"><span data-stu-id="95795-269">[SAP HANA on Red Hat Linux Site](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+Red+Hat).</span></span>

<span data-ttu-id="95795-270">SAP 支援附註適用於 tooimplementing Red Hat 上的 SAP HANA:</span><span class="sxs-lookup"><span data-stu-id="95795-270">SAP Support Notes applicable tooimplementing SAP HANA on Red Hat:</span></span>

- <span data-ttu-id="95795-271">[SAP 支援附註 #2009879 - 適用於 Red Hat Enterprise Linux (RHEL) 作業系統的 SAP HANA 指南](https://launchpad.support.sap.com/#/notes/2009879/E)。</span><span class="sxs-lookup"><span data-stu-id="95795-271">[SAP Support Note #2009879 - SAP HANA Guidelines for Red Hat Enterprise Linux (RHEL) Operating System](https://launchpad.support.sap.com/#/notes/2009879/E).</span></span>
- <span data-ttu-id="95795-272">[SAP 支援附註 #2292690 - SAP HANA DB：適用於 RHEL 7 的建議作業系統設定](https://launchpad.support.sap.com/#/notes/2292690)。</span><span class="sxs-lookup"><span data-stu-id="95795-272">[SAP Support Note #2292690 - SAP HANA DB: Recommended OS settings for RHEL 7](https://launchpad.support.sap.com/#/notes/2292690).</span></span>
- <span data-ttu-id="95795-273">[SAP 支援附註 #2247020 - SAP HANA DB：適用於 RHEL 6.7 的建議作業系統設定](https://launchpad.support.sap.com/#/notes/2247020)。</span><span class="sxs-lookup"><span data-stu-id="95795-273">[SAP Support Note #2247020 - SAP HANA DB: Recommended OS settings for RHEL 6.7](https://launchpad.support.sap.com/#/notes/2247020).</span></span>
- <span data-ttu-id="95795-274">[SAP 支援附註 #1391070 – Linux UUID 解決方案](https://launchpad.support.sap.com/#/notes/1391070)。</span><span class="sxs-lookup"><span data-stu-id="95795-274">[SAP Support Note #1391070 – Linux UUID Solutions](https://launchpad.support.sap.com/#/notes/1391070).</span></span>
- <span data-ttu-id="95795-275">[SAP 支援附註 #2228351 - Linux：RHEL 6 或 SLES 11 上的 SAP HANA Database SPS 11 修訂版 110 (或更新版本)](https://launchpad.support.sap.com/#/notes/2228351)。</span><span class="sxs-lookup"><span data-stu-id="95795-275">[SAP Support Note #2228351 - Linux: SAP HANA Database SPS 11 revision 110 (or higher) on RHEL 6 or SLES 11](https://launchpad.support.sap.com/#/notes/2228351).</span></span>
- <span data-ttu-id="95795-276">[SAP 支援附註 #2397039 - 常見問題集：SAP on RHEL](https://launchpad.support.sap.com/#/notes/2397039)。</span><span class="sxs-lookup"><span data-stu-id="95795-276">[SAP Support Note #2397039 - FAQ: SAP on RHEL](https://launchpad.support.sap.com/#/notes/2397039).</span></span>
- <span data-ttu-id="95795-277">[SAP 支援附註 #1496410 - Red Hat Enterprise Linux 6.x：安裝和升級](https://launchpad.support.sap.com/#/notes/1496410)。</span><span class="sxs-lookup"><span data-stu-id="95795-277">[SAP Support Note #1496410 - Red Hat Enterprise Linux 6.x: Installation and Upgrade](https://launchpad.support.sap.com/#/notes/1496410).</span></span>
- <span data-ttu-id="95795-278">[SAP 支援附註 #2002167 - Red Hat Enterprise Linux 7.x：安裝和升級](https://launchpad.support.sap.com/#/notes/2002167)。</span><span class="sxs-lookup"><span data-stu-id="95795-278">[SAP Support Note #2002167 - Red Hat Enterprise Linux 7.x: Installation and Upgrade](https://launchpad.support.sap.com/#/notes/2002167).</span></span>

## <a name="time-synchronization"></a><span data-ttu-id="95795-279">時間同步處理</span><span class="sxs-lookup"><span data-stu-id="95795-279">Time synchronization</span></span>

<span data-ttu-id="95795-280">Hello 各種元件組成 hello SAP 系統在 hello SAP NetWeaver 架構上建置的 SAP 應用程式是機密的時間差異。</span><span class="sxs-lookup"><span data-stu-id="95795-280">SAP applications built on hello SAP NetWeaver architecture are sensitive on time differences for hello various components that comprise hello SAP system.</span></span> <span data-ttu-id="95795-281">簡短的 SAP ABAP 傾印的 ZDATE hello 錯誤標題\_大\_時間\_差異是可能熟悉的內容，這些簡短的傾印時，會出現 hello 不同的伺服器或 Vm 的系統時間會變動太距離。</span><span class="sxs-lookup"><span data-stu-id="95795-281">SAP ABAP short dumps with hello error title of ZDATE\_LARGE\_TIME\_DIFF are likely familiar, as these short dumps appear when hello system time of different servers or VMs is drifting too far apart.</span></span>

<span data-ttu-id="95795-282">在 Azure （大型執行個體），在 Azure 規定 &#39; 中完成的時間同步處理上的 SAP hana t 套用 toohello hello 大型執行個體戳記中的計算單位。</span><span class="sxs-lookup"><span data-stu-id="95795-282">For SAP HANA on Azure (Large Instances), time synchronization done in Azure doesn&#39;t apply toohello compute units in hello Large Instance stamps.</span></span> <span data-ttu-id="95795-283">這項同步處理並不適用於在原生 Azure VM 中執行 SAP 應用程式，因為 Azure 可確保正確同步處理系統時間。</span><span class="sxs-lookup"><span data-stu-id="95795-283">This synchronization is not applicable for running SAP applications in native Azure VMs, as Azure ensures a system&#39;s time is properly synchronized.</span></span> <span data-ttu-id="95795-284">如此一來，個別的時間必須設定伺服器，可供 Azure Vm 上執行的 SAP 應用程式伺服器和 hello SAP HANA 資料庫 HANA 大型執行個體上執行的執行個體。</span><span class="sxs-lookup"><span data-stu-id="95795-284">As a result, a separate time server must be set up that can be used by SAP application servers running on Azure VMs and hello SAP HANA database instances running on HANA Large Instances.</span></span> <span data-ttu-id="95795-285">在大型執行個體戳記中的 hello 儲存體基礎結構是與 NTP 伺服器同步處理的時間。</span><span class="sxs-lookup"><span data-stu-id="95795-285">hello storage infrastructure in Large Instance stamps is time synchronized with NTP servers.</span></span>

## <a name="setting-up-smt-server-for-suse-linux"></a><span data-ttu-id="95795-286">設定 SUSE Linux 的 SMT 伺服器</span><span class="sxs-lookup"><span data-stu-id="95795-286">Setting up SMT server for SUSE Linux</span></span>
<span data-ttu-id="95795-287">SAP HANA 大型執行個體沒有直接連線 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="95795-287">SAP HANA Large Instances don't have direct connectivity toohello Internet.</span></span> <span data-ttu-id="95795-288">因此它不是簡單的程序 tooregister hello OS 提供者與 toodownload 這類的單位，並套用修補程式。</span><span class="sxs-lookup"><span data-stu-id="95795-288">Hence it is not a straightforward process tooregister such a unit with hello OS provider and toodownload and apply patches.</span></span> <span data-ttu-id="95795-289">SUSE Linux 的 hello 案例中，在其中一種解決方案可能是 tooset SMT 台伺服器，Azure VM 中。</span><span class="sxs-lookup"><span data-stu-id="95795-289">In hello case of SUSE Linux, one solution could be tooset up an SMT server in an Azure VM.</span></span> <span data-ttu-id="95795-290">而 hello Azure VM 需要 toobe 裝載於 Azure 的 VNet，也就是連接的 toohello HANA 大型執行個體。</span><span class="sxs-lookup"><span data-stu-id="95795-290">Whereas hello Azure VM needs toobe hosted in an Azure VNet, which is connected toohello HANA Large Instance.</span></span> <span data-ttu-id="95795-291">與這類 SMT 伺服器 hello HANA 大型執行個體單位無法註冊，並下載修補程式。</span><span class="sxs-lookup"><span data-stu-id="95795-291">With such an SMT server, hello HANA Large Instance unit could register and download patches.</span></span> 

<span data-ttu-id="95795-292">SUSE 提供大量有關 [Subscription Management Tool for SLES 12 SP2](https://www.suse.com/documentation/sles-12/pdfdoc/book_smt/book_smt.pdf) (SLES 12 SP2 訂用帳戶管理工具) 的指南。</span><span class="sxs-lookup"><span data-stu-id="95795-292">SUSE provides a larger guide on their [Subscription Management Tool for SLES 12 SP2](https://www.suse.com/documentation/sles-12/pdfdoc/book_smt/book_smt.pdf).</span></span> 

<span data-ttu-id="95795-293">成套 hello HANA 大型執行個體，可滿足 hello 工作 SMT 伺服器安裝，您需要：</span><span class="sxs-lookup"><span data-stu-id="95795-293">As precondition for hello installation of an SMT server that fulfills hello task for HANA Large Instance, you would need:</span></span>

- <span data-ttu-id="95795-294">Azure VNet 的連接的 toohello HANA 大型執行個體 ER 循環。</span><span class="sxs-lookup"><span data-stu-id="95795-294">An Azure VNet that is connected toohello HANA Large Instance ER circuit.</span></span>
- <span data-ttu-id="95795-295">與組織相關聯的 SUSE 帳戶。</span><span class="sxs-lookup"><span data-stu-id="95795-295">A SUSE account that is associated with an organization.</span></span> <span data-ttu-id="95795-296">而 hello 組織需要 toohave 某些有效 SUSE 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="95795-296">Whereas hello organization would need toohave some valid SUSE subscription.</span></span>

### <a name="installation-of-smt-server-on-azure-vm"></a><span data-ttu-id="95795-297">在 Azure VM 上安裝 SMT 伺服器</span><span class="sxs-lookup"><span data-stu-id="95795-297">Installation of SMT server on Azure VM</span></span>

<span data-ttu-id="95795-298">在此步驟中，您可以安裝在 Azure VM 中的 hello SMT 伺服器。</span><span class="sxs-lookup"><span data-stu-id="95795-298">In this step, you install hello SMT server in an Azure VM.</span></span> <span data-ttu-id="95795-299">hello 第一個量值是在 toohello toolog [SUSE 客戶中心](https://scc.suse.com/)</span><span class="sxs-lookup"><span data-stu-id="95795-299">hello first measure is toolog in toohello [SUSE Customer Center](https://scc.suse.com/)</span></span>

<span data-ttu-id="95795-300">當您登入，請移 tooOrganization--> 組織的認證。</span><span class="sxs-lookup"><span data-stu-id="95795-300">As you are logged in, go tooOrganization--> Organization Credentials.</span></span> <span data-ttu-id="95795-301">在該區段中，您應該尋找必要 tooset hello SMT 伺服器 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="95795-301">In that section you should find hello credentials that are necessary tooset up hello SMT server.</span></span>

<span data-ttu-id="95795-302">hello 第三個步驟是 tooinstall hello Azure VNet 中的 SUSE Linux VM。</span><span class="sxs-lookup"><span data-stu-id="95795-302">hello third step is tooinstall a SUSE Linux VM in hello Azure VNet.</span></span> <span data-ttu-id="95795-303">toodeploy hello VM 需要 Azure 的 SLES 12 SP2 圖庫映像。</span><span class="sxs-lookup"><span data-stu-id="95795-303">toodeploy hello VM, take a SLES 12 SP2 gallery image of Azure.</span></span> <span data-ttu-id="95795-304">Hello 部署程序，在未定義的 DNS 名稱，而且不會使用靜態 IP 位址這個螢幕擷取畫面所示</span><span class="sxs-lookup"><span data-stu-id="95795-304">In hello deployment process, don't define a DNS name and do not use static IP addresses as seen in this screen shot</span></span>

![SMT 伺服器的 VM 部署](./media/hana-installation/image3_vm_deployment.png)

<span data-ttu-id="95795-306">hello 已部署的 VM 是較小的 VM，並且收到 hello 的 10.34.1.4 Azure VNet 中的 hello 內部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="95795-306">hello deployed VM was a smaller VM and got hello internal IP address in hello Azure VNet of 10.34.1.4.</span></span> <span data-ttu-id="95795-307">Hello VM 的名稱為 smtserver。</span><span class="sxs-lookup"><span data-stu-id="95795-307">Name of hello VM was smtserver.</span></span> <span data-ttu-id="95795-308">Hello 安裝之後，已核取 hello 連線 toohello HANA 大型執行個體單元。</span><span class="sxs-lookup"><span data-stu-id="95795-308">After hello installation, hello connectivity toohello HANA Large instance unit(s) was checked.</span></span> <span data-ttu-id="95795-309">取決於您的組織名稱解析方式您可能需要等/主機的 hello Azure VM 中的 hello HANA 大型執行個體單位 tooconfigure 解析度。</span><span class="sxs-lookup"><span data-stu-id="95795-309">Dependent on how you organized name resolution you might need tooconfigure resolution of hello HANA Large Instance units in etc/hosts of hello Azure VM.</span></span> <span data-ttu-id="95795-310">加入額外的磁碟 toohello 即將 toobe 用 toohold hello 修補程式的 VM。</span><span class="sxs-lookup"><span data-stu-id="95795-310">Add an additional disk toohello VM that is going toobe used toohold hello patches.</span></span> <span data-ttu-id="95795-311">hello 開機磁碟本身可能太小。</span><span class="sxs-lookup"><span data-stu-id="95795-311">hello boot disk itself could be too small.</span></span> <span data-ttu-id="95795-312">在示範 hello 的情況下，hello 磁碟了掛接太/srv/www/htdocs hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="95795-312">In hello case demonstrated, hello disk got mounted too/srv/www/htdocs as shown in hello following screenshot.</span></span> <span data-ttu-id="95795-313">100 GB 的磁碟應已足夠。</span><span class="sxs-lookup"><span data-stu-id="95795-313">A 100 GB disk should suffice.</span></span>

![SMT 伺服器的 VM 部署](./media/hana-installation/image4_additional_disk_on_smtserver.PNG)

<span data-ttu-id="95795-315">登入 toohello HANA 大型執行個體單元、 維護 /etc/hosts 並檢查是否可達到 hello 應該 toorun hello SMT 伺服器 hello 網路上的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="95795-315">Log in toohello HANA Large Instance unit(s), maintain /etc/hosts and check whether you can reach hello Azure VM that is supposed toorun hello SMT server over hello network.</span></span>

<span data-ttu-id="95795-316">這項檢查已成功完成之後，您會需要 toolog toohello hello SMT 伺服器上執行的 Azure VM 中。</span><span class="sxs-lookup"><span data-stu-id="95795-316">After this check is done successfully, you need toolog in toohello Azure VM that should run hello SMT server.</span></span> <span data-ttu-id="95795-317">如果您使用 putty toolog toohello VM 中，您需要 tooexecute 這一系列命令的 bash 視窗中：</span><span class="sxs-lookup"><span data-stu-id="95795-317">If you are using putty toolog in toohello VM, you need tooexecute this sequence of commands in your bash window:</span></span>

```
cd ~
echo "export NCURSES_NO_UTF8_ACS=1" >> .bashrc
```

<span data-ttu-id="95795-318">在執行這些命令之後, 重新啟動您 bash tooactivate hello 的設定。</span><span class="sxs-lookup"><span data-stu-id="95795-318">After executing these commands, restart your bash tooactivate hello settings.</span></span> <span data-ttu-id="95795-319">然後啟動 YAST。</span><span class="sxs-lookup"><span data-stu-id="95795-319">Then start YAST.</span></span>

<span data-ttu-id="95795-320">在 YAST，請前往 tooSoftware 維護 smt 搜尋。</span><span class="sxs-lookup"><span data-stu-id="95795-320">In YAST, go tooSoftware Maintenance and search for smt.</span></span> <span data-ttu-id="95795-321">選取 smt，自動切換 tooyast2 smt 如下所示</span><span class="sxs-lookup"><span data-stu-id="95795-321">Select smt, which switches automatically tooyast2-smt as shown below</span></span>

![yast 中的 SMT](./media/hana-installation/image5_smt_in_yast.PNG)


<span data-ttu-id="95795-323">接受 hello hello smtserver 上安裝的選取範圍。</span><span class="sxs-lookup"><span data-stu-id="95795-323">Accept hello selection for installation on hello smtserver.</span></span> <span data-ttu-id="95795-324">安裝之後，移 toohello SMT 伺服器組態，並輸入 hello SUSE 客戶中心您稍早擷取 hello 組織認證。</span><span class="sxs-lookup"><span data-stu-id="95795-324">Once installed, go toohello SMT server configuration and enter hello organizational credentials from hello SUSE Customer Center you retrieved earlier.</span></span> <span data-ttu-id="95795-325">也為 hello SMT 伺服器 URL 輸入您的 Azure VM 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="95795-325">Also enter your Azure VM hostname as hello SMT Server URL.</span></span> <span data-ttu-id="95795-326">在此示範中，它會是 https://smtserver hello 下一個圖形中所示。</span><span class="sxs-lookup"><span data-stu-id="95795-326">In this demonstration, it was https://smtserver as displayed in hello next graphics.</span></span>

![SMT 伺服器組態](./media/hana-installation/image6_configuration_of_smtserver1.png)

<span data-ttu-id="95795-328">在下一個步驟中，您會需要 tootest 是否 hello 連接 toohello SUSE 客戶 Center 的運作方式。</span><span class="sxs-lookup"><span data-stu-id="95795-328">As next step, you need tootest whether hello connection toohello SUSE Customer Center works.</span></span> <span data-ttu-id="95795-329">您在 hello 下列圖形，在 hello 示範案例中，看到能夠運作。</span><span class="sxs-lookup"><span data-stu-id="95795-329">As you see in hello following graphics, in hello demonstration case, it did work.</span></span>

![測試連接 tooSUSE 客戶 Center](./media/hana-installation/image7_test_connect.png)

<span data-ttu-id="95795-331">一次 hello SMT 安裝程式啟動時，您會需要 tooprovide 資料庫密碼。</span><span class="sxs-lookup"><span data-stu-id="95795-331">Once hello SMT setup starts, you need tooprovide a database password.</span></span> <span data-ttu-id="95795-332">因為這是新的安裝，您需要 toodefine hello 下一個圖形中所示的密碼。</span><span class="sxs-lookup"><span data-stu-id="95795-332">Since it is a new installation, you need toodefine that password as shown in hello next graphics.</span></span>

![定義資料庫密碼](./media/hana-installation/image8_define_db_passwd.PNG)

<span data-ttu-id="95795-334">您擁有 hello 下一步互動時，取得建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="95795-334">hello next interaction you have is when a certificate gets created.</span></span> <span data-ttu-id="95795-335">瀏覽 hello 對話方塊如下所示，hello 步驟應該繼續進行。</span><span class="sxs-lookup"><span data-stu-id="95795-335">Go through hello dialog as shown next and hello step should proceed.</span></span>

![建立 SMT 伺服器憑證](./media/hana-installation/image9_certificate_creation.PNG)

<span data-ttu-id="95795-337">可能會有結尾 hello hello 組態執行同步處理檢查' hello 步驟中所花費幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="95795-337">There might be some minutes spent in hello step of 'Run synchronization check' at hello end of hello configuration.</span></span> <span data-ttu-id="95795-338">Hello 安裝及設定之後的 hello SMT 伺服器，您應該會發現下 hello 掛接點 /srv/www/htdocs hello 目錄儲存機制/再加上一些子目錄下儲存機制。</span><span class="sxs-lookup"><span data-stu-id="95795-338">After hello installation and configuration of hello SMT server, you should find hello directory repo under hello mount point /srv/www/htdocs/ plus some sub-directories under repo.</span></span> 

<span data-ttu-id="95795-339">重新啟動 hello SMT 伺服器及其相關的服務與這些命令。</span><span class="sxs-lookup"><span data-stu-id="95795-339">Restart hello SMT server and its related services with these commands.</span></span>

```
rcsmt restart
systemctl restart smt.service
systemctl restart apache2
```

### <a name="download-of-packages-onto-smt-server"></a><span data-ttu-id="95795-340">將套件下載到 SMT 伺服器</span><span class="sxs-lookup"><span data-stu-id="95795-340">Download of packages onto SMT server</span></span>

<span data-ttu-id="95795-341">在所有 hello 重新啟動服務、 選取 hello 使用 Yast SMT 管理中的適當套件。</span><span class="sxs-lookup"><span data-stu-id="95795-341">After all hello services are restarted, select hello appropriate packages in SMT Management using Yast.</span></span> <span data-ttu-id="95795-342">hello 套件選取項目取決於 hello hello HANA 大型執行個體伺服器的作業系統映像以及不 hello SLES 版本或 hello VM 執行 hello SMT 伺服器的版本。</span><span class="sxs-lookup"><span data-stu-id="95795-342">hello package selection depends on hello OS image of hello HANA Large Instance  server and not on hello SLES release or version of hello VM running hello SMT server.</span></span> <span data-ttu-id="95795-343">Hello 選取畫面的範例如下所示。</span><span class="sxs-lookup"><span data-stu-id="95795-343">An example of hello selection screen is shown below.</span></span>

![選取套件](./media/hana-installation/image10_select_packages.PNG)

<span data-ttu-id="95795-345">一旦您完成 hello 套件選取項目時，您會需要 toostart hello 初始複本的 hello 選取封裝 toohello SMT 伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="95795-345">Once you are finished with hello package selection, you need toostart hello initial copy of hello select packages toohello SMT server you set up.</span></span> <span data-ttu-id="95795-346">在使用 hello 命令 smt 鏡像如下所示的 hello 介面中觸發這個複本</span><span class="sxs-lookup"><span data-stu-id="95795-346">This copy is triggered in hello shell using hello command smt-mirror as shown below</span></span>


![下載封裝 tooSMT 伺服器](./media/hana-installation/image11_download_packages.PNG)

<span data-ttu-id="95795-348">您看到上方，hello 封裝應該複製到 hello hello 掛接點 /srv/www/htdocs 下建立的目錄。</span><span class="sxs-lookup"><span data-stu-id="95795-348">As you see above, hello packages should get copied into hello directories created under hello mount point /srv/www/htdocs.</span></span> <span data-ttu-id="95795-349">此程序需要一會兒。</span><span class="sxs-lookup"><span data-stu-id="95795-349">This process can take a while.</span></span> <span data-ttu-id="95795-350">取決於您選取的套件數目，就無法在 tooone 小時或更多。</span><span class="sxs-lookup"><span data-stu-id="95795-350">Dependent on how many packages you select, it could take up tooone hour or more.</span></span>
<span data-ttu-id="95795-351">如同此程序完成時，您會需要 toomove toohello SMT 用戶端安裝程式。</span><span class="sxs-lookup"><span data-stu-id="95795-351">As this process finishes, you need toomove toohello SMT client setup.</span></span> 

### <a name="set-up-hello-smt-client-on-hana-large-instance-units"></a><span data-ttu-id="95795-352">設定單元 HANA 大型執行個體上的 hello SMT 用戶端</span><span class="sxs-lookup"><span data-stu-id="95795-352">Set up hello SMT client on HANA Large Instance units</span></span>

<span data-ttu-id="95795-353">hello 用戶端在此情況下是 hello HANA 大型執行個體單位。</span><span class="sxs-lookup"><span data-stu-id="95795-353">hello client(s) in this case are hello HANA Large Instance units.</span></span> <span data-ttu-id="95795-354">hello SMT server 安裝程式會複製到 hello Azure VM 的 hello 指令碼 clientSetup4SMT.sh。</span><span class="sxs-lookup"><span data-stu-id="95795-354">hello SMT server setup copied hello script clientSetup4SMT.sh into hello Azure VM.</span></span> <span data-ttu-id="95795-355">將該指令碼複製 toohello HANA 大型執行個體單元要 tooconnect tooyour SMT 伺服器。</span><span class="sxs-lookup"><span data-stu-id="95795-355">Copy that script over toohello HANA Large Instance unit you want tooconnect tooyour SMT server.</span></span> <span data-ttu-id="95795-356">請使用 hello-h 選項啟動 hello 指令碼，並提供做為參數 hello SMT 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="95795-356">Start hello script with hello -h option and give it as parameter hello name of your SMT server.</span></span> <span data-ttu-id="95795-357">在此範例 smtserver 中。</span><span class="sxs-lookup"><span data-stu-id="95795-357">In this example smtserver.</span></span>

![設定 SMT 用戶端](./media/hana-installation/image12_configure_client.PNG)

<span data-ttu-id="95795-359">可能的案例，其中 hello hello 憑證從用戶端 hello hello 伺服器載入成功，但 hello 註冊失敗，如下所示。</span><span class="sxs-lookup"><span data-stu-id="95795-359">There might be a scenario where hello load of hello certificate from hello server by hello client succeeded, but hello registration failed as shown below.</span></span>

![用戶端註冊失敗](./media/hana-installation/image13_registration_failed.PNG)

<span data-ttu-id="95795-361">如果 hello 註冊失敗，請閱讀本[SUSE 支援文件](https://www.suse.com/de-de/support/kb/doc/?id=7006024)並執行 hello 那里所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="95795-361">If hello registration failed, read this [SUSE support document](https://www.suse.com/de-de/support/kb/doc/?id=7006024) and execute hello steps described there.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="95795-362">做為伺服器名稱，則會需要 tooprovide hello 名稱 hello VM，在此案例的 smtserver，不含 hello 完整的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="95795-362">As server name you need tooprovide hello name of hello VM, in this case smtserver, without hello fully qualified domain name.</span></span> <span data-ttu-id="95795-363">只要 hello VM 名稱運作。</span><span class="sxs-lookup"><span data-stu-id="95795-363">Just hello VM name works.</span></span> 

<span data-ttu-id="95795-364">在執行這些步驟之後，您需要下列命令在 hello HANA 大型執行個體單元 tooexecute hello</span><span class="sxs-lookup"><span data-stu-id="95795-364">After these steps have been executed, you need tooexecute hello following command on hello HANA Large Instance unit</span></span>

```
SUSEConnect –cleanup
```

> [!Note] 
> <span data-ttu-id="95795-365">在我們的測試，我們一律必須 toowait 幾分鐘的時間之後該步驟。</span><span class="sxs-lookup"><span data-stu-id="95795-365">In our tests we always had toowait a few minutes after that step.</span></span> <span data-ttu-id="95795-366">hello 立即執行 clientSetup4SMT.sh hello 矯正措施中所述 hello SUSE 發行項，以結束該 hello 憑證不是有效尚未的訊息。</span><span class="sxs-lookup"><span data-stu-id="95795-366">hello immediate execution clientSetup4SMT.sh, after hello corrective measures described in hello SUSE article, ended with messages that hello certificate would not be valid yet.</span></span> <span data-ttu-id="95795-367">通常等 5-10 分鐘後再執行 clientSetup4SMT.sh，就可以順利完成用戶端組態。</span><span class="sxs-lookup"><span data-stu-id="95795-367">Waiting for 5-10 minutes usually and executing clientSetup4SMT.sh ended in a successful client configuration.</span></span>

<span data-ttu-id="95795-368">如果您需要 toofix hello 步驟 hello SUSE 發行項所根據的 hello 問題，您需要 toorestart clientSetup4SMT.sh hello HANA 大型執行個體單位上的一次。</span><span class="sxs-lookup"><span data-stu-id="95795-368">If you ran into hello issue that you needed toofix based on hello steps of hello SUSE article, you need toorestart clientSetup4SMT.sh on hello HANA Large Instance unit again.</span></span> <span data-ttu-id="95795-369">現在它應該如下所示成功完成。</span><span class="sxs-lookup"><span data-stu-id="95795-369">Now it should finish successfully as shown below.</span></span>

![用戶端註冊成功](./media/hana-installation/image14_finish_client_config.PNG)

<span data-ttu-id="95795-371">有了這個步驟中，您可以設定對您在 hello Azure VM 中安裝的 hello SMT 伺服器 hello HANA 大型執行個體單元 tooconnect hello SMT 用戶端。</span><span class="sxs-lookup"><span data-stu-id="95795-371">With this step, you configured hello SMT client of hello HANA Large Instance unit tooconnect against hello SMT server you installed in hello Azure VM.</span></span> <span data-ttu-id="95795-372">您現在可以採用 'zypper up' 或 'zypper 中的' tooinstall OS 修補程式 tooHANA 大型執行個體，或安裝其他的封裝。</span><span class="sxs-lookup"><span data-stu-id="95795-372">You now can take 'zypper up' or 'zypper in' tooinstall OS patches tooHANA Large Instances or install additional packages.</span></span> <span data-ttu-id="95795-373">應該已知道，您只可以讓您先下載 hello SMT 伺服器的修補程式。</span><span class="sxs-lookup"><span data-stu-id="95795-373">It is understood that you only can get patches that you downloaded before on hello SMT server.</span></span>


## <a name="example-of-an-sap-hana-installation-on-hana-large-instances"></a><span data-ttu-id="95795-374">範例：在 HANA 大型執行個體上安裝 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="95795-374">Example of an SAP HANA installation on HANA Large Instances</span></span>
<span data-ttu-id="95795-375">本節說明如何 tooinstall SAP HANA HANA 大型執行個體單元上的。</span><span class="sxs-lookup"><span data-stu-id="95795-375">This section illustrates how tooinstall SAP HANA on a HANA Large Instance unit.</span></span> <span data-ttu-id="95795-376">hello 啟動狀態，我們必須看起來像：</span><span class="sxs-lookup"><span data-stu-id="95795-376">hello start state we have look  like:</span></span>

- <span data-ttu-id="95795-377">提供 Microsoft 所有的 hello 資料 toodeploy 您 SAP HANA 大型執行個體。</span><span class="sxs-lookup"><span data-stu-id="95795-377">You provided Microsoft all hello data toodeploy you an SAP HANA Large Instance.</span></span>
- <span data-ttu-id="95795-378">您可以從 Microsoft 收到 hello SAP HANA 大型執行個體。</span><span class="sxs-lookup"><span data-stu-id="95795-378">You received hello SAP HANA Large Instance from Microsoft.</span></span>
- <span data-ttu-id="95795-379">您建立 Azure VNet 連接的 tooyour 在內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="95795-379">You created an Azure VNet that is connected tooyour on-premise network.</span></span>
- <span data-ttu-id="95795-380">連接 HANA 大型執行個體 toohello 的 hello ExpressRotue 電路相同 Azure VNet。</span><span class="sxs-lookup"><span data-stu-id="95795-380">You connected hello ExpressRotue circuit for HANA Large Instances toohello same Azure VNet.</span></span>
- <span data-ttu-id="95795-381">您安裝了 Azure VM 用做為 HANA 大型執行個體的跳躍方塊。</span><span class="sxs-lookup"><span data-stu-id="95795-381">You installed an Azure VM you use as a jump box for HANA Large Instances.</span></span>
- <span data-ttu-id="95795-382">您確定您可以連接從 hello 跳躍方塊 tooyour HANA 大型執行個體單位，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="95795-382">You made sure that you can connect from hello jump box tooyour HANA Large Instance unit and vice versa.</span></span>
- <span data-ttu-id="95795-383">您可以檢查是否所有 hello 必要的封裝，並安裝修補程式。</span><span class="sxs-lookup"><span data-stu-id="95795-383">You checked whether all hello necessary packages and patches are installed.</span></span>
- <span data-ttu-id="95795-384">您可以閱讀 hello SAP 附註和文件之有關 HANA hello 您正在使用，並確定所選擇的 hello HANA 版本 hello 作業系統版本上支援的作業系統上的安裝。</span><span class="sxs-lookup"><span data-stu-id="95795-384">You read hello SAP notes and documentations regarding HANA installation on hello OS you are using and made sure that hello HANA release of choice is supported on hello OS release.</span></span>

<span data-ttu-id="95795-385">Hello 下一個序列中所示為 hello 下載 hello HANA 安裝封裝 toohello 跳躍方塊 VM，並且在 Windows 作業系統上，hello 封裝 toohello HANA 大型執行個體單元 hello 複本和 hello 一連串 hello 安裝程式在此情況下執行。</span><span class="sxs-lookup"><span data-stu-id="95795-385">What is shown in hello next sequences is hello download of hello HANA installation packages toohello jump box VM, in this case running on a Windows OS, hello copy of hello packages toohello HANA Large Instance unit and hello sequence of hello setup.</span></span>

### <a name="download-of-hello-sap-hana-installation-bits"></a><span data-ttu-id="95795-386">Hello SAP HANA 安裝 bits 下載</span><span class="sxs-lookup"><span data-stu-id="95795-386">Download of hello SAP HANA installation bits</span></span>
<span data-ttu-id="95795-387">由於 hello HANA 大型執行個體單位無法直接連線 toohello 網際網路，您無法直接下載 hello 安裝封裝從 SAP toohello HANA 大型執行個體 VM。</span><span class="sxs-lookup"><span data-stu-id="95795-387">Since hello HANA Large Instance units don't have direct connectivity toohello internet, you can't directly download hello installation packages from SAP toohello HANA Large Instance VM.</span></span> <span data-ttu-id="95795-388">tooovercome hello 遺漏直接網際網路連線，您需要 hello 跳躍方塊。</span><span class="sxs-lookup"><span data-stu-id="95795-388">tooovercome hello missing direct internet connectivity, you need hello jump box.</span></span> <span data-ttu-id="95795-389">您下載 hello 封裝 toohello 跳躍方塊 VM。</span><span class="sxs-lookup"><span data-stu-id="95795-389">You download hello packages toohello jump box VM.</span></span>

<span data-ttu-id="95795-390">在訂單 toodownload hello HANA 安裝封裝，您將需要 SAP S 使用者或其他使用者，可讓您 tooaccess hello SAP Marketplace。</span><span class="sxs-lookup"><span data-stu-id="95795-390">In order toodownload hello HANA installation packages, you need an SAP S-user or other user, which allows you tooaccess hello SAP Marketplace.</span></span> <span data-ttu-id="95795-391">登入之後，請完成這一系列的畫面：</span><span class="sxs-lookup"><span data-stu-id="95795-391">Go through this sequence of screens after logging in:</span></span>

<span data-ttu-id="95795-392">跳過[SAP 服務 Marketplace](https://support.sap.com/en/index.html) > 按一下 下載軟體 > 安裝與升級 > 依字母順序排列索引 > 下 H-SAP HANA 平台版本 > SAP HANA 平台版本 2.0 > 安裝 > 下載 hello下列檔案</span><span class="sxs-lookup"><span data-stu-id="95795-392">Go too[SAP Service Marketplace](https://support.sap.com/en/index.html) > Click Download Software > Installations and Upgrade >By Alphabetical Index >Under H – SAP HANA Platform Edition > SAP HANA Platform Edition 2.0 > Installation > Download hello following files</span></span>

![下載 HANA 安裝](./media/hana-installation/image16_download_hana.PNG)

<span data-ttu-id="95795-394">在 hello 示範案例中，我們會下載 SAP HANA 2.0 安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="95795-394">In hello demonstration case, we downloaded SAP HANA 2.0 installation packages.</span></span> <span data-ttu-id="95795-395">Hello Azure 跳躍方塊 VM，您可以展開 hello 自我解壓縮的封存到 hello 目錄，如下所示。</span><span class="sxs-lookup"><span data-stu-id="95795-395">On hello Azure jump box VM, you expand hello self-extracting archives into hello directory as shown below.</span></span>

![解壓縮 HANA 安裝](./media/hana-installation/image17_extract_hana.PNG)

<span data-ttu-id="95795-397">Hello 封存解壓縮，因為複製 hello 51052030，為您建立的目錄中的 hello /hana/shared 磁碟區 toohello HANA 大型執行個體單元上方 hello 案例中的 hello 擷取所建立的目錄。</span><span class="sxs-lookup"><span data-stu-id="95795-397">As hello archives are extracted, copy hello directory created by hello extraction, in hello case above 51052030, toohello HANA Large instance unit into hello /hana/shared volume into a directory you created.</span></span>

> [!Important]
> <span data-ttu-id="95795-398">請勿將 hello 安裝套件複製到 hello 根或開機 LUN，因為空間有限，而且必須由其他處理序 toobe。</span><span class="sxs-lookup"><span data-stu-id="95795-398">Do Not copy hello installation packages into hello root or boot LUN since space is limited and needs toobe used by other processes as well.</span></span>


### <a name="install-sap-hana-on-hello-hana-large-instance-unit"></a><span data-ttu-id="95795-399">在 hello HANA 大型執行個體單位上安裝 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="95795-399">Install SAP HANA on hello HANA Large Instance unit</span></span>
<span data-ttu-id="95795-400">順序 tooinstall SAP HANA，您需要在 toolog 為使用者的根。</span><span class="sxs-lookup"><span data-stu-id="95795-400">In order tooinstall SAP HANA, you need toolog in as user root.</span></span> <span data-ttu-id="95795-401">只有根有足夠的權限 tooinstall SAP HANA。</span><span class="sxs-lookup"><span data-stu-id="95795-401">Only root has enough permissions tooinstall SAP HANA.</span></span>
<span data-ttu-id="95795-402">您需要 toodo hello 第一件事是 tooset hello 目錄複製到/hana/共用權限。</span><span class="sxs-lookup"><span data-stu-id="95795-402">hello first thing you need toodo is tooset permissions on hello directory you copied over into /hana/shared.</span></span> <span data-ttu-id="95795-403">需要像 tooset hello 權限。</span><span class="sxs-lookup"><span data-stu-id="95795-403">hello permissions need tooset like</span></span>

```
chmod –R 744 <Installation bits folder>
```

<span data-ttu-id="95795-404">如果您想 tooinstall SAP HANA 使用 hello 圖形化安裝程式，hello gtk2 封裝需求 toobe hello HANA 大型執行個體上安裝。</span><span class="sxs-lookup"><span data-stu-id="95795-404">If you want tooinstall SAP HANA using hello graphical setup, hello gtk2 package needs toobe installed on hello HANA Large Instances.</span></span> <span data-ttu-id="95795-405">檢查是否已安裝與 hello 命令</span><span class="sxs-lookup"><span data-stu-id="95795-405">Check whether it is installed with hello command</span></span>

```
rpm –qa | grep gtk2
```

<span data-ttu-id="95795-406">在進一步步驟中，我們會示範 hello SAP HANA 安裝 hello 圖形化使用者介面。</span><span class="sxs-lookup"><span data-stu-id="95795-406">In further steps, we are demonstrating hello SAP HANA setup with hello graphical user interface.</span></span> <span data-ttu-id="95795-407">在下一個步驟中，進入 hello 安裝目錄，並瀏覽到 hello 子目錄 HDB_LCM_LINUX_X86_64。</span><span class="sxs-lookup"><span data-stu-id="95795-407">As next step, go into hello installation directory and navigate into hello sub directory HDB_LCM_LINUX_X86_64.</span></span> <span data-ttu-id="95795-408">Start</span><span class="sxs-lookup"><span data-stu-id="95795-408">Start</span></span>

```
./hdblcmgui 
```
<span data-ttu-id="95795-409">從該目錄。</span><span class="sxs-lookup"><span data-stu-id="95795-409">out of that directory.</span></span> <span data-ttu-id="95795-410">現在您會取得引導您完成一連串的螢幕 hello 安裝需要 tooprovide hello 資料。</span><span class="sxs-lookup"><span data-stu-id="95795-410">Now you are getting guided through a sequence of screens where you need tooprovide hello data for hello installation.</span></span> <span data-ttu-id="95795-411">在示範 hello 的情況下，我們要安裝 hello SAP HANA 資料庫伺服器和 hello SAP HANA 用戶端元件。</span><span class="sxs-lookup"><span data-stu-id="95795-411">In hello case demonstrated, we are installing hello SAP HANA database server and hello SAP HANA client components.</span></span> <span data-ttu-id="95795-412">因此我們選取 [SAP HANA 資料庫]，如下所示。</span><span class="sxs-lookup"><span data-stu-id="95795-412">Therefore our selection is 'SAP HANA Database' as shown below</span></span>

![在安裝中選取 [HANA]](./media/hana-installation/image18_hana_selection.PNG)

<span data-ttu-id="95795-414">在 hello 下一個畫面中，選擇 hello 選項安裝新 System'</span><span class="sxs-lookup"><span data-stu-id="95795-414">In hello next screen, you choose hello option 'Install New System'</span></span>

![新安裝選取 [HANA]](./media/hana-installation/image19_select_new.PNG)

<span data-ttu-id="95795-416">這個步驟之後，您需要可以另外安裝的數個其他元件之間的 tooselect toohello SAP HANA 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="95795-416">After this step, you need tooselect between several additional components that can be installed additionally toohello SAP HANA database server.</span></span>

![選取其他的 HANA 元件](./media/hana-installation/image20_select_components.PNG)

<span data-ttu-id="95795-418">這份文件的 hello 用途，我們選擇 hello SAP HANA 用戶端並 hello SAP HANA Studio。</span><span class="sxs-lookup"><span data-stu-id="95795-418">For hello purpose of this documentation, we chose hello SAP HANA Client and hello SAP HANA Studio.</span></span> <span data-ttu-id="95795-419">我們也安裝了相應增加執行個體。</span><span class="sxs-lookup"><span data-stu-id="95795-419">We also installed a scale-up instance.</span></span> <span data-ttu-id="95795-420">因此在 hello 下一個畫面中，您必須 toochoose 單一主機系統</span><span class="sxs-lookup"><span data-stu-id="95795-420">hence in hello next screen, you need toochoose 'Single-Host System'</span></span> 

![選取相應增加安裝](./media/hana-installation/image21_single_host.PNG)

<span data-ttu-id="95795-422">在 hello 下一個畫面中，您需要 tooprovide 某些資料</span><span class="sxs-lookup"><span data-stu-id="95795-422">In hello next screen, you need tooprovide some data</span></span>

![提供 SAP HANA SID](./media/hana-installation/image22_provide_sid.PNG)

> [!Important]
> <span data-ttu-id="95795-424">做為 HANA 系統識別碼 (SID)，您需要 tooprovide 排序 hello HANA 大型執行個體部署時，會提供 Microsoft hello 相同的 SID。</span><span class="sxs-lookup"><span data-stu-id="95795-424">As HANA System ID (SID), you need tooprovide hello same SID, as you provided Microsoft when you ordered hello HANA Large Instance deployment.</span></span> <span data-ttu-id="95795-425">選擇不同的 SID，將會因 tooaccess hello 不同磁碟區上的權限問題而失敗的 hello 安裝</span><span class="sxs-lookup"><span data-stu-id="95795-425">Choosing a different SID makes hello installation fail due tooaccess permission problems on hello different volumes</span></span>

<span data-ttu-id="95795-426">安裝目錄使用 hello /hana/shared 目錄。</span><span class="sxs-lookup"><span data-stu-id="95795-426">As installation directory you use hello /hana/shared directory.</span></span> <span data-ttu-id="95795-427">您可以在 hello 下一個步驟中，需要 tooprovide hello 位置來 hello HANA 資料檔案和 hello HANA 記錄檔</span><span class="sxs-lookup"><span data-stu-id="95795-427">In hello next step, you need tooprovide hello locations for hello HANA data files and hello HANA log files</span></span>


![提供 HANA 記錄檔位置](./media/hana-installation/image23_provide_log.PNG)

> [!Note]
> <span data-ttu-id="95795-429">您應該定義為資料和記錄檔 hello 已隨附包含 hello SID 您選擇在這個畫面之前 hello 螢幕選取範圍中的 hello 掛接點的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="95795-429">You should define as data and log files hello volumes that came already with hello mount points that contain hello SID you chose in hello screen selection before this screen.</span></span> <span data-ttu-id="95795-430">如果 hello SID 未不符以 hello 其中一個您輸入時，在囉 」 畫面之前，請返回並調整 hello 您擁有 hello 掛接點的 SID toohello 值。</span><span class="sxs-lookup"><span data-stu-id="95795-430">If hello SID does mismatch with hello one you typed in, in hello screen before, go back and adjust hello SID toohello value you have on hello mount points.</span></span>

<span data-ttu-id="95795-431">在 hello 下一個步驟中，檢閱 hello 主機名稱並最終加以更正。</span><span class="sxs-lookup"><span data-stu-id="95795-431">In hello next step, review hello host name and eventually correct it.</span></span> 

![檢閱主機名稱](./media/hana-installation/image24_review_host_name.PNG)

<span data-ttu-id="95795-433">在 hello 下一個步驟中，您也需要排序 hello HANA 大型執行個體部署時，指定給 tooMicrosoft tooretrieve 資料。</span><span class="sxs-lookup"><span data-stu-id="95795-433">In hello next step, you also need tooretrieve data you gave tooMicrosoft when you ordered hello HANA Large Instance deployment.</span></span> 

![提供系統使用者 UID 與 GID](./media/hana-installation/image25_provide_guid.PNG)

> [!Important]
> <span data-ttu-id="95795-435">您需要 tooprovide 排序 hello 單元部署時，會提供 Microsoft hello 相同的系統使用者識別碼和使用者群組的識別碼。</span><span class="sxs-lookup"><span data-stu-id="95795-435">You need tooprovide hello same System User ID and ID of User Group as you provided Microsoft as you order hello unit deployment.</span></span> <span data-ttu-id="95795-436">如果您非常容錯 toogive hello 相同的識別碼，SAP HANA 上 hello HANA 大型執行個體單元 hello 安裝將會失敗。</span><span class="sxs-lookup"><span data-stu-id="95795-436">If you fail toogive hello very same IDs, hello installation of SAP HANA on hello HANA Large Instance unit fails.</span></span>

<span data-ttu-id="95795-437">Hello 下面兩個畫面，我們不會顯示這份文件中，您需要 tooprovide hello 密碼 hello SAP HANA 資料庫與 hello hello sapadm 使用者密碼，用來取得安裝的一部分的 SAP Host Agent hello hello 系統使用者hello SAP HANA 資料庫執行個體。</span><span class="sxs-lookup"><span data-stu-id="95795-437">In hello next two screens, which we are not showing in this documentation, you need tooprovide hello password for hello SYSTEM user of hello SAP HANA database and hello password for hello sapadm user, which is used for hello SAP Host Agent that gets installed as part of hello SAP HANA database instance.</span></span>

<span data-ttu-id="95795-438">定義之後 hello 密碼，確認畫面會顯示。</span><span class="sxs-lookup"><span data-stu-id="95795-438">After defining hello password, a confirmation screen is showing up.</span></span> <span data-ttu-id="95795-439">檢查 hello 的所有資料列，然後再繼續進行 hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="95795-439">check all hello data listed and continue with hello installation.</span></span> <span data-ttu-id="95795-440">您到達文件 hello 安裝進度，類似下面其中一個 hello 進度畫面</span><span class="sxs-lookup"><span data-stu-id="95795-440">You reach a progress screen that documents hello installation progress, like hello one below</span></span>

![檢查安裝進度](./media/hana-installation/image27_show_progress.PNG)

<span data-ttu-id="95795-442">因為 hello 安裝完成後，您應該像 hello 下列其中一張圖片</span><span class="sxs-lookup"><span data-stu-id="95795-442">As hello installation finishes, you should a picture like hello following one</span></span>

![安裝完成](./media/hana-installation/image28_install_finished.PNG)

<span data-ttu-id="95795-444">此時，hello SAP HANA 執行個體應該啟動並執行並備妥可供使用。</span><span class="sxs-lookup"><span data-stu-id="95795-444">At this point, hello SAP HANA instance should be up and running and ready for usage.</span></span> <span data-ttu-id="95795-445">您應該能夠 tooconnect tooit 從 SAP HANA Studio。</span><span class="sxs-lookup"><span data-stu-id="95795-445">You should be able tooconnect tooit from SAP HANA Studio.</span></span> <span data-ttu-id="95795-446">也請確定您檢查 hello SAP HANA 的最新修補程式，並套用這些修補程式。</span><span class="sxs-lookup"><span data-stu-id="95795-446">Also make sure that you check for hello latest patches of SAP HANA and apply those patches.</span></span>
























































 







 




