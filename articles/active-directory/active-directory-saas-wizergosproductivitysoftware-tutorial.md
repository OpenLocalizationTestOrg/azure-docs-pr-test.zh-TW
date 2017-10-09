---
title: "教學課程：Azure Active Directory 與 Wizergos Productivity Software 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Wizergos 生產力軟體之間。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="54d85-103">教學課程：Azure Active Directory 與 Wizergos Productivity Software 整合</span><span class="sxs-lookup"><span data-stu-id="54d85-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="54d85-104">本教學課程的 hello 目標是 tooshow 您如何 toointegrate Wizergos 生產力軟體與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="54d85-104">hello objective of this tutorial is tooshow you how toointegrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="54d85-105">與 Azure AD 整合 Wizergos 生產力軟體可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="54d85-105">Integrating Wizergos Productivity Software with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="54d85-106">您可以控制存取 tooWizergos 生產力軟體的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="54d85-106">You can control in Azure AD who has access tooWizergos Productivity Software</span></span>
* <span data-ttu-id="54d85-107">您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooWizergos 生產力軟體單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="54d85-107">You can enable your users tooautomatically get signed-on tooWizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="54d85-108">您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="54d85-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="54d85-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="54d85-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54d85-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="54d85-110">Prerequisites</span></span>
<span data-ttu-id="54d85-111">tooconfigure Wizergos 生產力軟體與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="54d85-111">tooconfigure Azure AD integration with Wizergos Productivity Software, you need hello following items:</span></span>

* <span data-ttu-id="54d85-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="54d85-112">An Azure AD subscription</span></span>
* <span data-ttu-id="54d85-113">啟用 Wizergos Productivity Software SSO 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="54d85-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="54d85-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="54d85-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="54d85-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="54d85-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="54d85-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="54d85-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="54d85-117">如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="54d85-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="54d85-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="54d85-118">Scenario description</span></span>
<span data-ttu-id="54d85-119">本教學課程的 hello 目標是 tooenable 您 tootest Azure AD 的 SSO 在測試環境中。</span><span class="sxs-lookup"><span data-stu-id="54d85-119">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="54d85-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="54d85-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="54d85-121">從 hello 圖庫加入 Wizergos 生產力軟體</span><span class="sxs-lookup"><span data-stu-id="54d85-121">Adding Wizergos Productivity Software from hello gallery</span></span>
2. <span data-ttu-id="54d85-122">設定並測試 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="54d85-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a><span data-ttu-id="54d85-123">從 hello 圖庫加入 Wizergos 生產力軟體</span><span class="sxs-lookup"><span data-stu-id="54d85-123">Adding Wizergos Productivity Software from hello gallery</span></span>
<span data-ttu-id="54d85-124">tooconfigure hello 整合 Wizergos 生產力軟體到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Wizergos 生產力軟體。</span><span class="sxs-lookup"><span data-stu-id="54d85-124">tooconfigure hello integration of Wizergos Productivity Software into Azure AD, you need tooadd Wizergos Productivity Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="54d85-125">**tooadd Wizergos 生產力軟體從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="54d85-125">**tooadd Wizergos Productivity Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="54d85-126">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="54d85-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="54d85-128">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="54d85-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="54d85-129">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="54d85-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![應用程式][2]
4. <span data-ttu-id="54d85-131">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="54d85-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![應用程式][3]
5. <span data-ttu-id="54d85-133">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="54d85-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![應用程式][4]
6. <span data-ttu-id="54d85-135">在 [hello] 搜尋方塊中，輸入**Wizergos 生產力軟體**。</span><span class="sxs-lookup"><span data-stu-id="54d85-135">In hello search box, type **Wizergos Productivity Software**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="54d85-137">在 hello 結果 窗格中，選取  **Wizergos 生產力軟體**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="54d85-137">In hello results panel, select **Wizergos Productivity Software**, and then click **Complete** tooadd hello application.</span></span>
   
    ![選取在 hello 圖庫中的 hello 應用程式](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="54d85-139">設定並測試 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="54d85-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="54d85-140">hello 本節目標在於 tooshow 如何 tooconfigure 和測試 Azure AD SSO Wizergos 生產力軟體根據稱為 「 許 Simon"的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="54d85-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="54d85-141">SSO toowork Azure AD 需要 tooknow Wizergos 生產力軟體 tooan 使用者在 Azure AD 中哪些 hello 對等項目的使用者。</span><span class="sxs-lookup"><span data-stu-id="54d85-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Wizergos Productivity Software tooan user in Azure AD is.</span></span> <span data-ttu-id="54d85-142">換句話說，Azure AD 使用者與 hello Wizergos 生產力軟體中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="54d85-142">In other words, a link relationship between an Azure AD user and hello related user in Wizergos Productivity Software needs toobe established.</span></span>

<span data-ttu-id="54d85-143">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Wizergos 生產力軟體中。</span><span class="sxs-lookup"><span data-stu-id="54d85-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="54d85-144">tooconfigure 及 BynWizergos 產能 Softwareder 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="54d85-144">tooconfigure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="54d85-145">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="54d85-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="54d85-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="54d85-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="54d85-147">**[建立 Wizergos 生產力軟體測試使用者](#creating-a-wizergos-productivity-software-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Wizergos 生產力軟體中對應項目。</span><span class="sxs-lookup"><span data-stu-id="54d85-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - toohave a counterpart of Britta Simon in Wizergos Productivity Software that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="54d85-148">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="54d85-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="54d85-149">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="54d85-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="54d85-150">設定 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="54d85-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="54d85-151">在本節中，您可以啟用 Azure AD 單一登入 hello 傳統入口網站中，並 Wizergos 生產力軟體應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="54d85-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="54d85-152">**tooconfigure Azure AD 單一登入 Wizergos 生產力軟體，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="54d85-152">**tooconfigure Azure AD single sign-on with Wizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="54d85-153">Hello 傳統入口網站中，在 hello **Wizergos 生產力軟體**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="54d85-153">In hello classic portal, on hello **Wizergos Productivity Software** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![設定單一登入][6] 
2. <span data-ttu-id="54d85-155">在 hello**如何想您使用者 toosign tooWizergos 生產力軟體上**頁面上，選取**Azure AD 單一登入**，然後按一下**下一步**:</span><span class="sxs-lookup"><span data-stu-id="54d85-155">On hello **How would you like users toosign on tooWizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="54d85-157">在 hello**設定應用程式設定**對話方塊頁面上，按一下 **下一步**:</span><span class="sxs-lookup"><span data-stu-id="54d85-157">On hello **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="54d85-159">在 hello**於 Wizergos 產能 Software 設定單一登入**頁面上，按一下**下載憑證**，然後儲存您的電腦上的 hello 檔案：</span><span class="sxs-lookup"><span data-stu-id="54d85-159">On hello **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save hello file on your computer:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="54d85-161">在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour Wizergos 生產力軟體租用戶。</span><span class="sxs-lookup"><span data-stu-id="54d85-161">In a different web browser window, sign-on tooyour Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="54d85-162">從 hello 漢堡功能表上，選取**Admin**。</span><span class="sxs-lookup"><span data-stu-id="54d85-162">From hello hamburger menu, select **Admin**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="54d85-164">在 [系統管理] 頁面左側的功能表中，選取 [驗證]，然後按一下 [Azure AD]。</span><span class="sxs-lookup"><span data-stu-id="54d85-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="54d85-166">執行下列步驟 hello**驗證**> 一節。</span><span class="sxs-lookup"><span data-stu-id="54d85-166">Perform hello following steps on **AUTHENTICATION** section.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="54d85-168">按一下**上傳**按鈕 tooupload hello Azure AD 從下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="54d85-168">Click **UPLOAD** button tooupload hello downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="54d85-169">在 hello**簽發者 URL**文字方塊放 hello 值**簽發者 URL**從 Azure AD 應用程式組態精靈。</span><span class="sxs-lookup"><span data-stu-id="54d85-169">In hello **Issuer URL** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="54d85-170">在 hello**單一登入 URL**文字方塊放 hello 值**單一登入服務 URL**從 Azure AD 應用程式組態精靈。</span><span class="sxs-lookup"><span data-stu-id="54d85-170">In hello **Single Sign-On URL** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="54d85-171">在 hello**單一登出 URL**文字方塊放 hello 值**單一登出服務 URL**從 Azure AD 應用程式組態精靈。</span><span class="sxs-lookup"><span data-stu-id="54d85-171">In hello **Single Sign-Out URL** textbox put hello value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="54d85-172">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="54d85-172">Click **Save** button.</span></span>
9. <span data-ttu-id="54d85-173">Hello 傳統入口網站中選取 hello 單一登入組態確認，然後**下一步**。</span><span class="sxs-lookup"><span data-stu-id="54d85-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD 單一登入][10]
10. <span data-ttu-id="54d85-175">在 hello**單一登入確認**頁面上，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="54d85-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD 單一登入][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="54d85-177">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="54d85-177">Create an Azure AD test user</span></span>
<span data-ttu-id="54d85-178">本節 hello 目標是 toocreate 測試使用者呼叫許 Simon hello 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="54d85-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][20]

<span data-ttu-id="54d85-180">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="54d85-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="54d85-181">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="54d85-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="54d85-183">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="54d85-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="54d85-184">toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="54d85-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="54d85-186">tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="54d85-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="54d85-188">在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="54d85-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="54d85-190">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="54d85-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="54d85-191">在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="54d85-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="54d85-192">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="54d85-192">Click **Next**.</span></span>
6. <span data-ttu-id="54d85-193">在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="54d85-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="54d85-195">在 hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="54d85-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="54d85-196">在 hello**姓氏**文字方塊中，輸入， **Simon**。</span><span class="sxs-lookup"><span data-stu-id="54d85-196">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="54d85-197">在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="54d85-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="54d85-198">在 hello**角色**清單中，選取**使用者**。</span><span class="sxs-lookup"><span data-stu-id="54d85-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="54d85-199">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="54d85-199">Click **Next**.</span></span>
7. <span data-ttu-id="54d85-200">在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="54d85-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="54d85-202">在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="54d85-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="54d85-204">請記下 hello hello 值**新密碼**。</span><span class="sxs-lookup"><span data-stu-id="54d85-204">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="54d85-205">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="54d85-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="54d85-206">建立 Wizergos Productivity Software 測試使用者</span><span class="sxs-lookup"><span data-stu-id="54d85-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="54d85-207">在本節中，您要在 Wizergos Productivity Software 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="54d85-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="54d85-208">請使用透過 Wizergos 生產力軟體支援小組[ support@wizergos.com ](emailTo:support@wizergos.com) tooadd hello hello Wizergos 生產力軟體平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="54d85-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) tooadd hello users in hello Wizergos Productivity Software platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="54d85-209">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="54d85-209">Assign hello Azure AD test user</span></span>
<span data-ttu-id="54d85-210">本節 hello 目標是 tooenabling 許 Simon toouse Azure SSO 授與他們存取 tooWizergos 生產力軟體。</span><span class="sxs-lookup"><span data-stu-id="54d85-210">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooWizergos Productivity Software.</span></span>

  ![指派使用者][200]

<span data-ttu-id="54d85-212">**tooassign 許 Simon tooWizergos 生產力軟體，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="54d85-212">**tooassign Britta Simon tooWizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="54d85-213">Hello 傳統入口網站，tooopen hello 應用程式] 檢視，在 hello 目錄檢視中，按一下 [**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="54d85-213">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![指派使用者][201]
2. <span data-ttu-id="54d85-215">在 [hello] 應用程式清單中，選取**Wizergos 生產力軟體**。</span><span class="sxs-lookup"><span data-stu-id="54d85-215">In hello applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="54d85-217">在 hello 最上層顯示 hello 功能表上，按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="54d85-217">In hello menu on hello top, click **Users**.</span></span>
   
    ![指派使用者][203]
4. <span data-ttu-id="54d85-219">在 hello 使用者清單中選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="54d85-219">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="54d85-220">在 hello hello 底部的工具列中按一下**指派**。</span><span class="sxs-lookup"><span data-stu-id="54d85-220">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![指派使用者][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="54d85-222">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="54d85-222">Test single sign-on</span></span>
<span data-ttu-id="54d85-223">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="54d85-223">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="54d85-224">當您按一下 hello Wizergos 生產力軟體磚 hello 存取面板中的時，您應該取得自動登入 tooyour Wizergos 生產力軟體應用程式。</span><span class="sxs-lookup"><span data-stu-id="54d85-224">When you click hello Wizergos Productivity Software tile in hello Access Panel, you should get automatically signed-on tooyour Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="54d85-225">其他資源</span><span class="sxs-lookup"><span data-stu-id="54d85-225">Additional resources</span></span>
* [<span data-ttu-id="54d85-226">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54d85-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="54d85-227">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="54d85-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
