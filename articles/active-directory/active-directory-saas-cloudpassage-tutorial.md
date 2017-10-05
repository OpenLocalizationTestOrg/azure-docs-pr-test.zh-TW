---
title: "教學課程：Azure Active Directory 與 CloudPassage 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 CloudPassage 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 094740e20570665e975dec1a591989e411f90c16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="50b09-103">教學課程：Azure Active Directory 與 CloudPassage 整合</span><span class="sxs-lookup"><span data-stu-id="50b09-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="50b09-104">在本教學課程中，您會了解如何整合 CloudPassage 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="50b09-104">In this tutorial, you learn how to integrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="50b09-105">CloudPassage 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="50b09-105">Integrating CloudPassage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="50b09-106">您可以在 Azure AD 中控制可存取 CloudPassage 的人員</span><span class="sxs-lookup"><span data-stu-id="50b09-106">You can control in Azure AD who has access to CloudPassage</span></span>
- <span data-ttu-id="50b09-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 CloudPassage (單一登入)</span><span class="sxs-lookup"><span data-stu-id="50b09-107">You can enable your users to automatically get signed-on to CloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="50b09-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="50b09-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="50b09-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="50b09-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50b09-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="50b09-110">Prerequisites</span></span>

<span data-ttu-id="50b09-111">若要設定 Azure AD 與 CloudPassage 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="50b09-111">To configure Azure AD integration with CloudPassage, you need the following items:</span></span>

- <span data-ttu-id="50b09-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="50b09-112">An Azure AD subscription</span></span>
- <span data-ttu-id="50b09-113">已啟用 CloudPassage 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="50b09-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="50b09-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="50b09-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="50b09-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="50b09-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="50b09-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="50b09-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="50b09-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="50b09-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="50b09-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="50b09-118">Scenario description</span></span>
<span data-ttu-id="50b09-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="50b09-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="50b09-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="50b09-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="50b09-121">從資源庫新增 CloudPassage</span><span class="sxs-lookup"><span data-stu-id="50b09-121">Adding CloudPassage from the gallery</span></span>
2. <span data-ttu-id="50b09-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="50b09-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-the-gallery"></a><span data-ttu-id="50b09-123">從資源庫新增 CloudPassage</span><span class="sxs-lookup"><span data-stu-id="50b09-123">Adding CloudPassage from the gallery</span></span>
<span data-ttu-id="50b09-124">若要設定 CloudPassage 與 Azure AD 整合，您需要從資源庫將 CloudPassage 新增到受管理的 SaaS App 清單。</span><span class="sxs-lookup"><span data-stu-id="50b09-124">To configure the integration of CloudPassage into Azure AD, you need to add CloudPassage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="50b09-125">**若要從資源庫新增 CloudPassage，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="50b09-125">**To add CloudPassage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="50b09-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="50b09-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="50b09-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="50b09-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="50b09-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="50b09-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="50b09-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="50b09-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="50b09-133">在搜尋方塊中，輸入 **CloudPassage**。</span><span class="sxs-lookup"><span data-stu-id="50b09-133">In the search box, type **CloudPassage**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="50b09-135">在結果窗格中，選取 [CloudPassage]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="50b09-135">In the results panel, select **CloudPassage**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="50b09-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="50b09-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="50b09-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 CloudPassage 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="50b09-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="50b09-139">若要讓單一登入運作，Azure AD 必須知道 CloudPassage 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="50b09-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CloudPassage is to a user in Azure AD.</span></span> <span data-ttu-id="50b09-140">換句話說，必須在 Azure AD 使用者和 CloudPassage 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="50b09-140">In other words, a link relationship between an Azure AD user and the related user in CloudPassage needs to be established.</span></span>

<span data-ttu-id="50b09-141">在 CloudPassage 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="50b09-141">In CloudPassage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="50b09-142">若要使用 CloudPassage 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="50b09-142">To configure and test Azure AD single sign-on with CloudPassage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="50b09-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="50b09-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="50b09-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="50b09-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="50b09-145">**[建立 CloudPassage 測試使用者](#creating-a-cloudpassage-test-user)** - 在 CloudPassage 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="50b09-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - to have a counterpart of Britta Simon in CloudPassage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="50b09-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="50b09-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="50b09-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="50b09-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="50b09-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="50b09-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="50b09-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 CloudPassage 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="50b09-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="50b09-150">**若要使用 CloudPassage 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="50b09-150">**To configure Azure AD single sign-on with CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="50b09-151">在 Azure 入口網站的 [CloudPassage] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="50b09-151">In the Azure portal, on the **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="50b09-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="50b09-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="50b09-155">在 [CloudPassage 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="50b09-155">On the **CloudPassage Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="50b09-157">a.</span><span class="sxs-lookup"><span data-stu-id="50b09-157">a.</span></span> <span data-ttu-id="50b09-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="50b09-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="50b09-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="50b09-159">b.</span></span> <span data-ttu-id="50b09-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://portal.cloudpassage.com/saml/consume/accountid`。</span><span class="sxs-lookup"><span data-stu-id="50b09-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="50b09-161">您也可以在 CloudPassage 入口網站的 [單一登入設定] 區段中按一下 [SSO 安裝文件]，為這個屬性設定值。</span><span class="sxs-lookup"><span data-stu-id="50b09-161">You can get your value for this attribute by clicking **SSO Setup documentation** in the **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="50b09-163">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="50b09-163">These values are not real.</span></span> <span data-ttu-id="50b09-164">使用實際的回覆 URL 與登入 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="50b09-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="50b09-165">請連絡 [CloudPassage 用戶端支援小組](https://www.cloudpassage.com/company/contact/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="50b09-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) to get these values.</span></span> 

4. <span data-ttu-id="50b09-166">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="50b09-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="50b09-168">您的 CloudPassage 應用程式需要特定格式的 SAML 判斷提示，其會要求您將自訂屬性對應新增到 SAML Token 屬性設定。</span><span class="sxs-lookup"><span data-stu-id="50b09-168">Your CloudPassage application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="50b09-169">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="50b09-169">The following screenshot shows an example for this.</span></span>
   
   ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="50b09-171">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如上圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="50b09-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>

    | <span data-ttu-id="50b09-172">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="50b09-172">Attribute Name</span></span> | <span data-ttu-id="50b09-173">屬性值</span><span class="sxs-lookup"><span data-stu-id="50b09-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="50b09-174">firstname</span><span class="sxs-lookup"><span data-stu-id="50b09-174">firstname</span></span> |<span data-ttu-id="50b09-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="50b09-175">user.givenname</span></span> |
    | <span data-ttu-id="50b09-176">lastname</span><span class="sxs-lookup"><span data-stu-id="50b09-176">lastname</span></span> |<span data-ttu-id="50b09-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="50b09-177">user.surname</span></span> |
    | <span data-ttu-id="50b09-178">電子郵件</span><span class="sxs-lookup"><span data-stu-id="50b09-178">email</span></span> |<span data-ttu-id="50b09-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="50b09-179">user.mail</span></span> |
    
    <span data-ttu-id="50b09-180">a.</span><span class="sxs-lookup"><span data-stu-id="50b09-180">a.</span></span> <span data-ttu-id="50b09-181">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="50b09-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="50b09-184">b.</span><span class="sxs-lookup"><span data-stu-id="50b09-184">b.</span></span> <span data-ttu-id="50b09-185">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="50b09-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="50b09-186">c.</span><span class="sxs-lookup"><span data-stu-id="50b09-186">c.</span></span> <span data-ttu-id="50b09-187">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="50b09-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="50b09-188">d.</span><span class="sxs-lookup"><span data-stu-id="50b09-188">d.</span></span> <span data-ttu-id="50b09-189">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="50b09-189">Click **Ok**.</span></span>

7. <span data-ttu-id="50b09-190">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="50b09-190">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="50b09-192">在 [CloudPassage 組態] 區段上，按一下 [設定 CloudPassage] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="50b09-192">On the **CloudPassage Configuration** section, click **Configure CloudPassage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="50b09-193">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="50b09-193">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="50b09-195">在不同的瀏覽器視窗中，以系統管理員身分登入您的 CloudPassage 公司網站。</span><span class="sxs-lookup"><span data-stu-id="50b09-195">In a different browser window, sign-on to your CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="50b09-196">在頂端功能表中，按一下 [設定]，然後按一下 [網站管理]。</span><span class="sxs-lookup"><span data-stu-id="50b09-196">In the menu on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![設定單一登入][12]

11. <span data-ttu-id="50b09-198">按一下 [驗證設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="50b09-198">Click the **Authentication Settings** tab.</span></span> 
   
    ![設定單一登入][13]

12. <span data-ttu-id="50b09-200">在 [單一登入設定]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="50b09-200">In the **Single Sign-on Settings** section, perform the following steps:</span></span> 
   
    ![設定單一登入][14]

    <span data-ttu-id="50b09-202">a.</span><span class="sxs-lookup"><span data-stu-id="50b09-202">a.</span></span> <span data-ttu-id="50b09-203">選取 [啟用單一登入 (SSO) (SSO 安裝程式文件)/] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="50b09-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="50b09-204">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="50b09-204">b.</span></span> <span data-ttu-id="50b09-205">將 [SAML 實體識別碼] 貼入 [SAML 簽發者 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="50b09-205">Paste **SAML Entity ID** into the **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="50b09-206">c.</span><span class="sxs-lookup"><span data-stu-id="50b09-206">c.</span></span> <span data-ttu-id="50b09-207">將 [SAML 單一登入服務 URL] 貼入 [登入入口網站 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="50b09-207">Paste **SAML Single Sign-On Service URL** into the **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="50b09-208">d.</span><span class="sxs-lookup"><span data-stu-id="50b09-208">d.</span></span> <span data-ttu-id="50b09-209">將 [登出 URL] 貼入 [登出登陸頁面] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="50b09-209">Paste **Sign-Out URL** into the **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="50b09-210">e.</span><span class="sxs-lookup"><span data-stu-id="50b09-210">e.</span></span> <span data-ttu-id="50b09-211">在記事本中開啟您下載的憑證，將已下載憑證的內容複製到剪貼簿上，然後貼到 [x 509 憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="50b09-211">Open your downloaded certificate in notepad, copy the content of downloaded certificate into your clipboard, and then paste it into the **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="50b09-212">f.</span><span class="sxs-lookup"><span data-stu-id="50b09-212">f.</span></span> <span data-ttu-id="50b09-213">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="50b09-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="50b09-214">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="50b09-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="50b09-215">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="50b09-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="50b09-216">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="50b09-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="50b09-217">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="50b09-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="50b09-218">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="50b09-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="50b09-220">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="50b09-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="50b09-221">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="50b09-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="50b09-223">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="50b09-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="50b09-225">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="50b09-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="50b09-227">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="50b09-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="50b09-229">a.</span><span class="sxs-lookup"><span data-stu-id="50b09-229">a.</span></span> <span data-ttu-id="50b09-230">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="50b09-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="50b09-231">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="50b09-231">b.</span></span> <span data-ttu-id="50b09-232">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="50b09-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="50b09-233">c.</span><span class="sxs-lookup"><span data-stu-id="50b09-233">c.</span></span> <span data-ttu-id="50b09-234">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="50b09-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="50b09-235">d.</span><span class="sxs-lookup"><span data-stu-id="50b09-235">d.</span></span> <span data-ttu-id="50b09-236">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="50b09-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="50b09-237">建立 CloudPassage 測試使用者</span><span class="sxs-lookup"><span data-stu-id="50b09-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="50b09-238">本節目標是在 CloudPassage 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="50b09-238">The objective of this section is to create a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="50b09-239">**若要在 CloudPassage 中建立名為 Britta Simon 的使用者，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="50b09-239">**To create a user called Britta Simon in CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="50b09-240">以系統管理員身分登入您的 **CloudPassage** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="50b09-240">Sign-on to your **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="50b09-241">在頂端工具列中，按一下 [設定]，然後按一下 [網站管理]。</span><span class="sxs-lookup"><span data-stu-id="50b09-241">In the toolbar on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![建立 CloudPassage 測試使用者][22] 

3. <span data-ttu-id="50b09-243">按一下 [使用者] 索引標籤，然後按一下 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="50b09-243">Click the **Users** tab, and then click **Add New User**.</span></span> 
   
   ![建立 CloudPassage 測試使用者][23]

4. <span data-ttu-id="50b09-245">在 [新增使用者]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="50b09-245">In the **Add New User** section, perform the following steps:</span></span> 
   
   ![建立 CloudPassage 測試使用者][24]
    
    <span data-ttu-id="50b09-247">a.</span><span class="sxs-lookup"><span data-stu-id="50b09-247">a.</span></span> <span data-ttu-id="50b09-248">在 [名字] 文字方塊中，輸入 Britta。</span><span class="sxs-lookup"><span data-stu-id="50b09-248">In the **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="50b09-249">b.</span><span class="sxs-lookup"><span data-stu-id="50b09-249">b.</span></span> <span data-ttu-id="50b09-250">在 [姓氏] 文字方塊中，輸入 Simon。</span><span class="sxs-lookup"><span data-stu-id="50b09-250">In the **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="50b09-251">c.</span><span class="sxs-lookup"><span data-stu-id="50b09-251">c.</span></span> <span data-ttu-id="50b09-252">在 [使用者名稱] 文字方塊、[電子郵件] 文字方塊和 [重新輸入電子郵件] 文字方塊中，輸入 Britta 在 Azure AD 中的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="50b09-252">In the **Username** textbox, the **Email** textbox and the **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="50b09-253">d.</span><span class="sxs-lookup"><span data-stu-id="50b09-253">d.</span></span> <span data-ttu-id="50b09-254">對於 [存取類型]，選取 [啟用 Halo 入口網站存取]。</span><span class="sxs-lookup"><span data-stu-id="50b09-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="50b09-255">e.</span><span class="sxs-lookup"><span data-stu-id="50b09-255">e.</span></span> <span data-ttu-id="50b09-256">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="50b09-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="50b09-257">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="50b09-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="50b09-258">在本節中，您會將 CloudPassage 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="50b09-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CloudPassage.</span></span>

![指派使用者][200] 

<span data-ttu-id="50b09-260">**若要將 Britta Simon 指派到 CloudPassage，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="50b09-260">**To assign Britta Simon to CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="50b09-261">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="50b09-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="50b09-263">在應用程式清單中，選取 [CloudPassage] 。</span><span class="sxs-lookup"><span data-stu-id="50b09-263">In the applications list, select **CloudPassage**.</span></span>

    ![設定單一登入](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="50b09-265">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="50b09-265">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="50b09-267">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="50b09-267">Click **Add** button.</span></span> <span data-ttu-id="50b09-268">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="50b09-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="50b09-270">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="50b09-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="50b09-271">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="50b09-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="50b09-272">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="50b09-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="50b09-273">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="50b09-273">Testing single sign-on</span></span>

<span data-ttu-id="50b09-274">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="50b09-274">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="50b09-275">當您在存取面板中按一下 [CloudPassage] 磚時，應該會自動登入您的 CloudPassage 應用程式。</span><span class="sxs-lookup"><span data-stu-id="50b09-275">When you click the CloudPassage tile in the Access Panel, you should get automatically signed-on to your CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="50b09-276">其他資源</span><span class="sxs-lookup"><span data-stu-id="50b09-276">Additional resources</span></span>

* [<span data-ttu-id="50b09-277">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="50b09-277">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="50b09-278">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="50b09-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

