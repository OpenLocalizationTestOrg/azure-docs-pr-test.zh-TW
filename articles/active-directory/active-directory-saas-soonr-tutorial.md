---
title: "教學課程：Azure Active Directory 與 Soonr Workplace 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 之間 Soonr 工作地點。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="96a26-103">教學課程：Azure Active Directory 與 Soonr Workplace 整合</span><span class="sxs-lookup"><span data-stu-id="96a26-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="96a26-104">本教學課程的 hello 目標是 tooshow 您如何 toointegrate Soonr 與 Azure Active Directory (Azure AD) 的工作場所。</span><span class="sxs-lookup"><span data-stu-id="96a26-104">hello objective of this tutorial is tooshow you how toointegrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="96a26-105">與 Azure AD 整合 Soonr 工作地點可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="96a26-105">Integrating Soonr Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="96a26-106">您可以控制存取 tooSoonr 工作地點的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="96a26-106">You can control in Azure AD who has access tooSoonr Workplace</span></span>
- <span data-ttu-id="96a26-107">您可以啟用您的使用者 tooautomatically get 登入 tooSoonr （單一登入） 的工作地點使用其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="96a26-107">You can enable your users tooautomatically get signed-on tooSoonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="96a26-108">您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="96a26-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="96a26-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="96a26-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96a26-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="96a26-110">Prerequisites</span></span>

<span data-ttu-id="96a26-111">tooconfigure Soonr 工作場所的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="96a26-111">tooconfigure Azure AD integration with Soonr Workplace, you need hello following items:</span></span>

- <span data-ttu-id="96a26-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="96a26-112">An Azure AD subscription</span></span>
- <span data-ttu-id="96a26-113">已啟用 Soonr Workplace 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="96a26-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="96a26-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="96a26-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="96a26-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="96a26-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96a26-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="96a26-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="96a26-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="96a26-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="96a26-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="96a26-118">Scenario description</span></span>
<span data-ttu-id="96a26-119">本教學課程的 hello 目標是 tooenable 您 tootest Azure AD 單一登入的測試環境中。</span><span class="sxs-lookup"><span data-stu-id="96a26-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="96a26-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="96a26-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96a26-121">Soonr 工作地點加入從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="96a26-121">Adding Soonr Workplace from hello gallery</span></span>
2. <span data-ttu-id="96a26-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="96a26-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-hello-gallery"></a><span data-ttu-id="96a26-123">Soonr 工作地點加入從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="96a26-123">Adding Soonr Workplace from hello gallery</span></span>
<span data-ttu-id="96a26-124">tooconfigure hello 整合 Soonr 工作區到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Soonr 工作地點。</span><span class="sxs-lookup"><span data-stu-id="96a26-124">tooconfigure hello integration of Soonr Workplace into Azure AD, you need tooadd Soonr Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="96a26-125">**tooadd Soonr 工作場所 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="96a26-125">**tooadd Soonr Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="96a26-126">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="96a26-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="96a26-128">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="96a26-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="96a26-129">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="96a26-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![應用程式][2]

4. <span data-ttu-id="96a26-131">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="96a26-131">Click **Add** at hello bottom of hello page.</span></span>

    ![應用程式][3]

5. <span data-ttu-id="96a26-133">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="96a26-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
 
    ![應用程式][4]

6. <span data-ttu-id="96a26-135">在 [hello] 搜尋方塊中，輸入**Soonr 工作場所**。</span><span class="sxs-lookup"><span data-stu-id="96a26-135">In hello search box, type **Soonr Workplace**.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="96a26-137">在 hello 結果窗格中，選取  **Soonr 工作場所**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="96a26-137">In hello results pane, select **Soonr Workplace**, and then click **Complete** tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="96a26-139">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="96a26-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="96a26-140">hello 本節目標在於 tooshow 如何 tooconfigure 和測試 Azure AD 單一登入的工作場所 Soonr 根據稱為 「 許 Simon"的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="96a26-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="96a26-141">單一登入 toowork，Azure AD 需要 tooknow Soonr 工作場所 tooan 使用者在 Azure AD 中哪些 hello 對等項目的使用者。</span><span class="sxs-lookup"><span data-stu-id="96a26-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Soonr Workplace tooan user in Azure AD is.</span></span> <span data-ttu-id="96a26-142">換句話說，Azure AD 使用者與 hello Soonr 工作地點中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="96a26-142">In other words, a link relationship between an Azure AD user and hello related user in Soonr Workplace needs toobe established.</span></span>  

<span data-ttu-id="96a26-143">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Soonr 工作地點中。</span><span class="sxs-lookup"><span data-stu-id="96a26-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="96a26-144">tooconfigure 和測試 Azure AD 單一登入的 Soonr 工作地點網路，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="96a26-144">tooconfigure and test Azure AD single sign-on with Soonr Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="96a26-145">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="96a26-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="96a26-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="96a26-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96a26-147">**[建立測試使用者 Soonr 工作場所](#creating-a-soonr-workplace-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Soonr 工作地點中對應項目。</span><span class="sxs-lookup"><span data-stu-id="96a26-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - toohave a counterpart of Britta Simon in Soonr Workplace that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="96a26-148">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="96a26-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96a26-149">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="96a26-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="96a26-150">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="96a26-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="96a26-151">在本節中，您可以啟用 Azure AD 單一登入 hello 傳統入口網站中，並 Soonr 工作場所應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="96a26-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="96a26-152">**tooconfigure Azure AD 單一登入的 Soonr 工作地點網路，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="96a26-152">**tooconfigure Azure AD single sign-on with Soonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="96a26-153">在 Azure 傳統入口網站，在 hello hello **Soonr 工作場所**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="96a26-153">In hello Azure classic portal, on hello **Soonr Workplace** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>

    ![設定單一登入][6] 

2. <span data-ttu-id="96a26-155">在 hello**方式上 tooSoonr 工作地點的使用者 toosign 想您**頁面上，選取**Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="96a26-155">On hello **How would you like users toosign on tooSoonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![設定單一登入](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="96a26-157">在 hello**設定應用程式設定**對話方塊頁面上，執行下列步驟的 hello:。</span><span class="sxs-lookup"><span data-stu-id="96a26-157">On hello **Configure App Settings** dialog page, perform hello following steps:.</span></span>

    ![設定單一登入](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="96a26-159">a.</span><span class="sxs-lookup"><span data-stu-id="96a26-159">a.</span></span> <span data-ttu-id="96a26-160">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello: `https://<server-name>.soonr.com/singlesignon/saml/SSO`。</span><span class="sxs-lookup"><span data-stu-id="96a26-160">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="96a26-161">b.</span><span class="sxs-lookup"><span data-stu-id="96a26-161">b.</span></span> <span data-ttu-id="96a26-162">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="96a26-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="96a26-163">請注意，這不是 hello 真正的價值。</span><span class="sxs-lookup"><span data-stu-id="96a26-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="96a26-164">您有的 tooupdate 這個值與實際的 hello 登入 URL。</span><span class="sxs-lookup"><span data-stu-id="96a26-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="96a26-165">請連絡 Soonr 工作場所支援小組 tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="96a26-165">Contact Soonr Workplace support team tooget this value.</span></span>

4. <span data-ttu-id="96a26-166">在 hello **Soonr 工作場所設定單一登入**頁面上，按一下**下載中繼資料**然後儲存您的電腦上的 hello 檔案：</span><span class="sxs-lookup"><span data-stu-id="96a26-166">On hello **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save hello file on your computer:</span></span>

    ![設定單一登入](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="96a26-168">tooget SSO 設定應用程式，請連絡您 Soonr 工作地點的支援團隊並提供 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="96a26-168">tooget SSO configured for your application, contact your Soonr Workplace support team and provide them with hello following:</span></span> 

    <span data-ttu-id="96a26-169">• hello 下載**中繼資料**檔案</span><span class="sxs-lookup"><span data-stu-id="96a26-169">•  hello downloaded **Metadata** file</span></span>

    <span data-ttu-id="96a26-170">• hello**簽發者 URL**</span><span class="sxs-lookup"><span data-stu-id="96a26-170">•  hello **Issuer URL**</span></span>

    <span data-ttu-id="96a26-171">• hello **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="96a26-171">•  hello **SAML SSO URL**</span></span>

    <span data-ttu-id="96a26-172">• hello**單一登出服務 URL**</span><span class="sxs-lookup"><span data-stu-id="96a26-172">•  hello **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="96a26-173">此應用程式由取代<a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask 工作場所</a>，而且可以參考<a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">這</a>教學課程使用 Azure AD 設定 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="96a26-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring hello application with Azure AD.</span></span>
   
6. <span data-ttu-id="96a26-174">在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，然後再按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="96a26-174">In hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD 單一登入][10]

7. <span data-ttu-id="96a26-176">在 hello**單一登入確認**頁面上，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="96a26-176">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD 單一登入][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="96a26-178">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="96a26-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="96a26-179">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 傳統入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="96a26-179">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![建立 Azure AD 使用者][20]

<span data-ttu-id="96a26-181">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="96a26-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="96a26-182">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="96a26-182">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="96a26-184">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="96a26-184">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="96a26-185">toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="96a26-185">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="96a26-187">tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="96a26-187">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="96a26-189">在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="96a26-189">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="96a26-191">a.</span><span class="sxs-lookup"><span data-stu-id="96a26-191">a.</span></span> <span data-ttu-id="96a26-192">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="96a26-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="96a26-193">b.</span><span class="sxs-lookup"><span data-stu-id="96a26-193">b.</span></span> <span data-ttu-id="96a26-194">在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="96a26-194">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96a26-195">c.</span><span class="sxs-lookup"><span data-stu-id="96a26-195">c.</span></span> <span data-ttu-id="96a26-196">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="96a26-196">Click **Next**.</span></span>

6.  <span data-ttu-id="96a26-197">在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="96a26-197">On hello **User Profile** dialog page, perform hello following steps:</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="96a26-199">a.</span><span class="sxs-lookup"><span data-stu-id="96a26-199">a.</span></span> <span data-ttu-id="96a26-200">在 hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="96a26-200">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="96a26-201">b.</span><span class="sxs-lookup"><span data-stu-id="96a26-201">b.</span></span> <span data-ttu-id="96a26-202">在 hello**姓氏**文字方塊中，輸入， **Simon**。</span><span class="sxs-lookup"><span data-stu-id="96a26-202">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="96a26-203">c.</span><span class="sxs-lookup"><span data-stu-id="96a26-203">c.</span></span> <span data-ttu-id="96a26-204">在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="96a26-204">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="96a26-205">d.</span><span class="sxs-lookup"><span data-stu-id="96a26-205">d.</span></span> <span data-ttu-id="96a26-206">在 hello**角色**清單中，選取**使用者**。</span><span class="sxs-lookup"><span data-stu-id="96a26-206">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="96a26-207">e.</span><span class="sxs-lookup"><span data-stu-id="96a26-207">e.</span></span> <span data-ttu-id="96a26-208">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="96a26-208">Click **Next**.</span></span>

7. <span data-ttu-id="96a26-209">在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="96a26-209">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="96a26-211">在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="96a26-211">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="96a26-213">a.</span><span class="sxs-lookup"><span data-stu-id="96a26-213">a.</span></span> <span data-ttu-id="96a26-214">請記下 hello hello 值**新密碼**。</span><span class="sxs-lookup"><span data-stu-id="96a26-214">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="96a26-215">b.</span><span class="sxs-lookup"><span data-stu-id="96a26-215">b.</span></span> <span data-ttu-id="96a26-216">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="96a26-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="96a26-217">建立 Soonr Workplace 測試使用者</span><span class="sxs-lookup"><span data-stu-id="96a26-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="96a26-218">hello 本節目標在於 toocreate 呼叫許 Simon Soonr 工作地點中的使用者。</span><span class="sxs-lookup"><span data-stu-id="96a26-218">hello objective of this section is toocreate a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="96a26-219">請使用 Soonr 工作場所支援小組 toocreate hello 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="96a26-219">Please work with Soonr Workplace support team toocreate a user in hello platform.</span></span> <span data-ttu-id="96a26-220">您可以提高 hello 支援票證，以從 Soonr<a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">這裡</a>。</span><span class="sxs-lookup"><span data-stu-id="96a26-220">You can raise hello support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="96a26-221">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="96a26-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="96a26-222">本節 hello 目標是 tooenabling 許 Simon toouse Azure 單一登入授與他們存取 tooSoonr 工作地點。</span><span class="sxs-lookup"><span data-stu-id="96a26-222">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSoonr Workplace.</span></span>

![指派使用者][200] 

<span data-ttu-id="96a26-224">**tooassign 許 Simon tooSoonr 工作地點，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="96a26-224">**tooassign Britta Simon tooSoonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="96a26-225">在 hello Azure 傳統入口網站，tooopen hello 應用程式 檢視，在 hello 目錄檢視中，按一下 **應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="96a26-225">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="96a26-227">在 [hello] 應用程式清單中，選取**Soonr 工作場所**。</span><span class="sxs-lookup"><span data-stu-id="96a26-227">In hello applications list, select **Soonr Workplace**.</span></span>

    ![設定單一登入](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="96a26-229">在 hello 最上層顯示 hello 功能表上，按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="96a26-229">In hello menu on hello top, click **Users**.</span></span>

    ![指派使用者][203] 

1. <span data-ttu-id="96a26-231">在 hello 使用者清單中選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="96a26-231">In hello Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="96a26-232">在 hello hello 底部的工具列中按一下**指派**。</span><span class="sxs-lookup"><span data-stu-id="96a26-232">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![指派使用者][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="96a26-234">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="96a26-234">Testing single sign-on</span></span>

<span data-ttu-id="96a26-235">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="96a26-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="96a26-236">當您按一下的 hello Soonr 工作場所磚 hello 存取面板中時，您應該取得自動登入 tooyour Soonr 工作場所應用程式。</span><span class="sxs-lookup"><span data-stu-id="96a26-236">When you click hello Soonr Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="96a26-237">其他資源</span><span class="sxs-lookup"><span data-stu-id="96a26-237">Additional resources</span></span>

* [<span data-ttu-id="96a26-238">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96a26-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96a26-239">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="96a26-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
