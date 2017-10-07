---
title: "教學課程：Azure Active Directory 與 Pacific Timesheet 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與太平洋時程表之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e546e8ba-821a-4942-9545-c84b0670beab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 5fd57ff78a3a64c135f2de9895f4643b39e33bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pacific-timesheet"></a><span data-ttu-id="66284-103">教學課程：Azure Active Directory 與 Pacific Timesheet 整合</span><span class="sxs-lookup"><span data-stu-id="66284-103">Tutorial: Azure Active Directory integration with Pacific Timesheet</span></span>

<span data-ttu-id="66284-104">在此教學課程中，您學會如何 toointegrate 太平洋時程表與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="66284-104">In this tutorial, you learn how toointegrate Pacific Timesheet with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66284-105">與 Azure AD 整合太平洋時程表可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="66284-105">Integrating Pacific Timesheet with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="66284-106">您可以控制存取 tooPacific 時程表的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="66284-106">You can control in Azure AD who has access tooPacific Timesheet</span></span>
- <span data-ttu-id="66284-107">您可以啟用您的使用者 tooautomatically get 登入 tooPacific 時程表 （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="66284-107">You can enable your users tooautomatically get signed-on tooPacific Timesheet (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66284-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="66284-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="66284-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="66284-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66284-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="66284-110">Prerequisites</span></span>

<span data-ttu-id="66284-111">tooconfigure 太平洋時程表與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="66284-111">tooconfigure Azure AD integration with Pacific Timesheet, you need hello following items:</span></span>

- <span data-ttu-id="66284-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="66284-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66284-113">已啟用 Pacific Timesheet 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="66284-113">A Pacific Timesheet single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66284-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="66284-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66284-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="66284-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66284-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="66284-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66284-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="66284-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66284-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="66284-118">Scenario description</span></span>
<span data-ttu-id="66284-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66284-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66284-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="66284-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66284-121">從 hello 圖庫加入太平洋時程表</span><span class="sxs-lookup"><span data-stu-id="66284-121">Adding Pacific Timesheet from hello gallery</span></span>
2. <span data-ttu-id="66284-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="66284-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pacific-timesheet-from-hello-gallery"></a><span data-ttu-id="66284-123">從 hello 圖庫加入太平洋時程表</span><span class="sxs-lookup"><span data-stu-id="66284-123">Adding Pacific Timesheet from hello gallery</span></span>
<span data-ttu-id="66284-124">tooconfigure hello 整合太平洋時程表為 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 太平洋時程表。</span><span class="sxs-lookup"><span data-stu-id="66284-124">tooconfigure hello integration of Pacific Timesheet into Azure AD, you need tooadd Pacific Timesheet from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="66284-125">**tooadd 太平洋時程表從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="66284-125">**tooadd Pacific Timesheet from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="66284-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="66284-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="66284-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="66284-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="66284-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="66284-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="66284-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="66284-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="66284-133">在 [hello] 搜尋方塊中，輸入**太平洋時程表**。</span><span class="sxs-lookup"><span data-stu-id="66284-133">In hello search box, type **Pacific Timesheet**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_search.png)

5. <span data-ttu-id="66284-135">在 hello 結果 窗格中，選取 **太平洋時程表**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66284-135">In hello results panel, select **Pacific Timesheet**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="66284-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="66284-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="66284-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Pacific Timesheet 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66284-138">In this section, you configure and test Azure AD single sign-on with Pacific Timesheet based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="66284-139">單一登入 toowork，Azure AD 需要 tooknow 太平洋時程表中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="66284-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pacific Timesheet is tooa user in Azure AD.</span></span> <span data-ttu-id="66284-140">換句話說，Azure AD 使用者和太平洋時程表中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="66284-140">In other words, a link relationship between an Azure AD user and hello related user in Pacific Timesheet needs toobe established.</span></span>

<span data-ttu-id="66284-141">在太平洋時程表中，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="66284-141">In Pacific Timesheet, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="66284-142">tooconfigure 及測試 Azure AD 單一登入與太平洋時程表，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="66284-142">tooconfigure and test Azure AD single sign-on with Pacific Timesheet, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="66284-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="66284-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="66284-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="66284-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66284-145">**[建立測試使用者太平洋時程表](#creating-a-pacific-timesheet-test-user)** -toohave 許 Simon 太平洋時程表是連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="66284-145">**[Creating a Pacific Timesheet test user](#creating-a-pacific-timesheet-test-user)** - toohave a counterpart of Britta Simon in Pacific Timesheet that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="66284-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66284-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="66284-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="66284-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="66284-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="66284-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="66284-149">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並在太平洋時程表應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="66284-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pacific Timesheet application.</span></span>

<span data-ttu-id="66284-150">**tooconfigure Azure AD 單一登入與太平洋時程表中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="66284-150">**tooconfigure Azure AD single sign-on with Pacific Timesheet, perform hello following steps:**</span></span>

1. <span data-ttu-id="66284-151">在 Azure 入口網站上 hello hello**太平洋時程表**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="66284-151">In hello Azure portal, on hello **Pacific Timesheet** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="66284-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66284-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_samlbase.png)

3. <span data-ttu-id="66284-155">在 hello**太平洋時程表網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="66284-155">On hello **Pacific Timesheet Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_url.png)

    <span data-ttu-id="66284-157">a.</span><span class="sxs-lookup"><span data-stu-id="66284-157">a.</span></span> <span data-ttu-id="66284-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="66284-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    <span data-ttu-id="66284-159">b.</span><span class="sxs-lookup"><span data-stu-id="66284-159">b.</span></span> <span data-ttu-id="66284-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="66284-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="66284-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="66284-161">These values are not real.</span></span> <span data-ttu-id="66284-162">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="66284-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="66284-163">請連絡[太平洋時程表支援小組](http://www.pacifictimesheet.com/support)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="66284-163">Contact [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) tooget these values.</span></span>
 
4. <span data-ttu-id="66284-164">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="66284-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_certificate.png) 

5. <span data-ttu-id="66284-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="66284-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="66284-168">在 hello**太平洋時程表組態**區段中，按一下**設定太平洋時程表**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="66284-168">On hello **Pacific Timesheet Configuration** section, click **Configure Pacific Timesheet** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="66284-169">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="66284-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_configure.png) 

7. <span data-ttu-id="66284-171">tooconfigure 單一登入上**太平洋時程表**端，您需要下載 toosend hello**憑證 (Base64)**， **SAML 單一登入服務 URL**，和**SAML 實體識別碼**太[太平洋時程表支援小組](http://www.pacifictimesheet.com/support)。</span><span class="sxs-lookup"><span data-stu-id="66284-171">tooconfigure single sign-on on **Pacific Timesheet** side, you need toosend hello downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Pacific Timesheet support team](http://www.pacifictimesheet.com/support).</span></span> <span data-ttu-id="66284-172">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="66284-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="66284-173">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="66284-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="66284-174">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="66284-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="66284-175">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66284-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="66284-176">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="66284-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="66284-177">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="66284-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="66284-179">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="66284-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="66284-180">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="66284-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="66284-182">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="66284-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="66284-184">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="66284-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="66284-186">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="66284-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66284-188">a.</span><span class="sxs-lookup"><span data-stu-id="66284-188">a.</span></span> <span data-ttu-id="66284-189">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="66284-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66284-190">b.</span><span class="sxs-lookup"><span data-stu-id="66284-190">b.</span></span> <span data-ttu-id="66284-191">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="66284-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="66284-192">c.</span><span class="sxs-lookup"><span data-stu-id="66284-192">c.</span></span> <span data-ttu-id="66284-193">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="66284-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="66284-194">d.</span><span class="sxs-lookup"><span data-stu-id="66284-194">d.</span></span> <span data-ttu-id="66284-195">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="66284-195">Click **Create**.</span></span>
 
### <a name="creating-a-pacific-timesheet-test-user"></a><span data-ttu-id="66284-196">建立 Pacific Timesheet 測試使用者</span><span class="sxs-lookup"><span data-stu-id="66284-196">Creating a Pacific Timesheet test user</span></span>

<span data-ttu-id="66284-197">在本節中，您要在 Pacific Timesheet 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="66284-197">In this section, you create a user called Britta Simon in Pacific Timesheet.</span></span> <span data-ttu-id="66284-198">使用[太平洋時程表支援小組](http://www.pacifictimesheet.com/support)toocreate hello 應用程式中的使用者。</span><span class="sxs-lookup"><span data-stu-id="66284-198">Work with [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) toocreate a user in hello application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="66284-199">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="66284-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="66284-200">在本節中，您可以授與存取 tooPacific 時程表啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66284-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPacific Timesheet.</span></span>

![指派使用者][200] 

<span data-ttu-id="66284-202">**tooassign 許 Simon tooPacific 時程表中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="66284-202">**tooassign Britta Simon tooPacific Timesheet, perform hello following steps:**</span></span>

1. <span data-ttu-id="66284-203">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="66284-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="66284-205">在 [hello] 應用程式清單中，選取**太平洋時程表**。</span><span class="sxs-lookup"><span data-stu-id="66284-205">In hello applications list, select **Pacific Timesheet**.</span></span>

    ![設定單一登入](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_app.png) 

3. <span data-ttu-id="66284-207">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="66284-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="66284-209">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66284-209">Click **Add** button.</span></span> <span data-ttu-id="66284-210">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="66284-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="66284-212">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="66284-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="66284-213">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66284-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66284-214">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66284-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="66284-215">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="66284-215">Testing single sign-on</span></span>

<span data-ttu-id="66284-216">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="66284-216">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="66284-217">當您按一下 hello 太平洋時程表並排顯示 hello 存取面板中的時，您應該取得自動登入 tooyour 太平洋時程表應用程式。</span><span class="sxs-lookup"><span data-stu-id="66284-217">When you click hello Pacific Timesheet tile in hello Access Panel, you should get automatically signed-on tooyour Pacific Timesheet application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66284-218">其他資源</span><span class="sxs-lookup"><span data-stu-id="66284-218">Additional resources</span></span>

* [<span data-ttu-id="66284-219">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66284-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66284-220">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="66284-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_203.png

