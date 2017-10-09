---
title: "Azure VM 中的 HPC Pack 前端節點 aaaCreate |Microsoft 文件"
description: "了解如何 toouse hello Azure 入口網站與 hello 資源管理員部署的模型 toocreate Azure VM 中的 Microsoft HPC Pack 2012 R2 前端節點。"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: e6a13eaf-9124-47b4-8d75-2bc4672b8f21
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 3ddefb74b053a48a15f1ba1ca8edbc0192da51a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hello-head-node-of-an-hpc-pack-cluster-in-an-azure-vm-with-a-marketplace-image"></a><span data-ttu-id="f6751-103">建立 Azure VM 使用 Marketplace 映像中的 hello HPC Pack 叢集前端節點</span><span class="sxs-lookup"><span data-stu-id="f6751-103">Create hello head node of an HPC Pack cluster in an Azure VM with a Marketplace image</span></span>
<span data-ttu-id="f6751-104">使用[Microsoft HPC Pack 2012 R2 虛擬機器映像](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)從 hello Azure Marketplace 和 hello Azure 入口網站 toocreate hello 前端節點的 HPC 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6751-104">Use a [Microsoft HPC Pack 2012 R2 virtual machine image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) from hello Azure Marketplace and hello Azure portal toocreate hello head node of an HPC cluster.</span></span> <span data-ttu-id="f6751-105">此 HPC Pack VM 映像是基於已預先安裝 HPC Pack 2012 R2 Update 3 的 Windows Server 2012 R2 Datacenter。</span><span class="sxs-lookup"><span data-stu-id="f6751-105">This HPC Pack VM image is based on Windows Server 2012 R2 Datacenter with HPC Pack 2012 R2 Update 3 pre-installed.</span></span> <span data-ttu-id="f6751-106">使用此前端節點當作 Azure 中 HPC Pack 的概念證明部署。</span><span class="sxs-lookup"><span data-stu-id="f6751-106">Use this head node for a proof of concept deployment of HPC Pack in Azure.</span></span> <span data-ttu-id="f6751-107">您可以新增計算節點 toohello 叢集 toorun HPC 工作負載。</span><span class="sxs-lookup"><span data-stu-id="f6751-107">You can then add compute nodes toohello cluster toorun HPC workloads.</span></span>

> [!TIP]
> <span data-ttu-id="f6751-108">toodeploy 完整的 HPC Pack 2012 R2 叢集，包括 hello 前端節點和計算節點的 Azure 中，我們建議您最好使用自動化的方式。</span><span class="sxs-lookup"><span data-stu-id="f6751-108">toodeploy a complete HPC Pack 2012 R2 cluster in Azure that includes hello head node and compute nodes, we recommend that you use an automated method.</span></span> <span data-ttu-id="f6751-109">選項包括 hello [HPC Pack IaaS 部署指令碼](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)和資源管理員範本，例如 hello [Windows 工作負載的 HPC Pack 叢集](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)。</span><span class="sxs-lookup"><span data-stu-id="f6751-109">Options include hello [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and Resource Manager templates such as hello [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/).</span></span> <span data-ttu-id="f6751-110">此外，也有 [Microsoft HPC Pack 2016 叢集](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates)的 Resource Manager 範本可供使用。</span><span class="sxs-lookup"><span data-stu-id="f6751-110">Resource Manager templates are also available for [Microsoft HPC Pack 2016 clusters](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates).</span></span> 
> 
> 

## <a name="planning-considerations"></a><span data-ttu-id="f6751-111">規劃考量</span><span class="sxs-lookup"><span data-stu-id="f6751-111">Planning considerations</span></span>
<span data-ttu-id="f6751-112">Hello 遵循圖所示，您部署在 Azure 的虛擬網路中 Active Directory 網域中 hello HPC Pack 前端節點。</span><span class="sxs-lookup"><span data-stu-id="f6751-112">As shown in hello following figure, you deploy hello HPC Pack head node in an Active Directory domain in an Azure virtual network.</span></span>

![HPC Pack 前端節點][headnode]

* <span data-ttu-id="f6751-114">**Active Directory 網域**: hello 必須是前端節點的 HPC Pack 2012 R2 tooan Active Directory 網域，在 Azure 中的啟動之前加入您 hello HPC services hello VM 上。</span><span class="sxs-lookup"><span data-stu-id="f6751-114">**Active Directory domain**: hello HPC Pack 2012 R2 head node must be joined tooan Active Directory domain in Azure before you start hello HPC services on hello VM.</span></span> <span data-ttu-id="f6751-115">本文中，概念證明部署中所示，您可以升級 hello 您建立 hello 前端節點做為網域控制站才能啟動 hello HPC 服務的 VM。</span><span class="sxs-lookup"><span data-stu-id="f6751-115">As shown in this article, for a proof of concept deployment, you can promote hello VM you create for hello head node as a domain controller before starting hello HPC services.</span></span> <span data-ttu-id="f6751-116">另一個選項是 toodeploy 另一個網域控制站和樹系中您所加入的 Azure toowhich hello 前端節點 VM。</span><span class="sxs-lookup"><span data-stu-id="f6751-116">Another option is toodeploy a separate domain controller and forest in Azure toowhich you join hello head node VM.</span></span>

* <span data-ttu-id="f6751-117">**部署模型**： 對於大部分的新部署，Microsoft 建議您使用 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="f6751-117">**Deployment model**: For most new deployments, Microsoft recommends that you use hello Resource Manager deployment model.</span></span> <span data-ttu-id="f6751-118">本文假設您使用此部署模型。</span><span class="sxs-lookup"><span data-stu-id="f6751-118">This article assumes that you use this deployment model.</span></span>

* <span data-ttu-id="f6751-119">**Azure 虛擬網路**： 當您使用 hello 資源管理員部署模型 toodeploy hello 前端節點時，您指定或建立 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f6751-119">**Azure virtual network**: When you use hello Resource Manager deployment model toodeploy hello head node, you specify or create an Azure virtual network.</span></span> <span data-ttu-id="f6751-120">如果您需要 toojoin hello 前端節點 tooan 現有 Active Directory 網域，您可以使用 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f6751-120">You use hello virtual network if you need toojoin hello head node tooan existing Active Directory domain.</span></span> <span data-ttu-id="f6751-121">您也需要更新 tooadd 計算節點 Vm toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f6751-121">You also need it later tooadd compute node VMs toohello cluster.</span></span>

## <a name="steps-toocreate-hello-head-node"></a><span data-ttu-id="f6751-122">步驟 toocreate hello 前端節點</span><span class="sxs-lookup"><span data-stu-id="f6751-122">Steps toocreate hello head node</span></span>
<span data-ttu-id="f6751-123">以下是高層級步驟 toouse hello Azure 入口網站 toocreate Azure VM 的 hello HPC Pack 前端節點使用 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="f6751-123">Following are high-level steps toouse hello Azure portal toocreate an Azure VM for hello HPC Pack head node by using hello Resource Manager deployment model.</span></span> 

1. <span data-ttu-id="f6751-124">如果您想 toocreate 新 Active Directory 樹系在 Azure 中使用不同的網域控制站 Vm，其中一個選項是 toouse [Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc)。</span><span class="sxs-lookup"><span data-stu-id="f6751-124">If you want toocreate a new Active Directory forest in Azure with separate domain controller VMs, one option is toouse a [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc).</span></span> <span data-ttu-id="f6751-125">簡單概念證明部署，有好 tooomit 此步驟中，並將 hello 前端節點 VM 本身設定為網域控制站。</span><span class="sxs-lookup"><span data-stu-id="f6751-125">For a simple proof of concept deployment, it's fine tooomit this step and configure hello head node VM itself as a domain controller.</span></span> <span data-ttu-id="f6751-126">本文稍後將說明此選項。</span><span class="sxs-lookup"><span data-stu-id="f6751-126">This option is described later in this article.</span></span>
2. <span data-ttu-id="f6751-127">在 [hello [HPC Pack 2012 R2，在 Windows Server 2012 R2] 頁面上](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)hello Azure Marketplace，在按一下**建立虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="f6751-127">On hello [HPC Pack 2012 R2 on Windows Server 2012 R2 page](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) in hello Azure Marketplace, click **Create Virtual Machine**.</span></span> 
3. <span data-ttu-id="f6751-128">在 hello 入口網站上 hello **HPC Pack 2012 R2，Windows Server 2012 R2 上**頁面上，選取 hello**資源管理員**部署模型，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="f6751-128">In hello portal, on hello **HPC Pack 2012 R2 on Windows Server 2012 R2** page, select hello **Resource Manager** deployment model and then click **Create**.</span></span>
   
    ![HPC Pack 映像][marketplace]
4. <span data-ttu-id="f6751-130">使用 hello 入口 tooconfigure hello 設定並建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="f6751-130">Use hello portal tooconfigure hello settings and create hello VM.</span></span> <span data-ttu-id="f6751-131">如果您是新 tooAzure，請遵循 hello 教學課程[hello Azure 入口網站中建立 Windows 虛擬機器](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f6751-131">If you're new tooAzure, follow hello tutorial [Create a Windows virtual machine in hello Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="f6751-132">概念證明部署，您通常可以接受 hello 預設或建議的設定。</span><span class="sxs-lookup"><span data-stu-id="f6751-132">For a proof of concept deployment, you can usually accept hello default or recommended settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f6751-133">如果您想 toojoin hello 前端節點 tooan 現有的 azure Active Directory 網域，請確定您建立 hello VM 時指定 hello 該網域的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f6751-133">If you want toojoin hello head node tooan existing Active Directory domain in Azure, make sure you specify hello virtual network for that domain when creating hello VM.</span></span>
   > 
   > 
5. <span data-ttu-id="f6751-134">您建立 hello VM 和 hello VM 正在執行之後,[連接 toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)透過遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="f6751-134">After you create hello VM and hello VM is running, [connect toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) by Remote Desktop.</span></span> 
6. <span data-ttu-id="f6751-135">加入 hello VM tooan Active Directory 網域的樹系選擇其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="f6751-135">Join hello VM tooan Active Directory domain forest by choosing one of hello following options:</span></span>
   
   * <span data-ttu-id="f6751-136">如果您在 Azure 虛擬網路與現有的網域樹系中建立 hello VM，請使用標準伺服器管理員或 Windows PowerShell 工具將 hello VM toohello 樹系。</span><span class="sxs-lookup"><span data-stu-id="f6751-136">If you created hello VM in an Azure virtual network with an existing domain forest, join hello VM toohello forest by using standard Server Manager or Windows PowerShell tools.</span></span> <span data-ttu-id="f6751-137">然後重新啟動。</span><span class="sxs-lookup"><span data-stu-id="f6751-137">Then restart.</span></span>
   * <span data-ttu-id="f6751-138">如果您在新的虛擬網路 （不含現有的網域樹系） 中建立 hello VM，然後將 hello VM 升級為網域控制站。</span><span class="sxs-lookup"><span data-stu-id="f6751-138">If you created hello VM in a new virtual network (without an existing domain forest), then promote hello VM as a domain controller.</span></span> <span data-ttu-id="f6751-139">使用標準步驟 tooinstall 並 hello 前端節點上設定 hello Active Directory 網域服務角色。</span><span class="sxs-lookup"><span data-stu-id="f6751-139">Use standard steps tooinstall and configure hello Active Directory Domain Services role on hello head node.</span></span> <span data-ttu-id="f6751-140">如需詳細步驟，請參閱 [安裝新的 Windows Server 2012 Active Directory 樹系](https://technet.microsoft.com/library/jj574166.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f6751-140">For detailed steps, see [Install a New Windows Server 2012 Active Directory Forest](https://technet.microsoft.com/library/jj574166.aspx).</span></span>
7. <span data-ttu-id="f6751-141">之後 hello VM 正在執行，而且是聯結的 tooan Active Directory 樹系，請啟動 hello HPC Pack 服務，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f6751-141">After hello VM is running and is joined tooan Active Directory forest, start hello HPC Pack services as follows:</span></span>
   
    <span data-ttu-id="f6751-142">a.</span><span class="sxs-lookup"><span data-stu-id="f6751-142">a.</span></span> <span data-ttu-id="f6751-143">連接 toohello 前端節點 VM 使用 hello 本機 Administrators 群組成員的網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="f6751-143">Connect toohello head node VM using a domain account that is a member of hello local Administrators group.</span></span> <span data-ttu-id="f6751-144">例如，使用您建立 hello 前端節點 VM 時設定的 hello 系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="f6751-144">For example, use hello administrator account you set up when you created hello head node VM.</span></span>
   
    <span data-ttu-id="f6751-145">b.</span><span class="sxs-lookup"><span data-stu-id="f6751-145">b.</span></span> <span data-ttu-id="f6751-146">針對預設前端節點組態，系統管理員身分啟動 Windows PowerShell 並輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f6751-146">For a default head node configuration, start Windows PowerShell as an administrator and type hello following:</span></span>
   
    ```PowerShell
    & $env:CCP_HOME\bin\HPCHNPrepare.ps1 –DBServerInstance ".\ComputeCluster"
    ```
   
    <span data-ttu-id="f6751-147">可能需要幾分鐘的時間 hello HPC Pack services toostart。</span><span class="sxs-lookup"><span data-stu-id="f6751-147">It can take several minutes for hello HPC Pack services toostart.</span></span>
   
    <span data-ttu-id="f6751-148">如需其他前端節點組態選項，請輸入 `get-help HPCHNPrepare.ps1`。</span><span class="sxs-lookup"><span data-stu-id="f6751-148">For additional head node configuration options, type `get-help HPCHNPrepare.ps1`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6751-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6751-149">Next steps</span></span>
* <span data-ttu-id="f6751-150">您現在可以使用 hello HPC Pack 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="f6751-150">You can now work with hello head node of your HPC Pack cluster.</span></span> <span data-ttu-id="f6751-151">例如，啟動 HPC 叢集管理員，並完成 hello[部署待辦事項清單](https://technet.microsoft.com/library/jj884141.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f6751-151">For example, start HPC Cluster Manager, and complete hello [Deployment To-do List](https://technet.microsoft.com/library/jj884141.aspx).</span></span>
* <span data-ttu-id="f6751-152">如果您想 tooincrease hello 叢集計算容量隨，新增[Azure 高載節點](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)雲端服務中。</span><span class="sxs-lookup"><span data-stu-id="f6751-152">If you want tooincrease hello cluster compute capacity on-demand, add [Azure burst nodes](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) in a cloud service.</span></span> 
* <span data-ttu-id="f6751-153">請嘗試在 hello 叢集上執行測試工作負載。</span><span class="sxs-lookup"><span data-stu-id="f6751-153">Try running a test workload on hello cluster.</span></span> <span data-ttu-id="f6751-154">如需範例，請參閱 hello HPC Pack[入門指南](https://technet.microsoft.com/library/jj884144)。</span><span class="sxs-lookup"><span data-stu-id="f6751-154">For an example, see hello HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>

<!--Image references-->
[headnode]: ./media/hpcpack-cluster-headnode/headnode.png
[marketplace]: ./media/hpcpack-cluster-headnode/marketplace.png
