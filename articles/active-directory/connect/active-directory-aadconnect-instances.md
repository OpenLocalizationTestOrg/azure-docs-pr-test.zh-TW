---
title: "Azure AD Connect︰同步服務執行個體 | Microsoft Docs"
description: "本頁記載 Azure AD 執行個體的特殊考量。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e8321c3d16253226a5931cacbce6fa5d50b697bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="cfc43-103">Azure AD Connect：執行個體的特殊考量</span><span class="sxs-lookup"><span data-stu-id="cfc43-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="cfc43-104">Azure AD Connect 最常搭配 Azure AD 和 Office 365 的全球執行個體。</span><span class="sxs-lookup"><span data-stu-id="cfc43-104">Azure AD Connect is most commonly used with the world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="cfc43-105">但還有其他執行個體，而它們有不同的 URL 需求和其他特殊考量。</span><span class="sxs-lookup"><span data-stu-id="cfc43-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="cfc43-106">Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="cfc43-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="cfc43-107">[Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) 是由德國資料信託所運作的最高雲端。</span><span class="sxs-lookup"><span data-stu-id="cfc43-107">The [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="cfc43-108">要在 Proxy 伺服器中開啟的 URL</span><span class="sxs-lookup"><span data-stu-id="cfc43-108">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="cfc43-109">\*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="cfc43-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="cfc43-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="cfc43-110">\*.windows.net</span></span> |
| <span data-ttu-id="cfc43-111">+憑證撤銷清單</span><span class="sxs-lookup"><span data-stu-id="cfc43-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="cfc43-112">當您登入 Azure AD 租用戶時，必須使用 onmicrosoft.de 網域中的帳戶。</span><span class="sxs-lookup"><span data-stu-id="cfc43-112">When you sign in to your Azure AD tenant, you must use an account in the onmicrosoft.de domain.</span></span>

<span data-ttu-id="cfc43-113">Microsoft Cloud Germany 目前沒有的功能︰</span><span class="sxs-lookup"><span data-stu-id="cfc43-113">Features currently not present in the Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="cfc43-114">無法使用 **Azure AD Connect Health**。</span><span class="sxs-lookup"><span data-stu-id="cfc43-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="cfc43-115">無法使用「自動更新」。</span><span class="sxs-lookup"><span data-stu-id="cfc43-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="cfc43-116">**密碼回寫**適用於 Azure AD Connect 1.1.570.0 預覽版本和更新的版本。</span><span class="sxs-lookup"><span data-stu-id="cfc43-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="cfc43-117">無法使用其他 Azure AD Premium 服務。</span><span class="sxs-lookup"><span data-stu-id="cfc43-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="cfc43-118">Microsoft Azure Government 雲端</span><span class="sxs-lookup"><span data-stu-id="cfc43-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="cfc43-119">[Microsoft Azure Government 雲端](https://azure.microsoft.com/features/gov/) 是用於美國政府的雲端。</span><span class="sxs-lookup"><span data-stu-id="cfc43-119">The [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="cfc43-120">此雲端是以舊版的 DirSync 提供支援。</span><span class="sxs-lookup"><span data-stu-id="cfc43-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="cfc43-121">從 Azure AD Connect 組建 1.1.180 起，即支援新一代的雲端。</span><span class="sxs-lookup"><span data-stu-id="cfc43-121">From build 1.1.180 of Azure AD Connect, the next generation of the cloud is supported.</span></span> <span data-ttu-id="cfc43-122">這一代使用僅限美國的端點，而且有不同的 URL 清單要在您的 Proxy 伺服器中開啟。</span><span class="sxs-lookup"><span data-stu-id="cfc43-122">This generation is using US-only based endpoints and have a different list of URLs to open in your proxy server.</span></span>

| <span data-ttu-id="cfc43-123">要在 Proxy 伺服器中開啟的 URL</span><span class="sxs-lookup"><span data-stu-id="cfc43-123">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="cfc43-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="cfc43-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="cfc43-125">\*.microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="cfc43-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="cfc43-126">\*.gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="cfc43-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="cfc43-127">+憑證撤銷清單</span><span class="sxs-lookup"><span data-stu-id="cfc43-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="cfc43-128">Azure AD Connect 無法自動偵測您的 Azure AD 租用戶是否位於 Government 雲端。</span><span class="sxs-lookup"><span data-stu-id="cfc43-128">Azure AD Connect is not able to automatically detect that your Azure AD tenant is located in the Government cloud.</span></span> <span data-ttu-id="cfc43-129">而您在安裝 Azure AD Connect 時需要採取下列動作。</span><span class="sxs-lookup"><span data-stu-id="cfc43-129">Instead you need to take the following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="cfc43-130">開始 Azure AD Connect 安裝。</span><span class="sxs-lookup"><span data-stu-id="cfc43-130">Start the Azure AD Connect installation.</span></span>
2. <span data-ttu-id="cfc43-131">當您看見您應在其中接受 EULA 的第一頁時，請勿繼續進行，但讓安裝精靈保持執行。</span><span class="sxs-lookup"><span data-stu-id="cfc43-131">When you see the first page where you are supposed to accept the EULA, do not continue but leave the installation wizard running.</span></span>
3. <span data-ttu-id="cfc43-132">啟動 regedit 並將登錄機碼 `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` 變更為 `2` 值。</span><span class="sxs-lookup"><span data-stu-id="cfc43-132">Start regedit and change the registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` to the value `2`.</span></span>
4. <span data-ttu-id="cfc43-133">回到 Azure AD Connect 安裝精靈，接受 EULA 並繼續進行。</span><span class="sxs-lookup"><span data-stu-id="cfc43-133">Go back to the Azure AD Connect installation wizard, accept the EULA, and continue.</span></span> <span data-ttu-id="cfc43-134">在安裝期間，務必使用 **自訂組態** 安裝路徑 (而非快速安裝)。</span><span class="sxs-lookup"><span data-stu-id="cfc43-134">During installation, make sure to use the **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="cfc43-135">然後如往常一樣繼續安裝。</span><span class="sxs-lookup"><span data-stu-id="cfc43-135">Then continue the installation as usual.</span></span>

<span data-ttu-id="cfc43-136">Microsoft Azure Government 雲端目前沒有的功能︰</span><span class="sxs-lookup"><span data-stu-id="cfc43-136">Features currently not present in the Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="cfc43-137">無法使用 **Azure AD Connect Health**。</span><span class="sxs-lookup"><span data-stu-id="cfc43-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="cfc43-138">無法使用「自動更新」。</span><span class="sxs-lookup"><span data-stu-id="cfc43-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="cfc43-139">**密碼回寫**適用於 Azure AD Connect 1.1.570.0 預覽版本和更新的版本。</span><span class="sxs-lookup"><span data-stu-id="cfc43-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="cfc43-140">無法使用其他 Azure AD Premium 服務。</span><span class="sxs-lookup"><span data-stu-id="cfc43-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfc43-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cfc43-141">Next steps</span></span>
<span data-ttu-id="cfc43-142">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="cfc43-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
