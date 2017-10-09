# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="eff46-101">關於 Azure IaaS VM 磁碟及受控和非受控進階磁碟的常見問題集</span><span class="sxs-lookup"><span data-stu-id="eff46-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="eff46-102">此文章將回答有關 Azure 受控磁碟和 Azure 進階儲存體的一些常見問題。</span><span class="sxs-lookup"><span data-stu-id="eff46-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="eff46-103">受控磁碟</span><span class="sxs-lookup"><span data-stu-id="eff46-103">Managed Disks</span></span>

<span data-ttu-id="eff46-104">**何謂 Azure 受控磁碟？**</span><span class="sxs-lookup"><span data-stu-id="eff46-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="eff46-105">受控磁碟是可以為您管理儲存體帳戶而簡化 Azure IaaS VM 磁碟管理的一項功能。</span><span class="sxs-lookup"><span data-stu-id="eff46-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="eff46-106">如需詳細資訊，請參閱 hello[管理磁碟概觀](../articles/virtual-machines/windows/managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="eff46-106">For more information, see hello [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="eff46-107">**如果我從現有的 VHD (大小為 80 GB) 建立標準受控磁碟，需要多少費用？**</span><span class="sxs-lookup"><span data-stu-id="eff46-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="eff46-108">80 GB VHD 從建立標準受管理的磁碟視為與 hello 下一個可用的標準磁碟大小，也就是 S10 磁碟相同。</span><span class="sxs-lookup"><span data-stu-id="eff46-108">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="eff46-109">相應 toohello S10 磁碟價格收費。</span><span class="sxs-lookup"><span data-stu-id="eff46-109">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="eff46-110">如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/storage)。</span><span class="sxs-lookup"><span data-stu-id="eff46-110">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="eff46-111">**標準受控磁碟有任何交易成本嗎？**</span><span class="sxs-lookup"><span data-stu-id="eff46-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="eff46-112">是。</span><span class="sxs-lookup"><span data-stu-id="eff46-112">Yes.</span></span> <span data-ttu-id="eff46-113">我們會根據每一筆交易向您收費。</span><span class="sxs-lookup"><span data-stu-id="eff46-113">You're charged for each transaction.</span></span> <span data-ttu-id="eff46-114">如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/storage)。</span><span class="sxs-lookup"><span data-stu-id="eff46-114">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="eff46-115">**標準的受管理磁碟要收費 hello hello hello 磁碟資料的實際大小或佈建的 hello hello 磁碟容量？**</span><span class="sxs-lookup"><span data-stu-id="eff46-115">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="eff46-116">收費根據佈建的 hello hello 磁碟容量。</span><span class="sxs-lookup"><span data-stu-id="eff46-116">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="eff46-117">如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/storage)。</span><span class="sxs-lookup"><span data-stu-id="eff46-117">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="eff46-118">**進階受控磁碟和非受控磁碟的價格有何不同？**</span><span class="sxs-lookup"><span data-stu-id="eff46-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="eff46-119">hello 定價的受管理的高階磁碟是 hello 與未受管理的高階磁碟相同。</span><span class="sxs-lookup"><span data-stu-id="eff46-119">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="eff46-120">**可以變更 hello 儲存體帳戶類型 （Standard 或 Premium） 的 我的受管理磁碟嗎？**</span><span class="sxs-lookup"><span data-stu-id="eff46-120">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="eff46-121">是。</span><span class="sxs-lookup"><span data-stu-id="eff46-121">Yes.</span></span> <span data-ttu-id="eff46-122">您可以使用 hello Azure 入口網站、 PowerShell 或 hello Azure CLI 變更 hello 儲存體帳戶類型的受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="eff46-122">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="eff46-123">**有我可以複製或匯出受管理的磁碟 tooa 私人儲存體帳戶的方法嗎？**</span><span class="sxs-lookup"><span data-stu-id="eff46-123">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="eff46-124">是。</span><span class="sxs-lookup"><span data-stu-id="eff46-124">Yes.</span></span> <span data-ttu-id="eff46-125">您可以使用 hello Azure 入口網站、 PowerShell 或 hello Azure CLI 匯出受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="eff46-125">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="eff46-126">**可以使用 Azure 儲存體帳戶 toocreate 受管理磁碟的 VHD 檔案與不同的訂用帳戶嗎？**</span><span class="sxs-lookup"><span data-stu-id="eff46-126">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="eff46-127">否。</span><span class="sxs-lookup"><span data-stu-id="eff46-127">No.</span></span>

<span data-ttu-id="eff46-128">**可以使用 Azure 儲存體帳戶 toocreate 受管理磁碟的 VHD 檔案位於不同的區域嗎？**</span><span class="sxs-lookup"><span data-stu-id="eff46-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="eff46-129">否。</span><span class="sxs-lookup"><span data-stu-id="eff46-129">No.</span></span>

<span data-ttu-id="eff46-130">**客戶使用受控磁碟時是否有任何規模限制？**</span><span class="sxs-lookup"><span data-stu-id="eff46-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="eff46-131">受管理的磁碟排除 hello 限制與儲存體帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="eff46-131">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="eff46-132">不過，每個訂閱受管理的磁碟的 hello 數目為有限的 too2，根據預設 000。</span><span class="sxs-lookup"><span data-stu-id="eff46-132">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="eff46-133">您可以呼叫支援 tooincrease 這個數字。</span><span class="sxs-lookup"><span data-stu-id="eff46-133">You can call support tooincrease this number.</span></span>

<span data-ttu-id="eff46-134">**我是否可以建立受控磁碟的增量快照集？**</span><span class="sxs-lookup"><span data-stu-id="eff46-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="eff46-135">否。</span><span class="sxs-lookup"><span data-stu-id="eff46-135">No.</span></span> <span data-ttu-id="eff46-136">hello 目前的快照集功能可讓受管理磁碟的完整複本。</span><span class="sxs-lookup"><span data-stu-id="eff46-136">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="eff46-137">不過，我們正計劃在未來的 hello toosupport 增量快照。</span><span class="sxs-lookup"><span data-stu-id="eff46-137">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="eff46-138">**可用性設定組中的 VM 是否可以由受控和非受控磁碟混合組成？**</span><span class="sxs-lookup"><span data-stu-id="eff46-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="eff46-139">否。</span><span class="sxs-lookup"><span data-stu-id="eff46-139">No.</span></span> <span data-ttu-id="eff46-140">所有受管理的磁碟或未受管理的所有磁碟，必須使用可用性設定組中的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="eff46-140">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="eff46-141">當您建立可用性設定組時，您可以選擇哪一種磁碟想 toouse。</span><span class="sxs-lookup"><span data-stu-id="eff46-141">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="eff46-142">**管理磁碟 hello 預設選項處於 hello Azure 入口網站？**</span><span class="sxs-lookup"><span data-stu-id="eff46-142">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="eff46-143">目前不可以，但是它會變成 hello 預設，在未來的 hello。</span><span class="sxs-lookup"><span data-stu-id="eff46-143">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="eff46-144">**我是否可以建立空的受控磁碟？**</span><span class="sxs-lookup"><span data-stu-id="eff46-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="eff46-145">是。</span><span class="sxs-lookup"><span data-stu-id="eff46-145">Yes.</span></span> <span data-ttu-id="eff46-146">您可以建立空的磁碟。</span><span class="sxs-lookup"><span data-stu-id="eff46-146">You can create an empty disk.</span></span> <span data-ttu-id="eff46-147">受管理的磁碟可以建立獨立 VM，比方說，而不用附加它 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="eff46-147">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="eff46-148">**什麼是支援的 hello 容錯網域計數的可用性設定組來使用受管理磁碟？**</span><span class="sxs-lookup"><span data-stu-id="eff46-148">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="eff46-149">依據 hello hello 可用性設定組來使用受管理磁碟所在的地區，hello 支援容錯網域計數是 2 或 3。</span><span class="sxs-lookup"><span data-stu-id="eff46-149">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="eff46-150">**如何為 hello 診斷設定的標準儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="eff46-150">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="eff46-151">您需要為 VM 診斷設定私人儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="eff46-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="eff46-152">我們計劃在未來的 hello，tooswitch 診斷也 tooManaged 磁碟。</span><span class="sxs-lookup"><span data-stu-id="eff46-152">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="eff46-153">**受控磁碟適用何種角色型存取控制支援？**</span><span class="sxs-lookup"><span data-stu-id="eff46-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="eff46-154">受控磁碟支援三個主要預設角色︰</span><span class="sxs-lookup"><span data-stu-id="eff46-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="eff46-155">擁有者：可以管理所有項目，包括存取</span><span class="sxs-lookup"><span data-stu-id="eff46-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="eff46-156">參與者：可以管理存取以外的所有項目</span><span class="sxs-lookup"><span data-stu-id="eff46-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="eff46-157">讀取者：可以檢視所有項目，但是無法進行變更</span><span class="sxs-lookup"><span data-stu-id="eff46-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="eff46-158">**有我可以複製或匯出受管理的磁碟 tooa 私人儲存體帳戶的方法嗎？**</span><span class="sxs-lookup"><span data-stu-id="eff46-158">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="eff46-159">您可以取得 toocopy hello 內容 tooa 私用儲存體帳戶或內部部署儲存體的唯讀共用的存取簽章 URI hello 管理磁碟，並使用它。</span><span class="sxs-lookup"><span data-stu-id="eff46-159">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="eff46-160">**我是否可以建立受控磁碟的複本？**</span><span class="sxs-lookup"><span data-stu-id="eff46-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="eff46-161">客戶可以擷取受管理的磁碟的快照，然後再使用 hello 快照 toocreate 受管理的另一個磁碟。</span><span class="sxs-lookup"><span data-stu-id="eff46-161">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="eff46-162">**是否仍然支援非受控磁碟？**</span><span class="sxs-lookup"><span data-stu-id="eff46-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="eff46-163">是。</span><span class="sxs-lookup"><span data-stu-id="eff46-163">Yes.</span></span> <span data-ttu-id="eff46-164">我們支援受控磁碟和非受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="eff46-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="eff46-165">我們建議您針對新的工作負載使用受管理的磁碟，並移轉您目前的工作負載 toomanaged 磁碟。</span><span class="sxs-lookup"><span data-stu-id="eff46-165">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="eff46-166">**如果我建立 128 GB 的磁碟，然後再增加 hello 大小 too130 GB，將我支付 hello 下一個磁碟的大小 (512 GB)？**</span><span class="sxs-lookup"><span data-stu-id="eff46-166">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="eff46-167">是。</span><span class="sxs-lookup"><span data-stu-id="eff46-167">Yes.</span></span>

<span data-ttu-id="eff46-168">**我是否可以建立本地備援儲存體、異地備援儲存體和區域備援儲存體受控磁碟？**</span><span class="sxs-lookup"><span data-stu-id="eff46-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="eff46-169">Azure 受控磁碟目前只支援本地備援儲存體受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="eff46-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="eff46-170">**我是否可以壓縮受控磁碟或縮減其大小？**</span><span class="sxs-lookup"><span data-stu-id="eff46-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="eff46-171">否。</span><span class="sxs-lookup"><span data-stu-id="eff46-171">No.</span></span> <span data-ttu-id="eff46-172">目前不受支援此功能。</span><span class="sxs-lookup"><span data-stu-id="eff46-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="eff46-173">**當特殊的 （不使用 hello 系統準備工具所建立或一般化） 操作系統磁碟使用的 tooprovision VM 可以變更 hello 電腦 name 屬性嗎？**</span><span class="sxs-lookup"><span data-stu-id="eff46-173">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="eff46-174">否。</span><span class="sxs-lookup"><span data-stu-id="eff46-174">No.</span></span> <span data-ttu-id="eff46-175">您無法更新 hello 電腦名稱 屬性。</span><span class="sxs-lookup"><span data-stu-id="eff46-175">You can't update hello computer name property.</span></span> <span data-ttu-id="eff46-176">hello 新的 VM 會繼承它 hello 父 VM，這是使用的 toocreate hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="eff46-176">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="eff46-177">**哪裡可以找到範例 Azure Resource Manager 範本 toocreate 與受管理磁碟 Vm？**</span><span class="sxs-lookup"><span data-stu-id="eff46-177">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="eff46-178">使用受控磁碟的範本清單</span><span class="sxs-lookup"><span data-stu-id="eff46-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="eff46-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="eff46-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="eff46-180">受控磁碟和儲存體服務加密</span><span class="sxs-lookup"><span data-stu-id="eff46-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="eff46-181">**當我建立受控磁碟時，依預設是否啟用 Azure 儲存體服務加密？**</span><span class="sxs-lookup"><span data-stu-id="eff46-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="eff46-182">是。</span><span class="sxs-lookup"><span data-stu-id="eff46-182">Yes.</span></span>

<span data-ttu-id="eff46-183">**使用者管理 hello 加密金鑰？**</span><span class="sxs-lookup"><span data-stu-id="eff46-183">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="eff46-184">Microsoft 會管理 hello 加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="eff46-184">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="eff46-185">**我是否可以停用受控磁碟的儲存體服務加密？**</span><span class="sxs-lookup"><span data-stu-id="eff46-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="eff46-186">否。</span><span class="sxs-lookup"><span data-stu-id="eff46-186">No.</span></span>

<span data-ttu-id="eff46-187">**儲存體服務加密是否僅供特定地區使用？**</span><span class="sxs-lookup"><span data-stu-id="eff46-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="eff46-188">否。</span><span class="sxs-lookup"><span data-stu-id="eff46-188">No.</span></span> <span data-ttu-id="eff46-189">它提供了管理磁碟可使用的所有 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="eff46-189">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="eff46-190">受控磁碟在所有公開區域和德國都有提供。</span><span class="sxs-lookup"><span data-stu-id="eff46-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="eff46-191">**如何查看我的受控磁碟是否加密？**</span><span class="sxs-lookup"><span data-stu-id="eff46-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="eff46-192">您可以找出 hello hello Azure 入口網站、 hello Azure CLI 和 PowerShell 從受管理的磁碟建立時的時間。</span><span class="sxs-lookup"><span data-stu-id="eff46-192">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="eff46-193">如果 hello 時間之後 2017 年 6 月 9，便會加密您的磁碟。</span><span class="sxs-lookup"><span data-stu-id="eff46-193">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="eff46-194">**如何加密我在 2017 年 6 月 10 日之前建立的現有磁碟？**</span><span class="sxs-lookup"><span data-stu-id="eff46-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="eff46-195">自 2017 年 6 月 10 寫入 tooexisting 管理磁碟的新資料會自動加密。</span><span class="sxs-lookup"><span data-stu-id="eff46-195">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="eff46-196">我們也想要規劃 tooencrypt 現有的資料，並在 hello 背景中將會以非同步方式發生 hello 加密。</span><span class="sxs-lookup"><span data-stu-id="eff46-196">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="eff46-197">如果您現在必須加密現有資料，請建立一份磁碟複本。</span><span class="sxs-lookup"><span data-stu-id="eff46-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="eff46-198">新的磁碟將會加密。</span><span class="sxs-lookup"><span data-stu-id="eff46-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="eff46-199">使用 Azure CLI hello 複製受管理的磁碟</span><span class="sxs-lookup"><span data-stu-id="eff46-199">Copy managed disks by using hello Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="eff46-200">使用 PowerShell 複製受控磁碟</span><span class="sxs-lookup"><span data-stu-id="eff46-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="eff46-201">**受管理的快照集和映像是否加密？**</span><span class="sxs-lookup"><span data-stu-id="eff46-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="eff46-202">是。</span><span class="sxs-lookup"><span data-stu-id="eff46-202">Yes.</span></span> <span data-ttu-id="eff46-203">2017 年 6 月 9 日後建立之所有受管理的快照集和映像都將自動加密。</span><span class="sxs-lookup"><span data-stu-id="eff46-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="eff46-204">**可以轉換 Vm 與位於儲存體帳戶，或已 toomanaged 先前加密的磁碟的 unmanaged 磁碟嗎？**</span><span class="sxs-lookup"><span data-stu-id="eff46-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="eff46-205">是</span><span class="sxs-lookup"><span data-stu-id="eff46-205">Yes</span></span>

<span data-ttu-id="eff46-206">**從受控磁碟或快照集匯出的 VHD 是否也會加密？**</span><span class="sxs-lookup"><span data-stu-id="eff46-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="eff46-207">否。</span><span class="sxs-lookup"><span data-stu-id="eff46-207">No.</span></span> <span data-ttu-id="eff46-208">但如果您匯出 VHD tooan 加密的加密受管理的磁碟或快照集，儲存體帳戶，然後它會加密。</span><span class="sxs-lookup"><span data-stu-id="eff46-208">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="eff46-209">進階磁碟：受控和非受控</span><span class="sxs-lookup"><span data-stu-id="eff46-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="eff46-210">**如果 VM 使用的大小系列支援進階儲存體，例如 DSv2，我是否可以同時連結進階和標準資料磁碟？**</span><span class="sxs-lookup"><span data-stu-id="eff46-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="eff46-211">是。</span><span class="sxs-lookup"><span data-stu-id="eff46-211">Yes.</span></span>

<span data-ttu-id="eff46-212">**可以附加 premium 和 standard 磁碟 tooa 大小之資料數列不支援進階儲存體，例如 D、 Dv2、 G 或 F 數列嗎？**</span><span class="sxs-lookup"><span data-stu-id="eff46-212">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="eff46-213">否。</span><span class="sxs-lookup"><span data-stu-id="eff46-213">No.</span></span> <span data-ttu-id="eff46-214">您可以附加只標準資料磁碟 tooVMs 針對未使用支援進階儲存體大小數列。</span><span class="sxs-lookup"><span data-stu-id="eff46-214">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="eff46-215">**如果我從現有的 VHD (大小為 80 GB) 建立進階資料磁碟，需要多少費用？**</span><span class="sxs-lookup"><span data-stu-id="eff46-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="eff46-216">80 GB VHD 從建立高階資料磁碟會被視為 hello 下一個可用的 premium 磁碟大小，也就是 P10 磁碟。</span><span class="sxs-lookup"><span data-stu-id="eff46-216">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="eff46-217">相應 toohello P10 磁碟價格收費。</span><span class="sxs-lookup"><span data-stu-id="eff46-217">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="eff46-218">**是否有交易成本 toouse 高階儲存體？**</span><span class="sxs-lookup"><span data-stu-id="eff46-218">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="eff46-219">依 IOPS 和輸送量的特定限制而佈建的每個磁碟大小，都有固定成本。</span><span class="sxs-lookup"><span data-stu-id="eff46-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="eff46-220">hello 其他成本包含傳出的頻寬和快照集的容量，如果適用的話。</span><span class="sxs-lookup"><span data-stu-id="eff46-220">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="eff46-221">如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/storage)。</span><span class="sxs-lookup"><span data-stu-id="eff46-221">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="eff46-222">**IOPS 及輸送量我可以從 hello 磁碟快取中取得的 hello 限制有哪些？**</span><span class="sxs-lookup"><span data-stu-id="eff46-222">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="eff46-223">hello 結合的限制快取和本機 SSD DS 系列的每個核心的 4,000 IOPS 和每個核心每秒的 33 MB。</span><span class="sxs-lookup"><span data-stu-id="eff46-223">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="eff46-224">hello GS 系列提供每個核心 5,000 IOPS 和每個核心每秒 50 MB。</span><span class="sxs-lookup"><span data-stu-id="eff46-224">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="eff46-225">**為的 hello 本機 SSD 支援受管理磁碟 VM？**</span><span class="sxs-lookup"><span data-stu-id="eff46-225">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="eff46-226">hello 本機 SSD 是隨附於受管理磁碟 VM 的暫存位置。</span><span class="sxs-lookup"><span data-stu-id="eff46-226">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="eff46-227">暫時儲存體不需額外的成本。</span><span class="sxs-lookup"><span data-stu-id="eff46-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="eff46-228">我們建議您不要使用此本機 SSD toostore 應用程式資料不是保存在 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="eff46-228">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="eff46-229">**會那里任何影響 hello 的空白位置修剪上使用高階磁碟嗎？**</span><span class="sxs-lookup"><span data-stu-id="eff46-229">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="eff46-230">Azure 磁碟上是高階或標準磁碟上的空白位置修剪沒有缺點 toohello 使用了。</span><span class="sxs-lookup"><span data-stu-id="eff46-230">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="eff46-231">新磁碟大小：受控和非受控</span><span class="sxs-lookup"><span data-stu-id="eff46-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="eff46-232">**Hello 支援作業系統和資料磁碟最大磁碟大小為何？**</span><span class="sxs-lookup"><span data-stu-id="eff46-232">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="eff46-233">Azure 支援的作業系統磁碟的 hello 磁碟分割類型為 hello 主開機記錄 (MBR)。</span><span class="sxs-lookup"><span data-stu-id="eff46-233">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="eff46-234">hello MBR 格式支援向上 too2 TB 的磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="eff46-234">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="eff46-235">hello Azure 支援的作業系統磁碟的最大大小為 2 TB。</span><span class="sxs-lookup"><span data-stu-id="eff46-235">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="eff46-236">Azure 支援 too4 TB 的資料磁碟上。</span><span class="sxs-lookup"><span data-stu-id="eff46-236">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="eff46-237">**支援的 hello 最大頁面 blob 大小為何？**</span><span class="sxs-lookup"><span data-stu-id="eff46-237">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="eff46-238">Azure 支援的 hello 最大分頁 blob 大小為 8 TB (8,191 GB)。</span><span class="sxs-lookup"><span data-stu-id="eff46-238">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="eff46-239">我們不支援大於 4 TB (4095 GB) 附加 tooa VM 做為作業系統磁碟或資料的分頁 blob。</span><span class="sxs-lookup"><span data-stu-id="eff46-239">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="eff46-240">**我需要 toouse 新版本的 Azure tools toocreate 附加、 調整大小，並上傳大於 1 TB 的磁碟嗎？**</span><span class="sxs-lookup"><span data-stu-id="eff46-240">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="eff46-241">您不需要 tooupgrade 現有的 Azure tools toocreate、 附加，或調整大小大於 1 TB 的磁碟。</span><span class="sxs-lookup"><span data-stu-id="eff46-241">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="eff46-242">您的 VHD 檔案從 tooupload 內部直接 tooAzure 做為分頁 blob 或未受管理的磁碟，您需要 toouse hello 最新工具組：</span><span class="sxs-lookup"><span data-stu-id="eff46-242">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="eff46-243">Azure 工具</span><span class="sxs-lookup"><span data-stu-id="eff46-243">Azure tools</span></span>      | <span data-ttu-id="eff46-244">支援的版本</span><span class="sxs-lookup"><span data-stu-id="eff46-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="eff46-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="eff46-245">Azure PowerShell</span></span> | <span data-ttu-id="eff46-246">版本號碼 4.1.0：2017 年 6 月發行或更新版本</span><span class="sxs-lookup"><span data-stu-id="eff46-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="eff46-247">Azure CLI v1</span><span class="sxs-lookup"><span data-stu-id="eff46-247">Azure CLI v1</span></span>     | <span data-ttu-id="eff46-248">版本號碼 0.10.13：2017 年 5 月發行或更新版本</span><span class="sxs-lookup"><span data-stu-id="eff46-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="eff46-249">AzCopy</span><span class="sxs-lookup"><span data-stu-id="eff46-249">AzCopy</span></span>           | <span data-ttu-id="eff46-250">版本號碼 6.1.0：2017 年 6 月發行或更新版本</span><span class="sxs-lookup"><span data-stu-id="eff46-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="eff46-251">Azure CLI v2 和 Azure 儲存體總管的 hello 支援即將推出。</span><span class="sxs-lookup"><span data-stu-id="eff46-251">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="eff46-252">**針對非受控磁碟或分頁 Blob，是否支援 P4 和 P6 磁碟大小？**</span><span class="sxs-lookup"><span data-stu-id="eff46-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="eff46-253">否。</span><span class="sxs-lookup"><span data-stu-id="eff46-253">No.</span></span> <span data-ttu-id="eff46-254">只有受控磁碟才支援 P4 (32 GB) 和 P6 (64 GB) 磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="eff46-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="eff46-255">即將支援非受控磁碟和分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="eff46-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="eff46-256">**如果我管理的現有 premium 磁碟小於 hello 少數磁碟啟用 （大約是 2017 年 6 月 15) 之前，已建立 64 GB，如何為它收費？**</span><span class="sxs-lookup"><span data-stu-id="eff46-256">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="eff46-257">現有的小型高階磁碟不超過 64 GB 繼續計費 toobe 相應 toohello P10 定價層。</span><span class="sxs-lookup"><span data-stu-id="eff46-257">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="eff46-258">**我可以切換 hello 磁碟層小於 64 GB 的小型高階磁碟從 P10 tooP4 或 P6？**</span><span class="sxs-lookup"><span data-stu-id="eff46-258">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="eff46-259">您可以擷取您的小型磁碟的快照，然後建立 定價層 tooP4 磁碟 tooautomatically 交換器 hello 或 P6 根據 hello 佈建大小。</span><span class="sxs-lookup"><span data-stu-id="eff46-259">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="eff46-260">如果這裡沒有解答我的問題該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="eff46-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="eff46-261">如果這裡未列出您的問題，請告訴我們，我們將協助您找到答案。</span><span class="sxs-lookup"><span data-stu-id="eff46-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="eff46-262">您可以將在 hello 本文結尾處將問題張貼 hello 註解中。</span><span class="sxs-lookup"><span data-stu-id="eff46-262">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="eff46-263">tooengage 與 hello Azure 儲存體小組及其他社群成員關於本文中，使用 hello MSDN [Azure 儲存體論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)。</span><span class="sxs-lookup"><span data-stu-id="eff46-263">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="eff46-264">toorequest 功能提交您的要求和意見 toohello [Azure 儲存體意見反應論壇](https://feedback.azure.com/forums/217298-storage)。</span><span class="sxs-lookup"><span data-stu-id="eff46-264">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
