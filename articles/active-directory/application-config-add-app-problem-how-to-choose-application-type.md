---
title: "新增應用程式時如何選擇要使用的應用程式類型 | Microsoft Docs"
description: "了解支援與 Azure AD 整合的應用程式類型及其相關的設定選項"
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
ms.openlocfilehash: e0d41d1933531c2c633613bcbc1bbcbf075d6a69
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-choose-which-application-type-to-use-when-adding-an-application"></a><span data-ttu-id="e7862-103">新增應用程式時如何選擇要使用的應用程式類型</span><span class="sxs-lookup"><span data-stu-id="e7862-103">How to choose which application type to use when adding an application</span></span>

<span data-ttu-id="e7862-104">本文協助您了解可以與 Azure AD 整合的四種主要的應用程式類型︰</span><span class="sxs-lookup"><span data-stu-id="e7862-104">This article help you to understand the four main types of applications you can integrate with Azure AD:</span></span>

* <span data-ttu-id="e7862-105">每一項支援的功能</span><span class="sxs-lookup"><span data-stu-id="e7862-105">What is supported by each of them</span></span>
* <span data-ttu-id="e7862-106">您可能選擇哪個應用程式的理由</span><span class="sxs-lookup"><span data-stu-id="e7862-106">Why you might choose which application</span></span>
* <span data-ttu-id="e7862-107">如何設定這些應用程式的核心屬性，像是如何**佈建**使用者，或使用何種**單一登入**技術。</span><span class="sxs-lookup"><span data-stu-id="e7862-107">How to configure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology to use.</span></span>

## <a name="supported-application-types-in-azure-ad"></a><span data-ttu-id="e7862-108">Azure AD 中支援的應用程式類型</span><span class="sxs-lookup"><span data-stu-id="e7862-108">Supported application types in Azure AD</span></span>

<span data-ttu-id="e7862-109">Azure AD 支援四種主要的應用程式類型，您可以使用 [企業應用程式]下的 [新增] 功能新增這幾種類型。</span><span class="sxs-lookup"><span data-stu-id="e7862-109">Azure AD supports four main application types that you can add using the **Add** feature found under **Enterprise Applications**.</span></span> <span data-ttu-id="e7862-110">其中包含：</span><span class="sxs-lookup"><span data-stu-id="e7862-110">These include:</span></span>

-   <span data-ttu-id="e7862-111">**Azure AD 資源庫應用程式** – 與 Azure AD 預先整合以啟用單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7862-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

-   <span data-ttu-id="e7862-112">**應用程式 Proxy** – 您想要提供從對外進行安全單一登入的應用程式 (在內部部署環境中執行)。</span><span class="sxs-lookup"><span data-stu-id="e7862-112">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

-   <span data-ttu-id="e7862-113">**自訂開發的應用程式** – 您的組織想要在 Azure AD 應用程式開發平台上開發的應用程式，但可能尚不存在。</span><span class="sxs-lookup"><span data-stu-id="e7862-113">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

-   <span data-ttu-id="e7862-114">**不在資源庫內的應用程式** – 引進您自己的應用程式！</span><span class="sxs-lookup"><span data-stu-id="e7862-114">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="e7862-115">您想要的任何網頁連結，或任何呈現使用者名稱和密碼欄位的應用程式，都支援 SAML 或 OpenID Connect 通訊協定，或支援您想要與 Azure AD 整合以啟用單一登入的 SCIM。</span><span class="sxs-lookup"><span data-stu-id="e7862-115">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

## <a name="features-and-capabilities-supported-by-all-the-above-application-types"></a><span data-ttu-id="e7862-116">上述所有應用程式類型所支援的功能</span><span class="sxs-lookup"><span data-stu-id="e7862-116">Features and capabilities supported by all the above application types</span></span>

<span data-ttu-id="e7862-117">在 Azure AD 中，上述 4 種應用程式類型都支援下列功能︰</span><span class="sxs-lookup"><span data-stu-id="e7862-117">The following features are supported by any of the above 4 application types in Azure AD:</span></span>

-   <span data-ttu-id="e7862-118">**快速啟動** – 依照[簡單部署步驟](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)快速開始使用應用程式</span><span class="sxs-lookup"><span data-stu-id="e7862-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span></span>

-   <span data-ttu-id="e7862-119">**一般屬性管理** – 取得應用程式的[直接深層連結](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users)、為應用程式[自訂商標](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal)或對所有使用者[停用應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="e7862-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) to an application, [customize the branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable the application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span></span>

-   <span data-ttu-id="e7862-120">**使用者和群組管理** – 針對應用程式[指派](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)或[移除](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal)使用者和群組，並選擇性地指派這些使用者和群組可存取的特定應用程式角色</span><span class="sxs-lookup"><span data-stu-id="e7862-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups to an application, and optionally assign the specific application roles these users and groups have access to</span></span>

-   <span data-ttu-id="e7862-121">**自助應用程式存取** – 可讓您的使用者從應用程式存取面板直接新增應用程式，或[加入自助啟用的群組](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) (過程中可選擇需要商務核准)，以要求應用程式的[自助應用程式存取](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)</span><span class="sxs-lookup"><span data-stu-id="e7862-121">**Self-service application access** – enable your users to request [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to an application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along the way</span></span>

-   <span data-ttu-id="e7862-122">**單一登入** – 請參閱[應用程式的所有登入](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins)(或您的所有應用程式)</span><span class="sxs-lookup"><span data-stu-id="e7862-122">**Sign-in logs** – see [all the sign-ins to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span></span>

-   <span data-ttu-id="e7862-123">**稽核記錄** – 請參閱[有關應用程式修改的詳細稽核記錄](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) (或您的所有應用程式)</span><span class="sxs-lookup"><span data-stu-id="e7862-123">**Audit logs** – see [detailed audit logs about modifications to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or to all your applications</span></span>

-   <span data-ttu-id="e7862-124">**條件式和以風險為基礎的存取** – 設定強大的[條件式存取規則](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)，在使用者嘗試登入特定的應用程式時強制執行</span><span class="sxs-lookup"><span data-stu-id="e7862-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt to sign in to a specific application</span></span>

-   <span data-ttu-id="e7862-125">**權限檢視** – 從單一位置檢視應用程式在您的目錄中可存取的任何 [OAuth2 權限](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)</span><span class="sxs-lookup"><span data-stu-id="e7862-125">**Permissions view** – view any of the [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access to in your directory from a single place</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="e7862-126">特定應用程式類型所支援的單一登入和佈建模式</span><span class="sxs-lookup"><span data-stu-id="e7862-126">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="e7862-127">下表描述以上每個應用程式類型所支援的不同單一登入和佈建模式。</span><span class="sxs-lookup"><span data-stu-id="e7862-127">The table below describes the different single sign-on and provisioning modes supported by each of the above application types.</span></span> <span data-ttu-id="e7862-128">請利用此表格，協助您了解需要新增哪個應用程式以支援特定目標。</span><span class="sxs-lookup"><span data-stu-id="e7862-128">You can use this table to help you to understand which application you need to add to support a specific goal.</span></span>

  ![應用程式類型表格](./media/application-tables/table1.png)

## <a name="how-to-choose-a-single-sign-on-mode"></a><span data-ttu-id="e7862-130">如何選擇單一登入模式</span><span class="sxs-lookup"><span data-stu-id="e7862-130">How to choose a single sign-on mode</span></span>

<span data-ttu-id="e7862-131">以下列出 Azure AD 應用程式支援的**單一登入**模式。</span><span class="sxs-lookup"><span data-stu-id="e7862-131">The supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="e7862-132">**Azure AD 單一登入已停用** – 如果您還沒有準備好整合此應用程式與 Azure AD 的單一登入，或只是要測試，請選擇 Azure AD 單一登入已停用**單一登入模式**</span><span class="sxs-lookup"><span data-stu-id="e7862-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="e7862-133">**連結的登入** – 如果您的應用程式已連線至現有的單一登入解決方案，或您只是想要在使用者的[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)或 [Office 365 應用程式啟動程式](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)中發佈簡單連結，請選擇[連結的登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)**單一登入模式**</span><span class="sxs-lookup"><span data-stu-id="e7862-133">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="e7862-134">**以密碼為基礎的登入** – 如果您的應用程式呈現 HTML 使用者名稱和密碼欄位，而且您想要安全地儲存該使用者名稱和密碼，以便稍後重播給應用程式，請選擇[以密碼為基礎的登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)**單一登入模式**</span><span class="sxs-lookup"><span data-stu-id="e7862-134">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span></span>

-   <span data-ttu-id="e7862-135">**以 SAML 為基礎的登入** – 如果您的應用程式支援 SAML 或 OpenID Connect 通訊協定，或想要根據您在 SAML 宣告中定義的規則，將使用者對應至特定的應用程式角色，請選擇[以 SAML 為基礎的登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)單一登入模式 *</span><span class="sxs-lookup"><span data-stu-id="e7862-135">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims *</span></span>

   >[!NOTE]
   ><span data-ttu-id="e7862-136">已設定應用程式的應用程式 Proxy 時，無法使用此選項。</span><span class="sxs-lookup"><span data-stu-id="e7862-136">This option is not available when the application proxy is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="e7862-137">**以標頭為基礎的登入** – 如果有您想要執行單一登入的應用程式，且它使用的 PingAccess 支援以 HTTP 標頭為基礎的驗證 ，請選擇這個[以標頭為基礎的登入](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad)單一登入模式</span><span class="sxs-lookup"><span data-stu-id="e7862-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="e7862-138">只有在已設定應用程式的應用程式 Proxy 和 PingAccess 時，才能使用此選項。</span><span class="sxs-lookup"><span data-stu-id="e7862-138">This option is only available when the application proxy and PingAccess is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="e7862-139">**整合式 Windows 驗證** – 當公開您想要執行單一登入的內部部署 WIA 應用程式時，請選擇[整合式 Windows 驗證](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)單一登入模式</span><span class="sxs-lookup"><span data-stu-id="e7862-139">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="e7862-140">只有在已設定應用程式的應用程式 Proxy 時，才能使用此選項。</span><span class="sxs-lookup"><span data-stu-id="e7862-140">This option is only available when the application proxy is configured for an application.</span></span>
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="e7862-141">自訂開發之應用程式的單一登入模式</span><span class="sxs-lookup"><span data-stu-id="e7862-141">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="e7862-142">您透過[自訂開發的應用程式](#_Custom-Developed_Applications)經驗所自訂開發的應用程式，也支援以上未列出的其他單一登入模式。</span><span class="sxs-lookup"><span data-stu-id="e7862-142">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="e7862-143">其中包含：</span><span class="sxs-lookup"><span data-stu-id="e7862-143">These include:</span></span>

-   <span data-ttu-id="e7862-144">以 [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="e7862-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="e7862-145">以 [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="e7862-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="e7862-146">以 [WS-同盟 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="e7862-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="e7862-147">以 [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="e7862-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="e7862-148">請參閱 [Azure Active Directory 開發人員手冊](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)，以深入了解如何建立支援這些單一登入模式的自訂開發應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7862-148">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-to-set-an-applications-single-sign-on-mode"></a><span data-ttu-id="e7862-149">如何設定應用程式的單一登入模式</span><span class="sxs-lookup"><span data-stu-id="e7862-149">How to set an application’s single sign-on mode</span></span>

<span data-ttu-id="e7862-150">若要設定應用程式的**單一登入**模式，請遵循下列指示：</span><span class="sxs-lookup"><span data-stu-id="e7862-150">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="e7862-151">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**或 **共同管理員**身分登入</span><span class="sxs-lookup"><span data-stu-id="e7862-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e7862-152">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="e7862-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e7862-153">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="e7862-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e7862-154">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e7862-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e7862-155">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e7862-155">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="e7862-156">若在這裡沒看到您要的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e7862-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e7862-157">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7862-157">Select the application for which you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="e7862-158">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e7862-158">Once the application loads, click **Single sign-on** from the application’s left hand navigation menu.</span></span>

## <a name="how-to-choose-a-provisioning-mode"></a><span data-ttu-id="e7862-159">如何選擇佈建模式</span><span class="sxs-lookup"><span data-stu-id="e7862-159">How to choose a provisioning mode</span></span>

-   <span data-ttu-id="e7862-160">**手動佈建** – 如果您有現有的帳戶，或想要在 Azure AD 外部管理這個應用程式的帳戶，請選擇[手動](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes)佈建模式。</span><span class="sxs-lookup"><span data-stu-id="e7862-160">**Manual Provisioning** – choose the [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish to manage accounts for this application outside of Azure AD.</span></span>

-   <span data-ttu-id="e7862-161">**自動佈建** – 如果您想要啟用以 API 為基礎自動佈建和/或取消佈建此應用程式的使用者帳戶，請選擇[自動](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning)**佈建模式**</span><span class="sxs-lookup"><span data-stu-id="e7862-161">**Automatic Provisioning** – choose the [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want to enable automatic API-based provisioning and/or de-provisioning of user accounts to this application</span></span> 

   >[!NOTE]
   ><span data-ttu-id="e7862-162">此功能僅適用於 [Azure AD 應用程式庫](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery)的**精選**類別內的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7862-162">This option is available only for applications within the **featured** category of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span></span>
   >
   >

-   <span data-ttu-id="e7862-163">**以 SCIM 為基礎的自動佈建** – 如果您的應用程式支援 SCIM 通訊協定來偵測使用者和群組的變更 (與 Azure AD 整合的任何應用程式變更時會自動發出)，請使用[以 SCIM 為基礎的自動佈建](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning)</span><span class="sxs-lookup"><span data-stu-id="e7862-163">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports the SCIM protocol for detecting changes to users and groups, which are automatically emitted for changes to any application integrated with Azure AD</span></span> 

   >[!NOTE]
   ><span data-ttu-id="e7862-164">此選項未列為特定的佈建模式，但對於所有與 Azure AD 整合的應用程式，依預設會啟用。</span><span class="sxs-lookup"><span data-stu-id="e7862-164">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span></span>
   >
   >

## <a name="how-to-set-an-applications-provisioning-mode"></a><span data-ttu-id="e7862-165">如何設定應用程式的佈建模式</span><span class="sxs-lookup"><span data-stu-id="e7862-165">How to set an application’s provisioning mode</span></span>

<span data-ttu-id="e7862-166">若要設定應用程式的**佈建**模式，請遵循下列指示：</span><span class="sxs-lookup"><span data-stu-id="e7862-166">To set an application’s **provisioning** mode, follow the instructions below:</span></span>

<span data-ttu-id="e7862-167">若要設定應用程式的**單一登入**模式，請遵循下列指示：</span><span class="sxs-lookup"><span data-stu-id="e7862-167">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="e7862-168">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**或 **共同管理員**身分登入</span><span class="sxs-lookup"><span data-stu-id="e7862-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e7862-169">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="e7862-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e7862-170">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="e7862-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e7862-171">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e7862-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e7862-172">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e7862-172">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="e7862-173">若在這裡沒看到您要的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e7862-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e7862-174">選取您要設定佈建的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e7862-174">Select the application for which you want to configure provisioning.</span></span>

7.  <span data-ttu-id="e7862-175">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [佈建]。</span><span class="sxs-lookup"><span data-stu-id="e7862-175">Once the application loads, click **Provisioning** from the application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7862-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7862-176">Next steps</span></span>
[<span data-ttu-id="e7862-177">使用 Azure Active Directory 管理應用程式</span><span class="sxs-lookup"><span data-stu-id="e7862-177">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
