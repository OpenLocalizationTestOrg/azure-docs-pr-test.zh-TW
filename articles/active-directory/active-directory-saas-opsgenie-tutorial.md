---
title: "教學課程：Azure Active Directory 與 OpsGenie 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 OpsGenie 之間的單一登入"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: ce63726d2406d2f1415d29786f0ef92ca95b9b90
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="b5de6-103">教學課程：Azure Active Directory 與 OpsGenie 整合</span><span class="sxs-lookup"><span data-stu-id="b5de6-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>

<span data-ttu-id="b5de6-104">在本教學課程中，您將了解如何整合 OpsGenie 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b5de6-104">In this tutorial, you learn how to integrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b5de6-105">OpsGenie 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="b5de6-105">Integrating OpsGenie with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b5de6-106">您可以在 Azure AD 中控制可存取 OpsGenie 的人員</span><span class="sxs-lookup"><span data-stu-id="b5de6-106">You can control in Azure AD who has access to OpsGenie</span></span>
- <span data-ttu-id="b5de6-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 OpsGenie (單一登入)</span><span class="sxs-lookup"><span data-stu-id="b5de6-107">You can enable your users to automatically get signed-on to OpsGenie (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b5de6-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="b5de6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b5de6-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b5de6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5de6-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b5de6-110">Prerequisites</span></span>

<span data-ttu-id="b5de6-111">若要設定 Azure AD 與 OpsGenie 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="b5de6-111">To configure Azure AD integration with OpsGenie, you need the following items:</span></span>

- <span data-ttu-id="b5de6-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b5de6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b5de6-113">已啟用 OpsGenie 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b5de6-113">A OpsGenie single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b5de6-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b5de6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b5de6-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b5de6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b5de6-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b5de6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b5de6-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="b5de6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b5de6-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b5de6-118">Scenario description</span></span>
<span data-ttu-id="b5de6-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b5de6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b5de6-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="b5de6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b5de6-121">從資源庫新增 OpsGenie</span><span class="sxs-lookup"><span data-stu-id="b5de6-121">Adding OpsGenie from the gallery</span></span>
2. <span data-ttu-id="b5de6-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b5de6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opsgenie-from-the-gallery"></a><span data-ttu-id="b5de6-123">從資源庫新增 OpsGenie</span><span class="sxs-lookup"><span data-stu-id="b5de6-123">Adding OpsGenie from the gallery</span></span>
<span data-ttu-id="b5de6-124">若要設定將 OpsGenie 整合到 Azure AD 中，您需要從資源庫將 OpsGenie 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="b5de6-124">To configure the integration of OpsGenie into Azure AD, you need to add OpsGenie from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b5de6-125">**若要從資源庫新增 OpsGenie，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b5de6-125">**To add OpsGenie from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b5de6-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="b5de6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b5de6-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b5de6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b5de6-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b5de6-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="b5de6-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b5de6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="b5de6-133">在搜尋方塊中，輸入 **OpsGenie**。</span><span class="sxs-lookup"><span data-stu-id="b5de6-133">In the search box, type **OpsGenie**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. <span data-ttu-id="b5de6-135">在結果窗格中，選取 [OpsGenie]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5de6-135">In the results panel, select **OpsGenie**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b5de6-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b5de6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b5de6-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 OpsGenie 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b5de6-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b5de6-139">若要讓單一登入運作，Azure AD 必須知道 OpsGenie 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="b5de6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in OpsGenie is to a user in Azure AD.</span></span> <span data-ttu-id="b5de6-140">換句話說，必須建立 Azure AD 使用者和 OpsGenie 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b5de6-140">In other words, a link relationship between an Azure AD user and the related user in OpsGenie needs to be established.</span></span>

<span data-ttu-id="b5de6-141">在 OpsGenie 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b5de6-141">In OpsGenie, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b5de6-142">若要設定及測試與 OpsGenie 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="b5de6-142">To configure and test Azure AD single sign-on with OpsGenie, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b5de6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="b5de6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b5de6-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b5de6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5de6-145">**[建立 OpsGenie 測試使用者](#creating-a-opsgenie-test-user)** - 使 OpsGenie 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="b5de6-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - to have a counterpart of Britta Simon in OpsGenie that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b5de6-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b5de6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5de6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="b5de6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b5de6-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b5de6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b5de6-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 OpsGenie 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="b5de6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OpsGenie application.</span></span>

<span data-ttu-id="b5de6-150">**若要設定與 OpsGenie 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b5de6-150">**To configure Azure AD single sign-on with OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="b5de6-151">在 Azure 入口網站的 [OpsGenie] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="b5de6-151">In the Azure portal, on the **OpsGenie** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="b5de6-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="b5de6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. <span data-ttu-id="b5de6-155">在 [OpsGenie 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b5de6-155">On the **OpsGenie Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    <span data-ttu-id="b5de6-157">在 [登入 URL] 文字方塊中，輸入 URL：`https://app.opsgenie.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="b5de6-157">In the **Sign-on URL** textbox, type the URL: `https://app.opsgenie.com/auth/login`</span></span>

4. <span data-ttu-id="b5de6-158">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="b5de6-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. <span data-ttu-id="b5de6-160">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b5de6-160">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b5de6-162">在 [OpsGenie 組態] 區段上，按一下 [設定 OpsGenie] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="b5de6-162">On the **OpsGenie Configuration** section, click **Configure OpsGenie** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b5de6-163">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="b5de6-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. <span data-ttu-id="b5de6-165">開啟另一個瀏覽器執行個體，然後以系統管理員身分登入 OpsGenie。</span><span class="sxs-lookup"><span data-stu-id="b5de6-165">Open another browser instance, and then log-in to OpsGenie as an administrator.</span></span>

8. <span data-ttu-id="b5de6-166">按一下 [設定]，然後按一下 [單一登入] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b5de6-166">Click **Settings**, and then click the **Single Sign On** tab.</span></span>
   
    ![OpsGenie 設定單一登入](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. <span data-ttu-id="b5de6-168">若要啟用 SSO，請選取 [啟用] 。</span><span class="sxs-lookup"><span data-stu-id="b5de6-168">To enable SSO, select **Enabled**.</span></span>
   
    ![OpsGenie 設定](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. <span data-ttu-id="b5de6-170">在 [提供者] 區段中，按一下 [Azure Active Directory] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b5de6-170">In the **Provider** section, click the **Azure Active Directory** tab.</span></span>
   
    ![OpsGenie 設定](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. <span data-ttu-id="b5de6-172">在 [Azure Active Directory] 對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b5de6-172">On the Azure Active Directory dialog page, perform the following steps:</span></span>
   
    ![OpsGenie 設定](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    <span data-ttu-id="b5de6-174">a.</span><span class="sxs-lookup"><span data-stu-id="b5de6-174">a.</span></span> <span data-ttu-id="b5de6-175">將您從 Azure 入口網站複製的「單一登入服務 URL」貼到 [SAML 2.0 端點] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="b5de6-175">Paste **Single Sign On Service URL**, which you have copied from the Azure portal into the **SAML 2.0 Endpoint** textbox.</span></span>
    
    <span data-ttu-id="b5de6-176">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5de6-176">b.</span></span> <span data-ttu-id="b5de6-177">在記事本中開啟您下載的 Base-64 編碼憑證、將其內容複製到剪貼簿，然後將它貼到 [X.500 憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="b5de6-177">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **X.500 Certificate** textbox.</span></span>
    
    <span data-ttu-id="b5de6-178">c.</span><span class="sxs-lookup"><span data-stu-id="b5de6-178">c.</span></span> <span data-ttu-id="b5de6-179">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="b5de6-179">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="b5de6-180">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="b5de6-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b5de6-181">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="b5de6-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b5de6-182">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b5de6-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b5de6-183">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b5de6-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="b5de6-184">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b5de6-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="b5de6-186">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b5de6-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b5de6-187">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="b5de6-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b5de6-189">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b5de6-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b5de6-191">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b5de6-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b5de6-193">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b5de6-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b5de6-195">a.</span><span class="sxs-lookup"><span data-stu-id="b5de6-195">a.</span></span> <span data-ttu-id="b5de6-196">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b5de6-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b5de6-197">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5de6-197">b.</span></span> <span data-ttu-id="b5de6-198">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="b5de6-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b5de6-199">c.</span><span class="sxs-lookup"><span data-stu-id="b5de6-199">c.</span></span> <span data-ttu-id="b5de6-200">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="b5de6-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b5de6-201">d.</span><span class="sxs-lookup"><span data-stu-id="b5de6-201">d.</span></span> <span data-ttu-id="b5de6-202">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b5de6-202">Click **Create**.</span></span>
 
### <a name="creating-a-opsgenie-test-user"></a><span data-ttu-id="b5de6-203">建立 OpsGenie 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b5de6-203">Creating a OpsGenie test user</span></span>

<span data-ttu-id="b5de6-204">本節的目標是要在 OpsGenie 中建立一個名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="b5de6-204">The objective of this section is to create a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="b5de6-205">在 Web 瀏覽器視窗中，以系統管理員身分登入您的 OpsGenie 租用戶。</span><span class="sxs-lookup"><span data-stu-id="b5de6-205">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>

2. <span data-ttu-id="b5de6-206">按一下左側面板中的 [使用者]  以瀏覽至 [使用者] 清單。</span><span class="sxs-lookup"><span data-stu-id="b5de6-206">Navigate to Users list by clicking **User** in left panel.</span></span>
   
   ![OpsGenie 設定](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. <span data-ttu-id="b5de6-208">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="b5de6-208">Click **Add User**.</span></span>

4. <span data-ttu-id="b5de6-209">在 [加入使用者]  對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b5de6-209">On the **Add User** dialog, perform the following steps:</span></span>
   
   ![OpsGenie 設定](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   <span data-ttu-id="b5de6-211">a.</span><span class="sxs-lookup"><span data-stu-id="b5de6-211">a.</span></span> <span data-ttu-id="b5de6-212">在 [電子郵件] 文字方塊中，輸入 BrittaSimon 在 Azure Active Directory 中留下的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="b5de6-212">In the **Email** textbox, type the email address of BrittaSimon addressed in Azure Active Directory.</span></span>
   
   <span data-ttu-id="b5de6-213">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5de6-213">b.</span></span> <span data-ttu-id="b5de6-214">在 [全名] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="b5de6-214">In the **Full Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="b5de6-215">c.</span><span class="sxs-lookup"><span data-stu-id="b5de6-215">c.</span></span> <span data-ttu-id="b5de6-216">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b5de6-216">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="b5de6-217">Britta 會收到一封指示如何設定她的設定檔的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="b5de6-217">Britta gets an email with instructions for setting up her profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b5de6-218">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b5de6-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b5de6-219">在本節中，您會將 OpsGenie 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b5de6-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OpsGenie.</span></span>

![指派使用者][200] 

<span data-ttu-id="b5de6-221">**若要將 Britta Simon 指派給 OpsGenie，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b5de6-221">**To assign Britta Simon to OpsGenie, perform the following steps:**</span></span>

1. <span data-ttu-id="b5de6-222">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b5de6-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b5de6-224">在應用程式清單中，選取 [OpsGenie] 。</span><span class="sxs-lookup"><span data-stu-id="b5de6-224">In the applications list, select **OpsGenie**.</span></span>

    ![設定單一登入](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. <span data-ttu-id="b5de6-226">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b5de6-226">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="b5de6-228">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b5de6-228">Click **Add** button.</span></span> <span data-ttu-id="b5de6-229">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b5de6-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="b5de6-231">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="b5de6-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b5de6-232">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b5de6-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5de6-233">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b5de6-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b5de6-234">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b5de6-234">Testing single sign-on</span></span>

<span data-ttu-id="b5de6-235">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="b5de6-235">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="b5de6-236">當您在「存取面板」中按一下 [OpsGenie] 磚時，應該會自動登入您的 OpsGenie 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b5de6-236">When you click the OpsGenie tile in the Access Panel, you should get automatically signed-on to your OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b5de6-237">其他資源</span><span class="sxs-lookup"><span data-stu-id="b5de6-237">Additional resources</span></span>

* [<span data-ttu-id="b5de6-238">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="b5de6-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5de6-239">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b5de6-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

