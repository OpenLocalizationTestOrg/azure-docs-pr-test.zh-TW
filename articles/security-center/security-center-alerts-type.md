---
title: "由 Azure 資訊安全中心中的型別 aaaSecurity 警示 |Microsoft 文件"
description: "這篇文章討論 hello 不同的 Azure 資訊安全中心中可用的安全性警示。"
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
ms.openlocfilehash: ee69cb9035c35f5bc2ed51f9b9d6f29486b4caf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-security-alerts-in-azure-security-center"></a><span data-ttu-id="37c1c-103">了解 Azure 資訊安全中心的安全性警示</span><span class="sxs-lookup"><span data-stu-id="37c1c-103">Understanding security alerts in Azure Security Center</span></span>
<span data-ttu-id="37c1c-104">這篇文章可協助您 toounderstand hello 不同類型的安全性警示和相關的深入資訊，都是在 Azure 資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="37c1c-104">This article helps you toounderstand hello different types of security alerts and related insights that are available in Azure Security Center.</span></span> <span data-ttu-id="37c1c-105">如需有關如何 toomanage 警示和事件，請參閱[中 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="37c1c-105">For more information on how toomanage alerts and incidents, see [Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="37c1c-106">tooset 向上進階偵測，升級 tooAzure 安全性 Center 標準。</span><span class="sxs-lookup"><span data-stu-id="37c1c-106">tooset up advanced detections, upgrade tooAzure Security Center Standard.</span></span> <span data-ttu-id="37c1c-107">提供 60 天的免費試用。</span><span class="sxs-lookup"><span data-stu-id="37c1c-107">A free 60-day trial is available.</span></span> <span data-ttu-id="37c1c-108">選取 tooupgrade**定價層**在 hello[安全性原則](security-center-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="37c1c-108">tooupgrade, select **Pricing Tier** in hello [security policy](security-center-policies.md).</span></span> <span data-ttu-id="37c1c-109">toolearn 詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/security-center/)。</span><span class="sxs-lookup"><span data-stu-id="37c1c-109">toolearn more, see hello [pricing page](https://azure.microsoft.com/pricing/details/security-center/).</span></span>
>

## <a name="what-type-of-alerts-are-available"></a><span data-ttu-id="37c1c-110">可以使用何種類型的警示？</span><span class="sxs-lookup"><span data-stu-id="37c1c-110">What type of alerts are available?</span></span>
<span data-ttu-id="37c1c-111">Azure 資訊安全中心使用不同的[偵測功能](security-center-detection-capabilities.md)tooalert 作為目標環境的客戶 toopotential 攻擊。</span><span class="sxs-lookup"><span data-stu-id="37c1c-111">Azure Security Center uses a variety of [detection capabilities](security-center-detection-capabilities.md) tooalert customers toopotential attacks targeting their environments.</span></span> <span data-ttu-id="37c1c-112">觸發 hello hello 資源做為目標、 警示以及 hello hello 攻擊的來源，這些警示會包含 hello 等重要資訊。</span><span class="sxs-lookup"><span data-stu-id="37c1c-112">These alerts contain valuable information about hello what triggered hello alert, hello resources targeted, and hello source of hello attack.</span></span> <span data-ttu-id="37c1c-113">包含警示中的 hello 資訊依據分析使用 toodetect hello 威脅 hello 類型而異。</span><span class="sxs-lookup"><span data-stu-id="37c1c-113">hello information included in an alert varies based on hello type of analytics used toodetect hello threat.</span></span> <span data-ttu-id="37c1c-114">事件可能還會包含其他內容相關的資訊，在調查威脅時很有用。</span><span class="sxs-lookup"><span data-stu-id="37c1c-114">Incidents may also contain additional contextual information that can be useful when investigating a threat.</span></span>  <span data-ttu-id="37c1c-115">本文章提供 hello 下列警示類型的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="37c1c-115">This article provides information about hello following alert types:</span></span>

* <span data-ttu-id="37c1c-116">虛擬機器行為分析 (VMBA)</span><span class="sxs-lookup"><span data-stu-id="37c1c-116">Virtual Machine Behavioral Analysis (VMBA)</span></span>
* <span data-ttu-id="37c1c-117">網路分析</span><span class="sxs-lookup"><span data-stu-id="37c1c-117">Network Analysis</span></span>
* <span data-ttu-id="37c1c-118">資源分析</span><span class="sxs-lookup"><span data-stu-id="37c1c-118">Resource Analysis</span></span>
* <span data-ttu-id="37c1c-119">內容相關的資訊</span><span class="sxs-lookup"><span data-stu-id="37c1c-119">Contextual Information</span></span>

## <a name="virtual-machine-behavioral-analysis"></a><span data-ttu-id="37c1c-120">虛擬機器行為分析</span><span class="sxs-lookup"><span data-stu-id="37c1c-120">Virtual machine behavioral analysis</span></span>
<span data-ttu-id="37c1c-121">Azure 資訊安全中心可以使用行為分析 tooidentify 洩漏資源，根據虛擬機器的事件記錄檔的分析。</span><span class="sxs-lookup"><span data-stu-id="37c1c-121">Azure Security Center can use behavioral analytics tooidentify compromised resources based on analysis of virtual machine event logs.</span></span> <span data-ttu-id="37c1c-122">例如：程序建立事件和登入事件。</span><span class="sxs-lookup"><span data-stu-id="37c1c-122">For example, Process Creation Events and Login Events.</span></span> <span data-ttu-id="37c1c-123">此外，沒有與其他支援廣泛的行銷活動的辨識項的訊號 toocheck 相互關聯。</span><span class="sxs-lookup"><span data-stu-id="37c1c-123">In addition, there is correlation with other signals toocheck for supporting evidence of a widespread campaign.</span></span>

> [!NOTE]
> <span data-ttu-id="37c1c-124">如需資訊安全中心偵測功能運作方式的詳細資訊，請參閱 [Azure 資訊安全中心的偵測功能](security-center-detection-capabilities.md)。</span><span class="sxs-lookup"><span data-stu-id="37c1c-124">For more information on how Security Center detection capabilities work, see [Azure Security Center detection capabilities](security-center-detection-capabilities.md).</span></span>
>

### <a name="crash-analysis"></a><span data-ttu-id="37c1c-125">損毀分析</span><span class="sxs-lookup"><span data-stu-id="37c1c-125">Crash analysis</span></span>
<span data-ttu-id="37c1c-126">損毀傾印記憶體分析會使用方法 toodetect 複雜惡意程式碼是無法 tooevade 傳統的安全性解決方案。</span><span class="sxs-lookup"><span data-stu-id="37c1c-126">Crash dump memory analysis is a method used toodetect sophisticated malware that is able tooevade traditional security solutions.</span></span> <span data-ttu-id="37c1c-127">各種形式的惡意程式碼嘗試 tooreduce hello 的永遠不會寫入 toodisk，或是加密軟體元件撰寫 toodisk 偵測到的防毒產品的機率。</span><span class="sxs-lookup"><span data-stu-id="37c1c-127">Various forms of malware try tooreduce hello chance of being detected by antivirus products by never writing toodisk, or by encrypting software components written toodisk.</span></span> <span data-ttu-id="37c1c-128">透過使用傳統的反惡意程式碼方法，讓 hello 惡意程式碼難以 toodetect。</span><span class="sxs-lookup"><span data-stu-id="37c1c-128">This makes hello malware difficult toodetect by using traditional antimalware approaches.</span></span> <span data-ttu-id="37c1c-129">不過，這種惡意程式碼可以偵測到使用記憶體分析，因為惡意程式碼必須保留在記憶體中順序 toofunction 的追蹤。</span><span class="sxs-lookup"><span data-stu-id="37c1c-129">However, this kind of malware can be detected by using memory analysis, because malware must leave traces in memory in order toofunction.</span></span>

<span data-ttu-id="37c1c-130">軟體損毀，損毀傾印會擷取 hello hello 損毀時的記憶體部分。</span><span class="sxs-lookup"><span data-stu-id="37c1c-130">When software crashes, a crash dump captures a portion of memory at hello time of hello crash.</span></span> <span data-ttu-id="37c1c-131">惡意程式碼中，一般應用程式或系統問題可能因為 hello 損毀。</span><span class="sxs-lookup"><span data-stu-id="37c1c-131">hello crash may be caused by malware, general application or system issues.</span></span> <span data-ttu-id="37c1c-132">藉由分析 hello 記憶體 hello 損毀傾印中的，資訊安全中心可以偵測技術軟體中使用 tooexploit 弱點，存取機密資料，並暗中遭到洩露的機器內持續。</span><span class="sxs-lookup"><span data-stu-id="37c1c-132">By analyzing hello memory in hello crash dump, Security Center can detect techniques used tooexploit vulnerabilities in software, access confidential data, and surreptitiously persist within a compromised machine.</span></span> <span data-ttu-id="37c1c-133">這是具有最小的效能影響 toohosts hello 分析是的 hello 回資訊安全中心 」 結尾所執行。</span><span class="sxs-lookup"><span data-stu-id="37c1c-133">This is accomplished with minimum performance impact toohosts as hello analysis is performed by hello Security Center back end.</span></span>

<span data-ttu-id="37c1c-134">hello 遵循欄位都是常見 toohello 損毀傾印警示範例本文中稍後出現：</span><span class="sxs-lookup"><span data-stu-id="37c1c-134">hello following fields are common toohello crash dump alert examples that appear later in this article:</span></span>

* <span data-ttu-id="37c1c-135">傾印檔案以： Hello 損毀傾印檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="37c1c-135">DUMPFILE: Name of hello crash dump file.</span></span>
* <span data-ttu-id="37c1c-136">PROCESSNAME: Hello 損毀處理序名稱。</span><span class="sxs-lookup"><span data-stu-id="37c1c-136">PROCESSNAME: Name of hello crashing process.</span></span>
* <span data-ttu-id="37c1c-137">PROCESSVERSION: Hello 損毀處理序版本。</span><span class="sxs-lookup"><span data-stu-id="37c1c-137">PROCESSVERSION: Version of hello crashing process.</span></span>

### <a name="shellcode-discovered"></a><span data-ttu-id="37c1c-138">探索到 Shellcode</span><span class="sxs-lookup"><span data-stu-id="37c1c-138">Shellcode discovered</span></span>
<span data-ttu-id="37c1c-139">Shellcode 是 hello 裝載惡意程式碼利用軟體弱點後執行。</span><span class="sxs-lookup"><span data-stu-id="37c1c-139">Shellcode is hello payload that is run after malware exploits a software vulnerability.</span></span> <span data-ttu-id="37c1c-140">此警示代表毀損傾印分析偵測到的可執行程式碼顯現經常由惡意承載執行的行為。</span><span class="sxs-lookup"><span data-stu-id="37c1c-140">This alert indicates that crash dump analysis has detected executable code that exhibits behavior that is commonly performed by malicious payloads.</span></span> <span data-ttu-id="37c1c-141">雖然非惡意軟體可能會執行這種行為，不過這不是一般軟體開發的實務做法。</span><span class="sxs-lookup"><span data-stu-id="37c1c-141">Although non-malicious software may perform this behavior, it is not typical of normal software development practices.</span></span>

<span data-ttu-id="37c1c-142">hello Shellcode 警示範例提供下列額外欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="37c1c-142">hello Shellcode alert example provides hello following additional field:</span></span>

* <span data-ttu-id="37c1c-143">在記憶體中的 hello shellcode 位址： hello 位置。</span><span class="sxs-lookup"><span data-stu-id="37c1c-143">ADDRESS: hello location in memory of hello shellcode.</span></span>

<span data-ttu-id="37c1c-144">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="37c1c-144">This is an example of this type of alert:</span></span>

![Shellcode 警示](./media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a><span data-ttu-id="37c1c-146">探索到模組攔截</span><span class="sxs-lookup"><span data-stu-id="37c1c-146">Module hijacking discovered</span></span>
<span data-ttu-id="37c1c-147">Windows 會使用動態連結程式庫 (Dll) tooallow 軟體 tooutilize 常見 Windows 系統的功能。</span><span class="sxs-lookup"><span data-stu-id="37c1c-147">Windows uses dynamic-link libraries (DLLs) tooallow software tooutilize common Windows system functionality.</span></span> <span data-ttu-id="37c1c-148">DLL 劫持惡意程式碼變更時發生 hello DLL 載入順序 tooload 惡意裝載到記憶體中，可以執行任意程式碼。</span><span class="sxs-lookup"><span data-stu-id="37c1c-148">DLL Hijacking occurs when malware changes hello DLL load order tooload malicious payloads into memory, where arbitrary code can be executed.</span></span> <span data-ttu-id="37c1c-149">此警示表示 hello 損毀傾印分析偵測到名稱類似的模組載入從兩個不同的路徑。</span><span class="sxs-lookup"><span data-stu-id="37c1c-149">This alert indicates that hello crash dump analysis detected a similarly named module that is loaded from two different paths.</span></span> <span data-ttu-id="37c1c-150">其中一個 hello 載入路徑是來自一般 Windows 系統二進位檔位置。</span><span class="sxs-lookup"><span data-stu-id="37c1c-150">One of hello loaded paths comes from a common Windows system binary location.</span></span>

<span data-ttu-id="37c1c-151">合法軟體開發人員偶爾會變更非惡意的原因，例如檢測、 擴充 hello Windows 作業系統，或擴充 Windows 應用程式的 hello DLL 載入順序。</span><span class="sxs-lookup"><span data-stu-id="37c1c-151">Legitimate software developers occasionally change hello DLL load order for non-malicious reasons, such as instrumenting, extending hello Windows OS, or extending a Windows application.</span></span> <span data-ttu-id="37c1c-152">toohelp 區分惡意與潛在良性變更 toohello DLL 載入順序時，Azure 資訊安全中心檢查載入的模組是否符合 tooa 可疑的設定檔。</span><span class="sxs-lookup"><span data-stu-id="37c1c-152">toohelp differentiate between malicious and potentially benign changes toohello DLL load order, Azure Security Center checks whether a loaded module conforms tooa suspicious profile.</span></span> <span data-ttu-id="37c1c-153">這項檢查的 hello 結果指出 hello 警示 hello 「 簽章 」 欄位，而且會反映在 hello 嚴重性 hello 警示、 警示描述，以及警示的修復步驟。</span><span class="sxs-lookup"><span data-stu-id="37c1c-153">hello result of this check is indicated by hello “SIGNATURE” field of hello alert and is reflected in hello severity of hello alert, alert description, and alert remediation steps.</span></span> <span data-ttu-id="37c1c-154">tooresearch hello 模組是否合法或惡意的分析 hello hello 劫持模組副本磁碟上。</span><span class="sxs-lookup"><span data-stu-id="37c1c-154">tooresearch whether hello module is legitimate or malicious, analyze hello on disk copy of hello hijacking module.</span></span> <span data-ttu-id="37c1c-155">例如，您可以驗證 hello 檔案的數位簽章，或執行的防毒掃描。</span><span class="sxs-lookup"><span data-stu-id="37c1c-155">For example, you can verify hello file's digital signature, or run an antivirus scan.</span></span>

<span data-ttu-id="37c1c-156">此外 toohello hello 早"Shellcode 探索 」 一節所述共通的欄位，此警示提供下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="37c1c-156">In addition toohello common fields described in hello earlier “Shellcode discovered” section, this alert provides hello following fields:</span></span>

* <span data-ttu-id="37c1c-157">簽章： 表示是否 hello 劫持模組符合 tooa 可疑的行為設定檔。</span><span class="sxs-lookup"><span data-stu-id="37c1c-157">SIGNATURE: Indicates if hello hijacking module conforms tooa suspicious behavior profile.</span></span>
* <span data-ttu-id="37c1c-158">HIJACKEDMODULE: hello hello 名稱劫 Windows 系統模組。</span><span class="sxs-lookup"><span data-stu-id="37c1c-158">HIJACKEDMODULE: hello name of hello hijacked Windows system module.</span></span>
* <span data-ttu-id="37c1c-159">HIJACKEDMODULEPATH: hello hello 路徑劫 Windows 系統模組。</span><span class="sxs-lookup"><span data-stu-id="37c1c-159">HIJACKEDMODULEPATH: hello path of hello hijacked Windows system module.</span></span>
* <span data-ttu-id="37c1c-160">Hello 劫持模組 HIJACKINGMODULEPATH: hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="37c1c-160">HIJACKINGMODULEPATH: hello path of hello hijacking module.</span></span>

<span data-ttu-id="37c1c-161">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="37c1c-161">This is an example of this type of alert:</span></span>

![模組攔截警示](./media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a><span data-ttu-id="37c1c-163">偵測到偽裝的 Windows 模組</span><span class="sxs-lookup"><span data-stu-id="37c1c-163">Masquerading Windows module detected</span></span>
<span data-ttu-id="37c1c-164">惡意程式碼可能會使用 Windows 系統二進位檔 (例如，SVCHOST 一般名稱。EXE) 或模組 (例如，NTDLL。DLL) 太*blend*和混淆 hello 性質 hello 惡意軟體的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="37c1c-164">Malware may use common names of Windows system binaries (for example, SVCHOST.EXE) or modules (for example, NTDLL.DLL) too*blend in* and obscure hello nature of hello malicious software from system administrators.</span></span> <span data-ttu-id="37c1c-165">此警示表示 hello 損毀傾印分析偵測到該 hello 損毀傾印檔案包含使用 Windows 系統模組名稱，但不是符合其他準則典型的 Windows 模組的模組。</span><span class="sxs-lookup"><span data-stu-id="37c1c-165">This alert indicates that hello crash dump analysis detects that hello crash dump file contains modules that use Windows system module names, but do not satisfy other criteria that are typical of Windows modules.</span></span> <span data-ttu-id="37c1c-166">磁碟副本 hello 偽裝模組上的分析 hello 可能提供這個模組的 hello 合法或惡意的本質的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="37c1c-166">Analyzing hello on disk copy of hello masquerading module may provide more information about hello legitimate or malicious nature of this module.</span></span> <span data-ttu-id="37c1c-167">分析可能包括︰</span><span class="sxs-lookup"><span data-stu-id="37c1c-167">Analysis may include:</span></span>

* <span data-ttu-id="37c1c-168">請確認該問題的 hello 檔案隨附的合法軟體套件的一部分。</span><span class="sxs-lookup"><span data-stu-id="37c1c-168">Confirm that hello file in question is shipped as part of a legitimate software package.</span></span>
* <span data-ttu-id="37c1c-169">請確認 hello 檔案的數位簽章。</span><span class="sxs-lookup"><span data-stu-id="37c1c-169">Verify hello file’s digital signature.</span></span>
* <span data-ttu-id="37c1c-170">Hello 檔案上執行的防毒掃描。</span><span class="sxs-lookup"><span data-stu-id="37c1c-170">Run an antivirus scan on hello file.</span></span>

<span data-ttu-id="37c1c-171">此外 toohello 通用欄位前面 hello"Shellcode 探索 」 一節中所述，此警示提供下列其他欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="37c1c-171">In addition toohello common fields described earlier in hello “Shellcode discovered” section, this alert provides hello following additional fields:</span></span>

* <span data-ttu-id="37c1c-172">詳細資料： 描述 hello 模組中繼資料是否有效，以及是否 hello 模組已載入的系統路徑。</span><span class="sxs-lookup"><span data-stu-id="37c1c-172">DETAILS: Describes whether hello module's metadata is valid, and whether hello module was loaded from a system path.</span></span>
* <span data-ttu-id="37c1c-173">名稱： hello hello 偽裝 Windows 模組名稱。</span><span class="sxs-lookup"><span data-stu-id="37c1c-173">NAME: hello name of hello masquerading Windows module.</span></span>
* <span data-ttu-id="37c1c-174">路徑： hello 路徑 toohello 偽裝 Windows 模組。</span><span class="sxs-lookup"><span data-stu-id="37c1c-174">PATH: hello path toohello masquerading Windows module.</span></span>

<span data-ttu-id="37c1c-175">此警示也會擷取並顯示特定欄位 hello 模組的 PE 標頭，例如 「 總和檢查碼 」 和 「 時間 」 戳記。</span><span class="sxs-lookup"><span data-stu-id="37c1c-175">This alert also extracts and displays certain fields from hello module’s PE header, such as “CHECKSUM” and “TIMESTAMP.”</span></span> <span data-ttu-id="37c1c-176">只有 hello 欄位會出現在 hello 模組時，才會顯示這些欄位。</span><span class="sxs-lookup"><span data-stu-id="37c1c-176">These fields are only displayed if hello fields are present in hello module.</span></span> <span data-ttu-id="37c1c-177">請參閱 hello [Microsoft PE 和 COFF 規格](https://msdn.microsoft.com/windows/hardware/gg463119.aspx)如需詳細資訊，這些欄位上。</span><span class="sxs-lookup"><span data-stu-id="37c1c-177">See hello [Microsoft PE and COFF Specification](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) for details on these fields.</span></span>

<span data-ttu-id="37c1c-178">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="37c1c-178">This is an example of this type of alert:</span></span>

![偽裝的 Windows 警示](./media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a><span data-ttu-id="37c1c-180">探索到修改過的系統二進位檔</span><span class="sxs-lookup"><span data-stu-id="37c1c-180">Modified system binary discovered</span></span>
<span data-ttu-id="37c1c-181">惡意程式碼可能修改順序 toocovertly 存取資料的核心系統二進位碼檔案，或暗中遭到洩露的系統上保存。</span><span class="sxs-lookup"><span data-stu-id="37c1c-181">Malware may modify core system binaries in order toocovertly access data or surreptitiously persist on a compromised system.</span></span> <span data-ttu-id="37c1c-182">此警示表示 hello 損毀傾印分析程式偵測到核心 Windows 的 OS 二進位檔，已修改記憶體中或在磁碟上。</span><span class="sxs-lookup"><span data-stu-id="37c1c-182">This alert indicates that hello crash dump analysis has detected that core Windows OS binaries have been modified in memory or on disk.</span></span>

<span data-ttu-id="37c1c-183">合法軟體開發人員偶爾會為了非惡意的原因而修改記憶體中的系統模組，如 Detours 或處理應用程式相容性。</span><span class="sxs-lookup"><span data-stu-id="37c1c-183">Legitimate software developers occasionally modify system modules in memory for non-malicious reasons, such as Detours or for application compatibility.</span></span> <span data-ttu-id="37c1c-184">toohelp 區分惡意與潛在合法的模組時，Azure 資訊安全中心檢查 hello 修改的模組是否符合 tooa 可疑的設定檔。</span><span class="sxs-lookup"><span data-stu-id="37c1c-184">toohelp differentiate between malicious and potentially legitimate modules, Azure Security Center checks whether hello modified module conforms tooa suspicious profile.</span></span> <span data-ttu-id="37c1c-185">這項檢查的 hello 結果會指示 hello 嚴重性 hello 警示、 警示描述，以及警示的修復步驟。</span><span class="sxs-lookup"><span data-stu-id="37c1c-185">hello result of this check is indicated by hello severity of hello alert, alert description, and alert remediation steps.</span></span>

<span data-ttu-id="37c1c-186">此外 toohello 通用欄位前面 hello"Shellcode 探索 」 一節中所述，此警示提供下列其他欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="37c1c-186">In addition toohello common fields described earlier in hello “Shellcode discovered” section, this alert provides hello following additional fields:</span></span>

* <span data-ttu-id="37c1c-187">MODULENAME： 修改系統二進位 hello 的名稱。</span><span class="sxs-lookup"><span data-stu-id="37c1c-187">MODULENAME: Name of hello modified system binary.</span></span>
* <span data-ttu-id="37c1c-188">MODULEVERSION: Hello 的版本修改系統二進位檔案。</span><span class="sxs-lookup"><span data-stu-id="37c1c-188">MODULEVERSION: Version of hello modified system binary.</span></span>

<span data-ttu-id="37c1c-189">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="37c1c-189">This is an example of this type of alert:</span></span>

![系統二進位檔警示](./media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a><span data-ttu-id="37c1c-191">已執行可疑的處理序</span><span class="sxs-lookup"><span data-stu-id="37c1c-191">Suspicious process executed</span></span>
<span data-ttu-id="37c1c-192">資訊安全中心識別可疑的處理程序執行 hello 目標虛擬機器，而且會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="37c1c-192">Security Center identifies a suspicious process that runs on hello target virtual machine, and then triggers an alert.</span></span> <span data-ttu-id="37c1c-193">hello 偵測看起來不 hello 特定名稱，但看起來 hello 可執行檔的參數。</span><span class="sxs-lookup"><span data-stu-id="37c1c-193">hello detection doesn’t look for hello specific name, but does look for hello executable file's parameter.</span></span> <span data-ttu-id="37c1c-194">因此，即使 hello 攻擊者會重新命名可執行檔的 hello，資訊安全中心仍然可以偵測到 hello 可疑處理序。</span><span class="sxs-lookup"><span data-stu-id="37c1c-194">Therefore, even if hello attacker renames hello executable, Security Center can still detect hello suspicious process.</span></span>

<span data-ttu-id="37c1c-195">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="37c1c-195">This is an example of this type of alert:</span></span>

![可疑的處理序警示](./media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a><span data-ttu-id="37c1c-197">已查詢多個網域帳戶</span><span class="sxs-lookup"><span data-stu-id="37c1c-197">Multiple domain accounts queried</span></span>
<span data-ttu-id="37c1c-198">資訊安全中心可以偵測到多個嘗試 tooquery Active Directory 網域帳戶，這是通常由期間網路探查攻擊者。</span><span class="sxs-lookup"><span data-stu-id="37c1c-198">Security Center can detect multiple attempts tooquery Active Directory domain accounts, which is something usually performed by attackers during network reconnaissance.</span></span> <span data-ttu-id="37c1c-199">攻擊者可以利用這個技巧 tooquery hello 網域 tooidentify hello 使用者、 識別 hello 網域系統管理員帳戶，必須識別 hello 網域控制站，且也識別出 hello 潛在網域信任關係與其他網域的電腦。</span><span class="sxs-lookup"><span data-stu-id="37c1c-199">Attackers can leverage this technique tooquery hello domain tooidentify hello users, identify hello domain admin accounts, identify hello computers that are domain controllers, and also identify hello potential domain trust relationship with other domains.</span></span>

<span data-ttu-id="37c1c-200">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="37c1c-200">This is an example of this type of alert:</span></span>

![多個網域帳戶警示](./media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a><span data-ttu-id="37c1c-202">已列舉本機系統管理員群組成員</span><span class="sxs-lookup"><span data-stu-id="37c1c-202">Local Administrators group members were enumerated</span></span>

<span data-ttu-id="37c1c-203">Windows Server 2016 和 Windows 10 中的 hello 安全性事件 4798，觸發清理程序時，資訊安全中心 」 即將 tootrigger 警示。</span><span class="sxs-lookup"><span data-stu-id="37c1c-203">Security Center is going tootrigger an alert when hello security event 4798, in Windows Server 2016 and Windows 10, is trigged.</span></span> <span data-ttu-id="37c1c-204">這種情況會發生在本機系統管理員群組列舉時，通常是由攻擊者在網路偵察期間所執行。</span><span class="sxs-lookup"><span data-stu-id="37c1c-204">This happens when local administrator groups are enumerated, which is something usually performed by attackers during network reconnaissance.</span></span> <span data-ttu-id="37c1c-205">攻擊者可以利用這個技巧 tooquery hello 身分識別具有系統管理權限的使用者。</span><span class="sxs-lookup"><span data-stu-id="37c1c-205">Attackers can leverage this technique tooquery hello identity of users with administrative privileges.</span></span>

<span data-ttu-id="37c1c-206">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="37c1c-206">This is an example of this type of alert:</span></span>

![本機系統管理員](./media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a><span data-ttu-id="37c1c-208">異常混用大寫和小寫字元</span><span class="sxs-lookup"><span data-stu-id="37c1c-208">Anomalous mix of upper and lower case characters</span></span>

<span data-ttu-id="37c1c-209">當它偵測到 hello 混用大寫和小寫字元，在 hello 命令列使用資訊安全中心將會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="37c1c-209">Security Center will trigger an alert when it detects hello use of a mix of upper and lower case characters at hello command line.</span></span> <span data-ttu-id="37c1c-210">某些攻擊者可能會使用從區分大小寫這項技術 toohide 或雜湊型電腦的規則。</span><span class="sxs-lookup"><span data-stu-id="37c1c-210">Some attackers may use this technique toohide from case-sensitive or hash based machine rule.</span></span>

<span data-ttu-id="37c1c-211">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="37c1c-211">This is an example of this type of alert:</span></span>

![異常混用](./media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a><span data-ttu-id="37c1c-213">可疑的 Kerberos 黃金票證攻擊</span><span class="sxs-lookup"><span data-stu-id="37c1c-213">Suspected Kerberos Golden Ticket attack</span></span>

<span data-ttu-id="37c1c-214">洩漏[krbtgt](https://technet.microsoft.com/library/dn745899.aspx)攻擊者 toocreate Kerberos 「 黃金票證，「 允許 hello 攻擊者 tooimpersonate 他們希望任何使用者可以使用金鑰。</span><span class="sxs-lookup"><span data-stu-id="37c1c-214">A compromised [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) key can be used by an attacker toocreate Kerberos "Golden Tickets," allowing hello attacker tooimpersonate any user they wish.</span></span> <span data-ttu-id="37c1c-215">資訊安全中心即將 tootrigger 警示，當它偵測到這種類型的活動。</span><span class="sxs-lookup"><span data-stu-id="37c1c-215">Security Center is going tootrigger an alert when it detects this type of activity.</span></span>

> [!NOTE] 
> <span data-ttu-id="37c1c-216">如需 Kerberos 黃金票證的詳細資訊，請參閱 [Windows 10 認證竊取風險降低指南](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx)。</span><span class="sxs-lookup"><span data-stu-id="37c1c-216">For more information about Kerberos Golden Ticket, read [Windows 10 credential theft mitigation guide](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx).</span></span>

<span data-ttu-id="37c1c-217">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="37c1c-217">This is an example of this type of alert:</span></span>

![黃金票證](./media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a><span data-ttu-id="37c1c-219">已建立可疑帳戶</span><span class="sxs-lookup"><span data-stu-id="37c1c-219">Suspicious account created</span></span>

<span data-ttu-id="37c1c-220">若建立與現有內建系統管理權限帳戶非常相似的帳戶，資訊安全中心就會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="37c1c-220">Security Center will trigger an alert when an account is created with close resemblance of an existing built in administrative privilege account.</span></span> <span data-ttu-id="37c1c-221">這項技術可由攻擊者 toocreate rogue 帳戶 tooavoid 被注意到人力驗證所使用。</span><span class="sxs-lookup"><span data-stu-id="37c1c-221">This technique can be used by attackers toocreate a rogue account tooavoid being noticed by human verification.</span></span>
 
<span data-ttu-id="37c1c-222">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="37c1c-222">This is an example of this type of alert:</span></span>

![可疑的帳戶](./media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a><span data-ttu-id="37c1c-224">已建立可疑的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="37c1c-224">Suspicious Firewall rule created</span></span>

<span data-ttu-id="37c1c-225">攻擊者可能會嘗試 toocircumvent 主機安全性，藉由建立自訂的防火牆規則 tooallow 惡意應用程式 toocommunicate 命令與控制，或透過 hello 網路透過 hello toolaunch 攻擊危害的主機。</span><span class="sxs-lookup"><span data-stu-id="37c1c-225">Attackers might try toocircumvent host security by creating custom firewall rules tooallow malicious applications toocommunicate with command and control, or toolaunch attacks through hello network via hello compromised host.</span></span> <span data-ttu-id="37c1c-226">資訊安全中心偵測到從可疑位置的可執行檔建立的新防火牆規則時，就會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="37c1c-226">Security Center will trigger an alert when it detects that a new firewall rule was created from an executable file in a suspicious location.</span></span>
 
<span data-ttu-id="37c1c-227">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="37c1c-227">This is an example of this type of alert:</span></span>

![防火牆規則](./media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a><span data-ttu-id="37c1c-229">可疑的 HTA 和 PowerShell 組合</span><span class="sxs-lookup"><span data-stu-id="37c1c-229">Suspicious combination of HTA and PowerShell</span></span>

<span data-ttu-id="37c1c-230">資訊安全中心偵測到 Microsoft HTML 應用程式主機 (HTA) 正在啟動 PowerShell 命令時會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="37c1c-230">Security Center will trigger an alert when it detects that a Microsoft HTML Application Host (HTA) is launching PowerShell commands.</span></span> <span data-ttu-id="37c1c-231">這是攻擊者 toolaunch 惡意 PowerShell 指令碼所使用的技術。</span><span class="sxs-lookup"><span data-stu-id="37c1c-231">This is a technique used by attackers toolaunch malicious PowerShell scripts.</span></span>
 
<span data-ttu-id="37c1c-232">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="37c1c-232">This is an example of this type of alert:</span></span>

![HTA 和 PS](./media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a><span data-ttu-id="37c1c-234">網路分析</span><span class="sxs-lookup"><span data-stu-id="37c1c-234">Network analysis</span></span>
<span data-ttu-id="37c1c-235">資訊安全中心網路威脅偵測的運作方式如下：從 Azure IPFIX (Internet Protocol Flow Information Export) 流量自動收集安全性資訊。</span><span class="sxs-lookup"><span data-stu-id="37c1c-235">Security Center network threat detection works by automatically collecting security information from your Azure IPFIX (Internet Protocol Flow Information Export) traffic.</span></span> <span data-ttu-id="37c1c-236">它會分析這項資訊通常相互關聯多個來源，tooidentify 威脅的資訊。</span><span class="sxs-lookup"><span data-stu-id="37c1c-236">It analyzes this information, often correlating information from multiple sources, tooidentify threats.</span></span>

### <a name="suspicious-outgoing-traffic-detected"></a><span data-ttu-id="37c1c-237">偵測到可疑的連出流量</span><span class="sxs-lookup"><span data-stu-id="37c1c-237">Suspicious outgoing traffic detected</span></span>
<span data-ttu-id="37c1c-238">網路裝置可探索和剖析多 hello 與其他的系統類型相同的方式。</span><span class="sxs-lookup"><span data-stu-id="37c1c-238">Network devices can be discovered and profiled in much hello same way as other types of systems.</span></span> <span data-ttu-id="37c1c-239">攻擊者通常會使用連接埠掃描或連接埠掃掠來開始攻擊。</span><span class="sxs-lookup"><span data-stu-id="37c1c-239">Attackers usually start with port scanning or port sweeping.</span></span> <span data-ttu-id="37c1c-240">在 hello 下一個範例中，您必須從 VM 的可疑安全殼層 (SSH) 流量。</span><span class="sxs-lookup"><span data-stu-id="37c1c-240">In hello next example, you have suspicious Secure Shell (SSH) traffic from a VM.</span></span> <span data-ttu-id="37c1c-241">在此案例中，可能有對外部資源的 SSH 暴力密碼破解或連接埠掃掠攻擊。</span><span class="sxs-lookup"><span data-stu-id="37c1c-241">In this scenario, SSH brute force or a port sweeping attack against an external resource is possible.</span></span>

![可疑連出流量警示](./media/security-center-alerts-type/security-center-alerts-type-fig8.png)

<span data-ttu-id="37c1c-243">此警示會提供資訊，您可以使用 tooidentify hello 資源所使用的 tooinitiate 這種攻擊。</span><span class="sxs-lookup"><span data-stu-id="37c1c-243">This alert gives information that you can use tooidentify hello resource that was used tooinitiate this attack.</span></span> <span data-ttu-id="37c1c-244">此警示也會提供 tooidentify hello 入侵電腦、 hello 偵測時間，加上 hello 通訊協定和連接埠所使用的資訊。</span><span class="sxs-lookup"><span data-stu-id="37c1c-244">This alert also provides information tooidentify hello compromised machine, hello detection time, plus hello protocol and port that was used.</span></span> <span data-ttu-id="37c1c-245">此刀鋒視窗也可讓您可以的補救步驟的清單是使用的 toomitigate 此問題。</span><span class="sxs-lookup"><span data-stu-id="37c1c-245">This blade also gives you a list of remediation steps that can be used toomitigate this issue.</span></span>

### <a name="network-communication-with-a-malicious-machine"></a><span data-ttu-id="37c1c-246">與惡意電腦的網路通訊</span><span class="sxs-lookup"><span data-stu-id="37c1c-246">Network communication with a malicious machine</span></span>
<span data-ttu-id="37c1c-247">藉由利用 Microsoft 威脅情報摘要，Azure 資訊安全中心可以偵測與惡意 IP 位址通訊的遭入侵電腦。</span><span class="sxs-lookup"><span data-stu-id="37c1c-247">By leveraging Microsoft threat intelligence feeds, Azure Security Center can detect compromised machines that communicate with malicious IP addresses.</span></span> <span data-ttu-id="37c1c-248">在許多情況下，hello 惡意位址會是命令和控制中心。</span><span class="sxs-lookup"><span data-stu-id="37c1c-248">In many cases, hello malicious address is a command and control center.</span></span> <span data-ttu-id="37c1c-249">在此情況下，資訊安全中心偵測到使用騎小馬載入器惡意程式碼，已完成，hello 通訊 (也稱為[Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF))。</span><span class="sxs-lookup"><span data-stu-id="37c1c-249">In this case, Security Center detected that hello communication was done by using Pony Loader malware (also known as [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).</span></span>

![網路通訊警示](./media/security-center-alerts-type/security-center-alerts-type-fig9.png)

<span data-ttu-id="37c1c-251">此警示所提供的資訊，可讓您所使用的 tooinitiate tooidentify hello 資源這種攻擊，hello 攻擊資源、 hello 犧牲者的 IP、 hello 攻擊者的 IP，以及 hello 偵測時間。</span><span class="sxs-lookup"><span data-stu-id="37c1c-251">This alert gives information that enables you tooidentify hello resource that was used tooinitiate this attack, hello attacked resource, hello victim IP, hello attacker IP, and hello detection time.</span></span>

> [!NOTE]
> <span data-ttu-id="37c1c-252">為了保護隱私權，此螢幕擷取畫面的即時 IP 位址已遭到移除。</span><span class="sxs-lookup"><span data-stu-id="37c1c-252">Live IP addresses were removed from this screenshot for privacy purpose.</span></span>
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a><span data-ttu-id="37c1c-253">偵測到可能的連出拒絕服務攻擊</span><span class="sxs-lookup"><span data-stu-id="37c1c-253">Possible outgoing denial-of-service attack detected</span></span>
<span data-ttu-id="37c1c-254">異常來自一部虛擬機器的網路流量可能導致資訊安全中心 tootrigger 潛在的阻絕服務類型的攻擊。</span><span class="sxs-lookup"><span data-stu-id="37c1c-254">Abnormal network traffic that originates from one virtual machine can cause Security Center tootrigger a potential denial-of-service type of attack.</span></span>

<span data-ttu-id="37c1c-255">以下是本類型之警示的範例：</span><span class="sxs-lookup"><span data-stu-id="37c1c-255">This is an example of this type of alert:</span></span>

![連出 DOS](./media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a><span data-ttu-id="37c1c-257">資源分析</span><span class="sxs-lookup"><span data-stu-id="37c1c-257">Resource analysis</span></span>
<span data-ttu-id="37c1c-258">資訊安全中心資源分析著重於在平台服務 (PaaS) 服務，例如以 hello hello 整合[Azure SQL Database 威脅偵測](../sql-database/sql-database-threat-detection.md)功能。</span><span class="sxs-lookup"><span data-stu-id="37c1c-258">Security Center resource analysis focuses on platform as a service (PaaS) services, such as hello integration with hello [Azure SQL Database threat detection](../sql-database/sql-database-threat-detection.md) feature.</span></span> <span data-ttu-id="37c1c-259">根據這些區域中的 hello 分析結果，資訊安全中心觸發程序資源相關的警示。</span><span class="sxs-lookup"><span data-stu-id="37c1c-259">Based on hello analysis’s results from these areas, Security Center triggers a resource-related alert.</span></span>

### <a name="potential-sql-injection"></a><span data-ttu-id="37c1c-260">潛在的 SQL 插入式攻擊</span><span class="sxs-lookup"><span data-stu-id="37c1c-260">Potential SQL injection</span></span>
<span data-ttu-id="37c1c-261">SQL 資料隱碼攻擊是惡意程式碼插入到稍後傳遞 tooan SQL Server 執行個體進行剖析和執行的字串的位置。</span><span class="sxs-lookup"><span data-stu-id="37c1c-261">SQL injection is an attack where malicious code is inserted into strings that are later passed tooan instance of SQL Server for parsing and execution.</span></span> <span data-ttu-id="37c1c-262">因為 SQL Server 會執行它收到的所有語法上有效的查詢，所以建構 SQL 陳述式的任何程序皆應檢閱其中是否有插入式攻擊弱點。</span><span class="sxs-lookup"><span data-stu-id="37c1c-262">Because SQL Server executes all syntactically valid queries that it receives, any procedure that constructs SQL statements should be reviewed for injection vulnerabilities.</span></span> <span data-ttu-id="37c1c-263">機器學習、 行為分析，以及異常偵測 toodetermine 可疑事件的執行時間可能您的 Azure SQL 資料庫中的位置，則會使用 SQL 威脅偵測。</span><span class="sxs-lookup"><span data-stu-id="37c1c-263">SQL Threat Detection uses machine learning, behavioral analysis, and anomaly detection toodetermine suspicious events that might be taking place in your Azure SQL databases.</span></span> <span data-ttu-id="37c1c-264">例如：</span><span class="sxs-lookup"><span data-stu-id="37c1c-264">For example:</span></span>

* <span data-ttu-id="37c1c-265">離職員工嘗試的資料庫存取</span><span class="sxs-lookup"><span data-stu-id="37c1c-265">Attempted database access by a former employee</span></span>
* <span data-ttu-id="37c1c-266">SQL 插入式攻擊</span><span class="sxs-lookup"><span data-stu-id="37c1c-266">SQL injection attacks</span></span>
* <span data-ttu-id="37c1c-267">在使用者在家中的不尋常的存取 tooa 生產資料庫</span><span class="sxs-lookup"><span data-stu-id="37c1c-267">Unusual access tooa production database from a user at home</span></span>

![潛在的 SQL 插入式攻擊警示](./media/security-center-alerts-type/security-center-alerts-type-fig11.png)

<span data-ttu-id="37c1c-269">在這項警示的 hello 資訊可能會使用的 tooidentify 遭受攻擊的 hello 資源、 hello 偵測時間，以及 hello 攻擊 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="37c1c-269">hello information in this alert can be used tooidentify hello attacked resource, hello detection time, and hello state of hello attack.</span></span> <span data-ttu-id="37c1c-270">它也提供一個連結 toofurther 調查步驟。</span><span class="sxs-lookup"><span data-stu-id="37c1c-270">It also provides a link toofurther investigation steps.</span></span>

### <a name="vulnerability-toosql-injection"></a><span data-ttu-id="37c1c-271">弱點 tooSQL 資料隱碼</span><span class="sxs-lookup"><span data-stu-id="37c1c-271">Vulnerability tooSQL Injection</span></span>
<span data-ttu-id="37c1c-272">在資料庫上偵測到應用程式錯誤時，會觸發此警示。</span><span class="sxs-lookup"><span data-stu-id="37c1c-272">This alert is triggered when an application error is detected on a database.</span></span> <span data-ttu-id="37c1c-273">此警示可能表示可能的弱點可能會 tooSQL 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="37c1c-273">This alert may indicate a possible vulnerability tooSQL injection attacks.</span></span>

![潛在的 SQL 插入式攻擊警示](./media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a><span data-ttu-id="37c1c-275">來自不熟悉位置的異常存取</span><span class="sxs-lookup"><span data-stu-id="37c1c-275">Unusual access from unfamiliar location</span></span>
<span data-ttu-id="37c1c-276">找不到 hello 最後期間的 hello 伺服器上偵測到來自不熟悉的 IP 位址存取事件時，會觸發此警示。</span><span class="sxs-lookup"><span data-stu-id="37c1c-276">This alert is triggered when an access event from an unfamiliar IP address was detected on hello server, which was not seen in hello last period.</span></span>

![異常存取警示](./media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="contextual-information"></a><span data-ttu-id="37c1c-278">內容相關的資訊</span><span class="sxs-lookup"><span data-stu-id="37c1c-278">Contextual information</span></span>
<span data-ttu-id="37c1c-279">在調查中，分析師需要額外的內容 tooreach hello 威脅 hello 本質相關的結論以及 toomitigate 它。</span><span class="sxs-lookup"><span data-stu-id="37c1c-279">During an investigation, analysts need extra context tooreach a verdict about hello nature of hello threat and how toomitigate it.</span></span>  <span data-ttu-id="37c1c-280">例如，網路異常偵測，但不了解其他事 hello 網路上或考慮 toohello 目標資源具有它是每個硬碟 toounderstand 何種動作 tootake 下一步。</span><span class="sxs-lookup"><span data-stu-id="37c1c-280">For example, a network anomaly was detected, but without understanding what else is happening on hello network or with regard toohello targeted resource it is every hard toounderstand what actions tootake next.</span></span> <span data-ttu-id="37c1c-281">與 tooaid，安全性事件可能包含的成品、 相關的事件和資訊可能有助於 hello 調查。</span><span class="sxs-lookup"><span data-stu-id="37c1c-281">tooaid with that, a Security Incident may include artifacts, related events and information that may help hello investigator.</span></span> <span data-ttu-id="37c1c-282">hello 可用性的其他資訊會隨著 hello 偵測到威脅的型別和 hello 您環境的設定，且將無法使用所有安全性事件。</span><span class="sxs-lookup"><span data-stu-id="37c1c-282">hello availability of additional information will vary based on hello type of threat detected and hello configuration of your environment, and will not be available for all Security Incidents.</span></span>

<span data-ttu-id="37c1c-283">其他資訊是否可用，它將會顯示在 hello 安全性事件的警示 hello 清單下方。</span><span class="sxs-lookup"><span data-stu-id="37c1c-283">If additional information is available, it will be shown in hello Security Incident below hello list of alerts.</span></span> <span data-ttu-id="37c1c-284">這可能包括的資訊如：</span><span class="sxs-lookup"><span data-stu-id="37c1c-284">This could contain information like:</span></span>

- <span data-ttu-id="37c1c-285">清除事件記錄</span><span class="sxs-lookup"><span data-stu-id="37c1c-285">Log clear events</span></span>
- <span data-ttu-id="37c1c-286">從未知裝置插入的 PNP 裝置</span><span class="sxs-lookup"><span data-stu-id="37c1c-286">PNP device plugged from unknown device</span></span>
- <span data-ttu-id="37c1c-287">不可採取動作的警示</span><span class="sxs-lookup"><span data-stu-id="37c1c-287">Alerts which are not actionable</span></span> 

![異常存取警示](./media/security-center-alerts-type/security-center-alerts-type-fig20.png) 


## <a name="see-also"></a><span data-ttu-id="37c1c-289">另請參閱</span><span class="sxs-lookup"><span data-stu-id="37c1c-289">See also</span></span>
<span data-ttu-id="37c1c-290">在本文中，您學會有關 hello 不同警示類型的安全性資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="37c1c-290">In this article, you learned about hello different types of security alerts in Security Center.</span></span> <span data-ttu-id="37c1c-291">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="37c1c-291">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="37c1c-292">在 Azure 資訊安全中心處理安全性事件</span><span class="sxs-lookup"><span data-stu-id="37c1c-292">Handling security incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="37c1c-293">Azure 資訊安全中心的偵測功能</span><span class="sxs-lookup"><span data-stu-id="37c1c-293">Azure Security Center detection capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="37c1c-294">Azure 資訊安全中心規劃和操作指南</span><span class="sxs-lookup"><span data-stu-id="37c1c-294">Azure Security Center planning and operations guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="37c1c-295">[Azure 資訊安全中心常見問題集](security-center-faq.md)： 尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="37c1c-295">[Azure Security Center FAQ](security-center-faq.md): Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="37c1c-296">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)：尋找有關 Azure 安全性與合規性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="37c1c-296">[Azure security blog](http://blogs.msdn.com/b/azuresecurity/): Find blog posts about Azure security and compliance.</span></span>
