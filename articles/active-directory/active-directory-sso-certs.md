---
title: "在 Azure AD 中的 aaaManage 同盟憑證 |Microsoft 文件"
description: "了解如何 toocustomize hello 到期日您同盟的憑證，和如何 toorenew 憑證即將到期。"
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
ms.openlocfilehash: e17622d25c9babfa295cc0bb68c24e21b8c574d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a><span data-ttu-id="12445-103">在 Azure Active Directory 中管理同盟單一登入的憑證</span><span class="sxs-lookup"><span data-stu-id="12445-103">Manage certificates for federated single sign-on in Azure Active Directory</span></span>
<span data-ttu-id="12445-104">本文章涵蓋常見問題的解答，以及 Azure Active Directory (Azure AD) 建立 tooestablish toohello 憑證同盟單一登入 (SSO) tooyour SaaS 應用程式相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="12445-104">This article covers common questions and information related toohello certificates that Azure Active Directory (Azure AD) creates tooestablish federated single sign-on (SSO) tooyour SaaS applications.</span></span> <span data-ttu-id="12445-105">從 hello Azure AD app 資源庫，或使用非組件庫的應用程式範本，請新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="12445-105">Add applications from hello Azure AD app gallery or by using a non-gallery application template.</span></span> <span data-ttu-id="12445-106">使用 hello 同盟 SSO 選項設定 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="12445-106">Configure hello application by using hello federated SSO option.</span></span>

<span data-ttu-id="12445-107">本文是所設定的 SAML 同盟透過 toouse Azure AD 的 SSO 相關只有 tooapps hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="12445-107">This article is relevant only tooapps that are configured toouse Azure AD SSO through SAML federation, as shown in hello following example:</span></span>

![Azure AD 單一登入](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a><span data-ttu-id="12445-109">為資源庫和非資源庫應用程式自動產生的憑證</span><span class="sxs-lookup"><span data-stu-id="12445-109">Auto-generated certificate for gallery and non-gallery applications</span></span>
<span data-ttu-id="12445-110">當您從 hello 圖庫新增新的應用程式，並設定 SAML 型登入時，Azure AD 會產生的憑證有效期為三年的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="12445-110">When you add a new application from hello gallery and configure a SAML-based sign-on, Azure AD generates a certificate for hello application that is valid for three years.</span></span> <span data-ttu-id="12445-111">您可以將此憑證從 hello **SAML 簽章憑證**> 一節。</span><span class="sxs-lookup"><span data-stu-id="12445-111">You can download this certificate from hello **SAML Signing Certificate** section.</span></span> <span data-ttu-id="12445-112">組件庫的應用程式，選項 toodownload hello 憑證或中繼資料，根據 hello hello 應用程式的需求而定，可能會顯示這一節。</span><span class="sxs-lookup"><span data-stu-id="12445-112">For gallery applications, this section might show an option toodownload hello certificate or metadata, depending on hello requirement of hello application.</span></span>

![Azure AD 單一登入](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-hello-expiration-date-for-your-federation-certificate-and-roll-it-over-tooa-new-certificate"></a><span data-ttu-id="12445-114">自訂 hello 同盟憑證的到期日和變換 tooa 新憑證</span><span class="sxs-lookup"><span data-stu-id="12445-114">Customize hello expiration date for your federation certificate and roll it over tooa new certificate</span></span>
<span data-ttu-id="12445-115">根據預設，憑證會設定 tooexpire 後三年。</span><span class="sxs-lookup"><span data-stu-id="12445-115">By default, certificates are set tooexpire after three years.</span></span> <span data-ttu-id="12445-116">您可以藉由完成下列步驟的 hello 選擇不同的到期日期，您的憑證。</span><span class="sxs-lookup"><span data-stu-id="12445-116">You can choose a different expiration date for your certificate by completing hello following steps.</span></span>
<span data-ttu-id="12445-117">hello 螢幕擷取畫面的 hello 不錯的範例中，使用 Salesforce，但是這些步驟可以套用 tooany 同盟 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="12445-117">hello screenshots use Salesforce for hello sake of example, but these steps can apply tooany federated SaaS app.</span></span>

1. <span data-ttu-id="12445-118">在 [hello [Azure 入口網站](https://aad.portal.azure.com)，按一下**企業應用程式**在 hello 左的窗格，然後按一下 [**新的應用程式**上 hello**概觀**頁面上：</span><span class="sxs-lookup"><span data-stu-id="12445-118">In hello [Azure portal](https://aad.portal.azure.com), click **Enterprise application** in hello left pane and then click **New application** on hello **Overview** page:</span></span>

   ![開啟 hello SSO 組態精靈](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. <span data-ttu-id="12445-120">搜尋 hello 組件庫的應用程式，然後選取您想 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="12445-120">Search for hello gallery application and then select hello application that you want tooadd.</span></span> <span data-ttu-id="12445-121">如果找不到所需的 hello 應用程式，新增 hello 應用程式使用 hello**非組件庫的應用程式**選項。</span><span class="sxs-lookup"><span data-stu-id="12445-121">If you cannot find hello required application, add hello application by using hello **Non-gallery application** option.</span></span> <span data-ttu-id="12445-122">只有在 hello （P1 和 P2） 的 Azure AD Premium SKU 中使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="12445-122">This feature is available only in hello Azure AD Premium (P1 and P2) SKU.</span></span>

    ![Azure AD 單一登入](./media/active-directory-sso-certs/add_gallery_application.png)

3. <span data-ttu-id="12445-124">按一下 hello**單一登入**中 hello 左窗格和 [變更連結**單一登入模式**太**SAML 型登入**。</span><span class="sxs-lookup"><span data-stu-id="12445-124">Click hello **Single sign-on** link in hello left pane and change **Single Sign-on Mode** too**SAML-based Sign-on**.</span></span> <span data-ttu-id="12445-125">這個步驟會為您的應用程式產生三年的憑證。</span><span class="sxs-lookup"><span data-stu-id="12445-125">This step generates a three-year certificate for your application.</span></span>

4. <span data-ttu-id="12445-126">toocreate 新的憑證，按一下 hello**建立新憑證**hello 中的連結**SAML 簽章憑證**> 一節。</span><span class="sxs-lookup"><span data-stu-id="12445-126">toocreate a new certificate, click hello **Create new certificate** link in hello **SAML Signing Certificate** section.</span></span>

    ![產生新的憑證](./media/active-directory-sso-certs/create_new_certficate.png)

5. <span data-ttu-id="12445-128">hello**建立新的憑證**連結會開啟 hello 行事曆控制項。</span><span class="sxs-lookup"><span data-stu-id="12445-128">hello **Create a new certificate** link opens hello calendar control.</span></span> <span data-ttu-id="12445-129">您可以設定任何日期和時間設定 toothree 年 hello 從目前的日期。</span><span class="sxs-lookup"><span data-stu-id="12445-129">You can set any date and time up toothree years from hello current date.</span></span> <span data-ttu-id="12445-130">hello 選取日期和時間是您的新憑證的 hello 新的到期日期和時間。</span><span class="sxs-lookup"><span data-stu-id="12445-130">hello selected date and time is hello new expiration date and time of your new certificate.</span></span> <span data-ttu-id="12445-131">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="12445-131">Click **Save**.</span></span>

    ![下載，然後上傳 hello 憑證](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. <span data-ttu-id="12445-133">現在可用 toodownload hello 新憑證。</span><span class="sxs-lookup"><span data-stu-id="12445-133">Now hello new certificate is available toodownload.</span></span> <span data-ttu-id="12445-134">按一下 hello**憑證**連結 toodownload 它。</span><span class="sxs-lookup"><span data-stu-id="12445-134">Click hello **Certificate** link toodownload it.</span></span> <span data-ttu-id="12445-135">此時，您的憑證不在作用中。</span><span class="sxs-lookup"><span data-stu-id="12445-135">At this point, your certificate is not active.</span></span> <span data-ttu-id="12445-136">當您想 tooroll toothis 憑證上時，選取 hello**啟用新的憑證**核取方塊，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="12445-136">When you want tooroll over toothis certificate, select hello **Make new certificate active** check box and click **Save**.</span></span> <span data-ttu-id="12445-137">從該點，Azure AD 會開始使用簽署 hello 回應 hello 新憑證。</span><span class="sxs-lookup"><span data-stu-id="12445-137">From that point, Azure AD starts using hello new certificate for signing hello response.</span></span>

7.  <span data-ttu-id="12445-138">toolearn 如何 tooupload hello 憑證 tooyour 特定 SaaS 應用程式，請按一下 hello**檢視應用程式設定教學課程**連結。</span><span class="sxs-lookup"><span data-stu-id="12445-138">toolearn how tooupload hello certificate tooyour particular SaaS application, click hello **View application configuration tutorial** link.</span></span>

## <a name="renew-a-certificate-that-will-soon-expire"></a><span data-ttu-id="12445-139">更新即將到期的憑證</span><span class="sxs-lookup"><span data-stu-id="12445-139">Renew a certificate that will soon expire</span></span>
<span data-ttu-id="12445-140">hello 下列更新步驟應該導致為您的使用者沒有顯著的停機時間。</span><span class="sxs-lookup"><span data-stu-id="12445-140">hello following renewal steps should result in no significant downtime for your users.</span></span> <span data-ttu-id="12445-141">此區段功能 Salesforce 做為範例，但下列步驟中的 hello 螢幕擷取畫面可以套用 tooany 同盟 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="12445-141">hello screenshots in this section feature Salesforce as an example, but these steps can apply tooany federated SaaS app.</span></span>

1. <span data-ttu-id="12445-142">在 [hello **Azure Active Directory**應用程式**單一登入**頁面上，產生您的應用程式的 hello 新憑證。</span><span class="sxs-lookup"><span data-stu-id="12445-142">On hello **Azure Active Directory** application **Single sign-on** page, generate hello new certificate for your application.</span></span> <span data-ttu-id="12445-143">您可以按一下 hello**建立新憑證**hello 中的連結**SAML 簽章憑證**> 一節。</span><span class="sxs-lookup"><span data-stu-id="12445-143">You can do this by clicking hello **Create new certificate** link in hello **SAML Signing Certificate** section.</span></span>

    ![產生新的憑證](./media/active-directory-sso-certs/create_new_certficate.png)

2. <span data-ttu-id="12445-145">選取 hello 預期到期日期和時間，新的憑證然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="12445-145">Select hello desired expiration date and time for your new certificate and click **Save**.</span></span>

3. <span data-ttu-id="12445-146">下載 hello 憑證在 hello **SAML 簽章憑證**選項。</span><span class="sxs-lookup"><span data-stu-id="12445-146">Download hello certificate in hello **SAML Signing certificate** option.</span></span> <span data-ttu-id="12445-147">上傳 hello 新憑證 toohello SaaS 應用程式的單一登入組態畫面。</span><span class="sxs-lookup"><span data-stu-id="12445-147">Upload hello new certificate toohello SaaS application's single sign-on configuration screen.</span></span> <span data-ttu-id="12445-148">toolearn 如何 toodo 特定 SaaS 應用程式，請按一下 hello**檢視應用程式設定教學課程**連結。</span><span class="sxs-lookup"><span data-stu-id="12445-148">toolearn how toodo this for your particular SaaS application, click hello **View application configuration tutorial** link.</span></span>
   
4. <span data-ttu-id="12445-149">在 Azure AD 中，選取 hello tooactivate hello 新憑證**啟用新的憑證**核取方塊，然後按一下 hello**儲存**hello hello 頁頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="12445-149">tooactivate hello new certificate in Azure AD, select hello **Make new certificate active** check box and click hello **Save** button at hello top of hello page.</span></span> <span data-ttu-id="12445-150">這在 Azure AD 戶端 hello 彙總 hello 新憑證。</span><span class="sxs-lookup"><span data-stu-id="12445-150">This rolls over hello new certificate on hello Azure AD side.</span></span> <span data-ttu-id="12445-151">hello hello 憑證狀態變更從**新增**太**Active**。</span><span class="sxs-lookup"><span data-stu-id="12445-151">hello status of hello certificate changes from **New** too**Active**.</span></span> <span data-ttu-id="12445-152">從該點，Azure AD 會開始使用簽署 hello 回應 hello 新憑證。</span><span class="sxs-lookup"><span data-stu-id="12445-152">From that point, Azure AD starts using hello new certificate for signing hello response.</span></span> 
   
    ![產生新的憑證](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a><span data-ttu-id="12445-154">相關文章</span><span class="sxs-lookup"><span data-stu-id="12445-154">Related articles</span></span>
* [<span data-ttu-id="12445-155">如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12445-155">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="12445-156">Azure Active Directory 中應用程式管理的文件索引</span><span class="sxs-lookup"><span data-stu-id="12445-156">Article index for application management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="12445-157">搭配 Azure Active Directory 的應用程式存取和單一登入</span><span class="sxs-lookup"><span data-stu-id="12445-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="12445-158">針對 SAML 型單一登入進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="12445-158">Troubleshooting SAML-based single sign-on</span></span>](active-directory-saml-debugging.md)
