---
title: "教學課程：Azure Active Directory 與 8x8 Virtual Office 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 及 8 x 8 虛擬辦公室之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: df5c5de77285cd3912b68cc3b1e3eee274aa951c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="c37e9-103">教學課程：Azure Active Directory 與 8x8 Virtual Office 整合</span><span class="sxs-lookup"><span data-stu-id="c37e9-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="c37e9-104">在此教學課程中，您學會如何 toointegrate 8 x 8 虛擬 Office 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="c37e9-104">In this tutorial, you learn how toointegrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c37e9-105">整合 8 x 8 虛擬 Office 與 Azure AD 提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="c37e9-105">Integrating 8x8 Virtual Office with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c37e9-106">您可以在 Azure AD 中擁有存取 too8x8 控制虛擬 Office</span><span class="sxs-lookup"><span data-stu-id="c37e9-106">You can control in Azure AD who has access too8x8 Virtual Office</span></span>
- <span data-ttu-id="c37e9-107">您可以啟用 tooautomatically 取得的使用者登入 too8x8 虛擬辦公室 （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="c37e9-107">You can enable your users tooautomatically get signed-on too8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c37e9-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c37e9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c37e9-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c37e9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c37e9-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c37e9-110">Prerequisites</span></span>

<span data-ttu-id="c37e9-111">tooconfigure 8 x 8 虛擬 Office 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="c37e9-111">tooconfigure Azure AD integration with 8x8 Virtual Office, you need hello following items:</span></span>

- <span data-ttu-id="c37e9-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c37e9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c37e9-113">已啟用 8x8 Virtual Office 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c37e9-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c37e9-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="c37e9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c37e9-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c37e9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c37e9-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c37e9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c37e9-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="c37e9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c37e9-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="c37e9-118">Scenario description</span></span>
<span data-ttu-id="c37e9-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c37e9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c37e9-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="c37e9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c37e9-121">新增 8 x 8 虛擬 Office 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="c37e9-121">Adding 8x8 Virtual Office from hello gallery</span></span>
2. <span data-ttu-id="c37e9-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c37e9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-hello-gallery"></a><span data-ttu-id="c37e9-123">新增 8 x 8 虛擬 Office 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="c37e9-123">Adding 8x8 Virtual Office from hello gallery</span></span>
<span data-ttu-id="c37e9-124">tooconfigure hello 整合 8 x 8 虛擬 Office 到 Azure AD，您需要 tooadd 8 x 8 虛擬 Office hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c37e9-124">tooconfigure hello integration of 8x8 Virtual Office into Azure AD, you need tooadd 8x8 Virtual Office from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c37e9-125">**tooadd 8 x 8 虛擬 Office 從 hello 組件庫中，執行下列步驟 hello:**</span><span class="sxs-lookup"><span data-stu-id="c37e9-125">**tooadd 8x8 Virtual Office from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c37e9-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c37e9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c37e9-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c37e9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c37e9-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c37e9-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="c37e9-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="c37e9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="c37e9-133">在 [hello] 搜尋方塊中，輸入**8 x 8 虛擬 Office**。</span><span class="sxs-lookup"><span data-stu-id="c37e9-133">In hello search box, type **8x8 Virtual Office**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="c37e9-135">在 hello 結果 窗格中，選取  **8 x 8 虛擬 Office**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c37e9-135">In hello results panel, select **8x8 Virtual Office**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c37e9-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c37e9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c37e9-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 8x8 Virtual Office 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c37e9-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c37e9-139">單一登入 toowork，Azure AD 需要 tooknow 8 x 8 虛擬 Office 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="c37e9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 8x8 Virtual Office is tooa user in Azure AD.</span></span> <span data-ttu-id="c37e9-140">換句話說，Azure AD 使用者和 8 x 8 中的 hello 相關的使用者之間的連結關聯性虛擬辦公室需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="c37e9-140">In other words, a link relationship between an Azure AD user and hello related user in 8x8 Virtual Office needs toobe established.</span></span>

<span data-ttu-id="c37e9-141">8 x 8 虛擬辦公室，指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="c37e9-141">In 8x8 Virtual Office, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c37e9-142">tooconfigure 及 8 x 8 虛擬 Office 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="c37e9-142">tooconfigure and test Azure AD single sign-on with 8x8 Virtual Office, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c37e9-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="c37e9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c37e9-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="c37e9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c37e9-145">**[建立 8 x 8 虛擬 Office 測試使用者](#creating-a-8x8-virtual-office-test-user)** -toohave 許 Simon 8 x 8 虛擬 office 連結的 toohello Azure AD 使用者表示法的對應項目。</span><span class="sxs-lookup"><span data-stu-id="c37e9-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - toohave a counterpart of Britta Simon in 8x8 Virtual Office that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c37e9-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c37e9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c37e9-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="c37e9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c37e9-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c37e9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c37e9-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 8 x 8 虛擬 Office 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="c37e9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="c37e9-150">**tooconfigure Azure AD 單一登入與 8 x 8 虛擬 Office，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c37e9-150">**tooconfigure Azure AD single sign-on with 8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="c37e9-151">在 Azure 入口網站上 hello hello **8 x 8 虛擬 Office**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="c37e9-151">In hello Azure portal, on hello **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="c37e9-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c37e9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="c37e9-155">在 hello **8 x 8 虛擬網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c37e9-155">On hello **8x8 Virtual Office Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="c37e9-157">a.</span><span class="sxs-lookup"><span data-stu-id="c37e9-157">a.</span></span> <span data-ttu-id="c37e9-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="c37e9-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="c37e9-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="c37e9-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="c37e9-160">b.</span><span class="sxs-lookup"><span data-stu-id="c37e9-160">b.</span></span> <span data-ttu-id="c37e9-161">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="c37e9-161">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="c37e9-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="c37e9-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c37e9-163">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="c37e9-163">These values are not real.</span></span> <span data-ttu-id="c37e9-164">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="c37e9-164">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="c37e9-165">請連絡[8 x 8 虛擬 Office 支援小組](https://www.8x8.com/about-us/contact-us)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="c37e9-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) tooget these values.</span></span>
 


4. <span data-ttu-id="c37e9-166">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Raw)**然後儲存 hello 憑證檔案儲存在您的電腦。</span><span class="sxs-lookup"><span data-stu-id="c37e9-166">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="c37e9-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c37e9-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c37e9-170">在 hello **8 x 8 虛擬 Office 設定**區段中，按一下**設定 8 x 8 虛擬 Office** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="c37e9-170">On hello **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c37e9-171">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="c37e9-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="c37e9-173">以系統管理員身分登入 tooyour 8 x 8 虛擬 Office 租用戶。</span><span class="sxs-lookup"><span data-stu-id="c37e9-173">Sign-on tooyour 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="c37e9-174">在 [應用程式面板] 上選取 [Virtual Office 帳戶管理員]  。</span><span class="sxs-lookup"><span data-stu-id="c37e9-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![在應用程式端設定](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="c37e9-176">選取**商務**帳戶 toomanage 再按一下**登入** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c37e9-176">Select **Business** account toomanage and click **Sign In** button.</span></span>
   
    ![在應用程式端設定](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="c37e9-178">按一下**帳戶**hello 功能表清單中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c37e9-178">Click **Accounts** tab in hello menu list.</span></span>
   
    ![在應用程式端設定](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="c37e9-180">按一下**單一登入**hello 帳戶清單中。</span><span class="sxs-lookup"><span data-stu-id="c37e9-180">Click **Single Sign On** in hello list of Accounts.</span></span>
   
    ![在應用程式端設定](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="c37e9-182">選取 [驗證方法] 底下的 [單一登入]，然後按一下 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="c37e9-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![在應用程式端設定](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="c37e9-184">複製**SAML SSO URL**，**單一登登出服務 URL**和**簽發者 URL**從 Azure AD 太**登入 URL**，**登出 URL**和**簽發者 URL** 8 x 8 虛擬辦公室。</span><span class="sxs-lookup"><span data-stu-id="c37e9-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD too**Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![在應用程式端設定](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="c37e9-186">按一下**瀏覽器**按鈕 tooupload hello 憑證，您從 Azure AD 中，下載，然後按一下 hello**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c37e9-186">Click **Browser** button tooupload hello certificate which you downloaded from Azure AD, and click hello **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="c37e9-187">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="c37e9-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c37e9-188">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="c37e9-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c37e9-189">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c37e9-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c37e9-190">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c37e9-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="c37e9-191">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c37e9-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="c37e9-193">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c37e9-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c37e9-194">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c37e9-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c37e9-196">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="c37e9-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c37e9-198">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="c37e9-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c37e9-200">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c37e9-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c37e9-202">a.</span><span class="sxs-lookup"><span data-stu-id="c37e9-202">a.</span></span> <span data-ttu-id="c37e9-203">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="c37e9-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c37e9-204">b.</span><span class="sxs-lookup"><span data-stu-id="c37e9-204">b.</span></span> <span data-ttu-id="c37e9-205">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="c37e9-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c37e9-206">c.</span><span class="sxs-lookup"><span data-stu-id="c37e9-206">c.</span></span> <span data-ttu-id="c37e9-207">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="c37e9-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c37e9-208">d.</span><span class="sxs-lookup"><span data-stu-id="c37e9-208">d.</span></span> <span data-ttu-id="c37e9-209">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c37e9-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="c37e9-210">建立 8x8 Virtual Office 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c37e9-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="c37e9-211">hello 本節目標在於 toocreate 呼叫許 Simon 8 x 8 虛擬 Office 中的使用者。</span><span class="sxs-lookup"><span data-stu-id="c37e9-211">hello objective of this section is toocreate a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="c37e9-212">8x8 Virtual Office 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="c37e9-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="c37e9-213">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="c37e9-213">There is no action item for you in this section.</span></span> <span data-ttu-id="c37e9-214">會建立新使用者在嘗試 tooaccess 8 x 8 虛擬 Office 如果尚不存在。</span><span class="sxs-lookup"><span data-stu-id="c37e9-214">A new user is created during an attempt tooaccess 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="c37e9-215">若要手動 toocreate 使用者，您需要 toocontact hello [8 x 8 虛擬 Office 支援小組](https://www.8x8.com/about-us/contact-us)。</span><span class="sxs-lookup"><span data-stu-id="c37e9-215">If you need toocreate a user manually, you need toocontact hello [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c37e9-216">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="c37e9-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c37e9-217">在本節中，您可以啟用許 Simon toouse Azure 單一登入授與存取 too8x8 虛擬 Office。</span><span class="sxs-lookup"><span data-stu-id="c37e9-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too8x8 Virtual Office.</span></span>

![指派使用者][200] 

<span data-ttu-id="c37e9-219">**tooassign 許 Simon too8x8 虛擬 Office，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c37e9-219">**tooassign Britta Simon too8x8 Virtual Office, perform hello following steps:**</span></span>

1. <span data-ttu-id="c37e9-220">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c37e9-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c37e9-222">在 [hello] 應用程式清單中，選取**8 x 8 虛擬 Office**。</span><span class="sxs-lookup"><span data-stu-id="c37e9-222">In hello applications list, select **8x8 Virtual Office**.</span></span>

    ![設定單一登入](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="c37e9-224">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="c37e9-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="c37e9-226">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c37e9-226">Click **Add** button.</span></span> <span data-ttu-id="c37e9-227">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c37e9-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="c37e9-229">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="c37e9-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c37e9-230">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c37e9-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c37e9-231">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c37e9-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c37e9-232">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c37e9-232">Testing single sign-on</span></span>

<span data-ttu-id="c37e9-233">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="c37e9-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c37e9-234">當您按一下 hello 8 x 8 虛擬 Office 磚 hello 存取面板中的時，您應該取得自動登入 tooyour 8 x 8 虛擬 Office 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c37e9-234">When you click hello 8x8 Virtual Office tile in hello Access Panel, you should get automatically signed-on tooyour 8x8 Virtual Office application.</span></span>
<span data-ttu-id="c37e9-235">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="c37e9-235">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c37e9-236">其他資源</span><span class="sxs-lookup"><span data-stu-id="c37e9-236">Additional resources</span></span>

* [<span data-ttu-id="c37e9-237">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c37e9-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c37e9-238">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c37e9-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

