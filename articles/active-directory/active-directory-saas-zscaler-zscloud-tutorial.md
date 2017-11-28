---
title: "教學課程：Azure Active Directory 與 Zscaler ZSCloud 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Zscaler ZSCloud 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: af6d5c1994e715cccf959cc9fd3ba998e5b9effa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="5cdc2-103">教學課程：Azure Active Directory 與 Zscaler ZSCloud 整合</span><span class="sxs-lookup"><span data-stu-id="5cdc2-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="5cdc2-104">在此教學課程中，您學會如何 toointegrate Zscaler ZSCloud 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-104">In this tutorial, you learn how toointegrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5cdc2-105">Zscaler ZSCloud 整合與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="5cdc2-105">Integrating Zscaler ZSCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5cdc2-106">您可以控制存取 tooZscaler ZSCloud 的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="5cdc2-106">You can control in Azure AD who has access tooZscaler ZSCloud</span></span>
- <span data-ttu-id="5cdc2-107">您可以啟用您的使用者 tooautomatically get 登入 tooZscaler ZSCloud （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="5cdc2-107">You can enable your users tooautomatically get signed-on tooZscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5cdc2-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5cdc2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5cdc2-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5cdc2-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5cdc2-110">Prerequisites</span></span>

<span data-ttu-id="5cdc2-111">tooconfigure Azure AD 與 Zscaler ZSCloud 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="5cdc2-111">tooconfigure Azure AD integration with Zscaler ZSCloud, you need hello following items:</span></span>

- <span data-ttu-id="5cdc2-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5cdc2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5cdc2-113">啟用 Zscaler ZSCloud 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5cdc2-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5cdc2-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5cdc2-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5cdc2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5cdc2-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5cdc2-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5cdc2-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="5cdc2-118">Scenario description</span></span>
<span data-ttu-id="5cdc2-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5cdc2-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="5cdc2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5cdc2-121">從 hello 圖庫加入 Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="5cdc2-121">Adding Zscaler ZSCloud from hello gallery</span></span>
2. <span data-ttu-id="5cdc2-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5cdc2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-hello-gallery"></a><span data-ttu-id="5cdc2-123">從 hello 圖庫加入 Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="5cdc2-123">Adding Zscaler ZSCloud from hello gallery</span></span>
<span data-ttu-id="5cdc2-124">tooconfigure hello 整合 Zscaler ZSCloud 的 Azure AD，您需要 tooadd Zscaler ZSCloud hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-124">tooconfigure hello integration of Zscaler ZSCloud into Azure AD, you need tooadd Zscaler ZSCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5cdc2-125">**tooadd Zscaler ZSCloud 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5cdc2-125">**tooadd Zscaler ZSCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5cdc2-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5cdc2-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5cdc2-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="5cdc2-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="5cdc2-133">在 [hello] 搜尋方塊中，輸入**Zscaler ZSCloud**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-133">In hello search box, type **Zscaler ZSCloud**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. <span data-ttu-id="5cdc2-135">在 hello 結果 窗格中，選取  **Zscaler ZSCloud**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-135">In hello results panel, select **Zscaler ZSCloud**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5cdc2-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5cdc2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5cdc2-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Zscaler ZSCloud 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5cdc2-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 Zscaler ZSCloud 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler ZSCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="5cdc2-140">換句話說，Azure AD 使用者與 Zscaler ZSCloud 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler ZSCloud needs toobe established.</span></span>

<span data-ttu-id="5cdc2-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Zscaler ZSCloud 中。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="5cdc2-142">tooconfigure 及測試 Azure AD 單一登入 Zscaler ZSCloud，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="5cdc2-142">tooconfigure and test Azure AD single sign-on with Zscaler ZSCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5cdc2-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5cdc2-144">**[設定 proxy 設定](#configuring-proxy-settings)** -tooconfigure hello 在 Internet Explorer proxy 設定</span><span class="sxs-lookup"><span data-stu-id="5cdc2-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
2. <span data-ttu-id="5cdc2-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5cdc2-146">**[建立測試使用者 Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Zscaler ZSCloud 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - toohave a counterpart of Britta Simon in Zscaler ZSCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5cdc2-147">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5cdc2-148">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5cdc2-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5cdc2-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5cdc2-150">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Zscaler ZSCloud 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="5cdc2-151">**tooconfigure Azure AD 單一登入 Zscaler ZSCloud 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5cdc2-151">**tooconfigure Azure AD single sign-on with Zscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="5cdc2-152">在 Azure 入口網站上 hello hello **Zscaler ZSCloud**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-152">In hello Azure portal, on hello **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="5cdc2-154">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. <span data-ttu-id="5cdc2-156">在 hello **Zscaler ZSCloud 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5cdc2-156">On hello **Zscaler ZSCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="5cdc2-158">在 hello**登入 URL**文字方塊中，您的使用者 」 toosign 上 ZScaler ZSCloud 應用程式 tooyour 所使用的型別 hello URL。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-158">In hello **Sign-on URL** textbox, type hello URL used by your users toosign-on tooyour ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="5cdc2-159">具有這個值與 hello tooupdate 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5cdc2-160">請連絡[Zscaler ZSCloud 用戶端支援小組](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-160">Contact [Zscaler ZSCloud Client support team](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget this value.</span></span> 
 
4. <span data-ttu-id="5cdc2-161">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. <span data-ttu-id="5cdc2-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5cdc2-165">在 hello **Zscaler ZSCloud 設定**區段中，按一下**設定 Zscaler ZSCloud** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-165">On hello **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5cdc2-166">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="5cdc2-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. <span data-ttu-id="5cdc2-168">在不同的網頁瀏覽器視窗中，以登入 tooyour ZScaler ZSCloud 公司網站的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-168">In a different web browser window, log in tooyour ZScaler ZSCloud company site as an administrator.</span></span>

8. <span data-ttu-id="5cdc2-169">在 hello 最上層顯示 hello 功能表上，按一下**管理**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="5cdc2-170">![管理](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "管理")</span><span class="sxs-lookup"><span data-stu-id="5cdc2-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="5cdc2-171">在 [管理系統管理員和角色] 下按一下 [管理使用者和驗證]。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="5cdc2-172">![管理使用者和驗證](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "管理使用者和驗證")</span><span class="sxs-lookup"><span data-stu-id="5cdc2-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="5cdc2-173">在 hello**選擇驗證選項，為您的組織**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5cdc2-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="5cdc2-174">![驗證](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "驗證")</span><span class="sxs-lookup"><span data-stu-id="5cdc2-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="5cdc2-175">a.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-175">a.</span></span> <span data-ttu-id="5cdc2-176">選取 [使用 SAML 單一登入進行驗證] 。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="5cdc2-177">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-177">b.</span></span> <span data-ttu-id="5cdc2-178">按一下 [設定 SAML 單一登入參數] 。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="5cdc2-179">在 hello**設定 SAML 單一登入參數**對話方塊頁面上，執行下列步驟，hello，然後按一下**完成**</span><span class="sxs-lookup"><span data-stu-id="5cdc2-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="5cdc2-180">![單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="5cdc2-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="5cdc2-181">a.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-181">a.</span></span> <span data-ttu-id="5cdc2-182">貼上 hello **SAML 單一登入服務 URL**值傳入 hello **hello SAML 入口網站 toowhich 使用者的 URL 會傳送驗證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-182">Paste hello **SAML Single Sign-On Service URL** value into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="5cdc2-183">b.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-183">b.</span></span> <span data-ttu-id="5cdc2-184">在 hello**屬性包含登入名稱**文字方塊中，輸入**NameID**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="5cdc2-185">c.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-185">c.</span></span> <span data-ttu-id="5cdc2-186">tooupload 下載的憑證，按一下  **Zscaler pem**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="5cdc2-187">d.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-187">d.</span></span> <span data-ttu-id="5cdc2-188">選取 [啟用 SAML 自動佈建] 。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="5cdc2-189">在 hello**設定使用者驗證**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5cdc2-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="5cdc2-190">![管理](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "管理")</span><span class="sxs-lookup"><span data-stu-id="5cdc2-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="5cdc2-191">a.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-191">a.</span></span> <span data-ttu-id="5cdc2-192">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-192">Click **Save**.</span></span>

    <span data-ttu-id="5cdc2-193">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-193">b.</span></span> <span data-ttu-id="5cdc2-194">按一下 [立即啟用] 。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="5cdc2-195">進行 Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="5cdc2-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="5cdc2-196">在 Internet Explorer tooconfigure hello proxy 設定</span><span class="sxs-lookup"><span data-stu-id="5cdc2-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="5cdc2-197">啟動 **Internet Explorer**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="5cdc2-198">選取**網際網路選項**從 hello**工具**功能表開啟 hello**網際網路選項**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="5cdc2-199">![網際網路選項](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "網際網路選項")</span><span class="sxs-lookup"><span data-stu-id="5cdc2-199">![Internet Options](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="5cdc2-200">按一下 hello**連線** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="5cdc2-201">![連線](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "連線")</span><span class="sxs-lookup"><span data-stu-id="5cdc2-201">![Connections](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="5cdc2-202">按一下**LAN 設定**tooopen hello **LAN 設定**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="5cdc2-203">在 hello Proxy 伺服器區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5cdc2-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="5cdc2-204">![Proxy 伺服器](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy 伺服器")</span><span class="sxs-lookup"><span data-stu-id="5cdc2-204">![Proxy server](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="5cdc2-205">a.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-205">a.</span></span> <span data-ttu-id="5cdc2-206">選取 [在您的區域網路使用 Proxy 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="5cdc2-207">b.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-207">b.</span></span> <span data-ttu-id="5cdc2-208">在 [hello 位址] 文字方塊中輸入**gateway.zscalerone.ne**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-208">In hello Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="5cdc2-209">c.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-209">c.</span></span> <span data-ttu-id="5cdc2-210">在 [hello 連接埠] 文字方塊中，輸入**80**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="5cdc2-211">d.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-211">d.</span></span> <span data-ttu-id="5cdc2-212">選取 [近端網址不使用 Proxy 伺服器] 。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="5cdc2-213">e.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-213">e.</span></span> <span data-ttu-id="5cdc2-214">按一下**確定**tooclose hello**區域網路 (LAN) 設定**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="5cdc2-215">按一下**確定**tooclose hello**網際網路選項**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5cdc2-216">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5cdc2-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="5cdc2-217">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="5cdc2-219">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5cdc2-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5cdc2-220">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5cdc2-222">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5cdc2-224">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5cdc2-226">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5cdc2-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5cdc2-228">a.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-228">a.</span></span> <span data-ttu-id="5cdc2-229">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5cdc2-230">b.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-230">b.</span></span> <span data-ttu-id="5cdc2-231">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5cdc2-232">c.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-232">c.</span></span> <span data-ttu-id="5cdc2-233">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5cdc2-234">d.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-234">d.</span></span> <span data-ttu-id="5cdc2-235">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="5cdc2-236">建立 Zscaler ZSCloud 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5cdc2-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="5cdc2-237">tooenable Azure AD 使用者 toolog 中 tooZScaler ZSCloud，它們必須已佈建的 tooZScaler ZSCloud。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-237">tooenable Azure AD users toolog in tooZScaler ZSCloud, they must be provisioned tooZScaler ZSCloud.</span></span>  
<span data-ttu-id="5cdc2-238">在 ZScaler ZSCloud 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-238">In hello case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="5cdc2-239">tooconfigure 使用者佈建，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5cdc2-239">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="5cdc2-240">登入 tooyour **Zscaler**租用戶。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-240">Log in tooyour **Zscaler** tenant.</span></span>

2. <span data-ttu-id="5cdc2-241">按一下 [系統管理] 。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="5cdc2-242">![管理](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "管理")</span><span class="sxs-lookup"><span data-stu-id="5cdc2-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="5cdc2-243">按一下 [使用者管理] 。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="5cdc2-244">![新增](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "新增")</span><span class="sxs-lookup"><span data-stu-id="5cdc2-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

4. <span data-ttu-id="5cdc2-245">在 hello**使用者**索引標籤上，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-245">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="5cdc2-246">![新增](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "新增")</span><span class="sxs-lookup"><span data-stu-id="5cdc2-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="5cdc2-247">在 hello 新增使用者 區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5cdc2-247">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="5cdc2-248">![新增使用者](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="5cdc2-248">![Add User](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="5cdc2-249">a.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-249">a.</span></span> <span data-ttu-id="5cdc2-250">型別 hello **UserID**，**使用者顯示名稱**，**密碼**，**確認密碼**，然後選取**群組**和 hello**部門**想 tooprovision 之有效 AAD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-250">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="5cdc2-251">b.</span><span class="sxs-lookup"><span data-stu-id="5cdc2-251">b.</span></span> <span data-ttu-id="5cdc2-252">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="5cdc2-253">您可以使用任何其他 ZScaler ZSCloud 使用者帳戶建立工具或 Api 提供 ZScaler ZSCloud tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5cdc2-254">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="5cdc2-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5cdc2-255">在本節中，您可以授與存取 tooZscaler ZSCloud 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler ZSCloud.</span></span>

![指派使用者][200] 

<span data-ttu-id="5cdc2-257">**tooassign 許 Simon tooZscaler ZSCloud 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5cdc2-257">**tooassign Britta Simon tooZscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="5cdc2-258">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="5cdc2-260">在 [hello] 應用程式清單中，選取**Zscaler ZSCloud**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-260">In hello applications list, select **Zscaler ZSCloud**.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. <span data-ttu-id="5cdc2-262">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="5cdc2-264">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-264">Click **Add** button.</span></span> <span data-ttu-id="5cdc2-265">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="5cdc2-267">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5cdc2-268">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5cdc2-269">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5cdc2-270">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="5cdc2-270">Testing single sign-on</span></span>

<span data-ttu-id="5cdc2-271">如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-271">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>

<span data-ttu-id="5cdc2-272">當您按一下的 hello Zscaler ZSCloud 磚 hello 存取面板中時，您應該取得自動登入 tooyour Zscaler ZSCloud 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-272">When you click hello Zscaler ZSCloud tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler ZSCloud application.</span></span>

<span data-ttu-id="5cdc2-273">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="5cdc2-273">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5cdc2-274">其他資源</span><span class="sxs-lookup"><span data-stu-id="5cdc2-274">Additional resources</span></span>

* [<span data-ttu-id="5cdc2-275">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5cdc2-275">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5cdc2-276">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5cdc2-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

