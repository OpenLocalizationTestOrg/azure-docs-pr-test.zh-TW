---
title: "使用 Powershell 建立並上傳 VM 映像 | Microsoft Docs"
description: "了解如何使用傳統部署模型和 Azure Powershell 來建立並上傳一般化 Windows Server 映像 (VHD)。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: bc75c8cdd98b0ea0fbff6483c0e3c9d4468d3941
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-upload-a-windows-server-vhd-to-azure"></a><span data-ttu-id="bcf04-103">建立並上傳 Windows Server VHD 到 Azure</span><span class="sxs-lookup"><span data-stu-id="bcf04-103">Create and upload a Windows Server VHD to Azure</span></span>
<span data-ttu-id="bcf04-104">本文說明如何上傳您自己的一般化 VM 映像做為虛擬硬碟 (VHD)，以便使用它來建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bcf04-104">This article shows you how to upload your own generalized VM image as a virtual hard disk (VHD) so you can use it to create virtual machines.</span></span> <span data-ttu-id="bcf04-105">如需 Microsoft Azure 中磁碟和 VHD 的詳細資訊，請參閱[關於虛擬機器的磁碟和 VHD](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="bcf04-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bcf04-106">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="bcf04-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bcf04-107">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="bcf04-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="bcf04-108">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="bcf04-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="bcf04-109">您也可以使用 Resource Manager 模型來[上傳](../upload-generalized-managed.md)虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bcf04-109">You can also [upload](../upload-generalized-managed.md) a virtual machine using the Resource Manager model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bcf04-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="bcf04-110">Prerequisites</span></span>
<span data-ttu-id="bcf04-111">本文假設您具有：</span><span class="sxs-lookup"><span data-stu-id="bcf04-111">This article assumes you have:</span></span>

* <span data-ttu-id="bcf04-112">**Azure 訂用帳戶** - 如果您沒有帳戶，您可以 [免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="bcf04-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="bcf04-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - 您已安裝 Microsoft Azure PowerShell 模組，並設定成使用您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bcf04-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - You have the Microsoft Azure PowerShell module installed and configured to use your subscription.</span></span>
* <span data-ttu-id="bcf04-114">**.VHD 檔案** - 儲存在 .vhd 檔案中並連接至虛擬機器的受支援 Windows 作業系統。</span><span class="sxs-lookup"><span data-stu-id="bcf04-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached to a virtual machine.</span></span> <span data-ttu-id="bcf04-115">檢查以查看 Sysprep 是否支援在 VHD 上執行的伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="bcf04-115">Check to see if the server roles running on the VHD are supported by Sysprep.</span></span> <span data-ttu-id="bcf04-116">如需詳細資訊，請參閱 [Sysprep Support for Server Roles (伺服器角色的 Sysprep 支援)](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)。</span><span class="sxs-lookup"><span data-stu-id="bcf04-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="bcf04-117">Microsoft Azure 不支援 VHDX 格式。</span><span class="sxs-lookup"><span data-stu-id="bcf04-117">The VHDX format is not supported in Microsoft Azure.</span></span> <span data-ttu-id="bcf04-118">您可以使用 Hyper-V 管理員或 [Convert-VHD Cmdlet](http://technet.microsoft.com/library/hh848454.aspx)，將磁碟轉換為 VHD 格式。</span><span class="sxs-lookup"><span data-stu-id="bcf04-118">You can convert the disk to VHD format using Hyper-V Manager or the [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="bcf04-119">如需詳細資料，請參閱 [部落格文章](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bcf04-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span></span>

## <a name="step-1-prep-the-vhd"></a><span data-ttu-id="bcf04-120">步驟 1：準備 VHD</span><span class="sxs-lookup"><span data-stu-id="bcf04-120">Step 1: Prep the VHD</span></span>
<span data-ttu-id="bcf04-121">將 VHD 上傳至 Azure 之前，必須使用 Sysprep 工具來一般化。</span><span class="sxs-lookup"><span data-stu-id="bcf04-121">Before you upload the VHD to Azure, it needs to be generalized by using the Sysprep tool.</span></span> <span data-ttu-id="bcf04-122">這要準備 VHD 以做為映像。</span><span class="sxs-lookup"><span data-stu-id="bcf04-122">This prepares the VHD to be used as an image.</span></span> <span data-ttu-id="bcf04-123">如需 Sysprep 的詳細資訊，請參閱 [如何使用 Sysprep：簡介](http://technet.microsoft.com/library/bb457073.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bcf04-123">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> <span data-ttu-id="bcf04-124">執行 Sysprep 前，請先備份 VM。</span><span class="sxs-lookup"><span data-stu-id="bcf04-124">Back up the VM before running Sysprep.</span></span>

<span data-ttu-id="bcf04-125">從安裝作業系統的虛擬機器，完成下列程序：</span><span class="sxs-lookup"><span data-stu-id="bcf04-125">From the virtual machine that the operating system was installed to, complete the following procedure:</span></span>

1. <span data-ttu-id="bcf04-126">登入作業系統。</span><span class="sxs-lookup"><span data-stu-id="bcf04-126">Sign in to the operating system.</span></span>
2. <span data-ttu-id="bcf04-127">以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="bcf04-127">Open a command prompt window as an administrator.</span></span> <span data-ttu-id="bcf04-128">切換至 **%windir%\system32\sysprep** 目錄，然後執行 `sysprep.exe`。</span><span class="sxs-lookup"><span data-stu-id="bcf04-128">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>

    ![開啟 [命令提示字元] 視窗](./media/createupload-vhd/sysprep_commandprompt.png)
3. <span data-ttu-id="bcf04-130">[系統準備工具]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="bcf04-130">The **System Preparation Tool** dialog box appears.</span></span>

   ![啟動 Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. <span data-ttu-id="bcf04-132">在 [系統準備工具] 中，選取 [進入系統全新體驗 (OOBE)]，並確認已勾選 [一般化]。</span><span class="sxs-lookup"><span data-stu-id="bcf04-132">In the **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span>
5. <span data-ttu-id="bcf04-133">在 [關機選項] 中選取 [關機]。</span><span class="sxs-lookup"><span data-stu-id="bcf04-133">In **Shutdown Options**, select **Shutdown**.</span></span>
6. <span data-ttu-id="bcf04-134">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="bcf04-134">Click **OK**.</span></span>

## <a name="step-2-create-a-storage-account-and-a-container"></a><span data-ttu-id="bcf04-135">步驟 2：建立儲存體帳戶和容器</span><span class="sxs-lookup"><span data-stu-id="bcf04-135">Step 2: Create a storage account and a container</span></span>
<span data-ttu-id="bcf04-136">您需要 Azure 中的儲存體帳戶，讓您有空間可上傳 .vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="bcf04-136">You need a storage account in Azure so you have a place to upload the .vhd file.</span></span> <span data-ttu-id="bcf04-137">此步驟說明如何建立帳戶，或從現有的帳戶取得您需要的資訊。</span><span class="sxs-lookup"><span data-stu-id="bcf04-137">This step shows you how to create an account, or get the info you need from an existing account.</span></span> <span data-ttu-id="bcf04-138">使用您自己的資訊來取代 &lsaquo; 括號 &rsaquo;中的變數。</span><span class="sxs-lookup"><span data-stu-id="bcf04-138">Replace the variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

1. <span data-ttu-id="bcf04-139">登入</span><span class="sxs-lookup"><span data-stu-id="bcf04-139">Login</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="bcf04-140">設定您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bcf04-140">Set your Azure subscription.</span></span>

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. <span data-ttu-id="bcf04-141">建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bcf04-141">Create a new storage account.</span></span> <span data-ttu-id="bcf04-142">儲存體帳戶的名稱應該是唯一的且包含 3-24 個字元。</span><span class="sxs-lookup"><span data-stu-id="bcf04-142">The name of the storage account should be unique, 3-24 characters.</span></span> <span data-ttu-id="bcf04-143">名稱可以是字母和數字的任意組合。</span><span class="sxs-lookup"><span data-stu-id="bcf04-143">The name can be any combination of letters and numbers.</span></span> <span data-ttu-id="bcf04-144">您也必須指定一個位置，例如「美國東部」。</span><span class="sxs-lookup"><span data-stu-id="bcf04-144">You also need to specify a location like "East US"</span></span>

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. <span data-ttu-id="bcf04-145">將新儲存體帳戶設定為預設值。</span><span class="sxs-lookup"><span data-stu-id="bcf04-145">Set the new storage account as the default.</span></span>

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. <span data-ttu-id="bcf04-146">建立新的容器。</span><span class="sxs-lookup"><span data-stu-id="bcf04-146">Create a new container.</span></span>

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-the-vhd-file"></a><span data-ttu-id="bcf04-147">步驟 3：上傳 .vhd 檔案</span><span class="sxs-lookup"><span data-stu-id="bcf04-147">Step 3: Upload the .vhd file</span></span>
<span data-ttu-id="bcf04-148">使用 [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) 來上傳 VHD。</span><span class="sxs-lookup"><span data-stu-id="bcf04-148">Use the [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) to upload the VHD.</span></span>

<span data-ttu-id="bcf04-149">從您在上一個步驟中使用的 Azure PowerShell 視窗中，輸入下列命令並以您自己的資訊取代 &lsaquo; 括號 &rsaquo; 中的變數。</span><span class="sxs-lookup"><span data-stu-id="bcf04-149">From the Azure PowerShell window you used in the previous step, type the following command and replace the variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-the-image-to-your-list-of-custom-images"></a><span data-ttu-id="bcf04-150">步驟 4：將映像新增到您的自訂映像清單</span><span class="sxs-lookup"><span data-stu-id="bcf04-150">Step 4: Add the image to your list of custom images</span></span>
<span data-ttu-id="bcf04-151">使用 [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) Cmdlet 將映像新增到您的自訂映像清單。</span><span class="sxs-lookup"><span data-stu-id="bcf04-151">Use the [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet to add the image to the list of your custom images.</span></span>

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a><span data-ttu-id="bcf04-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bcf04-152">Next steps</span></span>
<span data-ttu-id="bcf04-153">您現在可以使用上傳的映像來[建立自訂的 VM](createportal.md)。</span><span class="sxs-lookup"><span data-stu-id="bcf04-153">You can now [create a custom VM](createportal.md) using the image you uploaded.</span></span>
