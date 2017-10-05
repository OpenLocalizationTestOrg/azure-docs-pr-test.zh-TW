---
title: "教學課程：Azure Active Directory 與 Dropbox for Business 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Dropbox for Business 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: a56a5af171eaca259db29f25fee4331a77313420
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="4a097-103">教學課程：Azure Active Directory 與 Dropbox for Business 整合</span><span class="sxs-lookup"><span data-stu-id="4a097-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="4a097-104">在本教學課程中，您會了解如何整合 Dropbox for Business 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="4a097-104">In this tutorial, you learn how to integrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4a097-105">Dropbox for Business 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="4a097-105">Integrating Dropbox for Business with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4a097-106">您可以在 Azure AD 中控制可存取 Dropbox for Business 的人員</span><span class="sxs-lookup"><span data-stu-id="4a097-106">You can control in Azure AD who has access to Dropbox for Business</span></span>
- <span data-ttu-id="4a097-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Dropbox for Business (單一登入)</span><span class="sxs-lookup"><span data-stu-id="4a097-107">You can enable your users to automatically get signed-on to Dropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4a097-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="4a097-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4a097-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="4a097-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a097-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4a097-110">Prerequisites</span></span>

<span data-ttu-id="4a097-111">若要設定 Azure AD 與 Dropbox for Business 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="4a097-111">To configure Azure AD integration with Dropbox for Business, you need the following items:</span></span>

- <span data-ttu-id="4a097-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4a097-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4a097-113">已啟用 Dropbox for Business 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4a097-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4a097-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4a097-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4a097-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="4a097-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4a097-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4a097-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4a097-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="4a097-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4a097-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="4a097-118">Scenario description</span></span>
<span data-ttu-id="4a097-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4a097-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4a097-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="4a097-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4a097-121">從資源庫新增 Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="4a097-121">Adding Dropbox for Business from the gallery</span></span>
2. <span data-ttu-id="4a097-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4a097-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-the-gallery"></a><span data-ttu-id="4a097-123">從資源庫新增 Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="4a097-123">Adding Dropbox for Business from the gallery</span></span>
<span data-ttu-id="4a097-124">若要設定 Dropbox for Business 與 Azure AD 整合，您需要從資源庫將 SAP Dropbox for Business 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="4a097-124">To configure the integration of Dropbox for Business into Azure AD, you need to add Dropbox for Business from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4a097-125">**若要從資源庫新增 Dropbox for Business，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4a097-125">**To add Dropbox for Business from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4a097-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="4a097-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4a097-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4a097-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4a097-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4a097-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="4a097-131">按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4a097-131">Click **New application** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="4a097-133">在搜尋方塊中，輸入 **Dropbox for Business**。</span><span class="sxs-lookup"><span data-stu-id="4a097-133">In the search box, type **Dropbox for Business**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="4a097-135">在結果窗格中選取 [Dropbox for Business]，然後按一下 [新增] 按鈕來新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a097-135">In the results panel, select **Dropbox for Business**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4a097-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4a097-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4a097-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Dropbox for Business 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4a097-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4a097-139">若要讓單一登入運作，Azure AD 必須知道 Dropbox for Business 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="4a097-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dropbox for Business is to a user in Azure AD.</span></span> <span data-ttu-id="4a097-140">換句話說，必須在 Azure AD 使用者與 Dropbox for Business 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4a097-140">In other words, a link relationship between an Azure AD user and the related user in Dropbox for Business needs to be established.</span></span>

<span data-ttu-id="4a097-141">建立此連結關聯性的方法是將 Azure AD 中**使用者名稱**的值，指定為 Dropbox for Business 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="4a097-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="4a097-142">若要設定及測試與 Dropbox for Business 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="4a097-142">To configure and test Azure AD single sign-on with Dropbox for Business, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4a097-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="4a097-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4a097-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4a097-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4a097-145">**[建立 Dropbox for Business 測試使用者](#creating-a-dropbox-for-business-test-user)** - 在 Dropbox for Business 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="4a097-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - to have a counterpart of Britta Simon in Dropbox for Business that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4a097-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4a097-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4a097-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="4a097-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4a097-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4a097-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4a097-149">在本節中，您將在 Azure 入口網站中啟用 Azure AD 單一登入，並在 Dropbox for Business 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="4a097-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="4a097-150">**若要使用 Dropbox for Business 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4a097-150">**To configure Azure AD single sign-on with Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="4a097-151">在 Azure 入口網站的 [Dropbox for Business] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="4a097-151">In the Azure portal, on the **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="4a097-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="4a097-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="4a097-155">在 [Dropbox for Business 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4a097-155">On the **Dropbox for Business Domain and URLs** section, perform the following steps:</span></span>

    <span data-ttu-id="4a097-156">a.</span><span class="sxs-lookup"><span data-stu-id="4a097-156">a.</span></span> <span data-ttu-id="4a097-157">登入您的 Dropbox for Business 租用戶。</span><span class="sxs-lookup"><span data-stu-id="4a097-157">Sign on to your Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="4a097-158">![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="4a097-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="4a097-159">b.</span><span class="sxs-lookup"><span data-stu-id="4a097-159">b.</span></span> <span data-ttu-id="4a097-160">在左側的導覽窗格中，按一下 [管理主控台]。</span><span class="sxs-lookup"><span data-stu-id="4a097-160">In the navigation pane on the left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="4a097-161">![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="4a097-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="4a097-162">c.</span><span class="sxs-lookup"><span data-stu-id="4a097-162">c.</span></span> <span data-ttu-id="4a097-163">在 [管理主控台] 上，按一下左側導覽窗格中的 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="4a097-163">On the **Admin Console**, click **Authentication** in the left navigation pane.</span></span> 
   
    <span data-ttu-id="4a097-164">![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="4a097-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="4a097-165">d.</span><span class="sxs-lookup"><span data-stu-id="4a097-165">d.</span></span> <span data-ttu-id="4a097-166">在 [單一登入] 區段中，選取 [啟用單一登入]，然後按一下 [更多資訊] 以展開此區段。</span><span class="sxs-lookup"><span data-stu-id="4a097-166">In the **Single sign-on** section, select **Enable single sign-on**, and then click **More** to expand this section.</span></span>  
   
    <span data-ttu-id="4a097-167">![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="4a097-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="4a097-168">e.</span><span class="sxs-lookup"><span data-stu-id="4a097-168">e.</span></span> <span data-ttu-id="4a097-169">複製 [使用者可藉由輸入其電子郵件地址進行登入或可直接前往] 旁邊的 URL。</span><span class="sxs-lookup"><span data-stu-id="4a097-169">Copy the URL next to **Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="4a097-171">f.</span><span class="sxs-lookup"><span data-stu-id="4a097-171">f.</span></span> <span data-ttu-id="4a097-172">在 Azure 入口網站的 [登入 URL] 文字方塊中，貼上 URL。</span><span class="sxs-lookup"><span data-stu-id="4a097-172">On the Azure portal, in the **Sign-on URL** textbox, paste the URL.</span></span>

    ![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="4a097-174">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="4a097-174">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4a097-175">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="4a097-175">This value is not real value.</span></span> <span data-ttu-id="4a097-176">使用您從他們的單一登入區段取得之實際登入 URL 將值更新。</span><span class="sxs-lookup"><span data-stu-id="4a097-176">Update the value with the actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="4a097-177">請連絡 [Dropbox for Business 用戶端支援小組](https://www.dropbox.com/business/contact)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="4a097-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) to get this value.</span></span> 
 
4. <span data-ttu-id="4a097-178">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="4a097-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="4a097-180">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="4a097-180">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4a097-182">在 [Dropbox for Business 設定] 區段中，按一下 [設定 Dropbox for Business] 可開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="4a097-182">On the **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4a097-183">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="4a097-183">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="4a097-185">若要在 [Dropbox for Business] 端上設定單一登入，於 [驗證] 頁面的 [單一登入] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4a097-185">To configure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in the **Single sign-on** section of the **Authentication** page, perform the following steps:</span></span> 
   
    <span data-ttu-id="4a097-186">![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="4a097-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="4a097-187">a.</span><span class="sxs-lookup"><span data-stu-id="4a097-187">a.</span></span> <span data-ttu-id="4a097-188">按一下 [必要]。</span><span class="sxs-lookup"><span data-stu-id="4a097-188">Click **Required**.</span></span>
   
    <span data-ttu-id="4a097-189">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a097-189">b.</span></span> <span data-ttu-id="4a097-190">在 Azure 入口網站的 [設定登入] 視窗上，複製 [SAML 單一登入服務 URL] 值，然後將它貼至 [登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="4a097-190">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="4a097-191">c.</span><span class="sxs-lookup"><span data-stu-id="4a097-191">c.</span></span> <span data-ttu-id="4a097-192">按一下 [選擇憑證]，然後瀏覽至您的 **Base-64 編碼的憑證檔案**。</span><span class="sxs-lookup"><span data-stu-id="4a097-192">Click **Choose certificate**, and then browse to your **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="4a097-193">d.</span><span class="sxs-lookup"><span data-stu-id="4a097-193">d.</span></span> <span data-ttu-id="4a097-194">按一下 [儲存變更] 以完成 DropBox for Business 租用戶設定。</span><span class="sxs-lookup"><span data-stu-id="4a097-194">Click **Save changes** to complete the configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="4a097-195">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="4a097-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4a097-196">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="4a097-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4a097-197">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4a097-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4a097-198">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4a097-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="4a097-199">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="4a097-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="4a097-201">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4a097-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4a097-202">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="4a097-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="4a097-204">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="4a097-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4a097-206">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4a097-206">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4a097-208">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4a097-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4a097-210">a.</span><span class="sxs-lookup"><span data-stu-id="4a097-210">a.</span></span> <span data-ttu-id="4a097-211">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="4a097-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4a097-212">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a097-212">b.</span></span> <span data-ttu-id="4a097-213">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="4a097-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4a097-214">c.</span><span class="sxs-lookup"><span data-stu-id="4a097-214">c.</span></span> <span data-ttu-id="4a097-215">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="4a097-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4a097-216">d.</span><span class="sxs-lookup"><span data-stu-id="4a097-216">d.</span></span> <span data-ttu-id="4a097-217">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="4a097-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="4a097-218">建立 Dropbox for Business 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4a097-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="4a097-219">本節會在 Dropbox for Business 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="4a097-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="4a097-220">Dropbox for Business 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="4a097-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="4a097-221">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="4a097-221">There is no action item for you in this section.</span></span> <span data-ttu-id="4a097-222">如果 Dropbox for Business 中還沒有該使用者，當您嘗試存取 Dropbox for Business 時，就會建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="4a097-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt to access Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="4a097-223">如果您需要手動建立使用者，請連絡 [Dropbox for Business 用戶端支援小組](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="4a097-223">If you need to create a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4a097-224">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4a097-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4a097-225">在本節中，您會將 Dropbox for Business 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4a097-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dropbox for Business.</span></span>

![指派使用者][200] 

<span data-ttu-id="4a097-227">**若要將 Britta Simon 指派給 Dropbox for Business，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4a097-227">**To assign Britta Simon to Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="4a097-228">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4a097-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="4a097-230">在應用程式清單中，選取 [Dropbox for Business]。</span><span class="sxs-lookup"><span data-stu-id="4a097-230">In the applications list, select **Dropbox for Business**.</span></span>

    ![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="4a097-232">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4a097-232">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="4a097-234">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4a097-234">Click **Add** button.</span></span> <span data-ttu-id="4a097-235">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4a097-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="4a097-237">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="4a097-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4a097-238">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4a097-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4a097-239">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4a097-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4a097-240">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="4a097-240">Testing single sign-on</span></span>

<span data-ttu-id="4a097-241">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="4a097-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4a097-242">當您按一下「存取面板」中的 [Dropbox for Business] 圖格時，應該會取得您 Dropbox for Business 應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="4a097-242">When you click the Dropbox for Business tile in the Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4a097-243">其他資源</span><span class="sxs-lookup"><span data-stu-id="4a097-243">Additional resources</span></span>

* [<span data-ttu-id="4a097-244">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="4a097-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4a097-245">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="4a097-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4a097-246">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="4a097-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

