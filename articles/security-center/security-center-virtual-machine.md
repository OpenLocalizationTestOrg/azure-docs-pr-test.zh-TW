---
title: "Azure 資訊安全中心和 Azure 虛擬機器 | Microsoft Docs"
description: "本文件協助您了解 Azure 資訊安全中心可如何保護您的 Azure 虛擬機器。"
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5fe5a12c-5d25-430c-9d47-df9438b1d7c5
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/24/2017
ms.author: yurid
ms.openlocfilehash: 48314788dbe4618f271f0235f106dbe15ef004b8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-security-center-and-azure-virtual-machines"></a><span data-ttu-id="27c73-103">Azure 資訊安全中心和 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="27c73-103">Azure Security Center and Azure Virtual Machines</span></span>
<span data-ttu-id="27c73-104">[Azure 資訊安全中心](https://azure.microsoft.com/services/security-center/)可協助您保護、偵測威脅並採取相應的措施。</span><span class="sxs-lookup"><span data-stu-id="27c73-104">[Azure Security Center](https://azure.microsoft.com/services/security-center/) helps you prevent, detect, and respond to threats.</span></span> <span data-ttu-id="27c73-105">它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。</span><span class="sxs-lookup"><span data-stu-id="27c73-105">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

<span data-ttu-id="27c73-106">本文說明資訊安全中心如何協助您保護 Azure 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="27c73-106">This article shows how Security Center can help you secure your Azure Virtual Machines (VM).</span></span>

## <a name="why-use-security-center"></a><span data-ttu-id="27c73-107">為何使用資訊安全中心？</span><span class="sxs-lookup"><span data-stu-id="27c73-107">Why use Security Center?</span></span>
<span data-ttu-id="27c73-108">資訊安全中心可協助您保護 Azure 中的虛擬機器資料，方法為提供虛擬機器的安全性設定可見性。</span><span class="sxs-lookup"><span data-stu-id="27c73-108">Security Center helps you safeguard virtual machine data in Azure by providing visibility into your virtual machine’s security settings.</span></span> <span data-ttu-id="27c73-109">當資訊安全中心保護您的 VM 時，可使用下列功能︰</span><span class="sxs-lookup"><span data-stu-id="27c73-109">When Security Center safeguards your VMs, the following capabilities will be available:</span></span>

* <span data-ttu-id="27c73-110">具有建議設定規則的作業系統 (OS) 安全性設定</span><span class="sxs-lookup"><span data-stu-id="27c73-110">Operating System (OS) security settings with the recommended configuration rules</span></span>
* <span data-ttu-id="27c73-111">系統安全性和重大更新遺失</span><span class="sxs-lookup"><span data-stu-id="27c73-111">System security and critical updates that are missing</span></span>
* <span data-ttu-id="27c73-112">端點保護建議</span><span class="sxs-lookup"><span data-stu-id="27c73-112">Endpoint protection recommendations</span></span>
* <span data-ttu-id="27c73-113">磁碟加密驗證</span><span class="sxs-lookup"><span data-stu-id="27c73-113">Disk encryption validation</span></span>
* <span data-ttu-id="27c73-114">弱點評估和補救</span><span class="sxs-lookup"><span data-stu-id="27c73-114">Vulnerability assessment and remediation</span></span>
* <span data-ttu-id="27c73-115">威脅偵測</span><span class="sxs-lookup"><span data-stu-id="27c73-115">Threat detection</span></span>

<span data-ttu-id="27c73-116">除了協助您保護 Azure VM，資訊安全中心也提供雲端服務、應用程式服務、虛擬網路等的安全性監視和管理功能。</span><span class="sxs-lookup"><span data-stu-id="27c73-116">In addition to helping protect your Azure VMs, Security Center also provides security monitoring and management for Cloud Services, App Services, Virtual Networks, and more.</span></span> 

> [!NOTE]
> <span data-ttu-id="27c73-117">請參閱 [Azure 資訊安全中心簡介](security-center-intro.md)一文，以深入了解 Azure 資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="27c73-117">See [Introduction to Azure Security Center](security-center-intro.md) to learn more about Azure Security Center.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="27c73-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="27c73-118">Prerequisites</span></span>
<span data-ttu-id="27c73-119">若要開始使用 Azure 資訊安全中心，您將需要知道並考慮下列項目︰</span><span class="sxs-lookup"><span data-stu-id="27c73-119">To get started with Azure Security Center, you’ll need to know and consider the following:</span></span>

* <span data-ttu-id="27c73-120">您需要 Microsoft Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="27c73-120">You must have a subscription to Microsoft Azure.</span></span> <span data-ttu-id="27c73-121">請參閱[安全性中心價格](https://azure.microsoft.com/pricing/details/security-center/)，以深入了解資訊安全中心的免費和標準層。</span><span class="sxs-lookup"><span data-stu-id="27c73-121">See [Security Center Pricing](https://azure.microsoft.com/pricing/details/security-center/) for more information on Security Center’s free and standard tiers.</span></span>
* <span data-ttu-id="27c73-122">規劃資訊安全中心的採用，請參閱 [Azure 資訊安全中心規劃和操作指南](security-center-planning-and-operations-guide.md)，以深入了解規劃和作業考量。</span><span class="sxs-lookup"><span data-stu-id="27c73-122">Plan your Security Center adoption, see [Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md) to learn more about planning and operations considerations.</span></span>
* <span data-ttu-id="27c73-123">如需作業系統可支援性的相關資訊，請參閱 [Azure 資訊安全中心常見問題集 (FAQ)](security-center-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="27c73-123">For information regarding operating system supportability, see [Azure Security Center frequently asked questions (FAQ)](security-center-faq.md).</span></span> 

## <a name="set-security-policy"></a><span data-ttu-id="27c73-124">設定安全性原則</span><span class="sxs-lookup"><span data-stu-id="27c73-124">Set security policy</span></span>
<span data-ttu-id="27c73-125">必須啟用資料收集，讓 Azure 資訊安全中心可收集其提供建議所需的資訊，以及根據您所設定之安全性原則所產生的警示。</span><span class="sxs-lookup"><span data-stu-id="27c73-125">Data collection needs to be enabled so that Azure Security Center can gather the information it needs to provide recommendations and alerts that are generated based on the security policy you configure.</span></span> <span data-ttu-id="27c73-126">在下圖中，您可以看到**資料收集**已**開啟**。</span><span class="sxs-lookup"><span data-stu-id="27c73-126">In the figure below, you can see that **Data collection** has been turned **On**.</span></span>

<span data-ttu-id="27c73-127">安全性原則定義了一組控制項，這組控制項是針對指定之訂用帳戶或資源群組內的資源所建議的。</span><span class="sxs-lookup"><span data-stu-id="27c73-127">A security policy defines the set of controls which are recommended for resources within the specified subscription or resource group.</span></span> <span data-ttu-id="27c73-128">啟用安全性原則之前，您必須啟用資料收集，資訊安全中心會收集虛擬機器的資料，以便評估其安全性狀態、提供安全性建議，並對您發出威脅警示。</span><span class="sxs-lookup"><span data-stu-id="27c73-128">Before enabling security policy, you must have data collection enabled, Security Center collects data from your virtual machines in order to assess their security state, provide security recommendations, and alert you to threats.</span></span> <span data-ttu-id="27c73-129">在資訊安全中心，您可以根據公司安全性需求，以及每個訂用帳戶中應用程式的類型或資料的敏感性，為您的 Azure 訂用帳戶或資源群組定義原則。</span><span class="sxs-lookup"><span data-stu-id="27c73-129">In Security Center, you define policies for your Azure subscriptions or resource groups according to your company’s security needs and the type of applications or sensitivity of the data in each subscription.</span></span> 

![安全性原則](./media/security-center-virtual-machine/security-center-virtual-machine-fig1.png)

> [!NOTE]
> <span data-ttu-id="27c73-131">若要深入了解每個可用的**防止原則**，請參閱[設定安全性原則](security-center-policies.md)文章。</span><span class="sxs-lookup"><span data-stu-id="27c73-131">To learn more about each **Prevention policy** available, see [Set security policies](security-center-policies.md) article.</span></span>
> 
> 

## <a name="manage-security-recommendations"></a><span data-ttu-id="27c73-132">管理安全性建議</span><span class="sxs-lookup"><span data-stu-id="27c73-132">Manage security recommendations</span></span>
<span data-ttu-id="27c73-133">資訊安全中心會分析 Azure 資源的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="27c73-133">Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="27c73-134">當資訊安全中心識別潛在的安全性弱點時，它會建立建議。</span><span class="sxs-lookup"><span data-stu-id="27c73-134">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="27c73-135">這些建議會引導您完成設定所需控制項的程序。</span><span class="sxs-lookup"><span data-stu-id="27c73-135">The recommendations guide you through the process of configuring the needed controls.</span></span>

<span data-ttu-id="27c73-136">設定安全性原則之後，「資訊安全中心」會分析您資源的安全性狀態，以識別潛在的弱點。</span><span class="sxs-lookup"><span data-stu-id="27c73-136">After setting a security policy, Security Center analyzes the security state of your resources to identify potential vulnerabilities.</span></span> <span data-ttu-id="27c73-137">系統會以表格格式顯示建議，其中每一行代表一個特定的建議。</span><span class="sxs-lookup"><span data-stu-id="27c73-137">The recommendations are shown in a table format where each line represents one particular recommendation.</span></span> <span data-ttu-id="27c73-138">下表提供 Azure VM 建議以及套用時每一個會執行之作業的一些範例。</span><span class="sxs-lookup"><span data-stu-id="27c73-138">The table below provides some examples of recommendations for Azure VMs and what each one will do if you apply it.</span></span> <span data-ttu-id="27c73-139">當您選取建議時，會提供您說明如何在資訊安全中心實作建議的資訊。</span><span class="sxs-lookup"><span data-stu-id="27c73-139">When you select a recommendation, you will be provided information that shows you how to implement the recommendation in Security Center.</span></span>

| <span data-ttu-id="27c73-140">建議</span><span class="sxs-lookup"><span data-stu-id="27c73-140">Recommendation</span></span> | <span data-ttu-id="27c73-141">說明</span><span class="sxs-lookup"><span data-stu-id="27c73-141">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="27c73-142">啟用訂用帳戶的資料收集</span><span class="sxs-lookup"><span data-stu-id="27c73-142">Enable data collection for subscriptions</span></span>](security-center-enable-data-collection.md) |<span data-ttu-id="27c73-143">建議您為每個訂用帳戶和訂用帳戶中的所有虛擬機器 (VM) 開啟安全性原則中的 [資料收集]。</span><span class="sxs-lookup"><span data-stu-id="27c73-143">Recommends that you turn on data collection in the security policy for each of your subscriptions and all virtual machines (VMs) in your subscriptions.</span></span> |
| [<span data-ttu-id="27c73-144">修復 OS 弱點</span><span class="sxs-lookup"><span data-stu-id="27c73-144">Remediate OS vulnerabilities</span></span>](security-center-remediate-os-vulnerabilities.md) |<span data-ttu-id="27c73-145">建議您讓作業系統組態符合建議的設定規則，例如不允許儲存密碼。</span><span class="sxs-lookup"><span data-stu-id="27c73-145">Recommends that you align your OS configurations with the recommended configuration rules, e.g. do not allow passwords to be saved.</span></span> |
| [<span data-ttu-id="27c73-146">套用系統更新</span><span class="sxs-lookup"><span data-stu-id="27c73-146">Apply system updates</span></span>](security-center-apply-system-updates.md) |<span data-ttu-id="27c73-147">建議您將遺漏的系統安全性與重大更新部署到 VM。</span><span class="sxs-lookup"><span data-stu-id="27c73-147">Recommends that you deploy missing system security and critical updates to VMs.</span></span> |
| [<span data-ttu-id="27c73-148">在系統更新之後重新開機</span><span class="sxs-lookup"><span data-stu-id="27c73-148">Reboot after system updates</span></span>](security-center-apply-system-updates.md#reboot-after-system-updates) |<span data-ttu-id="27c73-149">建議您重新啟動 VM 以完成套用系統更新的程序。</span><span class="sxs-lookup"><span data-stu-id="27c73-149">Recommends that you reboot a VM to complete the process of applying system updates.</span></span> |
| [<span data-ttu-id="27c73-150">安裝端點保護</span><span class="sxs-lookup"><span data-stu-id="27c73-150">Install Endpoint Protection</span></span>](security-center-install-endpoint-protection.md) |<span data-ttu-id="27c73-151">建議您將反惡意程式碼程式佈建到 VM (僅適用於 Windows VM)。</span><span class="sxs-lookup"><span data-stu-id="27c73-151">Recommends that you provision antimalware programs to VMs (Windows VMs only).</span></span> |
| [<span data-ttu-id="27c73-152">解決端點保護健全狀況警示</span><span class="sxs-lookup"><span data-stu-id="27c73-152">Resolve Endpoint Protection health alerts</span></span>](security-center-resolve-endpoint-protection-health-alerts.md) |<span data-ttu-id="27c73-153">建議您先解決端點保護失敗。</span><span class="sxs-lookup"><span data-stu-id="27c73-153">Recommends that you resolve endpoint protection failures.</span></span> |
| [<span data-ttu-id="27c73-154">啟用 VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="27c73-154">Enable VM Agent</span></span>](security-center-enable-vm-agent.md) |<span data-ttu-id="27c73-155">可讓您查看哪些 VM 需要「VM 代理程式」。</span><span class="sxs-lookup"><span data-stu-id="27c73-155">Enables you to see which VMs require the VM Agent.</span></span> <span data-ttu-id="27c73-156">為了佈建修補程式掃描、基準掃描及反惡意程式碼程式，必須在 VM 上安裝「VM 代理程式」。</span><span class="sxs-lookup"><span data-stu-id="27c73-156">The VM Agent must be installed on VMs in order to provision patch scanning, baseline scanning, and antimalware programs.</span></span> <span data-ttu-id="27c73-157">預設會為從 Azure Marketplace 部署的 VM 安裝「VM 代理程式」。</span><span class="sxs-lookup"><span data-stu-id="27c73-157">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span></span> <span data-ttu-id="27c73-158">如需如何安裝 VM 代理程式的相關資訊，請參閱 [VM 代理程式和擴充功能 – 第 2 部分](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) 。</span><span class="sxs-lookup"><span data-stu-id="27c73-158">The article [VM Agent and Extensions – Part 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span></span> |
| [<span data-ttu-id="27c73-159">套用磁碟加密</span><span class="sxs-lookup"><span data-stu-id="27c73-159">Apply disk encryption</span></span>](security-center-apply-disk-encryption.md) |<span data-ttu-id="27c73-160">建議您使用 Azure 磁碟加密來加密您的 VM 磁碟 (Windows 和 Linux VM)。</span><span class="sxs-lookup"><span data-stu-id="27c73-160">Recommends that you encrypt your VM disks using Azure Disk Encryption (Windows and Linux VMs).</span></span> <span data-ttu-id="27c73-161">建議您的 VM 上的作業系統和資料磁碟區都進行加密。</span><span class="sxs-lookup"><span data-stu-id="27c73-161">Encryption is recommended for both the OS and data volumes on your VM.</span></span> |
| [<span data-ttu-id="27c73-162">未安裝弱點評估</span><span class="sxs-lookup"><span data-stu-id="27c73-162">Vulnerability assessment not installed</span></span>](security-center-vulnerability-assessment-recommendations.md) |<span data-ttu-id="27c73-163">建議在 VM 上安裝弱點評估解決方案。</span><span class="sxs-lookup"><span data-stu-id="27c73-163">Recommends that you install a vulnerability assessment solution on your VM.</span></span> |
| [<span data-ttu-id="27c73-164">修復弱點</span><span class="sxs-lookup"><span data-stu-id="27c73-164">Remediate vulnerabilities</span></span>](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |<span data-ttu-id="27c73-165">可讓您查看 VM 上安裝的弱點評估解決方案所偵測到的系統和應用程式弱點。</span><span class="sxs-lookup"><span data-stu-id="27c73-165">Enables you to see system and application vulnerabilities detected by the vulnerability assessment solution installed on your VM.</span></span> |

> [!NOTE]
> <span data-ttu-id="27c73-166">若要深入了解相關建議，請參閱[管理安全性建議](security-center-recommendations.md)文章。</span><span class="sxs-lookup"><span data-stu-id="27c73-166">To learn more about recommendations, see [Managing security recommendations](security-center-recommendations.md) article.</span></span>
> 
> 

## <a name="monitor-security-health"></a><span data-ttu-id="27c73-167">監視安全性健康狀態</span><span class="sxs-lookup"><span data-stu-id="27c73-167">Monitor security health</span></span>
<span data-ttu-id="27c73-168">在您為訂用帳戶的資源啟用 [安全性原則](security-center-policies.md) 之後，資訊安全中心會分析您資源的安全性狀態，以找出潛在的弱點。</span><span class="sxs-lookup"><span data-stu-id="27c73-168">After you enable [security policies](security-center-policies.md) for a subscription’s resources, Security Center will analyze the security of your resources to identify potential vulnerabilities.</span></span>  <span data-ttu-id="27c73-169">您可以在 [資源安全性健全狀況] 刀鋒視窗中，檢視資源的安全性狀態及任何問題。</span><span class="sxs-lookup"><span data-stu-id="27c73-169">You can view the security state of your resources, along with any issues in the **Resource security health** blade.</span></span> <span data-ttu-id="27c73-170">當您在 [資源安全性] 健全狀況圖格中按一下 [虛擬機器] 時，會開啟 [虛擬機器] 刀鋒視窗，並提供您 VM 的建議。</span><span class="sxs-lookup"><span data-stu-id="27c73-170">When you click **Virtual machines** in the **Resource security** health tile, the **Virtual machines** blade will open with recommendations for your VMs.</span></span> 

![安全性健康狀態](./media/security-center-virtual-machine/security-center-virtual-machine-fig2.png)

## <a name="manage-and-respond-to-security-alerts"></a><span data-ttu-id="27c73-172">管理和回應安全性警示</span><span class="sxs-lookup"><span data-stu-id="27c73-172">Manage and respond to security alerts</span></span>
<span data-ttu-id="27c73-173">資訊安全中心會自動收集、分析及整合您 Azure 資源、網路和已連線的合作夥伴解決方案 (例如防火牆和端點保護解決方案) 的記錄檔資料，來偵測真正的威脅並減少誤判情形。</span><span class="sxs-lookup"><span data-stu-id="27c73-173">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions (like firewall and endpoint protection solutions), to detect real threats and reduce false positives.</span></span> <span data-ttu-id="27c73-174">藉由利用[偵測功能](security-center-detection-capabilities.md)的各種彙總，資訊安全中心能夠產生優先順序的安全性警示，協助您快速地調查問題並提供如何修正可能攻擊的建議。</span><span class="sxs-lookup"><span data-stu-id="27c73-174">By leveraging a diverse aggregation of [detection capabilities](security-center-detection-capabilities.md), Security Center is able to generate prioritized security alerts to help you quickly investigate the problem and provide recommendations for how to remediate possible attacks.</span></span>

![安全性警示](./media/security-center-virtual-machine/security-center-virtual-machine-fig3.png)

<span data-ttu-id="27c73-176">選取一個安全性警示以深入了解觸發警示的事件；如果發現項目，您需要進行一些步驟來阻止攻擊。</span><span class="sxs-lookup"><span data-stu-id="27c73-176">Select a security alert to learn more about the event(s) that triggered the alert and what, if any, steps you need to take to remediate an attack.</span></span> <span data-ttu-id="27c73-177">安全性警示會依[類型](security-center-alerts-type.md)及日期區分。</span><span class="sxs-lookup"><span data-stu-id="27c73-177">Security alerts are grouped by [type](security-center-alerts-type.md) and date.</span></span>

## <a name="see-also"></a><span data-ttu-id="27c73-178">另請參閱</span><span class="sxs-lookup"><span data-stu-id="27c73-178">See also</span></span>
<span data-ttu-id="27c73-179">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="27c73-179">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="27c73-180">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md) -- 了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="27c73-180">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="27c73-181">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) -- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="27c73-181">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="27c73-182">[Azure 資訊安全中心常見問題集](security-center-faq.md) -- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="27c73-182">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>

