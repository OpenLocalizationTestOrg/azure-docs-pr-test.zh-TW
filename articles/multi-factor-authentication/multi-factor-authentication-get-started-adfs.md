---
title: "aaaTwo 步驟驗證，且 AD FS 的 Azure MFA |Microsoft 文件"
description: "這是描述 tooget 如何開始使用 Azure MFA 和 AD FS 的 hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="81351-103">開始使用 Azure Multi-Factor Authentication Server 和 Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="81351-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="81351-104"><center>![雲端](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="81351-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="81351-105">如果組織已使用 AD FS 讓內部部署 Active Directory 與 Azure Active Directory 同盟，就會有兩個使用 Azure Multi-Factor Authentication 的選項。</span><span class="sxs-lookup"><span data-stu-id="81351-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="81351-106">使用 Azure Multi-Factor Authentication 或 Active Directory Federation Services 保護雲端資源</span><span class="sxs-lookup"><span data-stu-id="81351-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="81351-107">使用 Azure Multi-Factor Authentication Server 保護雲端和內部部署資源</span><span class="sxs-lookup"><span data-stu-id="81351-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="81351-108">hello 下表摘要說明 hello 保護與 Azure Multi-factor Authentication Server 和 AD FS 資源之間的驗證體驗</span><span class="sxs-lookup"><span data-stu-id="81351-108">hello following table summarizes hello verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="81351-109">驗證體驗 - 瀏覽器型應用程式</span><span class="sxs-lookup"><span data-stu-id="81351-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="81351-110">驗證體驗 - 非瀏覽器型應用程式</span><span class="sxs-lookup"><span data-stu-id="81351-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="81351-111">使用 Azure Multi-Factor Authentication 保護 Azure AD 資源</span><span class="sxs-lookup"><span data-stu-id="81351-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="81351-112">hello 第一個驗證步驟會執行內部部署使用 AD FS。</span><span class="sxs-lookup"><span data-stu-id="81351-112">hello first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="81351-113">hello 第二個步驟是使用雲端驗證來執行的電話式方法。</span><span class="sxs-lookup"><span data-stu-id="81351-113">hello second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="81351-114">使用 Active Directory Federation Services 保護 Azure AD 資源</span><span class="sxs-lookup"><span data-stu-id="81351-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="81351-115">hello 第一個驗證步驟會執行內部部署使用 AD FS。</span><span class="sxs-lookup"><span data-stu-id="81351-115">hello first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="81351-116">hello 第二個步驟是內部執行區分 hello 宣告。</span><span class="sxs-lookup"><span data-stu-id="81351-116">hello second step is performed on-premises by honoring hello claim.</span></span></li> |

<span data-ttu-id="81351-117">有關同盟使用者之應用程式密碼的警告：</span><span class="sxs-lookup"><span data-stu-id="81351-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="81351-118">應用程式密碼是使用雲端驗證進行驗證，因此會略過同盟。</span><span class="sxs-lookup"><span data-stu-id="81351-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="81351-119">唯有在設定應用程式密碼時才能主動使用同盟。</span><span class="sxs-lookup"><span data-stu-id="81351-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="81351-120">應用程式密碼不會遵守內部部署用戶端存取控制設定。</span><span class="sxs-lookup"><span data-stu-id="81351-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="81351-121">您會失去應用程式密碼的內部部署驗證記錄功能。</span><span class="sxs-lookup"><span data-stu-id="81351-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="81351-122">帳戶停用/刪除可能需要針對目錄同步作業，因而延遲在 hello 雲端身分識別的應用程式密碼停用/刪除 toothree 小時。</span><span class="sxs-lookup"><span data-stu-id="81351-122">Account disable/deletion may take up toothree hours for directory sync, delaying disable/deletion of app passwords in hello cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81351-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="81351-123">Next steps</span></span>
<span data-ttu-id="81351-124">設定 Azure Multi-factor Authentication 或 hello 與 AD FS 的 Azure Multi-factor Authentication Server 上的資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="81351-124">For information on setting up either Azure Multi-Factor Authentication or hello Azure Multi-Factor Authentication Server with AD FS, see hello following articles:</span></span>

* [<span data-ttu-id="81351-125">使用 Azure Multi-Factor Authentication 和 AD FS 保護雲端資源</span><span class="sxs-lookup"><span data-stu-id="81351-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="81351-126">搭配 Windows Server 2012 R2 AD FS 使用 Azure Multi-Factor Authentication Server 保護雲端和內部部署資源</span><span class="sxs-lookup"><span data-stu-id="81351-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="81351-127">搭配 AD FS 2.0 使用 Azure Multi-Factor Authentication Server 保護雲端和內部部署資源</span><span class="sxs-lookup"><span data-stu-id="81351-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
