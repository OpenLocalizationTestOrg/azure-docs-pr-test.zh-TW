---
title: "aaaCreate 和上傳 VM 映像使用 Powershell |Microsoft 文件"
description: "了解 toocreate 和上傳一般化的 Windows Server 映像 (VHD) 使用 hello 傳統部署模型和 Azure Powershell。"
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
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a><span data-ttu-id="ce261-103">建立及上傳 Windows Server VHD tooAzure</span><span class="sxs-lookup"><span data-stu-id="ce261-103">Create and upload a Windows Server VHD tooAzure</span></span>
<span data-ttu-id="ce261-104">本文章將示範如何 tooupload 一般化的 VM 映像做為虛擬硬碟 (VHD)，您可以使用它 toocreate 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ce261-104">This article shows you how tooupload your own generalized VM image as a virtual hard disk (VHD) so you can use it toocreate virtual machines.</span></span> <span data-ttu-id="ce261-105">如需 Microsoft Azure 中磁碟和 VHD 的詳細資訊，請參閱[關於虛擬機器的磁碟和 VHD](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ce261-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce261-106">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="ce261-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ce261-107">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="ce261-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ce261-108">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="ce261-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ce261-109">您也可以[上傳](../upload-generalized-managed.md)使用 hello 資源管理員模型在虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ce261-109">You can also [upload](../upload-generalized-managed.md) a virtual machine using hello Resource Manager model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce261-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ce261-110">Prerequisites</span></span>
<span data-ttu-id="ce261-111">本文假設您具有：</span><span class="sxs-lookup"><span data-stu-id="ce261-111">This article assumes you have:</span></span>

* <span data-ttu-id="ce261-112">**Azure 訂用帳戶** - 如果您沒有帳戶，您可以 [免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="ce261-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="ce261-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)**  -您已擁有 hello Microsoft Azure PowerShell 模組安裝並設定 toouse 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ce261-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - You have hello Microsoft Azure PowerShell module installed and configured toouse your subscription.</span></span>
* <span data-ttu-id="ce261-114">**A。VHD 檔案**-支援的 Windows 作業系統中的.vhd 檔案和附加的 tooa 虛擬機器儲存。</span><span class="sxs-lookup"><span data-stu-id="ce261-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached tooa virtual machine.</span></span> <span data-ttu-id="ce261-115">如果 hello 伺服器角色上執行 hello VHD 的核取 toosee 都支援 Sysprep。</span><span class="sxs-lookup"><span data-stu-id="ce261-115">Check toosee if hello server roles running on hello VHD are supported by Sysprep.</span></span> <span data-ttu-id="ce261-116">如需詳細資訊，請參閱 [Sysprep Support for Server Roles (伺服器角色的 Sysprep 支援)](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)。</span><span class="sxs-lookup"><span data-stu-id="ce261-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ce261-117">在 Microsoft Azure 中不支援 hello VHDX 格式。</span><span class="sxs-lookup"><span data-stu-id="ce261-117">hello VHDX format is not supported in Microsoft Azure.</span></span> <span data-ttu-id="ce261-118">您可以將轉換 hello 磁碟 tooVHD 格式使用 HYPER-V 管理員] 或 [hello [CONVERT-VHD 指令程式](http://technet.microsoft.com/library/hh848454.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ce261-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="ce261-119">如需詳細資料，請參閱 [部落格文章](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ce261-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span></span>

## <a name="step-1-prep-hello-vhd"></a><span data-ttu-id="ce261-120">步驟 1： 準備 hello VHD</span><span class="sxs-lookup"><span data-stu-id="ce261-120">Step 1: Prep hello VHD</span></span>
<span data-ttu-id="ce261-121">您上傳 hello VHD tooAzure 之前，它會需要 toobe 使用 hello Sysprep 工具一般化。</span><span class="sxs-lookup"><span data-stu-id="ce261-121">Before you upload hello VHD tooAzure, it needs toobe generalized by using hello Sysprep tool.</span></span> <span data-ttu-id="ce261-122">這可讓準備 hello VHD toobe 做為映像。</span><span class="sxs-lookup"><span data-stu-id="ce261-122">This prepares hello VHD toobe used as an image.</span></span> <span data-ttu-id="ce261-123">如需 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介](http://technet.microsoft.com/library/bb457073.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ce261-123">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> <span data-ttu-id="ce261-124">執行 Sysprep 之前先備份 hello VM。</span><span class="sxs-lookup"><span data-stu-id="ce261-124">Back up hello VM before running Sysprep.</span></span>

<span data-ttu-id="ce261-125">從 hello hello 作業系統的虛擬機器已安裝，請以完成下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce261-125">From hello virtual machine that hello operating system was installed to, complete hello following procedure:</span></span>

1. <span data-ttu-id="ce261-126">登入 toohello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="ce261-126">Sign in toohello operating system.</span></span>
2. <span data-ttu-id="ce261-127">以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="ce261-127">Open a command prompt window as an administrator.</span></span> <span data-ttu-id="ce261-128">變更 hello 目錄太**%windir%\system32\sysprep**，然後執行`sysprep.exe`。</span><span class="sxs-lookup"><span data-stu-id="ce261-128">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>

    ![開啟 [命令提示字元] 視窗](./media/createupload-vhd/sysprep_commandprompt.png)
3. <span data-ttu-id="ce261-130">hello**系統準備工具** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="ce261-130">hello **System Preparation Tool** dialog box appears.</span></span>

   ![啟動 Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. <span data-ttu-id="ce261-132">在 hello**系統準備工具**，選取**輸入系統全新體驗 (OOBE)**並確定**一般化**已核取。</span><span class="sxs-lookup"><span data-stu-id="ce261-132">In hello **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span>
5. <span data-ttu-id="ce261-133">在 [關機選項] 中選取 [關機]。</span><span class="sxs-lookup"><span data-stu-id="ce261-133">In **Shutdown Options**, select **Shutdown**.</span></span>
6. <span data-ttu-id="ce261-134">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ce261-134">Click **OK**.</span></span>

## <a name="step-2-create-a-storage-account-and-a-container"></a><span data-ttu-id="ce261-135">步驟 2：建立儲存體帳戶和容器</span><span class="sxs-lookup"><span data-stu-id="ce261-135">Step 2: Create a storage account and a container</span></span>
<span data-ttu-id="ce261-136">您需要在 Azure 中的儲存體帳戶，因此您需要的地方 tooupload hello.vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="ce261-136">You need a storage account in Azure so you have a place tooupload hello .vhd file.</span></span> <span data-ttu-id="ce261-137">此步驟說明如何 toocreate 帳戶或 get hello 資訊您需要從現有的帳戶。</span><span class="sxs-lookup"><span data-stu-id="ce261-137">This step shows you how toocreate an account, or get hello info you need from an existing account.</span></span> <span data-ttu-id="ce261-138">取代中的 hello 變數&lsaquo;方括號&rsaquo;具有您個人資訊。</span><span class="sxs-lookup"><span data-stu-id="ce261-138">Replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

1. <span data-ttu-id="ce261-139">登入</span><span class="sxs-lookup"><span data-stu-id="ce261-139">Login</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="ce261-140">設定您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ce261-140">Set your Azure subscription.</span></span>

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. <span data-ttu-id="ce261-141">建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ce261-141">Create a new storage account.</span></span> <span data-ttu-id="ce261-142">hello hello 儲存體帳戶名稱是唯一的 3-24 個字元。</span><span class="sxs-lookup"><span data-stu-id="ce261-142">hello name of hello storage account should be unique, 3-24 characters.</span></span> <span data-ttu-id="ce261-143">hello 名稱可以是字母和數字的任意組合。</span><span class="sxs-lookup"><span data-stu-id="ce261-143">hello name can be any combination of letters and numbers.</span></span> <span data-ttu-id="ce261-144">您也需要 toospecify 位置，例如"East US"</span><span class="sxs-lookup"><span data-stu-id="ce261-144">You also need toospecify a location like "East US"</span></span>

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. <span data-ttu-id="ce261-145">設定 hello 新儲存體帳戶做為 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="ce261-145">Set hello new storage account as hello default.</span></span>

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. <span data-ttu-id="ce261-146">建立新的容器。</span><span class="sxs-lookup"><span data-stu-id="ce261-146">Create a new container.</span></span>

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a><span data-ttu-id="ce261-147">步驟 3: Hello.vhd 檔案上傳</span><span class="sxs-lookup"><span data-stu-id="ce261-147">Step 3: Upload hello .vhd file</span></span>
<span data-ttu-id="ce261-148">使用 hello [Add-azurevhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello VHD。</span><span class="sxs-lookup"><span data-stu-id="ce261-148">Use hello [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello VHD.</span></span>

<span data-ttu-id="ce261-149">從 hello 先前步驟中的 hello Azure PowerShell 視窗，輸入 hello 下列命令，並取代中的 hello 變數&lsaquo;方括號&rsaquo;具有您個人資訊。</span><span class="sxs-lookup"><span data-stu-id="ce261-149">From hello Azure PowerShell window you used in hello previous step, type hello following command and replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a><span data-ttu-id="ce261-150">步驟 4： 加入 hello 影像 tooyour 清單的自訂映像</span><span class="sxs-lookup"><span data-stu-id="ce261-150">Step 4: Add hello image tooyour list of custom images</span></span>
<span data-ttu-id="ce261-151">使用 hello [Add-azurevmimage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello 影像 toohello 清單的自訂映像。</span><span class="sxs-lookup"><span data-stu-id="ce261-151">Use hello [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello image toohello list of your custom images.</span></span>

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a><span data-ttu-id="ce261-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ce261-152">Next steps</span></span>
<span data-ttu-id="ce261-153">您現在可以[建立自訂 VM](createportal.md)使用 hello 映像上傳。</span><span class="sxs-lookup"><span data-stu-id="ce261-153">You can now [create a custom VM](createportal.md) using hello image you uploaded.</span></span>
