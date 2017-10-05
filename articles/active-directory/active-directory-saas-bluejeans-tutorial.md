---
title: "教學課程：Azure Active Directory 與 BlueJeans 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 BlueJeans 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 03bf65852b8d3cf14aebf155891a028db86e78d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="91858-103">教學課程：Azure Active Directory 與 BlueJeans 整合</span><span class="sxs-lookup"><span data-stu-id="91858-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="91858-104">在本教學課程中，您會了解如何將 BlueJeans 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="91858-104">In this tutorial, you learn how to integrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91858-105">將 BlueJeans 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="91858-105">Integrating BlueJeans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="91858-106">您可以在 Azure AD 中控制可存取 BlueJeans 的人員</span><span class="sxs-lookup"><span data-stu-id="91858-106">You can control in Azure AD who has access to BlueJeans</span></span>
- <span data-ttu-id="91858-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 BlueJeans (單一登入)</span><span class="sxs-lookup"><span data-stu-id="91858-107">You can enable your users to automatically get signed-on to BlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="91858-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="91858-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="91858-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="91858-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91858-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="91858-110">Prerequisites</span></span>

<span data-ttu-id="91858-111">若要設定 Azure AD 與 BlueJeans 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="91858-111">To configure Azure AD integration with BlueJeans, you need the following items:</span></span>

- <span data-ttu-id="91858-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="91858-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91858-113">已啟用 BlueJeans 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="91858-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91858-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="91858-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91858-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="91858-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91858-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="91858-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91858-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="91858-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91858-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="91858-118">Scenario description</span></span>
<span data-ttu-id="91858-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91858-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91858-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="91858-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91858-121">從資源庫新增 BlueJeans</span><span class="sxs-lookup"><span data-stu-id="91858-121">Adding BlueJeans from the gallery</span></span>
2. <span data-ttu-id="91858-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="91858-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-the-gallery"></a><span data-ttu-id="91858-123">從資源庫新增 BlueJeans</span><span class="sxs-lookup"><span data-stu-id="91858-123">Adding BlueJeans from the gallery</span></span>
<span data-ttu-id="91858-124">若要設定將 BlueJeans 整合到 Azure AD 中，您需要從資源庫將 BlueJeans 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="91858-124">To configure the integration of BlueJeans into Azure AD, you need to add BlueJeans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="91858-125">**若要從資源庫新增 BlueJeans，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="91858-125">**To add BlueJeans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="91858-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="91858-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="91858-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="91858-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="91858-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="91858-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="91858-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="91858-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="91858-133">在搜尋方塊中，輸入 **BlueJeans**。</span><span class="sxs-lookup"><span data-stu-id="91858-133">In the search box, type **BlueJeans**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="91858-135">在結果面板中，選取 [BlueJeans]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="91858-135">In the results panel, select **BlueJeans**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="91858-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="91858-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="91858-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 BlueJeans 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91858-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="91858-139">若要讓單一登入能夠運作，Azure AD 必須知道 BlueJeans 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="91858-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BlueJeans is to a user in Azure AD.</span></span> <span data-ttu-id="91858-140">換句話說，必須在 Azure AD 使用者與 BlueJeans 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="91858-140">In other words, a link relationship between an Azure AD user and the related user in BlueJeans needs to be established.</span></span>

<span data-ttu-id="91858-141">在 BlueJeans 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="91858-141">In BlueJeans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="91858-142">若要設定及測試與 BlueJeans 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="91858-142">To configure and test Azure AD single sign-on with BlueJeans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="91858-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="91858-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="91858-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91858-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="91858-145">**[建立 BlueJeans 測試使用者](#creating-a-bluejeans-test-user)** - 在 BlueJeans 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="91858-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - to have a counterpart of Britta Simon in BlueJeans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="91858-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91858-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="91858-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="91858-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="91858-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="91858-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="91858-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 BlueJeans 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="91858-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="91858-150">**若要設定與 BlueJeans 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="91858-150">**To configure Azure AD single sign-on with BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="91858-151">在 Azure 入口網站的 [BlueJeans] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="91858-151">In the Azure portal, on the **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="91858-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="91858-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="91858-155">在 [BlueJeans 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="91858-155">On the **BlueJeans Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="91858-157">a.</span><span class="sxs-lookup"><span data-stu-id="91858-157">a.</span></span> <span data-ttu-id="91858-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="91858-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="91858-159">b.</span><span class="sxs-lookup"><span data-stu-id="91858-159">b.</span></span> <span data-ttu-id="91858-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="91858-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="91858-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="91858-161">These values are not real.</span></span> <span data-ttu-id="91858-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="91858-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="91858-163">請連絡 [BlueJeans 用戶端支援小組](https://support.bluejeans.com/contact)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="91858-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="91858-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="91858-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="91858-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="91858-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="91858-168">在 [BlueJeans 組態] 區段上，按一下 [設定 BlueJeans] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="91858-168">On the **BlueJeans Configuration** section, click **Configure BlueJeans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="91858-169">從 [快速參考] 區段中複製「登出 URL」、「變更密碼 URL」及「SAML 單一登入服務 URL」。</span><span class="sxs-lookup"><span data-stu-id="91858-169">Copy the **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="91858-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **BlueJeans** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="91858-171">In a different web browser window, log in to your **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="91858-172">移至 [管理] \> [群組設定] \> > [安全性]。</span><span class="sxs-lookup"><span data-stu-id="91858-172">Go to **ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="91858-173">![管理](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "管理")</span><span class="sxs-lookup"><span data-stu-id="91858-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="91858-174">在 [安全性] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="91858-174">In the **Security** section, perform the following steps:</span></span>
   
   <span data-ttu-id="91858-175">![SAML 單一登入](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML 單一登入")</span><span class="sxs-lookup"><span data-stu-id="91858-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="91858-176">a.</span><span class="sxs-lookup"><span data-stu-id="91858-176">a.</span></span> <span data-ttu-id="91858-177">選取 [SAML 單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="91858-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="91858-178">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="91858-178">b.</span></span> <span data-ttu-id="91858-179">選取 [啟用自動佈建] 。</span><span class="sxs-lookup"><span data-stu-id="91858-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="91858-180">繼續執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="91858-180">Move on with the following steps:</span></span>

    <span data-ttu-id="91858-181">![憑證路徑](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "憑證路徑")</span><span class="sxs-lookup"><span data-stu-id="91858-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="91858-182">a.</span><span class="sxs-lookup"><span data-stu-id="91858-182">a.</span></span> <span data-ttu-id="91858-183">按一下 [選擇檔案] ，然後上傳下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="91858-183">Click **Choose File**, and then upload the downloaded certificate.</span></span>
   
    <span data-ttu-id="91858-184">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="91858-184">b.</span></span> <span data-ttu-id="91858-185">將「SAML 單一登入服務 URL」貼到 [登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="91858-185">Paste **SAML Single Sign-On Service URL** into the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="91858-186">c.</span><span class="sxs-lookup"><span data-stu-id="91858-186">c.</span></span> <span data-ttu-id="91858-187">將「變更密碼 URL」貼到 [密碼變更 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="91858-187">Paste **Change Password URL** into the **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="91858-188">d.</span><span class="sxs-lookup"><span data-stu-id="91858-188">d.</span></span> <span data-ttu-id="91858-189">將「登出 URL」貼到 [登出 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="91858-189">Paste **Sign-Out URL** into the **Logout URL** textbox.</span></span>

11. <span data-ttu-id="91858-190">繼續執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="91858-190">Move on with the following steps:</span></span>
    
    <span data-ttu-id="91858-191">![儲存變更](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "儲存變更")</span><span class="sxs-lookup"><span data-stu-id="91858-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="91858-192">a.</span><span class="sxs-lookup"><span data-stu-id="91858-192">a.</span></span> <span data-ttu-id="91858-193">在 [使用者識別碼] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`。</span><span class="sxs-lookup"><span data-stu-id="91858-193">In the **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="91858-194">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="91858-194">b.</span></span> <span data-ttu-id="91858-195">在 [電子郵件] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`。</span><span class="sxs-lookup"><span data-stu-id="91858-195">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="91858-196">c.</span><span class="sxs-lookup"><span data-stu-id="91858-196">c.</span></span> <span data-ttu-id="91858-197">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="91858-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="91858-198">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="91858-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="91858-199">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="91858-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="91858-200">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="91858-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="91858-201">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="91858-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="91858-202">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="91858-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="91858-204">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="91858-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="91858-205">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="91858-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="91858-207">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="91858-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="91858-209">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="91858-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="91858-211">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="91858-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="91858-213">a.</span><span class="sxs-lookup"><span data-stu-id="91858-213">a.</span></span> <span data-ttu-id="91858-214">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="91858-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91858-215">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="91858-215">b.</span></span> <span data-ttu-id="91858-216">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="91858-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="91858-217">c.</span><span class="sxs-lookup"><span data-stu-id="91858-217">c.</span></span> <span data-ttu-id="91858-218">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="91858-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="91858-219">d.</span><span class="sxs-lookup"><span data-stu-id="91858-219">d.</span></span> <span data-ttu-id="91858-220">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="91858-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="91858-221">建立 BlueJeans 測試使用者</span><span class="sxs-lookup"><span data-stu-id="91858-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="91858-222">若要讓 Azure AD 使用者能夠登入 BlueJeans，必須將他們佈建到 BlueJeans。</span><span class="sxs-lookup"><span data-stu-id="91858-222">To enable Azure AD users to log in to BlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="91858-223">就 BlueJeans 而言，需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="91858-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="91858-224">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="91858-224">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="91858-225">以系統管理員身分登入您的 **BlueJeans** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="91858-225">Log in to your **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="91858-226">移至 [管理] \> [管理使用者] \> [加入使用者]。</span><span class="sxs-lookup"><span data-stu-id="91858-226">Go to **ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="91858-227">![管理](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "管理")</span><span class="sxs-lookup"><span data-stu-id="91858-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="91858-228">只有在未核取 [安全性] 索引標籤中的 [啟用自動佈建] 時，才能使用 [加入使用者] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="91858-228">The **Add User** tab is only available if, in the **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="91858-229">在 [加入使用者] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="91858-229">In the **Add User** section, perform the following steps:</span></span>

    <span data-ttu-id="91858-230">![新增使用者](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="91858-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="91858-231">a.</span><span class="sxs-lookup"><span data-stu-id="91858-231">a.</span></span> <span data-ttu-id="91858-232">在相關的文字方塊中，輸入您想要佈建之有效 AAD 帳戶的 [BlueJeans 使用者名稱]、[電子郵件地址]、[BlueJeans 會議識別碼]、[仲裁者密碼]、[全名]、[公司]。</span><span class="sxs-lookup"><span data-stu-id="91858-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, the **Company** of a valid AAD account you want to provision into the related textboxes.</span></span>
    
    <span data-ttu-id="91858-233">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="91858-233">b.</span></span> <span data-ttu-id="91858-234">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="91858-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="91858-235">您可以使用任何其他的 BlueJeans 使用者帳戶建立工具或 BlueJeans 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="91858-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="91858-236">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="91858-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="91858-237">在本節中，您會將 BlueJeans 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91858-237">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BlueJeans.</span></span>

![指派使用者][200] 

<span data-ttu-id="91858-239">**若要將 Britta Simon 指派給 BlueJeans，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="91858-239">**To assign Britta Simon to BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="91858-240">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="91858-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="91858-242">在應用程式清單中，選取 [BlueJeans]。</span><span class="sxs-lookup"><span data-stu-id="91858-242">In the applications list, select **BlueJeans**.</span></span>

    ![設定單一登入](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="91858-244">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="91858-244">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="91858-246">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="91858-246">Click **Add** button.</span></span> <span data-ttu-id="91858-247">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="91858-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="91858-249">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="91858-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="91858-250">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="91858-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="91858-251">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="91858-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="91858-252">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="91858-252">Testing single sign-on</span></span>

<span data-ttu-id="91858-253">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="91858-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="91858-254">當您在「存取面板」中按一下 [BlueJeans] 圖格時，應該會看到 BlueJeans 應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="91858-254">When you click the BlueJeans tile in the Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="91858-255">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="91858-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="91858-256">其他資源</span><span class="sxs-lookup"><span data-stu-id="91858-256">Additional resources</span></span>

* [<span data-ttu-id="91858-257">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="91858-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91858-258">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="91858-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

