---
title: "使用 Azure PowerShell 管理虛擬機器 | Microsoft Docs"
description: "了解可用來自動執行管理虛擬機器工作的命令。"
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
ms.openlocfilehash: fd2df7e1029ced11974d0b832258bed2cf3bbb27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="292dc-103">使用 Azure PowerShell 管理您的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="292dc-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="292dc-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="292dc-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="292dc-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="292dc-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="292dc-106">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="292dc-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="292dc-107">如需使用 Resource Manager 模型的常見 PowerShell 命令，請參閱[這裡](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="292dc-107">For common PowerShell commands using the Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="292dc-108">可以使用 Azure PowerShell Cmdlet 自動執行許多 VM 的日常管理工作。</span><span class="sxs-lookup"><span data-stu-id="292dc-108">Many tasks you do each day to manage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="292dc-109">這篇文章提供了幾個簡單工作的範例命令，另外也提供顯示用來完成更複雜的工作之命令的文章連結。</span><span class="sxs-lookup"><span data-stu-id="292dc-109">This article gives you example commands for simpler tasks, and links to articles that show the commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="292dc-110">如果您尚未安裝和設定 Azure PowerShell，可以在 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)文章中取得相關指示。</span><span class="sxs-lookup"><span data-stu-id="292dc-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in the article [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-to-use-the-example-commands"></a><span data-ttu-id="292dc-111">如何使用範例命令</span><span class="sxs-lookup"><span data-stu-id="292dc-111">How to use the example commands</span></span>
<span data-ttu-id="292dc-112">命令中的某些文字必須換成適合您環境的文字。</span><span class="sxs-lookup"><span data-stu-id="292dc-112">You'll need to replace some of the text in the commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="292dc-113">< 和 > 符號表示您需要取代的文字。</span><span class="sxs-lookup"><span data-stu-id="292dc-113">The < and > symbols indicate text you need to replace.</span></span> <span data-ttu-id="292dc-114">當您取代文字時，請移除符號，但將引號保留在原處。</span><span class="sxs-lookup"><span data-stu-id="292dc-114">When you replace the text, remove the symbols but leave the quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="292dc-115">取得 VM</span><span class="sxs-lookup"><span data-stu-id="292dc-115">Get a VM</span></span>
<span data-ttu-id="292dc-116">這是您會經常使用的基本工作。</span><span class="sxs-lookup"><span data-stu-id="292dc-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="292dc-117">使用它來取得 VM 的相關資訊、在 VM 上執行工作，或取得輸出以儲存至變數中。</span><span class="sxs-lookup"><span data-stu-id="292dc-117">Use it to get information about a VM, perform tasks on a VM, or get output to store in a variable.</span></span>

<span data-ttu-id="292dc-118">若要取得 VM 的相關資訊，請執行此命令，並取代引號中的所有內容 (包括 < 和 > 字元)：</span><span class="sxs-lookup"><span data-stu-id="292dc-118">To get information about the VM, run this command, replacing everything in the quotes, including the < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="292dc-119">若要儲存 $vm 變數中的輸出，請執行：</span><span class="sxs-lookup"><span data-stu-id="292dc-119">To store the output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-to-a-windows-based-vm"></a><span data-ttu-id="292dc-120">登入以 Windows 為基礎的 VM</span><span class="sxs-lookup"><span data-stu-id="292dc-120">Log on to a Windows-based VM</span></span>
<span data-ttu-id="292dc-121">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="292dc-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="292dc-122">您可以從 **Get-azurevm** 命令顯示的畫面中，取得虛擬機器和雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="292dc-122">You can get the virtual machine and cloud service name from the display of the **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="292dc-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<儲存已下載 RDP 檔案的磁碟機和資料夾位置，例如：c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span><span class="sxs-lookup"><span data-stu-id="292dc-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location to store the downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="292dc-124">停止 VM</span><span class="sxs-lookup"><span data-stu-id="292dc-124">Stop a VM</span></span>
<span data-ttu-id="292dc-125">請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="292dc-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="292dc-126">萬一它是雲端服務的最後一個 VM，您可以使用這個參數來保留雲端服務的虛擬 IP (VIP)。</span><span class="sxs-lookup"><span data-stu-id="292dc-126">Use this parameter to keep the virtual IP (VIP) of the cloud service in case it's the last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="292dc-127">如果使用 StayProvisioned 參數，還是需要支付 VM 的費用。</span><span class="sxs-lookup"><span data-stu-id="292dc-127">If you use the StayProvisioned parameter, you'll still be billed for the VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="292dc-128">啟動 VM</span><span class="sxs-lookup"><span data-stu-id="292dc-128">Start a VM</span></span>
<span data-ttu-id="292dc-129">請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="292dc-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="292dc-130">連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="292dc-130">Attach a data disk</span></span>
<span data-ttu-id="292dc-131">這項工作需要幾個步驟。</span><span class="sxs-lookup"><span data-stu-id="292dc-131">This task requires a few steps.</span></span> <span data-ttu-id="292dc-132">首先，請使用 ****Add-AzureDataDisk**** Cmdlet 將磁碟新增至 $vm 物件。</span><span class="sxs-lookup"><span data-stu-id="292dc-132">First, you use the ****Add-AzureDataDisk**** cmdlet to add the disk to the $vm object.</span></span> <span data-ttu-id="292dc-133">然後使用 **Update-AzureVM** Cmdlet 來更新 VM 的組態。</span><span class="sxs-lookup"><span data-stu-id="292dc-133">Then, you use **Update-AzureVM** cmdlet to update the configuration of the VM.</span></span>

<span data-ttu-id="292dc-134">您也需要決定是否要附加新的磁碟或附加已經包含資料的磁碟。</span><span class="sxs-lookup"><span data-stu-id="292dc-134">You'll also need to decide whether to attach a new disk or one that contains data.</span></span> <span data-ttu-id="292dc-135">如果是新的磁碟，此命令會建立 .vhd 檔案，並附加該檔案。</span><span class="sxs-lookup"><span data-stu-id="292dc-135">For a new disk, the command creates the .vhd file and attaches it.</span></span>

<span data-ttu-id="292dc-136">若要附加新的磁碟，請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="292dc-136">To attach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="292dc-137">若要附加現有的資料磁碟，請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="292dc-137">To attach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="292dc-138">若要從 Blob 儲存體中現有的 .vhd 檔案附加資料磁碟，請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="292dc-138">To attach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="292dc-139">建立以 Windows 為基礎的 VM</span><span class="sxs-lookup"><span data-stu-id="292dc-139">Create a Windows-based VM</span></span>
<span data-ttu-id="292dc-140">若要在 Azure 中建立以 Windows 為基礎的新虛擬機器，請依照[使用 Azure PowerShell 建立和預先設定建立以 Windows 為基礎的虛擬機器](create-powershell.md)中的指示執行。</span><span class="sxs-lookup"><span data-stu-id="292dc-140">To create a new Windows-based virtual machine in Azure, use the instructions in [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="292dc-141">本主題會逐步引導您建立 Azure PowerShell 命令集，以建立可預先設定的 Windows 型 VM：</span><span class="sxs-lookup"><span data-stu-id="292dc-141">This topic steps you through the creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="292dc-142">具有 Active Directory 網域成員資格。</span><span class="sxs-lookup"><span data-stu-id="292dc-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="292dc-143">具有額外的磁碟。</span><span class="sxs-lookup"><span data-stu-id="292dc-143">With additional disks.</span></span>
* <span data-ttu-id="292dc-144">成為現有負載平衡集的成員。</span><span class="sxs-lookup"><span data-stu-id="292dc-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="292dc-145">具有靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="292dc-145">With a static IP address.</span></span>

