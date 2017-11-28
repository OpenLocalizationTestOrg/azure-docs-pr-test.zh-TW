---
title: "教學課程：Azure Active Directory 與 Front 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與前端之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 4be363a3d338ec9268f3324daab4a80346ec3131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="a18a8-103">教學課程：Azure Active Directory 與 Front 整合</span><span class="sxs-lookup"><span data-stu-id="a18a8-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="a18a8-104">在此教學課程中，您學會如何 toointegrate 與 Azure Active Directory (Azure AD) 的前面。</span><span class="sxs-lookup"><span data-stu-id="a18a8-104">In this tutorial, you learn how toointegrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a18a8-105">與 Azure AD 整合前端可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="a18a8-105">Integrating Front with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a18a8-106">您可以控制存取 tooFront Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a18a8-106">You can control in Azure AD who has access tooFront.</span></span>
- <span data-ttu-id="a18a8-107">您可以啟用您的使用者 tooautomatically get 登入 tooFront （單一登入） 具有其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a18a8-107">You can enable your users tooautomatically get signed-on tooFront (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a18a8-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a18a8-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="a18a8-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a18a8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a18a8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a18a8-110">Prerequisites</span></span>

<span data-ttu-id="a18a8-111">前端 tooconfigure Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="a18a8-111">tooconfigure Azure AD integration with Front, you need hello following items:</span></span>

- <span data-ttu-id="a18a8-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a18a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a18a8-113">已啟用 Front 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a18a8-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a18a8-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="a18a8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a18a8-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a18a8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a18a8-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a18a8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a18a8-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a18a8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a18a8-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a18a8-118">Scenario description</span></span>
<span data-ttu-id="a18a8-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a18a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a18a8-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a18a8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a18a8-121">正在將前端從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="a18a8-121">Adding Front from hello gallery</span></span>
2. <span data-ttu-id="a18a8-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a18a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-hello-gallery"></a><span data-ttu-id="a18a8-123">正在將前端從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="a18a8-123">Adding Front from hello gallery</span></span>
<span data-ttu-id="a18a8-124">tooconfigure hello 整合前端到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 前面。</span><span class="sxs-lookup"><span data-stu-id="a18a8-124">tooconfigure hello integration of Front into Azure AD, you need tooadd Front from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a18a8-125">**tooadd 前端 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a18a8-125">**tooadd Front from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a18a8-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a18a8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="a18a8-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a18a8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a18a8-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a18a8-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="a18a8-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a18a8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="a18a8-133">在 hello 搜尋方塊中，輸入**前端**，選取**前端**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a18a8-133">In hello search box, type **Front**, select **Front** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Hello [結果] 清單中的最上層](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a18a8-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a18a8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a18a8-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Front 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a18a8-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a18a8-137">單一登入 toowork，Azure AD 需要 tooknow hello 對應的使用者在前面是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a18a8-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Front is tooa user in Azure AD.</span></span> <span data-ttu-id="a18a8-138">換句話說，Azure AD 使用者與前面 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="a18a8-138">In other words, a link relationship between an Azure AD user and hello related user in Front needs toobe established.</span></span>

<span data-ttu-id="a18a8-139">在最前面，將指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a18a8-139">In Front, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a18a8-140">tooconfigure 及測試 Azure AD 單一登入前的，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="a18a8-140">tooconfigure and test Azure AD single sign-on with Front, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a18a8-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="a18a8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a18a8-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="a18a8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a18a8-143">**[建立最上層測試使用者](#create-a-front-test-user)** -toohave 對應項目許 Simon 前面所連結的 toohello Azure AD 使用者表示法。</span><span class="sxs-lookup"><span data-stu-id="a18a8-143">**[Create a Front test user](#create-a-front-test-user)** - toohave a counterpart of Britta Simon in Front that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a18a8-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a18a8-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a18a8-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="a18a8-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a18a8-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a18a8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a18a8-147">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並在最上層應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="a18a8-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="a18a8-148">**tooconfigure Azure AD 單一登入前，以執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a18a8-148">**tooconfigure Azure AD single sign-on with Front, perform hello following steps:**</span></span>

1. <span data-ttu-id="a18a8-149">在 Azure 入口網站上 hello hello**前端**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="a18a8-149">In hello Azure portal, on hello **Front** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="a18a8-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a18a8-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="a18a8-153">在 hello**前端網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="a18a8-153">On hello **Front Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="a18a8-155">a.</span><span class="sxs-lookup"><span data-stu-id="a18a8-155">a.</span></span> <span data-ttu-id="a18a8-156">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="a18a8-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="a18a8-157">b.</span><span class="sxs-lookup"><span data-stu-id="a18a8-157">b.</span></span> <span data-ttu-id="a18a8-158">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="a18a8-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="a18a8-159">請檢查**顯示進階的 URL 設定**，如果您想 tooconfigure hello 應用程式中的**SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="a18a8-159">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="a18a8-161">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="a18a8-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a18a8-162">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="a18a8-162">These values are not real.</span></span> <span data-ttu-id="a18a8-163">這些值與 hello 實際識別項、 回覆 URL 和登入 URL 稍後在教學課程中或連絡所說明的更新[前端用戶端支援小組](mailto:support@frontapp.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="a18a8-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) tooget these values.</span></span> 

5. <span data-ttu-id="a18a8-164">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="a18a8-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="a18a8-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a18a8-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a18a8-168">在 hello**前端組態**區段中，按一下**設定前端**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="a18a8-168">On hello **Front Configuration** section, click **Configure Front** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a18a8-169">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="a18a8-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="a18a8-171">以系統管理員身分登入 tooyour 最上層租用戶。</span><span class="sxs-lookup"><span data-stu-id="a18a8-171">Sign-on tooyour Front tenant as an administrator.</span></span>

9. <span data-ttu-id="a18a8-172">跳過**設定 （齒輪圖示在 hello 左提要欄位中的 hello 底部） > 喜好設定**。</span><span class="sxs-lookup"><span data-stu-id="a18a8-172">Go too**Settings (cog icon at hello bottom of hello left sidebar) > Preferences**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="a18a8-174">按一下 [單一登入]  連結。</span><span class="sxs-lookup"><span data-stu-id="a18a8-174">Click **Single Sign On** link.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="a18a8-176">選取**SAML** hello 下拉式清單中**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="a18a8-176">Select **SAML** in hello drop-down list of **Single Sign On**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="a18a8-178">在 hello**進入點**文字方塊放 hello 值**單一登入服務 URL**從 Azure AD 應用程式組態精靈。</span><span class="sxs-lookup"><span data-stu-id="a18a8-178">In hello **Entry Point** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="a18a8-180">開啟您下載**Certificate(Base64)** [記事本]，複製 hello 到剪貼簿，它的內容中，然後將它貼入 toohello **Signing certificate**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a18a8-180">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Signing certificate** textbox.</span></span>
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="a18a8-182">在 hello**服務提供者設定**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a18a8-182">On hello **Service provider settings** section, perform hello following steps:</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="a18a8-184">a.</span><span class="sxs-lookup"><span data-stu-id="a18a8-184">a.</span></span> <span data-ttu-id="a18a8-185">複製 hello 值**實體識別碼**並將它貼到 hello**識別碼** 文字方塊中的**前端網域和 Url** Azure 入口網站中的區段。</span><span class="sxs-lookup"><span data-stu-id="a18a8-185">Copy hello value of **Entity ID** and paste it into hello **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="a18a8-186">b.</span><span class="sxs-lookup"><span data-stu-id="a18a8-186">b.</span></span> <span data-ttu-id="a18a8-187">複製 hello 值**ACS URL**並將它貼到 hello**登入 URL**  文字方塊中的**前端網域和 Url** Azure 入口網站中的區段。</span><span class="sxs-lookup"><span data-stu-id="a18a8-187">Copy hello value of **ACS URL** and paste it into hello **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="a18a8-188">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a18a8-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="a18a8-189">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="a18a8-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a18a8-190">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="a18a8-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a18a8-191">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a18a8-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a18a8-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a18a8-192">Create an Azure AD test user</span></span>

<span data-ttu-id="a18a8-193">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a18a8-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="a18a8-195">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a18a8-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a18a8-196">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a18a8-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a18a8-198">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="a18a8-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a18a8-200">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a18a8-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a18a8-202">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a18a8-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a18a8-204">a.</span><span class="sxs-lookup"><span data-stu-id="a18a8-204">a.</span></span> <span data-ttu-id="a18a8-205">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a18a8-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a18a8-206">b.</span><span class="sxs-lookup"><span data-stu-id="a18a8-206">b.</span></span> <span data-ttu-id="a18a8-207">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="a18a8-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="a18a8-208">c.</span><span class="sxs-lookup"><span data-stu-id="a18a8-208">c.</span></span> <span data-ttu-id="a18a8-209">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="a18a8-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="a18a8-210">d.</span><span class="sxs-lookup"><span data-stu-id="a18a8-210">d.</span></span> <span data-ttu-id="a18a8-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a18a8-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="a18a8-212">建立 Front 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a18a8-212">Create a Front test user</span></span>

<span data-ttu-id="a18a8-213">在本節中，您會於 Front 建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="a18a8-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="a18a8-214">使用[前端用戶端支援小組](mailto:support@frontapp.com)hello 前端平台中新增 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="a18a8-214">Work with [Front Client support team](mailto:support@frontapp.com) to add hello users in hello Front platform.</span></span> <span data-ttu-id="a18a8-215">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="a18a8-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a18a8-216">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a18a8-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a18a8-217">在本節中，您可以授與存取 tooFront 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a18a8-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFront.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="a18a8-219">**tooassign 許 Simon tooFront，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a18a8-219">**tooassign Britta Simon tooFront, perform hello following steps:**</span></span>

1. <span data-ttu-id="a18a8-220">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a18a8-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a18a8-222">在 [hello] 應用程式清單中，選取**前端**。</span><span class="sxs-lookup"><span data-stu-id="a18a8-222">In hello applications list, select **Front**.</span></span>

    ![hello 應用程式清單中的 hello 前方連結](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="a18a8-224">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="a18a8-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="a18a8-226">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a18a8-226">Click **Add** button.</span></span> <span data-ttu-id="a18a8-227">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a18a8-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="a18a8-229">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="a18a8-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a18a8-230">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a18a8-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a18a8-231">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a18a8-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a18a8-232">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a18a8-232">Test single sign-on</span></span>

<span data-ttu-id="a18a8-233">hello 本節目標在於 tootest 您使用 Azure AD SSOconfiguration hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="a18a8-233">hello objective of this section is tootest your Azure AD SSOconfiguration using hello Access Panel.</span></span>

<span data-ttu-id="a18a8-234">當您按一下 hello 前面的圖格 hello 存取面板中時，您應該取得自動登入 tooyour 前端應用程式。</span><span class="sxs-lookup"><span data-stu-id="a18a8-234">When you click hello Front tile in hello Access Panel, you should get automatically signed-on tooyour Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a18a8-235">其他資源</span><span class="sxs-lookup"><span data-stu-id="a18a8-235">Additional resources</span></span>

* [<span data-ttu-id="a18a8-236">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a18a8-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a18a8-237">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a18a8-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

