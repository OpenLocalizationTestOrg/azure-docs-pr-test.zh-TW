---
title: "教學課程：Azure Active Directory 與 SilkRoad Life Suite 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 SilkRoad 生命套件之間。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="d982f-103">教學課程：Azure Active Directory 與 SilkRoad Life Suite 整合</span><span class="sxs-lookup"><span data-stu-id="d982f-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="d982f-104">本教學課程的 hello 目標是 tooshow 您如何 toointegrate SilkRoad 生命 Suite 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d982f-104">hello objective of this tutorial is tooshow you how toointegrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="d982f-105">與 Azure AD 整合 SilkRoad 生命套件可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="d982f-105">Integrating SilkRoad Life Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="d982f-106">您可以控制存取 tooSilkRoad 生命套件的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="d982f-106">You can control in Azure AD who has access tooSilkRoad Life Suite</span></span> 
* <span data-ttu-id="d982f-107">您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooSilkRoad 生命套件單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="d982f-107">You can enable your users tooautomatically get signed-on tooSilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="d982f-108">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d982f-108">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d982f-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="d982f-109">Prerequisites</span></span>
<span data-ttu-id="d982f-110">tooconfigure SilkRoad 生命 Suite 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="d982f-110">tooconfigure Azure AD integration with SilkRoad Life Suite, you need hello following items:</span></span>

* <span data-ttu-id="d982f-111">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d982f-111">An Azure AD subscription</span></span>
* <span data-ttu-id="d982f-112">已啟用 SilkRoad Life Suite SSO 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d982f-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="d982f-113">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="d982f-113">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="d982f-114">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d982f-114">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="d982f-115">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="d982f-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="d982f-116">如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="d982f-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="d982f-117">案例描述</span><span class="sxs-lookup"><span data-stu-id="d982f-117">Scenario Description</span></span>
<span data-ttu-id="d982f-118">本教學課程的 hello 目標是 tooenable 您 tootest Azure AD 的 SSO 在測試環境中。</span><span class="sxs-lookup"><span data-stu-id="d982f-118">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="d982f-119">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="d982f-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d982f-120">從 hello 圖庫加入 SilkRoad 生命套件</span><span class="sxs-lookup"><span data-stu-id="d982f-120">Adding SilkRoad Life Suite from hello gallery</span></span> 
2. <span data-ttu-id="d982f-121">設定並測試 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d982f-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-hello-gallery"></a><span data-ttu-id="d982f-122">從 hello 圖庫加入 SilkRoad 生命套件</span><span class="sxs-lookup"><span data-stu-id="d982f-122">Add SilkRoad Life Suite from hello gallery</span></span>
<span data-ttu-id="d982f-123">tooconfigure hello 整合 SilkRoad 生命套件到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd SilkRoad 生命套件。</span><span class="sxs-lookup"><span data-stu-id="d982f-123">tooconfigure hello integration of SilkRoad Life Suite into Azure AD, you need tooadd SilkRoad Life Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d982f-124">**tooadd SilkRoad 生命套件從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d982f-124">**tooadd SilkRoad Life Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d982f-125">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="d982f-125">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="d982f-127">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="d982f-127">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="d982f-128">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="d982f-128">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![應用程式][2]

4. <span data-ttu-id="d982f-130">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="d982f-130">Click **Add** at hello bottom of hello page.</span></span>
   
    ![應用程式][3]

5. <span data-ttu-id="d982f-132">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d982f-132">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![應用程式][4]

6. <span data-ttu-id="d982f-134">在 [hello] 搜尋方塊中，輸入**SilkRoad 生命套件**。</span><span class="sxs-lookup"><span data-stu-id="d982f-134">In hello search box, type **SilkRoad Life Suite**.</span></span>
   
    ![應用程式][5]

7. <span data-ttu-id="d982f-136">在 hello 結果窗格中，選取  **SilkRoad 生命套件**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d982f-136">In hello results pane, select **SilkRoad Life Suite**, and then click **Complete** tooadd hello application.</span></span>
   
    ![應用程式][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d982f-138">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d982f-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d982f-139">hello 本節目標在於 tooshow 如何 tooconfigure 和測試 Azure AD SSO 與 SilkRoad 生命套件根據稱為 「 許 Simon"的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d982f-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d982f-140">SSO toowork Azure AD 需要 tooknow SilkRoad 生命套件 tooan 使用者在 Azure AD 中哪些 hello 對等項目的使用者。</span><span class="sxs-lookup"><span data-stu-id="d982f-140">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SilkRoad Life Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="d982f-141">換句話說，Azure AD 使用者與 hello SilkRoad 生命套件中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="d982f-141">In other words, a link relationship between an Azure AD user and hello related user in SilkRoad Life Suite needs toobe established.</span></span>

<span data-ttu-id="d982f-142">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** SilkRoad 生命套件中。</span><span class="sxs-lookup"><span data-stu-id="d982f-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="d982f-143">tooconfigure 及 SilkRoad 生命 Suite 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="d982f-143">tooconfigure and test Azure AD single sign-on with SilkRoad Life Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d982f-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="d982f-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d982f-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="d982f-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d982f-146">**[建立 SilkRoad 生命套件的測試使用者](#creating-a-silkroad-life-suite-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 SilkRoad 生命套件中的對應項目。</span><span class="sxs-lookup"><span data-stu-id="d982f-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - toohave a counterpart of Britta Simon in SilkRoad Life Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="d982f-147">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d982f-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d982f-148">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="d982f-148">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d982f-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d982f-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="d982f-150">本節 hello 目標是 hello Azure 傳統入口網站中的 Azure AD 的 SSO tooenable 和 tooconfigure SSO SilkRoad 生命 Suite 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="d982f-150">hello objective of this section is tooenable Azure AD SSO in hello Azure classic portal and tooconfigure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="d982f-151">**利用 SilkRoad 生命 Suite，Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d982f-151">**tooconfigure Azure AD single sign-on with SilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="d982f-152">以系統管理員身分登入 tooyour SilkRoad 公司網站。</span><span class="sxs-lookup"><span data-stu-id="d982f-152">Sign-on tooyour SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="d982f-153">tooobtain 存取 toohello SilkRoad 生命套件驗證應用程式中設定同盟時與 Microsoft Azure AD，請連絡 SilkRoad 支援或 SilkRoad 服務人員。</span><span class="sxs-lookup"><span data-stu-id="d982f-153">tooobtain access toohello SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="d982f-154">跳過**服務提供者**，然後按一下**同盟的詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="d982f-154">Go too**Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Azure AD 單一登入][10] 

3. <span data-ttu-id="d982f-156">按一下**下載同盟中繼資料**，然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="d982f-156">Click **Download Federation Metadata**, and then save hello metadata file on your computer.</span></span>
   
    ![Azure AD 單一登入][11] 

4. <span data-ttu-id="d982f-158">在 Azure 傳統入口網站，在 hello hello **SilkRoad 生命套件**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d982f-158">In hello Azure classic portal, on hello **SilkRoad Life Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![設定單一登入][6] 

5. <span data-ttu-id="d982f-160">Hello 上**如何想您 tooSilkRoad 生命套件上的使用者 toosign**頁面上，選取**Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="d982f-160">On hello **How would you like users toosign on tooSilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD 單一登入][7] 

6. <span data-ttu-id="d982f-162">在 hello**設定應用程式設定**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d982f-162">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD 單一登入][8]   
 1. <span data-ttu-id="d982f-164">在 hello**登入 URL**文字方塊中，使用者 toosign 上 tooyour SilkRoad 生命套件站台所使用的型別 hello URL (例如： *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*)。</span><span class="sxs-lookup"><span data-stu-id="d982f-164">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="d982f-165">開啟下載的 hello **Silkroad**中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="d982f-165">Open hello downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="d982f-166">找出 hello **AssertionConsumerService**標記，然後再複製 hello**位置**屬性。</span><span class="sxs-lookup"><span data-stu-id="d982f-166">Locate hello **AssertionConsumerService** tag, and then copy hello **Location** attribute.</span></span>         
   
    ![Azure AD 單一登入][21] 
 4. <span data-ttu-id="d982f-168">Hello 值貼到 hello**回覆 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="d982f-168">Paste hello value into hello **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="d982f-169">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d982f-169">Click **Next**.</span></span>

6. <span data-ttu-id="d982f-170">在 hello **SilkRoad 生命套件在設定單一登入**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d982f-170">On hello **Configure single sign-on at SilkRoad Life Suite** page, perform hello following steps:</span></span>
   
    ![Azure AD 單一登入][9]  
 1. <span data-ttu-id="d982f-172">按一下 下載憑證，然後儲存您的電腦上的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="d982f-172">Click Download certificate, and then save hello file on your computer.</span></span>  
 2. <span data-ttu-id="d982f-173">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d982f-173">Click **Next**.</span></span>

7. <span data-ttu-id="d982f-174">在您的 **SilkRoad** 應用程式中，按一下 [驗證來源]。</span><span class="sxs-lookup"><span data-stu-id="d982f-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Azure AD 單一登入][12] 

8. <span data-ttu-id="d982f-176">按一下 [加入驗證來源] 。</span><span class="sxs-lookup"><span data-stu-id="d982f-176">Click **Add Authentication Source**.</span></span> 
   
    ![Azure AD 單一登入][13] 

9. <span data-ttu-id="d982f-178">在 hello**加入驗證來源**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d982f-178">In hello **Add Authentication Source** section, perform hello following steps:</span></span> 
   
    ![Azure AD 單一登入][14]  
 1. <span data-ttu-id="d982f-180">在下**選項 2-中繼資料檔案**，按一下 **瀏覽**tooupload hello 下載中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="d982f-180">Under **Option 2 - Metadata File**, click **Browse** tooupload hello downloaded metadata file.</span></span>  
 2. <span data-ttu-id="d982f-181">按一下 [使用檔案資料建立身分識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="d982f-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="d982f-182">在 hello**驗證來源**區段中，按一下**編輯**。</span><span class="sxs-lookup"><span data-stu-id="d982f-182">In hello **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Azure AD 單一登入][15] 

11. <span data-ttu-id="d982f-184">在 [hello**編輯驗證來源**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d982f-184">On hello **Edit Authentication Source** dialog, perform hello following steps:</span></span> 
    
     ![Azure AD 單一登入][16] 
 1. <span data-ttu-id="d982f-186">對 [已啟用] 選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="d982f-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="d982f-187">在 hello **IdP 描述**文字方塊中，輸入您的組態的描述 (例如： *Azure AD 的 SSO*)。</span><span class="sxs-lookup"><span data-stu-id="d982f-187">In hello **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="d982f-188">在 hello **IdP 名稱**文字方塊中，輸入特定 tooyour 組態的名稱 (例如： *Azure SP*)。</span><span class="sxs-lookup"><span data-stu-id="d982f-188">In hello **IdP Name** textbox, type a name that is specific tooyour configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="d982f-189">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="d982f-189">Click **Save**.</span></span>

12. <span data-ttu-id="d982f-190">停用所有其他驗證來源。</span><span class="sxs-lookup"><span data-stu-id="d982f-190">Disable all other authentication sources.</span></span> 
    
     ![Azure AD 單一登入][17]

13. <span data-ttu-id="d982f-192">在 Azure 傳統入口網站，在 hello hello**單一登入確認**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="d982f-192">In hello Azure classic portal, on hello **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Azure AD 單一登入][18]

14. <span data-ttu-id="d982f-194">在 hello**單一登入確認**頁面上，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="d982f-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Azure AD 單一登入][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d982f-196">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d982f-196">Create an Azure AD test user</span></span>
<span data-ttu-id="d982f-197">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 傳統入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d982f-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][20]

<span data-ttu-id="d982f-199">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d982f-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d982f-200">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="d982f-200">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="d982f-202">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="d982f-202">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="d982f-203">toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="d982f-203">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d982f-205">tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="d982f-205">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="d982f-207">在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d982f-207">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="d982f-209">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="d982f-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="d982f-210">在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d982f-210">In hello User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="d982f-211">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d982f-211">Click **Next**.</span></span>

6. <span data-ttu-id="d982f-212">在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d982f-212">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="d982f-214">在 hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="d982f-214">In hello **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="d982f-215">在 hello**姓氏**文字方塊中，輸入， **Simon**。</span><span class="sxs-lookup"><span data-stu-id="d982f-215">In hello **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="d982f-216">在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="d982f-216">In hello **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="d982f-217">在 hello**角色**清單中，選取**使用者**。</span><span class="sxs-lookup"><span data-stu-id="d982f-217">In hello **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="d982f-218">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d982f-218">Click **Next**.</span></span>

7. <span data-ttu-id="d982f-219">在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="d982f-219">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="d982f-221">在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d982f-221">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="d982f-223">請記下 hello hello 值**新密碼**。</span><span class="sxs-lookup"><span data-stu-id="d982f-223">Write down hello value of hello **New Password**.</span></span> 
 2. <span data-ttu-id="d982f-224">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="d982f-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="d982f-225">建立 SilkRoad Life Suite 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d982f-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="d982f-226">hello 本節目標在於 toocreate 呼叫許 Simon SilkRoad 生命套件中的使用者。</span><span class="sxs-lookup"><span data-stu-id="d982f-226">hello objective of this section is toocreate a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="d982f-227">許的必須具有 SSO 識別碼 (有時稱為 tooas *AuthParam*) 符合許的**emailaddress**在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="d982f-227">Britta's must have an SSO ID (sometimes referred tooas an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="d982f-228">**toocreate 呼叫許 Simon SilkRoad 生命套件中的使用者執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d982f-228">**toocreate a user called Britta Simon in SilkRoad Life Suite, perform hello following steps:**</span></span>

- <span data-ttu-id="d982f-229">詢問使用者，其具有與您 SilkRoad 生命套件支援小組 toocreate **SSO 識別碼**屬性 hello 相同的值為 hello **emailaddress**許 Simon 在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="d982f-229">Ask your SilkRoad Life Suite support team toocreate a user that has as **SSO ID** attribute hello same value as hello **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d982f-230">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d982f-230">Assign hello Azure AD test user</span></span>
<span data-ttu-id="d982f-231">本節 hello 目標是 tooenable 許 Simon toouse Azure SSO 授與他們存取 tooSilkRoad 生命套件。</span><span class="sxs-lookup"><span data-stu-id="d982f-231">hello objective of this section is tooenable Britta Simon toouse Azure SSO by granting her access tooSilkRoad Life Suite.</span></span>

![指派使用者][200] 

<span data-ttu-id="d982f-233">**tooassign 許 Simon tooSilkRoad 生命套件時，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d982f-233">**tooassign Britta Simon tooSilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="d982f-234">在 hello Azure 傳統入口網站，tooopen hello 應用程式 檢視，在 hello 目錄檢視中，按一下 **應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="d982f-234">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![指派使用者][201] 

2. <span data-ttu-id="d982f-236">在 [hello] 應用程式清單中，選取**SilkRoad 生命套件**。</span><span class="sxs-lookup"><span data-stu-id="d982f-236">In hello applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![指派使用者][202] 

3. <span data-ttu-id="d982f-238">在 hello 最上層顯示 hello 功能表上，按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="d982f-238">In hello menu on hello top, click **Users**.</span></span>
   
    ![指派使用者][203] 

4. <span data-ttu-id="d982f-240">在 hello 使用者清單中選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="d982f-240">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="d982f-241">在 hello hello 底部的工具列中按一下**指派**。</span><span class="sxs-lookup"><span data-stu-id="d982f-241">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![指派使用者][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="d982f-243">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d982f-243">Test single sign-on</span></span>
<span data-ttu-id="d982f-244">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="d982f-244">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="d982f-245">當您按一下 hello SilkRoad 生命套件磚 hello 存取面板中的時，您應該取得自動登入 tooyour SilkRoad 生命 Suite 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d982f-245">When you click hello SilkRoad Life Suite tile in hello Access Panel, you should get automatically signed-on tooyour SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d982f-246">其他資源</span><span class="sxs-lookup"><span data-stu-id="d982f-246">Additional Resources</span></span>
* [<span data-ttu-id="d982f-247">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d982f-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d982f-248">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d982f-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





