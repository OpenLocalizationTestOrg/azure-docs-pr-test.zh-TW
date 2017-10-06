---
title: "Active Directory 條件式存取 aaaAzure |Microsoft 文件"
description: "使用條件式存取控制在 Azure Active Directory toocheck 特定條件的存取 tooapplications 驗證時。"
services: active-directory
keywords: "條件式存取 tooapps，Azure AD 中，使用條件式存取保護存取 toocompany 資源，條件式存取原則"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 9fa8a5c3e514c032fbe3aa56f33d759485a018c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-azure-active-directory"></a><span data-ttu-id="fedc6-104">Azure Active Directory 中的條件式存取</span><span class="sxs-lookup"><span data-stu-id="fedc6-104">Conditional access in Azure Active Directory</span></span>

<span data-ttu-id="fedc6-105">在行動裝置-首先，雲端優先世界中，Azure Active Directory 可讓單一登入 toodevices、 應用程式和服務從任何地方。</span><span class="sxs-lookup"><span data-stu-id="fedc6-105">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="fedc6-106">關閉公司網路中，可以使用的裝置 （包括 BYOD） 的 hello 激增，和第 3 個合作對象 SaaS 應用程式，IT 專業人員正面臨著逼近對方的兩個目標：</span><span class="sxs-lookup"><span data-stu-id="fedc6-106">With hello proliferation of devices (including BYOD), work off corporate networks, and 3rd party SaaS apps, IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="fedc6-107">無論在何處，每當加持 hello 使用者 toobe 生產力</span><span class="sxs-lookup"><span data-stu-id="fedc6-107">Empower hello end users toobe productive wherever and whenever</span></span>
- <span data-ttu-id="fedc6-108">在任何階段保護 hello 公司資產</span><span class="sxs-lookup"><span data-stu-id="fedc6-108">Protect hello corporate assets at any time</span></span>

<span data-ttu-id="fedc6-109">tooimprove 產能，Azure Active Directory 提供您廣泛的選項 tooaccess 的使用者，您公司的資產。</span><span class="sxs-lookup"><span data-stu-id="fedc6-109">tooimprove productivity, Azure Active Directory provides your users with a broad range of options tooaccess your corporate assets.</span></span> <span data-ttu-id="fedc6-110">應用程式存取管理，與 Azure Active Directory 可讓您只 tooensure *hello 適當人員*可以存取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fedc6-110">With application access management, Azure Active Directory enables you tooensure that only *hello right people* can access your applications.</span></span> <span data-ttu-id="fedc6-111">如果您想 toohave 更充分掌控 hello 適當人員如何存取您在某些情況下的資源嗎？</span><span class="sxs-lookup"><span data-stu-id="fedc6-111">What if you want toohave more control over how hello right people are accessing your resources under certain conditions?</span></span> <span data-ttu-id="fedc6-112">如果您即使有的條件下您想要 tooblock 存取 toocertain 應用程式甚至 hello*人以滑鼠右鍵*嗎？</span><span class="sxs-lookup"><span data-stu-id="fedc6-112">What if you even have conditions under which you want tooblock access toocertain apps even for hello *right people*?</span></span> <span data-ttu-id="fedc6-113">比方說，如果可能很確定為您 hello 適當人員要從受信任的網路; 存取特定應用程式不過，您可能不希望他們 tooaccess 這些應用程式從您不信任的網路。</span><span class="sxs-lookup"><span data-stu-id="fedc6-113">For example, it might be OK for you if hello right people are accessing certain apps from a trusted network; however, you might not want them tooaccess these apps from a network you don't trust.</span></span> <span data-ttu-id="fedc6-114">您可以使用條件式存取解決這些問題。</span><span class="sxs-lookup"><span data-stu-id="fedc6-114">You can address these questions using conditional access.</span></span>

<span data-ttu-id="fedc6-115">條件式存取是 Azure Active directory，可讓您根據特定條件在環境中的 hello 存取 tooapps tooenforce 控制項的功能。</span><span class="sxs-lookup"><span data-stu-id="fedc6-115">Conditional access is a capability of Azure Active Directory that enables you tooenforce controls on hello access tooapps in your environment based on specific conditions.</span></span> <span data-ttu-id="fedc6-116">使用的控制項，可以是連接的其他需求 toohello 存取，或您可以封鎖它。</span><span class="sxs-lookup"><span data-stu-id="fedc6-116">With controls, you can either tie additional requirements toohello access or you can block it.</span></span> <span data-ttu-id="fedc6-117">條件式存取的 hello 實作是以原則為基礎。</span><span class="sxs-lookup"><span data-stu-id="fedc6-117">hello implementation of conditional access is based on policies.</span></span> <span data-ttu-id="fedc6-118">以原則為基礎的方法可簡化設定經驗，因為它會依照您的想法存取需求的 hello 方式。</span><span class="sxs-lookup"><span data-stu-id="fedc6-118">A policy-based approach simplifies your configuration experience because it follows hello way you think about your access requirements.</span></span>  

<span data-ttu-id="fedc6-119">一般而言，您會定義您使用 hello 遵循模式為基礎的陳述式的存取需求：</span><span class="sxs-lookup"><span data-stu-id="fedc6-119">Typically, you define your access requirements using statements that are based on hello following pattern:</span></span>

![控制](./media/active-directory-conditional-access-azure-portal/10.png)

<span data-ttu-id="fedc6-121">當您取代 hello 兩個 「*這*」 以真實世界的詳細資訊，您有可能已經很熟悉 tooyou 的原則陳述式的範例：</span><span class="sxs-lookup"><span data-stu-id="fedc6-121">When you replace hello two occurrences of “*this*” with real-world information, you have an example for a policy statement that probably looks familiar tooyou:</span></span>

<span data-ttu-id="fedc6-122">*當約聘人員嘗試 tooaccess 我們的雲端應用程式，從位於不受信任的網路時，然後封鎖存取。*</span><span class="sxs-lookup"><span data-stu-id="fedc6-122">*When contractors are trying tooaccess our cloud apps from networks that are not trusted, then block access.*</span></span>

<span data-ttu-id="fedc6-123">上面的 hello 原則陳述式會反白顯示 hello 電源條件式存取。</span><span class="sxs-lookup"><span data-stu-id="fedc6-123">hello policy statement above highlights hello power of conditional access.</span></span> <span data-ttu-id="fedc6-124">雖然您可以啟用約聘人員 toobasically 存取雲端應用程式 (**人員**)，使用條件式存取，您也可以定義在哪一個 hello 存取就可以使用條件 (**如何**)。</span><span class="sxs-lookup"><span data-stu-id="fedc6-124">While you can enable contractors toobasically access your cloud apps (**who**), with conditional access, you can also define conditions under which hello access is possible (**how**).</span></span>

<span data-ttu-id="fedc6-125">Azure Active Directory 條件式存取，hello 內容中</span><span class="sxs-lookup"><span data-stu-id="fedc6-125">In hello context of Azure Active Directory conditional access,</span></span>

- <span data-ttu-id="fedc6-126">"**When this happens**" 稱為**條件陳述式**</span><span class="sxs-lookup"><span data-stu-id="fedc6-126">"**When this happens**" is called **condition statement**</span></span>
- <span data-ttu-id="fedc6-127">"**Then do this**" 成為**控制項**</span><span class="sxs-lookup"><span data-stu-id="fedc6-127">"**Then do this**" is called **controls**</span></span>

![控制](./media/active-directory-conditional-access-azure-portal/11.png)

<span data-ttu-id="fedc6-129">條件陳述式與您的控制項的 hello 組合代表條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="fedc6-129">hello combination of a condition statement with your controls represents a conditional access policy.</span></span>

![控制](./media/active-directory-conditional-access-azure-portal/12.png)


## <a name="controls"></a><span data-ttu-id="fedc6-131">控制</span><span class="sxs-lookup"><span data-stu-id="fedc6-131">Controls</span></span>

<span data-ttu-id="fedc6-132">在條件式存取原則中，控制項定義滿足條件陳述式時所應發生的狀況。</span><span class="sxs-lookup"><span data-stu-id="fedc6-132">In a conditional access policy, controls define what it is that should happen when a condition statement has been satisfied.</span></span>  
<span data-ttu-id="fedc6-133">利用控制項，您可以封鎖存取，或允許有額外需求的存取。</span><span class="sxs-lookup"><span data-stu-id="fedc6-133">With controls, you can either block access or allow access with additional requirements.</span></span>
<span data-ttu-id="fedc6-134">當您設定的原則允許存取時，您需要 tooselect 至少一項需求。</span><span class="sxs-lookup"><span data-stu-id="fedc6-134">When you configure a policy that allows access, you need tooselect at least one requirement.</span></span>   

### <a name="grant-controls"></a><span data-ttu-id="fedc6-135">授與控制</span><span class="sxs-lookup"><span data-stu-id="fedc6-135">Grant controls</span></span>
<span data-ttu-id="fedc6-136">hello 目前的 Azure Active Directory 的實作可讓您 tooconfigure hello 遵循授與控制需求：</span><span class="sxs-lookup"><span data-stu-id="fedc6-136">hello current implementation of Azure Active Directory enables you tooconfigure hello following grant control requirements:</span></span>

![控制](./media/active-directory-conditional-access-azure-portal/05.png)

- <span data-ttu-id="fedc6-138">**Multi-Factor Authentication** - 您可以透過 Multi-Factor Authentication 來要求增強式驗證。</span><span class="sxs-lookup"><span data-stu-id="fedc6-138">**Multi-factor Authentication** - You can require strong authentication through multi-factor authentication.</span></span> <span data-ttu-id="fedc6-139">身為提供者，您可以使用 Azure Multi-Factor Authentication，或使用結合 Active Directory Federation Services (AD FS) 的內部部署多重要素驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="fedc6-139">As provider, you can use Azure Multi-Factor or an on-premises multi-factor authentication provider, combined with Active Directory Federation Services (AD FS).</span></span> <span data-ttu-id="fedc6-140">使用多因素驗證，可協助防止未經授權的使用者，可能會獲得了存取 toohello 認證是有效的使用者所存取資源。</span><span class="sxs-lookup"><span data-stu-id="fedc6-140">Using multi-factor authentication helps protect resources from being accessed by an unauthorized user who might have gained access toohello credentials of a valid user.</span></span>

- <span data-ttu-id="fedc6-141">**相容的裝置**-您可以在 hello 裝置層級設定條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="fedc6-141">**Compliant device** - You can set conditional access policies at hello device level.</span></span> <span data-ttu-id="fedc6-142">您可以設定相容，原則 tooonly 啟用電腦或行動裝置的行動裝置管理 tooaccess 中註冊您的組織資源。</span><span class="sxs-lookup"><span data-stu-id="fedc6-142">You might set up a policy tooonly enable computers that are compliant, or mobile devices that are enrolled in a mobile device management tooaccess your organization's resources.</span></span> <span data-ttu-id="fedc6-143">比方說，您可以使用 Intune toocheck 裝置相容性，並再回報 tooAzure 強制 AD hello 使用者嘗試 tooaccess 應用程式時。</span><span class="sxs-lookup"><span data-stu-id="fedc6-143">For example, you can use Intune toocheck device compliance, and then report it tooAzure AD for enforcement when hello user attempts tooaccess an application.</span></span> <span data-ttu-id="fedc6-144">如需如何 toouse Intune tooprotect 應用程式和資料，請參閱詳細指引[使用 Microsoft Intune 保護應用程式和資料](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune)。</span><span class="sxs-lookup"><span data-stu-id="fedc6-144">For detailed guidance about how toouse Intune tooprotect apps and data, see [Protect apps and data with Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune).</span></span> <span data-ttu-id="fedc6-145">您也可以使用 Intune tooenforce 資料保護遺失或遭竊的裝置。</span><span class="sxs-lookup"><span data-stu-id="fedc6-145">You also can use Intune tooenforce data protection for lost or stolen devices.</span></span> <span data-ttu-id="fedc6-146">如需詳細資訊，請參閱 [使用 Microsoft Intune 搭配完整或選擇性抹除協助保護您的資料](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)。</span><span class="sxs-lookup"><span data-stu-id="fedc6-146">For more information, see [Help protect your data with full or selective wipe using Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).</span></span>

- <span data-ttu-id="fedc6-147">**已加入網域裝置**– 您可以要求您已經使用 tooconnect tooAzure Active Directory toobe 已加入網域的 tooyour hello 裝置內部部署 Active Directory (AD)。</span><span class="sxs-lookup"><span data-stu-id="fedc6-147">**Domain joined device** – You can require hello device you have used tooconnect tooAzure Active Directory toobe domain-joined tooyour on-premises Active Directory (AD).</span></span> <span data-ttu-id="fedc6-148">此原則適用於 tooWindows 桌上型電腦、 膝上型電腦和企業平板電腦。</span><span class="sxs-lookup"><span data-stu-id="fedc6-148">This policy applies tooWindows desktops, laptops, and enterprise tablets.</span></span> 

<span data-ttu-id="fedc6-149">如果您選取多個控制項，也可以設定在處理您的原則時是否全都為必要。</span><span class="sxs-lookup"><span data-stu-id="fedc6-149">If you have multiple controls selected, you can also configure whether all of them are required when your policy is processed.</span></span>

![控制](./media/active-directory-conditional-access-azure-portal/06.png)

### <a name="session-controls"></a><span data-ttu-id="fedc6-151">工作階段控制項</span><span class="sxs-lookup"><span data-stu-id="fedc6-151">Session controls</span></span>
<span data-ttu-id="fedc6-152">工作階段控制項可讓您限制雲端應用程式內的體驗。</span><span class="sxs-lookup"><span data-stu-id="fedc6-152">Session controls enable limiting experience within a cloud app.</span></span> <span data-ttu-id="fedc6-153">hello 工作階段控制項強制執行的雲端應用程式，而且依賴 hello 工作階段的相關的 Azure AD toohello 應用程式所提供的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="fedc6-153">hello session controls are enforced by cloud apps and rely on additional information provided by Azure AD toohello app about hello session.</span></span>

![控制](./media/active-directory-conditional-access-azure-portal/session-control-pic.png)

#### <a name="use-app-enforced-restrictions"></a><span data-ttu-id="fedc6-155">使用應用程式強制執行限制</span><span class="sxs-lookup"><span data-stu-id="fedc6-155">Use app enforced restrictions</span></span>
<span data-ttu-id="fedc6-156">您可以使用此控制 toorequire Azure AD toopass hello 裝置資訊 toohello 雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="fedc6-156">You can use this control toorequire Azure AD toopass hello device information toohello cloud app.</span></span> <span data-ttu-id="fedc6-157">這有助於 hello 知道如果 hello 使用者來自相容的裝置或已加入網域裝置的雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="fedc6-157">This helps hello cloud app know if hello user is coming from a compliant device or domain joined device.</span></span> <span data-ttu-id="fedc6-158">此控制項是目前僅支援 SharePoint 當做 hello 雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="fedc6-158">This control is currently only supported with SharePoint as hello cloud app.</span></span> <span data-ttu-id="fedc6-159">SharePoint 會使用 hello 裝置資訊 tooprovide 使用者有限或完整的經驗視 hello 裝置狀態而定。</span><span class="sxs-lookup"><span data-stu-id="fedc6-159">SharePoint uses hello device information tooprovide users a limited or full experience depending on hello device state.</span></span>
<span data-ttu-id="fedc6-160">深入了解如何 toorequire 限制存取 SharePoint toolearn 移[這裡](https://aka.ms/spolimitedaccessdocs)。</span><span class="sxs-lookup"><span data-stu-id="fedc6-160">toolearn more about how toorequire limited access with SharePoint, go [here](https://aka.ms/spolimitedaccessdocs).</span></span>

## <a name="condition-statement"></a><span data-ttu-id="fedc6-161">條件陳述式</span><span class="sxs-lookup"><span data-stu-id="fedc6-161">Condition Statement</span></span>

<span data-ttu-id="fedc6-162">hello 上一節介紹了 toosupported 選項 tooblock 或限制存取 tooyour 資源中表單的控制項。</span><span class="sxs-lookup"><span data-stu-id="fedc6-162">hello previous section has introduced you toosupported options tooblock or restrict access tooyour resources in form of controls.</span></span> <span data-ttu-id="fedc6-163">在條件式存取原則中，您可以定義 hello 準則，針對您在條件陳述式的格式中套用的控制項 toobe toobe 符合。</span><span class="sxs-lookup"><span data-stu-id="fedc6-163">In a conditional access policy, you define hello criteria that need toobe met for your controls toobe applied in form of a condition statement.</span></span>  

<span data-ttu-id="fedc6-164">您可以包含下列工作分派到您的條件陳述式的 hello:</span><span class="sxs-lookup"><span data-stu-id="fedc6-164">You can include hello following assignments into your condition statement:</span></span>

![控制](./media/active-directory-conditional-access-azure-portal/07.png)


- <span data-ttu-id="fedc6-166">**誰**-要在許多情況下，您的控制項 toobe 套用 tooa 特定一組使用者。</span><span class="sxs-lookup"><span data-stu-id="fedc6-166">**Who** - In many cases, you want your controls toobe applied tooa specific set of users.</span></span> <span data-ttu-id="fedc6-167">條件陳述式中您可以選取 hello 使用者和群組原則套用至定義這個集合。</span><span class="sxs-lookup"><span data-stu-id="fedc6-167">In a condition statement, you can define this set by selecting hello users and groups your policy applies to.</span></span> <span data-ttu-id="fedc6-168">如有必要，您也可以明確豁免一組使用者，進行從您的原則中排除這些使用者。</span><span class="sxs-lookup"><span data-stu-id="fedc6-168">If necessary, you can also explicitly exclude a set of users from your policy by exempting them.</span></span>  
<span data-ttu-id="fedc6-169">選取使用者和群組，您可以定義您的原則套用至使用者 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="fedc6-169">By selecting users and groups, you define hello scope of users your policy applies to.</span></span>    

    ![控制](./media/active-directory-conditional-access-azure-portal/08.png)



- <span data-ttu-id="fedc6-171">**什麼** - 從保護的觀點而言，有些在您的環境中執行的應用程式通常需要更多關注 (相較於其他應用程式)。</span><span class="sxs-lookup"><span data-stu-id="fedc6-171">**What** - Typically, there are certain apps that are running in your environment requiring, from a protection perspective, more attention than others.</span></span> <span data-ttu-id="fedc6-172">這會影響，例如，具有存取 toosensitive 資料應用程式。</span><span class="sxs-lookup"><span data-stu-id="fedc6-172">This affects, for example, apps that have access toosensitive data.</span></span>
<span data-ttu-id="fedc6-173">藉由選取的雲端應用程式，您可以定義您的原則套用至雲端應用程式 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="fedc6-173">By selecting cloud apps, you define hello scope of cloud apps your policy applies to.</span></span> <span data-ttu-id="fedc6-174">如有必要，您也可以從您的原則中明確排除一組應用程式。</span><span class="sxs-lookup"><span data-stu-id="fedc6-174">If necessary, you can also explicitly exclude a set of apps from your policy.</span></span>

    ![控制](./media/active-directory-conditional-access-azure-portal/09.png)


- <span data-ttu-id="fedc6-176">**如何**-只要存取 tooyour 應用程式會在您可以控制，不需要諸額外的控制項上如何雲端應用程式存取您的使用者有可能的情況下執行。</span><span class="sxs-lookup"><span data-stu-id="fedc6-176">**How** - As long as access tooyour apps is performed under conditions you can control, there might be no need for imposing additional controls on how your cloud apps are accessed by your users.</span></span> <span data-ttu-id="fedc6-177">不過，畫面可能看起來不同，如果存取 tooyour 雲端應用程式執行時，比方說，不受信任的網路或不相容的裝置。</span><span class="sxs-lookup"><span data-stu-id="fedc6-177">However, things might look different if access tooyour cloud apps is performed, for example, from networks that are not trusted or devices that are not compliant.</span></span> <span data-ttu-id="fedc6-178">在條件陳述式中，您可以定義特定存取條件會有存取 tooyour 應用程式的執行方式的其他需求。</span><span class="sxs-lookup"><span data-stu-id="fedc6-178">In a condition statement, you can define certain access conditions that have additional requirements for how access tooyour apps is performed.</span></span>

    ![條件](./media/active-directory-conditional-access-azure-portal/21.png)


## <a name="conditions"></a><span data-ttu-id="fedc6-180">條件</span><span class="sxs-lookup"><span data-stu-id="fedc6-180">Conditions</span></span>

<span data-ttu-id="fedc6-181">在 hello 目前實作中的 Azure Active Directory，您可以定義下列區域的 hello 的條件：</span><span class="sxs-lookup"><span data-stu-id="fedc6-181">In hello current implementation of Azure Active Directory, you can define conditions for hello following areas:</span></span>

- <span data-ttu-id="fedc6-182">登入風險</span><span class="sxs-lookup"><span data-stu-id="fedc6-182">Sign-in risk</span></span>
- <span data-ttu-id="fedc6-183">裝置平台</span><span class="sxs-lookup"><span data-stu-id="fedc6-183">Device platforms</span></span>
- <span data-ttu-id="fedc6-184">位置</span><span class="sxs-lookup"><span data-stu-id="fedc6-184">Locations</span></span>
- <span data-ttu-id="fedc6-185">用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="fedc6-185">Client apps</span></span>

![條件](./media/active-directory-conditional-access-azure-portal/21.png)

### <a name="sign-in-risk"></a><span data-ttu-id="fedc6-187">登入風險</span><span class="sxs-lookup"><span data-stu-id="fedc6-187">Sign-in risk</span></span>

<span data-ttu-id="fedc6-188">登入的風險是物件，可由 Azure Active Directory tootrack hello 可能性 hello 合法的使用者帳戶擁有者未執行的登入嘗試。</span><span class="sxs-lookup"><span data-stu-id="fedc6-188">A sign-in risk is an object that is used by Azure Active Directory tootrack hello likelihood that a sign-in attempt was not performed by hello legitimate owner of a user account.</span></span> <span data-ttu-id="fedc6-189">此物件，在 hello 可能性 （高、 中或低） 會儲存在表單的屬性稱為[登入風險層級](active-directory-reporting-risk-events.md#risk-level)。</span><span class="sxs-lookup"><span data-stu-id="fedc6-189">In this object, hello likelihood (High, Medium, or Low) is stored in form of an attribute called [sign-in risk level](active-directory-reporting-risk-events.md#risk-level).</span></span> <span data-ttu-id="fedc6-190">如果 Azure Active Directory 偵測到登入風險，則會在使用者登入期間產生此物件。</span><span class="sxs-lookup"><span data-stu-id="fedc6-190">This object is generated during a sign-in of a user if sign-in risks have been detected by Azure Active Directory.</span></span> <span data-ttu-id="fedc6-191">如需詳細資訊，請參閱[有風險的登入](active-directory-identityprotection.md#risky-sign-ins)。</span><span class="sxs-lookup"><span data-stu-id="fedc6-191">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span>  
<span data-ttu-id="fedc6-192">您可以使用計算的 hello 登入風險層級做為條件式存取原則中的條件。</span><span class="sxs-lookup"><span data-stu-id="fedc6-192">You can use hello calculated sign-in risk level as condition in a conditional access policy.</span></span> 

![條件](./media/active-directory-conditional-access-azure-portal/22.png)

### <a name="device-platforms"></a><span data-ttu-id="fedc6-194">裝置平台</span><span class="sxs-lookup"><span data-stu-id="fedc6-194">Device platforms</span></span>

<span data-ttu-id="fedc6-195">hello 您裝置執行作業系統的特點在於 hello 裝置平台：</span><span class="sxs-lookup"><span data-stu-id="fedc6-195">hello device platform is characterized by hello operating system that is running on your device:</span></span>

- <span data-ttu-id="fedc6-196">Android</span><span class="sxs-lookup"><span data-stu-id="fedc6-196">Android</span></span>
- <span data-ttu-id="fedc6-197">iOS</span><span class="sxs-lookup"><span data-stu-id="fedc6-197">iOS</span></span>
- <span data-ttu-id="fedc6-198">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fedc6-198">Windows Phone</span></span>
- <span data-ttu-id="fedc6-199">Windows</span><span class="sxs-lookup"><span data-stu-id="fedc6-199">Windows</span></span>
- <span data-ttu-id="fedc6-200">macOS (預覽)。</span><span class="sxs-lookup"><span data-stu-id="fedc6-200">macOS (preview).</span></span> 

![條件](./media/active-directory-conditional-access-azure-portal/02.png)

<span data-ttu-id="fedc6-202">您可以定義包含會豁免原則的裝置平台以及 hello 裝置平台。</span><span class="sxs-lookup"><span data-stu-id="fedc6-202">You can define hello device platforms that are included as well as device platforms that are exempted from a policy.</span></span>  
<span data-ttu-id="fedc6-203">toouse hello 原則中的裝置平台，第一個變更 hello 設定切換太**是**，然後選取所有或個別的裝置平台 hello 原則會套用至。</span><span class="sxs-lookup"><span data-stu-id="fedc6-203">toouse device platforms in hello policy, first change hello configure toggles too**Yes**, and then select all or individual device platforms hello policy applies to.</span></span> <span data-ttu-id="fedc6-204">如果您選取個別的裝置平台，hello 原則會在這些平台上有只影響。</span><span class="sxs-lookup"><span data-stu-id="fedc6-204">If you select individual device platforms, hello policy has only an impact on these platforms.</span></span> <span data-ttu-id="fedc6-205">在此情況下，登入 tooother 支援平台不會受到 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="fedc6-205">In this case, sign-ins tooother supported platforms are not impacted by hello policy.</span></span>


### <a name="locations"></a><span data-ttu-id="fedc6-206">位置</span><span class="sxs-lookup"><span data-stu-id="fedc6-206">Locations</span></span>

<span data-ttu-id="fedc6-207">hello 位置識別 hello hello 用戶端的 IP 位址，您已使用 tooconnect tooAzure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="fedc6-207">hello location is identified by hello IP address of hello client you have used tooconnect tooAzure Active Directory.</span></span> <span data-ttu-id="fedc6-208">這種情況需要您熟悉 toobe**名為位置**和**MFA 可信任 Ip**。</span><span class="sxs-lookup"><span data-stu-id="fedc6-208">This condition requires you toobe familiar with **named locations** and **MFA trusted IPs**.</span></span>  

<span data-ttu-id="fedc6-209">**名為位置**是 Azure Active Directory 可讓您的組織中的 toolabel 受信任的 IP 位址範圍的功能。</span><span class="sxs-lookup"><span data-stu-id="fedc6-209">**Named locations** is a feature of Azure Active Directory which allows you toolabel trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="fedc6-210">在您的環境，您可以使用具名的位置 hello 內容中的 hello 偵測[風險事件](active-directory-reporting-risk-events.md)以及條件式存取。</span><span class="sxs-lookup"><span data-stu-id="fedc6-210">In your environment, you can use named locations in hello context of hello detection of [risk events](active-directory-reporting-risk-events.md) as well as conditional access.</span></span> <span data-ttu-id="fedc6-211">如需有關在 Azure Active Directory 中設定具名位置的詳細資訊，請參閱 [Azure Active Directory 中的具名位置](active-directory-named-locations.md)。</span><span class="sxs-lookup"><span data-stu-id="fedc6-211">For more details about configuring named locations in Azure Active Directory, see [named locations in Azure Active Directory](active-directory-named-locations.md).</span></span>

<span data-ttu-id="fedc6-212">在 Azure AD 中位置可以設定的 hello 數目受到 hello hello 相關物件的大小。</span><span class="sxs-lookup"><span data-stu-id="fedc6-212">hello number of locations you can configure is constrained by hello size of hello related object in Azure AD.</span></span> <span data-ttu-id="fedc6-213">您可以設定：</span><span class="sxs-lookup"><span data-stu-id="fedc6-213">You can configure:</span></span>
 
 - <span data-ttu-id="fedc6-214">其中一個名為向上 too500 IP 範圍的位置</span><span class="sxs-lookup"><span data-stu-id="fedc6-214">One named location with up too500 IP ranges</span></span>
 - <span data-ttu-id="fedc6-215">使用其中一個 IP 範圍指派 tooeach 最多 60 具名位置 （預覽）</span><span class="sxs-lookup"><span data-stu-id="fedc6-215">A maximum of 60 named locations (preview) with one IP range assigned tooeach of them</span></span> 


<span data-ttu-id="fedc6-216">**MFA 可信任 Ip**是一項功能可讓您 toodefine 受信任的 IP 位址範圍代表您組織的近端內部網路的多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="fedc6-216">**MFA trusted IPs** is a feature of multi-factor authentication that enables you toodefine trusted IP address ranges representing your organization's local intranet.</span></span> <span data-ttu-id="fedc6-217">當您設定位置條件時，信任的 Ip 可讓您 toodistinguish 之間進行從您的組織網路和所有其他位置的連線。</span><span class="sxs-lookup"><span data-stu-id="fedc6-217">When you configure a location conditions, Trusted IPs enables you toodistinguish between connections made from your organization's network and all other locations.</span></span> <span data-ttu-id="fedc6-218">如需詳細資訊，請參閱[信任的 IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)。</span><span class="sxs-lookup"><span data-stu-id="fedc6-218">For more details, see [trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>  



<span data-ttu-id="fedc6-219">您可以包含所有位置或所有信任的 IP，也可以排除所有信任的 IP。</span><span class="sxs-lookup"><span data-stu-id="fedc6-219">You can either include all locations or all trusted IPs and you can exclude all trusted IPs.</span></span>

![條件](./media/active-directory-conditional-access-azure-portal/03.png)


### <a name="client-app"></a><span data-ttu-id="fedc6-221">用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="fedc6-221">Client app</span></span>

<span data-ttu-id="fedc6-222">hello 用戶端應用程式可以是泛型的層級 hello 的應用程式的網頁瀏覽器、 行動裝置應用程式 （桌面用戶端） 上使用 tooconnect tooAzure Active Directory 或您可以明確選取 Exchange Active Sync。</span><span class="sxs-lookup"><span data-stu-id="fedc6-222">hello client app can be either on a generic level hello app (web browser, mobile app, desktop client) you have used tooconnect tooAzure Active Directory or you can specifically select Exchange Active Sync.</span></span>  
<span data-ttu-id="fedc6-223">舊有的驗證是指 tooclients 使用基本驗證，例如不使用新式驗證的舊版 Office 用戶端。</span><span class="sxs-lookup"><span data-stu-id="fedc6-223">Legacy authentication refers tooclients using basic authentication such as older Office clients that don’t use modern authentication.</span></span> <span data-ttu-id="fedc6-224">舊式驗證目前不支援條件式存取。</span><span class="sxs-lookup"><span data-stu-id="fedc6-224">Conditional access is currently not supported with legacy authentication.</span></span>

![條件](./media/active-directory-conditional-access-azure-portal/04.png)


## <a name="common-scenarios"></a><span data-ttu-id="fedc6-226">常見案例</span><span class="sxs-lookup"><span data-stu-id="fedc6-226">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="fedc6-227">應用程式需要 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="fedc6-227">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="fedc6-228">許多環境中有其他人需要比 hello 較高的保護層級的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fedc6-228">Many environments have apps requiring a higher level of protection than hello others.</span></span>
<span data-ttu-id="fedc6-229">這種，例如 hello 擁有存取 toosensitive 資料的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fedc6-229">This is, for example, hello case for apps that have access toosensitive data.</span></span>
<span data-ttu-id="fedc6-230">如果您想 tooadd 另一層保護 toothese 應用程式，您可以設定條件式存取原則，當使用者同時存取這些應用程式要求多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="fedc6-230">If you want tooadd another layer of protection toothese apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="fedc6-231">從不受信任的網路存取時需要 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="fedc6-231">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="fedc6-232">此案例中是類似 toohello 前一個案例，因為它會增加多因素驗證的需求。</span><span class="sxs-lookup"><span data-stu-id="fedc6-232">This scenario is similar toohello previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="fedc6-233">不過，hello 主要差異是這項需求的 hello 條件。</span><span class="sxs-lookup"><span data-stu-id="fedc6-233">However, hello main difference is hello condition for this requirement.</span></span>  
<span data-ttu-id="fedc6-234">當應用程式存取 toosensitve 資料與已 hello 焦點的 hello 前一個案例時，這種情況的 hello 焦點是受信任的位置。</span><span class="sxs-lookup"><span data-stu-id="fedc6-234">While hello focus of hello previous scenario was on apps with access toosensitve data, hello focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="fedc6-235">換句話說，如果使用者從您不信任的網路存取應用程式，您可能需要 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="fedc6-235">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="fedc6-236">只有受信任的裝置可以存取 Office 365 服務</span><span class="sxs-lookup"><span data-stu-id="fedc6-236">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="fedc6-237">如果您使用 Intune 在您的環境中，您可以立即開始使用 hello Azure 主控台中的 hello 條件式存取原則介面。</span><span class="sxs-lookup"><span data-stu-id="fedc6-237">If you are using Intune in your environment, you can immediately start using hello conditional access policy interface in hello Azure console.</span></span>

<span data-ttu-id="fedc6-238">許多 Intune 客戶使用條件式存取 tooensure 只有受信任的裝置才可以存取 Office 365 服務。</span><span class="sxs-lookup"><span data-stu-id="fedc6-238">Many Intune customers are using conditional access tooensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="fedc6-239">這表示，行動裝置向 Intune 註冊並符合相容性原則的需求，Windows 電腦會聯結的 tooan 在內部部署網域。</span><span class="sxs-lookup"><span data-stu-id="fedc6-239">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined tooan on-premises domain.</span></span> <span data-ttu-id="fedc6-240">重要的改進是，您不需要 tooset hello hello Office 365 服務的每個相同的原則。</span><span class="sxs-lookup"><span data-stu-id="fedc6-240">A key improvement is that you do not have tooset hello same policy for each of hello Office 365 services.</span></span>  <span data-ttu-id="fedc6-241">當您建立新的原則時，設定 hello 雲端應用程式 tooinclude 每個您想使用 tooprotect 使用條件式存取的 hello O365 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fedc6-241">When you create a new policy, configure hello Cloud apps tooinclude each of hello O365 apps that you wish tooprotect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fedc6-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fedc6-242">Next steps</span></span>

<span data-ttu-id="fedc6-243">如果您想如何 tooconfigure 條件式存取原則，請參閱的 tooknow[開始使用 Azure Active Directory 中的條件式存取](active-directory-conditional-access-azure-portal-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="fedc6-243">If you want tooknow how tooconfigure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>

<span data-ttu-id="fedc6-244">如果您針對您的環境準備好 tooconfigure 條件式存取原則，請參閱 hello [Azure Active Directory 中的條件式存取的最佳做法](active-directory-conditional-access-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="fedc6-244">If you are ready tooconfigure conditional access policies for your environment, see hello [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span> 
