---
title: "教學課程：Azure Active Directory 與 Bambu by Sprout Social 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Bambu by Sprout Social 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 985966d26f6ed0dcd4db47589abf94260ce62bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="10429-103">教學課程：Azure Active Directory 與 Bambu by Sprout Social 整合</span><span class="sxs-lookup"><span data-stu-id="10429-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="10429-104">在本教學課程中，您將了解如何將 Bambu by Sprout Social 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="10429-104">In this tutorial, you learn how to integrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="10429-105">將 Bambu by Sprout Social 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="10429-105">Integrating Bambu by Sprout Social with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="10429-106">您可以在 Azure AD 中控制可存取 Bambu by Sprout Social 的人員</span><span class="sxs-lookup"><span data-stu-id="10429-106">You can control in Azure AD who has access to Bambu by Sprout Social</span></span>
- <span data-ttu-id="10429-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Bambu by Sprout Social (單一登入)</span><span class="sxs-lookup"><span data-stu-id="10429-107">You can enable your users to automatically get signed-on to Bambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="10429-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="10429-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="10429-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="10429-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Bambu by Sprout Social, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="10429-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="10429-110">Prerequisites</span></span>

<span data-ttu-id="10429-111">若要設定 Azure AD 與 Bambu by Sprout Social 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="10429-111">To configure Azure AD integration with Bambu by Sprout Social, you need the following items:</span></span>

- <span data-ttu-id="10429-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="10429-112">An Azure AD subscription</span></span>
- <span data-ttu-id="10429-113">啟用 Bambu by Sprout Social 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="10429-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="10429-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="10429-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="10429-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="10429-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="10429-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="10429-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="10429-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="10429-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="10429-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="10429-118">Scenario description</span></span>
<span data-ttu-id="10429-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="10429-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="10429-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="10429-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="10429-121">從資源庫新增 Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="10429-121">Adding Bambu by Sprout Social from the gallery</span></span>
2. <span data-ttu-id="10429-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="10429-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-the-gallery"></a><span data-ttu-id="10429-123">從資源庫新增 Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="10429-123">Adding Bambu by Sprout Social from the gallery</span></span>
<span data-ttu-id="10429-124">若要設定將 Bambu by Sprout Social 整合到 Azure AD 中，您需要從資源庫將 Bambu by Sprout Social 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="10429-124">To configure the integration of Bambu by Sprout Social into Azure AD, you need to add Bambu by Sprout Social from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="10429-125">**若要從資源庫新增 Bambu by Sprout Social，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="10429-125">**To add Bambu by Sprout Social from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="10429-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="10429-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="10429-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="10429-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="10429-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="10429-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="10429-131">按一下對話方塊頂端的 [新應用程式] 按鈕來新增新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="10429-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="10429-133">在搜尋方塊中，輸入 **Bambu by Sprout Social**。</span><span class="sxs-lookup"><span data-stu-id="10429-133">In the search box, type **Bambu by Sprout Social**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="10429-135">在結果窗格中，選取 [Bambu by Sprout Social]，然後按一下 [加入] 按鈕來新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="10429-135">In the results panel, select **Bambu by Sprout Social**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="10429-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="10429-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="10429-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Bambu by Sprout Social 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="10429-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="10429-139">若要讓單一登入能夠運作，Azure AD 必須知道 Bambu by Sprout Social 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="10429-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bambu by Sprout Social is to a user in Azure AD.</span></span> <span data-ttu-id="10429-140">換句話說，必須在 Azure AD 使用者與 Bambu by Sprout Social 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="10429-140">In other words, a link relationship between an Azure AD user and the related user in Bambu by Sprout Social needs to be established.</span></span>

<span data-ttu-id="10429-141">建立此連結關聯性的方法，就是將 Azure AD 中 [使用者名稱] 的值，指派為 Bambu by Sprout Social 中 [Username] 的值。</span><span class="sxs-lookup"><span data-stu-id="10429-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="10429-142">若要設定及測試與 Bambu by Sprout Social 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="10429-142">To configure and test Azure AD single sign-on with Bambu by Sprout Social, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="10429-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="10429-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="10429-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="10429-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="10429-145">**[建立 Bambu by Sprout Social 測試使用者](#creating-a-bambu-by-sprout-social-test-user)** - 在 Bambu by Sprout Social 中建立一個與 Azure AD 中代表 Britta Simon 的項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="10429-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - to have a counterpart of Britta Simon in Bambu by Sprout Social that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="10429-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="10429-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="10429-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="10429-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="10429-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="10429-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="10429-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Bambu by Sprout Social 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="10429-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="10429-150">**若要設定與 Bambu by Sprout Social 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="10429-150">**To configure Azure AD single sign-on with Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="10429-151">在 Azure 入口網站的 [Bambu by Sprout Social] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="10429-151">In the Azure portal, on the **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="10429-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="10429-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="10429-155">在 [Bambu by Sprout Social 網域和 URL] 區段中，使用者不需要執行任何步驟，因為應用程式已經與 Azure 預先整合。</span><span class="sxs-lookup"><span data-stu-id="10429-155">On the **Bambu by Sprout Social Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![設定單一登入](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="10429-157">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="10429-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="10429-159">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="10429-159">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="10429-161">在 [Bambu by Sprout Social 組態] 區段上，按一下 [設定 Bambu by Sprout Social] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="10429-161">On the **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** to open **Configure sign-on** window.</span></span> <span data-ttu-id="10429-162">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="10429-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="10429-164">若要在 **Bambu by Sprout Social** 這一端設定單一登入，您必須將所下載的「中繼資料 XML」和「SAML 單一登入服務 URL」傳送給 [Bambu by Sprout Social 支援小組](mailto:support@getbambu.com)。</span><span class="sxs-lookup"><span data-stu-id="10429-164">To configure single sign-on on **Bambu by Sprout Social** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="10429-165">他們將會設定妥當，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="10429-165">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="10429-166">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="10429-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="10429-167">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="10429-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click on the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="10429-168">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="10429-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

To ensure users can sign-in to Bambu by Sprout Social after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Bambu by Sprout Social in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="10429-169">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="10429-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="10429-170">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="10429-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="10429-172">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="10429-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="10429-173">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="10429-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="10429-175">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="10429-175">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="10429-177">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="10429-177">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="10429-179">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="10429-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="10429-181">a.</span><span class="sxs-lookup"><span data-stu-id="10429-181">a.</span></span> <span data-ttu-id="10429-182">在 [名稱] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="10429-182">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="10429-183">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="10429-183">b.</span></span> <span data-ttu-id="10429-184">在 [使用者名稱] 文字方塊中，輸入 Britta Simon 的「電子郵件地址」。</span><span class="sxs-lookup"><span data-stu-id="10429-184">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="10429-185">c.</span><span class="sxs-lookup"><span data-stu-id="10429-185">c.</span></span> <span data-ttu-id="10429-186">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="10429-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="10429-187">d.</span><span class="sxs-lookup"><span data-stu-id="10429-187">d.</span></span> <span data-ttu-id="10429-188">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="10429-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="10429-189">建立 Bambu by Sprout Social 測試使用者</span><span class="sxs-lookup"><span data-stu-id="10429-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="10429-190">應用程式支援及時 (Just In Time) 使用者佈建，而在驗證之後，則會在應用程式中自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="10429-190">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="10429-191">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="10429-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="10429-192">在本節中，您會將 Bambu by Sprout Social 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="10429-192">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bambu by Sprout Social.</span></span>

![指派使用者][200] 

<span data-ttu-id="10429-194">**若要將 Britta Simon 指派給 Bambu by Sprout Social，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="10429-194">**To assign Britta Simon to Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="10429-195">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="10429-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="10429-197">在應用程式清單中，選取 [Bambu by Sprout Social]。</span><span class="sxs-lookup"><span data-stu-id="10429-197">In the applications list, select **Bambu by Sprout Social**.</span></span>

    ![設定單一登入](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="10429-199">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="10429-199">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="10429-201">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="10429-201">Click **Add** button.</span></span> <span data-ttu-id="10429-202">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="10429-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="10429-204">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="10429-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="10429-205">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="10429-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="10429-206">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="10429-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="10429-207">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="10429-207">Testing single sign-on</span></span>

<span data-ttu-id="10429-208">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="10429-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="10429-209">當您在「存取面板」中按一下 [Bambu by Sprout Social] 圖格時，應該會自動登入您的 Bambu by Sprout Social 應用程式。</span><span class="sxs-lookup"><span data-stu-id="10429-209">When you click the Bambu by Sprout Social tile in the Access Panel, you should get automatically signed-on to your Bambu by Sprout Social application.</span></span> <span data-ttu-id="10429-210">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="10429-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="10429-211">其他資源</span><span class="sxs-lookup"><span data-stu-id="10429-211">Additional resources</span></span>

* [<span data-ttu-id="10429-212">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="10429-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="10429-213">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="10429-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

