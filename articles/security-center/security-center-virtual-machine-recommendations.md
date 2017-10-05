---
title: "保護 Azure 資訊安全中心內的虛擬機器 | Microsoft Docs"
description: "本文件說明可協助您保護虛擬機器及遵守安全性原則的 Azure 資訊安全中心建議。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 47fa1f76-683d-4230-b4ed-d123fef9a3e8
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: 2b7f22e5c27f5ba2123d8a1d913887191a536740
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="protecting-your-virtual-machines-in-azure-security-center"></a><span data-ttu-id="fa9d1-103">保護 Azure 資訊安全中心內的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="fa9d1-103">Protecting your virtual machines in Azure Security Center</span></span>
<span data-ttu-id="fa9d1-104">「Azure 資訊安全中心」會分析 Azure 資源的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="fa9d1-105">當資訊安全中心發現潛在的安全性弱點時，它會建立可引導您完成所需控制之設定程序的建議。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="fa9d1-106">這些建議適用於下列 Azure 資源類型︰虛擬機器 (VM)、網路、SQL 和應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="fa9d1-107">本文說明適用於 VM 的建議。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-107">This article addresses recommendations that apply to VMs.</span></span>  <span data-ttu-id="fa9d1-108">VM 建議圍繞在資料收集、套用系統更新、佈建反惡意程式碼、加密 VM 磁碟等等。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-108">VM recommendations center around data collection, applying system updates, provisioning antimalware, encrypting your VM disks, and more.</span></span>  <span data-ttu-id="fa9d1-109">請使用下表做為參考，以協助您了解可用的 VM 建議，以及如果套用建議，每一個建議將產生的作用。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-109">Use the table below as a reference to help you understand the available VM recommendations and what each one will do if you apply it.</span></span>

## <a name="available-vm-recommendations"></a><span data-ttu-id="fa9d1-110">可用的 VM 建議</span><span class="sxs-lookup"><span data-stu-id="fa9d1-110">Available VM recommendations</span></span>
| <span data-ttu-id="fa9d1-111">建議</span><span class="sxs-lookup"><span data-stu-id="fa9d1-111">Recommendation</span></span> | <span data-ttu-id="fa9d1-112">說明</span><span class="sxs-lookup"><span data-stu-id="fa9d1-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="fa9d1-113">啟用訂用帳戶的資料收集</span><span class="sxs-lookup"><span data-stu-id="fa9d1-113">Enable data collection for subscriptions</span></span>](security-center-enable-data-collection.md) |<span data-ttu-id="fa9d1-114">建議您為每個訂用帳戶和訂用帳戶中的所有虛擬機器 (VM) 開啟安全性原則中的 [資料收集]。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-114">Recommends that you turn on data collection in the security policy for each of your subscriptions and all virtual machines (VMs) in your subscriptions.</span></span> |
| [<span data-ttu-id="fa9d1-115">為 Azure 儲存體帳戶啟用加密</span><span class="sxs-lookup"><span data-stu-id="fa9d1-115">Enable encryption for Azure Storage Account</span></span>](security-center-enable-encryption-for-storage-account.md) | <span data-ttu-id="fa9d1-116">建議您為待用資料啟用「Azure 儲存體服務加密」。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-116">Recommends that you enable Azure Storage Service Encryption for data at rest.</span></span> <span data-ttu-id="fa9d1-117">「儲存體服務加密」(SSE) 會在資料被寫入 Azure 儲存體時加密資料，並於擷取資料之前將其解密。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-117">Storage Service Encryption (SSE) works by encrypting the data when it is written to Azure storage and decrypts before retrieval.</span></span> <span data-ttu-id="fa9d1-118">SSE 目前僅適用於 Azure Blob 服務，可用於區塊 Blob、分頁 Blob 和附加 Blob。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-118">SSE is currently available only for the Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span> <span data-ttu-id="fa9d1-119">若要深入了解，請參閱[待用資料的儲存體服務加密](../storage/common/storage-service-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-119">To learn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span></br><span data-ttu-id="fa9d1-120">只有在 Resource Manager 儲存體帳戶上才支援 SSE。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-120">SSE is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="fa9d1-121">目前不支援傳統儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-121">Classic storage accounts are currently not supported.</span></span> <span data-ttu-id="fa9d1-122">若要了解傳統和 Resource Manager 部署模型，請參閱 [Azure 部署模型](../azure-classic-rm.md)。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-122">To understand the classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span> |
| [<span data-ttu-id="fa9d1-123">修復 OS 弱點</span><span class="sxs-lookup"><span data-stu-id="fa9d1-123">Remediate OS vulnerabilities</span></span>](security-center-remediate-os-vulnerabilities.md) |<span data-ttu-id="fa9d1-124">建議您讓作業系統組態符合建議的設定規則，例如不允許儲存密碼。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-124">Recommends that you align your OS configurations with the recommended configuration rules, e.g. do not allow passwords to be saved.</span></span> |
| [<span data-ttu-id="fa9d1-125">套用系統更新</span><span class="sxs-lookup"><span data-stu-id="fa9d1-125">Apply system updates</span></span>](security-center-apply-system-updates.md) |<span data-ttu-id="fa9d1-126">建議您將遺漏的系統安全性與重大更新部署到 VM。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-126">Recommends that you deploy missing system security and critical updates to VMs.</span></span> |
| [<span data-ttu-id="fa9d1-127">套用 Just-in-Time 網路存取控制</span><span class="sxs-lookup"><span data-stu-id="fa9d1-127">Apply a Just-In-Time network access control</span></span>](security-center-just-in-time.md) | <span data-ttu-id="fa9d1-128">建議您套用 Just-in-Time 虛擬機器存取。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-128">Recommends that you apply just in time VM access.</span></span> <span data-ttu-id="fa9d1-129">Just-in-Time 為預覽功能，由資訊安全中心的標準層提供。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-129">The just in time feature is in preview and available on the Standard tier of Security Center.</span></span> <span data-ttu-id="fa9d1-130">若要深入了解資訊安全中心的定價層，請參閱[價格](security-center-pricing.md)。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-130">See [Pricing](security-center-pricing.md) to learn more about Security Center's pricing tiers.</span></span> |
| [<span data-ttu-id="fa9d1-131">在系統更新之後重新開機</span><span class="sxs-lookup"><span data-stu-id="fa9d1-131">Reboot after system updates</span></span>](security-center-apply-system-updates.md#reboot-after-system-updates) |<span data-ttu-id="fa9d1-132">建議您重新啟動 VM 以完成套用系統更新的程序。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-132">Recommends that you reboot a VM to complete the process of applying system updates.</span></span> |
| [<span data-ttu-id="fa9d1-133">安裝端點保護</span><span class="sxs-lookup"><span data-stu-id="fa9d1-133">Install Endpoint Protection</span></span>](security-center-install-endpoint-protection.md) |<span data-ttu-id="fa9d1-134">建議您將反惡意程式碼程式佈建到 VM (僅適用於 Windows VM)。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-134">Recommends that you provision antimalware programs to VMs (Windows VMs only).</span></span> |
| [<span data-ttu-id="fa9d1-135">解決端點保護健全狀況警示</span><span class="sxs-lookup"><span data-stu-id="fa9d1-135">Resolve Endpoint Protection health alerts</span></span>](security-center-resolve-endpoint-protection-health-alerts.md) |<span data-ttu-id="fa9d1-136">建議您先解決端點保護失敗。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-136">Recommends that you resolve endpoint protection failures.</span></span> |
| [<span data-ttu-id="fa9d1-137">啟用 VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="fa9d1-137">Enable VM Agent</span></span>](security-center-enable-vm-agent.md) |<span data-ttu-id="fa9d1-138">可讓您查看哪些 VM 需要「VM 代理程式」。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-138">Enables you to see which VMs require the VM Agent.</span></span> <span data-ttu-id="fa9d1-139">為了佈建修補程式掃描、基準掃描及反惡意程式碼程式，必須在 VM 上安裝「VM 代理程式」。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-139">The VM Agent must be installed on VMs in order to provision patch scanning, baseline scanning, and antimalware programs.</span></span> <span data-ttu-id="fa9d1-140">預設會為從 Azure Marketplace 部署的 VM 安裝「VM 代理程式」。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-140">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span></span> <span data-ttu-id="fa9d1-141">如需如何安裝 VM 代理程式的相關資訊，請參閱 [VM 代理程式和擴充功能 – 第 2 部分](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) 。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-141">The article [VM Agent and Extensions – Part 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span></span> |
| [<span data-ttu-id="fa9d1-142">套用磁碟加密</span><span class="sxs-lookup"><span data-stu-id="fa9d1-142">Apply disk encryption</span></span>](security-center-apply-disk-encryption.md) |<span data-ttu-id="fa9d1-143">建議您使用 Azure 磁碟加密來加密您的 VM 磁碟 (Windows 和 Linux VM)。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-143">Recommends that you encrypt your VM disks using Azure Disk Encryption (Windows and Linux VMs).</span></span> <span data-ttu-id="fa9d1-144">建議您的 VM 上的作業系統和資料磁碟區都進行加密。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-144">Encryption is recommended for both the OS and data volumes on your VM.</span></span> |
| [<span data-ttu-id="fa9d1-145">更新作業系統版本</span><span class="sxs-lookup"><span data-stu-id="fa9d1-145">Update OS version</span></span>](security-center-update-os-version.md) |<span data-ttu-id="fa9d1-146">建議您將雲端服務的作業系統 (OS) 版本更新為作業系統系列可用的最新版本。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-146">Recommends that you update the operating system (OS) version for your Cloud Service to the most recent version available for your OS family.</span></span>  <span data-ttu-id="fa9d1-147">若要深入了解雲端服務，請參閱 [雲端服務概觀](../cloud-services/cloud-services-choose-me.md)。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-147">To learn more about Cloud Services, see the [Cloud Services overview](../cloud-services/cloud-services-choose-me.md).</span></span> |
| [<span data-ttu-id="fa9d1-148">未安裝弱點評估</span><span class="sxs-lookup"><span data-stu-id="fa9d1-148">Vulnerability assessment not installed</span></span>](security-center-vulnerability-assessment-recommendations.md) |<span data-ttu-id="fa9d1-149">建議在 VM 上安裝弱點評估解決方案。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-149">Recommends that you install a vulnerability assessment solution on your VM.</span></span> |
| [<span data-ttu-id="fa9d1-150">修復弱點</span><span class="sxs-lookup"><span data-stu-id="fa9d1-150">Remediate vulnerabilities</span></span>](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |<span data-ttu-id="fa9d1-151">可讓您查看 VM 上安裝的弱點評估解決方案所偵測到的系統和應用程式弱點。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-151">Enables you to see system and application vulnerabilities detected by the vulnerability assessment solution installed on your VM.</span></span> |

## <a name="see-also"></a><span data-ttu-id="fa9d1-152">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fa9d1-152">See also</span></span>
<span data-ttu-id="fa9d1-153">若要深入了解適用於其他 Azure 資源類型的建議，請參閱下列文章︰</span><span class="sxs-lookup"><span data-stu-id="fa9d1-153">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="fa9d1-154">保護 Azure 資訊安全中心內的應用程式</span><span class="sxs-lookup"><span data-stu-id="fa9d1-154">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="fa9d1-155">保護 Azure 資訊安全中心內的網路</span><span class="sxs-lookup"><span data-stu-id="fa9d1-155">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)
* [<span data-ttu-id="fa9d1-156">保護 Azure 資訊安全中心內的 Azure SQL 服務</span><span class="sxs-lookup"><span data-stu-id="fa9d1-156">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="fa9d1-157">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="fa9d1-157">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="fa9d1-158">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md) -- 了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-158">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="fa9d1-159">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) -- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-159">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="fa9d1-160">[Azure 資訊安全中心常見問題集](security-center-faq.md) -- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="fa9d1-160">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>