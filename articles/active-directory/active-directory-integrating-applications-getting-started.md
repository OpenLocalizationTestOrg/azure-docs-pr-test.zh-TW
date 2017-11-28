---
title: "aaaGet 啟動 Azure AD 整合與應用程式 |Microsoft 文件"
description: "本文章是整合 Azure Active Directory (AD) 與在內部部署應用程式和雲端應用程式的入門指南。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: db6d210d-c970-49e9-bd20-36d984bcd1c3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 5a7a851e8418083fee72ab58477a9cab75d0d4bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a><span data-ttu-id="4e249-103">整合 Azure Active Directory 與應用程式入門指南</span><span class="sxs-lookup"><span data-stu-id="4e249-103">Integrating Azure Active Directory with applications getting started guide</span></span>
## <a name="overview"></a><span data-ttu-id="4e249-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4e249-104">Overview</span></span>
<span data-ttu-id="4e249-105">本主題是預定的 toogive 您與 Azure Active Directory (AD) 整合應用程式的藍圖。</span><span class="sxs-lookup"><span data-stu-id="4e249-105">This topic is intended toogive you a roadmap for integrating applications with Azure Active Directory (AD).</span></span> <span data-ttu-id="4e249-106">每個 hello 的以下各節包含更詳細主題的簡短摘要，以便識別這個使用者入門指南的哪些部分是相關 tooyou。</span><span class="sxs-lookup"><span data-stu-id="4e249-106">Each of hello sections below contain a brief summary of a more detailed topic so you can identify which parts of this getting started guide are relevant tooyou.</span></span>  <span data-ttu-id="4e249-107">按照每個主體 hello 連結以取得深入剖析。</span><span class="sxs-lookup"><span data-stu-id="4e249-107">Follow hello links for a deeper dive on each subject.</span></span>

## <a name="before-you-begin-take-inventory"></a><span data-ttu-id="4e249-108">在開始之前，請取得清查</span><span class="sxs-lookup"><span data-stu-id="4e249-108">Before you begin, take inventory</span></span>
<span data-ttu-id="4e249-109">您跳 toointegrating 應用程式與 Azure AD 中之前，您和您想要 toogo 是重要的 tooknow。</span><span class="sxs-lookup"><span data-stu-id="4e249-109">Before you jump in toointegrating applications with Azure AD, it is important tooknow where you are and where you want toogo.</span></span>  <span data-ttu-id="4e249-110">hello 下列問題會預期的 toohelp 想像您 Azure AD 應用程式整合專案。</span><span class="sxs-lookup"><span data-stu-id="4e249-110">hello following questions are intended toohelp you think about your Azure AD application integration project.</span></span>

### <a name="application-inventory"></a><span data-ttu-id="4e249-111">應用程式清查</span><span class="sxs-lookup"><span data-stu-id="4e249-111">Application inventory</span></span>
* <span data-ttu-id="4e249-112">您所有應用程式的所在位置？</span><span class="sxs-lookup"><span data-stu-id="4e249-112">Where are all of your applications?</span></span> <span data-ttu-id="4e249-113">擁有者為？</span><span class="sxs-lookup"><span data-stu-id="4e249-113">Who owns them?</span></span>
* <span data-ttu-id="4e249-114">您的應用程式需要何種驗證？</span><span class="sxs-lookup"><span data-stu-id="4e249-114">What kind of authentication do your applications require?</span></span>
* <span data-ttu-id="4e249-115">需要哪些人存取 toowhich 應用程式？</span><span class="sxs-lookup"><span data-stu-id="4e249-115">Who needs access toowhich applications?</span></span>
* <span data-ttu-id="4e249-116">您想 toodeploy 新的應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="4e249-116">Do you want toodeploy a new application?</span></span>
  * <span data-ttu-id="4e249-117">您將在公司內部建立並將它部署在 Azure 計算執行個體？</span><span class="sxs-lookup"><span data-stu-id="4e249-117">Will you build it in-house and deploy it on an Azure compute instance?</span></span>
  * <span data-ttu-id="4e249-118">您可以使用其中所提供之 hello Azure 應用程式庫？</span><span class="sxs-lookup"><span data-stu-id="4e249-118">Will you use one that is available in hello Azure Application Gallery?</span></span>

### <a name="user-and-group-inventory"></a><span data-ttu-id="4e249-119">使用者和群組清查</span><span class="sxs-lookup"><span data-stu-id="4e249-119">User and group inventory</span></span>
* <span data-ttu-id="4e249-120">您的使用者帳戶所在的位置？</span><span class="sxs-lookup"><span data-stu-id="4e249-120">Where do your user accounts reside?</span></span>
  * <span data-ttu-id="4e249-121">內部部署 Active Directory</span><span class="sxs-lookup"><span data-stu-id="4e249-121">On-premises Active Directory</span></span>
  * <span data-ttu-id="4e249-122">Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e249-122">Azure AD</span></span>
  * <span data-ttu-id="4e249-123">您擁有在個別的應用程式資料庫中</span><span class="sxs-lookup"><span data-stu-id="4e249-123">Within a separate application database that you own</span></span>
  * <span data-ttu-id="4e249-124">在未經約束的應用程式中</span><span class="sxs-lookup"><span data-stu-id="4e249-124">In unsanctioned applications</span></span>
  * <span data-ttu-id="4e249-125">所有上述 hello</span><span class="sxs-lookup"><span data-stu-id="4e249-125">All of hello above</span></span>
* <span data-ttu-id="4e249-126">個別使用者目前有哪些權限和角色指派？</span><span class="sxs-lookup"><span data-stu-id="4e249-126">What permissions and role assignments do individual users currently have?</span></span> <span data-ttu-id="4e249-127">您需要 tooreview 其存取權或您確定您的使用者存取和角色指派是適當現在嗎？</span><span class="sxs-lookup"><span data-stu-id="4e249-127">Do you need tooreview their access or are you sure that your user access and role assignments are appropriate now?</span></span>
* <span data-ttu-id="4e249-128">是否已經在您的內部部署 Active Directory 中建立群組？</span><span class="sxs-lookup"><span data-stu-id="4e249-128">Are groups already established in your on-premises Active Directory?</span></span>
  * <span data-ttu-id="4e249-129">您的群組的組織方式？</span><span class="sxs-lookup"><span data-stu-id="4e249-129">How are your groups organized?</span></span>
  * <span data-ttu-id="4e249-130">Hello 群組成員是誰？</span><span class="sxs-lookup"><span data-stu-id="4e249-130">Who are hello group members?</span></span>
  * <span data-ttu-id="4e249-131">哪些權限/角色指派 hello 群組目前有？</span><span class="sxs-lookup"><span data-stu-id="4e249-131">What permissions/role assignments do hello groups currently have?</span></span>
* <span data-ttu-id="4e249-132">您將會整合之前需要 tooclean 使用者/群組的資料庫嗎？</span><span class="sxs-lookup"><span data-stu-id="4e249-132">Will you need tooclean up user/group databases before integrating?</span></span>  <span data-ttu-id="4e249-133">(這是很重要的問題。</span><span class="sxs-lookup"><span data-stu-id="4e249-133">(This is a pretty important question.</span></span> <span data-ttu-id="4e249-134">垃圾進，垃圾出 - 應當避免無用資料。)</span><span class="sxs-lookup"><span data-stu-id="4e249-134">Garbage in, garbage out.)</span></span>

### <a name="access-management-inventory"></a><span data-ttu-id="4e249-135">存取管理清查</span><span class="sxs-lookup"><span data-stu-id="4e249-135">Access management inventory</span></span>
* <span data-ttu-id="4e249-136">您如何目前管理使用者存取 tooapplications？</span><span class="sxs-lookup"><span data-stu-id="4e249-136">How do you currently manage user access tooapplications?</span></span> <span data-ttu-id="4e249-137">所需要 toochange 嗎？</span><span class="sxs-lookup"><span data-stu-id="4e249-137">Does that need toochange?</span></span>  <span data-ttu-id="4e249-138">您是否有考慮其他方式 toomanage 存取，例如與[RBAC](role-based-access-control-configure.md)例如？</span><span class="sxs-lookup"><span data-stu-id="4e249-138">Have you considered other ways toomanage access, such as with [RBAC](role-based-access-control-configure.md) for example?</span></span>
* <span data-ttu-id="4e249-139">需要哪些人存取 toowhat？</span><span class="sxs-lookup"><span data-stu-id="4e249-139">Who needs access toowhat?</span></span>

<span data-ttu-id="4e249-140">或許您沒有 hello 的這些問題的答案 tooall 最前面位置，但是沒關係。</span><span class="sxs-lookup"><span data-stu-id="4e249-140">Maybe you don't have hello answers tooall of these questions up front but that's okay.</span></span>  <span data-ttu-id="4e249-141">本指南可協助您回答其中一些問題，並做出一些明智的決策。</span><span class="sxs-lookup"><span data-stu-id="4e249-141">This guide can help you answer some of those questions and make some informed decisions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e249-142">必要條件</span><span class="sxs-lookup"><span data-stu-id="4e249-142">Prerequisites</span></span>
* <span data-ttu-id="4e249-143">一個 Azure 訂用帳戶，以及一個 Azure Active Directory 目錄。</span><span class="sxs-lookup"><span data-stu-id="4e249-143">An Azure subscription and an Azure Active Directory directory.</span></span>  <span data-ttu-id="4e249-144">如果您尚沒有 Azure 訂用帳戶，可以免費試用 Azure 30 天。</span><span class="sxs-lookup"><span data-stu-id="4e249-144">If you don't already have an Azure subscription, you can try out Azure for free for 30 days.</span></span> [<span data-ttu-id="4e249-145">立即試用！</span><span class="sxs-lookup"><span data-stu-id="4e249-145">Try it out!</span></span>](https://azure.microsoft.com/trial/get-started-active-directory/)

## <a name="application-integration-with-azure-ad"></a><span data-ttu-id="4e249-146">與 Azure AD 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="4e249-146">Application integration with Azure AD</span></span>
### <a name="finding-unsanctioned-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="4e249-147">使用 Cloud App Discovery 尋找未經約束的雲端應用程式</span><span class="sxs-lookup"><span data-stu-id="4e249-147">Finding unsanctioned cloud applications with Cloud App Discovery</span></span>
<span data-ttu-id="4e249-148">如上所述，可能有應用程式到目前為止仍未受到組織的管理。</span><span class="sxs-lookup"><span data-stu-id="4e249-148">As mentioned above, there may be applications that haven't been managed by your organization until now.</span></span>  <span data-ttu-id="4e249-149">Hello 清查程序的一部分，很可能 toofind 未經批准雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e249-149">As part of hello inventory process, it is possible toofind unsanctioned cloud applications.</span></span> <span data-ttu-id="4e249-150">請參閱 [使用 Cloud App Discovery 尋找未經約束的雲端應用程式](active-directory-cloudappdiscovery-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="4e249-150">See [Finding unsanctioned cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

### <a name="authentication-types"></a><span data-ttu-id="4e249-151">驗證類型</span><span class="sxs-lookup"><span data-stu-id="4e249-151">Authentication Types</span></span>
<span data-ttu-id="4e249-152">每個應用程式可能有不同的驗證需求。</span><span class="sxs-lookup"><span data-stu-id="4e249-152">Each of your applications may have different authentication requirements.</span></span> <span data-ttu-id="4e249-153">利用 Azure AD，可將簽署憑證用於使用 SAML 2.0、WS-同盟或 OpenID Connect 通訊協定，以及密碼單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e249-153">With Azure AD, signing certificates can be used with applications that use SAML 2.0, WS-Federation, or OpenID Connect Protocols as well as Password Single Sign On.</span></span> <span data-ttu-id="4e249-154">如需要與 Azure AD 搭配使用的應用程式驗證類型的詳細資訊，請參閱[在 Azure Active Directory 中管理同盟單一登入的憑證](active-directory-sso-certs.md)和[密碼式單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="4e249-154">For more information about application authentication types for use with Azure AD see [Managing Certificates for Federated Single Sign-On in Azure Active Directory](active-directory-sso-certs.md) and [Password based single sign on](active-directory-appssoaccess-whatis.md).</span></span>

### <a name="enabling-sso-with-azure-ad-app-proxy"></a><span data-ttu-id="4e249-155">使用 Azure AD 應用程式 Proxy 啟用 SSO</span><span class="sxs-lookup"><span data-stu-id="4e249-155">Enabling SSO with Azure AD App Proxy</span></span>
<span data-ttu-id="4e249-156">與 Microsoft Azure AD 應用程式 Proxy，您可以提供存取 tooapplications 位於您私人網路安全地從任何地方和任何裝置上。</span><span class="sxs-lookup"><span data-stu-id="4e249-156">With Microsoft Azure AD Application Proxy, you can provide access tooapplications located inside your private network securely, from anywhere and on any device.</span></span> <span data-ttu-id="4e249-157">在您的環境中安裝應用程式 Proxy 連接器之後，可以輕鬆地使用 Azure AD 來加以設定。</span><span class="sxs-lookup"><span data-stu-id="4e249-157">After you have installed an application proxy connector within your environment, it can be easily configured with Azure AD.</span></span>

### <a name="integrating-applications-with-azure-ad"></a><span data-ttu-id="4e249-158">整合應用程式與 Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e249-158">Integrating applications with Azure AD</span></span>
<span data-ttu-id="4e249-159">hello 下列文章中討論的 hello 不同方式的應用程式整合與 Azure AD，並提供一些指引。</span><span class="sxs-lookup"><span data-stu-id="4e249-159">hello following articles discuss hello different ways applications integrate with Azure AD, and provide some guidance.</span></span>

* [<span data-ttu-id="4e249-160">判斷哪一個 Active Directory toouse</span><span class="sxs-lookup"><span data-stu-id="4e249-160">Determining which Active Directory toouse</span></span>](active-directory-administer.md)
* [<span data-ttu-id="4e249-161">在 hello Azure 應用程式庫中使用應用程式</span><span class="sxs-lookup"><span data-stu-id="4e249-161">Using applications in hello Azure application gallery</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4e249-162">整合 SaaS 應用程式教學課程清單</span><span class="sxs-lookup"><span data-stu-id="4e249-162">Integrating SaaS applications tutorials list</span></span>](active-directory-saas-tutorial-list.md)

## <a name="managing-access-tooapplications"></a><span data-ttu-id="4e249-163">管理存取 tooapplications</span><span class="sxs-lookup"><span data-stu-id="4e249-163">Managing access tooapplications</span></span>
<span data-ttu-id="4e249-164">hello 下列文章說明已整合 Azure AD 連接器，使用 Azure AD 與 Azure AD 之後，您可以管理存取 tooapplications 的方式。</span><span class="sxs-lookup"><span data-stu-id="4e249-164">hello following articles describe ways you can manage access tooapplications once they have been integrated with Azure AD using Azure AD Connectors and Azure AD.</span></span>

* [<span data-ttu-id="4e249-165">使用 Azure AD 的管理存取 tooapps</span><span class="sxs-lookup"><span data-stu-id="4e249-165">Managing access tooapps using Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="4e249-166">使用 Azure AD 連接器自動化</span><span class="sxs-lookup"><span data-stu-id="4e249-166">Automating with Azure AD Connectors</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="4e249-167">將使用者指派 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="4e249-167">Assigning users tooan application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)
* [<span data-ttu-id="4e249-168">將群組指派 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="4e249-168">Assigning groups tooan application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)
* [<span data-ttu-id="4e249-169">共用帳戶</span><span class="sxs-lookup"><span data-stu-id="4e249-169">Sharing accounts</span></span>](active-directory-sharing-accounts.md)

## <a name="integrating-custom-applications"></a><span data-ttu-id="4e249-170">整合自訂應用程式</span><span class="sxs-lookup"><span data-stu-id="4e249-170">Integrating custom applications</span></span>
<span data-ttu-id="4e249-171">如果您要撰寫新的應用程式，而且想 tooassist 開發人員運用 hello 電源 Azure AD，請參閱[Guiding 開發人員](active-directory-applications-guiding-developers-for-lob-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="4e249-171">If you are writing a new application and want tooassist developers in leveraging hello power Azure AD, see [Guiding developers](active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="4e249-172">如果您想 tooadd 您自訂的應用程式 toohello Azure 應用程式庫，請參閱[「 攜帶您自己的應用程式 」 使用自助 Azure AD SAML 組態](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4e249-172">If you want tooadd your custom application toohello Azure Application Gallery, see [“Bring your own app” with Azure AD Self-Service SAML configuration](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="4e249-173">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4e249-173">See also</span></span>
* [<span data-ttu-id="4e249-174">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="4e249-174">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

