---
title: "教學課程：Azure Active Directory 與 Collaborative Innovation 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Collaborative Innovation 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 5706ba9f4e7c92de77a0edc5146aa150de379c9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="56fa4-103">教學課程：Azure Active Directory 與 Collaborative Innovation 整合</span><span class="sxs-lookup"><span data-stu-id="56fa4-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="56fa4-104">在本教學課程中，您將了解如何整合 Collaborative Innovation 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="56fa4-104">In this tutorial, you learn how to integrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="56fa4-105">Collaborative Innovation 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="56fa4-105">Integrating Collaborative Innovation with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="56fa4-106">您可以在 Azure AD 中控制可存取 Collaborative Innovation 的人員</span><span class="sxs-lookup"><span data-stu-id="56fa4-106">You can control in Azure AD who has access to Collaborative Innovation</span></span>
- <span data-ttu-id="56fa4-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Collaborative Innovation (單一登入)</span><span class="sxs-lookup"><span data-stu-id="56fa4-107">You can enable your users to automatically get signed-on to Collaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="56fa4-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="56fa4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="56fa4-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="56fa4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56fa4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="56fa4-110">Prerequisites</span></span>

<span data-ttu-id="56fa4-111">若要設定 Collaborative Innovation 與 Azure AD 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="56fa4-111">To configure Azure AD integration with Collaborative Innovation, you need the following items:</span></span>

- <span data-ttu-id="56fa4-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="56fa4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="56fa4-113">已啟用 Collaborative Innovation 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="56fa4-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56fa4-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="56fa4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="56fa4-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="56fa4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="56fa4-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="56fa4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="56fa4-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="56fa4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56fa4-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="56fa4-118">Scenario description</span></span>
<span data-ttu-id="56fa4-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="56fa4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="56fa4-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="56fa4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56fa4-121">從資源庫新增 Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="56fa4-121">Adding Collaborative Innovation from the gallery</span></span>
2. <span data-ttu-id="56fa4-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="56fa4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-the-gallery"></a><span data-ttu-id="56fa4-123">從資源庫新增 Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="56fa4-123">Adding Collaborative Innovation from the gallery</span></span>
<span data-ttu-id="56fa4-124">若要設定 Collaborative Innovation 與 Azure AD 整合，您需要從資源庫將 Collaborative Innovation 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="56fa4-124">To configure the integration of Collaborative Innovation into Azure AD, you need to add Collaborative Innovation from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="56fa4-125">**若要從資源庫新增 Collaborative Innovation，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="56fa4-125">**To add Collaborative Innovation from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="56fa4-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="56fa4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="56fa4-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="56fa4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="56fa4-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="56fa4-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="56fa4-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="56fa4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="56fa4-133">在搜尋方塊中，輸入 **Collaborative Innovation**。</span><span class="sxs-lookup"><span data-stu-id="56fa4-133">In the search box, type **Collaborative Innovation**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="56fa4-135">在結果窗格中，選取 [Collaborative Innovation]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="56fa4-135">In the results panel, select **Collaborative Innovation**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="56fa4-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="56fa4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="56fa4-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Collaborative Innovation 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="56fa4-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="56fa4-139">若要讓單一登入運作，Azure AD 必須知道 Collaborative Innovation 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="56fa4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Collaborative Innovation is to a user in Azure AD.</span></span> <span data-ttu-id="56fa4-140">換句話說，必須在 Azure AD 使用者與 Collaborative Innovation 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="56fa4-140">In other words, a link relationship between an Azure AD user and the related user in Collaborative Innovation needs to be established.</span></span>

<span data-ttu-id="56fa4-141">在 Collaborative Innovation 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="56fa4-141">In Collaborative Innovation, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="56fa4-142">若要設定及測試與 Collaborative Innovation 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="56fa4-142">To configure and test Azure AD single sign-on with Collaborative Innovation, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="56fa4-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="56fa4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="56fa4-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="56fa4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56fa4-145">**[建立 Collaborative Innovation 測試使用者](#creating-a-collaborative-innovation-test-user)** - 在 Collaborative Innovation 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="56fa4-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - to have a counterpart of Britta Simon in Collaborative Innovation that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="56fa4-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="56fa4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56fa4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="56fa4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="56fa4-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="56fa4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="56fa4-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Collaborative Innovation 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="56fa4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="56fa4-150">**若要設定與 Collaborative Innovation 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="56fa4-150">**To configure Azure AD single sign-on with Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="56fa4-151">在 Azure 入口網站的 [Collaborative Innovation] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="56fa4-151">In the Azure portal, on the **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="56fa4-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="56fa4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="56fa4-155">在 [Collaborative Innovation 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="56fa4-155">On the **Collaborative Innovation Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="56fa4-157">a.</span><span class="sxs-lookup"><span data-stu-id="56fa4-157">a.</span></span> <span data-ttu-id="56fa4-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="56fa4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="56fa4-159">b.</span><span class="sxs-lookup"><span data-stu-id="56fa4-159">b.</span></span> <span data-ttu-id="56fa4-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="56fa4-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="56fa4-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="56fa4-161">These values are not real.</span></span> <span data-ttu-id="56fa4-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="56fa4-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="56fa4-163">請連絡 [Collaborative Innovation 用戶端支援小組](https://www.unilever.com/contact/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="56fa4-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) to get these values.</span></span>  

4. <span data-ttu-id="56fa4-164">Collaborative Innovation 應用程式需要特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="56fa4-164">Collaborative Innovation application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="56fa4-165">請設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="56fa4-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="56fa4-166">您可以在應用程式整合頁面的 [使用者屬性] 區段中管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="56fa4-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="56fa4-167">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="56fa4-167">The following screenshot shows an example for this.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="56fa4-169">在 [使用者屬性] 區段中，按一下 [檢視及編輯所有其他使用者屬性] 核取方塊，可展開屬性。</span><span class="sxs-lookup"><span data-stu-id="56fa4-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="56fa4-170">在每個顯示的屬性上執行下列步驟-</span><span class="sxs-lookup"><span data-stu-id="56fa4-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="56fa4-171">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="56fa4-171">Attribute Name</span></span> | <span data-ttu-id="56fa4-172">屬性值</span><span class="sxs-lookup"><span data-stu-id="56fa4-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="56fa4-173">givenname</span><span class="sxs-lookup"><span data-stu-id="56fa4-173">givenname</span></span> | <span data-ttu-id="56fa4-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="56fa4-174">user.givenname</span></span> |
    | <span data-ttu-id="56fa4-175">surname</span><span class="sxs-lookup"><span data-stu-id="56fa4-175">surname</span></span> | <span data-ttu-id="56fa4-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="56fa4-176">user.surname</span></span> |
    | <span data-ttu-id="56fa4-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="56fa4-177">emailaddress</span></span> | <span data-ttu-id="56fa4-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="56fa4-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="56fa4-179">名稱</span><span class="sxs-lookup"><span data-stu-id="56fa4-179">name</span></span> | <span data-ttu-id="56fa4-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="56fa4-180">user.userprincipalname</span></span> |

    <span data-ttu-id="56fa4-181">a.</span><span class="sxs-lookup"><span data-stu-id="56fa4-181">a.</span></span> <span data-ttu-id="56fa4-182">按一下該屬性開啟 [編輯屬性] 視窗。</span><span class="sxs-lookup"><span data-stu-id="56fa4-182">Click the attribute to open the **Edit Attribute** window.</span></span>

    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="56fa4-184">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="56fa4-184">b.</span></span> <span data-ttu-id="56fa4-185">刪除 **Namespace** 中的 URL 值。</span><span class="sxs-lookup"><span data-stu-id="56fa4-185">Delete the URL value from the **Namespace**.</span></span>
    
    <span data-ttu-id="56fa4-186">c.</span><span class="sxs-lookup"><span data-stu-id="56fa4-186">c.</span></span> <span data-ttu-id="56fa4-187">按一下 [確定] 儲存設定。</span><span class="sxs-lookup"><span data-stu-id="56fa4-187">Click **Ok** to save the setting.</span></span>

6. <span data-ttu-id="56fa4-188">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="56fa4-188">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="56fa4-190">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="56fa4-190">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="56fa4-192">若要在 **Collaborative Innovation** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [Collaborative Innovation 支援小組](https://www.unilever.com/contact/)。</span><span class="sxs-lookup"><span data-stu-id="56fa4-192">To configure single sign-on on **Collaborative Innovation** side, you need to send the downloaded **Metadata XML** to [Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="56fa4-193">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="56fa4-193">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="56fa4-194">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="56fa4-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="56fa4-195">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="56fa4-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="56fa4-196">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="56fa4-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="56fa4-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="56fa4-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="56fa4-198">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="56fa4-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="56fa4-200">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="56fa4-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="56fa4-201">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="56fa4-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="56fa4-203">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="56fa4-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="56fa4-205">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="56fa4-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="56fa4-207">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="56fa4-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="56fa4-209">a.</span><span class="sxs-lookup"><span data-stu-id="56fa4-209">a.</span></span> <span data-ttu-id="56fa4-210">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="56fa4-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="56fa4-211">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="56fa4-211">b.</span></span> <span data-ttu-id="56fa4-212">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="56fa4-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="56fa4-213">c.</span><span class="sxs-lookup"><span data-stu-id="56fa4-213">c.</span></span> <span data-ttu-id="56fa4-214">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="56fa4-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="56fa4-215">d.</span><span class="sxs-lookup"><span data-stu-id="56fa4-215">d.</span></span> <span data-ttu-id="56fa4-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="56fa4-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="56fa4-217">建立 Collaborative Innovation 測試使用者</span><span class="sxs-lookup"><span data-stu-id="56fa4-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="56fa4-218">若要讓 Azure AD 使用者能夠登入 Collaborative Innovation，必須將它們佈建到 Collaborative Innovation。</span><span class="sxs-lookup"><span data-stu-id="56fa4-218">To enable Azure AD users to log in to Collaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="56fa4-219">在此應用程式佈建是自動的情況下，如應用程式支援即時使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="56fa4-219">In case of this application provisioning is automatic as the application supports just in time user provisioning.</span></span> <span data-ttu-id="56fa4-220">因此不需要在這裡執行任何步驟。</span><span class="sxs-lookup"><span data-stu-id="56fa4-220">So there is no need to perform any steps here.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="56fa4-221">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="56fa4-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="56fa4-222">在本節中，您會將 Collaborative Innovation 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="56fa4-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Collaborative Innovation.</span></span>

![指派使用者][200] 

<span data-ttu-id="56fa4-224">**若要將 Britta Simon 指派給 Collaborative Innovation，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="56fa4-224">**To assign Britta Simon to Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="56fa4-225">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="56fa4-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="56fa4-227">在應用程式清單中，選取 **Collaborative Innovation**。</span><span class="sxs-lookup"><span data-stu-id="56fa4-227">In the applications list, select **Collaborative Innovation**.</span></span>

    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="56fa4-229">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="56fa4-229">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="56fa4-231">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="56fa4-231">Click **Add** button.</span></span> <span data-ttu-id="56fa4-232">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="56fa4-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="56fa4-234">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="56fa4-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="56fa4-235">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="56fa4-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="56fa4-236">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="56fa4-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="56fa4-237">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="56fa4-237">Testing single sign-on</span></span>

<span data-ttu-id="56fa4-238">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="56fa4-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="56fa4-239">當您按一下 [存取面板] 中的 [Collaborative Innovation] 圖格時，應該會取得 Collaborative Innovation 應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="56fa4-239">When you click the Collaborative Innovation tile in the Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="56fa4-240">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="56fa4-240">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="56fa4-241">其他資源</span><span class="sxs-lookup"><span data-stu-id="56fa4-241">Additional resources</span></span>

* [<span data-ttu-id="56fa4-242">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="56fa4-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56fa4-243">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="56fa4-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png

