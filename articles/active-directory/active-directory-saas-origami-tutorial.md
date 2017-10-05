---
title: "教學課程：Azure Active Directory 與 Origami 整合 | Microsoft Docs"
description: "了解如何在 Azure Active Directory 與 Origami 之間設定單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3420409b72ff032e64ac59365083dd141dfc3c1b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="59f13-103">教學課程：Azure Active Directory 與 Origami 整合</span><span class="sxs-lookup"><span data-stu-id="59f13-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="59f13-104">在本教學課程中，您會了解如何整合 Origami 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="59f13-104">In this tutorial, you learn how to integrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="59f13-105">Origami 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="59f13-105">Integrating Origami with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="59f13-106">您可以在 Azure AD 中控制可存取 Origami 的人員</span><span class="sxs-lookup"><span data-stu-id="59f13-106">You can control in Azure AD who has access to Origami</span></span>
- <span data-ttu-id="59f13-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Origami (單一登入)</span><span class="sxs-lookup"><span data-stu-id="59f13-107">You can enable your users to automatically get signed-on to Origami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="59f13-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="59f13-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="59f13-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="59f13-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59f13-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="59f13-110">Prerequisites</span></span>

<span data-ttu-id="59f13-111">若要設定 Azure AD 與 Origami 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="59f13-111">To configure Azure AD integration with Origami, you need the following items:</span></span>

- <span data-ttu-id="59f13-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="59f13-112">An Azure AD subscription</span></span>
- <span data-ttu-id="59f13-113">已啟用 Origami 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="59f13-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="59f13-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="59f13-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="59f13-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="59f13-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="59f13-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="59f13-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="59f13-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="59f13-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="59f13-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="59f13-118">Scenario description</span></span>
<span data-ttu-id="59f13-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="59f13-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="59f13-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="59f13-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59f13-121">從資源庫加入 Origami</span><span class="sxs-lookup"><span data-stu-id="59f13-121">Adding Origami from the gallery</span></span>
2. <span data-ttu-id="59f13-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="59f13-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-the-gallery"></a><span data-ttu-id="59f13-123">從資源庫加入 Origami</span><span class="sxs-lookup"><span data-stu-id="59f13-123">Adding Origami from the gallery</span></span>
<span data-ttu-id="59f13-124">若要設定將 Origami 整合到 Azure AD 中，您需要從資源庫將 Origami 加入到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="59f13-124">To configure the integration of Origami into Azure AD, you need to add Origami from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="59f13-125">**若要從資源庫加入 Origami，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="59f13-125">**To add Origami from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="59f13-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="59f13-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="59f13-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="59f13-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="59f13-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="59f13-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="59f13-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="59f13-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="59f13-133">在搜尋方塊中，輸入 **Origami**。</span><span class="sxs-lookup"><span data-stu-id="59f13-133">In the search box, type **Origami**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="59f13-135">在結果窗格中，選取 [Origami]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="59f13-135">In the results panel, select **Origami**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="59f13-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="59f13-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="59f13-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Origami 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="59f13-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="59f13-139">若要讓單一登入運作，Azure AD 必須知道 Origami 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="59f13-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Origami is to a user in Azure AD.</span></span> <span data-ttu-id="59f13-140">換句話說，必須要建立某位 Azure AD 使用者與 Origami 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="59f13-140">In other words, a link relationship between an Azure AD user and the related user in Origami needs to be established.</span></span>

<span data-ttu-id="59f13-141">在 Origami 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="59f13-141">In Origami, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="59f13-142">若要使用 Origami 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="59f13-142">To configure and test Azure AD single sign-on with Origami, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="59f13-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="59f13-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="59f13-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="59f13-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="59f13-145">**[建立 Origami 測試使用者](#creating-an-origami-test-user)** - 在 Origami 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="59f13-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - to have a counterpart of Britta Simon in Origami that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="59f13-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="59f13-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="59f13-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="59f13-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="59f13-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="59f13-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="59f13-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Origami 中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="59f13-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="59f13-150">**若要設定與 Origami 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="59f13-150">**To configure Azure AD single sign-on with Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="59f13-151">在 Azure 入口網站的 [Origami] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="59f13-151">In the Azure portal, on the **Origami** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="59f13-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="59f13-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="59f13-155">在 [Origami 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="59f13-155">On the **Origami Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="59f13-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="59f13-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="59f13-158">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="59f13-158">The value is not real.</span></span> <span data-ttu-id="59f13-159">請使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="59f13-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="59f13-160">請連絡 [Origami 客戶支援小組](https://wordpress.org/support/theme/origami)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="59f13-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) to get the value.</span></span> 
 
4. <span data-ttu-id="59f13-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="59f13-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="59f13-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="59f13-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="59f13-165">在 [Origami 組態] 區段上，按一下 [設定 Origami] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="59f13-165">On the **Origami Configuration** section, click **Configure Origami** to open **Configure sign-on** window.</span></span> <span data-ttu-id="59f13-166">從 [快速參考] 區段中複製 [登出 URL 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="59f13-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="59f13-168">以系統管理員權限登入 Origami 帳戶。</span><span class="sxs-lookup"><span data-stu-id="59f13-168">Log in to the Origami account with Admin rights.</span></span>

8. <span data-ttu-id="59f13-169">在頂端的功能表中，按一下 [系統管理員] 。</span><span class="sxs-lookup"><span data-stu-id="59f13-169">In the menu on the top, click **Admin**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="59f13-171">在 [單一登入設定] 對話方塊頁面執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="59f13-171">On the Single Sign On Setup dialog page, perform the following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="59f13-173">a.</span><span class="sxs-lookup"><span data-stu-id="59f13-173">a.</span></span> <span data-ttu-id="59f13-174">選取 [啟用單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="59f13-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="59f13-175">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="59f13-175">b.</span></span> <span data-ttu-id="59f13-176">在 [識別提供者的登入頁面 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="59f13-176">In the **Identity Provider's Sign-in Page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="59f13-177">c.</span><span class="sxs-lookup"><span data-stu-id="59f13-177">c.</span></span> <span data-ttu-id="59f13-178">在 [識別提供者的登出頁面 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="59f13-178">In the **Identity Provider's Sign-out Page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="59f13-179">d.</span><span class="sxs-lookup"><span data-stu-id="59f13-179">d.</span></span> <span data-ttu-id="59f13-180">按一下 [瀏覽] 以上傳您從 Azure 入口網站下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="59f13-180">Click **Browse** to upload the certificate you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="59f13-181">e.</span><span class="sxs-lookup"><span data-stu-id="59f13-181">e.</span></span> <span data-ttu-id="59f13-182">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="59f13-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="59f13-183">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="59f13-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="59f13-184">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="59f13-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="59f13-185">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="59f13-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="59f13-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="59f13-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="59f13-187">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="59f13-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="59f13-189">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="59f13-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="59f13-190">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="59f13-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="59f13-192">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="59f13-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="59f13-194">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="59f13-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="59f13-196">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="59f13-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="59f13-198">a.</span><span class="sxs-lookup"><span data-stu-id="59f13-198">a.</span></span> <span data-ttu-id="59f13-199">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="59f13-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="59f13-200">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="59f13-200">b.</span></span> <span data-ttu-id="59f13-201">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="59f13-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="59f13-202">c.</span><span class="sxs-lookup"><span data-stu-id="59f13-202">c.</span></span> <span data-ttu-id="59f13-203">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="59f13-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="59f13-204">d.</span><span class="sxs-lookup"><span data-stu-id="59f13-204">d.</span></span> <span data-ttu-id="59f13-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="59f13-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="59f13-206">建立 Origami 測試使用者</span><span class="sxs-lookup"><span data-stu-id="59f13-206">Creating an Origami test user</span></span>

<span data-ttu-id="59f13-207">在本節中，您要在 Origami 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="59f13-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="59f13-208">以系統管理員權限登入 Origami 帳戶。</span><span class="sxs-lookup"><span data-stu-id="59f13-208">Log in to the Origami account with Admin rights.</span></span>

2. <span data-ttu-id="59f13-209">在頂端的功能表中，按一下 [系統管理員] 。</span><span class="sxs-lookup"><span data-stu-id="59f13-209">In the menu on the top, click **Admin**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="59f13-211">在 [使用者與安全性] 對話方塊中，按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="59f13-211">On the **Users and Security** dialog, click **Users**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="59f13-213">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="59f13-213">Click **Add New User**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="59f13-215">在 [新增使用者] 對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="59f13-215">On the Add New User dialog, perform the following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="59f13-217">a.</span><span class="sxs-lookup"><span data-stu-id="59f13-217">a.</span></span> <span data-ttu-id="59f13-218">在 [使用者名稱] 文字方塊中，輸入使用者的電子郵件，例如 **brittasimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="59f13-218">In the **User Name** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="59f13-219">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="59f13-219">b.</span></span> <span data-ttu-id="59f13-220">在 [密碼] 文字方塊中輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="59f13-220">In the **Password** textbox, type a password.</span></span>

    <span data-ttu-id="59f13-221">c.</span><span class="sxs-lookup"><span data-stu-id="59f13-221">c.</span></span> <span data-ttu-id="59f13-222">在 [確認密碼] 文字方塊中再次輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="59f13-222">In the **Confirm Password** textbox, type the password again.</span></span>

    <span data-ttu-id="59f13-223">d.</span><span class="sxs-lookup"><span data-stu-id="59f13-223">d.</span></span> <span data-ttu-id="59f13-224">在 [名字] 文字方塊中，輸入使用者的名字，例如 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="59f13-224">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="59f13-225">e.</span><span class="sxs-lookup"><span data-stu-id="59f13-225">e.</span></span> <span data-ttu-id="59f13-226">在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="59f13-226">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="59f13-227">f.</span><span class="sxs-lookup"><span data-stu-id="59f13-227">f.</span></span> <span data-ttu-id="59f13-228">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="59f13-228">Click **Save**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="59f13-230">將**使用者角色**和**用戶端存取**指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="59f13-230">Assign **User Roles** and **Client Access** to the user.</span></span> 
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="59f13-232">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="59f13-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="59f13-233">在本節中，您會把 Origami 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="59f13-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Origami.</span></span>

![指派使用者][200] 

<span data-ttu-id="59f13-235">**若要將 Britta Simon 指派給 Origami，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="59f13-235">**To assign Britta Simon to Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="59f13-236">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="59f13-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="59f13-238">在應用程式清單中，選取 [Origami] 。</span><span class="sxs-lookup"><span data-stu-id="59f13-238">In the applications list, select **Origami**.</span></span>

    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="59f13-240">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="59f13-240">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="59f13-242">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="59f13-242">Click **Add** button.</span></span> <span data-ttu-id="59f13-243">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="59f13-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="59f13-245">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="59f13-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="59f13-246">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="59f13-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="59f13-247">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="59f13-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="59f13-248">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="59f13-248">Testing single sign-on</span></span>

<span data-ttu-id="59f13-249">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="59f13-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="59f13-250">當您在存取面板中按一下 [Origami] 圖格時，應該會自動登入您的 Origami 應用程式。</span><span class="sxs-lookup"><span data-stu-id="59f13-250">When you click the Origami tile in the Access Panel, you should get automatically signed-on to your Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="59f13-251">其他資源</span><span class="sxs-lookup"><span data-stu-id="59f13-251">Additional resources</span></span>

* [<span data-ttu-id="59f13-252">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="59f13-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="59f13-253">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="59f13-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

