---
title: "教學課程：Azure Active Directory 與 OfficeSpace Software 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 OfficeSpace Software 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 43d2ecfe851d8f6c43cd4ce7fc4bd872818f4137
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="20fdc-103">教學課程：Azure Active Directory 與 OfficeSpace Software 整合</span><span class="sxs-lookup"><span data-stu-id="20fdc-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="20fdc-104">在本教學課程中，您將了解如何整合 OfficeSpace Software 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="20fdc-104">In this tutorial, you learn how to integrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="20fdc-105">OfficeSpace Software 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="20fdc-105">Integrating OfficeSpace Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="20fdc-106">您可以在 Azure AD 中控制可存取 OfficeSpace Software 的人員。</span><span class="sxs-lookup"><span data-stu-id="20fdc-106">You can control in Azure AD who has access to OfficeSpace Software.</span></span>
- <span data-ttu-id="20fdc-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 OfficeSpace Software (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="20fdc-107">You can enable your users to automatically get signed-on to OfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="20fdc-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="20fdc-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="20fdc-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="20fdc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20fdc-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="20fdc-110">Prerequisites</span></span>

<span data-ttu-id="20fdc-111">若要設定 Azure AD 與 OfficeSpace Software 整合，您需要以下項目：</span><span class="sxs-lookup"><span data-stu-id="20fdc-111">To configure Azure AD integration with OfficeSpace Software, you need the following items:</span></span>

- <span data-ttu-id="20fdc-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="20fdc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="20fdc-113">已啟用 OfficeSpace Software 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="20fdc-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="20fdc-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="20fdc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="20fdc-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="20fdc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="20fdc-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="20fdc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="20fdc-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="20fdc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="20fdc-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="20fdc-118">Scenario description</span></span>
<span data-ttu-id="20fdc-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="20fdc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="20fdc-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="20fdc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="20fdc-121">從資源庫加入 OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="20fdc-121">Adding OfficeSpace Software from the gallery</span></span>
2. <span data-ttu-id="20fdc-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="20fdc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-the-gallery"></a><span data-ttu-id="20fdc-123">從資源庫加入 OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="20fdc-123">Adding OfficeSpace Software from the gallery</span></span>
<span data-ttu-id="20fdc-124">若要設定 OfficeSpace Software 與 Azure AD 整合，您需要從資源庫將 OfficeSpace Software 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="20fdc-124">To configure the integration of OfficeSpace Software into Azure AD, you need to add OfficeSpace Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="20fdc-125">**若要從資源庫新增 OfficeSpace Software，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="20fdc-125">**To add OfficeSpace Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="20fdc-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="20fdc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="20fdc-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="20fdc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="20fdc-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="20fdc-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="20fdc-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="20fdc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="20fdc-133">在搜尋方塊中，輸入 **OfficeSpace Software**，從結果面板中選取 [OfficeSpace Software]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="20fdc-133">In the search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="20fdc-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="20fdc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="20fdc-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 OfficeSpace Software 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="20fdc-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="20fdc-137">若要讓單一登入運作，Azure AD 必須知道 OfficeSpace Software 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="20fdc-137">For single sign-on to work, Azure AD needs to know what the counterpart user in OfficeSpace Software is to a user in Azure AD.</span></span> <span data-ttu-id="20fdc-138">換句話說，Azure AD 使用者和 OfficeSpace Software 中的相關使用者之間必須建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="20fdc-138">In other words, a link relationship between an Azure AD user and the related user in OfficeSpace Software needs to be established.</span></span>

<span data-ttu-id="20fdc-139">在 OfficeSpace Software 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="20fdc-139">In OfficeSpace Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="20fdc-140">若要使用 OfficeSpace Software 設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="20fdc-140">To configure and test Azure AD single sign-on with OfficeSpace Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="20fdc-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="20fdc-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="20fdc-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="20fdc-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="20fdc-143">**[建立 OfficeSpace Software 測試使用者](#create-a-officespace-software-test-user)** - 使 OfficeSpace Software 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="20fdc-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - to have a counterpart of Britta Simon in OfficeSpace Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="20fdc-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="20fdc-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="20fdc-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="20fdc-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="20fdc-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="20fdc-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="20fdc-147">在本節中，您會於 Azure 入口網站啟用 Azure AD 單一登入，然後在您的 OfficeSpace Software 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="20fdc-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="20fdc-148">**若要使用 OfficeSpace Software 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="20fdc-148">**To configure Azure AD single sign-on with OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="20fdc-149">在 Azure 入口網站的 [OfficeSpace Software] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="20fdc-149">In the Azure portal, on the **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="20fdc-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="20fdc-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="20fdc-153">在 [OfficeSpace Software 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="20fdc-153">On the **OfficeSpace Software Domain and URLs** section, perform the following steps:</span></span>

    ![OfficeSpace Software 網域與 URL 單一登入資訊](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="20fdc-155">a.</span><span class="sxs-lookup"><span data-stu-id="20fdc-155">a.</span></span> <span data-ttu-id="20fdc-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="20fdc-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="20fdc-157">b.</span><span class="sxs-lookup"><span data-stu-id="20fdc-157">b.</span></span> <span data-ttu-id="20fdc-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="20fdc-158">In the **Identifier** textbox, type a URL using the following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="20fdc-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="20fdc-159">These values are not real.</span></span> <span data-ttu-id="20fdc-160">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="20fdc-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="20fdc-161">請連絡 [OfficeSpace Software 用戶端支援小組](mailto:support@officespacesoftware.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="20fdc-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) to get these values.</span></span> 

4. <span data-ttu-id="20fdc-162">OfficeSpace Software 應用程式會預期要有特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="20fdc-162">OfficeSpace Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="20fdc-163">請設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="20fdc-163">Please configure the following claims for this application.</span></span> <span data-ttu-id="20fdc-164">您可以在應用程式整合頁面的 [使用者屬性] 區段中管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="20fdc-164">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="20fdc-165">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="20fdc-165">The following screenshot shows an example for this.</span></span>
    
    ![設定屬性](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="20fdc-167">在 [單一登入] 對話方塊內的 [使用者屬性] 區段中，選取 [user.mail] 當作 [使用者識別碼]，並在下表顯示的每個列上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="20fdc-167">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="20fdc-168">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="20fdc-168">Attribute Name</span></span> | <span data-ttu-id="20fdc-169">屬性值</span><span class="sxs-lookup"><span data-stu-id="20fdc-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="20fdc-170">電子郵件</span><span class="sxs-lookup"><span data-stu-id="20fdc-170">email</span></span> | <span data-ttu-id="20fdc-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="20fdc-171">user.mail</span></span> |
    | <span data-ttu-id="20fdc-172">名稱</span><span class="sxs-lookup"><span data-stu-id="20fdc-172">name</span></span> | <span data-ttu-id="20fdc-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="20fdc-173">user.displayname</span></span> |
    | <span data-ttu-id="20fdc-174">first_name</span><span class="sxs-lookup"><span data-stu-id="20fdc-174">first_name</span></span> | <span data-ttu-id="20fdc-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="20fdc-175">user.givenname</span></span> |
    | <span data-ttu-id="20fdc-176">last_name</span><span class="sxs-lookup"><span data-stu-id="20fdc-176">last_name</span></span> | <span data-ttu-id="20fdc-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="20fdc-177">user.surname</span></span> |

    <span data-ttu-id="20fdc-178">a.</span><span class="sxs-lookup"><span data-stu-id="20fdc-178">a.</span></span> <span data-ttu-id="20fdc-179">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="20fdc-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="20fdc-180">設定新增</span><span class="sxs-lookup"><span data-stu-id="20fdc-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![設定屬性](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="20fdc-182">b.</span><span class="sxs-lookup"><span data-stu-id="20fdc-182">b.</span></span> <span data-ttu-id="20fdc-183">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="20fdc-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="20fdc-184">c.</span><span class="sxs-lookup"><span data-stu-id="20fdc-184">c.</span></span> <span data-ttu-id="20fdc-185">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="20fdc-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="20fdc-186">d.</span><span class="sxs-lookup"><span data-stu-id="20fdc-186">d.</span></span> <span data-ttu-id="20fdc-187">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="20fdc-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="20fdc-188">在 [SAML 簽署憑證] 區段上，複製憑證的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="20fdc-188">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of the certificate.</span></span>

    ![憑證下載連結](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="20fdc-190">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="20fdc-190">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="20fdc-192">在 [OfficeSpace Software 組態] 區段上，按一下 [設定 OfficeSpace Software] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="20fdc-192">On the **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="20fdc-193">從 [快速參考] 區段中複製 [登入 URL] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="20fdc-193">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![OfficeSpace Software 設定](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="20fdc-195">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 OfficeSpace Software 租用戶。</span><span class="sxs-lookup"><span data-stu-id="20fdc-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="20fdc-196">移至 [設定]，然後按一下 [連接器]。</span><span class="sxs-lookup"><span data-stu-id="20fdc-196">Go to **Settings** and click **Connectors**.</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="20fdc-198">按一下 [SAML 驗證]。</span><span class="sxs-lookup"><span data-stu-id="20fdc-198">Click **SAML Authentication**.</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="20fdc-200">在 [SAML 驗證]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="20fdc-200">In the **SAML Authentication** section, perform the following steps:</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="20fdc-202">a.</span><span class="sxs-lookup"><span data-stu-id="20fdc-202">a.</span></span> <span data-ttu-id="20fdc-203">在 [登出提供者 url] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="20fdc-203">In the **Logout provider url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="20fdc-204">b.</span><span class="sxs-lookup"><span data-stu-id="20fdc-204">b.</span></span> <span data-ttu-id="20fdc-205">在 [用戶端 idp 目標 url] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="20fdc-205">In the **Client idp target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="20fdc-206">c.</span><span class="sxs-lookup"><span data-stu-id="20fdc-206">c.</span></span> <span data-ttu-id="20fdc-207">將您從 Azure 入口網站複製的 [指紋] 值，貼到 [用戶端 IDP 憑證指紋] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="20fdc-207">Paste the **Thumbprint** value which you have copied from Azure portal, into the **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="20fdc-208">d.</span><span class="sxs-lookup"><span data-stu-id="20fdc-208">d.</span></span> <span data-ttu-id="20fdc-209">按一下 [儲存設定] 。</span><span class="sxs-lookup"><span data-stu-id="20fdc-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="20fdc-210">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="20fdc-210">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="20fdc-211">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="20fdc-211">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="20fdc-212">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="20fdc-212">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="20fdc-213">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="20fdc-213">Create an Azure AD test user</span></span>

<span data-ttu-id="20fdc-214">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="20fdc-214">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="20fdc-216">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="20fdc-216">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="20fdc-217">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="20fdc-217">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="20fdc-219">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="20fdc-219">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="20fdc-221">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="20fdc-221">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="20fdc-223">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="20fdc-223">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="20fdc-225">a.</span><span class="sxs-lookup"><span data-stu-id="20fdc-225">a.</span></span> <span data-ttu-id="20fdc-226">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="20fdc-226">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="20fdc-227">b.</span><span class="sxs-lookup"><span data-stu-id="20fdc-227">b.</span></span> <span data-ttu-id="20fdc-228">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="20fdc-228">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="20fdc-229">c.</span><span class="sxs-lookup"><span data-stu-id="20fdc-229">c.</span></span> <span data-ttu-id="20fdc-230">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="20fdc-230">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="20fdc-231">d.</span><span class="sxs-lookup"><span data-stu-id="20fdc-231">d.</span></span> <span data-ttu-id="20fdc-232">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="20fdc-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="20fdc-233">建立 OfficeSpace Software 測試使用者</span><span class="sxs-lookup"><span data-stu-id="20fdc-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="20fdc-234">本節目標是在 OfficeSpace Software 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="20fdc-234">The objective of this section is to create a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="20fdc-235">OfficeSpace Software 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="20fdc-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="20fdc-236">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="20fdc-236">There is no action item for you in this section.</span></span> <span data-ttu-id="20fdc-237">嘗試存取 OfficeSpace Software 時，如果使用者還不存在，就會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="20fdc-237">A new user will be created during an attempt to access OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="20fdc-238">如果您需要手動建立使用者，您需要連絡 [OfficeSpace Software 支援小組](mailto:support@officespacesoftware.com)。</span><span class="sxs-lookup"><span data-stu-id="20fdc-238">If you need to create an user manually, you need to Contact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="20fdc-239">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="20fdc-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="20fdc-240">在本節中，您會將 OfficeSpace Software 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="20fdc-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to OfficeSpace Software.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="20fdc-242">**若要指派 Britta Simon 到 OfficeSpace Software，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="20fdc-242">**To assign Britta Simon to OfficeSpace Software, perform the following steps:**</span></span>

1. <span data-ttu-id="20fdc-243">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="20fdc-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="20fdc-245">在應用程式清單中，選取 [OfficeSpace Software]。</span><span class="sxs-lookup"><span data-stu-id="20fdc-245">In the applications list, select **OfficeSpace Software**.</span></span>

    ![應用程式清單中的 OfficeSpace Software 連結](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="20fdc-247">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="20fdc-247">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="20fdc-249">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="20fdc-249">Click **Add** button.</span></span> <span data-ttu-id="20fdc-250">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="20fdc-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="20fdc-252">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="20fdc-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="20fdc-253">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="20fdc-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="20fdc-254">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="20fdc-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="20fdc-255">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="20fdc-255">Test single sign-on</span></span>

<span data-ttu-id="20fdc-256">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="20fdc-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="20fdc-257">當您在 [存取面板] 中按一下 [OfficeSpace Software] 圖格時，您應該會自動登入您的 OfficeSpace Software 應用程式。</span><span class="sxs-lookup"><span data-stu-id="20fdc-257">When you click the OfficeSpace Software tile in the Access Panel, you should get automatically signed-on to your OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="20fdc-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="20fdc-258">Additional resources</span></span>

* [<span data-ttu-id="20fdc-259">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="20fdc-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="20fdc-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="20fdc-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

