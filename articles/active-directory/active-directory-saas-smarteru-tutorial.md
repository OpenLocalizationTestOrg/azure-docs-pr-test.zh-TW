---
title: "教學課程：Azure Active Directory 與 SmarterU 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 SmarterU 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: a3b81b557c47e31f09e61bcf75dd23f370e642e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="aff72-103">教學課程：Azure Active Directory 與 SmarterU 整合</span><span class="sxs-lookup"><span data-stu-id="aff72-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="aff72-104">在此教學課程中，您學會如何 toointegrate SmarterU 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="aff72-104">In this tutorial, you learn how toointegrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aff72-105">整合 Azure AD 與 SmarterU 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="aff72-105">Integrating SmarterU with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="aff72-106">您可以控制存取 tooSmarterU Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="aff72-106">You can control in Azure AD who has access tooSmarterU</span></span>
- <span data-ttu-id="aff72-107">您可以啟用您的使用者 tooautomatically get 登入 tooSmarterU （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="aff72-107">You can enable your users tooautomatically get signed-on tooSmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aff72-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="aff72-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="aff72-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="aff72-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aff72-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="aff72-110">Prerequisites</span></span>

<span data-ttu-id="aff72-111">tooconfigure Azure AD 與 SmarterU 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="aff72-111">tooconfigure Azure AD integration with SmarterU, you need hello following items:</span></span>

- <span data-ttu-id="aff72-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="aff72-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aff72-113">已啟用 SmarterU 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="aff72-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aff72-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="aff72-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aff72-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="aff72-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aff72-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="aff72-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aff72-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="aff72-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aff72-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="aff72-118">Scenario description</span></span>
<span data-ttu-id="aff72-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="aff72-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aff72-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="aff72-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aff72-121">從 hello 圖庫加入 SmarterU</span><span class="sxs-lookup"><span data-stu-id="aff72-121">Adding SmarterU from hello gallery</span></span>
2. <span data-ttu-id="aff72-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="aff72-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-hello-gallery"></a><span data-ttu-id="aff72-123">從 hello 圖庫加入 SmarterU</span><span class="sxs-lookup"><span data-stu-id="aff72-123">Adding SmarterU from hello gallery</span></span>
<span data-ttu-id="aff72-124">tooconfigure hello 整合 SmarterU 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd SmarterU。</span><span class="sxs-lookup"><span data-stu-id="aff72-124">tooconfigure hello integration of SmarterU into Azure AD, you need tooadd SmarterU from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="aff72-125">**tooadd SmarterU 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="aff72-125">**tooadd SmarterU from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="aff72-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="aff72-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aff72-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="aff72-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="aff72-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="aff72-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="aff72-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="aff72-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="aff72-133">在 [hello] 搜尋方塊中，輸入**SmarterU**。</span><span class="sxs-lookup"><span data-stu-id="aff72-133">In hello search box, type **SmarterU**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="aff72-135">在 hello 結果 窗格中，選取  **SmarterU**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aff72-135">In hello results panel, select **SmarterU**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aff72-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="aff72-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aff72-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 SmarterU 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="aff72-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="aff72-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 SmarterU 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="aff72-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SmarterU is tooa user in Azure AD.</span></span> <span data-ttu-id="aff72-140">換句話說，Azure AD 使用者與 SmarterU 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="aff72-140">In other words, a link relationship between an Azure AD user and hello related user in SmarterU needs toobe established.</span></span>

<span data-ttu-id="aff72-141">在 SmarterU 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="aff72-141">In SmarterU, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="aff72-142">tooconfigure 和測試 Azure AD 單一登入與 SmarterU，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="aff72-142">tooconfigure and test Azure AD single sign-on with SmarterU, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="aff72-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="aff72-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="aff72-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="aff72-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aff72-145">**[建立測試使用者 SmarterU](#creating-a-smarteru-test-user)**  -toohave 許 Simon SmarterU 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="aff72-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - toohave a counterpart of Britta Simon in SmarterU that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="aff72-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="aff72-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aff72-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="aff72-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aff72-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="aff72-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aff72-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 SmarterU 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="aff72-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="aff72-150">**tooconfigure Azure AD 單一登入 SmarterU 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="aff72-150">**tooconfigure Azure AD single sign-on with SmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="aff72-151">在 Azure 入口網站上 hello hello **SmarterU**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="aff72-151">In hello Azure portal, on hello **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="aff72-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="aff72-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="aff72-155">在 hello **SmarterU 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="aff72-155">On hello **SmarterU Domain and URLs** section, perform hello following steps:</span></span> 

    ![設定單一登入](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="aff72-157">在 hello**識別碼**文字方塊中，型別 hello URL:`https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="aff72-157">In hello **Identifier** textbox, type hello URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="aff72-158">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="aff72-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="aff72-160">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="aff72-160">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="aff72-162">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour SmarterU 公司網站。</span><span class="sxs-lookup"><span data-stu-id="aff72-162">In a different web browser window, log in tooyour SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="aff72-163">在 hello hello 上方的工具列中按一下**帳戶設定**。</span><span class="sxs-lookup"><span data-stu-id="aff72-163">In hello toolbar on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="aff72-164">![帳戶設定](./media/active-directory-saas-smarteru-tutorial/IC777326.png "帳戶設定")</span><span class="sxs-lookup"><span data-stu-id="aff72-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="aff72-165">在 hello 帳戶設定 頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="aff72-165">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="aff72-166">![外部授權](./media/active-directory-saas-smarteru-tutorial/IC777327.png "外部授權")</span><span class="sxs-lookup"><span data-stu-id="aff72-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="aff72-167">a.</span><span class="sxs-lookup"><span data-stu-id="aff72-167">a.</span></span> <span data-ttu-id="aff72-168">選取 [啟用外部授權] 。</span><span class="sxs-lookup"><span data-stu-id="aff72-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="aff72-169">b.</span><span class="sxs-lookup"><span data-stu-id="aff72-169">b.</span></span> <span data-ttu-id="aff72-170">在 [hello**主登入控制**區段中，選取 hello **SmarterU** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="aff72-170">In hello **Master Login Control** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="aff72-171">c.</span><span class="sxs-lookup"><span data-stu-id="aff72-171">c.</span></span> <span data-ttu-id="aff72-172">在 [hello**使用者預設登入**區段中，選取 hello **SmarterU** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="aff72-172">In hello **User Default Login** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="aff72-173">d.</span><span class="sxs-lookup"><span data-stu-id="aff72-173">d.</span></span> <span data-ttu-id="aff72-174">選取 [啟用 Okta] 。</span><span class="sxs-lookup"><span data-stu-id="aff72-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="aff72-175">e.</span><span class="sxs-lookup"><span data-stu-id="aff72-175">e.</span></span> <span data-ttu-id="aff72-176">Hello 內容的 hello 下載的中繼資料檔案，請複製並貼到 hello **Okta 中繼資料**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="aff72-176">Copy hello content of hello downloaded metadata file, and then paste it into hello **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="aff72-177">f.</span><span class="sxs-lookup"><span data-stu-id="aff72-177">f.</span></span> <span data-ttu-id="aff72-178">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="aff72-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="aff72-179">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="aff72-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="aff72-180">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="aff72-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="aff72-181">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aff72-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aff72-182">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="aff72-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="aff72-183">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="aff72-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="aff72-185">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="aff72-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="aff72-186">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="aff72-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aff72-188">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="aff72-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aff72-190">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="aff72-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aff72-192">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="aff72-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aff72-194">a.</span><span class="sxs-lookup"><span data-stu-id="aff72-194">a.</span></span> <span data-ttu-id="aff72-195">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="aff72-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aff72-196">b.</span><span class="sxs-lookup"><span data-stu-id="aff72-196">b.</span></span> <span data-ttu-id="aff72-197">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="aff72-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aff72-198">c.</span><span class="sxs-lookup"><span data-stu-id="aff72-198">c.</span></span> <span data-ttu-id="aff72-199">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="aff72-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="aff72-200">d.</span><span class="sxs-lookup"><span data-stu-id="aff72-200">d.</span></span> <span data-ttu-id="aff72-201">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="aff72-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="aff72-202">建立 SmarterU 測試使用者</span><span class="sxs-lookup"><span data-stu-id="aff72-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="aff72-203">tooenable Azure AD 使用者 toolog 中 tooSmarterU，它們必須佈建到 SmarterU。</span><span class="sxs-lookup"><span data-stu-id="aff72-203">tooenable Azure AD users toolog in tooSmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="aff72-204">SmarterU 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="aff72-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="aff72-205">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="aff72-205">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="aff72-206">登入 tooyour **SmarterU**租用戶。</span><span class="sxs-lookup"><span data-stu-id="aff72-206">Log in tooyour **SmarterU** tenant.</span></span>

2. <span data-ttu-id="aff72-207">跳過**使用者**。</span><span class="sxs-lookup"><span data-stu-id="aff72-207">Go too**Users**.</span></span>

3. <span data-ttu-id="aff72-208">在 hello 使用者區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="aff72-208">In hello user section, perform hello following steps:</span></span>
   
    <span data-ttu-id="aff72-209">![新增使用者](./media/active-directory-saas-smarteru-tutorial/IC777329.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="aff72-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="aff72-210">a.</span><span class="sxs-lookup"><span data-stu-id="aff72-210">a.</span></span> <span data-ttu-id="aff72-211">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="aff72-211">Click **+User**.</span></span>
    
    <span data-ttu-id="aff72-212">b.</span><span class="sxs-lookup"><span data-stu-id="aff72-212">b.</span></span> <span data-ttu-id="aff72-213">型別 hello hello 下列文字方塊將相關的 hello Azure AD 使用者帳戶的屬性值：**主要電子郵件**，**員工識別碼**，**密碼**， **驗證密碼**，**名字**，**姓氏**。</span><span class="sxs-lookup"><span data-stu-id="aff72-213">Type hello related attribute values of hello Azure AD user account into hello following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="aff72-214">c.</span><span class="sxs-lookup"><span data-stu-id="aff72-214">c.</span></span> <span data-ttu-id="aff72-215">按一下 [作用中] 。</span><span class="sxs-lookup"><span data-stu-id="aff72-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="aff72-216">d.</span><span class="sxs-lookup"><span data-stu-id="aff72-216">d.</span></span> <span data-ttu-id="aff72-217">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="aff72-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="aff72-218">您可以使用任何其他 SmarterU 使用者帳戶建立工具或 Api 提供 SmarterU tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="aff72-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="aff72-219">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="aff72-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="aff72-220">在本節中，您可以授與存取 tooSmarterU 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="aff72-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmarterU.</span></span>

![指派使用者][200] 

<span data-ttu-id="aff72-222">**tooassign 許 Simon tooSmarterU，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="aff72-222">**tooassign Britta Simon tooSmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="aff72-223">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="aff72-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="aff72-225">在 [hello] 應用程式清單中，選取**SmarterU**。</span><span class="sxs-lookup"><span data-stu-id="aff72-225">In hello applications list, select **SmarterU**.</span></span>

    ![設定單一登入](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="aff72-227">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="aff72-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="aff72-229">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="aff72-229">Click **Add** button.</span></span> <span data-ttu-id="aff72-230">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="aff72-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="aff72-232">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="aff72-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="aff72-233">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="aff72-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aff72-234">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="aff72-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aff72-235">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="aff72-235">Testing single sign-on</span></span>

<span data-ttu-id="aff72-236">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="aff72-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="aff72-237">當您按一下 hello SmarterU 磚 hello 存取面板中的時，您應該取得自動登入 tooyour SmarterU 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="aff72-237">When you click hello SmarterU tile in hello Access Panel, you should get automatically signed-on tooyour SmarterU application.</span></span>
<span data-ttu-id="aff72-238">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="aff72-238">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="aff72-239">其他資源</span><span class="sxs-lookup"><span data-stu-id="aff72-239">Additional resources</span></span>

* [<span data-ttu-id="aff72-240">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aff72-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aff72-241">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="aff72-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

