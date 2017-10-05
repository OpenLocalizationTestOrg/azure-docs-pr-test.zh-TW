---
title: "如何設定讓已加入網域的 Windows 裝置自動向 Azure Active Directory 註冊 | Microsoft Docs"
description: "設定讓已加入網域的 Windows 裝置以自動和無訊息方式向 Azure Active Directory 註冊。"
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
ms.openlocfilehash: 38750050e8525272079e1f3a5509da1e8f0a557b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="60623-103">開始使用 Azure Active Directory 裝置註冊</span><span class="sxs-lookup"><span data-stu-id="60623-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="60623-104">Azure Active Directory 裝置註冊是裝置型條件式存取案例的基礎。</span><span class="sxs-lookup"><span data-stu-id="60623-104">Azure Active Directory device registration is the foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="60623-105">當裝置已註冊時，Azure Active Directory 裝置註冊會在使用者登入時為裝置提供用來驗證裝置的身分識別。</span><span class="sxs-lookup"><span data-stu-id="60623-105">When a device is registered, Azure Active Directory device registration provides the device with an identity which is used to authenticate the device when the user signs in.</span></span> <span data-ttu-id="60623-106">然後已驗證的裝置和裝置的屬性即可用來對裝載於雲端和內部部署的應用程式，強制執行條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="60623-106">The authenticated device, and the attributes of the device, can then be used to enforce conditional access policies for applications that are hosted in the cloud and on-premises.</span></span>

<span data-ttu-id="60623-107">與 Microsoft Intune 這類的行動裝置管理 (MDM) 解決方案結合時，將會以裝置的其他相關資訊更新 Azure Active Directory 中的裝置屬性。</span><span class="sxs-lookup"><span data-stu-id="60623-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure Active Directory are updated with additional information about the device.</span></span> <span data-ttu-id="60623-108">這可讓您建立條件式存取規則，強制讓裝置的存取符合您的安全性和相容性標準。</span><span class="sxs-lookup"><span data-stu-id="60623-108">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span> <span data-ttu-id="60623-109">如需如何在 Microsoft Intune 中註冊裝置的詳細資訊，請參閱＜在 Intune 中註冊要管理的裝置＞。</span><span class="sxs-lookup"><span data-stu-id="60623-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="60623-110">由 Azure Active Directory 裝置註冊 Azure Active Directory 裝置註冊啟用的案例包括對 iOS、Android 與 Windows 裝置的支援。</span><span class="sxs-lookup"><span data-stu-id="60623-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="60623-111">利用 Azure AD 裝置註冊的個別案例可能會有更明確的需求和平台支援。</span><span class="sxs-lookup"><span data-stu-id="60623-111">The individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="60623-112">這些案例如下所示︰</span><span class="sxs-lookup"><span data-stu-id="60623-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="60623-113">**適用於包含 Microsoft Intune 之 Office 365 應用程式的條件式存取：**IT 系統管理員可以佈建條件式存取裝置原則來保護公司資源，同時允許符合規範之裝置上的資訊工作者存取服務。</span><span class="sxs-lookup"><span data-stu-id="60623-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies to secure corporate resources, while at the same time allowing information workers on compliant devices to access the services.</span></span> <span data-ttu-id="60623-114">如需詳細資訊，請參閱 Office 365 服務的條件式存取裝置原則。</span><span class="sxs-lookup"><span data-stu-id="60623-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="60623-115">**內部部署環境裝載之應用程式的條件式存取：**您可以使用已註冊的裝置搭配適用於已設定為使用 Windows Server 2012 R2 AD FS 之應用程式的存取原則。</span><span class="sxs-lookup"><span data-stu-id="60623-115">**Conditional access to applications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured to use AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="60623-116">如需有關設定內部部署之條件式存取的詳細資訊，請參閱[使用 Azure Active Directory 裝置註冊設定內部部署條件式存取](active-directory-device-registration-on-premises-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="60623-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="60623-117">設定 Azure Active Directory 裝置註冊</span><span class="sxs-lookup"><span data-stu-id="60623-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="60623-118">若要設定裝置註冊，您有多個選項：</span><span class="sxs-lookup"><span data-stu-id="60623-118">To setup device registration, you have multiple options:</span></span>

- <span data-ttu-id="60623-119">裝置可以在加入 Azure AD 網域時註冊。</span><span class="sxs-lookup"><span data-stu-id="60623-119">Devices can register when joined to Azure AD domain.</span></span> <span data-ttu-id="60623-120">如需有關此主題的詳細資訊，您可以深入了解 Azure AD 加入與讓使用者加入 Azure AD 網域所需的設定。</span><span class="sxs-lookup"><span data-stu-id="60623-120">For more on this topic, you can Learn more about Azure AD Join and the settings required for users to join Azure AD domain.</span></span>

- <span data-ttu-id="60623-121">裝置可以在使用者在個人裝置上新增公司或學校帳戶到 Windows 或在行動裝置連線到需要註冊的公司資源時註冊。</span><span class="sxs-lookup"><span data-stu-id="60623-121">Devices can be registered when users add work or school accounts to Windows on a personal device or when mobile devices connect to a work resources requiring registration.</span></span> <span data-ttu-id="60623-122">若要確保此行為，您必須在 Azure 入口網站中啟用 Azure AD 裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="60623-122">To ensure this, you must enable Azure AD Device Registration in the Azure Portal.</span></span> 

- <span data-ttu-id="60623-123">裝置可以針對已加入網域的傳統電腦使用自動裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="60623-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="60623-124">為確保此行為，您必須先設定 Azure AD Connect，才能進行自動裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="60623-124">To ensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="60623-125">如需最新的指示，請參閱[如何設定讓已加入網域的 Windows 裝置自動向 Azure Active Directory 註冊](active-directory-conditional-access-automatic-device-registration-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="60623-125">For latest instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="60623-126">您也可以使用 Azure Active Directory 中的「系統管理員入口網站」來檢視及啟用/停用已註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="60623-126">You can also review and enable or disable registered devices using the Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-the-azure-active-directory-device-registration-service"></a><span data-ttu-id="60623-127">啟用 Azure Active Directory 裝置註冊服務</span><span class="sxs-lookup"><span data-stu-id="60623-127">Enable the Azure Active Directory device registration service</span></span>

<span data-ttu-id="60623-128">**啟用 Azure Active Directory 裝置註冊服務：**</span><span class="sxs-lookup"><span data-stu-id="60623-128">**To enable the Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="60623-129">以系統管理員身分登入 Microsoft Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="60623-129">Sign in to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="60623-130">在左窗格中選取 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="60623-130">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="60623-131">在 [目錄] 索引標籤中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="60623-131">On the Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="60623-132">按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="60623-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="60623-133">捲動到 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="60623-133">Scroll to **Devices**.</span></span>

6.  <span data-ttu-id="60623-134">針對 [使用者可以向 Azure AD 註冊其裝置] 選取 [全部]。</span><span class="sxs-lookup"><span data-stu-id="60623-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="60623-135">選取您要依每位使用者授權的裝置數目上限。</span><span class="sxs-lookup"><span data-stu-id="60623-135">Select the maximum number of devices you want to authorize per user.</span></span>

<span data-ttu-id="60623-136">Microsoft Intune 註冊或 Office 365 的行動裝置管理要求必須執行裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="60623-136">The enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="60623-137">如果您已設定任一服務，則會選取 [全部] 並停用 [無]。</span><span class="sxs-lookup"><span data-stu-id="60623-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="60623-138">請確定已正確設定它們，而且它們有適當的授權。</span><span class="sxs-lookup"><span data-stu-id="60623-138">Please ensure that they are configured correctly and have the appropriate licensing.</span></span>

<span data-ttu-id="60623-139">根據預設，服務未啟用雙因素驗證。</span><span class="sxs-lookup"><span data-stu-id="60623-139">By default, two-factor authentication is not enabled for the service.</span></span> <span data-ttu-id="60623-140">不過，建議在註冊裝置時使用雙因素驗證。</span><span class="sxs-lookup"><span data-stu-id="60623-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="60623-141">在要求此服務的雙因素驗證之前，您必須先在 Azure Active Directory 中設定雙因素驗證提供者以及針對 Multi-Factor Authentication 設定您的使用者帳戶，請參閱將 Multi-Factor Authentication 新增至 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60623-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication to Azure Active Directory</span></span>

- <span data-ttu-id="60623-142">如果您搭配使用 AD FS 與 Windows Server 2012 R2，則必須在 AD FS 中設定雙因素驗證模組，請參閱＜搭配使用 Multi-Factor Authentication 與 Active Directory 同盟服務＞。</span><span class="sxs-lookup"><span data-stu-id="60623-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="60623-143">在 Azure Active Directory 中檢視和管理裝置物件</span><span class="sxs-lookup"><span data-stu-id="60623-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="60623-144">從 Azure 系統管理員入口網站，您可以檢視、封鎖和解除封鎖裝置。</span><span class="sxs-lookup"><span data-stu-id="60623-144">From the Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="60623-145">已封鎖的裝置將無法再存取已設為僅允許已註冊裝置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="60623-145">A device that is blocked will no longer have access to applications that are configured to allow only registered devices.</span></span>

<span data-ttu-id="60623-146">**在 Azure Active Directory 中檢視及管理裝置物件：**</span><span class="sxs-lookup"><span data-stu-id="60623-146">**To view and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="60623-147">以系統管理員身分登入 Microsoft Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="60623-147">Log on to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="60623-148">在左窗格中選取 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="60623-148">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="60623-149">選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="60623-149">Select your directory.</span></span>

4.  <span data-ttu-id="60623-150">選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="60623-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="60623-151">按一下您要查看其裝置的使用者。</span><span class="sxs-lookup"><span data-stu-id="60623-151">Click the user for which you want to see the devices.</span></span>

6.  <span data-ttu-id="60623-152">選取 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="60623-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="60623-153">選取 [註冊的裝置]。</span><span class="sxs-lookup"><span data-stu-id="60623-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="60623-154">現在您可以檢閱、封鎖或解除封鎖使用者已註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="60623-154">Now, you can review, block, or unblock the user's registered devices.</span></span>
<span data-ttu-id="60623-155">已加入內部部署網域且已自動註冊的 Windows 10 裝置不會出現在 [使用者] 索引標籤下。</span><span class="sxs-lookup"><span data-stu-id="60623-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under the Users tab.</span></span> <span data-ttu-id="60623-156">請使用 Get-MsolDevice PowerShell 命令來尋找您的所有企業裝置。</span><span class="sxs-lookup"><span data-stu-id="60623-156">Please use the Get-MsolDevice PowerShell command to find all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="60623-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="60623-157">Next steps</span></span>

<span data-ttu-id="60623-158">若要設定自動裝置註冊，請參閱[如何設定讓已加入網域的 Windows 裝置自動向 Azure Active Directory 註冊](active-directory-conditional-access-automatic-device-registration-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="60623-158">To setup automated device registration, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


