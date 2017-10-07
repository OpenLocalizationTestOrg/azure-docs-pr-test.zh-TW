---
title: "教學課程：Azure Active Directory 與 AirWatch 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 AirWatch 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="ee30b-103">教學課程：Azure Active Directory 與 AirWatch 整合</span><span class="sxs-lookup"><span data-stu-id="ee30b-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="ee30b-104">在此教學課程中，您學會如何 toointegrate AirWatch 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="ee30b-104">In this tutorial, you learn how toointegrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ee30b-105">與 Azure AD 整合 AirWatch 可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee30b-105">Integrating AirWatch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ee30b-106">您可以控制存取 tooAirWatch Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="ee30b-106">You can control in Azure AD who has access tooAirWatch</span></span>
- <span data-ttu-id="ee30b-107">您可以啟用您的使用者 tooautomatically get 登入 tooAirWatch （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="ee30b-107">You can enable your users tooautomatically get signed-on tooAirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ee30b-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ee30b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ee30b-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ee30b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee30b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ee30b-110">Prerequisites</span></span>

<span data-ttu-id="ee30b-111">tooconfigure 與 AirWatch 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="ee30b-111">tooconfigure Azure AD integration with AirWatch, you need hello following items:</span></span>

- <span data-ttu-id="ee30b-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ee30b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ee30b-113">啟用 AirWatch 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ee30b-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ee30b-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="ee30b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ee30b-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ee30b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ee30b-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ee30b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ee30b-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ee30b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ee30b-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ee30b-118">Scenario description</span></span>
<span data-ttu-id="ee30b-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ee30b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ee30b-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="ee30b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ee30b-121">從 hello 圖庫加入 AirWatch</span><span class="sxs-lookup"><span data-stu-id="ee30b-121">Adding AirWatch from hello gallery</span></span>
2. <span data-ttu-id="ee30b-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ee30b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-hello-gallery"></a><span data-ttu-id="ee30b-123">從 hello 圖庫加入 AirWatch</span><span class="sxs-lookup"><span data-stu-id="ee30b-123">Adding AirWatch from hello gallery</span></span>
<span data-ttu-id="ee30b-124">tooconfigure hello 整合 AirWatch 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd AirWatch。</span><span class="sxs-lookup"><span data-stu-id="ee30b-124">tooconfigure hello integration of AirWatch into Azure AD, you need tooadd AirWatch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ee30b-125">**tooadd AirWatch 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ee30b-125">**tooadd AirWatch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee30b-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="ee30b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ee30b-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ee30b-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ee30b-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="ee30b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ee30b-133">在 [hello] 搜尋方塊中，輸入**AirWatch**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-133">In hello search box, type **AirWatch**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="ee30b-135">在 hello 結果 窗格中，選取  **AirWatch**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee30b-135">In hello results panel, select **AirWatch**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ee30b-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ee30b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ee30b-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 AirWatch 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ee30b-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ee30b-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 AirWatch 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="ee30b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AirWatch is tooa user in Azure AD.</span></span> <span data-ttu-id="ee30b-140">換句話說，Azure AD 使用者與 hello AirWatch 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="ee30b-140">In other words, a link relationship between an Azure AD user and hello related user in AirWatch needs toobe established.</span></span>

<span data-ttu-id="ee30b-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** AirWatch 中。</span><span class="sxs-lookup"><span data-stu-id="ee30b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in AirWatch.</span></span>

<span data-ttu-id="ee30b-142">tooconfigure 及測試 Azure AD 單一登入 AirWatch，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="ee30b-142">tooconfigure and test Azure AD single sign-on with AirWatch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ee30b-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="ee30b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ee30b-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="ee30b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ee30b-145">**[建立測試使用者 AirWatch](#creating-a-airwatch-test-user)**  -toohave 許 Simon AirWatch 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="ee30b-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - toohave a counterpart of Britta Simon in AirWatch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ee30b-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ee30b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ee30b-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="ee30b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ee30b-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ee30b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ee30b-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 AirWatch 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="ee30b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="ee30b-150">**tooconfigure Azure AD 單一登入 AirWatch 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ee30b-150">**tooconfigure Azure AD single sign-on with AirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee30b-151">在 Azure 入口網站上 hello hello **AirWatch**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-151">In hello Azure portal, on hello **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ee30b-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ee30b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="ee30b-155">在 hello **AirWatch 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee30b-155">On hello **AirWatch Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="ee30b-157">a.</span><span class="sxs-lookup"><span data-stu-id="ee30b-157">a.</span></span> <span data-ttu-id="ee30b-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="ee30b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="ee30b-159">b.</span><span class="sxs-lookup"><span data-stu-id="ee30b-159">b.</span></span> <span data-ttu-id="ee30b-160">在 hello**識別碼**文字方塊中，做為型別 hello 值`AirWatch`</span><span class="sxs-lookup"><span data-stu-id="ee30b-160">In hello **Identifier** textbox, type hello value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ee30b-161">這個值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="ee30b-161">This value is not hello real.</span></span> <span data-ttu-id="ee30b-162">更新此值與 hello 實際登入 URL。</span><span class="sxs-lookup"><span data-stu-id="ee30b-162">Update this value with hello actual Sign-on URL.</span></span> <span data-ttu-id="ee30b-163">請連絡[AirWatch 用戶端支援小組](http://www.air-watch.com/company/contact-us/)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="ee30b-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) tooget this value.</span></span> 
 
4. <span data-ttu-id="ee30b-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee30b-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="ee30b-166">在 hello **AirWatch 組態**區段中，按一下**設定 AirWatch** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="ee30b-166">On hello **AirWatch Configuration** section, click **Configure AirWatch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ee30b-167">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="ee30b-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="ee30b-169">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ee30b-169">Click **Save** button.</span></span>

    <span data-ttu-id="ee30b-170">![設定單一登入](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="ee30b-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="ee30b-171">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour AirWatch 公司網站。</span><span class="sxs-lookup"><span data-stu-id="ee30b-171">In a different web browser window, log in tooyour AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="ee30b-172">Hello 左側瀏覽窗格中，按一下**帳戶**，然後按一下**管理員**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-172">In hello left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="ee30b-173">![系統管理員](./media/active-directory-saas-airwatch-tutorial/ic791920.png "系統管理員")</span><span class="sxs-lookup"><span data-stu-id="ee30b-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="ee30b-174">展開 hello**設定**功能表，然後再按一下**目錄服務**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-174">Expand hello **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="ee30b-175">![設定](./media/active-directory-saas-airwatch-tutorial/ic791921.png "設定")</span><span class="sxs-lookup"><span data-stu-id="ee30b-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="ee30b-176">按一下 hello**使用者**索引標籤上，在 hello**基本 DN**文字方塊中，輸入您的網域名稱，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-176">Click hello **User** tab, in hello **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="ee30b-177">![使用者](./media/active-directory-saas-airwatch-tutorial/ic791922.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="ee30b-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="ee30b-178">按一下 hello**伺服器** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ee30b-178">Click hello **Server** tab.</span></span>
   
   <span data-ttu-id="ee30b-179">![伺服器](./media/active-directory-saas-airwatch-tutorial/ic791923.png "伺服器")</span><span class="sxs-lookup"><span data-stu-id="ee30b-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="ee30b-180">執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee30b-180">Perform hello following steps:</span></span>
    
    <span data-ttu-id="ee30b-181">![上傳](./media/active-directory-saas-airwatch-tutorial/ic791924.png "上傳")</span><span class="sxs-lookup"><span data-stu-id="ee30b-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="ee30b-182">a.</span><span class="sxs-lookup"><span data-stu-id="ee30b-182">a.</span></span> <span data-ttu-id="ee30b-183">針對 [目錄類型]，選取 [無]。</span><span class="sxs-lookup"><span data-stu-id="ee30b-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="ee30b-184">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee30b-184">b.</span></span> <span data-ttu-id="ee30b-185">選取 [使用 SAML 進行驗證] 。</span><span class="sxs-lookup"><span data-stu-id="ee30b-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="ee30b-186">c.</span><span class="sxs-lookup"><span data-stu-id="ee30b-186">c.</span></span> <span data-ttu-id="ee30b-187">tooupload hello 下載的憑證，請按一下**上傳**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-187">tooupload hello downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="ee30b-188">在 hello**要求**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee30b-188">In hello **Request** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="ee30b-189">![要求](./media/active-directory-saas-airwatch-tutorial/ic791925.png "要求")</span><span class="sxs-lookup"><span data-stu-id="ee30b-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="ee30b-190">a.</span><span class="sxs-lookup"><span data-stu-id="ee30b-190">a.</span></span> <span data-ttu-id="ee30b-191">針對 [要求繫結類型]，選取 [POST]。</span><span class="sxs-lookup"><span data-stu-id="ee30b-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="ee30b-192">b.</span><span class="sxs-lookup"><span data-stu-id="ee30b-192">b.</span></span> <span data-ttu-id="ee30b-193">在 Azure 入口網站上 hello hello**於 Airwatch 設定單一登入**對話方塊頁面上，複製 hello **SAML 單一登入服務 URL**值並貼到 hello**身分識別提供者單一登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="ee30b-193">In hello Azure portal, on hello **Configure single sign-on at Airwatch** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="ee30b-194">c.</span><span class="sxs-lookup"><span data-stu-id="ee30b-194">c.</span></span> <span data-ttu-id="ee30b-195">針對 [NameID 格式]，選取 [電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="ee30b-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="ee30b-196">d.</span><span class="sxs-lookup"><span data-stu-id="ee30b-196">d.</span></span> <span data-ttu-id="ee30b-197">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ee30b-197">Click **Save**.</span></span>

14. <span data-ttu-id="ee30b-198">按一下 hello**使用者**索引標籤上一次。</span><span class="sxs-lookup"><span data-stu-id="ee30b-198">Click hello **User** tab again.</span></span>
    
    <span data-ttu-id="ee30b-199">![使用者](./media/active-directory-saas-airwatch-tutorial/ic791926.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="ee30b-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="ee30b-200">在 hello**屬性**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee30b-200">In hello **Attribute** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="ee30b-201">![屬性](./media/active-directory-saas-airwatch-tutorial/ic791927.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="ee30b-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="ee30b-202">a.</span><span class="sxs-lookup"><span data-stu-id="ee30b-202">a.</span></span> <span data-ttu-id="ee30b-203">在 hello**物件識別元**文字方塊中，輸入**http://schemas.microsoft.com/identity/claims/objectidentifier**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-203">In hello **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="ee30b-204">b.</span><span class="sxs-lookup"><span data-stu-id="ee30b-204">b.</span></span> <span data-ttu-id="ee30b-205">在 hello **Username**文字方塊中，輸入**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-205">In hello **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="ee30b-206">c.</span><span class="sxs-lookup"><span data-stu-id="ee30b-206">c.</span></span> <span data-ttu-id="ee30b-207">在 hello**顯示名稱**文字方塊中，輸入**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-207">In hello **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="ee30b-208">d.</span><span class="sxs-lookup"><span data-stu-id="ee30b-208">d.</span></span> <span data-ttu-id="ee30b-209">在 hello**名字**文字方塊中，輸入**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-209">In hello **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="ee30b-210">e.</span><span class="sxs-lookup"><span data-stu-id="ee30b-210">e.</span></span> <span data-ttu-id="ee30b-211">在 hello**姓氏**文字方塊中，輸入**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-211">In hello **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="ee30b-212">f.</span><span class="sxs-lookup"><span data-stu-id="ee30b-212">f.</span></span> <span data-ttu-id="ee30b-213">在 hello**電子郵件**文字方塊中，輸入**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-213">In hello **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="ee30b-214">g.</span><span class="sxs-lookup"><span data-stu-id="ee30b-214">g.</span></span> <span data-ttu-id="ee30b-215">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ee30b-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ee30b-216">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ee30b-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="ee30b-217">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ee30b-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ee30b-219">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ee30b-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee30b-220">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="ee30b-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ee30b-222">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ee30b-224">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="ee30b-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ee30b-226">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee30b-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ee30b-228">a.</span><span class="sxs-lookup"><span data-stu-id="ee30b-228">a.</span></span> <span data-ttu-id="ee30b-229">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ee30b-230">b.</span><span class="sxs-lookup"><span data-stu-id="ee30b-230">b.</span></span> <span data-ttu-id="ee30b-231">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**許 Simon。</span><span class="sxs-lookup"><span data-stu-id="ee30b-231">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="ee30b-232">c.</span><span class="sxs-lookup"><span data-stu-id="ee30b-232">c.</span></span> <span data-ttu-id="ee30b-233">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ee30b-234">d.</span><span class="sxs-lookup"><span data-stu-id="ee30b-234">d.</span></span> <span data-ttu-id="ee30b-235">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ee30b-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="ee30b-236">建立 AirWatch 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ee30b-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="ee30b-237">tooenable Azure AD 使用者 toolog 中 tooAirWatch，必須將他們佈建 tooAirWatch 中。</span><span class="sxs-lookup"><span data-stu-id="ee30b-237">tooenable Azure AD users toolog in tooAirWatch, they must be provisioned in tooAirWatch.</span></span>

* <span data-ttu-id="ee30b-238">AirWatch 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="ee30b-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="ee30b-239">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ee30b-239">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee30b-240">登入 tooyour **AirWatch**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="ee30b-240">Log in tooyour **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="ee30b-241">Hello hello 左側瀏覽窗格中按一下**帳戶**，然後按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-241">In hello navigation pane on hello left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="ee30b-242">![使用者](./media/active-directory-saas-airwatch-tutorial/ic791929.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="ee30b-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="ee30b-243">在 hello**使用者**功能表上，按一下 **清單檢視**，然後按一下**新增\>新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-243">In hello **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="ee30b-244">![新增使用者](./media/active-directory-saas-airwatch-tutorial/ic791930.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="ee30b-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="ee30b-245">在 [hello**新增 / 編輯使用者**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee30b-245">On hello **Add / Edit User** dialog, perform hello following steps:</span></span>

   <span data-ttu-id="ee30b-246">![新增使用者](./media/active-directory-saas-airwatch-tutorial/ic791931.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="ee30b-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="ee30b-247">型別 hello **Username**，**密碼**，**確認密碼**，**名字**，**姓氏**， **電子郵件地址**的有效 azure Active Directory 帳戶想成 hello tooprovision 相關的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="ee30b-247">Type hello **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="ee30b-248">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ee30b-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="ee30b-249">您可以使用任何其他 AirWatch 使用者帳戶建立工具或 Api 提供 AirWatch tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee30b-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ee30b-250">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="ee30b-250">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ee30b-251">在本節中，您可以授與存取 tooAirWatch 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ee30b-251">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAirWatch.</span></span>

![指派使用者][200] 

<span data-ttu-id="ee30b-253">**tooassign 許 Simon tooAirWatch，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ee30b-253">**tooassign Britta Simon tooAirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee30b-254">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-254">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ee30b-256">在 [hello] 應用程式清單中，選取**AirWatch**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-256">In hello applications list, select **AirWatch**.</span></span>

    ![設定單一登入](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="ee30b-258">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="ee30b-258">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ee30b-260">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ee30b-260">Click **Add** button.</span></span> <span data-ttu-id="ee30b-261">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ee30b-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ee30b-263">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="ee30b-263">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ee30b-264">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ee30b-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ee30b-265">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ee30b-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ee30b-266">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ee30b-266">Testing single sign-on</span></span>

<span data-ttu-id="ee30b-267">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="ee30b-267">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ee30b-268">如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="ee30b-268">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="ee30b-269">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="ee30b-269">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ee30b-270">其他資源</span><span class="sxs-lookup"><span data-stu-id="ee30b-270">Additional resources</span></span>

* [<span data-ttu-id="ee30b-271">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee30b-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ee30b-272">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ee30b-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

