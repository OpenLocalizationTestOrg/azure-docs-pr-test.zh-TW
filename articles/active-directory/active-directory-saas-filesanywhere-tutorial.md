---
title: "教學課程：Azure Active Directory 與 FilesAnywhere 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 FilesAnywhere 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 4153056bd21006061c6ad8ff9cf3c17de9248628
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="5b313-103">教學課程：Azure Active Directory 與 FilesAnywhere 整合</span><span class="sxs-lookup"><span data-stu-id="5b313-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="5b313-104">在本教學課程中，您會了解如何整合 FilesAnywhere 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="5b313-104">In this tutorial, you learn how to integrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b313-105">FilesAnywhere 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="5b313-105">Integrating FilesAnywhere with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5b313-106">您可以在 Azure AD 中控制可存取 FilesAnywhere 的人員</span><span class="sxs-lookup"><span data-stu-id="5b313-106">You can control in Azure AD who has access to FilesAnywhere</span></span>
- <span data-ttu-id="5b313-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 FilesAnywhere (單一登入)</span><span class="sxs-lookup"><span data-stu-id="5b313-107">You can enable your users to automatically get signed-on to FilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b313-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="5b313-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="5b313-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5b313-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b313-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5b313-110">Prerequisites</span></span>

<span data-ttu-id="5b313-111">若要設定 Azure AD 與 FilesAnywhere 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="5b313-111">To configure Azure AD integration with FilesAnywhere, you need the following items:</span></span>

- <span data-ttu-id="5b313-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5b313-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b313-113">啟用 FilesAnywhere 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5b313-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="5b313-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5b313-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="5b313-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5b313-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b313-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="5b313-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="5b313-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="5b313-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="5b313-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="5b313-118">Scenario description</span></span>
<span data-ttu-id="5b313-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b313-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b313-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="5b313-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b313-121">從資源庫新增 FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="5b313-121">Adding FilesAnywhere from the gallery</span></span>
2. <span data-ttu-id="5b313-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5b313-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-the-gallery"></a><span data-ttu-id="5b313-123">從資源庫新增 FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="5b313-123">Adding FilesAnywhere from the gallery</span></span>
<span data-ttu-id="5b313-124">若要設定 FilesAnywhere 與 Azure AD 整合，您需要從資源庫將 FilesAnywhere 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="5b313-124">To configure the integration of FilesAnywhere into Azure AD, you need to add FilesAnywhere from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5b313-125">**若要從資源庫新增 FilesAnywhere，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5b313-125">**To add FilesAnywhere from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5b313-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5b313-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5b313-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5b313-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5b313-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5b313-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="5b313-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b313-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="5b313-133">在搜尋方塊中，輸入 **FilesAnywhere**。</span><span class="sxs-lookup"><span data-stu-id="5b313-133">In the search box, type **FilesAnywhere**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="5b313-135">在結果窗格中，選取 [FilesAnywhere]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b313-135">In the results panel, select **FilesAnywhere**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b313-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5b313-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b313-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 FilesAnywhere 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b313-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b313-139">若要讓單一登入運作，Azure AD 必須知道 FilesAnywhere 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="5b313-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FilesAnywhere is to a user in Azure AD.</span></span> <span data-ttu-id="5b313-140">換句話說，必須在 Azure AD 使用者和 FilesAnywhere 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5b313-140">In other words, a link relationship between an Azure AD user and the related user in FilesAnywhere needs to be established.</span></span>

<span data-ttu-id="5b313-141">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 FilesAnywhere 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="5b313-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="5b313-142">若要設定並測試與 FilesAnywhere 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="5b313-142">To configure and test Azure AD single sign-on with FilesAnywhere, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5b313-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="5b313-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5b313-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b313-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b313-145">**[建立 FilesAnywhere 測試使用者](#creating-a-filesanywhere-test-user)** - 在 FilesAnywhere 中，建立一個與 Azure AD 中代表 Britta Simon 的項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="5b313-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - to have a counterpart of Britta Simon in FilesAnywhere that is linked to the Azure AD representation of her.</span></span>
3. <span data-ttu-id="5b313-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b313-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
4. <span data-ttu-id="5b313-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="5b313-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b313-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5b313-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b313-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 FilesAnywhere 中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b313-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="5b313-150">**若要設定與 FilesAnywhere 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5b313-150">**To configure Azure AD single sign-on with FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="5b313-151">在 Azure 管理入口網站的 [FilesAnywhere] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="5b313-151">In the Azure Management portal, on the **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="5b313-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b313-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="5b313-155">如果您想要以 **IDP 起始模式**設定應用程式，請在 [FilesAnywhere 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5b313-155">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="5b313-157">a.</span><span class="sxs-lookup"><span data-stu-id="5b313-157">a.</span></span> <span data-ttu-id="5b313-158">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="5b313-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="5b313-159">請注意，**clientid** 的值 **215** 只是範例。</span><span class="sxs-lookup"><span data-stu-id="5b313-159">Please note that the value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="5b313-160">您必須以實際的 clientid 值加以取代。</span><span class="sxs-lookup"><span data-stu-id="5b313-160">You need to replace it with the actual clientid value.</span></span>

4. <span data-ttu-id="5b313-161">在 [FilesAnywhere 網域和 URL] 區段中，如果您想要在 [SP 起始模式] 中設定應用程式，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5b313-161">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="5b313-163">a.</span><span class="sxs-lookup"><span data-stu-id="5b313-163">a.</span></span> <span data-ttu-id="5b313-164">按一下 [顯示進階 URL 設定] 選項</span><span class="sxs-lookup"><span data-stu-id="5b313-164">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="5b313-165">b.</span><span class="sxs-lookup"><span data-stu-id="5b313-165">b.</span></span> <span data-ttu-id="5b313-166">在 [登入 URL] 文字方塊中，以下列模式輸入 URL：`https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="5b313-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5b313-167">請注意這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="5b313-167">Please note that these are not the real values.</span></span> <span data-ttu-id="5b313-168">您必須使用實際的「登入 URL」及「回覆 URL」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="5b313-168">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="5b313-169">請連絡 [FilesAnywhere 支援小組](mailto:support@FilesAnywhere.com) 以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="5b313-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) to get these values.</span></span> 

5. <span data-ttu-id="5b313-170">FilesAnywhere Software 應用程式會預期要有特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="5b313-170">FilesAnywhere Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="5b313-171">請設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="5b313-171">Please configure the following claims for this application.</span></span> <span data-ttu-id="5b313-172">您可以在應用程式整合頁面的 [使用者屬性] 區段中管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="5b313-172">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="5b313-173">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="5b313-173">The following screenshot shows an example for this.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="5b313-175">當使用者註冊 FilesAnywhere 時，他們會取得來自 [FilesAnywhere 小組](mailto:support@FilesAnywhere.com)的 **clientid** 屬性值。</span><span class="sxs-lookup"><span data-stu-id="5b313-175">When the users signs up with FilesAnywhere they get the value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="5b313-176">您必須使用 FilesAnywhere 提供的唯一值，新增 [用戶端 ID] 屬性。</span><span class="sxs-lookup"><span data-stu-id="5b313-176">You have to add the "Client Id" attribute with the unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="5b313-177">上述的所有屬性都是必要屬性。</span><span class="sxs-lookup"><span data-stu-id="5b313-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="5b313-178">請注意，**clientid** 的值 **2331**只是範例。</span><span class="sxs-lookup"><span data-stu-id="5b313-178">Please note that the value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="5b313-179">您必須提供實際值。</span><span class="sxs-lookup"><span data-stu-id="5b313-179">You need to provide the actual value.</span></span>


6. <span data-ttu-id="5b313-180">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如上圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5b313-180">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="5b313-181">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="5b313-181">Attribute Name</span></span> | <span data-ttu-id="5b313-182">屬性值</span><span class="sxs-lookup"><span data-stu-id="5b313-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="5b313-183">clientid</span><span class="sxs-lookup"><span data-stu-id="5b313-183">clientid</span></span> | <span data-ttu-id="5b313-184">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="5b313-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="5b313-185">a.</span><span class="sxs-lookup"><span data-stu-id="5b313-185">a.</span></span> <span data-ttu-id="5b313-186">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5b313-186">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="5b313-189">b.</span><span class="sxs-lookup"><span data-stu-id="5b313-189">b.</span></span> <span data-ttu-id="5b313-190">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="5b313-190">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="5b313-191">c.</span><span class="sxs-lookup"><span data-stu-id="5b313-191">c.</span></span> <span data-ttu-id="5b313-192">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="5b313-192">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5b313-193">d.</span><span class="sxs-lookup"><span data-stu-id="5b313-193">d.</span></span> <span data-ttu-id="5b313-194">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5b313-194">Click **Ok**</span></span>

7. <span data-ttu-id="5b313-195">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b313-195">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5b313-197">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="5b313-197">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="5b313-199">在 [FilesAnywhere 組態] 區段上，按一下 [設定 FilesAnywhere] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="5b313-199">On the **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** to open **Configure sign-on** window.</span></span>

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="5b313-202">若要在 FilesAnywhere 結尾為您的應用程式完成 SSO 組態，請連絡 [FilesAnywhere 支援小組](mailto:support@FilesAnywhere.com)，並且提供已下載的 SAML 權杖簽署憑證和單一登入 (SSO) URL。</span><span class="sxs-lookup"><span data-stu-id="5b313-202">To get SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them the downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b313-203">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5b313-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b313-204">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5b313-204">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="5b313-206">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5b313-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5b313-207">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5b313-207">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b313-209">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="5b313-209">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b313-211">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5b313-211">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b313-213">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5b313-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b313-215">a.</span><span class="sxs-lookup"><span data-stu-id="5b313-215">a.</span></span> <span data-ttu-id="5b313-216">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="5b313-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b313-217">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b313-217">b.</span></span> <span data-ttu-id="5b313-218">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="5b313-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b313-219">c.</span><span class="sxs-lookup"><span data-stu-id="5b313-219">c.</span></span> <span data-ttu-id="5b313-220">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="5b313-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5b313-221">d.</span><span class="sxs-lookup"><span data-stu-id="5b313-221">d.</span></span> <span data-ttu-id="5b313-222">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5b313-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="5b313-223">建立 FilesAnywhere 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5b313-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="5b313-224">應用程式僅在使用者佈建時支援，驗證之後，會在應用程式中自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="5b313-224">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5b313-225">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5b313-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5b313-226">在本節中，您會將 FilesAnywhere 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b313-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FilesAnywhere.</span></span>

![指派使用者][200] 

<span data-ttu-id="5b313-228">**若要將 Britta Simon 指派到 FilesAnywhere，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5b313-228">**To assign Britta Simon to FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="5b313-229">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5b313-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="5b313-231">在應用程式清單中，選取 [FilesAnywhere] 。</span><span class="sxs-lookup"><span data-stu-id="5b313-231">In the applications list, select **FilesAnywhere**.</span></span>

    ![設定單一登入](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="5b313-233">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5b313-233">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="5b313-235">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b313-235">Click **Add** button.</span></span> <span data-ttu-id="5b313-236">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5b313-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="5b313-238">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="5b313-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5b313-239">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b313-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b313-240">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b313-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="5b313-241">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="5b313-241">Testing single sign-on</span></span>

<span data-ttu-id="5b313-242">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="5b313-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5b313-243">當您在存取面板中按一下 [FilesAnywhere] 圖格時，應該會自動登入您的 FilesAnywhere 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b313-243">When you click the FilesAnywhere tile in the Access Panel, you should get automatically signed-on to your FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5b313-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="5b313-244">Additional resources</span></span>

* [<span data-ttu-id="5b313-245">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="5b313-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b313-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5b313-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
