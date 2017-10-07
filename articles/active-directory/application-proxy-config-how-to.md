---
title: "aaaHow tooconfigure 應用程式 Proxy 應用程式 |Microsoft 文件"
description: "深入了解如何 toocreate 設定應用程式 Proxy 中的應用程式一些簡單的步驟"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a><span data-ttu-id="14e8d-103">如何 tooconfigure 應用程式 Proxy 應用程式</span><span class="sxs-lookup"><span data-stu-id="14e8d-103">How tooconfigure an Application Proxy application</span></span>

<span data-ttu-id="14e8d-104">本文將協助您 toounderstand 如何 tooconfigure tooexpose Azure AD 應用程式 Proxy 應用程式在內部部署應用程式 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="14e8d-104">This article help you toounderstand how tooconfigure an Application Proxy application within Azure AD tooexpose your on-premises applications toohello cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="14e8d-105">建議的文件</span><span class="sxs-lookup"><span data-stu-id="14e8d-105">Recommended documents</span></span> 

<span data-ttu-id="14e8d-106">hello 初始設定及應用程式 Proxy 應用程式透過 hello 管理員入口網站中建立相關 toolearn 遵循 hello[使用 Azure AD Application Proxy 發行應用程式](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="14e8d-106">toolearn about hello initial configurations and creation of an Application Proxy application through hello Admin Portal, follow hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="14e8d-107">如需有關設定連接器的詳細資訊，請參閱[hello Azure 入口網站中啟用應用程式 Proxy](active-directory-application-proxy-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="14e8d-107">For details on configuring Connectors, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="14e8d-108">如需上傳憑證和使用自訂網域的詳細資訊，請參閱[使用 Azure AD 應用程式 Proxy 中的自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)。</span><span class="sxs-lookup"><span data-stu-id="14e8d-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-hello-applicationsetting-hello-urls"></a><span data-ttu-id="14e8d-109">建立 hello 應用程式/設定 hello Url</span><span class="sxs-lookup"><span data-stu-id="14e8d-109">Create hello Application/Setting hello URLs</span></span>

<span data-ttu-id="14e8d-110">如果您要遵照 hello 步驟 hello[使用 Azure AD Application Proxy 發行應用程式](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)文件且 hello 錯誤詳細資料的資訊和建議的方式取得錯誤建立 hello 應用程式，請參閱toofix hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="14e8d-110">If you are following hello steps in hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="14e8d-111">大部分的錯誤訊息都包含建議的修正。</span><span class="sxs-lookup"><span data-stu-id="14e8d-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="14e8d-112">tooavoid 常見的錯誤，請確認：</span><span class="sxs-lookup"><span data-stu-id="14e8d-112">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="14e8d-113">您是系統管理員的權限 toocreate 應用程式 Proxy 應用程式</span><span class="sxs-lookup"><span data-stu-id="14e8d-113">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="14e8d-114">是唯一的 hello 內部 URL</span><span class="sxs-lookup"><span data-stu-id="14e8d-114">hello internal URL is unique</span></span>

-   <span data-ttu-id="14e8d-115">hello 外部 URL 是唯一的</span><span class="sxs-lookup"><span data-stu-id="14e8d-115">hello external URL is unique</span></span>

-   <span data-ttu-id="14e8d-116">hello http 或 https 的 Url 開頭和結尾為"/"</span><span class="sxs-lookup"><span data-stu-id="14e8d-116">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="14e8d-117">hello URL 應該是網域名稱，不是 IP 位址</span><span class="sxs-lookup"><span data-stu-id="14e8d-117">hello URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="14e8d-118">當您建立 hello 應用程式時應該顯示 hello 右上角 hello 錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="14e8d-118">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="14e8d-119">您也可以選取 hello 通知圖示 toosee hello 錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="14e8d-119">You can also select hello notification icon toosee hello error messages.</span></span>

   ![通知提示](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="14e8d-121">設定連接器/連接器群組</span><span class="sxs-lookup"><span data-stu-id="14e8d-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="14e8d-122">如果您無法設定您的應用程式，因為 hello 連接器與連接器群組的相關警告，請參閱指示啟用應用程式 Proxy 的詳細資料 toodownload 連接器。</span><span class="sxs-lookup"><span data-stu-id="14e8d-122">If you are having difficulty configuring your application because of warning about hello connectors and connector groups, see instructions on enabling Application Proxy for details on how toodownload connectors.</span></span> <span data-ttu-id="14e8d-123">如果您想深入了解連接器 toolearn，請參閱 hello[連接器文件](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors)。</span><span class="sxs-lookup"><span data-stu-id="14e8d-123">If you want toolearn more about connectors, see hello [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="14e8d-124">如果您的連接器處於非使用狀態，這表示它們是無法 tooreach hello 服務。</span><span class="sxs-lookup"><span data-stu-id="14e8d-124">If your connectors are inactive, this means that they are unable tooreach hello service.</span></span> <span data-ttu-id="14e8d-125">這通常是因為 hello 所需的所有連接埠未開啟。</span><span class="sxs-lookup"><span data-stu-id="14e8d-125">This is often because all hello required ports are not open.</span></span> <span data-ttu-id="14e8d-126">toosee 必要的連接埠的清單，請參閱啟用應用程式 Proxy 的文件的 hello hello 必要條件一節。</span><span class="sxs-lookup"><span data-stu-id="14e8d-126">toosee a list of required ports, see hello pre-requisites section of hello enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="14e8d-127">上傳自訂網域的憑證</span><span class="sxs-lookup"><span data-stu-id="14e8d-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="14e8d-128">自訂網域可讓您對外部 Url 的 toospecify hello 網域。</span><span class="sxs-lookup"><span data-stu-id="14e8d-128">Custom Domains allow you toospecify hello domain of your external URLs.</span></span> <span data-ttu-id="14e8d-129">toouse 自訂網域，您會需要 tooupload hello 憑證該網域。</span><span class="sxs-lookup"><span data-stu-id="14e8d-129">toouse custom domains, you need tooupload hello certificate for that domain.</span></span> <span data-ttu-id="14e8d-130">如需使用自訂網域和憑證的詳細資訊，請參閱[使用 Azure AD 應用程式 Proxy 中的自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)。</span><span class="sxs-lookup"><span data-stu-id="14e8d-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="14e8d-131">如果您遇到問題上, 傳您的憑證，尋找 hello hello hello hello 憑證問題的其他資訊的入口網站中的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="14e8d-131">If you are encountering issues uploading your certificate, look for hello error messages in hello portal for additional information on hello problem with hello certificate.</span></span> <span data-ttu-id="14e8d-132">常見的憑證問題包括：</span><span class="sxs-lookup"><span data-stu-id="14e8d-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="14e8d-133">過期的憑證</span><span class="sxs-lookup"><span data-stu-id="14e8d-133">Expired certificate</span></span>

-   <span data-ttu-id="14e8d-134">憑證為自我簽署</span><span class="sxs-lookup"><span data-stu-id="14e8d-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="14e8d-135">遺漏 hello 私密金鑰憑證。</span><span class="sxs-lookup"><span data-stu-id="14e8d-135">Certificate is missing hello private key</span></span>

<span data-ttu-id="14e8d-136">在右下角，當您嘗試 tooupload hello 憑證 hello 最佳 hello 錯誤訊息顯示。</span><span class="sxs-lookup"><span data-stu-id="14e8d-136">hello error message display in hello top right corner as you try tooupload hello certificate.</span></span> <span data-ttu-id="14e8d-137">您也可以選取 hello 通知圖示 toosee hello 錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="14e8d-137">You can also select hello notification icon toosee hello error messages.</span></span>

   ![通知提示](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="14e8d-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14e8d-139">Next steps</span></span>
[<span data-ttu-id="14e8d-140">使用 Azure AD 應用程式 Proxy 發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="14e8d-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
