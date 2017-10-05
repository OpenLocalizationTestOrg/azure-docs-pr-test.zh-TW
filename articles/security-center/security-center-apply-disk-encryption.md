---
title: "在 Azure 資訊安全中心中套用磁碟加密 | Microsoft Docs"
description: "本文件說明如何實作 Azure 資訊安全中心建議的「套用磁碟加密」。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 6cc7824a-8d6b-4a5f-ab40-e3bbaebc4a91
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 67cff664f3723b2194ecd1519729cca17069d07f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="apply-disk-encryption-in-azure-security-center"></a><span data-ttu-id="1dc16-103">在 Azure 資訊安全中心中套用磁碟加密</span><span class="sxs-lookup"><span data-stu-id="1dc16-103">Apply disk encryption in Azure Security Center</span></span>
<span data-ttu-id="1dc16-104">如果您有未使用 Azure 磁碟加密進行加密的 Windows 或 Linux VM 磁碟，Azure 資訊安全中心會建議您套用磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="1dc16-104">Azure Security Center recommends that you apply disk encryption if you have Windows or Linux VM disks that are not encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="1dc16-105">磁碟加密可讓您替 Windows 和 Linux IaaS VM 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="1dc16-105">Disk Encryption lets you encrypt your Windows and Linux IaaS VM disks.</span></span>  <span data-ttu-id="1dc16-106">建議您的 VM 上的作業系統和資料磁碟區都進行加密。</span><span class="sxs-lookup"><span data-stu-id="1dc16-106">Encryption is recommended for both the OS and data volumes on your VM.</span></span>

<span data-ttu-id="1dc16-107">磁碟加密使用 Windows 的業界標準 [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) 功能和 Linux 的 [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt)功能。</span><span class="sxs-lookup"><span data-stu-id="1dc16-107">Disk Encryption uses the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux.</span></span> <span data-ttu-id="1dc16-108">這些功能為 OS 和資料提供加密來協助保護資料安全，以符合您的組織安全性和合規性承諾。</span><span class="sxs-lookup"><span data-stu-id="1dc16-108">These features provide OS and data encryption to help protect and safeguard your data and meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="1dc16-109">磁碟加密與 [Azure 金鑰保存庫](https://azure.microsoft.com/documentation/services/key-vault/)整合，可幫助您控制和管理您的金鑰保存庫訂用帳戶中的磁碟加密金鑰和密碼，同時確保 VM 磁碟中的所有資料會在您的 [Azure 儲存體](https://azure.microsoft.com/documentation/services/storage/)中輕鬆加密。</span><span class="sxs-lookup"><span data-stu-id="1dc16-109">Disk Encryption is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) to help you control and manage the disk encryption keys and secrets in your Key Vault subscription, while ensuring that all data in the VM disks are encrypted at rest in your [Azure Storage](https://azure.microsoft.com/documentation/services/storage/).</span></span>

> [!NOTE]
> <span data-ttu-id="1dc16-110">下列 Windows 伺服器作業系統支援 Azure 磁碟加密 - Windows Server 2008 R2、Windows Server 2012 和 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="1dc16-110">Azure Disk Encryption is supported on the following Windows server operating systems - Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span> <span data-ttu-id="1dc16-111">下列 Linux 伺服器作業系統支援磁碟加密 - Ubuntu、CentOS、SUSE 和 SUSE Linux Enterprise Server (SLES)。</span><span class="sxs-lookup"><span data-stu-id="1dc16-111">Disk encryption is supported on the following Linux server operating systems - Ubuntu, CentOS, SUSE, and SUSE Linux Enterprise Server (SLES).</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="1dc16-112">實作建議</span><span class="sxs-lookup"><span data-stu-id="1dc16-112">Implement the recommendation</span></span>
1. <span data-ttu-id="1dc16-113">在 [建議] 刀鋒視窗中，選取 [套用磁碟加密]。</span><span class="sxs-lookup"><span data-stu-id="1dc16-113">In the **Recommendations** blade, select **Apply disk encryption**.</span></span>
2. <span data-ttu-id="1dc16-114">在 [套用磁碟加密]  刀鋒視窗中，您會看到建議進行磁碟加密的 VM 清單。</span><span class="sxs-lookup"><span data-stu-id="1dc16-114">In the **Apply disk encryption** blade, you see a list of VMs for which Disk Encryption is recommended.</span></span>
3. <span data-ttu-id="1dc16-115">依照指示將加密套用至這些 VM。</span><span class="sxs-lookup"><span data-stu-id="1dc16-115">Follow the instructions to apply encryption to these VMs.</span></span>

![][1]

<span data-ttu-id="1dc16-116">若要加密已由資訊安全中心識別為需要加密的 Azure 虛擬機器，建議您執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="1dc16-116">To encrypt Azure Virtual Machines that have been identified by Security Center as needing encryption, we recommend the following steps:</span></span>

* <span data-ttu-id="1dc16-117">安裝並設定 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="1dc16-117">Install and configure Azure PowerShell.</span></span> <span data-ttu-id="1dc16-118">這可讓您執行必要的 PowerShell 命令，以便設定用來加密 Azure 虛擬機器的必要條件。</span><span class="sxs-lookup"><span data-stu-id="1dc16-118">This enables you to run the PowerShell commands required to set up the prerequisites required to encrypt Azure Virtual Machines.</span></span>
* <span data-ttu-id="1dc16-119">取得並執行 Azure 磁碟加密先決條件 Azure PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1dc16-119">Obtain and run the Azure Disk Encryption Prerequisites Azure PowerShell script.</span></span>
* <span data-ttu-id="1dc16-120">加密虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1dc16-120">Encrypt your virtual machines.</span></span>

<span data-ttu-id="1dc16-121">[加密 Azure 虛擬機器](security-center-disk-encryption.md)逐步引導您完成這些步驟。</span><span class="sxs-lookup"><span data-stu-id="1dc16-121">[Encrypt an Azure Virtual Machine](security-center-disk-encryption.md) walks you through these steps.</span></span>  <span data-ttu-id="1dc16-122">本主題假設您使用 Windows 10 做為用戶端電腦，並從中設定磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="1dc16-122">This topic assumes you are using Windows 10 as the client machine from which you configure disk encryption.</span></span>

<span data-ttu-id="1dc16-123">有許多方法可以用於 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1dc16-123">There are many approaches that can be used for Azure Virtual Machines.</span></span> <span data-ttu-id="1dc16-124">如果您已經很熟悉 Azure PowerShell 或 Azure CLI，可能會想要使用其他方法。</span><span class="sxs-lookup"><span data-stu-id="1dc16-124">If you are already well-versed in Azure PowerShell or Azure CLI, then you may prefer to use alternate approaches.</span></span> <span data-ttu-id="1dc16-125">若要深入了解其他這些方法，請參閱 [Azure 磁碟加密](../security/azure-security-disk-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="1dc16-125">To learn about these other approaches, see [Azure disk encryption](../security/azure-security-disk-encryption.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="1dc16-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1dc16-126">See also</span></span>
<span data-ttu-id="1dc16-127">本文件說明如何實作 Azure 資訊安全中心建議的「套用磁碟加密」。</span><span class="sxs-lookup"><span data-stu-id="1dc16-127">This document showed you how to implement the Security Center recommendation "Apply disk encryption."</span></span> <span data-ttu-id="1dc16-128">若要深入了解磁碟加密，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="1dc16-128">To learn more about disk encryption, see the following:</span></span>

* <span data-ttu-id="1dc16-129">[Azure 金鑰保存庫的加密和金鑰管理](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (影片，36 分 39 秒) -- 了解如何使用 IaaS VM 和 Azure 金鑰保存庫的磁碟加密管理功能，協助保護您的資料。</span><span class="sxs-lookup"><span data-stu-id="1dc16-129">[Encryption and key management with Azure Key Vault](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (video, 36 min 39 sec) -- Learn how to use disk encryption management for IaaS VMs and Azure Key Vault to help protect and safeguard your data.</span></span>
* <span data-ttu-id="1dc16-130">[加密 Azure 虛擬機器](security-center-disk-encryption.md) (文件) - 了解如何加密 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1dc16-130">[Encrypt an Azure Virtual Machine](security-center-disk-encryption.md) (document) -- Learn how to encrypt Azure Virtual Machines.</span></span>
* <span data-ttu-id="1dc16-131">[Azure 磁碟加密](../security/azure-security-disk-encryption.md) (文件) -- 了解如何為 Windows 和 Linux VM 啟用磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="1dc16-131">[Azure disk encryption](../security/azure-security-disk-encryption.md) (document) -- Learn how to enable disk encryption for Windows and Linux VMs.</span></span>

<span data-ttu-id="1dc16-132">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="1dc16-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="1dc16-133">[設定 Azure 資訊安全中心的安全性原則](security-center-policies.md) -- 了解如何設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="1dc16-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="1dc16-134">[Azure 資訊安全中心的安全性健康狀態監視](security-center-monitoring.md) -- 了解如何監視 Azure 資源的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="1dc16-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="1dc16-135">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) -- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="1dc16-135">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="1dc16-136">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助您保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="1dc16-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="1dc16-137">[Azure 安全性中心常見問題集](security-center-faq.md) -- 尋找使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="1dc16-137">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="1dc16-138">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="1dc16-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png
