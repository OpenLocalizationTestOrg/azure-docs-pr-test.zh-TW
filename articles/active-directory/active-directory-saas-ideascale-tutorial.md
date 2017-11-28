---
title: "教學課程：Azure Active Directory 與 IdeaScale 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 IdeaScale 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="74f12-103">教學課程：Azure Active Directory 與 IdeaScale 整合</span><span class="sxs-lookup"><span data-stu-id="74f12-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="74f12-104">在此教學課程中，您學會如何 toointegrate IdeaScale 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="74f12-104">In this tutorial, you learn how toointegrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="74f12-105">與 Azure AD 整合 IdeaScale 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="74f12-105">Integrating IdeaScale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="74f12-106">您可以控制存取 tooIdeaScale Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="74f12-106">You can control in Azure AD who has access tooIdeaScale</span></span>
- <span data-ttu-id="74f12-107">您可以啟用您的使用者 tooautomatically get 登入 tooIdeaScale （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="74f12-107">You can enable your users tooautomatically get signed-on tooIdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="74f12-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="74f12-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="74f12-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="74f12-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74f12-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="74f12-110">Prerequisites</span></span>

<span data-ttu-id="74f12-111">tooconfigure 與 IdeaScale 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="74f12-111">tooconfigure Azure AD integration with IdeaScale, you need hello following items:</span></span>

- <span data-ttu-id="74f12-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="74f12-112">An Azure AD subscription</span></span>
- <span data-ttu-id="74f12-113">已啟用 IdeaScale 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="74f12-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="74f12-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="74f12-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="74f12-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="74f12-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="74f12-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="74f12-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="74f12-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="74f12-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="74f12-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="74f12-118">Scenario description</span></span>
<span data-ttu-id="74f12-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="74f12-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="74f12-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="74f12-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="74f12-121">從 hello 圖庫加入 IdeaScale</span><span class="sxs-lookup"><span data-stu-id="74f12-121">Adding IdeaScale from hello gallery</span></span>
2. <span data-ttu-id="74f12-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="74f12-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-hello-gallery"></a><span data-ttu-id="74f12-123">從 hello 圖庫加入 IdeaScale</span><span class="sxs-lookup"><span data-stu-id="74f12-123">Adding IdeaScale from hello gallery</span></span>
<span data-ttu-id="74f12-124">tooconfigure hello 整合 IdeaScale 的 Azure AD，您需要 tooadd IdeaScale hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="74f12-124">tooconfigure hello integration of IdeaScale into Azure AD, you need tooadd IdeaScale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="74f12-125">**tooadd IdeaScale 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="74f12-125">**tooadd IdeaScale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="74f12-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="74f12-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="74f12-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="74f12-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="74f12-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="74f12-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="74f12-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="74f12-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="74f12-133">在 [hello] 搜尋方塊中，輸入**IdeaScale**。</span><span class="sxs-lookup"><span data-stu-id="74f12-133">In hello search box, type **IdeaScale**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="74f12-135">在 hello 結果 窗格中，選取  **IdeaScale**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="74f12-135">In hello results panel, select **IdeaScale**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="74f12-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="74f12-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="74f12-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 IdeaScale 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="74f12-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="74f12-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 IdeaScale 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="74f12-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IdeaScale is tooa user in Azure AD.</span></span> <span data-ttu-id="74f12-140">換句話說，Azure AD 使用者與 hello IdeaScale 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="74f12-140">In other words, a link relationship between an Azure AD user and hello related user in IdeaScale needs toobe established.</span></span>

<span data-ttu-id="74f12-141">在 IdeaScale 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="74f12-141">In IdeaScale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="74f12-142">tooconfigure 及測試 Azure AD 單一登入 IdeaScale，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="74f12-142">tooconfigure and test Azure AD single sign-on with IdeaScale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="74f12-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="74f12-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="74f12-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="74f12-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="74f12-145">**[建立測試使用者 IdeaScale](#creating-an-ideascale-test-user)**  -toohave 許 Simon IdeaScale 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="74f12-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - toohave a counterpart of Britta Simon in IdeaScale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="74f12-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="74f12-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="74f12-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="74f12-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="74f12-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="74f12-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="74f12-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 IdeaScale 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="74f12-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="74f12-150">**tooconfigure Azure AD 單一登入 IdeaScale，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="74f12-150">**tooconfigure Azure AD single sign-on with IdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="74f12-151">在 Azure 入口網站上 hello hello **IdeaScale**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="74f12-151">In hello Azure portal, on hello **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="74f12-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="74f12-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="74f12-155">在 hello **IdeaScale 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="74f12-155">On hello **IdeaScale Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="74f12-157">a.</span><span class="sxs-lookup"><span data-stu-id="74f12-157">a.</span></span> <span data-ttu-id="74f12-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="74f12-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="74f12-159">b.</span><span class="sxs-lookup"><span data-stu-id="74f12-159">b.</span></span> <span data-ttu-id="74f12-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="74f12-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="74f12-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="74f12-161">These values are not real.</span></span> <span data-ttu-id="74f12-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="74f12-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="74f12-163">請連絡[IdeaScale 用戶端支援小組](http://support.ideascale.com/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="74f12-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="74f12-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="74f12-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="74f12-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="74f12-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="74f12-168">在 hello **IdeaScale 組態**區段中，按一下**設定 IdeaScale** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="74f12-168">On hello **IdeaScale Configuration** section, click **Configure IdeaScale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="74f12-169">複製 hello**登出 URL 和 SAML 實體識別碼**從 hello**快速參考章節**。</span><span class="sxs-lookup"><span data-stu-id="74f12-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section**.</span></span>

    ![設定單一登入](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="74f12-171">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour IdeaScale 公司網站。</span><span class="sxs-lookup"><span data-stu-id="74f12-171">In a different web browser window, log in tooyour IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="74f12-172">跳過**社群設定**。</span><span class="sxs-lookup"><span data-stu-id="74f12-172">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="74f12-173">![社群設定](./media/active-directory-saas-ideascale-tutorial/ic790847.png "社群設定")</span><span class="sxs-lookup"><span data-stu-id="74f12-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="74f12-174">跳過**安全性\>單一登入設定**。</span><span class="sxs-lookup"><span data-stu-id="74f12-174">Go too**Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="74f12-175">![單一登入設定](./media/active-directory-saas-ideascale-tutorial/ic790848.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="74f12-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="74f12-176">在 [單一登入類型]，選取 [SAML 2.0]。</span><span class="sxs-lookup"><span data-stu-id="74f12-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="74f12-177">![單一登入類型](./media/active-directory-saas-ideascale-tutorial/ic790849.png "單一登入類型")</span><span class="sxs-lookup"><span data-stu-id="74f12-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="74f12-178">在 [hello**單一登入設定**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="74f12-178">On hello **Single Signon Settings** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="74f12-179">![單一登入設定](./media/active-directory-saas-ideascale-tutorial/ic790850.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="74f12-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="74f12-180">a.</span><span class="sxs-lookup"><span data-stu-id="74f12-180">a.</span></span> <span data-ttu-id="74f12-181">在**SAML Ldp 實體識別碼**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="74f12-181">In **SAML IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="74f12-182">b.</span><span class="sxs-lookup"><span data-stu-id="74f12-182">b.</span></span> <span data-ttu-id="74f12-183">從 Azure 入口網站的下載的中繼資料檔案的 hello 內容複製並貼到 hello **SAML Ldp 中繼資料**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="74f12-183">Copy hello content of your downloaded metadata file from Azure portal, and paste it into hello **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="74f12-184">c.</span><span class="sxs-lookup"><span data-stu-id="74f12-184">c.</span></span> <span data-ttu-id="74f12-185">在**登出成功 URL**文字方塊中，貼上 hello 值**登出 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="74f12-185">In **Logout Success URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="74f12-186">d.</span><span class="sxs-lookup"><span data-stu-id="74f12-186">d.</span></span> <span data-ttu-id="74f12-187">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="74f12-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="74f12-188">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="74f12-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="74f12-189">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="74f12-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="74f12-190">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="74f12-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="74f12-191">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="74f12-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="74f12-192">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="74f12-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="74f12-194">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="74f12-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="74f12-195">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="74f12-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="74f12-197">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="74f12-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="74f12-199">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="74f12-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="74f12-201">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="74f12-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="74f12-203">a.</span><span class="sxs-lookup"><span data-stu-id="74f12-203">a.</span></span> <span data-ttu-id="74f12-204">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="74f12-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="74f12-205">b.</span><span class="sxs-lookup"><span data-stu-id="74f12-205">b.</span></span> <span data-ttu-id="74f12-206">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="74f12-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="74f12-207">c.</span><span class="sxs-lookup"><span data-stu-id="74f12-207">c.</span></span> <span data-ttu-id="74f12-208">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="74f12-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="74f12-209">d.</span><span class="sxs-lookup"><span data-stu-id="74f12-209">d.</span></span> <span data-ttu-id="74f12-210">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="74f12-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="74f12-211">建立 IdeaScale 測試使用者</span><span class="sxs-lookup"><span data-stu-id="74f12-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="74f12-212">tooenable Azure AD 使用者 toolog 入 IdeaScale，必須將他們佈建 tooIdeaScale 中。</span><span class="sxs-lookup"><span data-stu-id="74f12-212">tooenable Azure AD users toolog into IdeaScale, they must be provisioned in tooIdeaScale.</span></span> <span data-ttu-id="74f12-213">在 IdeaScale 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="74f12-213">In hello case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="74f12-214">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="74f12-214">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="74f12-215">登入 tooyour **IdeaScale**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="74f12-215">Log in tooyour **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="74f12-216">跳過**社群設定**。</span><span class="sxs-lookup"><span data-stu-id="74f12-216">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="74f12-217">![社群設定](./media/active-directory-saas-ideascale-tutorial/ic790847.png "社群設定")</span><span class="sxs-lookup"><span data-stu-id="74f12-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="74f12-218">跳過**基本設定\>成員管理**。</span><span class="sxs-lookup"><span data-stu-id="74f12-218">Go too**Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="74f12-219">按一下 [新增成員] 。</span><span class="sxs-lookup"><span data-stu-id="74f12-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="74f12-220">![成員管理](./media/active-directory-saas-ideascale-tutorial/ic790852.png "成員管理")</span><span class="sxs-lookup"><span data-stu-id="74f12-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="74f12-221">在 hello 加入新成員 區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="74f12-221">In hello Add New Member section, perform hello following steps:</span></span>
   
    <span data-ttu-id="74f12-222">![加入新成員](./media/active-directory-saas-ideascale-tutorial/ic790853.png "加入新成員")</span><span class="sxs-lookup"><span data-stu-id="74f12-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="74f12-223">a.</span><span class="sxs-lookup"><span data-stu-id="74f12-223">a.</span></span> <span data-ttu-id="74f12-224">在 hello**電子郵件地址**文字方塊中，您想 tooprovision 之有效 AAD 帳戶類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="74f12-224">In hello **Email Addresses** textbox, type hello email address of a valid AAD account you want tooprovision.</span></span>
   
    <span data-ttu-id="74f12-225">b.</span><span class="sxs-lookup"><span data-stu-id="74f12-225">b.</span></span> <span data-ttu-id="74f12-226">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="74f12-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="74f12-227">hello Azure Active Directory 帳戶持有者取得含有連結 tooconfirm hello 帳戶的電子郵件之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="74f12-227">hello Azure Active Directory account holder gets an email with a link tooconfirm hello account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="74f12-228">您可以使用任何其他 IdeaScale 使用者帳戶建立工具或 Api 提供 IdeaScale tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="74f12-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="74f12-229">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="74f12-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="74f12-230">在本節中，您可以授與存取 tooIdeaScale 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="74f12-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIdeaScale.</span></span>

![指派使用者][200] 

<span data-ttu-id="74f12-232">**tooassign 許 Simon tooIdeaScale，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="74f12-232">**tooassign Britta Simon tooIdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="74f12-233">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="74f12-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="74f12-235">在 [hello] 應用程式清單中，選取**IdeaScale**。</span><span class="sxs-lookup"><span data-stu-id="74f12-235">In hello applications list, select **IdeaScale**.</span></span>

    ![設定單一登入](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="74f12-237">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="74f12-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="74f12-239">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="74f12-239">Click **Add** button.</span></span> <span data-ttu-id="74f12-240">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="74f12-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="74f12-242">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="74f12-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="74f12-243">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="74f12-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="74f12-244">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="74f12-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="74f12-245">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="74f12-245">Testing single sign-on</span></span>


<span data-ttu-id="74f12-246">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="74f12-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="74f12-247">當您按一下 hello IdeaScale 磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 IdeaScale 應用程式。</span><span class="sxs-lookup"><span data-stu-id="74f12-247">When you click hello IdeaScale tile in hello Access Panel, you should get automatically signed-on tooyour IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="74f12-248">其他資源</span><span class="sxs-lookup"><span data-stu-id="74f12-248">Additional resources</span></span>

* [<span data-ttu-id="74f12-249">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="74f12-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="74f12-250">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="74f12-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

