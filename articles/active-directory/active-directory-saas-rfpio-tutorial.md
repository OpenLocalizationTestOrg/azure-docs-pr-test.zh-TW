---
title: "教學課程：Azure Active Directory 與 RFPIO 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 RFPIO 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 26a8bb17dad5a01b401ce7f9b484f09822825cbf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="838a7-103">教學課程：Azure Active Directory 與 RFPIO 整合</span><span class="sxs-lookup"><span data-stu-id="838a7-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="838a7-104">在本教學課程中，您會了解如何整合 RFPIO 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="838a7-104">In this tutorial, you learn how to integrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="838a7-105">RFPIO 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="838a7-105">Integrating RFPIO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="838a7-106">您可以在 Azure AD 中控制可存取 RFPIO 的人員。</span><span class="sxs-lookup"><span data-stu-id="838a7-106">You can control who in Azure AD who has access to RFPIO.</span></span>
- <span data-ttu-id="838a7-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 RFPIO (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="838a7-107">You can enable your users to automatically get signed-on to RFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="838a7-108">您可以在 Azure 入口網站集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="838a7-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="838a7-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="838a7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="838a7-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="838a7-110">Prerequisites</span></span>

<span data-ttu-id="838a7-111">若要設定 Azure AD 與 RFPIO 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="838a7-111">To configure Azure AD integration with RFPIO, you need the following items:</span></span>

- <span data-ttu-id="838a7-112">Azure AD 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="838a7-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="838a7-113">已啟用 RFPIO 單一登入的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="838a7-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="838a7-114">我們不建議使用生產環境來測試本教學課程中的步驟。</span><span class="sxs-lookup"><span data-stu-id="838a7-114">We don't recommend that you use a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="838a7-115">若要測試本教學課程中的步驟，請遵循下列建議：</span><span class="sxs-lookup"><span data-stu-id="838a7-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="838a7-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="838a7-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="838a7-117">如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="838a7-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="838a7-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="838a7-118">Scenario description</span></span>
<span data-ttu-id="838a7-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="838a7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="838a7-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="838a7-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="838a7-121">從資源庫新增 RFPIO。</span><span class="sxs-lookup"><span data-stu-id="838a7-121">Adding RFPIO from the gallery.</span></span>
2. <span data-ttu-id="838a7-122">設定並測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="838a7-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-the-gallery"></a><span data-ttu-id="838a7-123">從資源庫新增 RFPIO</span><span class="sxs-lookup"><span data-stu-id="838a7-123">Add RFPIO from the gallery</span></span>
<span data-ttu-id="838a7-124">若要設定將 RFPIO 整合到 Azure AD 中，您需要從資源庫將 RFPIO 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="838a7-124">To configure the integration of RFPIO into Azure AD, you need to add RFPIO from the gallery to your list of managed SaaS apps.</span></span>

### <a name="to-add-rfpio-from-the-gallery"></a><span data-ttu-id="838a7-125">從資源庫新增 RFPIO</span><span class="sxs-lookup"><span data-stu-id="838a7-125">To add RFPIO from the gallery</span></span>

1. <span data-ttu-id="838a7-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，選取 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="838a7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="838a7-128">選取 [企業應用程式]，然後選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="838a7-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="838a7-130">若要新增新的應用程式，請選取對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="838a7-130">To add a new application, select the **New application** button on the top of dialog box.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="838a7-132">在搜尋方塊中，輸入 **RFPIO**。</span><span class="sxs-lookup"><span data-stu-id="838a7-132">In the search box, type **RFPIO**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="838a7-134">在結果窗格中，選取 [RFPIO]，然後選取 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="838a7-134">In the results panel, select **RFPIO**, and then select the **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="838a7-136">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="838a7-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="838a7-137">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 RFPIO 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="838a7-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="838a7-138">若要讓單一登入能夠運作，Azure AD 必須知道 RFPIO 中的對應使用者與 Azure AD 中的使用者之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="838a7-138">For single sign-on to work, Azure AD needs to know what the relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="838a7-139">換句話說，必須建立 Azure AD 使用者和 RFPIO 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="838a7-139">In other words, a link relationship between an Azure AD user and the related user in RFPIO needs to be established.</span></span>

<span data-ttu-id="838a7-140">在 RFPIO 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="838a7-140">In RFPIO, assign the value of **user name** in Azure AD as the value of  **Username** to establish the link relationship.</span></span>

<span data-ttu-id="838a7-141">若要設定及測試與 RFPIO 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="838a7-141">To configure and test Azure AD single sign-on with RFPIO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="838a7-142">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -- 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="838a7-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--to enable your users to use this feature.</span></span>
2. <span data-ttu-id="838a7-143">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -- 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="838a7-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="838a7-144">**[建立 RFPIO 測試使用者](#creating-a-rfpio-test-user)** -- 在 RFPIO 中建立一個與 Azure AD 中代表使用者的項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="838a7-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --to have a counterpart of Britta Simon in RFPIO that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="838a7-145">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** -- 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="838a7-145">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)**--to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="838a7-146">**[測試單一登入](#testing-single-sign-on)** -- 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="838a7-146">**[Test Single Sign-On](#testing-single-sign-on)** --to verify if the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="838a7-147">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="838a7-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="838a7-148">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 RFPIO 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="838a7-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="838a7-149">**若要設定與 RFPIO 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="838a7-149">**To configure Azure AD single sign-on with RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="838a7-150">在 Azure 入口網站的 [RFPIO] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="838a7-150">In the Azure portal, on the **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="838a7-152">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="838a7-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="838a7-154">如果您想要以 **IDP** 起始模式設定應用程式，請在 [RFPIO 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="838a7-154">On the **RFPIO Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="838a7-156">a.</span><span class="sxs-lookup"><span data-stu-id="838a7-156">a.</span></span> <span data-ttu-id="838a7-157">在 [識別碼] 文字方塊中，輸入 URL：`https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="838a7-157">In the **Identifier** textbox, type the URL: `https://www.rfpio.com`</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="838a7-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="838a7-159">b.</span></span> <span data-ttu-id="838a7-160">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="838a7-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="838a7-161">c.</span><span class="sxs-lookup"><span data-stu-id="838a7-161">c.</span></span> <span data-ttu-id="838a7-162">在 [回覆狀態] 文字方塊中輸入一個字串值。</span><span class="sxs-lookup"><span data-stu-id="838a7-162">In the **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="838a7-163">請連絡 [RFPIO 支援小組](https://www.rfpio.com/contact/)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="838a7-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) to get this value.</span></span> 

4. <span data-ttu-id="838a7-164">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="838a7-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="838a7-165">如果您想要以 **SP** 起始模式設定應用程式：</span><span class="sxs-lookup"><span data-stu-id="838a7-165">If you wish to configure the application in **SP** initiated mode:</span></span> 

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="838a7-167">在 [登入 URL] 文字方塊中，輸入 URL：`https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="838a7-167">In the **Sign on URL** textbox, type the URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="838a7-168">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="838a7-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="838a7-170">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="838a7-170">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="838a7-172">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **RFPIO** 網站。</span><span class="sxs-lookup"><span data-stu-id="838a7-172">In a different web browser window, login to the **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="838a7-173">按一下左上角的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="838a7-173">Click on the bottom left corner dropdown.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="838a7-175">按一下 [組織設定]。</span><span class="sxs-lookup"><span data-stu-id="838a7-175">Click on the **Organization Settings**.</span></span> 

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="838a7-177">按一下 [功能和整合]。</span><span class="sxs-lookup"><span data-stu-id="838a7-177">Click on the **FEATURES & INTEGRATION**.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="838a7-179">在 [SAML SSO 組態] 中按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="838a7-179">In the **SAML SSO Configuration** Click **Edit**.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="838a7-181">在本節中執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="838a7-181">In this Section perform following actions:</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="838a7-183">a.</span><span class="sxs-lookup"><span data-stu-id="838a7-183">a.</span></span> <span data-ttu-id="838a7-184">複製 [下載的中繼資料 XML] 內容，然後貼到 [身分識別組態] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="838a7-184">Copy the content of the **Downloaded Metadata XML** and paste it into the **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="838a7-185">若要複製下載的 [中繼資料 XML] 內容，請使用 [Notepad++] 或適當的 [XML 編輯器]。</span><span class="sxs-lookup"><span data-stu-id="838a7-185">To copy the content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="838a7-186">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="838a7-186">b.</span></span> <span data-ttu-id="838a7-187">按一下 [驗證] 。</span><span class="sxs-lookup"><span data-stu-id="838a7-187">Click **Validate**.</span></span>

    <span data-ttu-id="838a7-188">c.</span><span class="sxs-lookup"><span data-stu-id="838a7-188">c.</span></span> <span data-ttu-id="838a7-189">按一下 [驗證] 後，將 [SAML (已啟用)] 翻轉為開啟狀態。</span><span class="sxs-lookup"><span data-stu-id="838a7-189">After Clicking **Validate**, Flip **SAML(Enabled)** to on.</span></span>

    <span data-ttu-id="838a7-190">d.</span><span class="sxs-lookup"><span data-stu-id="838a7-190">d.</span></span> <span data-ttu-id="838a7-191">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="838a7-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="838a7-192">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="838a7-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="838a7-193">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="838a7-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="838a7-194">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="838a7-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="838a7-195">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="838a7-195">Create an Azure AD test user</span></span>
<span data-ttu-id="838a7-196">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="838a7-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="838a7-198">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="838a7-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="838a7-199">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="838a7-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="838a7-201">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="838a7-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="838a7-203">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="838a7-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="838a7-205">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="838a7-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="838a7-207">a.</span><span class="sxs-lookup"><span data-stu-id="838a7-207">a.</span></span> <span data-ttu-id="838a7-208">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="838a7-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="838a7-209">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="838a7-209">b.</span></span> <span data-ttu-id="838a7-210">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="838a7-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="838a7-211">c.</span><span class="sxs-lookup"><span data-stu-id="838a7-211">c.</span></span> <span data-ttu-id="838a7-212">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="838a7-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="838a7-213">d.</span><span class="sxs-lookup"><span data-stu-id="838a7-213">d.</span></span> <span data-ttu-id="838a7-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="838a7-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="838a7-215">建立 RFPIO 測試使用者</span><span class="sxs-lookup"><span data-stu-id="838a7-215">Create a RFPIO test user</span></span>

<span data-ttu-id="838a7-216">若要讓 Azure AD 使用者登入 RFPIO，必須將他們佈建到 RFPIO。</span><span class="sxs-lookup"><span data-stu-id="838a7-216">To enable Azure AD users to log in to RFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="838a7-217">RFPIO 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="838a7-217">In the case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="838a7-218">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="838a7-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="838a7-219">以系統管理員身分登入您的 RFPIO 公司網站。</span><span class="sxs-lookup"><span data-stu-id="838a7-219">Log in to your RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="838a7-220">按一下左上角的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="838a7-220">Click on the bottom left corner dropdown.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="838a7-222">按一下 [組織設定]。</span><span class="sxs-lookup"><span data-stu-id="838a7-222">Click on the **Organization Settings**.</span></span> 

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="838a7-224">按一下 [小組成員]。</span><span class="sxs-lookup"><span data-stu-id="838a7-224">Click **TEAM MEMBERS**.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="838a7-226">按一下 [新增成員]。</span><span class="sxs-lookup"><span data-stu-id="838a7-226">Click on **ADD MEMBERS**.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="838a7-228">在 [新增成員] 區段中。</span><span class="sxs-lookup"><span data-stu-id="838a7-228">In the **Add New Members** section.</span></span> <span data-ttu-id="838a7-229">執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="838a7-229">Perform following actions:</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="838a7-231">a.</span><span class="sxs-lookup"><span data-stu-id="838a7-231">a.</span></span> <span data-ttu-id="838a7-232">在 [每行輸入一個電子郵件] 欄位中輸入[電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="838a7-232">Enter **Email address** in the **Enter one email per line** field.</span></span>

    <span data-ttu-id="838a7-233">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="838a7-233">b.</span></span> <span data-ttu-id="838a7-234">請根據您的需求選取 [角色]。</span><span class="sxs-lookup"><span data-stu-id="838a7-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="838a7-235">c.</span><span class="sxs-lookup"><span data-stu-id="838a7-235">c.</span></span> <span data-ttu-id="838a7-236">按一下[新增成員]。</span><span class="sxs-lookup"><span data-stu-id="838a7-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="838a7-237">Azure Active Directory 帳戶的持有者會收到一封電子郵件，並依照連結在啟用其帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="838a7-237">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="838a7-238">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="838a7-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="838a7-239">在本節中，您會將 RFPIO 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="838a7-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RFPIO.</span></span>

![指派使用者][200] 

<span data-ttu-id="838a7-241">**若要將 Britta Simon 指派給 RFPIO，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="838a7-241">**To assign Britta Simon to RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="838a7-242">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="838a7-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="838a7-244">在應用程式清單中，選取 [RFPIO]。</span><span class="sxs-lookup"><span data-stu-id="838a7-244">In the applications list, select **RFPIO**.</span></span>

    ![設定單一登入](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="838a7-246">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="838a7-246">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="838a7-248">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="838a7-248">Click **Add** button.</span></span> <span data-ttu-id="838a7-249">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="838a7-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="838a7-251">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="838a7-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="838a7-252">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="838a7-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="838a7-253">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="838a7-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="838a7-254">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="838a7-254">Test single sign-on</span></span>

<span data-ttu-id="838a7-255">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="838a7-255">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="838a7-256">當您在存取面板中按一下 RFPIO 圖格時，應該會自動登入您的 RFPIO 應用程式。</span><span class="sxs-lookup"><span data-stu-id="838a7-256">When you click the RFPIO tile in the Access Panel, you should get automatically signed-on to your RFPIO application.</span></span>
<span data-ttu-id="838a7-257">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="838a7-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="838a7-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="838a7-258">Additional resources</span></span>

* [<span data-ttu-id="838a7-259">有關如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="838a7-259">List of tutorials about how to integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="838a7-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="838a7-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

