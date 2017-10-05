---
title: "教學課程：Azure Active Directory 與 Promapp 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Promapp 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 27013ca9724cf2f57fc85f5f4ccb71921ca57a3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="9e35c-103">教學課程：Azure Active Directory 與 Promapp 整合</span><span class="sxs-lookup"><span data-stu-id="9e35c-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="9e35c-104">在本教學課程中，您會了解如何整合 Promapp 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="9e35c-104">In this tutorial, you learn how to integrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9e35c-105">Promapp 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="9e35c-105">Integrating Promapp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9e35c-106">您可以在 Azure AD 中控制可存取 Promapp 的人員</span><span class="sxs-lookup"><span data-stu-id="9e35c-106">You can control in Azure AD who has access to Promapp</span></span>
- <span data-ttu-id="9e35c-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Promapp (單一登入)</span><span class="sxs-lookup"><span data-stu-id="9e35c-107">You can enable your users to automatically get signed-on to Promapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9e35c-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="9e35c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9e35c-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="9e35c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e35c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9e35c-110">Prerequisites</span></span>

<span data-ttu-id="9e35c-111">若要設定與 Promapp 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="9e35c-111">To configure Azure AD integration with Promapp, you need the following items:</span></span>

- <span data-ttu-id="9e35c-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9e35c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9e35c-113">啟用 Promapp 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9e35c-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9e35c-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9e35c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9e35c-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="9e35c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9e35c-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9e35c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9e35c-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="9e35c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9e35c-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="9e35c-118">Scenario description</span></span>
<span data-ttu-id="9e35c-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9e35c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9e35c-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="9e35c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9e35c-121">從資源庫加入 Promapp</span><span class="sxs-lookup"><span data-stu-id="9e35c-121">Adding Promapp from the gallery</span></span>
2. <span data-ttu-id="9e35c-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9e35c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-the-gallery"></a><span data-ttu-id="9e35c-123">從資源庫加入 Promapp</span><span class="sxs-lookup"><span data-stu-id="9e35c-123">Adding Promapp from the gallery</span></span>
<span data-ttu-id="9e35c-124">若要設定 Promapp 與 Azure AD 整合，您需要從資源庫將 Promapp 加入到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="9e35c-124">To configure the integration of Promapp into Azure AD, you need to add Promapp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9e35c-125">**若要從資源庫加入 Promapp，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9e35c-125">**To add Promapp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9e35c-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="9e35c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9e35c-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9e35c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9e35c-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9e35c-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="9e35c-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9e35c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="9e35c-133">在搜尋方塊中，輸入 **Promapp**。</span><span class="sxs-lookup"><span data-stu-id="9e35c-133">In the search box, type **Promapp**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="9e35c-135">在結果面板中，選取 [Promapp]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="9e35c-135">In the results panel, select **Promapp**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9e35c-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9e35c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9e35c-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Promapp 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9e35c-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9e35c-139">若要讓單一登入運作，Azure AD 必須知道 Promapp 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="9e35c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Promapp is to a user in Azure AD.</span></span> <span data-ttu-id="9e35c-140">換句話說，必須在 Azure AD 使用者和 Promapp 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9e35c-140">In other words, a link relationship between an Azure AD user and the related user in Promapp needs to be established.</span></span>

<span data-ttu-id="9e35c-141">在 Promapp 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9e35c-141">In Promapp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9e35c-142">若要設定及測試對 Promapp 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="9e35c-142">To configure and test Azure AD single sign-on with Promapp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9e35c-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="9e35c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9e35c-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9e35c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9e35c-145">**[建立 Promapp 測試使用者](#creating-a-promapp-test-user)** - 使 Promapp 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="9e35c-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - to have a counterpart of Britta Simon in Promapp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9e35c-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9e35c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9e35c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="9e35c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9e35c-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9e35c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9e35c-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Promapp 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="9e35c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="9e35c-150">**若要使用 Promapp 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9e35c-150">**To configure Azure AD single sign-on with Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="9e35c-151">在 Azure 入口網站的 [Promapp] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="9e35c-151">In the Azure portal, on the **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="9e35c-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="9e35c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="9e35c-155">在 [Promapp 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9e35c-155">On the **Promapp Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="9e35c-157">a.</span><span class="sxs-lookup"><span data-stu-id="9e35c-157">a.</span></span> <span data-ttu-id="9e35c-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="9e35c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="9e35c-159">b.</span><span class="sxs-lookup"><span data-stu-id="9e35c-159">b.</span></span> <span data-ttu-id="9e35c-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="9e35c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9e35c-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="9e35c-161">These values are not real.</span></span> <span data-ttu-id="9e35c-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="9e35c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9e35c-163">請連絡 [Promapp 客戶支援小組](https://www.promapp.com/about-us/contact-us/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="9e35c-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="9e35c-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="9e35c-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="9e35c-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="9e35c-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9e35c-168">在 [Promapp 組態] 區段上，按一下 [設定 Promapp] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="9e35c-168">On the **Promapp Configuration** section, click **Configure Promapp** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9e35c-169">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="9e35c-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="9e35c-171">以系統管理員身分登入您的 Promapp 公司網站。</span><span class="sxs-lookup"><span data-stu-id="9e35c-171">Sign-on to your Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="9e35c-172">在頂端的功能表中，按一下 [系統管理員] 。</span><span class="sxs-lookup"><span data-stu-id="9e35c-172">In the menu on the top, click **Admin**.</span></span> 
   
    ![Azure AD 單一登入][12]

9. <span data-ttu-id="9e35c-174">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="9e35c-174">Click **Configure**.</span></span> 
   
    ![Azure AD 單一登入][13]

10. <span data-ttu-id="9e35c-176">在 [安全性]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9e35c-176">On the **Security** dialog, perform the following steps:</span></span>
   
    ![Azure AD 單一登入][14]
    
    <span data-ttu-id="9e35c-178">a.</span><span class="sxs-lookup"><span data-stu-id="9e35c-178">a.</span></span> <span data-ttu-id="9e35c-179">將您從 Azure 入口網站複製的 [SAML 單一登入服務 URL]，貼到 [SSO 登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="9e35c-179">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="9e35c-180">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="9e35c-180">b.</span></span> <span data-ttu-id="9e35c-181">針對 [SSO - 單一登入模式]，選取 [選擇性]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="9e35c-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="9e35c-182">c.</span><span class="sxs-lookup"><span data-stu-id="9e35c-182">c.</span></span> <span data-ttu-id="9e35c-183">在記事本中開啟下載的憑證，複製憑證的內容但不包含第一行 (-----BEGIN CERTIFICATE-----) 和最後一行 (-----END CERTIFICATE-----)，將它貼到 [SSO-x.509 憑證] 文字方塊中，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="9e35c-183">Open the downloaded certificate in notepad, copy the certificate content without the first line (-----BEGIN CERTIFICATE-----) and the last line (-----END CERTIFICATE-----), paste it into the **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="9e35c-184">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="9e35c-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9e35c-185">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="9e35c-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9e35c-186">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9e35c-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9e35c-187">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9e35c-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="9e35c-188">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="9e35c-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="9e35c-190">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9e35c-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9e35c-191">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="9e35c-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9e35c-193">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="9e35c-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9e35c-195">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9e35c-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9e35c-197">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9e35c-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9e35c-199">a.</span><span class="sxs-lookup"><span data-stu-id="9e35c-199">a.</span></span> <span data-ttu-id="9e35c-200">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="9e35c-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9e35c-201">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="9e35c-201">b.</span></span> <span data-ttu-id="9e35c-202">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="9e35c-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9e35c-203">c.</span><span class="sxs-lookup"><span data-stu-id="9e35c-203">c.</span></span> <span data-ttu-id="9e35c-204">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="9e35c-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9e35c-205">d.</span><span class="sxs-lookup"><span data-stu-id="9e35c-205">d.</span></span> <span data-ttu-id="9e35c-206">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9e35c-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="9e35c-207">建立 Promapp 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9e35c-207">Creating a Promapp test user</span></span>

<span data-ttu-id="9e35c-208">Promapp 應用程式支援 Just-in-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="9e35c-208">The Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="9e35c-209">這表示，在使用存取面板嘗試存取應用程式期間，必要時會自動建立使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e35c-209">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9e35c-210">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9e35c-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9e35c-211">在本節中，您會將 Promapp 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9e35c-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Promapp.</span></span>

![指派使用者][200] 

<span data-ttu-id="9e35c-213">**若要將 Britta Simon 指派到 Promapp，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="9e35c-213">**To assign Britta Simon to Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="9e35c-214">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9e35c-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="9e35c-216">在應用程式清單中，選取 **Promapp**。</span><span class="sxs-lookup"><span data-stu-id="9e35c-216">In the applications list, select **Promapp**.</span></span>

    ![設定單一登入](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="9e35c-218">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9e35c-218">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="9e35c-220">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9e35c-220">Click **Add** button.</span></span> <span data-ttu-id="9e35c-221">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9e35c-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="9e35c-223">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="9e35c-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9e35c-224">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9e35c-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9e35c-225">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9e35c-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9e35c-226">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="9e35c-226">Testing single sign-on</span></span>

<span data-ttu-id="9e35c-227">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="9e35c-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="9e35c-228">當您在存取面板中按一下 Promapp 磚時，應該會自動登入您的 Promapp 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9e35c-228">When you click the Promapp tile in the Access Panel, you should get automatically signed-on to your Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9e35c-229">其他資源</span><span class="sxs-lookup"><span data-stu-id="9e35c-229">Additional resources</span></span>

* [<span data-ttu-id="9e35c-230">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="9e35c-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9e35c-231">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="9e35c-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png

