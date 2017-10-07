---
title: "哪一個應用程式加入應用程式時，請輸入 toouse aaaHow toochoose |Microsoft 文件"
description: "了解支援的 hello 類型，您可以使用 Azure AD 整合的應用程式及其相關的組態選項"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 46e3672e7f5048b0fa54171f0fc169362c9d5ac6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a><span data-ttu-id="d5521-103">如何新增應用程式時，哪一個應用程式輸入 toouse toochoose</span><span class="sxs-lookup"><span data-stu-id="d5521-103">How toochoose which application type toouse when adding an application</span></span>

<span data-ttu-id="d5521-104">這篇文章可協助您 toounderstand hello 四種主要類型的應用程式，您可以使用 Azure AD 整合：</span><span class="sxs-lookup"><span data-stu-id="d5521-104">This article help you toounderstand hello four main types of applications you can integrate with Azure AD:</span></span>

* <span data-ttu-id="d5521-105">每一項支援的功能</span><span class="sxs-lookup"><span data-stu-id="d5521-105">What is supported by each of them</span></span>
* <span data-ttu-id="d5521-106">您可能選擇哪個應用程式的理由</span><span class="sxs-lookup"><span data-stu-id="d5521-106">Why you might choose which application</span></span>
* <span data-ttu-id="d5521-107">如何 tooconfigure 這些應用程式的核心屬性，例如使用者的方式**佈建**，到底**單一登入**技術 toouse。</span><span class="sxs-lookup"><span data-stu-id="d5521-107">How tooconfigure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology toouse.</span></span>

## <a name="supported-application-types-in-azure-ad"></a><span data-ttu-id="d5521-108">Azure AD 中支援的應用程式類型</span><span class="sxs-lookup"><span data-stu-id="d5521-108">Supported application types in Azure AD</span></span>

<span data-ttu-id="d5521-109">Azure AD 支援四種主要的應用程式類型，您可以使用新增 hello**新增**功能下找到**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d5521-109">Azure AD supports four main application types that you can add using hello **Add** feature found under **Enterprise Applications**.</span></span> <span data-ttu-id="d5521-110">其中包含：</span><span class="sxs-lookup"><span data-stu-id="d5521-110">These include:</span></span>

-   <span data-ttu-id="d5521-111">**Azure AD 資源庫應用程式** – 與 Azure AD 預先整合以啟用單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5521-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

-   <span data-ttu-id="d5521-112">**應用程式 Proxy 應用程式**– 您想 tooprovide 安全單一登入 tooexternally 在內部部署環境中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5521-112">**Application Proxy Applications** – An application running in your on-premises environment that you want tooprovide secure single-sign on tooexternally.</span></span>

-   <span data-ttu-id="d5521-113">**自訂開發的應用程式**– 的應用程式，您的組織希望 toodevelop 上 hello Azure AD 應用程式開發平台，但所可能尚不存在。</span><span class="sxs-lookup"><span data-stu-id="d5521-113">**Custom-developed Applications** – An application that your organization wishes toodevelop on hello Azure AD Application Development Platform, but that may not exist yet.</span></span>

-   <span data-ttu-id="d5521-114">**不在資源庫內的應用程式** – 引進您自己的應用程式！</span><span class="sxs-lookup"><span data-stu-id="d5521-114">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="d5521-115">您想，任何網頁連結或呈現使用者名稱和密碼欄位中，任何應用程式支援 SAML 或 OpenID Connect 通訊協定，或支援您想進行單一登入 Azure AD 與 toointegrate SCIM。</span><span class="sxs-lookup"><span data-stu-id="d5521-115">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish toointegrate for single sign-on with Azure AD.</span></span>

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a><span data-ttu-id="d5521-116">功能和所有 hello 上方的應用程式類型所支援的功能</span><span class="sxs-lookup"><span data-stu-id="d5521-116">Features and capabilities supported by all hello above application types</span></span>

<span data-ttu-id="d5521-117">hello 支援下列功能是由任何 hello 上方 4 應用程式類型在 Azure AD 中：</span><span class="sxs-lookup"><span data-stu-id="d5521-117">hello following features are supported by any of hello above 4 application types in Azure AD:</span></span>

-   <span data-ttu-id="d5521-118">**快速啟動** – 依照[簡單部署步驟](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)快速開始使用應用程式</span><span class="sxs-lookup"><span data-stu-id="d5521-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span></span>

-   <span data-ttu-id="d5521-119">**一般屬性管理**– 取得[直接深層連結](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users)tooan 應用程式，[自訂商標 hello](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal)應用程式，或[停用 hello 應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal)所有使用者。</span><span class="sxs-lookup"><span data-stu-id="d5521-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) tooan application, [customize hello branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable hello application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span></span>

-   <span data-ttu-id="d5521-120">**使用者和群組管理**–[指派](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)或[移除](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal)使用者和群組的 tooan 應用程式，以及選擇性地指派 hello 特定應用程式角色，而這些使用者和群組具有存取權</span><span class="sxs-lookup"><span data-stu-id="d5521-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups tooan application, and optionally assign hello specific application roles these users and groups have access to</span></span>

-   <span data-ttu-id="d5521-121">**自助式應用程式存取**– 啟用使用者 toorequest[自助式應用程式存取](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)tooan 應用程式從其應用程式存取面板藉由直接新增應用程式或[聯結自助服務啟用的群組](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management)，選擇性地需要 business 核准沿著 hello 方法</span><span class="sxs-lookup"><span data-stu-id="d5521-121">**Self-service application access** – enable your users toorequest [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooan application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along hello way</span></span>

-   <span data-ttu-id="d5521-122">**單一登入**– 請參閱[所有 hello 登入 tooan 應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins)，或您的應用程式</span><span class="sxs-lookup"><span data-stu-id="d5521-122">**Sign-in logs** – see [all hello sign-ins tooan application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span></span>

-   <span data-ttu-id="d5521-123">**稽核記錄檔**– 請參閱[詳細的稽核記錄檔的修改 tooan 應用程式的相關](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs)，tooall 或您的應用程式</span><span class="sxs-lookup"><span data-stu-id="d5521-123">**Audit logs** – see [detailed audit logs about modifications tooan application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or tooall your applications</span></span>

-   <span data-ttu-id="d5521-124">**條件式和風險型存取**– 強大設定[條件式存取規則](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)當使用者嘗試 toosign tooa 特定應用程式中的時，會強制執行</span><span class="sxs-lookup"><span data-stu-id="d5521-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt toosign in tooa specific application</span></span>

-   <span data-ttu-id="d5521-125">**權限檢視**– 檢視任何 hello [OAuth2 權限](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)應用程式具有存取 tooin 目錄從單一位置</span><span class="sxs-lookup"><span data-stu-id="d5521-125">**Permissions view** – view any of hello [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access tooin your directory from a single place</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="d5521-126">特定應用程式類型所支援的單一登入和佈建模式</span><span class="sxs-lookup"><span data-stu-id="d5521-126">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="d5521-127">hello 下表描述 hello 不同單一登入和佈建 hello 上方的應用程式類型的每個支援的模式。</span><span class="sxs-lookup"><span data-stu-id="d5521-127">hello table below describes hello different single sign-on and provisioning modes supported by each of hello above application types.</span></span> <span data-ttu-id="d5521-128">您可以使用此資料表 toohelp 您 toounderstand 哪一個應用程式需要 tooadd toosupport 特定的目標。</span><span class="sxs-lookup"><span data-stu-id="d5521-128">You can use this table toohelp you toounderstand which application you need tooadd toosupport a specific goal.</span></span>

  ![應用程式類型表格](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a><span data-ttu-id="d5521-130">如何 toochoose 單一登入模式</span><span class="sxs-lookup"><span data-stu-id="d5521-130">How toochoose a single sign-on mode</span></span>

<span data-ttu-id="d5521-131">支援的 hello**單一登入**以下列出 Azure AD 應用程式模式。</span><span class="sxs-lookup"><span data-stu-id="d5521-131">hello supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="d5521-132">**Azure AD 單一登入已停用**– 選擇 Azure AD 單一登入已停用**單一登入模式**您是否尚未準備 toointegrate 搭配單一登入 Azure AD，與此應用程式或只測試它</span><span class="sxs-lookup"><span data-stu-id="d5521-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready toointegrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="d5521-133">**登入連結**– 選擇 hello[連結登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)**單一登入模式**如果您使用現有單一登入的方案，已連線的應用程式，或者如果您只想toopublish 簡單連結為您的使用者在其[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)或[Office 365 應用程式啟動器](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="d5521-133">**Linked Sign-on** – choose hello [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want toopublish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="d5521-134">**密碼型登入**– 選擇 hello[密碼式登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)**單一登入模式**如果您的應用程式呈現 HTML 使用者名稱和密碼欄位，而且您想 toostore，使用者名稱和密碼安全地 toobe 重新執行 toohello 應用程式更新版本</span><span class="sxs-lookup"><span data-stu-id="d5521-134">**Password-based Sign-on** – choose hello [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want toostore that username and password securely toobe replayed toohello application later</span></span>

-   <span data-ttu-id="d5521-135">**SAML 型登入**– 選擇 hello [SAML 型登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)基礎的單一登入模式，如果您的應用程式支援 hello SAML 或 OpenID Connect 通訊協定，或您要讓 toobe 無法 toomap 使用者 toospecific 應用程式角色在 規則定義在您的 SAML 宣告 *</span><span class="sxs-lookup"><span data-stu-id="d5521-135">**SAML-based Sign-on** – choose hello [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports hello SAML or OpenID Connect protocols, or you want toobe able toomap users toospecific application roles based on rules you define in your SAML claims *</span></span>

   >[!NOTE]
   ><span data-ttu-id="d5521-136">Hello 應用程式 proxy 已針對應用程式時，不使用此選項。</span><span class="sxs-lookup"><span data-stu-id="d5521-136">This option is not available when hello application proxy is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="d5521-137">**標頭型登入**– 請選擇此選項[標頭型登入](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad)單一登入模式如果您使用支援 HTTP 標頭的 PingAccess 的應用程式以您想 tooperform 單一登入太的驗證</span><span class="sxs-lookup"><span data-stu-id="d5521-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish tooperform single-sign on too</span></span>

   >[!NOTE]
   ><span data-ttu-id="d5521-138">Hello 應用程式 proxy 與 PingAccess 設定應用程式時，才可用這個選項。</span><span class="sxs-lookup"><span data-stu-id="d5521-138">This option is only available when hello application proxy and PingAccess is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="d5521-139">**整合式 Windows 驗證**– 選擇 hello[整合式 Windows 驗證](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)單一登入模式公開您希望 tooperform 單一登入太內部 WIA 應用程式時</span><span class="sxs-lookup"><span data-stu-id="d5521-139">**Integrated Windows Authentication** – choose hello [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish tooperform single-sign on too</span></span>

   >[!NOTE]
   ><span data-ttu-id="d5521-140">Hello 應用程式 proxy 設定的應用程式時，才可用這個選項。</span><span class="sxs-lookup"><span data-stu-id="d5521-140">This option is only available when hello application proxy is configured for an application.</span></span>
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="d5521-141">自訂開發之應用程式的單一登入模式</span><span class="sxs-lookup"><span data-stu-id="d5521-141">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="d5521-142">您可以透過 hello 開發的自訂應用程式[自訂開發的應用程式](#_Custom-Developed_Applications)經驗也支援其他單一登入模式以上未列出。</span><span class="sxs-lookup"><span data-stu-id="d5521-142">Applications you have custom developed through hello [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="d5521-143">其中包含：</span><span class="sxs-lookup"><span data-stu-id="d5521-143">These include:</span></span>

-   <span data-ttu-id="d5521-144">以 [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="d5521-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="d5521-145">以 [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="d5521-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="d5521-146">以 [WS-同盟 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="d5521-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="d5521-147">以 [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="d5521-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="d5521-148">讀取 hello [Azure Active Directory 開發人員手冊 》](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn 深入了解如何支援這些 toocreate 自訂開發應用程式的單一登入模式。</span><span class="sxs-lookup"><span data-stu-id="d5521-148">Read hello [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn more about how toocreate a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-tooset-an-applications-single-sign-on-mode"></a><span data-ttu-id="d5521-149">如何 tooset 應用程式的單一登入模式</span><span class="sxs-lookup"><span data-stu-id="d5521-149">How tooset an application’s single sign-on mode</span></span>

<span data-ttu-id="d5521-150">tooset 應用程式的**單一登入**模式中，遵循下方的 hello 指示：</span><span class="sxs-lookup"><span data-stu-id="d5521-150">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="d5521-151">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="d5521-151">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d5521-152">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="d5521-152">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d5521-153">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="d5521-153">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d5521-154">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="d5521-154">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d5521-155">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="d5521-155">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d5521-156">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="d5521-156">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d5521-157">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5521-157">Select hello application for which you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d5521-158">一旦 hello 應用程式載入時，按一下 **單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="d5521-158">Once hello application loads, click **Single sign-on** from hello application’s left hand navigation menu.</span></span>

## <a name="how-toochoose-a-provisioning-mode"></a><span data-ttu-id="d5521-159">如何 toochoose 佈建模式</span><span class="sxs-lookup"><span data-stu-id="d5521-159">How toochoose a provisioning mode</span></span>

-   <span data-ttu-id="d5521-160">**手動佈建**– 選擇 hello[手動](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes)佈建模式，如果您有現有的帳戶，或想 toomanage 此應用程式之外的 Azure AD 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5521-160">**Manual Provisioning** – choose hello [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish toomanage accounts for this application outside of Azure AD.</span></span>

-   <span data-ttu-id="d5521-161">**自動佈建**– 選擇 hello[自動](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning)**佈建模式**如果您想 tooenable 自動 API 為基礎的佈建及/或取消佈建使用者帳戶 toothis應用程式</span><span class="sxs-lookup"><span data-stu-id="d5521-161">**Automatic Provisioning** – choose hello [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want tooenable automatic API-based provisioning and/or de-provisioning of user accounts toothis application</span></span> 

   >[!NOTE]
   ><span data-ttu-id="d5521-162">這個選項是僅適用於應用程式內 hello**精選**分類的 hello [Azure AD 應用程式庫](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery)。</span><span class="sxs-lookup"><span data-stu-id="d5521-162">This option is available only for applications within hello **featured** category of hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span></span>
   >
   >

-   <span data-ttu-id="d5521-163">**SCIM 為基礎的自動佈建**– 使用[SCIM 為基礎的自動佈建](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning)您的應用程式是否支援偵測變更 toousers 和群組，變更會自動發出 hello SCIM 通訊協定tooany 應用程式與 Azure AD 整合</span><span class="sxs-lookup"><span data-stu-id="d5521-163">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports hello SCIM protocol for detecting changes toousers and groups, which are automatically emitted for changes tooany application integrated with Azure AD</span></span> 

   >[!NOTE]
   ><span data-ttu-id="d5521-164">此選項未列為特定的佈建模式，但對於所有與 Azure AD 整合的應用程式，依預設會啟用。</span><span class="sxs-lookup"><span data-stu-id="d5521-164">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span></span>
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a><span data-ttu-id="d5521-165">如何 tooset 應用程式的佈建模式</span><span class="sxs-lookup"><span data-stu-id="d5521-165">How tooset an application’s provisioning mode</span></span>

<span data-ttu-id="d5521-166">tooset 應用程式的**佈建**模式中，遵循下方的 hello 指示：</span><span class="sxs-lookup"><span data-stu-id="d5521-166">tooset an application’s **provisioning** mode, follow hello instructions below:</span></span>

<span data-ttu-id="d5521-167">tooset 應用程式的**單一登入**模式中，遵循下方的 hello 指示：</span><span class="sxs-lookup"><span data-stu-id="d5521-167">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="d5521-168">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="d5521-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d5521-169">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="d5521-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d5521-170">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="d5521-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d5521-171">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="d5521-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d5521-172">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="d5521-172">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d5521-173">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="d5521-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d5521-174">選取您要為其 tooconfigure 佈建的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5521-174">Select hello application for which you want tooconfigure provisioning.</span></span>

7.  <span data-ttu-id="d5521-175">一旦 hello 應用程式載入時，按一下 **佈建**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="d5521-175">Once hello application loads, click **Provisioning** from hello application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5521-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d5521-176">Next steps</span></span>
[<span data-ttu-id="d5521-177">使用 Azure Active Directory 管理應用程式</span><span class="sxs-lookup"><span data-stu-id="d5521-177">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
