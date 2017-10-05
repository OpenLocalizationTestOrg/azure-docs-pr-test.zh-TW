---
title: "SaaS 應用程式的 Azure 條件式存取 | Microsoft Docs"
description: "Azure AD 中的條件式存取可讓您設定每個應用程式的多重要素驗證存取規則，且能夠封鎖不在受信任網路上的使用者存取。 "
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
ms.openlocfilehash: efaa70467346e910a78a63d182041029bb34b1cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a><span data-ttu-id="8f4ca-103">開始使用 Azure Active Directory 條件式存取</span><span class="sxs-lookup"><span data-stu-id="8f4ca-103">Getting started with Azure Active Directory Conditional Access</span></span>
<span data-ttu-id="8f4ca-104">[SaaS](https://azure.microsoft.com/overview/what-is-saas/) 應用程式及 Azure AD 連線應用程式的「Azure Active Directory 條件式存取」可讓您根據群組、位置和應用程式敏感性來設定條件式存取。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-104">Azure Active Directory Conditional Access for [SaaS](https://azure.microsoft.com/overview/what-is-saas/) apps and Azure AD connected apps lets you configure conditional access based on group, location, and application sensitivity.</span></span> 

<span data-ttu-id="8f4ca-105">使用以應用程式敏感性為基礎的條件式存取時，您可以設定每一應用程式的多重要素驗證 (MFA) 存取規則。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-105">With conditional access based on application sensitivity, you can set multi-factor authentication (MFA) access rules per application.</span></span> <span data-ttu-id="8f4ca-106">每一應用程式 MFA 會讓您能夠封鎖不在受信任網路上的使用者。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-106">MFA per application provides the ability to block access for users who are not on a trusted network.</span></span> <span data-ttu-id="8f4ca-107">您可以將 MFA 規則套用到所有已指派給應用程式的使用者，或只套用到所指定安全性群組內的使用者。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-107">You can apply MFA rules to all users that are assigned to the application, or only for users within specified security groups.</span></span>  <span data-ttu-id="8f4ca-108">如果使用者是從組織網路內的 IP 位址存取應用程式，則可以從 MFA 需求中排除這些使用者。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-108">Users may be excluded from the MFA requirement if they are accessing the application from an IP address that is inside the organization’s network.</span></span>

<span data-ttu-id="8f4ca-109">購買 Azure Active Directory Premium 授權的客戶可使用這些功能。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-109">These capabilities will be available to customers that have purchased an Azure Active Directory Premium license.</span></span>

## <a name="scenario-prerequisites"></a><span data-ttu-id="8f4ca-110">案例必要條件</span><span class="sxs-lookup"><span data-stu-id="8f4ca-110">Scenario prerequisites</span></span>
* <span data-ttu-id="8f4ca-111">Azure Active Directory Premium 的授權</span><span class="sxs-lookup"><span data-stu-id="8f4ca-111">License for Azure Active Directory Premium</span></span>
* <span data-ttu-id="8f4ca-112">同盟或受管理的 Azure Active Directory 租用戶</span><span class="sxs-lookup"><span data-stu-id="8f4ca-112">Federated or managed Azure Active Directory tenant</span></span>
* <span data-ttu-id="8f4ca-113">同盟租用戶需要啟用多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-113">Federated tenants require that multi-factor authentication be enabled.</span></span>

## <a name="configure-per-application-access-rules"></a><span data-ttu-id="8f4ca-114">設定每個應用程式的存取規則</span><span class="sxs-lookup"><span data-stu-id="8f4ca-114">Configure per-application access rules</span></span>
<span data-ttu-id="8f4ca-115">本節描述如何設定每個應用程式的存取規則。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-115">This section describes how to configure per-application access rules.</span></span>

1. <span data-ttu-id="8f4ca-116">使用 Azure AD 全域管理員身分的帳戶登入 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-116">Sign in to the Azure classic portal Using an account that is a global administrator for Azure AD.</span></span>
2. <span data-ttu-id="8f4ca-117">在左窗格中選取 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-117">On the left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="8f4ca-118">在 [目錄] 索引標籤中，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-118">On the Directory tab, select your directory.</span></span>
4. <span data-ttu-id="8f4ca-119">選取 [應用程式]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-119">Select the **Applications** tab.</span></span>
5. <span data-ttu-id="8f4ca-120">選取要設定規則的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-120">Select the application that the rule will be set for.</span></span>
6. <span data-ttu-id="8f4ca-121">選取 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-121">Select the **Configure** tab.</span></span>
7. <span data-ttu-id="8f4ca-122">向下捲動至存取規則區段。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-122">Scroll down to the access rules section.</span></span> <span data-ttu-id="8f4ca-123">選取所需的存取規則。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-123">Select the desired access rule.</span></span>
8. <span data-ttu-id="8f4ca-124">指定將套用此規則的使用者。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-124">Specify the users the rule will apply to.</span></span>
9. <span data-ttu-id="8f4ca-125">將 [啟用] 設定為 [開啟] 以啟用原則。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-125">Enable the policy by selecting **Enabled to be On**.</span></span>

## <a name="understanding-access-rules"></a><span data-ttu-id="8f4ca-126">了解存取規則</span><span class="sxs-lookup"><span data-stu-id="8f4ca-126">Understanding access rules</span></span>
<span data-ttu-id="8f4ca-127">本節提供 Azure 條件式應用程式存取中支援的存取規則的詳細描述。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-127">This section gives a detailed description of the access rules supported in the Azure Conditional Application Access.</span></span>

### <a name="specifying-the-users-the-access-rules-apply-to"></a><span data-ttu-id="8f4ca-128">指定套用存取規則的使用者</span><span class="sxs-lookup"><span data-stu-id="8f4ca-128">Specifying the users the access rules apply to</span></span>
<span data-ttu-id="8f4ca-129">根據預設，規則會套用至所有可存取應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-129">By default the policy will apply to all users that have access to the application.</span></span> <span data-ttu-id="8f4ca-130">不過，您也可以將原則限制為指定安全性群組的成員使用者。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-130">However, you can also restrict the policy to users that are members of the specified security groups.</span></span> <span data-ttu-id="8f4ca-131">[加入群組]  按鈕用來從群組選取對話方塊中，選取將套用存取規則的一或多個群組。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-131">The **Add Group** button is used to select one or more groups from the group selection dialog that the access rule will apply to.</span></span> <span data-ttu-id="8f4ca-132">此對話方塊也可用來移除選取的群組。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-132">This dialog can also be used to remove selected groups.</span></span> <span data-ttu-id="8f4ca-133">當選擇將規則套用至「群組」時，只會對屬於其中一個指定安全性群組的使用者強制執行存取規則。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-133">When the rules are selected to apply to Groups, the access rules will only be enforced for users that belong to one of the specified security groups.</span></span>

<span data-ttu-id="8f4ca-134">您也可以選取 [例外]  選項並指定一個或多個群組，來明確地從原則中排除安全性群組。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-134">Security groups can also be explicitly excluded from the policy by selecting the **Except** option and specifying one or more groups.</span></span> <span data-ttu-id="8f4ca-135">使用者如果是 [例外]  清單中群組的成員，則即使身為套用存取規則群組的成員，也不會受到多重要素驗證需求限制。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-135">Users that are a member of a group in the **Except** list will not be subject to the multi-factor authentication requirement, even if they are a member of a group that the access rule applies to.</span></span>
<span data-ttu-id="8f4ca-136">以下顯示的存取規則會要求「管理員」群組中的所有使用者，在存取應用程式時使用多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-136">The access rule shown below will require all users in the Managers group to use multi-factor authentication when accessing the application.</span></span>

![使用 MFA 設定條件式存取規則](./media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a><span data-ttu-id="8f4ca-138">條件式存取規則和 MFA</span><span class="sxs-lookup"><span data-stu-id="8f4ca-138">Conditional Access Rules with MFA</span></span>
<span data-ttu-id="8f4ca-139">如果已使用每個使用者的多重要素驗證功能來設定使用者，則使用者的這項設定將與應用程式的多重要素驗證規則相結合。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-139">If a user has been configured using the per-user multi-factor authentication feature, this setting on the user will combine with the multi-factor authentication rules of the app.</span></span> <span data-ttu-id="8f4ca-140">這表示已設定每個使用者多重要素驗證的使用者，即使已從應用程式多重要素驗證規則中免除，也都必須執行多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-140">This means a user that has been configured for per-user multi-factor authentication will be required to perform multi-factor authentication even if they have been exempted from the application multi-factor authentication rules.</span></span> <span data-ttu-id="8f4ca-141">深入了解多重要素驗證和每個使用者設定。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-141">Learn more about multi-factor authentication and per-user settings.</span></span>

### <a name="access-rule-options"></a><span data-ttu-id="8f4ca-142">存取規則選項</span><span class="sxs-lookup"><span data-stu-id="8f4ca-142">Access rule options</span></span>
<span data-ttu-id="8f4ca-143">支援下列選項：</span><span class="sxs-lookup"><span data-stu-id="8f4ca-143">The following options are supported:</span></span>

* <span data-ttu-id="8f4ca-144">**需要多重要素驗證**︰套用存取規則的使用者必須先完成多重要素驗證，才能存取套用規則的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-144">**Require multi-factor authentication**: The users to whom the access rules apply to, will be required to complete multi-factor authentication before accessing the application that the policy applies to.</span></span>
* <span data-ttu-id="8f4ca-145">**不在工作時需要多重要素驗證**︰來自受信任 IP 位址的使用者將不需要執行多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-145">**Require multi-factor authentication when not at work**: A user that is coming from a trusted IP address will not be required to perform multi-factor authentication.</span></span> <span data-ttu-id="8f4ca-146">可以在 [Multi-Factor Authentication 設定] 頁面上設定受信任的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-146">The trusted IP address ranges can be configured on the multi-factor authentication settings page.</span></span>
* <span data-ttu-id="8f4ca-147">**不工作時封鎖存取**：將會封鎖不是來自受信任 IP 位址的使用者。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-147">**Block access when not at work**: A user that is not coming from a trusted IP address will be blocked.</span></span> <span data-ttu-id="8f4ca-148">可以在 [Multi-Factor Authentication 設定] 頁面上設定受信任的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-148">The trusted IP address ranges can be configured on the multi-factor authentication settings page.</span></span>

### <a name="setting-rule-status"></a><span data-ttu-id="8f4ca-149">設定規則狀態</span><span class="sxs-lookup"><span data-stu-id="8f4ca-149">Setting rule status</span></span>
<span data-ttu-id="8f4ca-150">存取規則狀態可讓您開啟或關閉規則。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-150">Access rule status allows turning the rules on or off.</span></span> <span data-ttu-id="8f4ca-151">當存取規則關閉時，將不會強制執行多重要素驗證需求。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-151">When the access rules are off, the multi-factor authentication requirement is not enforced.</span></span>

### <a name="access-rule-evaluation"></a><span data-ttu-id="8f4ca-152">存取規則評估</span><span class="sxs-lookup"><span data-stu-id="8f4ca-152">Access rule evaluation</span></span>
<span data-ttu-id="8f4ca-153">當使用者存取使用 OAuth 2.0、OpenID Connect、SAML 或 WS-同盟的同盟應用程式時，就會評估存取規則。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-153">Access rules are evaluated when a user accesses a federated application that uses OAuth 2.0, OpenID Connect, SAML or WS-Federation.</span></span> <span data-ttu-id="8f4ca-154">此外，當 OAuth 2.0 和 OpenID Connect 使用重新整理權杖來取得存取權杖時，也會評估存取規則。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-154">In addition, access rules are evaluated when the OAuth 2.0 and OpenID Connect use a refresh token to acquire an access token.</span></span> <span data-ttu-id="8f4ca-155">如果使用重新整理權杖時原則評估失敗，將會傳回 **invalid_grant** 錯誤，這表示使用者必須向用戶端重新進行驗證。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-155">If policy evaluation fails when a refresh token is used, the error **invalid_grant** will be returned, this indicates the user needs to re-authenticate to the client.</span></span>

### <a name="configure-federation-services-to-provide-multi-factor-authentication"></a><span data-ttu-id="8f4ca-156">設定同盟服務以提供多重要素驗證</span><span class="sxs-lookup"><span data-stu-id="8f4ca-156">Configure federation services to provide multi-factor authentication</span></span>
<span data-ttu-id="8f4ca-157">就同盟的租用戶而言，MFA 可由 Azure Active Directory 或內部部署 AD FS 伺服器執行。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-157">For federated tenants, MFA may be performed by Azure Active Directory or by the on-premises AD FS server.</span></span>

<span data-ttu-id="8f4ca-158">根據預設，MFA 會發生在 Azure Active Directory 所裝載的頁面上。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-158">By default, MFA will occur at a page hosted by Azure Active Directory.</span></span> <span data-ttu-id="8f4ca-159">若要設定內部部署 MFA，必須使用 Windows PowerShell 的 Azure AD 模組，在 Azure Active Directory 中將 **-SupportsMFA** 屬性設定為 **true**。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-159">To configure MFA on-premises, the **–SupportsMFA** property must be set to **true** in Azure Active Directory, by using the Azure AD module for Windows PowerShell.</span></span>

<span data-ttu-id="8f4ca-160">下列範例示範如何在 consoso.com 租用戶上使用 [Set-MsolDomainFederationSettings Cmdlet](https://msdn.microsoft.com/library/azure/dn194088.aspx) 來啟用內部部署 MFA︰</span><span class="sxs-lookup"><span data-stu-id="8f4ca-160">The following example shows how to enable on-premises MFA by using the [Set-MsolDomainFederationSettings cmdlet](https://msdn.microsoft.com/library/azure/dn194088.aspx) on the contoso.com tenant:</span></span>

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

<span data-ttu-id="8f4ca-161">除了設定這個旗標，同盟租用戶 AD FS 執行個體必須設為執行多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-161">In addition to setting this flag, the federated tenant AD FS instance must be configured to perform multi-factor authentication.</span></span> <span data-ttu-id="8f4ca-162">請依照 [在內部部署環境部署 Microsoft Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-server.md)的指示操作。</span><span class="sxs-lookup"><span data-stu-id="8f4ca-162">Follow the instructions for [deploying Azure Multi-Factor Authentication on-premises](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="8f4ca-163">相關文章</span><span class="sxs-lookup"><span data-stu-id="8f4ca-163">Related Articles</span></span>
* [<span data-ttu-id="8f4ca-164">保護對 Office 365 及其他連接至 Azure Active Directory 之應用程式的存取</span><span class="sxs-lookup"><span data-stu-id="8f4ca-164">Securing access to Office 365 and other apps connected to Azure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="8f4ca-165">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="8f4ca-165">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

