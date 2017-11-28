---
title: "在 Azure VM 中建立 HPC Pack 前端節點 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站和 Resource Manager 部署模型，在 Azure VM 中建立 Microsoft HPC Pack 2012 R2 前端節點。"
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
ms.openlocfilehash: b2bb9caf82a580dc5f67ea0b0b1c2e9a46363e9c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-the-head-node-of-an-hpc-pack-cluster-in-an-azure-vm-with-a-marketplace-image"></a><span data-ttu-id="80438-103">使用 Marketplace 映像在 Azure VM 中建立 HPC Pack 叢集的前端節點</span><span class="sxs-lookup"><span data-stu-id="80438-103">Create the head node of an HPC Pack cluster in an Azure VM with a Marketplace image</span></span>
<span data-ttu-id="80438-104">您可以使用來自 Azure Marketplace 的 [Microsoft HPC Pack 2012 R2 虛擬機器映像](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) 和 Azure 入口網站，來建立 HPC 叢集的前端節點。</span><span class="sxs-lookup"><span data-stu-id="80438-104">Use a [Microsoft HPC Pack 2012 R2 virtual machine image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) from the Azure Marketplace and the Azure portal to create the head node of an HPC cluster.</span></span> <span data-ttu-id="80438-105">此 HPC Pack VM 映像是基於已預先安裝 HPC Pack 2012 R2 Update 3 的 Windows Server 2012 R2 Datacenter。</span><span class="sxs-lookup"><span data-stu-id="80438-105">This HPC Pack VM image is based on Windows Server 2012 R2 Datacenter with HPC Pack 2012 R2 Update 3 pre-installed.</span></span> <span data-ttu-id="80438-106">使用此前端節點當作 Azure 中 HPC Pack 的概念證明部署。</span><span class="sxs-lookup"><span data-stu-id="80438-106">Use this head node for a proof of concept deployment of HPC Pack in Azure.</span></span> <span data-ttu-id="80438-107">然後您可以將計算節點加入叢集以執行 HPC 工作負載。</span><span class="sxs-lookup"><span data-stu-id="80438-107">You can then add compute nodes to the cluster to run HPC workloads.</span></span>

> [!TIP]
> <span data-ttu-id="80438-108">若要在 Azure 中部署包含前端節點和計算節點的完整 HPC Pack 2012 R2 叢集，建議您使用自動化方法。</span><span class="sxs-lookup"><span data-stu-id="80438-108">To deploy a complete HPC Pack 2012 R2 cluster in Azure that includes the head node and compute nodes, we recommend that you use an automated method.</span></span> <span data-ttu-id="80438-109">選項包括 [HPC Pack IaaS 部署指令碼](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)和 Resource Manager 範本，例如[適用於 Windows 工作負載的 HPC Pack 叢集](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)。</span><span class="sxs-lookup"><span data-stu-id="80438-109">Options include the [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and Resource Manager templates such as the [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/).</span></span> <span data-ttu-id="80438-110">此外，也有 [Microsoft HPC Pack 2016 叢集](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates)的 Resource Manager 範本可供使用。</span><span class="sxs-lookup"><span data-stu-id="80438-110">Resource Manager templates are also available for [Microsoft HPC Pack 2016 clusters](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates).</span></span> 
> 
> 

## <a name="planning-considerations"></a><span data-ttu-id="80438-111">規劃考量</span><span class="sxs-lookup"><span data-stu-id="80438-111">Planning considerations</span></span>
<span data-ttu-id="80438-112">如下圖所示，您會將 HPC Pack 前端節點部署在 Azure 虛擬網路的 Active Directory 網域中。</span><span class="sxs-lookup"><span data-stu-id="80438-112">As shown in the following figure, you deploy the HPC Pack head node in an Active Directory domain in an Azure virtual network.</span></span>

![HPC Pack 前端節點][headnode]

* <span data-ttu-id="80438-114">**Active Directory 網域**：在您啟動 VM 上的 HPC 服務之前，HPC Pack 2012 R2 前端節點必須先加入 Azure 中的 Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="80438-114">**Active Directory domain**: The HPC Pack 2012 R2 head node must be joined to an Active Directory domain in Azure before you start the HPC services on the VM.</span></span> <span data-ttu-id="80438-115">如本文中所示，針對概念證明部署，您可以在啟動 HPC 服務之前，將您為前端節點建立的 VM 升級為網域控制站。</span><span class="sxs-lookup"><span data-stu-id="80438-115">As shown in this article, for a proof of concept deployment, you can promote the VM you create for the head node as a domain controller before starting the HPC services.</span></span> <span data-ttu-id="80438-116">另一個選項則是在 Azure 中部署您要將前端節點 VM 加入其中的個別網域控制站和樹系。</span><span class="sxs-lookup"><span data-stu-id="80438-116">Another option is to deploy a separate domain controller and forest in Azure to which you join the head node VM.</span></span>

* <span data-ttu-id="80438-117">**部署模型**：針對大多數新的部署，Microsoft 建議您使用 Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="80438-117">**Deployment model**: For most new deployments, Microsoft recommends that you use the Resource Manager deployment model.</span></span> <span data-ttu-id="80438-118">本文假設您使用此部署模型。</span><span class="sxs-lookup"><span data-stu-id="80438-118">This article assumes that you use this deployment model.</span></span>

* <span data-ttu-id="80438-119">**Azure 虛擬網路**：當您使用 Resource Manager 部署模型來部署前端節點時，您需指定或建立 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="80438-119">**Azure virtual network**: When you use the Resource Manager deployment model to deploy the head node, you specify or create an Azure virtual network.</span></span> <span data-ttu-id="80438-120">如果您需要將前端節點加入現有的 Active Directory 網域中，您就會用到虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="80438-120">You use the virtual network if you need to join the head node to an existing Active Directory domain.</span></span> <span data-ttu-id="80438-121">您稍後也需要使用它來將計算節點 VM 新增到叢集中。</span><span class="sxs-lookup"><span data-stu-id="80438-121">You also need it later to add compute node VMs to the cluster.</span></span>

## <a name="steps-to-create-the-head-node"></a><span data-ttu-id="80438-122">建立前端節點的步驟</span><span class="sxs-lookup"><span data-stu-id="80438-122">Steps to create the head node</span></span>
<span data-ttu-id="80438-123">以下是使用 Azure 入口網站，利用 Resource Manager 部署模型為 HPC Pack 前端節點建立 Azure VM 的概略步驟。</span><span class="sxs-lookup"><span data-stu-id="80438-123">Following are high-level steps to use the Azure portal to create an Azure VM for the HPC Pack head node by using the Resource Manager deployment model.</span></span> 

1. <span data-ttu-id="80438-124">如果您想要以個別的網域控制站 VM 在 Azure 中建立新的 Active Directory 樹系，其中一個選項是使用 [Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc)。</span><span class="sxs-lookup"><span data-stu-id="80438-124">If you want to create a new Active Directory forest in Azure with separate domain controller VMs, one option is to use a [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc).</span></span> <span data-ttu-id="80438-125">若要進行簡單的概念驗證部署，則可以略過此步驟，而將前端節點 VM 本身設定為網域控制站。</span><span class="sxs-lookup"><span data-stu-id="80438-125">For a simple proof of concept deployment, it's fine to omit this step and configure the head node VM itself as a domain controller.</span></span> <span data-ttu-id="80438-126">本文稍後將說明此選項。</span><span class="sxs-lookup"><span data-stu-id="80438-126">This option is described later in this article.</span></span>
2. <span data-ttu-id="80438-127">在 Azure Marketplace 的 [HPC Pack 2012 R2 on Windows Server 2012 R2 (Windows Server 2012 R2 上的 HPC Pack 2012 R2) 頁面](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)上，按一下 [建立虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="80438-127">On the [HPC Pack 2012 R2 on Windows Server 2012 R2 page](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) in the Azure Marketplace, click **Create Virtual Machine**.</span></span> 
3. <span data-ttu-id="80438-128">在入口網站中，於 **HPC Pack 2012 R2 on Windows Server 2012 R2 (Windows Server 2012 R2 上的 HPC Pack 2012 R2)** 頁面上，選取 [Resource Manager] 部署模型，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="80438-128">In the portal, on the **HPC Pack 2012 R2 on Windows Server 2012 R2** page, select the **Resource Manager** deployment model and then click **Create**.</span></span>
   
    ![HPC Pack 映像][marketplace]
4. <span data-ttu-id="80438-130">使用入口網站設定並建立該 VM。</span><span class="sxs-lookup"><span data-stu-id="80438-130">Use the portal to configure the settings and create the VM.</span></span> <span data-ttu-id="80438-131">如果您不熟悉 Azure，請依照 [在 Azure 入口網站中建立 Windows 虛擬機器](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)教學課程操作。</span><span class="sxs-lookup"><span data-stu-id="80438-131">If you're new to Azure, follow the tutorial [Create a Windows virtual machine in the Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="80438-132">若要進行概念驗證部署，您通常可以接受預設或建議的設定。</span><span class="sxs-lookup"><span data-stu-id="80438-132">For a proof of concept deployment, you can usually accept the default or recommended settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="80438-133">如果您想要將前端節點加入 Azure 現有的 Active Directory 網域中，請務必在建立 VM 時，指定該網域的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="80438-133">If you want to join the head node to an existing Active Directory domain in Azure, make sure you specify the virtual network for that domain when creating the VM.</span></span>
   > 
   > 
5. <span data-ttu-id="80438-134">建立 VM 且 VM 開始執行之後，請透過「遠端桌面」 [連接到 VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="80438-134">After you create the VM and the VM is running, [connect to the VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) by Remote Desktop.</span></span> 
6. <span data-ttu-id="80438-135">選擇下列其中一個選項以將 VM 加入 Active Directory 網域樹系：</span><span class="sxs-lookup"><span data-stu-id="80438-135">Join the VM to an Active Directory domain forest by choosing one of the following options:</span></span>
   
   * <span data-ttu-id="80438-136">如果您是在具有現有網域樹系的 Azure 虛擬網路中建立了 VM，請使用標準的「伺服器管理員」或 Windows PowerShell 工具將該 VM 加入網域樹系中。</span><span class="sxs-lookup"><span data-stu-id="80438-136">If you created the VM in an Azure virtual network with an existing domain forest, join the VM to the forest by using standard Server Manager or Windows PowerShell tools.</span></span> <span data-ttu-id="80438-137">然後重新啟動。</span><span class="sxs-lookup"><span data-stu-id="80438-137">Then restart.</span></span>
   * <span data-ttu-id="80438-138">如果您是在無現有網域樹系的新虛擬網路中建立了 VM，則請將該 VM 升級為網域控制站。</span><span class="sxs-lookup"><span data-stu-id="80438-138">If you created the VM in a new virtual network (without an existing domain forest), then promote the VM as a domain controller.</span></span> <span data-ttu-id="80438-139">請使用標準步驟在前端節點上安裝並設定「Active Directory 網域服務」角色。</span><span class="sxs-lookup"><span data-stu-id="80438-139">Use standard steps to install and configure the Active Directory Domain Services role on the head node.</span></span> <span data-ttu-id="80438-140">如需詳細步驟，請參閱 [安裝新的 Windows Server 2012 Active Directory 樹系](https://technet.microsoft.com/library/jj574166.aspx)。</span><span class="sxs-lookup"><span data-stu-id="80438-140">For detailed steps, see [Install a New Windows Server 2012 Active Directory Forest](https://technet.microsoft.com/library/jj574166.aspx).</span></span>
7. <span data-ttu-id="80438-141">在 VM 已開始執行並加入 Active Directory 樹系之後，請依下列方式啟動 HPC Pack 服務：</span><span class="sxs-lookup"><span data-stu-id="80438-141">After the VM is running and is joined to an Active Directory forest, start the HPC Pack services as follows:</span></span>
   
    <span data-ttu-id="80438-142">a.</span><span class="sxs-lookup"><span data-stu-id="80438-142">a.</span></span> <span data-ttu-id="80438-143">使用具備本機 Administrators 群組成員身分的網域帳戶來連接到前端節點 VM。</span><span class="sxs-lookup"><span data-stu-id="80438-143">Connect to the head node VM using a domain account that is a member of the local Administrators group.</span></span> <span data-ttu-id="80438-144">例如，使用建立前端節點 VM 時所設定的系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="80438-144">For example, use the administrator account you set up when you created the head node VM.</span></span>
   
    <span data-ttu-id="80438-145">b.</span><span class="sxs-lookup"><span data-stu-id="80438-145">b.</span></span> <span data-ttu-id="80438-146">針對預設前端節點組態，請以系統管理員身分啟動 Windows PowerShell，並輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="80438-146">For a default head node configuration, start Windows PowerShell as an administrator and type the following:</span></span>
   
    ```PowerShell
    & $env:CCP_HOME\bin\HPCHNPrepare.ps1 –DBServerInstance ".\ComputeCluster"
    ```
   
    <span data-ttu-id="80438-147">可能需要幾分鐘的時間，HPC Pack 服務才能啟動。</span><span class="sxs-lookup"><span data-stu-id="80438-147">It can take several minutes for the HPC Pack services to start.</span></span>
   
    <span data-ttu-id="80438-148">如需其他前端節點組態選項，請輸入 `get-help HPCHNPrepare.ps1`。</span><span class="sxs-lookup"><span data-stu-id="80438-148">For additional head node configuration options, type `get-help HPCHNPrepare.ps1`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80438-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="80438-149">Next steps</span></span>
* <span data-ttu-id="80438-150">您現在已可以使用 HPC Pack 叢集的前端節點。</span><span class="sxs-lookup"><span data-stu-id="80438-150">You can now work with the head node of your HPC Pack cluster.</span></span> <span data-ttu-id="80438-151">例如，啟動「HPC 叢集管理員」並完成 [部署待辦事項清單](https://technet.microsoft.com/library/jj884141.aspx)。</span><span class="sxs-lookup"><span data-stu-id="80438-151">For example, start HPC Cluster Manager, and complete the [Deployment To-do List](https://technet.microsoft.com/library/jj884141.aspx).</span></span>
* <span data-ttu-id="80438-152">如果您想要視需要增加叢集計算能力，請在雲端服務中新增 [Azure 高載節點](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="80438-152">If you want to increase the cluster compute capacity on-demand, add [Azure burst nodes](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) in a cloud service.</span></span> 
* <span data-ttu-id="80438-153">嘗試在叢集上執行測試工作負載。</span><span class="sxs-lookup"><span data-stu-id="80438-153">Try running a test workload on the cluster.</span></span> <span data-ttu-id="80438-154">如需範例，請參閱 HPC Pack [快速入門指南](https://technet.microsoft.com/library/jj884144)。</span><span class="sxs-lookup"><span data-stu-id="80438-154">For an example, see the HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>

<!--Image references-->
[headnode]: ./media/hpcpack-cluster-headnode/headnode.png
[marketplace]: ./media/hpcpack-cluster-headnode/marketplace.png
