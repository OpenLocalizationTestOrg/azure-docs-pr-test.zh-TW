---
title: "如何針對應用程式 Proxy 應用程式設定單一登入 | Microsoft Docs"
description: "如何快速針對應用程式 Proxy 應用程式設定單一登入"
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
ms.openlocfilehash: ccab427857b1439f37f3d9f193e35a4fc2237014
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-single-sign-on-to-an-application-proxy-application"></a><span data-ttu-id="67778-103">如何針對應用程式 Proxy 應用程式設定單一登入</span><span class="sxs-lookup"><span data-stu-id="67778-103">How to configure single sign-on to an Application Proxy application</span></span>

<span data-ttu-id="67778-104">單一登入 (SSO) 可讓您的使用者在不需要多次驗證的情況下存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="67778-104">Single sign-on (SSO) allows your users to access an application without authenticating multiple times.</span></span> <span data-ttu-id="67778-105">它允許單一驗證在雲端中針對 Azure Active Directory 發生，並允許服務或連接器模擬使用者，以完成來自應用程式的任何其他驗證挑戰。</span><span class="sxs-lookup"><span data-stu-id="67778-105">It allows the single authentication to occur in the cloud, against Azure Active Directory, and allows the service or Connector to impersonate the user to complete any additional authentication challenges from the application.</span></span>

## <a name="how-to-configure-single-sign-on"></a><span data-ttu-id="67778-106">如何設定單一登入</span><span class="sxs-lookup"><span data-stu-id="67778-106">How to configure single-sign on</span></span>
<span data-ttu-id="67778-107">若要設定 SSO，請先確定您的應用程式已透過 Azure Active Directory 針對預先驗證進行設定。</span><span class="sxs-lookup"><span data-stu-id="67778-107">To configure SSO, first make sure that your application is configured for Pre-Authentication through Azure Active Directory.</span></span> <span data-ttu-id="67778-108">若要這樣做，請移至 [Azure Active Directory] -&gt; [企業應用程式] -&gt; [所有應用程式] -&gt; 您的應用程式 -&gt; [應用程式 Proxy]。</span><span class="sxs-lookup"><span data-stu-id="67778-108">To do this, go to **Azure Active Directory** -&gt; **Enterprise Applications** -&gt; **All Applications** -&gt; Your application **-&gt; Application Proxy**.</span></span> <span data-ttu-id="67778-109">在這個頁面上，您會看到 [預先驗證] 欄位，請確定它已設定為 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="67778-109">On this page, you see the “Pre Authentication” field, and make sure that is set to “Azure Active Directory.</span></span> 

<span data-ttu-id="67778-110">如需預先驗證方法的詳細資訊，請參閱[應用程式發佈文件](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)的步驟四。</span><span class="sxs-lookup"><span data-stu-id="67778-110">For more information on the Pre-Authentication methods, see step four of the [app publishing document](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

   ![Azure 入口網站中的預先驗證方法](./media/application-proxy-config-sso-how-to/app-proxy.png)

## <a name="configuring-single-sign-on-modes-for-application-proxy-applications"></a><span data-ttu-id="67778-112">針對應用程式 Proxy 應用程式設定單一登入模式</span><span class="sxs-lookup"><span data-stu-id="67778-112">Configuring single sign-on modes for Application Proxy Applications</span></span>
<span data-ttu-id="67778-113">接下來，我們會設定單一登入的特定類型。</span><span class="sxs-lookup"><span data-stu-id="67778-113">Next we configure the specific type of single sign-on.</span></span> <span data-ttu-id="67778-114">登入方法是根據後端應用程式所使用的驗證類型來分類。</span><span class="sxs-lookup"><span data-stu-id="67778-114">The sign-on methods are classified based on what type of authentication the backend application uses.</span></span> <span data-ttu-id="67778-115">應用程式 Proxy 應用程式支援三種登入類型：</span><span class="sxs-lookup"><span data-stu-id="67778-115">App Proxy applications supports three types of sign-on:</span></span>

-   <span data-ttu-id="67778-116">**密碼登入**：密碼登入可用於任何使用使用者名稱和密碼欄位進行登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="67778-116">**Password-based Sign-On**: Password-based sign-on can be used for any application that uses username and password fields to sign-on.</span></span> <span data-ttu-id="67778-117">您可以在我們的[密碼 SSO 設定文件](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#bring-your-own-password-sso-applications)中找到設定步驟。</span><span class="sxs-lookup"><span data-stu-id="67778-117">Configuration steps can be found in our [password-SSO configuration documentation](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#bring-your-own-password-sso-applications).</span></span>

-   <span data-ttu-id="67778-118">**整合式 Windows 驗證**：對於使用整合式 Windows 驗證 (IWA) 的應用程式，單一登入是透過 Kerberos 限制委派 (KCD) 來啟用。</span><span class="sxs-lookup"><span data-stu-id="67778-118">**Integrated Windows Authentication**: For applications using Integrated Windows Authentication (IWA), single sign-on is enabled through Kerberos Constrained Delegation (KCD).</span></span> <span data-ttu-id="67778-119">這會提供應用程式 Proxy 連接器在 Active Directory 中模擬使用者並代表他們傳送及接收權杖的權限。</span><span class="sxs-lookup"><span data-stu-id="67778-119">This gives Application Proxy Connectors permission in Active Directory to impersonate users, and to send and receive tokens on their behalf.</span></span> <span data-ttu-id="67778-120">您可以在[使用 KCD 進行單一登入文件](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)中找到設定 KCD 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="67778-120">Details on configuring KCD can be found in the [Single Sign-On with KCD documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd).</span></span>

-   <span data-ttu-id="67778-121">**標頭形式的登入**：標頭形式的登入是透過合作關係啟用，並且需要一些額外設定。</span><span class="sxs-lookup"><span data-stu-id="67778-121">**Header-based Sign-On**: Header-based sign on is enabled through a partnership and does require some additional configuration.</span></span> <span data-ttu-id="67778-122">如需合作關係的詳細資料，以及針對使用標頭進行驗證之應用程式設定單一登入的逐步指示，請參閱 [Azure AD 的 PingAccess 文件](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access)。</span><span class="sxs-lookup"><span data-stu-id="67778-122">For details on the partnership and step-by-step instructions for configuring single sign-on to an application that uses headers for authentication, see the [PingAccess for Azure AD documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span></span>

<span data-ttu-id="67778-123">每個選項都可透過在 [企業應用程式] 中移至您的應用程式，然後開啟左側功能表上的 [單一登入] 頁面來找到。</span><span class="sxs-lookup"><span data-stu-id="67778-123">Each of these options can be found by going to your application in “Enterprise Applications”, and opening the **Single Sign-On** page on the left menu.</span></span> <span data-ttu-id="67778-124">請注意，如果您的應用程式是在舊版入口網站中建立，您可能無法看到所有選項。</span><span class="sxs-lookup"><span data-stu-id="67778-124">note that if your application was created in the old portal, you may not see all these options.</span></span>

<span data-ttu-id="67778-125">在此頁面上，您還會看到一個額外登入選項：連結的登入。</span><span class="sxs-lookup"><span data-stu-id="67778-125">On this page, you also see one additional Sign-On option: Linked Sign-On.</span></span> <span data-ttu-id="67778-126">應用程式 Proxy 也支援此選項。</span><span class="sxs-lookup"><span data-stu-id="67778-126">This is also supported by Application Proxy.</span></span> <span data-ttu-id="67778-127">不過請注意，此選項並不會將單一登入新增至應用程式。</span><span class="sxs-lookup"><span data-stu-id="67778-127">However, note that this option does not add single sign-on to the application.</span></span> <span data-ttu-id="67778-128">不過，應用程式可能已經使用另一項服務 (例如 Active Directory 同盟服務) 來實作單一登入。</span><span class="sxs-lookup"><span data-stu-id="67778-128">That said the application may already have single sign-on implemented using another service such as Active Directory Federation Services.</span></span> 

<span data-ttu-id="67778-129">這個選項可讓系統管理員建立應用程式連結，以供使用者首次存取應用程式時使用。</span><span class="sxs-lookup"><span data-stu-id="67778-129">This option allows an admin to create a link to an application that users first land on when accessing the application.</span></span> <span data-ttu-id="67778-130">例如，如果有一個應用程式設定為使用 Active Directory 同盟服務 2.0 來驗證使用者，系統管理員可以使用 [連結的登入] 選項在存取面板上建立應用程式的連結。</span><span class="sxs-lookup"><span data-stu-id="67778-130">For example, if there is an application that is configured to authenticate users using Active Directory Federation Services 2.0, an administrator can use the “Linked Sign-On” option to create a link to it on the access panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67778-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="67778-131">Next steps</span></span>
[<span data-ttu-id="67778-132">使用應用程式 Proxy 提供單一登入應用程式</span><span class="sxs-lookup"><span data-stu-id="67778-132">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
