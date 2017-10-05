---
title: "教學課程：Azure Active Directory 與 UNIFI 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 UNIFI 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 09074d4628825909f0bb961c8001e53fb06cf7c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="3ed92-103">教學課程：Azure Active Directory 與 UNIFI 整合</span><span class="sxs-lookup"><span data-stu-id="3ed92-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="3ed92-104">在本教學課程中，您會了解如何整合 UNIFI 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="3ed92-104">In this tutorial, you learn how to integrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ed92-105">UNIFI 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="3ed92-105">Integrating UNIFI with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3ed92-106">您可以在 Azure AD 中控制可存取 UNIFI 的人員</span><span class="sxs-lookup"><span data-stu-id="3ed92-106">You can control in Azure AD who has access to UNIFI</span></span>
- <span data-ttu-id="3ed92-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 UNIFI (單一登入)</span><span class="sxs-lookup"><span data-stu-id="3ed92-107">You can enable your users to automatically get signed-on to UNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3ed92-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="3ed92-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3ed92-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="3ed92-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ed92-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="3ed92-110">Prerequisites</span></span>

<span data-ttu-id="3ed92-111">若要設定 Azure AD 與 UNIFI 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="3ed92-111">To configure Azure AD integration with UNIFI, you need the following items:</span></span>

- <span data-ttu-id="3ed92-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3ed92-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3ed92-113">已啟用 UNIFI 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3ed92-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ed92-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3ed92-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ed92-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="3ed92-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ed92-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3ed92-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ed92-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="3ed92-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ed92-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="3ed92-118">Scenario description</span></span>
<span data-ttu-id="3ed92-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3ed92-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ed92-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="3ed92-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ed92-121">從資源庫新增 UNIFI</span><span class="sxs-lookup"><span data-stu-id="3ed92-121">Adding UNIFI from the gallery</span></span>
2. <span data-ttu-id="3ed92-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3ed92-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-the-gallery"></a><span data-ttu-id="3ed92-123">從資源庫新增 UNIFI</span><span class="sxs-lookup"><span data-stu-id="3ed92-123">Adding UNIFI from the gallery</span></span>
<span data-ttu-id="3ed92-124">若要設定將 UNIFI 整合到 Azure AD 中，您需要從資源庫將 UNIFI 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="3ed92-124">To configure the integration of UNIFI into Azure AD, you need to add UNIFI from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3ed92-125">**若要從資源庫新增 UNIFI，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3ed92-125">**To add UNIFI from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3ed92-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="3ed92-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3ed92-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3ed92-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3ed92-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3ed92-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="3ed92-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3ed92-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="3ed92-133">在搜尋方塊中，輸入 **UNIFI**。</span><span class="sxs-lookup"><span data-stu-id="3ed92-133">In the search box, type **UNIFI**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. <span data-ttu-id="3ed92-135">在結果窗格中，選取 [UNIFI]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ed92-135">In the results panel, select **UNIFI**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3ed92-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3ed92-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3ed92-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 UNIFI 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3ed92-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3ed92-139">若要讓單一登入運作，Azure AD 必須知道 UNIFI 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="3ed92-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UNIFI is to a user in Azure AD.</span></span> <span data-ttu-id="3ed92-140">換句話說，必須建立 Azure AD 使用者和 UNIFI 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="3ed92-140">In other words, a link relationship between an Azure AD user and the related user in UNIFI needs to be established.</span></span>

<span data-ttu-id="3ed92-141">在 UNIFI 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="3ed92-141">In UNIFI, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3ed92-142">若要設定及測試與 UNIFI 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="3ed92-142">To configure and test Azure AD single sign-on with UNIFI, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3ed92-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="3ed92-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3ed92-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3ed92-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3ed92-145">**[建立 UNIFI 測試使用者](#creating-a-unifi-test-user)** - 讓 UNIFI 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="3ed92-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - to have a counterpart of Britta Simon in UNIFI that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3ed92-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3ed92-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3ed92-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="3ed92-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3ed92-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3ed92-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3ed92-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 UNIFI 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="3ed92-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="3ed92-150">**若要設定與 UNIFI 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3ed92-150">**To configure Azure AD single sign-on with UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="3ed92-151">在 Azure 入口網站的 [UNIFI] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="3ed92-151">In the Azure portal, on the **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="3ed92-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="3ed92-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. <span data-ttu-id="3ed92-155">如果您想要以 **IDP** 起始模式設定應用程式，請在 [UNIFI 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3ed92-155">On the **UNIFI Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="3ed92-157">在 [識別碼] 文字方塊中，輸入值：`INVIEWlabs`</span><span class="sxs-lookup"><span data-stu-id="3ed92-157">In the **Identifier** textbox, type the value: `INVIEWlabs`</span></span> 

4. <span data-ttu-id="3ed92-158">如果您想要以 **SP** 起始模式設定應用程式，請勾選 [顯示進階 URL 設定]：</span><span class="sxs-lookup"><span data-stu-id="3ed92-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="3ed92-160">在 [登入 URL] 文字方塊中，輸入 URL：`https://app.discoverunifi.com/login`</span><span class="sxs-lookup"><span data-stu-id="3ed92-160">In the **Sign-on URL** textbox, type the URL: `https://app.discoverunifi.com/login`</span></span>

5. <span data-ttu-id="3ed92-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="3ed92-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. <span data-ttu-id="3ed92-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3ed92-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="3ed92-165">在 [UNIFI 組態] 區段上，按一下 [設定 UNIFI] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="3ed92-165">On the **UNIFI Configuration** section, click **Configure UNIFI** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3ed92-166">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="3ed92-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. <span data-ttu-id="3ed92-168">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 **UNIFI** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="3ed92-168">In a different web browser window, sign on to your **UNIFI** company site as administrator.</span></span>

9. <span data-ttu-id="3ed92-169">按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="3ed92-169">Click on the **Users**.</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. <span data-ttu-id="3ed92-171">按一下 [新增識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="3ed92-171">Click on the **Add New Identity Provider**.</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/app2.png)

11. <span data-ttu-id="3ed92-173">在 [新增識別提供者] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3ed92-173">In the **Add Identity Provider** section, perform the following steps:</span></span>   

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/app3.png) 

    <span data-ttu-id="3ed92-175">a.</span><span class="sxs-lookup"><span data-stu-id="3ed92-175">a.</span></span> <span data-ttu-id="3ed92-176">在 [提供者名稱] 文字方塊中，輸入識別提供者的名稱。</span><span class="sxs-lookup"><span data-stu-id="3ed92-176">In the **Provider Name** textbox, type the name of the Identity Provider..</span></span>

    <span data-ttu-id="3ed92-177">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ed92-177">b.</span></span> <span data-ttu-id="3ed92-178">在 [提供者 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="3ed92-178">In the the **Provider URL** textbox paste the **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3ed92-179">c.</span><span class="sxs-lookup"><span data-stu-id="3ed92-179">c.</span></span> <span data-ttu-id="3ed92-180">在記事本中開啟您從 Azure 入口網站下載的憑證，移除 **---BEGIN CERTIFICATE---** 和 **---END CERTIFICATE---** 標記，然後在 [憑證] 文字方塊中貼上其餘內容。</span><span class="sxs-lookup"><span data-stu-id="3ed92-180">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Certificate** textbox.</span></span>

    <span data-ttu-id="3ed92-181">d.</span><span class="sxs-lookup"><span data-stu-id="3ed92-181">d.</span></span> <span data-ttu-id="3ed92-182">選取 [是預設提供者] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="3ed92-182">Select the **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="3ed92-183">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="3ed92-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3ed92-184">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="3ed92-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3ed92-185">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3ed92-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3ed92-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3ed92-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="3ed92-187">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="3ed92-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="3ed92-189">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3ed92-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3ed92-190">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="3ed92-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3ed92-192">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="3ed92-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3ed92-194">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="3ed92-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3ed92-196">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3ed92-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3ed92-198">a.</span><span class="sxs-lookup"><span data-stu-id="3ed92-198">a.</span></span> <span data-ttu-id="3ed92-199">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="3ed92-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ed92-200">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ed92-200">b.</span></span> <span data-ttu-id="3ed92-201">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="3ed92-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3ed92-202">c.</span><span class="sxs-lookup"><span data-stu-id="3ed92-202">c.</span></span> <span data-ttu-id="3ed92-203">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="3ed92-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3ed92-204">d.</span><span class="sxs-lookup"><span data-stu-id="3ed92-204">d.</span></span> <span data-ttu-id="3ed92-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3ed92-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="3ed92-206">建立 UNIFI 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3ed92-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="3ed92-207">在本節中，您會建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="3ed92-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="3ed92-208">**UNIFI** 支援自動使用者佈建，因此不不需要任何手動步驟。</span><span class="sxs-lookup"><span data-stu-id="3ed92-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="3ed92-209">從 Azure AD 成功驗證後會自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="3ed92-209">Users are created automatically after successful authentication from the Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3ed92-210">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3ed92-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3ed92-211">在本節中，您會將 UNIFI 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3ed92-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UNIFI.</span></span>

![指派使用者][200] 

<span data-ttu-id="3ed92-213">**若要將 Britta Simon 指派給 UNIFI，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3ed92-213">**To assign Britta Simon to UNIFI, perform the following steps:**</span></span>

1. <span data-ttu-id="3ed92-214">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3ed92-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="3ed92-216">在應用程式清單中，選取 [UNIFI]。</span><span class="sxs-lookup"><span data-stu-id="3ed92-216">In the applications list, select **UNIFI**.</span></span>

    ![設定單一登入](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. <span data-ttu-id="3ed92-218">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3ed92-218">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="3ed92-220">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3ed92-220">Click **Add** button.</span></span> <span data-ttu-id="3ed92-221">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3ed92-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="3ed92-223">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="3ed92-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3ed92-224">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3ed92-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3ed92-225">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3ed92-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3ed92-226">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="3ed92-226">Testing single sign-on</span></span>

<span data-ttu-id="3ed92-227">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="3ed92-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3ed92-228">當您在存取面板中按一下 UNIFI 圖格時，應該會自動登入您的 UNIFI 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ed92-228">When you click the UNIFI tile in the Access Panel, you should get automatically signed-on to your UNIFI application.</span></span>
<span data-ttu-id="3ed92-229">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3ed92-229">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3ed92-230">其他資源</span><span class="sxs-lookup"><span data-stu-id="3ed92-230">Additional resources</span></span>

* [<span data-ttu-id="3ed92-231">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="3ed92-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3ed92-232">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="3ed92-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png

