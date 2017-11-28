---
title: "aaaAzure 資訊安全中心和 Azure 虛擬機器 |Microsoft 文件"
description: "這份文件可協助您 toounderstand 如何 Azure 資訊安全中心可以保護您 Azure 虛擬機器。"
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
ms.openlocfilehash: d5e80e9341263a57f3100cb032a066f037e913a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-virtual-machines"></a><span data-ttu-id="4883c-103">Azure 資訊安全中心和 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4883c-103">Azure Security Center and Azure Virtual Machines</span></span>
<span data-ttu-id="4883c-104">[Azure 資訊安全中心](https://azure.microsoft.com/services/security-center/)可協助您防止、 偵測，並回應 toothreats。</span><span class="sxs-lookup"><span data-stu-id="4883c-104">[Azure Security Center](https://azure.microsoft.com/services/security-center/) helps you prevent, detect, and respond toothreats.</span></span> <span data-ttu-id="4883c-105">它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。</span><span class="sxs-lookup"><span data-stu-id="4883c-105">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

<span data-ttu-id="4883c-106">本文說明資訊安全中心如何協助您保護 Azure 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="4883c-106">This article shows how Security Center can help you secure your Azure Virtual Machines (VM).</span></span>

## <a name="why-use-security-center"></a><span data-ttu-id="4883c-107">為何使用資訊安全中心？</span><span class="sxs-lookup"><span data-stu-id="4883c-107">Why use Security Center?</span></span>
<span data-ttu-id="4883c-108">資訊安全中心可協助您保護 Azure 中的虛擬機器資料，方法為提供虛擬機器的安全性設定可見性。</span><span class="sxs-lookup"><span data-stu-id="4883c-108">Security Center helps you safeguard virtual machine data in Azure by providing visibility into your virtual machine’s security settings.</span></span> <span data-ttu-id="4883c-109">當資訊安全中心 」 可保護您的 Vm 時，將可提供下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="4883c-109">When Security Center safeguards your VMs, hello following capabilities will be available:</span></span>

* <span data-ttu-id="4883c-110">作業系統 (OS) 安全性設定以 hello 建議組態規則</span><span class="sxs-lookup"><span data-stu-id="4883c-110">Operating System (OS) security settings with hello recommended configuration rules</span></span>
* <span data-ttu-id="4883c-111">系統安全性和重大更新遺失</span><span class="sxs-lookup"><span data-stu-id="4883c-111">System security and critical updates that are missing</span></span>
* <span data-ttu-id="4883c-112">端點保護建議</span><span class="sxs-lookup"><span data-stu-id="4883c-112">Endpoint protection recommendations</span></span>
* <span data-ttu-id="4883c-113">磁碟加密驗證</span><span class="sxs-lookup"><span data-stu-id="4883c-113">Disk encryption validation</span></span>
* <span data-ttu-id="4883c-114">弱點評估和補救</span><span class="sxs-lookup"><span data-stu-id="4883c-114">Vulnerability assessment and remediation</span></span>
* <span data-ttu-id="4883c-115">威脅偵測</span><span class="sxs-lookup"><span data-stu-id="4883c-115">Threat detection</span></span>

<span data-ttu-id="4883c-116">此外 toohelping 保護您的 Azure Vm，資訊安全中心也提供安全性監視及管理雲端服務、 應用程式服務、 虛擬網路，等等。</span><span class="sxs-lookup"><span data-stu-id="4883c-116">In addition toohelping protect your Azure VMs, Security Center also provides security monitoring and management for Cloud Services, App Services, Virtual Networks, and more.</span></span> 

> [!NOTE]
> <span data-ttu-id="4883c-117">請參閱[簡介 tooAzure 資訊安全中心](security-center-intro.md)toolearn 深入了解 Azure 資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="4883c-117">See [Introduction tooAzure Security Center](security-center-intro.md) toolearn more about Azure Security Center.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4883c-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="4883c-118">Prerequisites</span></span>
<span data-ttu-id="4883c-119">tooget 開始使用 Azure 資訊安全中心，您將需要 tooknow 並考慮下列 hello:</span><span class="sxs-lookup"><span data-stu-id="4883c-119">tooget started with Azure Security Center, you’ll need tooknow and consider hello following:</span></span>

* <span data-ttu-id="4883c-120">您必須擁有 Azure 的訂用帳戶 tooMicrosoft。</span><span class="sxs-lookup"><span data-stu-id="4883c-120">You must have a subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="4883c-121">請參閱[安全性中心價格](https://azure.microsoft.com/pricing/details/security-center/)，以深入了解資訊安全中心的免費和標準層。</span><span class="sxs-lookup"><span data-stu-id="4883c-121">See [Security Center Pricing](https://azure.microsoft.com/pricing/details/security-center/) for more information on Security Center’s free and standard tiers.</span></span>
* <span data-ttu-id="4883c-122">資訊安全中心採用計劃，請參閱[Azure 資訊安全中心規劃及作業指南](security-center-planning-and-operations-guide.md)toolearn 深入了解規劃和作業的考量。</span><span class="sxs-lookup"><span data-stu-id="4883c-122">Plan your Security Center adoption, see [Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md) toolearn more about planning and operations considerations.</span></span>
* <span data-ttu-id="4883c-123">如需作業系統可支援性的相關資訊，請參閱 [Azure 資訊安全中心常見問題集 (FAQ)](security-center-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="4883c-123">For information regarding operating system supportability, see [Azure Security Center frequently asked questions (FAQ)](security-center-faq.md).</span></span> 

## <a name="set-security-policy"></a><span data-ttu-id="4883c-124">設定安全性原則</span><span class="sxs-lookup"><span data-stu-id="4883c-124">Set security policy</span></span>
<span data-ttu-id="4883c-125">啟用，因此，該 Azure 資訊安全中心會收集 hello 資訊需要 tooprovide 建議和所產生的警示資料集合需求 toobe 根據您設定的 hello 安全性原則。</span><span class="sxs-lookup"><span data-stu-id="4883c-125">Data collection needs toobe enabled so that Azure Security Center can gather hello information it needs tooprovide recommendations and alerts that are generated based on hello security policy you configure.</span></span> <span data-ttu-id="4883c-126">Hello 在圖中，您可以看到**資料收集**已開啟**上**。</span><span class="sxs-lookup"><span data-stu-id="4883c-126">In hello figure below, you can see that **Data collection** has been turned **On**.</span></span>

<span data-ttu-id="4883c-127">安全性原則定義 hello 組 hello 指定訂用帳戶或資源群組中資源的建議使用的控制項。</span><span class="sxs-lookup"><span data-stu-id="4883c-127">A security policy defines hello set of controls which are recommended for resources within hello specified subscription or resource group.</span></span> <span data-ttu-id="4883c-128">在啟用安全性原則，您必須啟用資料收集，從您的虛擬機器中的資訊安全中心會收集資料排序 tooassess 他們的安全性狀態，提供安全性建議事項，並警示您 toothreats。</span><span class="sxs-lookup"><span data-stu-id="4883c-128">Before enabling security policy, you must have data collection enabled, Security Center collects data from your virtual machines in order tooassess their security state, provide security recommendations, and alert you toothreats.</span></span> <span data-ttu-id="4883c-129">資訊安全中心，您會定義您的 Azure 訂用帳戶或資源群組，根據 tooyour 公司的安全性需求與 hello 的應用程式的類型或大小寫的每個訂用帳戶中的 hello 資料的原則。</span><span class="sxs-lookup"><span data-stu-id="4883c-129">In Security Center, you define policies for your Azure subscriptions or resource groups according tooyour company’s security needs and hello type of applications or sensitivity of hello data in each subscription.</span></span> 

![安全性原則](./media/security-center-virtual-machine/security-center-virtual-machine-fig1.png)

> [!NOTE]
> <span data-ttu-id="4883c-131">深入了解每個 toolearn**防止原則**可用，請參閱[設定安全性原則](security-center-policies.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="4883c-131">toolearn more about each **Prevention policy** available, see [Set security policies](security-center-policies.md) article.</span></span>
> 
> 

## <a name="manage-security-recommendations"></a><span data-ttu-id="4883c-132">管理安全性建議</span><span class="sxs-lookup"><span data-stu-id="4883c-132">Manage security recommendations</span></span>
<span data-ttu-id="4883c-133">資訊安全中心會分析您的 Azure 資源 hello 安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="4883c-133">Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="4883c-134">當資訊安全中心識別潛在的安全性弱點時，它會建立建議。</span><span class="sxs-lookup"><span data-stu-id="4883c-134">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="4883c-135">hello 建議會引導您完成設定所需的 hello 控制項的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="4883c-135">hello recommendations guide you through hello process of configuring hello needed controls.</span></span>

<span data-ttu-id="4883c-136">設定安全性原則之後, 的資訊安全中心會分析資源 tooidentify 的潛在弱點的 hello 安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="4883c-136">After setting a security policy, Security Center analyzes hello security state of your resources tooidentify potential vulnerabilities.</span></span> <span data-ttu-id="4883c-137">hello 建議會出現以資料表格式，其中每一行代表一個特定的建議。</span><span class="sxs-lookup"><span data-stu-id="4883c-137">hello recommendations are shown in a table format where each line represents one particular recommendation.</span></span> <span data-ttu-id="4883c-138">hello 下表提供的 Azure Vm 和什麼每一個將執行動作，您將它套用建議的一些範例。</span><span class="sxs-lookup"><span data-stu-id="4883c-138">hello table below provides some examples of recommendations for Azure VMs and what each one will do if you apply it.</span></span> <span data-ttu-id="4883c-139">當您選取建議時，您將提供示範如何 tooimplement hello 資訊安全中心的建議事項的資訊。</span><span class="sxs-lookup"><span data-stu-id="4883c-139">When you select a recommendation, you will be provided information that shows you how tooimplement hello recommendation in Security Center.</span></span>

| <span data-ttu-id="4883c-140">建議</span><span class="sxs-lookup"><span data-stu-id="4883c-140">Recommendation</span></span> | <span data-ttu-id="4883c-141">說明</span><span class="sxs-lookup"><span data-stu-id="4883c-141">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="4883c-142">啟用訂用帳戶的資料收集</span><span class="sxs-lookup"><span data-stu-id="4883c-142">Enable data collection for subscriptions</span></span>](security-center-enable-data-collection.md) |<span data-ttu-id="4883c-143">建議您在您的訂用帳戶中開啟 hello 安全性原則中的每個訂用帳戶及所有虛擬機器 (Vm) 的資料收集。</span><span class="sxs-lookup"><span data-stu-id="4883c-143">Recommends that you turn on data collection in hello security policy for each of your subscriptions and all virtual machines (VMs) in your subscriptions.</span></span> |
| [<span data-ttu-id="4883c-144">修復 OS 弱點</span><span class="sxs-lookup"><span data-stu-id="4883c-144">Remediate OS vulnerabilities</span></span>](security-center-remediate-os-vulnerabilities.md) |<span data-ttu-id="4883c-145">建議您設定規則的 hello 配合您作業系統的組態建議例如不允許儲存密碼 toobe。</span><span class="sxs-lookup"><span data-stu-id="4883c-145">Recommends that you align your OS configurations with hello recommended configuration rules, e.g. do not allow passwords toobe saved.</span></span> |
| [<span data-ttu-id="4883c-146">套用系統更新</span><span class="sxs-lookup"><span data-stu-id="4883c-146">Apply system updates</span></span>](security-center-apply-system-updates.md) |<span data-ttu-id="4883c-147">建議您部署遺失系統的安全性和重大更新 tooVMs。</span><span class="sxs-lookup"><span data-stu-id="4883c-147">Recommends that you deploy missing system security and critical updates tooVMs.</span></span> |
| [<span data-ttu-id="4883c-148">在系統更新之後重新開機</span><span class="sxs-lookup"><span data-stu-id="4883c-148">Reboot after system updates</span></span>](security-center-apply-system-updates.md#reboot-after-system-updates) |<span data-ttu-id="4883c-149">建議您重新啟動 VM toocomplete hello 程序套用系統更新。</span><span class="sxs-lookup"><span data-stu-id="4883c-149">Recommends that you reboot a VM toocomplete hello process of applying system updates.</span></span> |
| [<span data-ttu-id="4883c-150">安裝端點保護</span><span class="sxs-lookup"><span data-stu-id="4883c-150">Install Endpoint Protection</span></span>](security-center-install-endpoint-protection.md) |<span data-ttu-id="4883c-151">建議您佈建反惡意程式碼程式 tooVMs (僅限 Windows Vm)。</span><span class="sxs-lookup"><span data-stu-id="4883c-151">Recommends that you provision antimalware programs tooVMs (Windows VMs only).</span></span> |
| [<span data-ttu-id="4883c-152">解決端點保護健全狀況警示</span><span class="sxs-lookup"><span data-stu-id="4883c-152">Resolve Endpoint Protection health alerts</span></span>](security-center-resolve-endpoint-protection-health-alerts.md) |<span data-ttu-id="4883c-153">建議您先解決端點保護失敗。</span><span class="sxs-lookup"><span data-stu-id="4883c-153">Recommends that you resolve endpoint protection failures.</span></span> |
| [<span data-ttu-id="4883c-154">啟用 VM 代理程式</span><span class="sxs-lookup"><span data-stu-id="4883c-154">Enable VM Agent</span></span>](security-center-enable-vm-agent.md) |<span data-ttu-id="4883c-155">可讓您 toosee Vm 需要 hello VM 代理程式。</span><span class="sxs-lookup"><span data-stu-id="4883c-155">Enables you toosee which VMs require hello VM Agent.</span></span> <span data-ttu-id="4883c-156">hello VM 代理程式必須安裝在 Vm 上，在掃描中，基準和反惡意程式碼程式掃描順序 tooprovision 修補程式。</span><span class="sxs-lookup"><span data-stu-id="4883c-156">hello VM Agent must be installed on VMs in order tooprovision patch scanning, baseline scanning, and antimalware programs.</span></span> <span data-ttu-id="4883c-157">預設會安裝 VM 代理程式的 hello hello Azure Marketplace 會從部署的 vm。</span><span class="sxs-lookup"><span data-stu-id="4883c-157">hello VM Agent is installed by default for VMs that are deployed from hello Azure Marketplace.</span></span> <span data-ttu-id="4883c-158">hello 文章[VM 代理程式和延伸模組 – 第 2 部分](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/)tooinstall hello VM 代理程式的方式提供相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4883c-158">hello article [VM Agent and Extensions – Part 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) provides information on how tooinstall hello VM Agent.</span></span> |
| [<span data-ttu-id="4883c-159">套用磁碟加密</span><span class="sxs-lookup"><span data-stu-id="4883c-159">Apply disk encryption</span></span>](security-center-apply-disk-encryption.md) |<span data-ttu-id="4883c-160">建議您使用 Azure 磁碟加密來加密您的 VM 磁碟 (Windows 和 Linux VM)。</span><span class="sxs-lookup"><span data-stu-id="4883c-160">Recommends that you encrypt your VM disks using Azure Disk Encryption (Windows and Linux VMs).</span></span> <span data-ttu-id="4883c-161">加密是建議使用 hello OS 和 VM 上的資料磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4883c-161">Encryption is recommended for both hello OS and data volumes on your VM.</span></span> |
| [<span data-ttu-id="4883c-162">未安裝弱點評估</span><span class="sxs-lookup"><span data-stu-id="4883c-162">Vulnerability assessment not installed</span></span>](security-center-vulnerability-assessment-recommendations.md) |<span data-ttu-id="4883c-163">建議在 VM 上安裝弱點評估解決方案。</span><span class="sxs-lookup"><span data-stu-id="4883c-163">Recommends that you install a vulnerability assessment solution on your VM.</span></span> |
| [<span data-ttu-id="4883c-164">修復弱點</span><span class="sxs-lookup"><span data-stu-id="4883c-164">Remediate vulnerabilities</span></span>](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |<span data-ttu-id="4883c-165">可讓您 toosee 系統和應用程式的弱點可能會偵測到的 hello 的弱點可能會評估解決方案安裝在您的 VM 上。</span><span class="sxs-lookup"><span data-stu-id="4883c-165">Enables you toosee system and application vulnerabilities detected by hello vulnerability assessment solution installed on your VM.</span></span> |

> [!NOTE]
> <span data-ttu-id="4883c-166">toolearn 深入了解建議事項，請參閱[管理安全性建議](security-center-recommendations.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="4883c-166">toolearn more about recommendations, see [Managing security recommendations](security-center-recommendations.md) article.</span></span>
> 
> 

## <a name="monitor-security-health"></a><span data-ttu-id="4883c-167">監視安全性健康狀態</span><span class="sxs-lookup"><span data-stu-id="4883c-167">Monitor security health</span></span>
<span data-ttu-id="4883c-168">啟用後[安全性原則](security-center-policies.md)訂用帳戶的資源資訊安全中心會分析 hello 安全性資源 tooidentify 的潛在弱點的風險。</span><span class="sxs-lookup"><span data-stu-id="4883c-168">After you enable [security policies](security-center-policies.md) for a subscription’s resources, Security Center will analyze hello security of your resources tooidentify potential vulnerabilities.</span></span>  <span data-ttu-id="4883c-169">您可以檢視您的資源，以及任何問題，在 hello hello 安全性狀態**資源安全性健全狀況**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4883c-169">You can view hello security state of your resources, along with any issues in hello **Resource security health** blade.</span></span> <span data-ttu-id="4883c-170">當您按一下**虛擬機器**在 hello**資源安全性**健全狀況圖格、 hello**虛擬機器**刀鋒視窗會開啟您的 Vm 的建議。</span><span class="sxs-lookup"><span data-stu-id="4883c-170">When you click **Virtual machines** in hello **Resource security** health tile, hello **Virtual machines** blade will open with recommendations for your VMs.</span></span> 

![安全性健康狀態](./media/security-center-virtual-machine/security-center-virtual-machine-fig2.png)

## <a name="manage-and-respond-toosecurity-alerts"></a><span data-ttu-id="4883c-172">管理及回應 toosecurity 警示</span><span class="sxs-lookup"><span data-stu-id="4883c-172">Manage and respond toosecurity alerts</span></span>
<span data-ttu-id="4883c-173">資訊安全中心會自動收集、 分析，並整合您的 Azure 資源、 hello 網路和連線的交易夥伴方案 （例如防火牆和 endpoint protection 解決方案），從記錄檔資料 toodetect 威脅，並減少誤判。</span><span class="sxs-lookup"><span data-stu-id="4883c-173">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions (like firewall and endpoint protection solutions), toodetect real threats and reduce false positives.</span></span> <span data-ttu-id="4883c-174">利用不同的彙總的[偵測功能](security-center-detection-capabilities.md)，資訊安全中心是無法設定優先權的 toogenerate 快速調查 hello 問題並提供建議的方式，安全性警示 toohelp tooremediate可能的攻擊。</span><span class="sxs-lookup"><span data-stu-id="4883c-174">By leveraging a diverse aggregation of [detection capabilities](security-center-detection-capabilities.md), Security Center is able toogenerate prioritized security alerts toohelp you quickly investigate hello problem and provide recommendations for how tooremediate possible attacks.</span></span>

![安全性警示](./media/security-center-virtual-machine/security-center-virtual-machine-fig3.png)

<span data-ttu-id="4883c-176">選取 安全性警示 toolearn hello 事件觸發 hello 警示，以及項目，如果有的話會引導您有關需要 tootake tooremediate 攻擊。</span><span class="sxs-lookup"><span data-stu-id="4883c-176">Select a security alert toolearn more about hello event(s) that triggered hello alert and what, if any, steps you need tootake tooremediate an attack.</span></span> <span data-ttu-id="4883c-177">安全性警示會依[類型](security-center-alerts-type.md)及日期區分。</span><span class="sxs-lookup"><span data-stu-id="4883c-177">Security alerts are grouped by [type](security-center-alerts-type.md) and date.</span></span>

## <a name="see-also"></a><span data-ttu-id="4883c-178">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4883c-178">See also</span></span>
<span data-ttu-id="4883c-179">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="4883c-179">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="4883c-180">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="4883c-180">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="4883c-181">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="4883c-181">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="4883c-182">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="4883c-182">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>

