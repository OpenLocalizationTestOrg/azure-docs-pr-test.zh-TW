---
title: "Microsoft Cloud Germany 中的 Azure AD Connect"
description: "Azure AD Connect 會整合您的內部部署目錄與 Azure Active Directory。 這可讓您為與 Azure AD 整合的 Office 365、Azure 和 SaaS 應用程式提供通用身分識別。"
keywords: "Azure AD Connect 簡介, Azure AD Connect 概觀, 何謂 Azure AD Connect, 安裝 active directory, 德國, 黑森林"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4c55b116c0dc080ae316caca873a7b693caa793b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="d0bff-105">Microsoft Cloud Germany 中的 Azure AD Connect - 公開預覽</span><span class="sxs-lookup"><span data-stu-id="d0bff-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="d0bff-106">簡介</span><span class="sxs-lookup"><span data-stu-id="d0bff-106">Introduction</span></span>
<span data-ttu-id="d0bff-107">Azure AD Connect 可進行內部部署 Active Directory 與 Azure Active Directory 之間的同步處理。</span><span class="sxs-lookup"><span data-stu-id="d0bff-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="d0bff-108">[Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) 中目前有許多案例必須由操作員來完成。</span><span class="sxs-lookup"><span data-stu-id="d0bff-108">Currently, many of the scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by the operator.</span></span> <span data-ttu-id="d0bff-109">使用 Microsoft Cloud Germany 時，您必須注意下列事項︰</span><span class="sxs-lookup"><span data-stu-id="d0bff-109">When using Microsoft Cloud Germany, you must be aware of the following:</span></span>

* <span data-ttu-id="d0bff-110">下列 URL 必須在 Proxy 伺服器上開啟，才能成功進行同步處理：</span><span class="sxs-lookup"><span data-stu-id="d0bff-110">The following URLs must be opened on a proxy server for synchronization to occur successfully:</span></span>
  
  * <span data-ttu-id="d0bff-111">*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="d0bff-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="d0bff-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="d0bff-112">*.windows.net</span></span>
  * * <span data-ttu-id="d0bff-113">憑證撤銷清單</span><span class="sxs-lookup"><span data-stu-id="d0bff-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="d0bff-114">當您登入 Azure AD 目錄時，必須使用 onmicrosoft.de 網域中的帳戶。</span><span class="sxs-lookup"><span data-stu-id="d0bff-114">When you sign in to your Azure AD directory, you must use an account in the onmicrosoft.de domain.</span></span>
* <span data-ttu-id="d0bff-115">無法使用下列功能：</span><span class="sxs-lookup"><span data-stu-id="d0bff-115">The following features are not available:</span></span>
  * <span data-ttu-id="d0bff-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="d0bff-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="d0bff-117">自動更新</span><span class="sxs-lookup"><span data-stu-id="d0bff-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="d0bff-118">下載</span><span class="sxs-lookup"><span data-stu-id="d0bff-118">Download</span></span>
<span data-ttu-id="d0bff-119">您可以從入口網站中的 [Azure AD Connect] 刀鋒視窗下載 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="d0bff-119">You can download Azure AD Connect from the Azure AD Connect blade within the portal.</span></span>  <span data-ttu-id="d0bff-120">使用下列指示來尋找 Azure AD Connect 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d0bff-120">Use the instructions below to locate the Azure AD Connect blade.</span></span>

### <a name="the-azure-ad-connect-blade"></a><span data-ttu-id="d0bff-121">Azure AD Connect 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="d0bff-121">The Azure AD Connect Blade</span></span>
<span data-ttu-id="d0bff-122">登入 Azure 入口網站後，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d0bff-122">Once you have signed in to the Azure portal, do the following:</span></span>

1. <span data-ttu-id="d0bff-123">移至瀏覽</span><span class="sxs-lookup"><span data-stu-id="d0bff-123">Go to Browse</span></span>
2. <span data-ttu-id="d0bff-124">選取 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0bff-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="d0bff-125">然後選取 Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="d0bff-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="d0bff-126">您應該會看見下列內容：</span><span class="sxs-lookup"><span data-stu-id="d0bff-126">You should see the following:</span></span>

![Azure AD Connect 刀鋒視窗](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="d0bff-128">下表描述刀鋒視窗中顯示的功能。</span><span class="sxs-lookup"><span data-stu-id="d0bff-128">The following table describes the features shown in the blade.</span></span>

| <span data-ttu-id="d0bff-129">課程名稱</span><span class="sxs-lookup"><span data-stu-id="d0bff-129">Title</span></span> | <span data-ttu-id="d0bff-130">說明</span><span class="sxs-lookup"><span data-stu-id="d0bff-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d0bff-131">同步處理狀態</span><span class="sxs-lookup"><span data-stu-id="d0bff-131">SYNC STATUS</span></span> |<span data-ttu-id="d0bff-132">讓您知道已啟用或停用同步處理。</span><span class="sxs-lookup"><span data-stu-id="d0bff-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="d0bff-133">上次同步處理</span><span class="sxs-lookup"><span data-stu-id="d0bff-133">LAST SYNC</span></span> |<span data-ttu-id="d0bff-134">上次成功完成同步處理。</span><span class="sxs-lookup"><span data-stu-id="d0bff-134">The last time a successful sync completed.</span></span> |
| <span data-ttu-id="d0bff-135">同盟網域</span><span class="sxs-lookup"><span data-stu-id="d0bff-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="d0bff-136">顯示目前設定的同盟網域數目。</span><span class="sxs-lookup"><span data-stu-id="d0bff-136">Shows the number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="d0bff-137">安裝</span><span class="sxs-lookup"><span data-stu-id="d0bff-137">Installation</span></span>
<span data-ttu-id="d0bff-138">若要安裝 Azure AD Connect，您可以使用 [這裡](active-directory-aadconnect.md#install-azure-ad-connect)的文件。</span><span class="sxs-lookup"><span data-stu-id="d0bff-138">To install Azure AD Connect, you can use the documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="d0bff-139">進階功能和其他資訊</span><span class="sxs-lookup"><span data-stu-id="d0bff-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="d0bff-140">如需自訂設定或進階組態的其他資訊和指引，請從 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)著手。</span><span class="sxs-lookup"><span data-stu-id="d0bff-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="d0bff-141">此頁面會提供其他指引的資訊和連結。</span><span class="sxs-lookup"><span data-stu-id="d0bff-141">This page provides information and links to additional guidance.</span></span>

