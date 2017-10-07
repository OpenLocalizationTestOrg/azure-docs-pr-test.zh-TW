---
title: "aaaProtect 個人資料與 Azure 資訊安全中心 |Microsoft 文件"
description: "使用 Azure 資訊安全中心保護個人資料"
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
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="a2912-103">保護個人資料免受入侵和攻擊：Azure 資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="a2912-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="a2912-104">本文將協助您了解如何 toouse Azure 資訊安全中心 tooprotect 個人資料與破壞，攻擊。</span><span class="sxs-lookup"><span data-stu-id="a2912-104">This article will help you understand how toouse Azure Security Center tooprotect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="a2912-105">案例</span><span class="sxs-lookup"><span data-stu-id="a2912-105">Scenario</span></span> 

<span data-ttu-id="a2912-106">大型出航公司搬遷後在 hello 美國，展開在 hello 地中海與波羅的海文海，以及 hello 不列顛群島其作業 toooffer 行程。</span><span class="sxs-lookup"><span data-stu-id="a2912-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="a2912-107">toohelp 中這些工作，它所取得數個較小的出航行位於義大利、 德國、 丹麥和 hello 英國</span><span class="sxs-lookup"><span data-stu-id="a2912-107">toohelp in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="a2912-108">hello 公司使用 Microsoft Azure toostore 公司資料 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="a2912-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="a2912-109">其中包含名稱、地址、電話號碼和信用卡資訊等個人識別資訊。</span><span class="sxs-lookup"><span data-stu-id="a2912-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="a2912-110">它也包含類似如下的人力資源資訊：</span><span class="sxs-lookup"><span data-stu-id="a2912-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="a2912-111">位址</span><span class="sxs-lookup"><span data-stu-id="a2912-111">Addresses</span></span>
- <span data-ttu-id="a2912-112">電話號碼</span><span class="sxs-lookup"><span data-stu-id="a2912-112">Phone numbers</span></span>
- <span data-ttu-id="a2912-113">稅務識別編號</span><span class="sxs-lookup"><span data-stu-id="a2912-113">Tax identification numbers</span></span>
- <span data-ttu-id="a2912-114">醫療資訊</span><span class="sxs-lookup"><span data-stu-id="a2912-114">Medical information</span></span>

<span data-ttu-id="a2912-115">hello 出航列也會維護報酬和忠誠度計劃成員大型資料庫。</span><span class="sxs-lookup"><span data-stu-id="a2912-115">hello cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="a2912-116">位於 hello 世界各地的公司員工存取 hello 網路從 hello 公司遠端辦公室和旅行代理程式已存取 toosome 公司資源。</span><span class="sxs-lookup"><span data-stu-id="a2912-116">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>
<span data-ttu-id="a2912-117">個人資料會傳送 hello 網路中，這些位置與 hello Microsoft 資料中心之間。</span><span class="sxs-lookup"><span data-stu-id="a2912-117">Personal data travels across hello network between these locations and hello Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="a2912-118">問題陳述</span><span class="sxs-lookup"><span data-stu-id="a2912-118">Problem statement</span></span>

<span data-ttu-id="a2912-119">hello 公司是擔心 hello 威脅的攻擊，在他們的 Azure 資源上。</span><span class="sxs-lookup"><span data-stu-id="a2912-119">hello company is concerned about hello threat of attacks on their Azure resources.</span></span> <span data-ttu-id="a2912-120">他們想 tooprevent 公開客戶的和員工的個人資料 toounauthorized 人員。</span><span class="sxs-lookup"><span data-stu-id="a2912-120">They want tooprevent exposure of customers’ and employees’ personal data toounauthorized persons.</span></span> <span data-ttu-id="a2912-121">他們想防止和回應/修復所造成，以及與其雲端資源有效地 toomonitor hello 持續安全性的指引。</span><span class="sxs-lookup"><span data-stu-id="a2912-121">They want guidance on both prevention and response/remediation, as well as an effective way toomonitor hello ongoing security of their cloud resources.</span></span>
<span data-ttu-id="a2912-122">他們需要堅強的防線來抵禦今日複雜且有組織的攻擊者。</span><span class="sxs-lookup"><span data-stu-id="a2912-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="a2912-123">公司目標</span><span class="sxs-lookup"><span data-stu-id="a2912-123">Company goal</span></span>

<span data-ttu-id="a2912-124">其中一個 hello 公司的目標是客戶和員工的個人資料 tooensure hello 隱私權保護不受威脅。</span><span class="sxs-lookup"><span data-stu-id="a2912-124">One of hello company’s goals is tooensure hello privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="a2912-125">其目標是 toorespond 立即的缺口 toomitigate toosigns hello 影響。</span><span class="sxs-lookup"><span data-stu-id="a2912-125">One of their goals is toorespond immediately toosigns of breach toomitigate hello impact.</span></span> <span data-ttu-id="a2912-126">它需要 tooassess hello 目前的安全性狀態的方式、 識別易受攻擊的組態，並進行補救。</span><span class="sxs-lookup"><span data-stu-id="a2912-126">It requires a way tooassess hello current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="a2912-127">解決方案</span><span class="sxs-lookup"><span data-stu-id="a2912-127">Solutions</span></span>

<span data-ttu-id="a2912-128">Microsoft Azure 資訊安全中心 (ASC) 提供了整合式安全性監控和原則管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="a2912-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="a2912-129">它提供威脅預防、偵測及回應功能，簡單易用又有效。</span><span class="sxs-lookup"><span data-stu-id="a2912-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="a2912-130">預防</span><span class="sxs-lookup"><span data-stu-id="a2912-130">Prevention</span></span>

<span data-ttu-id="a2912-131">ASC 有助於讓您 tooset 安全性原則，以避免破壞，提供在 just-in-time 存取，並實作安全性建議。</span><span class="sxs-lookup"><span data-stu-id="a2912-131">ASC helps you prevent breaches by enabling you tooset security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="a2912-132">安全性原則會定義控制項中指定的 hello 資源的建議 hello 組訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2912-132">A security policy defines hello set of controls recommended for resources within hello specified subscription.</span></span> <span data-ttu-id="a2912-133">在可以存取使用的 toolock 輸入的流量 tooyour Azure Vm，降低暴露 tooattacks 關閉。</span><span class="sxs-lookup"><span data-stu-id="a2912-133">Just in time access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks.</span></span> <span data-ttu-id="a2912-134">安全性建議會分析您的 Azure 資源 hello 安全性狀態後建立 ASC。</span><span class="sxs-lookup"><span data-stu-id="a2912-134">Security recommendations are created by ASC after analyzing hello security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="a2912-135">如何在 ASC 設定安全性原則？</span><span class="sxs-lookup"><span data-stu-id="a2912-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="a2912-136">您可以為每個訂用帳戶設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="a2912-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="a2912-137">toomodify 安全性原則，您必須是擁有者或參與者的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2912-137">toomodify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="a2912-138">在 hello Azure 入口網站，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="a2912-138">In hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="a2912-139">選取**原則**hello ASC 儀表板中。</span><span class="sxs-lookup"><span data-stu-id="a2912-139">Select **Policy** in hello ASC dashboard.</span></span>

2. <span data-ttu-id="a2912-140">選取您想要 tooenable hello 原則 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2912-140">Select hello subscription on which you want tooenable hello policy.</span></span>

3. <span data-ttu-id="a2912-141">選擇**防止原則**tooconfigure 每個訂閱的原則。</span><span class="sxs-lookup"><span data-stu-id="a2912-141">Choose **Prevention policy** tooconfigure policies per subscription.</span></span> <span data-ttu-id="a2912-142">**從虛擬機器收集資料**應該設定太**上。**</span><span class="sxs-lookup"><span data-stu-id="a2912-142">**Collect data from virtual machines** should be set too**On.**</span></span>

4. <span data-ttu-id="a2912-143">在 hello**防止原則**選項中，選取**上**hello 訂用帳戶相關的 tooenable hello 安全性建議。</span><span class="sxs-lookup"><span data-stu-id="a2912-143">In hello **Prevention policy** options, select **On** tooenable hello security recommendations that are relevant for hello subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="a2912-144">如需詳細指示，以及每個可啟用的 hello 原則建議的說明，請參閱[Azure 資訊安全中心中設定安全性原則](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies)。</span><span class="sxs-lookup"><span data-stu-id="a2912-144">For more detailed instructions and an explanation of each of hello policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="a2912-145">如何設定 Just-In-Time (JIT) 存取？</span><span class="sxs-lookup"><span data-stu-id="a2912-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="a2912-146">啟用 JIT 時，資訊安全中心鎖定輸入的流量 tooyour Azure Vm 建立 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="a2912-146">When JIT is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="a2912-147">您選取 hello 連接埠上 hello VM toowhich 輸入的流量會鎖定。</span><span class="sxs-lookup"><span data-stu-id="a2912-147">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="a2912-148">toouse JIT 存取，請執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="a2912-148">toouse JIT access, do hello following:</span></span>

1. <span data-ttu-id="a2912-149">選取 hello**時間 VM 存取磚中的恰好**hello ASC 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="a2912-149">Select hello **Just in time VM access tile** on hello ASC blade.</span></span>

2. <span data-ttu-id="a2912-150">選取 hello**建議** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a2912-150">Select hello **Recommended** tab.</span></span>

3. <span data-ttu-id="a2912-151">在下**Vm**，選取您想 tooenable hello Vm。</span><span class="sxs-lookup"><span data-stu-id="a2912-151">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="a2912-152">這會使核取記號下一步 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="a2912-152">This puts a checkmark next tooa VM.</span></span> 
4. <span data-ttu-id="a2912-153">在 VM 上選取 [啟用 JIT]。</span><span class="sxs-lookup"><span data-stu-id="a2912-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="a2912-154">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="a2912-154">Select **Save**.</span></span>

<span data-ttu-id="a2912-155">然後您就可以看到 ASC 建議啟用 JIT hello 預設連接埠。</span><span class="sxs-lookup"><span data-stu-id="a2912-155">Then you can see hello default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="a2912-156">您也可以加入，並設定新的連接埠，您想要只在時間方案 tooenable hello。</span><span class="sxs-lookup"><span data-stu-id="a2912-156">You can also add and configure a new port on which you want tooenable hello just in time solution.</span></span> <span data-ttu-id="a2912-157">hello**階段 VM 存取中的恰好**hello 資訊安全中心中的磚會顯示 hello 設定 JIT 權限的 Vm 數目。</span><span class="sxs-lookup"><span data-stu-id="a2912-157">hello **Just in time VM access** tile in hello Security Center shows hello number of VMs configured for JIT access.</span></span> <span data-ttu-id="a2912-158">它也會顯示 hello 核准的存取提出的要求數目 hello 在過去一週。</span><span class="sxs-lookup"><span data-stu-id="a2912-158">It also shows hello number of approved access requests made in hello last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="a2912-159">如需有關指示 toodo，以及其他有關恰好階段存取，請參閱[管理只在時間中使用的虛擬機器存取權。](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span><span class="sxs-lookup"><span data-stu-id="a2912-159">For instructions on how toodo this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="a2912-160">如何實作 ASC 安全性建議？</span><span class="sxs-lookup"><span data-stu-id="a2912-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="a2912-161">當資訊安全中心識別潛在的安全性弱點時，它會建立建議。</span><span class="sxs-lookup"><span data-stu-id="a2912-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="a2912-162">hello 建議會引導您完成設定所需的 hello 控制項的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="a2912-162">hello recommendations guide you through hello process of configuring hello needed controls.</span></span> 
1. <span data-ttu-id="a2912-163">選取 hello**建議**hello ASC 儀表板上的磚。</span><span class="sxs-lookup"><span data-stu-id="a2912-163">Select hello **Recommendations** tile on hello ASC dashboard.</span></span>

2. <span data-ttu-id="a2912-164">檢視會顯示以資料表格式，其中每一行代表一個建議的 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="a2912-164">View hello recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="a2912-165">toofilter 建議選取**篩選**並選取您想 toosee hello 嚴重性和狀態值。</span><span class="sxs-lookup"><span data-stu-id="a2912-165">toofilter recommendations, select **Filter** and select hello severity and state values you wish toosee.</span></span>

4. <span data-ttu-id="a2912-166">toodismiss 不適用的建議，您可以以滑鼠右鍵按一下並選取**解除。**</span><span class="sxs-lookup"><span data-stu-id="a2912-166">toodismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="a2912-167">評估應該先套用的建議。</span><span class="sxs-lookup"><span data-stu-id="a2912-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="a2912-168">適用於 hello 建議的優先順序。</span><span class="sxs-lookup"><span data-stu-id="a2912-168">Apply hello recommendations in order of priority.</span></span>

<span data-ttu-id="a2912-169">如需可能的建議和逐步解說如何 tooapply 每個，請參閱[管理 Azure 資訊安全中心中的安全性建議。](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span><span class="sxs-lookup"><span data-stu-id="a2912-169">For a list of possible recommendations and walk-throughs on how tooapply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="a2912-170">偵測和回應</span><span class="sxs-lookup"><span data-stu-id="a2912-170">Detection and Response</span></span>

<span data-ttu-id="a2912-171">偵測和回應會一起使用，因為您之後想要 toorespond 盡快偵測到威脅。</span><span class="sxs-lookup"><span data-stu-id="a2912-171">Detection and response go together, as you want toorespond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="a2912-172">ASC 威脅偵測的運作方式自動收集您的 Azure 資源、 hello 網路和連線的交易夥伴方案中的 安全性資訊。</span><span class="sxs-lookup"><span data-stu-id="a2912-172">ASC threat detection works by automatically collecting security information from your Azure resources, hello network, and connected partner solutions.</span></span> <span data-ttu-id="a2912-173">ASC 可以在攻擊者發行新的和日益複雜的攻擊時，快速地更新其偵測演算法。</span><span class="sxs-lookup"><span data-stu-id="a2912-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="a2912-174">如需 ASC 威脅偵測運作方式的詳細資訊，請參閱 [Azure 資訊安全中心的偵測功能](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)。</span><span class="sxs-lookup"><span data-stu-id="a2912-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a><span data-ttu-id="a2912-175">如何管理及回應 toosecurity 警示？</span><span class="sxs-lookup"><span data-stu-id="a2912-175">How do I manage and respond toosecurity alerts?</span></span>

<span data-ttu-id="a2912-176">優先順序的安全性警示的清單會顯示在資訊安全中心，以及 hello 資訊需要 tooquickly 調查 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="a2912-176">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem.</span></span> <span data-ttu-id="a2912-177">資訊安全中心也包含如何建議 tooremediate 攻擊。</span><span class="sxs-lookup"><span data-stu-id="a2912-177">Security Center also includes recommendations for how tooremediate an attack.</span></span> <span data-ttu-id="a2912-178">您的安全性警示，執行下列的 hello toomanage:</span><span class="sxs-lookup"><span data-stu-id="a2912-178">toomanage your security alerts, do hello following:</span></span>

1. <span data-ttu-id="a2912-179">選取 hello**安全性警示**磚 hello ASC 儀表板中。</span><span class="sxs-lookup"><span data-stu-id="a2912-179">Select hello **Security alerts** tile in hello ASC dashboard.</span></span> <span data-ttu-id="a2912-180">這會顯示每個警示的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a2912-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="a2912-181">根據日期、 狀態和嚴重性，toofilter 警示選取**篩選**，然後選取您想要 toosee hello 值。</span><span class="sxs-lookup"><span data-stu-id="a2912-181">toofilter alerts based on date, state, and severity, select **Filter** and then select hello values you want toosee.</span></span>

3. <span data-ttu-id="a2912-182">toorespond tooan 警示，請選取它並檢閱 hello 的詳細資訊，然後選取遭到攻擊的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="a2912-182">toorespond tooan alert, select it and review hello information, then select hello resource that was attacked.</span></span>

4. <span data-ttu-id="a2912-183">在 [hello**描述**] 欄位中，您會看到的詳細資訊，包括建議的修復。</span><span class="sxs-lookup"><span data-stu-id="a2912-183">In hello **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="a2912-184">如需詳細指示回應 toosecurity 警示，請參閱[中 Azure 資訊安全中心的管理，而且有回應 toosecurity 警示。](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span><span class="sxs-lookup"><span data-stu-id="a2912-184">For more detailed instructions on responding toosecurity alerts, see [Managing and responding toosecurity alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="a2912-185">取得進一步的協助調查安全性警示，hello 公司可以有它自己的 SIEM 解決方案，整合 ASC 警示使用[Azure 記錄檔整合](https://aka.ms/AzLog)。</span><span class="sxs-lookup"><span data-stu-id="a2912-185">For further help in investigating security alerts, hello company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="a2912-186">如何管理安全性事件？</span><span class="sxs-lookup"><span data-stu-id="a2912-186">How do I manage security incidents?</span></span>

<span data-ttu-id="a2912-187">在 ASC 中，安全性事件是符合攻擊鏈模式之資源的所有警示彙總。</span><span class="sxs-lookup"><span data-stu-id="a2912-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="a2912-188">事件會顯示 hello 相關警示清單，可讓您 tooobtain 每次出現的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a2912-188">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span> <span data-ttu-id="a2912-189">事件會出現在 安全性警示磚的 hello 和刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a2912-189">Incidents appear in hello Security Alerts tile and blade.</span></span>

<span data-ttu-id="a2912-190">tooreview 及管理安全性事件，請執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="a2912-190">tooreview and manage security incidents, do hello following:</span></span>

1. <span data-ttu-id="a2912-191">選取 hello**安全性警示**磚。</span><span class="sxs-lookup"><span data-stu-id="a2912-191">Select hello **Security alerts** tile.</span></span> <span data-ttu-id="a2912-192">如果偵測到安全性事件時，它會顯示 hello 安全性警示圖表下方。</span><span class="sxs-lookup"><span data-stu-id="a2912-192">if a security incident is detected, it will appear under hello security alerts graph.</span></span> <span data-ttu-id="a2912-193">它會有不同於其他警示的圖示。</span><span class="sxs-lookup"><span data-stu-id="a2912-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="a2912-194">選取 hello 事件 toosee 此安全性事件相關的更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a2912-194">Select hello incident toosee more details about this security incident.</span></span> <span data-ttu-id="a2912-195">包含其完整描述，其嚴重性、 其目前狀態、 遭受攻擊的 hello 資源，hello 修復步驟 hello 事件的詳細資訊和 hello 已包含在此事件的警示。</span><span class="sxs-lookup"><span data-stu-id="a2912-195">Additional details include its full description, its severity, its current state, hello attacked resource, hello remediation steps for hello incident, and hello alerts that were included in this incident.</span></span>

<span data-ttu-id="a2912-196">您可以篩選 toosee**事件只**，**警示只**，或**兩者**。</span><span class="sxs-lookup"><span data-stu-id="a2912-196">You can filter toosee **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a><span data-ttu-id="a2912-197">如何存取 hello Threat Intelligence 報表？</span><span class="sxs-lookup"><span data-stu-id="a2912-197">How do I access hello Threat Intelligence Report?</span></span>

<span data-ttu-id="a2912-198">ASC 會分析來自多個來源 tooidentify 威脅的資訊。</span><span class="sxs-lookup"><span data-stu-id="a2912-198">ASC analyzes information from multiple sources tooidentify threats.</span></span> <span data-ttu-id="a2912-199">tooassist 事件回應小組調查並補救威脅，資訊安全中心包含威脅智慧報表，其中包含已偵測到的 hello 威脅的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a2912-199">tooassist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about hello threat that was detected.</span></span>

<span data-ttu-id="a2912-200">資訊安全中心有三種威脅報告，不同攻擊會提供不同的報告。</span><span class="sxs-lookup"><span data-stu-id="a2912-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="a2912-201">可用的 hello 報告為：</span><span class="sxs-lookup"><span data-stu-id="a2912-201">hello reports available are:</span></span>

- <span data-ttu-id="a2912-202">群組活動報告︰提供攻擊者、其目標和策略的深入探討。</span><span class="sxs-lookup"><span data-stu-id="a2912-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="a2912-203">活動報告︰著重說明特定攻擊活動的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a2912-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="a2912-204">威脅的摘要報告： 涵蓋 hello 先前的兩個報表中的所有項目。</span><span class="sxs-lookup"><span data-stu-id="a2912-204">Threat Summary Report: covers all items in hello previous two reports.</span></span>

<span data-ttu-id="a2912-205">這種類型的資訊是很有幫助 hello 事件回應程序期間，當 hello 攻擊的進行中調查 toounderstand hello 來源時，hello 攻擊者的動機和哪些 toodo toomitigate 這個問題接下來。</span><span class="sxs-lookup"><span data-stu-id="a2912-205">This type of information is very useful during hello incident response process, where there is an ongoing investigation toounderstand hello source of hello attack, hello attacker’s motivations, and what toodo toomitigate this issue moving forward.</span></span>

1. <span data-ttu-id="a2912-206">tooaccess hello 威脅情報回報，請執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="a2912-206">tooaccess hello threat intelligence report, do hello following:</span></span>

2. <span data-ttu-id="a2912-207">選取 hello**安全性警示**hello ASC 儀表板上的磚。</span><span class="sxs-lookup"><span data-stu-id="a2912-207">Select hello **Security alerts** tile on hello ASC dashboard.</span></span>

3. <span data-ttu-id="a2912-208">選取您想要的 tooobtain hello 安全性警示的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a2912-208">Select hello security alert for which you want tooobtain more information.</span></span>

4. <span data-ttu-id="a2912-209">在 hello**報表**欄位中，按一下 hello 連結 toohello threat intelligence 報表。</span><span class="sxs-lookup"><span data-stu-id="a2912-209">In hello **Reports** field, click hello link toohello threat intelligence report.</span></span>

5. <span data-ttu-id="a2912-210">這會開啟 hello PDF 檔案，您可以下載。</span><span class="sxs-lookup"><span data-stu-id="a2912-210">This will open hello PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="a2912-211">如需 hello ASC threat intelligence 報告的詳細資訊，請參閱[Azure 安全性中心 Threat Intelligence 報告。](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="a2912-211">For additional information about hello ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="a2912-212">評量</span><span class="sxs-lookup"><span data-stu-id="a2912-212">Assessment</span></span>

<span data-ttu-id="a2912-213">toohelp 與測試、 評估和評估安全性狀態，ASC 提供整合的弱點可能會評估與 Qualys 雲端代理程式，其虛擬機器的建議元件的一部分。</span><span class="sxs-lookup"><span data-stu-id="a2912-213">toohelp with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="a2912-214">hello Qualys 代理程式回報的弱點可能會資料 toohello Qualys 管理平台，然後將傳送的弱點可能會和狀況監控資料回 tooASC。</span><span class="sxs-lookup"><span data-stu-id="a2912-214">hello Qualys agent reports vulnerability data toohello Qualys management platform, which then sends vulnerability and health monitoring data back tooASC.</span></span> <span data-ttu-id="a2912-215">hello 的弱點可能會評估解決方案會顯示在 hello 建議 tooadd**建議**hello ASC 儀表板上的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a2912-215">hello recommendation tooadd a vulnerability assessment solution is displayed in hello **Recommendations** blade on hello ASC dashboard.</span></span>

<span data-ttu-id="a2912-216">Hello 目標 VM 上安裝 hello 的弱點可能會評估解決方案後，資訊安全中心掃描 hello VM toodetect 和識別系統和應用程式的安全性弱點。</span><span class="sxs-lookup"><span data-stu-id="a2912-216">After hello vulnerability assessment solution is installed on hello target VM, Security Center scans hello VM toodetect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="a2912-217">偵測到問題會顯示在下面的 hello**虛擬機器建議**選項。</span><span class="sxs-lookup"><span data-stu-id="a2912-217">Detected issues are shown under hello **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="a2912-218">如何實作弱點評量解決方案？</span><span class="sxs-lookup"><span data-stu-id="a2912-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="a2912-219">如果虛擬機器尚未部署整合式弱點評量解決方案，資訊安全中心會建議予以安裝。</span><span class="sxs-lookup"><span data-stu-id="a2912-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="a2912-220">Hello ASC 儀表板 上 hello**建議**刀鋒視窗中，選取**新增的弱點可能會評估解決方案。**</span><span class="sxs-lookup"><span data-stu-id="a2912-220">In hello ASC dashboard, on hello **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="a2912-221">選取您想要 tooinstall hello 的弱點可能會評估解決方案的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="a2912-221">Select hello VMs where you want tooinstall hello vulnerability assessment solution.</span></span>

3. <span data-ttu-id="a2912-222">按一下 [Install on [number of] VMs] \(安裝在 [數目] 部 VM 上)。</span><span class="sxs-lookup"><span data-stu-id="a2912-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="a2912-223">Hello Azure Marketplace 中或之下，選取夥伴方案**使用現有的方案，**選取**Qualys。**</span><span class="sxs-lookup"><span data-stu-id="a2912-223">Select a partner solution in hello Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="a2912-224">您可以開啟 hello 的自動更新設定開啟或關閉在 hello**協力廠商解決方案**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a2912-224">You can turn hello auto update settings on or off in hello **Partner Solutions** blade.</span></span>

<span data-ttu-id="a2912-225">如需有關的進一步指示 tooimplement 的弱點可能會評估解決方案，請參閱[Azure 資訊安全中心中的弱點可能會評估。](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span><span class="sxs-lookup"><span data-stu-id="a2912-225">For further instructions on how tooimplement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2912-226">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a2912-226">Next steps</span></span>

- [<span data-ttu-id="a2912-227">Azure 資訊安全中心快速入門指南</span><span class="sxs-lookup"><span data-stu-id="a2912-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="a2912-228">簡介 tooAzure 資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="a2912-228">Introduction tooAzure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="a2912-229">整合 Azure 資訊安全中心警示與 Azure 記錄整合</span><span class="sxs-lookup"><span data-stu-id="a2912-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- <span data-ttu-id="a2912-230">[Boost Azure Security Center with Integrated Vulnerability Assessment](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/) (利用整合式弱點評量增強 Azure 資訊安全中心)</span><span class="sxs-lookup"><span data-stu-id="a2912-230">[Boost Azure Security Center with Integrated Vulnerability Assessment](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)</span></span>
