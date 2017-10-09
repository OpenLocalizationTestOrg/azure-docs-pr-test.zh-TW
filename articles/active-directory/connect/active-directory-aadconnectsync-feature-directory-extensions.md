---
title: "Azure AD Connect 同步：目錄擴充 | Microsoft Docs"
description: "本主題說明在 Azure AD Connect 的 hello 目錄延伸模組功能。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="ab317-103">Azure AD Connect 同步處理：目錄擴充</span><span class="sxs-lookup"><span data-stu-id="ab317-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="ab317-104">目錄延伸模組可讓您 tooextend hello 結構描述在您自己的屬性從內部部署 Active Directory 與 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="ab317-104">Directory extensions allows you tooextend hello schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="ab317-105">這項功能可讓您 toobuild LOB 應用程式耗用繼續 toomanage 內部部署的屬性。</span><span class="sxs-lookup"><span data-stu-id="ab317-105">This feature allows you toobuild LOB apps consuming attributes you continue toomanage on-premises.</span></span> <span data-ttu-id="ab317-106">透過 [Azure AD Graph 目錄擴充](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)或 [Microsoft Graph](https://graph.microsoft.io/) 即可取用這些屬性。</span><span class="sxs-lookup"><span data-stu-id="ab317-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="ab317-107">您可以看到 hello 屬性可以透過[Azure AD Graph 總管](https://graphexplorer.cloudapp.net)和[Microsoft 圖表總管](https://graphexplorer2.azurewebsites.net/)分別。</span><span class="sxs-lookup"><span data-stu-id="ab317-107">You can see hello attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="ab317-108">目前沒有任何 Office 365 工作負載取用這些屬性。</span><span class="sxs-lookup"><span data-stu-id="ab317-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="ab317-109">您設定的其他屬性想 toosynchronize hello hello 安裝精靈 中的自訂設定路徑中。</span><span class="sxs-lookup"><span data-stu-id="ab317-109">You configure which additional attributes you want toosynchronize in hello custom settings path in hello installation wizard.</span></span>
<span data-ttu-id="ab317-110">![結構描述擴充精靈](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="ab317-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="ab317-111">hello 安裝顯示 hello 下列屬性，也就是有效的候選項目：</span><span class="sxs-lookup"><span data-stu-id="ab317-111">hello installation shows hello following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="ab317-112">使用者和群組物件類型</span><span class="sxs-lookup"><span data-stu-id="ab317-112">User and Group object types</span></span>
* <span data-ttu-id="ab317-113">單一值屬性︰字串、布林值、整數、二進位檔</span><span class="sxs-lookup"><span data-stu-id="ab317-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="ab317-114">多值屬性︰字串、二進位檔</span><span class="sxs-lookup"><span data-stu-id="ab317-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="ab317-115">hello 份屬性清單會從 Azure AD connect 的安裝期間建立的 hello 結構描述快取讀取。</span><span class="sxs-lookup"><span data-stu-id="ab317-115">hello list of attributes is read from hello schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="ab317-116">如果您已延伸 hello Active Directory 架構，與其他屬性，然後 hello[結構描述必須重新整理](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema)會顯示這些新的屬性之前。</span><span class="sxs-lookup"><span data-stu-id="ab317-116">If you have extended hello Active Directory schema with additional attributes, then hello [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="ab317-117">Azure AD 中的物件可以有 too100 目錄延伸模組屬性。</span><span class="sxs-lookup"><span data-stu-id="ab317-117">An object in Azure AD can have up too100 directory extensions attributes.</span></span> <span data-ttu-id="ab317-118">hello 長度上限是 250 個字元。</span><span class="sxs-lookup"><span data-stu-id="ab317-118">hello max length is 250 characters.</span></span> <span data-ttu-id="ab317-119">如果屬性值的長度，則會截斷 hello 同步處理引擎。</span><span class="sxs-lookup"><span data-stu-id="ab317-119">If an attribute value is longer, then it is truncated by hello sync engine.</span></span>

<span data-ttu-id="ab317-120">在 Azure AD Connect 安裝期間，會註冊可提供這些屬性的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab317-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="ab317-121">您可以看到這個 hello Azure 入口網站中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab317-121">You can see this application in hello Azure portal.</span></span>  
![結構描述擴充應用程式](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="ab317-123">現在可透過 Graph 提供這些屬性：</span><span class="sxs-lookup"><span data-stu-id="ab317-123">These attributes are now available through Graph:</span></span>  
![圖形](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="ab317-125">hello 屬性前面會加上副檔名\_{AppClientId}\_。</span><span class="sxs-lookup"><span data-stu-id="ab317-125">hello attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="ab317-126">hello AppClientId 有的 hello 相同 Azure AD 租用戶中的所有屬性的值。</span><span class="sxs-lookup"><span data-stu-id="ab317-126">hello AppClientId has hello same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab317-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ab317-127">Next steps</span></span>
<span data-ttu-id="ab317-128">深入了解 hello [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)組態。</span><span class="sxs-lookup"><span data-stu-id="ab317-128">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="ab317-129">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="ab317-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
