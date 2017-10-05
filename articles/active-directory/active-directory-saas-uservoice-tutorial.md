---
title: "教學課程：Azure Active Directory 與 UserVoice 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 UserVoice 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: fcfda1c2ecb162fb93b70574a18bd745b72ee4db
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="11549-103">教學課程：Azure Active Directory 與 UserVoice 整合</span><span class="sxs-lookup"><span data-stu-id="11549-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="11549-104">在本教學課程中，您會了解如何整合 UserVoice 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="11549-104">In this tutorial, you learn how to integrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="11549-105">UserVoice 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="11549-105">Integrating UserVoice with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="11549-106">您可以在 Azure AD 中控制可存取 UserVoice 的人員。</span><span class="sxs-lookup"><span data-stu-id="11549-106">You can control in Azure AD who has access to UserVoice.</span></span>
- <span data-ttu-id="11549-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 UserVoice (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="11549-107">You can enable your users to automatically get signed-on to UserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="11549-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="11549-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="11549-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="11549-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11549-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="11549-110">Prerequisites</span></span>

<span data-ttu-id="11549-111">若要設定 Azure AD 與 UserVoice 的整合作業，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="11549-111">To configure Azure AD integration with UserVoice, you need the following items:</span></span>

- <span data-ttu-id="11549-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="11549-112">An Azure AD subscription</span></span>
- <span data-ttu-id="11549-113">已啟用 UserVoice 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="11549-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="11549-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="11549-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="11549-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="11549-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="11549-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="11549-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="11549-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="11549-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11549-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="11549-118">Scenario description</span></span>
<span data-ttu-id="11549-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11549-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="11549-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="11549-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11549-121">從資源庫新增 UserVoice</span><span class="sxs-lookup"><span data-stu-id="11549-121">Adding UserVoice from the gallery</span></span>
2. <span data-ttu-id="11549-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="11549-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-the-gallery"></a><span data-ttu-id="11549-123">從資源庫新增 UserVoice</span><span class="sxs-lookup"><span data-stu-id="11549-123">Adding UserVoice from the gallery</span></span>
<span data-ttu-id="11549-124">若要設定將 UserVoice 整合到 Azure AD 中，您需要從資源庫將 UserVoice 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="11549-124">To configure the integration of UserVoice into Azure AD, you need to add UserVoice from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="11549-125">**若要從資源庫新增 UserVoice，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="11549-125">**To add UserVoice from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="11549-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="11549-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="11549-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="11549-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="11549-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="11549-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="11549-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="11549-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="11549-133">在搜尋方塊中，輸入 **UserVoice**，從結果面板中選取 **UserVoice**，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="11549-133">In the search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="11549-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="11549-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="11549-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 UserVoice 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11549-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="11549-137">若要讓單一登入運作，Azure AD 必須知道 UserVoice 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="11549-137">For single sign-on to work, Azure AD needs to know what the counterpart user in UserVoice is to a user in Azure AD.</span></span> <span data-ttu-id="11549-138">換句話說，必須在 Azure AD 使用者和 UserVoice 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="11549-138">In other words, a link relationship between an Azure AD user and the related user in UserVoice needs to be established.</span></span>

<span data-ttu-id="11549-139">在 UserVoice 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="11549-139">In UserVoice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="11549-140">若要使用 UserVoice 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="11549-140">To configure and test Azure AD single sign-on with UserVoice, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="11549-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="11549-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="11549-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11549-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="11549-143">**[建立 UserVoice 測試使用者](#create-a-uservoice-test-user)** - 讓 UserVoice 中對應的 Britta Simon 連結到使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="11549-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - to have a counterpart of Britta Simon in UserVoice that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="11549-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11549-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="11549-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="11549-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="11549-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="11549-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="11549-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 UserVoice 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="11549-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="11549-148">**若要使用 UserVoice 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="11549-148">**To configure Azure AD single sign-on with UserVoice, perform the following steps:**</span></span>

1. <span data-ttu-id="11549-149">在 Azure 入口網站的 [UserVoice] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="11549-149">In the Azure portal, on the **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="11549-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="11549-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="11549-153">在 [UserVoice 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="11549-153">On the **UserVoice Domain and URLs** section, perform the following steps:</span></span>

    ![UserVoice 網域和 URL 單一登入資訊](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="11549-155">a.</span><span class="sxs-lookup"><span data-stu-id="11549-155">a.</span></span> <span data-ttu-id="11549-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="11549-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="11549-157">b.</span><span class="sxs-lookup"><span data-stu-id="11549-157">b.</span></span> <span data-ttu-id="11549-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="11549-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="11549-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="11549-159">These values are not real.</span></span> <span data-ttu-id="11549-160">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="11549-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="11549-161">請連絡 [UserVoice 客戶支援小組](https://www.uservoice.com/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="11549-161">Contact [UserVoice Client support team](https://www.uservoice.com/) to get these values.</span></span>

4. <span data-ttu-id="11549-162">在 [SAML 簽署憑證] 區段上，複製憑證的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="11549-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![憑證下載連結](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="11549-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="11549-164">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="11549-166">在 [UserVoice 組態] 區段上，按一下 [設定 UserVoice] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="11549-166">On the **UserVoice Configuration** section, click **Configure UserVoice** to open **Configure sign-on** window.</span></span> <span data-ttu-id="11549-167">從 [快速參考] 區段中複製 [登入 URL] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="11549-167">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![UserVoice 組態](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="11549-169">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 UserVoice 公司網站。</span><span class="sxs-lookup"><span data-stu-id="11549-169">In a different web browser window, log in to your UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="11549-170">在頂端工具列中，按一下 [設定]，然後從功能表選取 [Web 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="11549-170">In the toolbar on the top, click **Settings**, and then select **Web portal** from the menu.</span></span>
   
    <span data-ttu-id="11549-171">![應用程式端上的設定區段](./media/active-directory-saas-uservoice-tutorial/ic777519.png "設定")</span><span class="sxs-lookup"><span data-stu-id="11549-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="11549-172">在 [Web 入口網站] 索引標籤的 [使用者驗證] 區段中，按一下 [編輯]，以開啟 [編輯使用者驗證] 對話頁面。</span><span class="sxs-lookup"><span data-stu-id="11549-172">On the **Web portal** tab, in the **User authentication** section, click **Edit** to open the **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="11549-173">![[Web 入口網站] 索引標籤](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web 入口網站")</span><span class="sxs-lookup"><span data-stu-id="11549-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="11549-174">在 [編輯使用者驗證]  對話頁面上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="11549-174">On the **Edit User Authentication** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="11549-175">![編輯使用者驗證](./media/active-directory-saas-uservoice-tutorial/ic777521.png "編輯使用者驗證")</span><span class="sxs-lookup"><span data-stu-id="11549-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="11549-176">a.</span><span class="sxs-lookup"><span data-stu-id="11549-176">a.</span></span> <span data-ttu-id="11549-177">按一下 [單一登入 (SSO)] 。</span><span class="sxs-lookup"><span data-stu-id="11549-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="11549-178">b.</span><span class="sxs-lookup"><span data-stu-id="11549-178">b.</span></span> <span data-ttu-id="11549-179">將您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值，貼到 [SSO 遠端登入] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="11549-179">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="11549-180">c.</span><span class="sxs-lookup"><span data-stu-id="11549-180">c.</span></span> <span data-ttu-id="11549-181">將您從 Azure 入口網站複製的 [登出 URL] 值，貼到 [SSO 遠端登出] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="11549-181">Paste the **Sign-Out URL** value, which you have copied from the Azure portal into the **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="11549-182">d.</span><span class="sxs-lookup"><span data-stu-id="11549-182">d.</span></span> <span data-ttu-id="11549-183">將您從 Azure 入口網站複製的 [指紋] 值，貼到 [目前的憑證 SHA1 指紋] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="11549-183">Paste the **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="11549-184">e.</span><span class="sxs-lookup"><span data-stu-id="11549-184">e.</span></span> <span data-ttu-id="11549-185">按一下 [儲存驗證設定] 。</span><span class="sxs-lookup"><span data-stu-id="11549-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="11549-186">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="11549-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="11549-187">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="11549-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="11549-188">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="11549-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="11549-189">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="11549-189">Create an Azure AD test user</span></span>

<span data-ttu-id="11549-190">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="11549-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="11549-192">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="11549-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="11549-193">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="11549-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="11549-195">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="11549-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="11549-197">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="11549-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="11549-199">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="11549-199">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="11549-201">a.</span><span class="sxs-lookup"><span data-stu-id="11549-201">a.</span></span> <span data-ttu-id="11549-202">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="11549-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11549-203">b.</span><span class="sxs-lookup"><span data-stu-id="11549-203">b.</span></span> <span data-ttu-id="11549-204">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="11549-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="11549-205">c.</span><span class="sxs-lookup"><span data-stu-id="11549-205">c.</span></span> <span data-ttu-id="11549-206">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="11549-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="11549-207">d.</span><span class="sxs-lookup"><span data-stu-id="11549-207">d.</span></span> <span data-ttu-id="11549-208">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="11549-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="11549-209">建立 UserVoice 測試使用者</span><span class="sxs-lookup"><span data-stu-id="11549-209">Create a UserVoice test user</span></span>

<span data-ttu-id="11549-210">若要讓 Azure AD 使用者可以登入 UserVoice，則必須將他們佈建到 UserVoice。</span><span class="sxs-lookup"><span data-stu-id="11549-210">To enable Azure AD users to log in to UserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="11549-211">UserVoice 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="11549-211">In the case of UserVoice, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="11549-212">若要佈建使用者帳戶，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="11549-212">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="11549-213">登入您的 **UserVoice** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="11549-213">Log in to your **UserVoice** tenant.</span></span>

2. <span data-ttu-id="11549-214">移至 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="11549-214">Go to **Settings**.</span></span>
   
    <span data-ttu-id="11549-215">![設定](./media/active-directory-saas-uservoice-tutorial/ic777811.png "設定")</span><span class="sxs-lookup"><span data-stu-id="11549-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="11549-216">按一下 [一般] 。</span><span class="sxs-lookup"><span data-stu-id="11549-216">Click **General**.</span></span>

4. <span data-ttu-id="11549-217">按一下 [代理程式和權限] 。</span><span class="sxs-lookup"><span data-stu-id="11549-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="11549-218">![代理程式和權限](./media/active-directory-saas-uservoice-tutorial/ic777812.png "代理程式和權限")</span><span class="sxs-lookup"><span data-stu-id="11549-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="11549-219">按一下 [加入管理員] 。</span><span class="sxs-lookup"><span data-stu-id="11549-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="11549-220">![新增管理員](./media/active-directory-saas-uservoice-tutorial/ic777813.png "新增管理員")</span><span class="sxs-lookup"><span data-stu-id="11549-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="11549-221">在 [邀請管理員]  對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="11549-221">On the **Invite admins** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="11549-222">![邀請管理員](./media/active-directory-saas-uservoice-tutorial/ic777814.png "邀請管理員")</span><span class="sxs-lookup"><span data-stu-id="11549-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="11549-223">a.</span><span class="sxs-lookup"><span data-stu-id="11549-223">a.</span></span> <span data-ttu-id="11549-224">在 [電子郵件] 文字方塊中，輸入您要佈建之帳戶的電子郵件地址，然後按一下 [加入] 。</span><span class="sxs-lookup"><span data-stu-id="11549-224">In the Emails textbox, type the email address of the account you want to provision, and then click **Add**.</span></span>
   
    <span data-ttu-id="11549-225">b.</span><span class="sxs-lookup"><span data-stu-id="11549-225">b.</span></span> <span data-ttu-id="11549-226">按一下 [邀請] 。</span><span class="sxs-lookup"><span data-stu-id="11549-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="11549-227">您可以使用任何其他的 UserVoice 使用者帳戶建立工具或 UserVoice 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="11549-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice to provision AAD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="11549-228">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="11549-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="11549-229">在本節中，您會將 UserVoice 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="11549-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UserVoice.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="11549-231">**若要將 Britta Simon 指派給 UserVoice，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="11549-231">**To assign Britta Simon to UserVoice, perform the following steps:**</span></span>

1. <span data-ttu-id="11549-232">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="11549-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="11549-234">在應用程式清單中，選取 [UserVoice]。</span><span class="sxs-lookup"><span data-stu-id="11549-234">In the applications list, select **UserVoice**.</span></span>

    ![應用程式清單中的 UserVoice 連結](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="11549-236">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="11549-236">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="11549-238">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="11549-238">Click **Add** button.</span></span> <span data-ttu-id="11549-239">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="11549-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="11549-241">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="11549-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="11549-242">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="11549-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="11549-243">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="11549-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="11549-244">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="11549-244">Test single sign-on</span></span>

<span data-ttu-id="11549-245">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="11549-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="11549-246">當您在存取面板中按一下 [UserVoice] 圖格時，應該會自動登入您的 UserVoice 應用程式。</span><span class="sxs-lookup"><span data-stu-id="11549-246">When you click the UserVoice tile in the Access Panel, you should get automatically signed-on to your UserVoice application.</span></span>
<span data-ttu-id="11549-247">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="11549-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="11549-248">其他資源</span><span class="sxs-lookup"><span data-stu-id="11549-248">Additional resources</span></span>

* [<span data-ttu-id="11549-249">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="11549-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="11549-250">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="11549-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

