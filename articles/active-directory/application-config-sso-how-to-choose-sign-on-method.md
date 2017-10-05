---
title: "如何決定要使用的單一登入方法 | Microsoft Docs"
description: "了解 Azure AD 支援的單一登入模式，以及如何為您感興趣的應用程式選擇何種模式。"
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
ms.openlocfilehash: 80f4a965920fec9cb578c1bee235c7857f37431e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-determine-what-single-sign-on-method-to-use"></a><span data-ttu-id="761b7-103">如何決定要使用的單一登入方法</span><span class="sxs-lookup"><span data-stu-id="761b7-103">How to determine what single-sign on method to use</span></span>

<span data-ttu-id="761b7-104">本文協助您了解 Azure AD 支援的單一登入模式，以及如何為您感興趣的應用程式選擇何種模式。</span><span class="sxs-lookup"><span data-stu-id="761b7-104">This article help you to understand the single sign-on modes supported by Azure AD and how to pick which one to choose for the application you are interested in.</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="761b7-105">特定應用程式類型所支援的單一登入和佈建模式</span><span class="sxs-lookup"><span data-stu-id="761b7-105">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="761b7-106">下表描述以上每個應用程式類型所支援的不同單一登入和佈建模式。</span><span class="sxs-lookup"><span data-stu-id="761b7-106">The table below describes the different single sign-on and provisioning modes supported by each of the above application types.</span></span> <span data-ttu-id="761b7-107">請利用此表格，協助您了解需要新增哪個應用程式以支援特定目標。</span><span class="sxs-lookup"><span data-stu-id="761b7-107">You can use this table to help you to understand which application you need to add to support a specific goal.</span></span>

  ![應用程式類型表格](./media/application-tables/table1.png)

## <a name="how-to-choose-a-single-sign-on-mode"></a><span data-ttu-id="761b7-109">如何選擇單一登入模式</span><span class="sxs-lookup"><span data-stu-id="761b7-109">How to choose a single sign-on mode</span></span>

<span data-ttu-id="761b7-110">以下列出 Azure AD 應用程式支援的**單一登入**模式。</span><span class="sxs-lookup"><span data-stu-id="761b7-110">The supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="761b7-111">**Azure AD 單一登入已停用** – 如果您還沒有準備好整合此應用程式與 Azure AD 的單一登入，或只是要測試，請選擇 Azure AD 單一登入已停用**單一登入模式**</span><span class="sxs-lookup"><span data-stu-id="761b7-111">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="761b7-112">**連結的登入** – 如果您的應用程式已連線至現有的單一登入解決方案，或您只是想要在使用者的[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)或 [Office 365 應用程式啟動程式](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)中發佈簡單連結，請選擇[連結的登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)**單一登入模式**</span><span class="sxs-lookup"><span data-stu-id="761b7-112">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="761b7-113">**以密碼為基礎的登入** – 如果您的應用程式呈現 HTML 使用者名稱和密碼欄位，而且您想要安全地儲存該使用者名稱和密碼，以便稍後重播給應用程式，請選擇[以密碼為基礎的登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)**單一登入模式**</span><span class="sxs-lookup"><span data-stu-id="761b7-113">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span></span>

-   <span data-ttu-id="761b7-114">**以 SAML 為基礎的登入** – 如果您的應用程式支援 SAML 或 OpenID Connect 通訊協定，或想要根據您在 SAML 宣告中定義的規則，將使用者對應至特定的應用程式角色，請選擇[以 SAML 為基礎的登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)單一登入模式 *(**附註：** 已設定應用程式的應用程式 Proxy 時，無法使用此選項)*</span><span class="sxs-lookup"><span data-stu-id="761b7-114">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims *(**Note:** this option is not available when the application proxy is configured for an application)*</span></span>

-   <span data-ttu-id="761b7-115">**以標頭為基礎的登入** – 如果有您想要執行單一登入的應用程式，且它使用的 PingAccess 支援以 HTTP 標頭為基礎的驗證 ，請選擇這個[以標頭為基礎的登入](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad)單一登入模式 *(**附註：** 只有在已設定應用程式的應用程式 Proxy 和 PingAccess 時，才能使用此選項)*</span><span class="sxs-lookup"><span data-stu-id="761b7-115">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish to perform single-sign on to *(**Note:** this option is only available when the application proxy and PingAccess is configured for an application)*</span></span>

-   <span data-ttu-id="761b7-116">**整合式 Windows 驗證** – 當公開您想要執行單一登入的內部部署 WIA 應用程式時，請選擇[整合式 Windows 驗證](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)單一登入模式 *(**附註：** 只有在已設定應用程式的應用程式 Proxy 時，才能使用此選項)*</span><span class="sxs-lookup"><span data-stu-id="761b7-116">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to *(**Note:** this option is only available when the application proxy is configured for an application)*</span></span>

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="761b7-117">自訂開發之應用程式的單一登入模式</span><span class="sxs-lookup"><span data-stu-id="761b7-117">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="761b7-118">您透過[自訂開發的應用程式](#_Custom-Developed_Applications)經驗所自訂開發的應用程式，也支援以上未列出的其他單一登入模式。</span><span class="sxs-lookup"><span data-stu-id="761b7-118">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="761b7-119">其中包含：</span><span class="sxs-lookup"><span data-stu-id="761b7-119">These include:</span></span>

-   <span data-ttu-id="761b7-120">以 [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="761b7-120">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="761b7-121">以 [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="761b7-121">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="761b7-122">以 [WS-同盟 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="761b7-122">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="761b7-123">以 [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="761b7-123">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="761b7-124">請參閱 [Azure Active Directory 開發人員手冊](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)，以深入了解如何建立支援這些單一登入模式的自訂開發應用程式。</span><span class="sxs-lookup"><span data-stu-id="761b7-124">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-to-set-an-applications-single-sign-on-mode"></a><span data-ttu-id="761b7-125">如何設定應用程式的單一登入模式</span><span class="sxs-lookup"><span data-stu-id="761b7-125">How to set an application’s single sign-on mode</span></span>

<span data-ttu-id="761b7-126">若要設定應用程式的**單一登入**模式，請遵循下列指示：</span><span class="sxs-lookup"><span data-stu-id="761b7-126">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="761b7-127">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**或 **共同管理員**身分登入</span><span class="sxs-lookup"><span data-stu-id="761b7-127">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="761b7-128">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="761b7-128">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="761b7-129">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="761b7-129">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="761b7-130">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="761b7-130">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="761b7-131">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="761b7-131">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="761b7-132">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="761b7-132">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="761b7-133">選取您要設定單一登入的應用程式</span><span class="sxs-lookup"><span data-stu-id="761b7-133">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="761b7-134">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="761b7-134">Once the application loads, click **Single sign-on** from the application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="761b7-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="761b7-135">Next steps</span></span>
[<span data-ttu-id="761b7-136">使用應用程式 Proxy 提供單一登入應用程式</span><span class="sxs-lookup"><span data-stu-id="761b7-136">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

