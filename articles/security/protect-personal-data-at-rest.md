---
title: "Azure 的保護個人資料使用加密待用 |Microsoft 文件"
description: "這篇文章是可幫助您使用 Azure 來保護個人資料的一系列的一部分"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: d0ef3ca8d48f5ba11a89c787ff59df39eeaf673b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a><span data-ttu-id="f7d44-103">Azure 加密技術：使用加密保護個人待用資料</span><span class="sxs-lookup"><span data-stu-id="f7d44-103">Azure encryption technologies: Protect personal data at rest with encryption</span></span>

<span data-ttu-id="f7d44-104">本文可協助您了解及使用 Azure 加密技術來保護待用資料。</span><span class="sxs-lookup"><span data-stu-id="f7d44-104">This article helps you understand and use Azure encryption technologies to secure data at rest.</span></span>

<span data-ttu-id="f7d44-105">待用資料加密是保護敏感性或個人資料，以及符合合規性和資料隱私權需求之最佳做法不可或缺的一部分。</span><span class="sxs-lookup"><span data-stu-id="f7d44-105">Encryption of data at rest is essential as a best practice to protect sensitive or personal data and to meet compliance and data privacy requirements.</span></span>
<span data-ttu-id="f7d44-106">靜態加密旨在防止攻擊者存取未加密的資料，方法是確保資料在磁碟上時就已加密。</span><span class="sxs-lookup"><span data-stu-id="f7d44-106">Encryption at rest is designed to prevent the attacker from accessing the unencrypted data by ensuring the data is encrypted when on disk.</span></span>

## <a name="scenario"></a><span data-ttu-id="f7d44-107">案例</span><span class="sxs-lookup"><span data-stu-id="f7d44-107">Scenario</span></span> 

<span data-ttu-id="f7d44-108">總部設於美國的大型郵輪公司將擴展其營運，以提供地中海、波羅的海和不列顛群島的行程。</span><span class="sxs-lookup"><span data-stu-id="f7d44-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="f7d44-109">為了支援這些工作，它收購了以義大利、德國、丹麥和英國為據點的數個較小型郵輪公司。</span><span class="sxs-lookup"><span data-stu-id="f7d44-109">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and the U.K.</span></span>

<span data-ttu-id="f7d44-110">此公司使用 Microsoft Azure 在雲端儲存公司資料。</span><span class="sxs-lookup"><span data-stu-id="f7d44-110">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="f7d44-111">這可能包括員工及/或客戶資訊，例如：</span><span class="sxs-lookup"><span data-stu-id="f7d44-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="f7d44-112">地址</span><span class="sxs-lookup"><span data-stu-id="f7d44-112">addresses</span></span>
- <span data-ttu-id="f7d44-113">電話號碼</span><span class="sxs-lookup"><span data-stu-id="f7d44-113">phone numbers</span></span>
- <span data-ttu-id="f7d44-114">稅務識別編號</span><span class="sxs-lookup"><span data-stu-id="f7d44-114">tax identification numbers</span></span>
- <span data-ttu-id="f7d44-115">醫療資訊</span><span class="sxs-lookup"><span data-stu-id="f7d44-115">medical information</span></span>
- <span data-ttu-id="f7d44-116">信用卡資訊</span><span class="sxs-lookup"><span data-stu-id="f7d44-116">credit card information</span></span>

<span data-ttu-id="f7d44-117">公司必須保護員工和客戶資料的隱私權，同時可讓資料存取需要這些部門。</span><span class="sxs-lookup"><span data-stu-id="f7d44-117">The company must protect the privacy of employee and customer data while making data accessible to those departments that need it.</span></span> <span data-ttu-id="f7d44-118">(例如薪資部門和訂位部門) 可以存取資料。</span><span class="sxs-lookup"><span data-stu-id="f7d44-118">(such as payroll and reservations departments)</span></span>

<span data-ttu-id="f7d44-119">此郵輪公司也會維護獎勵和忠誠度方案會員的大型資料庫，其中包含的個人資訊可追蹤與目前和過去客戶的關係。</span><span class="sxs-lookup"><span data-stu-id="f7d44-119">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

### <a name="problem-statement"></a><span data-ttu-id="f7d44-120">問題陳述</span><span class="sxs-lookup"><span data-stu-id="f7d44-120">Problem statement</span></span>

<span data-ttu-id="f7d44-121">公司必須保護員工和客戶的個人資料的隱私權，同時可讓資料存取需要它 （例如，薪資和保留項目的部門） 這些部門。</span><span class="sxs-lookup"><span data-stu-id="f7d44-121">The company must protect the privacy of employees’ and customers’ personal data while making data accessible to those departments that need it (such as payroll and reservations departments).</span></span> <span data-ttu-id="f7d44-122">此個人資料儲存在公司控制的資料中心外部，因此不受公司的實體控制。</span><span class="sxs-lookup"><span data-stu-id="f7d44-122">This personal data is stored outside of the corporate-controlled data center and is not under the company’s physical control.</span></span>

### <a name="company-goal"></a><span data-ttu-id="f7d44-123">公司目標</span><span class="sxs-lookup"><span data-stu-id="f7d44-123">Company goal</span></span>

<span data-ttu-id="f7d44-124">作為多層深度防禦安全性策略的一部分，公司目標是確保包含個人資料的所有資料來源都經過加密，包括位於雲端儲存體的資料來源。</span><span class="sxs-lookup"><span data-stu-id="f7d44-124">As part of a multi-layered defense-in-depth security strategy, it is a company goal to ensure that all data sources that contain personal data are encrypted, including those residing in cloud storage.</span></span> <span data-ttu-id="f7d44-125">如有未經授權的人員取得個人資料的存取權，必須採用讓資料變得無法讀取的格式。</span><span class="sxs-lookup"><span data-stu-id="f7d44-125">If unauthorized persons gain access to the personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="f7d44-126">對於使用者和系統管理員而言，套用加密應該很容易或很透明。</span><span class="sxs-lookup"><span data-stu-id="f7d44-126">Applying encryption should be easy, or transparent – for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="f7d44-127">解決方案</span><span class="sxs-lookup"><span data-stu-id="f7d44-127">Solutions</span></span>

<span data-ttu-id="f7d44-128">Azure 服務提供多種工具和技術，可協助您透過加密來保護個人待用資料。</span><span class="sxs-lookup"><span data-stu-id="f7d44-128">Azure services provide multiple tools and technologies to help you protect personal data at rest by encrypting it.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="f7d44-129">Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f7d44-129">Azure Key Vault</span></span>

<span data-ttu-id="f7d44-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) 為用來加密 Azure 服務中待用資料的金鑰提供安全存放裝置，是建議的金鑰儲存和管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="f7d44-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) provides secure storage for the keys used to encrypt data at rest in Azure services and is the recommended key storage and management solution.</span></span> <span data-ttu-id="f7d44-131">加密金鑰管理對保護儲存的資料很重要。</span><span class="sxs-lookup"><span data-stu-id="f7d44-131">Encryption key management is essential to securing stored data.</span></span>

#### <a name="how-do-i-use-azure-key-vault-to-protect-keys-that-encrypt-personal-data"></a><span data-ttu-id="f7d44-132">如何使用 Azure Key Vault 來保護加密個人資料的金鑰？</span><span class="sxs-lookup"><span data-stu-id="f7d44-132">How do I use Azure Key Vault to protect keys that encrypt personal data?</span></span>

<span data-ttu-id="f7d44-133">若要使用 Azure Key Vault，您需要 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f7d44-133">To use Azure Key Vault, you need a subscription to an Azure account.</span></span> <span data-ttu-id="f7d44-134">您也需要安裝 Azure Powershell。</span><span class="sxs-lookup"><span data-stu-id="f7d44-134">You also need Azure PowerShell installed.</span></span> <span data-ttu-id="f7d44-135">其步驟包括使用 PowerShell Cmdlet 來執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="f7d44-135">Steps include using PowerShell cmdlets to do the following:</span></span>

1. <span data-ttu-id="f7d44-136">連線到您的訂閱</span><span class="sxs-lookup"><span data-stu-id="f7d44-136">Connect to your subscriptions</span></span>

2. <span data-ttu-id="f7d44-137">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f7d44-137">Create a key vault</span></span>

3. <span data-ttu-id="f7d44-138">將金鑰或密碼加入至金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f7d44-138">Add a key or secret to the key vault</span></span>

4. <span data-ttu-id="f7d44-139">利用 Azure Active Directory 註冊將會使用金鑰保存庫的應用程式</span><span class="sxs-lookup"><span data-stu-id="f7d44-139">Register applications that will use the key vault with Azure Active Directory</span></span>

5. <span data-ttu-id="f7d44-140">授權應用程式使用金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="f7d44-140">Authorize the applications to use the key or secret</span></span>

<span data-ttu-id="f7d44-141">若要建立金鑰保存庫，請使用 New-AzureRmKeyVault PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f7d44-141">To create a key vault, use the New-AzureRmKeyVault PowerShell CmDlt.</span></span> <span data-ttu-id="f7d44-142">您將會指派保存庫名稱、資源群組名稱和地理位置。</span><span class="sxs-lookup"><span data-stu-id="f7d44-142">You will assign a vault name, resource group name, and geographic location.</span></span> <span data-ttu-id="f7d44-143">當您透過其他 Cmdlet 管理金鑰時，您將會使用保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="f7d44-143">You’ll use the vault name when managing keys via other Cmdlets.</span></span> <span data-ttu-id="f7d44-144">透過 REST API 使用保存庫的應用程式將會使用保存庫 URI。</span><span class="sxs-lookup"><span data-stu-id="f7d44-144">Applications that use the vault through the REST API will use the vault URI.</span></span>

<span data-ttu-id="f7d44-145">Azure Key Vault 可為您提供受軟體保護的金鑰；或者，您也可以匯入 .PFX 檔案中的現有金鑰。</span><span class="sxs-lookup"><span data-stu-id="f7d44-145">Azure Key Vault can provide a software-protected key for you, or you can import an existing key in a .PFX file.</span></span> <span data-ttu-id="f7d44-146">您也可以在保存庫中儲存密碼。</span><span class="sxs-lookup"><span data-stu-id="f7d44-146">You can also store secrets (passwords) in the vault.</span></span>

<span data-ttu-id="f7d44-147">您也可以在本機 HSM 中產生金鑰，且在金鑰無需離開 HSM 界限的情況下，即可將它傳輸到 Key Vault 服務中的 HSM。</span><span class="sxs-lookup"><span data-stu-id="f7d44-147">You can also generate a key in your local HSM and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary.</span></span>

<span data-ttu-id="f7d44-148">如需使用 Azure Key Vault 的詳細指示，請遵循[開始使用 Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started) 中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="f7d44-148">For detailed instructions on using Azure Key Vault, follow the steps in [Get Started with Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span></span>

<span data-ttu-id="f7d44-149">如需搭配 Azure Key Vault 使用的 PowerShell Cmdlet 清單，請參閱 [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0)。</span><span class="sxs-lookup"><span data-stu-id="f7d44-149">For a list of PowerShell Cmdlets used with Azure Key Vault, see [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

### <a name="azure-disk-encryption-for-windows"></a><span data-ttu-id="f7d44-150">Windows 適用的 Azure 磁碟加密</span><span class="sxs-lookup"><span data-stu-id="f7d44-150">Azure Disk Encryption for Windows</span></span>

<span data-ttu-id="f7d44-151">[Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)會保護 Azure 虛擬機器上的個人待用資料，並與 Azure Key Vault 整合。</span><span class="sxs-lookup"><span data-stu-id="f7d44-151">[Azure Disk Encryption for Windows and Linux IaaS VMs](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protects personal data at rest on Azure virtual machines and integrates with Azure Key Vault.</span></span> <span data-ttu-id="f7d44-152">Azure 磁碟加密使用 [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) (在 Windows 中) 及 [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) (在 Linux 中) 來加密 OS 和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="f7d44-152">Azure Disk Encryption uses [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows and [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux to encrypt both the OS and the data disks.</span></span> <span data-ttu-id="f7d44-153">Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016 以及 Windows 8 和 Windows 10 用戶端支援 Azure 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="f7d44-153">Azure Disk Encryption is supported on Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, and on Windows 8 and Windows 10 clients.</span></span>

#### <a name="how-do-i-use-azure-disk-encryption-to-protect-personal-data"></a><span data-ttu-id="f7d44-154">如何使用 Azure 磁碟加密來保護個人資料？</span><span class="sxs-lookup"><span data-stu-id="f7d44-154">How do I use Azure Disk Encryption to protect personal data?</span></span>

<span data-ttu-id="f7d44-155">若要使用 Azure 磁碟加密，您需要 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f7d44-155">To use Azure Disk Encryption, you need a subscription to an Azure account.</span></span> <span data-ttu-id="f7d44-156">若要啟用 Windows 和 Linux VM 適用的 Azure 磁碟加密，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="f7d44-156">To enable Azure Disk Encryption for Windows and Linux VMs, do the following:</span></span>

1. <span data-ttu-id="f7d44-157">使用 Azure 磁碟加密 Resource Manager 範本、PowerShell 或命令列介面 (CLI) 啟用磁碟加密，並指定加密設定。</span><span class="sxs-lookup"><span data-stu-id="f7d44-157">Use the Azure Disk Encryption Resource Manager template, PowerShell, or the command line interface (CLI) to enable disk encryption and specify the  encryption configuration.</span></span> 

2. <span data-ttu-id="f7d44-158">授與 Azure 平台的存取權，以從金鑰保存庫讀取加密資料。</span><span class="sxs-lookup"><span data-stu-id="f7d44-158">Grant access to the Azure platform to read the encryption material from your key vault.</span></span>

3. <span data-ttu-id="f7d44-159">提供 Azure Active Directory (AAD) 應用程式識別碼，以將加密金鑰資料寫入至金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="f7d44-159">Provide an Azure Active Directory (AAD) application identity to write the encryption key material to your key vault.</span></span>

<span data-ttu-id="f7d44-160">Azure 將會更新 VM 和金鑰保存庫設定，並設定加密的 VM。</span><span class="sxs-lookup"><span data-stu-id="f7d44-160">Azure will update the VM and the key vault configuration, and set up your encrypted VM.</span></span>

<span data-ttu-id="f7d44-161">當您設定金鑰保存庫以支援 Azure 磁碟加密時，您可以新增金鑰加密金鑰 (KEK)，以提高安全性並支援備份加密的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f7d44-161">When you set up your key vault to support Azure Disk Encryption, you can add a key encryption key (KEK) for added security and to support backup of encrypted virtual machines.</span></span>

![](media/protect-personal-data-at-rest/create-key.png)

<span data-ttu-id="f7d44-162">如需特定部署案例和使用者體驗的詳細指示，請參閱 [Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)。</span><span class="sxs-lookup"><span data-stu-id="f7d44-162">Detailed instructions for specific deployment scenarios and user experiences are included in [Azure Disk Encryption for Windows and Linux IaaS VMs.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span></span>

### <a name="azure-storage-service-encryption"></a><span data-ttu-id="f7d44-163">Azure 儲存體服務加密</span><span class="sxs-lookup"><span data-stu-id="f7d44-163">Azure Storage Service Encryption</span></span>

<span data-ttu-id="f7d44-164">[Azure Storage Service Encryption (SSE) for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) (待用資料的 Azure 儲存體服務加密 (SSE)) 會協助您保護資料安全，以符合組織安全性和合規性承諾。</span><span class="sxs-lookup"><span data-stu-id="f7d44-164">[Azure Storage Service Encryption (SSE) for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helps you protect and safeguard your data to meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="f7d44-165">Azure 儲存體會先自動使用 256 位元 AES 加密來加密資料，再保存到儲存體，以及在擷取之前將它解密。</span><span class="sxs-lookup"><span data-stu-id="f7d44-165">Azure Storage automatically encrypts your data using 256-bit AES encryption prior to persisting to storage, and decrypts it prior to retrieval.</span></span> <span data-ttu-id="f7d44-166">這個服務適用於 Azure Blob 和檔案。</span><span class="sxs-lookup"><span data-stu-id="f7d44-166">This service is available for Azure Blobs and Files.</span></span>

#### <a name="how-do-i-use-storage-service-encryption-to-protect-personal-data"></a><span data-ttu-id="f7d44-167">如何使用儲存體服務加密來保護個人資料？</span><span class="sxs-lookup"><span data-stu-id="f7d44-167">How do I use Storage Service Encryption to protect personal data?</span></span>

<span data-ttu-id="f7d44-168">若要啟用儲存體服務加密，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="f7d44-168">To enable Storage Service Encryption, do the following:</span></span>

1. <span data-ttu-id="f7d44-169">登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f7d44-169">Log into the Azure portal.</span></span>

2. <span data-ttu-id="f7d44-170">選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f7d44-170">Select a storage account.</span></span>

3. <span data-ttu-id="f7d44-171">在 [設定] 的 [Blob 服務] 區段下，選取 [加密]。</span><span class="sxs-lookup"><span data-stu-id="f7d44-171">In Settings, under the Blob Service section, select Encryption.</span></span>

4. <span data-ttu-id="f7d44-172">在 [檔案服務] 區段下，選取 [加密]。</span><span class="sxs-lookup"><span data-stu-id="f7d44-172">Under the File Service section, select Encryption.</span></span>

<span data-ttu-id="f7d44-173">按一下 [加密] 設定之後，您可以啟用或停用「儲存體服務加密」。</span><span class="sxs-lookup"><span data-stu-id="f7d44-173">After you click the Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

<span data-ttu-id="f7d44-174">新的資料將會加密。</span><span class="sxs-lookup"><span data-stu-id="f7d44-174">New data will be encrypted.</span></span> <span data-ttu-id="f7d44-175">此儲存體帳戶中現有檔案的資料將保持未加密狀態。</span><span class="sxs-lookup"><span data-stu-id="f7d44-175">Data in existing files in this storage account will remain unencrypted.</span></span>

<span data-ttu-id="f7d44-176">啟用加密之後，使用下列其中一個方法將資料複製到儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="f7d44-176">After enabling encryption, copy data to the storage account using one of the following methods:</span></span>

1. <span data-ttu-id="f7d44-177">使用 [AzCopy 命令列公用程式](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy)複製 Blob 或檔案。</span><span class="sxs-lookup"><span data-stu-id="f7d44-177">Copy blobs or files with the [AzCopy Command Line utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span></span>

2. <span data-ttu-id="f7d44-178">[使用 SMB 掛接檔案共用](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows)，因此您可以使用 Robocopy 等公用程式來複製檔案。</span><span class="sxs-lookup"><span data-stu-id="f7d44-178">[Mount a file share using SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) so you can use a utility such as Robocopy to copy files.</span></span>

3. <span data-ttu-id="f7d44-179">使用 [.NET 等儲存體用戶端程式庫](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs)，在 Blob 儲存體或儲存體帳戶之間來回複製 Blob 或檔案資料。</span><span class="sxs-lookup"><span data-stu-id="f7d44-179">Copy blob or file data to and from blob storage or between storage accounts using [Storage Client Libraries such as .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

4.  <span data-ttu-id="f7d44-180">使用[儲存體總管](https://docs.microsoft.com/en-us/azure/storage/storage-explorers)將 Blob 上傳至儲存體帳戶，並且啟用加密。</span><span class="sxs-lookup"><span data-stu-id="f7d44-180">Use a [Storage Explorer](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) to upload blobs to your storage account with encryption enabled.</span></span>

### <a name="transparent-data-encryption"></a><span data-ttu-id="f7d44-181">透明資料加密</span><span class="sxs-lookup"><span data-stu-id="f7d44-181">Transparent Data Encryption</span></span>

<span data-ttu-id="f7d44-182">透明資料加密 (TDE) 是 SQL Azure 功能，可讓您在資料庫和伺服器層級加密資料。</span><span class="sxs-lookup"><span data-stu-id="f7d44-182">Transparent Data Encryption (TDE) is a feature in SQL Azure by which you can encrypt data at both the database and server levels.</span></span> <span data-ttu-id="f7d44-183">現在預設會在所有新建立的資料庫上啟用 TDE。</span><span class="sxs-lookup"><span data-stu-id="f7d44-183">TDE is now enabled by default on all newly created databases.</span></span> <span data-ttu-id="f7d44-184">TDE 會執行資料和記錄檔的即時 I/O 加密和解密。</span><span class="sxs-lookup"><span data-stu-id="f7d44-184">TDE performs real-time I/O encryption and decryption of the data and log files.</span></span>

#### <a name="how-do-i-use-tde-to-protect-personal-data"></a><span data-ttu-id="f7d44-185">如何使用 TDE 來保護個人資料？</span><span class="sxs-lookup"><span data-stu-id="f7d44-185">How do I use TDE to protect personal data?</span></span>

<span data-ttu-id="f7d44-186">您可以透過 Azure 入口網站、使用 REST API 或使用 PowerShell 來設定 TDE。</span><span class="sxs-lookup"><span data-stu-id="f7d44-186">You can configure TDE through the Azure portal, by using the REST API, or by using PowerShell.</span></span> <span data-ttu-id="f7d44-187">若要使用 Azure 入口網站在現有的資料庫上啟用 TDE，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="f7d44-187">To enable TDE on an existing database using the Azure Portal, do the following:</span></span>

1. <span data-ttu-id="f7d44-188">前往 Azure 入口網站 (網址為 <https://portal.azure.com>)，並使用您的 Azure 系統管理員或參與者帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="f7d44-188">Visit the Azure portal at <https://portal.azure.com> and sign-in with your Azure Administrator or Contributor account.</span></span>

2. <span data-ttu-id="f7d44-189">在左橫幅上，按一下 [瀏覽]，然後按一下 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f7d44-189">On the left banner, click to BROWSE, and then click SQL databases.</span></span>

3. <span data-ttu-id="f7d44-190">在左窗格中選取 SQL 資料庫時，按一下您的使用者資料庫。</span><span class="sxs-lookup"><span data-stu-id="f7d44-190">With SQL databases selected in the left pane, click your user database.</span></span>

4. <span data-ttu-id="f7d44-191">在資料庫刀鋒視窗中，按一下 [所有設定]。</span><span class="sxs-lookup"><span data-stu-id="f7d44-191">In the database blade, click All settings.</span></span>

5. <span data-ttu-id="f7d44-192">在 [設定] 刀鋒視窗中，按一下 [透明資料加密] 部分以開啟 [透明資料加密] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f7d44-192">In the Settings blade, click Transparent data encryption part to open the Transparent data encryption blade.</span></span>

6. <span data-ttu-id="f7d44-193">在資料加密刀鋒視窗中，將 [資料加密] 按鈕移至 [開啟]，然後按一下 [儲存] (在頁面頂端) 以套用設定。</span><span class="sxs-lookup"><span data-stu-id="f7d44-193">In the Data encryption blade, move the Data encryption button to On, and then click Save (at the top of the page) to apply the setting.</span></span> <span data-ttu-id="f7d44-194">加密狀態將會粗略估算透明資料加密的進度。</span><span class="sxs-lookup"><span data-stu-id="f7d44-194">The Encryption status will approximate the progress of the transparent data encryption.</span></span>

![啟用資料加密](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

<span data-ttu-id="f7d44-196">如需如何啟用 TDE 的指示，以及將受 TDE 保護的資料庫解密的資訊及其他資訊，請參閱 [Azure SQL Database 的透明資料加密](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)一文。</span><span class="sxs-lookup"><span data-stu-id="f7d44-196">Instructions on how to enable TDE and information on decrypting TDE-protected databases and more can be found in the article [Transparent Data Encryption with Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span></span>

## <a name="summary"></a><span data-ttu-id="f7d44-197">摘要</span><span class="sxs-lookup"><span data-stu-id="f7d44-197">Summary</span></span>

<span data-ttu-id="f7d44-198">此公司可以完成加密儲存在 Azure 雲端中個人資料的目標。</span><span class="sxs-lookup"><span data-stu-id="f7d44-198">The company can accomplish its goal of encrypting personal data stored in the Azure cloud.</span></span> <span data-ttu-id="f7d44-199">他們可以透過使用 Azure 磁碟加密保護整個磁碟區來達成此目的。</span><span class="sxs-lookup"><span data-stu-id="f7d44-199">They can do this by using Azure Disk Encryption to  protect entire volumes.</span></span> <span data-ttu-id="f7d44-200">這可能包含保存個人識別資訊和其他敏感性資料的作業系統檔案和資料檔案。</span><span class="sxs-lookup"><span data-stu-id="f7d44-200">This may include both the operating system files and data files that hold personal identifiable information and other sensitive data.</span></span> <span data-ttu-id="f7d44-201">Azure 儲存體服務加密可用來保護儲存在 Blob 和檔案中的個人資料。</span><span class="sxs-lookup"><span data-stu-id="f7d44-201">Azure Storage Service encryption can be used to protect personal data that is stored in blobs and files.</span></span> <span data-ttu-id="f7d44-202">對於儲存在 Azure SQL Database 中的資料，透明資料加密會提供保護，以防止未經授權公開個人資訊。</span><span class="sxs-lookup"><span data-stu-id="f7d44-202">For data that is stored in Azure SQL databases, Transparent Data Encryption provides protection from unauthorized exposure of personal information.</span></span>

<span data-ttu-id="f7d44-203">此公司可以使用 Azure Key Vault，來保護用來加密 Azure 中資料的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f7d44-203">To protect the keys that are used to encrypt data in Azure, the company can use Azure Key Vault.</span></span> <span data-ttu-id="f7d44-204">這會簡化金鑰管理程序，並可讓公司控管存取和加密個人資料的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f7d44-204">This streamlines the key management process and enables the company to maintain control of keys that access and encrypt personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7d44-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f7d44-205">Next steps</span></span>

- [<span data-ttu-id="f7d44-206">Azure 磁碟加密疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="f7d44-206">Azure Disk Encryption Troubleshooting Guide</span></span>](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [<span data-ttu-id="f7d44-207">加密 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f7d44-207">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [<span data-ttu-id="f7d44-208">Azure Data Lake Store 中的資料加密</span><span class="sxs-lookup"><span data-stu-id="f7d44-208">Encryption of data in Azure Data Lake Store</span></span>](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [<span data-ttu-id="f7d44-209">Azure Cosmos DB 資料庫待用加密</span><span class="sxs-lookup"><span data-stu-id="f7d44-209">Azure Cosmos DB database encryption at rest</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
