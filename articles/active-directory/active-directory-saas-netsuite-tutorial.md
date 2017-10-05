---
title: "教學課程：Azure Active Directory 與 Netsuite 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Netsuite 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 4a19ab310212b93a53495a6fc6c25c77dfb82e79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="32d80-103">教學課程：Azure Active Directory 與 Netsuite 整合</span><span class="sxs-lookup"><span data-stu-id="32d80-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="32d80-104">在本教學課程中，您會了解如何整合 Netsuite 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="32d80-104">In this tutorial, you learn how to integrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32d80-105">Netsuite 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="32d80-105">Integrating Netsuite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="32d80-106">您可以在 Azure AD 中控制可存取 Netsuite 的人員</span><span class="sxs-lookup"><span data-stu-id="32d80-106">You can control in Azure AD who has access to Netsuite</span></span>
- <span data-ttu-id="32d80-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Netsuite (單一登入)</span><span class="sxs-lookup"><span data-stu-id="32d80-107">You can enable your users to automatically get signed-on to Netsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32d80-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="32d80-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="32d80-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="32d80-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32d80-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="32d80-110">Prerequisites</span></span>

<span data-ttu-id="32d80-111">若要設定 Azure AD 與 Netsuite 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="32d80-111">To configure Azure AD integration with Netsuite, you need the following items:</span></span>

- <span data-ttu-id="32d80-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="32d80-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32d80-113">啟用 Netsuite 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="32d80-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32d80-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="32d80-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32d80-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="32d80-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32d80-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="32d80-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32d80-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="32d80-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32d80-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="32d80-118">Scenario description</span></span>
<span data-ttu-id="32d80-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="32d80-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32d80-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="32d80-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32d80-121">從資源庫新增 Netsuite</span><span class="sxs-lookup"><span data-stu-id="32d80-121">Adding Netsuite from the gallery</span></span>
2. <span data-ttu-id="32d80-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="32d80-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-the-gallery"></a><span data-ttu-id="32d80-123">從資源庫新增 Netsuite</span><span class="sxs-lookup"><span data-stu-id="32d80-123">Adding Netsuite from the gallery</span></span>
<span data-ttu-id="32d80-124">若要設定將 Netsuite 整合到 Azure AD 中，您需要從資源庫將 Netsuite 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="32d80-124">To configure the integration of Netsuite into Azure AD, you need to add Netsuite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="32d80-125">**若要從資源庫新增 Netsuite，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="32d80-125">**To add Netsuite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="32d80-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="32d80-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32d80-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="32d80-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="32d80-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="32d80-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="32d80-131">按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="32d80-131">Click **New application** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="32d80-133">在搜尋方塊中，輸入 **Netsuite**。</span><span class="sxs-lookup"><span data-stu-id="32d80-133">In the search box, type **Netsuite**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="32d80-135">在結果面板中，選取 [Netsuite]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="32d80-135">In the results panel, select **Netsuite**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32d80-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="32d80-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32d80-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Netsuite 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="32d80-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="32d80-139">若要讓單一登入運作，Azure AD 必須知道 Netsuite 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="32d80-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Netsuite is to a user in Azure AD.</span></span> <span data-ttu-id="32d80-140">換句話說，必須在 Azure AD 使用者和 Netsuite 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="32d80-140">In other words, a link relationship between an Azure AD user and the related user in Netsuite needs to be established.</span></span>

<span data-ttu-id="32d80-141">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 Netsuite 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="32d80-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Netsuite.</span></span>

<span data-ttu-id="32d80-142">若要設定及測試與 Netsuite 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="32d80-142">To configure and test Azure AD single sign-on with Netsuite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="32d80-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="32d80-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="32d80-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="32d80-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32d80-145">**[建立 Netsuite 測試使用者](#creating-a-netsuite-test-user)** - 使 Netsuite 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="32d80-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - to have a counterpart of Britta Simon in Netsuite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="32d80-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="32d80-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32d80-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="32d80-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32d80-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="32d80-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32d80-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Netsuite 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="32d80-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="32d80-150">**若要設定與 Netsuite 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="32d80-150">**To configure Azure AD single sign-on with Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="32d80-151">在 Azure 入口網站的 [Netsuite] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="32d80-151">In the Azure portal, on the **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="32d80-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="32d80-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="32d80-155">在 [Netsuite 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="32d80-155">On the **Netsuite Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="32d80-157">在 [回覆 URL] 文字方塊中，使用下列模式輸入 URL：`https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="32d80-157">In the **Reply URL** textbox, type a URL using the following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32d80-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="32d80-158">This value is not real value.</span></span> <span data-ttu-id="32d80-159">請使用實際的「回覆 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="32d80-159">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="32d80-160">請連絡 [Netsuite 支援小組](http://www.netsuite.com/portal/services/support.shtml)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="32d80-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) to get this value.</span></span>
 
4. <span data-ttu-id="32d80-161">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="32d80-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="32d80-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="32d80-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32d80-165">在 [Netsuite 組態] 區段上，按一下 [設定 Netsuite] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="32d80-165">On the **Netsuite Configuration** section, click **Configure Netsuite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="32d80-166">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="32d80-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="32d80-168">在瀏覽器中開啟新索引標籤，以系統管理員的身分登入您的 Netsuite 公司站台。</span><span class="sxs-lookup"><span data-stu-id="32d80-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="32d80-169">在頁面頂端的工具列上，按一下 [設定]，然後按一下 [設定管理員]。</span><span class="sxs-lookup"><span data-stu-id="32d80-169">In the toolbar at the top of the page, click **Setup**, then click **Setup Manager**.</span></span>

    ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="32d80-171">從 [設定工作] 清單中，選取 [整合]。</span><span class="sxs-lookup"><span data-stu-id="32d80-171">From the **Setup Tasks** list, select **Integration**.</span></span>

    ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="32d80-173">在 [管理驗證] 區段中，按一下 [SAML 單一登入]。</span><span class="sxs-lookup"><span data-stu-id="32d80-173">In the **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="32d80-175">在 [SAML 設定]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="32d80-175">On the **SAML Setup** page, perform the following steps:</span></span>
   
    <span data-ttu-id="32d80-176">a.</span><span class="sxs-lookup"><span data-stu-id="32d80-176">a.</span></span> <span data-ttu-id="32d80-177">從 [設定登入]的 [快速參考] 區段複製 [SAML 單一登入服務 URL] 值，然後貼到 Netsuite 的 [識別提供者登入頁面] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="32d80-177">Copy the **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into the **Identity Provider Login Page** field in Netsuite.</span></span>

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="32d80-179">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="32d80-179">b.</span></span> <span data-ttu-id="32d80-180">在 Netsuite 中，選取 [主要驗證方法] 。</span><span class="sxs-lookup"><span data-stu-id="32d80-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="32d80-181">c.</span><span class="sxs-lookup"><span data-stu-id="32d80-181">c.</span></span> <span data-ttu-id="32d80-182">對標示為 [SAMLV2 身分識別提供者中繼資料] 的欄位，選取 [上傳 IDP 中繼資料檔案]。</span><span class="sxs-lookup"><span data-stu-id="32d80-182">For the field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="32d80-183">然後按一下 [瀏覽] ，上傳您從 Azure 入口網站下載的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="32d80-183">Then click **Browse** to upload the metadata file that you downloaded from Azure portal.</span></span>

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="32d80-185">d.</span><span class="sxs-lookup"><span data-stu-id="32d80-185">d.</span></span> <span data-ttu-id="32d80-186">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="32d80-186">Click **Submit**.</span></span>

12. <span data-ttu-id="32d80-187">在 Azure AD 中，按一下 [檢視及編輯所有其他使用者屬性] 核取方塊並新增屬性。</span><span class="sxs-lookup"><span data-stu-id="32d80-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="32d80-189">在 [屬性名稱] 欄位中，輸入 `account`。</span><span class="sxs-lookup"><span data-stu-id="32d80-189">For the **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="32d80-190">在 [屬性值] 欄位中，輸入您的 Netsuite 帳戶識別碼。這個值是常數，隨帳戶而不同。</span><span class="sxs-lookup"><span data-stu-id="32d80-190">For the **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="32d80-191">如何找出帳戶識別碼的指示如下：</span><span class="sxs-lookup"><span data-stu-id="32d80-191">Instructions on how to find your account ID are included below:</span></span>

      ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="32d80-193">a.</span><span class="sxs-lookup"><span data-stu-id="32d80-193">a.</span></span> <span data-ttu-id="32d80-194">在 Netsuite 中，從頂端導覽功能表按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="32d80-194">In Netsuite, click **Setup** from the top navigation menu.</span></span>

    <span data-ttu-id="32d80-195">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="32d80-195">b.</span></span> <span data-ttu-id="32d80-196">然後，在左方導覽功能表的 [設定工作] 區段下，選取 [整合] 區段，然後按一下 [Web 服務喜好設定]。</span><span class="sxs-lookup"><span data-stu-id="32d80-196">Then click under the **Setup Tasks** section of the left navigation menu, select the **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="32d80-197">c.</span><span class="sxs-lookup"><span data-stu-id="32d80-197">c.</span></span> <span data-ttu-id="32d80-198">複製您的 Netsuite 帳戶識別碼，並將它貼到 Azure AD 中的 [屬性值]  欄位。</span><span class="sxs-lookup"><span data-stu-id="32d80-198">Copy your Netsuite Account ID and paste it into the **Attribute Value** field in Azure AD.</span></span>

    ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="32d80-200">在使用者可以執行單一登入 Netsuite 之前，必須先在 Netsuite 中指派適當的權限。</span><span class="sxs-lookup"><span data-stu-id="32d80-200">Before users can perform single sign-on into Netsuite, they must first be assigned the appropriate permissions in Netsuite.</span></span> <span data-ttu-id="32d80-201">請依照下列指示來指派這些權限。</span><span class="sxs-lookup"><span data-stu-id="32d80-201">Follow the instructions below to assign these permissions.</span></span>

    <span data-ttu-id="32d80-202">a.</span><span class="sxs-lookup"><span data-stu-id="32d80-202">a.</span></span> <span data-ttu-id="32d80-203">在頂端的瀏覽功能表上，按一下 [設定]，然後按一下 [設定管理員]。</span><span class="sxs-lookup"><span data-stu-id="32d80-203">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="32d80-205">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="32d80-205">b.</span></span> <span data-ttu-id="32d80-206">在左方的瀏覽功能表上，選取 [使用者/角色]，然後按一下 [管理角色]。</span><span class="sxs-lookup"><span data-stu-id="32d80-206">On the left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="32d80-208">c.</span><span class="sxs-lookup"><span data-stu-id="32d80-208">c.</span></span> <span data-ttu-id="32d80-209">按一下 [新角色] 。</span><span class="sxs-lookup"><span data-stu-id="32d80-209">Click **New Role**.</span></span>

    <span data-ttu-id="32d80-210">d.</span><span class="sxs-lookup"><span data-stu-id="32d80-210">d.</span></span> <span data-ttu-id="32d80-211">輸入新角色的 [名稱]，然後選取 [僅單一登入] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="32d80-211">Type in a **Name** for your new role, and select the **Single Sign-On Only** checkbox.</span></span>
      
      ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="32d80-213">e.</span><span class="sxs-lookup"><span data-stu-id="32d80-213">e.</span></span> <span data-ttu-id="32d80-214">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="32d80-214">Click **Save**.</span></span>

    <span data-ttu-id="32d80-215">f.</span><span class="sxs-lookup"><span data-stu-id="32d80-215">f.</span></span> <span data-ttu-id="32d80-216">在頂端的功能表中，按一下 [權限] 。</span><span class="sxs-lookup"><span data-stu-id="32d80-216">In the menu on the top, click **Permissions**.</span></span> <span data-ttu-id="32d80-217">然後按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="32d80-217">Then click **Setup**.</span></span>
      
       ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="32d80-219">g.</span><span class="sxs-lookup"><span data-stu-id="32d80-219">g.</span></span> <span data-ttu-id="32d80-220">選取 [設定 SAM 單一登入]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="32d80-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="32d80-221">h.</span><span class="sxs-lookup"><span data-stu-id="32d80-221">h.</span></span> <span data-ttu-id="32d80-222">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="32d80-222">Click **Save**.</span></span>

    <span data-ttu-id="32d80-223">i.</span><span class="sxs-lookup"><span data-stu-id="32d80-223">i.</span></span> <span data-ttu-id="32d80-224">在頂端的瀏覽功能表上，按一下 [設定]，然後按一下 [設定管理員]。</span><span class="sxs-lookup"><span data-stu-id="32d80-224">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="32d80-226">j.</span><span class="sxs-lookup"><span data-stu-id="32d80-226">j.</span></span> <span data-ttu-id="32d80-227">在左方的瀏覽功能表上，選取 [使用者/角色]，然後按一下 [管理使用者]。</span><span class="sxs-lookup"><span data-stu-id="32d80-227">On the left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="32d80-229">k.</span><span class="sxs-lookup"><span data-stu-id="32d80-229">k.</span></span> <span data-ttu-id="32d80-230">選取測試使用者。</span><span class="sxs-lookup"><span data-stu-id="32d80-230">Select a test user.</span></span> <span data-ttu-id="32d80-231">然後按一下 [編輯] 。</span><span class="sxs-lookup"><span data-stu-id="32d80-231">Then click **Edit**.</span></span>
      
       ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="32d80-233">l.</span><span class="sxs-lookup"><span data-stu-id="32d80-233">l.</span></span> <span data-ttu-id="32d80-234">在 [角色] 對話方塊中，選取您建立的角色，然後按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="32d80-234">On the Roles dialog, select the role that you have created and click **Add**.</span></span>
      
       ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="32d80-236">m.</span><span class="sxs-lookup"><span data-stu-id="32d80-236">m.</span></span> <span data-ttu-id="32d80-237">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="32d80-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="32d80-238">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="32d80-238">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="32d80-239">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="32d80-239">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="32d80-240">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="32d80-240">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32d80-241">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="32d80-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="32d80-242">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="32d80-242">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="32d80-244">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="32d80-244">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="32d80-245">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="32d80-245">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="32d80-247">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="32d80-247">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32d80-249">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="32d80-249">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32d80-251">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="32d80-251">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32d80-253">a.</span><span class="sxs-lookup"><span data-stu-id="32d80-253">a.</span></span> <span data-ttu-id="32d80-254">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="32d80-254">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32d80-255">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="32d80-255">b.</span></span> <span data-ttu-id="32d80-256">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="32d80-256">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32d80-257">c.</span><span class="sxs-lookup"><span data-stu-id="32d80-257">c.</span></span> <span data-ttu-id="32d80-258">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="32d80-258">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="32d80-259">d.</span><span class="sxs-lookup"><span data-stu-id="32d80-259">d.</span></span> <span data-ttu-id="32d80-260">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="32d80-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="32d80-261">建立 Netsuite 測試使用者</span><span class="sxs-lookup"><span data-stu-id="32d80-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="32d80-262">本節會在 Netsuite 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="32d80-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="32d80-263">Netsuite 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="32d80-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="32d80-264">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="32d80-264">There is no action item for you in this section.</span></span> <span data-ttu-id="32d80-265">如果 Netsuite 中還沒有使用者，當您嘗試存取 Netsuite 時，就會建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="32d80-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt to access Netsuite.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="32d80-266">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="32d80-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="32d80-267">在本節中，您會將 Netsuite 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="32d80-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Netsuite.</span></span>

![指派使用者][200] 

<span data-ttu-id="32d80-269">**若要將 Britta Simon 指派給 Netsuite，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="32d80-269">**To assign Britta Simon to Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="32d80-270">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="32d80-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="32d80-272">在應用程式清單中，選取 [Netsuite]。</span><span class="sxs-lookup"><span data-stu-id="32d80-272">In the applications list, select **Netsuite**.</span></span>

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="32d80-274">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="32d80-274">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="32d80-276">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="32d80-276">Click **Add** button.</span></span> <span data-ttu-id="32d80-277">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="32d80-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="32d80-279">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="32d80-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="32d80-280">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="32d80-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32d80-281">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="32d80-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32d80-282">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="32d80-282">Testing single sign-on</span></span>

<span data-ttu-id="32d80-283">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="32d80-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="32d80-284">若要測試您的單一登入設定，請開啟位於 [https://myapps.microsoft.com](https://myapps.microsoft.com/) 的存取面板，登入測試帳戶，然後按一下 [Netsuite]。</span><span class="sxs-lookup"><span data-stu-id="32d80-284">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into the test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32d80-285">其他資源</span><span class="sxs-lookup"><span data-stu-id="32d80-285">Additional resources</span></span>

* [<span data-ttu-id="32d80-286">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="32d80-286">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32d80-287">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="32d80-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="32d80-288">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="32d80-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

