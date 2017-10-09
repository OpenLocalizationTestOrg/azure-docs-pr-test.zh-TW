---
title: "aaaAzure AD + 的 Azure RemoteApp 的 Active Directory 需求 |Microsoft 文件"
description: "深入了解如何設定 Active Directory 與 Azure RemoteApp 的 toowork tooset。"
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
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="87cbb-103">Azure RemoteApp 的 Azure AD + Active Directory 需求</span><span class="sxs-lookup"><span data-stu-id="87cbb-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="87cbb-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="87cbb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="87cbb-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="87cbb-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="87cbb-106">對於您 Azure RemoteApp 的混合式集合，或您想要使用 AD Connect toofederate 雲端集合，您會需要 toodo hello 下列。</span><span class="sxs-lookup"><span data-stu-id="87cbb-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want toofederate using AD Connect, you need toodo hello following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="87cbb-107">連接 Azure AD 和 Active Directory</span><span class="sxs-lookup"><span data-stu-id="87cbb-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="87cbb-108">如果您想要 tooconnect，Azure AD 租用戶和您在內部部署 Active Directory 環境中，使用 AD Connect。</span><span class="sxs-lookup"><span data-stu-id="87cbb-108">If you want tooconnect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="87cbb-109">它只會執行[4 按一下](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/)tooconnect hello 兩個目錄。</span><span class="sxs-lookup"><span data-stu-id="87cbb-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello two directories.</span></span>

<span data-ttu-id="87cbb-110">注意 - 混合式集合需使用目錄同步處理。</span><span class="sxs-lookup"><span data-stu-id="87cbb-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="87cbb-111">請確定您的 "@domain.com" 是相符的</span><span class="sxs-lookup"><span data-stu-id="87cbb-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="87cbb-112">開始之前，請確定您的 Azure AD 網域您在內部部署樹系相符項目 hello 尾碼該 hello UPN。</span><span class="sxs-lookup"><span data-stu-id="87cbb-112">Before you get started, make sure that hello UPN for your on-premises forest matches hello suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="87cbb-113">所有使用者登入 Azure RemoteApp hello UPN 網域尾碼設定 Azure AD 中之後，將身分都登入 「 使用者 @<hello suffix you set up>。 」</span><span class="sxs-lookup"><span data-stu-id="87cbb-113">After you set up hello UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<hello suffix you set up>."</span></span> <span data-ttu-id="87cbb-114">請確定使用者可以也登入 hello 相同user@suffix到 hello 在內部部署網域。</span><span class="sxs-lookup"><span data-stu-id="87cbb-114">Make sure that users can also log in with hello same user@suffix into hello on-premises domain.</span></span> <span data-ttu-id="87cbb-115">在某些情況下您可以設定一個網域名稱時指定不同的網域尾碼，如 hello 使用者內部部署的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="87cbb-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for hello user on-prem.</span></span> <span data-ttu-id="87cbb-116">在此情況下，您的使用者會無法 tooconnect tooany 已加入網域的電腦或透過 Azure RemoteApp 的資源。</span><span class="sxs-lookup"><span data-stu-id="87cbb-116">In this case, your users won't be able tooconnect tooany domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="87cbb-117">例如，如果您設定您的 UPN 網域尾碼為 contoso.com，AAD 中，但是有些使用者在內部部署/AD 中使用的設定的 toolog @contoso.uk，這些使用者將不會無法 toocorrectly 記錄，到 hello ARA 集合。</span><span class="sxs-lookup"><span data-stu-id="87cbb-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured toolog in with @contoso.uk, then those users will not be able toocorrectly log into hello ARA collection.</span></span> <span data-ttu-id="87cbb-118">使用者必須是 UPN AAD 和 AD 中的將相同 hello 登入 toobe 可能 hello"</span><span class="sxs-lookup"><span data-stu-id="87cbb-118">Users UPN in AAD and AD must be hello same for hello login toobe possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="87cbb-119">建立 Azure RemoteApp 的物件</span><span class="sxs-lookup"><span data-stu-id="87cbb-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="87cbb-120">您還需要下列內部部署 Active Directory 物件 toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="87cbb-120">You also need toocreate hello following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="87cbb-121">服務帳戶 tooprovide 存取 toodomain 資源的 RemoteApp 程式加入 RDSH 結束點 toohello 在內部部署網域。</span><span class="sxs-lookup"><span data-stu-id="87cbb-121">A service account tooprovide access toodomain resources for RemoteApp programs by joining RDSH end points toohello on-premises domain.</span></span>
* <span data-ttu-id="87cbb-122">組織單位 (OU) toocontain RemoteApp 的電腦物件。</span><span class="sxs-lookup"><span data-stu-id="87cbb-122">An Organizational Unit (OU) toocontain RemoteApp machine objects.</span></span> <span data-ttu-id="87cbb-123">使用 hello OU 是建議 （但非必要） tooisolate hello 帳戶與您將 RemoteApp 搭配使用的原則。</span><span class="sxs-lookup"><span data-stu-id="87cbb-123">Use of hello OU is recommended (but not required) tooisolate hello accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="87cbb-124">您會需要這些物件的這兩個當您建立您的 RemoteApp 集合，因此先確定 toodo 這些步驟。</span><span class="sxs-lookup"><span data-stu-id="87cbb-124">You need both of these objects when you create your RemoteApp collection, so be sure toodo these steps first.</span></span>

