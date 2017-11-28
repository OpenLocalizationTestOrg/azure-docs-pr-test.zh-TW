---
title: "aaaHow toocreate 管理或刪除儲存體帳戶中 hello Azure 入口網站 |Microsoft 文件"
description: "建立新的儲存體帳戶、 管理您的帳戶存取金鑰，或刪除 hello Azure 入口網站的儲存體帳戶。 了解標準和進階儲存體帳戶。"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 87c37da0-6cc6-4d88-a330-ef2896a1531d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
f1_keywords: sql13.swb.windowsazurestorage.connect.f1
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 3a2a07c4131fbe594c7007f59950bf94339809fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a><span data-ttu-id="b83dc-104">關於 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b83dc-104">About Azure storage accounts</span></span>
[!INCLUDE [storage-selector-portal-create-storage-account](../../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-table-cosmos-db-tip-include](../../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="b83dc-105">概觀</span><span class="sxs-lookup"><span data-stu-id="b83dc-105">Overview</span></span>
<span data-ttu-id="b83dc-106">Azure 儲存體帳戶提供唯一的命名空間 toostore，並存取您的 Azure 儲存體資料物件。</span><span class="sxs-lookup"><span data-stu-id="b83dc-106">An Azure storage account provides a unique namespace toostore and access your Azure Storage data objects.</span></span> <span data-ttu-id="b83dc-107">儲存體帳戶中的所有物件會做為群組共同計費。</span><span class="sxs-lookup"><span data-stu-id="b83dc-107">All objects in a storage account are billed together as a group.</span></span> <span data-ttu-id="b83dc-108">根據預設，您的帳戶中的 hello 資料會是可用的唯一 tooyou，hello 帳戶擁有者。</span><span class="sxs-lookup"><span data-stu-id="b83dc-108">By default, hello data in your account is available only tooyou, hello account owner.</span></span>

[!INCLUDE [storage-account-types-include](../../../includes/storage-account-types-include.md)]

## <a name="storage-account-billing"></a><span data-ttu-id="b83dc-109">儲存體帳戶計費</span><span class="sxs-lookup"><span data-stu-id="b83dc-109">Storage account billing</span></span>
[!INCLUDE [storage-account-billing-include](../../../includes/storage-account-billing-include.md)]

> [!NOTE]
> <span data-ttu-id="b83dc-110">當您建立 Azure 虛擬機器時，儲存體帳戶會為您自動建立 hello 部署位置中如果您不在該位置中已經有儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b83dc-110">When you create an Azure virtual machine, a storage account is created for you automatically in hello deployment location if you do not already have a storage account in that location.</span></span> <span data-ttu-id="b83dc-111">如此就不需要 toofollow hello 步驟 toocreate 虛擬機器磁碟的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b83dc-111">So it's not necessary toofollow hello steps below toocreate a storage account for your virtual machine disks.</span></span> <span data-ttu-id="b83dc-112">hello 儲存體帳戶名稱將會根據 hello 虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="b83dc-112">hello storage account name will be based on hello virtual machine name.</span></span> <span data-ttu-id="b83dc-113">請參閱 hello [Azure 虛擬機器文件](https://azure.microsoft.com/documentation/services/virtual-machines/)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b83dc-113">See hello [Azure Virtual Machines documentation](https://azure.microsoft.com/documentation/services/virtual-machines/) for more details.</span></span>
> 
> 

## <a name="storage-account-endpoints"></a><span data-ttu-id="b83dc-114">儲存體帳戶端點</span><span class="sxs-lookup"><span data-stu-id="b83dc-114">Storage account endpoints</span></span>
<span data-ttu-id="b83dc-115">每個儲存在 Azure 儲存體中的物件都有一個唯一 URL 位址。</span><span class="sxs-lookup"><span data-stu-id="b83dc-115">Every object that you store in Azure Storage has a unique URL address.</span></span> <span data-ttu-id="b83dc-116">hello 儲存體帳戶名稱 form hello 該位址的子網域。</span><span class="sxs-lookup"><span data-stu-id="b83dc-116">hello storage account name forms hello subdomain of that address.</span></span> <span data-ttu-id="b83dc-117">hello 組合子網域和網域名稱，這是特定 tooeach 服務，形成*端點*儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b83dc-117">hello combination of subdomain and domain name, which is specific tooeach service, forms an *endpoint* for your storage account.</span></span>

<span data-ttu-id="b83dc-118">例如，如果您的儲存體帳戶命名為*mystorageaccount*，則 hello 預設端點，您的儲存體帳戶必須：</span><span class="sxs-lookup"><span data-stu-id="b83dc-118">For example, if your storage account is named *mystorageaccount*, then hello default endpoints for your storage account are:</span></span>

* <span data-ttu-id="b83dc-119">Blob 服務：http://*mystorageaccount*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="b83dc-119">Blob service: http://*mystorageaccount*.blob.core.windows.net</span></span>
* <span data-ttu-id="b83dc-120">表格服務：http://*mystorageaccount*.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="b83dc-120">Table service: http://*mystorageaccount*.table.core.windows.net</span></span>
* <span data-ttu-id="b83dc-121">佇列服務：http://*mystorageaccount*.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="b83dc-121">Queue service: http://*mystorageaccount*.queue.core.windows.net</span></span>
* <span data-ttu-id="b83dc-122">檔案服務：http://*mystorageaccount.file.core.windows.net*.file.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="b83dc-122">File service: http://*mystorageaccount*.file.core.windows.net</span></span>

> [!NOTE]
> <span data-ttu-id="b83dc-123">Blob 儲存體帳戶只會顯示 hello Blob 服務端點。</span><span class="sxs-lookup"><span data-stu-id="b83dc-123">A Blob storage account only exposes hello Blob service endpoint.</span></span>
> 
> 

<span data-ttu-id="b83dc-124">藉由附加 hello 儲存體帳戶 toohello 端點中的 hello 物件的位置建立 hello URL 來存取儲存體帳戶中的物件。</span><span class="sxs-lookup"><span data-stu-id="b83dc-124">hello URL for accessing an object in a storage account is built by appending hello object's location in hello storage account toohello endpoint.</span></span> <span data-ttu-id="b83dc-125">例如，blob 位址可能會有如下格式︰http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*。</span><span class="sxs-lookup"><span data-stu-id="b83dc-125">For example, a blob address might have this format: http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*.</span></span>

<span data-ttu-id="b83dc-126">您也可以設定自訂網域名稱 toouse 與儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b83dc-126">You can also configure a custom domain name toouse with your storage account.</span></span> <span data-ttu-id="b83dc-127">如需詳細資訊，請參閱[針對 Blob 儲存體端點設定自訂網域名稱](../blobs/storage-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="b83dc-127">For more information, see [Configure a custom domain Name for your Blob Storage Endpoint](../blobs/storage-custom-domain-name.md).</span></span> <span data-ttu-id="b83dc-128">您也可以使用 PowerShell 加以設定。</span><span class="sxs-lookup"><span data-stu-id="b83dc-128">You can also configure it with PowerShell.</span></span> <span data-ttu-id="b83dc-129">如需詳細資訊，請參閱 hello[組 AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b83dc-129">For more information, see hello [Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) cmdlet.</span></span>  


## <a name="create-a-storage-account"></a><span data-ttu-id="b83dc-130">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b83dc-130">Create a storage account</span></span>
1. <span data-ttu-id="b83dc-131">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b83dc-131">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b83dc-132">在 hello 中樞功能表中，選取 **新增** -> **儲存體** -> **儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="b83dc-132">On hello Hub menu, select **New** -> **Storage** -> **Storage account**.</span></span>
3. <span data-ttu-id="b83dc-133">輸入儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="b83dc-133">Enter a name for your storage account.</span></span> <span data-ttu-id="b83dc-134">請參閱[儲存體帳戶端點](#storage-account-endpoints)如需詳細資訊關於如何 hello 儲存體帳戶名稱將會使用的 tooaddress 您 Azure 儲存體中的物件。</span><span class="sxs-lookup"><span data-stu-id="b83dc-134">See [Storage account endpoints](#storage-account-endpoints) for details about how hello storage account name will be used tooaddress your objects in Azure Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b83dc-135">儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能包含數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="b83dc-135">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>
   > 
   > <span data-ttu-id="b83dc-136">儲存體帳戶名稱必須在 Azure 中是獨一無二的。</span><span class="sxs-lookup"><span data-stu-id="b83dc-136">Your storage account name must be unique within Azure.</span></span> <span data-ttu-id="b83dc-137">hello Azure 入口網站會指出是否 hello 您選取的儲存體帳戶名稱已在使用中。</span><span class="sxs-lookup"><span data-stu-id="b83dc-137">hello Azure portal will indicate if hello storage account name you select is already in use.</span></span>
   > 
   > 
4. <span data-ttu-id="b83dc-138">指定使用 hello 部署模型 toobe:**資源管理員**或**傳統**。</span><span class="sxs-lookup"><span data-stu-id="b83dc-138">Specify hello deployment model toobe used: **Resource Manager** or **Classic**.</span></span> <span data-ttu-id="b83dc-139">**資源管理員**hello 建議部署模型。</span><span class="sxs-lookup"><span data-stu-id="b83dc-139">**Resource Manager** is hello recommended deployment model.</span></span> <span data-ttu-id="b83dc-140">如需詳細資訊，請參閱 [了解資源管理員部署和傳統部署](../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="b83dc-140">For more information, see [Understanding Resource Manager deployment and classic deployment](../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b83dc-141">Blob 儲存體帳戶只能建立使用 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="b83dc-141">Blob storage accounts can only be created using hello Resource Manager deployment model.</span></span>

5. <span data-ttu-id="b83dc-142">選取的儲存體帳戶的 hello 類型：**一般用途**或**Blob 儲存體**。</span><span class="sxs-lookup"><span data-stu-id="b83dc-142">Select hello type of storage account: **General purpose** or **Blob storage**.</span></span> <span data-ttu-id="b83dc-143">**一般用途**hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="b83dc-143">**General purpose** is hello default.</span></span>
   
    <span data-ttu-id="b83dc-144">如果**一般用途**已選取，然後指定 hello 效能層：**標準**或**Premium**。</span><span class="sxs-lookup"><span data-stu-id="b83dc-144">If **General purpose** was selected, then specify hello performance tier: **Standard** or **Premium**.</span></span> <span data-ttu-id="b83dc-145">hello 預設值是**標準**。</span><span class="sxs-lookup"><span data-stu-id="b83dc-145">hello default is **Standard**.</span></span> <span data-ttu-id="b83dc-146">如需標準和進階儲存體帳戶的詳細資訊，請參閱[簡介 tooMicrosoft Azure 儲存體](storage-introduction.md)和[高階儲存體： Azure 虛擬機器工作負載的高效能儲存體](storage-premium-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="b83dc-146">For more details on standard and premium storage accounts, see [Introduction tooMicrosoft Azure Storage](storage-introduction.md) and [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span>
   
    <span data-ttu-id="b83dc-147">如果**Blob 儲存體**已選取，然後指定 hello 存取層：**作用**或**Cool**。</span><span class="sxs-lookup"><span data-stu-id="b83dc-147">If **Blob Storage** was selected, then specify hello access tier: **Hot** or **Cool**.</span></span> <span data-ttu-id="b83dc-148">hello 預設值是**作用**。</span><span class="sxs-lookup"><span data-stu-id="b83dc-148">hello default is **Hot**.</span></span> <span data-ttu-id="b83dc-149">如需詳細資訊，請參閱 [Azure Blob 儲存體：經常存取及不常存取層](../blobs/storage-blob-storage-tiers.md) 。</span><span class="sxs-lookup"><span data-stu-id="b83dc-149">See [Azure Blob Storage: Cool and Hot tiers](../blobs/storage-blob-storage-tiers.md) for more details.</span></span>
6. <span data-ttu-id="b83dc-150">選取 hello hello 儲存體帳戶的複寫選項： **LRS**， **GRS**， **RA-GRS**，或**ZRS**。</span><span class="sxs-lookup"><span data-stu-id="b83dc-150">Select hello replication option for hello storage account: **LRS**, **GRS**, **RA-GRS**, or **ZRS**.</span></span> <span data-ttu-id="b83dc-151">hello 預設值是**RA-GRS**。</span><span class="sxs-lookup"><span data-stu-id="b83dc-151">hello default is **RA-GRS**.</span></span> <span data-ttu-id="b83dc-152">如需 Azure 儲存體複寫選項的詳細資訊，請參閱 [Azure 儲存體複寫](storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="b83dc-152">For more details on Azure Storage replication options, see [Azure Storage replication](storage-redundancy.md).</span></span>
7. <span data-ttu-id="b83dc-153">選取您想在其中 toocreate hello 新儲存體帳戶的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b83dc-153">Select hello subscription in which you want toocreate hello new storage account.</span></span>
8. <span data-ttu-id="b83dc-154">指定新的資源群組，或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b83dc-154">Specify a new resource group or select an existing resource group.</span></span> <span data-ttu-id="b83dc-155">如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b83dc-155">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>
9. <span data-ttu-id="b83dc-156">選取儲存體帳戶的 hello 地理位置。</span><span class="sxs-lookup"><span data-stu-id="b83dc-156">Select hello geographic location for your storage account.</span></span> <span data-ttu-id="b83dc-157">如需各區域可用服務的詳細資訊，請參閱 [Azure 區域](https://azure.microsoft.com/regions/#services) 。</span><span class="sxs-lookup"><span data-stu-id="b83dc-157">See [Azure Regions](https://azure.microsoft.com/regions/#services) for more information about what services are available in which region.</span></span>
10. <span data-ttu-id="b83dc-158">按一下**建立**toocreate hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b83dc-158">Click **Create** toocreate hello storage account.</span></span>

## <a name="manage-your-storage-account"></a><span data-ttu-id="b83dc-159">管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b83dc-159">Manage your storage account</span></span>
### <a name="change-your-account-configuration"></a><span data-ttu-id="b83dc-160">變更帳戶組態</span><span class="sxs-lookup"><span data-stu-id="b83dc-160">Change your account configuration</span></span>
<span data-ttu-id="b83dc-161">建立儲存體帳戶之後，您可以修改其組態，例如變更 hello hello 帳戶或變更 hello 存取層的 Blob 儲存體帳戶時所使用的複寫選項。</span><span class="sxs-lookup"><span data-stu-id="b83dc-161">After you create your storage account, you can modify its configuration, such as changing hello replication option used for hello account or changing hello access tier for a Blob storage account.</span></span> <span data-ttu-id="b83dc-162">在 hello [Azure 入口網站](https://portal.azure.com)，tooyour 儲存體帳戶中，尋找並按一下瀏覽**組態**下**設定**tooview 和/或變更 hello 帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="b83dc-162">In hello [Azure portal](https://portal.azure.com), navigate tooyour storage account, find and click **Configuration** under **SETTINGS** tooview and/or change hello account configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="b83dc-163">根據 hello 效能層，您可以選擇建立 hello 儲存體帳戶時，可能無法使用某些複寫選項。</span><span class="sxs-lookup"><span data-stu-id="b83dc-163">Depending on hello performance tier you chose when creating hello storage account, some replication options may not be available.</span></span>
> 
> 

<span data-ttu-id="b83dc-164">變更 hello replication 選項，將會變更您的定價。</span><span class="sxs-lookup"><span data-stu-id="b83dc-164">Changing hello replication option will change your pricing.</span></span> <span data-ttu-id="b83dc-165">如需詳細資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/storage/) 頁面。</span><span class="sxs-lookup"><span data-stu-id="b83dc-165">For more details, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/) page.</span></span>

<span data-ttu-id="b83dc-166">Blob 儲存體帳戶、 變更 hello 存取層可能需支付費用 hello 變更此外 toochanging 價格。</span><span class="sxs-lookup"><span data-stu-id="b83dc-166">For Blob storage accounts, changing hello access tier may incur charges for hello change in addition toochanging your pricing.</span></span> <span data-ttu-id="b83dc-167">請參閱 hello [Blob 儲存體帳戶-定價和計費](../blobs/storage-blob-storage-tiers.md#pricing-and-billing)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b83dc-167">Please see hello [Blob storage accounts - Pricing and Billing](../blobs/storage-blob-storage-tiers.md#pricing-and-billing) for more details.</span></span>

### <a name="manage-your-storage-access-keys"></a><span data-ttu-id="b83dc-168">管理儲存體存取金鑰</span><span class="sxs-lookup"><span data-stu-id="b83dc-168">Manage your storage access keys</span></span>
<span data-ttu-id="b83dc-169">當您建立儲存體帳戶時，Azure 會產生兩個 512 位元儲存體存取金鑰，以存取 hello 儲存體帳戶時用於驗證。</span><span class="sxs-lookup"><span data-stu-id="b83dc-169">When you create a storage account, Azure generates two 512-bit storage access keys, which are used for authentication when hello storage account is accessed.</span></span> <span data-ttu-id="b83dc-170">藉由提供兩個儲存體存取金鑰，Azure 可讓您使用不中斷 tooyour 儲存體服務或存取 toothat 服務 tooregenerate hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b83dc-170">By providing two storage access keys, Azure enables you tooregenerate hello keys with no interruption tooyour storage service or access toothat service.</span></span>

> [!NOTE]
> <span data-ttu-id="b83dc-171">建議您避免將儲存體存取金鑰透露給其他任何人。</span><span class="sxs-lookup"><span data-stu-id="b83dc-171">We recommend that you avoid sharing your storage access keys with anyone else.</span></span> <span data-ttu-id="b83dc-172">toopermit 存取 toostorage 資源卻不用釋出儲存存取金鑰，您可以使用*共用的存取簽章*。</span><span class="sxs-lookup"><span data-stu-id="b83dc-172">toopermit access toostorage resources without giving out your access keys, you can use a *shared access signature*.</span></span> <span data-ttu-id="b83dc-173">您定義的間隔及 hello 權限，您所指定，共用的存取簽章提供給您的帳戶中存取 tooa 資源。</span><span class="sxs-lookup"><span data-stu-id="b83dc-173">A shared access signature provides access tooa resource in your account for an interval that you define and with hello permissions that you specify.</span></span> <span data-ttu-id="b83dc-174">如需詳細資訊，請參閱 [使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md) 。</span><span class="sxs-lookup"><span data-stu-id="b83dc-174">See [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) for more information.</span></span>
> 
> 
<a id="view-and-copy-storage-access-keys"/></a>
#### <a name="view-and-copy-storage-access-keys"></a><span data-ttu-id="b83dc-175">檢視並複製儲存體存取金鑰</span><span class="sxs-lookup"><span data-stu-id="b83dc-175">View and copy storage access keys</span></span>
<span data-ttu-id="b83dc-176">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour 儲存體帳戶，按一下 **所有設定**，然後按一下**存取金鑰**tooview、 複製和重新產生您的帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="b83dc-176">In hello [Azure portal](https://portal.azure.com), navigate tooyour storage account, click **All settings** and then click **Access keys** tooview, copy, and regenerate your account access keys.</span></span> <span data-ttu-id="b83dc-177">hello**便捷鍵**刀鋒視窗中也包含使用您的主要和次要金鑰，您可以在應用程式中複製 toouse 預先設定的連接字串。</span><span class="sxs-lookup"><span data-stu-id="b83dc-177">hello **Access Keys** blade also includes pre-configured connection strings using your primary and secondary keys that you can copy toouse in your applications.</span></span>

#### <a name="regenerate-storage-access-keys"></a><span data-ttu-id="b83dc-178">重新產生儲存體存取金鑰</span><span class="sxs-lookup"><span data-stu-id="b83dc-178">Regenerate storage access keys</span></span>
<span data-ttu-id="b83dc-179">我們建議您變更 hello tooyour 儲存體帳戶定期 toohelp 保護您的儲存體連接的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="b83dc-179">We recommend that you change hello access keys tooyour storage account periodically toohelp keep your storage connections secure.</span></span> <span data-ttu-id="b83dc-180">如此您就可以維護連接 toohello 儲存體帳戶使用一個存取金鑰，當您重新產生 hello 其他存取金鑰，則會指派兩個存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="b83dc-180">Two access keys are assigned so that you can maintain connections toohello storage account by using one access key while you regenerate hello other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="b83dc-181">重新產生存取金鑰，可能會影響 Azure 為您的應用程式相依於 hello 儲存體帳戶中的服務。</span><span class="sxs-lookup"><span data-stu-id="b83dc-181">Regenerating your access keys can affect services in Azure as well as your own applications that are dependent on hello storage account.</span></span> <span data-ttu-id="b83dc-182">使用 hello 存取金鑰 tooaccess hello 儲存體帳戶的所有用戶端必須更新的 toouse hello 新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="b83dc-182">All clients that use hello access key tooaccess hello storage account must be updated toouse hello new key.</span></span>
> 
> 

<span data-ttu-id="b83dc-183">**媒體服務**-如果您有依存於儲存體帳戶的媒體服務時，您必須重新同步處理 hello 存取金鑰與媒體服務重新產生 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b83dc-183">**Media services** - If you have media services that are dependent on your storage account, you must re-sync hello access keys with your media service after you regenerate hello keys.</span></span>

<span data-ttu-id="b83dc-184">**應用程式**-如果您有 web 應用程式或雲端服務該使用 hello 儲存體帳戶，您將會遺失 hello 連線如果您重新產生金鑰，除非您復原您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="b83dc-184">**Applications** - If you have web applications or cloud services that use hello storage account, you will lose hello connections if you regenerate keys, unless you roll your keys.</span></span>

<span data-ttu-id="b83dc-185">**儲存體總管**-如果您使用任何[儲存體總管 中應用程式](storage-explorers.md)，您可能需要 tooupdate hello 儲存體金鑰，而這些應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="b83dc-185">**Storage Explorers** - If you are using any [storage explorer applications](storage-explorers.md), you will probably need tooupdate hello storage key used by those applications.</span></span>

<span data-ttu-id="b83dc-186">以下是 hello 輪替儲存體存取金鑰的程序：</span><span class="sxs-lookup"><span data-stu-id="b83dc-186">Here is hello process for rotating your storage access keys:</span></span>

1. <span data-ttu-id="b83dc-187">更新您的應用程式程式碼 tooreference hello 次要存取金鑰的 hello 儲存體帳戶中的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="b83dc-187">Update hello connection strings in your application code tooreference hello secondary access key of hello storage account.</span></span>
2. <span data-ttu-id="b83dc-188">重新產生儲存體帳戶的 hello 主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="b83dc-188">Regenerate hello primary access key for your storage account.</span></span> <span data-ttu-id="b83dc-189">在 hello**便捷鍵**刀鋒視窗中，按一下**重新產生 Key1**，然後按一下**是**tooconfirm 想 toogenerate 新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="b83dc-189">On hello **Access Keys** blade, click **Regenerate Key1**, and then click **Yes** tooconfirm that you want toogenerate a new key.</span></span>
3. <span data-ttu-id="b83dc-190">更新 hello 連接字串中的程式碼 tooreference hello 新主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="b83dc-190">Update hello connection strings in your code tooreference hello new primary access key.</span></span>
4. <span data-ttu-id="b83dc-191">Hello 重新產生次要存取金鑰 hello 中相同的方式。</span><span class="sxs-lookup"><span data-stu-id="b83dc-191">Regenerate hello secondary access key in hello same manner.</span></span>

## <a name="delete-a-storage-account"></a><span data-ttu-id="b83dc-192">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b83dc-192">Delete a storage account</span></span>
<span data-ttu-id="b83dc-193">tooremove 儲存體帳戶，您無法再使用，瀏覽 toohello 儲存體帳戶中 hello [Azure 入口網站](https://portal.azure.com)，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b83dc-193">tooremove a storage account that you are no longer using, navigate toohello storage account in hello [Azure portal](https://portal.azure.com), and click **Delete**.</span></span> <span data-ttu-id="b83dc-194">刪除儲存體帳戶刪除 hello 整個帳戶，其中包括 hello 帳戶中的所有資料。</span><span class="sxs-lookup"><span data-stu-id="b83dc-194">Deleting a storage account deletes hello entire account, including all data in hello account.</span></span>

> [!WARNING]
> <span data-ttu-id="b83dc-195">它是不可能 toorestore 刪除儲存體帳戶，或擷取的任何它所包含刪除之前 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="b83dc-195">It's not possible toorestore a deleted storage account or retrieve any of hello content that it contained before deletion.</span></span> <span data-ttu-id="b83dc-196">刪除 hello 帳戶之前，您有想 toosave 來確定 tooback 任何項目。</span><span class="sxs-lookup"><span data-stu-id="b83dc-196">Be sure tooback up anything you want toosave before you delete hello account.</span></span> <span data-ttu-id="b83dc-197">這也會保存 true 的任何資源 hello 帳戶中，一旦刪除 blob、 資料表、 佇列或檔案時，將會永久刪除。</span><span class="sxs-lookup"><span data-stu-id="b83dc-197">This also holds true for any resources in hello account—once you delete a blob, table, queue, or file, it is permanently deleted.</span></span>
> 

<span data-ttu-id="b83dc-198">如果您嘗試的 toodelete 與 Azure 虛擬機器相關聯的儲存體帳戶，您可能會收到 hello 仍在使用的儲存體帳戶相關錯誤。</span><span class="sxs-lookup"><span data-stu-id="b83dc-198">If you try toodelete a storage account associated with an Azure virtual machine, you may get an error about hello storage account still being in use.</span></span> <span data-ttu-id="b83dc-199">如需此錯誤的疑難排解協助，請參閱[針對刪除儲存體帳戶時的錯誤進行疑難排解](../common/storage-resource-manager-cannot-delete-storage-account-container-vhd.md)。</span><span class="sxs-lookup"><span data-stu-id="b83dc-199">For help troubleshooting this error, please see [Troubleshoot errors when you delete storage accounts](../common/storage-resource-manager-cannot-delete-storage-account-container-vhd.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b83dc-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b83dc-200">Next steps</span></span>
* <span data-ttu-id="b83dc-201">[Microsoft Azure 儲存體總管](../../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。</span><span class="sxs-lookup"><span data-stu-id="b83dc-201">[Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="b83dc-202">Azure Blob 儲存體：經常存取及不常存取層</span><span class="sxs-lookup"><span data-stu-id="b83dc-202">Azure Blob Storage: Cool and Hot tiers</span></span>](../blobs/storage-blob-storage-tiers.md)
* [<span data-ttu-id="b83dc-203">Azure 儲存體複寫</span><span class="sxs-lookup"><span data-stu-id="b83dc-203">Azure Storage replication</span></span>](storage-redundancy.md)
* [<span data-ttu-id="b83dc-204">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="b83dc-204">Configure Azure Storage Connection Strings</span></span>](../storage-configure-connection-string.md)
* [<span data-ttu-id="b83dc-205">使用 AzCopy 命令列公用程式的 hello 傳輸資料</span><span class="sxs-lookup"><span data-stu-id="b83dc-205">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)
* <span data-ttu-id="b83dc-206">請瀏覽 hello [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)。</span><span class="sxs-lookup"><span data-stu-id="b83dc-206">Visit hello [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

