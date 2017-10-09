---
title: "aaaManage 您的虛擬機器使用 Azure PowerShell |Microsoft 文件"
description: "了解您可以使用中管理虛擬機器的 tooautomate 工作的命令。"
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="fe0d6-103">使用 Azure PowerShell 管理您的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="fe0d6-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="fe0d6-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fe0d6-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="fe0d6-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="fe0d6-107">使用 hello 資源管理員模型的一般 PowerShell 命令，請參閱[這裡](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-107">For common PowerShell commands using hello Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="fe0d6-108">可以使用 Azure PowerShell cmdlet 來自動化執行每日 toomanage Vm 的許多工作。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-108">Many tasks you do each day toomanage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="fe0d6-109">這篇文章提供您命令範例更簡單的工作和連結 tooarticles 顯示 hello 指令更複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-109">This article gives you example commands for simpler tasks, and links tooarticles that show hello commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="fe0d6-110">如果您並未安裝及設定 Azure PowerShell，您可以在 hello 文件中取得指示[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-toouse-hello-example-commands"></a><span data-ttu-id="fe0d6-111">如何 toouse hello 範例命令</span><span class="sxs-lookup"><span data-stu-id="fe0d6-111">How toouse hello example commands</span></span>
<span data-ttu-id="fe0d6-112">您將需要的 tooreplace hello 中的 hello 文字的某些命令搭配適用於您環境的文字。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-112">You'll need tooreplace some of hello text in hello commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="fe0d6-113">hello < 和 > 符號表示您需要 tooreplace 的文字。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-113">hello < and > symbols indicate text you need tooreplace.</span></span> <span data-ttu-id="fe0d6-114">當您取代 hello 文字時，移除 hello 符號，但讓 hello 引號留在原處。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-114">When you replace hello text, remove hello symbols but leave hello quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="fe0d6-115">取得 VM</span><span class="sxs-lookup"><span data-stu-id="fe0d6-115">Get a VM</span></span>
<span data-ttu-id="fe0d6-116">這是您會經常使用的基本工作。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="fe0d6-117">使用 VM 的 tooget 資訊、 在 VM 上執行工作或取得輸出 toostore 在變數中。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-117">Use it tooget information about a VM, perform tasks on a VM, or get output toostore in a variable.</span></span>

<span data-ttu-id="fe0d6-118">tooget 資訊 hello VM，執行下列命令，取代 hello 加上引號，包括 hello < 和 > 字元的所有項目：</span><span class="sxs-lookup"><span data-stu-id="fe0d6-118">tooget information about hello VM, run this command, replacing everything in hello quotes, including hello < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="fe0d6-119">toostore hello 輸出在 $vm 變數中，執行：</span><span class="sxs-lookup"><span data-stu-id="fe0d6-119">toostore hello output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a><span data-ttu-id="fe0d6-120">登入 tooa Windows 架構的 VM</span><span class="sxs-lookup"><span data-stu-id="fe0d6-120">Log on tooa Windows-based VM</span></span>
<span data-ttu-id="fe0d6-121">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="fe0d6-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="fe0d6-122">您可以從 hello 顯示 hello 取得 hello 虛擬機器和雲端服務名稱**Get-azurevm**命令。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-122">You can get hello virtual machine and cloud service name from hello display of hello **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="fe0d6-123">$svcName ="<cloud service name>"$vmName ="<virtual machine name>"$localPath ="< 磁碟機和資料夾位置 toostore hello 下載 RDP 檔案，範例： c:\temp >"$localFile = $localPath +"\" + $vmname +".rdp 」 Get-azureremotedesktopfile-ServiceName $svcName-命名 $vmName LocalPath $localFile-啟動</span><span class="sxs-lookup"><span data-stu-id="fe0d6-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location toostore hello downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="fe0d6-124">停止 VM</span><span class="sxs-lookup"><span data-stu-id="fe0d6-124">Stop a VM</span></span>
<span data-ttu-id="fe0d6-125">請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="fe0d6-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="fe0d6-126">使用虛擬 IP (VIP) 的 hello 雲端服務，以便在此參數 tookeep hello hello 該雲端服務中的最後一個 VM。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-126">Use this parameter tookeep hello virtual IP (VIP) of hello cloud service in case it's hello last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="fe0d6-127">如果您使用 hello StayProvisioned 參數時，您將仍然要支付 hello VM。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-127">If you use hello StayProvisioned parameter, you'll still be billed for hello VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="fe0d6-128">啟動 VM</span><span class="sxs-lookup"><span data-stu-id="fe0d6-128">Start a VM</span></span>
<span data-ttu-id="fe0d6-129">請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="fe0d6-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="fe0d6-130">連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="fe0d6-130">Attach a data disk</span></span>
<span data-ttu-id="fe0d6-131">這項工作需要幾個步驟。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-131">This task requires a few steps.</span></span> <span data-ttu-id="fe0d6-132">首先，您可以使用 hello * * * 新增-AzureDataDisk * * * cmdlet tooadd hello 磁碟 toohello $vm 物件。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-132">First, you use hello ****Add-AzureDataDisk**** cmdlet tooadd hello disk toohello $vm object.</span></span> <span data-ttu-id="fe0d6-133">然後，您使用**Update-azurevm** hello VM cmdlet tooupdate hello 設定。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-133">Then, you use **Update-AzureVM** cmdlet tooupdate hello configuration of hello VM.</span></span>

<span data-ttu-id="fe0d6-134">您還需要 toodecide 是否 tooattach 新磁碟或其中所包含的資料。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-134">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="fe0d6-135">為新的磁碟，hello 命令會建立 hello.vhd 檔案，並將它附加。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-135">For a new disk, hello command creates hello .vhd file and attaches it.</span></span>

<span data-ttu-id="fe0d6-136">tooattach 新磁碟時，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="fe0d6-136">tooattach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="fe0d6-137">tooattach 現有的資料磁碟，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="fe0d6-137">tooattach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="fe0d6-138">從現有的.vhd 檔案在 blob 儲存體，tooattach 資料磁碟會執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="fe0d6-138">tooattach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="fe0d6-139">建立以 Windows 為基礎的 VM</span><span class="sxs-lookup"><span data-stu-id="fe0d6-139">Create a Windows-based VM</span></span>
<span data-ttu-id="fe0d6-140">新視窗為基礎的虛擬機器在 Azure 中，使用中的 hello 指示 toocreate[使用 Azure PowerShell toocreate 並預先設定 Windows 型虛擬機器](create-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-140">toocreate a new Windows-based virtual machine in Azure, use hello instructions in [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="fe0d6-141">此主題會逐步引導您透過 hello 建立的 Azure PowerShell 命令設定，會建立可以預先設定的 windows VM:</span><span class="sxs-lookup"><span data-stu-id="fe0d6-141">This topic steps you through hello creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="fe0d6-142">具有 Active Directory 網域成員資格。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="fe0d6-143">具有額外的磁碟。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-143">With additional disks.</span></span>
* <span data-ttu-id="fe0d6-144">成為現有負載平衡集的成員。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="fe0d6-145">具有靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fe0d6-145">With a static IP address.</span></span>

