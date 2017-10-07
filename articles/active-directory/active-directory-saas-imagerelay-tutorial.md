---
title: "教學課程：Azure Active Directory 與 Image Relay 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與映像轉送之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: baf39e4437b85c2de5b524984ad5ca39badbab63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="a1f74-103">教學課程：Azure Active Directory 與 Image Relay 整合</span><span class="sxs-lookup"><span data-stu-id="a1f74-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="a1f74-104">在此教學課程中，您學會如何 toointegrate 與 Azure Active Directory (Azure AD) 的映像轉送。</span><span class="sxs-lookup"><span data-stu-id="a1f74-104">In this tutorial, you learn how toointegrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a1f74-105">整合與 Azure AD 的映像轉送可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="a1f74-105">Integrating Image Relay with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a1f74-106">您可以控制存取 tooImage 轉送的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="a1f74-106">You can control in Azure AD who has access tooImage Relay</span></span>
- <span data-ttu-id="a1f74-107">您可以啟用您的使用者 tooautomatically get 登入 tooImage 轉送 （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="a1f74-107">You can enable your users tooautomatically get signed-on tooImage Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a1f74-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a1f74-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a1f74-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a1f74-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1f74-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a1f74-110">Prerequisites</span></span>

<span data-ttu-id="a1f74-111">tooconfigure 與映像轉送的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="a1f74-111">tooconfigure Azure AD integration with Image Relay, you need hello following items:</span></span>

- <span data-ttu-id="a1f74-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a1f74-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a1f74-113">啟用 Image Relay 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a1f74-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a1f74-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="a1f74-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a1f74-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a1f74-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a1f74-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a1f74-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a1f74-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="a1f74-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a1f74-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a1f74-118">Scenario description</span></span>
<span data-ttu-id="a1f74-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1f74-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a1f74-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a1f74-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a1f74-121">從 hello 組件庫中加入影像轉送</span><span class="sxs-lookup"><span data-stu-id="a1f74-121">Adding Image Relay from hello gallery</span></span>
2. <span data-ttu-id="a1f74-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a1f74-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-hello-gallery"></a><span data-ttu-id="a1f74-123">從 hello 組件庫中加入影像轉送</span><span class="sxs-lookup"><span data-stu-id="a1f74-123">Adding Image Relay from hello gallery</span></span>
<span data-ttu-id="a1f74-124">tooconfigure hello 整合映像轉送到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 映像轉送。</span><span class="sxs-lookup"><span data-stu-id="a1f74-124">tooconfigure hello integration of Image Relay into Azure AD, you need tooadd Image Relay from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a1f74-125">**tooadd hello 圖庫中，從映像轉送執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a1f74-125">**tooadd Image Relay from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1f74-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a1f74-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a1f74-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a1f74-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a1f74-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a1f74-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="a1f74-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1f74-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="a1f74-133">在 [hello] 搜尋方塊中，輸入**映像轉送**。</span><span class="sxs-lookup"><span data-stu-id="a1f74-133">In hello search box, type **Image Relay**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="a1f74-135">在 hello 結果 窗格中，選取 **映像轉送**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a1f74-135">In hello results panel, select **Image Relay**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a1f74-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a1f74-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a1f74-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Image Relay 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1f74-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a1f74-139">單一登入 toowork，Azure AD 需要 tooknow 哪些 hello 對應項目中的使用者映像轉送都 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a1f74-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Image Relay is tooa user in Azure AD.</span></span> <span data-ttu-id="a1f74-140">換句話說，Azure AD 使用者與 hello 映像轉接中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="a1f74-140">In other words, a link relationship between an Azure AD user and hello related user in Image Relay needs toobe established.</span></span>

<span data-ttu-id="a1f74-141">映像轉接中指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a1f74-141">In Image Relay, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a1f74-142">tooconfigure 及測試 Azure AD 單一登入與映像轉送，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="a1f74-142">tooconfigure and test Azure AD single sign-on with Image Relay, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a1f74-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="a1f74-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a1f74-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="a1f74-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a1f74-145">**[建立映像轉送測試使用者](#creating-an-image-relay-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的映像轉接中對應項目。</span><span class="sxs-lookup"><span data-stu-id="a1f74-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - toohave a counterpart of Britta Simon in Image Relay that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a1f74-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1f74-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a1f74-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="a1f74-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a1f74-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a1f74-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a1f74-149">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入映像轉送應用程式中。</span><span class="sxs-lookup"><span data-stu-id="a1f74-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="a1f74-150">**tooconfigure Azure AD 單一登入與映像轉送執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a1f74-150">**tooconfigure Azure AD single sign-on with Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1f74-151">在 Azure 入口網站上 hello hello**映像轉送**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="a1f74-151">In hello Azure portal, on hello **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="a1f74-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1f74-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="a1f74-155">在 hello**映像轉送的網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a1f74-155">On hello **Image Relay Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="a1f74-157">a.</span><span class="sxs-lookup"><span data-stu-id="a1f74-157">a.</span></span> <span data-ttu-id="a1f74-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="a1f74-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="a1f74-159">b.</span><span class="sxs-lookup"><span data-stu-id="a1f74-159">b.</span></span> <span data-ttu-id="a1f74-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="a1f74-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a1f74-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="a1f74-161">These values are not real.</span></span> <span data-ttu-id="a1f74-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="a1f74-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a1f74-163">請連絡[映像轉接用戶端支援小組](http://support.imagerelay.com/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="a1f74-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="a1f74-164">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="a1f74-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="a1f74-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1f74-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a1f74-168">在 hello**映像轉送設定**區段中，按一下**設定映像轉送**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="a1f74-168">On hello **Image Relay Configuration** section, click **Configure Image Relay** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a1f74-169">複製 hello**登出服務 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="a1f74-169">Copy hello **Sign-Out Service URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="a1f74-171">在另一個瀏覽器視窗中，以系統管理員身分登入 tooyour 映像轉送公司網站。</span><span class="sxs-lookup"><span data-stu-id="a1f74-171">In another browser window, sign in tooyour Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="a1f74-172">在 hello 最上層顯示 hello 工具列上，按一下 hello**使用者與權限**工作負載。</span><span class="sxs-lookup"><span data-stu-id="a1f74-172">In hello toolbar on hello top, click hello **Users & Permissions** workload.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="a1f74-174">按一下 [建立新的權限] 。</span><span class="sxs-lookup"><span data-stu-id="a1f74-174">Click **Create New Permission**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="a1f74-176">在 hello**單一登入設定**工作負載、 選取 hello**這個群組可以只登入透過單一登入**核取方塊，然後**儲存**。</span><span class="sxs-lookup"><span data-stu-id="a1f74-176">In hello **Single Sign On Settings** workload, select hello **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="a1f74-178">跳過**帳戶設定**。</span><span class="sxs-lookup"><span data-stu-id="a1f74-178">Go too**Account Settings**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="a1f74-180">移 toohello**單一登入設定**工作負載。</span><span class="sxs-lookup"><span data-stu-id="a1f74-180">Go toohello **Single Sign On Settings** workload.</span></span>
    
     ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="a1f74-182">在 [hello **SAML 設定**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a1f74-182">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="a1f74-184">a.</span><span class="sxs-lookup"><span data-stu-id="a1f74-184">a.</span></span> <span data-ttu-id="a1f74-185">在**登入 URL**文字方塊中，貼上 hello 值**單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="a1f74-185">In **Login URL** textbox, paste hello value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a1f74-186">b.</span><span class="sxs-lookup"><span data-stu-id="a1f74-186">b.</span></span> <span data-ttu-id="a1f74-187">在**登出 URL**文字方塊中，貼上 hello 值**單一登出服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="a1f74-187">In **Logout URL**  textbox, paste hello value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a1f74-188">c.</span><span class="sxs-lookup"><span data-stu-id="a1f74-188">c.</span></span> <span data-ttu-id="a1f74-189">選取 **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress** 做為 [名稱識別碼格式]。</span><span class="sxs-lookup"><span data-stu-id="a1f74-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="a1f74-190">d.</span><span class="sxs-lookup"><span data-stu-id="a1f74-190">d.</span></span> <span data-ttu-id="a1f74-191">做為**hello 服務提供者 （映像轉送） 的要求繫結選項**，選取**POST 繫結**。</span><span class="sxs-lookup"><span data-stu-id="a1f74-191">As **Binding Options for Requests from hello Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="a1f74-192">e.</span><span class="sxs-lookup"><span data-stu-id="a1f74-192">e.</span></span> <span data-ttu-id="a1f74-193">在 [x.509 憑證] 下方，按一下 [更新憑證]。</span><span class="sxs-lookup"><span data-stu-id="a1f74-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="a1f74-195">f.</span><span class="sxs-lookup"><span data-stu-id="a1f74-195">f.</span></span> <span data-ttu-id="a1f74-196">在記事本中開啟下載的 hello 憑證、 hello 內容複製並貼到 hello x.509 憑證 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a1f74-196">Open hello downloaded certificate in notepad, copy hello content, and then paste it into hello x.509 Certificate textbox.</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="a1f74-198">g.</span><span class="sxs-lookup"><span data-stu-id="a1f74-198">g.</span></span> <span data-ttu-id="a1f74-199">在**Just-In-Time 使用者佈建**區段中，選取 hello**啟用 Just-In-Time 使用者佈建**。</span><span class="sxs-lookup"><span data-stu-id="a1f74-199">In **Just-In-Time User Provisioning** section, select hello **Enable Just-In-Time User Provisioning**.</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="a1f74-201">h.</span><span class="sxs-lookup"><span data-stu-id="a1f74-201">h.</span></span> <span data-ttu-id="a1f74-202">選取 hello 權限群組 (例如， **SSO 基本**) 這允許 toosign 中的只能透過單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1f74-202">Select hello permission group (for example, **SSO Basic**) which is allowed toosign in only through single sign-on.</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="a1f74-204">i.</span><span class="sxs-lookup"><span data-stu-id="a1f74-204">i.</span></span> <span data-ttu-id="a1f74-205">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="a1f74-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a1f74-206">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="a1f74-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a1f74-207">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="a1f74-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a1f74-208">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a1f74-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a1f74-209">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a1f74-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="a1f74-210">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a1f74-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="a1f74-212">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a1f74-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1f74-213">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a1f74-213">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a1f74-215">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="a1f74-215">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a1f74-217">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="a1f74-217">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a1f74-219">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a1f74-219">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a1f74-221">a.</span><span class="sxs-lookup"><span data-stu-id="a1f74-221">a.</span></span> <span data-ttu-id="a1f74-222">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a1f74-222">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a1f74-223">b.</span><span class="sxs-lookup"><span data-stu-id="a1f74-223">b.</span></span> <span data-ttu-id="a1f74-224">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="a1f74-224">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a1f74-225">c.</span><span class="sxs-lookup"><span data-stu-id="a1f74-225">c.</span></span> <span data-ttu-id="a1f74-226">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="a1f74-226">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a1f74-227">d.</span><span class="sxs-lookup"><span data-stu-id="a1f74-227">d.</span></span> <span data-ttu-id="a1f74-228">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a1f74-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="a1f74-229">建立 Image Relay 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a1f74-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="a1f74-230">hello 本節目標在於 toocreate 呼叫許 Simon 轉接映像中的使用者。</span><span class="sxs-lookup"><span data-stu-id="a1f74-230">hello objective of this section is toocreate a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="a1f74-231">**toocreate 呼叫許 Simon 映像轉送中的使用者執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a1f74-231">**toocreate a user called Britta Simon in Image Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1f74-232">以系統管理員身分登入 tooyour 映像轉送公司網站。</span><span class="sxs-lookup"><span data-stu-id="a1f74-232">Sign-on tooyour Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="a1f74-233">跳過**使用者與權限**選取**建立 SSO 使用者**。</span><span class="sxs-lookup"><span data-stu-id="a1f74-233">Go too**Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="a1f74-235">輸入 hello**電子郵件**，**名字**，**姓氏**，和**公司**的 hello 使用者想 tooprovision 和選取 hello 權限群組（例如，SSO 基本） 即 hello 群組只能透過單一登入可以登入。</span><span class="sxs-lookup"><span data-stu-id="a1f74-235">Enter hello **Email**, **First Name**, **Last Name**, and **Company** of hello user you want tooprovision and select hello permission group (for example, SSO Basic) which is hello group that can sign in only through single sign-on.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="a1f74-237">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a1f74-237">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a1f74-238">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="a1f74-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a1f74-239">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooImage 轉送。</span><span class="sxs-lookup"><span data-stu-id="a1f74-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooImage Relay.</span></span>

![指派使用者][200] 

<span data-ttu-id="a1f74-241">**tooassign 許 Simon tooImage 轉送，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a1f74-241">**tooassign Britta Simon tooImage Relay, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1f74-242">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a1f74-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a1f74-244">在 [hello] 應用程式清單中，選取**映像轉送**。</span><span class="sxs-lookup"><span data-stu-id="a1f74-244">In hello applications list, select **Image Relay**.</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="a1f74-246">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="a1f74-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="a1f74-248">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1f74-248">Click **Add** button.</span></span> <span data-ttu-id="a1f74-249">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a1f74-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="a1f74-251">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="a1f74-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a1f74-252">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1f74-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a1f74-253">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1f74-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a1f74-254">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a1f74-254">Testing single sign-on</span></span>

<span data-ttu-id="a1f74-255">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="a1f74-255">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>    

<span data-ttu-id="a1f74-256">當您按一下 hello 映像轉送磚 hello 存取面板中的時，您應該取得自動登入 tooyour 映像轉送應用程式。</span><span class="sxs-lookup"><span data-stu-id="a1f74-256">When you click hello Image Relay tile in hello Access Panel, you should get automatically signed-on tooyour Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a1f74-257">其他資源</span><span class="sxs-lookup"><span data-stu-id="a1f74-257">Additional resources</span></span>

* [<span data-ttu-id="a1f74-258">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1f74-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a1f74-259">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a1f74-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

