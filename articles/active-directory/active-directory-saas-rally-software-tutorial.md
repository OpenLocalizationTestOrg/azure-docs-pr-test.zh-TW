---
title: "教學課程：Azure Active Directory 與 Rally Software 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Rally Software 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: c75c8b98ce7fab19964c13de5ad7e19ef3ebd0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="12728-103">教學課程：Azure Active Directory 與 Rally Software 整合</span><span class="sxs-lookup"><span data-stu-id="12728-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="12728-104">在此教學課程中，您學會如何 toointegrate Rally Software 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="12728-104">In this tutorial, you learn how toointegrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="12728-105">整合 Azure AD 與 Rally Software 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="12728-105">Integrating Rally Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="12728-106">您可以控制存取 tooRally 軟體的 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="12728-106">You can control in Azure AD who has access tooRally Software.</span></span>
- <span data-ttu-id="12728-107">您可以啟用您的使用者 tooautomatically get 登入 tooRally （單一登入） 的軟體與他們的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="12728-107">You can enable your users tooautomatically get signed-on tooRally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="12728-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="12728-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="12728-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="12728-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12728-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="12728-110">Prerequisites</span></span>

<span data-ttu-id="12728-111">tooconfigure Azure AD 與 Rally Software 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="12728-111">tooconfigure Azure AD integration with Rally Software, you need hello following items:</span></span>

- <span data-ttu-id="12728-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="12728-112">An Azure AD subscription</span></span>
- <span data-ttu-id="12728-113">已啟用 Rally Software 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="12728-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="12728-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="12728-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="12728-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="12728-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="12728-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="12728-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="12728-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="12728-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="12728-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="12728-118">Scenario description</span></span>
<span data-ttu-id="12728-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="12728-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="12728-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="12728-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="12728-121">從 hello 圖庫加入 Rally Software</span><span class="sxs-lookup"><span data-stu-id="12728-121">Adding Rally Software from hello gallery</span></span>
2. <span data-ttu-id="12728-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="12728-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-hello-gallery"></a><span data-ttu-id="12728-123">從 hello 圖庫加入 Rally Software</span><span class="sxs-lookup"><span data-stu-id="12728-123">Adding Rally Software from hello gallery</span></span>
<span data-ttu-id="12728-124">tooconfigure hello 整合 Rally Software 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Rally Software。</span><span class="sxs-lookup"><span data-stu-id="12728-124">tooconfigure hello integration of Rally Software into Azure AD, you need tooadd Rally Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="12728-125">**tooadd Rally Software 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="12728-125">**tooadd Rally Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="12728-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="12728-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory] 按鈕][1]

2. <span data-ttu-id="12728-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="12728-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="12728-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="12728-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式] 刀鋒視窗][2]
    
3. <span data-ttu-id="12728-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="12728-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="12728-133">在 [hello] 搜尋方塊中，輸入**Rally Software**，選取**Rally Software**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="12728-133">In hello search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![在結果清單中 hello rally 軟體](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="12728-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="12728-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="12728-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Rally Software 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="12728-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="12728-137">單一登入 toowork，Azure AD 需要 tooknow Rally Software 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="12728-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rally Software is tooa user in Azure AD.</span></span> <span data-ttu-id="12728-138">換句話說，Azure AD 使用者與 Rally Software 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="12728-138">In other words, a link relationship between an Azure AD user and hello related user in Rally Software needs toobe established.</span></span>

<span data-ttu-id="12728-139">在 Rally Software，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="12728-139">In Rally Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="12728-140">tooconfigure 及測試 Azure AD 單一登入 Rally Software，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="12728-140">tooconfigure and test Azure AD single sign-on with Rally Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="12728-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="12728-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="12728-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="12728-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="12728-143">**[建立測試使用者 Rally Software](#create-a-rally-software-test-user) ** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Rally Software 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="12728-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - toohave a counterpart of Britta Simon in Rally Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="12728-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="12728-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="12728-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="12728-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="12728-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="12728-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="12728-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Rally Software 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="12728-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="12728-148">**tooconfigure Azure AD 單一登入 Rally Software，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="12728-148">**tooconfigure Azure AD single sign-on with Rally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="12728-149">在 Azure 入口網站上 hello hello **Rally Software**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="12728-149">In hello Azure portal, on hello **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="12728-151">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="12728-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="12728-153">在 [hello **Rally 軟體網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="12728-153">On hello **Rally Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Rally Software 網域與 URL 單一登入資訊](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="12728-155">a.</span><span class="sxs-lookup"><span data-stu-id="12728-155">a.</span></span> <span data-ttu-id="12728-156">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="12728-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="12728-157">b.</span><span class="sxs-lookup"><span data-stu-id="12728-157">b.</span></span> <span data-ttu-id="12728-158">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="12728-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="12728-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="12728-159">These values are not real.</span></span> <span data-ttu-id="12728-160">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="12728-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="12728-161">請連絡[Rally 軟體用戶端支援小組](https://help.rallydev.com/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="12728-161">Contact [Rally Software Client support team](https://help.rallydev.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="12728-162">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="12728-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="12728-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="12728-164">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="12728-166">在 [hello **Rally 軟體組態**區段中，按一下**設定 Rally Software** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="12728-166">On hello **Rally Software Configuration** section, click **Configure Rally Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="12728-167">複製 hello**登出 URL 和 SAML 實體識別碼**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="12728-167">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Rally Software 設定](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="12728-169">登入 tooyour **Rally Software**租用戶。</span><span class="sxs-lookup"><span data-stu-id="12728-169">Log in tooyour **Rally Software** tenant.</span></span>

8. <span data-ttu-id="12728-170">在 hello hello 上方的工具列中按一下**安裝**，然後選取**訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="12728-170">In hello toolbar on hello top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="12728-171">![訂用帳戶](./media/active-directory-saas-rally-software-tutorial/ic769531.png "訂用帳戶")</span><span class="sxs-lookup"><span data-stu-id="12728-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="12728-172">按一下 hello**動作**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="12728-172">Click hello **Action** button.</span></span> <span data-ttu-id="12728-173">選取**編輯訂用帳戶**在 hello 右上方的 hello 工具列。</span><span class="sxs-lookup"><span data-stu-id="12728-173">Select **Edit Subscription** at hello top right side of hello toolbar.</span></span>

10. <span data-ttu-id="12728-174">在 [hello**訂用帳戶**對話方塊頁面上，執行下列步驟，hello，然後按一下 [**儲存並關閉**:</span><span class="sxs-lookup"><span data-stu-id="12728-174">On hello **Subscription** dialog page, perform hello following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="12728-175">![驗證](./media/active-directory-saas-rally-software-tutorial/ic769542.png "驗證")</span><span class="sxs-lookup"><span data-stu-id="12728-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="12728-176">a.</span><span class="sxs-lookup"><span data-stu-id="12728-176">a.</span></span> <span data-ttu-id="12728-177">從 [驗證] 下拉式清單中選取 [Rally 或 SSO 驗證]。</span><span class="sxs-lookup"><span data-stu-id="12728-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="12728-178">b.</span><span class="sxs-lookup"><span data-stu-id="12728-178">b.</span></span> <span data-ttu-id="12728-179">在 [hello**身分識別提供者 URL**文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="12728-179">In hello **Identity provider URL** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="12728-180">c.</span><span class="sxs-lookup"><span data-stu-id="12728-180">c.</span></span> <span data-ttu-id="12728-181">在 [hello **SSO 登出**文字方塊中，貼上 hello 值**登出 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="12728-181">In hello **SSO Logout** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="12728-182">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="12728-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="12728-183">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="12728-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="12728-184">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="12728-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="12728-185">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="12728-185">Create an Azure AD test user</span></span>

<span data-ttu-id="12728-186">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="12728-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="12728-188">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="12728-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="12728-189">在 [hello Azure 入口網站，hello 左窗格中，按一下 [hello **Azure Active Directory** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="12728-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory] 按鈕](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="12728-191">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下 [**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="12728-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="12728-193">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="12728-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="12728-195">在 [hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="12728-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="12728-197">a.</span><span class="sxs-lookup"><span data-stu-id="12728-197">a.</span></span> <span data-ttu-id="12728-198">在 [hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="12728-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="12728-199">b.</span><span class="sxs-lookup"><span data-stu-id="12728-199">b.</span></span> <span data-ttu-id="12728-200">在 [hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="12728-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="12728-201">c.</span><span class="sxs-lookup"><span data-stu-id="12728-201">c.</span></span> <span data-ttu-id="12728-202">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 [hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="12728-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="12728-203">d.</span><span class="sxs-lookup"><span data-stu-id="12728-203">d.</span></span> <span data-ttu-id="12728-204">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="12728-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="12728-205">建立 Rally Software 測試使用者</span><span class="sxs-lookup"><span data-stu-id="12728-205">Create a Rally Software test user</span></span>

<span data-ttu-id="12728-206">Azure AD 使用者 toobe 無法 toosign 中，它們必須已佈建的 toohello Rally Software 的應用程式使用他們的 Azure Active Directory 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="12728-206">For Azure AD users toobe able toosign in, they must be provisioned toohello Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="12728-207">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="12728-207">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="12728-208">登入 tooyour Rally Software 租用戶。</span><span class="sxs-lookup"><span data-stu-id="12728-208">Log in tooyour Rally Software tenant.</span></span>

2. <span data-ttu-id="12728-209">跳過**安裝\>使用者**，然後按一下 [ **+ 加入新**。</span><span class="sxs-lookup"><span data-stu-id="12728-209">Go too**Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="12728-210">![使用者](./media/active-directory-saas-rally-software-tutorial/ic781039.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="12728-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="12728-211">在 hello 新使用者] 文字方塊中輸入 hello 名稱，然後按一下**新增詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="12728-211">Type hello name in hello New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="12728-212">在 [hello **Create User**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="12728-212">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="12728-213">![建立使用者](./media/active-directory-saas-rally-software-tutorial/ic781040.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="12728-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="12728-214">a.</span><span class="sxs-lookup"><span data-stu-id="12728-214">a.</span></span> <span data-ttu-id="12728-215">在 [hello**使用者名稱**文字方塊中，像是使用者的型別 hello 名稱**Brittsimon**。</span><span class="sxs-lookup"><span data-stu-id="12728-215">In hello **User Name** textbox, type hello name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="12728-216">b.</span><span class="sxs-lookup"><span data-stu-id="12728-216">b.</span></span> <span data-ttu-id="12728-217">在**電子郵件地址**文字方塊中，輸入 hello 電子郵件的使用者，例如** brittasimon@contoso.com **。</span><span class="sxs-lookup"><span data-stu-id="12728-217">In **E-mail Address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="12728-218">c.</span><span class="sxs-lookup"><span data-stu-id="12728-218">c.</span></span> <span data-ttu-id="12728-219">在**名字**文字方塊中，輸入 hello 名字，例如使用者的**許**。</span><span class="sxs-lookup"><span data-stu-id="12728-219">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="12728-220">d.</span><span class="sxs-lookup"><span data-stu-id="12728-220">d.</span></span> <span data-ttu-id="12728-221">在**姓氏**文字方塊中，輸入 hello 姓氏的使用者，例如**Simon**。</span><span class="sxs-lookup"><span data-stu-id="12728-221">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="12728-222">e.</span><span class="sxs-lookup"><span data-stu-id="12728-222">e.</span></span> <span data-ttu-id="12728-223">按一下 [儲存並關閉]。</span><span class="sxs-lookup"><span data-stu-id="12728-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="12728-224">您可以使用任何其他 Rally Software 使用者帳戶建立工具或 Api 提供 Rally Software tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="12728-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="12728-225">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="12728-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="12728-226">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooRally 軟體。</span><span class="sxs-lookup"><span data-stu-id="12728-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRally Software.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="12728-228">**tooassign 許 Simon tooRally 軟體，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="12728-228">**tooassign Britta Simon tooRally Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="12728-229">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="12728-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="12728-231">在 [hello] 應用程式清單中，選取**Rally Software**。</span><span class="sxs-lookup"><span data-stu-id="12728-231">In hello applications list, select **Rally Software**.</span></span>

    ![hello 應用程式清單中的 hello Rally Software 連結](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="12728-233">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="12728-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="12728-235">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="12728-235">Click **Add** button.</span></span> <span data-ttu-id="12728-236">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="12728-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="12728-238">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="12728-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="12728-239">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="12728-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="12728-240">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="12728-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="12728-241">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="12728-241">Test single sign-on</span></span>

<span data-ttu-id="12728-242">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="12728-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="12728-243">當您按一下 hello Rally Software 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Rally Software 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="12728-243">When you click hello Rally Software tile in hello Access Panel, you should get automatically signed-on tooyour Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="12728-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="12728-244">Additional resources</span></span>

* [<span data-ttu-id="12728-245">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12728-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="12728-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="12728-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

