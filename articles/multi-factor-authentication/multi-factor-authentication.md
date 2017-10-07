---
title: "需在 Azure MFA 的兩步驟驗證 aaaLearn |Microsoft 文件"
description: "什麼是 Azure multi-factor Authentication，為什麼要使用 MFA，hello multi-factor Authentication 用戶端以及 hello 不同的方法和版本的詳細資訊。 "
keywords: "簡介 tooMFA，mfa 概觀、 何謂 mfa"
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
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="c2c13-104">什麼是 Azure Multi-Factor Authentication？</span><span class="sxs-lookup"><span data-stu-id="c2c13-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="c2c13-105">雙步驟驗證是驗證的需要一個以上的驗證方法，並將重要的第二層安全性 toouser 登入和交易方法。</span><span class="sxs-lookup"><span data-stu-id="c2c13-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security toouser sign-ins and transactions.</span></span> <span data-ttu-id="c2c13-106">其運作方式是要求任何兩個或多個下列驗證方法的 hello:</span><span class="sxs-lookup"><span data-stu-id="c2c13-106">It works by requiring any two or more of hello following verification methods:</span></span>

* <span data-ttu-id="c2c13-107">您知道的某些資訊 (通常是密碼)</span><span class="sxs-lookup"><span data-stu-id="c2c13-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="c2c13-108">您擁有的某些東西 (不容易輕易複製的信任裝置，例如電話)</span><span class="sxs-lookup"><span data-stu-id="c2c13-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="c2c13-109">您身上的某些特徵 (生物識別技術)</span><span class="sxs-lookup"><span data-stu-id="c2c13-109">Something you are (biometrics)</span></span>

<span data-ttu-id="c2c13-110"><center>![使用者名稱和密碼](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![憑證](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![智慧型手機](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![智慧卡](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![虛擬智慧卡](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![使用者名稱和密碼](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="c2c13-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="c2c13-111">Azure Multi-Factor Authentication (MFA) 是 Microsoft 的雙步驟驗證解決方案。</span><span class="sxs-lookup"><span data-stu-id="c2c13-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="c2c13-112">Azure MFA 有助於保護存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求。</span><span class="sxs-lookup"><span data-stu-id="c2c13-112">Azure MFA helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="c2c13-113">它可以透過一些驗證方法 (包括電話、文字訊息，或行動應用程式驗證) 來提供強大的驗證功能。</span><span class="sxs-lookup"><span data-stu-id="c2c13-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="c2c13-114">為何使用 Azure Multi-Factor Authentication？</span><span class="sxs-lookup"><span data-stu-id="c2c13-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="c2c13-115">與以前比較起來，現今人們連線網路的時間越來越長。</span><span class="sxs-lookup"><span data-stu-id="c2c13-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="c2c13-116">智慧型手機、 平板電腦、 膝上型電腦和電腦的人有如何將 tooconnect 並隨時保持連線的幾個不同選項。</span><span class="sxs-lookup"><span data-stu-id="c2c13-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going tooconnect and stay connected at any time.</span></span> <span data-ttu-id="c2c13-117">人們可以從任何地方存取他們的帳戶與應用程式，這表示他們可以完成更多工作並為客戶提供更好的服務。</span><span class="sxs-lookup"><span data-stu-id="c2c13-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="c2c13-118">Azure Multi-factor Authentication 是簡單 toouse，可擴充、 可靠的解決方案，以及提供驗證第二種方法讓您的使用者永遠會受到保護。</span><span class="sxs-lookup"><span data-stu-id="c2c13-118">Azure Multi-Factor Authentication is an easy toouse, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![輕鬆 tooUse](./media/multi-factor-authentication/simple.png) | ![可調整](./media/multi-factor-authentication/scalable.png) | ![永遠受到保護](./media/multi-factor-authentication/protected.png) | ![可靠](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="c2c13-123">**輕鬆 toouse**</span><span class="sxs-lookup"><span data-stu-id="c2c13-123">**Easy toouse**</span></span> |<span data-ttu-id="c2c13-124">**可調整**</span><span class="sxs-lookup"><span data-stu-id="c2c13-124">**Scalable**</span></span> |<span data-ttu-id="c2c13-125">**永遠受到保護**</span><span class="sxs-lookup"><span data-stu-id="c2c13-125">**Always Protected**</span></span> |<span data-ttu-id="c2c13-126">**可靠**</span><span class="sxs-lookup"><span data-stu-id="c2c13-126">**Reliable**</span></span> |

* <span data-ttu-id="c2c13-127">**輕鬆 tooUse** -Azure Multi-factor Authentication 是簡單 tooset 註冊和使用。</span><span class="sxs-lookup"><span data-stu-id="c2c13-127">**Easy tooUse** - Azure Multi-Factor Authentication is simple tooset up and use.</span></span> <span data-ttu-id="c2c13-128">hello 額外的保護，隨附於 Azure Multi-factor Authentication Server 可讓使用者 toomanage 自己的裝置。</span><span class="sxs-lookup"><span data-stu-id="c2c13-128">hello extra protection that comes with Azure Multi-Factor Authentication allows users toomanage their own devices.</span></span> <span data-ttu-id="c2c13-129">最棒的是，在許多情況下，只需簡單按幾下滑鼠即可進行設定。</span><span class="sxs-lookup"><span data-stu-id="c2c13-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="c2c13-130">**可擴充**-Azure Multi-factor Authentication 使用 hello 雲端的 hello 電源，並整合與您內部部署 AD 和自訂應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2c13-130">**Scalable** - Azure Multi-Factor Authentication uses hello power of hello cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="c2c13-131">這項保護甚至會擴充 tooyour 高容量的關鍵任務的案例。</span><span class="sxs-lookup"><span data-stu-id="c2c13-131">This protection is even extended tooyour high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="c2c13-132">**永遠會受到保護**-Azure Multi-factor Authentication 提供使用 hello 最高的業界標準的強式驗證。</span><span class="sxs-lookup"><span data-stu-id="c2c13-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using hello highest industry standards.</span></span>
* <span data-ttu-id="c2c13-133">**可靠** - 我們保證 Azure Multi-Factor Authentication 的可用性可達到 99.9%。</span><span class="sxs-lookup"><span data-stu-id="c2c13-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="c2c13-134">hello 服務會被視為無法使用時無法 tooreceive 或處理序的 hello 雙步驟驗證的驗證要求。</span><span class="sxs-lookup"><span data-stu-id="c2c13-134">hello service is considered unavailable when it is unable tooreceive or process verification requests for hello two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="c2c13-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c2c13-135">Next steps</span></span>

- <span data-ttu-id="c2c13-136">深入了解 [Azure Multi-Factor Authentication 的作用](multi-factor-authentication-how-it-works.md)</span><span class="sxs-lookup"><span data-stu-id="c2c13-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="c2c13-137">了解不同的 hello[版本和 Azure Multi-factor Authentication 的耗用量方法](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="c2c13-137">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>
