---
title: "Azure Active Directory 裝置註冊概觀 | Microsoft Docs"
description: "Azure Active Directory 裝置註冊是裝置型條件式存取案例的基礎。 註冊裝置時，Azure Active Directory 裝置註冊會利用當使用者登入時用來驗證裝置的身分識別來佈建裝置。"
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
ms.openlocfilehash: 9f8605d65a3852b85a8682ca74fdf99bc785db5b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="0eb74-105">開始使用 Azure Active Directory 裝置註冊</span><span class="sxs-lookup"><span data-stu-id="0eb74-105">Get started with Azure Active Directory device registration</span></span>
<span data-ttu-id="0eb74-106">Azure Active Directory 裝置註冊是裝置型條件式存取案例的基礎。</span><span class="sxs-lookup"><span data-stu-id="0eb74-106">Azure Active Directory device registration is the foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="0eb74-107">當裝置已註冊時，Azure Active Directory 裝置註冊會在使用者登入時為裝置提供用來驗證裝置的身分識別。</span><span class="sxs-lookup"><span data-stu-id="0eb74-107">When a device is registered, Azure Active Directory device registration provides the device with an identity which is used to authenticate the device when the user signs in.</span></span> <span data-ttu-id="0eb74-108">然後已驗證的裝置和裝置的屬性即可用來對裝載於雲端和內部部署的應用程式，強制執行條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="0eb74-108">The authenticated device, and the attributes of the device, can then be used to enforce conditional access policies for applications that are hosted in the cloud and on-premises.</span></span>

<span data-ttu-id="0eb74-109">與 Microsoft Intune 這類的行動裝置管理 (MDM) 解決方案結合時，將會以裝置的其他相關資訊更新 Azure Active Directory 中的裝置屬性。</span><span class="sxs-lookup"><span data-stu-id="0eb74-109">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure Active Directory are updated with additional information about the device.</span></span> <span data-ttu-id="0eb74-110">這可讓您建立條件式存取規則，強制讓裝置的存取符合您的安全性和相容性標準。</span><span class="sxs-lookup"><span data-stu-id="0eb74-110">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span> <span data-ttu-id="0eb74-111">如需如何在 Microsoft Intune 中註冊裝置的詳細資訊，請參閱 [在 Intune 中註冊要管理的裝置](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)。</span><span class="sxs-lookup"><span data-stu-id="0eb74-111">For more information on enrolling devices in Microsoft Intune, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span>

## <a name="scenarios-enabled-by-azure-active-directory-device-registration"></a><span data-ttu-id="0eb74-112">Azure Active Directory 裝置註冊所啟用的案例</span><span class="sxs-lookup"><span data-stu-id="0eb74-112">Scenarios enabled by Azure Active Directory device registration</span></span>
<span data-ttu-id="0eb74-113">Azure Active Directory 裝置註冊可支援 iOS、Android 和 Windows 裝置。</span><span class="sxs-lookup"><span data-stu-id="0eb74-113">Azure Active Directory device registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="0eb74-114">利用 Azure AD 裝置註冊的個別案例可能會有更明確的需求和平台支援。</span><span class="sxs-lookup"><span data-stu-id="0eb74-114">The individual scenarios that utilize Azure AD device registration may have more specific requirements and platform support.</span></span> <span data-ttu-id="0eb74-115">這些案例如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0eb74-115">These scenarios are as follows:</span></span>

* <span data-ttu-id="0eb74-116">**內部部署託管之應用程式的條件式存取**：您可以使用已註冊的裝置，搭配適用於已設定為使用 AD FS with Windows Server 2012 R2 之應用程式的存取原則。</span><span class="sxs-lookup"><span data-stu-id="0eb74-116">**Conditional access to applications that are hosted on-premises**: You can use registered devices with access policies for applications that are configured to use AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="0eb74-117">如需有關設定內部部署之條件式存取的詳細資訊，請參閱[使用 Azure Active Directory 裝置註冊設定內部部署條件式存取](active-directory-device-registration-on-premises-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="0eb74-117">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>
* <span data-ttu-id="0eb74-118">**適用於包含 Microsoft Intune 的 Office 365 應用程式條件式存取** ︰IT 管理員可以佈建條件式存取裝置原則來保護公司資源，同時允許相容裝置上的資訊工作者存取服務。</span><span class="sxs-lookup"><span data-stu-id="0eb74-118">**Conditional access for Office 365 applications with Microsoft Intune** : IT admins can provision conditional access device policies to secure corporate resources, while at the same time allowing information workers on compliant devices to access the services.</span></span> <span data-ttu-id="0eb74-119">如需詳細資訊，請參閱 [Office 365 服務的條件式存取裝置原則](active-directory-conditional-access-device-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="0eb74-119">For more information, see [Conditional Access Device Policies for Office 365 services](active-directory-conditional-access-device-policies.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="0eb74-120">設定 Azure Active Directory 裝置註冊</span><span class="sxs-lookup"><span data-stu-id="0eb74-120">Setting up Azure Active Directory device registration</span></span>
<span data-ttu-id="0eb74-121">您必須在 Azure 入口網站啟用 Azure AD 裝置註冊，讓行動裝置可以透過尋找知名的 DNS 記錄來探索服務。</span><span class="sxs-lookup"><span data-stu-id="0eb74-121">You need to enable Azure AD device registration in the Azure Portal so that mobile devices  can discover the service by looking for well-known DNS records.</span></span> <span data-ttu-id="0eb74-122">您必須設定公司 DNS，讓 Windows 10、Windows 8.1、Windows 7、Android 和 iOS 裝置可以探索和使用服務。</span><span class="sxs-lookup"><span data-stu-id="0eb74-122">You must configure your company DNS so that Windows 10, Windows 8.1, Windows 7, Android and iOS devices can discover and use the service.</span></span>
<span data-ttu-id="0eb74-123">您可以使用 Azure Active Directory 中的系統管理員入口網站，檢視並啟用/停用已註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="0eb74-123">You can view and enable/disable registered devices using the Administrator Portal in Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="0eb74-124">如需有關如何設定自動裝置註冊的最新指示，請參閱 [如何設定讓已加入網域的 Windows 裝置自動向 Azure Active Directory 註冊](active-directory-conditional-access-automatic-device-registration-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="0eb74-124">For latest instructions on how to set up automatic device registration see, [How to setup automatic registration of Windows domain joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>
> 
> 

### <a name="enable-azure-active-directory-device-registration-service"></a><span data-ttu-id="0eb74-125">啟用 Azure Active Directory 裝置註冊服務</span><span class="sxs-lookup"><span data-stu-id="0eb74-125">Enable Azure Active Directory device registration Service</span></span>
1. <span data-ttu-id="0eb74-126">以系統管理員身分登入 Microsoft Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0eb74-126">Sign in to the Microsoft Azure portal as Administrator.</span></span>
2. <span data-ttu-id="0eb74-127">在左窗格中選取 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="0eb74-127">On the left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="0eb74-128">在 [目錄]  索引標籤中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="0eb74-128">On the **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="0eb74-129">選取 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0eb74-129">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="0eb74-130">捲動至名為[裝置] 的區段。</span><span class="sxs-lookup"><span data-stu-id="0eb74-130">Scroll to the section called **Devices**.</span></span>
6. <span data-ttu-id="0eb74-131">針對 [使用者可以使用「加入工作場所」裝置] 選取 [全部]。</span><span class="sxs-lookup"><span data-stu-id="0eb74-131">Select **ALL** for **USERS MAY WORKPLACE JOIN DEVICES**.</span></span>
7. <span data-ttu-id="0eb74-132">選取您要依每位使用者授權的裝置數目上限。</span><span class="sxs-lookup"><span data-stu-id="0eb74-132">Select the maximum number of devices you want to authorize per user.</span></span>

> [!NOTE]
> <span data-ttu-id="0eb74-133">Microsoft Intune 註冊或 Office 365 的行動裝置管理需要加入工作場所。</span><span class="sxs-lookup"><span data-stu-id="0eb74-133">Enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires Workplace Join.</span></span> <span data-ttu-id="0eb74-134">如果您已設定任一項服務，則會選取 [全部] 並停用 [無] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0eb74-134">If you have configured either of these services, ALL is selected and the NONE button is disabled.</span></span>
> 
> 

<span data-ttu-id="0eb74-135">根據預設，服務未啟用雙因素驗證。</span><span class="sxs-lookup"><span data-stu-id="0eb74-135">By default, two-factor authentication is not enabled for the service.</span></span> <span data-ttu-id="0eb74-136">不過，建議在註冊裝置時使用雙因素驗證。</span><span class="sxs-lookup"><span data-stu-id="0eb74-136">However, two-factor authentication is recommended when registering a device.</span></span>

* <span data-ttu-id="0eb74-137">在要求此服務的雙因素驗證之前，您必須先在 Azure Active Directory 中設定雙因素驗證提供者，並針對 Multi-Factor Authentication 設定您的使用者帳戶，請參閱 [將 Multi-Factor Authentication 新增至 Azure Active Directory](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="0eb74-137">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see [Adding Multi-Factor Authentication to Azure Active Directory](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span></span>
* <span data-ttu-id="0eb74-138">如果您搭配使用 AD FS 與 Windows Server 2012 R2，則必須在 AD FS 中設定雙因素驗證模組，請參閱 [搭配使用 Multi-Factor Authentication 與 Active Directory Federation Services](../multi-factor-authentication/multi-factor-authentication-get-started-server.md)。</span><span class="sxs-lookup"><span data-stu-id="0eb74-138">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see [Using Multi-Factor Authentication with Active Directory Federation Services](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).</span></span>

## <a name="configure-azure-active-directory-device-registration-discovery"></a><span data-ttu-id="0eb74-139">設定 Azure Active Directory 裝置註冊探索</span><span class="sxs-lookup"><span data-stu-id="0eb74-139">Configure Azure Active Directory device registration discovery</span></span>
<span data-ttu-id="0eb74-140">Windows 7 和 Windows 8.1 裝置會藉由結合使用者帳戶名稱與知名裝置註冊伺服器名稱，探索裝置註冊服務。</span><span class="sxs-lookup"><span data-stu-id="0eb74-140">Windows 7 and Windows 8.1 devices will discover the device registration service by combining the user account name with a well-known device registration server name.</span></span>

<span data-ttu-id="0eb74-141">您必須建立 DNS CNAME 記錄，該記錄指向與您 Azure Active Directory 裝置註冊服務相關聯的 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="0eb74-141">You must create a DNS CNAME record that points to the A record associated with your Azure Active Directory device registration service.</span></span> <span data-ttu-id="0eb74-142">CNAME 記錄必須使用知名的前置詞 enterpriseregistration，其後面接著貴組織的使用者帳戶所使用的 UPN 尾碼。</span><span class="sxs-lookup"><span data-stu-id="0eb74-142">The CNAME record must use the well-known prefix enterpriseregistration followed by the UPN suffix used by the user accounts at your organization.</span></span> <span data-ttu-id="0eb74-143">如果您的組織使用多個 UPN 尾碼，則必須在 DNS 中建立多個 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="0eb74-143">If your organization uses multiple UPN suffixes, multiple CNAME records must be created in DNS.</span></span>

<span data-ttu-id="0eb74-144">例如，如果您在貴組織使用兩個名為 @contoso.com 和 @region.contoso.com 的 UPN 尾碼，您將建立下列 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="0eb74-144">For example, if you use two UPN suffixes at your organization named @contoso.com and @region.contoso.com, you will create the following DNS records.</span></span>

| <span data-ttu-id="0eb74-145">項目</span><span class="sxs-lookup"><span data-stu-id="0eb74-145">Entry</span></span> | <span data-ttu-id="0eb74-146">類型</span><span class="sxs-lookup"><span data-stu-id="0eb74-146">Type</span></span> | <span data-ttu-id="0eb74-147">位址</span><span class="sxs-lookup"><span data-stu-id="0eb74-147">Address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0eb74-148">enterpriseregistration.contoso.com</span><span class="sxs-lookup"><span data-stu-id="0eb74-148">enterpriseregistration.contoso.com</span></span> |<span data-ttu-id="0eb74-149">CNAME</span><span class="sxs-lookup"><span data-stu-id="0eb74-149">CNAME</span></span> |<span data-ttu-id="0eb74-150">enterpriseregistration.windows.net</span><span class="sxs-lookup"><span data-stu-id="0eb74-150">enterpriseregistration.windows.net</span></span> |
| <span data-ttu-id="0eb74-151">enterpriseregistration.region.contoso.com</span><span class="sxs-lookup"><span data-stu-id="0eb74-151">enterpriseregistration.region.contoso.com</span></span> |<span data-ttu-id="0eb74-152">CNAME</span><span class="sxs-lookup"><span data-stu-id="0eb74-152">CNAME</span></span> |<span data-ttu-id="0eb74-153">enterpriseregistration.windows.net</span><span class="sxs-lookup"><span data-stu-id="0eb74-153">enterpriseregistration.windows.net</span></span> |

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="0eb74-154">在 Azure Active Directory 中檢視和管理裝置物件</span><span class="sxs-lookup"><span data-stu-id="0eb74-154">View and manage device objects in Azure Active Directory</span></span>
1. <span data-ttu-id="0eb74-155">從 Azure 系統管理員入口網站，您可以檢視、封鎖和解除封鎖裝置。</span><span class="sxs-lookup"><span data-stu-id="0eb74-155">From the Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="0eb74-156">已封鎖的裝置將無法再存取已設為僅允許已註冊裝置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0eb74-156">A device that is blocked will no longer have access to applications that are configured to allow only registered devices.</span></span>
2. <span data-ttu-id="0eb74-157">以系統管理員身分登入 Microsoft Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0eb74-157">Log on to the Microsoft Azure Portal as Administrator.</span></span>
3. <span data-ttu-id="0eb74-158">在左窗格中選取 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="0eb74-158">On the left pane, select **Active Directory**.</span></span>
4. <span data-ttu-id="0eb74-159">選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="0eb74-159">Select your directory.</span></span>
5. <span data-ttu-id="0eb74-160">選取 [使用者]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0eb74-160">Select the **Users** tab.</span></span> <span data-ttu-id="0eb74-161">然後選取使用者以檢視其裝置。</span><span class="sxs-lookup"><span data-stu-id="0eb74-161">Then select a user to view their devices</span></span>
6. <span data-ttu-id="0eb74-162">選取 [裝置]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0eb74-162">Select the **Devices** tab.</span></span>
7. <span data-ttu-id="0eb74-163">從下拉式功能表中選取 [已註冊的裝置]  。</span><span class="sxs-lookup"><span data-stu-id="0eb74-163">Select **Registered Devices** from the drop down menu.</span></span>
8. <span data-ttu-id="0eb74-164">您可以在此檢視、封鎖或解除封鎖使用者已註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="0eb74-164">Here you can view, block, or unblock the users registered devices.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="0eb74-165">其他主題</span><span class="sxs-lookup"><span data-stu-id="0eb74-165">Additional topics</span></span>
<span data-ttu-id="0eb74-166">您可以向 Azure AD 裝置註冊註冊 Windows 7 和 Windows 8.1 加入網域的裝置。</span><span class="sxs-lookup"><span data-stu-id="0eb74-166">You can register your Windows 7 and Windows 8.1 Domain Joined devices with Azure AD device registration.</span></span> <span data-ttu-id="0eb74-167">下列主題提供有關在 Windows 7 和 Windows 8.1 裝置上設定裝置註冊所需之先決條件和步驟的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0eb74-167">The following topics provides more information about the prerequisites and the steps required to configure device registration on Windows 7 and Windows 8.1 devices.</span></span>

* [<span data-ttu-id="0eb74-168">自動向 Azure Active Directory 註冊加入網域的 Windows 裝置</span><span class="sxs-lookup"><span data-stu-id="0eb74-168">Automatic device registration with Azure Active Directory for Windows Domain-Joined Devices</span></span>](active-directory-conditional-access-automatic-device-registration.md)
* [<span data-ttu-id="0eb74-169">自動向 Azure Active Directory 註冊加入網域的 Windows 10 裝置</span><span class="sxs-lookup"><span data-stu-id="0eb74-169">Automatic device registration with Azure Active Directory for Windows 10 domain-joined devices</span></span>](active-directory-azureadjoin-devices-group-policy.md)

