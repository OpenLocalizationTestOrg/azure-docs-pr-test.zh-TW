---
title: "教學課程：Azure Active Directory 與 LogicMonitor 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 LogicMonitor 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: e49960cac868f80af3e9165a9f75e49be87515f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="9b650-103">教學課程：Azure Active Directory 與 LogicMonitor 整合</span><span class="sxs-lookup"><span data-stu-id="9b650-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="9b650-104">在本教學課程中，您將了解如何整合 LogicMonitor 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="9b650-104">In this tutorial, you learn how to integrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9b650-105">LogicMonitor 與 Azure AD 整合有下列優點：</span><span class="sxs-lookup"><span data-stu-id="9b650-105">Integrating LogicMonitor with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9b650-106">您可以在 Azure AD 中控制可存取 LogicMonitor 的人員</span><span class="sxs-lookup"><span data-stu-id="9b650-106">You can control in Azure AD who has access to LogicMonitor</span></span>
- <span data-ttu-id="9b650-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 LogicMonitor (單一登入)</span><span class="sxs-lookup"><span data-stu-id="9b650-107">You can enable your users to automatically get signed-on to LogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9b650-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="9b650-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9b650-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="9b650-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b650-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9b650-110">Prerequisites</span></span>

<span data-ttu-id="9b650-111">若要進行 Azure AD 與 LogicMonitor 整合的設定，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="9b650-111">To configure Azure AD integration with LogicMonitor, you need the following items:</span></span>

- <span data-ttu-id="9b650-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9b650-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9b650-113">已啟用 LogicMonitor 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9b650-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9b650-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9b650-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9b650-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="9b650-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9b650-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9b650-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9b650-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="9b650-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9b650-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="9b650-118">Scenario description</span></span>
<span data-ttu-id="9b650-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9b650-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9b650-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="9b650-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9b650-121">從資源庫新增 LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="9b650-121">Adding LogicMonitor from the gallery</span></span>
2. <span data-ttu-id="9b650-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9b650-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-the-gallery"></a><span data-ttu-id="9b650-123">從資源庫新增 LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="9b650-123">Adding LogicMonitor from the gallery</span></span>
<span data-ttu-id="9b650-124">若要進行 LogicMonitor 與 Azure AD 整合的設定，您需要從資源庫將 LogicMonitor 新增至受管理 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="9b650-124">To configure the integration of LogicMonitor into Azure AD, you need to add LogicMonitor from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9b650-125">**若要從資源庫新增 LogicMonitor，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9b650-125">**To add LogicMonitor from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9b650-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="9b650-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9b650-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9b650-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9b650-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9b650-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="9b650-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b650-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="9b650-133">在搜尋方塊中，輸入 **LogicMonitor**。</span><span class="sxs-lookup"><span data-stu-id="9b650-133">In the search box, type **LogicMonitor**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="9b650-135">在結果面板中，選取 [LogicMonitor]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b650-135">In the results panel, select **LogicMonitor**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9b650-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9b650-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9b650-138">在本節中，您將以名為 "Britta Simon" 的測試使用者身分，設定及測試與 LogicMonitor 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9b650-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9b650-139">為了讓單一登入正常運作，Azure AD 必須知道 Azure AD 使用者在 LogicMonitor 中的對應使用者是誰。</span><span class="sxs-lookup"><span data-stu-id="9b650-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LogicMonitor is to a user in Azure AD.</span></span> <span data-ttu-id="9b650-140">換句話說，必須在 Azure AD 使用者與 LogicMonitor 的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9b650-140">In other words, a link relationship between an Azure AD user and the related user in LogicMonitor needs to be established.</span></span>

<span data-ttu-id="9b650-141">在 LogicMonitor 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9b650-141">In LogicMonitor, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9b650-142">若要設定及測試與 LogicMonitor 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="9b650-142">To configure and test Azure AD single sign-on with LogicMonitor, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9b650-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="9b650-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9b650-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9b650-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9b650-145">**[建立 LogicMonitor 測試使用者](#creating-a-logicmonitor-test-user)** - 使 LogicMonitor 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="9b650-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - to have a counterpart of Britta Simon in LogicMonitor that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9b650-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9b650-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9b650-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="9b650-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9b650-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9b650-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9b650-149">在本節中，您將在 Azure 入口網站中啟用 Azure AD 單一登入，並在 LogicMonitor 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="9b650-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="9b650-150">**若要設定 LogicMonitor 的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9b650-150">**To configure Azure AD single sign-on with LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="9b650-151">在 Azure 入口網站的 [LogicMonitor] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="9b650-151">In the Azure portal, on the **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="9b650-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="9b650-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="9b650-155">在 [LogicMonitor 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9b650-155">On the **LogicMonitor Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="9b650-157">a.</span><span class="sxs-lookup"><span data-stu-id="9b650-157">a.</span></span> <span data-ttu-id="9b650-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="9b650-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="9b650-159">b.</span><span class="sxs-lookup"><span data-stu-id="9b650-159">b.</span></span> <span data-ttu-id="9b650-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="9b650-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9b650-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="9b650-161">These values are not real.</span></span> <span data-ttu-id="9b650-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="9b650-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9b650-163">請連絡 [LogicMonitor 用戶端支援小組](https://www.logicmonitor.com/contact/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="9b650-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="9b650-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="9b650-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="9b650-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b650-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9b650-168">以系統管理員身分登入您的 **LogicMonitor** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="9b650-168">Log in to your **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="9b650-169">在頂端的功能表中，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="9b650-169">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="9b650-170">![設定](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "設定")</span><span class="sxs-lookup"><span data-stu-id="9b650-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="9b650-171">在左側導覽列中按一下 [單一登入] </span><span class="sxs-lookup"><span data-stu-id="9b650-171">In the navigation bat on the left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="9b650-172">![單一登入](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="9b650-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="9b650-173">在 [單一登入 (SSO) 設定]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9b650-173">In the **Single Sign-on (SSO) settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="9b650-174">![單一登入設定](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="9b650-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="9b650-175">a.</span><span class="sxs-lookup"><span data-stu-id="9b650-175">a.</span></span> <span data-ttu-id="9b650-176">選取 [啟用單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="9b650-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="9b650-177">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b650-177">b.</span></span> <span data-ttu-id="9b650-178">在 [預設角色指派] 中選取 [唯讀]。</span><span class="sxs-lookup"><span data-stu-id="9b650-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="9b650-179">c.</span><span class="sxs-lookup"><span data-stu-id="9b650-179">c.</span></span> <span data-ttu-id="9b650-180">在記事本中開啟下載的中繼資料檔，然後將檔案內容貼到 [識別提供者中繼資料]  文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="9b650-180">Open the downloaded metadata file in notepad, and then paste content of the file into the **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="9b650-181">d.</span><span class="sxs-lookup"><span data-stu-id="9b650-181">d.</span></span> <span data-ttu-id="9b650-182">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="9b650-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="9b650-183">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="9b650-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9b650-184">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="9b650-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9b650-185">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9b650-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9b650-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9b650-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="9b650-187">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="9b650-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="9b650-189">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9b650-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9b650-190">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="9b650-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9b650-192">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="9b650-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9b650-194">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9b650-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9b650-196">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9b650-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9b650-198">a.</span><span class="sxs-lookup"><span data-stu-id="9b650-198">a.</span></span> <span data-ttu-id="9b650-199">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="9b650-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9b650-200">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b650-200">b.</span></span> <span data-ttu-id="9b650-201">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="9b650-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9b650-202">c.</span><span class="sxs-lookup"><span data-stu-id="9b650-202">c.</span></span> <span data-ttu-id="9b650-203">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="9b650-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9b650-204">d.</span><span class="sxs-lookup"><span data-stu-id="9b650-204">d.</span></span> <span data-ttu-id="9b650-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9b650-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="9b650-206">建立 LogicMonitor 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9b650-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="9b650-207">若要讓 AAD 使用者能夠登入，必須使用他們的 Azure Active Directory 使用者名稱將他們佈建到 LogicMonitor 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b650-207">For AAD users to be able to sign in, they must be provisioned to the LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="9b650-208">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9b650-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="9b650-209">以系統管理員身分登入您的 LogicMonitor 公司網站。</span><span class="sxs-lookup"><span data-stu-id="9b650-209">Log in to your LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="9b650-210">在頂端的功能表中，按一下 [設定]，然後按一下 [角色與使用者]。</span><span class="sxs-lookup"><span data-stu-id="9b650-210">In the menu on the top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="9b650-211">![角色和使用者](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "角色和使用者")</span><span class="sxs-lookup"><span data-stu-id="9b650-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="9b650-212">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="9b650-212">Click **Add**.</span></span>

4. <span data-ttu-id="9b650-213">在 [新增帳戶]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9b650-213">In the **Add an account** section, perform the following steps:</span></span>
   
   <span data-ttu-id="9b650-214">![新增帳戶](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "新增帳戶")</span><span class="sxs-lookup"><span data-stu-id="9b650-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="9b650-215">a.</span><span class="sxs-lookup"><span data-stu-id="9b650-215">a.</span></span> <span data-ttu-id="9b650-216">在相關的文字方塊中輸入您想要佈建之 Azure Active Directory 使用者的 [使用者名稱]、[電子郵件]、[密碼] 及 [重新輸入密碼] 值。</span><span class="sxs-lookup"><span data-stu-id="9b650-216">Type the **Username**, **Email**, **Password**, and **Retype password** values of the Azure Active Directory user you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="9b650-217">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b650-217">b.</span></span> <span data-ttu-id="9b650-218">選取 [角色]、[檢視權限] 及 [狀態]。</span><span class="sxs-lookup"><span data-stu-id="9b650-218">Select **Roles**, **View Permissions**, and the **Status**.</span></span>
   
   <span data-ttu-id="9b650-219">c.</span><span class="sxs-lookup"><span data-stu-id="9b650-219">c.</span></span> <span data-ttu-id="9b650-220">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="9b650-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="9b650-221">您可以使用任何其他的 LogicMonitor 使用者帳戶建立工具或 LogicMonitor 提供的 API，佈建 Azure Active Directory 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b650-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9b650-222">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9b650-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9b650-223">在本節中，您將把 LogicMonitor 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9b650-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LogicMonitor.</span></span>

![指派使用者][200] 

<span data-ttu-id="9b650-225">**若要將 Britta Simon 指派到 LogicMonitor，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9b650-225">**To assign Britta Simon to LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="9b650-226">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9b650-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="9b650-228">在應用程式清單中，選取 [LogicMonitor]。</span><span class="sxs-lookup"><span data-stu-id="9b650-228">In the applications list, select **LogicMonitor**.</span></span>

    ![設定單一登入](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="9b650-230">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9b650-230">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="9b650-232">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b650-232">Click **Add** button.</span></span> <span data-ttu-id="9b650-233">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9b650-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="9b650-235">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="9b650-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9b650-236">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b650-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9b650-237">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b650-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9b650-238">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="9b650-238">Testing single sign-on</span></span>

<span data-ttu-id="9b650-239">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="9b650-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="9b650-240">按一下存取面板中的 [LogicMonitor] 圖格，應會自動登入您的 LogicMonitor 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b650-240">When you click the LogicMonitor tile in the Access Panel, you should get automatically signed-on to your LogicMonitor application.</span></span>
<span data-ttu-id="9b650-241">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="9b650-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9b650-242">其他資源</span><span class="sxs-lookup"><span data-stu-id="9b650-242">Additional resources</span></span>

* [<span data-ttu-id="9b650-243">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="9b650-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9b650-244">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="9b650-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

