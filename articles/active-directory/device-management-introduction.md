---
title: "在 Azure Active Directory aaaIntroduction toodevice 管理 |Microsoft 文件"
description: "瞭解裝置的管理可以協助您 tooget 控制 hello 裝置存取您的環境中的資源。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a><span data-ttu-id="124c5-103">Azure Active Directory 中的簡介 toodevice 管理</span><span class="sxs-lookup"><span data-stu-id="124c5-103">Introduction toodevice management in Azure Active Directory</span></span>

<span data-ttu-id="124c5-104">在行動裝置-首先，雲端優先世界中，Azure Active Directory (Azure AD) 可讓單一登入 toodevices、 應用程式和服務從任何地方。</span><span class="sxs-lookup"><span data-stu-id="124c5-104">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="124c5-105">Hello 激增裝置-包括攜帶您自己的裝置 (BYOD)，與 IT 專業人員正面臨著逼近對方的兩個目標：</span><span class="sxs-lookup"><span data-stu-id="124c5-105">With hello proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="124c5-106">無論在何處，每當加持 hello 使用者 toobe 生產力</span><span class="sxs-lookup"><span data-stu-id="124c5-106">Empower hello end users toobe productive wherever and whenever</span></span>
- <span data-ttu-id="124c5-107">在任何階段保護 hello 公司資產</span><span class="sxs-lookup"><span data-stu-id="124c5-107">Protect hello corporate assets at any time</span></span>

<span data-ttu-id="124c5-108">透過裝置，您的使用者能夠存取 tooyour 公司資產。</span><span class="sxs-lookup"><span data-stu-id="124c5-108">Through devices, your users are getting access tooyour corporate assets.</span></span> <span data-ttu-id="124c5-109">tooprotect 公司資產，身為 IT 管理員，您會想 toohave 控制這些裝置。</span><span class="sxs-lookup"><span data-stu-id="124c5-109">tooprotect your corporate assets, as an IT administrator, you want toohave control over these devices.</span></span> <span data-ttu-id="124c5-110">這可讓您 toomake 確定您的使用者會從符合您的安全性與相容性的標準的裝置存取您的資源。</span><span class="sxs-lookup"><span data-stu-id="124c5-110">This enables you toomake sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="124c5-111">裝置管理也是 hello 基礎[裝置型條件式存取](active-directory-conditional-access-policy-connected-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="124c5-111">Device management is also hello foundation for [device-based conditional access](active-directory-conditional-access-policy-connected-applications.md).</span></span> <span data-ttu-id="124c5-112">使用裝置型條件式存取，您可以確保的存取您的環境中 tooresources 只適用於受信任的裝置。</span><span class="sxs-lookup"><span data-stu-id="124c5-112">With device-based conditional access, you can ensure that access tooresources in your environment is only possible with trusted devices.</span></span>   

<span data-ttu-id="124c5-113">本主題說明 Azure Active Directory 中的裝置管理運作方式。</span><span class="sxs-lookup"><span data-stu-id="124c5-113">This topic explains how device management in Azure Active Directory works.</span></span>

## <a name="getting-devices-under-hello-control-of-azure-ad"></a><span data-ttu-id="124c5-114">取得 Azure AD 的 hello 控制下的裝置</span><span class="sxs-lookup"><span data-stu-id="124c5-114">Getting devices under hello control of Azure AD</span></span>

<span data-ttu-id="124c5-115">tooget hello 控制項下的 Azure AD 的裝置，您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="124c5-115">tooget a device under hello control of Azure AD, you have two options:</span></span>

- <span data-ttu-id="124c5-116">註冊</span><span class="sxs-lookup"><span data-stu-id="124c5-116">Registering</span></span> 
- <span data-ttu-id="124c5-117">加入</span><span class="sxs-lookup"><span data-stu-id="124c5-117">Joining</span></span>

<span data-ttu-id="124c5-118">**註冊**裝置 tooAzure AD 可讓您 toomanage 裝置的身分識別。</span><span class="sxs-lookup"><span data-stu-id="124c5-118">**Registering** a device tooAzure AD enables you toomanage a device’s identity.</span></span> <span data-ttu-id="124c5-119">裝置註冊時，Azure AD 裝置註冊提供 hello 裝置是使用的 tooauthenticate hello 裝置時使用者 」 登入時 AD tooAzure 的身分。</span><span class="sxs-lookup"><span data-stu-id="124c5-119">When a device is registered, Azure AD device registration provides hello device with an identity that is used tooauthenticate hello device when a user signs-in tooAzure AD.</span></span> <span data-ttu-id="124c5-120">您可以使用 hello 識別 tooenable 或停用裝置。</span><span class="sxs-lookup"><span data-stu-id="124c5-120">You can use hello identity tooenable or disable a device.</span></span>

<span data-ttu-id="124c5-121">與 Microsoft Intune 等行動裝置 management(MDM) 解決方案結合時，在 Azure AD 中的 hello 裝置屬性會更新 hello 裝置有關的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="124c5-121">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure AD are updated with additional information about hello device.</span></span> <span data-ttu-id="124c5-122">這可讓您 toocreate 條件式存取規則，以強制從裝置 toomeet 存取您的安全性與相容性的標準。</span><span class="sxs-lookup"><span data-stu-id="124c5-122">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="124c5-123">如需如何在 Microsoft Intune 中註冊裝置的詳細資訊，請參閱＜在 Intune 中註冊要管理的裝置＞。</span><span class="sxs-lookup"><span data-stu-id="124c5-123">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span></span>

<span data-ttu-id="124c5-124">**聯結**裝置是副檔名 tooregistering 裝置。</span><span class="sxs-lookup"><span data-stu-id="124c5-124">**Joining** a device is an extension tooregistering a device.</span></span> <span data-ttu-id="124c5-125">這表示，它可讓您獲得所有 hello 優勢註冊裝置，以及在加法 toothis，它也會變更裝置的 hello 本機狀態。</span><span class="sxs-lookup"><span data-stu-id="124c5-125">This means, it provides you with all hello benefits of registering a device and in addition toothis, it also changes hello local state of a device.</span></span> <span data-ttu-id="124c5-126">變更 hello 本機狀態可讓您使用組織的工作或學校帳戶，而不個人帳戶的使用者 toosign 中 tooa 裝置。</span><span class="sxs-lookup"><span data-stu-id="124c5-126">Changing hello local state enables your users toosign-in tooa device using an organizational work or school account instead of a personal account.</span></span>

## <a name="azure-ad-registered-devices"></a><span data-ttu-id="124c5-127">Azure AD 註冊裝置</span><span class="sxs-lookup"><span data-stu-id="124c5-127">Azure AD registered devices</span></span>   

<span data-ttu-id="124c5-128">hello 的目標 Azure AD 註冊的裝置是您的支援 hello tooprovide**攜帶您自己的裝置 (BYOD)**案例。</span><span class="sxs-lookup"><span data-stu-id="124c5-128">hello goal of Azure AD registered devices is tooprovide you with support for hello **Bring Your Own Device (BYOD)** scenario.</span></span> <span data-ttu-id="124c5-129">在此案例中，使用者可以使用個人裝置存取貴組織的 Azure Active Directory 受控資源。</span><span class="sxs-lookup"><span data-stu-id="124c5-129">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span></span>  

![Azure AD 註冊裝置](./media/device-management-introduction/03.png)

<span data-ttu-id="124c5-131">hello 存取根據已輸入 hello 裝置的工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="124c5-131">hello access is based on a work or school account that has been entered on hello device.</span></span>  
<span data-ttu-id="124c5-132">例如，Windows 10 可讓使用者 tooadd 工作或學校帳戶 tooa 個人電腦、 平板電腦或電話。</span><span class="sxs-lookup"><span data-stu-id="124c5-132">For example, Windows 10 enables users tooadd a work or school account tooa personal computer, tablet, or phone.</span></span>  
<span data-ttu-id="124c5-133">當將使用者新增工作或學校帳戶，hello 裝置是向 Azure AD 註冊，並選擇性地註冊您的組織已設定的 hello 行動裝置管理 (MDM) 系統中。</span><span class="sxs-lookup"><span data-stu-id="124c5-133">When a user has added a work or school account, hello device is registered with Azure AD and optionally enrolled in hello mobile device management (MDM) system that your organization has configured.</span></span> <span data-ttu-id="124c5-134">貴組織的使用者可以將工作或學校帳戶 tooa 個人裝置方便：</span><span class="sxs-lookup"><span data-stu-id="124c5-134">Your organization’s users can add a work or school account tooa personal device conveniently:</span></span>

- <span data-ttu-id="124c5-135">當存取 hello 第一次的工作應用程式</span><span class="sxs-lookup"><span data-stu-id="124c5-135">When accessing a work application for hello first time</span></span>
- <span data-ttu-id="124c5-136">手動透過 hello**設定**功能表中的 Windows 10 的 hello 大小寫</span><span class="sxs-lookup"><span data-stu-id="124c5-136">Manually via hello **Settings** menu in hello case of Windows 10</span></span> 

<span data-ttu-id="124c5-137">您可以為 Windows 10、iOS、Android 和 macOS 設定 Azure AD 註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="124c5-137">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span></span>

## <a name="azure-ad-joined-devices"></a><span data-ttu-id="124c5-138">Azure AD 加入裝置</span><span class="sxs-lookup"><span data-stu-id="124c5-138">Azure AD joined devices</span></span>

<span data-ttu-id="124c5-139">加入 Azure AD 裝置 hello 目標是 toosimplify:</span><span class="sxs-lookup"><span data-stu-id="124c5-139">hello goal of Azure AD joined devices is toosimplify:</span></span>

- <span data-ttu-id="124c5-140">Windows 部署工作用的裝置</span><span class="sxs-lookup"><span data-stu-id="124c5-140">Windows deployments of work-owned devices</span></span> 
- <span data-ttu-id="124c5-141">存取 tooorganizational 應用程式和任何 Windows 裝置的資源</span><span class="sxs-lookup"><span data-stu-id="124c5-141">Access tooorganizational apps and resources from any Windows device</span></span>

![Azure AD 註冊裝置](./media/device-management-introduction/02.png)


<span data-ttu-id="124c5-143">這些目標被透過提供自助服務體驗中的使用者，讓 Azure AD 的 hello 控制下工作所擁有的裝置。</span><span class="sxs-lookup"><span data-stu-id="124c5-143">These goals are accomplished by providing your users with a self-service experience for getting work-owned devices under hello control of Azure AD.</span></span>  
<span data-ttu-id="124c5-144">**Azure AD Join** 適用於雲端優先/僅限雲端的組織。</span><span class="sxs-lookup"><span data-stu-id="124c5-144">**Azure AD Join** is intended for organizations that are cloud-first / cloud-only.</span></span> <span data-ttu-id="124c5-145">這些通常是不具內部部署 Windows Server Active Directory 基礎結構的中小型企業。</span><span class="sxs-lookup"><span data-stu-id="124c5-145">These are typically small- and medium-sized businesses that do not have an on-premises Windows Server Active Directory infrastructure.</span></span> 

<span data-ttu-id="124c5-146">實作已加入 Azure AD 裝置可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="124c5-146">Implementing Azure AD joined devices provides you with hello following benefits:</span></span>

- <span data-ttu-id="124c5-147">**單一登入 (SSO)** tooyour Azure 管理 SaaS 應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="124c5-147">**Single-Sign-On (SSO)** tooyour Azure managed SaaS apps and services.</span></span> <span data-ttu-id="124c5-148">存取工作資源時，您的使用者看不到額外的驗證提示。</span><span class="sxs-lookup"><span data-stu-id="124c5-148">Your users don’t see additional authentication prompts when accessing work resources.</span></span> <span data-ttu-id="124c5-149">hello SSO 功能是，即使當它們不是可用的連接的 toohello 網域網路。</span><span class="sxs-lookup"><span data-stu-id="124c5-149">hello SSO functionality is even when they are not connected toohello domain network available.</span></span>

- <span data-ttu-id="124c5-150">在跨加入裝置之間進行使用者設定的**企業符合規範漫遊**。</span><span class="sxs-lookup"><span data-stu-id="124c5-150">**Enterprise compliant roaming** of user settings across joined devices.</span></span> <span data-ttu-id="124c5-151">使用者不需要 tooconnect Microsoft 帳戶 (例如 Hotmail) toosee 設定跨裝置。</span><span class="sxs-lookup"><span data-stu-id="124c5-151">Users don’t need tooconnect a Microsoft account (for example, Hotmail) toosee settings across devices.</span></span>

- <span data-ttu-id="124c5-152">**商務用市集存取 tooWindows**使用 AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="124c5-152">**Access tooWindows Store for Business** using AD account.</span></span> <span data-ttu-id="124c5-153">您的使用者可以選擇從清查 hello 組織預先選取的應用程式。</span><span class="sxs-lookup"><span data-stu-id="124c5-153">Your users can choose from an inventory of applications pre-selected by hello organization.</span></span>

- <span data-ttu-id="124c5-154">**用 Windows Hello**安全且方便存取 toowork 資源的支援。</span><span class="sxs-lookup"><span data-stu-id="124c5-154">**Windows Hello** support for secure and convenient access toowork resources.</span></span>

- <span data-ttu-id="124c5-155">**存取的限制**tooapps 從符合相容性原則的裝置。</span><span class="sxs-lookup"><span data-stu-id="124c5-155">**Restriction of access** tooapps from only devices that meet compliance policy.</span></span>

<span data-ttu-id="124c5-156">雖然 Azure AD Join 主要適用於沒有內部部署 Windows Server Active Directory 基礎結構的組織，您當然也可以在下列情況下使用之：</span><span class="sxs-lookup"><span data-stu-id="124c5-156">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly also use it in scenarios where:</span></span>

- <span data-ttu-id="124c5-157">例如，如果您需要 tooget 行動裝置如平板電腦和手機控制下的，您無法使用在內部部署網域聯結。</span><span class="sxs-lookup"><span data-stu-id="124c5-157">You can’t use an on-premises domain join, for example, if you need tooget mobile devices such as tablets and phones under control.</span></span>

- <span data-ttu-id="124c5-158">您的使用者主要需要 tooaccess Office 365 或其他與 Azure AD 整合的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="124c5-158">Your users primarily need tooaccess Office 365 or other SaaS apps integrated with Azure AD.</span></span>

- <span data-ttu-id="124c5-159">您想 toomanage 一群使用者，而不是在 Active Directory 中的 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="124c5-159">You want toomanage a group of users in Azure AD instead of in Active Directory.</span></span> <span data-ttu-id="124c5-160">這可以套用，比方說，tooseasonal 工作者、 約聘員工或學生。</span><span class="sxs-lookup"><span data-stu-id="124c5-160">This can apply, for example, tooseasonal workers, contractors, or students.</span></span>

- <span data-ttu-id="124c5-161">您想在具有有限的內部部署基礎結構的遠端分公司 tooprovide 聯結功能 tooworkers。</span><span class="sxs-lookup"><span data-stu-id="124c5-161">You want tooprovide joining capabilities tooworkers in remote branch offices with limited on-premises infrastructure.</span></span>

<span data-ttu-id="124c5-162">您可以設定適用於 Windows 10 裝置的 Azure AD 已加入裝置。</span><span class="sxs-lookup"><span data-stu-id="124c5-162">You can configure Azure AD joined devices for Windows 10 devices.</span></span>


## <a name="hybrid-azure-ad-joined-devices"></a><span data-ttu-id="124c5-163">混合式 Azure AD 已加入裝置</span><span class="sxs-lookup"><span data-stu-id="124c5-163">Hybrid Azure AD joined devices</span></span>

<span data-ttu-id="124c5-164">超過十年以上，許多組織已使用 hello 網域聯結 tootheir 在內部部署 Active Directory tooenable:</span><span class="sxs-lookup"><span data-stu-id="124c5-164">For more than a decade, many organizations have used hello domain join tootheir on-premises Active Directory tooenable:</span></span>

- <span data-ttu-id="124c5-165">IT 部門 toomanage 工作所擁有的裝置從中央位置。</span><span class="sxs-lookup"><span data-stu-id="124c5-165">IT departments toomanage work-owned devices from a central location.</span></span>

- <span data-ttu-id="124c5-166">Tootheir 裝置向其 Active Directory 中的使用者 toosign 工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="124c5-166">Users toosign in tootheir devices with their Active Directory work or school accounts.</span></span> 

<span data-ttu-id="124c5-167">通常，組織在內部部署磁碟使用量依賴影像方法 tooprovision 裝置，並經常使用**System Center Configuration Manager (SCCM)**或**群組原則 (GP)** toomanage它們。</span><span class="sxs-lookup"><span data-stu-id="124c5-167">Typically, organizations with an on-premises footprint rely on imaging methods tooprovision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** toomanage them.</span></span>

<span data-ttu-id="124c5-168">如果您的環境具有內部部署 AD 使用量，並也獲益 hello Azure Active Directory 所提供的功能，您可以實作混合式已加入 Azure AD 裝置。</span><span class="sxs-lookup"><span data-stu-id="124c5-168">If your environment has an on-premises AD footprint and you also want benefit from hello capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="124c5-169">這些是兩者的裝置，聯結的 tooyour 內部部署 Active Directory 與 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="124c5-169">These are devices that are both, joined tooyour on-premises Active Directory and your Azure Active Directory.</span></span>

![Azure AD 註冊裝置](./media/device-management-introduction/01.png)


<span data-ttu-id="124c5-171">您應該使用 Azure AD 混合式加入裝置，如果：</span><span class="sxs-lookup"><span data-stu-id="124c5-171">You should use Azure AD hybrid joined devices if:</span></span>

- <span data-ttu-id="124c5-172">您有使用 NTLM 的 Win32 應用程式部署的 toothese 裝置 / Kerberos。</span><span class="sxs-lookup"><span data-stu-id="124c5-172">You have Win32 apps deployed toothese devices that use NTLM / Kerberos.</span></span>

- <span data-ttu-id="124c5-173">您需要 GP 或使用 SCCM / DCM toomanage 裝置。</span><span class="sxs-lookup"><span data-stu-id="124c5-173">You require GP or SCCM / DCM toomanage devices.</span></span>

- <span data-ttu-id="124c5-174">您想 toocontinue toouse 影像解決方案 tooconfigure 裝置的員工。</span><span class="sxs-lookup"><span data-stu-id="124c5-174">You want toocontinue toouse imaging solutions tooconfigure devices for your employees.</span></span>

<span data-ttu-id="124c5-175">您可以針對 Windows 10 及舊版裝置 (例如 Windows 8 和 Windows 7) 設定混合式 Azure AD 已加入裝置。</span><span class="sxs-lookup"><span data-stu-id="124c5-175">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span></span>

## <a name="summary"></a><span data-ttu-id="124c5-176">摘要</span><span class="sxs-lookup"><span data-stu-id="124c5-176">Summary</span></span>

<span data-ttu-id="124c5-177">使用 Azure AD 中的裝置管理，您可以：</span><span class="sxs-lookup"><span data-stu-id="124c5-177">With device management in Azure AD, you can:</span></span> 

- <span data-ttu-id="124c5-178">簡化 Azure AD 的 hello 控制權攜帶裝置 hello 程的序</span><span class="sxs-lookup"><span data-stu-id="124c5-178">Simplify hello process of bringing devices under hello control of Azure AD</span></span>

- <span data-ttu-id="124c5-179">為使用者提供輕鬆 toouse 存取 tooyour 組織的雲端資源</span><span class="sxs-lookup"><span data-stu-id="124c5-179">Provide your users with an easy toouse access tooyour organization’s cloud-based resources</span></span>

<span data-ttu-id="124c5-180">根據經驗法則，您應該使用：</span><span class="sxs-lookup"><span data-stu-id="124c5-180">As a rule of a thumb, you should use:</span></span>

- <span data-ttu-id="124c5-181">適用於個人裝置的 Azure AD 註冊裝置</span><span class="sxs-lookup"><span data-stu-id="124c5-181">Azure AD registered devices for personal devices</span></span>

- <span data-ttu-id="124c5-182">Azure AD 已加入裝置的裝置加入 tooan 在內部部署 AD</span><span class="sxs-lookup"><span data-stu-id="124c5-182">Azure AD joined devices for devices that are not joined tooan on-premises AD</span></span> 

- <span data-ttu-id="124c5-183">Azure AD 混合式已加入裝置的裝置加入 tooan 在內部部署 AD</span><span class="sxs-lookup"><span data-stu-id="124c5-183">Hybrid Azure AD joined devices for devices that are joined tooan on-premises AD</span></span>     




## <a name="next-steps"></a><span data-ttu-id="124c5-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="124c5-184">Next steps</span></span>

- <span data-ttu-id="124c5-185">如何在 toomanage 裝置 hello Azure 入口網站，請參閱概觀 tooget[管理使用 hello Azure 入口網站的裝置](device-management-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="124c5-185">tooget an overview of how toomanage device in hello Azure portal, see [managing devices using hello Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="124c5-186">toolearn 進一步了解裝置型條件式存取，請參閱[設定 Azure Active Directory 裝置型條件式存取原則](active-directory-conditional-access-policy-connected-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="124c5-186">toolearn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](active-directory-conditional-access-policy-connected-applications.md).</span></span>

- <span data-ttu-id="124c5-187">toosetup 混合加入 Azure AD 裝置，請參閱[tooconfigure 混合 Azure Active Directory 如何聯結裝置](device-management-hybrid-azuread-joined-devices-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="124c5-187">toosetup hybrid Azure AD joined devices, see [how tooconfigure hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md).</span></span>


