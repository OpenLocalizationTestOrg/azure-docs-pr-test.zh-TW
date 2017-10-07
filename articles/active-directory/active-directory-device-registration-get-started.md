---
title: "aaaHow tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory |Microsoft 文件"
description: "設定您已加入網域的 Windows 裝置 tooregister 自動且無訊息地與 Azure Active Directory。"
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="c99c1-103">開始使用 Azure Active Directory 裝置註冊</span><span class="sxs-lookup"><span data-stu-id="c99c1-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="c99c1-104">Azure Active Directory 裝置註冊是裝置型條件式存取案例的 hello 基礎。</span><span class="sxs-lookup"><span data-stu-id="c99c1-104">Azure Active Directory device registration is hello foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="c99c1-105">裝置註冊時，Azure Active Directory 裝置註冊提供 hello 裝置時，才能使用的 tooauthenticate hello 裝置 hello 使用者登入身分識別。</span><span class="sxs-lookup"><span data-stu-id="c99c1-105">When a device is registered, Azure Active Directory device registration provides hello device with an identity which is used tooauthenticate hello device when hello user signs in.</span></span> <span data-ttu-id="c99c1-106">hello 驗證裝置 hello 裝置 hello 屬性接著可以使用的 tooenforce hello 雲端和內部部署中裝載的應用程式的條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="c99c1-106">hello authenticated device, and hello attributes of hello device, can then be used tooenforce conditional access policies for applications that are hosted in hello cloud and on-premises.</span></span>

<span data-ttu-id="c99c1-107">與 Microsoft Intune 等行動裝置 management(MDM) 解決方案結合時，Azure Active Directory 中的 hello 裝置屬性會更新 hello 裝置有關的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="c99c1-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure Active Directory are updated with additional information about hello device.</span></span> <span data-ttu-id="c99c1-108">這可讓您 toocreate 條件式存取規則，以強制從裝置 toomeet 存取您的安全性與相容性的標準。</span><span class="sxs-lookup"><span data-stu-id="c99c1-108">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="c99c1-109">如需如何在 Microsoft Intune 中註冊裝置的詳細資訊，請參閱＜在 Intune 中註冊要管理的裝置＞。</span><span class="sxs-lookup"><span data-stu-id="c99c1-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="c99c1-110">由 Azure Active Directory 裝置註冊 Azure Active Directory 裝置註冊啟用的案例包括對 iOS、Android 與 Windows 裝置的支援。</span><span class="sxs-lookup"><span data-stu-id="c99c1-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="c99c1-111">利用 Azure AD 裝置註冊的 hello 個別案例可能更特定的需求和支援的平台。</span><span class="sxs-lookup"><span data-stu-id="c99c1-111">hello individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="c99c1-112">這些案例如下所示︰</span><span class="sxs-lookup"><span data-stu-id="c99c1-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="c99c1-113">**Office 365 應用程式使用 Microsoft Intune 的條件式存取：** IT 系統管理員可以佈建條件式存取裝置原則 toosecure 公司資源，而 hello 在相同時間允許相容裝置上的資訊工作者tooaccess hello 服務。</span><span class="sxs-lookup"><span data-stu-id="c99c1-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies toosecure corporate resources, while at hello same time allowing information workers on compliant devices tooaccess hello services.</span></span> <span data-ttu-id="c99c1-114">如需詳細資訊，請參閱 Office 365 服務的條件式存取裝置原則。</span><span class="sxs-lookup"><span data-stu-id="c99c1-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="c99c1-115">**條件式存取 tooapplications 屬於裝載在內部部署：**的應用程式設定 toouse AD FS 與 Windows Server 2012 R2，您可以存取原則搭配使用已註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="c99c1-115">**Conditional access tooapplications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured toouse AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="c99c1-116">如需有關設定內部部署之條件式存取的詳細資訊，請參閱[使用 Azure Active Directory 裝置註冊設定內部部署條件式存取](active-directory-device-registration-on-premises-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="c99c1-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="c99c1-117">設定 Azure Active Directory 裝置註冊</span><span class="sxs-lookup"><span data-stu-id="c99c1-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="c99c1-118">toosetup 裝置註冊，您有多個選項：</span><span class="sxs-lookup"><span data-stu-id="c99c1-118">toosetup device registration, you have multiple options:</span></span>

- <span data-ttu-id="c99c1-119">裝置可以註冊時聯結的 tooAzure AD 網域。</span><span class="sxs-lookup"><span data-stu-id="c99c1-119">Devices can register when joined tooAzure AD domain.</span></span> <span data-ttu-id="c99c1-120">如需本主題的詳細資訊，您可以進一步了解 Azure AD Join 和 hello 設定所需的使用者 toojoin Azure AD 網域。</span><span class="sxs-lookup"><span data-stu-id="c99c1-120">For more on this topic, you can Learn more about Azure AD Join and hello settings required for users toojoin Azure AD domain.</span></span>

- <span data-ttu-id="c99c1-121">當使用者新增工作或學校帳戶 tooWindows，個人裝置或行動裝置連線需要登錄 tooa 工作資源時，就可以註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="c99c1-121">Devices can be registered when users add work or school accounts tooWindows on a personal device or when mobile devices connect tooa work resources requiring registration.</span></span> <span data-ttu-id="c99c1-122">tooensure，您必須啟用 Azure AD 裝置註冊 hello Azure 入口網站中的。</span><span class="sxs-lookup"><span data-stu-id="c99c1-122">tooensure this, you must enable Azure AD Device Registration in hello Azure Portal.</span></span> 

- <span data-ttu-id="c99c1-123">裝置可以針對已加入網域的傳統電腦使用自動裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="c99c1-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="c99c1-124">tooensure，繼續進行 自動註冊裝置之前，必須第一個安裝 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="c99c1-124">tooensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="c99c1-125">最新說明，請參閱[如何 tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="c99c1-125">For latest instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="c99c1-126">您也可以檢閱和啟用或停用已註冊的裝置使用 Azure Active Directory 中的 hello 管理員入口網站。</span><span class="sxs-lookup"><span data-stu-id="c99c1-126">You can also review and enable or disable registered devices using hello Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-hello-azure-active-directory-device-registration-service"></a><span data-ttu-id="c99c1-127">啟用 hello Azure Active Directory 裝置註冊服務</span><span class="sxs-lookup"><span data-stu-id="c99c1-127">Enable hello Azure Active Directory device registration service</span></span>

<span data-ttu-id="c99c1-128">**tooenable hello Azure Active Directory 裝置註冊服務：**</span><span class="sxs-lookup"><span data-stu-id="c99c1-128">**tooenable hello Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="c99c1-129">Toohello Microsoft Azure 入口網站管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="c99c1-129">Sign in toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="c99c1-130">在 hello 左窗格中，選取  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="c99c1-130">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="c99c1-131">Hello 目錄索引標籤上，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="c99c1-131">On hello Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="c99c1-132">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="c99c1-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="c99c1-133">捲動太**裝置**。</span><span class="sxs-lookup"><span data-stu-id="c99c1-133">Scroll too**Devices**.</span></span>

6.  <span data-ttu-id="c99c1-134">針對 [使用者可以向 Azure AD 註冊其裝置] 選取 [全部]。</span><span class="sxs-lookup"><span data-stu-id="c99c1-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="c99c1-135">選取 hello 最大數目的裝置，您想 tooauthorize 每位使用者。</span><span class="sxs-lookup"><span data-stu-id="c99c1-135">Select hello maximum number of devices you want tooauthorize per user.</span></span>

<span data-ttu-id="c99c1-136">使用 Microsoft Intune 或行動裝置管理 Office 365 的 hello 註冊需要裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="c99c1-136">hello enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="c99c1-137">如果您已設定任一服務，則會選取 [全部] 並停用 [無]。</span><span class="sxs-lookup"><span data-stu-id="c99c1-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="c99c1-138">請確定它們已正確設定，且有 hello 適當授權。</span><span class="sxs-lookup"><span data-stu-id="c99c1-138">Please ensure that they are configured correctly and have hello appropriate licensing.</span></span>

<span data-ttu-id="c99c1-139">根據預設，不會對 hello 服務啟用雙因素驗證。</span><span class="sxs-lookup"><span data-stu-id="c99c1-139">By default, two-factor authentication is not enabled for hello service.</span></span> <span data-ttu-id="c99c1-140">不過，建議在註冊裝置時使用雙因素驗證。</span><span class="sxs-lookup"><span data-stu-id="c99c1-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="c99c1-141">此服務要求雙因素驗證，您必須在 Azure Active Directory 中設定雙因素驗證提供者和設定您的使用者帳戶的多重要素驗證，請參閱新增多因素驗證tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c99c1-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication tooAzure Active Directory</span></span>

- <span data-ttu-id="c99c1-142">如果您搭配使用 AD FS 與 Windows Server 2012 R2，則必須在 AD FS 中設定雙因素驗證模組，請參閱＜搭配使用 Multi-Factor Authentication 與 Active Directory 同盟服務＞。</span><span class="sxs-lookup"><span data-stu-id="c99c1-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="c99c1-143">在 Azure Active Directory 中檢視和管理裝置物件</span><span class="sxs-lookup"><span data-stu-id="c99c1-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="c99c1-144">從 hello Azure 系統管理員入口網站，您可以檢視、 封鎖和解除封鎖裝置。</span><span class="sxs-lookup"><span data-stu-id="c99c1-144">From hello Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="c99c1-145">已封鎖的裝置將不再有存取 tooapplications 設定的 tooallow 只有已註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="c99c1-145">A device that is blocked will no longer have access tooapplications that are configured tooallow only registered devices.</span></span>

<span data-ttu-id="c99c1-146">**tooview 和管理 Azure Active Directory 中的裝置物件：**</span><span class="sxs-lookup"><span data-stu-id="c99c1-146">**tooview and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="c99c1-147">Toohello Microsoft Azure 入口網站管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="c99c1-147">Log on toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="c99c1-148">在 hello 左窗格中，選取  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="c99c1-148">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="c99c1-149">選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="c99c1-149">Select your directory.</span></span>

4.  <span data-ttu-id="c99c1-150">選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="c99c1-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="c99c1-151">按一下您想要的 toosee hello 裝置 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="c99c1-151">Click hello user for which you want toosee hello devices.</span></span>

6.  <span data-ttu-id="c99c1-152">選取 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="c99c1-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="c99c1-153">選取 [註冊的裝置]。</span><span class="sxs-lookup"><span data-stu-id="c99c1-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="c99c1-154">現在，您可以檢閱、 封鎖或解除封鎖 hello 使用者已註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="c99c1-154">Now, you can review, block, or unblock hello user's registered devices.</span></span>
<span data-ttu-id="c99c1-155">會在內部部署網域和自動註冊的 Windows 10 裝置不會出現在 hello 使用者 索引標籤下。請使用 hello Get MsolDevice PowerShell 命令 toofind 所有企業裝置。</span><span class="sxs-lookup"><span data-stu-id="c99c1-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under hello Users tab. Please use hello Get-MsolDevice PowerShell command toofind all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="c99c1-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c99c1-156">Next steps</span></span>

<span data-ttu-id="c99c1-157">toosetup 自動裝置註冊，請參閱[如何 tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="c99c1-157">toosetup automated device registration, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


