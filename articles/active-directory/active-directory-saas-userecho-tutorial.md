---
title: "教學課程：Azure Active Directory 與 UserEcho 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 UserEcho 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2d824d8d5eb8a25db128397b908a126bd87213ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="84fee-103">教學課程：Azure Active Directory 與 UserEcho 整合</span><span class="sxs-lookup"><span data-stu-id="84fee-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>

<span data-ttu-id="84fee-104">在本教學課程中，您將了解如何整合 UserEcho 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="84fee-104">In this tutorial, you learn how to integrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="84fee-105">將 UserEcho 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="84fee-105">Integrating UserEcho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="84fee-106">您可以在 Azure AD 中控制可存取 UserEcho 的人員</span><span class="sxs-lookup"><span data-stu-id="84fee-106">You can control in Azure AD who has access to UserEcho</span></span>
- <span data-ttu-id="84fee-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 UserEcho (單一登入)</span><span class="sxs-lookup"><span data-stu-id="84fee-107">You can enable your users to automatically get signed-on to UserEcho (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="84fee-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="84fee-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="84fee-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="84fee-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84fee-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="84fee-110">Prerequisites</span></span>

<span data-ttu-id="84fee-111">若要設定 Azure AD 與 UserEcho 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="84fee-111">To configure Azure AD integration with UserEcho, you need the following items:</span></span>

- <span data-ttu-id="84fee-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="84fee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="84fee-113">已啟用 UserEcho 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="84fee-113">A UserEcho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="84fee-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="84fee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="84fee-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="84fee-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="84fee-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="84fee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="84fee-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="84fee-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="84fee-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="84fee-118">Scenario description</span></span>
<span data-ttu-id="84fee-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84fee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="84fee-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="84fee-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="84fee-121">從資源庫新增 UserEcho</span><span class="sxs-lookup"><span data-stu-id="84fee-121">Adding UserEcho from the gallery</span></span>
2. <span data-ttu-id="84fee-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="84fee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-userecho-from-the-gallery"></a><span data-ttu-id="84fee-123">從資源庫新增 UserEcho</span><span class="sxs-lookup"><span data-stu-id="84fee-123">Adding UserEcho from the gallery</span></span>
<span data-ttu-id="84fee-124">若要設定將 UserEcho 整合到 Azure AD 中，您需要從資源庫將 UserEcho 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="84fee-124">To configure the integration of UserEcho into Azure AD, you need to add UserEcho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="84fee-125">**若要從資源庫新增 UserEcho，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="84fee-125">**To add UserEcho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="84fee-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="84fee-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="84fee-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="84fee-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="84fee-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="84fee-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="84fee-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84fee-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="84fee-133">在搜尋方塊中，輸入 **UserEcho**。</span><span class="sxs-lookup"><span data-stu-id="84fee-133">In the search box, type **UserEcho**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. <span data-ttu-id="84fee-135">在結果窗格中，選取 [UserEcho]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="84fee-135">In the results panel, select **UserEcho**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="84fee-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="84fee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="84fee-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 UserEcho 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84fee-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="84fee-139">若要讓單一登入運作，Azure AD 必須知道 UserEcho 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="84fee-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UserEcho is to a user in Azure AD.</span></span> <span data-ttu-id="84fee-140">換句話說，必須在 Azure AD 使用者與 UserEcho 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="84fee-140">In other words, a link relationship between an Azure AD user and the related user in UserEcho needs to be established.</span></span>

<span data-ttu-id="84fee-141">在 UserEcho 中，將 Azure AD 中 [使用者名稱]的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="84fee-141">In UserEcho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="84fee-142">若要設定及測試與 UserEcho 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="84fee-142">To configure and test Azure AD single sign-on with UserEcho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="84fee-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="84fee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="84fee-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84fee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="84fee-145">**[建立 UserEcho 測試使用者](#creating-a-userecho-test-user)** - 使 UserEcho 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="84fee-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - to have a counterpart of Britta Simon in UserEcho that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="84fee-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84fee-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="84fee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="84fee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="84fee-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="84fee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="84fee-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 UserEcho 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="84fee-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UserEcho application.</span></span>

<span data-ttu-id="84fee-150">**若要設定與 UserEcho 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="84fee-150">**To configure Azure AD single sign-on with UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="84fee-151">在 Azure 入口網站的 [UserEcho] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="84fee-151">In the Azure portal, on the **UserEcho** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="84fee-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="84fee-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. <span data-ttu-id="84fee-155">在 [UserEcho 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="84fee-155">On the **UserEcho Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    <span data-ttu-id="84fee-157">a.</span><span class="sxs-lookup"><span data-stu-id="84fee-157">a.</span></span> <span data-ttu-id="84fee-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.userecho.com/`</span><span class="sxs-lookup"><span data-stu-id="84fee-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.userecho.com/`</span></span>

    <span data-ttu-id="84fee-159">b.</span><span class="sxs-lookup"><span data-stu-id="84fee-159">b.</span></span> <span data-ttu-id="84fee-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.userecho.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="84fee-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="84fee-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="84fee-161">These values are not real.</span></span> <span data-ttu-id="84fee-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="84fee-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="84fee-163">請連絡 [UserEcho 用戶端支援小組](https://feedback.userecho.com/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="84fee-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) to get these values.</span></span> 

4. <span data-ttu-id="84fee-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="84fee-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. <span data-ttu-id="84fee-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="84fee-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="84fee-168">在 [UserEcho 組態] 區段上，按一下 [設定 UserEcho] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="84fee-168">On the **UserEcho Configuration** section, click **Configure UserEcho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="84fee-169">從 [快速參考] 區段中複製 [登出 URL 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="84fee-169">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. <span data-ttu-id="84fee-171">在另一個瀏覽器視窗中，以系統管理員身分登入您的 UserEcho 公司網站。</span><span class="sxs-lookup"><span data-stu-id="84fee-171">In another browser window, sign on to your UserEcho company site as an administrator.</span></span>

8. <span data-ttu-id="84fee-172">在頂端工具列中，按一下您的使用者名稱以展開功能表，然後按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="84fee-172">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. <span data-ttu-id="84fee-174">按一下 [整合] 。</span><span class="sxs-lookup"><span data-stu-id="84fee-174">Click **Integrations**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. <span data-ttu-id="84fee-176">按一下 [網站]，然後按一下 [單一登入 (SAML2)]。</span><span class="sxs-lookup"><span data-stu-id="84fee-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. <span data-ttu-id="84fee-178">在 [單一登入 (SAML)]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="84fee-178">On the **Single sign-on (SAML)** page, perform the following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    <span data-ttu-id="84fee-180">a.</span><span class="sxs-lookup"><span data-stu-id="84fee-180">a.</span></span> <span data-ttu-id="84fee-181">在 [已啟用 SAML] 選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="84fee-181">As **SAML-enabled**, select **Yes**.</span></span>
    
    <span data-ttu-id="84fee-182">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="84fee-182">b.</span></span> <span data-ttu-id="84fee-183">將您從 Azure 入口網站複製的 [SAML 單一登入服務 URL]，貼到 [SAML SSO URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="84fee-183">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SAML SSO URL** textbox.</span></span>
    
    <span data-ttu-id="84fee-184">c.</span><span class="sxs-lookup"><span data-stu-id="84fee-184">c.</span></span> <span data-ttu-id="84fee-185">將您從 Azure 入口網站複製的「登出 URL」貼到 [遠端登出 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="84fee-185">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Remote logoout URL** textbox.</span></span>
    
    <span data-ttu-id="84fee-186">d.</span><span class="sxs-lookup"><span data-stu-id="84fee-186">d.</span></span> <span data-ttu-id="84fee-187">在記事本中開啟下載的憑證，複製其內容，然後貼到 [X.509 憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="84fee-187">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="84fee-188">e.</span><span class="sxs-lookup"><span data-stu-id="84fee-188">e.</span></span> <span data-ttu-id="84fee-189">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="84fee-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="84fee-190">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="84fee-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="84fee-191">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="84fee-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="84fee-192">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="84fee-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="84fee-193">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="84fee-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="84fee-194">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="84fee-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="84fee-196">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="84fee-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="84fee-197">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="84fee-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="84fee-199">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="84fee-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="84fee-201">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="84fee-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="84fee-203">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="84fee-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="84fee-205">a.</span><span class="sxs-lookup"><span data-stu-id="84fee-205">a.</span></span> <span data-ttu-id="84fee-206">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="84fee-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="84fee-207">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="84fee-207">b.</span></span> <span data-ttu-id="84fee-208">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="84fee-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="84fee-209">c.</span><span class="sxs-lookup"><span data-stu-id="84fee-209">c.</span></span> <span data-ttu-id="84fee-210">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="84fee-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="84fee-211">d.</span><span class="sxs-lookup"><span data-stu-id="84fee-211">d.</span></span> <span data-ttu-id="84fee-212">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="84fee-212">Click **Create**.</span></span>
 
### <a name="creating-a-userecho-test-user"></a><span data-ttu-id="84fee-213">建立 UserEcho 測試使用者</span><span class="sxs-lookup"><span data-stu-id="84fee-213">Creating a UserEcho test user</span></span>

<span data-ttu-id="84fee-214">本節的目標是要在 UserEcho 中建立一個名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="84fee-214">The objective of this section is to create a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="84fee-215">**若要在 UserEcho 中建立名為 Britta Simon 的使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="84fee-215">**To create a user called Britta Simon in UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="84fee-216">以系統管理員身分登入您的 UserEcho 公司網站。</span><span class="sxs-lookup"><span data-stu-id="84fee-216">Sign-on to your UserEcho company site as an administrator.</span></span>

2. <span data-ttu-id="84fee-217">在頂端工具列中，按一下您的使用者名稱以展開功能表，然後按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="84fee-217">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. <span data-ttu-id="84fee-219">按一下 [使用者] 以展開 [使用者] 區段。</span><span class="sxs-lookup"><span data-stu-id="84fee-219">Click **Users**, to expand the **Users** section.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. <span data-ttu-id="84fee-221">按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="84fee-221">Click **Users**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. <span data-ttu-id="84fee-223">按一下 [邀請新使用者] 。</span><span class="sxs-lookup"><span data-stu-id="84fee-223">Click **Invite a new user**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. <span data-ttu-id="84fee-225">在 [邀請新使用者]  對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="84fee-225">On the **Invite a new user** dialog, perform the following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    <span data-ttu-id="84fee-227">a.</span><span class="sxs-lookup"><span data-stu-id="84fee-227">a.</span></span> <span data-ttu-id="84fee-228">在 [名稱] 文字方塊中，輸入使用者的名稱，例如 Britta Simon。</span><span class="sxs-lookup"><span data-stu-id="84fee-228">In the **Name** textbox, type name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="84fee-229">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="84fee-229">b.</span></span>  <span data-ttu-id="84fee-230">在 [電子郵件] 文字方塊中，輸入像是 Brittasimon@contoso.com 的使用者電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="84fee-230">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="84fee-231">c.</span><span class="sxs-lookup"><span data-stu-id="84fee-231">c.</span></span> <span data-ttu-id="84fee-232">按一下 [邀請] 。</span><span class="sxs-lookup"><span data-stu-id="84fee-232">Click **Invite**.</span></span>

<span data-ttu-id="84fee-233">會傳送邀請給 Britta，邀請可讓她開始使用 UserEcho。</span><span class="sxs-lookup"><span data-stu-id="84fee-233">An invitation is sent to Britta, which enables her to start using UserEcho.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="84fee-234">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="84fee-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="84fee-235">在本節中，您會將 UserEcho 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84fee-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UserEcho.</span></span>

![指派使用者][200] 

<span data-ttu-id="84fee-237">**若要將 Britta Simon 指派給 UserEcho，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="84fee-237">**To assign Britta Simon to UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="84fee-238">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="84fee-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="84fee-240">在應用程式清單中，選取 [UserEcho] 。</span><span class="sxs-lookup"><span data-stu-id="84fee-240">In the applications list, select **UserEcho**.</span></span>

    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. <span data-ttu-id="84fee-242">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="84fee-242">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="84fee-244">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84fee-244">Click **Add** button.</span></span> <span data-ttu-id="84fee-245">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="84fee-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="84fee-247">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="84fee-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="84fee-248">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84fee-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="84fee-249">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84fee-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="84fee-250">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="84fee-250">Testing single sign-on</span></span>

<span data-ttu-id="84fee-251">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="84fee-251">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="84fee-252">當您在存取面板中按一下 [UserEcho] 磚時，應該會自動登入您的 UserEcho 應用程式。</span><span class="sxs-lookup"><span data-stu-id="84fee-252">When you click the UserEcho tile in the Access Panel, you should get automatically signed-on to your UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84fee-253">其他資源</span><span class="sxs-lookup"><span data-stu-id="84fee-253">Additional resources</span></span>

* [<span data-ttu-id="84fee-254">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="84fee-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="84fee-255">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="84fee-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

