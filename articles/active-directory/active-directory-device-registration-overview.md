---
title: "aaaAzure Active Directory 裝置註冊概觀 |Microsoft 文件"
description: "Azure Active Directory 裝置註冊是裝置型條件式存取案例的 hello 基礎。 註冊裝置時，Azure Active Directory 裝置註冊會佈建 hello 裝置時，才能使用的 tooauthenticate hello 裝置 hello 使用者登入身分識別。"
services: active-directory
keywords: "裝置註冊, 啟用裝置註冊, 裝置註冊和 MDM"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 1e92c1a2-01b8-4225-950b-373cd601b035
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: b9846e34fe873d271ebe71cbf8e70c6b4768885b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="48c03-105">開始使用 Azure Active Directory 裝置註冊</span><span class="sxs-lookup"><span data-stu-id="48c03-105">Get started with Azure Active Directory device registration</span></span>
<span data-ttu-id="48c03-106">Azure Active Directory 裝置註冊是裝置型條件式存取案例的 hello 基礎。</span><span class="sxs-lookup"><span data-stu-id="48c03-106">Azure Active Directory device registration is hello foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="48c03-107">裝置註冊時，Azure Active Directory 裝置註冊提供 hello 裝置時，才能使用的 tooauthenticate hello 裝置 hello 使用者登入身分識別。</span><span class="sxs-lookup"><span data-stu-id="48c03-107">When a device is registered, Azure Active Directory device registration provides hello device with an identity which is used tooauthenticate hello device when hello user signs in.</span></span> <span data-ttu-id="48c03-108">hello 驗證裝置 hello 裝置 hello 屬性接著可以使用的 tooenforce hello 雲端和內部部署中裝載的應用程式的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="48c03-108">hello authenticated device, and hello attributes of hello device, can then be used tooenforce conditional access policies for applications that are hosted in hello cloud and on-premises.</span></span>

<span data-ttu-id="48c03-109">與 Microsoft Intune 等行動裝置 management(MDM) 解決方案結合時，Azure Active Directory 中的 hello 裝置屬性會更新 hello 裝置有關的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="48c03-109">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure Active Directory are updated with additional information about hello device.</span></span> <span data-ttu-id="48c03-110">這可讓您 toocreate 條件式存取規則，以強制從裝置 toomeet 存取您的安全性與相容性的標準。</span><span class="sxs-lookup"><span data-stu-id="48c03-110">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="48c03-111">如需如何在 Microsoft Intune 中註冊裝置的詳細資訊，請參閱 [在 Intune 中註冊要管理的裝置](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)。</span><span class="sxs-lookup"><span data-stu-id="48c03-111">For more information on enrolling devices in Microsoft Intune, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span>

## <a name="scenarios-enabled-by-azure-active-directory-device-registration"></a><span data-ttu-id="48c03-112">Azure Active Directory 裝置註冊所啟用的案例</span><span class="sxs-lookup"><span data-stu-id="48c03-112">Scenarios enabled by Azure Active Directory device registration</span></span>
<span data-ttu-id="48c03-113">Azure Active Directory 裝置註冊可支援 iOS、Android 和 Windows 裝置。</span><span class="sxs-lookup"><span data-stu-id="48c03-113">Azure Active Directory device registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="48c03-114">利用 Azure AD 裝置註冊的 hello 個別案例可能更特定的需求和支援的平台。</span><span class="sxs-lookup"><span data-stu-id="48c03-114">hello individual scenarios that utilize Azure AD device registration may have more specific requirements and platform support.</span></span> <span data-ttu-id="48c03-115">這些案例如下所示︰</span><span class="sxs-lookup"><span data-stu-id="48c03-115">These scenarios are as follows:</span></span>

* <span data-ttu-id="48c03-116">**條件式存取 tooapplications 會裝載於內部**： 您可以使用已註冊的裝置存取原則的應用程式設定 toouse AD FS 與 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="48c03-116">**Conditional access tooapplications that are hosted on-premises**: You can use registered devices with access policies for applications that are configured toouse AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="48c03-117">如需有關設定內部部署之條件式存取的詳細資訊，請參閱[使用 Azure Active Directory 裝置註冊設定內部部署條件式存取](active-directory-device-registration-on-premises-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="48c03-117">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>
* <span data-ttu-id="48c03-118">**Office 365 應用程式使用 Microsoft Intune 的條件式存取**: IT 系統管理員可以佈建條件式存取裝置原則 toosecure 公司資源，而 hello 在相同時間允許相容裝置上的資訊工作者tooaccess hello 服務。</span><span class="sxs-lookup"><span data-stu-id="48c03-118">**Conditional access for Office 365 applications with Microsoft Intune** : IT admins can provision conditional access device policies toosecure corporate resources, while at hello same time allowing information workers on compliant devices tooaccess hello services.</span></span> <span data-ttu-id="48c03-119">如需詳細資訊，請參閱 [Office 365 服務的條件式存取裝置原則](active-directory-conditional-access-device-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="48c03-119">For more information, see [Conditional Access Device Policies for Office 365 services](active-directory-conditional-access-device-policies.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="48c03-120">設定 Azure Active Directory 裝置註冊</span><span class="sxs-lookup"><span data-stu-id="48c03-120">Setting up Azure Active Directory device registration</span></span>
<span data-ttu-id="48c03-121">您需要 tooenable Azure AD 裝置註冊 hello Azure 入口網站中的，讓行動裝置來探索 hello 服務尋找已知的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="48c03-121">You need tooenable Azure AD device registration in hello Azure Portal so that mobile devices  can discover hello service by looking for well-known DNS records.</span></span> <span data-ttu-id="48c03-122">您必須設定公司 DNS，讓 Windows 10、 Windows 8.1、 Windows 7、 Android 和 iOS 裝置可以探索並使用 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="48c03-122">You must configure your company DNS so that Windows 10, Windows 8.1, Windows 7, Android and iOS devices can discover and use hello service.</span></span>
<span data-ttu-id="48c03-123">您可以檢視及啟用/停用已註冊的裝置使用 Azure Active Directory 中的 hello 管理員入口網站。</span><span class="sxs-lookup"><span data-stu-id="48c03-123">You can view and enable/disable registered devices using hello Administrator Portal in Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="48c03-124">如需如何設定自動裝置註冊 tooset 看到，最新的指示[toosetup 自動註冊的 Windows 網域如何聯結裝置與 Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="48c03-124">For latest instructions on how tooset up automatic device registration see, [How toosetup automatic registration of Windows domain joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>
> 
> 

### <a name="enable-azure-active-directory-device-registration-service"></a><span data-ttu-id="48c03-125">啟用 Azure Active Directory 裝置註冊服務</span><span class="sxs-lookup"><span data-stu-id="48c03-125">Enable Azure Active Directory device registration Service</span></span>
1. <span data-ttu-id="48c03-126">Toohello Microsoft Azure 入口網站管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="48c03-126">Sign in toohello Microsoft Azure portal as Administrator.</span></span>
2. <span data-ttu-id="48c03-127">在 hello 左窗格中，選取  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="48c03-127">On hello left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="48c03-128">在 hello**目錄**索引標籤上，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="48c03-128">On hello **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="48c03-129">選取 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="48c03-129">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="48c03-130">捲動 toohello 區段呼叫**裝置**。</span><span class="sxs-lookup"><span data-stu-id="48c03-130">Scroll toohello section called **Devices**.</span></span>
6. <span data-ttu-id="48c03-131">針對 [使用者可以使用「加入工作場所」裝置] 選取 [全部]。</span><span class="sxs-lookup"><span data-stu-id="48c03-131">Select **ALL** for **USERS MAY WORKPLACE JOIN DEVICES**.</span></span>
7. <span data-ttu-id="48c03-132">選取 hello 最大數目的裝置，您想 tooauthorize 每位使用者。</span><span class="sxs-lookup"><span data-stu-id="48c03-132">Select hello maximum number of devices you want tooauthorize per user.</span></span>

> [!NOTE]
> <span data-ttu-id="48c03-133">Microsoft Intune 註冊或 Office 365 的行動裝置管理需要加入工作場所。</span><span class="sxs-lookup"><span data-stu-id="48c03-133">Enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires Workplace Join.</span></span> <span data-ttu-id="48c03-134">如果您已設定任一這些服務，選取所有與 hello NONE 按鈕已停用。</span><span class="sxs-lookup"><span data-stu-id="48c03-134">If you have configured either of these services, ALL is selected and hello NONE button is disabled.</span></span>
> 
> 

<span data-ttu-id="48c03-135">根據預設，不會對 hello 服務啟用雙因素驗證。</span><span class="sxs-lookup"><span data-stu-id="48c03-135">By default, two-factor authentication is not enabled for hello service.</span></span> <span data-ttu-id="48c03-136">不過，建議在註冊裝置時使用雙因素驗證。</span><span class="sxs-lookup"><span data-stu-id="48c03-136">However, two-factor authentication is recommended when registering a device.</span></span>

* <span data-ttu-id="48c03-137">此服務要求雙因素驗證，您必須在 Azure Active Directory 中設定雙因素驗證提供者和設定您的使用者帳戶的多重要素驗證，請參閱[新增多因素驗證 tooAzure Active Directory](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="48c03-137">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see [Adding Multi-Factor Authentication tooAzure Active Directory](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span></span>
* <span data-ttu-id="48c03-138">如果您搭配使用 AD FS 與 Windows Server 2012 R2，則必須在 AD FS 中設定雙因素驗證模組，請參閱 [搭配使用 Multi-Factor Authentication 與 Active Directory Federation Services](../multi-factor-authentication/multi-factor-authentication-get-started-server.md)。</span><span class="sxs-lookup"><span data-stu-id="48c03-138">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see [Using Multi-Factor Authentication with Active Directory Federation Services](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).</span></span>

## <a name="configure-azure-active-directory-device-registration-discovery"></a><span data-ttu-id="48c03-139">設定 Azure Active Directory 裝置註冊探索</span><span class="sxs-lookup"><span data-stu-id="48c03-139">Configure Azure Active Directory device registration discovery</span></span>
<span data-ttu-id="48c03-140">Windows 7 和 Windows 8.1 裝置會結合 hello 使用者帳戶名稱與已知的裝置註冊的伺服器名稱以探索 hello 裝置註冊服務。</span><span class="sxs-lookup"><span data-stu-id="48c03-140">Windows 7 and Windows 8.1 devices will discover hello device registration service by combining hello user account name with a well-known device registration server name.</span></span>

<span data-ttu-id="48c03-141">您必須建立 DNS CNAME 記錄指向與您的 Azure Active Directory 裝置註冊服務相關聯的 toohello A 記錄。</span><span class="sxs-lookup"><span data-stu-id="48c03-141">You must create a DNS CNAME record that points toohello A record associated with your Azure Active Directory device registration service.</span></span> <span data-ttu-id="48c03-142">hello CNAME 記錄必須使用 hello 已知的首碼 enterpriseregistration 後面接著 hello hello 您組織的使用者帳戶所使用的 UPN 尾碼。</span><span class="sxs-lookup"><span data-stu-id="48c03-142">hello CNAME record must use hello well-known prefix enterpriseregistration followed by hello UPN suffix used by hello user accounts at your organization.</span></span> <span data-ttu-id="48c03-143">如果您的組織使用多個 UPN 尾碼，則必須在 DNS 中建立多個 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="48c03-143">If your organization uses multiple UPN suffixes, multiple CNAME records must be created in DNS.</span></span>

<span data-ttu-id="48c03-144">例如，如果您在組織中名為使用兩個 UPN 尾碼@contoso.com和@region.contoso.com，您將建立下列 DNS 記錄的 hello。</span><span class="sxs-lookup"><span data-stu-id="48c03-144">For example, if you use two UPN suffixes at your organization named @contoso.com and @region.contoso.com, you will create hello following DNS records.</span></span>

| <span data-ttu-id="48c03-145">項目</span><span class="sxs-lookup"><span data-stu-id="48c03-145">Entry</span></span> | <span data-ttu-id="48c03-146">類型</span><span class="sxs-lookup"><span data-stu-id="48c03-146">Type</span></span> | <span data-ttu-id="48c03-147">位址</span><span class="sxs-lookup"><span data-stu-id="48c03-147">Address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="48c03-148">enterpriseregistration.contoso.com</span><span class="sxs-lookup"><span data-stu-id="48c03-148">enterpriseregistration.contoso.com</span></span> |<span data-ttu-id="48c03-149">CNAME</span><span class="sxs-lookup"><span data-stu-id="48c03-149">CNAME</span></span> |<span data-ttu-id="48c03-150">enterpriseregistration.windows.net</span><span class="sxs-lookup"><span data-stu-id="48c03-150">enterpriseregistration.windows.net</span></span> |
| <span data-ttu-id="48c03-151">enterpriseregistration.region.contoso.com</span><span class="sxs-lookup"><span data-stu-id="48c03-151">enterpriseregistration.region.contoso.com</span></span> |<span data-ttu-id="48c03-152">CNAME</span><span class="sxs-lookup"><span data-stu-id="48c03-152">CNAME</span></span> |<span data-ttu-id="48c03-153">enterpriseregistration.windows.net</span><span class="sxs-lookup"><span data-stu-id="48c03-153">enterpriseregistration.windows.net</span></span> |

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="48c03-154">在 Azure Active Directory 中檢視和管理裝置物件</span><span class="sxs-lookup"><span data-stu-id="48c03-154">View and manage device objects in Azure Active Directory</span></span>
1. <span data-ttu-id="48c03-155">從 hello Azure 系統管理員入口網站，您可以檢視、 封鎖和解除封鎖裝置。</span><span class="sxs-lookup"><span data-stu-id="48c03-155">From hello Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="48c03-156">已封鎖的裝置將不再有存取 tooapplications 設定的 tooallow 只有已註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="48c03-156">A device that is blocked will no longer have access tooapplications that are configured tooallow only registered devices.</span></span>
2. <span data-ttu-id="48c03-157">系統管理員身分登入 toohello Microsoft Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="48c03-157">Log on toohello Microsoft Azure Portal as Administrator.</span></span>
3. <span data-ttu-id="48c03-158">在 hello 左窗格中，選取  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="48c03-158">On hello left pane, select **Active Directory**.</span></span>
4. <span data-ttu-id="48c03-159">選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="48c03-159">Select your directory.</span></span>
5. <span data-ttu-id="48c03-160">選取 hello**使用者** 索引標籤。然後選取使用者 tooview 他們的裝置</span><span class="sxs-lookup"><span data-stu-id="48c03-160">Select hello **Users** tab. Then select a user tooview their devices</span></span>
6. <span data-ttu-id="48c03-161">選取 hello**裝置** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="48c03-161">Select hello **Devices** tab.</span></span>
7. <span data-ttu-id="48c03-162">選取**登錄裝置**hello 從下拉功能表。</span><span class="sxs-lookup"><span data-stu-id="48c03-162">Select **Registered Devices** from hello drop down menu.</span></span>
8. <span data-ttu-id="48c03-163">您可以在此檢視，封鎖或解除封鎖 hello 使用者已註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="48c03-163">Here you can view, block, or unblock hello users registered devices.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="48c03-164">其他主題</span><span class="sxs-lookup"><span data-stu-id="48c03-164">Additional topics</span></span>
<span data-ttu-id="48c03-165">您可以向 Azure AD 裝置註冊註冊 Windows 7 和 Windows 8.1 加入網域的裝置。</span><span class="sxs-lookup"><span data-stu-id="48c03-165">You can register your Windows 7 and Windows 8.1 Domain Joined devices with Azure AD device registration.</span></span> <span data-ttu-id="48c03-166">hello 下列主題提供在 Windows 7 和 Windows 8.1 裝置上的 hello 必要條件與 hello 步驟需要的 tooconfigure 裝置註冊的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="48c03-166">hello following topics provides more information about hello prerequisites and hello steps required tooconfigure device registration on Windows 7 and Windows 8.1 devices.</span></span>

* [<span data-ttu-id="48c03-167">自動向 Azure Active Directory 註冊加入網域的 Windows 裝置</span><span class="sxs-lookup"><span data-stu-id="48c03-167">Automatic device registration with Azure Active Directory for Windows Domain-Joined Devices</span></span>](active-directory-conditional-access-automatic-device-registration.md)
* [<span data-ttu-id="48c03-168">自動向 Azure Active Directory 註冊加入網域的 Windows 10 裝置</span><span class="sxs-lookup"><span data-stu-id="48c03-168">Automatic device registration with Azure Active Directory for Windows 10 domain-joined devices</span></span>](active-directory-azureadjoin-devices-group-policy.md)

