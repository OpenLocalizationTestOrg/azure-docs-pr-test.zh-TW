---
title: "Azure RemoteApp 的 Azure AD + Active Directory 需求 | Microsoft Docs"
description: "了解如何設定 Active Directory 以使用 Azure RemoteApp。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 78008a032faa93795cc02b720d68a0c6f5f16e9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="fcacb-103">Azure RemoteApp 的 Azure AD + Active Directory 需求</span><span class="sxs-lookup"><span data-stu-id="fcacb-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fcacb-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="fcacb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="fcacb-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="fcacb-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="fcacb-106">針對 Azure RemoteApp 混合式集合，或您要使用 AD Connect 建立同盟的雲端集合，您必須執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="fcacb-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want to federate using AD Connect, you need to do the following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="fcacb-107">連接 Azure AD 和 Active Directory</span><span class="sxs-lookup"><span data-stu-id="fcacb-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="fcacb-108">如果您要連接 Azure AD 租用戶和內部部署的 Active Directory 環境，請使用 AD Connect。</span><span class="sxs-lookup"><span data-stu-id="fcacb-108">If you want to connect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="fcacb-109">您只要 [按 4 下](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) 即可連接兩個目錄。</span><span class="sxs-lookup"><span data-stu-id="fcacb-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) to connect the two directories.</span></span>

<span data-ttu-id="fcacb-110">注意 - 混合式集合需使用目錄同步處理。</span><span class="sxs-lookup"><span data-stu-id="fcacb-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="fcacb-111">請確定您的 "@domain.com" 是相符的</span><span class="sxs-lookup"><span data-stu-id="fcacb-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="fcacb-112">在開始之前，請確定您在內部部署樹系的 UPN 符合您 Azure AD 網域的尾碼。</span><span class="sxs-lookup"><span data-stu-id="fcacb-112">Before you get started, make sure that the UPN for your on-premises forest matches the suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="fcacb-113">當您在 Azure AD 中設定 UPN 網域尾碼後，所有登入 Azure RemoteApp 的使用者都會以 "user@<the suffix you set up>" 的身分登入。</span><span class="sxs-lookup"><span data-stu-id="fcacb-113">After you set up the UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<the suffix you set up>."</span></span> <span data-ttu-id="fcacb-114">請確定使用者也可以用相同的 user@suffix 登入到內部部署網域。</span><span class="sxs-lookup"><span data-stu-id="fcacb-114">Make sure that users can also log in with the same user@suffix into the on-premises domain.</span></span> <span data-ttu-id="fcacb-115">在某些情況下，您可以在 Azure AD 中設定一個網域名稱，並同時為內部部署使用者指定不同的網域尾碼。</span><span class="sxs-lookup"><span data-stu-id="fcacb-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for the user on-prem.</span></span> <span data-ttu-id="fcacb-116">在此情況下，您的使用者將無法透過 Azure RemoteApp，連接至任何已加入網域的電腦或資源。</span><span class="sxs-lookup"><span data-stu-id="fcacb-116">In this case, your users won't be able to connect to any domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="fcacb-117">例如，如果您在 AAD 中將 UPN 網域尾碼設定為 contoso.com，但內部部署/AD 的某些使用者是設為以 @contoso.uk 登入，則那些使用者將無法正確登入 ARA 集合。</span><span class="sxs-lookup"><span data-stu-id="fcacb-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured to log in with @contoso.uk, then those users will not be able to correctly log into the ARA collection.</span></span> <span data-ttu-id="fcacb-118">AAD 和 AD 中的使用者 UPN 必須相同才能登入。</span><span class="sxs-lookup"><span data-stu-id="fcacb-118">Users UPN in AAD and AD must be the same for the login to be possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="fcacb-119">建立 Azure RemoteApp 的物件</span><span class="sxs-lookup"><span data-stu-id="fcacb-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="fcacb-120">您也必須建立下列內部部署 Active Directory 物件：</span><span class="sxs-lookup"><span data-stu-id="fcacb-120">You also need to create the following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="fcacb-121">服務帳戶，以透過將 RDSH 端點加入內部部署的網域，提供 RemoteApp 程式的網域資源存取權。</span><span class="sxs-lookup"><span data-stu-id="fcacb-121">A service account to provide access to domain resources for RemoteApp programs by joining RDSH end points to the on-premises domain.</span></span>
* <span data-ttu-id="fcacb-122">組織單位 (OU)，以包含 RemoteApp 電腦物件。</span><span class="sxs-lookup"><span data-stu-id="fcacb-122">An Organizational Unit (OU) to contain RemoteApp machine objects.</span></span> <span data-ttu-id="fcacb-123">建議您使用 OU (但非必要) 來隔離帳戶與將用於 RemoteApp 的原則。</span><span class="sxs-lookup"><span data-stu-id="fcacb-123">Use of the OU is recommended (but not required) to isolate the accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="fcacb-124">當您建立 RemoteApp 集合時，您會需要這兩個物件，因此請務必先執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="fcacb-124">You need both of these objects when you create your RemoteApp collection, so be sure to do these steps first.</span></span>

