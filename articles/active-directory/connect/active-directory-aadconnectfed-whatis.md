---
title: "Azure AD Connect 和同盟 | Microsoft Docs"
description: "此頁面是使用 Azure AD Connect 之 AD FS 作業的所有相關文件的中心位置。"
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
ms.openlocfilehash: 6822320c92d106d28607289a90f2f08a51e04070
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-and-federation"></a><span data-ttu-id="880d5-103">Azure AD Connect 和同盟</span><span class="sxs-lookup"><span data-stu-id="880d5-103">Azure AD Connect and federation</span></span>
<span data-ttu-id="880d5-104">Azure Active Directory (Azure AD) Connect 可讓您使用內部部署 Active Directory 同盟服務 (AD FS) 與 Azure AD 來設定同盟。</span><span class="sxs-lookup"><span data-stu-id="880d5-104">Azure Active Directory (Azure AD) Connect lets you configure federation with on-premises Active Directory Federation Services (AD FS) and Azure AD.</span></span> <span data-ttu-id="880d5-105">使用同盟登入，您可以讓使用者使用他們的內部部署密碼登入 Azure AD 服務，並且在使用公司網路時，無須再次輸入密碼就可登入服務。</span><span class="sxs-lookup"><span data-stu-id="880d5-105">With federation sign-in, you can enable users to sign in to Azure AD-based services with their on-premises passwords--and, while on the corporate network, without having to enter their passwords again.</span></span> <span data-ttu-id="880d5-106">您可以藉由使用具備 AD FS 的同盟選項來部署新安裝的 AD FS，或者您可以在 Windows Server 2012 R2 伺服器陣列中指定現有的安裝。</span><span class="sxs-lookup"><span data-stu-id="880d5-106">By using the federation option with AD FS, you can deploy a new installation of AD FS, or you can specify an existing installation in a Windows Server 2012 R2 farm.</span></span>

<span data-ttu-id="880d5-107">本主題是 Azure AD Connect 同盟相關功能的主要資訊來源。</span><span class="sxs-lookup"><span data-stu-id="880d5-107">This topic is the home for information on federation-related functionalities for Azure AD Connect.</span></span> <span data-ttu-id="880d5-108">它會列出所有相關的主題連結。</span><span class="sxs-lookup"><span data-stu-id="880d5-108">It lists links to all related topics.</span></span> <span data-ttu-id="880d5-109">如需 Azure AD Connect 的連結，請參閱 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="880d5-109">For links to Azure AD Connect, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="azure-ad-connect-federation-topics"></a><span data-ttu-id="880d5-110">Azure AD Connect：同盟主題</span><span class="sxs-lookup"><span data-stu-id="880d5-110">Azure AD Connect: federation topics</span></span>
| <span data-ttu-id="880d5-111">主題</span><span class="sxs-lookup"><span data-stu-id="880d5-111">Topic</span></span> | <span data-ttu-id="880d5-112">涵蓋內容和閱讀時機</span><span class="sxs-lookup"><span data-stu-id="880d5-112">What it covers and when to read it</span></span> |
|:--- |:--- |
| <span data-ttu-id="880d5-113">**Azure AD Connect 使用者登入選項**</span><span class="sxs-lookup"><span data-stu-id="880d5-113">**Azure AD Connect user sign-in options**</span></span> | |
| [<span data-ttu-id="880d5-114">了解使用者登入選項</span><span class="sxs-lookup"><span data-stu-id="880d5-114">Understand user sign-in options</span></span>](active-directory-aadconnect-user-signin.md) |<span data-ttu-id="880d5-115">了解各種使用者登入選項及其如何影響 Azure 登入使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="880d5-115">Learn about various user sign-in options and how they affect the Azure sign-in user experience.</span></span> |
| <span data-ttu-id="880d5-116">**使用 Azure AD Connect 安裝 AD FS**</span><span class="sxs-lookup"><span data-stu-id="880d5-116">**Install AD FS by using Azure AD Connect**</span></span> | |
| [<span data-ttu-id="880d5-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="880d5-117">Prerequisites</span></span>](active-directory-aadconnect-get-started-custom.md#ad-fs-configuration-pre-requisites) |<span data-ttu-id="880d5-118">請查看透過 Azure AD Connect 成功安裝 AD FS 安裝的必要條件。</span><span class="sxs-lookup"><span data-stu-id="880d5-118">See the prerequisites for a successful AD FS installation via Azure AD Connect.</span></span> |
| [<span data-ttu-id="880d5-119">設定 AD FS 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="880d5-119">Configure an AD FS farm</span></span>](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs) |<span data-ttu-id="880d5-120">使用 Azure AD Connect 安裝新的 AD FS 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="880d5-120">Install a new AD FS farm by using Azure AD Connect.</span></span> |
| [<span data-ttu-id="880d5-121">使用替代登入識別碼與 Azure AD 建立同盟關係</span><span class="sxs-lookup"><span data-stu-id="880d5-121">Federate with Azure AD using alternate login ID </span></span>](active-directory-aadconnect-federation-management.md#alternateid) | <span data-ttu-id="880d5-122">使用替代登入識別碼設定同盟</span><span class="sxs-lookup"><span data-stu-id="880d5-122">Configure federation using alternate login ID</span></span>  |
| <span data-ttu-id="880d5-123">**修改 AD FS 組態**</span><span class="sxs-lookup"><span data-stu-id="880d5-123">**Modify the AD FS configuration**</span></span> | |
| [<span data-ttu-id="880d5-124">修復信任</span><span class="sxs-lookup"><span data-stu-id="880d5-124">Repair the trust</span></span>](active-directory-aadconnect-federation-management.md#repairthetrust) |<span data-ttu-id="880d5-125">修復內部部署 AD FS 和 Office 365/Azure 之間目前的信任。</span><span class="sxs-lookup"><span data-stu-id="880d5-125">Repair the current trust between on-premises AD FS and Office 365/Azure.</span></span> |
| [<span data-ttu-id="880d5-126">新增 AD FS 伺服器</span><span class="sxs-lookup"><span data-stu-id="880d5-126">Add a new AD FS server</span></span>](active-directory-aadconnect-federation-management.md#addadfsserver) |<span data-ttu-id="880d5-127">在初始安裝之後，增加 AD FS 伺服器來擴充 AD FS 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="880d5-127">Expand an AD FS farm with an additional AD FS server after initial installation.</span></span> |
| [<span data-ttu-id="880d5-128">新增 AD FS WAP 伺服器</span><span class="sxs-lookup"><span data-stu-id="880d5-128">Add a new AD FS WAP server</span></span>](active-directory-aadconnect-federation-management.md#addwapserver) |<span data-ttu-id="880d5-129">在初始安裝之後，增加 Web 應用程式 Proxy (WAP) 伺服器來擴充 AD FS 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="880d5-129">Expand an AD FS farm with an additional Web Application Proxy (WAP) server after initial installation.</span></span> |
| [<span data-ttu-id="880d5-130">新增新的同盟網域</span><span class="sxs-lookup"><span data-stu-id="880d5-130">Add a new federated domain</span></span>](active-directory-aadconnect-federation-management.md#addfeddomain) |<span data-ttu-id="880d5-131">新增要與 Azure AD 同盟的其他網域。</span><span class="sxs-lookup"><span data-stu-id="880d5-131">Add another domain to be federated with Azure AD.</span></span> |
| [<span data-ttu-id="880d5-132">更新 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="880d5-132">Update the SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="880d5-133">更新 AD FS 伺服器陣列的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="880d5-133">Update the SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="880d5-134">**其他同盟組態**</span><span class="sxs-lookup"><span data-stu-id="880d5-134">**Other federation configuration**</span></span> | |
| [<span data-ttu-id="880d5-135">將多個 Azure AD 執行個體與單一 AD FS 執行個體同盟</span><span class="sxs-lookup"><span data-stu-id="880d5-135">Federate multiple instances of Azure AD with single instance of AD FS</span></span>](active-directory-aadconnectfed-single-adfs-multitenant-federation.md) | <span data-ttu-id="880d5-136">將多個 Azure AD 和單一 AD FS 伺服器陣列建立同盟關係</span><span class="sxs-lookup"><span data-stu-id="880d5-136">Federate multiple Azure AD with single AD FS farm</span></span>| 
| [<span data-ttu-id="880d5-137">新增自訂公司標誌/圖例</span><span class="sxs-lookup"><span data-stu-id="880d5-137">Add a custom company logo/illustration</span></span>](active-directory-aadconnect-federation-management.md#customlogo) |<span data-ttu-id="880d5-138">指定要顯示於 AD FS 登入頁面的自訂標誌來修改登入體驗。</span><span class="sxs-lookup"><span data-stu-id="880d5-138">Modify the sign-in experience by specifying the custom logo that is shown on the AD FS sign-in page.</span></span> |
| [<span data-ttu-id="880d5-139">新增登入說明</span><span class="sxs-lookup"><span data-stu-id="880d5-139">Add a sign-in description</span></span>](active-directory-aadconnect-federation-management.md#addsignindescription) |<span data-ttu-id="880d5-140">變更 AD FS 登入頁面上的登入說明。</span><span class="sxs-lookup"><span data-stu-id="880d5-140">Change the sign-in description on the AD FS sign-in page.</span></span> |
| [<span data-ttu-id="880d5-141">修改 AD FS 宣告規則</span><span class="sxs-lookup"><span data-stu-id="880d5-141">Modify AD FS claim rules</span></span>](active-directory-aadconnect-federation-management.md#modclaims) |<span data-ttu-id="880d5-142">修改或新增對應至 Azure AD Connect 同步組態之 AD FS 中的宣告規則。</span><span class="sxs-lookup"><span data-stu-id="880d5-142">Modify or add claim rules in AD FS that correspond to Azure AD Connect sync configuration.</span></span> |


## <a name="additional-resources"></a><span data-ttu-id="880d5-143">其他資源</span><span class="sxs-lookup"><span data-stu-id="880d5-143">Additional resources</span></span>
* [<span data-ttu-id="880d5-144">將兩個 Azure AD 和單一 AD FS 建立同盟關係</span><span class="sxs-lookup"><span data-stu-id="880d5-144">Federating two Azure AD with single AD FS</span></span>](active-directory-aadconnectfed-single-adfs-multitenant-federation.md)
* [<span data-ttu-id="880d5-145">Azure 中的 AD FS 部署</span><span class="sxs-lookup"><span data-stu-id="880d5-145">AD FS deployment in Azure</span></span>](active-directory-aadconnect-azure-adfs.md)
* [<span data-ttu-id="880d5-146">使用 Azure 流量管理員在 Azure 中部署高可用性跨地區 AD FS</span><span class="sxs-lookup"><span data-stu-id="880d5-146">High-availability cross-geographic AD FS deployment in Azure with Azure Traffic Manager</span></span>](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)
