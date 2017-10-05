---
title: "了解 Azure MFA 中的雙步驟驗證 | Microsoft Docs"
description: "何謂 Azure Multi-factor Authentication、為什麼使用 MFA，還有 Multi-Factor Authentication 用戶端、不同的方法及可用版本的詳細資訊。 "
keywords: "MFA 的簡介, mfa 概觀, 什麼是 mfa"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: 7334ab5b278c3339fdbc2e363fd5c609604d3e14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="96ddf-104">什麼是 Azure Multi-Factor Authentication？</span><span class="sxs-lookup"><span data-stu-id="96ddf-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="96ddf-105">雙步驟驗證是需要多種驗證方法，並在使用者登入和交易中新增重要的第二層安全性的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="96ddf-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security to user sign-ins and transactions.</span></span> <span data-ttu-id="96ddf-106">其運作方式需要下列其中任何二或多個驗證方法：</span><span class="sxs-lookup"><span data-stu-id="96ddf-106">It works by requiring any two or more of the following verification methods:</span></span>

* <span data-ttu-id="96ddf-107">您知道的某些資訊 (通常是密碼)</span><span class="sxs-lookup"><span data-stu-id="96ddf-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="96ddf-108">您擁有的某些東西 (不容易輕易複製的信任裝置，例如電話)</span><span class="sxs-lookup"><span data-stu-id="96ddf-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="96ddf-109">您身上的某些特徵 (生物識別技術)</span><span class="sxs-lookup"><span data-stu-id="96ddf-109">Something you are (biometrics)</span></span>

<span data-ttu-id="96ddf-110"><center>![使用者名稱和密碼](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![憑證](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![智慧型手機](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![智慧卡](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![虛擬智慧卡](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![使用者名稱和密碼](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="96ddf-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="96ddf-111">Azure Multi-Factor Authentication (MFA) 是 Microsoft 的雙步驟驗證解決方案。</span><span class="sxs-lookup"><span data-stu-id="96ddf-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="96ddf-112">Azure MFA 有助於保護對資料與應用程式的存取，同時可以滿足使用者對簡單登入程序的需求。</span><span class="sxs-lookup"><span data-stu-id="96ddf-112">Azure MFA helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="96ddf-113">它可以透過一些驗證方法 (包括電話、文字訊息，或行動應用程式驗證) 來提供強大的驗證功能。</span><span class="sxs-lookup"><span data-stu-id="96ddf-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="96ddf-114">為何使用 Azure Multi-Factor Authentication？</span><span class="sxs-lookup"><span data-stu-id="96ddf-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="96ddf-115">與以前比較起來，現今人們連線網路的時間越來越長。</span><span class="sxs-lookup"><span data-stu-id="96ddf-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="96ddf-116">透過智慧型手機、平板電腦、膝上型電腦以及電腦，人們有幾種不同選擇可隨時用來連線網路並維持連線。</span><span class="sxs-lookup"><span data-stu-id="96ddf-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going to connect and stay connected at any time.</span></span> <span data-ttu-id="96ddf-117">人們可以從任何地方存取他們的帳戶與應用程式，這表示他們可以完成更多工作並為客戶提供更好的服務。</span><span class="sxs-lookup"><span data-stu-id="96ddf-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="96ddf-118">Azure Multi-Factor Authentication 是一個容易使用、可調整且可靠的解決方案，可提供第二種驗證方法讓您的使用者永遠受到保護。</span><span class="sxs-lookup"><span data-stu-id="96ddf-118">Azure Multi-Factor Authentication is an easy to use, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![容易使用](./media/multi-factor-authentication/simple.png) | ![可調整](./media/multi-factor-authentication/scalable.png) | ![永遠受到保護](./media/multi-factor-authentication/protected.png) | ![可靠](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="96ddf-123">**容易使用**</span><span class="sxs-lookup"><span data-stu-id="96ddf-123">**Easy to use**</span></span> |<span data-ttu-id="96ddf-124">**可調整**</span><span class="sxs-lookup"><span data-stu-id="96ddf-124">**Scalable**</span></span> |<span data-ttu-id="96ddf-125">**永遠受到保護**</span><span class="sxs-lookup"><span data-stu-id="96ddf-125">**Always Protected**</span></span> |<span data-ttu-id="96ddf-126">**可靠**</span><span class="sxs-lookup"><span data-stu-id="96ddf-126">**Reliable**</span></span> |

* <span data-ttu-id="96ddf-127">**容易使用** - Azure Multi-Factor Authentication 很容易設定及使用。</span><span class="sxs-lookup"><span data-stu-id="96ddf-127">**Easy to Use** - Azure Multi-Factor Authentication is simple to set up and use.</span></span> <span data-ttu-id="96ddf-128">隨附於 Azure Multi-Factor Authentication 的額外保護可讓使用者管理他們自己的裝置。</span><span class="sxs-lookup"><span data-stu-id="96ddf-128">The extra protection that comes with Azure Multi-Factor Authentication allows users to manage their own devices.</span></span> <span data-ttu-id="96ddf-129">最棒的是，在許多情況下，只需簡單按幾下滑鼠即可進行設定。</span><span class="sxs-lookup"><span data-stu-id="96ddf-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="96ddf-130">**可調整** - Azure Multi-Factor Authentication 採用雲端技術且與您內部部署的 AD 與自訂應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="96ddf-130">**Scalable** - Azure Multi-Factor Authentication uses the power of the cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="96ddf-131">此保護功能甚至可以擴充以因應您高任務關鍵性的狀況。</span><span class="sxs-lookup"><span data-stu-id="96ddf-131">This protection is even extended to your high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="96ddf-132">**永遠受到保護** - Azure Multi-Factor Authentication 使用最高工業標準提供強大驗證功能。</span><span class="sxs-lookup"><span data-stu-id="96ddf-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using the highest industry standards.</span></span>
* <span data-ttu-id="96ddf-133">**可靠** - 我們保證 Azure Multi-Factor Authentication 的可用性可達到 99.9%。</span><span class="sxs-lookup"><span data-stu-id="96ddf-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="96ddf-134">當服務無法接收或處理雙步驟驗證的驗證要求時，服務會被視為無法使用。</span><span class="sxs-lookup"><span data-stu-id="96ddf-134">The service is considered unavailable when it is unable to receive or process verification requests for the two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="96ddf-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96ddf-135">Next steps</span></span>

- <span data-ttu-id="96ddf-136">深入了解 [Azure Multi-Factor Authentication 的作用](multi-factor-authentication-how-it-works.md)</span><span class="sxs-lookup"><span data-stu-id="96ddf-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="96ddf-137">請參閱不同的 [Azure Multi-Factor Authentication 版本和耗用方法](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="96ddf-137">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>
