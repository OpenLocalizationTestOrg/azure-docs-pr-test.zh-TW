---
title: "教學課程：Azure Active Directory 與 HappyFox 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 HappyFox 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 8b5ad750d7849e4037ed7ee93c48b5645c68e799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="cd0f6-103">教學課程：Azure Active Directory 與 HappyFox 整合</span><span class="sxs-lookup"><span data-stu-id="cd0f6-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="cd0f6-104">在本教學課程中，您將了解如何整合 HappyFox 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-104">In this tutorial, you learn how to integrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cd0f6-105">HappyFox 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="cd0f6-105">Integrating HappyFox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cd0f6-106">您可以在 Azure AD 中控制可存取 HappyFox 的人員</span><span class="sxs-lookup"><span data-stu-id="cd0f6-106">You can control in Azure AD who has access to HappyFox</span></span>
- <span data-ttu-id="cd0f6-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 HappyFox (單一登入)</span><span class="sxs-lookup"><span data-stu-id="cd0f6-107">You can enable your users to automatically get signed-on to HappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cd0f6-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="cd0f6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cd0f6-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd0f6-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="cd0f6-110">Prerequisites</span></span>

<span data-ttu-id="cd0f6-111">若要設定 Azure AD 與 HappyFox 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="cd0f6-111">To configure Azure AD integration with HappyFox, you need the following items:</span></span>

- <span data-ttu-id="cd0f6-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cd0f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cd0f6-113">啟用 HappyFox 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cd0f6-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cd0f6-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cd0f6-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="cd0f6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cd0f6-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cd0f6-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cd0f6-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="cd0f6-118">Scenario description</span></span>
<span data-ttu-id="cd0f6-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cd0f6-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="cd0f6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cd0f6-121">從資源庫新增 HappyFox</span><span class="sxs-lookup"><span data-stu-id="cd0f6-121">Adding HappyFox from the gallery</span></span>
2. <span data-ttu-id="cd0f6-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cd0f6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-the-gallery"></a><span data-ttu-id="cd0f6-123">從資源庫新增 HappyFox</span><span class="sxs-lookup"><span data-stu-id="cd0f6-123">Adding HappyFox from the gallery</span></span>
<span data-ttu-id="cd0f6-124">若要設定 HappyFox 與 Azure AD 整合，您需要從資源庫將 HappyFox 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-124">To configure the integration of HappyFox into Azure AD, you need to add HappyFox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cd0f6-125">**若要從資源庫新增 HappyFox，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cd0f6-125">**To add HappyFox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cd0f6-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cd0f6-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cd0f6-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="cd0f6-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="cd0f6-133">在搜尋方塊中，鍵入 **HappyFox**。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-133">In the search box, type **HappyFox**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_search.png)

5. <span data-ttu-id="cd0f6-135">在結果窗格中，選取 [HappyFox]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-135">In the results panel, select **HappyFox**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cd0f6-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cd0f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cd0f6-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 HappyFox 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cd0f6-139">若要讓單一登入運作，Azure AD 必須知道 HappyFox 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HappyFox is to a user in Azure AD.</span></span> <span data-ttu-id="cd0f6-140">換句話說，必須在 Azure AD 使用者和 HappyFox 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-140">In other words, a link relationship between an Azure AD user and the related user in HappyFox needs to be established.</span></span>

<span data-ttu-id="cd0f6-141">在 HappyFox 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-141">In HappyFox, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cd0f6-142">若要設定及測試與 HappyFox 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="cd0f6-142">To configure and test Azure AD single sign-on with HappyFox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cd0f6-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cd0f6-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cd0f6-145">**[建立 HappyFox 測試使用者](#creating-a-happyfox-test-user)** - 在 HappyFox 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - to have a counterpart of Britta Simon in HappyFox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cd0f6-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cd0f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cd0f6-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cd0f6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cd0f6-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 HappyFox 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="cd0f6-150">**若要設定與 HappyFox 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cd0f6-150">**To configure Azure AD single sign-on with HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="cd0f6-151">在 Azure 入口網站的 [HappyFox] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-151">In the Azure portal, on the **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="cd0f6-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_samlbase.png)

3. <span data-ttu-id="cd0f6-155">在 [HappyFox 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cd0f6-155">On the **HappyFox Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="cd0f6-157">a.</span><span class="sxs-lookup"><span data-stu-id="cd0f6-157">a.</span></span> <span data-ttu-id="cd0f6-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.happyfox.com/`</span><span class="sxs-lookup"><span data-stu-id="cd0f6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="cd0f6-159">b.</span><span class="sxs-lookup"><span data-stu-id="cd0f6-159">b.</span></span> <span data-ttu-id="cd0f6-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="cd0f6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cd0f6-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-161">These values are not real.</span></span> <span data-ttu-id="cd0f6-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cd0f6-163">請連絡 [HappyFox 客戶支援小組](https://support.happyfox.com/home)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) to get these values.</span></span> 
 
4. <span data-ttu-id="cd0f6-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_certificate.png) 

5. <span data-ttu-id="cd0f6-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cd0f6-168">在 [HappyFox 設定] 區段上，按一下 [設定 HappyFox] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-168">On the **HappyFox Configuration** section, click **Configure HappyFox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cd0f6-169">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section**.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_configure.png) 

7. <span data-ttu-id="cd0f6-171">登入您的 HappyFox 人員入口網站並巡覽至 [管理]，然後按一下 [整合] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-171">Sign on to your HappyFox staff portal and navigate to **Manage**, Click on **Integrations** tab.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/header.png) 

8. <span data-ttu-id="cd0f6-173">在 [整合] 索引標籤中，按一下 [SAML 整合] 下的 [設定] 以開啟 [單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-173">In the Integrations tab, Click **Configure** under **SAML Integration** to open the Single Sign On Settings.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/configure.png) 

9. <span data-ttu-id="cd0f6-175">在 [SAML 設定] 區段中，將您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 貼到 [SSO 目標 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-175">Inside SAML configuration section, paste the **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/targeturl.png)

10. <span data-ttu-id="cd0f6-177">在筆記本中開啟從 Azure 入口網站下載的憑證，然後將其內容貼到 [IdP 簽章] 區段中。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-177">Open the certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/cert.png)

11. <span data-ttu-id="cd0f6-179">按一下 [儲存設定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-179">Click **Save Settings** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="cd0f6-181">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="cd0f6-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cd0f6-182">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cd0f6-183">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cd0f6-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cd0f6-184">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cd0f6-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="cd0f6-185">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="cd0f6-187">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cd0f6-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cd0f6-188">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-happyfox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cd0f6-190">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-happyfox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cd0f6-192">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-happyfox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cd0f6-194">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cd0f6-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cd0f6-196">a.</span><span class="sxs-lookup"><span data-stu-id="cd0f6-196">a.</span></span> <span data-ttu-id="cd0f6-197">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cd0f6-198">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-198">b.</span></span> <span data-ttu-id="cd0f6-199">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cd0f6-200">c.</span><span class="sxs-lookup"><span data-stu-id="cd0f6-200">c.</span></span> <span data-ttu-id="cd0f6-201">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cd0f6-202">d.</span><span class="sxs-lookup"><span data-stu-id="cd0f6-202">d.</span></span> <span data-ttu-id="cd0f6-203">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="cd0f6-204">建立 HappyFox 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cd0f6-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="cd0f6-205">應用程式支援及時 (Just In Time) 使用者佈建，而在驗證之後，則會在應用程式中自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-205">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cd0f6-206">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cd0f6-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cd0f6-207">在本節中，您會將 HappyFox 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HappyFox.</span></span>

![指派使用者][200] 

<span data-ttu-id="cd0f6-209">**若要將 Britta Simon 指派給 HappyFox，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cd0f6-209">**To assign Britta Simon to HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="cd0f6-210">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="cd0f6-212">在應用程式清單中，選取 [HappyFox]。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-212">In the applications list, select **HappyFox**.</span></span>

    ![設定單一登入](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_app.png) 

3. <span data-ttu-id="cd0f6-214">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-214">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="cd0f6-216">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-216">Click **Add** button.</span></span> <span data-ttu-id="cd0f6-217">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="cd0f6-219">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cd0f6-220">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cd0f6-221">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cd0f6-222">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="cd0f6-222">Testing single sign-on</span></span>

<span data-ttu-id="cd0f6-223">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="cd0f6-224">當您在存取面板中按一下 [HappyFox] 磚時，應該會看到 HappyFox 應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-224">When you click the HappyFox tile in the Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="cd0f6-225">您應該會在登入頁面上看到 [SAML] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-225">You should see the **‘SAML’** button on the sign-in page.</span></span>

    ![外掛程式](./media/active-directory-saas-happyfox-tutorial/saml.png) 

2. <span data-ttu-id="cd0f6-227">按一下 [SAML] 按鈕，使用您的 Azure AD 帳戶登入 HappyFox。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-227">Click the **‘SAML’** button to log in to HappyFox using your Azure AD account.</span></span>

<span data-ttu-id="cd0f6-228">如需存取面板的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="cd0f6-228">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cd0f6-229">其他資源</span><span class="sxs-lookup"><span data-stu-id="cd0f6-229">Additional resources</span></span>

* [<span data-ttu-id="cd0f6-230">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="cd0f6-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cd0f6-231">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="cd0f6-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_203.png

