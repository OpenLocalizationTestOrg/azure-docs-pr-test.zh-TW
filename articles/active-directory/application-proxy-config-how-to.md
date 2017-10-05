---
title: "如何設定應用程式 Proxy 應用程式 | Microsoft Docs"
description: "了解如何使用幾個簡單步驟來建立及設定應用程式 Proxy 應用程式"
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
ms.openlocfilehash: c8f98536048a85ebb3f061d840457130579196d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application"></a><span data-ttu-id="89c94-103">如何設定應用程式 Proxy 應用程式</span><span class="sxs-lookup"><span data-stu-id="89c94-103">How to configure an Application Proxy application</span></span>

<span data-ttu-id="89c94-104">本文協助您了解如何在 Azure AD 內設定應用程式 Proxy 應用程式，以向雲端公開您的內部部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="89c94-104">This article help you to understand how to configure an Application Proxy application within Azure AD to expose your on-premises applications to the cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="89c94-105">建議的文件</span><span class="sxs-lookup"><span data-stu-id="89c94-105">Recommended documents</span></span> 

<span data-ttu-id="89c94-106">若要深入了解應用程式 Proxy 應用程式透過管理入口網站的初始設定與建立，請遵循[使用 Azure AD 應用程式 Proxy 發佈應用程式](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="89c94-106">To learn about the initial configurations and creation of an Application Proxy application through the Admin Portal, follow the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="89c94-107">如需設定連接器的詳細資料，請參閱[在 Azure 入口網站中啟用應用程式 Proxy](active-directory-application-proxy-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="89c94-107">For details on configuring Connectors, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="89c94-108">如需上傳憑證和使用自訂網域的詳細資訊，請參閱[使用 Azure AD 應用程式 Proxy 中的自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)。</span><span class="sxs-lookup"><span data-stu-id="89c94-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-the-applicationsetting-the-urls"></a><span data-ttu-id="89c94-109">建立應用程式/設定 URL</span><span class="sxs-lookup"><span data-stu-id="89c94-109">Create the Application/Setting the URLs</span></span>

<span data-ttu-id="89c94-110">如果您依照[使用 Azure AD 應用程式 Proxy 發佈應用程式](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)文件中的步驟，並在建立應用程式時發生錯誤，請查看錯誤詳細資料，以取得修正應用程式的資訊及建議。</span><span class="sxs-lookup"><span data-stu-id="89c94-110">If you are following the steps in the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="89c94-111">大部分的錯誤訊息都包含建議的修正。</span><span class="sxs-lookup"><span data-stu-id="89c94-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="89c94-112">若要避免常見的錯誤，請確認：</span><span class="sxs-lookup"><span data-stu-id="89c94-112">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="89c94-113">您是具有建立應用程式 Proxy 應用程式權限的系統管理員</span><span class="sxs-lookup"><span data-stu-id="89c94-113">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="89c94-114">內部 URL 是唯一的</span><span class="sxs-lookup"><span data-stu-id="89c94-114">The internal URL is unique</span></span>

-   <span data-ttu-id="89c94-115">外部 URL 是唯一的</span><span class="sxs-lookup"><span data-stu-id="89c94-115">The external URL is unique</span></span>

-   <span data-ttu-id="89c94-116">URL 開頭為 http 或 https，且結尾為 “/”</span><span class="sxs-lookup"><span data-stu-id="89c94-116">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="89c94-117">URL 應該是網域名稱，而非 IP 位址</span><span class="sxs-lookup"><span data-stu-id="89c94-117">The URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="89c94-118">當您建立應用程式時，錯誤訊息應該會在右上角顯示。</span><span class="sxs-lookup"><span data-stu-id="89c94-118">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="89c94-119">您也可以選取通知圖示來查看錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="89c94-119">You can also select the notification icon to see the error messages.</span></span>

   ![通知提示](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="89c94-121">設定連接器/連接器群組</span><span class="sxs-lookup"><span data-stu-id="89c94-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="89c94-122">如果您因為連接器和連接器群組的警告而無法設定應用程式，請參閱啟用應用程式 Proxy 的指示，以取得下載連接器的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="89c94-122">If you are having difficulty configuring your application because of warning about the connectors and connector groups, see instructions on enabling Application Proxy for details on how to download connectors.</span></span> <span data-ttu-id="89c94-123">如果您想要深入了解連接器，請參閱[連接器文件](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors)。</span><span class="sxs-lookup"><span data-stu-id="89c94-123">If you want to learn more about connectors, see the [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="89c94-124">如果您的連接器處於非作用中狀態，這表示它們無法連線到服務。</span><span class="sxs-lookup"><span data-stu-id="89c94-124">If your connectors are inactive, this means that they are unable to reach the service.</span></span> <span data-ttu-id="89c94-125">這通常是因為沒有開啟所有必要的連接埠。</span><span class="sxs-lookup"><span data-stu-id="89c94-125">This is often because all the required ports are not open.</span></span> <span data-ttu-id="89c94-126">若要查看必要連接埠的清單，請參閱《啟用應用程式 Proxy》文件的＜必要條件＞一節。</span><span class="sxs-lookup"><span data-stu-id="89c94-126">To see a list of required ports, see the pre-requisites section of the enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="89c94-127">上傳自訂網域的憑證</span><span class="sxs-lookup"><span data-stu-id="89c94-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="89c94-128">自訂網域可讓您指定外部 URL 的網域。</span><span class="sxs-lookup"><span data-stu-id="89c94-128">Custom Domains allow you to specify the domain of your external URLs.</span></span> <span data-ttu-id="89c94-129">若要使用自訂網域，您需要上傳該網域的憑證。</span><span class="sxs-lookup"><span data-stu-id="89c94-129">To use custom domains, you need to upload the certificate for that domain.</span></span> <span data-ttu-id="89c94-130">如需使用自訂網域和憑證的詳細資訊，請參閱[使用 Azure AD 應用程式 Proxy 中的自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)。</span><span class="sxs-lookup"><span data-stu-id="89c94-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="89c94-131">如果您在上傳憑證時遇到問題，請尋找入口網站中的錯誤訊息以取得憑證問題的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="89c94-131">If you are encountering issues uploading your certificate, look for the error messages in the portal for additional information on the problem with the certificate.</span></span> <span data-ttu-id="89c94-132">常見的憑證問題包括：</span><span class="sxs-lookup"><span data-stu-id="89c94-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="89c94-133">過期的憑證</span><span class="sxs-lookup"><span data-stu-id="89c94-133">Expired certificate</span></span>

-   <span data-ttu-id="89c94-134">憑證為自我簽署</span><span class="sxs-lookup"><span data-stu-id="89c94-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="89c94-135">憑證沒有私密金鑰</span><span class="sxs-lookup"><span data-stu-id="89c94-135">Certificate is missing the private key</span></span>

<span data-ttu-id="89c94-136">當您嘗試上傳憑證時，錯誤訊息會顯示在右上角。</span><span class="sxs-lookup"><span data-stu-id="89c94-136">The error message display in the top right corner as you try to upload the certificate.</span></span> <span data-ttu-id="89c94-137">您也可以選取通知圖示來查看錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="89c94-137">You can also select the notification icon to see the error messages.</span></span>

   ![通知提示](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="89c94-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="89c94-139">Next steps</span></span>
[<span data-ttu-id="89c94-140">使用 Azure AD 應用程式 Proxy 發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="89c94-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
