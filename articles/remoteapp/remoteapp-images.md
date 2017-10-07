---
title: "aaaWhat 處於 hello Azure RemoteApp 範本映像嗎？ | Microsoft Docs"
description: "深入了解 hello 隨附於 Azure RemoteApp 的範本映像。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a><span data-ttu-id="7fe25-104">什麼是 hello Azure RemoteApp 範本映像中？</span><span class="sxs-lookup"><span data-stu-id="7fe25-104">What is in hello Azure RemoteApp template images?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7fe25-105">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="7fe25-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7fe25-106">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7fe25-106">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7fe25-107">Azure RemoteApp 訂用帳戶包含三個範本映像：</span><span class="sxs-lookup"><span data-stu-id="7fe25-107">Your Azure RemoteApp subscription includes three template images:</span></span>

* <span data-ttu-id="7fe25-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="7fe25-108">Windows Server 2012</span></span>
* <span data-ttu-id="7fe25-109">Microsoft Office 365 ProPlus (需有 Office 365 訂用帳戶)</span><span class="sxs-lookup"><span data-stu-id="7fe25-109">Microsoft Office 365 ProPlus (Office 365 subscription required)</span></span>
* <span data-ttu-id="7fe25-110">Microsoft Office 2013 Professional Plus (僅限試用版)</span><span class="sxs-lookup"><span data-stu-id="7fe25-110">Microsoft Office 2013 Professional Plus (trial only)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7fe25-111">Azure RemoteApp 訂用帳戶會授與存取 toohello hello 映像，但 hello 的例外是 Office 365 ProPlus，這需要不同的訂用帳戶，並不能在生產環境中的 Office 2013 中的軟體。</span><span class="sxs-lookup"><span data-stu-id="7fe25-111">Your Azure RemoteApp subscription grants you access toohello software in hello images, with hello exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production.</span></span> <span data-ttu-id="7fe25-112">這表示您可以與您的使用者共用 hello 程式或 hello 範本映像上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7fe25-112">This means that you can share hello programs or apps on hello template images with your users.</span></span> <span data-ttu-id="7fe25-113">例如，如果您建立使用 hello Windows Server 2012 R2 映像的集合，您可以發佈 System Center Endpoint Protection 的使用者透過 RemoteApp 的 tooaccess。</span><span class="sxs-lookup"><span data-stu-id="7fe25-113">For example, if you create a collection that uses hello Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users tooaccess through RemoteApp.</span></span>
> 
> <span data-ttu-id="7fe25-114">簽出 hello[授權詳細資料的 RemoteApp](remoteapp-licensing.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7fe25-114">Check out hello [RemoteApp licensing details](remoteapp-licensing.md) for more information.</span></span> <span data-ttu-id="7fe25-115">和[與 Azure RemoteApp 一起使用的 Office](remoteapp-o365.md) hello Office 授權資訊。</span><span class="sxs-lookup"><span data-stu-id="7fe25-115">And [Using Office with Azure RemoteApp](remoteapp-o365.md) for hello Office licensing info.</span></span>
> 
> 

<span data-ttu-id="7fe25-116">閱讀每個映像包含之內容的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7fe25-116">Read on for details on what each image contains.</span></span>

## <a name="windows-server-2012-r2--hello-vanilla-image"></a><span data-ttu-id="7fe25-117">Windows Server 2012 R2 （"hello 香草映像）</span><span class="sxs-lookup"><span data-stu-id="7fe25-117">Windows Server 2012 R2  ("hello vanilla image")</span></span>
<span data-ttu-id="7fe25-118">此影像以 Microsoft Windows Server 2012 R2 Datacenter 作業系統且已 hello 下列角色和功能安裝 Azure RemoteApp 範本映像的 toomeet hello 需求：</span><span class="sxs-lookup"><span data-stu-id="7fe25-118">This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has hello following roles and features installed toomeet hello requirements for Azure RemoteApp template images:</span></span>

* <span data-ttu-id="7fe25-119">.NET Framework 4.5、3.5.1、3.5</span><span class="sxs-lookup"><span data-stu-id="7fe25-119">.NET Framework 4.5, 3.5.1, 3.5</span></span>
* <span data-ttu-id="7fe25-120">桌面體驗</span><span class="sxs-lookup"><span data-stu-id="7fe25-120">Desktop Experience</span></span>
* <span data-ttu-id="7fe25-121">筆跡和手寫服務</span><span class="sxs-lookup"><span data-stu-id="7fe25-121">Ink and Handwriting Services</span></span>
* <span data-ttu-id="7fe25-122">媒體基礎</span><span class="sxs-lookup"><span data-stu-id="7fe25-122">Media Foundation</span></span>
* <span data-ttu-id="7fe25-123">遠端桌面工作階段主機</span><span class="sxs-lookup"><span data-stu-id="7fe25-123">Remote Desktop Session Host</span></span>
* <span data-ttu-id="7fe25-124">Windows PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="7fe25-124">Windows PowerShell 4.0</span></span>
* <span data-ttu-id="7fe25-125">Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="7fe25-125">Windows PowerShell ISE</span></span>
* <span data-ttu-id="7fe25-126">WoW64 支援</span><span class="sxs-lookup"><span data-stu-id="7fe25-126">WoW64 Support</span></span>

<span data-ttu-id="7fe25-127">這個映像也有下列安裝的應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="7fe25-127">This image also has hello following applications installed:</span></span>

* <span data-ttu-id="7fe25-128">Adobe Flash Player</span><span class="sxs-lookup"><span data-stu-id="7fe25-128">Adobe Flash Player</span></span>
* <span data-ttu-id="7fe25-129">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="7fe25-129">Microsoft Silverlight</span></span>
* <span data-ttu-id="7fe25-130">Microsoft System Center 2012 Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="7fe25-130">Microsoft System Center 2012 Endpoint Protection</span></span>
* <span data-ttu-id="7fe25-131">Microsoft Windows Media Player</span><span class="sxs-lookup"><span data-stu-id="7fe25-131">Microsoft Windows Media Player</span></span>

## <a name="microsoft-office-365-proplus-subscription-required"></a><span data-ttu-id="7fe25-132">Microsoft Office 365 ProPlus (需有訂用帳戶)</span><span class="sxs-lookup"><span data-stu-id="7fe25-132">Microsoft Office 365 ProPlus (subscription required)</span></span>
<span data-ttu-id="7fe25-133">Office 365 是 hello 最要求的應用程式，讓我們的 「 自訂 」 映像為您建立與 toowork。</span><span class="sxs-lookup"><span data-stu-id="7fe25-133">Office 365 is hello most requested application, so we created a "custom" image for you toowork with.</span></span>

<span data-ttu-id="7fe25-134">此映像 hello 香草映像的延伸模組並已 hello 安裝下列元件的 Microsoft Office 365 ProPlus 此外 toohello hello Windows Server 2012 R2 映像中所述的元件：</span><span class="sxs-lookup"><span data-stu-id="7fe25-134">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 365 ProPlus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="7fe25-135">Access</span><span class="sxs-lookup"><span data-stu-id="7fe25-135">Access</span></span>
* <span data-ttu-id="7fe25-136">Excel</span><span class="sxs-lookup"><span data-stu-id="7fe25-136">Excel</span></span>
* <span data-ttu-id="7fe25-137">Lync</span><span class="sxs-lookup"><span data-stu-id="7fe25-137">Lync</span></span>
* <span data-ttu-id="7fe25-138">OneNote</span><span class="sxs-lookup"><span data-stu-id="7fe25-138">OneNote</span></span>
* <span data-ttu-id="7fe25-139">商務用 OneDrive （請注意該 hello 同步代理程式不支援與 Azure RemoteApp 搭配使用）</span><span class="sxs-lookup"><span data-stu-id="7fe25-139">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="7fe25-140">Outlook</span><span class="sxs-lookup"><span data-stu-id="7fe25-140">Outlook</span></span>
* <span data-ttu-id="7fe25-141">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="7fe25-141">PowerPoint</span></span>
* <span data-ttu-id="7fe25-142">Word</span><span class="sxs-lookup"><span data-stu-id="7fe25-142">Word</span></span>
* <span data-ttu-id="7fe25-143">Microsoft Office 校訂工具</span><span class="sxs-lookup"><span data-stu-id="7fe25-143">Microsoft Office Proofing Tools</span></span>

<span data-ttu-id="7fe25-144">hello 映像也包括 Visio 專業版和專業版的專案。</span><span class="sxs-lookup"><span data-stu-id="7fe25-144">hello image also includes Visio Pro and Project Pro.</span></span>

<span data-ttu-id="7fe25-145">和下列應用程式，以及 hello:</span><span class="sxs-lookup"><span data-stu-id="7fe25-145">And hello following applications, as well:</span></span>

* <span data-ttu-id="7fe25-146">SQL 原生用戶端</span><span class="sxs-lookup"><span data-stu-id="7fe25-146">SQL Native client</span></span>
* <span data-ttu-id="7fe25-147">ODBC 驅動程式</span><span class="sxs-lookup"><span data-stu-id="7fe25-147">ODBC Driver</span></span>
* <span data-ttu-id="7fe25-148">SQL Server 資料採礦用戶端</span><span class="sxs-lookup"><span data-stu-id="7fe25-148">SQL Server Data Mining client</span></span>
* <span data-ttu-id="7fe25-149">MasterDataServices 用戶端</span><span class="sxs-lookup"><span data-stu-id="7fe25-149">MasterDataServices client</span></span>
* <span data-ttu-id="7fe25-150">Microsoft Publisher</span><span class="sxs-lookup"><span data-stu-id="7fe25-150">Microsoft Publisher</span></span>
* <span data-ttu-id="7fe25-151">PowerQuery</span><span class="sxs-lookup"><span data-stu-id="7fe25-151">PowerQuery</span></span>
* <span data-ttu-id="7fe25-152">PowerMap</span><span class="sxs-lookup"><span data-stu-id="7fe25-152">PowerMap</span></span>

<span data-ttu-id="7fe25-153">Office 365 ProPlus 應用程式的完整功能只適用於擁有 Office 365 ProPlus 方案的使用者。</span><span class="sxs-lookup"><span data-stu-id="7fe25-153">Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan.</span></span> <span data-ttu-id="7fe25-154">如需有關 hello Office 365 訂用帳戶查看計劃[Office 365 服務計劃](http://technet.microsoft.com/library/office-365-plan-options.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7fe25-154">For more details on hello Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span> <span data-ttu-id="7fe25-155">還有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="7fe25-155">Still have questions?</span></span> <span data-ttu-id="7fe25-156">簽出 hello [Office 365 + RemoteApp](remoteapp-o365.md)資訊。</span><span class="sxs-lookup"><span data-stu-id="7fe25-156">Check out hello [Office 365 + RemoteApp](remoteapp-o365.md) information.</span></span> <span data-ttu-id="7fe25-157">也請參閱 hello 新發行項，[如何 toouse 您 Office 365 訂用帳戶與 Azure RemoteApp 一起](remoteapp-officesubscription.md)。</span><span class="sxs-lookup"><span data-stu-id="7fe25-157">Also check out hello new article, [How toouse your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

<span data-ttu-id="7fe25-158">請注意，您需要 Office 365 ProPlus toolicense、 Visio 專業版、 和專案 Pro 個別-它們都各自具有自己的授權。</span><span class="sxs-lookup"><span data-stu-id="7fe25-158">Note that you need toolicense Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.</span></span>

## <a name="microsoft-office-2013-professional-plus-trial-only"></a><span data-ttu-id="7fe25-159">Microsoft Office 2013 Professional Plus (僅限試用版)</span><span class="sxs-lookup"><span data-stu-id="7fe25-159">Microsoft Office 2013 Professional Plus (trial only)</span></span>
<span data-ttu-id="7fe25-160">Hello 免費試用期間，您可以測試 hello 服務與 hello Office 2013 映像。</span><span class="sxs-lookup"><span data-stu-id="7fe25-160">During hello free trial period, you can test hello service with hello Office 2013 image.</span></span>

<span data-ttu-id="7fe25-161">此映像 hello 香草映像的延伸模組並已 hello 安裝下列元件的 Microsoft Office 2013 Professional Plus 此外 toohello hello Windows Server 2012 R2 映像中所述的元件：</span><span class="sxs-lookup"><span data-stu-id="7fe25-161">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 2013 Professional Plus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="7fe25-162">Access</span><span class="sxs-lookup"><span data-stu-id="7fe25-162">Access</span></span>
* <span data-ttu-id="7fe25-163">Excel</span><span class="sxs-lookup"><span data-stu-id="7fe25-163">Excel</span></span>
* <span data-ttu-id="7fe25-164">Lync</span><span class="sxs-lookup"><span data-stu-id="7fe25-164">Lync</span></span>
* <span data-ttu-id="7fe25-165">OneNote</span><span class="sxs-lookup"><span data-stu-id="7fe25-165">OneNote</span></span>
* <span data-ttu-id="7fe25-166">商務用 OneDrive （請注意該 hello 同步代理程式不支援與 Azure RemoteApp 搭配使用）</span><span class="sxs-lookup"><span data-stu-id="7fe25-166">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="7fe25-167">Outlook</span><span class="sxs-lookup"><span data-stu-id="7fe25-167">Outlook</span></span>
* <span data-ttu-id="7fe25-168">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="7fe25-168">PowerPoint</span></span>
* <span data-ttu-id="7fe25-169">隨附此逐步解說的專案</span><span class="sxs-lookup"><span data-stu-id="7fe25-169">Project</span></span>
* <span data-ttu-id="7fe25-170">Visio</span><span class="sxs-lookup"><span data-stu-id="7fe25-170">Visio</span></span>
* <span data-ttu-id="7fe25-171">Word</span><span class="sxs-lookup"><span data-stu-id="7fe25-171">Word</span></span>
* <span data-ttu-id="7fe25-172">Microsoft Office 校訂工具</span><span class="sxs-lookup"><span data-stu-id="7fe25-172">Microsoft Office Proofing Tools</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7fe25-173">**法律資訊：**此映像不包含 Microsoft Office 授權，且「無法用於生產環境」。</span><span class="sxs-lookup"><span data-stu-id="7fe25-173">**Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*.</span></span> <span data-ttu-id="7fe25-174">hello Office 2013 Professional Plus 影像是只能用於試用版。</span><span class="sxs-lookup"><span data-stu-id="7fe25-174">hello Office 2013 Professional Plus image is intended for trial use only.</span></span> <span data-ttu-id="7fe25-175">如果您想要實際執行 toouse Azure RemoteApp 中的 Office 應用程式，您會需要 toouse hello Office 365 ProPlus 映像。</span><span class="sxs-lookup"><span data-stu-id="7fe25-175">If you want toouse Office apps in Azure RemoteApp for production, you need toouse hello Office 365 ProPlus image.</span></span> <span data-ttu-id="7fe25-176">如需授權 Office 的詳細資訊，請參閱 [使用 Office 365 與 Azure RemoteApp 搭配](remoteapp-o365.md)</span><span class="sxs-lookup"><span data-stu-id="7fe25-176">For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)</span></span>
> 
> 

