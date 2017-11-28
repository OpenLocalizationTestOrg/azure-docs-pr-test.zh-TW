---
title: "教學課程：Azure Active Directory 與 RFPIO 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 RFPIO 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="d6009-103">教學課程：Azure Active Directory 與 RFPIO 整合</span><span class="sxs-lookup"><span data-stu-id="d6009-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="d6009-104">在此教學課程中，您學會如何 toointegrate RFPIO 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d6009-104">In this tutorial, you learn how toointegrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d6009-105">與 Azure AD 整合 RFPIO 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="d6009-105">Integrating RFPIO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d6009-106">您可以控制誰能夠存取 tooRFPIO Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="d6009-106">You can control who in Azure AD who has access tooRFPIO.</span></span>
- <span data-ttu-id="d6009-107">您可以啟用您的使用者 tooautomatically get 登入 tooRFPIO （單一登入） 具有其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6009-107">You can enable your users tooautomatically get signed-on tooRFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d6009-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d6009-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="d6009-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d6009-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6009-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d6009-110">Prerequisites</span></span>

<span data-ttu-id="d6009-111">tooconfigure RFPIO 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="d6009-111">tooconfigure Azure AD integration with RFPIO, you need hello following items:</span></span>

- <span data-ttu-id="d6009-112">Azure AD 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6009-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="d6009-113">已啟用 RFPIO 單一登入的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d6009-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="d6009-114">我們不建議您在本教學課程使用實際執行環境 tootest hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="d6009-114">We don't recommend that you use a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="d6009-115">tootest hello 步驟在本教學課程，請遵循下列建議：</span><span class="sxs-lookup"><span data-stu-id="d6009-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="d6009-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d6009-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="d6009-117">如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="d6009-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d6009-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="d6009-118">Scenario description</span></span>
<span data-ttu-id="d6009-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d6009-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d6009-120">此教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="d6009-120">hello scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6009-121">加入 RFPIO 從 hello 組件庫。</span><span class="sxs-lookup"><span data-stu-id="d6009-121">Adding RFPIO from hello gallery.</span></span>
2. <span data-ttu-id="d6009-122">設定並測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d6009-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-hello-gallery"></a><span data-ttu-id="d6009-123">從 hello 圖庫新增 RFPIO</span><span class="sxs-lookup"><span data-stu-id="d6009-123">Add RFPIO from hello gallery</span></span>
<span data-ttu-id="d6009-124">tooconfigure hello 整合 RFPIO 到 Azure AD，您需要 tooadd RFPIO hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6009-124">tooconfigure hello integration of RFPIO into Azure AD, you need tooadd RFPIO from hello gallery tooyour list of managed SaaS apps.</span></span>

### <a name="tooadd-rfpio-from-hello-gallery"></a><span data-ttu-id="d6009-125">tooadd RFPIO 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="d6009-125">tooadd RFPIO from hello gallery</span></span>

1. <span data-ttu-id="d6009-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，在 hello 左側的導覽窗格中，選取 hello **Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="d6009-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d6009-128">選取 [企業應用程式]，然後選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d6009-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="d6009-130">tooadd 新的應用程式中，選取 hello**新的應用程式**上 hello 對話方塊頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="d6009-130">tooadd a new application, select hello **New application** button on hello top of dialog box.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="d6009-132">在 [hello] 搜尋方塊中，輸入**RFPIO**。</span><span class="sxs-lookup"><span data-stu-id="d6009-132">In hello search box, type **RFPIO**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="d6009-134">在 hello 結果 窗格中，選取  **RFPIO**，然後選取 hello**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6009-134">In hello results panel, select **RFPIO**, and then select hello **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d6009-136">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d6009-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d6009-137">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 RFPIO 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d6009-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d6009-138">單一登入 toowork，Azure AD 需要 tooknow RFPIO 中的對等項目的使用者與 Azure AD 中的使用者之間是什麼 hello 關聯性。</span><span class="sxs-lookup"><span data-stu-id="d6009-138">For single sign-on toowork, Azure AD needs tooknow what hello relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="d6009-139">換句話說，Azure AD 使用者與 hello RFPIO 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="d6009-139">In other words, a link relationship between an Azure AD user and hello related user in RFPIO needs toobe established.</span></span>

<span data-ttu-id="d6009-140">RFPIO 中, 指派的 hello 值**使用者名**做為 hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d6009-140">In RFPIO, assign hello value of **user name** in Azure AD as hello value of  **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d6009-141">tooconfigure 及 RFPIO 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="d6009-141">tooconfigure and test Azure AD single sign-on with RFPIO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d6009-142">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)**-tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="d6009-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d6009-143">**[建立 Azure AD 的測試使用者](#creating-an-azure-ad-test-user)**-許 Simon 與 Azure AD 單一登入 tootest。</span><span class="sxs-lookup"><span data-stu-id="d6009-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6009-144">**[建立測試使用者 RFPIO](#creating-a-rfpio-test-user)**  -toohave 許 Simon RFPIO 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="d6009-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --toohave a counterpart of Britta Simon in RFPIO that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d6009-145">**[指派給 Azure AD hello 測試使用者](#assigning-the-azure-ad-test-user)**-tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d6009-145">**[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6009-146">**[測試單一登入](#testing-single-sign-on)** -tooverify 如果 hello 設定可正常運作。</span><span class="sxs-lookup"><span data-stu-id="d6009-146">**[Test Single Sign-On](#testing-single-sign-on)** --tooverify if hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d6009-147">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d6009-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d6009-148">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 RFPIO 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d6009-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="d6009-149">**tooconfigure Azure AD 單一登入與 RFPIO，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d6009-149">**tooconfigure Azure AD single sign-on with RFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6009-150">在 Azure 入口網站上 hello hello **RFPIO**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="d6009-150">In hello Azure portal, on hello **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="d6009-152">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d6009-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="d6009-154">在 hello **RFPIO 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="d6009-154">On hello **RFPIO Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="d6009-156">a.</span><span class="sxs-lookup"><span data-stu-id="d6009-156">a.</span></span> <span data-ttu-id="d6009-157">在 hello**識別碼**文字方塊中，型別 hello URL:`https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="d6009-157">In hello **Identifier** textbox, type hello URL: `https://www.rfpio.com`</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="d6009-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6009-159">b.</span></span> <span data-ttu-id="d6009-160">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="d6009-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="d6009-161">c.</span><span class="sxs-lookup"><span data-stu-id="d6009-161">c.</span></span> <span data-ttu-id="d6009-162">在 hello**轉送狀態**文字方塊中輸入的字串值。</span><span class="sxs-lookup"><span data-stu-id="d6009-162">In hello **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="d6009-163">請連絡[RFPIO 支援小組](https://www.rfpio.com/contact/)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="d6009-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) tooget this value.</span></span> 

4. <span data-ttu-id="d6009-164">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="d6009-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="d6009-165">如果您想 tooconfigure hello 應用程式中的**SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="d6009-165">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>   

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="d6009-167">在 hello**登入 URL**文字方塊中，型別 hello URL:`https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="d6009-167">In hello **Sign on URL** textbox, type hello URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="d6009-168">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="d6009-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="d6009-170">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d6009-170">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d6009-172">在不同的網頁瀏覽器視窗中，登入 toohello **RFPIO**身為系統管理員的網站。</span><span class="sxs-lookup"><span data-stu-id="d6009-172">In a different web browser window, login toohello **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="d6009-173">按一下 hello 底部左上的角的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="d6009-173">Click on hello bottom left corner dropdown.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="d6009-175">按一下 hello**組織設定**。</span><span class="sxs-lookup"><span data-stu-id="d6009-175">Click on hello **Organization Settings**.</span></span> 

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="d6009-177">按一下 hello**功能和整合**。</span><span class="sxs-lookup"><span data-stu-id="d6009-177">Click on hello **FEATURES & INTEGRATION**.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="d6009-179">在 hello **SAML SSO 設定**按一下**編輯**。</span><span class="sxs-lookup"><span data-stu-id="d6009-179">In hello **SAML SSO Configuration** Click **Edit**.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="d6009-181">在本節中執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d6009-181">In this Section perform following actions:</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="d6009-183">a.</span><span class="sxs-lookup"><span data-stu-id="d6009-183">a.</span></span> <span data-ttu-id="d6009-184">複製的 hello hello 內容**下載中繼資料 XML**並將它貼到 hello**身分識別組態**欄位。</span><span class="sxs-lookup"><span data-stu-id="d6009-184">Copy hello content of hello **Downloaded Metadata XML** and paste it into hello **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="d6009-185">toocopy hello 內容的下載**中繼資料 XML**使用**記事本 + +**或適當**XML 編輯器**。</span><span class="sxs-lookup"><span data-stu-id="d6009-185">toocopy hello content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="d6009-186">b.</span><span class="sxs-lookup"><span data-stu-id="d6009-186">b.</span></span> <span data-ttu-id="d6009-187">按一下 [驗證] 。</span><span class="sxs-lookup"><span data-stu-id="d6009-187">Click **Validate**.</span></span>

    <span data-ttu-id="d6009-188">c.</span><span class="sxs-lookup"><span data-stu-id="d6009-188">c.</span></span> <span data-ttu-id="d6009-189">按一下之後**驗證**、 翻轉**SAML(Enabled)** tooon。</span><span class="sxs-lookup"><span data-stu-id="d6009-189">After Clicking **Validate**, Flip **SAML(Enabled)** tooon.</span></span>

    <span data-ttu-id="d6009-190">d.</span><span class="sxs-lookup"><span data-stu-id="d6009-190">d.</span></span> <span data-ttu-id="d6009-191">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="d6009-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="d6009-192">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="d6009-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d6009-193">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="d6009-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d6009-194">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d6009-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d6009-195">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d6009-195">Create an Azure AD test user</span></span>
<span data-ttu-id="d6009-196">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d6009-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="d6009-198">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d6009-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6009-199">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="d6009-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d6009-201">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="d6009-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d6009-203">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="d6009-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d6009-205">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d6009-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d6009-207">a.</span><span class="sxs-lookup"><span data-stu-id="d6009-207">a.</span></span> <span data-ttu-id="d6009-208">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d6009-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d6009-209">b.</span><span class="sxs-lookup"><span data-stu-id="d6009-209">b.</span></span> <span data-ttu-id="d6009-210">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="d6009-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d6009-211">c.</span><span class="sxs-lookup"><span data-stu-id="d6009-211">c.</span></span> <span data-ttu-id="d6009-212">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="d6009-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d6009-213">d.</span><span class="sxs-lookup"><span data-stu-id="d6009-213">d.</span></span> <span data-ttu-id="d6009-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d6009-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="d6009-215">建立 RFPIO 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d6009-215">Create a RFPIO test user</span></span>

<span data-ttu-id="d6009-216">tooenable Azure AD 使用者 toolog 中 tooRFPIO，它們必須佈建到 RFPIO。</span><span class="sxs-lookup"><span data-stu-id="d6009-216">tooenable Azure AD users toolog in tooRFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="d6009-217">中的 RFPIO hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="d6009-217">In hello case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="d6009-218">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d6009-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6009-219">登入 tooyour RFPIO 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="d6009-219">Log in tooyour RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="d6009-220">按一下 hello 底部左上的角的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="d6009-220">Click on hello bottom left corner dropdown.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="d6009-222">按一下 hello**組織設定**。</span><span class="sxs-lookup"><span data-stu-id="d6009-222">Click on hello **Organization Settings**.</span></span> 

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="d6009-224">按一下 [小組成員]。</span><span class="sxs-lookup"><span data-stu-id="d6009-224">Click **TEAM MEMBERS**.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="d6009-226">按一下 [新增成員]。</span><span class="sxs-lookup"><span data-stu-id="d6009-226">Click on **ADD MEMBERS**.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="d6009-228">在 hello**加入新成員**> 一節。</span><span class="sxs-lookup"><span data-stu-id="d6009-228">In hello **Add New Members** section.</span></span> <span data-ttu-id="d6009-229">執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d6009-229">Perform following actions:</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="d6009-231">a.</span><span class="sxs-lookup"><span data-stu-id="d6009-231">a.</span></span> <span data-ttu-id="d6009-232">Enter**電子郵件地址**在 hello**輸入每行一個電子郵件**欄位。</span><span class="sxs-lookup"><span data-stu-id="d6009-232">Enter **Email address** in hello **Enter one email per line** field.</span></span>

    <span data-ttu-id="d6009-233">b.</span><span class="sxs-lookup"><span data-stu-id="d6009-233">b.</span></span> <span data-ttu-id="d6009-234">請根據您的需求選取 [角色]。</span><span class="sxs-lookup"><span data-stu-id="d6009-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="d6009-235">c.</span><span class="sxs-lookup"><span data-stu-id="d6009-235">c.</span></span> <span data-ttu-id="d6009-236">按一下[新增成員]。</span><span class="sxs-lookup"><span data-stu-id="d6009-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="d6009-237">hello Azure Active Directory 帳戶持有者會收到一封電子郵件，並且遵循連結 tooconfirm 他們的帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="d6009-237">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d6009-238">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d6009-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d6009-239">在本節中，您可以授與存取 tooRFPIO 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d6009-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRFPIO.</span></span>

![指派使用者][200] 

<span data-ttu-id="d6009-241">**tooassign 許 Simon tooRFPIO，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d6009-241">**tooassign Britta Simon tooRFPIO, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6009-242">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d6009-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="d6009-244">在 [hello] 應用程式清單中，選取**RFPIO**。</span><span class="sxs-lookup"><span data-stu-id="d6009-244">In hello applications list, select **RFPIO**.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="d6009-246">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="d6009-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="d6009-248">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d6009-248">Click **Add** button.</span></span> <span data-ttu-id="d6009-249">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d6009-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="d6009-251">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="d6009-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d6009-252">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d6009-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d6009-253">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d6009-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d6009-254">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d6009-254">Test single sign-on</span></span>

<span data-ttu-id="d6009-255">在本節中，您 Azure AD 單一登入組態使用測試 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="d6009-255">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="d6009-256">當您按一下的 hello RFPIO 磚 hello 存取面板中時，您應該取得自動登入 tooyour RFPIO 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6009-256">When you click hello RFPIO tile in hello Access Panel, you should get automatically signed-on tooyour RFPIO application.</span></span>
<span data-ttu-id="d6009-257">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="d6009-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6009-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="d6009-258">Additional resources</span></span>

* [<span data-ttu-id="d6009-259">教學課程有關清單 toointegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6009-259">List of tutorials about how toointegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6009-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d6009-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

