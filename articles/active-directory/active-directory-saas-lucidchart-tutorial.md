---
title: "教學課程：Azure Active Directory 與 Lucidchart 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Lucidchart 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2dea669f03c893632c08d30feeb3173efc2d8243
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a><span data-ttu-id="c0edd-103">教學課程：Azure Active Directory 與 Lucidchart 整合</span><span class="sxs-lookup"><span data-stu-id="c0edd-103">Tutorial: Azure Active Directory integration with Lucidchart</span></span>

<span data-ttu-id="c0edd-104">在本教學課程中，您將了解如何整合 Lucidchart 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="c0edd-104">In this tutorial, you learn how to integrate Lucidchart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0edd-105">Lucidchart 與 Azure AD 整合有下列優點：</span><span class="sxs-lookup"><span data-stu-id="c0edd-105">Integrating Lucidchart with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c0edd-106">您可以在 Azure AD 中控制可存取 Lucidchart 的人員</span><span class="sxs-lookup"><span data-stu-id="c0edd-106">You can control in Azure AD who has access to Lucidchart</span></span>
- <span data-ttu-id="c0edd-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Lucidchart (單一登入)</span><span class="sxs-lookup"><span data-stu-id="c0edd-107">You can enable your users to automatically get signed-on to Lucidchart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0edd-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="c0edd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c0edd-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c0edd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0edd-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c0edd-110">Prerequisites</span></span>

<span data-ttu-id="c0edd-111">若要進行 Azure AD 與 Lucidchart 整合的設定，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="c0edd-111">To configure Azure AD integration with Lucidchart, you need the following items:</span></span>

- <span data-ttu-id="c0edd-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c0edd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0edd-113">啟用 Lucidchart 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c0edd-113">A Lucidchart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0edd-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c0edd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0edd-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c0edd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0edd-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c0edd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0edd-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="c0edd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0edd-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="c0edd-118">Scenario description</span></span>
<span data-ttu-id="c0edd-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0edd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0edd-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="c0edd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0edd-121">從資源庫新增 Lucidchart</span><span class="sxs-lookup"><span data-stu-id="c0edd-121">Adding Lucidchart from the gallery</span></span>
2. <span data-ttu-id="c0edd-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c0edd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lucidchart-from-the-gallery"></a><span data-ttu-id="c0edd-123">從資源庫新增 Lucidchart</span><span class="sxs-lookup"><span data-stu-id="c0edd-123">Adding Lucidchart from the gallery</span></span>
<span data-ttu-id="c0edd-124">若要進行 Lucidchart 與 Azure AD 整合的設定，您需要從資源庫將 Lucidchart 新增至受管理 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="c0edd-124">To configure the integration of Lucidchart into Azure AD, you need to add Lucidchart from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c0edd-125">**若要從資源庫新增 Lucidchart，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c0edd-125">**To add Lucidchart from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c0edd-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="c0edd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0edd-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c0edd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c0edd-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c0edd-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="c0edd-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0edd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="c0edd-133">在搜尋方塊中，輸入 **Lucidchart**。</span><span class="sxs-lookup"><span data-stu-id="c0edd-133">In the search box, type **Lucidchart**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_search.png)

5. <span data-ttu-id="c0edd-135">在結果面板中，選取 [Lucidchart]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0edd-135">In the results panel, select **Lucidchart**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0edd-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c0edd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0edd-138">在本節中，您將以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Lucidchart 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0edd-138">In this section, you configure and test Azure AD single sign-on with Lucidchart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c0edd-139">為了讓單一登入正常運作，Azure AD 必須知道 Azure AD 使用者在 Lucidchart 中的對應使用者是誰。</span><span class="sxs-lookup"><span data-stu-id="c0edd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lucidchart is to a user in Azure AD.</span></span> <span data-ttu-id="c0edd-140">換句話說，必須在 Azure AD 使用者與 Lucidchart 的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="c0edd-140">In other words, a link relationship between an Azure AD user and the related user in Lucidchart needs to be established.</span></span>

<span data-ttu-id="c0edd-141">在 Lucidchar 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="c0edd-141">In Lucidchart, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c0edd-142">若要設定及測試與 Lucidchart 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="c0edd-142">To configure and test Azure AD single sign-on with Lucidchart, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c0edd-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="c0edd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c0edd-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0edd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0edd-145">**[建立 Lucidchart 測試使用者](#creating-a-lucidchart-test-user)** - 使 Lucidchart 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="c0edd-145">**[Creating a Lucidchart test user](#creating-a-lucidchart-test-user)** - to have a counterpart of Britta Simon in Lucidchart that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0edd-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0edd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0edd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="c0edd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0edd-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c0edd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0edd-149">在本節中，您將在 Azure 入口網站中啟用 Azure AD 單一登入，並在 Lucidchart 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0edd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lucidchart application.</span></span>

<span data-ttu-id="c0edd-150">**若要設定 Lucidchart 的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c0edd-150">**To configure Azure AD single sign-on with Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="c0edd-151">在 Azure 入口網站的 [Lucidchart] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="c0edd-151">In the Azure portal, on the **Lucidchart** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="c0edd-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0edd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

3. <span data-ttu-id="c0edd-155">在 [Lucidchart 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c0edd-155">On the **Lucidchart Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_url.png)

    <span data-ttu-id="c0edd-157">在 [登入 URL] 文字方塊中，將 URL 輸入為：`https://chart2.office.lucidchart.com/saml/sso/azure`</span><span class="sxs-lookup"><span data-stu-id="c0edd-157">In the **Sign-on URL** textbox, type a URL as: `https://chart2.office.lucidchart.com/saml/sso/azure`</span></span>

4. <span data-ttu-id="c0edd-158">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="c0edd-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

5. <span data-ttu-id="c0edd-160">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0edd-160">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-lucidchart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c0edd-162">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Lucidchart 公司網站。</span><span class="sxs-lookup"><span data-stu-id="c0edd-162">In a different web browser window, log into your Lucidchart company site as an administrator.</span></span>

7. <span data-ttu-id="c0edd-163">在頂端的功能表中，按一下 [小組] 。</span><span class="sxs-lookup"><span data-stu-id="c0edd-163">In the menu on the top, click **Team**.</span></span>
   
    <span data-ttu-id="c0edd-164">![小組](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "小組")</span><span class="sxs-lookup"><span data-stu-id="c0edd-164">![Team](./media/active-directory-saas-lucidchart-tutorial/ic791190.png "Team")</span></span>

8. <span data-ttu-id="c0edd-165">按一下 [應用程式] \> [管理 SAML]。</span><span class="sxs-lookup"><span data-stu-id="c0edd-165">Click **Applications \> Manage SAML**.</span></span>
   
    <span data-ttu-id="c0edd-166">![管理 SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "管理 SAML")</span><span class="sxs-lookup"><span data-stu-id="c0edd-166">![Manage SAML](./media/active-directory-saas-lucidchart-tutorial/ic791191.png "Manage SAML")</span></span>

9. <span data-ttu-id="c0edd-167">在 [SAML 驗證設定]  對話方塊頁面上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c0edd-167">On the **SAML Authentication Settings** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="c0edd-168">a.</span><span class="sxs-lookup"><span data-stu-id="c0edd-168">a.</span></span> <span data-ttu-id="c0edd-169">選取 [啟用 SAML 驗證]，然後按一下 [選用]。</span><span class="sxs-lookup"><span data-stu-id="c0edd-169">Select **Enable SAML Authentication**, and then click **Optional**.</span></span>

    <span data-ttu-id="c0edd-170">![SAML 驗證設定](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML 驗證設定")</span><span class="sxs-lookup"><span data-stu-id="c0edd-170">![SAML Authentication Settings](./media/active-directory-saas-lucidchart-tutorial/ic791192.png "SAML Authentication Settings")</span></span>
 
    <span data-ttu-id="c0edd-171">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0edd-171">b.</span></span> <span data-ttu-id="c0edd-172">在 [網域] 文字方塊中，輸入您的網域，然後按一下 [變更憑證]。 </span><span class="sxs-lookup"><span data-stu-id="c0edd-172">In the **Domain** textbox, type your domain, and then click **Change Certificate**.</span></span>

    <span data-ttu-id="c0edd-173">![變更憑證](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "變更憑證")</span><span class="sxs-lookup"><span data-stu-id="c0edd-173">![Change Certificate](./media/active-directory-saas-lucidchart-tutorial/ic791193.png "Change Certificate")</span></span>
 
    <span data-ttu-id="c0edd-174">c.</span><span class="sxs-lookup"><span data-stu-id="c0edd-174">c.</span></span> <span data-ttu-id="c0edd-175">開啟您下載的中繼資料檔案，然後複製內容並貼到並 [上傳中繼資料]  文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="c0edd-175">Open your downloaded metadata file, copy the content, and then paste it into the **Upload Metadata** textbox.</span></span>

    <span data-ttu-id="c0edd-176">![上傳中繼資料](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "上傳中繼資料")</span><span class="sxs-lookup"><span data-stu-id="c0edd-176">![Upload Metadata](./media/active-directory-saas-lucidchart-tutorial/ic791194.png "Upload Metadata")</span></span>
 
    <span data-ttu-id="c0edd-177">d.</span><span class="sxs-lookup"><span data-stu-id="c0edd-177">d.</span></span> <span data-ttu-id="c0edd-178">選取 [Automatically Add new users to the team]\(自動新增使用者至小組\)，然後按一下 [儲存變更]。</span><span class="sxs-lookup"><span data-stu-id="c0edd-178">Select **Automatically Add new users to the team**, and then click **Save changes**.</span></span>

    <span data-ttu-id="c0edd-179">![儲存變更](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "儲存變更")</span><span class="sxs-lookup"><span data-stu-id="c0edd-179">![Save Changes](./media/active-directory-saas-lucidchart-tutorial/ic791195.png "Save Changes")</span></span>

> [!TIP]
> <span data-ttu-id="c0edd-180">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="c0edd-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c0edd-181">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="c0edd-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c0edd-182">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0edd-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0edd-183">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c0edd-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0edd-184">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c0edd-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="c0edd-186">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c0edd-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c0edd-187">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="c0edd-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0edd-189">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="c0edd-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0edd-191">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="c0edd-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0edd-193">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c0edd-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lucidchart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0edd-195">a.</span><span class="sxs-lookup"><span data-stu-id="c0edd-195">a.</span></span> <span data-ttu-id="c0edd-196">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="c0edd-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0edd-197">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0edd-197">b.</span></span> <span data-ttu-id="c0edd-198">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="c0edd-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0edd-199">c.</span><span class="sxs-lookup"><span data-stu-id="c0edd-199">c.</span></span> <span data-ttu-id="c0edd-200">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="c0edd-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c0edd-201">d.</span><span class="sxs-lookup"><span data-stu-id="c0edd-201">d.</span></span> <span data-ttu-id="c0edd-202">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c0edd-202">Click **Create**.</span></span>
 
### <a name="creating-a-lucidchart-test-user"></a><span data-ttu-id="c0edd-203">建立 Lucidchart 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c0edd-203">Creating a Lucidchart test user</span></span>

<span data-ttu-id="c0edd-204">沒有動作項目可讓您設定 Lucidchart 使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="c0edd-204">There is no action item for you to configure user provisioning to Lucidchart.</span></span>  <span data-ttu-id="c0edd-205">當指派的使用者嘗試使用存取面板登入 Lucidchart 時，Lucidchart 會檢查使用者是否存在。</span><span class="sxs-lookup"><span data-stu-id="c0edd-205">When an assigned user tries to log into Lucidchart using the access panel, Lucidchart checks whether the user exists.</span></span>  

<span data-ttu-id="c0edd-206">如果尚無可用的使用者帳戶，Lucidchart 會自動予以建立。</span><span class="sxs-lookup"><span data-stu-id="c0edd-206">If there is no user account available yet, it is automatically created by Lucidchart.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c0edd-207">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c0edd-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c0edd-208">在本節中，您將把 Lucidchart 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0edd-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lucidchart.</span></span>

![指派使用者][200] 

<span data-ttu-id="c0edd-210">**若要將 Britta Simon 指派到 Lucidchart，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c0edd-210">**To assign Britta Simon to Lucidchart, perform the following steps:**</span></span>

1. <span data-ttu-id="c0edd-211">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c0edd-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c0edd-213">在應用程式清單中，選取 [Lucidchart]。</span><span class="sxs-lookup"><span data-stu-id="c0edd-213">In the applications list, select **Lucidchart**.</span></span>

    ![設定單一登入](./media/active-directory-saas-lucidchart-tutorial/tutorial_lucidchart_app.png) 

3. <span data-ttu-id="c0edd-215">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c0edd-215">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="c0edd-217">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0edd-217">Click **Add** button.</span></span> <span data-ttu-id="c0edd-218">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c0edd-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="c0edd-220">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="c0edd-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c0edd-221">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0edd-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0edd-222">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0edd-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0edd-223">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c0edd-223">Testing single sign-on</span></span>

<span data-ttu-id="c0edd-224">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="c0edd-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c0edd-225">按一下存取面板中的 [Lucidchart] 圖格，應會自動登入您的 Lucidchart 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0edd-225">When you click the Lucidchart tile in the Access Panel, you should get automatically signed-on to your Lucidchart application.</span></span>
<span data-ttu-id="c0edd-226">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="c0edd-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0edd-227">其他資源</span><span class="sxs-lookup"><span data-stu-id="c0edd-227">Additional resources</span></span>

* [<span data-ttu-id="c0edd-228">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="c0edd-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0edd-229">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c0edd-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lucidchart-tutorial/tutorial_general_203.png

