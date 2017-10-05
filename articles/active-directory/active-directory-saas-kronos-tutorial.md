---
title: "教學課程：Azure Active Directory 與 Kronos 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Kronos 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: eb61ec0a7d3e992a285b1af3d4a7fbe1feb8d991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="b3b6a-103">教學課程：Azure Active Directory 與 Kronos 整合</span><span class="sxs-lookup"><span data-stu-id="b3b6a-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="b3b6a-104">在本教學課程中，您將了解如何整合 Kronos 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-104">In this tutorial, you learn how to integrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b3b6a-105">將 Kronos 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="b3b6a-105">Integrating Kronos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b3b6a-106">您可以在 Azure AD 中管控可存取 Kronos 的人員</span><span class="sxs-lookup"><span data-stu-id="b3b6a-106">You can control in Azure AD who has access to Kronos</span></span>
- <span data-ttu-id="b3b6a-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Kronos (單一登入)</span><span class="sxs-lookup"><span data-stu-id="b3b6a-107">You can enable your users to automatically get signed-on to Kronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b3b6a-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="b3b6a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b3b6a-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3b6a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b3b6a-110">Prerequisites</span></span>

<span data-ttu-id="b3b6a-111">若要設定 Azure AD 與 Kronos 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="b3b6a-111">To configure Azure AD integration with Kronos, you need the following items:</span></span>

- <span data-ttu-id="b3b6a-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b3b6a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b3b6a-113">已啟用 **Kronos Workforce Central** SSO 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b3b6a-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b3b6a-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b3b6a-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b3b6a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b3b6a-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b3b6a-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b3b6a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b3b6a-118">Scenario description</span></span>
<span data-ttu-id="b3b6a-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b3b6a-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="b3b6a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b3b6a-121">從資源庫新增 Kronos</span><span class="sxs-lookup"><span data-stu-id="b3b6a-121">Adding Kronos from the gallery</span></span>
2. <span data-ttu-id="b3b6a-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b3b6a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-the-gallery"></a><span data-ttu-id="b3b6a-123">從資源庫新增 Kronos</span><span class="sxs-lookup"><span data-stu-id="b3b6a-123">Adding Kronos from the gallery</span></span>
<span data-ttu-id="b3b6a-124">若要設定將 Kronos 整合到 Azure AD 中，您需要從資源庫將 Kronos 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-124">To configure the integration of Kronos into Azure AD, you need to add Kronos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b3b6a-125">**若要從資源庫新增 Kronos，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b3b6a-125">**To add Kronos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b3b6a-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b3b6a-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b3b6a-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="b3b6a-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="b3b6a-133">在搜尋方塊中，輸入 **Kronos**。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-133">In the search box, type **Kronos**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="b3b6a-135">在結果窗格中，選取 [Kronos]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-135">In the results panel, select **Kronos**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b3b6a-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b3b6a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b3b6a-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Kronos 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b3b6a-139">若要讓單一登入能夠運作，Azure AD 必須知道 Kronos 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kronos is to a user in Azure AD.</span></span> <span data-ttu-id="b3b6a-140">換句話說，必須在 Azure AD 使用者與 Kronos 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-140">In other words, a link relationship between an Azure AD user and the related user in Kronos needs to be established.</span></span>

<span data-ttu-id="b3b6a-141">在 Kronos 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-141">In Kronos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b3b6a-142">若要設定及測試與 Kronos 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="b3b6a-142">To configure and test Azure AD single sign-on with Kronos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b3b6a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b3b6a-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b3b6a-145">**[建立 Kronos 測試使用者](#creating-a-kronos-test-user)** - 使 Kronos 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - to have a counterpart of Britta Simon in Kronos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b3b6a-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b3b6a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b3b6a-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b3b6a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b3b6a-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Kronos 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="b3b6a-150">**若要設定與 Kronos 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b3b6a-150">**To configure Azure AD single sign-on with Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="b3b6a-151">在 Azure 入口網站的 [Kronos] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-151">In the Azure portal, on the **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="b3b6a-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="b3b6a-155">在 [Kronos 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b3b6a-155">On the **Kronos Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="b3b6a-157">a.</span><span class="sxs-lookup"><span data-stu-id="b3b6a-157">a.</span></span> <span data-ttu-id="b3b6a-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="b3b6a-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="b3b6a-159">b.</span><span class="sxs-lookup"><span data-stu-id="b3b6a-159">b.</span></span> <span data-ttu-id="b3b6a-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="b3b6a-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b3b6a-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-161">These values are not real.</span></span> <span data-ttu-id="b3b6a-162">請使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="b3b6a-163">請連絡 [Kronos 支援小組](https://www.kronos.in/contact/en-in/form) 以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) to get these values.</span></span>
 
4. <span data-ttu-id="b3b6a-164">您的 Kronos 應用程式會預期要有特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-164">Your Kronos application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="b3b6a-165">請先與 [Kronos 支援小組](https://www.kronos.in/contact/en-in/form)合作，識別出將對應到應用程式中的正確使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first to identify the correct user identifier, which is mapped into the application.</span></span> <span data-ttu-id="b3b6a-166">另外，關於小組要用於此對應的屬性方面，也請接受指引。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-166">Also please take the guidance about the attribute, which they want to use for this mapping.</span></span>
 
     <span data-ttu-id="b3b6a-167">Microsoft 建議使用 **"NameIdentifier"** 屬性做為使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-167">Microsoft recommends using the **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="b3b6a-168">您可以在應用程式整合頁面的 [使用者屬性] 區段中管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-168">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="b3b6a-169">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="b3b6a-170">我們已將 **使用者識別碼 (nameid)** 對應至 **user.userprincipalname** 的 **ExtractMailPrefix()** 函數。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-170">Here we have mapped the **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="b3b6a-171">如此一來，使用者電子郵件的首碼值便會是唯一的使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-171">This gives the prefix value of email of the user which is the unique User ID.</span></span> <span data-ttu-id="b3b6a-172">在每次成功的回應中，都會傳送至 Kronos 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-172">This is sent to the Kronos application in every successful response.</span></span> 
     
    ![設定單一登入](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="b3b6a-174">在 [單一登入] 對話方塊的 [使用者屬性] 區段中：</span><span class="sxs-lookup"><span data-stu-id="b3b6a-174">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="b3b6a-175">a.</span><span class="sxs-lookup"><span data-stu-id="b3b6a-175">a.</span></span> <span data-ttu-id="b3b6a-176">在 [使用者識別碼] 下拉式清單中，選取 [ExtractMailPrefix]。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-176">In the User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="b3b6a-177">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-177">b.</span></span> <span data-ttu-id="b3b6a-178">在 [郵件] 下拉式清單中，選取 [user.userprincipalname]。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-178">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="b3b6a-179">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="b3b6a-181">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-181">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b3b6a-183">若要在 **Kronos** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [Kronos 支援小組](https://www.kronos.in/contact/en-in/form)。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-183">To configure single sign-on on **Kronos** side, you need to send the downloaded **Metadata XML** to [Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="b3b6a-184">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="b3b6a-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b3b6a-185">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b3b6a-186">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b3b6a-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b3b6a-187">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b3b6a-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="b3b6a-188">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="b3b6a-190">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b3b6a-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b3b6a-191">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b3b6a-193">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b3b6a-195">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b3b6a-197">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b3b6a-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b3b6a-199">a.</span><span class="sxs-lookup"><span data-stu-id="b3b6a-199">a.</span></span> <span data-ttu-id="b3b6a-200">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b3b6a-201">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-201">b.</span></span> <span data-ttu-id="b3b6a-202">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b3b6a-203">c.</span><span class="sxs-lookup"><span data-stu-id="b3b6a-203">c.</span></span> <span data-ttu-id="b3b6a-204">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b3b6a-205">d.</span><span class="sxs-lookup"><span data-stu-id="b3b6a-205">d.</span></span> <span data-ttu-id="b3b6a-206">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="b3b6a-207">建立 Kronos 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b3b6a-207">Creating a Kronos test user</span></span>

<span data-ttu-id="b3b6a-208">在本節中，您會在 Kronos 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="b3b6a-209">Kronos 應用程式必須先在應用程式中佈建所有使用者，才能執行 SSO。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-209">Kronos application needs all the users to be provisioned in the application before doing SSO.</span></span> 

<span data-ttu-id="b3b6a-210">請與 [Kronos 支援小組](https://www.kronos.in/contact/en-in/form)合作，將所有這些使用者佈建到應用程式中。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-210">Work with the [Kronos support team](https://www.kronos.in/contact/en-in/form) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b3b6a-211">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b3b6a-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b3b6a-212">在本節中，您會把 Kronos 的存取權授與 Britta Simo，讓 Britta Simon 能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kronos.</span></span>

![指派使用者][200] 

<span data-ttu-id="b3b6a-214">**若要將 Britta Simon 指派給 Kronos，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b3b6a-214">**To assign Britta Simon to Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="b3b6a-215">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b3b6a-217">在應用程式清單中，選取 [Kronos] 。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-217">In the applications list, select **Kronos**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="b3b6a-219">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-219">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="b3b6a-221">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-221">Click **Add** button.</span></span> <span data-ttu-id="b3b6a-222">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="b3b6a-224">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b3b6a-225">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b3b6a-226">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b3b6a-227">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b3b6a-227">Testing single sign-on</span></span>

<span data-ttu-id="b3b6a-228">在本節中，您會使用存取面板來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-228">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="b3b6a-229">當您在「存取面板」中按一下 [Kronos] 磚時，應該會自動登入您的 Kronos 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3b6a-229">When you click the Kronos tile in the Access Panel, you should get automatically signed-on to your Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b3b6a-230">其他資源</span><span class="sxs-lookup"><span data-stu-id="b3b6a-230">Additional resources</span></span>

* [<span data-ttu-id="b3b6a-231">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="b3b6a-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b3b6a-232">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b3b6a-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png

