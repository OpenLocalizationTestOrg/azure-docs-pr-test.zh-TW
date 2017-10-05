---
title: "教學課程：Azure Active Directory 與 SAP HANA Cloud Platform Identity Authentication 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SAP HANA Cloud Platform Identity Authentication 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 7799bf03cc6705f805a48f329a265a3d84bed55f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="3f9c4-103">教學課程：Azure Active Directory 與 SAP HANA Cloud Platform Identity Authentication 整合</span><span class="sxs-lookup"><span data-stu-id="3f9c4-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="3f9c4-104">在本教學課程中，您會了解如何整合 SAP HANA Cloud Platform Identity Authentication 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-104">In this tutorial, you learn how to integrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="3f9c4-105">SAP HANA Cloud Platform Identity Authentication 可做為 Proxy IdP，來存取以 Azure AD 做為主要 IdP 的 SAP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP to access SAP applications using Azure AD as the main IdP.</span></span>

<span data-ttu-id="3f9c4-106">整合 SAP HANA Cloud Platform Identity Authentication 與 Azure AD 提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="3f9c4-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3f9c4-107">您可以在 Azure AD 中控制可存取 SAP 應用程式的人員</span><span class="sxs-lookup"><span data-stu-id="3f9c4-107">You can control in Azure AD who has access to SAP application</span></span>
- <span data-ttu-id="3f9c4-108">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SAP 應用程式單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="3f9c4-108">You can enable your users to automatically get signed-on to SAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="3f9c4-109">您可以在 Azure 傳統入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="3f9c4-109">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="3f9c4-110">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-110">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3f9c4-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="3f9c4-111">Prerequisites</span></span>

<span data-ttu-id="3f9c4-112">若要設定 Azure AD 與 SAP HANA Cloud Platform Identity Authentication 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="3f9c4-112">To configure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need the following items:</span></span>

- <span data-ttu-id="3f9c4-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3f9c4-113">An Azure AD subscription</span></span>
- <span data-ttu-id="3f9c4-114">已啟用 SSO 的 **SAP HANA Cloud Platform Identity Authentication** 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3f9c4-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="3f9c4-115">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="3f9c4-116">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="3f9c4-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3f9c4-117">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3f9c4-118">如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3f9c4-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="3f9c4-119">Scenario description</span></span>
<span data-ttu-id="3f9c4-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="3f9c4-121">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="3f9c4-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3f9c4-122">從資源庫新增 SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="3f9c4-122">Adding SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
2. <span data-ttu-id="3f9c4-123">設定並測試 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="3f9c4-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="3f9c4-124">深入探討技術細節之前，一定要了解您即將查看的概念。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-124">Before diving into the technical details, it is vital to understand the concepts you're going to look at.</span></span> <span data-ttu-id="3f9c4-125">SAP HANA Cloud Platform Identity Authentication 和 Azure Active Directory 同盟可讓您利用 SAP HANA Cloud Platform Identity Authentication 所保護的 SAP 應用程式和服務，跨越 AAD (如 IdP) 所保護的應用程式或服務實作 SSO。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-125">The SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you to implement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="3f9c4-126">SAP HANA Cloud Platform Identity Authentication 目前做為 SAP 應用程式的領導 Proxy 識別提供者。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider to SAP-applications.</span></span> <span data-ttu-id="3f9c4-127">而 Azure Active Directory 做為此設定中的識別提供者。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-127">Azure Active Directory in turn acts as the leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="3f9c4-128">下圖說明：</span><span class="sxs-lookup"><span data-stu-id="3f9c4-128">The following diagram illustrates this:</span></span>    

![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="3f9c4-130">透過此設定，您的 SAP HANA Cloud Platform Identity Authentication 租用戶會設定為 Azure Active Directory 中信任的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="3f9c4-131">接著會在 SAP HANA Cloud Platform Identity Authentication 管理主控台中設定您想透過此方式保護的所有 SAP 應用程式和服務！</span><span class="sxs-lookup"><span data-stu-id="3f9c4-131">All SAP applications and services you want to protect through this way are subsequently configured in the SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="3f9c4-132">這表示對於這類設定 (相對於在 Azure Active Directory 中設定授權)，必須在 SAP HANA Cloud Platform Identity Authentication 中進行授與 SAP 應用程式和服務存取權的授權作業。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-132">This means that authorization for granting access to SAP applications and services needs to take place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed to configuring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="3f9c4-133">透過 Azure Active Directory Marketplace 將 SAP HANA Cloud Platform Identity Authentication 設定為應用程式，您就不需處理所需個別宣告 / SAML 判斷提示和轉換的設定，即可為 SAP 應用程式產生有效的驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through the Azure Active Directory Marketplace, you don't need to take care of configuring needed individual claims / SAML assertions and transformations needed to produce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="3f9c4-134">Web SSO 目前只經過這兩個合作夥伴測試。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="3f9c4-135">應用程式對 API 或 API 對 API 通訊所需的流程應能運作，但尚未經過測試。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="3f9c4-136">它們會在後續活動中進行測試。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-the-gallery"></a><span data-ttu-id="3f9c4-137">從資源庫新增 SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="3f9c4-137">Add SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
<span data-ttu-id="3f9c4-138">若要設定將 SAP HANA Cloud Platform Identity Authentication 整合到 Azure AD 中，您需要將 SAP HANA Cloud Platform Identity Authentication 從資源庫新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-138">To configure the integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need to add SAP HANA Cloud Platform Identity Authentication from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3f9c4-139">**若要從資源庫新增 SAP HANA Cloud Platform Identity Authentication，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3f9c4-139">**To add SAP HANA Cloud Platform Identity Authentication from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3f9c4-140">在 [**Azure 管理入口網站**](https://portal.azure.com)的左側瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-140">In the [**Azure Management portal**](https://portal.azure.com), on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3f9c4-142">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-142">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3f9c4-143">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-143">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="3f9c4-145">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-145">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="3f9c4-147">在搜尋方塊中，輸入 **SAP HANA Cloud Platform Identity Authentication**。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-147">In the search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="3f9c4-149">在結果窗格中，選取 [SAP HANA Cloud Platform Identity Authentication]，然後按一下 [新增] 按鈕來新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-149">In the results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3f9c4-151">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3f9c4-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="3f9c4-152">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAP HANA Cloud Platform Identity Authentication 設定及測試 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3f9c4-153">若要讓 SSO 運作，Azure AD 必須知道 SAP HANA Cloud Platform Identity Authentication 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-153">For SSO to work, Azure AD needs to know what the counterpart user in SAP HANA Cloud Platform Identity Authentication is to a user in Azure AD.</span></span> <span data-ttu-id="3f9c4-154">換句話說，必須在 Azure AD 使用者與 SAP HANA Cloud Platform Identity Authentication 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-154">In other words, a link relationship between an Azure AD user and the related user in SAP HANA Cloud Platform Identity Authentication needs to be established.</span></span>

<span data-ttu-id="3f9c4-155">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值，指派為 SAP HANA Cloud Platform Identity Authentication 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-155">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="3f9c4-156">若要使用 SAP HANA Cloud Platform Identity Authentication 來設定並測試 Azure AD SSO，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="3f9c4-156">To configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3f9c4-157">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3f9c4-158">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3f9c4-159">**[建立 SAP HANA Cloud Platform Identity Authentication 測試使用者](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - 使 SAP HANA Cloud Platform Identity Authentication 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - to have a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="3f9c4-160">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-160">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3f9c4-161">**[測試單一登入](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-161">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="3f9c4-162">設定 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="3f9c4-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="3f9c4-163">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD SSO，並在您的 SAP HANA Cloud Platform Identity Authentication 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-163">In this section, you enable Azure AD SSO in the Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="3f9c4-164">SAP HANA Cloud Platform Identity Authentication 應用程式需要特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-164">SAP HANA Cloud Platform Identity Authentication application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="3f9c4-165">您可以在應用程式整合頁面的 [使用者屬性] 區段中管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="3f9c4-166">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-166">The following screenshot shows an example for this.</span></span>

![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="3f9c4-168">**若要使用 SAP HANA Cloud Platform Identity Authentication 設定 Azure AD SSO，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3f9c4-168">**To configure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="3f9c4-169">在 Azure 管理入口網站的 [SAP HANA Cloud Platform Identity Authentication] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-169">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="3f9c4-171">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-171">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入][5]

3. <span data-ttu-id="3f9c4-173">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如果您的 SAP 應用程式預期屬性，例如 "firstName"。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-173">In the **User Attributes** section on the **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="3f9c4-174">在 [SAML Token 屬性] 對話方塊中新增 "firstName" 屬性。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-174">On the SAML token attributes dialog, add the "firstName" attribute.</span></span>
 1. <span data-ttu-id="3f9c4-175">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
 
    ![設定單一登入][6]

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="3f9c4-178">在 [屬性名稱] 文字方塊中，輸入屬性名稱 "firstName"。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-178">In the **Attribute Name** textbox, type the attribute name "firstName".</span></span>
 3. <span data-ttu-id="3f9c4-179">從 [屬性值] 清單選取 "user.givenname" 屬性值。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-179">From the **Attribute Value** list, select the attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="3f9c4-180">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-180">Click **Ok**.</span></span>

4. <span data-ttu-id="3f9c4-181">在 [SAP HANA Cloud Platform Identity Authentication 網域和 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3f9c4-181">On the **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="3f9c4-183">在 [登入 URL] 文字方塊中，輸入 SAP 應用程式的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-183">In the **Sign On URL** textbox, type the sign on URL for the SAP application.</span></span>
 2. <span data-ttu-id="3f9c4-184">在 [識別碼] 文字方塊中，輸入下列模式的值：`<entity-id>.accounts.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="3f9c4-184">In the **Identifier** textbox, type the value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="3f9c4-185">如果您不知道此值，請依照[租用戶 SAML 2.0 設定](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html)上的 SAP HANA Cloud Platform Identity Authentication 文件執行。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-185">If you don't know this value, please follow the SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="3f9c4-186">在 [SAP HANA Cloud Platform Identity Authentication 設定] 區段上，按一下 [設定 SAP HANA Cloud Platform Identity Authentication] 以開啟 [設定登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-186">On the **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** to open **Configure sign-on** dialog.</span></span> <span data-ttu-id="3f9c4-187">然後，按一下 [SAML XML 中繼資料] 並將檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-187">Then, click on **SAML XML Metadata** and save the file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="3f9c4-190">若要取得為您的應用程式設定的 SSO，請移至 SAP HANA Cloud Platform Identity Authentication 管理主控台。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-190">To get SSO configured for your application, go to SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="3f9c4-191">URL 具有下列模式：`https://<tenant-id>.accounts.ondemand.com/admin`</span><span class="sxs-lookup"><span data-stu-id="3f9c4-191">The URL has the following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="3f9c4-192">然後，遵循 SAP HANA Cloud Platform Identity Authentication 文件[將 Microsoft Azure AD 設定成為 SAP HANA Cloud Platform Identity Authentication 的公司識別提供者](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html)。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-192">Then, follow the documentation on SAP HANA Cloud Platform Identity Authentication to [Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="3f9c4-193">在 Azure 管理入口網站中，按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-193">In the Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="3f9c4-194">只有當您想要為另一個 SAP 應用程式新增和啟用 SSO 時，才繼續以下步驟。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-194">Continue the following steps only if you want to add and enable SSO for another SAP application.</span></span> <span data-ttu-id="3f9c4-195">重複＜從資源庫新增 SAP HANA Cloud Platform Identity Authentication＞一節下的步驟，新增另一個 SAP HANA Cloud Platform Identity Authentication 執行個體。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-195">Repeat steps under the section “Adding SAP HANA Cloud Platform Identity Authentication from the gallery” to add another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="3f9c4-196">在 Azure 管理入口網站的 [SAP HANA Cloud Platform Identity Authentication] 應用程式整合頁面上，按一下 [連結的登入]。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-196">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![設定連結的登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="3f9c4-198">然後儲存組態。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-198">Then, save the configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="3f9c4-199">新的應用程式將會利用先前 SAP 應用程式的 SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-199">The new application will leverage the SSO configuration for the previous SAP application.</span></span> <span data-ttu-id="3f9c4-200">請確定您在 SAP HANA Cloud Platform Identity Authentication 管理主控台中使用相同的公司識別提供者。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-200">Please make sure you use the same Corporate Identity Providers in the SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3f9c4-201">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3f9c4-201">Create an Azure AD test user</span></span>
<span data-ttu-id="3f9c4-202">本節的目標是要在新的入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-202">The objective of this section is to create a test user in the new portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="3f9c4-204">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3f9c4-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3f9c4-205">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-205">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3f9c4-207">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-207">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3f9c4-209">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-209">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3f9c4-211">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3f9c4-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="3f9c4-213">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-213">In the **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="3f9c4-214">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="3f9c4-215">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-215">Select **Show Password** and write down the value of the **Password**.</span></span>
  4. <span data-ttu-id="3f9c4-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="3f9c4-217">建立 SAP HANA Cloud Platform Identity Authentication 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3f9c4-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="3f9c4-218">您不需要在 SAP HANA Cloud Platform Identity Authentication 上建立使用者。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-218">You don't need to create an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="3f9c4-219">Azure AD 使用者存放區中的使用者可以使用 SSO 功能。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-219">Users who are in the Azure AD user store can use the SSO functionality.</span></span>

<span data-ttu-id="3f9c4-220">SAP HANA Cloud Platform Identity Authentication 支援 [識別身分同盟] 選項。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-220">SAP HANA Cloud Platform Identity Authentication supports the Identity Federation option.</span></span> <span data-ttu-id="3f9c4-221">此選項可讓應用程式檢查公司識別提供者所驗證的使用者是否存在於 SAP HANA Cloud Platform Identity Authentication 的使用者存放區中。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-221">This option allows the application to check if the users authenticated by the corporate identity provider exist in the user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="3f9c4-222">在預設設定中，[識別身分同盟] 選項已停用。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-222">In the default setting, the Identity Federation option is disabled.</span></span> <span data-ttu-id="3f9c4-223">如果已啟用 [識別身分同盟]，則只有匯入 SAP HANA Cloud Platform Identity Authentication 的使用者可以存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-223">If Identity Federation is enabled, only the users that are imported in SAP HANA Cloud Platform Identity Authentication are able to access the application.</span></span> 

<span data-ttu-id="3f9c4-224">如需如何啟用或停用與 SAP HANA Cloud Platform Identity Authentication 之識別身分同盟的詳細資訊，請參閱[設定與 SAP HANA Cloud Platform Identity Authentication 之使用者存放區的識別身分同盟](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html)中的〈啟用與 SAP HANA Cloud Platform Identity Authentication 的識別身分同盟〉。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-224">For more information about how to enable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with the User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3f9c4-225">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3f9c4-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="3f9c4-226">在本節中，您可將 SAP HANA Cloud Platform Identity Authentication 的存取權授予 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SAP HANA Cloud Platform Identity Authentication.</span></span>

![指派使用者][200] 

<span data-ttu-id="3f9c4-228">**若要將 Britta Simon 指派給 SAP HANA Cloud Platform Identity Authentication，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3f9c4-228">**To assign Britta Simon to SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="3f9c4-229">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="3f9c4-231">在應用程式清單中，選取 **SAP HANA Cloud Platform Identity Authentication**。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-231">In the applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="3f9c4-233">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-233">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="3f9c4-235">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-235">Click **Add** button.</span></span> <span data-ttu-id="3f9c4-236">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="3f9c4-238">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3f9c4-239">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3f9c4-240">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="3f9c4-241">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="3f9c4-241">Test single sign-on</span></span>

<span data-ttu-id="3f9c4-242">在本節中，您會使用存取面板來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-242">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="3f9c4-243">按一下存取面板中的 SAP HANA Cloud Platform Identity Authentication 圖格時，您應該會自動登入 SAP HANA Cloud Platform Identity Authentication 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f9c4-243">When you click the SAP HANA Cloud Platform Identity Authentication tile in the Access Panel, you should get automatically signed-on to your SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="3f9c4-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="3f9c4-244">Additional resources</span></span>

* [<span data-ttu-id="3f9c4-245">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="3f9c4-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3f9c4-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="3f9c4-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png