---
title: "Azure 虛擬機器具有加速網路 aaaCreate |Microsoft 文件"
description: "深入了解如何 toocreate 具有加速網路的虛擬機器。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="8319a-103">使用加速網路來建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8319a-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="8319a-104">在此教學課程中，您了解如何在 Azure 虛擬機器 (VM) 具有加速網路 toocreate。</span><span class="sxs-lookup"><span data-stu-id="8319a-104">In this tutorial, you learn how toocreate an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="8319a-105">加速網路是 GA for Windows，而且針對特定 Linux 發佈則處於公開預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="8319a-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="8319a-106">加速的網路啟用單一根目錄 I/O 虛擬化 (SR-IOV) tooa VM，大幅改善網路效能。</span><span class="sxs-lookup"><span data-stu-id="8319a-106">Accelerated networking enables single root I/O virtualization (SR-IOV) tooa VM, greatly improving its networking performance.</span></span> <span data-ttu-id="8319a-107">這個高效能的路徑會略過 hello 主機減少延遲、 抖動和與 hello 最嚴苛網路上的工作負載支援的 VM 類型搭配使用的 CPU 使用量，hello 資料路徑。</span><span class="sxs-lookup"><span data-stu-id="8319a-107">This high-performance path bypasses hello host from hello datapath reducing latency, jitter, and CPU utilization, for use with hello most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="8319a-108">下列圖片顯示通訊兩台虛擬機器 (VM)，不使用加速網路與 hello:</span><span class="sxs-lookup"><span data-stu-id="8319a-108">hello following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![比較](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="8319a-110">不使用加速網路，所有的網路流量進出 hello VM 必須穿過 hello 主機和 hello 虛擬交換器。</span><span class="sxs-lookup"><span data-stu-id="8319a-110">Without accelerated networking, all networking traffic in and out of hello VM must traverse hello host and hello virtual switch.</span></span> <span data-ttu-id="8319a-111">hello 虛擬交換器提供所有的原則強制執行，例如網路安全性群組，存取控制清單、 隔離以及其他網路虛擬化服務 toonetwork 流量。</span><span class="sxs-lookup"><span data-stu-id="8319a-111">hello virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services toonetwork traffic.</span></span> <span data-ttu-id="8319a-112">深入了解虛擬交換器，讀取 hello toolearn [HYPER-V 網路虛擬化和虛擬交換器](https://technet.microsoft.com/library/jj945275.aspx)發行項。</span><span class="sxs-lookup"><span data-stu-id="8319a-112">toolearn more about virtual switches, read hello [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="8319a-113">使用加速網路，網路流量送達 hello VM 的網路介面 (NIC)，，然後再轉送 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="8319a-113">With accelerated networking, network traffic arrives at hello VM's network interface (NIC), and is then forwarded toohello VM.</span></span> <span data-ttu-id="8319a-114">沒有的卸載加速的網路，並將其套用在硬體中，適用於所有 hello 虛擬交換器的網路原則。</span><span class="sxs-lookup"><span data-stu-id="8319a-114">All network policies that hello virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="8319a-115">套用原則中的硬體啟用 hello NIC tooforward 網路流量直接 toohello VM，同時維護它套用 hello 主應用程式中的所有 hello 原則略過 hello 主機和虛擬交換器 hello。</span><span class="sxs-lookup"><span data-stu-id="8319a-115">Applying policy in hardware enables hello NIC tooforward network traffic directly toohello VM, bypassing hello host and hello virtual switch, while maintaining all hello policy it applied in hello host.</span></span>

<span data-ttu-id="8319a-116">hello 加速網路功能的優點僅適用於 toohello 啟用的 VM。</span><span class="sxs-lookup"><span data-stu-id="8319a-116">hello benefits of accelerated networking only apply toohello VM that it is enabled on.</span></span> <span data-ttu-id="8319a-117">Hello 獲得最佳結果，它是理想的 tooenable 這項功能至少兩個 Vm 上的連接 toohello 相同 Azure 虛擬網路 (VNet)。</span><span class="sxs-lookup"><span data-stu-id="8319a-117">For hello best results, it is ideal tooenable this feature on at least two VMs connected toohello same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="8319a-118">當跨 Vnet 或連線在內部部署伺服器通訊，這項功能會有影響降到最低 toooverall 延遲。</span><span class="sxs-lookup"><span data-stu-id="8319a-118">When communicating across VNets or connecting on-premises, this feature has minimal impact toooverall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="8319a-119">此 Linux 公用預覽不能有相同的層級的可用性和可靠性功能，因為是的 hello 一般可用性釋放。</span><span class="sxs-lookup"><span data-stu-id="8319a-119">This Linux Public Preview may not have hello same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="8319a-120">hello 功能不支援，可能有限制功能，並可能無法使用所有的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="8319a-120">hello feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="8319a-121">Hello 上這項功能的可用性與狀態的最新通知，請檢查 hello Azure 虛擬網路更新 頁面。</span><span class="sxs-lookup"><span data-stu-id="8319a-121">For hello most up-to-date notifications on availability and status of this feature, check hello Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="8319a-122">優點</span><span class="sxs-lookup"><span data-stu-id="8319a-122">Benefits</span></span>
* <span data-ttu-id="8319a-123">**較低延遲高每秒封包 (pps) 秒：**從 hello 資料路徑移除 hello 虛擬交換器移除原則處理的 hello 主機中的 hello 封包所花的時間並增加 hello 可處理 hello VM 內部的封包數目。</span><span class="sxs-lookup"><span data-stu-id="8319a-123">**Lower Latency / Higher packets per second (pps):** Removing hello virtual switch from hello datapath removes hello time packets spend in hello host for policy processing and increases hello number of packets that can be processed inside hello VM.</span></span>
* <span data-ttu-id="8319a-124">**降低抖動：**虛擬交換器處理取決於 hello 需要 toobe 套用的原則數量和執行 hello 處理的 hello CPU 的 hello 工作負載。</span><span class="sxs-lookup"><span data-stu-id="8319a-124">**Reduced jitter:** Virtual switch processing depends on hello amount of policy that needs toobe applied and hello workload of hello CPU that is doing hello processing.</span></span> <span data-ttu-id="8319a-125">卸載 hello 原則強制 toohello 硬體所傳送的封包，直接 toohello VM，移除 hello 主機 tooVM 通訊和所有軟體插斷和內容切換移除該變化性。</span><span class="sxs-lookup"><span data-stu-id="8319a-125">Offloading hello policy enforcement toohello hardware removes that variability by delivering packets directly toohello VM, removing hello host tooVM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="8319a-126">**降低 CPU 使用率：** hello 主應用程式中的略過 hello 虛擬交換器會導致處理網路流量 tooless CPU 使用率。</span><span class="sxs-lookup"><span data-stu-id="8319a-126">**Decreased CPU utilization:** Bypassing hello virtual switch in hello host leads tooless CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="8319a-127"><a name="Limitations"></a>限制</span><span class="sxs-lookup"><span data-stu-id="8319a-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="8319a-128">使用這項功能時，就會存在 hello 下列限制：</span><span class="sxs-lookup"><span data-stu-id="8319a-128">hello following limitations exist when using this capability:</span></span>

* <span data-ttu-id="8319a-129">**網路介面建立︰**您只能對新的 NIC 啟用加速網路。</span><span class="sxs-lookup"><span data-stu-id="8319a-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="8319a-130">無法對現有 NIC 來啟用。</span><span class="sxs-lookup"><span data-stu-id="8319a-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="8319a-131">**建立 VM:**時 hello 會附加的 tooa VM 建立 VM 只能與加速啟用的網路功能的 NIC。</span><span class="sxs-lookup"><span data-stu-id="8319a-131">**VM creation:** A NIC with accelerated networking enabled can only be attached tooa VM when hello VM is created.</span></span> <span data-ttu-id="8319a-132">hello NIC 不可以是附加的 tooan 現有 VM。</span><span class="sxs-lookup"><span data-stu-id="8319a-132">hello NIC cannot be attached tooan existing VM.</span></span>
* <span data-ttu-id="8319a-133">**區域︰**大多數 Azure 區域都有提供具有加速網路的 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="8319a-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="8319a-134">多個區域都提供具有加速網路的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="8319a-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="8319a-135">展開這項功能可用於 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="8319a-135">hello regions this capability is available in is expanding.</span></span> <span data-ttu-id="8319a-136">請 hello Azure 虛擬網路功能更新的部落格下方 hello 最新的資訊，參閱。</span><span class="sxs-lookup"><span data-stu-id="8319a-136">Please see hello Azure Virtual Networking Updates blog below for hello latest information.</span></span>   
* <span data-ttu-id="8319a-137">**支援的作業系統︰**Windows：Microsoft Windows Server 2012 R2 Datacenter 和 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="8319a-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="8319a-138">Linux：Ubuntu Server 16.04 LTS (含核心 4.4.0-77 或更高版本)、SLES 12 SP2、RHEL 7.3 和 CentOS 7.3 (由 “Rogue Wave Software” 發佈)。</span><span class="sxs-lookup"><span data-stu-id="8319a-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="8319a-139">**VM 大小︰**一般用途和具有八個以上核心的計算最佳化執行個體大小。</span><span class="sxs-lookup"><span data-stu-id="8319a-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="8319a-140">如需詳細資訊，請參閱 hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json)和[Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM 大小的發行項。</span><span class="sxs-lookup"><span data-stu-id="8319a-140">For more information, see hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="8319a-141">hello 的集合支援的 VM 執行個體大小將擴充在未來的 hello。</span><span class="sxs-lookup"><span data-stu-id="8319a-141">hello set of supported VM instance sizes will expand in hello future.</span></span>
* <span data-ttu-id="8319a-142">**僅限透過 Azure Resource Manager (ARM) 進行部署：**您無法透過 ASM/RDFE 部署加速網路。</span><span class="sxs-lookup"><span data-stu-id="8319a-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="8319a-143">變更 toothese 限制上經過宣布透過 hello [Azure 虛擬網路更新](https://azure.microsoft.com/updates/accelerated-networking-in-preview)頁面。</span><span class="sxs-lookup"><span data-stu-id="8319a-143">Changes toothese limitations are announced through hello [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="8319a-144">建立 Windows VM</span><span class="sxs-lookup"><span data-stu-id="8319a-144">Create a Windows VM</span></span>
<span data-ttu-id="8319a-145">您可以使用 hello Azure 入口網站或 Azure [PowerShell](#windows-powershell) toocreate hello VM。</span><span class="sxs-lookup"><span data-stu-id="8319a-145">You can use hello Azure portal or Azure [PowerShell](#windows-powershell) toocreate hello VM.</span></span>

### <span data-ttu-id="8319a-146"><a name="windows-portal"></a>入口網站</span><span class="sxs-lookup"><span data-stu-id="8319a-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="8319a-147">從網際網路瀏覽器中，開啟 hello Azure[入口網站](https://portal.azure.com)並以您的 Azure 登入[帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)。</span><span class="sxs-lookup"><span data-stu-id="8319a-147">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="8319a-148">如果您還沒有帳戶，則可以註冊[免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)帳戶。</span><span class="sxs-lookup"><span data-stu-id="8319a-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="8319a-149">在 hello 入口網站中，按一下  **+ 新增** > **計算** > **Windows Server 2016 Datacenter**。</span><span class="sxs-lookup"><span data-stu-id="8319a-149">In hello portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="8319a-150">在 hello **Windows Server 2016 Datacenter**刀鋒視窗中出現，保持*資源管理員*底下選取**選取部署模型**，按一下**建立**.</span><span class="sxs-lookup"><span data-stu-id="8319a-150">In hello **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="8319a-151">在 hello**基本概念**刀鋒視窗中，輸入下列值的 hello、 保留其餘的預設選項的 hello 或選取或輸入您自己的值，然後按一下 hello**確定**按鈕：</span><span class="sxs-lookup"><span data-stu-id="8319a-151">In hello **Basics** blade that appears, enter hello following values, leave hello remaining default options or select or enter your own values, and click hello **OK** button:</span></span>

    |<span data-ttu-id="8319a-152">設定</span><span class="sxs-lookup"><span data-stu-id="8319a-152">Setting</span></span>|<span data-ttu-id="8319a-153">值</span><span class="sxs-lookup"><span data-stu-id="8319a-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="8319a-154">名稱</span><span class="sxs-lookup"><span data-stu-id="8319a-154">Name</span></span>|<span data-ttu-id="8319a-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="8319a-155">MyVm</span></span>|
    |<span data-ttu-id="8319a-156">資源群組</span><span class="sxs-lookup"><span data-stu-id="8319a-156">Resource group</span></span>|<span data-ttu-id="8319a-157">讓 [新建] 保持選取狀態，並輸入 MyResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8319a-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="8319a-158">位置</span><span class="sxs-lookup"><span data-stu-id="8319a-158">Location</span></span>|<span data-ttu-id="8319a-159">美國西部 2</span><span class="sxs-lookup"><span data-stu-id="8319a-159">West US 2</span></span>|

    <span data-ttu-id="8319a-160">如果您是新 tooAzure，深入了解[資源群組](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group)，[訂閱](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription)，和[位置](https://azure.microsoft.com/regions)（這也是指 tooas 區域）。</span><span class="sxs-lookup"><span data-stu-id="8319a-160">If you're new tooAzure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred tooas regions).</span></span>
5. <span data-ttu-id="8319a-161">在 hello**大小選擇 「**刀鋒視窗中，輸入*8*在 hello**核心下限**方塊，然後按一下 **檢視所有**。</span><span class="sxs-lookup"><span data-stu-id="8319a-161">In hello **Choose a size** blade that appears, enter *8* in hello **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="8319a-162">按一下**DS4_V2 標準**，或任何支援的 VM，然後按一下 [hello**選取**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8319a-162">Click **DS4_V2 Standard**, or any supported VM, then click hello **Select** button.</span></span>
7. <span data-ttu-id="8319a-163">在 hello**設定**刀鋒視窗中出現，讓所有設定，-，除了按一下**啟用**下**加速網路**，然後按一下 [hello**確定** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8319a-163">In hello **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click hello **OK** button.</span></span> <span data-ttu-id="8319a-164">**注意：**如果，在先前步驟中，您選取的 VM 大小、 作業系統或位置的值未列出的 hello[限制](#Limitations)本文中，區段**加速網路**看不到。</span><span class="sxs-lookup"><span data-stu-id="8319a-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in hello [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="8319a-165">在 [hello**摘要**刀鋒視窗中，按一下 hello**確定**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8319a-165">In hello **Summary** blade that appears, click hello **OK** button.</span></span> <span data-ttu-id="8319a-166">Azure 會開始建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="8319a-166">Azure starts creating hello VM.</span></span> <span data-ttu-id="8319a-167">VM 需要花幾分鐘的時間來建立。</span><span class="sxs-lookup"><span data-stu-id="8319a-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="8319a-168">tooinstall hello 加速 windows 網路驅動程式、 完成 hello 步驟 hello[設定 Windows](#configure-windows)本文一節。</span><span class="sxs-lookup"><span data-stu-id="8319a-168">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="8319a-169"><a name="windows-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="8319a-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="8319a-170">安裝 Azure PowerShell hello hello 最新版本[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。</span><span class="sxs-lookup"><span data-stu-id="8319a-170">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="8319a-171">如果您是新 tooAzure PowerShell 時，讀取 hello [Azure PowerShell 概觀](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項。</span><span class="sxs-lookup"><span data-stu-id="8319a-171">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="8319a-172">按一下 hello Windows [開始] 按鈕，啟動 PowerShell 工作階段輸入**powershell**，然後按一下**PowerShell** hello 搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="8319a-172">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="8319a-173">在 PowerShell 視窗中，輸入 hello`login-azurermaccount`入您的 Azure 命令 toosign[帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)。</span><span class="sxs-lookup"><span data-stu-id="8319a-173">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="8319a-174">如果您還沒有帳戶，則可以註冊[免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)帳戶。</span><span class="sxs-lookup"><span data-stu-id="8319a-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="8319a-175">在瀏覽器中，複製下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="8319a-175">In your browser, copy hello following script:</span></span>
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="8319a-176">在 PowerShell 視窗中，以滑鼠右鍵按一下 toopaste hello 指令碼，並開始執行它。</span><span class="sxs-lookup"><span data-stu-id="8319a-176">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="8319a-177">系統會提示您輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="8319a-177">You are prompted for a username and password.</span></span> <span data-ttu-id="8319a-178">當連接 tooit hello 下一個步驟中，請使用這些認證 toolog toohello VM 中。</span><span class="sxs-lookup"><span data-stu-id="8319a-178">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="8319a-179">如果 hello 指令碼失敗，而且您執行之前變更 hello 指令碼中的值，確認您所使用的 VM 大小，作業系統的 hello 值和位置會列在 hello[限制](#Limitations)本文一節。</span><span class="sxs-lookup"><span data-stu-id="8319a-179">If hello script fails, and you changed values in hello script before executing it, confirm hello values you used for VM size, operating system, and location are listed in hello [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="8319a-180">tooinstall hello 加速 windows 網路驅動程式、 完成 hello 步驟 hello[設定 Windows](#configure-windows)本文一節。</span><span class="sxs-lookup"><span data-stu-id="8319a-180">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="8319a-181"><a name="configure-windows"></a>設定 Windows</span><span class="sxs-lookup"><span data-stu-id="8319a-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="8319a-182">一旦您在 Azure 中建立 hello VM，您必須安裝 Windows hello 加速網路驅動程式。</span><span class="sxs-lookup"><span data-stu-id="8319a-182">Once you create hello VM in Azure, you must install hello accelerated networking driver for Windows.</span></span> <span data-ttu-id="8319a-183">在完成之前 hello 下列步驟，您必須建立 Windows VM 使用任一 hello 加速網路[入口網站](#windows-portal)或[PowerShell](#windows-powershell)這篇文章中的步驟。</span><span class="sxs-lookup"><span data-stu-id="8319a-183">Before completing hello following steps, you must have created a Windows VM with accelerated networking using either hello [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="8319a-184">從網際網路瀏覽器中，開啟 hello Azure[入口網站](https://portal.azure.com)並以您的 Azure 登入[帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)。</span><span class="sxs-lookup"><span data-stu-id="8319a-184">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="8319a-185">如果您還沒有帳戶，則可以註冊[免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)帳戶。</span><span class="sxs-lookup"><span data-stu-id="8319a-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="8319a-186">在 hello 方塊包含的 hello 文字*搜尋資源*hello hello Azure 入口網站頂端，在輸入*MyVm*。</span><span class="sxs-lookup"><span data-stu-id="8319a-186">In hello box that contains hello text *Search resources* at hello top of hello Azure portal, type *MyVm*.</span></span> <span data-ttu-id="8319a-187">當**MyVm**會出現在 hello 搜尋結果中，按一下它。</span><span class="sxs-lookup"><span data-stu-id="8319a-187">When **MyVm** appears in hello search results, click it.</span></span>
3. <span data-ttu-id="8319a-188">在 hello **MyVm**刀鋒視窗中，按一下 hello**連接**hello 的左上角 hello 刀鋒視窗中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="8319a-188">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="8319a-189">**注意：**如果**建立**hello 底下看見**連接**按鈕時，Azure 尚未完成建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="8319a-189">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="8319a-190">按一下**連接**只有您無法再查看之後**建立**下 hello**連接** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8319a-190">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
4. <span data-ttu-id="8319a-191">允許您的瀏覽器 toodownload hello **MyVm.rdp**檔案。</span><span class="sxs-lookup"><span data-stu-id="8319a-191">Allow your browser toodownload hello **MyVm.rdp** file.</span></span>  <span data-ttu-id="8319a-192">在下載後，按一下 hello 檔案 tooopen 它。</span><span class="sxs-lookup"><span data-stu-id="8319a-192">Once downloaded, click hello file tooopen it.</span></span> 
5. <span data-ttu-id="8319a-193">按一下 hello**連接**按鈕在 hello**遠端桌面連線**隨即出現，通知您該 hello hello 遠端連線的發行者無法識別的方塊。</span><span class="sxs-lookup"><span data-stu-id="8319a-193">Click hello **Connect** button in hello **Remote Desktop Connection** box that appears, notifying you that hello publisher of hello remote connection can't be identified.</span></span>
6. <span data-ttu-id="8319a-194">在 hello **Windows 安全性**方塊中，按一下**更多選擇**，然後按一下 **使用不同的帳戶**。</span><span class="sxs-lookup"><span data-stu-id="8319a-194">In hello **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="8319a-195">輸入 hello 使用者名稱和您在步驟 4 中，輸入的密碼，然後按一下 [hello**確定**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8319a-195">Enter hello username and password you entered in step 4, then click hello **OK** button.</span></span>
7. <span data-ttu-id="8319a-196">按一下 hello**是**hello 隨即出現，通知您，無法驗證 hello hello 遠端電腦識別的遠端桌面連線方塊中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="8319a-196">Click hello **Yes** button in hello Remote Desktop Connection box that appears, notifying you that hello identity of hello remote computer cannot be verified.</span></span>
8. <span data-ttu-id="8319a-197">以滑鼠右鍵按一下 hello Windows [開始] 按鈕，然後按一下**裝置管理員**。</span><span class="sxs-lookup"><span data-stu-id="8319a-197">Right-click hello Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="8319a-198">展開 hello**網路介面卡**節點。</span><span class="sxs-lookup"><span data-stu-id="8319a-198">Expand hello **Network adapters** node.</span></span> <span data-ttu-id="8319a-199">確認該 hello **Mellanox connectx-3 虛擬函式乙太網路介面卡**隨即出現，如 hello 下列圖片所示：</span><span class="sxs-lookup"><span data-stu-id="8319a-199">Confirm that hello **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in hello following picture:</span></span>
   
    ![裝置管理員](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="8319a-201">現在已啟用您 VM 的加速網路。</span><span class="sxs-lookup"><span data-stu-id="8319a-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="8319a-202">建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="8319a-202">Create a Linux VM</span></span>
<span data-ttu-id="8319a-203">您可以使用 hello Azure 入口網站或 Azure [PowerShell](#linux-powershell) toocreate Ubuntu 或 SLES VM。</span><span class="sxs-lookup"><span data-stu-id="8319a-203">You can use hello Azure portal or Azure [PowerShell](#linux-powershell) toocreate an Ubuntu or SLES VM.</span></span> <span data-ttu-id="8319a-204">RHEL 和 CentOS VM 的工作流程不同。</span><span class="sxs-lookup"><span data-stu-id="8319a-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="8319a-205">請參閱下列的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="8319a-205">Please see hello instructions below.</span></span>

### <span data-ttu-id="8319a-206"><a name="linux-portal"></a>入口網站</span><span class="sxs-lookup"><span data-stu-id="8319a-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="8319a-207">完成步驟 1-5 的 hello 網路 Linux preview 加速 hello 註冊[PowerShell 建立 Linux VM-](#linux-powershell)本文一節。</span><span class="sxs-lookup"><span data-stu-id="8319a-207">Register for hello accelerated networking for Linux preview by completing steps 1-5 of hello [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="8319a-208">您無法註冊 hello 入口網站中的 hello 預覽。</span><span class="sxs-lookup"><span data-stu-id="8319a-208">You cannot register for hello preview in hello portal.</span></span>
2. <span data-ttu-id="8319a-209">完成步驟 1-8 中的 hello[建立 Windows VM-入口網站](#windows-portal)本文一節。</span><span class="sxs-lookup"><span data-stu-id="8319a-209">Complete steps 1-8 in hello [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="8319a-210">在步驟 2 中，按一下 [Ubuntu Server 16.04 LTS] 而不是 [Windows Server 2016 Datacenter]。</span><span class="sxs-lookup"><span data-stu-id="8319a-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="8319a-211">此教學課程中，選擇 toouse 密碼，而不是 SSH 金鑰，但實際執行部署，您可以使用。</span><span class="sxs-lookup"><span data-stu-id="8319a-211">For this tutorial, choose toouse a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="8319a-212">如果**加速網路**不會出現在您完成步驟 7 的 hello[建立 Windows VM-入口網站](#windows-portal)> 一節的本文中，可能是其中一個 hello 下列原因：</span><span class="sxs-lookup"><span data-stu-id="8319a-212">If **Accelerated networking** does not appear when you complete step 7 of hello [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of hello following reasons:</span></span>
    - <span data-ttu-id="8319a-213">尚未登錄 hello 預覽。</span><span class="sxs-lookup"><span data-stu-id="8319a-213">You are not yet registered for hello preview.</span></span> <span data-ttu-id="8319a-214">確認您的註冊狀態是**註冊**hello 的步驟 4 中所述， [Powershell 建立 Linux VM-](#linux-powershell)本文一節。</span><span class="sxs-lookup"><span data-stu-id="8319a-214">Confirm that your registration state is **Registered**, as explained in step 4 of hello [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="8319a-215">**注意：**如果您已參與 hello 加速網路 Windows Vm preview （它的任何較長的必要 tooregister toouse 加速適用於 Windows Vm 網路），您都不會自動註冊 hello 加速的網路Linux Vm 預覽。</span><span class="sxs-lookup"><span data-stu-id="8319a-215">**Note:** If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="8319a-216">您必須註冊 hello 加速網路的 Linux Vm 預覽 tooparticipate 中。</span><span class="sxs-lookup"><span data-stu-id="8319a-216">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
    - <span data-ttu-id="8319a-217">您尚未選取 VM 大小、 作業系統或所列位置中 hello[限制](#limitations)本文一節。</span><span class="sxs-lookup"><span data-stu-id="8319a-217">You have not selected a VM size, operating system, or location listed in hello [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="8319a-218">tooinstall hello 加速適用於 Linux 的網路驅動程式、 完成 hello 步驟 hello[設定 Linux](#configure-linux)本文一節。</span><span class="sxs-lookup"><span data-stu-id="8319a-218">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="8319a-219"><a name="linux-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="8319a-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="8319a-220">如果您建立 Linux Vm 加速網路中的訂用帳戶，然後嘗試 toocreate hello 加速網路功能與 Windows VM 相同的訂用帳戶，hello 建立 Windows VM 可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="8319a-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt toocreate a Windows VM with accelerated networking in hello same subscription, hello Windows VM creation may fail.</span></span> <span data-ttu-id="8319a-221">在預覽版測時期間，建議您在不同的訂用帳戶中測試具有加速網路功能的 Linux 和 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="8319a-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="8319a-222">安裝 Azure PowerShell hello hello 最新版本[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。</span><span class="sxs-lookup"><span data-stu-id="8319a-222">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="8319a-223">如果您是新 tooAzure PowerShell 時，讀取 hello [Azure PowerShell 概觀](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json)發行項。</span><span class="sxs-lookup"><span data-stu-id="8319a-223">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="8319a-224">按一下 hello Windows [開始] 按鈕，啟動 PowerShell 工作階段輸入**powershell**，然後按一下**PowerShell** hello 搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="8319a-224">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="8319a-225">在 PowerShell 視窗中，輸入 hello`login-azurermaccount`入您的 Azure 命令 toosign[帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)。</span><span class="sxs-lookup"><span data-stu-id="8319a-225">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="8319a-226">如果您還沒有帳戶，則可以註冊[免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)帳戶。</span><span class="sxs-lookup"><span data-stu-id="8319a-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="8319a-227">Azure 網路加速 hello 註冊預覽，藉由完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8319a-227">Register for hello accelerated networking for Azure preview by completing hello following steps:</span></span>
    - <span data-ttu-id="8319a-228">傳送電子郵件太[axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e)與您的 Azure 訂用帳戶 ID 預定的用途。</span><span class="sxs-lookup"><span data-stu-id="8319a-228">Send an email too[axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="8319a-229">請等候來自 Microsoft 有關正在啟用您訂用帳戶的電子郵件確認。</span><span class="sxs-lookup"><span data-stu-id="8319a-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="8319a-230">輸入下列命令 tooconfirm hello preview 註冊您的 hello:</span><span class="sxs-lookup"><span data-stu-id="8319a-230">Enter hello following command tooconfirm you are registered for hello preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="8319a-231">請繼續進行步驟 5，直到**註冊**hello 後輸入 hello 前一個命令輸出中會出現。</span><span class="sxs-lookup"><span data-stu-id="8319a-231">Do not continue with step 5 until **Registered** appears in hello output after you enter hello previous command.</span></span> <span data-ttu-id="8319a-232">您的輸出必須看起來像 hello 以下輸出再繼續進行：</span><span class="sxs-lookup"><span data-stu-id="8319a-232">Your output must look like hello following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="8319a-233">如果您已參與 hello 加速網路 Windows Vm preview （它的任何較長的必要 tooregister toouse 加速適用於 Windows Vm 網路），您都不會自動註冊 hello 加速預覽 Linux Vm 的網路功能。</span><span class="sxs-lookup"><span data-stu-id="8319a-233">If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="8319a-234">您必須註冊 hello 加速網路的 Linux Vm 預覽 tooparticipate 中。</span><span class="sxs-lookup"><span data-stu-id="8319a-234">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
      >
5. <span data-ttu-id="8319a-235">在瀏覽器中，複製下列指令碼取代為所需的 Ubuntu 或 SLES hello。</span><span class="sxs-lookup"><span data-stu-id="8319a-235">In your browser, copy hello following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="8319a-236">同樣地，Redhat 和 CentOS 具有不同的工作流程，如下所述：</span><span class="sxs-lookup"><span data-stu-id="8319a-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="8319a-237">在 PowerShell 視窗中，以滑鼠右鍵按一下 toopaste hello 指令碼，並開始執行它。</span><span class="sxs-lookup"><span data-stu-id="8319a-237">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="8319a-238">系統會提示您輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="8319a-238">You are prompted for a username and password.</span></span> <span data-ttu-id="8319a-239">當連接 tooit hello 下一個步驟中，請使用這些認證 toolog toohello VM 中。</span><span class="sxs-lookup"><span data-stu-id="8319a-239">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="8319a-240">如果 hello 指令碼失敗，請確認：</span><span class="sxs-lookup"><span data-stu-id="8319a-240">If hello script fails, confirm that:</span></span>
    - <span data-ttu-id="8319a-241">步驟 4 中所述，您會註冊 hello preview</span><span class="sxs-lookup"><span data-stu-id="8319a-241">You are registered for hello preview, as explained in step 4</span></span>
    - <span data-ttu-id="8319a-242">如果您變更 VM 大小、 作業系統類型或位置值 hello 指令碼中的執行它之前，hello 值會列在 hello[限制](#Limitations)本文一節。</span><span class="sxs-lookup"><span data-stu-id="8319a-242">If you changed VM size, operating system type, or location values in hello script before executing it, that hello values are listed in hello [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="8319a-243">tooinstall hello 加速適用於 Linux 的網路驅動程式、 完成 hello 步驟 hello[設定 Linux](#configure-linux)本文一節。</span><span class="sxs-lookup"><span data-stu-id="8319a-243">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="8319a-244"><a name="configure-linux"></a>設定 Linux</span><span class="sxs-lookup"><span data-stu-id="8319a-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="8319a-245">一旦您在 Azure 中建立 hello VM，您必須安裝適用於 Linux 的 hello 加速網路驅動程式。</span><span class="sxs-lookup"><span data-stu-id="8319a-245">Once you create hello VM in Azure, you must install hello accelerated networking driver for Linux.</span></span> <span data-ttu-id="8319a-246">在完成之前 hello 下列步驟，您必須建立 Linux VM 使用任一 hello 加速網路[入口網站](#linux-portal)或[PowerShell](#linux-powershell)這篇文章中的步驟。</span><span class="sxs-lookup"><span data-stu-id="8319a-246">Before completing hello following steps, you must have created a Linux VM with accelerated networking using either hello [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="8319a-247">從網際網路瀏覽器中，開啟 hello Azure[入口網站](https://portal.azure.com)並以您的 Azure 登入[帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)。</span><span class="sxs-lookup"><span data-stu-id="8319a-247">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="8319a-248">如果您還沒有帳戶，則可以註冊[免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)帳戶。</span><span class="sxs-lookup"><span data-stu-id="8319a-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="8319a-249">頂端的 hello 入口網站中，toohello 右邊的 hello hello*搜尋資源*列上，按一下 hello **> _**圖示 toostart Bash 雲端殼層 （預覽）。</span><span class="sxs-lookup"><span data-stu-id="8319a-249">At hello top of hello portal, toohello right of hello *Search resources* bar, click hello **>_** icon toostart a Bash cloud shell (Preview).</span></span> <span data-ttu-id="8319a-250">hello Bash 雲端殼層窗格會顯示在 hello 下方 hello 入口網站並在幾秒鐘之後, 呈現 **username@Azure:~ $**提示字元。</span><span class="sxs-lookup"><span data-stu-id="8319a-250">hello Bash cloud shell pane appears at hello bottom of hello portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="8319a-251">雖然您可以從您的電腦，而不是 hello 雲端殼層 SSH toohello VM，在此教學課程中的 hello 指示會假設您使用 hello 雲端殼層。</span><span class="sxs-lookup"><span data-stu-id="8319a-251">Though you can SSH toohello VM from your computer, rather than hello cloud shell, hello instructions in this tutorial assume you're using hello cloud shell.</span></span>
3. <span data-ttu-id="8319a-252">在 hello hello 入口網站頂端，在 [hello] 方塊中，其中包含 hello 文字*搜尋資源*，型別*MyVm*。</span><span class="sxs-lookup"><span data-stu-id="8319a-252">At hello top of hello portal, in hello box that contains hello text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="8319a-253">當**MyVm**會出現在 hello 搜尋結果中，按一下它。</span><span class="sxs-lookup"><span data-stu-id="8319a-253">When **MyVm** appears in hello search results, click it.</span></span>
4. <span data-ttu-id="8319a-254">在 hello **MyVm**刀鋒視窗中，按一下 hello**連接**hello 的左上角 hello 刀鋒視窗中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="8319a-254">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="8319a-255">**注意：**如果**建立**hello 底下看見**連接**按鈕時，Azure 尚未完成建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="8319a-255">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="8319a-256">按一下**連接**只有您無法再查看之後**建立**下 hello**連接** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8319a-256">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
5. <span data-ttu-id="8319a-257">Azure 會開啟告訴您 tooenter hello 方塊`ssh adminuser@<ipaddress>`。</span><span class="sxs-lookup"><span data-stu-id="8319a-257">Azure opens a box telling you tooenter hello `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="8319a-258">輸入這個命令在 hello 雲端殼層 （或複製從 hello 方塊出現在步驟 4，並將它貼入 toohello 雲端殼層中），然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="8319a-258">Enter this command in hello cloud shell (or copy it from hello box that appeared in step 4 and paste it in toohello cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="8319a-259">Enter**是**toohello 問題詢問您是否 toocontinue 連接，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="8319a-259">Enter **yes** toohello question asking you if you want toocontinue connecting, then press Enter.</span></span>
7. <span data-ttu-id="8319a-260">輸入 hello 建立 hello VM 時，您所輸入的密碼。</span><span class="sxs-lookup"><span data-stu-id="8319a-260">Enter hello password you entered when creating hello VM.</span></span> <span data-ttu-id="8319a-261">一次成功登入 toohello VM，您會看到adminuser@MyVm:~ $ 提示字元。</span><span class="sxs-lookup"><span data-stu-id="8319a-261">Once successfully logged in toohello VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="8319a-262">您現在會記錄在 toohello VM 透過 hello 雲端殼層工作階段。</span><span class="sxs-lookup"><span data-stu-id="8319a-262">You are now logged in toohello VM through hello cloud shell session.</span></span> <span data-ttu-id="8319a-263">**注意︰**Cloud Shell 工作階段會在閒置 10 分鐘後逾時。</span><span class="sxs-lookup"><span data-stu-id="8319a-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="8319a-264">此時，hello 指示隨著您正在使用的 hello 發佈。</span><span class="sxs-lookup"><span data-stu-id="8319a-264">At this point, hello instructions vary based on hello distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="8319a-265">Ubuntu/SLES</span><span class="sxs-lookup"><span data-stu-id="8319a-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="8319a-266">Hello 提示字元之下，輸入`uname -r`並確認 hello 版本：</span><span class="sxs-lookup"><span data-stu-id="8319a-266">At hello prompt, enter `uname -r` and confirm hello version for:</span></span>

    * <span data-ttu-id="8319a-267">Ubuntu 是 "4.4.0-77-generic" 或更新版本</span><span class="sxs-lookup"><span data-stu-id="8319a-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="8319a-268">SLES 是 "4.4.59-92.20-default" 或更新版本</span><span class="sxs-lookup"><span data-stu-id="8319a-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="8319a-269">由執行 hello 命令，請遵循建立 hello 標準網路 vNIC 與 hello 加速網路 vNIC 之間連結。</span><span class="sxs-lookup"><span data-stu-id="8319a-269">Create a bond between hello standard networking vNIC and hello accelerated networking vNIC by running hello commands that follow.</span></span> <span data-ttu-id="8319a-270">網路流量會使用更高版本來執行 hello 證券可確保網路流量沒有被中斷的某些設定變更跨加速網路 vNIC，hello。</span><span class="sxs-lookup"><span data-stu-id="8319a-270">Network traffic uses hello higher performing accelerated networking vNIC, while hello bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="8319a-271">執行 hello 指令碼之後, hello VM 會重新啟動之後暫停 60 秒。</span><span class="sxs-lookup"><span data-stu-id="8319a-271">After running hello script, hello VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="8319a-272">一次重新啟動 VM，hello 重新連線 tooit 再次完成步驟 5-7。</span><span class="sxs-lookup"><span data-stu-id="8319a-272">Once hello VM is restarted, reconnect tooit by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="8319a-273">執行 hello`ifconfig`命令，並確認結果是 bond0 hello 介面顯示為向上。</span><span class="sxs-lookup"><span data-stu-id="8319a-273">Run hello `ifconfig` command and confirm that bond0 has come up and hello interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="8319a-274">使用加速網路功能的應用程式必須透過 hello 通訊*bond0*介面未*eth0*。</span><span class="sxs-lookup"><span data-stu-id="8319a-274">Applications using accelerated networking must communicate over hello *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="8319a-275">加速網路功能正式運作之前，可能會變更 hello 介面名稱。</span><span class="sxs-lookup"><span data-stu-id="8319a-275">hello interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="8319a-276">RHEL/CentOS</span><span class="sxs-lookup"><span data-stu-id="8319a-276">RHEL/CentOS</span></span>

<span data-ttu-id="8319a-277">建立 Red Hat Enterprise Linux 或 CentOS 7.3 VM 需要一些額外步驟 tooload hello 最新驅動程式所需的 SR-IOV 與 hello hello 網路卡的虛擬函式 (VF) 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="8319a-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps tooload hello latest drivers needed for SR-IOV and hello Virtual Function (VF) driver for hello network card.</span></span> <span data-ttu-id="8319a-278">hello 第一階段中的 hello 指示準備映像可能是使用的 toomake 擁有 hello 預先載入的驅動程式的一個或多個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8319a-278">hello first phase of hello instructions prepares an image that can be used toomake one or more virtual machines that have hello drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="8319a-279">第一個階段：準備 Red Hat Enterprise Linux 或 CentOS 7.3 基礎映像。</span><span class="sxs-lookup"><span data-stu-id="8319a-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="8319a-280">在 Azure 上佈建非 SRIOV CentOS 7.3 VM</span><span class="sxs-lookup"><span data-stu-id="8319a-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="8319a-281">安裝 LIS 4.2.2：</span><span class="sxs-lookup"><span data-stu-id="8319a-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="8319a-282">下載設定檔</span><span class="sxs-lookup"><span data-stu-id="8319a-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="8319a-283">取消佈建此 VM</span><span class="sxs-lookup"><span data-stu-id="8319a-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="8319a-284">從 Azure 入口網站停止此 VM。移 tooVM 的 「 磁碟 」，擷取 hello OSDisk VHD URI。</span><span class="sxs-lookup"><span data-stu-id="8319a-284">From Azure portal, stop this VM; and go tooVM’s "Disks", capture hello OSDisk’s VHD URI.</span></span> <span data-ttu-id="8319a-285">此 URI 包含 hello 基底映像的 VHD 名稱和其儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8319a-285">This URI contains hello base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="8319a-286">第二個階段：在 Azure 上佈建新的 VM</span><span class="sxs-lookup"><span data-stu-id="8319a-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="8319a-287">佈建與新增 AzureRMVMConfig 基礎的新 Vm 使用 hello 基底映像使用 AcceleratedNetworking hello vNIC 上啟用第一，階段中所擷取的 VHD:</span><span class="sxs-lookup"><span data-stu-id="8319a-287">Provision new VMs based with New-AzureRMVMConfig using hello base image VHD captured in phase one, with AcceleratedNetworking enabled on hello vNIC:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="8319a-288">Vm 開機後，檢查 「 lspci"hello VF 裝置，並檢查 hello Mellanox 項目。</span><span class="sxs-lookup"><span data-stu-id="8319a-288">After VMs boot up, check hello VF device by "lspci" and check hello Mellanox entry.</span></span> <span data-ttu-id="8319a-289">例如，我們應該會看到 hello lspci 輸出的這個項目：</span><span class="sxs-lookup"><span data-stu-id="8319a-289">For example, we should see this item in hello lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="8319a-290">執行 hello 聯結指令碼：</span><span class="sxs-lookup"><span data-stu-id="8319a-290">Run hello bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="8319a-291">重新啟動 hello 新的 Vm:</span><span class="sxs-lookup"><span data-stu-id="8319a-291">Reboot hello new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="8319a-292">hello VM 應該啟動 bond0 設定與 hello 啟用加速網路路徑。</span><span class="sxs-lookup"><span data-stu-id="8319a-292">hello VM should start with bond0 configured and hello Accelerated Networking path enabled.</span></span>  <span data-ttu-id="8319a-293">執行`ifconfig`tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="8319a-293">Run `ifconfig` tooconfirm.</span></span>
