---
title: "aaaHow tooconfigure 單一登入 tooan 應用程式 Proxy 應用程式 |Microsoft 文件"
description: "如何快速地設定單一登入 tooyour 應用程式 proxy 應用程式"
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
ms.openlocfilehash: e1289203177c77b3a8bcc9058c5c0b8ae50f243e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-single-sign-on-tooan-application-proxy-application"></a><span data-ttu-id="843b8-103">如何 tooconfigure 單一登入 tooan 應用程式 Proxy 應用程式</span><span class="sxs-lookup"><span data-stu-id="843b8-103">How tooconfigure single sign-on tooan Application Proxy application</span></span>

<span data-ttu-id="843b8-104">單一登入 (SSO) 允許使用者 tooaccess 應用程式而不需驗證多次。</span><span class="sxs-lookup"><span data-stu-id="843b8-104">Single sign-on (SSO) allows your users tooaccess an application without authenticating multiple times.</span></span> <span data-ttu-id="843b8-105">它可讓 hello 單一驗證 toooccur 在 hello 雲端中，對 Azure Active Directory，並允許 hello 服務或連接器 tooimpersonate hello 使用者 toocomplete hello 應用程式從任何額外的驗證挑戰。</span><span class="sxs-lookup"><span data-stu-id="843b8-105">It allows hello single authentication toooccur in hello cloud, against Azure Active Directory, and allows hello service or Connector tooimpersonate hello user toocomplete any additional authentication challenges from hello application.</span></span>

## <a name="how-tooconfigure-single-sign-on"></a><span data-ttu-id="843b8-106">如何 tooconfigure 單一登入</span><span class="sxs-lookup"><span data-stu-id="843b8-106">How tooconfigure single-sign on</span></span>
<span data-ttu-id="843b8-107">tooconfigure SSO，首先請確定您的應用程式已設定為預先驗證透過 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="843b8-107">tooconfigure SSO, first make sure that your application is configured for Pre-Authentication through Azure Active Directory.</span></span> <span data-ttu-id="843b8-108">toodo，請移過**Azure Active Directory**  - &gt; **企業應用程式** - &gt; **所有應用程式**  - &gt;您的應用程式 **- &gt;應用程式 Proxy**。</span><span class="sxs-lookup"><span data-stu-id="843b8-108">toodo this, go too**Azure Active Directory** -&gt; **Enterprise Applications** -&gt; **All Applications** -&gt; Your application **-&gt; Application Proxy**.</span></span> <span data-ttu-id="843b8-109">在此頁面上，您會看見 hello [預先驗證] 欄位中，並確定太設定 「 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="843b8-109">On this page, you see hello “Pre Authentication” field, and make sure that is set too“Azure Active Directory.</span></span> 

<span data-ttu-id="843b8-110">如需有關 hello 預先驗證方法的詳細資訊，請參閱 hello 的步驟 4[應用程式發行文件](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="843b8-110">For more information on hello Pre-Authentication methods, see step four of hello [app publishing document](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

   ![Azure 入口網站中的預先驗證方法](./media/application-proxy-config-sso-how-to/app-proxy.png)

## <a name="configuring-single-sign-on-modes-for-application-proxy-applications"></a><span data-ttu-id="843b8-112">針對應用程式 Proxy 應用程式設定單一登入模式</span><span class="sxs-lookup"><span data-stu-id="843b8-112">Configuring single sign-on modes for Application Proxy Applications</span></span>
<span data-ttu-id="843b8-113">接下來，我們設定 hello 特定類型的單一登入。</span><span class="sxs-lookup"><span data-stu-id="843b8-113">Next we configure hello specific type of single sign-on.</span></span> <span data-ttu-id="843b8-114">根據使用何種驗證 hello 後端應用程式分類 hello 登入方法。</span><span class="sxs-lookup"><span data-stu-id="843b8-114">hello sign-on methods are classified based on what type of authentication hello backend application uses.</span></span> <span data-ttu-id="843b8-115">應用程式 Proxy 應用程式支援三種登入類型：</span><span class="sxs-lookup"><span data-stu-id="843b8-115">App Proxy applications supports three types of sign-on:</span></span>

-   <span data-ttu-id="843b8-116">**密碼型登入**： 密碼式登入可以用於任何使用使用者名稱和密碼欄位 toosign 上應用程式。</span><span class="sxs-lookup"><span data-stu-id="843b8-116">**Password-based Sign-On**: Password-based sign-on can be used for any application that uses username and password fields toosign-on.</span></span> <span data-ttu-id="843b8-117">您可以在我們的[密碼 SSO 設定文件](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#bring-your-own-password-sso-applications)中找到設定步驟。</span><span class="sxs-lookup"><span data-stu-id="843b8-117">Configuration steps can be found in our [password-SSO configuration documentation](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#bring-your-own-password-sso-applications).</span></span>

-   <span data-ttu-id="843b8-118">**整合式 Windows 驗證**：對於使用整合式 Windows 驗證 (IWA) 的應用程式，單一登入是透過 Kerberos 限制委派 (KCD) 來啟用。</span><span class="sxs-lookup"><span data-stu-id="843b8-118">**Integrated Windows Authentication**: For applications using Integrated Windows Authentication (IWA), single sign-on is enabled through Kerberos Constrained Delegation (KCD).</span></span> <span data-ttu-id="843b8-119">這提供中 Active Directory tooimpersonate 使用者和 toosend 的應用程式 Proxy 連接器權限，並接收權杖，代表它們。</span><span class="sxs-lookup"><span data-stu-id="843b8-119">This gives Application Proxy Connectors permission in Active Directory tooimpersonate users, and toosend and receive tokens on their behalf.</span></span> <span data-ttu-id="843b8-120">設定 KCD 的詳細資訊，請參閱 hello[單一登入 KCD 文件](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)。</span><span class="sxs-lookup"><span data-stu-id="843b8-120">Details on configuring KCD can be found in hello [Single Sign-On with KCD documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd).</span></span>

-   <span data-ttu-id="843b8-121">**標頭形式的登入**：標頭形式的登入是透過合作關係啟用，並且需要一些額外設定。</span><span class="sxs-lookup"><span data-stu-id="843b8-121">**Header-based Sign-On**: Header-based sign on is enabled through a partnership and does require some additional configuration.</span></span> <span data-ttu-id="843b8-122">如需 hello 合作關係與設定單一登入 tooan 應用程式使用標頭進行驗證的逐步指示的詳細資訊，請參閱 hello [Azure AD 文件的 PingAccess](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access)。</span><span class="sxs-lookup"><span data-stu-id="843b8-122">For details on hello partnership and step-by-step instructions for configuring single sign-on tooan application that uses headers for authentication, see hello [PingAccess for Azure AD documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span></span>

<span data-ttu-id="843b8-123">每個選項可以找到移 tooyour 應用程式 「 企業應用程式 」 及開啟 hello**單一登入**hello 左邊功能表上的頁面。</span><span class="sxs-lookup"><span data-stu-id="843b8-123">Each of these options can be found by going tooyour application in “Enterprise Applications”, and opening hello **Single Sign-On** page on hello left menu.</span></span> <span data-ttu-id="843b8-124">請注意，是否 hello 舊的入口網站中建立您的應用程式，您可能不會看到所有這些選項。</span><span class="sxs-lookup"><span data-stu-id="843b8-124">note that if your application was created in hello old portal, you may not see all these options.</span></span>

<span data-ttu-id="843b8-125">在此頁面上，您還會看到一個額外登入選項：連結的登入。</span><span class="sxs-lookup"><span data-stu-id="843b8-125">On this page, you also see one additional Sign-On option: Linked Sign-On.</span></span> <span data-ttu-id="843b8-126">應用程式 Proxy 也支援此選項。</span><span class="sxs-lookup"><span data-stu-id="843b8-126">This is also supported by Application Proxy.</span></span> <span data-ttu-id="843b8-127">不過請注意此選項不會新增單一登入 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="843b8-127">However, note that this option does not add single sign-on toohello application.</span></span> <span data-ttu-id="843b8-128">話雖如此 hello 應用程式可能已經有單一登入使用另一個服務，例如 Active Directory 同盟服務實作。</span><span class="sxs-lookup"><span data-stu-id="843b8-128">That said hello application may already have single sign-on implemented using another service such as Active Directory Federation Services.</span></span> 

<span data-ttu-id="843b8-129">此選項可讓系統管理員 toocreate 連結 tooan 應用程式，使用者第一次進入存取 hello 應用程式時。</span><span class="sxs-lookup"><span data-stu-id="843b8-129">This option allows an admin toocreate a link tooan application that users first land on when accessing hello application.</span></span> <span data-ttu-id="843b8-130">例如，如果沒有為應用程式設定使用 Active Directory Federation Services 2.0 tooauthenticate 使用者，系統管理員可以使用 hello 」 連結登入 選項 toocreate 連結 tooit hello 存取面板上。</span><span class="sxs-lookup"><span data-stu-id="843b8-130">For example, if there is an application that is configured tooauthenticate users using Active Directory Federation Services 2.0, an administrator can use hello “Linked Sign-On” option toocreate a link tooit on hello access panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="843b8-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="843b8-131">Next steps</span></span>
[<span data-ttu-id="843b8-132">提供單一登入 tooyour 應用程式與應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="843b8-132">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
