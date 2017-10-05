---
title: "教學課程：Azure Active Directory 與 Adobe Creative Cloud 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Adobe Creative Cloud 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 3d13608612c77236346b0e98551d7fc427d602e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="d46d0-103">教學課程：Azure Active Directory 與 Adobe Creative Cloud 整合</span><span class="sxs-lookup"><span data-stu-id="d46d0-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="d46d0-104">在本教學課程中，您會了解如何整合 Adobe Creative Cloud 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d46d0-104">In this tutorial, you learn how to integrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d46d0-105">Adobe Creative Cloud 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="d46d0-105">Integrating Adobe Creative Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d46d0-106">您可以在 Azure AD 中控制可存取 Adobe Creative Cloud 的人員</span><span class="sxs-lookup"><span data-stu-id="d46d0-106">You can control in Azure AD who has access to Adobe Creative Cloud</span></span>
- <span data-ttu-id="d46d0-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Adobe Creative Cloud (單一登入)</span><span class="sxs-lookup"><span data-stu-id="d46d0-107">You can enable your users to automatically get signed-on to Adobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d46d0-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="d46d0-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="d46d0-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d46d0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d46d0-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d46d0-110">Prerequisites</span></span>

<span data-ttu-id="d46d0-111">若要設定 Azure AD 與 Adobe Creative Cloud 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="d46d0-111">To configure Azure AD integration with Adobe Creative Cloud, you need the following items:</span></span>

- <span data-ttu-id="d46d0-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d46d0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d46d0-113">已啟用 Adobe Creative Cloud 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d46d0-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d46d0-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d46d0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d46d0-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d46d0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d46d0-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="d46d0-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d46d0-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="d46d0-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d46d0-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="d46d0-118">Scenario description</span></span>
<span data-ttu-id="d46d0-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d46d0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d46d0-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="d46d0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d46d0-121">從資源庫新增 Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="d46d0-121">Adding Adobe Creative Cloud from the gallery</span></span>
2. <span data-ttu-id="d46d0-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d46d0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-the-gallery"></a><span data-ttu-id="d46d0-123">從資源庫新增 Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="d46d0-123">Adding Adobe Creative Cloud from the gallery</span></span>
<span data-ttu-id="d46d0-124">若要設定將 Adobe Creative Cloud 整合至 Azure AD 中，您需要從資源庫將 Adobe Creative Cloud 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="d46d0-124">To configure the integration of Adobe Creative Cloud into Azure AD, you need to add Adobe Creative Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d46d0-125">**若要從資源庫新增 Adobe Creative Cloud，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d46d0-125">**To add Adobe Creative Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d46d0-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d46d0-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d46d0-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d46d0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d46d0-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d46d0-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="d46d0-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d46d0-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="d46d0-133">在搜尋方塊中，輸入 [Adobe Creative Cloud]。</span><span class="sxs-lookup"><span data-stu-id="d46d0-133">In the search box, type **Adobe Creative Cloud**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="d46d0-135">在結果窗格中，選取 [Adobe Creative Cloud]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="d46d0-135">In the results panel, select **Adobe Creative Cloud**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d46d0-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d46d0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d46d0-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Adobe Creative Cloud 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d46d0-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d46d0-139">若要讓單一登入能夠運作，Azure AD 必須知道 Adobe Creative Cloud 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="d46d0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Creative Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="d46d0-140">換句話說，必須在 Azure AD 使用者與 Adobe Creative Cloud 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d46d0-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Creative Cloud needs to be established.</span></span>

<span data-ttu-id="d46d0-141">建立此連結關聯性的方法，是將 Azure AD 中**使用者名稱**的值指派為 Adobe Creative Cloud 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="d46d0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="d46d0-142">若要設定及測試與 Adobe Creative Cloud 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="d46d0-142">To configure and test Azure AD single sign-on with Adobe Creative Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d46d0-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="d46d0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d46d0-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d46d0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d46d0-145">**[建立 Adobe Creative Cloud 測試使用者](#creating-an-adobe-creative-cloud-test-user)** - 在 Adobe Creative Cloud 中，建立一個與 Azure AD 中代表 Britta Simon 的項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="d46d0-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - to have a counterpart of Britta Simon in Adobe Creative Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d46d0-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d46d0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d46d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="d46d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d46d0-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d46d0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d46d0-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 Adobe Creative Cloud 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d46d0-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="d46d0-150">**若要設定與 Adobe Creative Cloud 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d46d0-150">**To configure Azure AD single sign-on with Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="d46d0-151">在 Azure 管理入口網站的 [Adobe Creative Cloud] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="d46d0-151">In the Azure Management portal, on the **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="d46d0-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="d46d0-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="d46d0-155">如果您想要以 **IDP** 起始模式設定應用程式，請在 [Adobe Creative Cloud 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d46d0-155">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="d46d0-157">a.</span><span class="sxs-lookup"><span data-stu-id="d46d0-157">a.</span></span> <span data-ttu-id="d46d0-158">在 [識別碼] 文字方塊中，以下列形式輸入值：`https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="d46d0-158">In the **Identifier** textbox, type the value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="d46d0-159">b.</span><span class="sxs-lookup"><span data-stu-id="d46d0-159">b.</span></span> <span data-ttu-id="d46d0-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="d46d0-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d46d0-161">請注意這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="d46d0-161">Please note that these are not the real values.</span></span> <span data-ttu-id="d46d0-162">您必須使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="d46d0-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="d46d0-163">在此建議您在 [識別碼] 中使用唯一的字串值。</span><span class="sxs-lookup"><span data-stu-id="d46d0-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="d46d0-164">如果您需要手動建立使用者，請連絡 Adobe Creative Cloud 支援小組。</span><span class="sxs-lookup"><span data-stu-id="d46d0-164">If you need to create an user manually, you need to contact the Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="d46d0-165">如果您想要以  起始模式設定應用程式，請在 [Adobe Creative Cloud 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d46d0-165">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="d46d0-167">a.</span><span class="sxs-lookup"><span data-stu-id="d46d0-167">a.</span></span> <span data-ttu-id="d46d0-168">按一下 [顯示進階 URL 設定] 選項</span><span class="sxs-lookup"><span data-stu-id="d46d0-168">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="d46d0-169">b.</span><span class="sxs-lookup"><span data-stu-id="d46d0-169">b.</span></span> <span data-ttu-id="d46d0-170">在 [登入 URL] 文字方塊中，輸入下列值：`https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="d46d0-170">In the **Sign-on URL** textbox, type the value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="d46d0-171">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="d46d0-171">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="d46d0-173">在 [Adobe Creative Cloud 組態] 區段中，按一下 [設定 Adobe Creative Cloud] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="d46d0-173">On the **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d46d0-174">請從 [快速參考] 區段複製 [SAML 實體 ID] 和 [SAML SSO 服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="d46d0-174">Please copy the **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="d46d0-176">在不同的網頁瀏覽器視窗中，以管理員身分登入您的 Adobe Creative Cloud 租用戶。</span><span class="sxs-lookup"><span data-stu-id="d46d0-176">In a different web browser window, sign-on to your Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="d46d0-177">移至左側瀏覽窗格上的 [身分識別]，然後按一下您的網域。</span><span class="sxs-lookup"><span data-stu-id="d46d0-177">Go to **Identity** on the left navigation pane and click your domain.</span></span> <span data-ttu-id="d46d0-178">接著執行 [需要單一登入組態] 區段中的下列步驟。</span><span class="sxs-lookup"><span data-stu-id="d46d0-178">Then perform the following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="d46d0-179">![設定](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "設定")</span><span class="sxs-lookup"><span data-stu-id="d46d0-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="d46d0-180">按一下 [瀏覽]，將已從 Azure AD 下載的憑證上傳至 **IDP 憑證**。</span><span class="sxs-lookup"><span data-stu-id="d46d0-180">Click **Browse** to upload the downloaded certificate from Azure AD to **IDP Certificate**.</span></span>

10. <span data-ttu-id="d46d0-181">在 [IDP 簽發者] 文字方塊中，放入 [SAML 實體 ID] 的值，該值是您從 Azure 入口網站的 [設定登入] 區段複製而來。</span><span class="sxs-lookup"><span data-stu-id="d46d0-181">In the **IDP issuer** textbox, put the value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="d46d0-182">在 [IDP 登入 URL] 文字方塊中，放入 [SAML SSO 服務 URL] 的值，該值是您從 Azure 入口網站的 [設定登入] 區段複製而來。</span><span class="sxs-lookup"><span data-stu-id="d46d0-182">In the **IDP Login URL** textbox, put the value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="d46d0-183">選取 [HTTP - 重新導向] 作為 **IDP 繫結**。</span><span class="sxs-lookup"><span data-stu-id="d46d0-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="d46d0-184">選取 [電子郵件地址] 作為**使用者登入設定**。</span><span class="sxs-lookup"><span data-stu-id="d46d0-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="d46d0-185">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d46d0-185">Click **Save** button.</span></span>

15. <span data-ttu-id="d46d0-186">儀表板現在會顯示 XML「下載中繼資料」檔案。</span><span class="sxs-lookup"><span data-stu-id="d46d0-186">The dashboard will now present the XML **"Download Metadata"** file.</span></span> <span data-ttu-id="d46d0-187">它包含 Adobe 的 EntityDescriptor URL 和 AssertionConsumerService URL。</span><span class="sxs-lookup"><span data-stu-id="d46d0-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="d46d0-188">請開啟檔案，然後在 Azure AD 應用程式中加以設定。</span><span class="sxs-lookup"><span data-stu-id="d46d0-188">Please open the file and configure them in the Azure AD application.</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![在應用程式端設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="d46d0-191">a.</span><span class="sxs-lookup"><span data-stu-id="d46d0-191">a.</span></span> <span data-ttu-id="d46d0-192">在 [設定應用程式設定] 對話方塊上，使用 Adobe 提供給您的 EntityDescriptor 值作為**識別碼**。</span><span class="sxs-lookup"><span data-stu-id="d46d0-192">Use the EntityDescriptor value Adobe provided you for **Identifier** on the **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="d46d0-193">b.</span><span class="sxs-lookup"><span data-stu-id="d46d0-193">b.</span></span> <span data-ttu-id="d46d0-194">在 [設定應用程式設定] 對話方塊上，使用 Adobe 提供給您的 AssertionConsumerService 值作為**回覆 URL**。</span><span class="sxs-lookup"><span data-stu-id="d46d0-194">Use the AssertionConsumerService value Adobe provided you for **Reply URL** on the **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d46d0-195">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d46d0-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="d46d0-196">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d46d0-196">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="d46d0-198">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d46d0-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d46d0-199">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d46d0-199">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d46d0-201">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="d46d0-201">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d46d0-203">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d46d0-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d46d0-205">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d46d0-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d46d0-207">a.</span><span class="sxs-lookup"><span data-stu-id="d46d0-207">a.</span></span> <span data-ttu-id="d46d0-208">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d46d0-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d46d0-209">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d46d0-209">b.</span></span> <span data-ttu-id="d46d0-210">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="d46d0-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d46d0-211">c.</span><span class="sxs-lookup"><span data-stu-id="d46d0-211">c.</span></span> <span data-ttu-id="d46d0-212">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="d46d0-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d46d0-213">d.</span><span class="sxs-lookup"><span data-stu-id="d46d0-213">d.</span></span> <span data-ttu-id="d46d0-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d46d0-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="d46d0-215">建立 Adobe Creative Cloud 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d46d0-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="d46d0-216">若要讓 Azure AD 使用者能夠登入 Adobe Creative Cloud，必須將他們佈建到 Adobe Creative Cloud。</span><span class="sxs-lookup"><span data-stu-id="d46d0-216">In order to enable Azure AD users to log into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="d46d0-217">Adobe Creative Cloud 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="d46d0-217">In the case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="d46d0-218">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d46d0-218">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="d46d0-219">以系統管理員身分登入您的 Adobe Creative Cloud 公司網站。</span><span class="sxs-lookup"><span data-stu-id="d46d0-219">Log in to your Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="d46d0-220">按一下 [人員] 。</span><span class="sxs-lookup"><span data-stu-id="d46d0-220">Click **People**.</span></span>

    <span data-ttu-id="d46d0-221">![人員](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "人員")</span><span class="sxs-lookup"><span data-stu-id="d46d0-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="d46d0-222">按一下 [邀請使用者] 。</span><span class="sxs-lookup"><span data-stu-id="d46d0-222">Click **Invite User**.</span></span>

    <span data-ttu-id="d46d0-223">![邀請使用者](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "邀請使用者")</span><span class="sxs-lookup"><span data-stu-id="d46d0-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="d46d0-224">在 [邀請人員] 對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d46d0-224">On the **Invite People** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="d46d0-225">![邀請人員](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "邀請人員")</span><span class="sxs-lookup"><span data-stu-id="d46d0-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="d46d0-226">a.</span><span class="sxs-lookup"><span data-stu-id="d46d0-226">a.</span></span> <span data-ttu-id="d46d0-227">在 [電子郵件] 文字方塊中，輸入 Britta Simon 帳戶的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="d46d0-227">In the **Email** textbox, type the email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="d46d0-228">b.</span><span class="sxs-lookup"><span data-stu-id="d46d0-228">b.</span></span> <span data-ttu-id="d46d0-229">按一下 [邀請] 。</span><span class="sxs-lookup"><span data-stu-id="d46d0-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d46d0-230">Azure Active Directory 帳戶的持有者會收到一封電子郵件，並依照連結在啟用其帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="d46d0-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d46d0-231">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d46d0-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d46d0-232">在本節中，您會將 Adobe Creative Cloud 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d46d0-232">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Adobe Creative Cloud.</span></span>

![指派使用者][200] 

<span data-ttu-id="d46d0-234">**若要將 Britta Simon 指派給 Adobe Creative Cloud，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d46d0-234">**To assign Britta Simon to Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="d46d0-235">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d46d0-235">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="d46d0-237">在應用程式清單中，選取 [Adobe Creative Cloud]。</span><span class="sxs-lookup"><span data-stu-id="d46d0-237">In the applications list, select **Adobe Creative Cloud**.</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="d46d0-239">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d46d0-239">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="d46d0-241">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d46d0-241">Click **Add** button.</span></span> <span data-ttu-id="d46d0-242">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d46d0-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="d46d0-244">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="d46d0-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d46d0-245">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d46d0-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d46d0-246">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d46d0-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d46d0-247">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d46d0-247">Testing single sign-on</span></span>

<span data-ttu-id="d46d0-248">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="d46d0-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d46d0-249">當您在存取面板中按一下 [Adobe Creative Cloud] 圖格時，應該會自動登入您的 Adobe Creative Cloud 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d46d0-249">When you click the Adobe Creative Cloud tile in the Access Panel, you should get automatically signed-on to your Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d46d0-250">其他資源</span><span class="sxs-lookup"><span data-stu-id="d46d0-250">Additional resources</span></span>

* [<span data-ttu-id="d46d0-251">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="d46d0-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d46d0-252">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d46d0-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png