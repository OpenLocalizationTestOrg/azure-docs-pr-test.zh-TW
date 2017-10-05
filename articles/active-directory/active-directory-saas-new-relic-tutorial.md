---
title: "教學課程：Azure Active Directory 與 New Relic 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 New Relic 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 605e85c23a849f70fcc0237361d7a891f716ca3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="3f414-103">教學課程：Azure Active Directory 與 New Relic 整合</span><span class="sxs-lookup"><span data-stu-id="3f414-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="3f414-104">在本教學課程中，您將了解如何整合 New Relic 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="3f414-104">In this tutorial, you learn how to integrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3f414-105">New Relic 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="3f414-105">Integrating New Relic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3f414-106">您可以在 Azure AD 中控制可存取 New Relic 的人員</span><span class="sxs-lookup"><span data-stu-id="3f414-106">You can control in Azure AD who has access to New Relic</span></span>
- <span data-ttu-id="3f414-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 New Relic (單一登入)</span><span class="sxs-lookup"><span data-stu-id="3f414-107">You can enable your users to automatically get signed-on to New Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3f414-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="3f414-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3f414-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="3f414-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f414-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="3f414-110">Prerequisites</span></span>

<span data-ttu-id="3f414-111">若要設定與 New Relic 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="3f414-111">To configure Azure AD integration with New Relic, you need the following items:</span></span>

- <span data-ttu-id="3f414-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3f414-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3f414-113">啟用 New Relic 單一登入的訂閱</span><span class="sxs-lookup"><span data-stu-id="3f414-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3f414-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3f414-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3f414-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="3f414-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3f414-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3f414-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3f414-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="3f414-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3f414-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="3f414-118">Scenario description</span></span>
<span data-ttu-id="3f414-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3f414-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3f414-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="3f414-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3f414-121">從資源庫新增 New Relic</span><span class="sxs-lookup"><span data-stu-id="3f414-121">Adding New Relic from the gallery</span></span>
2. <span data-ttu-id="3f414-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3f414-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-the-gallery"></a><span data-ttu-id="3f414-123">從資源庫新增 New Relic</span><span class="sxs-lookup"><span data-stu-id="3f414-123">Adding New Relic from the gallery</span></span>
<span data-ttu-id="3f414-124">若要設定將 New Relic 整合到 Azure AD 中，您需要從資源庫將 New Relic 新增到受管理的 SaaS app 清單。</span><span class="sxs-lookup"><span data-stu-id="3f414-124">To configure the integration of New Relic into Azure AD, you need to add New Relic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3f414-125">**若要從資源庫新增 New Relic，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3f414-125">**To add New Relic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3f414-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="3f414-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3f414-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3f414-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3f414-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3f414-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="3f414-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3f414-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="3f414-133">在搜尋方塊中，輸入 **New Relic**。</span><span class="sxs-lookup"><span data-stu-id="3f414-133">In the search box, type **New Relic**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="3f414-135">在結果窗格中，選取 [New Relic]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f414-135">In the results panel, select **New Relic**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3f414-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3f414-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3f414-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 New Relic 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3f414-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3f414-139">若要讓單一登入運作，Azure AD 必須知道 New Relic 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="3f414-139">For single sign-on to work, Azure AD needs to know what the counterpart user in New Relic is to a user in Azure AD.</span></span> <span data-ttu-id="3f414-140">換句話說，必須建立 Azure AD 使用者和 New Relic 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="3f414-140">In other words, a link relationship between an Azure AD user and the related user in New Relic needs to be established.</span></span>

<span data-ttu-id="3f414-141">在 New Relic 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="3f414-141">In New Relic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3f414-142">若要使用 New Relic 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="3f414-142">To configure and test Azure AD single sign-on with New Relic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3f414-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="3f414-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3f414-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3f414-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3f414-145">**[建立 New Relic 測試使用者](#creating-a-new-relic-test-user)** - 使 New Relic 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="3f414-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - to have a counterpart of Britta Simon in New Relic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3f414-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3f414-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3f414-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="3f414-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3f414-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3f414-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3f414-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 New Relic 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="3f414-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="3f414-150">**若要使用 New Relic 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3f414-150">**To configure Azure AD single sign-on with New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="3f414-151">在 Azure 入口網站的 [New Relic] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="3f414-151">In the Azure portal, on the **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="3f414-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="3f414-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="3f414-155">在 [New Relic 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3f414-155">On the **New Relic Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="3f414-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="3f414-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3f414-158">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="3f414-158">The value is not real.</span></span> <span data-ttu-id="3f414-159">請使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="3f414-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="3f414-160">請連絡 [New Relic 客戶支援小組](https://support.newrelic.com/)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="3f414-160">Contact [New Relic Client support team](https://support.newrelic.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="3f414-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="3f414-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="3f414-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3f414-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3f414-165">在 [New Relic 組態] 區段上，按一下 [設定 New Relic] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="3f414-165">On the **New Relic Configuration** section, click **Configure New Relic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3f414-166">從 [快速參考] 區段中複製 [登出 URL 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="3f414-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="3f414-168">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 **New Relic** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="3f414-168">In a different web browser window, sign on to your **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="3f414-169">在頂端的功能表中，按一下 [帳戶設定] 。</span><span class="sxs-lookup"><span data-stu-id="3f414-169">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="3f414-170">![帳戶設定](./media/active-directory-saas-new-relic-tutorial/ic797036.png "帳戶設定")</span><span class="sxs-lookup"><span data-stu-id="3f414-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="3f414-171">按一下 [安全性及驗證] 索引標籤，然後再按一下 [單一登入] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3f414-171">Click the **Security and authentication** tab, and then click the **Single sign on** tab.</span></span>
   
    <span data-ttu-id="3f414-172">![單一登入](./media/active-directory-saas-new-relic-tutorial/ic797037.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="3f414-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="3f414-173">在 SAML 對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3f414-173">On the SAML dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="3f414-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="3f414-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="3f414-175">a.</span><span class="sxs-lookup"><span data-stu-id="3f414-175">a.</span></span> <span data-ttu-id="3f414-176">按一下 [選擇檔案]  上傳已下載的 Azure Active Directory 憑證。</span><span class="sxs-lookup"><span data-stu-id="3f414-176">Click **Choose File** to upload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="3f414-177">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f414-177">b.</span></span> <span data-ttu-id="3f414-178">在 [遠端登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的**「SAML 單一登入服務 URL」**值。</span><span class="sxs-lookup"><span data-stu-id="3f414-178">In the **Remote login URL** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="3f414-179">c.</span><span class="sxs-lookup"><span data-stu-id="3f414-179">c.</span></span> <span data-ttu-id="3f414-180">在 [登出登陸 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="3f414-180">In the **Logout landing URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="3f414-181">d.</span><span class="sxs-lookup"><span data-stu-id="3f414-181">d.</span></span> <span data-ttu-id="3f414-182">按一下 [儲存我的變更] 。</span><span class="sxs-lookup"><span data-stu-id="3f414-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="3f414-183">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="3f414-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3f414-184">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="3f414-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3f414-185">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3f414-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3f414-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3f414-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="3f414-187">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="3f414-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="3f414-189">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3f414-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3f414-190">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="3f414-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3f414-192">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="3f414-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3f414-194">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="3f414-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3f414-196">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3f414-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3f414-198">a.</span><span class="sxs-lookup"><span data-stu-id="3f414-198">a.</span></span> <span data-ttu-id="3f414-199">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="3f414-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3f414-200">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f414-200">b.</span></span> <span data-ttu-id="3f414-201">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="3f414-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3f414-202">c.</span><span class="sxs-lookup"><span data-stu-id="3f414-202">c.</span></span> <span data-ttu-id="3f414-203">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="3f414-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3f414-204">d.</span><span class="sxs-lookup"><span data-stu-id="3f414-204">d.</span></span> <span data-ttu-id="3f414-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3f414-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="3f414-206">建立 New Relic 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3f414-206">Creating a New Relic test user</span></span>

<span data-ttu-id="3f414-207">為了讓 Azure Active Directory 使用者登入 New Relic，他們必須佈建到 New Relic 中。</span><span class="sxs-lookup"><span data-stu-id="3f414-207">In order to enable Azure Active Directory users to log in to New Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="3f414-208">在 New Relic 的情況下，需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="3f414-208">In the case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="3f414-209">**若要將使用者帳戶佈建到 New Relic，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3f414-209">**To provision a user account to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="3f414-210">以系統管理員身分登入您的 **New Relic** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="3f414-210">Log in to your **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="3f414-211">在頂端的功能表中，按一下 [帳戶設定] 。</span><span class="sxs-lookup"><span data-stu-id="3f414-211">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="3f414-212">![帳戶設定](./media/active-directory-saas-new-relic-tutorial/ic797040.png "帳戶設定")</span><span class="sxs-lookup"><span data-stu-id="3f414-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="3f414-213">在左邊的**帳戶**窗格中按一下 [摘要]，然後按一下 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="3f414-213">In the **Account** pane on the left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="3f414-214">![帳戶設定](./media/active-directory-saas-new-relic-tutorial/ic797041.png "帳戶設定")</span><span class="sxs-lookup"><span data-stu-id="3f414-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="3f414-215">在 [作用中使用者]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3f414-215">On the **Active users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="3f414-216">![作用中使用者](./media/active-directory-saas-new-relic-tutorial/ic797042.png "作用中使用者")</span><span class="sxs-lookup"><span data-stu-id="3f414-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="3f414-217">a.</span><span class="sxs-lookup"><span data-stu-id="3f414-217">a.</span></span> <span data-ttu-id="3f414-218">在 [電子郵件]  文字方塊中輸入您想要佈建的有效 Azure Active Directory 使用者電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="3f414-218">In the **Email** textbox, type the email address of a valid Azure Active Directory user you want to provision.</span></span>

    <span data-ttu-id="3f414-219">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f414-219">b.</span></span> <span data-ttu-id="3f414-220">針對 [角色]，選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="3f414-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="3f414-221">c.</span><span class="sxs-lookup"><span data-stu-id="3f414-221">c.</span></span> <span data-ttu-id="3f414-222">按一下 [新增此使用者] 。</span><span class="sxs-lookup"><span data-stu-id="3f414-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="3f414-223">您可以使用任何其他的 New Relic 使用者帳戶建立工具或 New Relic 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f414-223">You can use any other New Relic user account creation tools or APIs provided by New Relic to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3f414-224">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3f414-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3f414-225">在本節中，您會將 New Relic 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3f414-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to New Relic.</span></span>

![指派使用者][200] 

<span data-ttu-id="3f414-227">**若要將 Britta Simon 指派到 New Relic，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="3f414-227">**To assign Britta Simon to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="3f414-228">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3f414-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="3f414-230">在應用程式清單中，選取 [New Relic]。</span><span class="sxs-lookup"><span data-stu-id="3f414-230">In the applications list, select **New Relic**.</span></span>

    ![設定單一登入](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="3f414-232">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3f414-232">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="3f414-234">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3f414-234">Click **Add** button.</span></span> <span data-ttu-id="3f414-235">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3f414-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="3f414-237">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="3f414-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3f414-238">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3f414-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3f414-239">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3f414-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3f414-240">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="3f414-240">Testing single sign-on</span></span>

<span data-ttu-id="3f414-241">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="3f414-241">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3f414-242">當您在存取面板中按一下 [New Relic] 圖格時，應該會自動登入您的 New Relic 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f414-242">When you click the New Relic tile in the Access Panel, you should get automatically signed-on to your New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3f414-243">其他資源</span><span class="sxs-lookup"><span data-stu-id="3f414-243">Additional resources</span></span>

* [<span data-ttu-id="3f414-244">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="3f414-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3f414-245">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="3f414-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

