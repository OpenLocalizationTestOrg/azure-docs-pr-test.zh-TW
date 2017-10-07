---
title: "教學課程：Azure Active Directory 與 Atomic Learning 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與不可部分完成的學習之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 495f54a6-e6c4-41b0-aafa-a6283d33efc8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 12d7c380dbe47899eb35486c5e2a6936e8fb8b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atomic-learning"></a><span data-ttu-id="ad67f-103">教學課程：Azure Active Directory 與 Atomic Learning 整合</span><span class="sxs-lookup"><span data-stu-id="ad67f-103">Tutorial: Azure Active Directory integration with Atomic Learning</span></span>

<span data-ttu-id="ad67f-104">在此教學課程中，您學會如何 toointegrate 不可部分完成的學習與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="ad67f-104">In this tutorial, you learn how toointegrate Atomic Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad67f-105">整合與 Azure AD 的不可部分完成的學習可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="ad67f-105">Integrating Atomic Learning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ad67f-106">您可以控制存取 tooAtomic Azure AD 中學習</span><span class="sxs-lookup"><span data-stu-id="ad67f-106">You can control in Azure AD who has access tooAtomic Learning</span></span>
- <span data-ttu-id="ad67f-107">您可以啟用您的使用者 tooautomatically get 登入 tooAtomic 機器學習其 Azure AD 帳戶 （單一登入）</span><span class="sxs-lookup"><span data-stu-id="ad67f-107">You can enable your users tooautomatically get signed-on tooAtomic Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ad67f-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ad67f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ad67f-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ad67f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad67f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ad67f-110">Prerequisites</span></span>

<span data-ttu-id="ad67f-111">tooconfigure 與不可部分完成的學習的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="ad67f-111">tooconfigure Azure AD integration with Atomic Learning, you need hello following items:</span></span>

- <span data-ttu-id="ad67f-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ad67f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ad67f-113">已啟用 Atomic Learning 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ad67f-113">An Atomic Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad67f-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="ad67f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ad67f-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ad67f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad67f-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ad67f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ad67f-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ad67f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad67f-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ad67f-118">Scenario description</span></span>
<span data-ttu-id="ad67f-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ad67f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad67f-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="ad67f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad67f-121">從 hello 圖庫加入不可部分完成的學習</span><span class="sxs-lookup"><span data-stu-id="ad67f-121">Adding Atomic Learning from hello gallery</span></span>
2. <span data-ttu-id="ad67f-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ad67f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atomic-learning-from-hello-gallery"></a><span data-ttu-id="ad67f-123">從 hello 圖庫加入不可部分完成的學習</span><span class="sxs-lookup"><span data-stu-id="ad67f-123">Adding Atomic Learning from hello gallery</span></span>
<span data-ttu-id="ad67f-124">tooconfigure hello 整合不可部分完成的學習到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 不可部分完成的學習。</span><span class="sxs-lookup"><span data-stu-id="ad67f-124">tooconfigure hello integration of Atomic Learning into Azure AD, you need tooadd Atomic Learning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ad67f-125">**tooadd 不可部分完成的學習 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ad67f-125">**tooadd Atomic Learning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad67f-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="ad67f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ad67f-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ad67f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ad67f-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ad67f-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ad67f-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="ad67f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ad67f-133">在 [hello] 搜尋方塊中，輸入**不可部分完成的學習**。</span><span class="sxs-lookup"><span data-stu-id="ad67f-133">In hello search box, type **Atomic Learning**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_search.png)

5. <span data-ttu-id="ad67f-135">在 hello 結果 窗格中，選取 **不可部分完成的學習**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ad67f-135">In hello results panel, select **Atomic Learning**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ad67f-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ad67f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ad67f-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Atomic Learning 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ad67f-138">In this section, you configure and test Azure AD single sign-on with Atomic Learning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ad67f-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者不可部分完成的了解 Azure AD 中是 tooa 使用者。</span><span class="sxs-lookup"><span data-stu-id="ad67f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Atomic Learning is tooa user in Azure AD.</span></span> <span data-ttu-id="ad67f-140">換句話說，Azure AD 使用者與 hello 不可部分完成的了解相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="ad67f-140">In other words, a link relationship between an Azure AD user and hello related user in Atomic Learning needs toobe established.</span></span>

<span data-ttu-id="ad67f-141">在不可部分完成學習 」 中，將指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ad67f-141">In Atomic Learning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ad67f-142">tooconfigure 及測試 Azure AD 單一登入與不可部分完成的學習，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="ad67f-142">tooconfigure and test Azure AD single sign-on with Atomic Learning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ad67f-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="ad67f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ad67f-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="ad67f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ad67f-145">**[建立不可部分完成的學習測試使用者](#creating-an-atomic-learning-test-user)** -toohave 中不可部分完成是表示連結的 toohello Azure AD 使用者的學習許 Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="ad67f-145">**[Creating an Atomic Learning test user](#creating-an-atomic-learning-test-user)** - toohave a counterpart of Britta Simon in Atomic Learning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ad67f-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ad67f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad67f-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="ad67f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ad67f-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ad67f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ad67f-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並不可部分完成的學習應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="ad67f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Atomic Learning application.</span></span>

<span data-ttu-id="ad67f-150">**tooconfigure Azure AD 單一登入與不可部分完成學習 」 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ad67f-150">**tooconfigure Azure AD single sign-on with Atomic Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad67f-151">在 Azure 入口網站上 hello hello**不可部分完成的學習**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="ad67f-151">In hello Azure portal, on hello **Atomic Learning** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ad67f-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ad67f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_samlbase.png)

3. <span data-ttu-id="ad67f-155">在 hello**不可部分完成的學習網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ad67f-155">On hello **Atomic Learning Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_url.png)

     <span data-ttu-id="ad67f-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="ad67f-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="ad67f-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="ad67f-158">This value is not real.</span></span> <span data-ttu-id="ad67f-159">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="ad67f-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ad67f-160">請連絡[不可部分完成的學習用戶端支援小組](mailto:cs@atomiclearning.com)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="ad67f-160">Contact [Atomic Learning Client support team](mailto:cs@atomiclearning.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="ad67f-161">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="ad67f-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_certificate.png) 

5. <span data-ttu-id="ad67f-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ad67f-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ad67f-165">tooconfigure 單一登入上**不可部分完成的學習**端，您需要下載 toosend hello**中繼資料 XML**太[不可部分完成的學習技術支援小組](mailto:cs@atomiclearning.com)。</span><span class="sxs-lookup"><span data-stu-id="ad67f-165">tooconfigure single sign-on on **Atomic Learning** side, you need toosend hello downloaded **Metadata XML** too[Atomic Learning support team](mailto:cs@atomiclearning.com).</span></span> <span data-ttu-id="ad67f-166">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="ad67f-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ad67f-167">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="ad67f-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ad67f-168">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="ad67f-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ad67f-169">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ad67f-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ad67f-170">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ad67f-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="ad67f-171">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ad67f-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ad67f-173">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ad67f-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad67f-174">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="ad67f-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ad67f-176">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="ad67f-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ad67f-178">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="ad67f-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ad67f-180">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ad67f-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ad67f-182">a.</span><span class="sxs-lookup"><span data-stu-id="ad67f-182">a.</span></span> <span data-ttu-id="ad67f-183">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ad67f-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad67f-184">b.</span><span class="sxs-lookup"><span data-stu-id="ad67f-184">b.</span></span> <span data-ttu-id="ad67f-185">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="ad67f-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ad67f-186">c.</span><span class="sxs-lookup"><span data-stu-id="ad67f-186">c.</span></span> <span data-ttu-id="ad67f-187">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="ad67f-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ad67f-188">d.</span><span class="sxs-lookup"><span data-stu-id="ad67f-188">d.</span></span> <span data-ttu-id="ad67f-189">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ad67f-189">Click **Create**.</span></span>
 
### <a name="creating-an-atomic-learning-test-user"></a><span data-ttu-id="ad67f-190">建立 Atomic Learning 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ad67f-190">Creating an Atomic Learning test user</span></span>

<span data-ttu-id="ad67f-191">在本節中，您會在 Atomic Learning 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ad67f-191">In this section, you create a user called Britta Simon in Atomic Learning.</span></span> <span data-ttu-id="ad67f-192">Atomic Learning 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="ad67f-192">Atomic Learning supports just-in-time provisioning, which is by default enabled.</span></span> 

<span data-ttu-id="ad67f-193">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="ad67f-193">There is no action item for you in this section.</span></span> <span data-ttu-id="ad67f-194">如果不存在尚未使用 hello 電子郵件地址 hello 使用者嘗試 tooaccess 不可部分完成的學習期間，建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="ad67f-194">A new user is created during an attempt tooaccess Atomic Learning if it doesn't exist yet using hello email address for hello user.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ad67f-195">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="ad67f-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ad67f-196">在本節中，您必須啟用 Azure 單一登入許 Simon toouse 授與存取 tooAtomic 學習。</span><span class="sxs-lookup"><span data-stu-id="ad67f-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAtomic Learning.</span></span>

![指派使用者][200] 

<span data-ttu-id="ad67f-198">**tooassign 許 Simon tooAtomic 學習，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ad67f-198">**tooassign Britta Simon tooAtomic Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad67f-199">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ad67f-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ad67f-201">在 [hello] 應用程式清單中，選取**不可部分完成的學習**。</span><span class="sxs-lookup"><span data-stu-id="ad67f-201">In hello applications list, select **Atomic Learning**.</span></span>

    ![設定單一登入](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_app.png) 

3. <span data-ttu-id="ad67f-203">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="ad67f-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ad67f-205">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ad67f-205">Click **Add** button.</span></span> <span data-ttu-id="ad67f-206">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ad67f-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ad67f-208">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="ad67f-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ad67f-209">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ad67f-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ad67f-210">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ad67f-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ad67f-211">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ad67f-211">Testing single sign-on</span></span>

<span data-ttu-id="ad67f-212">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="ad67f-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ad67f-213">當您按一下 hello 不可部分完成的學習磚 hello 存取面板中時，您應該取得自動登入 tooyour 不可部分完成的學習應用程式。</span><span class="sxs-lookup"><span data-stu-id="ad67f-213">When you click hello Atomic Learning tile in hello Access Panel, you should get automatically signed-on tooyour Atomic Learning application.</span></span>
<span data-ttu-id="ad67f-214">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="ad67f-214">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ad67f-215">其他資源</span><span class="sxs-lookup"><span data-stu-id="ad67f-215">Additional resources</span></span>

* [<span data-ttu-id="ad67f-216">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad67f-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad67f-217">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ad67f-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_203.png

