# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="a4ba8-101">關於 Azure IaaS VM 磁碟及受控和非受控進階磁碟的常見問題集</span><span class="sxs-lookup"><span data-stu-id="a4ba8-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="a4ba8-102">此文章將回答有關 Azure 受控磁碟和 Azure 進階儲存體的一些常見問題。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="a4ba8-103">受控磁碟</span><span class="sxs-lookup"><span data-stu-id="a4ba8-103">Managed Disks</span></span>

<span data-ttu-id="a4ba8-104">**何謂 Azure 受控磁碟？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="a4ba8-105">受控磁碟是可以為您管理儲存體帳戶而簡化 Azure IaaS VM 磁碟管理的一項功能。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="a4ba8-106">如需詳細資訊，請參閱[受控磁碟概觀](../articles/virtual-machines/windows/managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-106">For more information, see the [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="a4ba8-107">**如果我從現有的 VHD (大小為 80 GB) 建立標準受控磁碟，需要多少費用？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="a4ba8-108">從 80 GB VHD 建立的標準受控磁碟會被視為下一個可用的標準磁碟大小 (S10 磁碟)。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-108">A standard managed disk created from an 80-GB VHD is treated as the next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="a4ba8-109">將根據 S10 磁碟定價向您收費。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-109">You're charged according to the S10 disk pricing.</span></span> <span data-ttu-id="a4ba8-110">如需詳細資訊，請參閱[價格頁面](https://azure.microsoft.com/pricing/details/storage)。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-110">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="a4ba8-111">**標準受控磁碟有任何交易成本嗎？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="a4ba8-112">是。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-112">Yes.</span></span> <span data-ttu-id="a4ba8-113">我們會根據每一筆交易向您收費。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-113">You're charged for each transaction.</span></span> <span data-ttu-id="a4ba8-114">如需詳細資訊，請參閱[價格頁面](https://azure.microsoft.com/pricing/details/storage)。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-114">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="a4ba8-115">**對於標準受控磁碟，收費是依據磁碟上的資料實際大小，還是磁碟的佈建容量？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-115">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span></span>

<span data-ttu-id="a4ba8-116">收費是依據磁碟的佈建容量。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-116">You're charged based on the provisioned capacity of the disk.</span></span> <span data-ttu-id="a4ba8-117">如需詳細資訊，請參閱[價格頁面](https://azure.microsoft.com/pricing/details/storage)。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-117">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="a4ba8-118">**進階受控磁碟和非受控磁碟的價格有何不同？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="a4ba8-119">進階受控磁碟與進階非受控磁碟的價格相同。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-119">The pricing of premium managed disks is the same as unmanaged premium disks.</span></span>

<span data-ttu-id="a4ba8-120">**我是否可以變更受控磁碟的儲存體帳戶類型 (標準或進階)？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-120">**Can I change the storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="a4ba8-121">是。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-121">Yes.</span></span> <span data-ttu-id="a4ba8-122">您可以使用 Azure 入口網站、PowerShell 或 Azure CLI 來變更受控磁碟的儲存體帳戶類型。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-122">You can change the storage account type of your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="a4ba8-123">**是否有方法可以將受控磁碟複製或匯出至私人儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-123">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="a4ba8-124">是。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-124">Yes.</span></span> <span data-ttu-id="a4ba8-125">您可以使用 Azure 入口網站、PowerShell 或 Azure CLI 來匯出受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-125">You can export your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="a4ba8-126">**我是否可以使用 Azure 儲存體帳戶中的 VHD 檔案，透過不同的訂用帳戶來建立受控磁碟？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-126">**Can I use a VHD file in an Azure storage account to create a managed disk with a different subscription?**</span></span>

<span data-ttu-id="a4ba8-127">否。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-127">No.</span></span>

<span data-ttu-id="a4ba8-128">**我是否可以使用 Azure 儲存體帳戶中的 VHD 檔案在不同的區域中建立受控磁碟？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-128">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span></span>

<span data-ttu-id="a4ba8-129">否。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-129">No.</span></span>

<span data-ttu-id="a4ba8-130">**客戶使用受控磁碟時是否有任何規模限制？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="a4ba8-131">受控磁碟沒有儲存體帳戶方面的限制。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-131">Managed Disks eliminates the limits associated with storage accounts.</span></span> <span data-ttu-id="a4ba8-132">不過，依預設，每一訂用帳戶的受控磁碟數目限制是 2,000 個。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-132">However, the number of managed disks per subscription is limited to 2,000 by default.</span></span> <span data-ttu-id="a4ba8-133">您可以連絡支援人員來增加此數目。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-133">You can call support to increase this number.</span></span>

<span data-ttu-id="a4ba8-134">**我是否可以建立受控磁碟的增量快照集？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="a4ba8-135">否。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-135">No.</span></span> <span data-ttu-id="a4ba8-136">目前的快照集功能會建立受控磁碟的完整複本。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-136">The current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="a4ba8-137">不過，我們已規劃在未來支援增量快照集。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-137">However, we are planning to support incremental snapshots in the future.</span></span>

<span data-ttu-id="a4ba8-138">**可用性設定組中的 VM 是否可以由受控和非受控磁碟混合組成？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="a4ba8-139">否。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-139">No.</span></span> <span data-ttu-id="a4ba8-140">可用性設定組中的 VM 必須全部使用受控磁碟，或全部使用非受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-140">The VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="a4ba8-141">當您建立可用性設定組時，可以選擇想要使用的磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-141">When you create an availability set, you can choose which type of disks you want to use.</span></span>

<span data-ttu-id="a4ba8-142">**受控磁碟是否為 Azure 入口網站中的預設選項？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-142">**Is Managed Disks the default option in the Azure portal?**</span></span>

<span data-ttu-id="a4ba8-143">目前不是，但未來會變成預設值。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-143">Not currently, but it will become the default in the future.</span></span>

<span data-ttu-id="a4ba8-144">**我是否可以建立空的受控磁碟？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="a4ba8-145">是。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-145">Yes.</span></span> <span data-ttu-id="a4ba8-146">您可以建立空的磁碟。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-146">You can create an empty disk.</span></span> <span data-ttu-id="a4ba8-147">受控磁碟可在 VM 外獨立建立，例如，不連結至 VM。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-147">A managed disk can be created independently of a VM, for example, without attaching it to a VM.</span></span>

<span data-ttu-id="a4ba8-148">**使用受控磁碟的可用性設定組支援的容錯網域計數為何？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-148">**What is the supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="a4ba8-149">根據使用受控磁碟的可用性設定組所在區域，支援的容錯網域計數為 2 或 3。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-149">Depending on the region where the availability set that uses Managed Disks is located, the supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="a4ba8-150">**如何設定診斷的標準儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-150">**How is the standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="a4ba8-151">您需要為 VM 診斷設定私人儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="a4ba8-152">在未來，我們規劃也將診斷切換至受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-152">In the future, we plan to switch diagnostics to Managed Disks as well.</span></span>

<span data-ttu-id="a4ba8-153">**受控磁碟適用何種角色型存取控制支援？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="a4ba8-154">受控磁碟支援三個主要預設角色︰</span><span class="sxs-lookup"><span data-stu-id="a4ba8-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="a4ba8-155">擁有者：可以管理所有項目，包括存取</span><span class="sxs-lookup"><span data-stu-id="a4ba8-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="a4ba8-156">參與者：可以管理存取以外的所有項目</span><span class="sxs-lookup"><span data-stu-id="a4ba8-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="a4ba8-157">讀取者：可以檢視所有項目，但是無法進行變更</span><span class="sxs-lookup"><span data-stu-id="a4ba8-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="a4ba8-158">**是否有方法可以將受控磁碟複製或匯出至私人儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-158">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="a4ba8-159">您可以取得受控磁碟的唯讀共用存取簽章 URI，並使用它將內容複製到私人儲存體帳戶或內部部署儲存體。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-159">You can get a read-only shared access signature URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span></span>

<span data-ttu-id="a4ba8-160">**我是否可以建立受控磁碟的複本？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="a4ba8-161">客戶可以建立受控磁碟的快照集，然後使用快照集建立另一個受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-161">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span></span>

<span data-ttu-id="a4ba8-162">**是否仍然支援非受控磁碟？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="a4ba8-163">是。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-163">Yes.</span></span> <span data-ttu-id="a4ba8-164">我們支援受控磁碟和非受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="a4ba8-165">我們建議您使用受控磁碟來處理新的工作負載，並將您目前的工作負載移轉至受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-165">We recommend that you use managed disks for new workloads and migrate your current workloads to managed disks.</span></span>


<span data-ttu-id="a4ba8-166">**如果我建立大小為 128 GB 的磁碟，然後將大小增加至 130 GB，我是否必須支付下一個磁碟大小 (512 GB) 的費用？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-166">**If I create a 128-GB disk and then increase the size to 130 GB, will I be charged for the next disk size (512 GB)?**</span></span>

<span data-ttu-id="a4ba8-167">是。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-167">Yes.</span></span>

<span data-ttu-id="a4ba8-168">**我是否可以建立本地備援儲存體、異地備援儲存體和區域備援儲存體受控磁碟？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="a4ba8-169">Azure 受控磁碟目前只支援本地備援儲存體受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="a4ba8-170">**我是否可以壓縮受控磁碟或縮減其大小？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="a4ba8-171">否。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-171">No.</span></span> <span data-ttu-id="a4ba8-172">目前不受支援此功能。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="a4ba8-173">**當特製化 (不是透過使用系統準備工具或一般化所建立) 作業系統磁碟用來佈建 VM 時，我是否可以變更電腦名稱屬性？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-173">**Can I change the computer name property when a specialized (not created by using the System Preparation tool or generalized) operating system disk is used to provision a VM?**</span></span>

<span data-ttu-id="a4ba8-174">否。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-174">No.</span></span> <span data-ttu-id="a4ba8-175">您無法更新電腦名稱屬性。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-175">You can't update the computer name property.</span></span> <span data-ttu-id="a4ba8-176">新的 VM 將從其父 VM 繼承它，並用來建立作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-176">The new VM inherits it from the parent VM, which was used to create the operating system disk.</span></span> 

<span data-ttu-id="a4ba8-177">**哪裡可以找到 Azure Resource Manager 範本範例以建立具有受控磁碟的 VM**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-177">**Where can I find sample Azure Resource Manager templates to create VMs with managed disks?**</span></span>
* [<span data-ttu-id="a4ba8-178">使用受控磁碟的範本清單</span><span class="sxs-lookup"><span data-stu-id="a4ba8-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="a4ba8-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="a4ba8-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="a4ba8-180">受控磁碟和儲存體服務加密</span><span class="sxs-lookup"><span data-stu-id="a4ba8-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="a4ba8-181">**當我建立受控磁碟時，依預設是否啟用 Azure 儲存體服務加密？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="a4ba8-182">是。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-182">Yes.</span></span>

<span data-ttu-id="a4ba8-183">**誰負責管理加密金鑰？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-183">**Who manages the encryption keys?**</span></span>

<span data-ttu-id="a4ba8-184">Microsoft 負責管理加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-184">Microsoft manages the encryption keys.</span></span>

<span data-ttu-id="a4ba8-185">**我是否可以停用受控磁碟的儲存體服務加密？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="a4ba8-186">否。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-186">No.</span></span>

<span data-ttu-id="a4ba8-187">**儲存體服務加密是否僅供特定地區使用？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="a4ba8-188">否。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-188">No.</span></span> <span data-ttu-id="a4ba8-189">它在受控磁碟可以使用的區域中都有提供。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-189">It's available in all the regions where Managed Disks is available.</span></span> <span data-ttu-id="a4ba8-190">受控磁碟在所有公開區域和德國都有提供。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="a4ba8-191">**如何查看我的受控磁碟是否加密？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="a4ba8-192">您可以從 Azure 入口網站、Azure CLI 和 PowerShell 找出建立受控磁碟的時間。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-192">You can find out the time when a managed disk was created from the Azure portal, the Azure CLI, and PowerShell.</span></span> <span data-ttu-id="a4ba8-193">如果時間是在 2017 年 6 月 9 日之後，那麼您的磁碟是加密的。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-193">If the time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="a4ba8-194">**如何加密我在 2017 年 6 月 10 日之前建立的現有磁碟？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="a4ba8-195">自 2017 年 6 月 10 日起，系統會自動將寫入現有受控磁碟的新資料加密。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-195">As of June 10, 2017, new data written to existing managed disks is automatically encrypted.</span></span> <span data-ttu-id="a4ba8-196">我們也計劃對現有資料進行加密，加密將以非同步方式在背景處理。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-196">We are also planning to encrypt existing data, and the encryption will happen asynchronously in the background.</span></span> <span data-ttu-id="a4ba8-197">如果您現在必須加密現有資料，請建立一份磁碟複本。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="a4ba8-198">新的磁碟將會加密。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="a4ba8-199">使用 Azure CLI 複製受控磁碟</span><span class="sxs-lookup"><span data-stu-id="a4ba8-199">Copy managed disks by using the Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="a4ba8-200">使用 PowerShell 複製受控磁碟</span><span class="sxs-lookup"><span data-stu-id="a4ba8-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="a4ba8-201">**受管理的快照集和映像是否加密？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="a4ba8-202">是。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-202">Yes.</span></span> <span data-ttu-id="a4ba8-203">2017 年 6 月 9 日後建立之所有受管理的快照集和映像都將自動加密。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="a4ba8-204">**我是否可以將具有非受控磁碟 (位於之前已加密的儲存體帳戶上) 的 VM 轉換為受控磁碟？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span></span>

<span data-ttu-id="a4ba8-205">是</span><span class="sxs-lookup"><span data-stu-id="a4ba8-205">Yes</span></span>

<span data-ttu-id="a4ba8-206">**從受控磁碟或快照集匯出的 VHD 是否也會加密？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="a4ba8-207">否。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-207">No.</span></span> <span data-ttu-id="a4ba8-208">但是，如果將 VHD 從加密的受控磁碟或快照集匯出到加密儲存體帳戶，則會將它加密。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-208">But if you export a VHD to an encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="a4ba8-209">進階磁碟：受控和非受控</span><span class="sxs-lookup"><span data-stu-id="a4ba8-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="a4ba8-210">**如果 VM 使用的大小系列支援進階儲存體，例如 DSv2，我是否可以同時連結進階和標準資料磁碟？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="a4ba8-211">是。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-211">Yes.</span></span>

<span data-ttu-id="a4ba8-212">**我是否可以同時將進階和標準資料磁碟連結至不支援進階儲存體的大小系列？例如 D、Dv2、G 或 F 系列？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-212">**Can I attach both premium and standard data disks to a size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="a4ba8-213">否。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-213">No.</span></span> <span data-ttu-id="a4ba8-214">只有當 VM 未使用支援進階儲存體的大小系列時，您才能將標準資料磁碟連結至 VM。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-214">You can attach only standard data disks to VMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="a4ba8-215">**如果我從現有的 VHD (大小為 80 GB) 建立進階資料磁碟，需要多少費用？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="a4ba8-216">從 80 GB VHD 建立的進階資料磁碟會被視為下一個可用的進階磁碟大小 (P10 磁碟)。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-216">A premium data disk created from an 80-GB VHD is treated as the next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="a4ba8-217">將根據 P10 磁碟定價向您收費。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-217">You're charged according to the P10 disk pricing.</span></span>

<span data-ttu-id="a4ba8-218">**使用進階儲存體是否有交易成本？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-218">**Are there transaction costs to use Premium Storage?**</span></span>

<span data-ttu-id="a4ba8-219">依 IOPS 和輸送量的特定限制而佈建的每個磁碟大小，都有固定成本。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="a4ba8-220">其他成本包括輸出頻寬和快照集容量 (如果適用的話)。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-220">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="a4ba8-221">如需詳細資訊，請參閱[價格頁面](https://azure.microsoft.com/pricing/details/storage)。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-221">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="a4ba8-222">**我可以從磁碟快取取得的 IOPS 和輸送量有何限制？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-222">**What are the limits for IOPS and throughput that I can get from the disk cache?**</span></span>

<span data-ttu-id="a4ba8-223">DS 系列的快取和本機 SSD 合併限制是每個核心 4,000 IOPS，以及每個核心每秒 33 MB。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-223">The combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="a4ba8-224">GS 系列提供每個核心 5,000 IOPS，以及每個核心每秒 50 MB。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-224">The GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="a4ba8-225">**受控磁碟 VM 是否支援本機 SSD？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-225">**Is the local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="a4ba8-226">本機 SSD 是受控磁碟 VM 隨附的暫時儲存體。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-226">The local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="a4ba8-227">暫時儲存體不需額外的成本。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="a4ba8-228">建議您不要使用本機 SSD 來儲存應用程式資料，因為它不會保留在 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-228">We recommend that you do not use this local SSD to store your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="a4ba8-229">**在進階磁碟上使用 TRIM 是否有任何影響？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-229">**Are there any repercussions for the use of TRIM on premium disks?**</span></span>

<span data-ttu-id="a4ba8-230">在進階或標準磁碟的 Azure 磁碟上使用 TRIM 並無任何不妥。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-230">There is no downside to the use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="a4ba8-231">新磁碟大小：受控和非受控</span><span class="sxs-lookup"><span data-stu-id="a4ba8-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="a4ba8-232">**作業系統和資料磁碟支援的最大磁碟大小是多少？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-232">**What is the largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="a4ba8-233">Azure 針對作業系統磁碟所支援的磁碟分割類型是主開機記錄 (MBR)。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-233">The partition type that Azure supports for an operating system disk is the master boot record (MBR).</span></span> <span data-ttu-id="a4ba8-234">MBR 格式支援的磁碟大小上限為 2 TB。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-234">The MBR format supports a disk size up to 2 TB.</span></span> <span data-ttu-id="a4ba8-235">Azure 針對作業系統磁碟支援的大小上限為 2 TB。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-235">The largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="a4ba8-236">Azure 支援最大 4 TB 的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-236">Azure supports up to 4 TB for data disks.</span></span> 

<span data-ttu-id="a4ba8-237">**支援的分頁 Blob 大小上限是多少？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-237">**What is the largest page blob size that's supported?**</span></span>

<span data-ttu-id="a4ba8-238">Azure 支援的分頁 Blob 大小上限是 8 TB (8,191 GB)。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-238">The largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="a4ba8-239">我們不支援將大於 4 TB (4,095 GB) 的分頁 Blob 連結到 VM 作為資料或作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-239">We don't support page blobs larger than 4 TB (4,095 GB) attached to a VM as data or operating system disks.</span></span>

<span data-ttu-id="a4ba8-240">**我是否需要使用新版 Azure 工具來建立磁碟、連結磁碟、調整磁碟大小及上傳大於 1 TB 的磁碟？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-240">**Do I need to use a new version of Azure tools to create, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="a4ba8-241">您不需要升級現有的 Azure工具來建立磁碟、連結磁碟或調整大於1 TB 的磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-241">You don't need to upgrade your existing Azure tools to create, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="a4ba8-242">若要將 VHD 檔案從內部部署直接上傳到 Azure 作為分頁 Blob 或非受控磁碟，您需要使用最新的工具集：</span><span class="sxs-lookup"><span data-stu-id="a4ba8-242">To upload your VHD file from on-premises directly to Azure as a page blob or unmanaged disk, you need to use the latest tool sets:</span></span>

|<span data-ttu-id="a4ba8-243">Azure 工具</span><span class="sxs-lookup"><span data-stu-id="a4ba8-243">Azure tools</span></span>      | <span data-ttu-id="a4ba8-244">支援的版本</span><span class="sxs-lookup"><span data-stu-id="a4ba8-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="a4ba8-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4ba8-245">Azure PowerShell</span></span> | <span data-ttu-id="a4ba8-246">版本號碼 4.1.0：2017 年 6 月發行或更新版本</span><span class="sxs-lookup"><span data-stu-id="a4ba8-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="a4ba8-247">Azure CLI v1</span><span class="sxs-lookup"><span data-stu-id="a4ba8-247">Azure CLI v1</span></span>     | <span data-ttu-id="a4ba8-248">版本號碼 0.10.13：2017 年 5 月發行或更新版本</span><span class="sxs-lookup"><span data-stu-id="a4ba8-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="a4ba8-249">AzCopy</span><span class="sxs-lookup"><span data-stu-id="a4ba8-249">AzCopy</span></span>           | <span data-ttu-id="a4ba8-250">版本號碼 6.1.0：2017 年 6 月發行或更新版本</span><span class="sxs-lookup"><span data-stu-id="a4ba8-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="a4ba8-251">即將支援 Azure CLI v2 和 Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-251">The support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="a4ba8-252">**針對非受控磁碟或分頁 Blob，是否支援 P4 和 P6 磁碟大小？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="a4ba8-253">否。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-253">No.</span></span> <span data-ttu-id="a4ba8-254">只有受控磁碟才支援 P4 (32 GB) 和 P6 (64 GB) 磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="a4ba8-255">即將支援非受控磁碟和分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="a4ba8-256">**如果小於 64 GB 的現有進階受控磁碟，是在啟用小型磁碟 (2017 年 6 月 15 日前後) 之前建立，該如何計費？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-256">**If my existing premium managed disk less than 64 GB was created before the small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="a4ba8-257">根據 P10 定價層，小於 64 GB 的現有小型進階磁碟繼續計費。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-257">Existing small premium disks less than 64 GB continue to be billed according to the P10 pricing tier.</span></span> 

<span data-ttu-id="a4ba8-258">**我要如何將小於 64 GB 的小型進階磁碟的磁碟層，從 P10 切換到 P4 或 P6？**</span><span class="sxs-lookup"><span data-stu-id="a4ba8-258">**How can I switch the disk tier of small premium disks less than 64 GB from P10 to P4 or P6?**</span></span>

<span data-ttu-id="a4ba8-259">您可以為小型磁碟建立快照集，然後建立一個磁碟，根據佈建大小自動將定價層切換為 P4 或 P6。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-259">You can take a snapshot of your small disks and then create a disk to automatically switch the pricing tier to P4 or P6 based on the provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="a4ba8-260">如果這裡沒有解答我的問題該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="a4ba8-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="a4ba8-261">如果這裡未列出您的問題，請告訴我們，我們將協助您找到答案。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="a4ba8-262">您可以在此文章結尾處將問題張貼在註解中。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-262">You can post a question at the end of this article in the comments.</span></span> <span data-ttu-id="a4ba8-263">若要就此文章與 Azure 儲存體小組和其他社群成員互動，請使用 MSDN [Azure 儲存體論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-263">To engage with the Azure Storage team and other community members about this article, use the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="a4ba8-264">若要提出功能要求，請將要求和想法提交到 [Azure 儲存體意見反應論壇](https://feedback.azure.com/forums/217298-storage)。</span><span class="sxs-lookup"><span data-stu-id="a4ba8-264">To request features, submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
