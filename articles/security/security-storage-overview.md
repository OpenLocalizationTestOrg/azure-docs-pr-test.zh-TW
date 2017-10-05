---
title: "可用於 Azure 儲存體的安全性功能 | Microsoft Docs"
description: " 本文提供可用於 Azure 儲存體的核心 Azure 安全性功能概觀。 "
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
ms.openlocfilehash: da28cbf5f6f91df1f89114a63bc3f2ebac0f6d73
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-security-overview"></a><span data-ttu-id="6f34f-103">Azure 儲存體安全性概觀</span><span class="sxs-lookup"><span data-stu-id="6f34f-103">Azure storage security overview</span></span>
<span data-ttu-id="6f34f-104">Azure 儲存體是現代應用程式的雲端儲存體解決方案，這些應用程式仰賴持續性、可用性和可調整性來滿足其客戶的需求。</span><span class="sxs-lookup"><span data-stu-id="6f34f-104">Azure Storage is the cloud storage solution for modern applications that rely on durability, availability, and scalability to meet the needs of their customers.</span></span> <span data-ttu-id="6f34f-105">Azure 儲存體提供一組完整的安全性功能：</span><span class="sxs-lookup"><span data-stu-id="6f34f-105">Azure Storage provides a comprehensive set of security capabilities:</span></span>

* <span data-ttu-id="6f34f-106">您可以使用角色型存取控制與 Azure Active Directory 來保護儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6f34f-106">The storage account can be secured using Role-Based Access Control and Azure Active Directory.</span></span>
* <span data-ttu-id="6f34f-107">您可以使用用戶端加密、HTTP 或 SMB 3.0，在應用程式和 Azure 之間進行傳輸時保護資料的安全。</span><span class="sxs-lookup"><span data-stu-id="6f34f-107">Data can be secured in transit between an application and Azure by using Client-Side Encryption, HTTPS, or SMB 3.0.</span></span>
* <span data-ttu-id="6f34f-108">使用儲存體服務加密寫入 Azure 儲存體時，可將資料設定為自動加密。</span><span class="sxs-lookup"><span data-stu-id="6f34f-108">Data can be set to be automatically encrypted when written to Azure Storage using Storage Service Encryption.</span></span>
* <span data-ttu-id="6f34f-109">您可以使用 Azure 磁碟加密，將虛擬機器所使用的作業系統和資料磁碟設定為加密。</span><span class="sxs-lookup"><span data-stu-id="6f34f-109">OS and Data disks used by virtual machines can be set to be encrypted using Azure Disk Encryption.</span></span>
* <span data-ttu-id="6f34f-110">Azure 儲存體中資料物件的委派存取權可以使用「共用存取簽章」來授與。</span><span class="sxs-lookup"><span data-stu-id="6f34f-110">Delegated access to the data objects in Azure Storage can be granted using Shared Access Signatures.</span></span>
* <span data-ttu-id="6f34f-111">可以使用儲存體分析來追蹤某人存取儲存體時所使用的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="6f34f-111">The authentication method used by someone when they access storage can be tracked using Storage analytics.</span></span>

<span data-ttu-id="6f34f-112">若要深入了解「Azure 儲存體」中的安全性，請參閱 [Azure 儲存體安全性指南](../storage/common/storage-security-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="6f34f-112">For a more detailed look at security in Azure Storage, see the [Azure Storage security guide](../storage/common/storage-security-guide.md).</span></span> <span data-ttu-id="6f34f-113">本指南深入探討 Azure 儲存體的安全性功能，例如儲存體帳戶金鑰、傳輸中資料和待用資料的加密，以及儲存體分析。</span><span class="sxs-lookup"><span data-stu-id="6f34f-113">This guide provides a deep dive into the security features of Azure Storage such as storage account keys, data encryption in transit and at rest, and storage analytics.</span></span>

<span data-ttu-id="6f34f-114">本文提供可與「Azure 儲存體」搭配使用的 Azure 安全性功能概觀。</span><span class="sxs-lookup"><span data-stu-id="6f34f-114">This article provides an overview of Azure security features that can be used with Azure Storage.</span></span> <span data-ttu-id="6f34f-115">針對提供每項功能詳細資料的文章都提供了連結，以讓您深入了解。</span><span class="sxs-lookup"><span data-stu-id="6f34f-115">Links are provided to articles that give details of each feature so you can learn more.</span></span>

<span data-ttu-id="6f34f-116">以下是本文所涵蓋的核心功能：</span><span class="sxs-lookup"><span data-stu-id="6f34f-116">Here are the core features to be covered in this article:</span></span>

* <span data-ttu-id="6f34f-117">角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="6f34f-117">Role-Based Access Control</span></span>
* <span data-ttu-id="6f34f-118">儲存體物件的委派存取權</span><span class="sxs-lookup"><span data-stu-id="6f34f-118">Delegated access to storage objects</span></span>
* <span data-ttu-id="6f34f-119">傳輸中加密</span><span class="sxs-lookup"><span data-stu-id="6f34f-119">Encryption in transit</span></span>
* <span data-ttu-id="6f34f-120">待用加密/儲存體服務加密</span><span class="sxs-lookup"><span data-stu-id="6f34f-120">Encryption at rest/Storage Service Encryption</span></span>
* <span data-ttu-id="6f34f-121">Azure 磁碟加密</span><span class="sxs-lookup"><span data-stu-id="6f34f-121">Azure Disk Encryption</span></span>
* <span data-ttu-id="6f34f-122">Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="6f34f-122">Azure Key Vault</span></span>

## <a name="role-based-access-control-rbac"></a><span data-ttu-id="6f34f-123">角色型存取控制 (RBAC)</span><span class="sxs-lookup"><span data-stu-id="6f34f-123">Role-Based Access Control (RBAC)</span></span>
<span data-ttu-id="6f34f-124">您可以使用角色型存取控制 (RBAC) 來保護儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6f34f-124">You can secure your storage account with Role-Based Access Control (RBAC).</span></span> <span data-ttu-id="6f34f-125">對於想要強制執行資料存取安全性原則的組織，根據[需要知道](https://en.wikipedia.org/wiki/Need_to_know)和[最低權限](https://en.wikipedia.org/wiki/Principle_of_least_privilege)安全性原則限制存取權限是必須做的事。</span><span class="sxs-lookup"><span data-stu-id="6f34f-125">Restricting access based on the [need to know](https://en.wikipedia.org/wiki/Need_to_know) and [least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) security principles is imperative for organizations that want to enforce security policies for data access.</span></span> <span data-ttu-id="6f34f-126">在特定範圍將適當的 RBAC 角色指派給群組和應用程式，即可授與這些存取權限。</span><span class="sxs-lookup"><span data-stu-id="6f34f-126">These access rights are granted by assigning the appropriate RBAC role to groups and applications at a certain scope.</span></span> <span data-ttu-id="6f34f-127">您可以使用 [內建的 RBAC 角色](../active-directory/role-based-access-built-in-roles.md)(例如儲存體帳戶參與者) 將權限指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="6f34f-127">You can use [built-in RBAC roles](../active-directory/role-based-access-built-in-roles.md), such as Storage Account Contributor, to assign privileges to users.</span></span>

<span data-ttu-id="6f34f-128">深入了解：</span><span class="sxs-lookup"><span data-stu-id="6f34f-128">Learn more:</span></span>

* [<span data-ttu-id="6f34f-129">Azure Active Directory 角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="6f34f-129">Azure Active Directory Role-based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="delegated-access-to-storage-objects"></a><span data-ttu-id="6f34f-130">儲存體物件的委派存取權</span><span class="sxs-lookup"><span data-stu-id="6f34f-130">Delegated access to storage objects</span></span>
<span data-ttu-id="6f34f-131">共用存取簽章 (SAS) 可提供您儲存體帳戶中資源的委派存取。</span><span class="sxs-lookup"><span data-stu-id="6f34f-131">A shared access signature (SAS) provides delegated access to resources in your storage account.</span></span> <span data-ttu-id="6f34f-132">SAS 意謂著您可以將儲存體帳戶中物件的有限權限授與用戶端，讓該用戶端可以在一段指定的時間內使用一組指定的權限來進行存取。</span><span class="sxs-lookup"><span data-stu-id="6f34f-132">The SAS means that you can grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions.</span></span> <span data-ttu-id="6f34f-133">您可以在不須分享您帳戶存取金鑰的情況下，授與這些有限的權限。</span><span class="sxs-lookup"><span data-stu-id="6f34f-133">You can grant these limited permissions without having to share your account access keys.</span></span> <span data-ttu-id="6f34f-134">SAS 是一種 URI，此 URI 會在其查詢參數中包含對儲存體資源進行驗證式存取所需的一切資訊。</span><span class="sxs-lookup"><span data-stu-id="6f34f-134">The SAS is a URI that encompasses in its query parameters all the information necessary for authenticated access to a storage resource.</span></span> <span data-ttu-id="6f34f-135">若要使用 SAS 存取儲存體資源，用戶端只需將 SAS 提供給適當的建構函式或方法即可。</span><span class="sxs-lookup"><span data-stu-id="6f34f-135">To access storage resources with the SAS, the client only needs to provide the SAS to the appropriate constructor or method.</span></span>

<span data-ttu-id="6f34f-136">深入了解：</span><span class="sxs-lookup"><span data-stu-id="6f34f-136">Learn more:</span></span>

* [<span data-ttu-id="6f34f-137">了解 SAS 模型</span><span class="sxs-lookup"><span data-stu-id="6f34f-137">Understanding the SAS model</span></span>](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="6f34f-138">透過 Blob 儲存體來建立與使用 SAS</span><span class="sxs-lookup"><span data-stu-id="6f34f-138">Create and use a SAS with Blob storage</span></span>](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)

## <a name="encryption-in-transit"></a><span data-ttu-id="6f34f-139">傳輸中加密</span><span class="sxs-lookup"><span data-stu-id="6f34f-139">Encryption in transit</span></span>
<span data-ttu-id="6f34f-140">傳輸中加密是透過網路傳輸資料時用來保護資料的機制。</span><span class="sxs-lookup"><span data-stu-id="6f34f-140">Encryption in transit is a mechanism of protecting data when it is transmitted across networks.</span></span> <span data-ttu-id="6f34f-141">使用 Azure 儲存體，您可以使用下列各向來保護資料︰</span><span class="sxs-lookup"><span data-stu-id="6f34f-141">With Azure Storage you can secure data using:</span></span>

* <span data-ttu-id="6f34f-142">[傳輸層級加密](../storage/common/storage-security-guide.md#encryption-in-transit)，例如從 Azure 儲存體傳入或傳出資料時的 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="6f34f-142">[Transport-level encryption](../storage/common/storage-security-guide.md#encryption-in-transit), such as HTTPS when you transfer data into or out of Azure Storage.</span></span>
* <span data-ttu-id="6f34f-143">[連線加密](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares)，例如 Azure 檔案共用的 SMB 3.0 加密。</span><span class="sxs-lookup"><span data-stu-id="6f34f-143">[Wire encryption](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), such as SMB 3.0 encryption for Azure File shares.</span></span>
* <span data-ttu-id="6f34f-144">[用戶端加密](../storage/common/storage-security-guide.md#using-client-side-encryption-to-secure-data-that-you-send-to-storage)，以在將資料傳輸至儲存體之前加密資料，以及自儲存體傳出後解密資料。</span><span class="sxs-lookup"><span data-stu-id="6f34f-144">[Client-side encryption](../storage/common/storage-security-guide.md#using-client-side-encryption-to-secure-data-that-you-send-to-storage), to encrypt the data before it is transferred into storage and to decrypt the data after it is transferred out of storage.</span></span>

<span data-ttu-id="6f34f-145">深入了解用戶端加密︰</span><span class="sxs-lookup"><span data-stu-id="6f34f-145">Learn more about client-side encryption:</span></span>

* [<span data-ttu-id="6f34f-146">Microsoft Azure 儲存體的用戶端加密</span><span class="sxs-lookup"><span data-stu-id="6f34f-146">Client-Side Encryption for Microsoft Azure Storage</span></span>](https://blogs.msdn.microsoft.com/windowsazurestorage/2015/04/28/client-side-encryption-for-microsoft-azure-storage-preview/)
* [<span data-ttu-id="6f34f-147">雲端安全性控制項系列︰加密傳輸中的資料</span><span class="sxs-lookup"><span data-stu-id="6f34f-147">Cloud security controls series: Encrypting Data in Transit</span></span>](http://blogs.microsoft.com/cybertrust/2015/08/10/cloud-security-controls-series-encrypting-data-in-transit/)

## <a name="encryption-at-rest"></a><span data-ttu-id="6f34f-148">待用加密</span><span class="sxs-lookup"><span data-stu-id="6f34f-148">Encryption at rest</span></span>
<span data-ttu-id="6f34f-149">對許多組織來說， [待用資料加密](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) 是達到資料隱私性、法規遵循及資料主權的必要步驟。</span><span class="sxs-lookup"><span data-stu-id="6f34f-149">For many organizations, [data encryption at rest](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) is a mandatory step towards data privacy, compliance, and data sovereignty.</span></span> <span data-ttu-id="6f34f-150">有三個 Azure 功能可提供「待用」資料的加密。</span><span class="sxs-lookup"><span data-stu-id="6f34f-150">There are three Azure features that provide encryption of data that is “at rest”:</span></span>

* <span data-ttu-id="6f34f-151">[儲存體服務加密](../storage/common/storage-security-guide.md#encryption-at-rest) 可讓您要求儲存體服務在將資料寫入 Azure 儲存體時自動加密資料。</span><span class="sxs-lookup"><span data-stu-id="6f34f-151">[Storage Service Encryption](../storage/common/storage-security-guide.md#encryption-at-rest) allows you to request that the storage service automatically encrypt data when writing it to Azure Storage.</span></span>
* <span data-ttu-id="6f34f-152">[用戶端加密](../storage/common/storage-security-guide.md#client-side-encryption) 也會提供待用加密的功能。</span><span class="sxs-lookup"><span data-stu-id="6f34f-152">[Client-side Encryption](../storage/common/storage-security-guide.md#client-side-encryption) also provides the feature of encryption at rest.</span></span>
* <span data-ttu-id="6f34f-153">[Azure 磁碟加密](../storage/common/storage-security-guide.md#using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) 允許您加密 IaaS 虛擬機器所使用的作業系統磁碟和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="6f34f-153">[Azure Disk Encryption](../storage/common/storage-security-guide.md#using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) allows you to encrypt the OS disks and data disks used by an IaaS virtual machine.</span></span>

<span data-ttu-id="6f34f-154">深入了解儲存體服務加密：</span><span class="sxs-lookup"><span data-stu-id="6f34f-154">Learn more about Storage Service Encryption:</span></span>

* <span data-ttu-id="6f34f-155">[Azure 儲存體服務加密](https://azure.microsoft.com/services/storage/)適用於 [Azure Blob 儲存體](https://azure.microsoft.com/services/storage/blobs/)。</span><span class="sxs-lookup"><span data-stu-id="6f34f-155">[Azure Storage Service Encryption](https://azure.microsoft.com/services/storage/) is available for [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/).</span></span> <span data-ttu-id="6f34f-156">如需其他 Azure 儲存體類型的詳細資訊，請參閱[檔案](https://azure.microsoft.com/services/storage/files/)、[磁碟 (進階儲存體)](https://azure.microsoft.com/services/storage/premium-storage/)、[資料表](https://azure.microsoft.com/services/storage/tables/)和[佇列](https://azure.microsoft.com/services/storage/queues/)。</span><span class="sxs-lookup"><span data-stu-id="6f34f-156">For details on other Azure storage types, see [File](https://azure.microsoft.com/services/storage/files/), [Disk (Premium Storage)](https://azure.microsoft.com/services/storage/premium-storage/), [Table](https://azure.microsoft.com/services/storage/tables/), and [Queue](https://azure.microsoft.com/services/storage/queues/).</span></span>
* [<span data-ttu-id="6f34f-157">待用資料的 Azure 儲存體服務加密</span><span class="sxs-lookup"><span data-stu-id="6f34f-157">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

## <a name="azure-disk-encryption"></a><span data-ttu-id="6f34f-158">Azure 磁碟加密</span><span class="sxs-lookup"><span data-stu-id="6f34f-158">Azure Disk Encryption</span></span>
<span data-ttu-id="6f34f-159">適用於虛擬機器 (VM) 的 Azure 磁碟加密會使用您在 [Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/)所控制的金鑰與原則將 VM 磁碟 (包括開機和資料磁碟) 加密，協助您達成組織安全性與相容性需求。</span><span class="sxs-lookup"><span data-stu-id="6f34f-159">Azure Disk Encryption for virtual machines (VMs) helps you address organizational security and compliance requirements by encrypting your VM disks (including boot and data disks) with keys and policies you control in [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).</span></span>

<span data-ttu-id="6f34f-160">適用於 VM 的磁碟加密可用於 Linux 與 Windows 作業系統。</span><span class="sxs-lookup"><span data-stu-id="6f34f-160">Disk Encryption for VMs works for Linux and Windows operating systems.</span></span> <span data-ttu-id="6f34f-161">也會使用金鑰保存庫，協助您防護、管理和稽核您的磁碟加密金鑰的使用情形。</span><span class="sxs-lookup"><span data-stu-id="6f34f-161">It also uses Key Vault to help you safeguard, manage, and audit use of your disk encryption keys.</span></span> <span data-ttu-id="6f34f-162">VM 磁碟中的所有資料皆在待用時，透過 Azure 儲存體帳戶中符合業界標準的加密技術進行加密。</span><span class="sxs-lookup"><span data-stu-id="6f34f-162">All the data in your VM disks is encrypted at rest by using industry-standard encryption technology in your Azure Storage accounts.</span></span> <span data-ttu-id="6f34f-163">Windows 的磁碟加密解決方案是建基於 [Microsoft BitLocker 磁碟機加密](https://technet.microsoft.com/library/cc732774.aspx)，而 Linux 解決方案是建基於 [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt)。</span><span class="sxs-lookup"><span data-stu-id="6f34f-163">The Disk Encryption solution for Windows is based on [Microsoft BitLocker Drive Encryption](https://technet.microsoft.com/library/cc732774.aspx), and the Linux solution is based on [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt).</span></span>

<span data-ttu-id="6f34f-164">深入了解：</span><span class="sxs-lookup"><span data-stu-id="6f34f-164">Learn more:</span></span>

* [<span data-ttu-id="6f34f-165">適用於 Windows 和 Linux IaaS 虛擬機器的 Azure 磁碟加密</span><span class="sxs-lookup"><span data-stu-id="6f34f-165">Azure Disk Encryption for Windows and Linux IaaS Virtual Machines</span></span>](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)

## <a name="azure-key-vault"></a><span data-ttu-id="6f34f-166">Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="6f34f-166">Azure Key Vault</span></span>
<span data-ttu-id="6f34f-167">「Azure 磁碟加密」會使用 [Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/) ，既幫助您控制和管理您的金鑰保存庫訂用帳戶中的磁碟加密金鑰和密碼，同時也確保虛擬機器磁碟中的所有資料在您「Azure 儲存體」中待用時會受到加密。</span><span class="sxs-lookup"><span data-stu-id="6f34f-167">Azure Disk Encryption uses [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) to help you control and manage disk encryption keys and secrets in your key vault subscription, while ensuring that all data in the virtual machine disks are encrypted at rest in your Azure Storage.</span></span> <span data-ttu-id="6f34f-168">您應使用金鑰保存庫來稽核金鑰和原則使用方式。</span><span class="sxs-lookup"><span data-stu-id="6f34f-168">You should use Key Vault to audit keys and policy usage.</span></span>

<span data-ttu-id="6f34f-169">深入了解：</span><span class="sxs-lookup"><span data-stu-id="6f34f-169">Learn more:</span></span>

* [<span data-ttu-id="6f34f-170">什麼是 Azure 金鑰保存庫？</span><span class="sxs-lookup"><span data-stu-id="6f34f-170">What is Azure Key Vault?</span></span>](../key-vault/key-vault-whatis.md)
* [<span data-ttu-id="6f34f-171">開始使用 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="6f34f-171">Get started with Azure Key Vault</span></span>](../key-vault/key-vault-get-started.md)
