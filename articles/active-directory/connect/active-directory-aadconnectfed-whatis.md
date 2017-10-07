---
title: "aaaAzure AD 連線和同盟 |Microsoft 文件"
description: "此頁面是 hello 中央位置，如需有關使用 Azure AD Connect 的 AD FS 作業的所有文件。"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: f9107cf5-0131-499a-9edf-616bf3afef4d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: anandy
ms.openlocfilehash: dc70206eee2296c2320712ef2ade48ccebcc912d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-and-federation"></a><span data-ttu-id="7c214-103">Azure AD Connect 和同盟</span><span class="sxs-lookup"><span data-stu-id="7c214-103">Azure AD Connect and federation</span></span>
<span data-ttu-id="7c214-104">Azure Active Directory (Azure AD) Connect 可讓您使用內部部署 Active Directory 同盟服務 (AD FS) 與 Azure AD 來設定同盟。</span><span class="sxs-lookup"><span data-stu-id="7c214-104">Azure Active Directory (Azure AD) Connect lets you configure federation with on-premises Active Directory Federation Services (AD FS) and Azure AD.</span></span> <span data-ttu-id="7c214-105">同盟登入，您可以啟用使用者 toosign tooAzure AD 為基礎的服務在內部部署密碼-，而在 hello 公司網路上而不需要 tooenter 密碼一次。</span><span class="sxs-lookup"><span data-stu-id="7c214-105">With federation sign-in, you can enable users toosign in tooAzure AD-based services with their on-premises passwords--and, while on hello corporate network, without having tooenter their passwords again.</span></span> <span data-ttu-id="7c214-106">藉由使用 AD FS 中的 hello 同盟選項，您可以部署新安裝的 AD FS，或您可以在 Windows Server 2012 R2 的伺服器陣列中指定現有的安裝。</span><span class="sxs-lookup"><span data-stu-id="7c214-106">By using hello federation option with AD FS, you can deploy a new installation of AD FS, or you can specify an existing installation in a Windows Server 2012 R2 farm.</span></span>

<span data-ttu-id="7c214-107">本主題為 hello 家用與同盟相關功能的 Azure AD Connect 的資訊。</span><span class="sxs-lookup"><span data-stu-id="7c214-107">This topic is hello home for information on federation-related functionalities for Azure AD Connect.</span></span> <span data-ttu-id="7c214-108">它會列出連結 tooall 相關主題。</span><span class="sxs-lookup"><span data-stu-id="7c214-108">It lists links tooall related topics.</span></span> <span data-ttu-id="7c214-109">連結 tooAzure AD Connect，請參閱[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="7c214-109">For links tooAzure AD Connect, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="azure-ad-connect-federation-topics"></a><span data-ttu-id="7c214-110">Azure AD Connect：同盟主題</span><span class="sxs-lookup"><span data-stu-id="7c214-110">Azure AD Connect: federation topics</span></span>
| <span data-ttu-id="7c214-111">主題</span><span class="sxs-lookup"><span data-stu-id="7c214-111">Topic</span></span> | <span data-ttu-id="7c214-112">它涵蓋了與時機 tooread 它</span><span class="sxs-lookup"><span data-stu-id="7c214-112">What it covers and when tooread it</span></span> |
|:--- |:--- |
| <span data-ttu-id="7c214-113">**Azure AD Connect 使用者登入選項**</span><span class="sxs-lookup"><span data-stu-id="7c214-113">**Azure AD Connect user sign-in options**</span></span> | |
| [<span data-ttu-id="7c214-114">了解使用者登入選項</span><span class="sxs-lookup"><span data-stu-id="7c214-114">Understand user sign-in options</span></span>](active-directory-aadconnect-user-signin.md) |<span data-ttu-id="7c214-115">深入了解各種使用者登入選項，以及它們如何影響 hello Azure 登入的使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="7c214-115">Learn about various user sign-in options and how they affect hello Azure sign-in user experience.</span></span> |
| <span data-ttu-id="7c214-116">**使用 Azure AD Connect 安裝 AD FS**</span><span class="sxs-lookup"><span data-stu-id="7c214-116">**Install AD FS by using Azure AD Connect**</span></span> | |
| [<span data-ttu-id="7c214-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="7c214-117">Prerequisites</span></span>](active-directory-aadconnect-get-started-custom.md#ad-fs-configuration-pre-requisites) |<span data-ttu-id="7c214-118">請參閱 AD FS 安裝 Azure AD Connect 透過成功的 hello 必要條件。</span><span class="sxs-lookup"><span data-stu-id="7c214-118">See hello prerequisites for a successful AD FS installation via Azure AD Connect.</span></span> |
| [<span data-ttu-id="7c214-119">設定 AD FS 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="7c214-119">Configure an AD FS farm</span></span>](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs) |<span data-ttu-id="7c214-120">使用 Azure AD Connect 安裝新的 AD FS 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="7c214-120">Install a new AD FS farm by using Azure AD Connect.</span></span> |
| [<span data-ttu-id="7c214-121">使用替代登入識別碼與 Azure AD 建立同盟關係</span><span class="sxs-lookup"><span data-stu-id="7c214-121">Federate with Azure AD using alternate login ID </span></span>](active-directory-aadconnect-federation-management.md#alternateid) | <span data-ttu-id="7c214-122">使用替代登入識別碼設定同盟</span><span class="sxs-lookup"><span data-stu-id="7c214-122">Configure federation using alternate login ID</span></span>  |
| <span data-ttu-id="7c214-123">**修改 hello AD FS 設定**</span><span class="sxs-lookup"><span data-stu-id="7c214-123">**Modify hello AD FS configuration**</span></span> | |
| [<span data-ttu-id="7c214-124">修復 hello 信任</span><span class="sxs-lookup"><span data-stu-id="7c214-124">Repair hello trust</span></span>](active-directory-aadconnect-federation-management.md#repairthetrust) |<span data-ttu-id="7c214-125">修復 hello 目前信任之間內部部署 AD FS 和 Office 365/Azure。</span><span class="sxs-lookup"><span data-stu-id="7c214-125">Repair hello current trust between on-premises AD FS and Office 365/Azure.</span></span> |
| [<span data-ttu-id="7c214-126">新增 AD FS 伺服器</span><span class="sxs-lookup"><span data-stu-id="7c214-126">Add a new AD FS server</span></span>](active-directory-aadconnect-federation-management.md#addadfsserver) |<span data-ttu-id="7c214-127">在初始安裝之後，增加 AD FS 伺服器來擴充 AD FS 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="7c214-127">Expand an AD FS farm with an additional AD FS server after initial installation.</span></span> |
| [<span data-ttu-id="7c214-128">新增 AD FS WAP 伺服器</span><span class="sxs-lookup"><span data-stu-id="7c214-128">Add a new AD FS WAP server</span></span>](active-directory-aadconnect-federation-management.md#addwapserver) |<span data-ttu-id="7c214-129">在初始安裝之後，增加 Web 應用程式 Proxy (WAP) 伺服器來擴充 AD FS 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="7c214-129">Expand an AD FS farm with an additional Web Application Proxy (WAP) server after initial installation.</span></span> |
| [<span data-ttu-id="7c214-130">新增新的同盟網域</span><span class="sxs-lookup"><span data-stu-id="7c214-130">Add a new federated domain</span></span>](active-directory-aadconnect-federation-management.md#addfeddomain) |<span data-ttu-id="7c214-131">加入另一個網域 toobe 與 Azure AD 建立同盟。</span><span class="sxs-lookup"><span data-stu-id="7c214-131">Add another domain toobe federated with Azure AD.</span></span> |
| [<span data-ttu-id="7c214-132">Hello SSL 憑證更新</span><span class="sxs-lookup"><span data-stu-id="7c214-132">Update hello SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="7c214-133">更新 AD FS 伺服器陣列的 hello SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="7c214-133">Update hello SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="7c214-134">**其他同盟組態**</span><span class="sxs-lookup"><span data-stu-id="7c214-134">**Other federation configuration**</span></span> | |
| [<span data-ttu-id="7c214-135">將多個 Azure AD 執行個體與單一 AD FS 執行個體同盟</span><span class="sxs-lookup"><span data-stu-id="7c214-135">Federate multiple instances of Azure AD with single instance of AD FS</span></span>](active-directory-aadconnectfed-single-adfs-multitenant-federation.md) | <span data-ttu-id="7c214-136">將多個 Azure AD 和單一 AD FS 伺服器陣列建立同盟關係</span><span class="sxs-lookup"><span data-stu-id="7c214-136">Federate multiple Azure AD with single AD FS farm</span></span>| 
| [<span data-ttu-id="7c214-137">新增自訂公司標誌/圖例</span><span class="sxs-lookup"><span data-stu-id="7c214-137">Add a custom company logo/illustration</span></span>](active-directory-aadconnect-federation-management.md#customlogo) |<span data-ttu-id="7c214-138">藉由指定 hello hello AD FS 登入頁面顯示的自訂標誌，請修改 hello 登入體驗。</span><span class="sxs-lookup"><span data-stu-id="7c214-138">Modify hello sign-in experience by specifying hello custom logo that is shown on hello AD FS sign-in page.</span></span> |
| [<span data-ttu-id="7c214-139">新增登入說明</span><span class="sxs-lookup"><span data-stu-id="7c214-139">Add a sign-in description</span></span>](active-directory-aadconnect-federation-management.md#addsignindescription) |<span data-ttu-id="7c214-140">變更 hello 登入描述 hello AD FS 登入頁面上。</span><span class="sxs-lookup"><span data-stu-id="7c214-140">Change hello sign-in description on hello AD FS sign-in page.</span></span> |
| [<span data-ttu-id="7c214-141">修改 AD FS 宣告規則</span><span class="sxs-lookup"><span data-stu-id="7c214-141">Modify AD FS claim rules</span></span>](active-directory-aadconnect-federation-management.md#modclaims) |<span data-ttu-id="7c214-142">修改或新增對應 tooAzure AD Connect 同步處理設定的 AD FS 中的宣告規則。</span><span class="sxs-lookup"><span data-stu-id="7c214-142">Modify or add claim rules in AD FS that correspond tooAzure AD Connect sync configuration.</span></span> |


## <a name="additional-resources"></a><span data-ttu-id="7c214-143">其他資源</span><span class="sxs-lookup"><span data-stu-id="7c214-143">Additional resources</span></span>
* [<span data-ttu-id="7c214-144">將兩個 Azure AD 和單一 AD FS 建立同盟關係</span><span class="sxs-lookup"><span data-stu-id="7c214-144">Federating two Azure AD with single AD FS</span></span>](active-directory-aadconnectfed-single-adfs-multitenant-federation.md)
* [<span data-ttu-id="7c214-145">Azure 中的 AD FS 部署</span><span class="sxs-lookup"><span data-stu-id="7c214-145">AD FS deployment in Azure</span></span>](active-directory-aadconnect-azure-adfs.md)
* [<span data-ttu-id="7c214-146">使用 Azure 流量管理員在 Azure 中部署高可用性跨地區 AD FS</span><span class="sxs-lookup"><span data-stu-id="7c214-146">High-availability cross-geographic AD FS deployment in Azure with Azure Traffic Manager</span></span>](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)
