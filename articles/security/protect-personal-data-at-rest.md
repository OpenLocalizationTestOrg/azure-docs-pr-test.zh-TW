---
title: "保護個人資料使用加密待用 aaaAzure |Microsoft 文件"
description: "這篇文章是協助您使用 Azure tooprotect 個人資料的一系列的一部分"
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
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a><span data-ttu-id="df303-103">Azure 加密技術：使用加密保護個人待用資料</span><span class="sxs-lookup"><span data-stu-id="df303-103">Azure encryption technologies: Protect personal data at rest with encryption</span></span>

<span data-ttu-id="df303-104">這篇文章可協助您了解及使用 Azure 加密技術 toosecure 資料靜止。</span><span class="sxs-lookup"><span data-stu-id="df303-104">This article helps you understand and use Azure encryption technologies toosecure data at rest.</span></span>

<span data-ttu-id="df303-105">待用資料加密務必要做為最佳作法 tooprotect 機密或個人資料以及 toomeet 相容性和資料的隱私權需求。</span><span class="sxs-lookup"><span data-stu-id="df303-105">Encryption of data at rest is essential as a best practice tooprotect sensitive or personal data and toomeet compliance and data privacy requirements.</span></span>
<span data-ttu-id="df303-106">設計的 tooprevent hello 攻擊者存取 hello 未加密資料，方法是確保資料會加密磁碟的 hello 靜止的加密。</span><span class="sxs-lookup"><span data-stu-id="df303-106">Encryption at rest is designed tooprevent hello attacker from accessing hello unencrypted data by ensuring hello data is encrypted when on disk.</span></span>

## <a name="scenario"></a><span data-ttu-id="df303-107">案例</span><span class="sxs-lookup"><span data-stu-id="df303-107">Scenario</span></span> 

<span data-ttu-id="df303-108">大型出航公司搬遷後在 hello 美國，展開在 hello 地中海與波羅的海文海，以及 hello 不列顛群島其作業 toooffer 行程。</span><span class="sxs-lookup"><span data-stu-id="df303-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="df303-109">toosupport 努力，它所取得數個較小的出航行位於義大利、 德國、 丹麥和 hello 英國</span><span class="sxs-lookup"><span data-stu-id="df303-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="df303-110">hello 公司使用 Microsoft Azure toostore 公司資料 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="df303-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="df303-111">這可能包括員工及/或客戶資訊，例如：</span><span class="sxs-lookup"><span data-stu-id="df303-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="df303-112">地址</span><span class="sxs-lookup"><span data-stu-id="df303-112">addresses</span></span>
- <span data-ttu-id="df303-113">電話號碼</span><span class="sxs-lookup"><span data-stu-id="df303-113">phone numbers</span></span>
- <span data-ttu-id="df303-114">稅務識別編號</span><span class="sxs-lookup"><span data-stu-id="df303-114">tax identification numbers</span></span>
- <span data-ttu-id="df303-115">醫療資訊</span><span class="sxs-lookup"><span data-stu-id="df303-115">medical information</span></span>
- <span data-ttu-id="df303-116">信用卡資訊</span><span class="sxs-lookup"><span data-stu-id="df303-116">credit card information</span></span>

<span data-ttu-id="df303-117">hello 公司必須保護員工和客戶資料的 hello 的隱私權，同時進行資料存取 toothose 部門需要它。</span><span class="sxs-lookup"><span data-stu-id="df303-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="df303-118">(例如薪資部門和訂位部門) 可以存取資料。</span><span class="sxs-lookup"><span data-stu-id="df303-118">(such as payroll and reservations departments)</span></span>

<span data-ttu-id="df303-119">hello 出航列也會維護報酬和忠誠度計劃成員大型資料庫，其中包含與目前和過去的客戶的個人資訊 tootrack 關聯性。</span><span class="sxs-lookup"><span data-stu-id="df303-119">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

### <a name="problem-statement"></a><span data-ttu-id="df303-120">問題陳述</span><span class="sxs-lookup"><span data-stu-id="df303-120">Problem statement</span></span>

<span data-ttu-id="df303-121">hello 公司必須保護員工和客戶的個人資料的 hello 的隱私權，同時進行資料存取 toothose 部門需要 （例如，薪資和保留項目的部門）。</span><span class="sxs-lookup"><span data-stu-id="df303-121">hello company must protect hello privacy of employees’ and customers’ personal data while making data accessible toothose departments that need it (such as payroll and reservations departments).</span></span> <span data-ttu-id="df303-122">此個人資料會儲存在 hello 公司控制資料中心外部，而不在 hello 公司的實體控制項。</span><span class="sxs-lookup"><span data-stu-id="df303-122">This personal data is stored outside of hello corporate-controlled data center and is not under hello company’s physical control.</span></span>

### <a name="company-goal"></a><span data-ttu-id="df303-123">公司目標</span><span class="sxs-lookup"><span data-stu-id="df303-123">Company goal</span></span>

<span data-ttu-id="df303-124">多層的深度防禦的安全性策略的一部分，就會加密所有資料來源，包含個人資料，包括雲端儲存體中公司目標 tooensure。</span><span class="sxs-lookup"><span data-stu-id="df303-124">As part of a multi-layered defense-in-depth security strategy, it is a company goal tooensure that all data sources that contain personal data are encrypted, including those residing in cloud storage.</span></span> <span data-ttu-id="df303-125">如果未經授權的人員獲得存取 toohello 個人資料，它必須是會轉譯無法讀取的格式。</span><span class="sxs-lookup"><span data-stu-id="df303-125">If unauthorized persons gain access toohello personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="df303-126">對於使用者和系統管理員而言，套用加密應該很容易或很透明。</span><span class="sxs-lookup"><span data-stu-id="df303-126">Applying encryption should be easy, or transparent – for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="df303-127">解決方案</span><span class="sxs-lookup"><span data-stu-id="df303-127">Solutions</span></span>

<span data-ttu-id="df303-128">Azure 服務可提供多個工具和技術 toohelp 加密保護靜止的個人資料。</span><span class="sxs-lookup"><span data-stu-id="df303-128">Azure services provide multiple tools and technologies toohelp you protect personal data at rest by encrypting it.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="df303-129">Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="df303-129">Azure Key Vault</span></span>

<span data-ttu-id="df303-130">[Azure 金鑰保存庫](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)提供安全的儲存體的 Azure 服務中的靜止使用 tooencrypt 資料 hello 金鑰並且 hello 建議儲存和管理的金鑰方案。</span><span class="sxs-lookup"><span data-stu-id="df303-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) provides secure storage for hello keys used tooencrypt data at rest in Azure services and is hello recommended key storage and management solution.</span></span> <span data-ttu-id="df303-131">儲存的重要 toosecuring 資料加密金鑰管理。</span><span class="sxs-lookup"><span data-stu-id="df303-131">Encryption key management is essential toosecuring stored data.</span></span>

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a><span data-ttu-id="df303-132">如何使用 Azure 金鑰保存庫 tooprotect 金鑰加密的個人資料？</span><span class="sxs-lookup"><span data-stu-id="df303-132">How do I use Azure Key Vault tooprotect keys that encrypt personal data?</span></span>

<span data-ttu-id="df303-133">toouse Azure 金鑰保存庫，您需要訂用帳戶 tooan Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="df303-133">toouse Azure Key Vault, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="df303-134">您也需要安裝 Azure Powershell。</span><span class="sxs-lookup"><span data-stu-id="df303-134">You also need Azure PowerShell installed.</span></span> <span data-ttu-id="df303-135">步驟包括使用 PowerShell cmdlet toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="df303-135">Steps include using PowerShell cmdlets toodo hello following:</span></span>

1. <span data-ttu-id="df303-136">連接 tooyour 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="df303-136">Connect tooyour subscriptions</span></span>

2. <span data-ttu-id="df303-137">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="df303-137">Create a key vault</span></span>

3. <span data-ttu-id="df303-138">新增金鑰或密碼 toohello 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="df303-138">Add a key or secret toohello key vault</span></span>

4. <span data-ttu-id="df303-139">註冊將使用金鑰保存庫 hello 與 Azure Active Directory 應用程式</span><span class="sxs-lookup"><span data-stu-id="df303-139">Register applications that will use hello key vault with Azure Active Directory</span></span>

5. <span data-ttu-id="df303-140">授權 hello 應用程式 toouse hello 金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="df303-140">Authorize hello applications toouse hello key or secret</span></span>

<span data-ttu-id="df303-141">toocreate 金鑰保存庫中，使用 hello 新增 AzureRmKeyVault PowerShell CmDlt。</span><span class="sxs-lookup"><span data-stu-id="df303-141">toocreate a key vault, use hello New-AzureRmKeyVault PowerShell CmDlt.</span></span> <span data-ttu-id="df303-142">您將會指派保存庫名稱、資源群組名稱和地理位置。</span><span class="sxs-lookup"><span data-stu-id="df303-142">You will assign a vault name, resource group name, and geographic location.</span></span> <span data-ttu-id="df303-143">管理透過其他 Cmdlet 的索引鍵時，您將使用 hello 保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="df303-143">You’ll use hello vault name when managing keys via other Cmdlets.</span></span> <span data-ttu-id="df303-144">使用透過 hello REST API 的 hello 保存庫的應用程式會使用 hello 保存庫 URI。</span><span class="sxs-lookup"><span data-stu-id="df303-144">Applications that use hello vault through hello REST API will use hello vault URI.</span></span>

<span data-ttu-id="df303-145">Azure Key Vault 可為您提供受軟體保護的金鑰；或者，您也可以匯入 .PFX 檔案中的現有金鑰。</span><span class="sxs-lookup"><span data-stu-id="df303-145">Azure Key Vault can provide a software-protected key for you, or you can import an existing key in a .PFX file.</span></span> <span data-ttu-id="df303-146">您也可以在 hello 保存庫中儲存機密資訊 （密碼）。</span><span class="sxs-lookup"><span data-stu-id="df303-146">You can also store secrets (passwords) in hello vault.</span></span>

<span data-ttu-id="df303-147">您也可以在本機 HSM 中產生金鑰並將金鑰傳輸 tooHSMs hello 金鑰保存庫服務中的沒有 hello 離開 hello HSM 界限的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="df303-147">You can also generate a key in your local HSM and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary.</span></span>

<span data-ttu-id="df303-148">中的詳細說明如何使用 Azure 金鑰保存庫，請依照下列步驟 hello[開始使用 Azure 金鑰保存庫。](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span><span class="sxs-lookup"><span data-stu-id="df303-148">For detailed instructions on using Azure Key Vault, follow hello steps in [Get Started with Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span></span>

<span data-ttu-id="df303-149">如需搭配 Azure Key Vault 使用的 PowerShell Cmdlet 清單，請參閱 [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0)。</span><span class="sxs-lookup"><span data-stu-id="df303-149">For a list of PowerShell Cmdlets used with Azure Key Vault, see [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

### <a name="azure-disk-encryption-for-windows"></a><span data-ttu-id="df303-150">Windows 適用的 Azure 磁碟加密</span><span class="sxs-lookup"><span data-stu-id="df303-150">Azure Disk Encryption for Windows</span></span>

<span data-ttu-id="df303-151">[Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)會保護 Azure 虛擬機器上的個人待用資料，並與 Azure Key Vault 整合。</span><span class="sxs-lookup"><span data-stu-id="df303-151">[Azure Disk Encryption for Windows and Linux IaaS VMs](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protects personal data at rest on Azure virtual machines and integrates with Azure Key Vault.</span></span> <span data-ttu-id="df303-152">Azure 磁碟加密使用[BitLocker](https://technet.microsoft.com/library/cc732774.aspx)在 Windows 和[DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux tooencrypt 中同時 hello OS 和 hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="df303-152">Azure Disk Encryption uses [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows and [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux tooencrypt both hello OS and hello data disks.</span></span> <span data-ttu-id="df303-153">Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016 以及 Windows 8 和 Windows 10 用戶端支援 Azure 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="df303-153">Azure Disk Encryption is supported on Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, and on Windows 8 and Windows 10 clients.</span></span>

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a><span data-ttu-id="df303-154">如何使用 Azure 磁碟加密 tooprotect 個人資料？</span><span class="sxs-lookup"><span data-stu-id="df303-154">How do I use Azure Disk Encryption tooprotect personal data?</span></span>

<span data-ttu-id="df303-155">toouse Azure 磁碟加密，您需要訂用帳戶 tooan Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="df303-155">toouse Azure Disk Encryption, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="df303-156">下列 hello tooenable Azure 磁碟加密適用於 Windows 及 Linux Vm:</span><span class="sxs-lookup"><span data-stu-id="df303-156">tooenable Azure Disk Encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="df303-157">使用 hello Azure 磁碟加密 Resource Manager 範本、 PowerShell 或 hello 命令列介面 (CLI) tooenable 磁碟加密，並指定的加密組態。</span><span class="sxs-lookup"><span data-stu-id="df303-157">Use hello Azure Disk Encryption Resource Manager template, PowerShell, or hello command line interface (CLI) tooenable disk encryption and specify the  encryption configuration.</span></span> 

2. <span data-ttu-id="df303-158">授與存取 toohello Azure 平台 tooread hello 從金鑰保存庫的加密內容。</span><span class="sxs-lookup"><span data-stu-id="df303-158">Grant access toohello Azure platform tooread hello encryption material from your key vault.</span></span>

3. <span data-ttu-id="df303-159">提供 Azure Active Directory (AAD) 應用程式識別 toowrite hello 加密金鑰材料 tooyour 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="df303-159">Provide an Azure Active Directory (AAD) application identity toowrite hello encryption key material tooyour key vault.</span></span>

<span data-ttu-id="df303-160">Azure 將會更新 hello VM 和 hello 金鑰保存庫設定，與您加密的 VM 設定。</span><span class="sxs-lookup"><span data-stu-id="df303-160">Azure will update hello VM and hello key vault configuration, and set up your encrypted VM.</span></span>

<span data-ttu-id="df303-161">當您設定您的金鑰保存庫 toosupport Azure 磁碟加密時，您可以提高的安全性和加密的虛擬機器 toosupport 備份加入加密金鑰 (KEK)。</span><span class="sxs-lookup"><span data-stu-id="df303-161">When you set up your key vault toosupport Azure Disk Encryption, you can add a key encryption key (KEK) for added security and toosupport backup of encrypted virtual machines.</span></span>

![](media/protect-personal-data-at-rest/create-key.png)

<span data-ttu-id="df303-162">如需特定部署案例和使用者體驗的詳細指示，請參閱 [Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)。</span><span class="sxs-lookup"><span data-stu-id="df303-162">Detailed instructions for specific deployment scenarios and user experiences are included in [Azure Disk Encryption for Windows and Linux IaaS VMs.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span></span>

### <a name="azure-storage-service-encryption"></a><span data-ttu-id="df303-163">Azure 儲存體服務加密</span><span class="sxs-lookup"><span data-stu-id="df303-163">Azure Storage Service Encryption</span></span>

<span data-ttu-id="df303-164">[Azure 儲存體服務加密 (SSE) 中的靜止資料](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption)可協助您保護與防衛資料 toomeet 您組織的安全性與相容性承諾。</span><span class="sxs-lookup"><span data-stu-id="df303-164">[Azure Storage Service Encryption (SSE) for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helps you protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="df303-165">Azure 儲存體自動會使用 256 位元 AES 加密先前 toopersisting toostorage 資料加密和解密先前 tooretrieval。</span><span class="sxs-lookup"><span data-stu-id="df303-165">Azure Storage automatically encrypts your data using 256-bit AES encryption prior toopersisting toostorage, and decrypts it prior tooretrieval.</span></span> <span data-ttu-id="df303-166">這個服務適用於 Azure Blob 和檔案。</span><span class="sxs-lookup"><span data-stu-id="df303-166">This service is available for Azure Blobs and Files.</span></span>

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a><span data-ttu-id="df303-167">如何使用儲存體服務加密 tooprotect 個人資料？</span><span class="sxs-lookup"><span data-stu-id="df303-167">How do I use Storage Service Encryption tooprotect personal data?</span></span>

<span data-ttu-id="df303-168">tooenable 儲存體服務加密，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="df303-168">tooenable Storage Service Encryption, do hello following:</span></span>

1. <span data-ttu-id="df303-169">登入 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="df303-169">Log into hello Azure portal.</span></span>

2. <span data-ttu-id="df303-170">選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="df303-170">Select a storage account.</span></span>

3. <span data-ttu-id="df303-171">在 [設定] 底下 hello Blob 服務區段中，選取加密。</span><span class="sxs-lookup"><span data-stu-id="df303-171">In Settings, under hello Blob Service section, select Encryption.</span></span>

4. <span data-ttu-id="df303-172">在 hello 檔案服務 區段中，選取 加密。</span><span class="sxs-lookup"><span data-stu-id="df303-172">Under hello File Service section, select Encryption.</span></span>

<span data-ttu-id="df303-173">按一下 hello 加密設定之後，您可以啟用或停用儲存體服務加密。</span><span class="sxs-lookup"><span data-stu-id="df303-173">After you click hello Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

<span data-ttu-id="df303-174">新的資料將會加密。</span><span class="sxs-lookup"><span data-stu-id="df303-174">New data will be encrypted.</span></span> <span data-ttu-id="df303-175">此儲存體帳戶中現有檔案的資料將保持未加密狀態。</span><span class="sxs-lookup"><span data-stu-id="df303-175">Data in existing files in this storage account will remain unencrypted.</span></span>

<span data-ttu-id="df303-176">啟用加密之後, 將複製資料 toohello 儲存體帳戶使用其中一種 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="df303-176">After enabling encryption, copy data toohello storage account using one of hello following methods:</span></span>

1. <span data-ttu-id="df303-177">複製 blob 或檔案以 hello [AzCopy 命令列公用程式](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy)。</span><span class="sxs-lookup"><span data-stu-id="df303-177">Copy blobs or files with hello [AzCopy Command Line utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span></span>

2. <span data-ttu-id="df303-178">[掛上使用 SMB 檔案共用](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows)因此您可以使用公用程式，例如 Robocopy toocopy 檔案。</span><span class="sxs-lookup"><span data-stu-id="df303-178">[Mount a file share using SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) so you can use a utility such as Robocopy toocopy files.</span></span>

3. <span data-ttu-id="df303-179">複製 blob 或檔案資料 tooand 從 blob 儲存體或儲存體帳戶使用[儲存體用戶端程式庫，例如.NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs)。</span><span class="sxs-lookup"><span data-stu-id="df303-179">Copy blob or file data tooand from blob storage or between storage accounts using [Storage Client Libraries such as .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

4.  <span data-ttu-id="df303-180">使用[存放裝置總管](https://docs.microsoft.com/en-us/azure/storage/storage-explorers)tooupload blob tooyour 儲存體帳戶並啟用加密。</span><span class="sxs-lookup"><span data-stu-id="df303-180">Use a [Storage Explorer](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload blobs tooyour storage account with encryption enabled.</span></span>

### <a name="transparent-data-encryption"></a><span data-ttu-id="df303-181">透明資料加密</span><span class="sxs-lookup"><span data-stu-id="df303-181">Transparent Data Encryption</span></span>

<span data-ttu-id="df303-182">透明資料加密 (TDE) 是 SQL Azure，您可以用來加密這兩個 hello 資料庫和伺服器層級的資料中的功能。</span><span class="sxs-lookup"><span data-stu-id="df303-182">Transparent Data Encryption (TDE) is a feature in SQL Azure by which you can encrypt data at both hello database and server levels.</span></span> <span data-ttu-id="df303-183">現在預設會在所有新建立的資料庫上啟用 TDE。</span><span class="sxs-lookup"><span data-stu-id="df303-183">TDE is now enabled by default on all newly created databases.</span></span> <span data-ttu-id="df303-184">TDE 會執行即時 I/O 加密和解密的 hello 資料和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="df303-184">TDE performs real-time I/O encryption and decryption of hello data and log files.</span></span>

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a><span data-ttu-id="df303-185">如何使用 TDE tooprotect 個人資料？</span><span class="sxs-lookup"><span data-stu-id="df303-185">How do I use TDE tooprotect personal data?</span></span>

<span data-ttu-id="df303-186">使用 hello REST API 或 PowerShell，您可以透過 hello Azure 入口網站設定 TDE。</span><span class="sxs-lookup"><span data-stu-id="df303-186">You can configure TDE through hello Azure portal, by using hello REST API, or by using PowerShell.</span></span> <span data-ttu-id="df303-187">在現有的資料庫使用 hello Azure 入口網站，tooenable TDE hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="df303-187">tooenable TDE on an existing database using hello Azure Portal, do hello following:</span></span>

1. <span data-ttu-id="df303-188">請瀏覽 hello Azure 入口網站在<https://portal.azure.com>和使用您的 Azure 系統管理員或參與者帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="df303-188">Visit hello Azure portal at <https://portal.azure.com> and sign-in with your Azure Administrator or Contributor account.</span></span>

2. <span data-ttu-id="df303-189">在 hello 左邊的橫幅中，按一下 tooBROWSE，，然後按一下 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="df303-189">On hello left banner, click tooBROWSE, and then click SQL databases.</span></span>

3. <span data-ttu-id="df303-190">Hello 左窗格中選取的 SQL 資料庫，按一下您的使用者資料庫。</span><span class="sxs-lookup"><span data-stu-id="df303-190">With SQL databases selected in hello left pane, click your user database.</span></span>

4. <span data-ttu-id="df303-191">在 hello 資料庫刀鋒視窗中，按一下 所有設定。</span><span class="sxs-lookup"><span data-stu-id="df303-191">In hello database blade, click All settings.</span></span>

5. <span data-ttu-id="df303-192">在 hello 設定刀鋒視窗中，按一下 透明資料加密部分 tooopen hello 透明資料加密 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="df303-192">In hello Settings blade, click Transparent data encryption part tooopen hello Transparent data encryption blade.</span></span>

6. <span data-ttu-id="df303-193">在 hello 資料加密 刀鋒視窗，將資料加密 按鈕 tooOn hello，，然後按一下儲存 （hello 頁面頂端的 hello） tooapply hello 設定。</span><span class="sxs-lookup"><span data-stu-id="df303-193">In hello Data encryption blade, move hello Data encryption button tooOn, and then click Save (at hello top of hello page) tooapply hello setting.</span></span> <span data-ttu-id="df303-194">hello 加密的狀態會顯示概略 hello 透明資料加密的 hello 的進度。</span><span class="sxs-lookup"><span data-stu-id="df303-194">hello Encryption status will approximate hello progress of hello transparent data encryption.</span></span>

![啟用資料加密](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

<span data-ttu-id="df303-196">說明如何在 hello 文章中找到 tooenable TDE，以及有關解密 TDE 保護的資料庫和多個[Azure SQL Database 的透明資料加密。](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span><span class="sxs-lookup"><span data-stu-id="df303-196">Instructions on how tooenable TDE and information on decrypting TDE-protected databases and more can be found in hello article [Transparent Data Encryption with Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span></span>

## <a name="summary"></a><span data-ttu-id="df303-197">摘要</span><span class="sxs-lookup"><span data-stu-id="df303-197">Summary</span></span>

<span data-ttu-id="df303-198">hello 公司可以完成其加密儲存在 hello Azure 雲端中的個人資料的目標。</span><span class="sxs-lookup"><span data-stu-id="df303-198">hello company can accomplish its goal of encrypting personal data stored in hello Azure cloud.</span></span> <span data-ttu-id="df303-199">他們可以使用 Azure 磁碟加密來進行這太保護整個磁碟區。</span><span class="sxs-lookup"><span data-stu-id="df303-199">They can do this by using Azure Disk Encryption too protect entire volumes.</span></span> <span data-ttu-id="df303-200">這可能包括 hello 作業系統檔案和存放個人識別資訊與其他敏感性資料的資料檔案。</span><span class="sxs-lookup"><span data-stu-id="df303-200">This may include both hello operating system files and data files that hold personal identifiable information and other sensitive data.</span></span> <span data-ttu-id="df303-201">Azure 儲存體服務加密可使用的 tooprotect 個人資料會儲存在 blob 和檔案。</span><span class="sxs-lookup"><span data-stu-id="df303-201">Azure Storage Service encryption can be used tooprotect personal data that is stored in blobs and files.</span></span> <span data-ttu-id="df303-202">對於儲存在 Azure SQL Database 中的資料，透明資料加密會提供保護，以防止未經授權公開個人資訊。</span><span class="sxs-lookup"><span data-stu-id="df303-202">For data that is stored in Azure SQL databases, Transparent Data Encryption provides protection from unauthorized exposure of personal information.</span></span>

<span data-ttu-id="df303-203">在 Azure 中使用的 tooencrypt 資料 tooprotect hello 索引鍵，hello 公司可以使用 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="df303-203">tooprotect hello keys that are used tooencrypt data in Azure, hello company can use Azure Key Vault.</span></span> <span data-ttu-id="df303-204">這可簡化 hello 金鑰管理程序，並啟用 hello 公司 toomaintain 控制存取和個人資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="df303-204">This streamlines hello key management process and enables hello company toomaintain control of keys that access and encrypt personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df303-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="df303-205">Next steps</span></span>

- [<span data-ttu-id="df303-206">Azure 磁碟加密疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="df303-206">Azure Disk Encryption Troubleshooting Guide</span></span>](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [<span data-ttu-id="df303-207">加密 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="df303-207">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [<span data-ttu-id="df303-208">Azure Data Lake Store 中的資料加密</span><span class="sxs-lookup"><span data-stu-id="df303-208">Encryption of data in Azure Data Lake Store</span></span>](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [<span data-ttu-id="df303-209">Azure Cosmos DB 資料庫待用加密</span><span class="sxs-lookup"><span data-stu-id="df303-209">Azure Cosmos DB database encryption at rest</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
