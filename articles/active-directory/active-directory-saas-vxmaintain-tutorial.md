---
title: "教學課程：整合 Azure Active Directory 與 vxMaintain | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 vxMaintain 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="34292-103">教學課程：整合 Azure Active Directory 與 vxMaintain</span><span class="sxs-lookup"><span data-stu-id="34292-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="34292-104">在此教學課程中，您學會如何 toointegrate vxMaintain 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="34292-104">In this tutorial, you learn how toointegrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34292-105">這項整合提供一些重要優勢。</span><span class="sxs-lookup"><span data-stu-id="34292-105">This integration provides several important benefits.</span></span> <span data-ttu-id="34292-106">您可以：</span><span class="sxs-lookup"><span data-stu-id="34292-106">You can:</span></span>

- <span data-ttu-id="34292-107">在具有 Azure AD 中的控制項存取 toovxMaintain。</span><span class="sxs-lookup"><span data-stu-id="34292-107">Control in Azure AD who has access toovxMaintain.</span></span>
- <span data-ttu-id="34292-108">使用其 Azure AD 帳戶，以啟用您的使用者 tooautomatically 登入 toovxMaintain 搭配單一登入 (SSO)。</span><span class="sxs-lookup"><span data-stu-id="34292-108">Enable your users tooautomatically sign in toovxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="34292-109">管理您的帳戶，在單一中央位置： hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="34292-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="34292-110">toolearn 進一步了解 SaaS 應用程式整合，使用 Azure AD，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="34292-110">toolearn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34292-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="34292-111">Prerequisites</span></span>

<span data-ttu-id="34292-112">tooconfigure vxMaintain 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="34292-112">tooconfigure Azure AD integration with vxMaintain, you need hello following items:</span></span>

- <span data-ttu-id="34292-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="34292-113">An Azure AD subscription</span></span>
- <span data-ttu-id="34292-114">已啟用 vxMaintain SSO 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="34292-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="34292-115">當您測試 hello 步驟在本教學課程時，我們建議您不要使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="34292-115">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="34292-116">tootest hello 步驟在本教學課程，請遵循下列建議：</span><span class="sxs-lookup"><span data-stu-id="34292-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="34292-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="34292-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="34292-118">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="34292-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="34292-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="34292-119">Scenario description</span></span>
<span data-ttu-id="34292-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="34292-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="34292-121">本教學課程中概述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="34292-121">hello scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="34292-122">從 hello 圖庫加入 vxMaintain</span><span class="sxs-lookup"><span data-stu-id="34292-122">Adding vxMaintain from hello gallery</span></span>
* <span data-ttu-id="34292-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="34292-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-hello-gallery"></a><span data-ttu-id="34292-124">從 hello 圖庫新增 vxMaintain</span><span class="sxs-lookup"><span data-stu-id="34292-124">Add vxMaintain from hello gallery</span></span>
<span data-ttu-id="34292-125">tooconfigure hello vxMaintain 與 Azure AD 整合，您需要 tooadd vxMaintain hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="34292-125">tooconfigure hello integration of vxMaintain with Azure AD, you need tooadd vxMaintain from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="34292-126">從 hello 圖庫 tooadd vxMaintain hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="34292-126">tooadd vxMaintain from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="34292-127">在 [hello [Azure 入口網站](https://portal.azure.com)，在 [hello 左的窗格中選取 hello **Azure Active Directory** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="34292-127">In hello [Azure portal](https://portal.azure.com), in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![hello Azure Active Directory] 按鈕][1]

2. <span data-ttu-id="34292-129">選取 [企業應用程式] > [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="34292-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![hello 「 企業應用程式 」 窗格][2]
    
3. <span data-ttu-id="34292-131">應用程式，在 hello tooadd**所有應用程式**對話方塊中，選取**新的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="34292-131">tooadd an application, in hello **All applications** dialog box, select **New application**.</span></span>

    ![hello 「 新的應用程式 」 按鈕][3]

4. <span data-ttu-id="34292-133">在 [hello] 搜尋方塊中，輸入**vxMaintain**。</span><span class="sxs-lookup"><span data-stu-id="34292-133">In hello search box, type **vxMaintain**.</span></span>

    ![hello 「 單一登入模式 」 的下拉式清單](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="34292-135">在 [hello 結果清單中，選取 [ **vxMaintain**，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="34292-135">In hello results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![hello vxMaintain 連結](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="34292-137">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="34292-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="34292-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，使用 vxMaintain 設定及測試 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="34292-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="34292-139">SSO toowork Azure AD 需要 tooknow hello vxMaintain 對應項目 toohello Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="34292-139">For SSO toowork, Azure AD needs tooknow hello vxMaintain counterpart toohello Azure AD user.</span></span> <span data-ttu-id="34292-140">也就是說，您必須建立 hello Azure AD 使用者與 hello 對應 vxMaintain 使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="34292-140">That is, you must establish a link relationship between hello Azure AD user and hello corresponding vxMaintain user.</span></span>

<span data-ttu-id="34292-141">tooestablish hello 連結關聯性，指派 hello vxMaintain**使用者名**值為 hello Azure AD **Username**值。</span><span class="sxs-lookup"><span data-stu-id="34292-141">tooestablish hello link relationship, assign hello vxMaintain **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="34292-142">tooconfigure 和測試 Azure AD SSO 使用 vxMaintain，完成下列建置組塊的 hello。</span><span class="sxs-lookup"><span data-stu-id="34292-142">tooconfigure and test Azure AD SSO by using vxMaintain, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="34292-143">設定 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="34292-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="34292-144">在本節中，您可在 hello Azure 入口網站中啟用 Azure AD 的 SSO 和 vxMaintain 應用程式中設定 SSO，藉由下列 hello:</span><span class="sxs-lookup"><span data-stu-id="34292-144">In this section, you can both enable Azure AD SSO in hello Azure portal and configure SSO in your vxMaintain application by doing hello following:</span></span>

1. <span data-ttu-id="34292-145">在 Azure 入口網站上 hello hello **vxMaintain**應用程式整合頁面上，選取**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="34292-145">In hello Azure portal, on hello **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![hello 「 單一登入 」 的命令][4]

2. <span data-ttu-id="34292-147">在 [hello tooenable SSO，**單一登入模式**下拉式清單中，選取**SAML 型登入**。</span><span class="sxs-lookup"><span data-stu-id="34292-147">tooenable SSO, in hello **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![hello [SAML 型登入] 命令](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="34292-149">在下**vxMaintain 網域和 Url**，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="34292-149">Under **vxMaintain Domain and URLs**, do hello following:</span></span>

    ![hello vxMaintain 網域和 Url 的區段](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="34292-151">a.</span><span class="sxs-lookup"><span data-stu-id="34292-151">a.</span></span> <span data-ttu-id="34292-152">在 [hello**識別碼**方塊中，輸入 URL，請使用下列語法已經 hello:`https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="34292-152">In hello **Identifier** box, type a URL that has hello following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="34292-153">b.</span><span class="sxs-lookup"><span data-stu-id="34292-153">b.</span></span> <span data-ttu-id="34292-154">在 [hello**回覆 URL**方塊中，輸入 URL，請使用下列語法已經 hello:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="34292-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="34292-155">hello 上述值不是實際。</span><span class="sxs-lookup"><span data-stu-id="34292-155">hello preceding values are not real.</span></span> <span data-ttu-id="34292-156">更新 hello 實際識別項，回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="34292-156">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="34292-157">tooobtain hello 值，請連絡 hello [vxMaintain 支援小組](http://www.verisae.com/contact-us)。</span><span class="sxs-lookup"><span data-stu-id="34292-157">tooobtain hello values, contact hello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="34292-158">在下**SAML 簽章憑證**，選取**中繼資料 XML**，然後儲存 hello 中繼資料檔案 tooyour 電腦。</span><span class="sxs-lookup"><span data-stu-id="34292-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file tooyour computer.</span></span>

    ![hello 「 SAML 簽章憑證 」 一節](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="34292-160">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="34292-160">Select **Save**.</span></span>

    ![hello [儲存] 按鈕](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="34292-162">tooconfigure **vxMaintain** SSO，傳送嗨下載**中繼資料 XML**檔案 toohello [vxMaintain 支援小組](http://www.verisae.com/contact-us)。</span><span class="sxs-lookup"><span data-stu-id="34292-162">tooconfigure **vxMaintain** SSO, send hello downloaded **Metadata XML** file toohello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="34292-163">當您設定 hello 應用程式時，您可以閱讀 hello hello 中前面指示的精簡版本[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="34292-163">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="34292-164">從 hello 新增 hello 應用程式之後**Active Directory** > **企業應用程式**區段中，選取 hello**單一登入**] 索引標籤，然後再存取 hello內嵌文件從 hello**組態**> 一節。</span><span class="sxs-lookup"><span data-stu-id="34292-164">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab, and then access hello embedded documentation from hello **Configuration** section.</span></span> 
>
><span data-ttu-id="34292-165">toolearn 進一步了解 hello embedded 文件功能，請參閱[管理單一登入企業應用程式](https://go.microsoft.com/fwlink/?linkid=845985)。</span><span class="sxs-lookup"><span data-stu-id="34292-165">toolearn more about hello embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="34292-166">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="34292-166">Create an Azure AD test user</span></span>
<span data-ttu-id="34292-167">在本節中，您可以建立 hello Azure 入口網站中的測試使用者許 Simon 執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="34292-167">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![hello Azure AD 的測試使用者][100]

1. <span data-ttu-id="34292-169">在 [hello **Azure 入口網站**，在 [hello 左的窗格中選取 hello **Azure Active Directory** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="34292-169">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![hello"Azure Active Directory"的按鈕](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="34292-171">toodisplay 使用者清單，請移過**使用者和群組** > **所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="34292-171">toodisplay a list of users, go too**Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="34292-172">![hello，"All users"連結](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="34292-172">![hello "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="34292-173">hello**所有使用者**對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="34292-173">hello **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="34292-174">tooopen hello**使用者**對話方塊中，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="34292-174">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![hello [新增] 按鈕](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="34292-176">在 [hello**使用者**對話方塊方塊中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="34292-176">In hello **User** dialog box, do hello following:</span></span>
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="34292-178">a.</span><span class="sxs-lookup"><span data-stu-id="34292-178">a.</span></span> <span data-ttu-id="34292-179">在 [hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="34292-179">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34292-180">b.</span><span class="sxs-lookup"><span data-stu-id="34292-180">b.</span></span> <span data-ttu-id="34292-181">在 [hello**使用者名**方塊中，測試使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="34292-181">In hello **User name** box, type hello email address of test user Britta Simon.</span></span>

    <span data-ttu-id="34292-182">c.</span><span class="sxs-lookup"><span data-stu-id="34292-182">c.</span></span> <span data-ttu-id="34292-183">選取 hello**顯示密碼**核取方塊，然後注意 hello 值所產生的 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="34292-183">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="34292-184">d.</span><span class="sxs-lookup"><span data-stu-id="34292-184">d.</span></span> <span data-ttu-id="34292-185">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="34292-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="34292-186">建立 vxMaintain 測試使用者</span><span class="sxs-lookup"><span data-stu-id="34292-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="34292-187">在本節中，您會在 vxMaintain 中建立測試使用者 Britta Simon。</span><span class="sxs-lookup"><span data-stu-id="34292-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="34292-188">在 hello vxMaintain 平台中，tooadd 使用者使用[vxMaintain 支援小組](http://www.verisae.com/contact-us)。</span><span class="sxs-lookup"><span data-stu-id="34292-188">tooadd users in hello vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="34292-189">使用 SSO 之前，先建立及啟動 hello 的使用者。</span><span class="sxs-lookup"><span data-stu-id="34292-189">Before you use SSO, create and activate hello users.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="34292-190">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="34292-190">Assign hello Azure AD test user</span></span>

<span data-ttu-id="34292-191">在本節中，您可以授與存取 toovxMaintain 啟用測試使用者許 Simon toouse Azure SSO。</span><span class="sxs-lookup"><span data-stu-id="34292-191">In this section, you enable test user Britta Simon toouse Azure SSO by granting access toovxMaintain.</span></span> <span data-ttu-id="34292-192">toodo，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="34292-192">toodo so, do hello following:</span></span>

![Hello 顯示名稱清單中的測試使用者][200] 

1. <span data-ttu-id="34292-194">在 Azure 入口網站 hello**應用程式**檢視，請進入太**目錄**檢視 >**企業應用程式** > **的所有應用程式**.</span><span class="sxs-lookup"><span data-stu-id="34292-194">In hello Azure portal **Applications** view, go too**Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![hello [所有應用程式] 連結][201] 

2. <span data-ttu-id="34292-196">在 [hello**應用程式**清單中，選取**vxMaintain**。</span><span class="sxs-lookup"><span data-stu-id="34292-196">In hello **Applications** list, select **vxMaintain**.</span></span>

    ![hello vxMaintain 連結](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="34292-198">Hello 左窗格中，選取**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="34292-198">In hello left pane, select **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202] 

4. <span data-ttu-id="34292-200">選取**新增**，然後在 hello**將作業加入**窗格中，選取**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="34292-200">Select **Add** and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][203]

5. <span data-ttu-id="34292-202">在 hello**使用者和群組**對話方塊中的，在 hello**使用者**清單中，選取**許 Simon**，然後選取 [hello**選取**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="34292-202">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**, and then select hello **Select** button.</span></span>

7. <span data-ttu-id="34292-203">在 [hello**將作業加入**對話方塊中，選取**指派**。</span><span class="sxs-lookup"><span data-stu-id="34292-203">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="34292-204">測試您的 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="34292-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="34292-205">本節中，在中，您可以測試您的 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="34292-205">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="34292-206">選取 hello **vxMaintain** hello 存取面板中的圖格應該自動登入 tooyour vxMaintain 應用程式。</span><span class="sxs-lookup"><span data-stu-id="34292-206">Selecting hello **vxMaintain** tile in hello Access Panel should sign you in tooyour vxMaintain application automatically.</span></span>

<span data-ttu-id="34292-207">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="34292-207">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="34292-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="34292-208">Next steps</span></span>

* [<span data-ttu-id="34292-209">整合 SaaS 應用程式與 Azure Active Directory 的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="34292-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34292-210">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="34292-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

