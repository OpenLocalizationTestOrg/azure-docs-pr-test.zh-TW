---
title: "Azure 資訊安全中心不同類型的安全性警示 | Microsoft Docs"
description: "本文討論 Azure 資訊安全中心各種可用的安全性警示。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b3e7b4bc-5ee0-4280-ad78-f49998675af1
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: 19f71e0d5a8a4642b86ae60a3ab2a4042fa2990e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-security-alerts-in-azure-security-center"></a><span data-ttu-id="b1c1e-103">了解 Azure 資訊安全中心的安全性警示</span><span class="sxs-lookup"><span data-stu-id="b1c1e-103">Understanding security alerts in Azure Security Center</span></span>
<span data-ttu-id="b1c1e-104">本文可協助您了解 Azure 資訊安全中心各種可用的安全性警示和相關深入資訊的類型。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-104">This article helps you to understand the different types of security alerts and related insights that are available in Azure Security Center.</span></span> <span data-ttu-id="b1c1e-105">如需如何管理警示和事件的詳細資訊，請參閱[管理及回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-105">For more information on how to manage alerts and incidents, see [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b1c1e-106">若要設定進階偵測，請升級至 Azure 資訊安全中心標準版。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-106">To set up advanced detections, upgrade to Azure Security Center Standard.</span></span> <span data-ttu-id="b1c1e-107">提供 60 天的免費試用。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-107">A free 60-day trial is available.</span></span> <span data-ttu-id="b1c1e-108">若要升級，請選取[安全性原則](security-center-policies.md) 中的 [定價層]。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-108">To upgrade, select **Pricing Tier** in the [security policy](security-center-policies.md).</span></span> <span data-ttu-id="b1c1e-109">若要深入了解，請參閱[價格頁面](https://azure.microsoft.com/pricing/details/security-center/)。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-109">To learn more, see the [pricing page](https://azure.microsoft.com/pricing/details/security-center/).</span></span>
>

## <a name="what-type-of-alerts-are-available"></a><span data-ttu-id="b1c1e-110">可以使用何種類型的警示？</span><span class="sxs-lookup"><span data-stu-id="b1c1e-110">What type of alerts are available?</span></span>
<span data-ttu-id="b1c1e-111">Azure 資訊安全中心會使用不同的[偵測功能](security-center-detection-capabilities.md)，向客戶警示以其環境為目標的潛在攻擊。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-111">Azure Security Center uses a variety of [detection capabilities](security-center-detection-capabilities.md) to alert customers to potential attacks targeting their environments.</span></span> <span data-ttu-id="b1c1e-112">這些警示包含觸發警示的項目、鎖定為目標的資源，以及攻擊來源等重要資訊。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-112">These alerts contain valuable information about the what triggered the alert, the resources targeted, and the source of the attack.</span></span> <span data-ttu-id="b1c1e-113">警示中包含的資訊會以用來偵測威脅的分析類型作為基礎而有所不同。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-113">The information included in an alert varies based on the type of analytics used to detect the threat.</span></span> <span data-ttu-id="b1c1e-114">事件可能還會包含其他內容相關的資訊，在調查威脅時很有用。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-114">Incidents may also contain additional contextual information that can be useful when investigating a threat.</span></span>  <span data-ttu-id="b1c1e-115">本文提供下列警示類型的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-115">This article provides information about the following alert types:</span></span>

* <span data-ttu-id="b1c1e-116">虛擬機器行為分析 (VMBA)</span><span class="sxs-lookup"><span data-stu-id="b1c1e-116">Virtual Machine Behavioral Analysis (VMBA)</span></span>
* <span data-ttu-id="b1c1e-117">網路分析</span><span class="sxs-lookup"><span data-stu-id="b1c1e-117">Network Analysis</span></span>
* <span data-ttu-id="b1c1e-118">資源分析</span><span class="sxs-lookup"><span data-stu-id="b1c1e-118">Resource Analysis</span></span>
* <span data-ttu-id="b1c1e-119">內容相關的資訊</span><span class="sxs-lookup"><span data-stu-id="b1c1e-119">Contextual Information</span></span>

## <a name="virtual-machine-behavioral-analysis"></a><span data-ttu-id="b1c1e-120">虛擬機器行為分析</span><span class="sxs-lookup"><span data-stu-id="b1c1e-120">Virtual machine behavioral analysis</span></span>
<span data-ttu-id="b1c1e-121">Azure 資訊安全中心可以使用行為分析，根據虛擬機器事件記錄的分析來識別遭到入侵的資源。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-121">Azure Security Center can use behavioral analytics to identify compromised resources based on analysis of virtual machine event logs.</span></span> <span data-ttu-id="b1c1e-122">例如：程序建立事件和登入事件。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-122">For example, Process Creation Events and Login Events.</span></span> <span data-ttu-id="b1c1e-123">此外，還與其他訊號相互關聯，以檢查廣泛行銷活動的支援證明。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-123">In addition, there is correlation with other signals to check for supporting evidence of a widespread campaign.</span></span>

> [!NOTE]
> <span data-ttu-id="b1c1e-124">如需資訊安全中心偵測功能運作方式的詳細資訊，請參閱 [Azure 資訊安全中心的偵測功能](security-center-detection-capabilities.md)。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-124">For more information on how Security Center detection capabilities work, see [Azure Security Center detection capabilities](security-center-detection-capabilities.md).</span></span>
>

### <a name="crash-analysis"></a><span data-ttu-id="b1c1e-125">損毀分析</span><span class="sxs-lookup"><span data-stu-id="b1c1e-125">Crash analysis</span></span>
<span data-ttu-id="b1c1e-126">損毀傾印記憶體分析是一種方法，可用來偵測能避開傳統安全性解決方案的複雜惡意程式碼。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-126">Crash dump memory analysis is a method used to detect sophisticated malware that is able to evade traditional security solutions.</span></span> <span data-ttu-id="b1c1e-127">各種形式的惡意程式碼會藉由決不寫入至磁碟或將寫入至磁碟的軟體元件加密，試圖減少被防毒產品偵測到的機會。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-127">Various forms of malware try to reduce the chance of being detected by antivirus products by never writing to disk, or by encrypting software components written to disk.</span></span> <span data-ttu-id="b1c1e-128">如此一來，使用傳統反惡意程式碼方法便難以偵測到惡意程式碼。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-128">This makes the malware difficult to detect by using traditional antimalware approaches.</span></span> <span data-ttu-id="b1c1e-129">不過，可以使用記憶體分析來偵測這類惡意程式碼，因為惡意程式碼必須在記憶體中留下蹤跡才能運作。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-129">However, this kind of malware can be detected by using memory analysis, because malware must leave traces in memory in order to function.</span></span>

<span data-ttu-id="b1c1e-130">當軟體損毀時，損毀傾印會在損毀時擷取部分的記憶體。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-130">When software crashes, a crash dump captures a portion of memory at the time of the crash.</span></span> <span data-ttu-id="b1c1e-131">惡意程式碼、一般應用程式或系統問題都可能造成損毀。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-131">The crash may be caused by malware, general application or system issues.</span></span> <span data-ttu-id="b1c1e-132">藉由分析損毀傾印中的記憶體，資訊安全中心可以偵測到用來惡意探索軟體弱點、存取機密資料，以及暗中存在於遭入侵電腦的技術。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-132">By analyzing the memory in the crash dump, Security Center can detect techniques used to exploit vulnerabilities in software, access confidential data, and surreptitiously persist within a compromised machine.</span></span> <span data-ttu-id="b1c1e-133">這可在對主機造成最小效能影響的情況下完成，因為此分析是由資訊安全中心後端所執行。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-133">This is accomplished with minimum performance impact to hosts as the analysis is performed by the Security Center back end.</span></span>

<span data-ttu-id="b1c1e-134">下列欄位通用於本文稍後顯示的損毀傾印警示範例︰</span><span class="sxs-lookup"><span data-stu-id="b1c1e-134">The following fields are common to the crash dump alert examples that appear later in this article:</span></span>

* <span data-ttu-id="b1c1e-135">DUMPFILE：損毀傾印檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-135">DUMPFILE: Name of the crash dump file.</span></span>
* <span data-ttu-id="b1c1e-136">PROCESSNAME︰損毀處理序的名稱。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-136">PROCESSNAME: Name of the crashing process.</span></span>
* <span data-ttu-id="b1c1e-137">PROCESSVERSION︰損毀處理序的版本。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-137">PROCESSVERSION: Version of the crashing process.</span></span>

### <a name="shellcode-discovered"></a><span data-ttu-id="b1c1e-138">探索到 Shellcode</span><span class="sxs-lookup"><span data-stu-id="b1c1e-138">Shellcode discovered</span></span>
<span data-ttu-id="b1c1e-139">Shellcode 是惡意程式碼惡意探索軟體弱點後執行的承載。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-139">Shellcode is the payload that is run after malware exploits a software vulnerability.</span></span> <span data-ttu-id="b1c1e-140">此警示代表毀損傾印分析偵測到的可執行程式碼顯現經常由惡意承載執行的行為。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-140">This alert indicates that crash dump analysis has detected executable code that exhibits behavior that is commonly performed by malicious payloads.</span></span> <span data-ttu-id="b1c1e-141">雖然非惡意軟體可能會執行這種行為，不過這不是一般軟體開發的實務做法。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-141">Although non-malicious software may perform this behavior, it is not typical of normal software development practices.</span></span>

<span data-ttu-id="b1c1e-142">Shellcode 警示範例提供下列額外欄位︰</span><span class="sxs-lookup"><span data-stu-id="b1c1e-142">The Shellcode alert example provides the following additional field:</span></span>

* <span data-ttu-id="b1c1e-143">ADDRESS：Shellcode 在記憶體中的位置。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-143">ADDRESS: The location in memory of the shellcode.</span></span>

<span data-ttu-id="b1c1e-144">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-144">This is an example of this type of alert:</span></span>

![Shellcode 警示](./media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a><span data-ttu-id="b1c1e-146">探索到模組攔截</span><span class="sxs-lookup"><span data-stu-id="b1c1e-146">Module hijacking discovered</span></span>
<span data-ttu-id="b1c1e-147">Windows 使用動態連結程式庫 (DLL) 允許軟體使用通用 Windows 系統功能。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-147">Windows uses dynamic-link libraries (DLLs) to allow software to utilize common Windows system functionality.</span></span> <span data-ttu-id="b1c1e-148">DLL 攔截發生於當惡意程式碼變更 DLL 載入順序，以便將惡意承載載入記憶體時，得手後有心人士便能執行任意程式碼。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-148">DLL Hijacking occurs when malware changes the DLL load order to load malicious payloads into memory, where arbitrary code can be executed.</span></span> <span data-ttu-id="b1c1e-149">此警示代表毀損傾印分析偵測到名稱相近的模組從兩個不同的路徑載入。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-149">This alert indicates that the crash dump analysis detected a similarly named module that is loaded from two different paths.</span></span> <span data-ttu-id="b1c1e-150">其中一個載入路徑來自通用 Windows 系統二進位檔位置。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-150">One of the loaded paths comes from a common Windows system binary location.</span></span>

<span data-ttu-id="b1c1e-151">合法軟體開發人員偶爾會為了非惡意的原因而變更 DLL 載入順序，如檢測、擴充 Windows 作業系統，或擴充 Windows 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-151">Legitimate software developers occasionally change the DLL load order for non-malicious reasons, such as instrumenting, extending the Windows OS, or extending a Windows application.</span></span> <span data-ttu-id="b1c1e-152">為了協助您區別 DLL 載入順序的惡意變更和潛在的良性變更，Azure 資訊安全中心會檢查載入的模組是否符合可疑設定檔。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-152">To help differentiate between malicious and potentially benign changes to the DLL load order, Azure Security Center checks whether a loaded module conforms to a suspicious profile.</span></span> <span data-ttu-id="b1c1e-153">這項檢查的結果會以警示的 “SIGNATURE” 欄位來表示，而且會反映在警示嚴重性、警示描述和警示補救步驟中。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-153">The result of this check is indicated by the “SIGNATURE” field of the alert and is reflected in the severity of the alert, alert description, and alert remediation steps.</span></span> <span data-ttu-id="b1c1e-154">若要研究此模組屬於合法或惡意，請分析攔截模組的磁碟複本。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-154">To research whether the module is legitimate or malicious, analyze the on disk copy of the hijacking module.</span></span> <span data-ttu-id="b1c1e-155">例如，您可以驗證檔案的數位簽章，或執行防毒掃描。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-155">For example, you can verify the file's digital signature, or run an antivirus scan.</span></span>

<span data-ttu-id="b1c1e-156">除了先前「探索到 Shellcode」一節描述的通用欄位之外，這項警示另提供下列欄位︰</span><span class="sxs-lookup"><span data-stu-id="b1c1e-156">In addition to the common fields described in the earlier “Shellcode discovered” section, this alert provides the following fields:</span></span>

* <span data-ttu-id="b1c1e-157">SIGNATURE︰指出攔截模組是否符合可疑行為設定檔。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-157">SIGNATURE: Indicates if the hijacking module conforms to a suspicious behavior profile.</span></span>
* <span data-ttu-id="b1c1e-158">HIJACKEDMODULE︰遭到攔截的 Windows 系統模組名稱。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-158">HIJACKEDMODULE: The name of the hijacked Windows system module.</span></span>
* <span data-ttu-id="b1c1e-159">HIJACKEDMODULEPATH︰遭到攔截的 Windows 系統模組路徑。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-159">HIJACKEDMODULEPATH: The path of the hijacked Windows system module.</span></span>
* <span data-ttu-id="b1c1e-160">HIJACKINGMODULEPATH︰攔截模組的路徑。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-160">HIJACKINGMODULEPATH: The path of the hijacking module.</span></span>

<span data-ttu-id="b1c1e-161">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-161">This is an example of this type of alert:</span></span>

![模組攔截警示](./media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a><span data-ttu-id="b1c1e-163">偵測到偽裝的 Windows 模組</span><span class="sxs-lookup"><span data-stu-id="b1c1e-163">Masquerading Windows module detected</span></span>
<span data-ttu-id="b1c1e-164">惡意程式碼可能會使用 Windows 系統二進位檔 (如 SVCHOST.EXE) 或模組 (如 NTDLL.DLL) 的常用名稱，以期能「蒙混過關」，避免系統管理員看清惡意軟體的本質。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-164">Malware may use common names of Windows system binaries (for example, SVCHOST.EXE) or modules (for example, NTDLL.DLL) to *blend in* and obscure the nature of the malicious software from system administrators.</span></span> <span data-ttu-id="b1c1e-165">此警示代表毀損傾印分析偵測到毀損傾印檔案含有使用 Windows 系統模組名稱的模組，但這些模組不符合 Windows 模組的其他典型條件。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-165">This alert indicates that the crash dump analysis detects that the crash dump file contains modules that use Windows system module names, but do not satisfy other criteria that are typical of Windows modules.</span></span> <span data-ttu-id="b1c1e-166">分析偽裝模組的磁碟複本，可讓您進一步瞭解此模組的本質屬於合法或惡意。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-166">Analyzing the on disk copy of the masquerading module may provide more information about the legitimate or malicious nature of this module.</span></span> <span data-ttu-id="b1c1e-167">分析可能包括︰</span><span class="sxs-lookup"><span data-stu-id="b1c1e-167">Analysis may include:</span></span>

* <span data-ttu-id="b1c1e-168">確認有問題的檔案隨附在合法軟體套件中。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-168">Confirm that the file in question is shipped as part of a legitimate software package.</span></span>
* <span data-ttu-id="b1c1e-169">驗證檔案的數位簽章。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-169">Verify the file’s digital signature.</span></span>
* <span data-ttu-id="b1c1e-170">針對檔案執行防毒軟體掃描。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-170">Run an antivirus scan on the file.</span></span>

<span data-ttu-id="b1c1e-171">除了先前「探索到 Shellcode」一節描述的通用欄位之外，這項警示另提供下列額外欄位︰</span><span class="sxs-lookup"><span data-stu-id="b1c1e-171">In addition to the common fields described earlier in the “Shellcode discovered” section, this alert provides the following additional fields:</span></span>

* <span data-ttu-id="b1c1e-172">DETAILS︰描述模組中繼資料是否有效，以及模組是否從系統路徑載入。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-172">DETAILS: Describes whether the module's metadata is valid, and whether the module was loaded from a system path.</span></span>
* <span data-ttu-id="b1c1e-173">NAME︰偽裝 Windows 模組的名稱。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-173">NAME: The name of the masquerading Windows module.</span></span>
* <span data-ttu-id="b1c1e-174">PATH︰偽裝 Windows 模組的路徑。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-174">PATH: The path to the masquerading Windows module.</span></span>

<span data-ttu-id="b1c1e-175">此警示也會從模組的 "CHECKSUM" 和 "TIMESTAMP" 等 PE 標頭擷取及顯示某些欄位。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-175">This alert also extracts and displays certain fields from the module’s PE header, such as “CHECKSUM” and “TIMESTAMP.”</span></span> <span data-ttu-id="b1c1e-176">唯有當模組有這些欄位時，它們才會出現。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-176">These fields are only displayed if the fields are present in the module.</span></span> <span data-ttu-id="b1c1e-177">如需這些欄位的詳細資料，請參閱 [Microsoft PE 和 COFF 規格](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-177">See the [Microsoft PE and COFF Specification](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) for details on these fields.</span></span>

<span data-ttu-id="b1c1e-178">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-178">This is an example of this type of alert:</span></span>

![偽裝的 Windows 警示](./media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a><span data-ttu-id="b1c1e-180">探索到修改過的系統二進位檔</span><span class="sxs-lookup"><span data-stu-id="b1c1e-180">Modified system binary discovered</span></span>
<span data-ttu-id="b1c1e-181">惡意程式碼可能會修改核心系統二進位檔，以便秘密存取資料或暗中存留在遭入侵的系統上。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-181">Malware may modify core system binaries in order to covertly access data or surreptitiously persist on a compromised system.</span></span> <span data-ttu-id="b1c1e-182">此警示代表毀損傾印分析偵測到記憶體中或磁碟上的核心 Windows 作業系統二進位檔已遭到修改。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-182">This alert indicates that the crash dump analysis has detected that core Windows OS binaries have been modified in memory or on disk.</span></span>

<span data-ttu-id="b1c1e-183">合法軟體開發人員偶爾會為了非惡意的原因而修改記憶體中的系統模組，如 Detours 或處理應用程式相容性。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-183">Legitimate software developers occasionally modify system modules in memory for non-malicious reasons, such as Detours or for application compatibility.</span></span> <span data-ttu-id="b1c1e-184">為了協助您區別惡意模組和可能合法的模組，Azure 資訊安全中心會檢查修改過的模組是否符合可疑設定檔。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-184">To help differentiate between malicious and potentially legitimate modules, Azure Security Center checks whether the modified module conforms to a suspicious profile.</span></span> <span data-ttu-id="b1c1e-185">這項檢查的結果會以警示嚴重性、警示描述和警示補救步驟來表示。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-185">The result of this check is indicated by the severity of the alert, alert description, and alert remediation steps.</span></span>

<span data-ttu-id="b1c1e-186">除了先前「探索到 Shellcode」一節描述的通用欄位之外，這項警示另提供下列額外欄位︰</span><span class="sxs-lookup"><span data-stu-id="b1c1e-186">In addition to the common fields described earlier in the “Shellcode discovered” section, this alert provides the following additional fields:</span></span>

* <span data-ttu-id="b1c1e-187">MODULENAME：修改過的系統二進位檔名稱。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-187">MODULENAME: Name of the modified system binary.</span></span>
* <span data-ttu-id="b1c1e-188">MODULEVERSION：修改過的系統二進位檔版本。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-188">MODULEVERSION: Version of the modified system binary.</span></span>

<span data-ttu-id="b1c1e-189">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-189">This is an example of this type of alert:</span></span>

![系統二進位檔警示](./media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a><span data-ttu-id="b1c1e-191">已執行可疑的處理序</span><span class="sxs-lookup"><span data-stu-id="b1c1e-191">Suspicious process executed</span></span>
<span data-ttu-id="b1c1e-192">資訊安全中心會識別在目標虛擬機器上執行的可疑處理序，然後觸發警示。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-192">Security Center identifies a suspicious process that runs on the target virtual machine, and then triggers an alert.</span></span> <span data-ttu-id="b1c1e-193">偵測不會尋找特定名稱，但會尋找可執行檔的參數。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-193">The detection doesn’t look for the specific name, but does look for the executable file's parameter.</span></span> <span data-ttu-id="b1c1e-194">因此，即使攻擊者將可執行檔重新命名，資訊安全中心仍可偵測可疑的程序。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-194">Therefore, even if the attacker renames the executable, Security Center can still detect the suspicious process.</span></span>

<span data-ttu-id="b1c1e-195">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-195">This is an example of this type of alert:</span></span>

![可疑的處理序警示](./media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a><span data-ttu-id="b1c1e-197">已查詢多個網域帳戶</span><span class="sxs-lookup"><span data-stu-id="b1c1e-197">Multiple domain accounts queried</span></span>
<span data-ttu-id="b1c1e-198">資訊安全中心可以偵測多次嘗試查詢 Active Directory 網域帳戶的動作，這通常是由攻擊者在網路偵察期間所執行。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-198">Security Center can detect multiple attempts to query Active Directory domain accounts, which is something usually performed by attackers during network reconnaissance.</span></span> <span data-ttu-id="b1c1e-199">攻擊者可以利用這項技術來查詢網域，以識別使用者、識別網域管理帳戶、識別當作網域控制站的電腦，以及識別與其他網域的潛在網域信任關係。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-199">Attackers can leverage this technique to query the domain to identify the users, identify the domain admin accounts, identify the computers that are domain controllers, and also identify the potential domain trust relationship with other domains.</span></span>

<span data-ttu-id="b1c1e-200">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-200">This is an example of this type of alert:</span></span>

![多個網域帳戶警示](./media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a><span data-ttu-id="b1c1e-202">已列舉本機系統管理員群組成員</span><span class="sxs-lookup"><span data-stu-id="b1c1e-202">Local Administrators group members were enumerated</span></span>

<span data-ttu-id="b1c1e-203">在 Windows Server 2016 和 Windows 10 中，資訊安全中心即將在安全性事件 4798 觸發時觸發警示。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-203">Security Center is going to trigger an alert when the security event 4798, in Windows Server 2016 and Windows 10, is trigged.</span></span> <span data-ttu-id="b1c1e-204">這種情況會發生在本機系統管理員群組列舉時，通常是由攻擊者在網路偵察期間所執行。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-204">This happens when local administrator groups are enumerated, which is something usually performed by attackers during network reconnaissance.</span></span> <span data-ttu-id="b1c1e-205">攻擊者可以利用這項技巧來查詢具有系統管理權限的使用者身分識別。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-205">Attackers can leverage this technique to query the identity of users with administrative privileges.</span></span>

<span data-ttu-id="b1c1e-206">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-206">This is an example of this type of alert:</span></span>

![本機系統管理員](./media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a><span data-ttu-id="b1c1e-208">異常混用大寫和小寫字元</span><span class="sxs-lookup"><span data-stu-id="b1c1e-208">Anomalous mix of upper and lower case characters</span></span>

<span data-ttu-id="b1c1e-209">資訊安全中心將會在偵測到命令列混合使用大寫和小寫字元時觸發警示。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-209">Security Center will trigger an alert when it detects the use of a mix of upper and lower case characters at the command line.</span></span> <span data-ttu-id="b1c1e-210">某些攻擊者可能會使用此技巧來規避區分大小寫或雜湊型電腦規則。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-210">Some attackers may use this technique to hide from case-sensitive or hash based machine rule.</span></span>

<span data-ttu-id="b1c1e-211">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-211">This is an example of this type of alert:</span></span>

![異常混用](./media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a><span data-ttu-id="b1c1e-213">可疑的 Kerberos 黃金票證攻擊</span><span class="sxs-lookup"><span data-stu-id="b1c1e-213">Suspected Kerberos Golden Ticket attack</span></span>

<span data-ttu-id="b1c1e-214">攻擊者可能會使用洩漏的 [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) 金鑰來建立 Kerberos「黃金票證」，讓攻擊者模擬他們想要的任何使用者。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-214">A compromised [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) key can be used by an attacker to create Kerberos "Golden Tickets," allowing the attacker to impersonate any user they wish.</span></span> <span data-ttu-id="b1c1e-215">資訊安全中心會在偵測到這類型的活動時觸發警示。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-215">Security Center is going to trigger an alert when it detects this type of activity.</span></span>

> [!NOTE] 
> <span data-ttu-id="b1c1e-216">如需 Kerberos 黃金票證的詳細資訊，請參閱 [Windows 10 認證竊取風險降低指南](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx)。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-216">For more information about Kerberos Golden Ticket, read [Windows 10 credential theft mitigation guide](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx).</span></span>

<span data-ttu-id="b1c1e-217">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-217">This is an example of this type of alert:</span></span>

![黃金票證](./media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a><span data-ttu-id="b1c1e-219">已建立可疑帳戶</span><span class="sxs-lookup"><span data-stu-id="b1c1e-219">Suspicious account created</span></span>

<span data-ttu-id="b1c1e-220">若建立與現有內建系統管理權限帳戶非常相似的帳戶，資訊安全中心就會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-220">Security Center will trigger an alert when an account is created with close resemblance of an existing built in administrative privilege account.</span></span> <span data-ttu-id="b1c1e-221">攻擊者可以使用這項技巧來建立 Rouge 帳戶，以避免被人為驗證所察覺。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-221">This technique can be used by attackers to create a rogue account to avoid being noticed by human verification.</span></span>
 
<span data-ttu-id="b1c1e-222">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-222">This is an example of this type of alert:</span></span>

![可疑的帳戶](./media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a><span data-ttu-id="b1c1e-224">已建立可疑的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="b1c1e-224">Suspicious Firewall rule created</span></span>

<span data-ttu-id="b1c1e-225">攻擊者可能會嘗試規避主機安全性，其方法是建立自訂防火牆規則來允許惡意應用程式與命令和控制項通訊，或經由遭入侵的主應用透過網路發動攻擊。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-225">Attackers might try to circumvent host security by creating custom firewall rules to allow malicious applications to communicate with command and control, or to launch attacks through the network via the compromised host.</span></span> <span data-ttu-id="b1c1e-226">資訊安全中心偵測到從可疑位置的可執行檔建立的新防火牆規則時，就會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-226">Security Center will trigger an alert when it detects that a new firewall rule was created from an executable file in a suspicious location.</span></span>
 
<span data-ttu-id="b1c1e-227">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-227">This is an example of this type of alert:</span></span>

![防火牆規則](./media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a><span data-ttu-id="b1c1e-229">可疑的 HTA 和 PowerShell 組合</span><span class="sxs-lookup"><span data-stu-id="b1c1e-229">Suspicious combination of HTA and PowerShell</span></span>

<span data-ttu-id="b1c1e-230">資訊安全中心偵測到 Microsoft HTML 應用程式主機 (HTA) 正在啟動 PowerShell 命令時會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-230">Security Center will trigger an alert when it detects that a Microsoft HTML Application Host (HTA) is launching PowerShell commands.</span></span> <span data-ttu-id="b1c1e-231">這是攻擊者用來啟動惡意 PowerShell 指令碼的技巧。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-231">This is a technique used by attackers to launch malicious PowerShell scripts.</span></span>
 
<span data-ttu-id="b1c1e-232">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-232">This is an example of this type of alert:</span></span>

![HTA 和 PS](./media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a><span data-ttu-id="b1c1e-234">網路分析</span><span class="sxs-lookup"><span data-stu-id="b1c1e-234">Network analysis</span></span>
<span data-ttu-id="b1c1e-235">資訊安全中心網路威脅偵測的運作方式如下：從 Azure IPFIX (Internet Protocol Flow Information Export) 流量自動收集安全性資訊。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-235">Security Center network threat detection works by automatically collecting security information from your Azure IPFIX (Internet Protocol Flow Information Export) traffic.</span></span> <span data-ttu-id="b1c1e-236">它會分析這項資訊 (通常是來自多個來源的相互關聯資訊) 以識別威脅。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-236">It analyzes this information, often correlating information from multiple sources, to identify threats.</span></span>

### <a name="suspicious-outgoing-traffic-detected"></a><span data-ttu-id="b1c1e-237">偵測到可疑的連出流量</span><span class="sxs-lookup"><span data-stu-id="b1c1e-237">Suspicious outgoing traffic detected</span></span>
<span data-ttu-id="b1c1e-238">網路裝置可以受到探索和分析，其方式和其他類型的系統非常類似。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-238">Network devices can be discovered and profiled in much the same way as other types of systems.</span></span> <span data-ttu-id="b1c1e-239">攻擊者通常會使用連接埠掃描或連接埠掃掠來開始攻擊。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-239">Attackers usually start with port scanning or port sweeping.</span></span> <span data-ttu-id="b1c1e-240">在下一個範例中，您有來自 VM 的可疑安全殼層 (SSH) 流量。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-240">In the next example, you have suspicious Secure Shell (SSH) traffic from a VM.</span></span> <span data-ttu-id="b1c1e-241">在此案例中，可能有對外部資源的 SSH 暴力密碼破解或連接埠掃掠攻擊。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-241">In this scenario, SSH brute force or a port sweeping attack against an external resource is possible.</span></span>

![可疑連出流量警示](./media/security-center-alerts-type/security-center-alerts-type-fig8.png)

<span data-ttu-id="b1c1e-243">此警示會提供資訊，以便您識別用來起始此攻擊的資源。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-243">This alert gives information that you can use to identify the resource that was used to initiate this attack.</span></span> <span data-ttu-id="b1c1e-244">此警示也會提供資訊，以識別遭入侵的電腦、偵測時間，以及所使用的通訊協定和連接埠。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-244">This alert also provides information to identify the compromised machine, the detection time, plus the protocol and port that was used.</span></span> <span data-ttu-id="b1c1e-245">此刀鋒視窗也可提供您可用來解決這個問題的補救步驟清單。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-245">This blade also gives you a list of remediation steps that can be used to mitigate this issue.</span></span>

### <a name="network-communication-with-a-malicious-machine"></a><span data-ttu-id="b1c1e-246">與惡意電腦的網路通訊</span><span class="sxs-lookup"><span data-stu-id="b1c1e-246">Network communication with a malicious machine</span></span>
<span data-ttu-id="b1c1e-247">藉由利用 Microsoft 威脅情報摘要，Azure 資訊安全中心可以偵測與惡意 IP 位址通訊的遭入侵電腦。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-247">By leveraging Microsoft threat intelligence feeds, Azure Security Center can detect compromised machines that communicate with malicious IP addresses.</span></span> <span data-ttu-id="b1c1e-248">在許多情況下，惡意位址會是命令和控制中心。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-248">In many cases, the malicious address is a command and control center.</span></span> <span data-ttu-id="b1c1e-249">在此情況下，資訊安全中心偵測到通訊是使用 Pony Loader 惡意程式碼 (也稱為 [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)) 來進行。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-249">In this case, Security Center detected that the communication was done by using Pony Loader malware (also known as [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).</span></span>

![網路通訊警示](./media/security-center-alerts-type/security-center-alerts-type-fig9.png)

<span data-ttu-id="b1c1e-251">此警示會提供資訊，讓您識別用來起始此攻擊的資源、受攻擊的資源、受害者 IP、攻擊者 IP 和偵測時間。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-251">This alert gives information that enables you to identify the resource that was used to initiate this attack, the attacked resource, the victim IP, the attacker IP, and the detection time.</span></span>

> [!NOTE]
> <span data-ttu-id="b1c1e-252">為了保護隱私權，此螢幕擷取畫面的即時 IP 位址已遭到移除。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-252">Live IP addresses were removed from this screenshot for privacy purpose.</span></span>
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a><span data-ttu-id="b1c1e-253">偵測到可能的連出拒絕服務攻擊</span><span class="sxs-lookup"><span data-stu-id="b1c1e-253">Possible outgoing denial-of-service attack detected</span></span>
<span data-ttu-id="b1c1e-254">源自一部虛擬機器的異常網路流量可能會導致資訊安全中心觸發潛在的拒絕服務攻擊類型。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-254">Abnormal network traffic that originates from one virtual machine can cause Security Center to trigger a potential denial-of-service type of attack.</span></span>

<span data-ttu-id="b1c1e-255">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-255">This is an example of this type of alert:</span></span>

![連出 DOS](./media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a><span data-ttu-id="b1c1e-257">資源分析</span><span class="sxs-lookup"><span data-stu-id="b1c1e-257">Resource analysis</span></span>
<span data-ttu-id="b1c1e-258">資訊安全中心資源分析著重於平台即服務 (PaaS) 服務，例如與 [Azure SQL Database 威脅偵測](../sql-database/sql-database-threat-detection.md)功能整合。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-258">Security Center resource analysis focuses on platform as a service (PaaS) services, such as the integration with the [Azure SQL Database threat detection](../sql-database/sql-database-threat-detection.md) feature.</span></span> <span data-ttu-id="b1c1e-259">根據來自這些區域的分析結果，資訊安全中心會觸發資源相關警示。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-259">Based on the analysis’s results from these areas, Security Center triggers a resource-related alert.</span></span>

### <a name="potential-sql-injection"></a><span data-ttu-id="b1c1e-260">潛在的 SQL 插入式攻擊</span><span class="sxs-lookup"><span data-stu-id="b1c1e-260">Potential SQL injection</span></span>
<span data-ttu-id="b1c1e-261">SQL 插入式攻擊會將惡意程式碼插入字串，而此字串稍後會傳遞至 SQL Server 執行個體以進行剖析和執行。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-261">SQL injection is an attack where malicious code is inserted into strings that are later passed to an instance of SQL Server for parsing and execution.</span></span> <span data-ttu-id="b1c1e-262">因為 SQL Server 會執行它收到的所有語法上有效的查詢，所以建構 SQL 陳述式的任何程序皆應檢閱其中是否有插入式攻擊弱點。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-262">Because SQL Server executes all syntactically valid queries that it receives, any procedure that constructs SQL statements should be reviewed for injection vulnerabilities.</span></span> <span data-ttu-id="b1c1e-263">SQL 威脅偵測會使用機器學習、行為分析和異常偵測，判斷 Azure SQL Database 中可能會發生的可疑事件。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-263">SQL Threat Detection uses machine learning, behavioral analysis, and anomaly detection to determine suspicious events that might be taking place in your Azure SQL databases.</span></span> <span data-ttu-id="b1c1e-264">例如：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-264">For example:</span></span>

* <span data-ttu-id="b1c1e-265">離職員工嘗試的資料庫存取</span><span class="sxs-lookup"><span data-stu-id="b1c1e-265">Attempted database access by a former employee</span></span>
* <span data-ttu-id="b1c1e-266">SQL 插入式攻擊</span><span class="sxs-lookup"><span data-stu-id="b1c1e-266">SQL injection attacks</span></span>
* <span data-ttu-id="b1c1e-267">從使用者家裡異常存取生產資料庫</span><span class="sxs-lookup"><span data-stu-id="b1c1e-267">Unusual access to a production database from a user at home</span></span>

![潛在的 SQL 插入式攻擊警示](./media/security-center-alerts-type/security-center-alerts-type-fig11.png)

<span data-ttu-id="b1c1e-269">這項警示的資訊可用來識別受攻擊的資源、偵測時間和攻擊的狀態。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-269">The information in this alert can be used to identify the attacked resource, the detection time, and the state of the attack.</span></span> <span data-ttu-id="b1c1e-270">它也提供進一步調查步驟的連結。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-270">It also provides a link to further investigation steps.</span></span>

### <a name="vulnerability-to-sql-injection"></a><span data-ttu-id="b1c1e-271">SQL 插入式攻擊的弱點</span><span class="sxs-lookup"><span data-stu-id="b1c1e-271">Vulnerability to SQL Injection</span></span>
<span data-ttu-id="b1c1e-272">在資料庫上偵測到應用程式錯誤時，會觸發此警示。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-272">This alert is triggered when an application error is detected on a database.</span></span> <span data-ttu-id="b1c1e-273">此警示表示 SQL 插入式攻擊的可能弱點。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-273">This alert may indicate a possible vulnerability to SQL injection attacks.</span></span>

![潛在的 SQL 插入式攻擊警示](./media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a><span data-ttu-id="b1c1e-275">來自不熟悉位置的異常存取</span><span class="sxs-lookup"><span data-stu-id="b1c1e-275">Unusual access from unfamiliar location</span></span>
<span data-ttu-id="b1c1e-276">在伺服器上偵測到來自不熟悉 IP 位址的存取事件 (未在最後一個期間看到) 時，會觸發此警示。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-276">This alert is triggered when an access event from an unfamiliar IP address was detected on the server, which was not seen in the last period.</span></span>

![異常存取警示](./media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="contextual-information"></a><span data-ttu-id="b1c1e-278">內容相關的資訊</span><span class="sxs-lookup"><span data-stu-id="b1c1e-278">Contextual information</span></span>
<span data-ttu-id="b1c1e-279">在調查期間，分析師需要額外的內容，才能觸達關於威脅的本質，以及如何降低威脅的結論。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-279">During an investigation, analysts need extra context to reach a verdict about the nature of the threat and how to mitigate it.</span></span>  <span data-ttu-id="b1c1e-280">例如，偵測到網路異常，但如果不了解網路上或關於鎖定為目標的資源發生了什麼其他情況，就很難以了解後續要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-280">For example, a network anomaly was detected, but without understanding what else is happening on the network or with regard to the targeted resource it is every hard to understand what actions to take next.</span></span> <span data-ttu-id="b1c1e-281">若要提供協助，安全性事件可能包含有助於調查的成品、相關事件和資訊。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-281">To aid with that, a Security Incident may include artifacts, related events and information that may help the investigator.</span></span> <span data-ttu-id="b1c1e-282">其他資訊的可用性會以偵測到的威脅及您環境的設定類型作為基礎而有所不同，且將無法用於所有的安全性事件。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-282">The availability of additional information will vary based on the type of threat detected and the configuration of your environment, and will not be available for all Security Incidents.</span></span>

<span data-ttu-id="b1c1e-283">若有其他資訊可供使用，會顯示在警示清單下方的安全性事件中。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-283">If additional information is available, it will be shown in the Security Incident below the list of alerts.</span></span> <span data-ttu-id="b1c1e-284">這可能包括的資訊如：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-284">This could contain information like:</span></span>

- <span data-ttu-id="b1c1e-285">清除事件記錄</span><span class="sxs-lookup"><span data-stu-id="b1c1e-285">Log clear events</span></span>
- <span data-ttu-id="b1c1e-286">從未知裝置插入的 PNP 裝置</span><span class="sxs-lookup"><span data-stu-id="b1c1e-286">PNP device plugged from unknown device</span></span>
- <span data-ttu-id="b1c1e-287">不可採取動作的警示</span><span class="sxs-lookup"><span data-stu-id="b1c1e-287">Alerts which are not actionable</span></span> 

![異常存取警示](./media/security-center-alerts-type/security-center-alerts-type-fig20.png) 


## <a name="see-also"></a><span data-ttu-id="b1c1e-289">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b1c1e-289">See also</span></span>
<span data-ttu-id="b1c1e-290">在本文中，您了解到資訊安全中心的各種安全性警示類型。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-290">In this article, you learned about the different types of security alerts in Security Center.</span></span> <span data-ttu-id="b1c1e-291">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="b1c1e-291">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="b1c1e-292">在 Azure 資訊安全中心處理安全性事件</span><span class="sxs-lookup"><span data-stu-id="b1c1e-292">Handling security incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="b1c1e-293">Azure 資訊安全中心的偵測功能</span><span class="sxs-lookup"><span data-stu-id="b1c1e-293">Azure Security Center detection capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="b1c1e-294">Azure 資訊安全中心規劃和操作指南</span><span class="sxs-lookup"><span data-stu-id="b1c1e-294">Azure Security Center planning and operations guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="b1c1e-295">[Azure 資訊安全中心常見問題集](security-center-faq.md)：尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-295">[Azure Security Center FAQ](security-center-faq.md): Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="b1c1e-296">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)：尋找有關 Azure 安全性與合規性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="b1c1e-296">[Azure security blog](http://blogs.msdn.com/b/azuresecurity/): Find blog posts about Azure security and compliance.</span></span>
