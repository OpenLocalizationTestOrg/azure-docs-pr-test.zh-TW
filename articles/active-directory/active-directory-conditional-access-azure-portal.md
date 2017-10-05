---
title: "Azure Active Directory 條件式存取 | Microsoft Docs"
description: "使用條件式存取控制，Azure Active Directory 會在驗證應用程式的存取權時，檢查特定的條件。"
services: active-directory
keywords: "應用程式的條件式存取, Azure AD 條件式存取, 安全存取公司資源, 條件式存取原則"
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
ms.openlocfilehash: 20572ecbde79bc2722f3a25f297c92d8e722a3e8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="conditional-access-in-azure-active-directory"></a><span data-ttu-id="01853-104">Azure Active Directory 中的條件式存取</span><span class="sxs-lookup"><span data-stu-id="01853-104">Conditional access in Azure Active Directory</span></span>

<span data-ttu-id="01853-105">在行動第一、雲端第一的世界中，Azure Active Directory 可讓您從任何地方單一登入至裝置、應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="01853-105">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="01853-106">隨著裝置 (包括 BYOD)、在公司網路外部作業，以及協力廠商 SaaS 應用程式的激增，IT 專業人員面臨到兩個相對的目標︰</span><span class="sxs-lookup"><span data-stu-id="01853-106">With the proliferation of devices (including BYOD), work off corporate networks, and 3rd party SaaS apps, IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="01853-107">讓使用者隨時隨地都具有生產力</span><span class="sxs-lookup"><span data-stu-id="01853-107">Empower the end users to be productive wherever and whenever</span></span>
- <span data-ttu-id="01853-108">隨時保護公司資產</span><span class="sxs-lookup"><span data-stu-id="01853-108">Protect the corporate assets at any time</span></span>

<span data-ttu-id="01853-109">為了改善生產力，Azure Active Directory 為使用者提供廣泛的選項，以便存取您的公司資產。</span><span class="sxs-lookup"><span data-stu-id="01853-109">To improve productivity, Azure Active Directory provides your users with a broad range of options to access your corporate assets.</span></span> <span data-ttu-id="01853-110">透過應用程式存取管理，Azure Active Directory 可讓您確保只有「適當人員」可以存取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="01853-110">With application access management, Azure Active Directory enables you to ensure that only *the right people* can access your applications.</span></span> <span data-ttu-id="01853-111">如果您想要更充分掌控適當人員在某些情況下如何存取您的資源，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="01853-111">What if you want to have more control over how the right people are accessing your resources under certain conditions?</span></span> <span data-ttu-id="01853-112">如果您甚至有想要封鎖「適當人員」存取某些應用程式的條件，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="01853-112">What if you even have conditions under which you want to block access to certain apps even for the *right people*?</span></span> <span data-ttu-id="01853-113">例如，您同意適當的人員從信任的網路存取某些應用程式；不過，您可能不希望他們從您不信任的網路存取這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="01853-113">For example, it might be OK for you if the right people are accessing certain apps from a trusted network; however, you might not want them to access these apps from a network you don't trust.</span></span> <span data-ttu-id="01853-114">您可以使用條件式存取解決這些問題。</span><span class="sxs-lookup"><span data-stu-id="01853-114">You can address these questions using conditional access.</span></span>

<span data-ttu-id="01853-115">條件式存取是 Azure Active Directory 的功能，可讓您根據特定條件，強制控制您環境中的應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="01853-115">Conditional access is a capability of Azure Active Directory that enables you to enforce controls on the access to apps in your environment based on specific conditions.</span></span> <span data-ttu-id="01853-116">利用控制項，您可以將額外需求繫結到存取，也可以封鎖存取。</span><span class="sxs-lookup"><span data-stu-id="01853-116">With controls, you can either tie additional requirements to the access or you can block it.</span></span> <span data-ttu-id="01853-117">條件式存取的實作是以原則為基礎。</span><span class="sxs-lookup"><span data-stu-id="01853-117">The implementation of conditional access is based on policies.</span></span> <span data-ttu-id="01853-118">以原則為基礎的方法可簡化您的設定經驗，因為它會依循您對於存取需求的想法。</span><span class="sxs-lookup"><span data-stu-id="01853-118">A policy-based approach simplifies your configuration experience because it follows the way you think about your access requirements.</span></span>  

<span data-ttu-id="01853-119">您通常會使用以下列模式為基礎的陳述式，定義您的存取需求︰</span><span class="sxs-lookup"><span data-stu-id="01853-119">Typically, you define your access requirements using statements that are based on the following pattern:</span></span>

![控制](./media/active-directory-conditional-access-azure-portal/10.png)

<span data-ttu-id="01853-121">當您以真實世界的資訊取代出現兩次的 “this”，您會有可能看似熟悉的原則陳述式範例︰</span><span class="sxs-lookup"><span data-stu-id="01853-121">When you replace the two occurrences of “*this*” with real-world information, you have an example for a policy statement that probably looks familiar to you:</span></span>

<span data-ttu-id="01853-122">*When contractors are trying to access our cloud apps from networks that are not trusted, then block access.*</span><span class="sxs-lookup"><span data-stu-id="01853-122">*When contractors are trying to access our cloud apps from networks that are not trusted, then block access.*</span></span>

<span data-ttu-id="01853-123">上述的原則陳述式凸顯了條件式存取的功效。</span><span class="sxs-lookup"><span data-stu-id="01853-123">The policy statement above highlights the power of conditional access.</span></span> <span data-ttu-id="01853-124">您雖然可以讓約聘人員基本上存取您的雲端應用程式 (**誰**)，但利用條件式存取，您也可以定義在哪些條件下可能存取 (**如何**)。</span><span class="sxs-lookup"><span data-stu-id="01853-124">While you can enable contractors to basically access your cloud apps (**who**), with conditional access, you can also define conditions under which the access is possible (**how**).</span></span>

<span data-ttu-id="01853-125">在 Azure Active Directory 條件式存取的內容中：</span><span class="sxs-lookup"><span data-stu-id="01853-125">In the context of Azure Active Directory conditional access,</span></span>

- <span data-ttu-id="01853-126">"**When this happens**" 稱為**條件陳述式**</span><span class="sxs-lookup"><span data-stu-id="01853-126">"**When this happens**" is called **condition statement**</span></span>
- <span data-ttu-id="01853-127">"**Then do this**" 成為**控制項**</span><span class="sxs-lookup"><span data-stu-id="01853-127">"**Then do this**" is called **controls**</span></span>

![控制](./media/active-directory-conditional-access-azure-portal/11.png)

<span data-ttu-id="01853-129">條件陳述式與控制項的組合代表條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="01853-129">The combination of a condition statement with your controls represents a conditional access policy.</span></span>

![控制](./media/active-directory-conditional-access-azure-portal/12.png)


## <a name="controls"></a><span data-ttu-id="01853-131">控制</span><span class="sxs-lookup"><span data-stu-id="01853-131">Controls</span></span>

<span data-ttu-id="01853-132">在條件式存取原則中，控制項定義滿足條件陳述式時所應發生的狀況。</span><span class="sxs-lookup"><span data-stu-id="01853-132">In a conditional access policy, controls define what it is that should happen when a condition statement has been satisfied.</span></span>  
<span data-ttu-id="01853-133">利用控制項，您可以封鎖存取，或允許有額外需求的存取。</span><span class="sxs-lookup"><span data-stu-id="01853-133">With controls, you can either block access or allow access with additional requirements.</span></span>
<span data-ttu-id="01853-134">當您設定可允許存取的原則時，您必須選取至少一個需求。</span><span class="sxs-lookup"><span data-stu-id="01853-134">When you configure a policy that allows access, you need to select at least one requirement.</span></span>   

### <a name="grant-controls"></a><span data-ttu-id="01853-135">授與控制</span><span class="sxs-lookup"><span data-stu-id="01853-135">Grant controls</span></span>
<span data-ttu-id="01853-136">目前的 Azure Active Directory 實作可讓您設定下列授與控制權需求︰</span><span class="sxs-lookup"><span data-stu-id="01853-136">The current implementation of Azure Active Directory enables you to configure the following grant control requirements:</span></span>

![控制](./media/active-directory-conditional-access-azure-portal/05.png)

- <span data-ttu-id="01853-138">**Multi-Factor Authentication** - 您可以透過 Multi-Factor Authentication 來要求增強式驗證。</span><span class="sxs-lookup"><span data-stu-id="01853-138">**Multi-factor Authentication** - You can require strong authentication through multi-factor authentication.</span></span> <span data-ttu-id="01853-139">身為提供者，您可以使用 Azure Multi-Factor Authentication，或使用結合 Active Directory Federation Services (AD FS) 的內部部署多重要素驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="01853-139">As provider, you can use Azure Multi-Factor or an on-premises multi-factor authentication provider, combined with Active Directory Federation Services (AD FS).</span></span> <span data-ttu-id="01853-140">對於未獲授權但已取得有效使用者之認證存取權的使用者，使用 Multi-Factor Authentication 有助於防止其存取資源。</span><span class="sxs-lookup"><span data-stu-id="01853-140">Using multi-factor authentication helps protect resources from being accessed by an unauthorized user who might have gained access to the credentials of a valid user.</span></span>

- <span data-ttu-id="01853-141">**符合規範的裝置** - 您可以在裝置層級設定條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="01853-141">**Compliant device** - You can set conditional access policies at the device level.</span></span> <span data-ttu-id="01853-142">您可以設定一個原則：只能夠讓符合規範的電腦，或已在行動裝置管理中註冊的行動裝置存取貴組織的資源。</span><span class="sxs-lookup"><span data-stu-id="01853-142">You might set up a policy to only enable computers that are compliant, or mobile devices that are enrolled in a mobile device management to access your organization's resources.</span></span> <span data-ttu-id="01853-143">例如，您可以使用 Intune 來檢查裝置相容性，然後向 Azure AD 回報，以便在使用者嘗試存取應用程式強制執行。</span><span class="sxs-lookup"><span data-stu-id="01853-143">For example, you can use Intune to check device compliance, and then report it to Azure AD for enforcement when the user attempts to access an application.</span></span> <span data-ttu-id="01853-144">如需如何使用 Intune 來保護應用程式和資料的詳細指引，請參閱[使用 Microsoft Intune 保護應用程式和資料](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune)。</span><span class="sxs-lookup"><span data-stu-id="01853-144">For detailed guidance about how to use Intune to protect apps and data, see [Protect apps and data with Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune).</span></span> <span data-ttu-id="01853-145">您也可以使用 Intune 來強制進行遺失或遭竊裝置的資料保護。</span><span class="sxs-lookup"><span data-stu-id="01853-145">You also can use Intune to enforce data protection for lost or stolen devices.</span></span> <span data-ttu-id="01853-146">如需詳細資訊，請參閱 [使用 Microsoft Intune 搭配完整或選擇性抹除協助保護您的資料](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)。</span><span class="sxs-lookup"><span data-stu-id="01853-146">For more information, see [Help protect your data with full or selective wipe using Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).</span></span>

- <span data-ttu-id="01853-147">**已加入網域的裝置** – 您可以要求您用來連線到 Azure Active Directory 的裝置加入內部部署 Active Directory (AD) 網域。</span><span class="sxs-lookup"><span data-stu-id="01853-147">**Domain joined device** – You can require the device you have used to connect to Azure Active Directory to be domain-joined to your on-premises Active Directory (AD).</span></span> <span data-ttu-id="01853-148">此原則適用於 Windows 桌上型電腦、膝上型電腦和企業平板電腦。</span><span class="sxs-lookup"><span data-stu-id="01853-148">This policy applies to Windows desktops, laptops, and enterprise tablets.</span></span> 

<span data-ttu-id="01853-149">如果您選取多個控制項，也可以設定在處理您的原則時是否全都為必要。</span><span class="sxs-lookup"><span data-stu-id="01853-149">If you have multiple controls selected, you can also configure whether all of them are required when your policy is processed.</span></span>

![控制](./media/active-directory-conditional-access-azure-portal/06.png)

### <a name="session-controls"></a><span data-ttu-id="01853-151">工作階段控制項</span><span class="sxs-lookup"><span data-stu-id="01853-151">Session controls</span></span>
<span data-ttu-id="01853-152">工作階段控制項可讓您限制雲端應用程式內的體驗。</span><span class="sxs-lookup"><span data-stu-id="01853-152">Session controls enable limiting experience within a cloud app.</span></span> <span data-ttu-id="01853-153">工作階段控制項是由雲端應用程式強制執行，並依賴 Azure AD 對應用程式提供有關工作階段的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="01853-153">The session controls are enforced by cloud apps and rely on additional information provided by Azure AD to the app about the session.</span></span>

![控制](./media/active-directory-conditional-access-azure-portal/session-control-pic.png)

#### <a name="use-app-enforced-restrictions"></a><span data-ttu-id="01853-155">使用應用程式強制執行限制</span><span class="sxs-lookup"><span data-stu-id="01853-155">Use app enforced restrictions</span></span>
<span data-ttu-id="01853-156">您可以使用這個控制項，要求 Azure AD 將裝置資訊傳遞至雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="01853-156">You can use this control to require Azure AD to pass the device information to the cloud app.</span></span> <span data-ttu-id="01853-157">這有助於雲端應用程式了解使用者是否來自符合規範的裝置或加入網域的裝置。</span><span class="sxs-lookup"><span data-stu-id="01853-157">This helps the cloud app know if the user is coming from a compliant device or domain joined device.</span></span> <span data-ttu-id="01853-158">此控制項目前僅支援使用 SharePoint 作為雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="01853-158">This control is currently only supported with SharePoint as the cloud app.</span></span> <span data-ttu-id="01853-159">視裝置狀態而定，SharePoint 會使用裝置資訊來提供使用者有限或完整的經驗。</span><span class="sxs-lookup"><span data-stu-id="01853-159">SharePoint uses the device information to provide users a limited or full experience depending on the device state.</span></span>
<span data-ttu-id="01853-160">若要深入了解如何要求 SharePoint 的有限存取，請移至[這裡](https://aka.ms/spolimitedaccessdocs)。</span><span class="sxs-lookup"><span data-stu-id="01853-160">To learn more about how to require limited access with SharePoint, go [here](https://aka.ms/spolimitedaccessdocs).</span></span>

## <a name="condition-statement"></a><span data-ttu-id="01853-161">條件陳述式</span><span class="sxs-lookup"><span data-stu-id="01853-161">Condition Statement</span></span>

<span data-ttu-id="01853-162">上一節介紹了以控制項形式封鎖或限制資源存取的支援選項。</span><span class="sxs-lookup"><span data-stu-id="01853-162">The previous section has introduced you to supported options to block or restrict access to your resources in form of controls.</span></span> <span data-ttu-id="01853-163">在條件式存取原則中，您可以定義必須符合才能以條件陳述式的形式套用您的控制項的準則。</span><span class="sxs-lookup"><span data-stu-id="01853-163">In a conditional access policy, you define the criteria that need to be met for your controls to be applied in form of a condition statement.</span></span>  

<span data-ttu-id="01853-164">您可以將下列指派包含在您的條件陳述式中︰</span><span class="sxs-lookup"><span data-stu-id="01853-164">You can include the following assignments into your condition statement:</span></span>

![控制](./media/active-directory-conditional-access-azure-portal/07.png)


- <span data-ttu-id="01853-166">**誰** - 在許多情況下，您想要讓控制項套用至一組特定的使用者。</span><span class="sxs-lookup"><span data-stu-id="01853-166">**Who** - In many cases, you want your controls to be applied to a specific set of users.</span></span> <span data-ttu-id="01853-167">在條件陳述式中，您可以選取原則套用至的使用者和群組，以定義這組使用者。</span><span class="sxs-lookup"><span data-stu-id="01853-167">In a condition statement, you can define this set by selecting the users and groups your policy applies to.</span></span> <span data-ttu-id="01853-168">如有必要，您也可以明確豁免一組使用者，進行從您的原則中排除這些使用者。</span><span class="sxs-lookup"><span data-stu-id="01853-168">If necessary, you can also explicitly exclude a set of users from your policy by exempting them.</span></span>  
<span data-ttu-id="01853-169">選取使用者和群組，您可以定義您的原則套用至的使用者範圍。</span><span class="sxs-lookup"><span data-stu-id="01853-169">By selecting users and groups, you define the scope of users your policy applies to.</span></span>    

    ![控制](./media/active-directory-conditional-access-azure-portal/08.png)



- <span data-ttu-id="01853-171">**什麼** - 從保護的觀點而言，有些在您的環境中執行的應用程式通常需要更多關注 (相較於其他應用程式)。</span><span class="sxs-lookup"><span data-stu-id="01853-171">**What** - Typically, there are certain apps that are running in your environment requiring, from a protection perspective, more attention than others.</span></span> <span data-ttu-id="01853-172">例如，這會影響有權存取敏感性資料的應用程式。</span><span class="sxs-lookup"><span data-stu-id="01853-172">This affects, for example, apps that have access to sensitive data.</span></span>
<span data-ttu-id="01853-173">選取雲端應用程式，您可以定義您的原則套用至的雲端應用程式範圍。</span><span class="sxs-lookup"><span data-stu-id="01853-173">By selecting cloud apps, you define the scope of cloud apps your policy applies to.</span></span> <span data-ttu-id="01853-174">如有必要，您也可以從您的原則中明確排除一組應用程式。</span><span class="sxs-lookup"><span data-stu-id="01853-174">If necessary, you can also explicitly exclude a set of apps from your policy.</span></span>

    ![控制](./media/active-directory-conditional-access-azure-portal/09.png)


- <span data-ttu-id="01853-176">**如何** - 只要您的應用程式存取是在您可以控制的條件下執行，就可能不需要對使用者存取您雲端應用程式的方式強加其他控制項。</span><span class="sxs-lookup"><span data-stu-id="01853-176">**How** - As long as access to your apps is performed under conditions you can control, there might be no need for imposing additional controls on how your cloud apps are accessed by your users.</span></span> <span data-ttu-id="01853-177">不過，如果從不受信任的網路或不符合規範的裝置執行您的雲端應用程式存取，情況可能會有所不同。</span><span class="sxs-lookup"><span data-stu-id="01853-177">However, things might look different if access to your cloud apps is performed, for example, from networks that are not trusted or devices that are not compliant.</span></span> <span data-ttu-id="01853-178">在條件陳述式中，您可以定義某些存取條件，其對應用程式存取的執行方式有額外需求。</span><span class="sxs-lookup"><span data-stu-id="01853-178">In a condition statement, you can define certain access conditions that have additional requirements for how access to your apps is performed.</span></span>

    ![條件](./media/active-directory-conditional-access-azure-portal/21.png)


## <a name="conditions"></a><span data-ttu-id="01853-180">條件</span><span class="sxs-lookup"><span data-stu-id="01853-180">Conditions</span></span>

<span data-ttu-id="01853-181">在目前的 Azure Active Directory 實作中，您可以定義下列領域的條件︰</span><span class="sxs-lookup"><span data-stu-id="01853-181">In the current implementation of Azure Active Directory, you can define conditions for the following areas:</span></span>

- <span data-ttu-id="01853-182">登入風險</span><span class="sxs-lookup"><span data-stu-id="01853-182">Sign-in risk</span></span>
- <span data-ttu-id="01853-183">裝置平台</span><span class="sxs-lookup"><span data-stu-id="01853-183">Device platforms</span></span>
- <span data-ttu-id="01853-184">位置</span><span class="sxs-lookup"><span data-stu-id="01853-184">Locations</span></span>
- <span data-ttu-id="01853-185">用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="01853-185">Client apps</span></span>

![條件](./media/active-directory-conditional-access-azure-portal/21.png)

### <a name="sign-in-risk"></a><span data-ttu-id="01853-187">登入風險</span><span class="sxs-lookup"><span data-stu-id="01853-187">Sign-in risk</span></span>

<span data-ttu-id="01853-188">登入風險是一種物件，供 Azure Active Directory 用於追蹤非由使用者帳戶合法擁有者執行登入的可能性。</span><span class="sxs-lookup"><span data-stu-id="01853-188">A sign-in risk is an object that is used by Azure Active Directory to track the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span></span> <span data-ttu-id="01853-189">在此物件中，可能性 (高、中或低) 會以名為[登入風險層級](active-directory-reporting-risk-events.md#risk-level)屬性形式儲存。</span><span class="sxs-lookup"><span data-stu-id="01853-189">In this object, the likelihood (High, Medium, or Low) is stored in form of an attribute called [sign-in risk level](active-directory-reporting-risk-events.md#risk-level).</span></span> <span data-ttu-id="01853-190">如果 Azure Active Directory 偵測到登入風險，則會在使用者登入期間產生此物件。</span><span class="sxs-lookup"><span data-stu-id="01853-190">This object is generated during a sign-in of a user if sign-in risks have been detected by Azure Active Directory.</span></span> <span data-ttu-id="01853-191">如需詳細資訊，請參閱[有風險的登入](active-directory-identityprotection.md#risky-sign-ins)。</span><span class="sxs-lookup"><span data-stu-id="01853-191">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span>  
<span data-ttu-id="01853-192">您可以使用計算出的登入風險層級作為條件式存取原則中的條件。</span><span class="sxs-lookup"><span data-stu-id="01853-192">You can use the calculated sign-in risk level as condition in a conditional access policy.</span></span> 

![條件](./media/active-directory-conditional-access-azure-portal/22.png)

### <a name="device-platforms"></a><span data-ttu-id="01853-194">裝置平台</span><span class="sxs-lookup"><span data-stu-id="01853-194">Device platforms</span></span>

<span data-ttu-id="01853-195">裝置平台的特點是您裝置執行的作業系統：</span><span class="sxs-lookup"><span data-stu-id="01853-195">The device platform is characterized by the operating system that is running on your device:</span></span>

- <span data-ttu-id="01853-196">Android</span><span class="sxs-lookup"><span data-stu-id="01853-196">Android</span></span>
- <span data-ttu-id="01853-197">iOS</span><span class="sxs-lookup"><span data-stu-id="01853-197">iOS</span></span>
- <span data-ttu-id="01853-198">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="01853-198">Windows Phone</span></span>
- <span data-ttu-id="01853-199">Windows</span><span class="sxs-lookup"><span data-stu-id="01853-199">Windows</span></span>
- <span data-ttu-id="01853-200">macOS (預覽)。</span><span class="sxs-lookup"><span data-stu-id="01853-200">macOS (preview).</span></span> 

![條件](./media/active-directory-conditional-access-azure-portal/02.png)

<span data-ttu-id="01853-202">您可以定義包含的裝置平台以及從原則中豁免的裝置平台。</span><span class="sxs-lookup"><span data-stu-id="01853-202">You can define the device platforms that are included as well as device platforms that are exempted from a policy.</span></span>  
<span data-ttu-id="01853-203">若要使用原則中的裝置平台，請先將 [設定] 切換為 [是]，然後選取原則套用至的所有或個別裝置平台。</span><span class="sxs-lookup"><span data-stu-id="01853-203">To use device platforms in the policy, first change the configure toggles to **Yes**, and then select all or individual device platforms the policy applies to.</span></span> <span data-ttu-id="01853-204">如果您選取個別的裝置平台，原則就只會影響這些平台。</span><span class="sxs-lookup"><span data-stu-id="01853-204">If you select individual device platforms, the policy has only an impact on these platforms.</span></span> <span data-ttu-id="01853-205">在此情況下，其他支援平台的登入不受此原則影響。</span><span class="sxs-lookup"><span data-stu-id="01853-205">In this case, sign-ins to other supported platforms are not impacted by the policy.</span></span>


### <a name="locations"></a><span data-ttu-id="01853-206">位置</span><span class="sxs-lookup"><span data-stu-id="01853-206">Locations</span></span>

<span data-ttu-id="01853-207">您用來連線到 Azure Active Directory 之用戶端 IP 位址所識別的位置。</span><span class="sxs-lookup"><span data-stu-id="01853-207">The location is identified by the IP address of the client you have used to connect to Azure Active Directory.</span></span> <span data-ttu-id="01853-208">此條件要求您需熟悉**具名位置**和 **MFA 信任 IP**。</span><span class="sxs-lookup"><span data-stu-id="01853-208">This condition requires you to be familiar with **named locations** and **MFA trusted IPs**.</span></span>  

<span data-ttu-id="01853-209">**具名位置**是 Azure Active Directory 的一個功能，可讓您標記組織中信任的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="01853-209">**Named locations** is a feature of Azure Active Directory which allows you to label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="01853-210">在您的環境中，您可以在[風險事件](active-directory-reporting-risk-events.md)偵測內容中使用具名位置以及條件式存取。</span><span class="sxs-lookup"><span data-stu-id="01853-210">In your environment, you can use named locations in the context of the detection of [risk events](active-directory-reporting-risk-events.md) as well as conditional access.</span></span> <span data-ttu-id="01853-211">如需有關在 Azure Active Directory 中設定具名位置的詳細資訊，請參閱 [Azure Active Directory 中的具名位置](active-directory-named-locations.md)。</span><span class="sxs-lookup"><span data-stu-id="01853-211">For more details about configuring named locations in Azure Active Directory, see [named locations in Azure Active Directory](active-directory-named-locations.md).</span></span>

<span data-ttu-id="01853-212">您可以設定的位置數目受到 Azure AD 中相關物件大小的限制。</span><span class="sxs-lookup"><span data-stu-id="01853-212">The number of locations you can configure is constrained by the size of the related object in Azure AD.</span></span> <span data-ttu-id="01853-213">您可以設定：</span><span class="sxs-lookup"><span data-stu-id="01853-213">You can configure:</span></span>
 
 - <span data-ttu-id="01853-214">一個具名位置最多有 500 個 IP 範圍</span><span class="sxs-lookup"><span data-stu-id="01853-214">One named location with up to 500 IP ranges</span></span>
 - <span data-ttu-id="01853-215">最多 60 個具名位置 (預覽)，每個位置皆指派一個 IP 範圍</span><span class="sxs-lookup"><span data-stu-id="01853-215">A maximum of 60 named locations (preview) with one IP range assigned to each of them</span></span> 


<span data-ttu-id="01853-216">**MFA 信任的 IP** 是 Multi-Factor Authentication 的功能，可讓您定義信任的 IP 位址範圍，以代表您組織的區域內部網路。</span><span class="sxs-lookup"><span data-stu-id="01853-216">**MFA trusted IPs** is a feature of multi-factor authentication that enables you to define trusted IP address ranges representing your organization's local intranet.</span></span> <span data-ttu-id="01853-217">當您設定位置條件時，信任的 IP 可讓您區分從您組織的網路與所有其他位置進行的連線。</span><span class="sxs-lookup"><span data-stu-id="01853-217">When you configure a location conditions, Trusted IPs enables you to distinguish between connections made from your organization's network and all other locations.</span></span> <span data-ttu-id="01853-218">如需詳細資訊，請參閱[信任的 IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)。</span><span class="sxs-lookup"><span data-stu-id="01853-218">For more details, see [trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>  



<span data-ttu-id="01853-219">您可以包含所有位置或所有信任的 IP，也可以排除所有信任的 IP。</span><span class="sxs-lookup"><span data-stu-id="01853-219">You can either include all locations or all trusted IPs and you can exclude all trusted IPs.</span></span>

![條件](./media/active-directory-conditional-access-azure-portal/03.png)


### <a name="client-app"></a><span data-ttu-id="01853-221">用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="01853-221">Client app</span></span>

<span data-ttu-id="01853-222">用戶端應用程式可以是您用來連線到 Azure Active Directory 的一般層級應用程式 (網頁瀏覽器、行動裝置應用程式、桌面用戶端)，或者您可以特別選取 Exchange Active Sync。</span><span class="sxs-lookup"><span data-stu-id="01853-222">The client app can be either on a generic level the app (web browser, mobile app, desktop client) you have used to connect to Azure Active Directory or you can specifically select Exchange Active Sync.</span></span>  
<span data-ttu-id="01853-223">舊式驗證是指使用基本驗證的用戶端，例如，未使用新式驗證的舊版 Office 用戶端。</span><span class="sxs-lookup"><span data-stu-id="01853-223">Legacy authentication refers to clients using basic authentication such as older Office clients that don’t use modern authentication.</span></span> <span data-ttu-id="01853-224">舊式驗證目前不支援條件式存取。</span><span class="sxs-lookup"><span data-stu-id="01853-224">Conditional access is currently not supported with legacy authentication.</span></span>

![條件](./media/active-directory-conditional-access-azure-portal/04.png)


## <a name="common-scenarios"></a><span data-ttu-id="01853-226">常見案例</span><span class="sxs-lookup"><span data-stu-id="01853-226">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="01853-227">應用程式需要 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="01853-227">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="01853-228">許多環境中的應用程式需要比其他應用程式更高層級的保護。</span><span class="sxs-lookup"><span data-stu-id="01853-228">Many environments have apps requiring a higher level of protection than the others.</span></span>
<span data-ttu-id="01853-229">例如，有權存取敏感性資料的應用程式。</span><span class="sxs-lookup"><span data-stu-id="01853-229">This is, for example, the case for apps that have access to sensitive data.</span></span>
<span data-ttu-id="01853-230">如果您想要對這些應用程式新增另一層的保護，您可以設定當使用者存取這些應用程式時需要 Multi-Factor Authentication 的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="01853-230">If you want to add another layer of protection to these apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="01853-231">從不受信任的網路存取時需要 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="01853-231">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="01853-232">此案例類似於前一個案例，因為這會新增 Multi-Factor Authentication 的需求。</span><span class="sxs-lookup"><span data-stu-id="01853-232">This scenario is similar to the previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="01853-233">不過，主要差異在於這項需求的條件。</span><span class="sxs-lookup"><span data-stu-id="01853-233">However, the main difference is the condition for this requirement.</span></span>  
<span data-ttu-id="01853-234">雖然前一個案例的焦點在於有權存取敏感性資料的應用程式，而此案例的焦點則在於信任的位置。</span><span class="sxs-lookup"><span data-stu-id="01853-234">While the focus of the previous scenario was on apps with access to sensitve data, the focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="01853-235">換句話說，如果使用者從您不信任的網路存取應用程式，您可能需要 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="01853-235">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="01853-236">只有受信任的裝置可以存取 Office 365 服務</span><span class="sxs-lookup"><span data-stu-id="01853-236">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="01853-237">如果您在自己的環境中使用 Intune，您可以在 Azure 主控台中立即開始使用條件式存取原則介面。</span><span class="sxs-lookup"><span data-stu-id="01853-237">If you are using Intune in your environment, you can immediately start using the conditional access policy interface in the Azure console.</span></span>

<span data-ttu-id="01853-238">許多 Intune 客戶都使用條件式存取來確保只有受信任的裝置可以存取 Office 365 服務。</span><span class="sxs-lookup"><span data-stu-id="01853-238">Many Intune customers are using conditional access to ensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="01853-239">這表示行動裝置已向 Intune 進行註冊並符合合規性原則需求，而且 Windows 電腦已加入內部部署網域。</span><span class="sxs-lookup"><span data-stu-id="01853-239">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined to an on-premises domain.</span></span> <span data-ttu-id="01853-240">您不需要為每項 Office 365 服務設定相同的原則，是一項重大改進。</span><span class="sxs-lookup"><span data-stu-id="01853-240">A key improvement is that you do not have to set the same policy for each of the Office 365 services.</span></span>  <span data-ttu-id="01853-241">當您建立新原則時，請設定雲端應用程式包含您想要使用條件式存取保護的每個 O365 應用程式。</span><span class="sxs-lookup"><span data-stu-id="01853-241">When you create a new policy, configure the Cloud apps to include each of the O365 apps that you wish to protect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01853-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="01853-242">Next steps</span></span>

<span data-ttu-id="01853-243">如果您想要知道如何設定條件式存取原則，請參閱[開始使用 Azure Active Directory 中的條件式存取](active-directory-conditional-access-azure-portal-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="01853-243">If you want to know how to configure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>

<span data-ttu-id="01853-244">如果您已準備好設定您環境的條件式存取原則，請參閱 [Azure Active Directory 中條件式存取的最佳做法](active-directory-conditional-access-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="01853-244">If you are ready to configure conditional access policies for your environment, see the [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span> 