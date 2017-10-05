---
title: "如何設定應用程式 Proxy 應用程式以使用 PingAccess | Microsoft Docs"
description: "了解如何使用 PingAccess 以利用標頭形式驗證，將應用程式 Proxy 的優點延伸到應用程式"
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
ms.openlocfilehash: a9da67373465cebbdbecae5c8fb8bd0a0ee3c171
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application-to-use-pingaccess"></a><span data-ttu-id="681f1-103">如何設定應用程式 Proxy 應用程式以使用 PingAccess</span><span class="sxs-lookup"><span data-stu-id="681f1-103">How to configure an Application Proxy application to use PingAccess</span></span>

<span data-ttu-id="681f1-104">我們與 PingAccess 的合作，使您現在可以使用標頭形式驗證，將應用程式 Proxy 的優點延伸到應用程式。</span><span class="sxs-lookup"><span data-stu-id="681f1-104">Our collaboration with PingAccess now allows you to extend the benefits of Application Proxy to applications using header-based authentication.</span></span> <span data-ttu-id="681f1-105">如果您的應用程式不使用標頭，請參閱我們的[單一登入文件](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)以取得其他選項的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="681f1-105">If your applications do not use headers, see our [Single Sign-On documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) for details on other options.</span></span>

## <a name="overview-of-steps-and-recommended-documents"></a><span data-ttu-id="681f1-106">步驟和建議文件的概觀</span><span class="sxs-lookup"><span data-stu-id="681f1-106">Overview of steps and recommended documents</span></span>

<span data-ttu-id="681f1-107">若要搭配 PingAccess 設定應用程式，請執行四個步驟：</span><span class="sxs-lookup"><span data-stu-id="681f1-107">To configure an application with PingAccess, there are four steps:</span></span>

1.  <span data-ttu-id="681f1-108">設定應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="681f1-108">Configure Application Proxy Connectors</span></span>

2.  <span data-ttu-id="681f1-109">建立 Azure AD 應用程式 Proxy 應用程式</span><span class="sxs-lookup"><span data-stu-id="681f1-109">Create an Azure AD Application Proxy Application</span></span>

3.  <span data-ttu-id="681f1-110">下載及設定 PingAccess</span><span class="sxs-lookup"><span data-stu-id="681f1-110">Download & Configure PingAccess</span></span>

4.  <span data-ttu-id="681f1-111">在 PingAccess 中設定應用程式</span><span class="sxs-lookup"><span data-stu-id="681f1-111">Configure Applications in PingAccess</span></span>

<span data-ttu-id="681f1-112">如需上述每個步驟的詳細資訊，請參閱我們的[搭配標頭的單一登入文件](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access)。</span><span class="sxs-lookup"><span data-stu-id="681f1-112">For details on each of these steps, see our [Single Sign-On with Headers documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span></span>
