---
title: "aaaCreating hello Azure Marketplace 的內部部署虛擬機器映像 |Microsoft 文件"
description: "了解並執行 hello 步驟 toocreate 在內部部署 VM 映像及部署 toohello Azure Marketplace 的其他人 toopurchase。"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="3dd15-103">開發 hello Azure Marketplace 的內部部署虛擬機器映像</span><span class="sxs-lookup"><span data-stu-id="3dd15-103">Develop an on-premises virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="3dd15-104">我們強烈建議直接在 hello 雲端開發 Azure 的虛擬硬碟 (Vhd)，使用遠端桌面通訊協定。</span><span class="sxs-lookup"><span data-stu-id="3dd15-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in hello cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="3dd15-105">不過，如果您必須是可能 toodownload 的 VHD，開發可以使用內部部署基礎結構。</span><span class="sxs-lookup"><span data-stu-id="3dd15-105">However, if you must, it is possible toodownload a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="3dd15-106">在內部部署開發，您必須下載 hello 作業系統 VHD 的 hello 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="3dd15-106">For on-premises development, you must download hello operating system VHD of hello created VM.</span></span> <span data-ttu-id="3dd15-107">這些步驟會在前述的步驟 3.3 進行。</span><span class="sxs-lookup"><span data-stu-id="3dd15-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="3dd15-108">下載 VHD 映像</span><span class="sxs-lookup"><span data-stu-id="3dd15-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="3dd15-109">找出 Blob URL</span><span class="sxs-lookup"><span data-stu-id="3dd15-109">Locate a blob URL</span></span>
<span data-ttu-id="3dd15-110">在訂單 toodownload hello VHD，您必須先找出 hello 作業系統磁碟的 hello blob URL。</span><span class="sxs-lookup"><span data-stu-id="3dd15-110">In order toodownload hello VHD, first locate hello blob URL for hello operating system disk.</span></span>

<span data-ttu-id="3dd15-111">找出 hello blob URL 從 hello 新[Microsoft Azure 入口網站](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="3dd15-111">Locate hello blob URL from hello new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="3dd15-112">跳過**瀏覽** > **Vm**，，然後選取 hello 部署 VM。</span><span class="sxs-lookup"><span data-stu-id="3dd15-112">Go too**Browse** > **VMs**, and then select hello deployed VM.</span></span>
2. <span data-ttu-id="3dd15-113">在下**設定**，選取 hello**磁碟**磚，以開啟 hello 磁碟刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3dd15-113">Under **Configure**, select hello **Disks** tile, which opens hello Disks blade.</span></span>
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="3dd15-115">選取 hello **OS 磁碟**，如此即會開啟另一個的刀鋒視窗，其中會顯示磁碟內容，包括 hello VHD 的位置。</span><span class="sxs-lookup"><span data-stu-id="3dd15-115">Select hello **OS Disk**, which opens another blade that displays disk properties, including hello VHD location.</span></span>
4. <span data-ttu-id="3dd15-116">複製此 Blob URL。</span><span class="sxs-lookup"><span data-stu-id="3dd15-116">Copy this blob URL.</span></span>
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="3dd15-118">現在，請刪除 hello 而不刪除 hello 備份磁碟部署 VM。</span><span class="sxs-lookup"><span data-stu-id="3dd15-118">Now, delete hello deployed VM without deleting hello backing disks.</span></span> <span data-ttu-id="3dd15-119">您也可以停止 hello VM 而不是刪除它。</span><span class="sxs-lookup"><span data-stu-id="3dd15-119">You can also stop hello VM instead of deleting it.</span></span> <span data-ttu-id="3dd15-120">Hello VM 正在執行時，請不要下載 hello 作業系統 VHD。</span><span class="sxs-lookup"><span data-stu-id="3dd15-120">Do not download hello operating system VHD when hello VM is running.</span></span>
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="3dd15-122">下載 VHD</span><span class="sxs-lookup"><span data-stu-id="3dd15-122">Download a VHD</span></span>
<span data-ttu-id="3dd15-123">您知道 hello blob URL 之後，您可以使用 hello 下載 hello VHD [Azure 入口網站](http://manage.windowsazure.com/)或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="3dd15-123">After you know hello blob URL, you can download hello VHD by using hello [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="3dd15-124">本指南建立 hello 時，hello 功能 toodownload VHD 尚未存在於 hello 新 Microsoft Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="3dd15-124">At hello time of this guide’s creation, hello functionality toodownload a VHD is not yet present in hello new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="3dd15-125">**下載 hello 作業系統 VHD hello 目前透過[Azure 入口網站](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="3dd15-125">**Download hello operating system VHD via hello current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="3dd15-126">如果您有尚未完成，再登入 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="3dd15-126">Sign in toohello Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="3dd15-127">按一下 hello**儲存體** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3dd15-127">Click hello **Storage** tab.</span></span>
3. <span data-ttu-id="3dd15-128">選取哪些 hello 內儲存 VHD 的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3dd15-128">Select hello storage account within which hello VHD is stored.</span></span>
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="3dd15-130">這樣即會顯示儲存體帳戶屬性</span><span class="sxs-lookup"><span data-stu-id="3dd15-130">This displays storage account properties.</span></span> <span data-ttu-id="3dd15-131">選取 hello**容器** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3dd15-131">Select hello **Containers** tab.</span></span>
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="3dd15-133">選取儲存 VHD 中的 hello hello 容器。</span><span class="sxs-lookup"><span data-stu-id="3dd15-133">Select hello container in which hello VHD is stored.</span></span> <span data-ttu-id="3dd15-134">根據預設，當從 hello 入口網站中，建立 hello VHD 儲存在 vhd 容器。</span><span class="sxs-lookup"><span data-stu-id="3dd15-134">By default, when created from hello portal, hello VHD is stored in a vhds container.</span></span>
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="3dd15-136">藉由比較您儲存一個 hello URL toohello 選取 hello 正確的作業系統 VHD。</span><span class="sxs-lookup"><span data-stu-id="3dd15-136">Select hello correct operating system VHD by comparing hello URL toohello one you saved.</span></span>
7. <span data-ttu-id="3dd15-137">按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="3dd15-137">Click **Download**.</span></span>
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="3dd15-139">使用 PowerShell 下載 VHD</span><span class="sxs-lookup"><span data-stu-id="3dd15-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="3dd15-140">此外 toousing hello Azure 入口網站，您可以使用 hello [Save-azurevhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello 作業系統 VHD。</span><span class="sxs-lookup"><span data-stu-id="3dd15-140">In addition toousing hello Azure portal, you can use hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="3dd15-141">例如，Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span><span class="sxs-lookup"><span data-stu-id="3dd15-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="3dd15-142">**Save-azurevhd**還有**NumberOfThreads**選項可用於 hello 下載 tooincrease 平行處理原則 toomake hello 充分利用可用的頻寬。</span><span class="sxs-lookup"><span data-stu-id="3dd15-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used tooincrease parallelism toomake hello best use of available bandwidth for hello download.</span></span>
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a><span data-ttu-id="3dd15-143">上傳 Vhd tooan Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="3dd15-143">Upload VHDs tooan Azure storage account</span></span>
<span data-ttu-id="3dd15-144">如果您準備的 Vhd 在內部，您會需要的 tooupload 到儲存體帳戶在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="3dd15-144">If you prepared your VHDs on-premises, you need tooupload them into a storage account in Azure.</span></span> <span data-ttu-id="3dd15-145">這個步驟會在建立內部部署的 VHD 之後，但在取得 VM 映像認證之前進行。</span><span class="sxs-lookup"><span data-stu-id="3dd15-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="3dd15-146">建立儲存體帳戶和容器</span><span class="sxs-lookup"><span data-stu-id="3dd15-146">Create a storage account and container</span></span>
<span data-ttu-id="3dd15-147">我們建議您到 hello 美國地區的儲存體帳戶上傳 Vhd。</span><span class="sxs-lookup"><span data-stu-id="3dd15-147">We recommend that VHDs be uploaded into a storage account in a region in hello United States.</span></span> <span data-ttu-id="3dd15-148">單一 SKU 的所有 VHD 都應該放在單一儲存體帳戶內的單一容器中。</span><span class="sxs-lookup"><span data-stu-id="3dd15-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="3dd15-149">toocreate 儲存體帳戶，您可以使用 hello [Microsoft Azure 入口網站](https://portal.azure.com/)、 PowerShell 或 hello Linux 命令列工具。</span><span class="sxs-lookup"><span data-stu-id="3dd15-149">toocreate a storage account, you can use hello [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or hello Linux command-line tool.</span></span>  

<span data-ttu-id="3dd15-150">**從 hello Microsoft Azure 入口網站建立儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="3dd15-150">**Create a storage account from hello Microsoft Azure portal**</span></span>

1. <span data-ttu-id="3dd15-151">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="3dd15-151">Click **New**.</span></span>
2. <span data-ttu-id="3dd15-152">選取 [儲存體] 。</span><span class="sxs-lookup"><span data-stu-id="3dd15-152">Select **Storage**.</span></span>
3. <span data-ttu-id="3dd15-153">填寫 hello 儲存體帳戶名稱，然後選取 位置。</span><span class="sxs-lookup"><span data-stu-id="3dd15-153">Fill in hello storage account name, and then select a location.</span></span>
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="3dd15-155">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3dd15-155">Click **Create**.</span></span>
5. <span data-ttu-id="3dd15-156">建立儲存體帳戶的 hello 的 hello 刀鋒視窗應開啟。</span><span class="sxs-lookup"><span data-stu-id="3dd15-156">hello blade for hello created storage account should be open.</span></span> <span data-ttu-id="3dd15-157">如果沒有，請選取 [瀏覽] > [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="3dd15-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="3dd15-158">在 hello 儲存體帳戶] 刀鋒視窗中，選取 [建立 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3dd15-158">On hello Storage account blade, select hello storage account created.</span></span>
6. <span data-ttu-id="3dd15-159">選取 [容器] 。</span><span class="sxs-lookup"><span data-stu-id="3dd15-159">Select **Containers**.</span></span>
   
   ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="3dd15-161">在 hello 容器刀鋒視窗中，選取 **新增**，然後輸入容器名稱和 hello 容器權限。</span><span class="sxs-lookup"><span data-stu-id="3dd15-161">On hello Containers blade, select **Add**, and then enter a container name and hello container permissions.</span></span> <span data-ttu-id="3dd15-162">為容器權限選取 [私人]  。</span><span class="sxs-lookup"><span data-stu-id="3dd15-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="3dd15-163">我們建議您建立一個容器，每個您計劃 toopublish SKU。</span><span class="sxs-lookup"><span data-stu-id="3dd15-163">We recommend that you create one container per SKU that you are planning toopublish.</span></span>
> 
> 

  ![繪圖](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="3dd15-165">使用 PowerShell 建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="3dd15-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="3dd15-166">使用 PowerShell，建立儲存體帳戶使用 hello[新增 AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3dd15-166">Using PowerShell, create a storage account by using hello [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="3dd15-167">然後您可以建立該儲存體帳戶內的容器使用 hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3dd15-167">Then you can create a container within that storage account by using hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="3dd15-168">這些命令假設在 PowerShell 中的 hello 目前儲存體帳戶內容已設定。</span><span class="sxs-lookup"><span data-stu-id="3dd15-168">Those commands assume that hello current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="3dd15-169">請參閱太[設定 Azure PowerShell](marketplace-publishing-powershell-setup.md)如需有關 PowerShell 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="3dd15-169">Refer too[Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="3dd15-170">使用適用於 Mac 和 Linux hello 命令列工具來建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="3dd15-170">Create a storage account by using hello command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="3dd15-171">從 [Linux 命令列工具](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)建立儲存體帳戶，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3dd15-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="3dd15-172">如下所示建立容器。</span><span class="sxs-lookup"><span data-stu-id="3dd15-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="3dd15-173">上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="3dd15-173">Upload a VHD</span></span>
<span data-ttu-id="3dd15-174">Hello 儲存體帳戶和容器建立後，您可以上傳您準備的 Vhd。</span><span class="sxs-lookup"><span data-stu-id="3dd15-174">After hello storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="3dd15-175">您可以使用 PowerShell、 hello Linux 命令列工具或其他 Azure 儲存體管理工具。</span><span class="sxs-lookup"><span data-stu-id="3dd15-175">You can use PowerShell, hello Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="3dd15-176">透過 PowerShell 上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="3dd15-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="3dd15-177">使用 hello [Add-azurevhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3dd15-177">Use hello [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="3dd15-178">使用適用於 Mac 和 Linux hello 命令列工具來上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="3dd15-178">Upload a VHD by using hello command-line tool for Mac and Linux</span></span>
<span data-ttu-id="3dd15-179">以 hello [Linux 命令列工具](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)，使用下列 hello: azure vm 映像建立<image name>-位置<Location of hello data center>-OS Linux<LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="3dd15-179">With hello [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use hello following: azure vm image create <image name> --location <Location of hello data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="3dd15-180">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3dd15-180">See also</span></span>
* [<span data-ttu-id="3dd15-181">建立虛擬機器映像的 hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="3dd15-181">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="3dd15-182">設定 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3dd15-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

