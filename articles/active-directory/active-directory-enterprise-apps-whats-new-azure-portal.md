---
title: "Azure Active Directory 中企業應用程式管理的新功能 | Microsoft Docs"
description: "了解 Azure Active Directory 中企業應用程式管理的新功能。"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
editor: 
ms.assetid: 34ac4028-a5aa-40d9-a93b-0db4e0abd793
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: asteen
ms.reviewer: asteen
ms.openlocfilehash: 0c32a6719292aa903aa32dfdc4a31114e7a28346
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="whats-new-in-enterprise-application-management-in-azure-active-directory"></a><span data-ttu-id="9ef93-103">Azure Active Directory 中企業應用程式管理的新功能</span><span class="sxs-lookup"><span data-stu-id="9ef93-103">What's new in Enterprise Application management in Azure Active Directory</span></span> 

<span data-ttu-id="9ef93-104">Azure Active Directory (Azure AD) 有增強的企業應用程式管理工具，其中有些新特性和功能可讓應用程式的管理變得更簡單且有效率。</span><span class="sxs-lookup"><span data-stu-id="9ef93-104">Azure Active Directory (Azure AD) has enhanced enterprise application management tools, with new features and capabilities to make managing apps simpler and efficient.</span></span>

<span data-ttu-id="9ef93-105">以下是 [Azure 入口網站](https://portal.azure.com)中的一些 Azure AD 增強功能。</span><span class="sxs-lookup"><span data-stu-id="9ef93-105">Following are some of the enhancements for Azure AD in the [Azure portal](https://portal.azure.com).</span></span>

- <span data-ttu-id="9ef93-106">改進的應用程式資源庫經驗，簡化了應用程式建立模型，並支援您使用的所有應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="9ef93-106">An improved application gallery experience, with a simplified application creation model and support for all the application types that you’re used to.</span></span> 
- <span data-ttu-id="9ef93-107">全新的快速啟動體驗，可協助您進行應用程式的試驗。</span><span class="sxs-lookup"><span data-stu-id="9ef93-107">A brand-new quick start experience that can help you get going with a pilot of your application.</span></span> 
- <span data-ttu-id="9ef93-108">只要按幾下滑鼠就能設定自助式原則。</span><span class="sxs-lookup"><span data-stu-id="9ef93-108">Configure self-service policies with just a few clicks.</span></span> 
- <span data-ttu-id="9ef93-109">應用程式 Proxy 的改進、單一登入組態，以及創造自己的應用程式體驗，可讓您執行比以往更多的作業。</span><span class="sxs-lookup"><span data-stu-id="9ef93-109">Improvements to application proxy, single sign-on configuration, and bring your own application experiences, allowing you to get more done than before.</span></span>

## <a name="improvements-to-the-azure-active-directory-application-gallery"></a><span data-ttu-id="9ef93-110">Azure Active Directory 應用程式資源庫的改進功能</span><span class="sxs-lookup"><span data-stu-id="9ef93-110">Improvements to the Azure Active Directory Application Gallery</span></span>

<span data-ttu-id="9ef93-111">新增您喜愛的應用程式，不論這些應用程式是來自[應用程式資源庫](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)、您延伸到雲端的自訂應用程式，或您正在開發的全新應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ef93-111">Add your favorite applications whether they are from the [application gallery](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), custom applications you’re extending to the cloud, or new applications you’re developing.</span></span>  <span data-ttu-id="9ef93-112">按一下 [企業應用程式] 概觀或 [所有應用程式] 刀鋒視窗上的 [新增]，即可開始使用此全新體驗。</span><span class="sxs-lookup"><span data-stu-id="9ef93-112">You can get started with this new experience by clicking **Add** on the **Enterprise Applications** overview or **All applications** blades.</span></span>
 
  ![新增應用程式](./media/active-directory-enterprise-apps-whats-new-azure-portal/01.png)

<span data-ttu-id="9ef93-114">在資源庫中，您會看到支援使用者佈建的所有精選應用程式顯示在最顯著的位置。</span><span class="sxs-lookup"><span data-stu-id="9ef93-114">Once in the gallery, you’ll see all our featured applications which support user provisioning displayed front-and-center.</span></span>  <span data-ttu-id="9ef93-115">您可以瀏覽各種不同的類別，深入鑽研您想知道的應用程式，您也可以使用搜尋體驗，快速找出您想要整合的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ef93-115">You can browse all sorts of different categories to drill into the applications you care about, or you can use the search experience to rapidly find the applications you want to integrate.</span></span>

  ![應用程式資源庫](./media/active-directory-enterprise-apps-whats-new-azure-portal/02.png)

## <a name="add-custom-applications-from-one-place"></a><span data-ttu-id="9ef93-117">從一個位置新增自訂應用程式</span><span class="sxs-lookup"><span data-stu-id="9ef93-117">Add custom applications from one place</span></span>

<span data-ttu-id="9ef93-118">除了從資源庫新增預先整合的應用程式，您在傳統管理入口網站中使用的所有自訂應用程式組態體驗現在均可用於在新的入口網站中。</span><span class="sxs-lookup"><span data-stu-id="9ef93-118">In addition to adding pre-integrated applications from the gallery, all the custom application configuration experiences that you were used to in the classic management portal are now possible in the new portal.</span></span> <span data-ttu-id="9ef93-119">不論您是使用應用程式 Proxy 從內部部署延伸應用程式、整合自己的密碼或同盟 SSO 應用程式，或是使用 Application Registry 建立全新的應用程式，您都可以從此單一位置達成目的。</span><span class="sxs-lookup"><span data-stu-id="9ef93-119">Whether you are extending an application from on-premises using the application proxy, integrating your own password or federated SSO application, or creating a brand-new application using the application registry, you can get to it all from this one single place.</span></span>

  ![新增自己的應用程式](./media/active-directory-enterprise-apps-whats-new-azure-portal/03.png)

 
<span data-ttu-id="9ef93-121">**若要開始新增自己的應用程式**：</span><span class="sxs-lookup"><span data-stu-id="9ef93-121">**To get started adding your own application**:</span></span>

1. <span data-ttu-id="9ef93-122">按一下應用程式資源庫頂端的 [新增您自己的連結]。</span><span class="sxs-lookup"><span data-stu-id="9ef93-122">Click the **add your own link** at the top of the application gallery.</span></span> 
2. <span data-ttu-id="9ef93-123">您的面前會出現兩個選項︰[部署現有的應用程式] 或 [開發新的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9ef93-123">You’ll see two options in front of you: **deploy an existing application** or **develop a new application**.</span></span> <span data-ttu-id="9ef93-124">繼續閱讀，以了解這兩個選項之間的差異以及如何使用它們。</span><span class="sxs-lookup"><span data-stu-id="9ef93-124">Read on to learn the difference between the two options and how to use them.</span></span>

### <a name="deploying-existing-applications"></a><span data-ttu-id="9ef93-125">部署現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="9ef93-125">Deploying existing applications</span></span>

1. <span data-ttu-id="9ef93-126">如果您已在執行應用程式，而只是想要將它整合至 Azure AD 中以便單一登入或佈建，選擇 [部署現有的應用程式] 選項。</span><span class="sxs-lookup"><span data-stu-id="9ef93-126">If you’ve got an application running already and just want to integrate it into Azure AD for single-sign on or provisioning, choose the **Deploy an existing application** option.</span></span> <span data-ttu-id="9ef93-127">挑選您應用程式的名稱，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9ef93-127">Pick a name for your application, click **Add**.</span></span>
2. <span data-ttu-id="9ef93-128">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="9ef93-128">That's it!</span></span> <span data-ttu-id="9ef93-129">您不需要知道應用程式的所有詳細資料，您現在可以隨時瀏覽左側功能表並依照您的喜好設定應用程式，即可設定新應用程式的運作方式。</span><span class="sxs-lookup"><span data-stu-id="9ef93-129">Instead of needing to know all the details about your application up front, you can now set up how your new application works by navigating through the left menu and configuring the application to your liking at any time.</span></span>

  ![按一下滑鼠即可新增現有的應用程式](./media/active-directory-enterprise-apps-whats-new-azure-portal/04.png)
 
### <a name="developing-new-applications"></a><span data-ttu-id="9ef93-131">開發新的應用程式</span><span class="sxs-lookup"><span data-stu-id="9ef93-131">Developing new applications</span></span>

1. <span data-ttu-id="9ef93-132">如果您正在開發新的應用程式，下列方法可讓您在資源庫中輕鬆取得 Application Registry︰</span><span class="sxs-lookup"><span data-stu-id="9ef93-132">If you’re developing a new application, there's an easy way for you to get to the Application Registry right from the gallery:</span></span>
2. <span data-ttu-id="9ef93-133">從 [應用程式資源庫] 按一下 [新增您自己的] 選項，選取 [開發現有的應用程式] 選項，您會看到應用程式新增體驗的快速連結。</span><span class="sxs-lookup"><span data-stu-id="9ef93-133">Click on the **add your own** option from the Application Gallery, select the **develop an existing application** choice, and you’ll see a quick link right to the application add experience.</span></span>

  ![按幾下滑鼠即可新增最近開發的應用程式](./media/active-directory-enterprise-apps-whats-new-azure-portal/05.png)


>[!NOTE]
><span data-ttu-id="9ef93-135">使用 Application Registry 新增應用程式後，您會看到該應用程式出現在企業應用程式清單中，您可以在其中設定單一登入及管理新應用程式的存取原則。</span><span class="sxs-lookup"><span data-stu-id="9ef93-135">Once you add an application using the Application Registry, you’ll see it show up in the list of Enterprise Applications where you’ll be able to configure single sign-on and manage access policies for your new application.</span></span>

  ![管理企業應用程式之下新應用程式的存取](./media/active-directory-enterprise-apps-whats-new-azure-portal/06.png)


## <a name="quick-start-get-going-with-your-new-application-right-away"></a><span data-ttu-id="9ef93-137">快速啟動︰立即開始使用新的應用程式</span><span class="sxs-lookup"><span data-stu-id="9ef93-137">Quick start: Get going with your new application right away</span></span> 

<span data-ttu-id="9ef93-138">新增應用程式之後，不論它已預先整合或是您自己的應用程式，我們都已建立特別量身訂製的快速啟動體驗，讓您快速地開始新的應用程式體驗。</span><span class="sxs-lookup"><span data-stu-id="9ef93-138">After you’ve added an application, whether it be pre-integrated or your own app, we’ve created a tailored quick-start experience to get you grounded in the new applications experience quickly.</span></span> <span data-ttu-id="9ef93-139">如果您有系統地遵循每個選項，我們將逐步引導您使用 UI，並且示範如何透過新應用程式的試驗盡快快速啟動。</span><span class="sxs-lookup"><span data-stu-id="9ef93-139">If you follow each option systematically, we’ll walk you through the UI and show you how to get going with a pilot of your new application as quickly as possible.</span></span> 
 
  ![新的應用程式快速啟動經驗](./media/active-directory-enterprise-apps-whats-new-azure-portal/07.png)

 <span data-ttu-id="9ef93-141">您可以隨時瀏覽這項新的快速啟動體驗，而對任何應用程式而言，只要按一下應用程式左導覽功能表中的 [快速啟動]。</span><span class="sxs-lookup"><span data-stu-id="9ef93-141">You can visit this new quick start experience at any time, and for any application, by clicking on **Quick start** from the application left navigation menu.</span></span>


## <a name="updated-application-proxy-configuration"></a><span data-ttu-id="9ef93-142">已更新的應用程式 Proxy 組態</span><span class="sxs-lookup"><span data-stu-id="9ef93-142">Updated application proxy configuration</span></span>
<span data-ttu-id="9ef93-143">現在，假設您新增的其中一個新應用程式正在內部部署環境中執行，而且您想要將它與 Azure AD 整合。</span><span class="sxs-lookup"><span data-stu-id="9ef93-143">Now, let’s say one of the new applications you added is running in your on-premises environment and you want to integrate it with Azure AD.</span></span>  <span data-ttu-id="9ef93-144">有關新的 Azure AD 入口網站中新應用程式設定體驗的其中一個酷炫新功能就是，藉由從應用程式 Proxy 組態中分割應用程式的登入模式，您現在即可輕鬆地將您公司網路中執行的密碼 SSO 或同盟應用程式直接公開至雲端，而不必建立多個應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="9ef93-144">One of the cool new things about the new application configuration experience in the new Azure AD portal is that by splitting the application’s sign-on mode from its application proxy configuration, you can now easily expose password SSO or federated applications that are running in your corporate network right to the cloud, without having to create multiple instances of the application.</span></span>

<span data-ttu-id="9ef93-145">除此之外，您現在也可以設定您新增的任何新應用程式 (包括支援原生 Windows 驗證經驗的應用程式)，以便直接從新的入口網站搭配 Azure AD 應用程式 Proxy 使用。</span><span class="sxs-lookup"><span data-stu-id="9ef93-145">In addition to this, you can now also configure any of the new applications you’ve added for use with the Azure AD Application Proxy right from the new portal, including applications which support native Windows authentication experiences.</span></span>

  ![設定應用程式以使用整合式 Windows 驗證登入選項](./media/active-directory-enterprise-apps-whats-new-azure-portal/08.png)
 

<span data-ttu-id="9ef93-147">若要開始設定採用應用程式 Proxy 的原生 Windows 驗證應用程式︰</span><span class="sxs-lookup"><span data-stu-id="9ef93-147">To get started configuring a native Windows authentication application with the Application Proxy:</span></span>
1. <span data-ttu-id="9ef93-148">在單一登入導覽項目上按一下，然後選擇登入設定刀鋒視窗中的 [整合式 Windows 驗證] 並設定您喜好的設定。</span><span class="sxs-lookup"><span data-stu-id="9ef93-148">Click on the Single sign-on navigation item and choose **Integrated Windows Authentication** from the sign-on settings blade and configure the settings to your liking.</span></span>
2. <span data-ttu-id="9ef93-149">除了支援這些新的驗證模式以外，您現在也可以從自訂網域上傳憑證，以支援在組織內安全端點上執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ef93-149">On top of supporting these new authentication modes, you can now also upload certificates from custom domains to support applications running on secure endpoints within your organization.</span></span>  
 
   ![上傳要搭配應用程式 Proxy 使用的憑證](./media/active-directory-enterprise-apps-whats-new-azure-portal/09.png)

3. <span data-ttu-id="9ef93-151">若要針對您最愛的內部部署應用程式上傳新憑證，請按一下左側導覽功能表中的 [應用程式 Proxy] 選項，按一下 [憑證] 選取器，然後上傳憑證檔案，以便用來加密我們的雲端端點對您的應用程式的要求。</span><span class="sxs-lookup"><span data-stu-id="9ef93-151">To upload a new certificate for your favorite on-premises application, click on the **Application proxy** option from the left navigation menu, click the **Certificate** selector, and upload a certificate file we can use to encrypt requests from our cloud endpoint to your application.</span></span>

## <a name="advanced-federated-single-sign-on-configuration"></a><span data-ttu-id="9ef93-152">進階同盟單一登入組態</span><span class="sxs-lookup"><span data-stu-id="9ef93-152">Advanced federated single sign-on configuration</span></span>

<span data-ttu-id="9ef93-153">對於目前使用同盟應用程式的使用者而言，SAML 型登入設定刀鋒視窗中有許多新功能。</span><span class="sxs-lookup"><span data-stu-id="9ef93-153">For those of you using federated applications today, there are many new features in the SAML-based sign-on configuration blade.</span></span> <span data-ttu-id="9ef93-154">首先，您現在可以完全自訂、新增、移除及對應在 SAML 權杖中以宣告形式發出的現有使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="9ef93-154">To start with, now you can fully customize, add, remove, and map the existing user attributes issued as claims in SAML tokens.</span></span>
 
  ![自訂傳遞至同盟應用程式的 SAML 權杖使用者屬性](./media/active-directory-enterprise-apps-whats-new-azure-portal/10.png)


<span data-ttu-id="9ef93-156">若要查看新的同盟 SSO 組態︰</span><span class="sxs-lookup"><span data-stu-id="9ef93-156">To check that out the new federated SSO configuration:</span></span>
1. <span data-ttu-id="9ef93-157">從左側導覽功能表開啟同盟應用程式的 [單一登入] 刀鋒視窗，並確定已選取 [SAML 型登入] 模式。</span><span class="sxs-lookup"><span data-stu-id="9ef93-157">Open a federated application’s **single sign-on** blade from the left navigation menu and make sure the ‘*SAML-based Sign-on** mode is selected.</span></span> 
2. <span data-ttu-id="9ef93-158">在那裡，啟用 [使用者屬性] 標題底下的核取方塊，以修改傳遞給該應用程式的 SAML 權杖中包含的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="9ef93-158">Once there, enable the checkbox under the **User Attributes** heading to modify all of the attributes included in the SAML token passed to that application.</span></span>

<span data-ttu-id="9ef93-159">您也可以建立、變換及管理用於同盟單一登入的憑證，以及編輯憑證即將到期時可取得通知的對象。</span><span class="sxs-lookup"><span data-stu-id="9ef93-159">You can also create, rollover, and manage certificates used for federated single sign-on, as well as edit who gets notified when your certificate is about to expire.</span></span> <span data-ttu-id="9ef93-160">您會在相同單一登入刀鋒視窗上的 [憑證] 標題之下看到這些新選項。</span><span class="sxs-lookup"><span data-stu-id="9ef93-160">You’ll see these new options under the **Certificates** heading on the same Single sign-on blade.</span></span>
 
  ![建立新憑證、自訂到期通知電子郵件和憑證簽署選項](./media/active-directory-enterprise-apps-whats-new-azure-portal/11.png)

### <a name="relay-state-paramenter"></a><span data-ttu-id="9ef93-162">轉送狀態參數</span><span class="sxs-lookup"><span data-stu-id="9ef93-162">Relay State paramenter</span></span>
<span data-ttu-id="9ef93-163">最後，我們還擴充了我們支援的這組 SAML URL 參數以包含 [轉送狀態參數]，這就是使用者在登入完成後將於同盟應用程式內登陸的頁面。</span><span class="sxs-lookup"><span data-stu-id="9ef93-163">Finally, we’ve also extended the set of SAML URL parameters we support to include the **Relay State parameter**, which is the page your users will land on inside of a federated application once the sign-in is completed.</span></span> <span data-ttu-id="9ef93-164">如果您想要將使用者快速送往應用程式內的特定位置，這是非常實用的設定。</span><span class="sxs-lookup"><span data-stu-id="9ef93-164">This is very useful setting to configure if you want to send your users to a specific place within the application to get them going quickly.</span></span>

  ![設定 SAML 轉送狀態參數](./media/active-directory-enterprise-apps-whats-new-azure-portal/12.png)
 
<span data-ttu-id="9ef93-166">**若要設定轉送狀態參數**：</span><span class="sxs-lookup"><span data-stu-id="9ef93-166">**To set the relay state parameter**:</span></span>

1. <span data-ttu-id="9ef93-167">在單一登入設定刀鋒視窗上，啟用 [網域和 URL] 標題之下的 [顯示進階 URL 設定] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="9ef93-167">Enable the **Show advanced URL settings** check-box under the **Domain and URLs** heading on the single-sign on configuration blade.</span></span> 
2. <span data-ttu-id="9ef93-168">這麼做之後，您就會看到一組新的 URL 輸入方塊出現，讓您進行這項和其他 SAML URL 設定。</span><span class="sxs-lookup"><span data-stu-id="9ef93-168">Once you do this, you’ll see a set of new URL input boxes appear which will allow you to set this, and other, SAML URL settings.</span></span>

## <a name="bring-your-own-password-sso-applications"></a><span data-ttu-id="9ef93-169">自備密碼 SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="9ef93-169">Bring your own password SSO applications</span></span>

<span data-ttu-id="9ef93-170">我們知道並非每個應用程式一開始都支援同盟。</span><span class="sxs-lookup"><span data-stu-id="9ef93-170">We know that not every application supports federation right out of the box.</span></span> <span data-ttu-id="9ef93-171">比方說，您新增的其中一個新應用程式或許有自訂登入畫面，可讓使用者以使用者名稱和密碼進行登入。</span><span class="sxs-lookup"><span data-stu-id="9ef93-171">For example, maybe one of the new applications you added has a custom login screen that your users use a username and password to sign in to.</span></span> <span data-ttu-id="9ef93-172">您仍可使用 [自備應用程式] 功能來整合這些類型的應用程式與 Azure AD，該項功能現在可供您在新的入口網站中進行設定。</span><span class="sxs-lookup"><span data-stu-id="9ef93-172">You can still integrate these types of applications with Azure AD using our **Bring your own applications** feature, which is now available for you to configure in the new portal.</span></span>
 
  ![整合自訂密碼儲存庫存應用程式與 Azure AD](./media/active-directory-enterprise-apps-whats-new-azure-portal/13.png)

<span data-ttu-id="9ef93-174">**若要查看「自備應用程式」功能**：</span><span class="sxs-lookup"><span data-stu-id="9ef93-174">**To check out the 'Bring your own applications' feature**:</span></span>

1. <span data-ttu-id="9ef93-175">為您已新增至 [密碼型登入] 的新自訂應用程式設定單一登入模式之後，輸入應用程式會呈現其登入畫面的 URL，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="9ef93-175">After you set the single sign-on mode for a new custom application that you’ve added to **Password-based Sign-on**, enter the URL where the application renders its login screen and click **Save**.</span></span>  
2. <span data-ttu-id="9ef93-176">這麼做之後，我們會自動擷取使用者名稱和密碼輸入方塊的該 URL，並可讓您使用 Azure AD 並利用存取面板瀏覽器擴充功能將密碼安全地傳輸到該應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ef93-176">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span>

## <a name="configure-self-service-application-access"></a><span data-ttu-id="9ef93-177">設定自助式應用程式存取</span><span class="sxs-lookup"><span data-stu-id="9ef93-177">Configure self-service application access</span></span>

<span data-ttu-id="9ef93-178">新增許多新的應用程式之後，您或許想要讓使用者瀏覽這些應用程式並將其新增到自己的存取面板，而不會讓系統管理員身分對您造成困擾。</span><span class="sxs-lookup"><span data-stu-id="9ef93-178">After you’ve added lots of new applications, maybe you want to allow your users to browse and add those applications to their own access panels, without needing to bother you as an administrator.</span></span> <span data-ttu-id="9ef93-179">現在，在此最新版本中，您可以從新的入口網站設定及管理自助式應用程式存取權限。</span><span class="sxs-lookup"><span data-stu-id="9ef93-179">Now, with this latest release, you can configure and manage self-service application access right from the new portal.</span></span>

  ![為密碼 SSO 應用程式設定自助式應用程式存取](./media/active-directory-enterprise-apps-whats-new-azure-portal/14.png)
 
<span data-ttu-id="9ef93-181">**若要設定和管理自助式應用程式存取**：</span><span class="sxs-lookup"><span data-stu-id="9ef93-181">**To configure and manage self-service application access**:</span></span>

1. <span data-ttu-id="9ef93-182">首先，您可以從應用程式的左側導覽功能表中選取 [自助式] 選項，並將 [允許使用者要求存取此應用程式？] 選項設定為 [是]。</span><span class="sxs-lookup"><span data-stu-id="9ef93-182">To get started, you can select the **Self-service** option from the application’s left navigation menu and set the **Allow users to request access to this application?** option to ‘**Yes**’.</span></span> 
2. <span data-ttu-id="9ef93-183">這可讓您設定允許誰核准此應用程式的存取權，以及哪個群組將會新增自助式使用者。</span><span class="sxs-lookup"><span data-stu-id="9ef93-183">This will enable you to configure who is allowed to approve access to this application, and which group self-service users will be added.</span></span> <span data-ttu-id="9ef93-184">此外，如果已針對密碼單一登入設定應用程式，您也會看到另一個選項，可讓您選擇性地允許這些核准者管理指派給應用程式的密碼。</span><span class="sxs-lookup"><span data-stu-id="9ef93-184">In addition, if the application is configured for password single-sign on, you’ll also see another option which lets you optionally allow those approvers to manage the passwords assigned to the application.</span></span>

##<a name="feedback"></a><span data-ttu-id="9ef93-185">意見反應</span><span class="sxs-lookup"><span data-stu-id="9ef93-185">Feedback</span></span>

<span data-ttu-id="9ef93-186">我們希望您喜歡使用改進後的 Azure AD 經驗。</span><span class="sxs-lookup"><span data-stu-id="9ef93-186">We hope you like using the improved Azure AD experience.</span></span> <span data-ttu-id="9ef93-187">請繼續提供意見反應！</span><span class="sxs-lookup"><span data-stu-id="9ef93-187">Please keep the feedback coming!</span></span> <span data-ttu-id="9ef93-188">請將您的意見反應和改進想法張貼在我們的[意見反應論壇](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal)的**管理員入口網站**區段中。</span><span class="sxs-lookup"><span data-stu-id="9ef93-188">Post your feedback and ideas for improvement in the **Admin Portal** section of our [feedback forum](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).</span></span>  <span data-ttu-id="9ef93-189">我們每天都很期待發展酷炫的新功能，並依照您的指導來塑造和定義我們接下來所要發展的項目。</span><span class="sxs-lookup"><span data-stu-id="9ef93-189">We’re excited about building cool new stuff every day, and use your guidance to shape and define what we build next.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ef93-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9ef93-190">Next steps</span></span>

<span data-ttu-id="9ef93-191">如需詳細資訊，請參閱[使用 Azure Active Directory 管理應用程式](active-directory-enable-sso-scenario.md)。</span><span class="sxs-lookup"><span data-stu-id="9ef93-191">For more details, see [Managing Applications with Azure Active Directory](active-directory-enable-sso-scenario.md).</span></span>



