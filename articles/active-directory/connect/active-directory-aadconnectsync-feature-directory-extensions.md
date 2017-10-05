---
title: "Azure AD Connect 同步：目錄擴充 | Microsoft Docs"
description: "本主題說明 Azure AD Connect 中的目錄擴充功能。"
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
ms.openlocfilehash: 8ab9944437443a6d796345782f4f798aec96a0f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="e8b4b-103">Azure AD Connect 同步處理：目錄擴充</span><span class="sxs-lookup"><span data-stu-id="e8b4b-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="e8b4b-104">目錄擴充可讓您從內部部署 Active Directory 利用自己的屬性擴充 Azure AD 中的架構。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-104">Directory extensions allows you to extend the schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="e8b4b-105">此功能可讓您建置 LOB 應用程式來取用您在內部部署中持續進行管理的屬性。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-105">This feature allows you to build LOB apps consuming attributes you continue to manage on-premises.</span></span> <span data-ttu-id="e8b4b-106">透過 [Azure AD Graph 目錄擴充](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)或 [Microsoft Graph](https://graph.microsoft.io/) 即可取用這些屬性。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="e8b4b-107">若要查看可用的屬性，可分別使用 [Azure AD Graph 總管](https://graphexplorer.cloudapp.net)和 [Microsoft Graph 總管](https://graphexplorer2.azurewebsites.net/)。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-107">You can see the attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="e8b4b-108">目前沒有任何 Office 365 工作負載取用這些屬性。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="e8b4b-109">您可以在安裝精靈的自訂設定路徑中，設定您想要同步處理的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-109">You configure which additional attributes you want to synchronize in the custom settings path in the installation wizard.</span></span>
<span data-ttu-id="e8b4b-110">![結構描述擴充精靈](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="e8b4b-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="e8b4b-111">安裝會顯示下列屬性，這些都是有效的候選項目：</span><span class="sxs-lookup"><span data-stu-id="e8b4b-111">The installation shows the following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="e8b4b-112">使用者和群組物件類型</span><span class="sxs-lookup"><span data-stu-id="e8b4b-112">User and Group object types</span></span>
* <span data-ttu-id="e8b4b-113">單一值屬性︰字串、布林值、整數、二進位檔</span><span class="sxs-lookup"><span data-stu-id="e8b4b-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="e8b4b-114">多值屬性︰字串、二進位檔</span><span class="sxs-lookup"><span data-stu-id="e8b4b-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="e8b4b-115">屬性清單是從 Azure AD Connect 安裝期間建立的結構描述快取讀取。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-115">The list of attributes is read from the schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="e8b4b-116">如果您已使用其他屬性擴充 Active Directory 結構描述，則[必須重新整理結構描述](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) ，才可看見這些新屬性。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-116">If you have extended the Active Directory schema with additional attributes, then the [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="e8b4b-117">Azure AD 中的物件最多可有 100 個目錄擴充屬性。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-117">An object in Azure AD can have up to 100 directory extensions attributes.</span></span> <span data-ttu-id="e8b4b-118">長度上限是 250 個字元。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-118">The max length is 250 characters.</span></span> <span data-ttu-id="e8b4b-119">如果屬性值較長，則會被同步處理引擎截斷。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-119">If an attribute value is longer, then it is truncated by the sync engine.</span></span>

<span data-ttu-id="e8b4b-120">在 Azure AD Connect 安裝期間，會註冊可提供這些屬性的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="e8b4b-121">您可以在 Azure 入口網站中看到這個應用程式。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-121">You can see this application in the Azure portal.</span></span>  
![結構描述擴充應用程式](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="e8b4b-123">現在可透過 Graph 提供這些屬性：</span><span class="sxs-lookup"><span data-stu-id="e8b4b-123">These attributes are now available through Graph:</span></span>  
![圖形](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="e8b4b-125">屬性的前面會加上 extension\_{AppClientId}\_。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-125">The attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="e8b4b-126">Azure AD 租用戶中的所有屬性會有相同的 AppClientId 值。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-126">The AppClientId has the same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8b4b-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8b4b-127">Next steps</span></span>
<span data-ttu-id="e8b4b-128">深入了解 [Azure AD Connect 同步](active-directory-aadconnectsync-whatis.md) 組態。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-128">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="e8b4b-129">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="e8b4b-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
