---
title: "可以搭配 Azure 儲存體的 aaaSecurity 功能 |Microsoft 文件"
description: " 本文章提供可以搭配 Azure 儲存體的 hello 核心 Azure 的安全性功能的概觀。 "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 521180dc-2cc9-43f1-ae87-2701de7ca6b8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 663cd2705527957d21ff9475a6322b42a16c95e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-overview"></a><span data-ttu-id="06561-103">Azure 儲存體安全性概觀</span><span class="sxs-lookup"><span data-stu-id="06561-103">Azure storage security overview</span></span>
<span data-ttu-id="06561-104">Azure 儲存體是 hello 雲端儲存體解決方案，依賴持續性、 可用性和延展性 toomeet hello 需求的客戶的現代應用程式。</span><span class="sxs-lookup"><span data-stu-id="06561-104">Azure Storage is hello cloud storage solution for modern applications that rely on durability, availability, and scalability toomeet hello needs of their customers.</span></span> <span data-ttu-id="06561-105">Azure 儲存體提供一組完整的安全性功能：</span><span class="sxs-lookup"><span data-stu-id="06561-105">Azure Storage provides a comprehensive set of security capabilities:</span></span>

* <span data-ttu-id="06561-106">可以使用角色型存取控制與 Azure Active Directory 來保護 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="06561-106">hello storage account can be secured using Role-Based Access Control and Azure Active Directory.</span></span>
* <span data-ttu-id="06561-107">您可以使用用戶端加密、HTTP 或 SMB 3.0，在應用程式和 Azure 之間進行傳輸時保護資料的安全。</span><span class="sxs-lookup"><span data-stu-id="06561-107">Data can be secured in transit between an application and Azure by using Client-Side Encryption, HTTPS, or SMB 3.0.</span></span>
* <span data-ttu-id="06561-108">資料可以設定自動加密 toobe 寫入 tooAzure 使用儲存體服務加密的存放裝置時。</span><span class="sxs-lookup"><span data-stu-id="06561-108">Data can be set toobe automatically encrypted when written tooAzure Storage using Storage Service Encryption.</span></span>
* <span data-ttu-id="06561-109">虛擬機器所使用的作業系統和資料磁碟可以設定 toobe 使用 Azure 磁碟加密進行加密。</span><span class="sxs-lookup"><span data-stu-id="06561-109">OS and Data disks used by virtual machines can be set toobe encrypted using Azure Disk Encryption.</span></span>
* <span data-ttu-id="06561-110">Azure 儲存體中的委派的存取 toohello 資料物件可以使用共用存取簽章授與。</span><span class="sxs-lookup"><span data-stu-id="06561-110">Delegated access toohello data objects in Azure Storage can be granted using Shared Access Signatures.</span></span>
* <span data-ttu-id="06561-111">存取儲存體時使用的其他人的 hello 驗證方法可以使用儲存體分析追蹤。</span><span class="sxs-lookup"><span data-stu-id="06561-111">hello authentication method used by someone when they access storage can be tracked using Storage analytics.</span></span>

<span data-ttu-id="06561-112">Azure 儲存體中的安全性更詳細探討，請參閱 hello [Azure 儲存體安全性指南 》](../storage/common/storage-security-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="06561-112">For a more detailed look at security in Azure Storage, see hello [Azure Storage security guide](../storage/common/storage-security-guide.md).</span></span> <span data-ttu-id="06561-113">本指南提供深入探討 hello 安全性功能，Azure 儲存體的儲存體帳戶金鑰，例如資料加密傳輸中和在其餘部分和儲存體分析。</span><span class="sxs-lookup"><span data-stu-id="06561-113">This guide provides a deep dive into hello security features of Azure Storage such as storage account keys, data encryption in transit and at rest, and storage analytics.</span></span>

<span data-ttu-id="06561-114">本文提供可與「Azure 儲存體」搭配使用的 Azure 安全性功能概觀。</span><span class="sxs-lookup"><span data-stu-id="06561-114">This article provides an overview of Azure security features that can be used with Azure Storage.</span></span> <span data-ttu-id="06561-115">提供給每項功能的詳細資料，因此，您可以深入的 tooarticles 時，會提供連結。</span><span class="sxs-lookup"><span data-stu-id="06561-115">Links are provided tooarticles that give details of each feature so you can learn more.</span></span>

<span data-ttu-id="06561-116">以下是本文章涵蓋 hello 核心功能 toobe:</span><span class="sxs-lookup"><span data-stu-id="06561-116">Here are hello core features toobe covered in this article:</span></span>

* <span data-ttu-id="06561-117">角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="06561-117">Role-Based Access Control</span></span>
* <span data-ttu-id="06561-118">委派的存取 toostorage 物件</span><span class="sxs-lookup"><span data-stu-id="06561-118">Delegated access toostorage objects</span></span>
* <span data-ttu-id="06561-119">傳輸中加密</span><span class="sxs-lookup"><span data-stu-id="06561-119">Encryption in transit</span></span>
* <span data-ttu-id="06561-120">待用加密/儲存體服務加密</span><span class="sxs-lookup"><span data-stu-id="06561-120">Encryption at rest/Storage Service Encryption</span></span>
* <span data-ttu-id="06561-121">Azure 磁碟加密</span><span class="sxs-lookup"><span data-stu-id="06561-121">Azure Disk Encryption</span></span>
* <span data-ttu-id="06561-122">Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="06561-122">Azure Key Vault</span></span>

## <a name="role-based-access-control-rbac"></a><span data-ttu-id="06561-123">角色型存取控制 (RBAC)</span><span class="sxs-lookup"><span data-stu-id="06561-123">Role-Based Access Control (RBAC)</span></span>
<span data-ttu-id="06561-124">您可以使用角色型存取控制 (RBAC) 來保護儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="06561-124">You can secure your storage account with Role-Based Access Control (RBAC).</span></span> <span data-ttu-id="06561-125">限制存取根據 hello[需要 tooknow](https://en.wikipedia.org/wiki/Need_to_know)和[最小權限](https://en.wikipedia.org/wiki/Principle_of_least_privilege)安全性原則是命令式 tooenforce 安全性原則所需的資料存取的組織。</span><span class="sxs-lookup"><span data-stu-id="06561-125">Restricting access based on hello [need tooknow](https://en.wikipedia.org/wiki/Need_to_know) and [least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) security principles is imperative for organizations that want tooenforce security policies for data access.</span></span> <span data-ttu-id="06561-126">這些存取權限會授與指定適當 RBAC 角色 toogroups hello 與應用程式在特定範圍內。</span><span class="sxs-lookup"><span data-stu-id="06561-126">These access rights are granted by assigning hello appropriate RBAC role toogroups and applications at a certain scope.</span></span> <span data-ttu-id="06561-127">您可以使用[內建的 RBAC 角色](../active-directory/role-based-access-built-in-roles.md)，例如儲存體帳戶參與者 tooassign 權限 toousers。</span><span class="sxs-lookup"><span data-stu-id="06561-127">You can use [built-in RBAC roles](../active-directory/role-based-access-built-in-roles.md), such as Storage Account Contributor, tooassign privileges toousers.</span></span>

<span data-ttu-id="06561-128">深入了解：</span><span class="sxs-lookup"><span data-stu-id="06561-128">Learn more:</span></span>

* [<span data-ttu-id="06561-129">Azure Active Directory 角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="06561-129">Azure Active Directory Role-based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="delegated-access-toostorage-objects"></a><span data-ttu-id="06561-130">委派的存取 toostorage 物件</span><span class="sxs-lookup"><span data-stu-id="06561-130">Delegated access toostorage objects</span></span>
<span data-ttu-id="06561-131">共用的存取簽章 (SAS) 提供儲存體帳戶中的委派的存取 tooresources。</span><span class="sxs-lookup"><span data-stu-id="06561-131">A shared access signature (SAS) provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="06561-132">hello SAS 表示您可以授與用戶端有限的儲存體帳戶中的權限 tooobjects 指定期間內的時間與指定權限集。</span><span class="sxs-lookup"><span data-stu-id="06561-132">hello SAS means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions.</span></span> <span data-ttu-id="06561-133">您可以授與這些有限權限，而不需要 tooshare 帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="06561-133">You can grant these limited permissions without having tooshare your account access keys.</span></span> <span data-ttu-id="06561-134">hello SAS 是包含在其查詢參數中所有的 hello 資訊所需的已驗證的存取 tooa 儲存體資源的 URI。</span><span class="sxs-lookup"><span data-stu-id="06561-134">hello SAS is a URI that encompasses in its query parameters all hello information necessary for authenticated access tooa storage resource.</span></span> <span data-ttu-id="06561-135">tooaccess 以 hello SAS 存放裝置資源，hello 用戶端只需要 tooprovide hello SAS toohello 適當建構函式或方法。</span><span class="sxs-lookup"><span data-stu-id="06561-135">tooaccess storage resources with hello SAS, hello client only needs tooprovide hello SAS toohello appropriate constructor or method.</span></span>

<span data-ttu-id="06561-136">深入了解：</span><span class="sxs-lookup"><span data-stu-id="06561-136">Learn more:</span></span>

* [<span data-ttu-id="06561-137">了解 hello SAS 模型</span><span class="sxs-lookup"><span data-stu-id="06561-137">Understanding hello SAS model</span></span>](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="06561-138">透過 Blob 儲存體來建立與使用 SAS</span><span class="sxs-lookup"><span data-stu-id="06561-138">Create and use a SAS with Blob storage</span></span>](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)

## <a name="encryption-in-transit"></a><span data-ttu-id="06561-139">傳輸中加密</span><span class="sxs-lookup"><span data-stu-id="06561-139">Encryption in transit</span></span>
<span data-ttu-id="06561-140">傳輸中加密是透過網路傳輸資料時用來保護資料的機制。</span><span class="sxs-lookup"><span data-stu-id="06561-140">Encryption in transit is a mechanism of protecting data when it is transmitted across networks.</span></span> <span data-ttu-id="06561-141">使用 Azure 儲存體，您可以使用下列各向來保護資料︰</span><span class="sxs-lookup"><span data-stu-id="06561-141">With Azure Storage you can secure data using:</span></span>

* <span data-ttu-id="06561-142">[傳輸層級加密](../storage/common/storage-security-guide.md#encryption-in-transit)，例如從 Azure 儲存體傳入或傳出資料時的 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="06561-142">[Transport-level encryption](../storage/common/storage-security-guide.md#encryption-in-transit), such as HTTPS when you transfer data into or out of Azure Storage.</span></span>
* <span data-ttu-id="06561-143">[連線加密](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares)，例如 Azure 檔案共用的 SMB 3.0 加密。</span><span class="sxs-lookup"><span data-stu-id="06561-143">[Wire encryption](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), such as SMB 3.0 encryption for Azure File shares.</span></span>
* <span data-ttu-id="06561-144">[用戶端加密](../storage/common/storage-security-guide.md#using-client-side-encryption-to-secure-data-that-you-send-to-storage)，tooencrypt hello 資料在傳輸之前儲存和 toodecrypt hello 資料超出儲存體傳輸後。</span><span class="sxs-lookup"><span data-stu-id="06561-144">[Client-side encryption](../storage/common/storage-security-guide.md#using-client-side-encryption-to-secure-data-that-you-send-to-storage), tooencrypt hello data before it is transferred into storage and toodecrypt hello data after it is transferred out of storage.</span></span>

<span data-ttu-id="06561-145">深入了解用戶端加密︰</span><span class="sxs-lookup"><span data-stu-id="06561-145">Learn more about client-side encryption:</span></span>

* [<span data-ttu-id="06561-146">Microsoft Azure 儲存體的用戶端加密</span><span class="sxs-lookup"><span data-stu-id="06561-146">Client-Side Encryption for Microsoft Azure Storage</span></span>](https://blogs.msdn.microsoft.com/windowsazurestorage/2015/04/28/client-side-encryption-for-microsoft-azure-storage-preview/)
* [<span data-ttu-id="06561-147">雲端安全性控制項系列︰加密傳輸中的資料</span><span class="sxs-lookup"><span data-stu-id="06561-147">Cloud security controls series: Encrypting Data in Transit</span></span>](http://blogs.microsoft.com/cybertrust/2015/08/10/cloud-security-controls-series-encrypting-data-in-transit/)

## <a name="encryption-at-rest"></a><span data-ttu-id="06561-148">待用加密</span><span class="sxs-lookup"><span data-stu-id="06561-148">Encryption at rest</span></span>
<span data-ttu-id="06561-149">對許多組織來說， [待用資料加密](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) 是達到資料隱私性、法規遵循及資料主權的必要步驟。</span><span class="sxs-lookup"><span data-stu-id="06561-149">For many organizations, [data encryption at rest](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) is a mandatory step towards data privacy, compliance, and data sovereignty.</span></span> <span data-ttu-id="06561-150">有三個 Azure 功能可提供「待用」資料的加密。</span><span class="sxs-lookup"><span data-stu-id="06561-150">There are three Azure features that provide encryption of data that is “at rest”:</span></span>

* <span data-ttu-id="06561-151">[儲存體服務加密](../storage/common/storage-security-guide.md#encryption-at-rest)可讓您 toorequest 寫入它 tooAzure 儲存體時，hello 儲存體服務會自動加密資料。</span><span class="sxs-lookup"><span data-stu-id="06561-151">[Storage Service Encryption](../storage/common/storage-security-guide.md#encryption-at-rest) allows you toorequest that hello storage service automatically encrypt data when writing it tooAzure Storage.</span></span>
* <span data-ttu-id="06561-152">[用戶端加密](../storage/common/storage-security-guide.md#client-side-encryption)也提供的加密在靜止 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="06561-152">[Client-side Encryption](../storage/common/storage-security-guide.md#client-side-encryption) also provides hello feature of encryption at rest.</span></span>
* <span data-ttu-id="06561-153">[Azure 磁碟加密](../storage/common/storage-security-guide.md#using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines)可讓您 tooencrypt hello OS 磁碟和 IaaS 虛擬機器所使用的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="06561-153">[Azure Disk Encryption](../storage/common/storage-security-guide.md#using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) allows you tooencrypt hello OS disks and data disks used by an IaaS virtual machine.</span></span>

<span data-ttu-id="06561-154">深入了解儲存體服務加密：</span><span class="sxs-lookup"><span data-stu-id="06561-154">Learn more about Storage Service Encryption:</span></span>

* <span data-ttu-id="06561-155">[Azure 儲存體服務加密](https://azure.microsoft.com/services/storage/)適用於 [Azure Blob 儲存體](https://azure.microsoft.com/services/storage/blobs/)。</span><span class="sxs-lookup"><span data-stu-id="06561-155">[Azure Storage Service Encryption](https://azure.microsoft.com/services/storage/) is available for [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/).</span></span> <span data-ttu-id="06561-156">如需其他 Azure 儲存體類型的詳細資訊，請參閱[檔案](https://azure.microsoft.com/services/storage/files/)、[磁碟 (進階儲存體)](https://azure.microsoft.com/services/storage/premium-storage/)、[資料表](https://azure.microsoft.com/services/storage/tables/)和[佇列](https://azure.microsoft.com/services/storage/queues/)。</span><span class="sxs-lookup"><span data-stu-id="06561-156">For details on other Azure storage types, see [File](https://azure.microsoft.com/services/storage/files/), [Disk (Premium Storage)](https://azure.microsoft.com/services/storage/premium-storage/), [Table](https://azure.microsoft.com/services/storage/tables/), and [Queue](https://azure.microsoft.com/services/storage/queues/).</span></span>
* [<span data-ttu-id="06561-157">待用資料的 Azure 儲存體服務加密</span><span class="sxs-lookup"><span data-stu-id="06561-157">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

## <a name="azure-disk-encryption"></a><span data-ttu-id="06561-158">Azure 磁碟加密</span><span class="sxs-lookup"><span data-stu-id="06561-158">Azure Disk Encryption</span></span>
<span data-ttu-id="06561-159">適用於虛擬機器 (VM) 的 Azure 磁碟加密會使用您在 [Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/)所控制的金鑰與原則將 VM 磁碟 (包括開機和資料磁碟) 加密，協助您達成組織安全性與相容性需求。</span><span class="sxs-lookup"><span data-stu-id="06561-159">Azure Disk Encryption for virtual machines (VMs) helps you address organizational security and compliance requirements by encrypting your VM disks (including boot and data disks) with keys and policies you control in [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).</span></span>

<span data-ttu-id="06561-160">適用於 VM 的磁碟加密可用於 Linux 與 Windows 作業系統。</span><span class="sxs-lookup"><span data-stu-id="06561-160">Disk Encryption for VMs works for Linux and Windows operating systems.</span></span> <span data-ttu-id="06561-161">它也會使用金鑰保存庫 toohelp 保護、 管理及稽核磁碟加密金鑰的使用。</span><span class="sxs-lookup"><span data-stu-id="06561-161">It also uses Key Vault toohelp you safeguard, manage, and audit use of your disk encryption keys.</span></span> <span data-ttu-id="06561-162">VM 磁碟中的所有 hello 資料都加密待用使用業界標準加密技術在 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="06561-162">All hello data in your VM disks is encrypted at rest by using industry-standard encryption technology in your Azure Storage accounts.</span></span> <span data-ttu-id="06561-163">hello 適用於 Windows 的磁碟加密解決方案根據[Microsoft BitLocker 磁碟機加密](https://technet.microsoft.com/library/cc732774.aspx)，並且根據 hello Linux 方案[dm crypt](https://en.wikipedia.org/wiki/Dm-crypt)。</span><span class="sxs-lookup"><span data-stu-id="06561-163">hello Disk Encryption solution for Windows is based on [Microsoft BitLocker Drive Encryption](https://technet.microsoft.com/library/cc732774.aspx), and hello Linux solution is based on [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt).</span></span>

<span data-ttu-id="06561-164">深入了解：</span><span class="sxs-lookup"><span data-stu-id="06561-164">Learn more:</span></span>

* [<span data-ttu-id="06561-165">適用於 Windows 和 Linux IaaS 虛擬機器的 Azure 磁碟加密</span><span class="sxs-lookup"><span data-stu-id="06561-165">Azure Disk Encryption for Windows and Linux IaaS Virtual Machines</span></span>](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)

## <a name="azure-key-vault"></a><span data-ttu-id="06561-166">Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="06561-166">Azure Key Vault</span></span>
<span data-ttu-id="06561-167">Azure 磁碟加密使用[Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/)toohelp 您控制，和您金鑰保存庫的訂用帳戶，同時確保 hello 虛擬機器磁碟中的所有資料會都加密在靜止於 Azure 中管理磁碟加密金鑰和密碼儲存體。</span><span class="sxs-lookup"><span data-stu-id="06561-167">Azure Disk Encryption uses [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) toohelp you control and manage disk encryption keys and secrets in your key vault subscription, while ensuring that all data in hello virtual machine disks are encrypted at rest in your Azure Storage.</span></span> <span data-ttu-id="06561-168">您應該使用金鑰保存庫 tooaudit 金鑰和原則使用方式。</span><span class="sxs-lookup"><span data-stu-id="06561-168">You should use Key Vault tooaudit keys and policy usage.</span></span>

<span data-ttu-id="06561-169">深入了解：</span><span class="sxs-lookup"><span data-stu-id="06561-169">Learn more:</span></span>

* [<span data-ttu-id="06561-170">什麼是 Azure 金鑰保存庫？</span><span class="sxs-lookup"><span data-stu-id="06561-170">What is Azure Key Vault?</span></span>](../key-vault/key-vault-whatis.md)
* [<span data-ttu-id="06561-171">開始使用 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="06561-171">Get started with Azure Key Vault</span></span>](../key-vault/key-vault-get-started.md)
