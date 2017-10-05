---
title: "教學課程：整合 Azure Active Directory 與 vxMaintain | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 vxMaintain 之間的單一登入。"
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
ms.openlocfilehash: ad87534af448356b8cc80d8ddd278bfb8a9165e7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="d186a-103">教學課程：整合 Azure Active Directory 與 vxMaintain</span><span class="sxs-lookup"><span data-stu-id="d186a-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="d186a-104">在本教學課程中，您會了解如何將 vxMaintain 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="d186a-104">In this tutorial, you learn how to integrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d186a-105">這項整合提供一些重要優勢。</span><span class="sxs-lookup"><span data-stu-id="d186a-105">This integration provides several important benefits.</span></span> <span data-ttu-id="d186a-106">您可以：</span><span class="sxs-lookup"><span data-stu-id="d186a-106">You can:</span></span>

- <span data-ttu-id="d186a-107">在 Azure AD 中控制可存取 vxMaintain 的人員。</span><span class="sxs-lookup"><span data-stu-id="d186a-107">Control in Azure AD who has access to vxMaintain.</span></span>
- <span data-ttu-id="d186a-108">可以讓您的使用者藉由使用其 Azure AD 帳戶，透過單一登入 (SSO) 自動登入 vxMaintain。</span><span class="sxs-lookup"><span data-stu-id="d186a-108">Enable your users to automatically sign in to vxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="d186a-109">在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="d186a-109">Manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="d186a-110">若要深入了解 SaaS 應用程式與 Azure AD 整合，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d186a-110">To learn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d186a-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="d186a-111">Prerequisites</span></span>

<span data-ttu-id="d186a-112">若要設定 Azure AD 與 vxMaintain 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="d186a-112">To configure Azure AD integration with vxMaintain, you need the following items:</span></span>

- <span data-ttu-id="d186a-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d186a-113">An Azure AD subscription</span></span>
- <span data-ttu-id="d186a-114">已啟用 vxMaintain SSO 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d186a-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d186a-115">當您測試本教學課程中的步驟時，不建議您使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d186a-115">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="d186a-116">若要測試本教學課程中的步驟，請遵循下列建議：</span><span class="sxs-lookup"><span data-stu-id="d186a-116">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="d186a-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d186a-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d186a-118">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="d186a-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d186a-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="d186a-119">Scenario description</span></span>
<span data-ttu-id="d186a-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d186a-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="d186a-121">本教學課程中說明的案例由二個主要構成要素組成：</span><span class="sxs-lookup"><span data-stu-id="d186a-121">The scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="d186a-122">從資源庫新增 vxMaintain</span><span class="sxs-lookup"><span data-stu-id="d186a-122">Adding vxMaintain from the gallery</span></span>
* <span data-ttu-id="d186a-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d186a-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-the-gallery"></a><span data-ttu-id="d186a-124">從資源庫新增 vxMaintain</span><span class="sxs-lookup"><span data-stu-id="d186a-124">Add vxMaintain from the gallery</span></span>
<span data-ttu-id="d186a-125">若要設定將 vxMaintain 與 Azure AD 整合，您需要從資源庫將 vxMaintain 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="d186a-125">To configure the integration of vxMaintain with Azure AD, you need to add vxMaintain from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d186a-126">若要從資源庫新增 vxMaintain，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d186a-126">To add vxMaintain from the gallery, do the following:</span></span>

1. <span data-ttu-id="d186a-127">在 [Azure 入口網站](https://portal.azure.com)的左側窗格中，選取 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d186a-127">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** button.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="d186a-129">選取 [企業應用程式] > [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d186a-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![[企業應用程式] 窗格][2]
    
3. <span data-ttu-id="d186a-131">若要新增應用程式，請在 [所有應用程式] 對話方塊中，選取 [新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d186a-131">To add an application, in the **All applications** dialog box, select **New application**.</span></span>

    ![[新增應用程式] 按鈕][3]

4. <span data-ttu-id="d186a-133">在搜尋方塊中，輸入 **vxMaintain**。</span><span class="sxs-lookup"><span data-stu-id="d186a-133">In the search box, type **vxMaintain**.</span></span>

    ![[單一登入模式] 下拉式清單](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="d186a-135">在結果清單中，選取 [vxMaintain]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d186a-135">In the results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![vxMaintain 連結](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d186a-137">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d186a-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d186a-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，使用 vxMaintain 設定及測試 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="d186a-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d186a-139">若要讓單一登入能夠運作，Azure AD 必須知道 vxMaintain 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="d186a-139">For SSO to work, Azure AD needs to know the vxMaintain counterpart to the Azure AD user.</span></span> <span data-ttu-id="d186a-140">也就是說，您必須在 Azure AD 使用者和對應的 vxMaintain 使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d186a-140">That is, you must establish a link relationship between the Azure AD user and the corresponding vxMaintain user.</span></span>

<span data-ttu-id="d186a-141">若要建立連結關聯性，請將 vxMaintain **使用者名稱**值指派為 Azure AD **Username** 值。</span><span class="sxs-lookup"><span data-stu-id="d186a-141">To establish the link relationship, assign the vxMaintain **user name** value as the Azure AD **Username** value.</span></span>

<span data-ttu-id="d186a-142">若要使用 vxMaintain 設定及測試 Azure AD SSO，請完成下列構成要素。</span><span class="sxs-lookup"><span data-stu-id="d186a-142">To configure and test Azure AD SSO by using vxMaintain, complete the following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="d186a-143">設定 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d186a-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="d186a-144">在本節中，您可以藉由執行下列步驟，在 Azure 入口網站中啟用 Azure AD SSO，並在 vxMaintain 應用程式中設定 SSO：</span><span class="sxs-lookup"><span data-stu-id="d186a-144">In this section, you can both enable Azure AD SSO in the Azure portal and configure SSO in your vxMaintain application by doing the following:</span></span>

1. <span data-ttu-id="d186a-145">在 Azure 入口網站的 [vxMaintain] 應用程式整合頁面上，選取 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="d186a-145">In the Azure portal, on the **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![[單一登入] 命令][4]

2. <span data-ttu-id="d186a-147">若要啟用 SSO，請在 [單一登入模式] 下拉式清單中，選取 [SAML 型登入]。</span><span class="sxs-lookup"><span data-stu-id="d186a-147">To enable SSO, in the **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![[SAML 型登入] 命令](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="d186a-149">在 [vxMaintain 網域與 URL] 中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d186a-149">Under **vxMaintain Domain and URLs**, do the following:</span></span>

    ![[vxMaintain 網域與 URL] 區段](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="d186a-151">a.</span><span class="sxs-lookup"><span data-stu-id="d186a-151">a.</span></span> <span data-ttu-id="d186a-152">在 [識別碼] 方塊中，輸入具有下列語法的 URL：`https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="d186a-152">In the **Identifier** box, type a URL that has the following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="d186a-153">b.</span><span class="sxs-lookup"><span data-stu-id="d186a-153">b.</span></span> <span data-ttu-id="d186a-154">在 [回覆 URL] 方塊中，輸入具有下列語法的 URL：`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="d186a-154">In the **Reply URL** box, type a URL that has the following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d186a-155">上述值並非真正的值。</span><span class="sxs-lookup"><span data-stu-id="d186a-155">The preceding values are not real.</span></span> <span data-ttu-id="d186a-156">請使用實際的識別碼和回覆 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="d186a-156">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="d186a-157">若要取得這些值，請連絡 [vxMaintain 支援小組](http://www.verisae.com/contact-us)。</span><span class="sxs-lookup"><span data-stu-id="d186a-157">To obtain the values, contact the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="d186a-158">在 [SAML 簽署憑證] 下，選取 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="d186a-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file to your computer.</span></span>

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="d186a-160">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="d186a-160">Select **Save**.</span></span>

    ![[儲存] 按鈕](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d186a-162">若要設定 **vxMaintain** SSO，將下載的**中繼資料 XML** 檔案傳送至 [vxMaintain 支援小組](http://www.verisae.com/contact-us)。</span><span class="sxs-lookup"><span data-stu-id="d186a-162">To configure **vxMaintain** SSO, send the downloaded **Metadata XML** file to the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="d186a-163">當您設定應用程式時，您可以在 [Azure 入口網站](https://portal.azure.com)中閱讀精簡版的先前說明。</span><span class="sxs-lookup"><span data-stu-id="d186a-163">As you set up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d186a-164">當您從 [Active Directory] > [企業應用程式] 區段新增應用程式之後，選取 [單一登入] 索引標籤，即可從 [設定] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="d186a-164">After you add the app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation from the **Configuration** section.</span></span> 
>
><span data-ttu-id="d186a-165">若要深入了解內嵌文件功能，請參閱[管理企業應用程式的單一登入](https://go.microsoft.com/fwlink/?linkid=845985)。</span><span class="sxs-lookup"><span data-stu-id="d186a-165">To learn more about the embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d186a-166">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d186a-166">Create an Azure AD test user</span></span>
<span data-ttu-id="d186a-167">在本節中，您會執行下列步驟，在 Azure 入口網站中建立測試使用者 Britta Simon：</span><span class="sxs-lookup"><span data-stu-id="d186a-167">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Azure AD 測試使用者][100]

1. <span data-ttu-id="d186a-169">在 **Azure 入口網站**的左側窗格中，選取 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d186a-169">In the **Azure portal**, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![[Azure Active Directory] 按鈕](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d186a-171">若要顯示使用者清單，請移至 [使用者和群組] > [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="d186a-171">To display a list of users, go to **Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="d186a-172">![[所有使用者] 連結](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="d186a-172">![The "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="d186a-173">[所有使用者] 對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d186a-173">The **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="d186a-174">若要開啟 [使用者] 對話方塊，請選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d186a-174">To open the **User** dialog box, select **Add**.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d186a-176">在 [使用者] 對話方塊中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d186a-176">In the **User** dialog box, do the following:</span></span>
 
    ![[使用者] 對話方塊](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d186a-178">a.</span><span class="sxs-lookup"><span data-stu-id="d186a-178">a.</span></span> <span data-ttu-id="d186a-179">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d186a-179">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d186a-180">b.</span><span class="sxs-lookup"><span data-stu-id="d186a-180">b.</span></span> <span data-ttu-id="d186a-181">在 [使用者名稱] 方塊中，輸入測試使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="d186a-181">In the **User name** box, type the email address of test user Britta Simon.</span></span>

    <span data-ttu-id="d186a-182">c.</span><span class="sxs-lookup"><span data-stu-id="d186a-182">c.</span></span> <span data-ttu-id="d186a-183">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中產生的值。</span><span class="sxs-lookup"><span data-stu-id="d186a-183">Select the **Show Password** check box, and then note the value that was generated in the **Password** box.</span></span>

    <span data-ttu-id="d186a-184">d.</span><span class="sxs-lookup"><span data-stu-id="d186a-184">d.</span></span> <span data-ttu-id="d186a-185">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="d186a-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="d186a-186">建立 vxMaintain 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d186a-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="d186a-187">在本節中，您會在 vxMaintain 中建立測試使用者 Britta Simon。</span><span class="sxs-lookup"><span data-stu-id="d186a-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="d186a-188">若要在 vxMaintain 平台中新增使用者，請與 [vxMaintain 支援小組](http://www.verisae.com/contact-us) 合作。</span><span class="sxs-lookup"><span data-stu-id="d186a-188">To add users in the vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="d186a-189">使用 SSO 之前，請先建立並啟用使用者。</span><span class="sxs-lookup"><span data-stu-id="d186a-189">Before you use SSO, create and activate the users.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d186a-190">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d186a-190">Assign the Azure AD test user</span></span>

<span data-ttu-id="d186a-191">在本節中，您會把 vxMaintain 的存取權授予 Britta Simon，讓 Britta Simon 能夠使用 Azure SSO。</span><span class="sxs-lookup"><span data-stu-id="d186a-191">In this section, you enable test user Britta Simon to use Azure SSO by granting access to vxMaintain.</span></span> <span data-ttu-id="d186a-192">若要這樣做，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d186a-192">To do so, do the following:</span></span>

![[顯示名稱] 清單中的測試使用者][200] 

1. <span data-ttu-id="d186a-194">在 Azure 入口網站的 [應用程式] 檢視中，移至 [目錄] 檢視 > [企業應用程式] > [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d186a-194">In the Azure portal **Applications** view, go to **Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![[所有應用程式] 連結][201] 

2. <span data-ttu-id="d186a-196">在 [應用程式] 清單中，選取 [vxMaintain]。</span><span class="sxs-lookup"><span data-stu-id="d186a-196">In the **Applications** list, select **vxMaintain**.</span></span>

    ![vxMaintain 連結](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="d186a-198">在左側窗格中，選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d186a-198">In the left pane, select **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202] 

4. <span data-ttu-id="d186a-200">選取 [新增]，然後在 [新增指派] 窗格中，選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d186a-200">Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![[使用者和群組] 連結][203]

5. <span data-ttu-id="d186a-202">在 [使用者和群組] 對話方塊的 [使用者] 清單中，選取 [Britta Simon]，然後選取 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d186a-202">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**, and then select the **Select** button.</span></span>

7. <span data-ttu-id="d186a-203">在 [新增指派] 對話方塊中，選取 [指派]。</span><span class="sxs-lookup"><span data-stu-id="d186a-203">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="d186a-204">測試您的 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d186a-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="d186a-205">在本節中，您會使用存取面板來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="d186a-205">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="d186a-206">在存取面板中選取 [vxMaintain] 圖格時，應該會自動登入您的 vxMaintain 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d186a-206">Selecting the **vxMaintain** tile in the Access Panel should sign you in to your vxMaintain application automatically.</span></span>

<span data-ttu-id="d186a-207">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="d186a-207">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d186a-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d186a-208">Next steps</span></span>

* [<span data-ttu-id="d186a-209">整合 SaaS 應用程式與 Azure Active Directory 的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="d186a-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d186a-210">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d186a-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

