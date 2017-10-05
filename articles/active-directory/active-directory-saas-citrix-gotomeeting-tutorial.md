---
title: "教學課程：Azure Active Directory 與 Citrix GoToMeeting 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Citrix GoToMeeting 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: c1ac144c4fa43312ec26fce03cd0ee1bfcf73d4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="d805b-103">教學課程：Azure Active Directory 與 Citrix GoToMeeting 整合</span><span class="sxs-lookup"><span data-stu-id="d805b-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="d805b-104">在本教學課程中，您會了解如何整合 Citrix GoToMeeting 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d805b-104">In this tutorial, you learn how to integrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d805b-105">Citrix GoToMeeting 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="d805b-105">Integrating Citrix GoToMeeting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d805b-106">您可以在 Azure AD 中控制可存取 Citrix GoToMeeting 的人員</span><span class="sxs-lookup"><span data-stu-id="d805b-106">You can control in Azure AD who has access to Citrix GoToMeeting</span></span>
- <span data-ttu-id="d805b-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Citrix GoToMeeting (單一登入)</span><span class="sxs-lookup"><span data-stu-id="d805b-107">You can enable your users to automatically get signed-on to Citrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d805b-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="d805b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d805b-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d805b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d805b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d805b-110">Prerequisites</span></span>

<span data-ttu-id="d805b-111">若要設定 Azure AD 與 Citrix GoToMeeting 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="d805b-111">To configure Azure AD integration with Citrix GoToMeeting, you need the following items:</span></span>

- <span data-ttu-id="d805b-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d805b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d805b-113">已啟用 Citrix GoToMeeting 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d805b-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d805b-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d805b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d805b-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d805b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d805b-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d805b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d805b-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="d805b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d805b-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="d805b-118">Scenario description</span></span>
<span data-ttu-id="d805b-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d805b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d805b-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="d805b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d805b-121">從資源庫新增 Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="d805b-121">Adding Citrix GoToMeeting from the gallery</span></span>
2. <span data-ttu-id="d805b-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d805b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-the-gallery"></a><span data-ttu-id="d805b-123">從資源庫新增 Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="d805b-123">Adding Citrix GoToMeeting from the gallery</span></span>
<span data-ttu-id="d805b-124">若要設定 Citrix GoToMeeting 與 Azure AD 整合，您需要從資源庫將 Citrix GoToMeeting 新增到受管理的 SaaS App 清單。</span><span class="sxs-lookup"><span data-stu-id="d805b-124">To configure the integration of Citrix GoToMeeting into Azure AD, you need to add Citrix GoToMeeting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d805b-125">**若要從資源庫新增 Citrix GoToMeeting，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d805b-125">**To add Citrix GoToMeeting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d805b-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d805b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d805b-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d805b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d805b-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d805b-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="d805b-131">按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d805b-131">Click **New application** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="d805b-133">在搜尋方塊中，輸入 **Citrix GoToMeeting**。</span><span class="sxs-lookup"><span data-stu-id="d805b-133">In the search box, type **Citrix GoToMeeting**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="d805b-135">在結果窗格中，選取 [Citrix GoToMeeting]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="d805b-135">In the results panel, select **Citrix GoToMeeting**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d805b-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d805b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d805b-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Citrix GoToMeeting 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d805b-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d805b-139">若要讓單一登入運作，Azure AD 必須知道 Citrix GoToMeeting 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="d805b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix GoToMeeting is to a user in Azure AD.</span></span> <span data-ttu-id="d805b-140">換句話說，必須在 Azure AD 使用者和 Citrix GoToMeeting 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d805b-140">In other words, a link relationship between an Azure AD user and the related user in Citrix GoToMeeting needs to be established.</span></span>

<span data-ttu-id="d805b-141">建立此連結關聯性的方法，是將 Azure AD 中**使用者名稱**的值，指派為 Citrix GoToMeeting 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="d805b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="d805b-142">若要設定及測試與 Citrix GoToMeeting 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="d805b-142">To configure and test Azure AD single sign-on with Citrix GoToMeeting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d805b-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="d805b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d805b-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d805b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d805b-145">**[建立 Citrix GoToMeeting 測試使用者](#creating-a-citrix-gotomeeting-test-user)** - 在 Citrix GoToMeeting 中建立一個與 Azure AD 中代表使用者的項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="d805b-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - to have a counterpart of Britta Simon in Citrix GoToMeeting that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d805b-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d805b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d805b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="d805b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d805b-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d805b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d805b-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Citrix GoToMeeting 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d805b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="d805b-150">**若要使用 Citrix GoToMeeting 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d805b-150">**To configure Azure AD single sign-on with Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="d805b-151">在 Azure 入口網站的 [Citrix GoToMeeting] 應用程式整合分頁上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="d805b-151">In the Azure portal, on the **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="d805b-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="d805b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="d805b-155">在 [Citrix GoToMeeting 網域和 URL] 區段中，不需要執行任何步驟。</span><span class="sxs-lookup"><span data-stu-id="d805b-155">On the **Citrix GoToMeeting Domain and URLs** section, no need to perform any steps.</span></span>

    ![設定單一登入](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="d805b-157">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="d805b-157">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="d805b-159">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d805b-159">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="d805b-161">在 [Citrix GoToMeeting 設定] 區段中，按一下 [設定 Citrix GoToMeeting] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="d805b-161">On the Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML to open Configure sign-on window.</span></span> <span data-ttu-id="d805b-162">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="d805b-162">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

6. <span data-ttu-id="d805b-163">在不同的瀏覽器視窗中，登入您的 [Citrix 組織中心](https://account.citrixonline.com/organization/administration/)。</span><span class="sxs-lookup"><span data-stu-id="d805b-163">In a different browser window, log in to your [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="d805b-164">按一下 [識別提供者]  索引標籤，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d805b-164">Click the **Identity Provider** tab, and then perform the following steps:</span></span>  
   
    <span data-ttu-id="d805b-165">![SAML 設定](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="d805b-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="d805b-166">a.</span><span class="sxs-lookup"><span data-stu-id="d805b-166">a.</span></span> <span data-ttu-id="d805b-167">選取 [手動]</span><span class="sxs-lookup"><span data-stu-id="d805b-167">Select **Manual**</span></span>

    <span data-ttu-id="d805b-168">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d805b-168">b.</span></span> <span data-ttu-id="d805b-169">在 Azure 入口網站的 [設定在 Citrix GoToMeeting 單一登入] 對話方塊頁面上，複製 [SAML 單一登入頁面服務 URL] 值，然後貼至 [登入分頁 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="d805b-169">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="d805b-170">c.</span><span class="sxs-lookup"><span data-stu-id="d805b-170">c.</span></span> <span data-ttu-id="d805b-171">在 Azure 入口網站的 [設定在 Citrix GoToMeeting 單一登入] 對話方塊頁面上，複製 [登出 URL] 值，然後貼至 [登出分頁 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="d805b-171">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Sign-Out URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="d805b-172">d.</span><span class="sxs-lookup"><span data-stu-id="d805b-172">d.</span></span> <span data-ttu-id="d805b-173">在 Azure 入口網站的 [設定在 Citrix GoToMeeting 單一登入] 對話方塊分頁上，複製 [SAML 實體 ID] 值，然後貼至 [識別提供者實體識別碼] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="d805b-173">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Entity ID** value, and then paste it into the **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="d805b-174">e.</span><span class="sxs-lookup"><span data-stu-id="d805b-174">e.</span></span> <span data-ttu-id="d805b-175">如果要上傳您下載的憑證，請按一下 [上傳憑證]。</span><span class="sxs-lookup"><span data-stu-id="d805b-175">To upload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="d805b-176">f.</span><span class="sxs-lookup"><span data-stu-id="d805b-176">f.</span></span> <span data-ttu-id="d805b-177">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="d805b-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d805b-178">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="d805b-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d805b-179">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="d805b-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d805b-180">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d805b-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d805b-181">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d805b-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="d805b-182">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d805b-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="d805b-184">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d805b-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d805b-185">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d805b-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d805b-187">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="d805b-187">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d805b-189">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d805b-189">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d805b-191">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d805b-191">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d805b-193">a.</span><span class="sxs-lookup"><span data-stu-id="d805b-193">a.</span></span> <span data-ttu-id="d805b-194">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d805b-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d805b-195">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d805b-195">b.</span></span> <span data-ttu-id="d805b-196">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="d805b-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d805b-197">c.</span><span class="sxs-lookup"><span data-stu-id="d805b-197">c.</span></span> <span data-ttu-id="d805b-198">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="d805b-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d805b-199">d.</span><span class="sxs-lookup"><span data-stu-id="d805b-199">d.</span></span> <span data-ttu-id="d805b-200">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d805b-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="d805b-201">建立 Citrix GoToMeeting 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d805b-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="d805b-202">本節會在 Citrix GoToMeeting 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="d805b-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="d805b-203">Citrix GoToMeeting 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="d805b-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="d805b-204">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="d805b-204">There is no action item for you in this section.</span></span> <span data-ttu-id="d805b-205">如果 Citrix GoToMeeting 中還沒有該使用者，當您嘗試存取 Citrix GoToMeeting 時，就會建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="d805b-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt to access Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="d805b-206">如果您需要手動建立使用者，請連絡 [Citrix GoToMeeting 支援小組](https://care.citrixonline.com/gotomeeting)。</span><span class="sxs-lookup"><span data-stu-id="d805b-206">If you need to create a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d805b-207">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d805b-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d805b-208">在本節中，您會將 Citrix GoToMeeting 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d805b-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix GoToMeeting.</span></span>

![指派使用者][200] 

<span data-ttu-id="d805b-210">**若要將 Britta Simon 指派給 Citrix GoToMeeting，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d805b-210">**To assign Britta Simon to Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="d805b-211">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d805b-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="d805b-213">在應用程式清單中，選取 [Citrix GoToMeeting]。</span><span class="sxs-lookup"><span data-stu-id="d805b-213">In the applications list, select **Citrix GoToMeeting**.</span></span>

    ![設定單一登入](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="d805b-215">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d805b-215">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="d805b-217">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d805b-217">Click **Add** button.</span></span> <span data-ttu-id="d805b-218">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d805b-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="d805b-220">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="d805b-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d805b-221">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d805b-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d805b-222">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d805b-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d805b-223">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d805b-223">Testing single sign-on</span></span>

<span data-ttu-id="d805b-224">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="d805b-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d805b-225">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="d805b-225">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="d805b-226">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="d805b-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d805b-227">其他資源</span><span class="sxs-lookup"><span data-stu-id="d805b-227">Additional resources</span></span>

* [<span data-ttu-id="d805b-228">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="d805b-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d805b-229">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d805b-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d805b-230">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="d805b-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

