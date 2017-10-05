---
title: "使用 Azure AD 應用程式 Proxy 登入內部部署應用程式時遇到問題 | Microsoft Docs"
description: "針對無法使用 Azure AD 應用程式 Proxy 登入與 Azure AD 整合的內部部署應用程式時的常見問題進行疑難排解"
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
ms.openlocfilehash: 5687f789355cc9769d26b53e98486bb213c66419
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-on-premises-application-using-the-azure-ad-application-proxy"></a><span data-ttu-id="f6eba-103">使用 Azure AD 應用程式 Proxy 登入內部部署應用程式時遇到問題</span><span class="sxs-lookup"><span data-stu-id="f6eba-103">Problems signing in to an on-premises application using the Azure AD application proxy</span></span>

<span data-ttu-id="f6eba-104">如果您無法登入內部部署應用程式，您可以嘗試下列步驟來解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="f6eba-104">If you are having problems signing in an on-premises application, you can try following the steps below to resolving your problem.</span></span>

## <a name="i-can-load-my-application-but-something-on-the-page-looks-broken"></a><span data-ttu-id="f6eba-105">我可以載入應用程式，但頁面上的某些內容看起來支離破碎</span><span class="sxs-lookup"><span data-stu-id="f6eba-105">I can load my application, but something on the page looks broken</span></span>

<span data-ttu-id="f6eba-106">下列文件可協助您解決此類別的一些最常見問題。</span><span class="sxs-lookup"><span data-stu-id="f6eba-106">The following documents can help you to resolve some of the most common issues in this category.</span></span>

  * [<span data-ttu-id="f6eba-107">我可以取得我的應用程式，但應用程式頁面未正確顯示</span><span class="sxs-lookup"><span data-stu-id="f6eba-107">I can get to my application, but the application page isn't displaying correctly</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-page-appearance-broken-problem/)
  * [<span data-ttu-id="f6eba-108">我可以取得我的應用程式，但應用程式的載入時間過久</span><span class="sxs-lookup"><span data-stu-id="f6eba-108">I can get to my application, but the application takes too long to load</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-page-load-speed-problem/)
  * [<span data-ttu-id="f6eba-109">我可以取得我的應用程式，但應用程式頁面上的連結無法作用</span><span class="sxs-lookup"><span data-stu-id="f6eba-109">I can get to my application, but the links on the application page do not work</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-page-links-broken-problem/)

## <a name="im-having-a-connectivity-problem-my-application"></a><span data-ttu-id="f6eba-110">我的應用程式在連線時遇到問題</span><span class="sxs-lookup"><span data-stu-id="f6eba-110">I'm having a connectivity problem my application</span></span>
  <span data-ttu-id="f6eba-111">下列文件可協助您解決此類別的一些最常見問題。</span><span class="sxs-lookup"><span data-stu-id="f6eba-111">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="f6eba-112">我不知道要為我的應用程式開啟哪些連接埠</span><span class="sxs-lookup"><span data-stu-id="f6eba-112">I don't know what ports to open for my application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-connectivity-ports-how-to/)
  * [<span data-ttu-id="f6eba-113">我遇到問題，連接器群組中沒有作用中的連接器可用於我的應用程式</span><span class="sxs-lookup"><span data-stu-id="f6eba-113">I encountered a problem because there was no working connector in a connector group for my application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-connectivity-no-working-connector/)

## <a name="im-having-a-problem-configuring-the-azure-ad-application-proxy-in-the-admin-portal"></a><span data-ttu-id="f6eba-114">我在管理入口網站中設定 Azure AD 應用程式 Proxy 時遇到問題</span><span class="sxs-lookup"><span data-stu-id="f6eba-114">I'm having a problem configuring the Azure AD Application Proxy in the admin portal</span></span>
  <span data-ttu-id="f6eba-115">下列文件可協助您解決此類別的一些最常見問題。</span><span class="sxs-lookup"><span data-stu-id="f6eba-115">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="f6eba-116">我無法設定使用應用程式 Proxy 的應用程式</span><span class="sxs-lookup"><span data-stu-id="f6eba-116">I am having difficulty configuring an application Proxy application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-config-how-to/)
  * [<span data-ttu-id="f6eba-117">我不知道如何為使用應用程式 Proxy 的應用程式設定單一登入</span><span class="sxs-lookup"><span data-stu-id="f6eba-117">I don't know how to configure single sign-on to my application Proxy application</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-config-sso-how-to/)
  * [<span data-ttu-id="f6eba-118">我在管理入口網站中建立我的應用程式時遇到問題</span><span class="sxs-lookup"><span data-stu-id="f6eba-118">I encountered a problem when creating my application in admin portal</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-config-problem/)

## <a name="im-having-a-problem-setting-up-back-end-authentication-to-my-application"></a><span data-ttu-id="f6eba-119">我在為應用程式設定後端驗證時遇到問題</span><span class="sxs-lookup"><span data-stu-id="f6eba-119">I'm having a problem setting up back-end authentication to my application</span></span>
  <span data-ttu-id="f6eba-120">下列文件可協助您解決此類別的一些最常見問題。</span><span class="sxs-lookup"><span data-stu-id="f6eba-120">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="f6eba-121">我不知道如何設定 Kerberos 限制委派</span><span class="sxs-lookup"><span data-stu-id="f6eba-121">I don't know how to configure Kerberos Constrained Delegation</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-back-end-kerberos-constrained-delegation-how-to/)
  * [<span data-ttu-id="f6eba-122">我不知道如何使用 PingAccess 設定我的應用程式</span><span class="sxs-lookup"><span data-stu-id="f6eba-122">I don't know how to configure my application with PingAccess</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-back-end-ping-access-how-to/)

## <a name="im-having-a-problem-when-signing-in-to-my-application"></a><span data-ttu-id="f6eba-123">我在登入應用程式時遇到問題</span><span class="sxs-lookup"><span data-stu-id="f6eba-123">I'm having a problem when signing in to my application</span></span>
  <span data-ttu-id="f6eba-124">下列文件可協助您解決此類別的一些最常見問題。</span><span class="sxs-lookup"><span data-stu-id="f6eba-124">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="f6eba-125">我收到「無法存取此公司應用程式」的錯誤</span><span class="sxs-lookup"><span data-stu-id="f6eba-125">I get a "Can't Access this Corporate Application" error</span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-sign-in-bad-gateway-timeout-error/)

## <a name="im-having-a-problem-with-the-application-proxy-agent-connector"></a><span data-ttu-id="f6eba-126">我在使用應用程式 Proxy 代理程式連接器時遇到問題</span><span class="sxs-lookup"><span data-stu-id="f6eba-126">I'm having a problem with the Application Proxy Agent Connector</span></span>
  <span data-ttu-id="f6eba-127">下列文件可協助您解決此類別的一些最常見問題。</span><span class="sxs-lookup"><span data-stu-id="f6eba-127">The following documents can help you to resolve some of the most common issues in this category.</span></span>
  * [<span data-ttu-id="f6eba-128">我在安裝應用程式 Proxy 代理程式連接器時遇到問題</span><span class="sxs-lookup"><span data-stu-id="f6eba-128">I am having issues installing the Application Proxy Agent Connector </span></span>](https://docs.microsoft.com/azure/active-directory/application-proxy-connector-installation-problem/)

## <a name="next-steps"></a><span data-ttu-id="f6eba-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6eba-129">Next steps</span></span>
[<span data-ttu-id="f6eba-130">如何為內部部署應用程式提供安全的遠端存取</span><span class="sxs-lookup"><span data-stu-id="f6eba-130">How to provide secure remote access to on-premises applications</span></span>](active-directory-application-proxy-get-started.md)
