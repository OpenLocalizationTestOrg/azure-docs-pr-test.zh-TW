---
title: "教學課程：Azure Active Directory 與 Bynder 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Bynder 之間。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="a7e52-103">教學課程：Azure Active Directory 與 Bynder 整合</span><span class="sxs-lookup"><span data-stu-id="a7e52-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="a7e52-104">本教學課程的 hello 目標是 tooshow 您如何 toointegrate Bynder 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a7e52-104">hello objective of this tutorial is tooshow you how toointegrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7e52-105">與 Azure AD 整合 Bynder 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="a7e52-105">Integrating Bynder with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="a7e52-106">您可以控制存取 tooBynder Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="a7e52-106">You can control in Azure AD who has access tooBynder</span></span>
* <span data-ttu-id="a7e52-107">您可以啟用您的使用者 tooautomatically get tooBynder 已登入的單一登入 (SSO) 與他們的 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="a7e52-107">You can enable your users tooautomatically get signed-on tooBynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="a7e52-108">您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="a7e52-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="a7e52-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a7e52-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7e52-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a7e52-110">Prerequisites</span></span>
<span data-ttu-id="a7e52-111">tooconfigure Bynder 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="a7e52-111">tooconfigure Azure AD integration with Bynder, you need hello following items:</span></span>

* <span data-ttu-id="a7e52-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a7e52-112">An Azure AD subscription</span></span>
* <span data-ttu-id="a7e52-113">已啟用 Bynder 單一登入 (SSO) 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a7e52-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="a7e52-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="a7e52-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="a7e52-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a7e52-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="a7e52-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="a7e52-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="a7e52-117">如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a7e52-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7e52-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a7e52-118">Scenario description</span></span>
<span data-ttu-id="a7e52-119">本教學課程的 hello 目標是 tooenable 您 tootest Microsoft Azure AD 的 SSO 在測試環境中。</span><span class="sxs-lookup"><span data-stu-id="a7e52-119">hello objective of this tutorial is tooenable you tootest Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="a7e52-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a7e52-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7e52-121">從 hello 圖庫加入 Bynder</span><span class="sxs-lookup"><span data-stu-id="a7e52-121">Adding Bynder from hello gallery</span></span>
2. <span data-ttu-id="a7e52-122">設定並測試 Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="a7e52-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-hello-gallery"></a><span data-ttu-id="a7e52-123">從 hello 圖庫新增 Bynder</span><span class="sxs-lookup"><span data-stu-id="a7e52-123">Add Bynder from hello gallery</span></span>
<span data-ttu-id="a7e52-124">tooconfigure hello 整合 Bynder 到 Azure AD，您需要 tooadd Bynder hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7e52-124">tooconfigure hello integration of Bynder into Azure AD, you need tooadd Bynder from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a7e52-125">**tooadd Bynder 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a7e52-125">**tooadd Bynder from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7e52-126">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="a7e52-128">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="a7e52-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="a7e52-129">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="a7e52-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![應用程式][2]
4. <span data-ttu-id="a7e52-131">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="a7e52-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![應用程式][3]
5. <span data-ttu-id="a7e52-133">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![應用程式][4]
6. <span data-ttu-id="a7e52-135">在 [hello] 搜尋方塊中，輸入**Bynder**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-135">In hello search box, type **Bynder**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="a7e52-137">在 hello 結果 窗格中，選取  **Bynder**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7e52-137">In hello results panel, select **Bynder**, and then click **Complete** tooadd hello application.</span></span>
   
    ![選取在 hello 圖庫中的 hello 應用程式](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="a7e52-139">設定並測試 Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="a7e52-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="a7e52-140">hello 本節目標在於 tooshow 如何 tooconfigure 和測試 Microsoft Azure AD SSO 與 Bynder 根據稱為 「 許 Simon"的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a7e52-140">hello objective of this section is tooshow you how tooconfigure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a7e52-141">SSO toowork Azure AD 需要 tooknow Bynder tooan 使用者在 Azure AD 中哪些 hello 對等項目的使用者。</span><span class="sxs-lookup"><span data-stu-id="a7e52-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Bynder tooan user in Azure AD is.</span></span> <span data-ttu-id="a7e52-142">換句話說，Azure AD 使用者與 hello Bynder 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="a7e52-142">In other words, a link relationship between an Azure AD user and hello related user in Bynder needs toobe established.</span></span>

<span data-ttu-id="a7e52-143">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Bynder 中。</span><span class="sxs-lookup"><span data-stu-id="a7e52-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bynder.</span></span>

<span data-ttu-id="a7e52-144">tooconfigure 及測試 Bynder 與 Microsoft Azure AD 的 SSO，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="a7e52-144">tooconfigure and test Microsoft Azure AD SSO with Bynder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a7e52-145">**[設定 Microsoft Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="a7e52-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a7e52-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -Microsoft Azure AD 單一登入與許 Simon tootest。</span><span class="sxs-lookup"><span data-stu-id="a7e52-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="a7e52-147">**[建立測試使用者 Bynder](#creating-a-bynder-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Bynder 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="a7e52-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - toohave a counterpart of Britta Simon in Bynder that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="a7e52-148">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Microsoft Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a7e52-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="a7e52-149">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="a7e52-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="a7e52-150">設定 Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="a7e52-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="a7e52-151">在本節中，您將 hello 傳統入口網站中啟用 Microsoft Azure AD 的 SSO 和 Bynder 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="a7e52-151">In this section, you enable Microsoft Azure AD SSO in hello classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="a7e52-152">**tooconfigure Bynder，與 Microsoft Azure AD 的 SSO 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a7e52-152">**tooconfigure Microsoft Azure AD SSO with Bynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7e52-153">Hello 傳統入口網站中，在 hello **Bynder**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a7e52-153">In hello classic portal, on hello **Bynder** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![設定單一登入][6] 
2. <span data-ttu-id="a7e52-155">在 hello**如何想您使用者 toosign tooBynder 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-155">On hello **How would you like users toosign on tooBynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="a7e52-157">在 [hello**設定應用程式設定**對話方塊頁面上，如果您想 tooconfigure hello 應用程式中的**IDP 初始化模式**，執行下列步驟的 hello，然後按一下**下一步]**:</span><span class="sxs-lookup"><span data-stu-id="a7e52-157">On hello **Configure App Settings** dialog page, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps and click **Next**:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="a7e52-159">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="a7e52-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="a7e52-160">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a7e52-160">Click **Next**.</span></span>
4. <span data-ttu-id="a7e52-161">如果您想 tooconfigure hello 應用程式中的**SP 初始模式**上 hello**設定應用程式設定**對話方塊頁面上，然後按一下 [hello **[顯示進階設定 （選擇性）]**]，然後輸入 hello**登入 URL**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-161">If you wish tooconfigure hello application in **SP initiated mode** on hello **Configure App Settings** dialog page, then click on hello **“Show advanced settings (optional)”** and then enter hello **Sign On URL** and click **Next**.</span></span>

    ![設定單一登入](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="a7e52-163">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="a7e52-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="a7e52-164">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a7e52-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="a7e52-165">在此教學課程中的 hello 登入 URL 的 hello 值為只 placeholfer。</span><span class="sxs-lookup"><span data-stu-id="a7e52-165">hello value for hello Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="a7e52-166">tooget hello 實際的環境，請連絡 Bynder。</span><span class="sxs-lookup"><span data-stu-id="a7e52-166">tooget hello actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="a7e52-167">在 hello **Bynder 在設定單一登入**頁面上，執行下列步驟的 hello，按一下 **下一步**:</span><span class="sxs-lookup"><span data-stu-id="a7e52-167">On hello **Configure single sign-on at Bynder** page, perform hello following steps and click **Next**:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="a7e52-169">按一下**下載中繼資料**，然後儲存您的電腦上的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="a7e52-169">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="a7e52-170">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a7e52-170">Click **Next**.</span></span>
6. <span data-ttu-id="a7e52-171">tooget SSO 設定應用程式，請連絡您 Bynder 的支援團隊。</span><span class="sxs-lookup"><span data-stu-id="a7e52-171">tooget SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="a7e52-172">附加 hello 下載的中繼資料檔案，並分享 Bynder 小組 tooset 向上 SSO 邊。</span><span class="sxs-lookup"><span data-stu-id="a7e52-172">Attach hello downloaded metadata file and share it with Bynder team tooset up SSO on their side.</span></span>
7. <span data-ttu-id="a7e52-173">Hello 傳統入口網站中選取 hello 單一登入組態確認，然後**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD 單一登入][10]
8. <span data-ttu-id="a7e52-175">在 hello**單一登入確認**頁面上，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD 單一登入][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a7e52-177">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a7e52-177">Create an Azure AD test user</span></span>
<span data-ttu-id="a7e52-178">本節 hello 目標是 toocreate 測試使用者呼叫許 Simon hello 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="a7e52-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][20]

<span data-ttu-id="a7e52-180">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a7e52-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7e52-181">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="a7e52-183">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="a7e52-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="a7e52-184">toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="a7e52-186">tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="a7e52-188">在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a7e52-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="a7e52-190">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="a7e52-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="a7e52-191">在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="a7e52-192">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a7e52-192">Click **Next**.</span></span>
6. <span data-ttu-id="a7e52-193">在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a7e52-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="a7e52-195">在 hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="a7e52-196">在 hello**姓氏**文字方塊中，輸入， **Simon**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-196">In hello **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="a7e52-197">在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="a7e52-198">在 hello**角色**清單中，選取**使用者**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="a7e52-199">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a7e52-199">Click **Next**.</span></span>
7. <span data-ttu-id="a7e52-200">在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="a7e52-202">在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a7e52-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="a7e52-204">請記下 hello hello 值**新密碼**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-204">Write down hello value of hello **New Password**.</span></span>
   2. <span data-ttu-id="a7e52-205">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="a7e52-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="a7e52-206">建立 Bynder 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a7e52-206">Create a Bynder test user</span></span>
<span data-ttu-id="a7e52-207">hello 本節目標在於 toocreate Bynder 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="a7e52-207">hello objective of this section is toocreate a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="a7e52-208">Bynder 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="a7e52-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a7e52-209">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="a7e52-209">There is no action item for you in this section.</span></span> <span data-ttu-id="a7e52-210">如果尚未存在，將會嘗試 tooaccess Bynder 期間建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="a7e52-210">A new user will be created during an attempt tooaccess Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="a7e52-211">若要手動 toocreate 使用者，您會需要 toocontact hello Bynder 支援小組。</span><span class="sxs-lookup"><span data-stu-id="a7e52-211">If you need toocreate an user manually, you need toocontact hello Bynder support team.</span></span> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a7e52-212">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a7e52-212">Assign hello Azure AD test user</span></span>
<span data-ttu-id="a7e52-213">本節 hello 目標是授與他們存取 tooBynder tooenabling 許 Simon toouse Azure SSO。</span><span class="sxs-lookup"><span data-stu-id="a7e52-213">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooBynder.</span></span>

   ![指派使用者][200]

<span data-ttu-id="a7e52-215">**tooassign 許 Simon tooBynder，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a7e52-215">**tooassign Britta Simon tooBynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7e52-216">Hello 傳統入口網站，tooopen hello 應用程式] 檢視，在 hello 目錄檢視中，按一下 [**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="a7e52-216">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![指派使用者][201]
2. <span data-ttu-id="a7e52-218">在 [hello] 應用程式清單中，選取**Bynder**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-218">In hello applications list, select **Bynder**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="a7e52-220">在 hello 最上層顯示 hello 功能表上，按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-220">In hello menu on hello top, click **Users**.</span></span>
   
    ![指派使用者][203]
4. <span data-ttu-id="a7e52-222">在 hello 使用者清單中選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-222">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="a7e52-223">在 hello hello 底部的工具列中按一下**指派**。</span><span class="sxs-lookup"><span data-stu-id="a7e52-223">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![指派使用者][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="a7e52-225">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a7e52-225">Test single sign-on</span></span>
<span data-ttu-id="a7e52-226">hello 本節目標在於 tootest 您 Microsoft Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="a7e52-226">hello objective of this section is tootest your Microsoft Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="a7e52-227">當您按一下 hello Bynder 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Bynder 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7e52-227">When you click hello Bynder tile in hello Access Panel, you should get automatically signed-on tooyour Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a7e52-228">其他資源</span><span class="sxs-lookup"><span data-stu-id="a7e52-228">Additional resources</span></span>
* [<span data-ttu-id="a7e52-229">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7e52-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7e52-230">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a7e52-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
