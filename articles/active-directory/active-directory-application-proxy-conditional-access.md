---
title: "條件式存取內部部署應用程式 - Azure AD | Microsoft Docs"
description: "說明如何針對您使用 Azure AD 應用程式 Proxy 發佈可供遠端存取的應用程式設定條件式存取。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2e97722b-eb4e-4078-b607-9fed210d8a0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 463946256f9e335fa6d98fc904835e5c3dc2725e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-conditional-access-in-azure-ad-application-proxy"></a><span data-ttu-id="fcdba-103">使用 Azure AD 應用程式 Proxy 中的條件式存取</span><span class="sxs-lookup"><span data-stu-id="fcdba-103">Working with conditional access in Azure AD Application Proxy</span></span>

>[!NOTE]
><span data-ttu-id="fcdba-104">本文適用於 Azure 傳統入口網站 (即將淘汰)。</span><span class="sxs-lookup"><span data-stu-id="fcdba-104">This article applies to the Azure classic portal, which is being retired.</span></span> <span data-ttu-id="fcdba-105">建議您使用 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="fcdba-105">We recommend that you use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fcdba-106">在 Azure 入口網站中，應用程式 Proxy 應用程式具有與任何其他 SaaS 應用程式相同的條件式式存取功能。</span><span class="sxs-lookup"><span data-stu-id="fcdba-106">In the Azure portal, Application Proxy apps have the same conditional access features as any other SaaS app.</span></span> <span data-ttu-id="fcdba-107">若要深入了解條件式存取，請參閱[開始使用 Azure Active Directory 中的條件式存取](active-directory-conditional-access-azure-portal-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="fcdba-107">To learn more about conditional access, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>

<span data-ttu-id="fcdba-108">對於使用應用程式 Proxy 發佈的應用程式，您可以設定存取規則，以授與對這些應用程式的條件式存取。</span><span class="sxs-lookup"><span data-stu-id="fcdba-108">You can configure access rules to grant conditional access to applications published using Application Proxy.</span></span> <span data-ttu-id="fcdba-109">這可讓您：</span><span class="sxs-lookup"><span data-stu-id="fcdba-109">This enables you to:</span></span>

* <span data-ttu-id="fcdba-110">要求各應用程式的多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="fcdba-110">Require multi-factor authentication per application</span></span>
* <span data-ttu-id="fcdba-111">只在使用者不在公司時要求多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="fcdba-111">Require multi-factor authentication only when users are not at work</span></span>
* <span data-ttu-id="fcdba-112">在使用者不在公司時封鎖使用者存取應用程式</span><span class="sxs-lookup"><span data-stu-id="fcdba-112">Block users from accessing the application when they are not at work</span></span>

<span data-ttu-id="fcdba-113">這些規則可以套用至所有使用者和群組，或只套用至特定使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="fcdba-113">These rules can be applied to all users and groups or only to specific users and groups.</span></span> <span data-ttu-id="fcdba-114">根據預設，規則會套用至所有可存取應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="fcdba-114">By default the rule applies to all users who have access to the application.</span></span> <span data-ttu-id="fcdba-115">不過，也可以將規則限制為指定之安全性群組的使用者成員。</span><span class="sxs-lookup"><span data-stu-id="fcdba-115">However the rule can also be restricted to users that are members of specified security groups.</span></span>  

<span data-ttu-id="fcdba-116">當使用者存取使用 OAuth 2.0、OpenID Connect、SAML 或 WS-同盟的同盟應用程式時，就會評估存取規則。</span><span class="sxs-lookup"><span data-stu-id="fcdba-116">Access rules are evaluated when a user accesses a federated application that uses OAuth 2.0, OpenID Connect, SAML, or WS-Federation.</span></span> <span data-ttu-id="fcdba-117">此外，當使用重新整理權杖來取得存取權杖時，會以 OAuth 2.0 和 OpenID Connect 評估存取規則。</span><span class="sxs-lookup"><span data-stu-id="fcdba-117">In addition, access rules are evaluated with OAuth 2.0 and OpenID Connect when a refresh token is used to acquire an access token.</span></span>

## <a name="conditional-access-prerequisites"></a><span data-ttu-id="fcdba-118">條件式存取的先決條件</span><span class="sxs-lookup"><span data-stu-id="fcdba-118">Conditional access prerequisites</span></span>
* <span data-ttu-id="fcdba-119">Azure Active Directory Premium 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fcdba-119">Subscription to Azure Active Directory Premium</span></span>
* <span data-ttu-id="fcdba-120">同盟或受管理的 Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="fcdba-120">A federated or managed Azure Active Directory tenant</span></span>
* <span data-ttu-id="fcdba-121">同盟租用戶需要 Multi-Factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="fcdba-121">Federated tenants require multi-factor authentication (MFA)</span></span>  
    ![設定存取規則 - 要求 Multi-Factor Authentication](./media/active-directory-application-proxy-conditional-access/application-proxy-conditional-access.png)

## <a name="configure-per-application-multi-factor-authentication"></a><span data-ttu-id="fcdba-123">設定每個應用程式的 Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="fcdba-123">Configure per-application multi-factor authentication</span></span>
1. <span data-ttu-id="fcdba-124">在 Azure 傳統入口網站中，以系統管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="fcdba-124">Sign in as an administrator in the Azure classic portal.</span></span>
2. <span data-ttu-id="fcdba-125">移至 Active Directory，並選取您要啟用應用程式 Proxy 所在的目錄。</span><span class="sxs-lookup"><span data-stu-id="fcdba-125">Go to Active Directory and select the directory in which you want to enable Application Proxy.</span></span>
3. <span data-ttu-id="fcdba-126">按一下 [應用程式] 並向下捲動至 [存取規則] 區段。</span><span class="sxs-lookup"><span data-stu-id="fcdba-126">Click **Applications** and scroll down to the **Access Rules** section.</span></span> <span data-ttu-id="fcdba-127">只有使用應用程式 Proxy 發佈並使用同盟驗證的應用程式，才會顯示 [存取規則] 區段。</span><span class="sxs-lookup"><span data-stu-id="fcdba-127">The access rules section only appears for applications published using Application Proxy that use federated authentication.</span></span>
4. <span data-ttu-id="fcdba-128">為 [啟用存取規則] 選取 [開啟] 來啟用規則。</span><span class="sxs-lookup"><span data-stu-id="fcdba-128">Enable the rule by selecting **Enable Access Rules** to **On**.</span></span>
5. <span data-ttu-id="fcdba-129">指定要套用規則的使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="fcdba-129">Specify the users and groups to whom the rules apply.</span></span> <span data-ttu-id="fcdba-130">使用 [新增群組] 按鈕來選取一或多個要套用存取規則的群組。</span><span class="sxs-lookup"><span data-stu-id="fcdba-130">Use the **Add Group** button to select one or more groups to which the access rule applies.</span></span> <span data-ttu-id="fcdba-131">此對話方塊也可用來移除選取的群組。</span><span class="sxs-lookup"><span data-stu-id="fcdba-131">This dialog can also be used to remove selected groups.</span></span>  <span data-ttu-id="fcdba-132">選取要套用至群組的規則之後，只會對屬於其中一個指定安全性群組的使用者強制執行存取規則。</span><span class="sxs-lookup"><span data-stu-id="fcdba-132">When the rules are selected to apply to groups, the access rules are enforced only for users that belong to one of the specified security groups.</span></span>  

   * <span data-ttu-id="fcdba-133">若要明確地將安全性群組從規則中排除，請選取 [例外]  並指定一或多個群組。</span><span class="sxs-lookup"><span data-stu-id="fcdba-133">To explicitly exclude security groups from the rule, check **Except** and specify one or more groups.</span></span> <span data-ttu-id="fcdba-134">如果使用者是 [除外] 清單中某個群組的成員，則不需要執行多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="fcdba-134">Users who are members of a group in the Except list are not required to perform multi-factor authentication.</span></span>  
   * <span data-ttu-id="fcdba-135">如果已使用每個使用者的多重要素驗證功能來設定使用者，則此設定會優先於應用程式的多重要素驗證規則。</span><span class="sxs-lookup"><span data-stu-id="fcdba-135">If a user was configured using the per-user multi-factor authentication feature, this setting takes precedence over the application multi-factor authentication rules.</span></span> <span data-ttu-id="fcdba-136">如果使用者已設定為使用每個使用者的多重要素驗證，則必須執行多重要素驗證，即使已從應用程式的多重要素驗證規則中免除他們也一樣。</span><span class="sxs-lookup"><span data-stu-id="fcdba-136">A user who has been configured for per-user multi-factor authentication is required to perform multi-factor authentication even if they have been exempted from the application's multi-factor authentication rules.</span></span> <span data-ttu-id="fcdba-137">深入了解 [多重要素驗證和每個使用者設定](../multi-factor-authentication/multi-factor-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="fcdba-137">Learn more about [multi-factor authentication and per-user settings](../multi-factor-authentication/multi-factor-authentication.md).</span></span>
6. <span data-ttu-id="fcdba-138">選取您要設定的存取規則：</span><span class="sxs-lookup"><span data-stu-id="fcdba-138">Select the access rule you want to set:</span></span>

   * <span data-ttu-id="fcdba-139">**需要多重要素驗證**︰套用存取規則的使用者必須先完成多重要素驗證，才能存取套用規則的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcdba-139">**Require Multi-factor authentication**: Users to whom access rules apply are required to complete multi-factor authentication before accessing the application to which the rule applies.</span></span>
   * <span data-ttu-id="fcdba-140">**不在工作時需要多重要素驗證**︰嘗試從受信任的 IP 位址存取應用程式的使用者不需要執行多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="fcdba-140">**Require Multi-factor authentication when not at work**: Users trying to access the application from a trusted IP address will not be required to perform multi-factor authentication.</span></span> <span data-ttu-id="fcdba-141">可以在 [Multi-Factor Authentication 設定] 頁面上設定受信任的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="fcdba-141">The trusted IP address ranges can be configured on the multi-factor authentication settings page.</span></span>
   * <span data-ttu-id="fcdba-142">**不在工作時封鎖存取**︰嘗試從公司網路外部存取應用程式的使用者將無法存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcdba-142">**Block access when not at work**: Users trying to access the application from outside your corporate network will not be able to access the application.</span></span>

## <a name="configuring-mfa-for-federation-services"></a><span data-ttu-id="fcdba-143">設定同盟服務的 MFA</span><span class="sxs-lookup"><span data-stu-id="fcdba-143">Configuring MFA for federation services</span></span>
<span data-ttu-id="fcdba-144">對於同盟的租用戶，Multi-Factor Authentication (MFA) 可能由 Azure Active Directory 或內部部署 AD FS 伺服器執行。</span><span class="sxs-lookup"><span data-stu-id="fcdba-144">For federated tenants, multi-factor authentication (MFA) may be performed by Azure Active Directory or by the on-premises AD FS server.</span></span> <span data-ttu-id="fcdba-145">根據預設，MFA 會發生在 Azure Active Directory 所裝載的任何頁面上。</span><span class="sxs-lookup"><span data-stu-id="fcdba-145">By default, MFA occurs on any page hosted by Azure Active Directory.</span></span> <span data-ttu-id="fcdba-146">若要設定內部部署 MFA，請執行 Windows PowerShell 並使用 –SupportsMFA 屬性來設定 Azure AD 模組。</span><span class="sxs-lookup"><span data-stu-id="fcdba-146">To configure MFA on-premises, run Windows PowerShell and use the –SupportsMFA property to set the Azure AD module.</span></span>

<span data-ttu-id="fcdba-147">下列範例示範如何在 consoso.com 租用戶上使用 [Set-MsolDomainFederationSettings Cmdlet](https://msdn.microsoft.com/library/azure/dn194088.aspx) 來啟用內部部署 MFA︰`Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true `</span><span class="sxs-lookup"><span data-stu-id="fcdba-147">The following example shows how to enable on-premises MFA by using the [Set-MsolDomainFederationSettings cmdlet](https://msdn.microsoft.com/library/azure/dn194088.aspx) on the contoso.com tenant: `Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true `</span></span>

<span data-ttu-id="fcdba-148">除了設定這個旗標，同盟租用戶 AD FS 執行個體必須設為執行多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="fcdba-148">In addition to setting this flag, the federated tenant AD FS instance must be configured to perform multi-factor authentication.</span></span> <span data-ttu-id="fcdba-149">請遵循 [內部部署 Microsoft Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-server.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="fcdba-149">Follow the instructions for [deploying Microsoft Azure multi-factor authentication on-premises](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="fcdba-150">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fcdba-150">See also</span></span>
* [<span data-ttu-id="fcdba-151">使用宣告感知應用程式</span><span class="sxs-lookup"><span data-stu-id="fcdba-151">Working with claims aware applications</span></span>](active-directory-application-proxy-claims-aware-apps.md)
* [<span data-ttu-id="fcdba-152">使用應用程式 Proxy 發行應用程式</span><span class="sxs-lookup"><span data-stu-id="fcdba-152">Publish applications with Application Proxy</span></span>](active-directory-application-proxy-publish.md)
* [<span data-ttu-id="fcdba-153">啟用單一登入</span><span class="sxs-lookup"><span data-stu-id="fcdba-153">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="fcdba-154">使用您自己的網域名稱發行應用程式</span><span class="sxs-lookup"><span data-stu-id="fcdba-154">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)

<span data-ttu-id="fcdba-155">如需最新消息，請查閱 [應用程式 Proxy 部落格](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="fcdba-155">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
