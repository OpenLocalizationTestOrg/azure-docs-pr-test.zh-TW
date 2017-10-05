---
title: "教學課程：Azure Active Directory 與 FreshGrade 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 FreshGrade 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1055bba6-f4df-462e-bc9b-1ad5ada0f638
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 3ff3e5aab679f8ee610c98f8a4089308adcce48f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshgrade"></a><span data-ttu-id="6a5a0-103">教學課程：Azure Active Directory 與 FreshGrade 整合</span><span class="sxs-lookup"><span data-stu-id="6a5a0-103">Tutorial: Azure Active Directory integration with FreshGrade</span></span>

<span data-ttu-id="6a5a0-104">在本教學課程中，您會了解如何整合 FreshGrade 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-104">In this tutorial, you learn how to integrate FreshGrade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a5a0-105">FreshGrade 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="6a5a0-105">Integrating FreshGrade with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6a5a0-106">您可以在 Azure AD 中控制可存取 FreshGrade 的人員</span><span class="sxs-lookup"><span data-stu-id="6a5a0-106">You can control in Azure AD who has access to FreshGrade</span></span>
- <span data-ttu-id="6a5a0-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 FreshGrade (單一登入)</span><span class="sxs-lookup"><span data-stu-id="6a5a0-107">You can enable your users to automatically get signed-on to FreshGrade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6a5a0-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="6a5a0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6a5a0-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a5a0-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6a5a0-110">Prerequisites</span></span>

<span data-ttu-id="6a5a0-111">若要設定 Azure AD 與 FreshGrade 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="6a5a0-111">To configure Azure AD integration with FreshGrade, you need the following items:</span></span>

- <span data-ttu-id="6a5a0-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6a5a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a5a0-113">已啟用 FreshGrade 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6a5a0-113">A FreshGrade single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a5a0-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a5a0-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="6a5a0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a5a0-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a5a0-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a5a0-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="6a5a0-118">Scenario description</span></span>
<span data-ttu-id="6a5a0-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a5a0-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="6a5a0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a5a0-121">從資源庫新增 FreshGrade</span><span class="sxs-lookup"><span data-stu-id="6a5a0-121">Adding FreshGrade from the gallery</span></span>
2. <span data-ttu-id="6a5a0-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6a5a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshgrade-from-the-gallery"></a><span data-ttu-id="6a5a0-123">從資源庫新增 FreshGrade</span><span class="sxs-lookup"><span data-stu-id="6a5a0-123">Adding FreshGrade from the gallery</span></span>
<span data-ttu-id="6a5a0-124">若要設定將 FreshGrade 整合到 Azure AD 中，您需要從資源庫將 FreshGrade 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-124">To configure the integration of FreshGrade into Azure AD, you need to add FreshGrade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6a5a0-125">**若要從資源庫新增 FreshGrade，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6a5a0-125">**To add FreshGrade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6a5a0-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6a5a0-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6a5a0-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="6a5a0-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="6a5a0-133">在搜尋方塊中，輸入 **FreshGrade**。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-133">In the search box, type **FreshGrade**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_search.png)

5. <span data-ttu-id="6a5a0-135">在結果窗格中，選取 [FreshGrade]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-135">In the results panel, select **FreshGrade**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6a5a0-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6a5a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6a5a0-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 FreshGrade 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-138">In this section, you configure and test Azure AD single sign-on with FreshGrade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6a5a0-139">若要讓單一登入運作，Azure AD 必須知道 FreshGrade 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshGrade is to a user in Azure AD.</span></span> <span data-ttu-id="6a5a0-140">換句話說，必須建立 Azure AD 使用者和 FreshGrade 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-140">In other words, a link relationship between an Azure AD user and the related user in FreshGrade needs to be established.</span></span>

<span data-ttu-id="6a5a0-141">在 FreshGrade 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-141">In FreshGrade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6a5a0-142">若要使用 FreshGrade 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="6a5a0-142">To configure and test Azure AD single sign-on with FreshGrade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6a5a0-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6a5a0-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a5a0-145">**[建立 FreshGrade 測試使用者](#creating-a-freshgrade-test-user)** - 在 FreshGrade 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - to have a counterpart of Britta Simon in FreshGrade that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6a5a0-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a5a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6a5a0-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6a5a0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6a5a0-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 FreshGrade 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FreshGrade application.</span></span>

<span data-ttu-id="6a5a0-150">**若要設定與 FreshGrade 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6a5a0-150">**To configure Azure AD single sign-on with FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="6a5a0-151">在 Azure 入口網站的 [FreshGrade] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-151">In the Azure portal, on the **FreshGrade** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="6a5a0-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_samlbase.png)

3. <span data-ttu-id="6a5a0-155">在 [FreshGrade 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6a5a0-155">On the **FreshGrade Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_url.png)

    <span data-ttu-id="6a5a0-157">a.</span><span class="sxs-lookup"><span data-stu-id="6a5a0-157">a.</span></span> <span data-ttu-id="6a5a0-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰</span><span class="sxs-lookup"><span data-stu-id="6a5a0-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
      | |
      |--|
      | `https://<subdomain>.freshgrade.com/login` |    
      | `https://<subdomain>.onboarding.freshgrade.com/login` |

    <span data-ttu-id="6a5a0-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-159">b.</span></span> <span data-ttu-id="6a5a0-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="6a5a0-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
      | |
      |--|
      | `https://login.onboarding.freshgrade.com:443/saml/metadata/alias/<instancename>` |      
      | `https://login.freshgrade.com:443/saml/metadata/alias/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="6a5a0-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-161">These values are not real.</span></span> <span data-ttu-id="6a5a0-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6a5a0-163">請連絡 [FreshGrade 用戶端支援小組](mailTo:support@freshgrade.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-163">Contact [FreshGrade Client support team](mailTo:support@freshgrade.com) to get these values.</span></span> 
 


4. <span data-ttu-id="6a5a0-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_certificate.png) 

5. <span data-ttu-id="6a5a0-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6a5a0-168">在 [FreshGrade 設定] 區段中，按一下 [設定 FreshGrade] 可開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-168">On the **FreshGrade Configuration** section, click **Configure FreshGrade** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6a5a0-169">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_configure.png) 

7. <span data-ttu-id="6a5a0-171">若要產生**中繼資料** URL，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="6a5a0-171">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="6a5a0-172">a.</span><span class="sxs-lookup"><span data-stu-id="6a5a0-172">a.</span></span> <span data-ttu-id="6a5a0-173">按一下 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-173">Click **App registrations**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appregistrations.png)
   
    <span data-ttu-id="6a5a0-175">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-175">b.</span></span> <span data-ttu-id="6a5a0-176">按一下 [端點] 以開啟 [端點] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-176">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpointicon.png)

    <span data-ttu-id="6a5a0-178">c.</span><span class="sxs-lookup"><span data-stu-id="6a5a0-178">c.</span></span> <span data-ttu-id="6a5a0-179">按一下複製按鈕複製 [同盟中繼資料文件] URL，並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-179">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpoint.png)
     
    <span data-ttu-id="6a5a0-181">d.</span><span class="sxs-lookup"><span data-stu-id="6a5a0-181">d.</span></span> <span data-ttu-id="6a5a0-182">現在，移至 [FreshGrade] 的屬性頁面，使用 [複製] 按鈕複製 [應用程式識別碼]，並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-182">Now go to the property page of **FreshGrade** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appid.png)

    <span data-ttu-id="6a5a0-184">e.</span><span class="sxs-lookup"><span data-stu-id="6a5a0-184">e.</span></span> <span data-ttu-id="6a5a0-185">使用下列模式產生**中繼資料 URL**︰`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="6a5a0-185">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

8. <span data-ttu-id="6a5a0-186">若要在 **FreshGrade** 端設定單一登入，您必須將「中繼資料 URL」和「SAML 單一登入服務 URL」傳送給 [FreshGrade 支援小組](mailTo:support@freshgrade.com)。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-186">To configure single sign-on on **FreshGrade** side, you need to send the **Metadata URL** and **SAML Single Sign-On Service URL** to [FreshGrade support team](mailTo:support@freshgrade.com).</span></span> <span data-ttu-id="6a5a0-187">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="6a5a0-188">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="6a5a0-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6a5a0-189">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6a5a0-190">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6a5a0-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6a5a0-191">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6a5a0-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="6a5a0-192">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="6a5a0-194">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6a5a0-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6a5a0-195">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6a5a0-197">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6a5a0-199">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6a5a0-201">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6a5a0-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6a5a0-203">a.</span><span class="sxs-lookup"><span data-stu-id="6a5a0-203">a.</span></span> <span data-ttu-id="6a5a0-204">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a5a0-205">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-205">b.</span></span> <span data-ttu-id="6a5a0-206">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6a5a0-207">c.</span><span class="sxs-lookup"><span data-stu-id="6a5a0-207">c.</span></span> <span data-ttu-id="6a5a0-208">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6a5a0-209">d.</span><span class="sxs-lookup"><span data-stu-id="6a5a0-209">d.</span></span> <span data-ttu-id="6a5a0-210">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-210">Click **Create**.</span></span>
 
### <a name="creating-a-freshgrade-test-user"></a><span data-ttu-id="6a5a0-211">建立 FreshGrade 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6a5a0-211">Creating a FreshGrade test user</span></span>

<span data-ttu-id="6a5a0-212">在本節中，您要在 FreshGrade 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-212">In this section, you create a user called Britta Simon in FreshGrade.</span></span> <span data-ttu-id="6a5a0-213">請與 [FreshGrade 支援小組](mailTo:support@freshgrade.com)合作，在 FreshGrade 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-213">Please work with [FreshGrade support team](mailTo:support@freshgrade.com) to add the users in the FreshGrade platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6a5a0-214">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6a5a0-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6a5a0-215">在本節中，您會授權 Britta Simon 存取 FreshGrade，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FreshGrade.</span></span>

![指派使用者][200] 

<span data-ttu-id="6a5a0-217">**若要將 Britta Simon 指派給 FreshGrade，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6a5a0-217">**To assign Britta Simon to FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="6a5a0-218">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="6a5a0-220">在應用程式清單中，選取 [FreshGrade]。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-220">In the applications list, select **FreshGrade**.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_app.png) 

3. <span data-ttu-id="6a5a0-222">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-222">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="6a5a0-224">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-224">Click **Add** button.</span></span> <span data-ttu-id="6a5a0-225">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="6a5a0-227">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6a5a0-228">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a5a0-229">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6a5a0-230">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="6a5a0-230">Testing single sign-on</span></span>

<span data-ttu-id="6a5a0-231">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6a5a0-232">當您在「存取面板」中按一下 [FreshGrade] 圖格時，應該會自動登入您的 FreshGrade 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-232">When you click the FreshGrade tile in the Access Panel, you should get automatically signed-on to your FreshGrade application.</span></span>
<span data-ttu-id="6a5a0-233">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="6a5a0-233">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6a5a0-234">其他資源</span><span class="sxs-lookup"><span data-stu-id="6a5a0-234">Additional resources</span></span>

* [<span data-ttu-id="6a5a0-235">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="6a5a0-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a5a0-236">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="6a5a0-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_203.png

