---
title: "aaaAzure 磁碟加密常見問題集 |Microsoft 文件"
description: "本文提供的解答 toofrequently 常見問題的 Microsoft Azure 磁碟加密適用於 Windows 及 Linux IaaS Vm。"
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: 7188da52-5540-421d-bf45-d124dee74979
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: devtiw
ms.openlocfilehash: 17f084628ba4ef22e9d37dd3052ef10f8eb2cd7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-frequently-asked-questions-faq"></a><span data-ttu-id="cd6af-103">Azure 磁碟加密常見問題集 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="cd6af-103">Azure Disk Encryption Frequently Asked Questions (FAQ)</span></span>

<span data-ttu-id="cd6af-104">此常見問題集中會解答 Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密的相關問題，如需這項服務的相關資訊，請參閱 [Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)。</span><span class="sxs-lookup"><span data-stu-id="cd6af-104">This FAQ answers questions about Azure disk encryption for Windows and Linux IaaS VMs, for more information about this service, read [Azure Disk Encryption for Windows and Linux IaaS VMs](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).</span></span>

## <a name="general-questions"></a><span data-ttu-id="cd6af-105">一般問題</span><span class="sxs-lookup"><span data-stu-id="cd6af-105">General questions</span></span>
<span data-ttu-id="cd6af-106">**問：**</span><span class="sxs-lookup"><span data-stu-id="cd6af-106">**Q.**</span></span> <span data-ttu-id="cd6af-107">Azure 磁碟加密在 GA 中的哪一個區域？</span><span class="sxs-lookup"><span data-stu-id="cd6af-107">Which region is Azure disk encryption in GA?</span></span>

<span data-ttu-id="cd6af-108">**答：**Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密會在所有 Azure 公用區域的 GA 中提供。</span><span class="sxs-lookup"><span data-stu-id="cd6af-108">**A:** Azure disk encryption for Windows and Linux IaaS VMs is available in GA in all Azure public regions.</span></span>

<span data-ttu-id="cd6af-109">**問：**Azure 磁碟加密有哪些使用者體驗？</span><span class="sxs-lookup"><span data-stu-id="cd6af-109">**Q:** What user experiences are available with Azure Disk Encryption?</span></span>

<span data-ttu-id="cd6af-110">**答：**Azure 磁碟加密 GA 支援 Azure Resource Manager 範本、Azure PowerShell、Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="cd6af-110">**A:** Azure Disk Encryption GA supports Azure Resource Manager templates, Azure PowerShell, Azure CLI.</span></span> <span data-ttu-id="cd6af-111">這為您提供很大的彈性，因為您會有三個不同選項可啟用您 IaaS VM 的磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="cd6af-111">This gives you a lot of flexibility in that you have three different options for enabling disk encryption for your IaaS VMs.</span></span> <span data-ttu-id="cd6af-112">Hello Azure 磁碟加密部署案例及體驗提供 hello 使用者體驗，以及逐步指引的更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="cd6af-112">More details on hello user experience and step by step guidance is available in hello Azure Disk Encryption deployment scenarios and experiences.</span></span>

<span data-ttu-id="cd6af-113">**問：**Azure 磁碟加密如何收費？</span><span class="sxs-lookup"><span data-stu-id="cd6af-113">**Q:** How much does Azure Disk Encryption cost?</span></span>

<span data-ttu-id="cd6af-114">**答：**使用 Azure 磁碟加密來加密 VM 磁碟完全免費。</span><span class="sxs-lookup"><span data-stu-id="cd6af-114">**A:** There is no charge for encrypting VM disks with Azure Disk Encryption.</span></span>

<span data-ttu-id="cd6af-115">**問：**可以使用 Azure 磁碟加密搭配哪些虛擬機器層？</span><span class="sxs-lookup"><span data-stu-id="cd6af-115">**Q:** What virtual machine tiers can I use Azure Disk Encryption with?</span></span>

<span data-ttu-id="cd6af-116">**答：**Azure 磁碟加密僅適用於標準層 VM，包括 [A、D、DS、G、GS、F](https://azure.microsoft.com/pricing/details/virtual-machines/) 等系列，IaaS VM 包括使用進階儲存體的 VM。</span><span class="sxs-lookup"><span data-stu-id="cd6af-116">**A:** Azure Disk Encryption is available only on Standard Tier VMs including [A, D, DS, G, GS, F](https://azure.microsoft.com/pricing/details/virtual-machines/) and so forth series IaaS VMs including VMs with premium storage.</span></span> <span data-ttu-id="cd6af-117">它並不適用於基本層 VM。</span><span class="sxs-lookup"><span data-stu-id="cd6af-117">It is not available on Basic Tier VMs.</span></span>

<span data-ttu-id="cd6af-118">**問：**Azure 磁碟加密支援哪些 Linux 散發套件？</span><span class="sxs-lookup"><span data-stu-id="cd6af-118">**Q:** What Linux distributions are supported by Azure Disk Encryption?</span></span>

<span data-ttu-id="cd6af-119">**答：** hello 下列 Linux 伺服器的發行版本和版本支援 Azure 磁碟加密：</span><span class="sxs-lookup"><span data-stu-id="cd6af-119">**A:** Azure Disk Encryption is supported on hello following Linux server distributions and versions:</span></span>

| <span data-ttu-id="cd6af-120">Linux 散發套件</span><span class="sxs-lookup"><span data-stu-id="cd6af-120">Linux Distribution</span></span> | <span data-ttu-id="cd6af-121">版本</span><span class="sxs-lookup"><span data-stu-id="cd6af-121">Version</span></span> | <span data-ttu-id="cd6af-122">支援加密的磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="cd6af-122">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="cd6af-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cd6af-123">Ubuntu</span></span> | <span data-ttu-id="cd6af-124">16.04-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="cd6af-124">16.04-DAILY-LTS</span></span> | <span data-ttu-id="cd6af-125">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-125">OS and Data disk</span></span> |
| <span data-ttu-id="cd6af-126">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cd6af-126">Ubuntu</span></span> | <span data-ttu-id="cd6af-127">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="cd6af-127">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="cd6af-128">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-128">OS and Data disk</span></span> |
| <span data-ttu-id="cd6af-129">RHEL</span><span class="sxs-lookup"><span data-stu-id="cd6af-129">RHEL</span></span> | <span data-ttu-id="cd6af-130">7.3</span><span class="sxs-lookup"><span data-stu-id="cd6af-130">7.3</span></span> | <span data-ttu-id="cd6af-131">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-131">OS and Data disk</span></span> |
| <span data-ttu-id="cd6af-132">RHEL</span><span class="sxs-lookup"><span data-stu-id="cd6af-132">RHEL</span></span> | <span data-ttu-id="cd6af-133">7.2</span><span class="sxs-lookup"><span data-stu-id="cd6af-133">7.2</span></span> | <span data-ttu-id="cd6af-134">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-134">OS and Data disk</span></span> |
| <span data-ttu-id="cd6af-135">RHEL</span><span class="sxs-lookup"><span data-stu-id="cd6af-135">RHEL</span></span> | <span data-ttu-id="cd6af-136">6.8</span><span class="sxs-lookup"><span data-stu-id="cd6af-136">6.8</span></span> | <span data-ttu-id="cd6af-137">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-137">OS and Data disk</span></span> |
| <span data-ttu-id="cd6af-138">RHEL</span><span class="sxs-lookup"><span data-stu-id="cd6af-138">RHEL</span></span> | <span data-ttu-id="cd6af-139">6.7</span><span class="sxs-lookup"><span data-stu-id="cd6af-139">6.7</span></span> | <span data-ttu-id="cd6af-140">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-140">Data disk</span></span> |
| <span data-ttu-id="cd6af-141">CentOS</span><span class="sxs-lookup"><span data-stu-id="cd6af-141">CentOS</span></span> | <span data-ttu-id="cd6af-142">7.3</span><span class="sxs-lookup"><span data-stu-id="cd6af-142">7.3</span></span> | <span data-ttu-id="cd6af-143">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-143">OS and Data disk</span></span> |
| <span data-ttu-id="cd6af-144">CentOS</span><span class="sxs-lookup"><span data-stu-id="cd6af-144">CentOS</span></span> | <span data-ttu-id="cd6af-145">7.2n</span><span class="sxs-lookup"><span data-stu-id="cd6af-145">7.2n</span></span> | <span data-ttu-id="cd6af-146">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-146">OS and Data disk</span></span> |
| <span data-ttu-id="cd6af-147">CentOS</span><span class="sxs-lookup"><span data-stu-id="cd6af-147">CentOS</span></span> | <span data-ttu-id="cd6af-148">6.8</span><span class="sxs-lookup"><span data-stu-id="cd6af-148">6.8</span></span> | <span data-ttu-id="cd6af-149">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-149">OS and Data disk</span></span> |
| <span data-ttu-id="cd6af-150">CentOS</span><span class="sxs-lookup"><span data-stu-id="cd6af-150">CentOS</span></span> | <span data-ttu-id="cd6af-151">7.1</span><span class="sxs-lookup"><span data-stu-id="cd6af-151">7.1</span></span> | <span data-ttu-id="cd6af-152">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-152">Data disk</span></span> |
| <span data-ttu-id="cd6af-153">CentOS</span><span class="sxs-lookup"><span data-stu-id="cd6af-153">CentOS</span></span> | <span data-ttu-id="cd6af-154">7.0</span><span class="sxs-lookup"><span data-stu-id="cd6af-154">7.0</span></span> | <span data-ttu-id="cd6af-155">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-155">Data disk</span></span> |
| <span data-ttu-id="cd6af-156">CentOS</span><span class="sxs-lookup"><span data-stu-id="cd6af-156">CentOS</span></span> | <span data-ttu-id="cd6af-157">6.7</span><span class="sxs-lookup"><span data-stu-id="cd6af-157">6.7</span></span> | <span data-ttu-id="cd6af-158">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-158">Data disk</span></span> |
| <span data-ttu-id="cd6af-159">CentOS</span><span class="sxs-lookup"><span data-stu-id="cd6af-159">CentOS</span></span> | <span data-ttu-id="cd6af-160">6.6</span><span class="sxs-lookup"><span data-stu-id="cd6af-160">6.6</span></span> | <span data-ttu-id="cd6af-161">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-161">Data disk</span></span> |
| <span data-ttu-id="cd6af-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="cd6af-162">CentOS</span></span> | <span data-ttu-id="cd6af-163">6.5</span><span class="sxs-lookup"><span data-stu-id="cd6af-163">6.5</span></span> | <span data-ttu-id="cd6af-164">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-164">Data disk</span></span> |
| <span data-ttu-id="cd6af-165">openSUSE</span><span class="sxs-lookup"><span data-stu-id="cd6af-165">openSUSE</span></span> | <span data-ttu-id="cd6af-166">13.2</span><span class="sxs-lookup"><span data-stu-id="cd6af-166">13.2</span></span> | <span data-ttu-id="cd6af-167">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-167">Data disk</span></span> |
| <span data-ttu-id="cd6af-168">SLES</span><span class="sxs-lookup"><span data-stu-id="cd6af-168">SLES</span></span> | <span data-ttu-id="cd6af-169">12 SP1</span><span class="sxs-lookup"><span data-stu-id="cd6af-169">12 SP1</span></span> | <span data-ttu-id="cd6af-170">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-170">Data disk</span></span> |
| <span data-ttu-id="cd6af-171">SLES</span><span class="sxs-lookup"><span data-stu-id="cd6af-171">SLES</span></span> | <span data-ttu-id="cd6af-172">優先順序：12-SP1</span><span class="sxs-lookup"><span data-stu-id="cd6af-172">Priority:12-SP1</span></span> | <span data-ttu-id="cd6af-173">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-173">Data disk</span></span> |
| <span data-ttu-id="cd6af-174">SLES</span><span class="sxs-lookup"><span data-stu-id="cd6af-174">SLES</span></span> | <span data-ttu-id="cd6af-175">HPC 12</span><span class="sxs-lookup"><span data-stu-id="cd6af-175">HPC 12</span></span> | <span data-ttu-id="cd6af-176">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-176">Data disk</span></span> |
| <span data-ttu-id="cd6af-177">SLES</span><span class="sxs-lookup"><span data-stu-id="cd6af-177">SLES</span></span> | <span data-ttu-id="cd6af-178">優先順序：11-SP4</span><span class="sxs-lookup"><span data-stu-id="cd6af-178">Priority:11-SP4</span></span> | <span data-ttu-id="cd6af-179">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-179">Data disk</span></span> |
| <span data-ttu-id="cd6af-180">SLES</span><span class="sxs-lookup"><span data-stu-id="cd6af-180">SLES</span></span> | <span data-ttu-id="cd6af-181">11 SP4</span><span class="sxs-lookup"><span data-stu-id="cd6af-181">11 SP4</span></span> | <span data-ttu-id="cd6af-182">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="cd6af-182">Data disk</span></span> |

<span data-ttu-id="cd6af-183">**問：**如何開始使用 Azure 磁碟加密？</span><span class="sxs-lookup"><span data-stu-id="cd6af-183">**Q:** How can I get started using Azure Disk Encryption?</span></span>

<span data-ttu-id="cd6af-184">**答：**客戶可以了解如何 tooget 啟動讀取 hello Azure 磁碟加密 （英文） 白皮書位於[這裡](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)</span><span class="sxs-lookup"><span data-stu-id="cd6af-184">**A:** Customers can learn how tooget started by reading hello Azure Disk Encryption whitepaper located [here](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)</span></span>

<span data-ttu-id="cd6af-185">**問：**是否可以使用 Azure 磁碟加密來加密開機和資料磁碟區？</span><span class="sxs-lookup"><span data-stu-id="cd6af-185">**Q:** Can I encrypt both boot and data volumes with Azure Disk Encryption?</span></span>

<span data-ttu-id="cd6af-186">**答：**是，您可以加密 Windows 和 Linux IaaS VM 適用的開機和資料磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cd6af-186">**A:** Yes, you can encrypt boot and data volumes for Windows and Linux IaaS VMs.</span></span> <span data-ttu-id="cd6af-187">適用於 Windows Vm，您無法加密 hello 資料，沒有第一個 encrpting hello OS 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cd6af-187">For Windows VMs, you cannot encrypt hello data without first encrpting hello OS volume.</span></span> <span data-ttu-id="cd6af-188">適用於 Linux Vm，您可以先加密 hello 沒有 encryptinng hello OS 磁碟區的資料磁碟區。</span><span class="sxs-lookup"><span data-stu-id="cd6af-188">For Linux VMs, you can encrypt hello data volume without encryptinng hello OS volume first.</span></span> <span data-ttu-id="cd6af-189">一旦您已如 Liux 加密 hello OS 磁碟區，不支援停用作業系統磁碟區上的 Linux IaaS Vm 的加密</span><span class="sxs-lookup"><span data-stu-id="cd6af-189">Once you have encrypted hello OS volume for Liux, disabling encryption on an OS volume for Linux IaaS VMs is not supported</span></span>

<span data-ttu-id="cd6af-190">**問：**Azure 磁碟加密可讓您使用「自備金鑰」(BYOK) 功能嗎？</span><span class="sxs-lookup"><span data-stu-id="cd6af-190">**Q:** Does Azure Disk Encryption enable a “bring your own key” (BYOK) capability?</span></span>

<span data-ttu-id="cd6af-191">**答：**是，您可以提供自己的金鑰加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="cd6af-191">**A:** Yes, you can supply your own key encryption keys.</span></span> <span data-ttu-id="cd6af-192">這些金鑰會受 Azure 金鑰保存庫，這是 hello Azure 磁碟加密金鑰存放區。</span><span class="sxs-lookup"><span data-stu-id="cd6af-192">Those keys are safeguarded in Azure Key Vault, which is hello key store for Azure Disk Encryption.</span></span> <span data-ttu-id="cd6af-193">如需 hello 的加密金鑰的詳細支援案例，請參閱 hello Azure 磁碟加密部署案例和體驗</span><span class="sxs-lookup"><span data-stu-id="cd6af-193">For more details on hello key encryption key support scenarios, see hello Azure Disk Encryption deployment scenarios and experiences</span></span>

<span data-ttu-id="cd6af-194">**問：**是否可以使用 Azure 建立的金鑰加密金鑰？</span><span class="sxs-lookup"><span data-stu-id="cd6af-194">**Q:** Can I use a Azure-created key encryption key?</span></span>

<span data-ttu-id="cd6af-195">**答：**是，您可以使用 Azure 金鑰保存庫 toogenerate 金鑰的加密金鑰，Azure 磁碟加密使用。</span><span class="sxs-lookup"><span data-stu-id="cd6af-195">**A:** Yes, you can use Azure Key vault toogenerate key encryption key for Azure disk encryption use.</span></span> <span data-ttu-id="cd6af-196">這些金鑰會受 Azure 金鑰保存庫，這是 hello Azure 磁碟加密金鑰存放區。</span><span class="sxs-lookup"><span data-stu-id="cd6af-196">Those keys are safeguarded in Azure Key Vault, which is hello key store for Azure Disk Encryption.</span></span> <span data-ttu-id="cd6af-197">如需 hello 的加密金鑰的詳細支援案例，請參閱 hello Azure 磁碟加密部署案例和體驗</span><span class="sxs-lookup"><span data-stu-id="cd6af-197">For more details on hello key encryption key support scenarios, see hello Azure Disk Encryption deployment scenarios and experiences</span></span>

<span data-ttu-id="cd6af-198">**問：**我可以使用內部部署金鑰管理服務/HSM toosafeguard hello 加密金鑰？</span><span class="sxs-lookup"><span data-stu-id="cd6af-198">**Q:** Can I use on-premises key management service/HSM toosafeguard hello encryption keys?</span></span>

<span data-ttu-id="cd6af-199">**答：** hello 在內部部署金鑰管理服務/HSM toosafeguard hello 加密金鑰無法使用 Azure 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="cd6af-199">**A:** You cannot use hello on-premises key management service/HSM toosafeguard hello encryption keys with Azure disk encryption.</span></span> <span data-ttu-id="cd6af-200">您只能使用 hello Azure 金鑰保存庫服務 toosafeguard hello 加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="cd6af-200">You can only use hello Azure key vault service toosafeguard hello encryption keys.</span></span> <span data-ttu-id="cd6af-201">如需 hello 的加密金鑰的詳細支援案例，請參閱 hello Azure 磁碟加密部署案例和體驗</span><span class="sxs-lookup"><span data-stu-id="cd6af-201">For more details on hello key encryption key support scenarios, see hello Azure Disk Encryption deployment scenarios and experiences</span></span>

<span data-ttu-id="cd6af-202">**問：** hello 必要條件 tooconfigure Azure 磁碟加密為何？</span><span class="sxs-lookup"><span data-stu-id="cd6af-202">**Q:** What are hello prerequisites tooconfigure Azure disk encryption?</span></span>

<span data-ttu-id="cd6af-203">**答：** hello Azure 磁碟加密必要條件 PowerShell 指令碼 toocreate AAD 應用程式，建立新的金鑰保存庫或設定現有磁碟加密存取 tooenable 加密和保護機密資料和金鑰的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="cd6af-203">**A:** hello Azure disk encryption prerequisite PowerShell script toocreate AAD application, create new key vault or setup existing key vault for disk encryption access tooenable encryption and safeguard secrets and key.</span></span>  <span data-ttu-id="cd6af-204">如需 hello 的加密金鑰的詳細支援案例，請參閱 hello Azure 磁碟加密先決條件和部署案例和體驗</span><span class="sxs-lookup"><span data-stu-id="cd6af-204">For more details on hello key encryption key support scenarios, see hello Azure Disk Encryption prerequisites and deployment scenarios and experiences</span></span>

<span data-ttu-id="cd6af-205">**問：**哪裡取得更多有關如何設定 Azure 磁碟加密 toouse PowerShell？</span><span class="sxs-lookup"><span data-stu-id="cd6af-205">**Q:** Where can I get more information on how toouse PowerShell for configuring Azure Disk Encryption?</span></span>

<span data-ttu-id="cd6af-206">**答：**我們有一些絕佳的文章，說明如何執行基本的 Azure 磁碟加密工作，以及更多進階的情節。</span><span class="sxs-lookup"><span data-stu-id="cd6af-206">**A:** We have some great articles on how you can perform basic Azure Disk Encryption tasks, as well as more advanced scenarios.</span></span> <span data-ttu-id="cd6af-207">如 hello 基本的工作，請參閱瀏覽[Azure 磁碟加密使用 Azure PowerShell-第 1 部分](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/explore-azure-disk-encryption-with-azure-powershell/)。</span><span class="sxs-lookup"><span data-stu-id="cd6af-207">For hello basic tasks, check out Explore [Azure Disk Encryption with Azure PowerShell - Part 1](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/explore-azure-disk-encryption-with-azure-powershell/).</span></span> <span data-ttu-id="cd6af-208">如需更多進階的情節，請參閱探索[使用 Azure PowerShell 的 Azure 磁碟加密 - 第 2 部分](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2/)</span><span class="sxs-lookup"><span data-stu-id="cd6af-208">For more advanced scenarios, see Explore [Azure Disk Encryption with Azure PowerShell – Part 2](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2/)</span></span>

<span data-ttu-id="cd6af-209">**問：**Azure 磁碟加密支援 Azure PowerShell 的什麼版本？</span><span class="sxs-lookup"><span data-stu-id="cd6af-209">**Q:** What version of Azure PowerShell is supported by Azure Disk Encryption?</span></span>

<span data-ttu-id="cd6af-210">**答：**使用 hello 最新版本的 Azure PowerShell SDK 版本 tooconfigure Azure 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="cd6af-210">**A:** Use hello latest version of Azure PowerShell SDK version tooconfigure Azure Disk Encryption.</span></span> <span data-ttu-id="cd6af-211">下載 hello 最新版本[Azure PowerShell](https://github.com/Azure/azure-powershell/releases)。</span><span class="sxs-lookup"><span data-stu-id="cd6af-211">Download hello latest version of [Azure PowerShell](https://github.com/Azure/azure-powershell/releases).</span></span> <span data-ttu-id="cd6af-212">Azure SDK version 1.1.0 版「不」支援 Azure 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="cd6af-212">Azure Disk Encryption is NOT supported by Azure SDK version 1.1.0.</span></span>

> [!NOTE]
> <span data-ttu-id="cd6af-213">hello Linux 的 Azure 磁碟加密預覽功能延伸模組已被取代。</span><span class="sxs-lookup"><span data-stu-id="cd6af-213">hello Linux Azure disk encryption preview extension is deprecated.</span></span> <span data-ttu-id="cd6af-214">如需詳細資訊，請參閱 toodocumentation[這裡](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/12/deprecating-azure-disk-encryption-preview-extension-for-linux-iaas-vms/)</span><span class="sxs-lookup"><span data-stu-id="cd6af-214">For details, refer toodocumentation [here](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/12/deprecating-azure-disk-encryption-preview-extension-for-linux-iaas-vms/)</span></span>

<span data-ttu-id="cd6af-215">**問：**是否可以在我的自訂 Linux 映像上套用 Azure 磁碟加密？</span><span class="sxs-lookup"><span data-stu-id="cd6af-215">**Q:** Can I apply Azure disk encryption on my custom Linux image?</span></span>

<span data-ttu-id="cd6af-216">**答：**無法在您的自訂 Linux 映像上套用 Azure 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="cd6af-216">**A:** You cannot apply Azure disk encryption on your custom Linux image.</span></span> <span data-ttu-id="cd6af-217">我們針對上述叫出 hello 支援散發版本支援只有 hello 圖庫 Linux 映像。</span><span class="sxs-lookup"><span data-stu-id="cd6af-217">We support only hello gallery Linux images for hello supported distros called out above.</span></span> <span data-ttu-id="cd6af-218">目前不支援自訂 Linux 映像</span><span class="sxs-lookup"><span data-stu-id="cd6af-218">We do not support custom Linux images currently</span></span>

<span data-ttu-id="cd6af-219">**問：**可以將套用更新 tooa Linux Red Hat VM 使用 Yum 更新嗎？</span><span class="sxs-lookup"><span data-stu-id="cd6af-219">**Q:** Can I apply updates tooa Linux Red Hat VM using Yum update?</span></span>

<span data-ttu-id="cd6af-220">**答：**是，您可以執行更新和/或修補遵循[這裡](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/13/applying-updates-to-a-encrypted-azure-iaas-red-hat-vm-using-yum-update/)所述之指引的 Red Hat Linnux VM</span><span class="sxs-lookup"><span data-stu-id="cd6af-220">**A:** Yes, you can perform update and or patch a Red Hat Linnux VM following guidance documented [here](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/13/applying-updates-to-a-encrypted-azure-iaas-red-hat-vm-using-yum-update/)</span></span>

<span data-ttu-id="cd6af-221">**問：**其中可以移 tooask 問題或提供意見反應</span><span class="sxs-lookup"><span data-stu-id="cd6af-221">**Q:** Where can I go tooask question or provide feedback</span></span>

<span data-ttu-id="cd6af-222">**答：**詢問問題或意見反應 hello Azure 磁碟加密論壇，您可以提供[這裡](https://social.msdn.microsoft.com/Forums/home?forum=AzureDiskEncryption)</span><span class="sxs-lookup"><span data-stu-id="cd6af-222">**A:** You can provide ask questions or feedback on hello Azure disk encryption forum [here](https://social.msdn.microsoft.com/Forums/home?forum=AzureDiskEncryption)</span></span>

## <a name="see-also"></a><span data-ttu-id="cd6af-223">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cd6af-223">See also</span></span>
<span data-ttu-id="cd6af-224">在本文件中，您學更 hello 最常見的問題相關的 tooAzure 磁碟加密，如需有關這項服務，並讀取其功能：</span><span class="sxs-lookup"><span data-stu-id="cd6af-224">In this document, you learned more about hello most frequent questions related tooAzure disk encryption, for more information about this service and its capability read:</span></span>

- [<span data-ttu-id="cd6af-225">在 Azure 資訊安全中心套用磁碟加密</span><span class="sxs-lookup"><span data-stu-id="cd6af-225">Apply disk encryption in Azure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [<span data-ttu-id="cd6af-226">加密 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="cd6af-226">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [<span data-ttu-id="cd6af-227">Azure 資料靜態加密</span><span class="sxs-lookup"><span data-stu-id="cd6af-227">Azure Data Encryption-at-Rest</span></span>](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)