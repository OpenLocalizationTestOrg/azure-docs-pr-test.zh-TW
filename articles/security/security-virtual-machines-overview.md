---
title: "用於 Azure 虛擬機器的 Azure 安全性功能 | Microsoft Docs"
description: " 可用於 Azure 虛擬機器的核心 Azure 安全性功能概觀。 Azure VM 讓您能夠有彈性地進行虛擬化，而不需購買並維護執行 VM 的實體硬體。 "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 467b2c83-0352-4e9d-9788-c77fb400fe54
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: terrylan
ms.openlocfilehash: f1fb7f876c7dc010c03f01a4f6698ddc18da1100
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-virtual-machines-security-overview"></a><span data-ttu-id="671c5-104">Azure 虛擬機器安全性概觀</span><span class="sxs-lookup"><span data-stu-id="671c5-104">Azure Virtual Machines security overview</span></span>
<span data-ttu-id="671c5-105">您可利用 Azure 虛擬機器以敏捷的方式部署範圍廣泛的許多運算解決方案。</span><span class="sxs-lookup"><span data-stu-id="671c5-105">Azure Virtual Machines lets you deploy a wide range of computing solutions in an agile way.</span></span> <span data-ttu-id="671c5-106">利用 Microsoft Windows、Linux、Microsoft SQL Server、Oracle、IBM、SAP 與 Azure BizTalk 服務的支援，就可以在近乎所有的作業系統上，使用任何語言部署所有工作負載。</span><span class="sxs-lookup"><span data-stu-id="671c5-106">With support for Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM, SAP, and Azure BizTalk Services, you can deploy any workload and any language on nearly any operating system.</span></span>

<span data-ttu-id="671c5-107">Azure 虛擬機器讓您能夠有彈性地進行虛擬化，而不需購買並維護執行虛擬機器的實體硬體。</span><span class="sxs-lookup"><span data-stu-id="671c5-107">An Azure virtual machine gives you the flexibility of virtualization without having to buy and maintain the physical hardware that runs the virtual machine.</span></span>  <span data-ttu-id="671c5-108">您可以建置並部署您的應用程式，並保證您的資料會在我們的高度安全資料中心中受到安全的保護。</span><span class="sxs-lookup"><span data-stu-id="671c5-108">You can build and deploy your applications with the assurance that your data is protected and safe in our highly secure datacenters.</span></span>

<span data-ttu-id="671c5-109">您可以使用 Azure 建置安全性已加強且相容的解決方案：</span><span class="sxs-lookup"><span data-stu-id="671c5-109">With Azure, you can build security-enhanced, compliant solutions that:</span></span>

* <span data-ttu-id="671c5-110">保護虛擬機器抵禦病毒和惡意程式碼</span><span class="sxs-lookup"><span data-stu-id="671c5-110">Protect your virtual machines from viruses and malware</span></span>
* <span data-ttu-id="671c5-111">將敏感性資料加密</span><span class="sxs-lookup"><span data-stu-id="671c5-111">Encrypt your sensitive data</span></span>
* <span data-ttu-id="671c5-112">保護網路流量</span><span class="sxs-lookup"><span data-stu-id="671c5-112">Secure network traffic</span></span>
* <span data-ttu-id="671c5-113">識別和偵測威脅</span><span class="sxs-lookup"><span data-stu-id="671c5-113">Identify and detect threats</span></span>
* <span data-ttu-id="671c5-114">符合規範需求</span><span class="sxs-lookup"><span data-stu-id="671c5-114">Meet compliance requirements</span></span>

<span data-ttu-id="671c5-115">本文的目的是對可用於虛擬機器的 Azure 安全性功能提供核心的概觀。</span><span class="sxs-lookup"><span data-stu-id="671c5-115">The goal of this article is to provide an overview of the core Azure security features that can be used with virtual machines.</span></span> <span data-ttu-id="671c5-116">我們也會提供文章的連結，更詳細說明每個功能，以讓您深入了解。</span><span class="sxs-lookup"><span data-stu-id="671c5-116">We also provide links to articles that give details of each feature so you can learn more.</span></span>  

<span data-ttu-id="671c5-117">本文涵蓋核心 Azure 虛擬機器安全性功能︰</span><span class="sxs-lookup"><span data-stu-id="671c5-117">The core Azure Virtual Machine security capabilities to be covered in this article:</span></span>

* <span data-ttu-id="671c5-118">反惡意程式碼</span><span class="sxs-lookup"><span data-stu-id="671c5-118">Antimalware</span></span>
* <span data-ttu-id="671c5-119">硬體安全性模型</span><span class="sxs-lookup"><span data-stu-id="671c5-119">Hardware Security Module</span></span>
* <span data-ttu-id="671c5-120">虛擬機器磁碟加密</span><span class="sxs-lookup"><span data-stu-id="671c5-120">Virtual machine disk encryption</span></span>
* <span data-ttu-id="671c5-121">虛擬機器備份</span><span class="sxs-lookup"><span data-stu-id="671c5-121">Virtual machine backup</span></span>
* <span data-ttu-id="671c5-122">Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="671c5-122">Azure Site Recovery</span></span>
* <span data-ttu-id="671c5-123">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="671c5-123">Virtual networking</span></span>
* <span data-ttu-id="671c5-124">安全性原則管理和報告</span><span class="sxs-lookup"><span data-stu-id="671c5-124">Security policy management and reporting</span></span>
* <span data-ttu-id="671c5-125">法規遵循</span><span class="sxs-lookup"><span data-stu-id="671c5-125">Compliance</span></span>

## <a name="antimalware"></a><span data-ttu-id="671c5-126">反惡意程式碼</span><span class="sxs-lookup"><span data-stu-id="671c5-126">Antimalware</span></span>
<span data-ttu-id="671c5-127">運用 Azure，您可以使用來自安全性廠商 (例如 Microsoft、Symantec、Trend Micro 和 Kaspersky) 的反惡意程式碼軟體，以保護您的虛擬機器抵禦惡意檔案、廣告軟體和其他威脅。</span><span class="sxs-lookup"><span data-stu-id="671c5-127">With Azure, you can use antimalware software from security vendors such as Microsoft, Symantec, Trend Micro, and Kaspersky to protect your virtual machines from malicious files, adware, and other threats.</span></span> <span data-ttu-id="671c5-128">請參閱以下的「深入了解」一節，尋找合作夥伴解決方案上的文章。</span><span class="sxs-lookup"><span data-stu-id="671c5-128">See the Learn More section below to find articles on partner solutions.</span></span>

<span data-ttu-id="671c5-129">適用於 Azure 雲端服務和虛擬機器的 Microsoft Antimalware 是即時保護功能，有助於識別和移除病毒、間諜軟體和其他惡意軟體。</span><span class="sxs-lookup"><span data-stu-id="671c5-129">Microsoft Antimalware for Azure Cloud Services and Virtual Machines is a real-time protection capability that helps identify and remove viruses, spyware, and other malicious software.</span></span>  <span data-ttu-id="671c5-130">Microsoft Antimalware 會提供可設定的警示，在已知的惡意或垃圾軟體嘗試自行安裝或在您的 Azure 系統上執行時發出警示。</span><span class="sxs-lookup"><span data-stu-id="671c5-130">Microsoft Antimalware provides configurable alerts when known malicious or unwanted software attempts to install itself or run on your Azure systems.</span></span>

<span data-ttu-id="671c5-131">Microsoft Antimalware 是一個針對應用程式和租用戶環境所提供的單一代理程式解決方案，其設計可於無人為介入的情況下在背景中執行。</span><span class="sxs-lookup"><span data-stu-id="671c5-131">Microsoft Antimalware is a single-agent solution for applications and tenant environments, designed to run in the background without human intervention.</span></span> <span data-ttu-id="671c5-132">您可依據應用程式工作負載需求，選擇預設的基本安全性或進階的自訂組態 (包括反惡意程式碼監視) 來部署保護。</span><span class="sxs-lookup"><span data-stu-id="671c5-132">You can deploy protection based on the needs of your application workloads, with either basic secure-by-default or advanced custom configuration, including antimalware monitoring.</span></span>

<span data-ttu-id="671c5-133">當您部署並啟用 Microsoft Antimalware 時，有下列幾項核心功能可供使用：</span><span class="sxs-lookup"><span data-stu-id="671c5-133">When you deploy and enable Microsoft Antimalware, the following core features are available:</span></span>

* <span data-ttu-id="671c5-134">即時保護 - 監視雲端服務和虛擬機器上的活動，以偵測和封鎖惡意程式碼執行。</span><span class="sxs-lookup"><span data-stu-id="671c5-134">Real-time protection - monitors activity in Cloud Services and on Virtual Machines to detect and block malware execution.</span></span>
* <span data-ttu-id="671c5-135">排程掃描 - 定期執行目標掃描以偵測惡意程式碼，包括主動執行程式。</span><span class="sxs-lookup"><span data-stu-id="671c5-135">Scheduled scanning - periodically performs targeted scanning to detect malware, including actively running programs.</span></span>
* <span data-ttu-id="671c5-136">惡意程式碼補救 - 自動針對偵測到的惡意程式碼採取行動，例如刪除或隔離惡意檔案及清除惡意的登錄項目。</span><span class="sxs-lookup"><span data-stu-id="671c5-136">Malware remediation - automatically takes action on detected malware, such as deleting or quarantining malicious files and cleaning up malicious registry entries.</span></span>
* <span data-ttu-id="671c5-137">簽章更新 - 自動安裝最新的保護簽章 (病毒定義) 以確保依預定頻率維持最新的保護狀態。</span><span class="sxs-lookup"><span data-stu-id="671c5-137">Signature updates - automatically installs the latest protection signatures (virus definitions) to ensure protection is up-to-date on a pre-determined frequency.</span></span>
* <span data-ttu-id="671c5-138">Antimalware 引擎更新 – 自動更新 Microsoft Antimalware 引擎。</span><span class="sxs-lookup"><span data-stu-id="671c5-138">Antimalware Engine updates – automatically updates the Microsoft Antimalware engine.</span></span>
* <span data-ttu-id="671c5-139">Antimalware 平台更新 – 自動更新 Microsoft Antimalware 平台。</span><span class="sxs-lookup"><span data-stu-id="671c5-139">Antimalware Platform updates – automatically updates the Microsoft Antimalware platform.</span></span>
* <span data-ttu-id="671c5-140">主動保護 - 對 Azure 遙測中繼資料報告有關偵測到的威脅和可疑的資源以確保能快速回應，並可透過 Microsoft Active Protection System (MAPS) 啟用即時的同步簽章傳遞。</span><span class="sxs-lookup"><span data-stu-id="671c5-140">Active protection - reports to Azure telemetry metadata about detected threats and suspicious resources to ensure rapid response and enables real-time synchronous signature delivery through the Microsoft Active Protection System (MAPS).</span></span>
* <span data-ttu-id="671c5-141">範例報告 - 將範例提供並報告至 Microsoftt Antimalware 服務，以協助改善其服務並啟用疑難排解。</span><span class="sxs-lookup"><span data-stu-id="671c5-141">Samples reporting - provides and reports samples to the Microsoft Antimalware service to help refine the service and enable troubleshooting.</span></span>
* <span data-ttu-id="671c5-142">排除項目 – 可讓應用程式和服務管理員設定特定的檔案、處理序及磁碟機，以因應效能及/或其他原因將其從保護和掃描中排除。</span><span class="sxs-lookup"><span data-stu-id="671c5-142">Exclusions – allows application and service administrators to configure certain files, processes, and drives to exclude them from protection and scanning for performance and other reasons.</span></span>
* <span data-ttu-id="671c5-143">事件收集 -記錄作業系統事件記錄檔中反惡意程式碼服務的健康狀況、可疑的活動及其所採取的補救動作，並將這些資料收集至客戶的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="671c5-143">Antimalware event collection - records the antimalware service health, suspicious activities, and remediation actions taken in the operating system event log and collects them into the customer’s Azure Storage account.</span></span>

<span data-ttu-id="671c5-144">深入了解︰若要深入了解反惡意程式碼軟體以保護虛擬機器，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="671c5-144">Learn more: To learn more about antimalware software to protect your virtual machines, see:</span></span>

* [<span data-ttu-id="671c5-145">適用於 Azure 雲端服務和虛擬機器的 Microsoft Antimalware</span><span class="sxs-lookup"><span data-stu-id="671c5-145">Microsoft Antimalware for Azure Cloud Services and Virtual Machines</span></span>](azure-security-antimalware.md)
* [<span data-ttu-id="671c5-146">在 Azure 虛擬機器上部署反惡意程式碼解決方案</span><span class="sxs-lookup"><span data-stu-id="671c5-146">Deploying Antimalware Solutions on Azure Virtual Machines</span></span>](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [<span data-ttu-id="671c5-147">如何在 Windows VM 上安裝和設定 Trend Micro Deep Security as a Service</span><span class="sxs-lookup"><span data-stu-id="671c5-147">How to install and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>](../virtual-machines/windows/classic/install-trend.md)
* [<span data-ttu-id="671c5-148">如何在 Windows VM 上安裝和設定 Symantec Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="671c5-148">How to install and configure Symantec Endpoint Protection on a Windows VM</span></span>](../virtual-machines/windows/classic/install-symantec.md)
* [<span data-ttu-id="671c5-149">Azure Marketplace 中的安全性解決方案</span><span class="sxs-lookup"><span data-stu-id="671c5-149">Security solutions in the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/?term=security)

## <a name="hardware-security-module"></a><span data-ttu-id="671c5-150">硬體安全性模型</span><span class="sxs-lookup"><span data-stu-id="671c5-150">Hardware security Module</span></span>
<span data-ttu-id="671c5-151">您可以藉由改善金鑰安全性來增強加密和驗證保護。</span><span class="sxs-lookup"><span data-stu-id="671c5-151">Encryption and authentication protections can be enhanced by improving key security.</span></span> <span data-ttu-id="671c5-152">您可以藉由將關鍵密碼和金鑰存放在 Azure 金鑰保存庫中來簡化其管理與安全性。</span><span class="sxs-lookup"><span data-stu-id="671c5-152">You can simplify the management and security of your critical secrets and keys by storing them in Azure Key Vault.</span></span> <span data-ttu-id="671c5-153">金鑰保存庫讓您能選擇將金鑰存放在通過 FIPS 140-2 Level 2 標準認證的硬體安全性模組 (HSM) 中。</span><span class="sxs-lookup"><span data-stu-id="671c5-153">Key Vault provides the option to store your keys in hardware security modules (HSMs) certified to FIPS 140-2 Level 2 standards.</span></span> <span data-ttu-id="671c5-154">備份或 [透明資料加密](https://msdn.microsoft.com/library/bb934049.aspx) 的 SQL Server 加密金鑰都能與應用程式的任何金鑰或密碼一起存放在金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="671c5-154">Your SQL Server encryption keys for backup or [transparent data encryption](https://msdn.microsoft.com/library/bb934049.aspx) can all be stored in Key Vault with any keys or secrets from your applications.</span></span> <span data-ttu-id="671c5-155">這些受保護項目的權限和存取權是透過 [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)來管理。</span><span class="sxs-lookup"><span data-stu-id="671c5-155">Permissions and access to these protected items are managed through [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span>

<span data-ttu-id="671c5-156">深入了解：</span><span class="sxs-lookup"><span data-stu-id="671c5-156">Learn more:</span></span>

* [<span data-ttu-id="671c5-157">什麼是 Azure 金鑰保存庫？</span><span class="sxs-lookup"><span data-stu-id="671c5-157">What is Azure Key Vault?</span></span>](../key-vault/key-vault-whatis.md)
* [<span data-ttu-id="671c5-158">開始使用 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="671c5-158">Get started with Azure Key Vault</span></span>](../key-vault/key-vault-get-started.md)
* [<span data-ttu-id="671c5-159">Azure 金鑰保存庫部落格</span><span class="sxs-lookup"><span data-stu-id="671c5-159">Azure Key Vault blog</span></span>](https://blogs.technet.microsoft.com/kv/)

## <a name="virtual-machine-disk-encryption"></a><span data-ttu-id="671c5-160">虛擬機器磁碟加密</span><span class="sxs-lookup"><span data-stu-id="671c5-160">Virtual machine disk encryption</span></span>
<span data-ttu-id="671c5-161">Azure 磁碟加密是可讓您加密您的 Windows 和 Linux Azure 虛擬機器磁碟的新功能。</span><span class="sxs-lookup"><span data-stu-id="671c5-161">Azure Disk Encryption is a new capability that lets you encrypt your Windows and Linux Azure Virtual Machine disks.</span></span> <span data-ttu-id="671c5-162">Azure 磁碟加密使用 Windows 的業界標準 [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) 功能和 Linux 的 [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt) 功能，為 OS 和資料磁碟提供磁碟區加密。</span><span class="sxs-lookup"><span data-stu-id="671c5-162">Azure Disk Encryption uses the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux to provide volume encryption for the OS and the data disks.</span></span>

<span data-ttu-id="671c5-163">此解決方案與 Azure 金鑰保存庫整合，可幫助您控制和管理您的金鑰保存庫訂用帳戶中的磁碟加密金鑰和密碼，同時確保虛擬機器磁碟中的所有資料會在您的 Azure 儲存體中輕鬆加密。</span><span class="sxs-lookup"><span data-stu-id="671c5-163">The solution is integrated with Azure Key Vault to help you control and manage the disk encryption keys and secrets in your key vault subscription, while ensuring that all data in the virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="671c5-164">深入了解：</span><span class="sxs-lookup"><span data-stu-id="671c5-164">Learn more:</span></span>

* [<span data-ttu-id="671c5-165">Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密</span><span class="sxs-lookup"><span data-stu-id="671c5-165">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)
* [<span data-ttu-id="671c5-166">適用於 Linux 和 Windows 虛擬機器的 Azure 磁碟加密</span><span class="sxs-lookup"><span data-stu-id="671c5-166">Azure Disk Encryption for Linux and Windows Virtual Machines</span></span>](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview-now-available/)
* [<span data-ttu-id="671c5-167">加密虛擬機器</span><span class="sxs-lookup"><span data-stu-id="671c5-167">Encrypt a virtual machine</span></span>](../security-center/security-center-disk-encryption.md)

## <a name="virtual-machine-backup"></a><span data-ttu-id="671c5-168">虛擬機器備份</span><span class="sxs-lookup"><span data-stu-id="671c5-168">Virtual machine backup</span></span>
<span data-ttu-id="671c5-169">Azure 備份是可調式解決方案，可以不需成本地保護您的應用程式資料，以及將操作成本降到最低。</span><span class="sxs-lookup"><span data-stu-id="671c5-169">Azure Backup is a scalable solution that protects your application data with zero capital investment and minimal operating costs.</span></span> <span data-ttu-id="671c5-170">應用程式錯誤可能導致資料損毀，而人為錯誤可能會將 Bug 導入應用程式中。</span><span class="sxs-lookup"><span data-stu-id="671c5-170">Application errors can corrupt your data, and human errors can introduce bugs into your applications.</span></span> <span data-ttu-id="671c5-171">使用 Azure 備份，您執行 Windows 與 Linux 的虛擬機器會受到保護。</span><span class="sxs-lookup"><span data-stu-id="671c5-171">With Azure Backup, your virtual machines running Windows and Linux are protected.</span></span>

<span data-ttu-id="671c5-172">深入了解：</span><span class="sxs-lookup"><span data-stu-id="671c5-172">Learn more:</span></span>

* [<span data-ttu-id="671c5-173">何謂 Azure 備份？</span><span class="sxs-lookup"><span data-stu-id="671c5-173">What is Azure Backup?</span></span>](../backup/backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="671c5-174">Azure 備份學習路徑</span><span class="sxs-lookup"><span data-stu-id="671c5-174">Azure Backup Learning Path</span></span>](https://azure.microsoft.com/documentation/learning-paths/backup/)
* [<span data-ttu-id="671c5-175">Azure 備份服務 - 常見問題集</span><span class="sxs-lookup"><span data-stu-id="671c5-175">Azure Backup Service - FAQ</span></span>](../backup/backup-azure-backup-faq.md)

## <a name="azure-site-recovery"></a><span data-ttu-id="671c5-176">Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="671c5-176">Azure Site Recovery</span></span>
<span data-ttu-id="671c5-177">組織的 BCDR 策略的其中一個重要部分是，找出在計劃中和非計劃中的中斷發生時讓企業工作負載和應用程式保持啟動並執行的方法。</span><span class="sxs-lookup"><span data-stu-id="671c5-177">An important part of your organization's BCDR strategy is figuring out how to keep corporate workloads and apps up and running when planned and unplanned outages occur.</span></span> <span data-ttu-id="671c5-178">Azure Site Recovery 有助於協調工作負載和應用程式的複寫、容錯移轉及復原，因此能夠在主要位置發生故障時透過次要位置來提供工作負載和應用程式。</span><span class="sxs-lookup"><span data-stu-id="671c5-178">Azure Site Recovery helps orchestrate replication, failover, and recovery of workloads and apps so that they are available from a secondary location if your primary location goes down.</span></span>

<span data-ttu-id="671c5-179">網站復原：</span><span class="sxs-lookup"><span data-stu-id="671c5-179">Site Recovery:</span></span>

* <span data-ttu-id="671c5-180">**簡化 BCDR 策略** - Site Recovery 可讓您從單一位置輕鬆處理多個商務工作負載和應用程式的複寫、容錯移轉及復原。</span><span class="sxs-lookup"><span data-stu-id="671c5-180">**Simplifies your BCDR strategy** — Site Recovery makes it easy to handle replication, failover, and recovery of multiple business workloads and apps from a single location.</span></span> <span data-ttu-id="671c5-181">Site Recovery 會協調複寫和容錯移轉，但不會攔截應用程式資料或擁有任何相關資訊。</span><span class="sxs-lookup"><span data-stu-id="671c5-181">Site recovery orchestrates replication and failover but doesn't intercept your application data or have any information about it.</span></span>
* <span data-ttu-id="671c5-182">**提供彈性的複寫** - 使用 Site Recovery，您就可以複寫 Hyper-V 虛擬機器、VMware 虛擬機器和 Windows/Linux 實體伺服器上執行的工作負載。</span><span class="sxs-lookup"><span data-stu-id="671c5-182">**Provides flexible replication** — Using Site Recovery you can replicate workloads running on Hyper-V virtual machines, VMware virtual machines, and Windows/Linux physical servers.</span></span>
* <span data-ttu-id="671c5-183">**支援容錯移轉和復原** - Site Recovery 可提供測試用容錯移轉，既能支援災害復原演練，又不會影響生產環境。</span><span class="sxs-lookup"><span data-stu-id="671c5-183">**Supports failover and recovery** — Site Recovery provides test failovers to support disaster recovery drills without affecting production environments.</span></span> <span data-ttu-id="671c5-184">您也可以執行計劃性容錯移轉，因為是預期中的中斷，所以不會遺失任何資料；或是執行非計劃性容錯移轉，以在發生非未預期的災害時將資料損失減到最少 (取決於複寫頻率)。</span><span class="sxs-lookup"><span data-stu-id="671c5-184">You can also run planned failovers with a zero-data loss for expected outages, or unplanned failovers with minimal data loss (depending on replication frequency) for unexpected disasters.</span></span> <span data-ttu-id="671c5-185">在容錯移轉之後，您可以容錯回復到主要站台。</span><span class="sxs-lookup"><span data-stu-id="671c5-185">After failover, you can failback to your primary sites.</span></span> <span data-ttu-id="671c5-186">Site Recovery 提供了包含指令碼和 Azure 自動化作業手冊的復原計畫，以供您自訂多層式應用程式的容錯移轉和復原。</span><span class="sxs-lookup"><span data-stu-id="671c5-186">Site Recovery provides recovery plans that can include scripts and Azure automation workbooks so that you can customize failover and recovery of multi-tier applications.</span></span>
* <span data-ttu-id="671c5-187">**消除次要資料中心** - 您可以複寫至次要內部部署站台或 Azure。</span><span class="sxs-lookup"><span data-stu-id="671c5-187">**Eliminates secondary datacenter** — You can replicate to a secondary on-premises site, or to Azure.</span></span> <span data-ttu-id="671c5-188">使用 Azure 做為災害復原目的地，可排除次要站台的維護成本和複雜度。</span><span class="sxs-lookup"><span data-stu-id="671c5-188">Using Azure as a destination for disaster recovery eliminates the cost and complexity of maintaining a secondary site.</span></span> <span data-ttu-id="671c5-189">複寫的資料會儲存在 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="671c5-189">Replicated data is stored in Azure Storage.</span></span>
* <span data-ttu-id="671c5-190">**與現有 BCDR 技術整合** - Site Recovery 能夠與其他應用程式的 BCDR 功能搭配使用。</span><span class="sxs-lookup"><span data-stu-id="671c5-190">**Integrates with existing BCDR technologies** — Site Recovery partners with other application BCDR features.</span></span> <span data-ttu-id="671c5-191">例如，您可以使用 Site Recovery 來保護公司工作負載的 SQL Server 後端。</span><span class="sxs-lookup"><span data-stu-id="671c5-191">For example, you can use Site Recovery to protect the SQL Server back end of corporate workloads.</span></span> <span data-ttu-id="671c5-192">這包括原生支援 SQL Server AlwaysOn 以管理可用性群組的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="671c5-192">This includes native support for SQL Server AlwaysOn to manage the failover of availability groups.</span></span>

<span data-ttu-id="671c5-193">深入了解：</span><span class="sxs-lookup"><span data-stu-id="671c5-193">Learn more:</span></span>

* [<span data-ttu-id="671c5-194">什麼是 Azure Site Recovery？</span><span class="sxs-lookup"><span data-stu-id="671c5-194">What is Azure Site Recovery?</span></span>](../site-recovery/site-recovery-overview.md)
* [<span data-ttu-id="671c5-195">Azure Site Recovery 如何運作？</span><span class="sxs-lookup"><span data-stu-id="671c5-195">How Does Azure Site Recovery Work?</span></span>](../site-recovery/site-recovery-components.md)
* [<span data-ttu-id="671c5-196">Azure Site Recovery 保護哪些工作負載？</span><span class="sxs-lookup"><span data-stu-id="671c5-196">What Workloads are Protected by Azure Site Recovery?</span></span>](../site-recovery/site-recovery-workload.md)

## <a name="virtual-networking"></a><span data-ttu-id="671c5-197">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="671c5-197">Virtual networking</span></span>
<span data-ttu-id="671c5-198">虛擬機器需要遠端連線。</span><span class="sxs-lookup"><span data-stu-id="671c5-198">Virtual machines need network connectivity.</span></span> <span data-ttu-id="671c5-199">為了支援該需求，Azure 需要虛擬機器連接到 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="671c5-199">To support that requirement, Azure requires virtual machines to be connected to an Azure Virtual Network.</span></span> <span data-ttu-id="671c5-200">Azure 虛擬網路是以實體 Azure 網路網狀架構為基礎所建置的邏輯建構。</span><span class="sxs-lookup"><span data-stu-id="671c5-200">An Azure Virtual Network is a logical construct built on top of the physical Azure network fabric.</span></span> <span data-ttu-id="671c5-201">每個邏輯 Azure 虛擬網路都會與其他所有 Azure 虛擬網路隔離。</span><span class="sxs-lookup"><span data-stu-id="671c5-201">Each logical Azure Virtual Network is isolated from all other Azure Virtual Networks.</span></span> <span data-ttu-id="671c5-202">此隔離可協助確保其他 Microsoft Azure 客戶無法存取您部署中的網路流量。</span><span class="sxs-lookup"><span data-stu-id="671c5-202">This isolation helps insure that network traffic in your deployments is not accessible to other Microsoft Azure customers.</span></span>

<span data-ttu-id="671c5-203">深入了解：</span><span class="sxs-lookup"><span data-stu-id="671c5-203">Learn more:</span></span>

* [<span data-ttu-id="671c5-204">Azure 網路安全性概觀</span><span class="sxs-lookup"><span data-stu-id="671c5-204">Azure Network Security Overview</span></span>](security-network-overview.md)
* [<span data-ttu-id="671c5-205">虛擬網路概觀</span><span class="sxs-lookup"><span data-stu-id="671c5-205">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)
* [<span data-ttu-id="671c5-206">網路功能與企業合作夥伴關係的案例</span><span class="sxs-lookup"><span data-stu-id="671c5-206">Networking features and partnerships for Enterprise scenarios</span></span>](https://azure.microsoft.com/blog/networking-enterprise/)

## <a name="security-policy-management-and-reporting"></a><span data-ttu-id="671c5-207">安全性原則管理和報告</span><span class="sxs-lookup"><span data-stu-id="671c5-207">Security policy management and reporting</span></span>
<span data-ttu-id="671c5-208">Azure 資訊安全中心可協助您預防、偵測和回應威脅，並加強提供對 Azure 資源安全性的能見度及控制權。</span><span class="sxs-lookup"><span data-stu-id="671c5-208">Azure Security Center helps you prevent, detect, and respond to threats, and provides you increased visibility into, and control over, the security of your Azure resources.</span></span> <span data-ttu-id="671c5-209">它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。</span><span class="sxs-lookup"><span data-stu-id="671c5-209">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

<span data-ttu-id="671c5-210">Azure 資訊安全中心藉由下列方式來協助您最佳化和監視虛擬機器︰</span><span class="sxs-lookup"><span data-stu-id="671c5-210">Azure Security Center helps you optimize and monitor virtual machine security by:</span></span>

* <span data-ttu-id="671c5-211">提供虛擬機器 [安全性建議](../security-center/security-center-recommendations.md) ，例如套用系統更新、設定 ACL 端點、啟用反惡意程式碼、啟用網路安全性群組，以及套用磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="671c5-211">Providing virtual machine [security recommendations](../security-center/security-center-recommendations.md) such as apply system updates, configure ACLs endpoints, enable antimalware, enable network security groups, and apply disk encryption.</span></span>
* <span data-ttu-id="671c5-212">監視您的虛擬機器的狀態</span><span class="sxs-lookup"><span data-stu-id="671c5-212">Monitoring the state of your virtual machines</span></span>

<span data-ttu-id="671c5-213">深入了解：</span><span class="sxs-lookup"><span data-stu-id="671c5-213">Learn more:</span></span>

* [<span data-ttu-id="671c5-214">Azure 資訊安全中心簡介</span><span class="sxs-lookup"><span data-stu-id="671c5-214">Introduction to Azure Security Center</span></span>](../security-center/security-center-intro.md)
* [<span data-ttu-id="671c5-215">Azure 資訊安全中心常見問題集</span><span class="sxs-lookup"><span data-stu-id="671c5-215">Azure Security Center Frequently Asked Questions</span></span>](../security-center/security-center-faq.md)
* [<span data-ttu-id="671c5-216">Azure 資訊安全中心規劃和操作</span><span class="sxs-lookup"><span data-stu-id="671c5-216">Azure Security Center Planning and Operations</span></span>](../security-center/security-center-planning-and-operations-guide.md)

## <a name="compliance"></a><span data-ttu-id="671c5-217">法規遵循</span><span class="sxs-lookup"><span data-stu-id="671c5-217">Compliance</span></span>
<span data-ttu-id="671c5-218">Azure 虛擬機器經過 FISMA、FedRAMP、HIPAA、PCI DSS Level 1 及其他重要規範計劃認證。</span><span class="sxs-lookup"><span data-stu-id="671c5-218">Azure Virtual Machines is certified for FISMA, FedRAMP, HIPAA, PCI DSS Level 1, and other key compliance programs.</span></span> <span data-ttu-id="671c5-219">此認證可讓您自己的 Azure 應用程式更容易符合規範要求，並讓您的企業解決廣泛的國內與國際法規要求。</span><span class="sxs-lookup"><span data-stu-id="671c5-219">This certification makes it easier for your own Azure applications to meet compliance requirements and for your business to address a wide range of domestic and international regulatory requirements.</span></span>

<span data-ttu-id="671c5-220">深入了解：</span><span class="sxs-lookup"><span data-stu-id="671c5-220">Learn more:</span></span>

* [<span data-ttu-id="671c5-221">Microsoft 信任中心：法規遵循</span><span class="sxs-lookup"><span data-stu-id="671c5-221">Microsoft Trust Center: Compliance</span></span>](https://www.microsoft.com/TrustCenter/Compliance/default.aspx)
* [<span data-ttu-id="671c5-222">受信任的雲端：Microsoft Azure 安全性、隱私權及法規遵循</span><span class="sxs-lookup"><span data-stu-id="671c5-222">Trusted Cloud: Microsoft Azure Security, Privacy, and Compliance</span></span>](http://download.microsoft.com/download/1/6/0/160216AA-8445-480B-B60F-5C8EC8067FCA/WindowsAzure-SecurityPrivacyCompliance.pdf)
