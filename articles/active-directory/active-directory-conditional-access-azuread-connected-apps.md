---
title: "aaaAzure SaaS 應用程式的條件式存取 |Microsoft 文件"
description: "在 Azure AD 中的條件式存取可讓您您 tooconfigure 每個應用程式多因素驗證存取規則和 hello 能力 tooblock 存取不受信任的網路上的使用者。 "
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 69748014c0c8e266ba66562980c784aba4c68d80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a><span data-ttu-id="9c516-103">開始使用 Azure Active Directory 條件式存取</span><span class="sxs-lookup"><span data-stu-id="9c516-103">Getting started with Azure Active Directory Conditional Access</span></span>
<span data-ttu-id="9c516-104">[SaaS](https://azure.microsoft.com/overview/what-is-saas/) 應用程式及 Azure AD 連線應用程式的「Azure Active Directory 條件式存取」可讓您根據群組、位置和應用程式敏感性來設定條件式存取。</span><span class="sxs-lookup"><span data-stu-id="9c516-104">Azure Active Directory Conditional Access for [SaaS](https://azure.microsoft.com/overview/what-is-saas/) apps and Azure AD connected apps lets you configure conditional access based on group, location, and application sensitivity.</span></span> 

<span data-ttu-id="9c516-105">使用以應用程式敏感性為基礎的條件式存取時，您可以設定每一應用程式的多重要素驗證 (MFA) 存取規則。</span><span class="sxs-lookup"><span data-stu-id="9c516-105">With conditional access based on application sensitivity, you can set multi-factor authentication (MFA) access rules per application.</span></span> <span data-ttu-id="9c516-106">每個應用程式的 MFA 提供 hello 能力 tooblock 存取不受信任的網路上的使用者。</span><span class="sxs-lookup"><span data-stu-id="9c516-106">MFA per application provides hello ability tooblock access for users who are not on a trusted network.</span></span> <span data-ttu-id="9c516-107">您可以套用 MFA 規則 tooall 使用者被指派 toohello 應用程式，或只適用於使用者在指定的安全性群組。</span><span class="sxs-lookup"><span data-stu-id="9c516-107">You can apply MFA rules tooall users that are assigned toohello application, or only for users within specified security groups.</span></span>  <span data-ttu-id="9c516-108">如果它們從 hello 組織的網路內的 IP 位址存取 hello 應用程式，使用者可能會排除從 hello MFA 需求。</span><span class="sxs-lookup"><span data-stu-id="9c516-108">Users may be excluded from hello MFA requirement if they are accessing hello application from an IP address that is inside hello organization’s network.</span></span>

<span data-ttu-id="9c516-109">這些功能將會使用 toocustomers 購買 Azure Active Directory Premium 授權。</span><span class="sxs-lookup"><span data-stu-id="9c516-109">These capabilities will be available toocustomers that have purchased an Azure Active Directory Premium license.</span></span>

## <a name="scenario-prerequisites"></a><span data-ttu-id="9c516-110">案例必要條件</span><span class="sxs-lookup"><span data-stu-id="9c516-110">Scenario prerequisites</span></span>
* <span data-ttu-id="9c516-111">Azure Active Directory Premium 的授權</span><span class="sxs-lookup"><span data-stu-id="9c516-111">License for Azure Active Directory Premium</span></span>
* <span data-ttu-id="9c516-112">同盟或受管理的 Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="9c516-112">Federated or managed Azure Active Directory tenant</span></span>
* <span data-ttu-id="9c516-113">同盟租用戶需要啟用多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="9c516-113">Federated tenants require that multi-factor authentication be enabled.</span></span>

## <a name="configure-per-application-access-rules"></a><span data-ttu-id="9c516-114">設定每個應用程式的存取規則</span><span class="sxs-lookup"><span data-stu-id="9c516-114">Configure per-application access rules</span></span>
<span data-ttu-id="9c516-115">本章節描述如何 tooconfigure 針對應用程式的存取規則。</span><span class="sxs-lookup"><span data-stu-id="9c516-115">This section describes how tooconfigure per-application access rules.</span></span>

1. <span data-ttu-id="9c516-116">登入 toohello 使用 Azure ad 中為全域管理員帳戶的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="9c516-116">Sign in toohello Azure classic portal Using an account that is a global administrator for Azure AD.</span></span>
2. <span data-ttu-id="9c516-117">在 hello 左窗格中，選取  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="9c516-117">On hello left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="9c516-118">Hello 目錄索引標籤上，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="9c516-118">On hello Directory tab, select your directory.</span></span>
4. <span data-ttu-id="9c516-119">選取 hello**應用程式** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9c516-119">Select hello **Applications** tab.</span></span>
5. <span data-ttu-id="9c516-120">選取 hello hello 規則的應用程式將會針對設定。</span><span class="sxs-lookup"><span data-stu-id="9c516-120">Select hello application that hello rule will be set for.</span></span>
6. <span data-ttu-id="9c516-121">選取 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9c516-121">Select hello **Configure** tab.</span></span>
7. <span data-ttu-id="9c516-122">捲動 toohello 存取規則區段。</span><span class="sxs-lookup"><span data-stu-id="9c516-122">Scroll down toohello access rules section.</span></span> <span data-ttu-id="9c516-123">選取 hello 所需的存取規則。</span><span class="sxs-lookup"><span data-stu-id="9c516-123">Select hello desired access rule.</span></span>
8. <span data-ttu-id="9c516-124">指定 hello hello 規則將套用到的使用者。</span><span class="sxs-lookup"><span data-stu-id="9c516-124">Specify hello users hello rule will apply to.</span></span>
9. <span data-ttu-id="9c516-125">選取以啟用 hello 原則**上啟用 toobe**。</span><span class="sxs-lookup"><span data-stu-id="9c516-125">Enable hello policy by selecting **Enabled toobe On**.</span></span>

## <a name="understanding-access-rules"></a><span data-ttu-id="9c516-126">了解存取規則</span><span class="sxs-lookup"><span data-stu-id="9c516-126">Understanding access rules</span></span>
<span data-ttu-id="9c516-127">本節提供支援 hello 條件式應用程式存取 Azure 中的 hello 存取規則的詳細的描述。</span><span class="sxs-lookup"><span data-stu-id="9c516-127">This section gives a detailed description of hello access rules supported in hello Azure Conditional Application Access.</span></span>

### <a name="specifying-hello-users-hello-access-rules-apply-to"></a><span data-ttu-id="9c516-128">指定 hello 使用者 hello 的存取規則會套用到</span><span class="sxs-lookup"><span data-stu-id="9c516-128">Specifying hello users hello access rules apply to</span></span>
<span data-ttu-id="9c516-129">根據預設 hello 原則會套用 tooall 使用者具有存取 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9c516-129">By default hello policy will apply tooall users that have access toohello application.</span></span> <span data-ttu-id="9c516-130">不過，您也可以限制 hello 原則 toousers 成員 hello 指定的安全性群組。</span><span class="sxs-lookup"><span data-stu-id="9c516-130">However, you can also restrict hello policy toousers that are members of hello specified security groups.</span></span> <span data-ttu-id="9c516-131">hello**加入群組**按鈕是使用的 tooselect 其中一個，或從 hello 群組選取項目對話方塊 hello 存取規則的多個群組會套用至。</span><span class="sxs-lookup"><span data-stu-id="9c516-131">hello **Add Group** button is used tooselect one or more groups from hello group selection dialog that hello access rule will apply to.</span></span> <span data-ttu-id="9c516-132">此對話方塊也可以使用的 tooremove 選取群組。</span><span class="sxs-lookup"><span data-stu-id="9c516-132">This dialog can also be used tooremove selected groups.</span></span> <span data-ttu-id="9c516-133">選取的 tooapply tooGroups hello 規則時，hello 存取將只會強制執行規則的使用者屬於 tooone hello 指定的安全性群組。</span><span class="sxs-lookup"><span data-stu-id="9c516-133">When hello rules are selected tooapply tooGroups, hello access rules will only be enforced for users that belong tooone of hello specified security groups.</span></span>

<span data-ttu-id="9c516-134">安全性群組可以也被明確排除 hello 原則選取 hello**除了**選項並指定一個或多個群組。</span><span class="sxs-lookup"><span data-stu-id="9c516-134">Security groups can also be explicitly excluded from hello policy by selecting hello **Except** option and specifying one or more groups.</span></span> <span data-ttu-id="9c516-135">使用者已在 hello 群組的成員**除了**清單不會主旨 toohello 多因素驗證要求，即使它們是群組的成員，hello 套用存取規則。</span><span class="sxs-lookup"><span data-stu-id="9c516-135">Users that are a member of a group in hello **Except** list will not be subject toohello multi-factor authentication requirement, even if they are a member of a group that hello access rule applies to.</span></span>
<span data-ttu-id="9c516-136">存取 hello 應用程式時，如下所示的 hello 存取規則將會需要 hello 管理員群組 toouse 多重要素驗證中的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="9c516-136">hello access rule shown below will require all users in hello Managers group toouse multi-factor authentication when accessing hello application.</span></span>

![使用 MFA 設定條件式存取規則](./media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a><span data-ttu-id="9c516-138">條件式存取規則和 MFA</span><span class="sxs-lookup"><span data-stu-id="9c516-138">Conditional Access Rules with MFA</span></span>
<span data-ttu-id="9c516-139">如果使用者已設定並使用 hello 每位使用者的多重要素驗證功能，這項設定在 hello 使用者會結合 hello 的 hello 應用程式的多因素驗證規則。</span><span class="sxs-lookup"><span data-stu-id="9c516-139">If a user has been configured using hello per-user multi-factor authentication feature, this setting on hello user will combine with hello multi-factor authentication rules of hello app.</span></span> <span data-ttu-id="9c516-140">這表示已針對每個使用者的 multi-factor authentication 的使用者會需要的 tooperform 多重要素驗證，即使它們有 hello 應用程式多因素驗證規則的豁免。</span><span class="sxs-lookup"><span data-stu-id="9c516-140">This means a user that has been configured for per-user multi-factor authentication will be required tooperform multi-factor authentication even if they have been exempted from hello application multi-factor authentication rules.</span></span> <span data-ttu-id="9c516-141">深入了解多重要素驗證和每個使用者設定。</span><span class="sxs-lookup"><span data-stu-id="9c516-141">Learn more about multi-factor authentication and per-user settings.</span></span>

### <a name="access-rule-options"></a><span data-ttu-id="9c516-142">存取規則選項</span><span class="sxs-lookup"><span data-stu-id="9c516-142">Access rule options</span></span>
<span data-ttu-id="9c516-143">支援下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="9c516-143">hello following options are supported:</span></span>

* <span data-ttu-id="9c516-144">**需要多重要素驗證**: hello 使用者 toowhom hello 套用存取規則，都需要的 toocomplete 多重要素驗證，才能存取 hello hello 原則的應用程式適用於。</span><span class="sxs-lookup"><span data-stu-id="9c516-144">**Require multi-factor authentication**: hello users toowhom hello access rules apply to, will be required toocomplete multi-factor authentication before accessing hello application that hello policy applies to.</span></span>
* <span data-ttu-id="9c516-145">**需要多重要素驗證，不在工作時**： 來自受信任的 IP 位址的使用者不會需要的 tooperform 多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="9c516-145">**Require multi-factor authentication when not at work**: A user that is coming from a trusted IP address will not be required tooperform multi-factor authentication.</span></span> <span data-ttu-id="9c516-146">hello 受信任的 IP 位址範圍可以設定 hello 多因素驗證設定 頁面上。</span><span class="sxs-lookup"><span data-stu-id="9c516-146">hello trusted IP address ranges can be configured on hello multi-factor authentication settings page.</span></span>
* <span data-ttu-id="9c516-147">**不工作時封鎖存取**：將會封鎖不是來自受信任 IP 位址的使用者。</span><span class="sxs-lookup"><span data-stu-id="9c516-147">**Block access when not at work**: A user that is not coming from a trusted IP address will be blocked.</span></span> <span data-ttu-id="9c516-148">hello 受信任的 IP 位址範圍可以設定 hello 多因素驗證設定 頁面上。</span><span class="sxs-lookup"><span data-stu-id="9c516-148">hello trusted IP address ranges can be configured on hello multi-factor authentication settings page.</span></span>

### <a name="setting-rule-status"></a><span data-ttu-id="9c516-149">設定規則狀態</span><span class="sxs-lookup"><span data-stu-id="9c516-149">Setting rule status</span></span>
<span data-ttu-id="9c516-150">存取規則狀態可讓您開啟或關閉 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="9c516-150">Access rule status allows turning hello rules on or off.</span></span> <span data-ttu-id="9c516-151">當 hello 關閉存取規則時，不會強制執行 hello 多因素驗證要求。</span><span class="sxs-lookup"><span data-stu-id="9c516-151">When hello access rules are off, hello multi-factor authentication requirement is not enforced.</span></span>

### <a name="access-rule-evaluation"></a><span data-ttu-id="9c516-152">存取規則評估</span><span class="sxs-lookup"><span data-stu-id="9c516-152">Access rule evaluation</span></span>
<span data-ttu-id="9c516-153">當使用者存取使用 OAuth 2.0、OpenID Connect、SAML 或 WS-同盟的同盟應用程式時，就會評估存取規則。</span><span class="sxs-lookup"><span data-stu-id="9c516-153">Access rules are evaluated when a user accesses a federated application that uses OAuth 2.0, OpenID Connect, SAML or WS-Federation.</span></span> <span data-ttu-id="9c516-154">此外，當 hello OAuth 2.0 和 OpenID Connect 使用重新整理語彙基元 tooacquire 存取權杖時，會評估存取規則。</span><span class="sxs-lookup"><span data-stu-id="9c516-154">In addition, access rules are evaluated when hello OAuth 2.0 and OpenID Connect use a refresh token tooacquire an access token.</span></span> <span data-ttu-id="9c516-155">如果原則評估失敗時可使用重新整理語彙基元，hello 錯誤**invalid_grant**便會傳回，這表示 hello 使用者需要 toore-toohello 用戶端進行驗證。</span><span class="sxs-lookup"><span data-stu-id="9c516-155">If policy evaluation fails when a refresh token is used, hello error **invalid_grant** will be returned, this indicates hello user needs toore-authenticate toohello client.</span></span>

### <a name="configure-federation-services-tooprovide-multi-factor-authentication"></a><span data-ttu-id="9c516-156">設定同盟服務 tooprovide 多因素驗證</span><span class="sxs-lookup"><span data-stu-id="9c516-156">Configure federation services tooprovide multi-factor authentication</span></span>
<span data-ttu-id="9c516-157">同盟租用戶，MFA 可能由 Azure Active Directory 或執行 hello 在內部部署 AD FS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9c516-157">For federated tenants, MFA may be performed by Azure Active Directory or by hello on-premises AD FS server.</span></span>

<span data-ttu-id="9c516-158">根據預設，MFA 會發生在 Azure Active Directory 所裝載的頁面上。</span><span class="sxs-lookup"><span data-stu-id="9c516-158">By default, MFA will occur at a page hosted by Azure Active Directory.</span></span> <span data-ttu-id="9c516-159">tooconfigure MFA 內部，hello **– SupportsMFA**屬性必須設定太**true** Azure Active Directory，適用於 Windows PowerShell 使用 hello Azure AD 模組中。</span><span class="sxs-lookup"><span data-stu-id="9c516-159">tooconfigure MFA on-premises, hello **–SupportsMFA** property must be set too**true** in Azure Active Directory, by using hello Azure AD module for Windows PowerShell.</span></span>

<span data-ttu-id="9c516-160">hello 下列範例示範如何 tooenable 內部部署 MFA 使用 hello [Set-msoldomainfederationsettings cmdlet](https://msdn.microsoft.com/library/azure/dn194088.aspx) hello contoso.com 租用戶上：</span><span class="sxs-lookup"><span data-stu-id="9c516-160">hello following example shows how tooenable on-premises MFA by using hello [Set-MsolDomainFederationSettings cmdlet](https://msdn.microsoft.com/library/azure/dn194088.aspx) on hello contoso.com tenant:</span></span>

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

<span data-ttu-id="9c516-161">在加法 toosetting 此旗標，hello 同盟租用戶 AD FS 執行個體必須設定 tooperform multi-factor authentication。</span><span class="sxs-lookup"><span data-stu-id="9c516-161">In addition toosetting this flag, hello federated tenant AD FS instance must be configured tooperform multi-factor authentication.</span></span> <span data-ttu-id="9c516-162">請依照指示 hello [Azure Multi-factor Authentication Server 在內部部署](../multi-factor-authentication/multi-factor-authentication-get-started-server.md)。</span><span class="sxs-lookup"><span data-stu-id="9c516-162">Follow hello instructions for [deploying Azure Multi-Factor Authentication on-premises](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="9c516-163">相關文章</span><span class="sxs-lookup"><span data-stu-id="9c516-163">Related Articles</span></span>
* [<span data-ttu-id="9c516-164">保護存取 tooOffice 365 和其他應用程式連接 tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9c516-164">Securing access tooOffice 365 and other apps connected tooAzure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="9c516-165">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="9c516-165">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

