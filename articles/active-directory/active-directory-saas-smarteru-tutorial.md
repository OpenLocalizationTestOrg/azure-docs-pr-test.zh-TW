---
title: "教學課程：Azure Active Directory 與 SmarterU 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SmarterU 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 129d08c8a7b4228d4d5f1a3b7938ab649b2747a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="b3d92-103">教學課程：Azure Active Directory 與 SmarterU 整合</span><span class="sxs-lookup"><span data-stu-id="b3d92-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="b3d92-104">在本教學課程中，您會了解如何整合 SmarterU 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b3d92-104">In this tutorial, you learn how to integrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b3d92-105">SmarterU 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="b3d92-105">Integrating SmarterU with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b3d92-106">您可以在 Azure AD 中控制可存取 SmarterU 的人員</span><span class="sxs-lookup"><span data-stu-id="b3d92-106">You can control in Azure AD who has access to SmarterU</span></span>
- <span data-ttu-id="b3d92-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SmarterU (單一登入)</span><span class="sxs-lookup"><span data-stu-id="b3d92-107">You can enable your users to automatically get signed-on to SmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b3d92-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="b3d92-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b3d92-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b3d92-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3d92-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b3d92-110">Prerequisites</span></span>

<span data-ttu-id="b3d92-111">若要設定 Azure AD 與 SmarterU 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="b3d92-111">To configure Azure AD integration with SmarterU, you need the following items:</span></span>

- <span data-ttu-id="b3d92-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b3d92-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b3d92-113">已啟用 SmarterU 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b3d92-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b3d92-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b3d92-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b3d92-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b3d92-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b3d92-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b3d92-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b3d92-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="b3d92-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b3d92-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b3d92-118">Scenario description</span></span>
<span data-ttu-id="b3d92-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3d92-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b3d92-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="b3d92-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b3d92-121">從資源庫新增 SmarterU</span><span class="sxs-lookup"><span data-stu-id="b3d92-121">Adding SmarterU from the gallery</span></span>
2. <span data-ttu-id="b3d92-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b3d92-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-the-gallery"></a><span data-ttu-id="b3d92-123">從資源庫新增 SmarterU</span><span class="sxs-lookup"><span data-stu-id="b3d92-123">Adding SmarterU from the gallery</span></span>
<span data-ttu-id="b3d92-124">若要設定將 SmarterU 整合到 Azure AD 中，您需要從資源庫將 SmarterU 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="b3d92-124">To configure the integration of SmarterU into Azure AD, you need to add SmarterU from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b3d92-125">**若要從資源庫新增 SmarterU，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b3d92-125">**To add SmarterU from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b3d92-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="b3d92-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b3d92-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b3d92-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b3d92-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b3d92-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="b3d92-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3d92-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="b3d92-133">在搜尋方塊中，輸入 **SmarterU**。</span><span class="sxs-lookup"><span data-stu-id="b3d92-133">In the search box, type **SmarterU**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="b3d92-135">在結果窗格中，選取 [SmarterU]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3d92-135">In the results panel, select **SmarterU**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b3d92-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b3d92-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b3d92-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 SmarterU 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3d92-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b3d92-139">若要讓單一登入運作，Azure AD 必須知道 SmarterU 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="b3d92-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SmarterU is to a user in Azure AD.</span></span> <span data-ttu-id="b3d92-140">換句話說，必須在 Azure AD 使用者和 SmarterU 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b3d92-140">In other words, a link relationship between an Azure AD user and the related user in SmarterU needs to be established.</span></span>

<span data-ttu-id="b3d92-141">在 SmarterU 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b3d92-141">In SmarterU, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b3d92-142">若要設定及測試與 SmarterU 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="b3d92-142">To configure and test Azure AD single sign-on with SmarterU, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b3d92-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="b3d92-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b3d92-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3d92-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b3d92-145">**[建立 SmarterU 測試使用者](#creating-a-smarteru-test-user)** - 使 SmarterU 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="b3d92-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - to have a counterpart of Britta Simon in SmarterU that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b3d92-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3d92-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b3d92-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="b3d92-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b3d92-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b3d92-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b3d92-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 SmarterU 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3d92-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="b3d92-150">**若要使用 SmarterU 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b3d92-150">**To configure Azure AD single sign-on with SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="b3d92-151">在 Azure 入口網站的 [SmarterU] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="b3d92-151">In the Azure portal, on the **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="b3d92-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3d92-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="b3d92-155">在 [SmarterU 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b3d92-155">On the **SmarterU Domain and URLs** section, perform the following steps:</span></span> 

    ![設定單一登入](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="b3d92-157">在 [識別碼] 文字方塊中，輸入 URL：`https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="b3d92-157">In the **Identifier** textbox, type the URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="b3d92-158">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="b3d92-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="b3d92-160">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3d92-160">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b3d92-162">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 SmarterU 公司網站。</span><span class="sxs-lookup"><span data-stu-id="b3d92-162">In a different web browser window, log in to your SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="b3d92-163">在上方工具列中按一下 [帳戶設定] 。</span><span class="sxs-lookup"><span data-stu-id="b3d92-163">In the toolbar on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="b3d92-164">![帳戶設定](./media/active-directory-saas-smarteru-tutorial/IC777326.png "帳戶設定")</span><span class="sxs-lookup"><span data-stu-id="b3d92-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="b3d92-165">在 [帳戶組態] 頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b3d92-165">On the account configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="b3d92-166">![外部授權](./media/active-directory-saas-smarteru-tutorial/IC777327.png "外部授權")</span><span class="sxs-lookup"><span data-stu-id="b3d92-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="b3d92-167">a.</span><span class="sxs-lookup"><span data-stu-id="b3d92-167">a.</span></span> <span data-ttu-id="b3d92-168">選取 [啟用外部授權] 。</span><span class="sxs-lookup"><span data-stu-id="b3d92-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="b3d92-169">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3d92-169">b.</span></span> <span data-ttu-id="b3d92-170">在 [主要登入控制] 區段中，選取 [SmarterU] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b3d92-170">In the **Master Login Control** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="b3d92-171">c.</span><span class="sxs-lookup"><span data-stu-id="b3d92-171">c.</span></span> <span data-ttu-id="b3d92-172">在 [使用者預設登入] 區段中，選取 [SmarterU] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b3d92-172">In the **User Default Login** section, select the **SmarterU** tab.</span></span>
  
      <span data-ttu-id="b3d92-173">d.</span><span class="sxs-lookup"><span data-stu-id="b3d92-173">d.</span></span> <span data-ttu-id="b3d92-174">選取 [啟用 Okta] 。</span><span class="sxs-lookup"><span data-stu-id="b3d92-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="b3d92-175">e.</span><span class="sxs-lookup"><span data-stu-id="b3d92-175">e.</span></span> <span data-ttu-id="b3d92-176">複製下載的中繼資料檔案內容，然後貼到 [Okta 中繼資料]  文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="b3d92-176">Copy the content of the downloaded metadata file, and then paste it into the **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="b3d92-177">f.</span><span class="sxs-lookup"><span data-stu-id="b3d92-177">f.</span></span> <span data-ttu-id="b3d92-178">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b3d92-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b3d92-179">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="b3d92-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b3d92-180">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="b3d92-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b3d92-181">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b3d92-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b3d92-182">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b3d92-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="b3d92-183">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b3d92-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="b3d92-185">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b3d92-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b3d92-186">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="b3d92-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b3d92-188">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b3d92-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b3d92-190">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b3d92-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b3d92-192">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b3d92-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b3d92-194">a.</span><span class="sxs-lookup"><span data-stu-id="b3d92-194">a.</span></span> <span data-ttu-id="b3d92-195">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b3d92-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b3d92-196">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3d92-196">b.</span></span> <span data-ttu-id="b3d92-197">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="b3d92-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b3d92-198">c.</span><span class="sxs-lookup"><span data-stu-id="b3d92-198">c.</span></span> <span data-ttu-id="b3d92-199">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="b3d92-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b3d92-200">d.</span><span class="sxs-lookup"><span data-stu-id="b3d92-200">d.</span></span> <span data-ttu-id="b3d92-201">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b3d92-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="b3d92-202">建立 SmarterU 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b3d92-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="b3d92-203">若要讓 Azure AD 使用者能夠登入 SmarterU，必須將他們佈建到 SmarterU。</span><span class="sxs-lookup"><span data-stu-id="b3d92-203">To enable Azure AD users to log in to SmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="b3d92-204">SmarterU 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="b3d92-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="b3d92-205">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b3d92-205">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b3d92-206">登入您的 **SmarterU** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="b3d92-206">Log in to your **SmarterU** tenant.</span></span>

2. <span data-ttu-id="b3d92-207">移至 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="b3d92-207">Go to **Users**.</span></span>

3. <span data-ttu-id="b3d92-208">在 [使用者] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b3d92-208">In the user section, perform the following steps:</span></span>
   
    <span data-ttu-id="b3d92-209">![新增使用者](./media/active-directory-saas-smarteru-tutorial/IC777329.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="b3d92-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="b3d92-210">a.</span><span class="sxs-lookup"><span data-stu-id="b3d92-210">a.</span></span> <span data-ttu-id="b3d92-211">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="b3d92-211">Click **+User**.</span></span>
    
    <span data-ttu-id="b3d92-212">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3d92-212">b.</span></span> <span data-ttu-id="b3d92-213">在下列文字方塊中輸入該 Azure AD 使用者帳戶的相關屬性值：**主要電子郵件地址**、**員工識別碼**、**密碼**、**確認密碼**、**名字**、**姓氏**。</span><span class="sxs-lookup"><span data-stu-id="b3d92-213">Type the related attribute values of the Azure AD user account into the following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="b3d92-214">c.</span><span class="sxs-lookup"><span data-stu-id="b3d92-214">c.</span></span> <span data-ttu-id="b3d92-215">按一下 [作用中] 。</span><span class="sxs-lookup"><span data-stu-id="b3d92-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="b3d92-216">d.</span><span class="sxs-lookup"><span data-stu-id="b3d92-216">d.</span></span> <span data-ttu-id="b3d92-217">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b3d92-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="b3d92-218">您可以使用任何其他的 SmarterU 使用者帳戶建立工具或 SmarterU 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3d92-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b3d92-219">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b3d92-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b3d92-220">在本節中，您會將 SmarterU 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3d92-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SmarterU.</span></span>

![指派使用者][200] 

<span data-ttu-id="b3d92-222">**若要將 Britta Simon 指派給 SmarterU，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b3d92-222">**To assign Britta Simon to SmarterU, perform the following steps:**</span></span>

1. <span data-ttu-id="b3d92-223">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b3d92-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b3d92-225">在應用程式清單中，選取 [SmarterU]。</span><span class="sxs-lookup"><span data-stu-id="b3d92-225">In the applications list, select **SmarterU**.</span></span>

    ![設定單一登入](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="b3d92-227">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3d92-227">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="b3d92-229">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3d92-229">Click **Add** button.</span></span> <span data-ttu-id="b3d92-230">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3d92-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="b3d92-232">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="b3d92-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b3d92-233">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3d92-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b3d92-234">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3d92-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b3d92-235">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b3d92-235">Testing single sign-on</span></span>

<span data-ttu-id="b3d92-236">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="b3d92-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="b3d92-237">當您在 [存取面板] 中按一下 [SmarterU] 圖格時，應該會自動登入您的 SmarterU 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3d92-237">When you click the SmarterU tile in the Access Panel, you should get automatically signed-on to your SmarterU application.</span></span>
<span data-ttu-id="b3d92-238">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b3d92-238">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="b3d92-239">其他資源</span><span class="sxs-lookup"><span data-stu-id="b3d92-239">Additional resources</span></span>

* [<span data-ttu-id="b3d92-240">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="b3d92-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b3d92-241">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b3d92-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

