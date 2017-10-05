---
title: "開始將 Azure AD 與應用程式整合 | Microsoft Docs"
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
ms.openlocfilehash: e273d27bacf6978c5056c0ab09846c26426dd12b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a><span data-ttu-id="b516a-103">整合 Azure Active Directory 與應用程式入門指南</span><span class="sxs-lookup"><span data-stu-id="b516a-103">Integrating Azure Active Directory with applications getting started guide</span></span>
## <a name="overview"></a><span data-ttu-id="b516a-104">Overview</span><span class="sxs-lookup"><span data-stu-id="b516a-104">Overview</span></span>
<span data-ttu-id="b516a-105">本主題旨在提供您一個藍圖來整合應用程式與 Azure Active Directory (AD)。</span><span class="sxs-lookup"><span data-stu-id="b516a-105">This topic is intended to give you a roadmap for integrating applications with Azure Active Directory (AD).</span></span> <span data-ttu-id="b516a-106">每個以下各節包含更詳細主題的簡短摘要，讓您可以識別本入門指南的哪些部分與您相關。</span><span class="sxs-lookup"><span data-stu-id="b516a-106">Each of the sections below contain a brief summary of a more detailed topic so you can identify which parts of this getting started guide are relevant to you.</span></span>  <span data-ttu-id="b516a-107">遵循連結來深入探索每個主題。</span><span class="sxs-lookup"><span data-stu-id="b516a-107">Follow the links for a deeper dive on each subject.</span></span>

## <a name="before-you-begin-take-inventory"></a><span data-ttu-id="b516a-108">在開始之前，請取得清查</span><span class="sxs-lookup"><span data-stu-id="b516a-108">Before you begin, take inventory</span></span>
<span data-ttu-id="b516a-109">您在直接跳到整合應用程式與 Azure AD 之前，務必知道您所在位置與您想要前往的位置。</span><span class="sxs-lookup"><span data-stu-id="b516a-109">Before you jump in to integrating applications with Azure AD, it is important to know where you are and where you want to go.</span></span>  <span data-ttu-id="b516a-110">下列問題的用意在於幫助您思考您的 Azure AD 應用程式整合專案。</span><span class="sxs-lookup"><span data-stu-id="b516a-110">The following questions are intended to help you think about your Azure AD application integration project.</span></span>

### <a name="application-inventory"></a><span data-ttu-id="b516a-111">應用程式清查</span><span class="sxs-lookup"><span data-stu-id="b516a-111">Application inventory</span></span>
* <span data-ttu-id="b516a-112">您所有應用程式的所在位置？</span><span class="sxs-lookup"><span data-stu-id="b516a-112">Where are all of your applications?</span></span> <span data-ttu-id="b516a-113">擁有者為？</span><span class="sxs-lookup"><span data-stu-id="b516a-113">Who owns them?</span></span>
* <span data-ttu-id="b516a-114">您的應用程式需要何種驗證？</span><span class="sxs-lookup"><span data-stu-id="b516a-114">What kind of authentication do your applications require?</span></span>
* <span data-ttu-id="b516a-115">誰需要存取哪些應用程式？</span><span class="sxs-lookup"><span data-stu-id="b516a-115">Who needs access to which applications?</span></span>
* <span data-ttu-id="b516a-116">您是否要部署新應用程式？</span><span class="sxs-lookup"><span data-stu-id="b516a-116">Do you want to deploy a new application?</span></span>
  * <span data-ttu-id="b516a-117">您將在公司內部建立並將它部署在 Azure 計算執行個體？</span><span class="sxs-lookup"><span data-stu-id="b516a-117">Will you build it in-house and deploy it on an Azure compute instance?</span></span>
  * <span data-ttu-id="b516a-118">您將使用 Azure 應用程式資源庫中所提供的其中一個應用程式？</span><span class="sxs-lookup"><span data-stu-id="b516a-118">Will you use one that is available in the Azure Application Gallery?</span></span>

### <a name="user-and-group-inventory"></a><span data-ttu-id="b516a-119">使用者和群組清查</span><span class="sxs-lookup"><span data-stu-id="b516a-119">User and group inventory</span></span>
* <span data-ttu-id="b516a-120">您的使用者帳戶所在的位置？</span><span class="sxs-lookup"><span data-stu-id="b516a-120">Where do your user accounts reside?</span></span>
  * <span data-ttu-id="b516a-121">內部部署 Active Directory</span><span class="sxs-lookup"><span data-stu-id="b516a-121">On-premises Active Directory</span></span>
  * <span data-ttu-id="b516a-122">Azure AD</span><span class="sxs-lookup"><span data-stu-id="b516a-122">Azure AD</span></span>
  * <span data-ttu-id="b516a-123">您擁有在個別的應用程式資料庫中</span><span class="sxs-lookup"><span data-stu-id="b516a-123">Within a separate application database that you own</span></span>
  * <span data-ttu-id="b516a-124">在未經約束的應用程式中</span><span class="sxs-lookup"><span data-stu-id="b516a-124">In unsanctioned applications</span></span>
  * <span data-ttu-id="b516a-125">以上皆是</span><span class="sxs-lookup"><span data-stu-id="b516a-125">All of the above</span></span>
* <span data-ttu-id="b516a-126">個別使用者目前有哪些權限和角色指派？</span><span class="sxs-lookup"><span data-stu-id="b516a-126">What permissions and role assignments do individual users currently have?</span></span> <span data-ttu-id="b516a-127">您需要檢閱其存取權或您確定使用者現在的存取和角色指派適當嗎？</span><span class="sxs-lookup"><span data-stu-id="b516a-127">Do you need to review their access or are you sure that your user access and role assignments are appropriate now?</span></span>
* <span data-ttu-id="b516a-128">是否已經在您的內部部署 Active Directory 中建立群組？</span><span class="sxs-lookup"><span data-stu-id="b516a-128">Are groups already established in your on-premises Active Directory?</span></span>
  * <span data-ttu-id="b516a-129">您的群組的組織方式？</span><span class="sxs-lookup"><span data-stu-id="b516a-129">How are your groups organized?</span></span>
  * <span data-ttu-id="b516a-130">有哪些群組成員？</span><span class="sxs-lookup"><span data-stu-id="b516a-130">Who are the group members?</span></span>
  * <span data-ttu-id="b516a-131">群組目前有哪些權限/角色指派？</span><span class="sxs-lookup"><span data-stu-id="b516a-131">What permissions/role assignments do the groups currently have?</span></span>
* <span data-ttu-id="b516a-132">您是否需要在整合之前清除使用者/群組資料庫？</span><span class="sxs-lookup"><span data-stu-id="b516a-132">Will you need to clean up user/group databases before integrating?</span></span>  <span data-ttu-id="b516a-133">(這是很重要的問題。</span><span class="sxs-lookup"><span data-stu-id="b516a-133">(This is a pretty important question.</span></span> <span data-ttu-id="b516a-134">垃圾進，垃圾出 - 應當避免無用資料。)</span><span class="sxs-lookup"><span data-stu-id="b516a-134">Garbage in, garbage out.)</span></span>

### <a name="access-management-inventory"></a><span data-ttu-id="b516a-135">存取管理清查</span><span class="sxs-lookup"><span data-stu-id="b516a-135">Access management inventory</span></span>
* <span data-ttu-id="b516a-136">您如何目前管理使用者對應用程式存的取？</span><span class="sxs-lookup"><span data-stu-id="b516a-136">How do you currently manage user access to applications?</span></span> <span data-ttu-id="b516a-137">需要變更嗎？</span><span class="sxs-lookup"><span data-stu-id="b516a-137">Does that need to change?</span></span>  <span data-ttu-id="b516a-138">曾經考量過管理存取的其他方式，例如使用 [RBAC](role-based-access-control-configure.md) 之類？</span><span class="sxs-lookup"><span data-stu-id="b516a-138">Have you considered other ways to manage access, such as with [RBAC](role-based-access-control-configure.md) for example?</span></span>
* <span data-ttu-id="b516a-139">誰需要存取哪些內容？</span><span class="sxs-lookup"><span data-stu-id="b516a-139">Who needs access to what?</span></span>

<span data-ttu-id="b516a-140">也許您事先對這所有問題沒有答案，但是沒關係。</span><span class="sxs-lookup"><span data-stu-id="b516a-140">Maybe you don't have the answers to all of these questions up front but that's okay.</span></span>  <span data-ttu-id="b516a-141">本指南可協助您回答其中一些問題，並做出一些明智的決策。</span><span class="sxs-lookup"><span data-stu-id="b516a-141">This guide can help you answer some of those questions and make some informed decisions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b516a-142">必要條件</span><span class="sxs-lookup"><span data-stu-id="b516a-142">Prerequisites</span></span>
* <span data-ttu-id="b516a-143">一個 Azure 訂用帳戶，以及一個 Azure Active Directory 目錄。</span><span class="sxs-lookup"><span data-stu-id="b516a-143">An Azure subscription and an Azure Active Directory directory.</span></span>  <span data-ttu-id="b516a-144">如果您尚沒有 Azure 訂用帳戶，可以免費試用 Azure 30 天。</span><span class="sxs-lookup"><span data-stu-id="b516a-144">If you don't already have an Azure subscription, you can try out Azure for free for 30 days.</span></span> [<span data-ttu-id="b516a-145">立即試用！</span><span class="sxs-lookup"><span data-stu-id="b516a-145">Try it out!</span></span>](https://azure.microsoft.com/trial/get-started-active-directory/)

## <a name="application-integration-with-azure-ad"></a><span data-ttu-id="b516a-146">與 Azure AD 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="b516a-146">Application integration with Azure AD</span></span>
### <a name="finding-unsanctioned-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="b516a-147">使用 Cloud App Discovery 尋找未經約束的雲端應用程式</span><span class="sxs-lookup"><span data-stu-id="b516a-147">Finding unsanctioned cloud applications with Cloud App Discovery</span></span>
<span data-ttu-id="b516a-148">如上所述，可能有應用程式到目前為止仍未受到組織的管理。</span><span class="sxs-lookup"><span data-stu-id="b516a-148">As mentioned above, there may be applications that haven't been managed by your organization until now.</span></span>  <span data-ttu-id="b516a-149">作為清查程序的一部分，您可以找到未經約束的雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="b516a-149">As part of the inventory process, it is possible to find unsanctioned cloud applications.</span></span> <span data-ttu-id="b516a-150">請參閱 [使用 Cloud App Discovery 尋找未經約束的雲端應用程式](active-directory-cloudappdiscovery-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b516a-150">See [Finding unsanctioned cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

### <a name="authentication-types"></a><span data-ttu-id="b516a-151">驗證類型</span><span class="sxs-lookup"><span data-stu-id="b516a-151">Authentication Types</span></span>
<span data-ttu-id="b516a-152">每個應用程式可能有不同的驗證需求。</span><span class="sxs-lookup"><span data-stu-id="b516a-152">Each of your applications may have different authentication requirements.</span></span> <span data-ttu-id="b516a-153">利用 Azure AD，可將簽署憑證用於使用 SAML 2.0、WS-同盟或 OpenID Connect 通訊協定，以及密碼單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b516a-153">With Azure AD, signing certificates can be used with applications that use SAML 2.0, WS-Federation, or OpenID Connect Protocols as well as Password Single Sign On.</span></span> <span data-ttu-id="b516a-154">如需要與 Azure AD 搭配使用的應用程式驗證類型的詳細資訊，請參閱[在 Azure Active Directory 中管理同盟單一登入的憑證](active-directory-sso-certs.md)和[密碼式單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b516a-154">For more information about application authentication types for use with Azure AD see [Managing Certificates for Federated Single Sign-On in Azure Active Directory](active-directory-sso-certs.md) and [Password based single sign on](active-directory-appssoaccess-whatis.md).</span></span>

### <a name="enabling-sso-with-azure-ad-app-proxy"></a><span data-ttu-id="b516a-155">使用 Azure AD 應用程式 Proxy 啟用 SSO</span><span class="sxs-lookup"><span data-stu-id="b516a-155">Enabling SSO with Azure AD App Proxy</span></span>
<span data-ttu-id="b516a-156">透過 Microsoft Azure AD 應用程式 Proxy，您可以從任何地方及任何裝置上安全地為位於您的私人網路上的應用程式提供存取。</span><span class="sxs-lookup"><span data-stu-id="b516a-156">With Microsoft Azure AD Application Proxy, you can provide access to applications located inside your private network securely, from anywhere and on any device.</span></span> <span data-ttu-id="b516a-157">在您的環境中安裝應用程式 Proxy 連接器之後，可以輕鬆地使用 Azure AD 來加以設定。</span><span class="sxs-lookup"><span data-stu-id="b516a-157">After you have installed an application proxy connector within your environment, it can be easily configured with Azure AD.</span></span>

### <a name="integrating-applications-with-azure-ad"></a><span data-ttu-id="b516a-158">整合應用程式與 Azure AD</span><span class="sxs-lookup"><span data-stu-id="b516a-158">Integrating applications with Azure AD</span></span>
<span data-ttu-id="b516a-159">以下文章將討論整合應用程式與 Azure AD 的各種不同方式，並提供一些指引。</span><span class="sxs-lookup"><span data-stu-id="b516a-159">The following articles discuss the different ways applications integrate with Azure AD, and provide some guidance.</span></span>

* [<span data-ttu-id="b516a-160">決定要使用的 Active Directory</span><span class="sxs-lookup"><span data-stu-id="b516a-160">Determining which Active Directory to use</span></span>](active-directory-administer.md)
* [<span data-ttu-id="b516a-161">使用 Azure 應用程式資源庫中的應用程式</span><span class="sxs-lookup"><span data-stu-id="b516a-161">Using applications in the Azure application gallery</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b516a-162">整合 SaaS 應用程式教學課程清單</span><span class="sxs-lookup"><span data-stu-id="b516a-162">Integrating SaaS applications tutorials list</span></span>](active-directory-saas-tutorial-list.md)

## <a name="managing-access-to-applications"></a><span data-ttu-id="b516a-163">管理應用程式的存取</span><span class="sxs-lookup"><span data-stu-id="b516a-163">Managing access to applications</span></span>
<span data-ttu-id="b516a-164">下列文章描述使用 Azure AD 連接器和 Azure AD 將應用程式與 Azure AD 整合之後，您可以管理對應用程式的存取的方式。</span><span class="sxs-lookup"><span data-stu-id="b516a-164">The following articles describe ways you can manage access to applications once they have been integrated with Azure AD using Azure AD Connectors and Azure AD.</span></span>

* [<span data-ttu-id="b516a-165">使用 Azure AD 管理應用程式的存取</span><span class="sxs-lookup"><span data-stu-id="b516a-165">Managing access to apps using Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="b516a-166">使用 Azure AD 連接器自動化</span><span class="sxs-lookup"><span data-stu-id="b516a-166">Automating with Azure AD Connectors</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="b516a-167">將使用者指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="b516a-167">Assigning users to an application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)
* [<span data-ttu-id="b516a-168">將群組指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="b516a-168">Assigning groups to an application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)
* [<span data-ttu-id="b516a-169">共用帳戶</span><span class="sxs-lookup"><span data-stu-id="b516a-169">Sharing accounts</span></span>](active-directory-sharing-accounts.md)

## <a name="integrating-custom-applications"></a><span data-ttu-id="b516a-170">整合自訂應用程式</span><span class="sxs-lookup"><span data-stu-id="b516a-170">Integrating custom applications</span></span>
<span data-ttu-id="b516a-171">如果您正在撰寫新的應用程式，並想要協助開發人員運用 Azure AD 的強大功能，請參閱 [引導開發人員](active-directory-applications-guiding-developers-for-lob-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="b516a-171">If you are writing a new application and want to assist developers in leveraging the power Azure AD, see [Guiding developers](active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="b516a-172">如果您想要加入您的自訂應用程式至 Azure 應用程式資源庫，請參閱 [使用 Azure AD 自助 SAML 組態「自備應用程式」](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b516a-172">If you want to add your custom application to the Azure Application Gallery, see [“Bring your own app” with Azure AD Self-Service SAML configuration](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="b516a-173">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b516a-173">See also</span></span>
* [<span data-ttu-id="b516a-174">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="b516a-174">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

