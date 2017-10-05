---
title: "教學課程：Azure Active Directory 與 AppDynamics 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 AppDynamics 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 634e68bdb937eba68b27b824dc62fe2677e24ffe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="de699-103">教學課程：Azure Active Directory 與 AppDynamics 整合</span><span class="sxs-lookup"><span data-stu-id="de699-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="de699-104">在本教學課程中，您會了解如何將 AppDynamics 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="de699-104">In this tutorial, you learn how to integrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de699-105">將 AppDynamics 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="de699-105">Integrating AppDynamics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="de699-106">您可以在 Azure AD 中控制可存取 AppDynamics 的人員</span><span class="sxs-lookup"><span data-stu-id="de699-106">You can control in Azure AD who has access to AppDynamics</span></span>
- <span data-ttu-id="de699-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 AppDynamics (單一登入)</span><span class="sxs-lookup"><span data-stu-id="de699-107">You can enable your users to automatically get signed-on to AppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="de699-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="de699-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="de699-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="de699-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de699-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="de699-110">Prerequisites</span></span>

<span data-ttu-id="de699-111">若要設定 Azure AD 與 AppDynamics 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="de699-111">To configure Azure AD integration with AppDynamics, you need the following items:</span></span>

- <span data-ttu-id="de699-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="de699-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de699-113">已啟用 AppDynamics 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="de699-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de699-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="de699-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="de699-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="de699-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de699-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="de699-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="de699-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="de699-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de699-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="de699-118">Scenario description</span></span>
<span data-ttu-id="de699-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de699-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de699-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="de699-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de699-121">從資源庫新增 AppDynamics</span><span class="sxs-lookup"><span data-stu-id="de699-121">Adding AppDynamics from the gallery</span></span>
2. <span data-ttu-id="de699-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="de699-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-the-gallery"></a><span data-ttu-id="de699-123">從資源庫新增 AppDynamics</span><span class="sxs-lookup"><span data-stu-id="de699-123">Adding AppDynamics from the gallery</span></span>
<span data-ttu-id="de699-124">若要設定將 AppDynamics 整合到 Azure AD 中，您需要從資源庫將 AppDynamics 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="de699-124">To configure the integration of AppDynamics into Azure AD, you need to add AppDynamics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="de699-125">**若要從資源庫新增 AppDynamics，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="de699-125">**To add AppDynamics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="de699-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="de699-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="de699-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="de699-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="de699-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="de699-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="de699-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de699-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="de699-133">在搜尋方塊中，輸入 **AppDynamics**。</span><span class="sxs-lookup"><span data-stu-id="de699-133">In the search box, type **AppDynamics**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="de699-135">在結果面板中，選取 [AppDynamics]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="de699-135">In the results panel, select **AppDynamics**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de699-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="de699-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de699-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 AppDynamics 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de699-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="de699-139">若要讓單一登入能夠運作，Azure AD 必須知道 AppDynamics 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="de699-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppDynamics is to a user in Azure AD.</span></span> <span data-ttu-id="de699-140">換句話說，必須在 Azure AD 使用者與 AppDynamics 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="de699-140">In other words, a link relationship between an Azure AD user and the related user in AppDynamics needs to be established.</span></span>

<span data-ttu-id="de699-141">在 AppDynamics 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="de699-141">In AppDynamics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="de699-142">若要設定及測試與 AppDynamics 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="de699-142">To configure and test Azure AD single sign-on with AppDynamics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="de699-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="de699-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="de699-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de699-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de699-145">**[建立 AppDynamics 測試使用者](#creating-an-appdynamics-test-user)** - 在 AppDynamics 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="de699-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - to have a counterpart of Britta Simon in AppDynamics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="de699-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de699-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de699-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="de699-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de699-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="de699-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="de699-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 AppDynamics 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="de699-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="de699-150">**若要設定與 AppDynamics 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="de699-150">**To configure Azure AD single sign-on with AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="de699-151">在 Azure 入口網站的 [AppDynamics] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="de699-151">In the Azure portal, on the **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="de699-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="de699-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="de699-155">在 [AppDynamics 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="de699-155">On the **AppDynamics Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="de699-157">a.</span><span class="sxs-lookup"><span data-stu-id="de699-157">a.</span></span> <span data-ttu-id="de699-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="de699-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="de699-159">b.</span><span class="sxs-lookup"><span data-stu-id="de699-159">b.</span></span> <span data-ttu-id="de699-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="de699-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="de699-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="de699-161">These values are not real.</span></span> <span data-ttu-id="de699-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="de699-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="de699-163">請連絡 [AppDynamics 用戶端支援小組](https://www.appdynamics.com/support/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="de699-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="de699-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="de699-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="de699-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="de699-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="de699-168">在 [AppDynamics 組態] 區段上，按一下 [設定 AppDynamics] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="de699-168">On the **AppDynamics Configuration** section, click **Configure AppDynamics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="de699-169">從 [快速參考] 區段中複製「登出 URL」和「SAML 單一登入服務 URL」。</span><span class="sxs-lookup"><span data-stu-id="de699-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="de699-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 AppDynamics 公司網站。</span><span class="sxs-lookup"><span data-stu-id="de699-171">In a different web browser window, log in to your AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="de699-172">在頂端工具列中，按一下 [設定]，然後按一下 [管理]。</span><span class="sxs-lookup"><span data-stu-id="de699-172">In the toolbar on the top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="de699-173">![管理](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "管理")</span><span class="sxs-lookup"><span data-stu-id="de699-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="de699-174">按一下 [驗證提供者]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="de699-174">Click the **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="de699-175">![驗證提供者](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "驗證提供者")</span><span class="sxs-lookup"><span data-stu-id="de699-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="de699-176">在 [驗證提供者] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="de699-176">In the **Authentication Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="de699-177">![SAML 設定](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="de699-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="de699-178">a.</span><span class="sxs-lookup"><span data-stu-id="de699-178">a.</span></span> <span data-ttu-id="de699-179">針對 [驗證提供者]，選取 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="de699-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="de699-180">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="de699-180">b.</span></span> <span data-ttu-id="de699-181">在 [登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="de699-181">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="de699-182">c.</span><span class="sxs-lookup"><span data-stu-id="de699-182">c.</span></span> <span data-ttu-id="de699-183">在 [登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="de699-183">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="de699-184">d.</span><span class="sxs-lookup"><span data-stu-id="de699-184">d.</span></span> <span data-ttu-id="de699-185">在記事本中開啟您的 Base-64 編碼的憑證，將其內容複製到您的剪貼簿，然後貼到 [憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="de699-185">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox</span></span>

    <span data-ttu-id="de699-186">e.</span><span class="sxs-lookup"><span data-stu-id="de699-186">e.</span></span> <span data-ttu-id="de699-187">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="de699-187">Click **Save**.</span></span>

     <span data-ttu-id="de699-188">![儲存](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "儲存")</span><span class="sxs-lookup"><span data-stu-id="de699-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="de699-189">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="de699-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="de699-190">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="de699-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="de699-191">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="de699-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de699-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="de699-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="de699-193">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="de699-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="de699-195">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="de699-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="de699-196">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="de699-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="de699-198">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="de699-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="de699-200">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="de699-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="de699-202">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="de699-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="de699-204">a.</span><span class="sxs-lookup"><span data-stu-id="de699-204">a.</span></span> <span data-ttu-id="de699-205">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="de699-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de699-206">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="de699-206">b.</span></span> <span data-ttu-id="de699-207">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="de699-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de699-208">c.</span><span class="sxs-lookup"><span data-stu-id="de699-208">c.</span></span> <span data-ttu-id="de699-209">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="de699-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="de699-210">d.</span><span class="sxs-lookup"><span data-stu-id="de699-210">d.</span></span> <span data-ttu-id="de699-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="de699-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="de699-212">建立 AppDynamics 測試使用者</span><span class="sxs-lookup"><span data-stu-id="de699-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="de699-213">若要讓 Azure AD 使用者能夠登入 AppDynamics，必須將他們佈建到 AppDynamics。</span><span class="sxs-lookup"><span data-stu-id="de699-213">To enable Azure AD users to log in to AppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="de699-214">就 AppDynamics 而言，需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="de699-214">In the case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="de699-215">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="de699-215">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="de699-216">以系統管理員身分登入您的 AppDynamics 公司網站。</span><span class="sxs-lookup"><span data-stu-id="de699-216">Log in to your AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="de699-217">移至 [使用者]，然後按一下 **+** 開啟 [建立使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="de699-217">Go to **Users**, and then click **+** to open the **Create User** dialog.</span></span>
   
    <span data-ttu-id="de699-218">![使用者](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="de699-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="de699-219">在 [建立使用者] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="de699-219">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="de699-220">![建立使用者](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="de699-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="de699-221">a.</span><span class="sxs-lookup"><span data-stu-id="de699-221">a.</span></span> <span data-ttu-id="de699-222">在相關的文字方塊中，輸入您要佈建之有效 AAD 帳戶的 [使用者名稱]、[名稱]、[電子郵件]、[新密碼]、[重複新密碼]。</span><span class="sxs-lookup"><span data-stu-id="de699-222">Type the **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="de699-223">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="de699-223">b.</span></span> <span data-ttu-id="de699-224">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="de699-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="de699-225">您可以使用任何其他的 AppDynamics 使用者帳戶建立工具或 AppDynamics 提供的 API 來佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="de699-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="de699-226">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="de699-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="de699-227">在本節中，您會將 AppDynamics 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de699-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppDynamics.</span></span>

![指派使用者][200] 

<span data-ttu-id="de699-229">**若要將 Britta Simon 指派給 AppDynamics，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="de699-229">**To assign Britta Simon to AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="de699-230">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="de699-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="de699-232">在應用程式清單中，選取 [AppDynamics]。</span><span class="sxs-lookup"><span data-stu-id="de699-232">In the applications list, select **AppDynamics**.</span></span>

    ![設定單一登入](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="de699-234">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="de699-234">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="de699-236">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de699-236">Click **Add** button.</span></span> <span data-ttu-id="de699-237">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="de699-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="de699-239">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="de699-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="de699-240">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de699-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de699-241">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de699-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="de699-242">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="de699-242">Testing single sign-on</span></span>

<span data-ttu-id="de699-243">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="de699-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="de699-244">當您在「存取面板」中按一下 [AppDynamics] 圖格時，應該會自動登入您的 AppDynamics 應用程式。</span><span class="sxs-lookup"><span data-stu-id="de699-244">When you click the AppDynamics tile in the Access Panel, you should get automatically signed-on to your AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="de699-245">其他資源</span><span class="sxs-lookup"><span data-stu-id="de699-245">Additional resources</span></span>

* [<span data-ttu-id="de699-246">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="de699-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de699-247">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="de699-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

