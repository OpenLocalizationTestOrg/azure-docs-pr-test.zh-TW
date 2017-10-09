---
title: "在 Azure 資訊安全中心 aaaApply 磁碟加密 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 適用於磁碟加密 * *。"
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
ms.openlocfilehash: cd803f1120018c5c86da91186eec1e59d425ede7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apply-disk-encryption-in-azure-security-center"></a><span data-ttu-id="62917-103">在 Azure 資訊安全中心中套用磁碟加密</span><span class="sxs-lookup"><span data-stu-id="62917-103">Apply disk encryption in Azure Security Center</span></span>
<span data-ttu-id="62917-104">如果您有未使用 Azure 磁碟加密進行加密的 Windows 或 Linux VM 磁碟，Azure 資訊安全中心會建議您套用磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="62917-104">Azure Security Center recommends that you apply disk encryption if you have Windows or Linux VM disks that are not encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="62917-105">磁碟加密可讓您替 Windows 和 Linux IaaS VM 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="62917-105">Disk Encryption lets you encrypt your Windows and Linux IaaS VM disks.</span></span>  <span data-ttu-id="62917-106">加密是建議使用 hello OS 和 VM 上的資料磁碟區。</span><span class="sxs-lookup"><span data-stu-id="62917-106">Encryption is recommended for both hello OS and data volumes on your VM.</span></span>

<span data-ttu-id="62917-107">磁碟加密使用 hello 業界標準[BitLocker](https://technet.microsoft.com/library/cc732774.aspx)功能的 Windows 和 hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux 的功能。</span><span class="sxs-lookup"><span data-stu-id="62917-107">Disk Encryption uses hello industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux.</span></span> <span data-ttu-id="62917-108">這些功能會提供作業系統，而且資料加密 toohelp 保護並保護您的資料符合您組織的安全性和相容性的承諾。</span><span class="sxs-lookup"><span data-stu-id="62917-108">These features provide OS and data encryption toohelp protect and safeguard your data and meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="62917-109">磁碟加密與整合[Azure 金鑰保存庫](https://azure.microsoft.com/documentation/services/key-vault/)toohelp 您控制，和管理您金鑰保存庫的訂用帳戶，同時確保 hello VM 磁碟中的所有資料會留在您都加密中的hello磁碟加密金鑰和密碼[Azure 儲存體](https://azure.microsoft.com/documentation/services/storage/)。</span><span class="sxs-lookup"><span data-stu-id="62917-109">Disk Encryption is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp you control and manage hello disk encryption keys and secrets in your Key Vault subscription, while ensuring that all data in hello VM disks are encrypted at rest in your [Azure Storage](https://azure.microsoft.com/documentation/services/storage/).</span></span>

> [!NOTE]
> <span data-ttu-id="62917-110">支援下列 Windows 伺服器作業系統-Windows Server 2008 R2、 Windows Server 2012 和 Windows Server 2012 R2 的 hello azure 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="62917-110">Azure Disk Encryption is supported on hello following Windows server operating systems - Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span> <span data-ttu-id="62917-111">磁碟加密支援下列 Linux 伺服器作業系統-Ubuntu、 CentOS、 SUSE 和 SUSE Linux Enterprise Server (SLES) hello。</span><span class="sxs-lookup"><span data-stu-id="62917-111">Disk encryption is supported on hello following Linux server operating systems - Ubuntu, CentOS, SUSE, and SUSE Linux Enterprise Server (SLES).</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="62917-112">實作 hello 建議</span><span class="sxs-lookup"><span data-stu-id="62917-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="62917-113">在 hello**建議**刀鋒視窗中，選取**套用磁碟加密**。</span><span class="sxs-lookup"><span data-stu-id="62917-113">In hello **Recommendations** blade, select **Apply disk encryption**.</span></span>
2. <span data-ttu-id="62917-114">在 hello**套用磁碟加密**刀鋒視窗中，您會看到一份磁碟加密建議您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="62917-114">In hello **Apply disk encryption** blade, you see a list of VMs for which Disk Encryption is recommended.</span></span>
3. <span data-ttu-id="62917-115">請遵循 hello 指示 tooapply 加密 toothese Vm。</span><span class="sxs-lookup"><span data-stu-id="62917-115">Follow hello instructions tooapply encryption toothese VMs.</span></span>

![][1]

<span data-ttu-id="62917-116">tooencrypt 已經由資訊安全中心識別為需要加密的 Azure 虛擬機器，我們建議 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="62917-116">tooencrypt Azure Virtual Machines that have been identified by Security Center as needing encryption, we recommend hello following steps:</span></span>

* <span data-ttu-id="62917-117">安裝並設定 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="62917-117">Install and configure Azure PowerShell.</span></span> <span data-ttu-id="62917-118">這可讓您 toorun hello PowerShell 命令需要的 tooset hello 必要條件需要 tooencrypt Azure 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="62917-118">This enables you toorun hello PowerShell commands required tooset up hello prerequisites required tooencrypt Azure Virtual Machines.</span></span>
* <span data-ttu-id="62917-119">取得並執行 hello Azure 磁碟加密必要條件 Azure PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="62917-119">Obtain and run hello Azure Disk Encryption Prerequisites Azure PowerShell script.</span></span>
* <span data-ttu-id="62917-120">加密虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="62917-120">Encrypt your virtual machines.</span></span>

<span data-ttu-id="62917-121">[加密 Azure 虛擬機器](security-center-disk-encryption.md)逐步引導您完成這些步驟。</span><span class="sxs-lookup"><span data-stu-id="62917-121">[Encrypt an Azure Virtual Machine](security-center-disk-encryption.md) walks you through these steps.</span></span>  <span data-ttu-id="62917-122">本主題假設您使用 Windows 10 做 hello 用戶端電腦，您可以從此處設定磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="62917-122">This topic assumes you are using Windows 10 as hello client machine from which you configure disk encryption.</span></span>

<span data-ttu-id="62917-123">有許多方法可以用於 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="62917-123">There are many approaches that can be used for Azure Virtual Machines.</span></span> <span data-ttu-id="62917-124">如果您已精通 Azure PowerShell 或 Azure CLI 中，您可能偏好 toouse 替代方式。</span><span class="sxs-lookup"><span data-stu-id="62917-124">If you are already well-versed in Azure PowerShell or Azure CLI, then you may prefer toouse alternate approaches.</span></span> <span data-ttu-id="62917-125">toolearn 有關這些其他方法，請參閱[Azure 磁碟加密](../security/azure-security-disk-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="62917-125">toolearn about these other approaches, see [Azure disk encryption](../security/azure-security-disk-encryption.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="62917-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="62917-126">See also</span></span>
<span data-ttu-id="62917-127">這份文件範例說明了如何 tooimplement 會 hello 資訊安全中心建議 」 套用磁碟加密 」。</span><span class="sxs-lookup"><span data-stu-id="62917-127">This document showed you how tooimplement hello Security Center recommendation "Apply disk encryption."</span></span> <span data-ttu-id="62917-128">toolearn 進一步了解磁碟加密，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="62917-128">toolearn more about disk encryption, see hello following:</span></span>

* <span data-ttu-id="62917-129">[使用 Azure 金鑰保存庫的加密和金鑰管理](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/)（視訊、 36 min 39 秒）-深入了解如何 toouse 磁碟加密管理的 IaaS Vm 和 Azure 金鑰保存庫 toohelp 保護，並保護您的資料。</span><span class="sxs-lookup"><span data-stu-id="62917-129">[Encryption and key management with Azure Key Vault](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (video, 36 min 39 sec) -- Learn how toouse disk encryption management for IaaS VMs and Azure Key Vault toohelp protect and safeguard your data.</span></span>
* <span data-ttu-id="62917-130">[加密 Azure 虛擬機器](security-center-disk-encryption.md)（文件）-深入了解如何 tooencrypt Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="62917-130">[Encrypt an Azure Virtual Machine](security-center-disk-encryption.md) (document) -- Learn how tooencrypt Azure Virtual Machines.</span></span>
* <span data-ttu-id="62917-131">[Azure 磁碟加密](../security/azure-security-disk-encryption.md)（文件）-深入了解如何 tooenable 磁碟適用於 Windows 和 Linux Vm 的加密。</span><span class="sxs-lookup"><span data-stu-id="62917-131">[Azure disk encryption](../security/azure-security-disk-encryption.md) (document) -- Learn how tooenable disk encryption for Windows and Linux VMs.</span></span>

<span data-ttu-id="62917-132">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="62917-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="62917-133">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 安全性原則。</span><span class="sxs-lookup"><span data-stu-id="62917-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="62917-134">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="62917-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="62917-135">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="62917-135">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="62917-136">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="62917-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="62917-137">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="62917-137">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="62917-138">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="62917-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png
