---
title: "教學課程：Azure Active Directory 與 Neota Logic Studio 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Neota Logic Studio 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: 99018277392cab44a6b579ad45b4611739a803d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="5c675-103">教學課程：Azure Active Directory 與 Neota Logic Studio 整合</span><span class="sxs-lookup"><span data-stu-id="5c675-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="5c675-104">在本教學課程中，您會了解如何整合 Neota Logic Studio 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="5c675-104">In this tutorial, you learn how to integrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c675-105">Neota Logic Studio 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="5c675-105">Integrating Neota Logic Studio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5c675-106">您可以在 Azure AD 中控制可存取 Neota Logic Studio 的人員</span><span class="sxs-lookup"><span data-stu-id="5c675-106">You can control in Azure AD who has access to Neota Logic Studio</span></span>
- <span data-ttu-id="5c675-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Neota Logic Studio (單一登入)</span><span class="sxs-lookup"><span data-stu-id="5c675-107">You can enable your users to automatically get signed-on to Neota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c675-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="5c675-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5c675-109">如果您想要知道與 Azure AD 整合的 SaaS 應用程式詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5c675-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="5c675-110">[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5c675-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c675-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="5c675-111">Prerequisites</span></span>

<span data-ttu-id="5c675-112">如要設定 Azure AD 與 Neota Logic Studio 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="5c675-112">To configure Azure AD integration with Neota Logic Studio, you need the following items:</span></span>

- <span data-ttu-id="5c675-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5c675-113">An Azure AD subscription</span></span>
- <span data-ttu-id="5c675-114">已啟用 Neota Logic Studio 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5c675-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c675-115">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5c675-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c675-116">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5c675-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c675-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5c675-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c675-118">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="5c675-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c675-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="5c675-119">Scenario description</span></span>

<span data-ttu-id="5c675-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c675-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c675-121">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="5c675-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c675-122">從資源庫新增 Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="5c675-122">Adding Neota Logic Studio from the gallery</span></span>
2. <span data-ttu-id="5c675-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5c675-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-the-gallery"></a><span data-ttu-id="5c675-124">從資源庫新增 Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="5c675-124">Adding Neota Logic Studio from the gallery</span></span>

<span data-ttu-id="5c675-125">若要設定將 Neota Logic Studio 整合到 Azure AD 中，您必須從資源庫將 Neota Logic Studio 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="5c675-125">To configure the integration of Neota Logic Studio into Azure AD, you need to add Neota Logic Studio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5c675-126">**若要從資源庫新增 Neota Logic Studio，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5c675-126">**To add Neota Logic Studio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5c675-127">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5c675-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c675-129">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5c675-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5c675-130">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5c675-130">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="5c675-132">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c675-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="5c675-134">在搜尋方塊中輸入 **Neota Logic Studio**。</span><span class="sxs-lookup"><span data-stu-id="5c675-134">In the search box, type **Neota Logic Studio**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

5. <span data-ttu-id="5c675-136">在結果窗格中，選取 [Neota Logic Studio]，然後按一下 [新增] 按鈕新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c675-136">In the results panel, select **Neota Logic Studio**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c675-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5c675-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="5c675-139">在本節中，您會以測試使用者 Britta Simon 的身分，設定及測試 Azure AD 與 Neota Logic Studio 的單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c675-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5c675-140">若要讓單一登入運作，Azure AD 必須知道 Neota Logic Studio 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="5c675-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Neota Logic Studio is to a user in Azure AD.</span></span> <span data-ttu-id="5c675-141">換句話說，必須建立 Azure AD 使用者和 Neota Logic Studio 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5c675-141">In other words, a link relationship between an Azure AD user and the related user in Neota Logic Studio needs to be established.</span></span>

<span data-ttu-id="5c675-142">建立此連結關聯性的方法，就是將 Azure AD 中 [使用者名稱] 的值指派為 Neota Logic Studio 中 [使用者名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="5c675-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="5c675-143">若要設定及測試 Azure AD 與 Neota Logic Studio 的單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="5c675-143">To configure and test Azure AD single sign-on with Neota Logic Studio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5c675-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="5c675-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5c675-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c675-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c675-146">**[建立 Neota Logic Studio 測試使用者](#creating-a-neota-logic-studio-test-user)** - 使 Neota Logic Studio 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="5c675-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - to have a counterpart of Britta Simon in Neota Logic Studio that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c675-147">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c675-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c675-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="5c675-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c675-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5c675-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c675-150">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Neota Logic Studio 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c675-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="5c675-151">**若要設定 Azure AD 與 Neota Logic Studio 的單一登入，執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5c675-151">**To configure Azure AD single sign-on with Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="5c675-152">在 Azure 入口網站的 [Neota Logic Studio] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="5c675-152">In the Azure portal, on the **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="5c675-154">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c675-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

3. <span data-ttu-id="5c675-156">在 [Neota Logic Studio 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5c675-156">On the **Neota Logic Studio Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="5c675-158">a.</span><span class="sxs-lookup"><span data-stu-id="5c675-158">a.</span></span> <span data-ttu-id="5c675-159">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<sub domain>.neotalogic.com/a/<sub application>`</span><span class="sxs-lookup"><span data-stu-id="5c675-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="5c675-160">b.</span><span class="sxs-lookup"><span data-stu-id="5c675-160">b.</span></span> <span data-ttu-id="5c675-161">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="5c675-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c675-162">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="5c675-162">These values are not the real.</span></span> <span data-ttu-id="5c675-163">使用實際的「登入 URL」和「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="5c675-163">Update these values with the actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="5c675-164">在此建議您在 [識別碼] 中使用唯一的字串值。</span><span class="sxs-lookup"><span data-stu-id="5c675-164">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="5c675-165">請連絡 [Neota Logic Studio 客戶支援小組](https://www.neotalogic.com/contact-us/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="5c675-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="5c675-166">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="5c675-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

5. <span data-ttu-id="5c675-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c675-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5c675-170">若要為您的應用程式設定 SSO，請連絡 [Neota Logic Studio支援小組](https://www.neotalogic.com/contact-us/)並提供所下載的**中繼資料 XML** 檔案。</span><span class="sxs-lookup"><span data-stu-id="5c675-170">To get SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="5c675-171">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="5c675-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5c675-172">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="5c675-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5c675-173">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c675-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c675-174">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5c675-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c675-175">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5c675-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="5c675-177">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5c675-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5c675-178">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5c675-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c675-180">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="5c675-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c675-182">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5c675-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c675-184">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5c675-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c675-186">a.</span><span class="sxs-lookup"><span data-stu-id="5c675-186">a.</span></span> <span data-ttu-id="5c675-187">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="5c675-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c675-188">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c675-188">b.</span></span> <span data-ttu-id="5c675-189">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="5c675-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c675-190">c.</span><span class="sxs-lookup"><span data-stu-id="5c675-190">c.</span></span> <span data-ttu-id="5c675-191">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="5c675-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5c675-192">d.</span><span class="sxs-lookup"><span data-stu-id="5c675-192">d.</span></span> <span data-ttu-id="5c675-193">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5c675-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="5c675-194">建立 Neota Logic Studio 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5c675-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="5c675-195">在本節中，您要在 Neota Logic Studio 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="5c675-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="5c675-196">與 [Neota Logic Studio 客戶支援小組](https://www.neotalogic.com/contact-us/)合作，在 Neota Logic Studio 平台新增使用者。</span><span class="sxs-lookup"><span data-stu-id="5c675-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add the users in the Neota Logic Studio platform.</span></span> <span data-ttu-id="5c675-197">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c675-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5c675-198">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5c675-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5c675-199">在本節中，您會將 Neota Logic Studio 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c675-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Neota Logic Studio.</span></span>

![指派使用者][200] 

<span data-ttu-id="5c675-201">**若要將 Britta Simon 指派至 Neota Logic Studio，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5c675-201">**To assign Britta Simon to Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="5c675-202">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5c675-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="5c675-204">在應用程式清單中，選取 [Neota Logic Studio]。</span><span class="sxs-lookup"><span data-stu-id="5c675-204">In the applications list, select **Neota Logic Studio**.</span></span>

    ![設定單一登入](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

3. <span data-ttu-id="5c675-206">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5c675-206">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="5c675-208">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c675-208">Click **Add** button.</span></span> <span data-ttu-id="5c675-209">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5c675-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="5c675-211">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="5c675-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5c675-212">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c675-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c675-213">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c675-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c675-214">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="5c675-214">Testing single sign-on</span></span>

<span data-ttu-id="5c675-215">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="5c675-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5c675-216">在存取面板中按一下 [Neota Logic Studio] 圖格，系統會將您重新導向組織登入頁面。</span><span class="sxs-lookup"><span data-stu-id="5c675-216">Click the Neota Logic Studio tile in the Access Panel, you will be redirected to Organization sign-on page.</span></span> <span data-ttu-id="5c675-217">成功登入之後，系統會將您登入 Neota Logic Studio 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c675-217">After successful login, you will be signed-on to your Neota Logic Studio application.</span></span> <span data-ttu-id="5c675-218">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="5c675-218">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

<span data-ttu-id="5c675-219">如需存取面板的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="5c675-219">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5c675-220">其他資源</span><span class="sxs-lookup"><span data-stu-id="5c675-220">Additional resources</span></span>

* [<span data-ttu-id="5c675-221">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="5c675-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c675-222">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5c675-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_203.png

