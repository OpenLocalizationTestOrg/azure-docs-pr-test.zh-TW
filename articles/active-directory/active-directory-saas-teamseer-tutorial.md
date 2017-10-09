---
title: "教學課程：Azure Active Directory 與 TeamSeer 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 TeamSeer 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 876d13e446115acd50b01c7f44db99357045e429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="e3d72-103">教學課程：Azure Active Directory 與 TeamSeer 整合</span><span class="sxs-lookup"><span data-stu-id="e3d72-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="e3d72-104">在此教學課程中，您學會如何 toointegrate TeamSeer 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="e3d72-104">In this tutorial, you learn how toointegrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e3d72-105">與 Azure AD 整合 TeamSeer 可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="e3d72-105">Integrating TeamSeer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e3d72-106">您可以控制存取 tooTeamSeer Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="e3d72-106">You can control in Azure AD who has access tooTeamSeer</span></span>
- <span data-ttu-id="e3d72-107">您可以啟用您的使用者 tooautomatically get 登入 tooTeamSeer （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="e3d72-107">You can enable your users tooautomatically get signed-on tooTeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e3d72-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e3d72-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e3d72-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e3d72-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3d72-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e3d72-110">Prerequisites</span></span>

<span data-ttu-id="e3d72-111">tooconfigure 與 TeamSeer 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="e3d72-111">tooconfigure Azure AD integration with TeamSeer, you need hello following items:</span></span>

- <span data-ttu-id="e3d72-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e3d72-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e3d72-113">已啟用 TeamSeer 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e3d72-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e3d72-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="e3d72-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e3d72-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e3d72-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e3d72-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e3d72-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e3d72-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="e3d72-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e3d72-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="e3d72-118">Scenario description</span></span>
<span data-ttu-id="e3d72-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e3d72-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e3d72-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="e3d72-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e3d72-121">從 hello 圖庫加入 TeamSeer</span><span class="sxs-lookup"><span data-stu-id="e3d72-121">Adding TeamSeer from hello gallery</span></span>
2. <span data-ttu-id="e3d72-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e3d72-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-hello-gallery"></a><span data-ttu-id="e3d72-123">從 hello 圖庫加入 TeamSeer</span><span class="sxs-lookup"><span data-stu-id="e3d72-123">Adding TeamSeer from hello gallery</span></span>
<span data-ttu-id="e3d72-124">tooconfigure hello 整合 TeamSeer tooAzure AD 中的，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd TeamSeer。</span><span class="sxs-lookup"><span data-stu-id="e3d72-124">tooconfigure hello integration of TeamSeer in tooAzure AD, you need tooadd TeamSeer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e3d72-125">**tooadd TeamSeer 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e3d72-125">**tooadd TeamSeer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3d72-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="e3d72-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e3d72-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e3d72-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e3d72-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e3d72-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="e3d72-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3d72-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="e3d72-133">在 [hello] 搜尋方塊中，輸入**TeamSeer**。</span><span class="sxs-lookup"><span data-stu-id="e3d72-133">In hello search box, type **TeamSeer**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="e3d72-135">在 hello 結果 窗格中，選取  **TeamSeer**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3d72-135">In hello results panel, select **TeamSeer**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e3d72-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e3d72-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e3d72-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 TeamSeer 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e3d72-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e3d72-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 TeamSeer 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="e3d72-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TeamSeer is tooa user in Azure AD.</span></span> <span data-ttu-id="e3d72-140">換句話說，Azure AD 使用者與 hello TeamSeer 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="e3d72-140">In other words, a link relationship between an Azure AD user and hello related user in TeamSeer needs toobe established.</span></span>

<span data-ttu-id="e3d72-141">在 TeamSeer 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e3d72-141">In TeamSeer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e3d72-142">tooconfigure 及測試 Azure AD 單一登入 TeamSeer，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="e3d72-142">tooconfigure and test Azure AD single sign-on with TeamSeer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e3d72-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="e3d72-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e3d72-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="e3d72-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e3d72-145">**[建立測試使用者 TeamSeer](#creating-a-teamseer-test-user)**  -toohave 許 Simon TeamSeer 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="e3d72-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - toohave a counterpart of Britta Simon in TeamSeer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e3d72-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e3d72-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e3d72-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="e3d72-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e3d72-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e3d72-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e3d72-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 TeamSeer 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="e3d72-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="e3d72-150">**tooconfigure Azure AD 單一登入 TeamSeer，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e3d72-150">**tooconfigure Azure AD single sign-on with TeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3d72-151">在 Azure 入口網站上 hello hello **TeamSeer**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="e3d72-151">In hello Azure portal, on hello **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="e3d72-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e3d72-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="e3d72-155">在 hello **TeamSeer 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e3d72-155">On hello **TeamSeer Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="e3d72-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="e3d72-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e3d72-158">hello 值不是真正的。</span><span class="sxs-lookup"><span data-stu-id="e3d72-158">hello value is not real.</span></span> <span data-ttu-id="e3d72-159">更新 hello 值與 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="e3d72-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="e3d72-160">請連絡[TeamSeer 用戶端支援小組](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html)tooget hello 值。</span><span class="sxs-lookup"><span data-stu-id="e3d72-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) tooget hello value.</span></span> 
 
4. <span data-ttu-id="e3d72-161">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="e3d72-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="e3d72-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3d72-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e3d72-165">在 hello **TeamSeer 組態**區段中，按一下**設定 TeamSeer** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="e3d72-165">On hello **TeamSeer Configuration** section, click **Configure TeamSeer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e3d72-166">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="e3d72-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="e3d72-168">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour TeamSeer 公司網站。</span><span class="sxs-lookup"><span data-stu-id="e3d72-168">In a different web browser window, log in tooyour TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="e3d72-169">跳過**HR 管理**。</span><span class="sxs-lookup"><span data-stu-id="e3d72-169">Go too**HR Admin**.</span></span>
   
    <span data-ttu-id="e3d72-170">![HR 管理](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR 管理")</span><span class="sxs-lookup"><span data-stu-id="e3d72-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="e3d72-171">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="e3d72-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="e3d72-172">![設定](./media/active-directory-saas-teamseer-tutorial/ic789635.png "設定")</span><span class="sxs-lookup"><span data-stu-id="e3d72-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="e3d72-173">按一下 [設定 SAML 提供者詳細資料] 。</span><span class="sxs-lookup"><span data-stu-id="e3d72-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="e3d72-174">![SAML 設定](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="e3d72-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="e3d72-175">在 hello SAML 提供者詳細資料 區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e3d72-175">In hello SAML provider details section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e3d72-176">![SAML 設定](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="e3d72-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="e3d72-177">a.</span><span class="sxs-lookup"><span data-stu-id="e3d72-177">a.</span></span> <span data-ttu-id="e3d72-178">貼上 hello**單一登入服務 URL**中 toohello 值**URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="e3d72-178">Paste hello **Single Sign-On Service URL** value in toohello **URL** textbox.</span></span>
          
    <span data-ttu-id="e3d72-179">b.</span><span class="sxs-lookup"><span data-stu-id="e3d72-179">b.</span></span> <span data-ttu-id="e3d72-180">在 記事本，複製 hello tooyour 剪貼簿 中，在它的內容中開啟 base-64 編碼的憑證，然後將它貼入 toohello **IdP 公用憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="e3d72-180">Open your base-64 encoded certificate in notepad, copy hello content of it in tooyour clipboard, and then paste it toohello **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="e3d72-181">toocomplete hello SAML 提供者組態，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e3d72-181">toocomplete hello SAML provider configuration, perform hello following steps:</span></span>
    
    <span data-ttu-id="e3d72-182">![SAML 設定](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="e3d72-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="e3d72-183">a.</span><span class="sxs-lookup"><span data-stu-id="e3d72-183">a.</span></span> <span data-ttu-id="e3d72-184">在 hello**測試電子郵件地址**，輸入 hello 測試使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="e3d72-184">In hello **Test Email Addresses**, type hello test user’s email address.</span></span> 
  
    <span data-ttu-id="e3d72-185">b.</span><span class="sxs-lookup"><span data-stu-id="e3d72-185">b.</span></span> <span data-ttu-id="e3d72-186">在 [hello**簽發者**類型 hello hello 服務提供者的簽發者 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="e3d72-186">In hello **Issuer** textbox, type hello Issuer URL of hello service provider.</span></span> 
  
    <span data-ttu-id="e3d72-187">c.</span><span class="sxs-lookup"><span data-stu-id="e3d72-187">c.</span></span> <span data-ttu-id="e3d72-188">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="e3d72-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e3d72-189">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="e3d72-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e3d72-190">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="e3d72-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e3d72-191">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e3d72-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e3d72-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e3d72-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="e3d72-193">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e3d72-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="e3d72-195">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e3d72-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3d72-196">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="e3d72-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e3d72-198">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="e3d72-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e3d72-200">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="e3d72-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e3d72-202">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e3d72-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e3d72-204">a.</span><span class="sxs-lookup"><span data-stu-id="e3d72-204">a.</span></span> <span data-ttu-id="e3d72-205">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e3d72-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e3d72-206">b.</span><span class="sxs-lookup"><span data-stu-id="e3d72-206">b.</span></span> <span data-ttu-id="e3d72-207">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="e3d72-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e3d72-208">c.</span><span class="sxs-lookup"><span data-stu-id="e3d72-208">c.</span></span> <span data-ttu-id="e3d72-209">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="e3d72-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e3d72-210">d.</span><span class="sxs-lookup"><span data-stu-id="e3d72-210">d.</span></span> <span data-ttu-id="e3d72-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e3d72-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="e3d72-212">建立 TeamSeer 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e3d72-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="e3d72-213">tooenable Azure AD 使用者 toolog 中 tooTeamSeer，必須將他們佈建 tooShiftPlanning 中。</span><span class="sxs-lookup"><span data-stu-id="e3d72-213">tooenable Azure AD users toolog in tooTeamSeer, they must be provisioned in tooShiftPlanning.</span></span> <span data-ttu-id="e3d72-214">在 TeamSeer 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="e3d72-214">In hello case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="e3d72-215">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e3d72-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3d72-216">登入 tooyour **TeamSeer**系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="e3d72-216">Log in tooyour **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="e3d72-217">執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e3d72-217">Perform hello following steps:</span></span>
   
    <span data-ttu-id="e3d72-218">![HR 管理](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR 管理")</span><span class="sxs-lookup"><span data-stu-id="e3d72-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="e3d72-219">a.</span><span class="sxs-lookup"><span data-stu-id="e3d72-219">a.</span></span> <span data-ttu-id="e3d72-220">跳過**HR 管理\>使用者**。</span><span class="sxs-lookup"><span data-stu-id="e3d72-220">Go too**HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="e3d72-221">b.</span><span class="sxs-lookup"><span data-stu-id="e3d72-221">b.</span></span> <span data-ttu-id="e3d72-222">按一下**執行 hello 新增使用者精靈**。</span><span class="sxs-lookup"><span data-stu-id="e3d72-222">Click **Run hello New User wizard**.</span></span>

3. <span data-ttu-id="e3d72-223">在 hello**使用者詳細資料**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e3d72-223">In hello **User Details** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e3d72-224">![使用者詳細資料](./media/active-directory-saas-teamseer-tutorial/ic789641.png "使用者詳細資料")</span><span class="sxs-lookup"><span data-stu-id="e3d72-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="e3d72-225">a.</span><span class="sxs-lookup"><span data-stu-id="e3d72-225">a.</span></span> <span data-ttu-id="e3d72-226">型別 hello**名字**，**姓氏**，**使用者名稱 （電子郵件地址）**的有效 AAD 帳戶，您想要在 toohello tooprovision 相關的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="e3d72-226">Type hello **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want tooprovision in toohello related textboxes.</span></span>
  
    <span data-ttu-id="e3d72-227">b.</span><span class="sxs-lookup"><span data-stu-id="e3d72-227">b.</span></span> <span data-ttu-id="e3d72-228">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="e3d72-228">Click **Next**.</span></span>

4. <span data-ttu-id="e3d72-229">依照 hello 螢幕上指示，加入新的使用者，並按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="e3d72-229">Follow hello on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="e3d72-230">您可以使用任何其他 TeamSeer 使用者帳戶建立工具或 Api 提供 TeamSeer tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="e3d72-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e3d72-231">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="e3d72-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e3d72-232">在本節中，您可以授與存取 tooTeamSeer 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e3d72-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTeamSeer.</span></span>

![指派使用者][200] 

<span data-ttu-id="e3d72-234">**tooassign 許 Simon tooTeamSeer，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e3d72-234">**tooassign Britta Simon tooTeamSeer, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3d72-235">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e3d72-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e3d72-237">在 [hello] 應用程式清單中，選取**TeamSeer**。</span><span class="sxs-lookup"><span data-stu-id="e3d72-237">In hello applications list, select **TeamSeer**.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="e3d72-239">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="e3d72-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="e3d72-241">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3d72-241">Click **Add** button.</span></span> <span data-ttu-id="e3d72-242">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e3d72-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="e3d72-244">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="e3d72-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e3d72-245">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3d72-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e3d72-246">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3d72-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e3d72-247">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e3d72-247">Testing single sign-on</span></span>

<span data-ttu-id="e3d72-248">如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="e3d72-248">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="e3d72-249">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="e3d72-249">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e3d72-250">其他資源</span><span class="sxs-lookup"><span data-stu-id="e3d72-250">Additional resources</span></span>

* [<span data-ttu-id="e3d72-251">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3d72-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e3d72-252">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e3d72-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

