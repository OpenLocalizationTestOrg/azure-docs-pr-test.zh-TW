---
title: "在 Azure AD 中管理同盟憑證 | Microsoft Docs"
description: "了解如何自訂同盟憑證的到期日期，以及如何更新即將到期的憑證。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f516f7f0-b25a-4901-8247-f5964666ce23
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2017
ms.author: jeedes
ms.openlocfilehash: 1283b570200f05003658824760ecbb6722f241d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a><span data-ttu-id="7a747-103">在 Azure Active Directory 中管理同盟單一登入的憑證</span><span class="sxs-lookup"><span data-stu-id="7a747-103">Manage certificates for federated single sign-on in Azure Active Directory</span></span>
<span data-ttu-id="7a747-104">本文涵蓋各種與 Azure Active Directory (Azure AD) 建立憑證，以對 SaaS 應用程式建立同盟單一登入 (SSO) 相關的常見問題和相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7a747-104">This article covers common questions and information related to the certificates that Azure Active Directory (Azure AD) creates to establish federated single sign-on (SSO) to your SaaS applications.</span></span> <span data-ttu-id="7a747-105">從 Azure AD 應用程式資源庫，或使用非資源庫的應用程式範本新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a747-105">Add applications from the Azure AD app gallery or by using a non-gallery application template.</span></span> <span data-ttu-id="7a747-106">使用同盟 SSO 選項以設定應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a747-106">Configure the application by using the federated SSO option.</span></span>

<span data-ttu-id="7a747-107">本文只與透過 SAML 同盟設定為使用 Azure AD SSO 的應用程式有關，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="7a747-107">This article is relevant only to apps that are configured to use Azure AD SSO through SAML federation, as shown in the following example:</span></span>

![Azure AD 單一登入](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a><span data-ttu-id="7a747-109">為資源庫和非資源庫應用程式自動產生的憑證</span><span class="sxs-lookup"><span data-stu-id="7a747-109">Auto-generated certificate for gallery and non-gallery applications</span></span>
<span data-ttu-id="7a747-110">當您從資源庫新增應用程式，並設定 SAML 型登入時，Azure AD 會為應用程式產生 3 年的有效憑證。</span><span class="sxs-lookup"><span data-stu-id="7a747-110">When you add a new application from the gallery and configure a SAML-based sign-on, Azure AD generates a certificate for the application that is valid for three years.</span></span> <span data-ttu-id="7a747-111">您可以從 [SAML 簽署憑證] 區段下載此憑證。</span><span class="sxs-lookup"><span data-stu-id="7a747-111">You can download this certificate from the **SAML Signing Certificate** section.</span></span> <span data-ttu-id="7a747-112">對於資源庫應用程式，本區段會視應用程式的需求而定，顯示下載憑證或中繼資料的選項。</span><span class="sxs-lookup"><span data-stu-id="7a747-112">For gallery applications, this section might show an option to download the certificate or metadata, depending on the requirement of the application.</span></span>

![Azure AD 單一登入](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-the-expiration-date-for-your-federation-certificate-and-roll-it-over-to-a-new-certificate"></a><span data-ttu-id="7a747-114">自訂同盟憑證的到期日期及變換新的憑證</span><span class="sxs-lookup"><span data-stu-id="7a747-114">Customize the expiration date for your federation certificate and roll it over to a new certificate</span></span>
<span data-ttu-id="7a747-115">根據預設，憑證會設定為三年之後到期。</span><span class="sxs-lookup"><span data-stu-id="7a747-115">By default, certificates are set to expire after three years.</span></span> <span data-ttu-id="7a747-116">您可以藉由完成下列步驟，為您的憑證選擇不同的到期日期。</span><span class="sxs-lookup"><span data-stu-id="7a747-116">You can choose a different expiration date for your certificate by completing the following steps.</span></span>
<span data-ttu-id="7a747-117">螢幕擷取畫面使用 Salesforce 作為範例，但是這些步驟可以套用在任何同盟的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a747-117">The screenshots use Salesforce for the sake of example, but these steps can apply to any federated SaaS app.</span></span>

1. <span data-ttu-id="7a747-118">在 [Azure 入口網站](https://aad.portal.azure.com)中，按一下左窗格中的 [企業應用程式]，然後按一下 [概觀] 分頁上的 [新增應用程式]：</span><span class="sxs-lookup"><span data-stu-id="7a747-118">In the [Azure portal](https://aad.portal.azure.com), click **Enterprise application** in the left pane and then click **New application** on the **Overview** page:</span></span>

   ![開啟 SSO 組態精靈](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. <span data-ttu-id="7a747-120">搜尋資源庫應用程式，然後選取您想要新增的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a747-120">Search for the gallery application and then select the application that you want to add.</span></span> <span data-ttu-id="7a747-121">如果找不到所需的應用程式，則使用 [非資源庫應用程式] 選項來新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a747-121">If you cannot find the required application, add the application by using the **Non-gallery application** option.</span></span> <span data-ttu-id="7a747-122">這項功只適用於 Azure AD Premium (P1 和 P2) SKU。</span><span class="sxs-lookup"><span data-stu-id="7a747-122">This feature is available only in the Azure AD Premium (P1 and P2) SKU.</span></span>

    ![Azure AD 單一登入](./media/active-directory-sso-certs/add_gallery_application.png)

3. <span data-ttu-id="7a747-124">按一下左窗格中的 [單一登入] 連結，然後將 [單一登入模式] 變更為 [SAML 型登入]。</span><span class="sxs-lookup"><span data-stu-id="7a747-124">Click the **Single sign-on** link in the left pane and change **Single Sign-on Mode** to **SAML-based Sign-on**.</span></span> <span data-ttu-id="7a747-125">這個步驟會為您的應用程式產生三年的憑證。</span><span class="sxs-lookup"><span data-stu-id="7a747-125">This step generates a three-year certificate for your application.</span></span>

4. <span data-ttu-id="7a747-126">若要建立新憑證，請按一下 [SAML 簽署憑證] 區段中的 [建立新憑證] 連結。</span><span class="sxs-lookup"><span data-stu-id="7a747-126">To create a new certificate, click the **Create new certificate** link in the **SAML Signing Certificate** section.</span></span>

    ![產生新的憑證](./media/active-directory-sso-certs/create_new_certficate.png)

5. <span data-ttu-id="7a747-128">[建立新憑證] 連結會開啟行事曆控制項。</span><span class="sxs-lookup"><span data-stu-id="7a747-128">The **Create a new certificate** link opens the calendar control.</span></span> <span data-ttu-id="7a747-129">您可以設定從目前日期起算最多三年的任何日期和時間。</span><span class="sxs-lookup"><span data-stu-id="7a747-129">You can set any date and time up to three years from the current date.</span></span> <span data-ttu-id="7a747-130">選取的日期和時間會是新憑證的新到期日期和時間。</span><span class="sxs-lookup"><span data-stu-id="7a747-130">The selected date and time is the new expiration date and time of your new certificate.</span></span> <span data-ttu-id="7a747-131">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7a747-131">Click **Save**.</span></span>

    ![下載，然後上傳憑證](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. <span data-ttu-id="7a747-133">新憑證現在可供下載。</span><span class="sxs-lookup"><span data-stu-id="7a747-133">Now the new certificate is available to download.</span></span> <span data-ttu-id="7a747-134">按一下 [憑證] 連結，以便下載它。</span><span class="sxs-lookup"><span data-stu-id="7a747-134">Click the **Certificate** link to download it.</span></span> <span data-ttu-id="7a747-135">此時，您的憑證不在作用中。</span><span class="sxs-lookup"><span data-stu-id="7a747-135">At this point, your certificate is not active.</span></span> <span data-ttu-id="7a747-136">當您想要變換此憑證時，按一下 [讓新憑證成為使用中] 核取方塊，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="7a747-136">When you want to roll over to this certificate, select the **Make new certificate active** check box and click **Save**.</span></span> <span data-ttu-id="7a747-137">從該時間點開始，Azure AD 會開始使用新憑證來簽署回應。</span><span class="sxs-lookup"><span data-stu-id="7a747-137">From that point, Azure AD starts using the new certificate for signing the response.</span></span>

7.  <span data-ttu-id="7a747-138">若要了解如何將憑證上傳至特定 SaaS 應用程式，請按一下[檢視應用程式設定教學課程] 連結。</span><span class="sxs-lookup"><span data-stu-id="7a747-138">To learn how to upload the certificate to your particular SaaS application, click the **View application configuration tutorial** link.</span></span>

## <a name="renew-a-certificate-that-will-soon-expire"></a><span data-ttu-id="7a747-139">更新即將到期的憑證</span><span class="sxs-lookup"><span data-stu-id="7a747-139">Renew a certificate that will soon expire</span></span>
<span data-ttu-id="7a747-140">以下的更新步驟應該不會讓您的使用者有任何明顯的停機時間。</span><span class="sxs-lookup"><span data-stu-id="7a747-140">The following renewal steps should result in no significant downtime for your users.</span></span> <span data-ttu-id="7a747-141">本節中的螢幕擷取畫面採用 Salesforce 作為範例，但這些步驟可以套用到任何同盟的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a747-141">The screenshots in this section feature Salesforce as an example, but these steps can apply to any federated SaaS app.</span></span>

1. <span data-ttu-id="7a747-142">在 **Azure Active Directory** 應用程式的 [單一登入] 分頁上，為您的應用程式產生新憑證。</span><span class="sxs-lookup"><span data-stu-id="7a747-142">On the **Azure Active Directory** application **Single sign-on** page, generate the new certificate for your application.</span></span> <span data-ttu-id="7a747-143">按一下 [SAML 簽署憑證] 區段中的 [建立新憑證] 連結，即可達成。</span><span class="sxs-lookup"><span data-stu-id="7a747-143">You can do this by clicking the **Create new certificate** link in the **SAML Signing Certificate** section.</span></span>

    ![產生新的憑證](./media/active-directory-sso-certs/create_new_certficate.png)

2. <span data-ttu-id="7a747-145">選取新憑證的所需到期日期與時間，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="7a747-145">Select the desired expiration date and time for your new certificate and click **Save**.</span></span>

3. <span data-ttu-id="7a747-146">下載 [SAML 簽署憑證] 選項中的憑證。</span><span class="sxs-lookup"><span data-stu-id="7a747-146">Download the certificate in the **SAML Signing certificate** option.</span></span> <span data-ttu-id="7a747-147">將新的憑證上傳至 SaaS 應用程式的單一登入設定畫面。</span><span class="sxs-lookup"><span data-stu-id="7a747-147">Upload the new certificate to the SaaS application's single sign-on configuration screen.</span></span> <span data-ttu-id="7a747-148">若要了解如何為特定 SaaS 應用程式執行這項操作，請按一下 [檢視應用程式設定教學課程] 連結。</span><span class="sxs-lookup"><span data-stu-id="7a747-148">To learn how to do this for your particular SaaS application, click the **View application configuration tutorial** link.</span></span>
   
4. <span data-ttu-id="7a747-149">若要在 Azure AD 上啟用新憑證，選取 [讓新憑證成為使用中] 核取方塊，然後按一下分頁頂端的 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7a747-149">To activate the new certificate in Azure AD, select the **Make new certificate active** check box and click the **Save** button at the top of the page.</span></span> <span data-ttu-id="7a747-150">這會在 Azure AD 端變換新憑證。</span><span class="sxs-lookup"><span data-stu-id="7a747-150">This rolls over the new certificate on the Azure AD side.</span></span> <span data-ttu-id="7a747-151">憑證的狀態會從 [新增] 變更為 [作用中]。</span><span class="sxs-lookup"><span data-stu-id="7a747-151">The status of the certificate changes from **New** to **Active**.</span></span> <span data-ttu-id="7a747-152">從該時間點開始，Azure AD 會開始使用新憑證來簽署回應。</span><span class="sxs-lookup"><span data-stu-id="7a747-152">From that point, Azure AD starts using the new certificate for signing the response.</span></span> 
   
    ![產生新的憑證](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a><span data-ttu-id="7a747-154">相關文章</span><span class="sxs-lookup"><span data-stu-id="7a747-154">Related articles</span></span>
* [<span data-ttu-id="7a747-155">如何整合 SaaS 應用程式與 Azure Active Directory 的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="7a747-155">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7a747-156">Azure Active Directory 中應用程式管理的文件索引</span><span class="sxs-lookup"><span data-stu-id="7a747-156">Article index for application management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="7a747-157">搭配 Azure Active Directory 的應用程式存取和單一登入</span><span class="sxs-lookup"><span data-stu-id="7a747-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="7a747-158">針對 SAML 型單一登入進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="7a747-158">Troubleshooting SAML-based single sign-on</span></span>](active-directory-saml-debugging.md)
