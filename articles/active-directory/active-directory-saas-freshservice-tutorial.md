---
title: "教學課程：Azure Active Directory 與 Freshservice 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Freshservice 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d73624b87d058f66885ae72fda69a0aacc89c1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="dd7f4-103">教學課程：Azure Active Directory 與 Freshservice 整合</span><span class="sxs-lookup"><span data-stu-id="dd7f4-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="dd7f4-104">在此教學課程中，您學會如何 toointegrate Freshservice 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-104">In this tutorial, you learn how toointegrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd7f4-105">與 Azure AD 整合 Freshservice 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="dd7f4-105">Integrating Freshservice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dd7f4-106">您可以控制存取 tooFreshservice Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="dd7f4-106">You can control in Azure AD who has access tooFreshservice</span></span>
- <span data-ttu-id="dd7f4-107">您可以啟用您的使用者 tooautomatically get 登入 tooFreshservice （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="dd7f4-107">You can enable your users tooautomatically get signed-on tooFreshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dd7f4-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dd7f4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dd7f4-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd7f4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="dd7f4-110">Prerequisites</span></span>

<span data-ttu-id="dd7f4-111">tooconfigure 與 Freshservice 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="dd7f4-111">tooconfigure Azure AD integration with Freshservice, you need hello following items:</span></span>

- <span data-ttu-id="dd7f4-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dd7f4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dd7f4-113">已啟用 Freshservice 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dd7f4-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd7f4-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd7f4-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="dd7f4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd7f4-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd7f4-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd7f4-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="dd7f4-118">Scenario description</span></span>
<span data-ttu-id="dd7f4-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd7f4-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="dd7f4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd7f4-121">從 hello 圖庫加入 Freshservice</span><span class="sxs-lookup"><span data-stu-id="dd7f4-121">Adding Freshservice from hello gallery</span></span>
2. <span data-ttu-id="dd7f4-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="dd7f4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-hello-gallery"></a><span data-ttu-id="dd7f4-123">從 hello 圖庫加入 Freshservice</span><span class="sxs-lookup"><span data-stu-id="dd7f4-123">Adding Freshservice from hello gallery</span></span>
<span data-ttu-id="dd7f4-124">tooconfigure hello 整合 Freshservice 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Freshservice。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-124">tooconfigure hello integration of Freshservice into Azure AD, you need tooadd Freshservice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dd7f4-125">**tooadd Freshservice 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="dd7f4-125">**tooadd Freshservice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd7f4-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dd7f4-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dd7f4-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="dd7f4-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="dd7f4-133">在 [hello] 搜尋方塊中，輸入**Freshservice**。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-133">In hello search box, type **Freshservice**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="dd7f4-135">在 hello 結果 窗格中，選取  **Freshservice**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-135">In hello results panel, select **Freshservice**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dd7f4-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="dd7f4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dd7f4-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Freshservice 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dd7f4-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Freshservice 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Freshservice is tooa user in Azure AD.</span></span> <span data-ttu-id="dd7f4-140">換句話說，Azure AD 使用者與 hello Freshservice 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-140">In other words, a link relationship between an Azure AD user and hello related user in Freshservice needs toobe established.</span></span>

<span data-ttu-id="dd7f4-141">在 Freshservice 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-141">In Freshservice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dd7f4-142">tooconfigure 及與 Freshservice 的測試 Azure AD 單一登入，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="dd7f4-142">tooconfigure and test Azure AD single sign-on with Freshservice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dd7f4-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dd7f4-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd7f4-145">**[建立測試使用者 Freshservice](#creating-a-freshservice-test-user)**  -toohave 許 Simon Freshservice 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - toohave a counterpart of Britta Simon in Freshservice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd7f4-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd7f4-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dd7f4-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="dd7f4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dd7f4-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Freshservice 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="dd7f4-150">**tooconfigure Azure AD 單一登入 Freshservice 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="dd7f4-150">**tooconfigure Azure AD single sign-on with Freshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd7f4-151">在 Azure 入口網站上 hello hello **Freshservice**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-151">In hello Azure portal, on hello **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="dd7f4-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="dd7f4-155">在 hello **Freshservice 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd7f4-155">On hello **Freshservice Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="dd7f4-157">a.</span><span class="sxs-lookup"><span data-stu-id="dd7f4-157">a.</span></span> <span data-ttu-id="dd7f4-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="dd7f4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="dd7f4-159">b.</span><span class="sxs-lookup"><span data-stu-id="dd7f4-159">b.</span></span> <span data-ttu-id="dd7f4-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="dd7f4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dd7f4-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-161">These values are not real.</span></span> <span data-ttu-id="dd7f4-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dd7f4-163">請連絡[Freshservice 用戶端支援小組](https://support.freshservice.com/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-163">Contact [Freshservice Client support team](https://support.freshservice.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="dd7f4-164">在 hello **SAML 簽章憑證**區段中，複製**指紋**憑證值。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-164">On hello **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="dd7f4-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dd7f4-168">在 hello **Freshservice 組態**區段中，按一下**設定 Freshservice** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-168">On hello **Freshservice Configuration** section, click **Configure Freshservice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dd7f4-169">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="dd7f4-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="dd7f4-171">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour Freshservice 公司網站。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-171">In a different web browser window, log in tooyour Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="dd7f4-172">在 hello 最上層顯示 hello 功能表上，按一下**Admin**。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="dd7f4-173">![管理](./media/active-directory-saas-freshservice-tutorial/ic790814.png "管理")</span><span class="sxs-lookup"><span data-stu-id="dd7f4-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="dd7f4-174">在 hello**客戶入口網站**，按一下 **安全性**。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-174">In hello **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="dd7f4-175">![安全性](./media/active-directory-saas-freshservice-tutorial/ic790815.png "安全性")</span><span class="sxs-lookup"><span data-stu-id="dd7f4-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="dd7f4-176">在 hello**安全性**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd7f4-176">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="dd7f4-177">![單一登入](./media/active-directory-saas-freshservice-tutorial/ic790816.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="dd7f4-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="dd7f4-178">a.</span><span class="sxs-lookup"><span data-stu-id="dd7f4-178">a.</span></span> <span data-ttu-id="dd7f4-179">將 [單一登入] 切換為 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="dd7f4-180">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-180">b.</span></span> <span data-ttu-id="dd7f4-181">選取 [SAML SSO] 。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="dd7f4-182">c.</span><span class="sxs-lookup"><span data-stu-id="dd7f4-182">c.</span></span> <span data-ttu-id="dd7f4-183">在 hello **SAML 登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-183">In hello **SAML Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dd7f4-184">d.</span><span class="sxs-lookup"><span data-stu-id="dd7f4-184">d.</span></span> <span data-ttu-id="dd7f4-185">在 hello**登出 URL**文字方塊中，貼上 hello 值**登出 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dd7f4-186">e.</span><span class="sxs-lookup"><span data-stu-id="dd7f4-186">e.</span></span> <span data-ttu-id="dd7f4-187">在**安全性憑證指紋**文字方塊中，貼上 hello**指紋**憑證，您從 Azure 入口網站複製的值。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-187">In **Security Certificate Fingerprint** textbox, paste hello **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dd7f4-188">f.</span><span class="sxs-lookup"><span data-stu-id="dd7f4-188">f.</span></span> <span data-ttu-id="dd7f4-189">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="dd7f4-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="dd7f4-190">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="dd7f4-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dd7f4-191">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dd7f4-192">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dd7f4-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dd7f4-193">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="dd7f4-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="dd7f4-194">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="dd7f4-196">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="dd7f4-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd7f4-197">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dd7f4-199">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dd7f4-201">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dd7f4-203">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd7f4-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dd7f4-205">a.</span><span class="sxs-lookup"><span data-stu-id="dd7f4-205">a.</span></span> <span data-ttu-id="dd7f4-206">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd7f4-207">b.</span><span class="sxs-lookup"><span data-stu-id="dd7f4-207">b.</span></span> <span data-ttu-id="dd7f4-208">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dd7f4-209">c.</span><span class="sxs-lookup"><span data-stu-id="dd7f4-209">c.</span></span> <span data-ttu-id="dd7f4-210">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dd7f4-211">d.</span><span class="sxs-lookup"><span data-stu-id="dd7f4-211">d.</span></span> <span data-ttu-id="dd7f4-212">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="dd7f4-213">建立 Freshservice 測試使用者</span><span class="sxs-lookup"><span data-stu-id="dd7f4-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="dd7f4-214">tooenable Azure AD 使用者 toolog 中 tooFreshService，它們必須佈建到 FreshService。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-214">tooenable Azure AD users toolog in tooFreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="dd7f4-215">在 FreshService 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-215">In hello case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="dd7f4-216">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="dd7f4-216">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd7f4-217">登入 tooyour **FreshService**系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-217">Log in tooyour **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="dd7f4-218">在 hello 最上層顯示 hello 功能表上，按一下**Admin**。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-218">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="dd7f4-219">![管理](./media/active-directory-saas-freshservice-tutorial/ic790814.png "管理")</span><span class="sxs-lookup"><span data-stu-id="dd7f4-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="dd7f4-220">在 hello**使用者管理**區段中，按一下**要求者**。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-220">In hello **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="dd7f4-221">![要求者](./media/active-directory-saas-freshservice-tutorial/ic790818.png "要求者")</span><span class="sxs-lookup"><span data-stu-id="dd7f4-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="dd7f4-222">按一下 [新要求者] 。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="dd7f4-223">![新要求者](./media/active-directory-saas-freshservice-tutorial/ic790819.png "新要求者")</span><span class="sxs-lookup"><span data-stu-id="dd7f4-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="dd7f4-224">在 hello**新要求者**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd7f4-224">In hello **New Requester** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="dd7f4-225">![新要求者](./media/active-directory-saas-freshservice-tutorial/ic790820.png "新要求者")</span><span class="sxs-lookup"><span data-stu-id="dd7f4-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="dd7f4-226">a.</span><span class="sxs-lookup"><span data-stu-id="dd7f4-226">a.</span></span> <span data-ttu-id="dd7f4-227">輸入 hello**名字**和**電子郵件**想成 hello tooprovision 之有效 Azure Active Directory 帳戶的屬性相關的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-227">Enter hello **First Name** and **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="dd7f4-228">b.</span><span class="sxs-lookup"><span data-stu-id="dd7f4-228">b.</span></span> <span data-ttu-id="dd7f4-229">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="dd7f4-230">hello Azure Active Directory 帳戶持有者取得包含連結 tooconfirm hello 帳戶之前它會變成作用中的電子郵件</span><span class="sxs-lookup"><span data-stu-id="dd7f4-230">hello Azure Active Directory account holder gets an email including a link tooconfirm hello account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="dd7f4-231">您可以使用任何其他 FreshService 使用者帳戶建立工具或 Api 提供 FreshService tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-231">You can use any other FreshService user account creation tools or APIs provided by FreshService tooprovision AAD user accounts.</span></span>
>  

![指派使用者][200] 

<span data-ttu-id="dd7f4-233">**tooassign 許 Simon tooFreshservice，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="dd7f4-233">**tooassign Britta Simon tooFreshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd7f4-234">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="dd7f4-236">在 [hello] 應用程式清單中，選取**Freshservice**。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-236">In hello applications list, select **Freshservice**.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="dd7f4-238">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="dd7f4-240">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-240">Click **Add** button.</span></span> <span data-ttu-id="dd7f4-241">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="dd7f4-243">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dd7f4-244">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd7f4-245">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dd7f4-246">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="dd7f4-246">Testing single sign-on</span></span>

<span data-ttu-id="dd7f4-247">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dd7f4-248">當您按一下 hello Freshservice 磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 Freshservice 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dd7f4-248">When you click hello Freshservice tile in hello Access Panel, you should get automatically signed-on tooyour Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd7f4-249">其他資源</span><span class="sxs-lookup"><span data-stu-id="dd7f4-249">Additional resources</span></span>

* [<span data-ttu-id="dd7f4-250">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd7f4-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd7f4-251">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="dd7f4-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

