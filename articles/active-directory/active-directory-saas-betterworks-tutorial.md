---
title: "教學課程：Azure Active Directory 與 BetterWorks 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 BetterWorks 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: d6a5b167c0befbd0fe2c65bdd16abc35ed0a659c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="167c5-103">教學課程：Azure Active Directory 與 BetterWorks 整合</span><span class="sxs-lookup"><span data-stu-id="167c5-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="167c5-104">在本教學課程中，您會了解如何將 BetterWorks 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="167c5-104">In this tutorial, you learn how to integrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="167c5-105">將 BetterWorks 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="167c5-105">Integrating BetterWorks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="167c5-106">您可以在 Azure AD 中控制可存取 BetterWorks 的人員</span><span class="sxs-lookup"><span data-stu-id="167c5-106">You can control in Azure AD who has access to BetterWorks</span></span>
- <span data-ttu-id="167c5-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 BetterWorks (單一登入)</span><span class="sxs-lookup"><span data-stu-id="167c5-107">You can enable your users to automatically get signed-on to BetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="167c5-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="167c5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="167c5-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="167c5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="167c5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="167c5-110">Prerequisites</span></span>

<span data-ttu-id="167c5-111">若要設定 Azure AD 與 BetterWorks 的整合作業，需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="167c5-111">To configure Azure AD integration with BetterWorks, you need the following items:</span></span>

- <span data-ttu-id="167c5-112">一個 Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="167c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="167c5-113">已啟用 BetterWorks 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="167c5-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="167c5-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="167c5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="167c5-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="167c5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="167c5-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="167c5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="167c5-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="167c5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="167c5-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="167c5-118">Scenario description</span></span>
<span data-ttu-id="167c5-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="167c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="167c5-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="167c5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="167c5-121">從資源庫新增 BetterWorks</span><span class="sxs-lookup"><span data-stu-id="167c5-121">Adding BetterWorks from the gallery</span></span>
2. <span data-ttu-id="167c5-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="167c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-the-gallery"></a><span data-ttu-id="167c5-123">從資源庫新增 BetterWorks</span><span class="sxs-lookup"><span data-stu-id="167c5-123">Adding BetterWorks from the gallery</span></span>
<span data-ttu-id="167c5-124">若要設定將 BetterWorks 整合到 Azure AD 中，您需要從資源庫將 BetterWorks 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="167c5-124">To configure the integration of BetterWorks into Azure AD, you need to add BetterWorks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="167c5-125">**若要從資源庫加入 BetterWorks，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="167c5-125">**To add BetterWorks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="167c5-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="167c5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="167c5-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="167c5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="167c5-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="167c5-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="167c5-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="167c5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="167c5-133">在搜尋方塊中，輸入 **BetterWorks**。</span><span class="sxs-lookup"><span data-stu-id="167c5-133">In the search box, type **BetterWorks**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="167c5-135">在結果面板中，選取 [BetterWorks]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="167c5-135">In the results panel, select **BetterWorks**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="167c5-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="167c5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="167c5-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 BetterWorks 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="167c5-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="167c5-139">若要讓單一登入能夠運作，Azure AD 必須知道 BetterWorks 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="167c5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BetterWorks is to a user in Azure AD.</span></span> <span data-ttu-id="167c5-140">換句話說，必須在 Azure AD 使用者和 BetterWorks 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="167c5-140">In other words, a link relationship between an Azure AD user and the related user in BetterWorks needs to be established.</span></span>

<span data-ttu-id="167c5-141">在 BetterWorks 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="167c5-141">In BetterWorks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="167c5-142">若要使用 BetterWorks 設定及測試 Azure AD 單一登入功能，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="167c5-142">To configure and test Azure AD single sign-on with BetterWorks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="167c5-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="167c5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="167c5-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="167c5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="167c5-145">**[建立 BetterWorks 測試使用者](#creating-a-betterworks-test-user)** - 在 BetterWorks 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="167c5-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - to have a counterpart of Britta Simon in BetterWorks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="167c5-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="167c5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="167c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="167c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="167c5-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="167c5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="167c5-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 BetterWorks 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="167c5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="167c5-150">**若要設定與 BetterWorks 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="167c5-150">**To configure Azure AD single sign-on with BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="167c5-151">在 Azure 入口網站的 [BetterWorks] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="167c5-151">In the Azure portal, on the **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="167c5-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="167c5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="167c5-155">如果您想要以「IDP 起始模式」設定應用程式，請在 [BetterWorks 網域及 URL] 區段上：</span><span class="sxs-lookup"><span data-stu-id="167c5-155">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="167c5-157">a.</span><span class="sxs-lookup"><span data-stu-id="167c5-157">a.</span></span> <span data-ttu-id="167c5-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="167c5-158">In the **Identifier** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="167c5-159">b.</span><span class="sxs-lookup"><span data-stu-id="167c5-159">b.</span></span> <span data-ttu-id="167c5-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="167c5-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="167c5-161">如果您想要在以「SP 起始模式」設定應用程式，請在 [BetterWorks 網域及 URL] 區段中執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="167c5-161">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="167c5-163">a.</span><span class="sxs-lookup"><span data-stu-id="167c5-163">a.</span></span> <span data-ttu-id="167c5-164">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="167c5-164">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="167c5-165">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="167c5-165">b.</span></span> <span data-ttu-id="167c5-166">在 [登入 URL] 文字方塊中，以下列模式輸入 URL：`https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="167c5-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="167c5-167">這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="167c5-167">These are not real values.</span></span> <span data-ttu-id="167c5-168">請使用「回覆 URL」、「識別碼」及實際的「登入 URL」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="167c5-168">Update these values with the Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="167c5-169">請連絡 [BetterWorks 支援小組](mailto:support@betterworks.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="167c5-169">Contact [BetterWorks support team](mailto:support@betterworks.com) to get these values.</span></span>
 
4. <span data-ttu-id="167c5-170">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="167c5-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="167c5-172">BetterWorks 應用程式會預期要有特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="167c5-172">BetterWorks application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="167c5-173">設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="167c5-173">Configure the following claims for this application.</span></span> <span data-ttu-id="167c5-174">您可以從應用程式的 [屬性] 索引標籤管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="167c5-174">You can manage the values of these attributes from the "**Attribute**" tab of the application.</span></span> <span data-ttu-id="167c5-175">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="167c5-175">The following screenshot shows an example for this.</span></span> 

    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="167c5-177">在 [SAML Token 屬性]  對話方塊上，針對下表中顯示的每一列執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="167c5-177">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
   | <span data-ttu-id="167c5-178">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="167c5-178">Attribute Name</span></span> | <span data-ttu-id="167c5-179">屬性值</span><span class="sxs-lookup"><span data-stu-id="167c5-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="167c5-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="167c5-180">saml_token</span></span>     | <span data-ttu-id="167c5-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="167c5-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="167c5-182">a.</span><span class="sxs-lookup"><span data-stu-id="167c5-182">a.</span></span> <span data-ttu-id="167c5-183">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="167c5-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="167c5-186">b.</span><span class="sxs-lookup"><span data-stu-id="167c5-186">b.</span></span> <span data-ttu-id="167c5-187">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="167c5-187">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

   <span data-ttu-id="167c5-188">c.</span><span class="sxs-lookup"><span data-stu-id="167c5-188">c.</span></span> <span data-ttu-id="167c5-189">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="167c5-189">From the **Value** list, type the attribute value shown for that row.</span></span>
    
   <span data-ttu-id="167c5-190">d.</span><span class="sxs-lookup"><span data-stu-id="167c5-190">d.</span></span> <span data-ttu-id="167c5-191">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="167c5-191">Click **Ok**.</span></span>

7. <span data-ttu-id="167c5-192">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="167c5-192">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="167c5-194">若要在 **BetterWorks** 端設定單一登入，您必須將已下載的「中繼資料 XML」傳送給 [BetterWorks 支援小組](mailto:support@betterworks.com)。</span><span class="sxs-lookup"><span data-stu-id="167c5-194">To configure single sign-on on **BetterWorks** side, you need to send the downloaded **Metadata XML** to [BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="167c5-195">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="167c5-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="167c5-196">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="167c5-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="167c5-197">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="167c5-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="167c5-198">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="167c5-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="167c5-199">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="167c5-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="167c5-201">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="167c5-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="167c5-202">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="167c5-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="167c5-204">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="167c5-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="167c5-206">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="167c5-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="167c5-208">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="167c5-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="167c5-210">a.</span><span class="sxs-lookup"><span data-stu-id="167c5-210">a.</span></span> <span data-ttu-id="167c5-211">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="167c5-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="167c5-212">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="167c5-212">b.</span></span> <span data-ttu-id="167c5-213">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="167c5-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="167c5-214">c.</span><span class="sxs-lookup"><span data-stu-id="167c5-214">c.</span></span> <span data-ttu-id="167c5-215">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="167c5-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="167c5-216">d.</span><span class="sxs-lookup"><span data-stu-id="167c5-216">d.</span></span> <span data-ttu-id="167c5-217">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="167c5-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="167c5-218">建立 BetterWorks 測試使用者</span><span class="sxs-lookup"><span data-stu-id="167c5-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="167c5-219">在本節中，您會在 BetterWorks 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="167c5-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="167c5-220">請與 [BetterWorks 支援小組](mailto:support@betterworks.com)合作，在 BetterWorks 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="167c5-220">Work with [BetterWorks support team](mailto:support@betterworks.com) to add the users in the BetterWorks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="167c5-221">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="167c5-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="167c5-222">在本節中，您會將 BetterWorks 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="167c5-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BetterWorks.</span></span>

![指派使用者][200] 

<span data-ttu-id="167c5-224">**若要將 Britta Simon 指派給 BetterWorks，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="167c5-224">**To assign Britta Simon to BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="167c5-225">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="167c5-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="167c5-227">在應用程式清單中，選取 [BetterWorks]。</span><span class="sxs-lookup"><span data-stu-id="167c5-227">In the applications list, select **BetterWorks**.</span></span>

    ![設定單一登入](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="167c5-229">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="167c5-229">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="167c5-231">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="167c5-231">Click **Add** button.</span></span> <span data-ttu-id="167c5-232">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="167c5-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="167c5-234">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="167c5-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="167c5-235">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="167c5-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="167c5-236">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="167c5-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="167c5-237">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="167c5-237">Testing single sign-on</span></span>

<span data-ttu-id="167c5-238">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="167c5-238">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="167c5-239">當您在「存取面板」中按一下 BetterWorks 磚時，應該會自動登入 BetterWorks 應用程式。</span><span class="sxs-lookup"><span data-stu-id="167c5-239">When you click the BetterWorks tile in the Access Panel, you should get automatically signed-on to your BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="167c5-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="167c5-240">Additional resources</span></span>

* [<span data-ttu-id="167c5-241">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="167c5-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="167c5-242">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="167c5-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

