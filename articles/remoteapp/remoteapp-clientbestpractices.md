---
title: "Azure RemoteApp 用戶端的 aaaBest 作法 |Microsoft 文件"
description: "深入了解使用 hello RemoteApp 用戶端的最佳作法"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 8c2e6068-8733-42f6-a05c-a2088634991b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: aa0ccb2f51d381462b78d60e966b87a67d8c247e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-remoteapp-clients"></a><span data-ttu-id="7b65f-103">Azure RemoteApp 用戶端的最佳作法</span><span class="sxs-lookup"><span data-stu-id="7b65f-103">Best practices for Azure RemoteApp clients</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7b65f-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="7b65f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7b65f-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7b65f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7b65f-106">hello 下列資訊可協助您使用 Azure RemoteApp 用戶端：</span><span class="sxs-lookup"><span data-stu-id="7b65f-106">hello following information can help you use Azure RemoteApp clients:</span></span>

* <span data-ttu-id="7b65f-107">一律使用最新用戶端 hello。</span><span class="sxs-lookup"><span data-stu-id="7b65f-107">Always use hello latest client.</span></span> <span data-ttu-id="7b65f-108">這可確保該 hello 您正在執行的用戶端版本具有 hello 最新的 bug 修正、 增強功能和功能。</span><span class="sxs-lookup"><span data-stu-id="7b65f-108">This ensures that hello client version you are running has hello latest bug fixes, improvements and features.</span></span> <span data-ttu-id="7b65f-109">您可能需要向上 tooautomatically toosign hello 適當的存放區中收到 hello 用戶端的更新。</span><span class="sxs-lookup"><span data-stu-id="7b65f-109">You might need toosign up tooautomatically receive updates for hello client in hello appropriate Store.</span></span>
* <span data-ttu-id="7b65f-110">如果您有段時間都沒有活動，RemoteApp 就會自動將您登出。</span><span class="sxs-lookup"><span data-stu-id="7b65f-110">RemoteApp will automatically log you off if you are inactive for a certain period of time.</span></span> <span data-ttu-id="7b65f-111">順序 tooprevent 造成資料遺失，建議您關閉您的應用程式，當您完成使用 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="7b65f-111">In order tooprevent data loss, we recommend closing your applications when you finish using hello service.</span></span>

