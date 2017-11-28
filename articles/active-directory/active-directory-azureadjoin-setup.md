---
title: "為您的使用者註冊 Azure AD Join aaaSetting |Microsoft 文件"
description: "說明系統管理員如何設定 Azure AD Join 以用於內部部署目錄及裝置註冊。"
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="f0090-103">在組織中設定 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="f0090-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="f0090-104">設定 Azure Active Directory Join (Azure AD Join) 之前，您需要 tooeither 同步處理您的內部部署目錄的使用者 toohello 雲端或手動建立在 Azure AD 中的 受管理的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f0090-104">Before you set up Azure Active Directory Join (Azure AD Join), you need tooeither sync up your on-premises directory of users toohello cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="f0090-105">同步處理您在內部部署使用者 tooAzure AD 中說明的詳細指示[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="f0090-105">Detailed instructions for syncing your on-premises users tooAzure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="f0090-106">toomanually 建立及管理 Azure AD 中的使用者，請參閱太[Azure AD 中的使用者管理](https://msdn.microsoft.com/library/azure/hh967609.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f0090-106">toomanually create and manage users in Azure AD, refer too[User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="f0090-107">設定裝置註冊</span><span class="sxs-lookup"><span data-stu-id="f0090-107">Set up device registration</span></span>
1. <span data-ttu-id="f0090-108">Toohello Azure 入口網站管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="f0090-108">Log on toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="f0090-109">在 hello 左窗格中，選取  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="f0090-109">On hello left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="f0090-110">在 hello**目錄**索引標籤上，選取您的目錄。</span><span class="sxs-lookup"><span data-stu-id="f0090-110">On hello **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="f0090-111">選取 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f0090-111">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="f0090-112">移 toohello**裝置**> 一節。</span><span class="sxs-lookup"><span data-stu-id="f0090-112">Go toohello **Devices** section.</span></span>
6. <span data-ttu-id="f0090-113">在 hello**裝置**索引標籤上，hello 下列設定：</span><span class="sxs-lookup"><span data-stu-id="f0090-113">On hello **devices** tab, set hello following:</span></span>  
   * <span data-ttu-id="f0090-114">**最大數目的裝置每個使用者**： 選取 hello 的使用者可以在 Azure AD 中擁有的裝置數目上限。</span><span class="sxs-lookup"><span data-stu-id="f0090-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select hello maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="f0090-115">如果使用者達到此配額時，它們將無法 tooadd 其他裝置之前無法移除一或多個現有的裝置。</span><span class="sxs-lookup"><span data-stu-id="f0090-115">If a user reaches this quota, they will not be able tooadd additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="f0090-116">**需要 MULTI-FACTOR AUTH tooJOIN 裝置**： 設定使用者是否需要的 tooprovide 第二個驗證因素 toojoin 其裝置 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="f0090-116">**REQUIRE MULTI-FACTOR AUTH tooJOIN DEVICES**: Set whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="f0090-117">如需有關 Azure Multi-factor Authentication 的詳細資訊，請參閱[開始使用 Azure Multi-factor Authentication hello 定域機組中](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="f0090-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in hello cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="f0090-118">**使用者可能 AZURE AD JOIN 裝置**： 選取 hello 使用者和群組允許 toojoin 裝置 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="f0090-118">**USERS MAY AZURE AD JOIN DEVICES**: Select hello users and groups that are allowed toojoin devices tooAzure AD.</span></span>
   * <span data-ttu-id="f0090-119">**其他系統管理員在 AZURE AD 加入裝置**: Azure AD Premium 或 hello Enterprise Mobility Suite (EMS)，您可以選擇哪些使用者授與本機系統管理員權限 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="f0090-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or hello Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights toohello device.</span></span> <span data-ttu-id="f0090-120">全域系統管理員和裝置擁有者預設會授與本機系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="f0090-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="f0090-121"><center>![設定裝置註冊](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="f0090-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="f0090-122">設定 Azure AD Join 為您的使用者之後，它們可以連接 tooAzure AD 透過其公司或個人裝置。</span><span class="sxs-lookup"><span data-stu-id="f0090-122">After you set up Azure AD Join for your users, they can connect tooAzure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="f0090-123">以下是您可以使用 tooenable 使用者 tooset 註冊 Azure AD Join hello 三個案例：</span><span class="sxs-lookup"><span data-stu-id="f0090-123">Following are hello three scenarios you can use tooenable your users tooset up Azure AD Join:</span></span>

* <span data-ttu-id="f0090-124">使用者將公司擁有的裝置直接 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="f0090-124">Users join a company-owned device directly tooAzure AD.</span></span>
* <span data-ttu-id="f0090-125">使用者網域加入公司擁有裝置 toohello 在內部部署 Active Directory，然後將擴充 hello 裝置 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="f0090-125">Users domain-join a company-owned device toohello on-premises Active Directory and then extend hello device tooAzure AD.</span></span>
* <span data-ttu-id="f0090-126">使用者新增工作或學校帳戶 tooWindows 個人裝置上</span><span class="sxs-lookup"><span data-stu-id="f0090-126">Users add work or school accounts tooWindows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="f0090-127">其他資訊</span><span class="sxs-lookup"><span data-stu-id="f0090-127">Additional information</span></span>
* [<span data-ttu-id="f0090-128">Hello 企業版的 Windows 10： 工作的方式 toouse 裝置</span><span class="sxs-lookup"><span data-stu-id="f0090-128">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="f0090-129">擴充功能 tooWindows 10 裝置透過 Azure Active Directory 加入雲端</span><span class="sxs-lookup"><span data-stu-id="f0090-129">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="f0090-130">了解適用於 Azure AD Join 的使用案例</span><span class="sxs-lookup"><span data-stu-id="f0090-130">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="f0090-131">連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗</span><span class="sxs-lookup"><span data-stu-id="f0090-131">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="f0090-132">設定 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="f0090-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

