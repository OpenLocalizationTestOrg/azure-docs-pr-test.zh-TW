---
title: "設定同盟單一登入非組件庫的應用程式的 aaaProblem |Microsoft 文件"
description: "解決部分 hello hello Azure AD 應用程式庫中設定同盟單一登入 tooyour 自訂 SAML 的應用程式未列出時，可能會遇到的常見問題"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="b7ec8-103">為不在資源庫內的應用程式設定同盟單一登入時遇到的問題</span><span class="sxs-lookup"><span data-stu-id="b7ec8-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="b7ec8-104">如果您在設定應用程式時遇到問題。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="b7ec8-105">請確認您已依照 hello 文件中的所有 hello 步驟[設定單一登入 tooapplications 不在 hello Azure Active Directory 應用程式庫中。](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span><span class="sxs-lookup"><span data-stu-id="b7ec8-105">Verify you have followed all hello steps in hello article [Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="b7ec8-106">無法加入 hello 應用程式的另一個執行個體</span><span class="sxs-lookup"><span data-stu-id="b7ec8-106">Can’t add another instance of hello application</span></span>

<span data-ttu-id="b7ec8-107">tooadd 應用程式的第二個執行個體，您需要 toobe 能夠：</span><span class="sxs-lookup"><span data-stu-id="b7ec8-107">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="b7ec8-108">設定 hello 第二個執行個體的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-108">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="b7ec8-109">您必須能夠 tooconfigure hello 相同識別項用於 hello 第一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-109">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="b7ec8-110">設定用於 hello 第一個執行個體的 hello 與不同的憑證。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-110">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="b7ec8-111">如果 hello 應用程式不支援任何上述 hello。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-111">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="b7ec8-112">然後，您必須能夠 tooconfigure 第二個執行個體。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-112">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="b7ec8-113">其中將 hello EntityID （使用者識別碼） 格式的設定</span><span class="sxs-lookup"><span data-stu-id="b7ec8-113">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="b7ec8-114">您必須能夠 tooselect hello EntityID （使用者識別碼） 格式，Azure AD 會傳送 toohello 應用程式以 hello 回應使用者驗證之後。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-114">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="b7ec8-115">Hello NameID 屬性 （使用者識別碼） 的 azure AD 選取 hello 格式會根據選取的 hello 值或 hello hello hello SAML AuthRequest 中的應用程式所要求的格式。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-115">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="b7ec8-116">如需詳細資訊，請造訪 hello 文章[單一登入的 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)hello 之下 NameIDPolicy，</span><span class="sxs-lookup"><span data-stu-id="b7ec8-116">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="b7ec8-117">其中從 Azure AD 取得 hello 應用程式中繼資料或憑證</span><span class="sxs-lookup"><span data-stu-id="b7ec8-117">Where do I get hello application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="b7ec8-118">toodownload hello 應用程式中繼資料或憑證從 Azure AD，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="b7ec8-118">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="b7ec8-119">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="b7ec8-119">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b7ec8-120">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b7ec8-121">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b7ec8-122">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b7ec8-123">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="b7ec8-124">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="b7ec8-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="b7ec8-125">選取您已設定單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-125">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b7ec8-126">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b7ec8-127">跳過**SAML 簽章憑證**區段，然後按一下 [**下載**資料行值。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-127">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="b7ec8-128">根據哪些 hello 應用程式需要設定單一登入，您會看到其中一個 hello 選項 toodownload hello 中繼資料 XML 或 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-128">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="b7ec8-129">Azure AD 不會提供 URL tooget hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-129">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="b7ec8-130">hello 中繼資料，才能擷取為 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-130">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="b7ec8-131">不知道如何 toocustomize SAML 宣告傳送 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="b7ec8-131">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="b7ec8-132">toolearn 如何 toocustomize hello SAML 屬性宣告傳送 tooyour 應用程式，請參閱[宣告 Azure Active Directory 中的對應](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b7ec8-132">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7ec8-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7ec8-133">Next steps</span></span>
[<span data-ttu-id="b7ec8-134">使用 Azure Active Directory 管理應用程式</span><span class="sxs-lookup"><span data-stu-id="b7ec8-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
