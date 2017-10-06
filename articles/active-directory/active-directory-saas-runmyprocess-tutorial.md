---
title: "教學課程：Azure Active Directory 與 RunMyProcess 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 RunMyProcess 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f02acda015aeb8d131d8e3ef88bf50c4e8e94750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="91f85-103">教學課程：Azure Active Directory 與 RunMyProcess 整合</span><span class="sxs-lookup"><span data-stu-id="91f85-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="91f85-104">在此教學課程中，您學會如何 toointegrate RunMyProcess 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="91f85-104">In this tutorial, you learn how toointegrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91f85-105">與 Azure AD 整合 RunMyProcess 可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="91f85-105">Integrating RunMyProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="91f85-106">您可以控制存取 tooRunMyProcess Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="91f85-106">You can control in Azure AD who has access tooRunMyProcess</span></span>
- <span data-ttu-id="91f85-107">您可以啟用您的使用者 tooautomatically get 登入 tooRunMyProcess （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="91f85-107">You can enable your users tooautomatically get signed-on tooRunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="91f85-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="91f85-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="91f85-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="91f85-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91f85-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="91f85-110">Prerequisites</span></span>

<span data-ttu-id="91f85-111">tooconfigure 與 RunMyProcess 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="91f85-111">tooconfigure Azure AD integration with RunMyProcess, you need hello following items:</span></span>

- <span data-ttu-id="91f85-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="91f85-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91f85-113">啟用 RunMyProcess 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="91f85-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91f85-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="91f85-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91f85-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="91f85-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91f85-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="91f85-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91f85-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="91f85-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91f85-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="91f85-118">Scenario description</span></span>
<span data-ttu-id="91f85-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91f85-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91f85-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="91f85-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91f85-121">從 hello 圖庫加入 RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="91f85-121">Adding RunMyProcess from hello gallery</span></span>
2. <span data-ttu-id="91f85-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="91f85-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-hello-gallery"></a><span data-ttu-id="91f85-123">從 hello 圖庫加入 RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="91f85-123">Adding RunMyProcess from hello gallery</span></span>
<span data-ttu-id="91f85-124">tooconfigure hello 整合 RunMyProcess 的 Azure AD，您需要 tooadd RunMyProcess hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="91f85-124">tooconfigure hello integration of RunMyProcess into Azure AD, you need tooadd RunMyProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="91f85-125">**tooadd RunMyProcess 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="91f85-125">**tooadd RunMyProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="91f85-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="91f85-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="91f85-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="91f85-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="91f85-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="91f85-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="91f85-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="91f85-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="91f85-133">在 [hello] 搜尋方塊中，輸入**RunMyProcess**。</span><span class="sxs-lookup"><span data-stu-id="91f85-133">In hello search box, type **RunMyProcess**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="91f85-135">在 [hello [結果] 窗格中，選取 [ **RunMyProcess**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="91f85-135">In hello results panel, select **RunMyProcess**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="91f85-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="91f85-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="91f85-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 RunMyProcess 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91f85-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="91f85-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 RunMyProcess 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="91f85-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RunMyProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="91f85-140">換句話說，Azure AD 使用者與 hello RunMyProcess 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="91f85-140">In other words, a link relationship between an Azure AD user and hello related user in RunMyProcess needs toobe established.</span></span>

<span data-ttu-id="91f85-141">在 RunMyProcess 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="91f85-141">In RunMyProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="91f85-142">tooconfigure 及測試 Azure AD 單一登入 RunMyProcess，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="91f85-142">tooconfigure and test Azure AD single sign-on with RunMyProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="91f85-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="91f85-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="91f85-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="91f85-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="91f85-145">**[建立測試使用者 RunMyProcess](#creating-a-runmyprocess-test-user) ** -toohave 許 Simon RunMyProcess 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="91f85-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - toohave a counterpart of Britta Simon in RunMyProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="91f85-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91f85-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="91f85-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="91f85-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="91f85-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="91f85-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="91f85-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 RunMyProcess 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="91f85-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="91f85-150">**tooconfigure Azure AD 單一登入 RunMyProcess，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="91f85-150">**tooconfigure Azure AD single sign-on with RunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="91f85-151">在 Azure 入口網站上 hello hello **RunMyProcess**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="91f85-151">In hello Azure portal, on hello **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="91f85-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91f85-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="91f85-155">在 [hello **RunMyProcess 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="91f85-155">On hello **RunMyProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="91f85-157">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="91f85-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="91f85-158">hello 值不是真正的。</span><span class="sxs-lookup"><span data-stu-id="91f85-158">hello value is not real.</span></span> <span data-ttu-id="91f85-159">更新 hello 值與 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="91f85-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="91f85-160">請連絡[RunMyProcess 用戶端支援小組](mailto:support@runmyprocess.com)tooget hello 值。</span><span class="sxs-lookup"><span data-stu-id="91f85-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) tooget hello value.</span></span> 

4. <span data-ttu-id="91f85-161">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="91f85-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="91f85-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="91f85-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="91f85-165">在 [hello **RunMyProcess 組態**區段中，按一下**設定 RunMyProcess** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="91f85-165">On hello **RunMyProcess Configuration** section, click **Configure RunMyProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="91f85-166">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="91f85-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="91f85-168">在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour RunMyProcess 租用戶。</span><span class="sxs-lookup"><span data-stu-id="91f85-168">In a different web browser window, sign-on tooyour RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="91f85-169">在左方瀏覽面板中，按一下 [帳戶]，然後選取 [組態]。</span><span class="sxs-lookup"><span data-stu-id="91f85-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="91f85-171">跳過**驗證方法**區段，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="91f85-171">Go too**Authentication method** section and perform below steps:</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="91f85-173">a.</span><span class="sxs-lookup"><span data-stu-id="91f85-173">a.</span></span> <span data-ttu-id="91f85-174">在 [方法]，選取 [使用 Samlv2 進行 SSO]。</span><span class="sxs-lookup"><span data-stu-id="91f85-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="91f85-175">b.</span><span class="sxs-lookup"><span data-stu-id="91f85-175">b.</span></span> <span data-ttu-id="91f85-176">在 [hello **SSO 重新導向**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="91f85-176">In hello **SSO redirect** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="91f85-177">c.</span><span class="sxs-lookup"><span data-stu-id="91f85-177">c.</span></span> <span data-ttu-id="91f85-178">在 [hello**登出重新導向**文字方塊中，貼上 hello 值**登出 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="91f85-178">In hello **Logout redirect** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="91f85-179">d.</span><span class="sxs-lookup"><span data-stu-id="91f85-179">d.</span></span> <span data-ttu-id="91f85-180">在 [hello**名稱識別碼格式**文字方塊中，類型 hello 值**名稱識別碼格式**為**urn: oasis： 名稱： tc: saml: 1.1 nameid-format-: emailAddress**。</span><span class="sxs-lookup"><span data-stu-id="91f85-180">In hello **Name Id Format** textbox, type hello value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="91f85-181">e.</span><span class="sxs-lookup"><span data-stu-id="91f85-181">e.</span></span> <span data-ttu-id="91f85-182">Hello 的 hello 下載的憑證檔案的內容複製並貼到 hello**憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="91f85-182">Copy hello content of hello downloaded certificate file and then paste it into hello **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="91f85-183">f.</span><span class="sxs-lookup"><span data-stu-id="91f85-183">f.</span></span> <span data-ttu-id="91f85-184">按一下 [儲存]  圖示。</span><span class="sxs-lookup"><span data-stu-id="91f85-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="91f85-185">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="91f85-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="91f85-186">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="91f85-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="91f85-187">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="91f85-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="91f85-188">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="91f85-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="91f85-189">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="91f85-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="91f85-191">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="91f85-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="91f85-192">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="91f85-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="91f85-194">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="91f85-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="91f85-196">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="91f85-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="91f85-198">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="91f85-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="91f85-200">a.</span><span class="sxs-lookup"><span data-stu-id="91f85-200">a.</span></span> <span data-ttu-id="91f85-201">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="91f85-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91f85-202">b.</span><span class="sxs-lookup"><span data-stu-id="91f85-202">b.</span></span> <span data-ttu-id="91f85-203">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="91f85-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="91f85-204">c.</span><span class="sxs-lookup"><span data-stu-id="91f85-204">c.</span></span> <span data-ttu-id="91f85-205">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="91f85-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="91f85-206">d.</span><span class="sxs-lookup"><span data-stu-id="91f85-206">d.</span></span> <span data-ttu-id="91f85-207">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="91f85-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="91f85-208">建立 RunMyProcess 測試使用者</span><span class="sxs-lookup"><span data-stu-id="91f85-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="91f85-209">在訂單 tooenable Azure AD 使用者 toolog tooRunMyProcess 中，您必須是佈建到 RunMyProcess。</span><span class="sxs-lookup"><span data-stu-id="91f85-209">In order tooenable Azure AD users toolog in tooRunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="91f85-210">在 RunMyProcess 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="91f85-210">In hello case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="91f85-211">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="91f85-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="91f85-212">登入 tooyour RunMyProcess 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="91f85-212">Log in tooyour RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="91f85-213">按一下 [帳戶] 並選取 [使用者]，然後按一下 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="91f85-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="91f85-214">![新增使用者](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="91f85-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="91f85-215">在 [hello**使用者設定**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="91f85-215">In hello **User Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="91f85-216">![設定檔](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "設定檔")</span><span class="sxs-lookup"><span data-stu-id="91f85-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="91f85-217">a.</span><span class="sxs-lookup"><span data-stu-id="91f85-217">a.</span></span> <span data-ttu-id="91f85-218">型別 hello**名稱**和**電子郵件**的有效 azure AD 帳戶想成 hello tooprovision 相關的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="91f85-218">Type hello **Name** and **E-mail** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="91f85-219">b.</span><span class="sxs-lookup"><span data-stu-id="91f85-219">b.</span></span> <span data-ttu-id="91f85-220">選取 [IDE 語言]、[語言] 和 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="91f85-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="91f85-221">c.</span><span class="sxs-lookup"><span data-stu-id="91f85-221">c.</span></span> <span data-ttu-id="91f85-222">選取**傳送帳戶建立電子郵件 toome**。</span><span class="sxs-lookup"><span data-stu-id="91f85-222">Select **Send account creation e-mail toome**.</span></span> 

    <span data-ttu-id="91f85-223">d.</span><span class="sxs-lookup"><span data-stu-id="91f85-223">d.</span></span> <span data-ttu-id="91f85-224">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="91f85-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="91f85-225">您可以使用任何其他 RunMyProcess 使用者帳戶建立工具或 Api 提供 RunMyProcess tooprovision Azure Active Directory 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="91f85-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess tooprovision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="91f85-226">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="91f85-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="91f85-227">在本節中，您可以授與存取 tooRunMyProcess 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91f85-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRunMyProcess.</span></span>

![指派使用者][200] 

<span data-ttu-id="91f85-229">**tooassign 許 Simon tooRunMyProcess，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="91f85-229">**tooassign Britta Simon tooRunMyProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="91f85-230">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="91f85-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="91f85-232">在 [hello] 應用程式清單中，選取**RunMyProcess**。</span><span class="sxs-lookup"><span data-stu-id="91f85-232">In hello applications list, select **RunMyProcess**.</span></span>

    ![設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="91f85-234">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="91f85-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="91f85-236">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="91f85-236">Click **Add** button.</span></span> <span data-ttu-id="91f85-237">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="91f85-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="91f85-239">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="91f85-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="91f85-240">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="91f85-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="91f85-241">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="91f85-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="91f85-242">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="91f85-242">Testing single sign-on</span></span>

<span data-ttu-id="91f85-243">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="91f85-243">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="91f85-244">當您按一下的 hello RunMyProcess 磚 hello 存取面板中時，您應該取得自動登入 tooyour RunMyProcess 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="91f85-244">When you click hello RunMyProcess tile in hello Access Panel, you should get automatically signed-on tooyour RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="91f85-245">其他資源</span><span class="sxs-lookup"><span data-stu-id="91f85-245">Additional resources</span></span>

* [<span data-ttu-id="91f85-246">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91f85-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91f85-247">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="91f85-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

