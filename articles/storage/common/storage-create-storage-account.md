---
title: "如何在 Azure 入口網站中建立、管理或刪除儲存體帳戶 | Microsoft Docs"
description: "在 Azure 入口網站中建立新的儲存體帳戶、管理帳戶存取金鑰，或刪除儲存體帳戶。 了解標準和進階儲存體帳戶。"
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
ms.openlocfilehash: 848f6b07e51b58b00b81dd42ca1d478fdba20d06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="about-azure-storage-accounts"></a><span data-ttu-id="63d9c-104">關於 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="63d9c-104">About Azure storage accounts</span></span>
[!INCLUDE [storage-selector-portal-create-storage-account](../../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-table-cosmos-db-tip-include](../../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="63d9c-105">Overview</span><span class="sxs-lookup"><span data-stu-id="63d9c-105">Overview</span></span>
<span data-ttu-id="63d9c-106">Azure 儲存體帳戶提供唯一命名空間來儲存及存取您的 Azure 儲存體資料物件。</span><span class="sxs-lookup"><span data-stu-id="63d9c-106">An Azure storage account provides a unique namespace to store and access your Azure Storage data objects.</span></span> <span data-ttu-id="63d9c-107">儲存體帳戶中的所有物件會做為群組共同計費。</span><span class="sxs-lookup"><span data-stu-id="63d9c-107">All objects in a storage account are billed together as a group.</span></span> <span data-ttu-id="63d9c-108">根據預設，您帳戶中的資料只有帳戶擁有者 (也就是您) 可以使用。</span><span class="sxs-lookup"><span data-stu-id="63d9c-108">By default, the data in your account is available only to you, the account owner.</span></span>

[!INCLUDE [storage-account-types-include](../../../includes/storage-account-types-include.md)]

## <a name="storage-account-billing"></a><span data-ttu-id="63d9c-109">儲存體帳戶計費</span><span class="sxs-lookup"><span data-stu-id="63d9c-109">Storage account billing</span></span>
[!INCLUDE [storage-account-billing-include](../../../includes/storage-account-billing-include.md)]

> [!NOTE]
> <span data-ttu-id="63d9c-110">當您建立 Azure 虛擬機器時，如果您在部署位置中沒有儲存體帳戶，則會在該位置自動建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="63d9c-110">When you create an Azure virtual machine, a storage account is created for you automatically in the deployment location if you do not already have a storage account in that location.</span></span> <span data-ttu-id="63d9c-111">因此，您無須依照下方的步驟為虛擬機器磁碟建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="63d9c-111">So it's not necessary to follow the steps below to create a storage account for your virtual machine disks.</span></span> <span data-ttu-id="63d9c-112">儲存體帳戶名稱將以虛擬機器名稱為基礎。</span><span class="sxs-lookup"><span data-stu-id="63d9c-112">The storage account name will be based on the virtual machine name.</span></span> <span data-ttu-id="63d9c-113">如需詳細資訊，請參閱 [Azure 虛擬機器文件](https://azure.microsoft.com/documentation/services/virtual-machines/) 。</span><span class="sxs-lookup"><span data-stu-id="63d9c-113">See the [Azure Virtual Machines documentation](https://azure.microsoft.com/documentation/services/virtual-machines/) for more details.</span></span>
> 
> 

## <a name="storage-account-endpoints"></a><span data-ttu-id="63d9c-114">儲存體帳戶端點</span><span class="sxs-lookup"><span data-stu-id="63d9c-114">Storage account endpoints</span></span>
<span data-ttu-id="63d9c-115">每個儲存在 Azure 儲存體中的物件都有一個唯一 URL 位址。</span><span class="sxs-lookup"><span data-stu-id="63d9c-115">Every object that you store in Azure Storage has a unique URL address.</span></span> <span data-ttu-id="63d9c-116">儲存體帳戶名稱會構成該位址的子網域。</span><span class="sxs-lookup"><span data-stu-id="63d9c-116">The storage account name forms the subdomain of that address.</span></span> <span data-ttu-id="63d9c-117">子網域和每個服務的特定網域名稱的組合，會構成儲存體帳戶的 *端點* 。</span><span class="sxs-lookup"><span data-stu-id="63d9c-117">The combination of subdomain and domain name, which is specific to each service, forms an *endpoint* for your storage account.</span></span>

<span data-ttu-id="63d9c-118">例如，如果您的儲存體帳戶名為 *mystorageaccount*，則儲存體帳戶的預設端點將是：</span><span class="sxs-lookup"><span data-stu-id="63d9c-118">For example, if your storage account is named *mystorageaccount*, then the default endpoints for your storage account are:</span></span>

* <span data-ttu-id="63d9c-119">Blob 服務：http://*mystorageaccount*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="63d9c-119">Blob service: http://*mystorageaccount*.blob.core.windows.net</span></span>
* <span data-ttu-id="63d9c-120">表格服務：http://*mystorageaccount*.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="63d9c-120">Table service: http://*mystorageaccount*.table.core.windows.net</span></span>
* <span data-ttu-id="63d9c-121">佇列服務：http://*mystorageaccount*.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="63d9c-121">Queue service: http://*mystorageaccount*.queue.core.windows.net</span></span>
* <span data-ttu-id="63d9c-122">檔案服務：http://*mystorageaccount.file.core.windows.net*.file.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="63d9c-122">File service: http://*mystorageaccount*.file.core.windows.net</span></span>

> [!NOTE]
> <span data-ttu-id="63d9c-123">Blob 儲存體帳戶只會公開 Blob 服務端點。</span><span class="sxs-lookup"><span data-stu-id="63d9c-123">A Blob storage account only exposes the Blob service endpoint.</span></span>
> 
> 

<span data-ttu-id="63d9c-124">用以存取儲存體帳戶中某物件的 URL，可藉由在端點後附加該物件在儲存體帳戶中的位置來建置。</span><span class="sxs-lookup"><span data-stu-id="63d9c-124">The URL for accessing an object in a storage account is built by appending the object's location in the storage account to the endpoint.</span></span> <span data-ttu-id="63d9c-125">例如，blob 位址可能會有如下格式︰http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*。</span><span class="sxs-lookup"><span data-stu-id="63d9c-125">For example, a blob address might have this format: http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*.</span></span>

<span data-ttu-id="63d9c-126">您也可以設定與儲存體帳戶搭配使用的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="63d9c-126">You can also configure a custom domain name to use with your storage account.</span></span> <span data-ttu-id="63d9c-127">如需詳細資訊，請參閱[針對 Blob 儲存體端點設定自訂網域名稱](../blobs/storage-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="63d9c-127">For more information, see [Configure a custom domain Name for your Blob Storage Endpoint](../blobs/storage-custom-domain-name.md).</span></span> <span data-ttu-id="63d9c-128">您也可以使用 PowerShell 加以設定。</span><span class="sxs-lookup"><span data-stu-id="63d9c-128">You can also configure it with PowerShell.</span></span> <span data-ttu-id="63d9c-129">如需詳細資訊，請參閱 [Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="63d9c-129">For more information, see the [Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) cmdlet.</span></span>  


## <a name="create-a-storage-account"></a><span data-ttu-id="63d9c-130">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="63d9c-130">Create a storage account</span></span>
1. <span data-ttu-id="63d9c-131">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="63d9c-131">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="63d9c-132">在 [中樞] 功能表上，選取 [新增] -> [儲存體] -> [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="63d9c-132">On the Hub menu, select **New** -> **Storage** -> **Storage account**.</span></span>
3. <span data-ttu-id="63d9c-133">輸入儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="63d9c-133">Enter a name for your storage account.</span></span> <span data-ttu-id="63d9c-134">請參閱 [儲存體帳戶端點](#storage-account-endpoints) 以深入了解此儲存體帳戶名稱如何用來解析 Azure 儲存體中的物件。</span><span class="sxs-lookup"><span data-stu-id="63d9c-134">See [Storage account endpoints](#storage-account-endpoints) for details about how the storage account name will be used to address your objects in Azure Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="63d9c-135">儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能包含數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="63d9c-135">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>
   > 
   > <span data-ttu-id="63d9c-136">儲存體帳戶名稱必須在 Azure 中是獨一無二的。</span><span class="sxs-lookup"><span data-stu-id="63d9c-136">Your storage account name must be unique within Azure.</span></span> <span data-ttu-id="63d9c-137">Azure 入口網站會指出您選取的儲存體帳戶名稱是否已在使用中。</span><span class="sxs-lookup"><span data-stu-id="63d9c-137">The Azure portal will indicate if the storage account name you select is already in use.</span></span>
   > 
   > 
4. <span data-ttu-id="63d9c-138">指定所要使用的部署模型：[Resource Manager] 或 [傳統]。</span><span class="sxs-lookup"><span data-stu-id="63d9c-138">Specify the deployment model to be used: **Resource Manager** or **Classic**.</span></span> <span data-ttu-id="63d9c-139"> 是建議的部署模型。</span><span class="sxs-lookup"><span data-stu-id="63d9c-139">**Resource Manager** is the recommended deployment model.</span></span> <span data-ttu-id="63d9c-140">如需詳細資訊，請參閱 [了解資源管理員部署和傳統部署](../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="63d9c-140">For more information, see [Understanding Resource Manager deployment and classic deployment](../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="63d9c-141">僅可使用資源管理員部署模型來建立 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="63d9c-141">Blob storage accounts can only be created using the Resource Manager deployment model.</span></span>

5. <span data-ttu-id="63d9c-142">選取儲存體帳戶的類型︰[一般用途] 或 [Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="63d9c-142">Select the type of storage account: **General purpose** or **Blob storage**.</span></span> <span data-ttu-id="63d9c-143"> 是預設值。</span><span class="sxs-lookup"><span data-stu-id="63d9c-143">**General purpose** is the default.</span></span>
   
    <span data-ttu-id="63d9c-144">如果已選取 [一般用途]，則指定效能層︰[標準] 或 [進階]。</span><span class="sxs-lookup"><span data-stu-id="63d9c-144">If **General purpose** was selected, then specify the performance tier: **Standard** or **Premium**.</span></span> <span data-ttu-id="63d9c-145">預設值是 [標準] 。</span><span class="sxs-lookup"><span data-stu-id="63d9c-145">The default is **Standard**.</span></span> <span data-ttu-id="63d9c-146">如需標準和進階儲存體帳戶的詳細資訊，請參閱 [Microsoft Azure 儲存體簡介](storage-introduction.md)和[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](storage-premium-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="63d9c-146">For more details on standard and premium storage accounts, see [Introduction to Microsoft Azure Storage](storage-introduction.md) and [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span>
   
    <span data-ttu-id="63d9c-147">如果已選取 **Blob 儲存體**，則指定存取層︰[經常存取] 或 [不常存取]。</span><span class="sxs-lookup"><span data-stu-id="63d9c-147">If **Blob Storage** was selected, then specify the access tier: **Hot** or **Cool**.</span></span> <span data-ttu-id="63d9c-148">預設值為 [經常存取] 。</span><span class="sxs-lookup"><span data-stu-id="63d9c-148">The default is **Hot**.</span></span> <span data-ttu-id="63d9c-149">如需詳細資訊，請參閱 [Azure Blob 儲存體：經常存取及不常存取層](../blobs/storage-blob-storage-tiers.md) 。</span><span class="sxs-lookup"><span data-stu-id="63d9c-149">See [Azure Blob Storage: Cool and Hot tiers](../blobs/storage-blob-storage-tiers.md) for more details.</span></span>
6. <span data-ttu-id="63d9c-150">選取儲存體帳戶的複寫選項︰[LRS]、[GRS]、[RA-GRS] 或 [ZRS]。</span><span class="sxs-lookup"><span data-stu-id="63d9c-150">Select the replication option for the storage account: **LRS**, **GRS**, **RA-GRS**, or **ZRS**.</span></span> <span data-ttu-id="63d9c-151">預設值是 [RA-GRS] 。</span><span class="sxs-lookup"><span data-stu-id="63d9c-151">The default is **RA-GRS**.</span></span> <span data-ttu-id="63d9c-152">如需 Azure 儲存體複寫選項的詳細資訊，請參閱 [Azure 儲存體複寫](storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="63d9c-152">For more details on Azure Storage replication options, see [Azure Storage replication](storage-redundancy.md).</span></span>
7. <span data-ttu-id="63d9c-153">選取您要在其中建立新儲存體帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="63d9c-153">Select the subscription in which you want to create the new storage account.</span></span>
8. <span data-ttu-id="63d9c-154">指定新的資源群組，或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="63d9c-154">Specify a new resource group or select an existing resource group.</span></span> <span data-ttu-id="63d9c-155">如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="63d9c-155">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>
9. <span data-ttu-id="63d9c-156">選取儲存體帳戶的地理位置。</span><span class="sxs-lookup"><span data-stu-id="63d9c-156">Select the geographic location for your storage account.</span></span> <span data-ttu-id="63d9c-157">如需各區域可用服務的詳細資訊，請參閱 [Azure 區域](https://azure.microsoft.com/regions/#services) 。</span><span class="sxs-lookup"><span data-stu-id="63d9c-157">See [Azure Regions](https://azure.microsoft.com/regions/#services) for more information about what services are available in which region.</span></span>
10. <span data-ttu-id="63d9c-158">按一下 [建立]  建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="63d9c-158">Click **Create** to create the storage account.</span></span>

## <a name="manage-your-storage-account"></a><span data-ttu-id="63d9c-159">管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="63d9c-159">Manage your storage account</span></span>
### <a name="change-your-account-configuration"></a><span data-ttu-id="63d9c-160">變更帳戶組態</span><span class="sxs-lookup"><span data-stu-id="63d9c-160">Change your account configuration</span></span>
<span data-ttu-id="63d9c-161">建立儲存體帳戶之後，您可以修改其組態，例如變更帳戶所用的複寫選項，或變更 Blob 儲存體帳戶的存取層。</span><span class="sxs-lookup"><span data-stu-id="63d9c-161">After you create your storage account, you can modify its configuration, such as changing the replication option used for the account or changing the access tier for a Blob storage account.</span></span> <span data-ttu-id="63d9c-162">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至您的儲存體帳戶，尋找並按一下 [設定] 之下的 [組態] 以檢視和/或變更帳戶組態。</span><span class="sxs-lookup"><span data-stu-id="63d9c-162">In the [Azure portal](https://portal.azure.com), navigate to your storage account, find and click **Configuration** under **SETTINGS** to view and/or change the account configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="63d9c-163">視您在建立儲存體帳戶時選擇的效能層而定，可能無法使用某些複寫選項。</span><span class="sxs-lookup"><span data-stu-id="63d9c-163">Depending on the performance tier you chose when creating the storage account, some replication options may not be available.</span></span>
> 
> 

<span data-ttu-id="63d9c-164">變更複寫選項，將會變更您的價格。</span><span class="sxs-lookup"><span data-stu-id="63d9c-164">Changing the replication option will change your pricing.</span></span> <span data-ttu-id="63d9c-165">如需詳細資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/storage/) 頁面。</span><span class="sxs-lookup"><span data-stu-id="63d9c-165">For more details, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/) page.</span></span>

<span data-ttu-id="63d9c-166">針對 Blob 儲存體帳戶，變更存取層除了會變更您的價格之外，可能還會產生費用的變更。</span><span class="sxs-lookup"><span data-stu-id="63d9c-166">For Blob storage accounts, changing the access tier may incur charges for the change in addition to changing your pricing.</span></span> <span data-ttu-id="63d9c-167">如需詳細資訊，請參閱 [Blob 儲存體帳戶 - 價格和計費](../blobs/storage-blob-storage-tiers.md#pricing-and-billing) 。</span><span class="sxs-lookup"><span data-stu-id="63d9c-167">Please see the [Blob storage accounts - Pricing and Billing](../blobs/storage-blob-storage-tiers.md#pricing-and-billing) for more details.</span></span>

### <a name="manage-your-storage-access-keys"></a><span data-ttu-id="63d9c-168">管理儲存體存取金鑰</span><span class="sxs-lookup"><span data-stu-id="63d9c-168">Manage your storage access keys</span></span>
<span data-ttu-id="63d9c-169">當您建立儲存體帳戶時，Azure 會產生兩個 512 位元的儲存體存取金鑰，做為存取儲存體帳戶時的驗證憑藉。</span><span class="sxs-lookup"><span data-stu-id="63d9c-169">When you create a storage account, Azure generates two 512-bit storage access keys, which are used for authentication when the storage account is accessed.</span></span> <span data-ttu-id="63d9c-170">透過提供這兩個儲存體存取金鑰，Azure 讓您可重新產生金鑰，同時又不需中斷儲存體服務或對該服務的存取。</span><span class="sxs-lookup"><span data-stu-id="63d9c-170">By providing two storage access keys, Azure enables you to regenerate the keys with no interruption to your storage service or access to that service.</span></span>

> [!NOTE]
> <span data-ttu-id="63d9c-171">建議您避免將儲存體存取金鑰透露給其他任何人。</span><span class="sxs-lookup"><span data-stu-id="63d9c-171">We recommend that you avoid sharing your storage access keys with anyone else.</span></span> <span data-ttu-id="63d9c-172">若要允許存取儲存體資源但不要公開您的存取金鑰，您可以使用「共用存取簽章」 。</span><span class="sxs-lookup"><span data-stu-id="63d9c-172">To permit access to storage resources without giving out your access keys, you can use a *shared access signature*.</span></span> <span data-ttu-id="63d9c-173">共用存取簽章可在您定義的間隔期間內，使用您所指定的權限，來存取帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="63d9c-173">A shared access signature provides access to a resource in your account for an interval that you define and with the permissions that you specify.</span></span> <span data-ttu-id="63d9c-174">如需詳細資訊，請參閱 [使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md) 。</span><span class="sxs-lookup"><span data-stu-id="63d9c-174">See [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) for more information.</span></span>
> 
> 
<a id="view-and-copy-storage-access-keys"/></a>
#### <a name="view-and-copy-storage-access-keys"></a><span data-ttu-id="63d9c-175">檢視並複製儲存體存取金鑰</span><span class="sxs-lookup"><span data-stu-id="63d9c-175">View and copy storage access keys</span></span>
<span data-ttu-id="63d9c-176">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至您的儲存體帳戶，按一下 [所有設定]，然後按一下 [存取金鑰] 圖示來檢視、複製和重新產生帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="63d9c-176">In the [Azure portal](https://portal.azure.com), navigate to your storage account, click **All settings** and then click **Access keys** to view, copy, and regenerate your account access keys.</span></span> <span data-ttu-id="63d9c-177">[存取金鑰]  刀鋒視窗也包含使用您主要與次要金鑰的預先設定連接字串，讓您可以複製以在應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="63d9c-177">The **Access Keys** blade also includes pre-configured connection strings using your primary and secondary keys that you can copy to use in your applications.</span></span>

#### <a name="regenerate-storage-access-keys"></a><span data-ttu-id="63d9c-178">重新產生儲存體存取金鑰</span><span class="sxs-lookup"><span data-stu-id="63d9c-178">Regenerate storage access keys</span></span>
<span data-ttu-id="63d9c-179">建議您定期變更儲存體帳戶的存取金鑰，保護儲存體連線的安全。</span><span class="sxs-lookup"><span data-stu-id="63d9c-179">We recommend that you change the access keys to your storage account periodically to help keep your storage connections secure.</span></span> <span data-ttu-id="63d9c-180">指派了兩個存取金鑰，因此您可以在重新產生一個存取金鑰的同時，使用另一個存取金鑰維持儲存體帳戶連線。</span><span class="sxs-lookup"><span data-stu-id="63d9c-180">Two access keys are assigned so that you can maintain connections to the storage account by using one access key while you regenerate the other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="63d9c-181">重新產生存取金鑰會影響 Azure 中的服務，以及您自己的相依於儲存體帳戶的應用程式。</span><span class="sxs-lookup"><span data-stu-id="63d9c-181">Regenerating your access keys can affect services in Azure as well as your own applications that are dependent on the storage account.</span></span> <span data-ttu-id="63d9c-182">所有使用存取金鑰來存取儲存體帳戶的用戶端，都必須更新為使用新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="63d9c-182">All clients that use the access key to access the storage account must be updated to use the new key.</span></span>
> 
> 

<span data-ttu-id="63d9c-183">**媒體服務** - 如果您有媒體服務相依於儲存體帳戶，您必須在重新產生金鑰之後，將存取金鑰與媒體服務重新同步。</span><span class="sxs-lookup"><span data-stu-id="63d9c-183">**Media services** - If you have media services that are dependent on your storage account, you must re-sync the access keys with your media service after you regenerate the keys.</span></span>

<span data-ttu-id="63d9c-184">**應用程式** - 如果您有 Web 應用程式或雲端服務使用儲存體帳戶，除非您變換金鑰，否則會在重新產生金鑰後失去連線。</span><span class="sxs-lookup"><span data-stu-id="63d9c-184">**Applications** - If you have web applications or cloud services that use the storage account, you will lose the connections if you regenerate keys, unless you roll your keys.</span></span>

<span data-ttu-id="63d9c-185">**儲存體總管** - 如果您使用任何 [儲存體總管應用程式](storage-explorers.md)，可能需要更新這些應用程式所使用的儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="63d9c-185">**Storage Explorers** - If you are using any [storage explorer applications](storage-explorers.md), you will probably need to update the storage key used by those applications.</span></span>

<span data-ttu-id="63d9c-186">以下是替換儲存體存取金鑰的程序：</span><span class="sxs-lookup"><span data-stu-id="63d9c-186">Here is the process for rotating your storage access keys:</span></span>

1. <span data-ttu-id="63d9c-187">更新應用程式程式碼中的連接字串，以參考儲存體帳戶的次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="63d9c-187">Update the connection strings in your application code to reference the secondary access key of the storage account.</span></span>
2. <span data-ttu-id="63d9c-188">重新產生儲存體帳戶的主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="63d9c-188">Regenerate the primary access key for your storage account.</span></span> <span data-ttu-id="63d9c-189">按一下 [存取金鑰] 刀鋒視窗上的 [重新產生 Key1]，然後按一下 [是] 確認您要重新產生新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="63d9c-189">On the **Access Keys** blade, click **Regenerate Key1**, and then click **Yes** to confirm that you want to generate a new key.</span></span>
3. <span data-ttu-id="63d9c-190">更新程式碼中的連接字串，以參考新的主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="63d9c-190">Update the connection strings in your code to reference the new primary access key.</span></span>
4. <span data-ttu-id="63d9c-191">以同樣的方式重新產生次要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="63d9c-191">Regenerate the secondary access key in the same manner.</span></span>

## <a name="delete-a-storage-account"></a><span data-ttu-id="63d9c-192">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="63d9c-192">Delete a storage account</span></span>
<span data-ttu-id="63d9c-193">若要移除不再使用的儲存體帳戶，請在 [Azure 入口網站](https://portal.azure.com)中瀏覽至儲存體帳戶，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="63d9c-193">To remove a storage account that you are no longer using, navigate to the storage account in the [Azure portal](https://portal.azure.com), and click **Delete**.</span></span> <span data-ttu-id="63d9c-194">刪除儲存體帳戶會刪除整個帳戶，包括帳戶中的所有資料。</span><span class="sxs-lookup"><span data-stu-id="63d9c-194">Deleting a storage account deletes the entire account, including all data in the account.</span></span>

> [!WARNING]
> <span data-ttu-id="63d9c-195">您無法還原已刪除的儲存體帳戶，也無法擷取刪除之前所包含的任何內容。</span><span class="sxs-lookup"><span data-stu-id="63d9c-195">It's not possible to restore a deleted storage account or retrieve any of the content that it contained before deletion.</span></span> <span data-ttu-id="63d9c-196">請務必先備份您想要儲存的任何資料，再刪除帳戶。</span><span class="sxs-lookup"><span data-stu-id="63d9c-196">Be sure to back up anything you want to save before you delete the account.</span></span> <span data-ttu-id="63d9c-197">這也適用於帳戶中的任何資源 - 一旦刪除 Blob、資料表、佇列或檔案，就是永久刪除。</span><span class="sxs-lookup"><span data-stu-id="63d9c-197">This also holds true for any resources in the account—once you delete a blob, table, queue, or file, it is permanently deleted.</span></span>
> 

<span data-ttu-id="63d9c-198">如果您嘗試刪除與 Azure 虛擬機器相關聯的儲存體帳戶，您可能會收到儲存體帳戶仍在使用中的相關錯誤。</span><span class="sxs-lookup"><span data-stu-id="63d9c-198">If you try to delete a storage account associated with an Azure virtual machine, you may get an error about the storage account still being in use.</span></span> <span data-ttu-id="63d9c-199">如需此錯誤的疑難排解協助，請參閱[針對刪除儲存體帳戶時的錯誤進行疑難排解](../common/storage-resource-manager-cannot-delete-storage-account-container-vhd.md)。</span><span class="sxs-lookup"><span data-stu-id="63d9c-199">For help troubleshooting this error, please see [Troubleshoot errors when you delete storage accounts](../common/storage-resource-manager-cannot-delete-storage-account-container-vhd.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="63d9c-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63d9c-200">Next steps</span></span>
* <span data-ttu-id="63d9c-201">[Microsoft Azure 儲存體總管](../../vs-azure-tools-storage-manage-with-storage-explorer.md) 是一個免費的獨立應用程式，可讓您在 Windows、MacOS 和 Linux 上以視覺化方式處理 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="63d9c-201">[Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="63d9c-202">Azure Blob 儲存體：經常存取及不常存取層</span><span class="sxs-lookup"><span data-stu-id="63d9c-202">Azure Blob Storage: Cool and Hot tiers</span></span>](../blobs/storage-blob-storage-tiers.md)
* [<span data-ttu-id="63d9c-203">Azure 儲存體複寫</span><span class="sxs-lookup"><span data-stu-id="63d9c-203">Azure Storage replication</span></span>](storage-redundancy.md)
* [<span data-ttu-id="63d9c-204">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="63d9c-204">Configure Azure Storage Connection Strings</span></span>](../storage-configure-connection-string.md)
* [<span data-ttu-id="63d9c-205">使用 AzCopy 命令列公用程式傳輸資料</span><span class="sxs-lookup"><span data-stu-id="63d9c-205">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)
* <span data-ttu-id="63d9c-206">造訪 [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)(英文)。</span><span class="sxs-lookup"><span data-stu-id="63d9c-206">Visit the [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

