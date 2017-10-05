---
title: "教學課程：Azure Active Directory 與 Pantheon 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Pantheon 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3f4ac1db2ee83d9f9fcb375d0fb7c40ad21c4688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="1ad52-103">教學課程：Azure Active Directory 與 Pantheon 整合</span><span class="sxs-lookup"><span data-stu-id="1ad52-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="1ad52-104">在本教學課程中，您會了解如何整合 Pantheon 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="1ad52-104">In this tutorial, you learn how to integrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1ad52-105">Pantheon 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="1ad52-105">Integrating Pantheon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1ad52-106">您可以在 Azure AD 中控制可存取 Pantheon 的人員</span><span class="sxs-lookup"><span data-stu-id="1ad52-106">You can control in Azure AD who has access to Pantheon</span></span>
- <span data-ttu-id="1ad52-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Pantheon (單一登入)</span><span class="sxs-lookup"><span data-stu-id="1ad52-107">You can enable your users to automatically get signed-on to Pantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1ad52-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="1ad52-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1ad52-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1ad52-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ad52-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1ad52-110">Prerequisites</span></span>

<span data-ttu-id="1ad52-111">若要設定 Pantheon 與 Azure AD 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="1ad52-111">To configure Azure AD integration with Pantheon, you need the following items:</span></span>

- <span data-ttu-id="1ad52-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1ad52-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1ad52-113">已啟用 Pantheon 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1ad52-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1ad52-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1ad52-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1ad52-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1ad52-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1ad52-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1ad52-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1ad52-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="1ad52-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1ad52-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1ad52-118">Scenario description</span></span>
<span data-ttu-id="1ad52-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ad52-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1ad52-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="1ad52-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1ad52-121">從資源庫新增 Pantheon</span><span class="sxs-lookup"><span data-stu-id="1ad52-121">Adding Pantheon from the gallery</span></span>
2. <span data-ttu-id="1ad52-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1ad52-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-the-gallery"></a><span data-ttu-id="1ad52-123">從資源庫新增 Pantheon</span><span class="sxs-lookup"><span data-stu-id="1ad52-123">Adding Pantheon from the gallery</span></span>
<span data-ttu-id="1ad52-124">若要設定 Pantheon 與 Azure AD 整合，您需要從資源庫將 Pantheon 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="1ad52-124">To configure the integration of Pantheon into Azure AD, you need to add Pantheon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1ad52-125">**若要從資源庫新增 Pantheon，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1ad52-125">**To add Pantheon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1ad52-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="1ad52-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1ad52-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1ad52-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1ad52-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1ad52-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="1ad52-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ad52-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="1ad52-133">在搜尋方塊中，輸入 **Pantheon**。</span><span class="sxs-lookup"><span data-stu-id="1ad52-133">In the search box, type **Pantheon**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. <span data-ttu-id="1ad52-135">在結果窗格中，選取 [Pantheon]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ad52-135">In the results panel, select **Pantheon**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1ad52-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1ad52-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1ad52-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Pantheon 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ad52-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1ad52-139">若要讓單一登入運作，Azure AD 必須知道 Pantheon 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="1ad52-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pantheon is to a user in Azure AD.</span></span> <span data-ttu-id="1ad52-140">換句話說，必須建立 Azure AD 使用者和 Pantheon 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1ad52-140">In other words, a link relationship between an Azure AD user and the related user in Pantheon needs to be established.</span></span>

<span data-ttu-id="1ad52-141">在 Pantheon 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1ad52-141">In Pantheon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1ad52-142">若要設定及測試與 Pantheon 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="1ad52-142">To configure and test Azure AD single sign-on with Pantheon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1ad52-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="1ad52-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1ad52-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ad52-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1ad52-145">**[建立 Pantheon 測試使用者](#creating-a-pantheon-test-user)** - 使 Pantheon 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="1ad52-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - to have a counterpart of Britta Simon in Pantheon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1ad52-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ad52-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1ad52-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="1ad52-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1ad52-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1ad52-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1ad52-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Pantheon 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ad52-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="1ad52-150">**若要使用 Pantheon 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1ad52-150">**To configure Azure AD single sign-on with Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="1ad52-151">在 Azure 入口網站的 [Pantheon] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="1ad52-151">In the Azure portal, on the **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="1ad52-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ad52-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. <span data-ttu-id="1ad52-155">在 [Pantheon 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1ad52-155">On the **Pantheon Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="1ad52-157">a.</span><span class="sxs-lookup"><span data-stu-id="1ad52-157">a.</span></span> <span data-ttu-id="1ad52-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="1ad52-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="1ad52-159">b.</span><span class="sxs-lookup"><span data-stu-id="1ad52-159">b.</span></span> <span data-ttu-id="1ad52-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="1ad52-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1ad52-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="1ad52-161">These values are not real.</span></span> <span data-ttu-id="1ad52-162">請使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="1ad52-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="1ad52-163">請連絡 [Pantheon 支援小組](https://pantheon.io/docs/getting-support/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="1ad52-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) to get these values.</span></span>

4. <span data-ttu-id="1ad52-164">Pantheon 應用程式需要特定格式的 SAML 判斷提示，您必須以使用者的電子郵件地址來設定 UserIdentifier 屬性值。</span><span class="sxs-lookup"><span data-stu-id="1ad52-164">Pantheon application expects the SAML assertion in specific format, which requires you to set the UserIdentifier attribute value with the user’s email address.</span></span> <span data-ttu-id="1ad52-165">根據預設，Azure AD 會使用 UserPrincipalName 作為 UserIdentifier 屬性。</span><span class="sxs-lookup"><span data-stu-id="1ad52-165">By default Azure AD uses the UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="1ad52-166">但您需要調整此值以符合使用者的電子郵件地址，才能成功整合。</span><span class="sxs-lookup"><span data-stu-id="1ad52-166">But for successful integration you need to adjust this value to match with user’s email address.</span></span> <span data-ttu-id="1ad52-167">在完成正確對應後，整合才有作用。</span><span class="sxs-lookup"><span data-stu-id="1ad52-167">The integration will only work after doing the correct mapping.</span></span>

    ![設定單一登入](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. <span data-ttu-id="1ad52-169">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="1ad52-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. <span data-ttu-id="1ad52-171">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ad52-171">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="1ad52-173">在 [Pantheon 組態] 區段上，按一下 [設定 Pantheon] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="1ad52-173">On the **Pantheon Configuration** section, click **Configure Pantheon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1ad52-174">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="1ad52-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. <span data-ttu-id="1ad52-176">若要在 **Pantheon** 端設定單一登入，您必須將已下載的「憑證」和「SAML 單一登入服務 URL」傳送給 [Pantheon 支援小組](https://pantheon.io/docs/getting-support/)。</span><span class="sxs-lookup"><span data-stu-id="1ad52-176">To configure single sign-on on **Pantheon** side, you need to send the downloaded **Certificate** and **SAML Single Sign-On Service URL** to [Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="1ad52-177">當您想要啟用這個連接時，您也需要提供電子郵件網域資訊和日期時間。</span><span class="sxs-lookup"><span data-stu-id="1ad52-177">You also need to provide the Email Domain(s) information and Date Time when you want to enable this connection.</span></span> <span data-ttu-id="1ad52-178">您可以從[這裡](https://pantheon.io/docs/sso-organizations/)找到更多詳細資訊</span><span class="sxs-lookup"><span data-stu-id="1ad52-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="1ad52-179">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="1ad52-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1ad52-180">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="1ad52-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1ad52-181">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1ad52-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1ad52-182">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1ad52-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="1ad52-183">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1ad52-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="1ad52-185">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1ad52-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1ad52-186">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="1ad52-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1ad52-188">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="1ad52-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1ad52-190">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="1ad52-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1ad52-192">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1ad52-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1ad52-194">a.</span><span class="sxs-lookup"><span data-stu-id="1ad52-194">a.</span></span> <span data-ttu-id="1ad52-195">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1ad52-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1ad52-196">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ad52-196">b.</span></span> <span data-ttu-id="1ad52-197">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="1ad52-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1ad52-198">c.</span><span class="sxs-lookup"><span data-stu-id="1ad52-198">c.</span></span> <span data-ttu-id="1ad52-199">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="1ad52-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1ad52-200">d.</span><span class="sxs-lookup"><span data-stu-id="1ad52-200">d.</span></span> <span data-ttu-id="1ad52-201">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1ad52-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="1ad52-202">建立 Pantheon 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1ad52-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="1ad52-203">在本節中，您要在 Pantheon 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="1ad52-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="1ad52-204">請遵循下列步驟，在 Pantheon 中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="1ad52-204">Please follow the below steps to add the user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="1ad52-205">必須先在 Pantheon 中建立使用者，SSO 才有作用。</span><span class="sxs-lookup"><span data-stu-id="1ad52-205">For SSO to work user needs to be created first in Pantheon.</span></span>

1. <span data-ttu-id="1ad52-206">以管理員認證登入 Pantheon。</span><span class="sxs-lookup"><span data-stu-id="1ad52-206">Login to Pantheon with admin credentials.</span></span>

2. <span data-ttu-id="1ad52-207">瀏覽至 [組織] 儀表板頁面。</span><span class="sxs-lookup"><span data-stu-id="1ad52-207">Navigate to **Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="1ad52-208">按一下 [人員] 。</span><span class="sxs-lookup"><span data-stu-id="1ad52-208">Click **People**.</span></span>

4. <span data-ttu-id="1ad52-209">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="1ad52-209">Click **Add user**.</span></span>

5. <span data-ttu-id="1ad52-210">輸入使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="1ad52-210">Enter the user's email address.</span></span>

6. <span data-ttu-id="1ad52-211">選擇使用者的角色。</span><span class="sxs-lookup"><span data-stu-id="1ad52-211">Choose the user's role.</span></span>

7. <span data-ttu-id="1ad52-212">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="1ad52-212">Click **Add user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1ad52-213">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1ad52-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1ad52-214">在本節中，您會將 Pantheon 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ad52-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pantheon.</span></span>

![指派使用者][200] 

<span data-ttu-id="1ad52-216">**若要將 Britta Simon 指派至 Pantheon，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="1ad52-216">**To assign Britta Simon to Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="1ad52-217">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1ad52-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1ad52-219">在應用程式清單中，選取 [Pantheon]。</span><span class="sxs-lookup"><span data-stu-id="1ad52-219">In the applications list, select **Pantheon**.</span></span>

    ![設定單一登入](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. <span data-ttu-id="1ad52-221">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1ad52-221">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="1ad52-223">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ad52-223">Click **Add** button.</span></span> <span data-ttu-id="1ad52-224">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1ad52-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="1ad52-226">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="1ad52-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1ad52-227">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ad52-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1ad52-228">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ad52-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1ad52-229">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1ad52-229">Testing single sign-on</span></span>

<span data-ttu-id="1ad52-230">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="1ad52-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1ad52-231">當您按一下存取面板中的 Pantheon 圖格時，應該會自動登入您的 Pantheon 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ad52-231">When you click the Pantheon tile in the Access Panel, you should get automatically signed-on to your Pantheon application.</span></span>
<span data-ttu-id="1ad52-232">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1ad52-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1ad52-233">其他資源</span><span class="sxs-lookup"><span data-stu-id="1ad52-233">Additional resources</span></span>

* [<span data-ttu-id="1ad52-234">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="1ad52-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1ad52-235">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1ad52-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

