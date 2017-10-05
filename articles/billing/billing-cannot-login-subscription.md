---
title: "無法登入 Azure 訂用帳戶 | Microsoft Docs"
description: "說明如何疑難排解一些常見 Azure 訂用帳戶的登入問題。"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: 4f67be9b59ab42e10c4cd755998795a72b711da6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="i-cant-sign-in-to-manage-my-azure-subscription"></a><span data-ttu-id="4131d-103">我無法登入來管理我的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4131d-103">I can't sign in to manage my Azure subscription</span></span>
<span data-ttu-id="4131d-104">本文將引導您完成一些可解決登入問題的最常見方法。</span><span class="sxs-lookup"><span data-stu-id="4131d-104">This article guides you through some of the most common methods to resolve login issues.</span></span>

## <a name="page-hangs-in-the-loading-status"></a><span data-ttu-id="4131d-105">頁面在載入狀態停止回應</span><span class="sxs-lookup"><span data-stu-id="4131d-105">Page hangs in the loading status</span></span>
<span data-ttu-id="4131d-106">如果您的網際網路瀏覽器頁面停滯，請嘗試下列每個步驟，直到您可以進入 [Azure 入口網站](https://portal.azure.com)為止。</span><span class="sxs-lookup"><span data-stu-id="4131d-106">If your internet browser page hangs, try each of the following steps until you can get to the [Azure portal](https://portal.azure.com).</span></span>

* <span data-ttu-id="4131d-107">重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="4131d-107">Refresh the page.</span></span>
* <span data-ttu-id="4131d-108">使用不同的網際網路瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="4131d-108">Use a different Internet browser.</span></span>
* <span data-ttu-id="4131d-109">如果您使用的是 Microsoft Internet Explorer，請使用「InPrivate 瀏覽」模式來瀏覽至 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4131d-109">If you’re using Microsoft Internet Explorer, browse to the Azure portal by using the InPrivate Browsing mode.</span></span> 
  
  <span data-ttu-id="4131d-110">A.</span><span class="sxs-lookup"><span data-stu-id="4131d-110">A.</span></span> <span data-ttu-id="4131d-111">按一下 [工具] ![工具按鈕](./media/billing-cannot-login-subscription/Toolsbutton.png) > [安全性] > [InPrivate 瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="4131d-111">Click **Tools** ![tools button](./media/billing-cannot-login-subscription/Toolsbutton.png) > **Safety** > **InPrivate Browsing**.</span></span>
  
  <span data-ttu-id="4131d-112">B.</span><span class="sxs-lookup"><span data-stu-id="4131d-112">B.</span></span> <span data-ttu-id="4131d-113">瀏覽至 [Azure 入口網站](https://portal.azure.com)，然後登入入口網站。</span><span class="sxs-lookup"><span data-stu-id="4131d-113">Browse to the [Azure portal](https://portal.azure.com), and then sign in to the portal.</span></span>

## <a name="you-are-automatically-signed-in-as-a-different-user"></a><span data-ttu-id="4131d-114">自動將您登入為不同的使用者</span><span class="sxs-lookup"><span data-stu-id="4131d-114">You are automatically signed in as a different user</span></span>
<span data-ttu-id="4131d-115">如果您在網際網路瀏覽器中使用多個使用者帳戶，就可能發生此問題。</span><span class="sxs-lookup"><span data-stu-id="4131d-115">This issue can occur if you use more than one user account in an Internet browser.</span></span>

<span data-ttu-id="4131d-116">若要解決此問題，請嘗試下列其中一個方法：</span><span class="sxs-lookup"><span data-stu-id="4131d-116">To resolve the issue, try one of the following methods:</span></span>

* <span data-ttu-id="4131d-117">清除快取並刪除網際網路 Cookie。</span><span class="sxs-lookup"><span data-stu-id="4131d-117">Clear the cache and delete Internet cookies.</span></span> <span data-ttu-id="4131d-118">在 Internet Explorer 中，按一下 [工具] ![工具按鈕](./media/billing-cannot-login-subscription/Toolsbutton.png) > [網際網路選項] > [刪除]。</span><span class="sxs-lookup"><span data-stu-id="4131d-118">In Internet Explorer, click **Tools** ![tools button](./media/billing-cannot-login-subscription/Toolsbutton.png) > **Internet Options** > **Delete**.</span></span> <span data-ttu-id="4131d-119">確定已選取暫存檔、Cookie、密碼及瀏覽歷程記錄的核取方塊，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="4131d-119">Make sure that the check boxes for temporary files, cookies, password, and browsing history are selected, and then click Delete.</span></span>
* <span data-ttu-id="4131d-120">重設 Internet Explorer 設定來還原您所做的任何個人設定。</span><span class="sxs-lookup"><span data-stu-id="4131d-120">Reset the Internet Explorer settings to revert any personal settings that you’ve made.</span></span> <span data-ttu-id="4131d-121">按一下 [工具]![工具按鈕](./media/billing-cannot-login-subscription/Toolsbutton.png)> [網際網路選項] > [進階] > 選取 [刪除個人設定] 方塊 > [重設]。</span><span class="sxs-lookup"><span data-stu-id="4131d-121">Click **Tools** ![tools button](./media/billing-cannot-login-subscription/Toolsbutton.png)> **Internet Options** > **Advanced** >select the **Delete personal settings** box > **Reset**.</span></span>
* <span data-ttu-id="4131d-122">以「InPrivate 模式」瀏覽至 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4131d-122">Browse to the Azure portal in InPrivate Browsing mode.</span></span> <span data-ttu-id="4131d-123">按一下 [工具] ![工具按鈕](./media/billing-cannot-login-subscription/Toolsbutton.png) > [安全性] > [InPrivate 瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="4131d-123">Click **Tools** ![tools button](./media/billing-cannot-login-subscription/Toolsbutton.png) > **Safety** > **InPrivate Browsing**.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="4131d-124">需要協助嗎？</span><span class="sxs-lookup"><span data-stu-id="4131d-124">Need help?</span></span> <span data-ttu-id="4131d-125">請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="4131d-125">Contact support.</span></span>
<span data-ttu-id="4131d-126">如果仍需要協助，請[連絡支援人員](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409)以快速解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="4131d-126">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) to get your issue resolved quickly.</span></span> 

