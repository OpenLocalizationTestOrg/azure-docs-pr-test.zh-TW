<span data-ttu-id="fa49a-101">本文概述一組已經實證的做法，以便在 Azure 上執行 Windows 虛擬機器 (VM)，並注意延展性、可用性、管理性和安全性。</span><span class="sxs-lookup"><span data-stu-id="fa49a-101">This article outlines a set of proven practices for running a Windows virtual machine (VM) on Azure, paying attention to scalability, availability, manageability, and security.</span></span>

> [!NOTE]
> <span data-ttu-id="fa49a-102">Azure 有兩個不同的部署模型：[Azure Resource Manager][resource-manager-overview] 和傳統。</span><span class="sxs-lookup"><span data-stu-id="fa49a-102">Azure has two different deployment models: [Azure Resource Manager][resource-manager-overview] and classic.</span></span> <span data-ttu-id="fa49a-103">本文使用 Microsoft 建議用於新部署的資源管理員。</span><span class="sxs-lookup"><span data-stu-id="fa49a-103">This article uses Resource Manager, which Microsoft recommends for new deployments.</span></span>
>
>

<span data-ttu-id="fa49a-104">我們不建議用使用單一 VM 進行關鍵任務工作負載，因為它會建立單一失敗點。</span><span class="sxs-lookup"><span data-stu-id="fa49a-104">We don't recommend using a single VM for mission critical workloads, because it creates a single point of failure.</span></span> <span data-ttu-id="fa49a-105">若要擁有較高的可用性，您必須在[可用性設定組][availability-set]中部署多個 VM。</span><span class="sxs-lookup"><span data-stu-id="fa49a-105">For higher availability, deploy multiple VMs in an [availability set][availability-set].</span></span> <span data-ttu-id="fa49a-106">如需詳細資訊，請參閱[在 Azure 上執行多個 VM][multi-vm]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-106">For more information, see [Running multiple VMs on Azure][multi-vm].</span></span>

## <a name="architecture-diagram"></a><span data-ttu-id="fa49a-107">架構圖表</span><span class="sxs-lookup"><span data-stu-id="fa49a-107">Architecture diagram</span></span>

<span data-ttu-id="fa49a-108">在 Azure 中佈建 VM 牽涉的移動組建比 VM 本身更多。</span><span class="sxs-lookup"><span data-stu-id="fa49a-108">Provisioning a VM in Azure involves more moving parts than just the VM itself.</span></span> <span data-ttu-id="fa49a-109">有計算、網路及儲存體元素。</span><span class="sxs-lookup"><span data-stu-id="fa49a-109">There are compute, networking, and storage elements.</span></span>

> <span data-ttu-id="fa49a-110">包含此架構圖表的 Visio 文件可在 [Microsoft 下載中心][visio-download]提供下載。</span><span class="sxs-lookup"><span data-stu-id="fa49a-110">A Visio document that includes this architecture diagram is available for download from the [Microsoft download center][visio-download].</span></span> <span data-ttu-id="fa49a-111">此圖表位於「計算 - 單一 VM」頁面。</span><span class="sxs-lookup"><span data-stu-id="fa49a-111">This diagram is on the "Compute - single VM" page.</span></span>
>
>

<span data-ttu-id="fa49a-112">![[0]][0]</span><span class="sxs-lookup"><span data-stu-id="fa49a-112">![[0]][0]</span></span>

* <span data-ttu-id="fa49a-113">**資源群組。**</span><span class="sxs-lookup"><span data-stu-id="fa49a-113">**Resource group.**</span></span> <span data-ttu-id="fa49a-114">[*資源群組*][resource-manager-overview]是保存相關資源的容器。</span><span class="sxs-lookup"><span data-stu-id="fa49a-114">A [*resource group*][resource-manager-overview] is a container that holds related resources.</span></span> <span data-ttu-id="fa49a-115">建立資源群組以保存此 VM 的資源。</span><span class="sxs-lookup"><span data-stu-id="fa49a-115">Create a resource group to hold the resources for this VM.</span></span>
* <span data-ttu-id="fa49a-116">**VM**。</span><span class="sxs-lookup"><span data-stu-id="fa49a-116">**VM**.</span></span> <span data-ttu-id="fa49a-117">您可以從已發佈的映像清單，或從您上傳至 Azure Blob 儲存體的虛擬硬碟 (VHD) 檔案佈建 VM。</span><span class="sxs-lookup"><span data-stu-id="fa49a-117">You can provision a VM from a list of published images or from a virtual hard disk (VHD) file that you upload to Azure Blob storage.</span></span>
* <span data-ttu-id="fa49a-118">**作業系統磁碟。**</span><span class="sxs-lookup"><span data-stu-id="fa49a-118">**OS disk.**</span></span> <span data-ttu-id="fa49a-119">作業系統磁碟是儲存在 [Azure 儲存體][azure-storage]中的 VHD。</span><span class="sxs-lookup"><span data-stu-id="fa49a-119">The OS disk is a VHD stored in [Azure Storage][azure-storage].</span></span> <span data-ttu-id="fa49a-120">這表示即使主機電腦關閉，它仍持續存在。</span><span class="sxs-lookup"><span data-stu-id="fa49a-120">That means it persists even if the host machine goes down.</span></span>
* <span data-ttu-id="fa49a-121">**暫存磁碟。**</span><span class="sxs-lookup"><span data-stu-id="fa49a-121">**Temporary disk.**</span></span> <span data-ttu-id="fa49a-122">VM 是使用暫存磁碟 (Windows 上的 `D:` 磁碟機) 來建立。</span><span class="sxs-lookup"><span data-stu-id="fa49a-122">The VM is created with a temporary disk (the `D:` drive on Windows).</span></span> <span data-ttu-id="fa49a-123">此磁碟會儲存在主機電腦的實體磁碟機上。</span><span class="sxs-lookup"><span data-stu-id="fa49a-123">This disk is stored on a physical drive on the host machine.</span></span> <span data-ttu-id="fa49a-124">不會  儲存在 Azure 儲存體中，而且可能在重新開機期間和其他 VM 生命週期事件中刪除。</span><span class="sxs-lookup"><span data-stu-id="fa49a-124">It is *not* saved in Azure Storage, and might be deleted during reboots and other VM lifecycle events.</span></span> <span data-ttu-id="fa49a-125">僅將此磁碟使用於暫存資料，例如分頁檔或交換檔。</span><span class="sxs-lookup"><span data-stu-id="fa49a-125">Use this disk only for temporary data, such as page or swap files.</span></span>
* <span data-ttu-id="fa49a-126">**資料磁碟。**</span><span class="sxs-lookup"><span data-stu-id="fa49a-126">**Data disks.**</span></span> <span data-ttu-id="fa49a-127">[資料磁碟][data-disk]是用於應用程式資料的持續性 VHD。</span><span class="sxs-lookup"><span data-stu-id="fa49a-127">A [data disk][data-disk] is a persistent VHD used for application data.</span></span> <span data-ttu-id="fa49a-128">資料磁碟會儲存在 Azure 儲存體中，例如作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="fa49a-128">Data disks are stored in Azure Storage, like the OS disk.</span></span>
* <span data-ttu-id="fa49a-129">**虛擬網路 (VNet) 和子網路。**</span><span class="sxs-lookup"><span data-stu-id="fa49a-129">**Virtual network (VNet) and subnet.**</span></span> <span data-ttu-id="fa49a-130">在 Azure 中的每個 VM 都會部署到 VNet 中，而虛擬網路會進一步分成數個子網路。</span><span class="sxs-lookup"><span data-stu-id="fa49a-130">Every VM in Azure is deployed into a VNet that is further divided into subnets.</span></span>
* <span data-ttu-id="fa49a-131">**公用 IP 位址。**</span><span class="sxs-lookup"><span data-stu-id="fa49a-131">**Public IP address.**</span></span> <span data-ttu-id="fa49a-132">必須要有公用 IP 位址才能與 VM&mdash; 進行通訊，例如透過遠端桌面 (RDP)。</span><span class="sxs-lookup"><span data-stu-id="fa49a-132">A public IP address is needed to communicate with the VM&mdash;for example over remote desktop (RDP).</span></span>
* <span data-ttu-id="fa49a-133">**網路介面 (NIC)**。</span><span class="sxs-lookup"><span data-stu-id="fa49a-133">**Network interface (NIC)**.</span></span> <span data-ttu-id="fa49a-134">NIC 可讓 VM 與虛擬網路通訊。</span><span class="sxs-lookup"><span data-stu-id="fa49a-134">The NIC enables the VM to communicate with the virtual network.</span></span>
* <span data-ttu-id="fa49a-135">**網路安全性群組 (NSG)**。</span><span class="sxs-lookup"><span data-stu-id="fa49a-135">**Network security group (NSG)**.</span></span> <span data-ttu-id="fa49a-136">[NSG][nsg] 是用來允許/拒絕對子網路的網路流量。</span><span class="sxs-lookup"><span data-stu-id="fa49a-136">The [NSG][nsg] is used to allow/deny network traffic to the subnet.</span></span> <span data-ttu-id="fa49a-137">您可以將 NSG 與獨立的 NIC 或子網路關聯。</span><span class="sxs-lookup"><span data-stu-id="fa49a-137">You can associate an NSG with an individual NIC or with a subnet.</span></span> <span data-ttu-id="fa49a-138">如果您將它與子網路關聯，該 NSG 規則會套用至子網路中的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="fa49a-138">If you associate it with a subnet, the NSG rules apply to all VMs in that subnet.</span></span>
* <span data-ttu-id="fa49a-139">**診斷。**</span><span class="sxs-lookup"><span data-stu-id="fa49a-139">**Diagnostics.**</span></span> <span data-ttu-id="fa49a-140">診斷記錄對於管理和針對 VM 進行疑難排解十分重要。</span><span class="sxs-lookup"><span data-stu-id="fa49a-140">Diagnostic logging is crucial for managing and troubleshooting the VM.</span></span>

## <a name="recommendations"></a><span data-ttu-id="fa49a-141">建議</span><span class="sxs-lookup"><span data-stu-id="fa49a-141">Recommendations</span></span>

<span data-ttu-id="fa49a-142">下列建議適用於大部分的案例。</span><span class="sxs-lookup"><span data-stu-id="fa49a-142">The following recommendations apply for most scenarios.</span></span> <span data-ttu-id="fa49a-143">除非您有特定的需求會覆寫它們，否則請遵循下列建議。</span><span class="sxs-lookup"><span data-stu-id="fa49a-143">Follow these recommendations unless you have a specific requirement that overrides them.</span></span>

### <a name="vm-recommendations"></a><span data-ttu-id="fa49a-144">VM 建議</span><span class="sxs-lookup"><span data-stu-id="fa49a-144">VM recommendations</span></span>

<span data-ttu-id="fa49a-145">Azure 提供許多不同的虛擬機器大小，但是我們建議使用 DS 和 GS 系列，因為這些機器大小支援[進階儲存體][premium-storage]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-145">Azure offers many different virtual machine sizes, but we recommend the DS- and GS-series because these machine sizes support [Premium Storage][premium-storage].</span></span> <span data-ttu-id="fa49a-146">選取其中一個機器大小，除非您有高效能運算等特殊工作負載。</span><span class="sxs-lookup"><span data-stu-id="fa49a-146">Select one of these machine sizes unless you have a specialized workload such as high-performance computing.</span></span> <span data-ttu-id="fa49a-147">如需詳細資訊，請參閱[虛擬機器的大小][virtual-machine-sizes]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-147">For details, see [virtual machine sizes][virtual-machine-sizes].</span></span>

<span data-ttu-id="fa49a-148">如果您將現有的工作負載移至 Azure，則從最符合您內部部署伺服器的 VM 大小開始。</span><span class="sxs-lookup"><span data-stu-id="fa49a-148">If you are moving an existing workload to Azure, start with the VM size that's the closest match to your on-premises servers.</span></span> <span data-ttu-id="fa49a-149">然後根據 CPU、記憶體和每秒的磁碟輸入/輸出作業 (IOPS) 測量您的實際工作負載效能，並視需要調整大小。</span><span class="sxs-lookup"><span data-stu-id="fa49a-149">Then measure the performance of your actual workload with respect to CPU, memory, and disk input/output operations per second (IOPS), and adjust the size if needed.</span></span> <span data-ttu-id="fa49a-150">如果您的 VM 需要多個 NIC，請注意 NIC 的最大數目是 [VM 大小][vm-size-tables]的函式。</span><span class="sxs-lookup"><span data-stu-id="fa49a-150">If you require multiple NICs for your VM, be aware that the maximum number of NICs is a function of the [VM size][vm-size-tables].</span></span>   

<span data-ttu-id="fa49a-151">當您佈建 VM 和其他資源時，必須指定一個區域。</span><span class="sxs-lookup"><span data-stu-id="fa49a-151">When you provision the VM and other resources, you must specify a region.</span></span> <span data-ttu-id="fa49a-152">一般而言，選擇最接近您的內部使用者或客戶的區域。</span><span class="sxs-lookup"><span data-stu-id="fa49a-152">Generally, choose a region closest to your internal users or customers.</span></span> <span data-ttu-id="fa49a-153">不過，並非所有 VM 大小在所有區域都可供使用。</span><span class="sxs-lookup"><span data-stu-id="fa49a-153">However, not all VM sizes may be available in all regions.</span></span> <span data-ttu-id="fa49a-154">如需詳細資訊，請參閱[依區域提供的服務][services-by-region]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-154">For details, see [services by region][services-by-region].</span></span> <span data-ttu-id="fa49a-155">若要查看指定區域中可用的 VM 大小清單，請執行下列 Azure 命令列介面 (CLI) 命令：</span><span class="sxs-lookup"><span data-stu-id="fa49a-155">To see a list of the VM sizes available in a given region, run the following Azure command-line interface (CLI) command:</span></span>

```
azure vm sizes --location <location>
```

<span data-ttu-id="fa49a-156">如需選擇已發佈 VM 映像的相關資訊，請參閱[在 Azure 中使用 Powershell 或 CLI 瀏覽並選取 Windows 虛擬機器映像][select-vm-image]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-156">For information about choosing a published VM image, see [Navigate and select Windows virtual machine images in Azure with Powershell or CLI][select-vm-image].</span></span>

### <a name="disk-and-storage-recommendations"></a><span data-ttu-id="fa49a-157">磁碟和儲存體建議</span><span class="sxs-lookup"><span data-stu-id="fa49a-157">Disk and storage recommendations</span></span>

<span data-ttu-id="fa49a-158">為了達到最佳的磁碟 I/O 效能，我們建議使用[進階儲存體][premium-storage]，這會將資料儲存在固態硬碟 (SSD)。</span><span class="sxs-lookup"><span data-stu-id="fa49a-158">For best disk I/O performance, we recommend [Premium Storage][premium-storage], which stores data on solid state drives (SSDs).</span></span> <span data-ttu-id="fa49a-159">成本是依佈建的磁碟大小而定。</span><span class="sxs-lookup"><span data-stu-id="fa49a-159">Cost is based on the size of the provisioned disk.</span></span> <span data-ttu-id="fa49a-160">IOPS 和輸送量也取決於磁碟大小，因此當您佈建磁碟時，請考慮以下三個因素 (容量、IOPS 和輸送量)。</span><span class="sxs-lookup"><span data-stu-id="fa49a-160">IOPS and throughput also depend on disk size, so when you provision a disk, consider all three factors (capacity, IOPS, and throughput).</span></span>

<span data-ttu-id="fa49a-161">針對每個 VM 建立個別的 Azure 儲存體帳戶來存放虛擬硬碟 (VHD)，以避免達到儲存體帳戶的 IOPS 限制。</span><span class="sxs-lookup"><span data-stu-id="fa49a-161">Create separate Azure storage accounts for each VM to hold the virtual hard disks (VHDs) in order to avoid hitting the IOPS limits for storage accounts.</span></span>

<span data-ttu-id="fa49a-162">新增一或多個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="fa49a-162">Add one or more data disks.</span></span> <span data-ttu-id="fa49a-163">當您建立新的 VHD 時，它仍未格式化。</span><span class="sxs-lookup"><span data-stu-id="fa49a-163">When you create a new VHD, it is unformatted.</span></span> <span data-ttu-id="fa49a-164">登入 VM 來格式化磁碟。</span><span class="sxs-lookup"><span data-stu-id="fa49a-164">Log into the VM to format the disk.</span></span> <span data-ttu-id="fa49a-165">如果您有大量的資料磁碟，請注意儲存體帳戶的總 I/O 限制。</span><span class="sxs-lookup"><span data-stu-id="fa49a-165">If you have a large number of data disks, be aware of the total I/O limits of the storage account.</span></span> <span data-ttu-id="fa49a-166">如需詳細資訊，請參閱[虛擬機器磁碟限制][vm-disk-limits]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-166">For more information, see [virtual machine disk limits][vm-disk-limits].</span></span>

<span data-ttu-id="fa49a-167">若情況允許，請將應用程式安裝在資料磁碟，不要安裝在作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="fa49a-167">When possible, install applications on a data disk, not the OS disk.</span></span> <span data-ttu-id="fa49a-168">不過，某些舊版的應用程式可能需要將元件安裝在 C: 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="fa49a-168">However, some legacy applications might need to install components on the C: drive.</span></span> <span data-ttu-id="fa49a-169">在此情況下，您可以使用 PowerShell 來[重新調整作業系統磁碟大小][resize-os-disk]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-169">In that case, you can [resize the OS disk][resize-os-disk] using PowerShell.</span></span>

<span data-ttu-id="fa49a-170">為了達到最佳效能，請建立個別的儲存體帳戶來保存診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="fa49a-170">For best performance, create a separate storage account to hold diagnostic logs.</span></span> <span data-ttu-id="fa49a-171">標準本地備援儲存體 (LRS) 帳戶已足以保存診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="fa49a-171">A standard locally redundant storage (LRS) account is sufficient for diagnostic logs.</span></span>

### <a name="network-recommendations"></a><span data-ttu-id="fa49a-172">網路建議</span><span class="sxs-lookup"><span data-stu-id="fa49a-172">Network recommendations</span></span>

<span data-ttu-id="fa49a-173">此公用 IP 位址可以是動態或靜態。</span><span class="sxs-lookup"><span data-stu-id="fa49a-173">The public IP address can be dynamic or static.</span></span> <span data-ttu-id="fa49a-174">預設值為動態。</span><span class="sxs-lookup"><span data-stu-id="fa49a-174">The default is dynamic.</span></span>

* <span data-ttu-id="fa49a-175">如果您需要一個不會變更的固定 IP 位址 &mdash;(例如，如果您需要在 DNS 中建立一個 A 記錄，或需要將 IP 位址加入安全清單)，請保留一個[靜態 IP 位址][static-ip]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-175">Reserve a [static IP address][static-ip] if you need a fixed IP address that won't change &mdash; for example, if you need to create an A record in DNS, or need the IP address to be added to a safe list.</span></span>
* <span data-ttu-id="fa49a-176">您也可以建立 IP 位址的完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="fa49a-176">You can also create a fully qualified domain name (FQDN) for the IP address.</span></span> <span data-ttu-id="fa49a-177">然後您可以在 DNS 中註冊指向該 FQDN 的 [CNAME 記錄][cname-record]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-177">You can then register a [CNAME record][cname-record] in DNS that points to the FQDN.</span></span> <span data-ttu-id="fa49a-178">如需詳細資訊，請參閱[在 Azure 入口網站中建立完整網域名稱][fqdn]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-178">For more information, see [create a fully qualified domain name in the Azure portal][fqdn].</span></span>

<span data-ttu-id="fa49a-179">所有 NSG 都包含一組[預設規則][nsg-default-rules]，包括一個封鎖所有網際網路輸入流量的規則。</span><span class="sxs-lookup"><span data-stu-id="fa49a-179">All NSGs contain a set of [default rules][nsg-default-rules], including a rule that blocks all inbound Internet traffic.</span></span> <span data-ttu-id="fa49a-180">預設的規則不能刪除，但其他規則可以覆寫它們。</span><span class="sxs-lookup"><span data-stu-id="fa49a-180">The default rules cannot be deleted, but other rules can override them.</span></span> <span data-ttu-id="fa49a-181">若要啟用網際網路流量，請建立允許輸入流量輸入特定連接埠的規則 &mdash; 例如，允許連接埠 80 用於 HTTP。</span><span class="sxs-lookup"><span data-stu-id="fa49a-181">To enable Internet traffic, create rules that allow inbound traffic to specific ports &mdash; for example, port 80 for HTTP.</span></span>  

<span data-ttu-id="fa49a-182">若要啟用 RDP，請新增一個 NSG 規則，以允許將輸入流量輸入至 TCP 連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="fa49a-182">To enable RDP, add an NSG rule that allows inbound traffic to TCP port 3389.</span></span>

## <a name="scalability-considerations"></a><span data-ttu-id="fa49a-183">延展性考量</span><span class="sxs-lookup"><span data-stu-id="fa49a-183">Scalability considerations</span></span>

<span data-ttu-id="fa49a-184">您可以藉由[變更 VM 大小](../articles/virtual-machines/windows/sizes.md)來相應增加或相應減少 VM。</span><span class="sxs-lookup"><span data-stu-id="fa49a-184">You can scale a VM up or down by [changing the VM size](../articles/virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="fa49a-185">若要水平相應放大，請將兩個以上的 VM 置於附載平衡器後方的可用性設定組中。</span><span class="sxs-lookup"><span data-stu-id="fa49a-185">To scale out horizontally, put two or more VMs into an availability set behind a load balancer.</span></span> <span data-ttu-id="fa49a-186">如需詳細資訊，請參閱[在 Azure 上執行多個 VM 以獲得延展性和可用性][multi-vm]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-186">For details, see [Running multiple VMs on Azure for scalability and availability][multi-vm].</span></span>

## <a name="availability-considerations"></a><span data-ttu-id="fa49a-187">可用性考量</span><span class="sxs-lookup"><span data-stu-id="fa49a-187">Availability considerations</span></span>

<span data-ttu-id="fa49a-188">若要擁有較高的可用性，您必須在可用性設定組中部署多個 VM。</span><span class="sxs-lookup"><span data-stu-id="fa49a-188">For higher availabiility, deploy multiple VMs in an availability set.</span></span> <span data-ttu-id="fa49a-189">這也會提供較高的[服務等級協定][vm-sla] (SLA)。</span><span class="sxs-lookup"><span data-stu-id="fa49a-189">This also provides a higher [service level agreement][vm-sla] (SLA).</span></span>

<span data-ttu-id="fa49a-190">您的 VM 可能會受到[計劃性維護][planned-maintenance]或[非計劃性維護][manage-vm-availability]影響。</span><span class="sxs-lookup"><span data-stu-id="fa49a-190">Your VM may be affected by [planned maintenance][planned-maintenance] or [unplanned maintenance][manage-vm-availability].</span></span> <span data-ttu-id="fa49a-191">您可以使用 [VM 重新啟動記錄檔][reboot-logs]來判斷 VM 重新啟動是否是因為計劃性維護所造成。</span><span class="sxs-lookup"><span data-stu-id="fa49a-191">You can use [VM reboot logs][reboot-logs] to determine whether a VM reboot was caused by planned maintenance.</span></span>

<span data-ttu-id="fa49a-192">VHD 是儲存在 [Azure 儲存體][azure-storage]，而系統會複寫 Azure 儲存體來提供持久性和可用性。</span><span class="sxs-lookup"><span data-stu-id="fa49a-192">VHDs are stored in [Azure storage][azure-storage], and Azure storage is replicated for durability and availability.</span></span>

<span data-ttu-id="fa49a-193">為了防止在正常作業期間意外遺失資料 (例如，因使用者錯誤而造成)，您也應該使用 [Blob 快照][blob-snapshot]或其他工具來實作時間點備份。</span><span class="sxs-lookup"><span data-stu-id="fa49a-193">To protect against accidental data loss during normal operations (for example, because of user error), you should also implement point-in-time backups, using [blob snapshots][blob-snapshot] or another tool.</span></span>

## <a name="manageability-considerations"></a><span data-ttu-id="fa49a-194">管理性考量</span><span class="sxs-lookup"><span data-stu-id="fa49a-194">Manageability considerations</span></span>

<span data-ttu-id="fa49a-195">**資源群組。**</span><span class="sxs-lookup"><span data-stu-id="fa49a-195">**Resource groups.**</span></span> <span data-ttu-id="fa49a-196">將關係密切且共用相同生命週期的資源置於同一個[資源群組][resource-manager-overview]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-196">Put tightly-coupled resources that share the same life cycle into the same [resource group][resource-manager-overview].</span></span> <span data-ttu-id="fa49a-197">資源群組可讓您以群組為單位來部署和監視資源，並根據資源群組列出帳單成本。</span><span class="sxs-lookup"><span data-stu-id="fa49a-197">Resource groups allow you to deploy and monitor resources as a group and roll up billing costs by resource group.</span></span> <span data-ttu-id="fa49a-198">您也可以刪除整組資源，這對於測試部署非常有用。</span><span class="sxs-lookup"><span data-stu-id="fa49a-198">You can also delete resources as a set, which is very useful for test deployments.</span></span> <span data-ttu-id="fa49a-199">為資源提供有意義的名稱。</span><span class="sxs-lookup"><span data-stu-id="fa49a-199">Give resources meaningful names.</span></span> <span data-ttu-id="fa49a-200">這樣能更容易找到特定資源及了解其角色。</span><span class="sxs-lookup"><span data-stu-id="fa49a-200">That makes it easier to locate a specific resource and understand its role.</span></span> <span data-ttu-id="fa49a-201">請參閱 [Azure 資源的建議命名慣例][naming conventions]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-201">See [Recommended Naming Conventions for Azure Resources][naming conventions].</span></span>

<span data-ttu-id="fa49a-202">**VM 診斷。**</span><span class="sxs-lookup"><span data-stu-id="fa49a-202">**VM diagnostics.**</span></span> <span data-ttu-id="fa49a-203">啟用監視和診斷，包括基本健全狀況度量、診斷基礎結構記錄檔及[開機診斷][boot-diagnostics]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-203">Enable monitoring and diagnostics, including basic health metrics, diagnostics infrastructure logs, and [boot diagnostics][boot-diagnostics].</span></span> <span data-ttu-id="fa49a-204">如果您的 VM 進入無法開機的狀態，開機診斷能協助您診斷開機失敗。</span><span class="sxs-lookup"><span data-stu-id="fa49a-204">Boot diagnostics can help you diagnose a boot failure if your VM gets into a nonbootable state.</span></span> <span data-ttu-id="fa49a-205">如需詳細資訊，請參閱[啟用監視和診斷][enable-monitoring]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-205">For more information, see [Enable monitoring and diagnostics][enable-monitoring].</span></span> <span data-ttu-id="fa49a-206">使用 [Azure 記錄檔收集][log-collector]擴充來收集 Azure 平台記錄檔並上傳至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="fa49a-206">Use the [Azure Log Collection][log-collector] extension to collect Azure platform logs and upload them to Azure storage.</span></span>   

<span data-ttu-id="fa49a-207">下列 CLI 命令會啟用診斷：</span><span class="sxs-lookup"><span data-stu-id="fa49a-207">The following CLI command enables diagnostics:</span></span>

```
azure vm enable-diag <resource-group> <vm-name>
```

<span data-ttu-id="fa49a-208">**停止 VM。**</span><span class="sxs-lookup"><span data-stu-id="fa49a-208">**Stopping a VM.**</span></span> <span data-ttu-id="fa49a-209">Azure 會區分「已停止」和「已解除配置」狀態。</span><span class="sxs-lookup"><span data-stu-id="fa49a-209">Azure makes a distinction between "stopped" and "deallocated" states.</span></span> <span data-ttu-id="fa49a-210">您需要在 VM 狀態停止時支付費用，而不是在取消配置 VM 時支付。</span><span class="sxs-lookup"><span data-stu-id="fa49a-210">You are charged when the VM status is stopped, but not when the VM is deallocated.</span></span>

<span data-ttu-id="fa49a-211">使用下列 CLI 命令來解除配置 VM：</span><span class="sxs-lookup"><span data-stu-id="fa49a-211">Use the following CLI command to deallocate a VM:</span></span>

```
azure vm deallocate <resource-group> <vm-name>
```

<span data-ttu-id="fa49a-212">在 Azure 入口網站中，[停止] 按鈕會取消配置 VM。</span><span class="sxs-lookup"><span data-stu-id="fa49a-212">In the Azure portal, the **Stop** button deallocates the VM.</span></span> <span data-ttu-id="fa49a-213">不過，如果您是在登入時透過作業系統進行關閉，則會將 VM 停止但「不會」  取消配置，因此您仍需付費。</span><span class="sxs-lookup"><span data-stu-id="fa49a-213">However, if you shut down through the OS while logged in, the VM is stopped but *not* deallocated, so you will still be charged.</span></span>

<span data-ttu-id="fa49a-214">**刪除 VM。**</span><span class="sxs-lookup"><span data-stu-id="fa49a-214">**Deleting a VM.**</span></span> <span data-ttu-id="fa49a-215">如果您刪除 VM，並不會刪除 VHD。</span><span class="sxs-lookup"><span data-stu-id="fa49a-215">If you delete a VM, the VHDs are not deleted.</span></span> <span data-ttu-id="fa49a-216">這表示您可以放心地刪除 VM，而不會遺失任何資料。</span><span class="sxs-lookup"><span data-stu-id="fa49a-216">That means you can safely delete the VM without losing data.</span></span> <span data-ttu-id="fa49a-217">不過，您仍需支付儲存體費用。</span><span class="sxs-lookup"><span data-stu-id="fa49a-217">However, you will still be charged for storage.</span></span> <span data-ttu-id="fa49a-218">若要刪除 VHD，請將檔案從 [Blob 儲存體][blob-storage]中刪除。</span><span class="sxs-lookup"><span data-stu-id="fa49a-218">To delete the VHD, delete the file from [Blob storage][blob-storage].</span></span>

<span data-ttu-id="fa49a-219">若要防止意外刪除，請使用[資源鎖定][resource-lock]來鎖定整個資源群組或鎖定個別資源 (例如 VM)。</span><span class="sxs-lookup"><span data-stu-id="fa49a-219">To prevent accidental deletion, use a [resource lock][resource-lock] to lock the entire resource group or lock individual resources, such as the VM.</span></span>

## <a name="security-considerations"></a><span data-ttu-id="fa49a-220">安全性考量</span><span class="sxs-lookup"><span data-stu-id="fa49a-220">Security considerations</span></span>

<span data-ttu-id="fa49a-221">使用 [Azure 資訊安全中心][security-center]來集中檢視 Azure 資源的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="fa49a-221">Use [Azure Security Center][security-center] to get a central view of the security state of your Azure resources.</span></span> <span data-ttu-id="fa49a-222">資訊安全中心會監視潛在的安全性問題，並提供全面性的部署安全性健康狀態。</span><span class="sxs-lookup"><span data-stu-id="fa49a-222">Security Center monitors potential security issues and provides a comprehensive picture of the security health of your deployment.</span></span> <span data-ttu-id="fa49a-223">資訊安全中心是依每個 Azure 訂用帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="fa49a-223">Security Center is configured per Azure subscription.</span></span> <span data-ttu-id="fa49a-224">按照 [使用資訊安全中心]所述來啟用安全資料收集。</span><span class="sxs-lookup"><span data-stu-id="fa49a-224">Enable security data collection as described in [Use Security Center].</span></span> <span data-ttu-id="fa49a-225">啟用資料收集時，資訊安全性中心就會自動掃描任何該訂用帳戶建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="fa49a-225">When data collection is enabled, Security Center automatically scans any VMs created under that subscription.</span></span>

<span data-ttu-id="fa49a-226">**修補程式管理。**</span><span class="sxs-lookup"><span data-stu-id="fa49a-226">**Patch management.**</span></span> <span data-ttu-id="fa49a-227">如果啟用，資訊安全性中心會檢查是否遺失安全性或重要更新。</span><span class="sxs-lookup"><span data-stu-id="fa49a-227">If enabled, Security Center checks whether security and critical updates are missing.</span></span> <span data-ttu-id="fa49a-228">使用 VM 上的[群組原則設定][group-policy]來啟用自動系統更新。</span><span class="sxs-lookup"><span data-stu-id="fa49a-228">Use [Group Policy settings][group-policy] on the VM to enable automatic system updates.</span></span>

<span data-ttu-id="fa49a-229">**反惡意程式碼。**</span><span class="sxs-lookup"><span data-stu-id="fa49a-229">**Antimalware.**</span></span> <span data-ttu-id="fa49a-230">如果啟用，資訊安全性中心會檢查是已安裝反惡意程式碼軟體。</span><span class="sxs-lookup"><span data-stu-id="fa49a-230">If enabled, Security Center checks whether antimalware software is installed.</span></span> <span data-ttu-id="fa49a-231">您也可以使用資訊安全中心來從 Azure 入口網站內安裝反惡意程式碼軟體。</span><span class="sxs-lookup"><span data-stu-id="fa49a-231">You can also use Security Center to install antimalware software from inside the Azure portal.</span></span>

<span data-ttu-id="fa49a-232">**作業。**</span><span class="sxs-lookup"><span data-stu-id="fa49a-232">**Operations.**</span></span> <span data-ttu-id="fa49a-233">使用[角色型存取控制][rbac] (RBAC) 來控制對您所部署 Azure 資源的存取。</span><span class="sxs-lookup"><span data-stu-id="fa49a-233">Use [role-based access control][rbac] (RBAC) to control access to the Azure resources that you deploy.</span></span> <span data-ttu-id="fa49a-234">RBAC 可讓您指派授權角色給您 DevOps 小組的成員。</span><span class="sxs-lookup"><span data-stu-id="fa49a-234">RBAC lets you assign authorization roles to members of your DevOps team.</span></span> <span data-ttu-id="fa49a-235">例如，「讀取者」角色能檢視 Azure 資源但不能建立、管理或刪除它們。</span><span class="sxs-lookup"><span data-stu-id="fa49a-235">For example, the Reader role can view Azure resources but not create, manage, or delete them.</span></span> <span data-ttu-id="fa49a-236">某些角色專門用於特定的 Azure 資源類型。</span><span class="sxs-lookup"><span data-stu-id="fa49a-236">Some roles are specific to particular Azure resource types.</span></span> <span data-ttu-id="fa49a-237">例如，「虛擬機器參與者」角色能重新啟動或解除配置 VM、重設系統管理員密碼、建立新的 VM 等等。</span><span class="sxs-lookup"><span data-stu-id="fa49a-237">For example, the Virtual Machine Contributor role can restart or deallocate a VM, reset the administrator password, create a new VM, and so forth.</span></span> <span data-ttu-id="fa49a-238">其他對此參考架構可能有用的[內建 RBAC 角色][rbac-roles]包括 [DevTest Lab 使用者][rbac-devtest]和[網路參與者][rbac-network]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-238">Other [built-in RBAC roles][rbac-roles] that might be useful for this reference architecture include [DevTest Labs User][rbac-devtest] and [Network Contributor][rbac-network].</span></span> <span data-ttu-id="fa49a-239">使用者可以被指派多個角色，且您可以針對更詳細的權限建立角色。</span><span class="sxs-lookup"><span data-stu-id="fa49a-239">A user can be assigned to multiple roles, and you can create custom roles for even more fine-grained permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="fa49a-240">RBAC 不會限制使用者登入 VM 可執行的動作。</span><span class="sxs-lookup"><span data-stu-id="fa49a-240">RBAC does not limit the actions that a user logged into a VM can perform.</span></span> <span data-ttu-id="fa49a-241">這些權限是由客體 OS上的帳戶類型來決定。</span><span class="sxs-lookup"><span data-stu-id="fa49a-241">Those permissions are determined by the account type on the guest OS.</span></span>   
>
>

<span data-ttu-id="fa49a-242">若要重設本機系統管理員密碼，請執行 `vm reset-access` Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="fa49a-242">To reset the local administrator password, run the `vm reset-access` Azure CLI command.</span></span>

```
azure vm reset-access -u <user> -p <new-password> <resource-group> <vm-name>
```

<span data-ttu-id="fa49a-243">使用[稽核記錄檔][audit-logs]來查看佈建動作和其他 VM 事件。</span><span class="sxs-lookup"><span data-stu-id="fa49a-243">Use [audit logs][audit-logs] to see provisioning actions and other VM events.</span></span>

<span data-ttu-id="fa49a-244">**資料加密。**</span><span class="sxs-lookup"><span data-stu-id="fa49a-244">**Data encryption.**</span></span> <span data-ttu-id="fa49a-245">如果您要加密作業系統和資料磁碟，請考慮使用 [Azure 磁碟加密][disk-encryption]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-245">Consider [Azure Disk Encryption][disk-encryption] if you need to encrypt the OS and data disks.</span></span>

## <a name="solution-deployment"></a><span data-ttu-id="fa49a-246">解決方案部署</span><span class="sxs-lookup"><span data-stu-id="fa49a-246">Solution deployment</span></span>

<span data-ttu-id="fa49a-247">此參考架構的部署可在 [GitHub][github-folder] 上取得。</span><span class="sxs-lookup"><span data-stu-id="fa49a-247">A deployment for this reference architecture is available on [GitHub][github-folder].</span></span> <span data-ttu-id="fa49a-248">它包含 VNet、NSG 及單一 VM。</span><span class="sxs-lookup"><span data-stu-id="fa49a-248">It includes a VNet, NSG, and a single VM.</span></span> <span data-ttu-id="fa49a-249">若要部署架構，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="fa49a-249">To deploy the architecture, follow these steps:</span></span>

1. <span data-ttu-id="fa49a-250">以滑鼠右鍵按一下下方的按鈕，然後選取 [在新索引標籤中開啟連結] 或 [在新視窗開啟連結]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-250">Right click the button below and select either "Open link in new tab" or "Open link in new window."</span></span>  
   <span data-ttu-id="fa49a-251">[![部署至 Azure](../articles/guidance/media/blueprints/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Freference-architectures%2Fmaster%2Fguidance-compute-single-vm%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="fa49a-251">[![Deploy to Azure](../articles/guidance/media/blueprints/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Freference-architectures%2Fmaster%2Fguidance-compute-single-vm%2Fazuredeploy.json)</span></span>
2. <span data-ttu-id="fa49a-252">一旦連結已在 Azure 入口網站中開啟，您必須輸入部分設定的值：</span><span class="sxs-lookup"><span data-stu-id="fa49a-252">Once the link has opened in the Azure portal, you must enter values for some of the settings:</span></span>

   * <span data-ttu-id="fa49a-253">**資源群組**名稱已在參數檔案中定義，因此請在文字方塊中選取 [新建] 並輸入 `ra-single-vm-rg`。</span><span class="sxs-lookup"><span data-stu-id="fa49a-253">The **Resource group** name is already defined in the parameter file, so select **Create New** and enter `ra-single-vm-rg` in the text box.</span></span>
   * <span data-ttu-id="fa49a-254">從 [位置] 下拉式方塊選取區域。</span><span class="sxs-lookup"><span data-stu-id="fa49a-254">Select the region from the **Location** drop down box.</span></span>
   * <span data-ttu-id="fa49a-255">請勿編輯 [範本的根 URI] 或 [參數根 URI] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="fa49a-255">Do not edit the **Template Root Uri** or the **Parameter Root Uri** text boxes.</span></span>
   * <span data-ttu-id="fa49a-256">選取 [作業系統類型] 下拉式方塊中的 [windows]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-256">Select **windows** in the **Os Type** drop down box.</span></span>
   * <span data-ttu-id="fa49a-257">檢閱條款和條件，然後按一下 [我同意上方所述的條款及條件] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="fa49a-257">Review the terms and conditions, then click the **I agree to the terms and conditions stated above** checkbox.</span></span>
   * <span data-ttu-id="fa49a-258">按一下 [購買] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fa49a-258">Click on the **Purchase** button.</span></span>
3. <span data-ttu-id="fa49a-259">等待部署完成。</span><span class="sxs-lookup"><span data-stu-id="fa49a-259">Wait for the deployment to complete.</span></span>
4. <span data-ttu-id="fa49a-260">參數檔案包含硬式編碼的系統管理員使用者名稱和密碼，並強烈建議您立即變更兩者。</span><span class="sxs-lookup"><span data-stu-id="fa49a-260">The parameter files  include a hard-coded administrator user name and password, and it is strongly recommended that you immediately change both.</span></span> <span data-ttu-id="fa49a-261">在 Azure 入口網站中按一下名為 `ra-single-vm0 ` 的 VM。</span><span class="sxs-lookup"><span data-stu-id="fa49a-261">Click on the VM named `ra-single-vm0 `in the Azure portal.</span></span> <span data-ttu-id="fa49a-262">然後，按一下 [支援與疑難排解] 刀鋒視窗中的 [重設密碼]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-262">Then, click on **Reset password** in the **Support + troubleshooting** blade.</span></span> <span data-ttu-id="fa49a-263">選取 [模式] 下拉式清單方塊中的 [重設密碼]，然後選取新的**使用者名稱**和**密碼**。</span><span class="sxs-lookup"><span data-stu-id="fa49a-263">Select **Reset password** in the **Mode** dropdown box, then select a new **User name** and **Password**.</span></span> <span data-ttu-id="fa49a-264">按一下 [更新] 按鈕，保存新的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="fa49a-264">Click the **Update** button to persist the new user name and password.</span></span>

<span data-ttu-id="fa49a-265">如需部署此參考架構的其他方式的相關資訊，請參閱 [guidance-single-vm][github-folder] GitHub 資料夾中的讀我檔案。</span><span class="sxs-lookup"><span data-stu-id="fa49a-265">For information on additional ways to deploy this reference architecture, see the readme file in the [guidance-single-vm][github-folder]] GitHub folder.</span></span>

## <a name="customize-the-deployment"></a><span data-ttu-id="fa49a-266">自訂部署</span><span class="sxs-lookup"><span data-stu-id="fa49a-266">Customize the deployment</span></span>
<span data-ttu-id="fa49a-267">如果您需要變更部署以符合需求，請依照 [Readme][github-folder] 頁面中的指示。</span><span class="sxs-lookup"><span data-stu-id="fa49a-267">If you need to change the deployment to match your needs, follow the instructions in the [readme][github-folder].</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa49a-268">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa49a-268">Next steps</span></span>
<span data-ttu-id="fa49a-269">如需較高的可用性，請在負載平衡器後面部署兩個以上的 VM。</span><span class="sxs-lookup"><span data-stu-id="fa49a-269">For higher availability, deploy two or more VMs behind a load balancer.</span></span> <span data-ttu-id="fa49a-270">如需詳細資訊，請參閱[在 Azure 上執行多個 VM][multi-vm]。</span><span class="sxs-lookup"><span data-stu-id="fa49a-270">For more information, see [Running multiple VMs on Azure][multi-vm].</span></span>

<!-- links -->

[audit-logs]: https://azure.microsoft.com/en-us/blog/analyze-azure-audit-logs-in-powerbi-more/
[availability-set]:../articles/virtual-machines/windows/tutorial-availability-sets.md
[azure-cli]: /cli/azure/get-started-with-az-cli2
[azure-storage]: ../articles/storage/storage-introduction.md
[blob-snapshot]: ../articles/storage/storage-blob-snapshots.md
[blob-storage]: ../articles/storage/storage-introduction.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[cname-record]: https://en.wikipedia.org/wiki/CNAME_record
[data-disk]: ../articles/storage/storage-about-disks-and-vhds-windows.md
[disk-encryption]: ../articles/security/azure-security-disk-encryption.md
[enable-monitoring]: ../articles/monitoring-and-diagnostics/insights-how-to-use-diagnostics.md
[fqdn]:../articles/virtual-machines/windows/portal-create-fqdn.md
[github-folder]: http://github.com/mspnp/reference-architectures/tree/master/guidance-compute-single-vm
[group-policy]: https://technet.microsoft.com/en-us/library/dn595129.aspx
[log-collector]: https://azure.microsoft.com/en-us/blog/simplifying-virtual-machine-troubleshooting-using-azure-log-collector/
[manage-vm-availability]:../articles/virtual-machines/windows/manage-availability.md
[multi-vm]: ../articles/guidance/guidance-compute-multi-vm.md
[naming conventions]: ../articles/guidance/guidance-naming-conventions.md
[nsg]: ../articles/virtual-network/virtual-networks-nsg.md
[nsg-default-rules]: ../articles/virtual-network/virtual-networks-nsg.md#default-rules
[planned-maintenance]:../articles/virtual-machines/windows/planned-maintenance.md
[premium-storage]: ../articles/storage/storage-premium-storage.md
[rbac]: ../articles/active-directory/role-based-access-control-what-is.md
[rbac-roles]: ../articles/active-directory/role-based-access-built-in-roles.md
[rbac-devtest]: ../articles/active-directory/role-based-access-built-in-roles.md#devtest-labs-user
[rbac-network]: ../articles/active-directory/role-based-access-built-in-roles.md#network-contributor
[reboot-logs]: https://azure.microsoft.com/en-us/blog/viewing-vm-reboot-logs/
[resize-os-disk]:../articles/virtual-machines/windows/expand-os-disk.md
[Resize-VHD]: https://technet.microsoft.com/en-us/library/hh848535.aspx
[Resize virtual machines]: https://azure.microsoft.com/en-us/blog/resize-virtual-machines/
[resource-lock]: ../articles/resource-group-lock-resources.md
[resource-manager-overview]: ../articles/azure-resource-manager/resource-group-overview.md
[security-center]: https://azure.microsoft.com/en-us/services/security-center/
[select-vm-image]:../articles/virtual-machines/windows/cli-ps-findimage.md
[services-by-region]: https://azure.microsoft.com/en-us/regions/#services
[static-ip]: ../articles/virtual-network/virtual-networks-reserved-public-ip.md
[storage-account-limits]: ../articles/azure-subscription-service-limits.md#storage-limits
[storage-price]: https://azure.microsoft.com/pricing/details/storage/
<span data-ttu-id="fa49a-271">[使用資訊安全中心]: ../articles/security-center/security-center-get-started.md#use-security-center</span><span class="sxs-lookup"><span data-stu-id="fa49a-271">[Use Security Center]: ../articles/security-center/security-center-get-started.md#use-security-center</span></span>
[virtual-machine-sizes]: ../articles/virtual-machines/windows/sizes.md
[visio-download]: http://download.microsoft.com/download/1/5/6/1569703C-0A82-4A9C-8334-F13D0DF2F472/RAs.vsdx
[vm-disk-limits]: ../articles/azure-subscription-service-limits.md#virtual-machine-disk-limits
[vm-resize]:../articles/virtual-machines/linux/change-vm-size.md
[vm-sla]: https://azure.microsoft.com/support/legal/sla/virtual-machines
[vm-size-tables]: ../articles/virtual-machines/windows/sizes.md
<span data-ttu-id="fa49a-272">[0]: ./media/guidance-blueprints/compute-single-vm.png "Azure 中的單一 Windows VM 架構"</span><span class="sxs-lookup"><span data-stu-id="fa49a-272">[0]: ./media/guidance-blueprints/compute-single-vm.png "Single Windows VM architecture in Azure"</span></span>
[readme]: https://github.com/mspnp/reference-architectures/blob/master/guidance-compute-single-vm
[blocks]: https://github.com/mspnp/template-building-blocks
