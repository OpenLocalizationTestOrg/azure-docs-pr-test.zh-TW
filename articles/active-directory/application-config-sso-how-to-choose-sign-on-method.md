---
title: "aaaHow toodetermine 哪些單一登入方法 toouse |Microsoft 文件"
description: "了解 hello 單一登入模式支援的 Azure AD 和如何針對哪一個 toochoose hello 應用程式的 toopick 您感興趣。"
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
ms.openlocfilehash: 64f0bc1dc8281d1ab8222fd50eaceaf710704886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetermine-what-single-sign-on-method-toouse"></a><span data-ttu-id="dcf92-103">如何 toodetermine 哪些單一登入方法 toouse</span><span class="sxs-lookup"><span data-stu-id="dcf92-103">How toodetermine what single-sign on method toouse</span></span>

<span data-ttu-id="dcf92-104">本文將協助您 toounderstand hello 單一登入模式支援的 Azure AD 和如何針對哪一個 toochoose hello 應用程式的 toopick 您感興趣。</span><span class="sxs-lookup"><span data-stu-id="dcf92-104">This article help you toounderstand hello single sign-on modes supported by Azure AD and how toopick which one toochoose for hello application you are interested in.</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="dcf92-105">特定應用程式類型所支援的單一登入和佈建模式</span><span class="sxs-lookup"><span data-stu-id="dcf92-105">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="dcf92-106">hello 下表描述 hello 不同單一登入和佈建 hello 上方的應用程式類型的每個支援的模式。</span><span class="sxs-lookup"><span data-stu-id="dcf92-106">hello table below describes hello different single sign-on and provisioning modes supported by each of hello above application types.</span></span> <span data-ttu-id="dcf92-107">您可以使用此資料表 toohelp 您 toounderstand 哪一個應用程式需要 tooadd toosupport 特定的目標。</span><span class="sxs-lookup"><span data-stu-id="dcf92-107">You can use this table toohelp you toounderstand which application you need tooadd toosupport a specific goal.</span></span>

  ![應用程式類型表格](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a><span data-ttu-id="dcf92-109">如何 toochoose 單一登入模式</span><span class="sxs-lookup"><span data-stu-id="dcf92-109">How toochoose a single sign-on mode</span></span>

<span data-ttu-id="dcf92-110">支援的 hello**單一登入**以下列出 Azure AD 應用程式模式。</span><span class="sxs-lookup"><span data-stu-id="dcf92-110">hello supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="dcf92-111">**Azure AD 單一登入已停用**– 選擇 Azure AD 單一登入已停用**單一登入模式**您是否尚未準備 toointegrate 搭配單一登入 Azure AD，與此應用程式或只測試它</span><span class="sxs-lookup"><span data-stu-id="dcf92-111">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready toointegrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="dcf92-112">**登入連結**– 選擇 hello[連結登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)**單一登入模式**如果您使用現有單一登入的方案，已連線的應用程式，或者如果您只想toopublish 簡單連結為您的使用者在其[應用程式存取面板](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)或[Office 365 應用程式啟動器](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="dcf92-112">**Linked Sign-on** – choose hello [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want toopublish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="dcf92-113">**密碼型登入**– 選擇 hello[密碼式登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)**單一登入模式**如果您的應用程式呈現 HTML 使用者名稱和密碼欄位，而且您想 toostore，使用者名稱和密碼安全地 toobe 重新執行 toohello 應用程式更新版本</span><span class="sxs-lookup"><span data-stu-id="dcf92-113">**Password-based Sign-on** – choose hello [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want toostore that username and password securely toobe replayed toohello application later</span></span>

-   <span data-ttu-id="dcf92-114">**SAML 型登入**– 選擇 hello [SAML 型登入](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)基礎的單一登入模式，如果您的應用程式支援 hello SAML 或 OpenID Connect 通訊協定，或您要讓 toobe 無法 toomap 使用者 toospecific 應用程式角色在 規則定義在您的 SAML 宣告*(**附註：** 此選項時，無法使用 hello 應用程式 proxy 已針對應用程式) *</span><span class="sxs-lookup"><span data-stu-id="dcf92-114">**SAML-based Sign-on** – choose hello [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports hello SAML or OpenID Connect protocols, or you want toobe able toomap users toospecific application roles based on rules you define in your SAML claims *(**Note:** this option is not available when hello application proxy is configured for an application)*</span></span>

-   <span data-ttu-id="dcf92-115">**標頭型登入**– 請選擇此選項[標頭型登入](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad)單一登入模式如果您使用支援 HTTP 標頭的 PingAccess 的應用程式以您想 tooperform 單一登入太的驗證*(**附註：** hello 應用程式 proxy 與 PingAccess 已針對應用程式時，才可用這個選項) *</span><span class="sxs-lookup"><span data-stu-id="dcf92-115">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish tooperform single-sign on too*(**Note:** this option is only available when hello application proxy and PingAccess is configured for an application)*</span></span>

-   <span data-ttu-id="dcf92-116">**整合式 Windows 驗證**– 選擇 hello[整合式 Windows 驗證](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)單一登入模式公開您希望 tooperform 單一登入太內部 WIA 應用程式時*(**附註：** hello 應用程式 proxy 已針對應用程式時，才可用這個選項) *</span><span class="sxs-lookup"><span data-stu-id="dcf92-116">**Integrated Windows Authentication** – choose hello [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish tooperform single-sign on too*(**Note:** this option is only available when hello application proxy is configured for an application)*</span></span>

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="dcf92-117">自訂開發之應用程式的單一登入模式</span><span class="sxs-lookup"><span data-stu-id="dcf92-117">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="dcf92-118">您可以透過 hello 開發的自訂應用程式[自訂開發的應用程式](#_Custom-Developed_Applications)經驗也支援其他單一登入模式以上未列出。</span><span class="sxs-lookup"><span data-stu-id="dcf92-118">Applications you have custom developed through hello [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="dcf92-119">其中包含：</span><span class="sxs-lookup"><span data-stu-id="dcf92-119">These include:</span></span>

-   <span data-ttu-id="dcf92-120">以 [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="dcf92-120">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="dcf92-121">以 [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="dcf92-121">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="dcf92-122">以 [WS-同盟 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="dcf92-122">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="dcf92-123">以 [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) 為基礎的登入</span><span class="sxs-lookup"><span data-stu-id="dcf92-123">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="dcf92-124">讀取 hello [Azure Active Directory 開發人員手冊 》](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn 深入了解如何支援這些 toocreate 自訂開發應用程式的單一登入模式。</span><span class="sxs-lookup"><span data-stu-id="dcf92-124">Read hello [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn more about how toocreate a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-tooset-an-applications-single-sign-on-mode"></a><span data-ttu-id="dcf92-125">如何 tooset 應用程式的單一登入模式</span><span class="sxs-lookup"><span data-stu-id="dcf92-125">How tooset an application’s single sign-on mode</span></span>

<span data-ttu-id="dcf92-126">tooset 應用程式的**單一登入**模式中，遵循下方的 hello 指示：</span><span class="sxs-lookup"><span data-stu-id="dcf92-126">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="dcf92-127">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="dcf92-127">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="dcf92-128">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="dcf92-128">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dcf92-129">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="dcf92-129">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dcf92-130">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="dcf92-130">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dcf92-131">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="dcf92-131">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="dcf92-132">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="dcf92-132">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="dcf92-133">選取您想 tooconfigure 單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="dcf92-133">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="dcf92-134">一旦 hello 應用程式載入時，按一下 **單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="dcf92-134">Once hello application loads, click **Single sign-on** from hello application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcf92-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dcf92-135">Next steps</span></span>
[<span data-ttu-id="dcf92-136">提供單一登入 tooyour 應用程式與應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="dcf92-136">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

