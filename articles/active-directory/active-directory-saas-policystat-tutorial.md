---
title: "教學課程：Azure Active Directory 與 PolicyStat 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 PolicyStat 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 704afd5515b02ce2a4fbf35da65fad74dc506271
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="dc506-103">教學課程：Azure Active Directory 與 PolicyStat 整合</span><span class="sxs-lookup"><span data-stu-id="dc506-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="dc506-104">在本教學課程中，您會了解如何整合 PolicyStat 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="dc506-104">In this tutorial, you learn how to integrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc506-105">PolicyStat 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="dc506-105">Integrating PolicyStat with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dc506-106">您可以在 Azure AD 中控制可存取 PolicyStat 的人員</span><span class="sxs-lookup"><span data-stu-id="dc506-106">You can control in Azure AD who has access to PolicyStat</span></span>
- <span data-ttu-id="dc506-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 PolicyStat (單一登入)</span><span class="sxs-lookup"><span data-stu-id="dc506-107">You can enable your users to automatically get signed-on to PolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dc506-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="dc506-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dc506-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="dc506-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc506-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="dc506-110">Prerequisites</span></span>

<span data-ttu-id="dc506-111">若要設定 Azure AD 與 PolicyStat 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="dc506-111">To configure Azure AD integration with PolicyStat, you need the following items:</span></span>

- <span data-ttu-id="dc506-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dc506-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc506-113">啟用 PolicyStat 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dc506-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc506-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="dc506-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dc506-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="dc506-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dc506-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="dc506-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dc506-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="dc506-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc506-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="dc506-118">Scenario description</span></span>
<span data-ttu-id="dc506-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dc506-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc506-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="dc506-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc506-121">從資源庫新增 PolicyStat</span><span class="sxs-lookup"><span data-stu-id="dc506-121">Adding PolicyStat from the gallery</span></span>
2. <span data-ttu-id="dc506-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="dc506-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-the-gallery"></a><span data-ttu-id="dc506-123">從資源庫新增 PolicyStat</span><span class="sxs-lookup"><span data-stu-id="dc506-123">Adding PolicyStat from the gallery</span></span>
<span data-ttu-id="dc506-124">若要設定將 PolicyStat 整合到 Azure AD 中，您需要從資源庫將 PolicyStat 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="dc506-124">To configure the integration of PolicyStat into Azure AD, you need to add PolicyStat from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dc506-125">**若要從資源庫新增 PolicyStat，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="dc506-125">**To add PolicyStat from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dc506-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="dc506-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dc506-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="dc506-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dc506-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="dc506-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="dc506-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc506-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="dc506-133">在搜尋方塊中，輸入 **PolicyStat**。</span><span class="sxs-lookup"><span data-stu-id="dc506-133">In the search box, type **PolicyStat**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="dc506-135">在結果面板中，選取 [PolicyStat]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc506-135">In the results panel, select **PolicyStat**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dc506-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="dc506-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dc506-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 PolicyStat 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dc506-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dc506-139">若要讓單一登入運作，Azure AD 必須知道 PolicyStat 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="dc506-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PolicyStat is to a user in Azure AD.</span></span> <span data-ttu-id="dc506-140">換句話說，必須在 Azure AD 使用者和 PolicyStat 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="dc506-140">In other words, a link relationship between an Azure AD user and the related user in PolicyStat needs to be established.</span></span>

<span data-ttu-id="dc506-141">在 PolicyStat 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="dc506-141">In PolicyStat, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dc506-142">若要設定及測試與 PolicyStat 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="dc506-142">To configure and test Azure AD single sign-on with PolicyStat, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dc506-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="dc506-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dc506-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dc506-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dc506-145">**[建立 PolicyStat 測試使用者](#creating-a-policystat-test-user)** - 使 PolicyStat 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="dc506-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - to have a counterpart of Britta Simon in PolicyStat that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dc506-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dc506-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dc506-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="dc506-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dc506-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="dc506-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dc506-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 PolicyStat 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="dc506-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="dc506-150">**若要設定與 PolicyStat 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="dc506-150">**To configure Azure AD single sign-on with PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="dc506-151">在 Azure 入口網站的 [PolicyStat] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="dc506-151">In the Azure portal, on the **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="dc506-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="dc506-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="dc506-155">在 [PolicyStat 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="dc506-155">On the **PolicyStat Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="dc506-157">a.</span><span class="sxs-lookup"><span data-stu-id="dc506-157">a.</span></span> <span data-ttu-id="dc506-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="dc506-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="dc506-159">b.</span><span class="sxs-lookup"><span data-stu-id="dc506-159">b.</span></span> <span data-ttu-id="dc506-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="dc506-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dc506-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="dc506-161">These values are not real.</span></span> <span data-ttu-id="dc506-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="dc506-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dc506-163">請連絡 [PolicyStat 客戶支援小組](http://www.policystat.com/support/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="dc506-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="dc506-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="dc506-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="dc506-166">本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己在 Azure AD 中的帳戶在 PolicyStat 中進行驗證。</span><span class="sxs-lookup"><span data-stu-id="dc506-166">The objective of this section is to outline how to enable users to authenticate to PolicyStat with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="dc506-167">PolicyStat 應用程式需要特定格式的 SAML 判斷提示，所以您必須將自訂屬性對應新增至 **SAML 權杖屬性**設定。</span><span class="sxs-lookup"><span data-stu-id="dc506-167">The PolicyStat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="dc506-168">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="dc506-168">The following screenshot shows an example of this.</span></span>

     <span data-ttu-id="dc506-169">![屬性](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="dc506-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="dc506-170">若要加入必要的屬性對應，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="dc506-170">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="dc506-171">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="dc506-171">Attribute Name</span></span>    |   <span data-ttu-id="dc506-172">屬性值</span><span class="sxs-lookup"><span data-stu-id="dc506-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="dc506-173">UID</span><span class="sxs-lookup"><span data-stu-id="dc506-173">uid</span></span> | <span data-ttu-id="dc506-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="dc506-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="dc506-175">a.</span><span class="sxs-lookup"><span data-stu-id="dc506-175">a.</span></span> <span data-ttu-id="dc506-176">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="dc506-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![設定單一登入](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="dc506-179">b.</span><span class="sxs-lookup"><span data-stu-id="dc506-179">b.</span></span> <span data-ttu-id="dc506-180">在 [屬性名稱] 文字方塊中，輸入 **uid**。</span><span class="sxs-lookup"><span data-stu-id="dc506-180">In the **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="dc506-181">c.</span><span class="sxs-lookup"><span data-stu-id="dc506-181">c.</span></span> <span data-ttu-id="dc506-182">在 [屬性值] 文字方塊中，選取 [ExtractMailPrefix()]。</span><span class="sxs-lookup"><span data-stu-id="dc506-182">In the **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="dc506-183">d.</span><span class="sxs-lookup"><span data-stu-id="dc506-183">d.</span></span> <span data-ttu-id="dc506-184">從 [郵件] 清單選取 [User.mail]。</span><span class="sxs-lookup"><span data-stu-id="dc506-184">From the **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="dc506-185">e.</span><span class="sxs-lookup"><span data-stu-id="dc506-185">e.</span></span> <span data-ttu-id="dc506-186">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="dc506-186">Click **Ok**</span></span>

7. <span data-ttu-id="dc506-187">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc506-187">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="dc506-189">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 PolicyStat 公司網站。</span><span class="sxs-lookup"><span data-stu-id="dc506-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="dc506-190">按一下 [管理] 索引標籤，然後按一下左側導覽窗格中的 [單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="dc506-190">Click the **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="dc506-191">![系統管理員功能表](./media/active-directory-saas-policystat-tutorial/ic808633.png "系統管理員功能表")</span><span class="sxs-lookup"><span data-stu-id="dc506-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="dc506-192">在 [安裝] 區段中，選取 [啟用單一登入整合]。</span><span class="sxs-lookup"><span data-stu-id="dc506-192">In the **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="dc506-193">![單一登入設定](./media/active-directory-saas-policystat-tutorial/ic808634.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="dc506-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="dc506-194">按一下 [設定屬性]，然後在 [設定屬性]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="dc506-194">Click **Configure Attributes**, and then, in the **Configure Attributes** section, perform the following steps:</span></span>
   
    <span data-ttu-id="dc506-195">![單一登入設定](./media/active-directory-saas-policystat-tutorial/ic808635.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="dc506-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="dc506-196">a.</span><span class="sxs-lookup"><span data-stu-id="dc506-196">a.</span></span> <span data-ttu-id="dc506-197">在 [使用者名稱屬性] 文字方塊中，輸入 **uid**。</span><span class="sxs-lookup"><span data-stu-id="dc506-197">In the **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="dc506-198">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc506-198">b.</span></span> <span data-ttu-id="dc506-199">在 [名字屬性] 文字方塊中，輸入使用者的**名字**：**Britta**。</span><span class="sxs-lookup"><span data-stu-id="dc506-199">In the **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="dc506-200">c.</span><span class="sxs-lookup"><span data-stu-id="dc506-200">c.</span></span> <span data-ttu-id="dc506-201">在 [姓氏屬性] 文字方塊中，輸入使用者的**姓氏**：**Simon**。</span><span class="sxs-lookup"><span data-stu-id="dc506-201">In the **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="dc506-202">d.</span><span class="sxs-lookup"><span data-stu-id="dc506-202">d.</span></span> <span data-ttu-id="dc506-203">在 [電子郵件屬性] 文字方塊中，輸入使用者的**電子郵件地址**：**BrittaSimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="dc506-203">In the **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="dc506-204">e.</span><span class="sxs-lookup"><span data-stu-id="dc506-204">e.</span></span> <span data-ttu-id="dc506-205">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="dc506-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="dc506-206">按一下 [您的 IDP 中繼資料]，然後在 [您的 IDP 中繼資料] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="dc506-206">Click **Your IDP Metadata**, and then, in the **Your IDP Metadata** section, perform the following steps:</span></span>
   
    <span data-ttu-id="dc506-207">![單一登入設定](./media/active-directory-saas-policystat-tutorial/ic808636.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="dc506-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="dc506-208">a.</span><span class="sxs-lookup"><span data-stu-id="dc506-208">a.</span></span> <span data-ttu-id="dc506-209">開啟您下載的中繼資料檔案，複製內容，然後貼到 [您的識別提供者中繼資料] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="dc506-209">Open your downloaded metadata file, copy the content, and  then paste it into the **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="dc506-210">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc506-210">b.</span></span> <span data-ttu-id="dc506-211">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="dc506-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="dc506-212">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="dc506-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dc506-213">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="dc506-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dc506-214">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dc506-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dc506-215">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="dc506-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="dc506-216">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="dc506-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="dc506-218">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="dc506-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dc506-219">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="dc506-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dc506-221">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="dc506-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dc506-223">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="dc506-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dc506-225">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="dc506-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dc506-227">a.</span><span class="sxs-lookup"><span data-stu-id="dc506-227">a.</span></span> <span data-ttu-id="dc506-228">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="dc506-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dc506-229">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc506-229">b.</span></span> <span data-ttu-id="dc506-230">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="dc506-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dc506-231">c.</span><span class="sxs-lookup"><span data-stu-id="dc506-231">c.</span></span> <span data-ttu-id="dc506-232">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="dc506-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dc506-233">d.</span><span class="sxs-lookup"><span data-stu-id="dc506-233">d.</span></span> <span data-ttu-id="dc506-234">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="dc506-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="dc506-235">建立 PolicyStat 測試使用者</span><span class="sxs-lookup"><span data-stu-id="dc506-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="dc506-236">為了讓 Azure AD 使用者能夠登入 PolicyStat，必須將他們佈建到 PolicyStat。</span><span class="sxs-lookup"><span data-stu-id="dc506-236">In order to enable Azure AD users to log into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="dc506-237">PolicyStat 支援即時使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="dc506-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="dc506-238">這表示您不需要手動將使用者新增至 PolicyStat。</span><span class="sxs-lookup"><span data-stu-id="dc506-238">This means, you do not need to add the users manually to PolicyStat.</span></span> <span data-ttu-id="dc506-239">使用者第一次透過 SSO 登入時就會被自動新增。</span><span class="sxs-lookup"><span data-stu-id="dc506-239">The users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="dc506-240">您可以使用任何其他的 PolicyStat 使用者帳戶建立工具，或 PolicyStat 提供的 API，以佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc506-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dc506-241">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="dc506-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dc506-242">在本節中，您會將 PolicyStat 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dc506-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PolicyStat.</span></span>

![指派使用者][200] 

<span data-ttu-id="dc506-244">**若要將 Britta Simon 指派給 PolicyStat，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="dc506-244">**To assign Britta Simon to PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="dc506-245">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="dc506-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="dc506-247">在應用程式清單中，選取 [PolicyStat]。</span><span class="sxs-lookup"><span data-stu-id="dc506-247">In the applications list, select **PolicyStat**.</span></span>

    ![設定單一登入](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="dc506-249">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="dc506-249">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="dc506-251">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc506-251">Click **Add** button.</span></span> <span data-ttu-id="dc506-252">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="dc506-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="dc506-254">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="dc506-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dc506-255">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc506-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dc506-256">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc506-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dc506-257">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="dc506-257">Testing single sign-on</span></span>

<span data-ttu-id="dc506-258">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="dc506-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dc506-259">當您在存取面板中按一下 PolicyStat 圖格時，應該會自動登入您的 PolicyStat 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc506-259">When you click the PolicyStat tile in the Access Panel, you should get automatically signed-on to your PolicyStat application.</span></span>
<span data-ttu-id="dc506-260">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="dc506-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dc506-261">其他資源</span><span class="sxs-lookup"><span data-stu-id="dc506-261">Additional resources</span></span>

* [<span data-ttu-id="dc506-262">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="dc506-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dc506-263">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="dc506-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

