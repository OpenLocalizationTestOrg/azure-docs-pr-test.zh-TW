---
title: "通知中心 aaaSecurity"
description: "本主題說明 Azure 通知中樞的安全性。"
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 6506177c-e25c-4af7-8508-a3ddca9dc07c
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f59ad4594c2c0a2e2b22ab0b6d6bad53825a4dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security"></a><span data-ttu-id="bb121-103">安全性</span><span class="sxs-lookup"><span data-stu-id="bb121-103">Security</span></span>
## <a name="overview"></a><span data-ttu-id="bb121-104">概觀</span><span class="sxs-lookup"><span data-stu-id="bb121-104">Overview</span></span>
<span data-ttu-id="bb121-105">本主題說明 Azure 通知中樞 hello 安全性模型。</span><span class="sxs-lookup"><span data-stu-id="bb121-105">This topic describes hello security model of Azure Notification Hubs.</span></span> <span data-ttu-id="bb121-106">由於通知中心為服務匯流排實體，這些物件實作 hello 與 Service Bus 相同的安全性模型。</span><span class="sxs-lookup"><span data-stu-id="bb121-106">Because Notification Hubs are a Service Bus entity, they implement hello same security model as Service Bus.</span></span> <span data-ttu-id="bb121-107">如需詳細資訊，請參閱 hello[服務匯流排驗證](https://msdn.microsoft.com/library/azure/dn155925.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="bb121-107">For more information, see hello [Service Bus Authentication](https://msdn.microsoft.com/library/azure/dn155925.aspx) topics.</span></span>

## <a name="shared-access-signature-security-sas"></a><span data-ttu-id="bb121-108">共用存取簽章的安全性 (SAS)</span><span class="sxs-lookup"><span data-stu-id="bb121-108">Shared Access Signature Security (SAS)</span></span>
<span data-ttu-id="bb121-109">通知中樞會實作實體層級的安全性配置，稱為 SAS (共用存取簽章)。</span><span class="sxs-lookup"><span data-stu-id="bb121-109">Notification Hubs implements an entity-level security scheme called SAS (Shared Access Signature).</span></span> <span data-ttu-id="bb121-110">此配置讓傳訊實體 toodeclare 描述 too12 授權規則，授與對該實體的權限。</span><span class="sxs-lookup"><span data-stu-id="bb121-110">This scheme enables messaging entities toodeclare up too12 authorization rules in their description that grant rights on that entity.</span></span>

<span data-ttu-id="bb121-111">每個規則包含名稱、 索引鍵的值 （共用密碼） 和一組權限，如述 hello > 一節 「 安全性宣告 」。</span><span class="sxs-lookup"><span data-stu-id="bb121-111">Each rule contains a name, a key value (shared secret), and a set of rights, as explained in hello section “Security Claims.”</span></span> <span data-ttu-id="bb121-112">建立通知中心時，會自動建立兩個規則： 其中一個接聽的權限 （hello 用戶端應用程式使用)，另一個具有所有權限 （hello 應用程式後端會使用)。</span><span class="sxs-lookup"><span data-stu-id="bb121-112">When creating a Notification Hub, two rules are automatically created: one with Listen rights (that hello client app uses) and one with all rights (that hello app backend uses).</span></span>

<span data-ttu-id="bb121-113">如果透過傳送嗨資訊，從用戶端應用程式，請執行註冊管理時通知並不是敏感資訊 （如範例中，天氣更新），常見的方式 tooaccess 通知中樞的 hello 規則只限 「 接聽 」 存取 toohello toogive hello 機碼值用戶端應用程式和 toogive hello 索引鍵值 hello 規則的完整存取 toohello 應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="bb121-113">When performing registration management from client apps, if hello information sent via notifications is not sensitive (for example, weather updates), a common way tooaccess a Notification Hub is toogive hello key value of hello rule Listen-only access toohello client app, and toogive hello key value of hello rule full access toohello app backend.</span></span>

<span data-ttu-id="bb121-114">不建議您在 Windows 市集用戶端應用程式中內嵌 hello 索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="bb121-114">It is not recommended that you embed hello key value in Windows Store client apps.</span></span> <span data-ttu-id="bb121-115">內嵌 hello 機碼值的方式 tooavoid 是 toohave hello 用戶端應用程式從擷取它在啟動 hello 應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="bb121-115">A way tooavoid embedding hello key value is toohave hello client app retrieve it from hello app backend at startup.</span></span>

<span data-ttu-id="bb121-116">請務必 toounderstand hello 與接聽 」 存取權的索引鍵，可讓用戶端應用程式 tooregister 任何標記。</span><span class="sxs-lookup"><span data-stu-id="bb121-116">It is important toounderstand that hello key with Listen access allows a client app tooregister for any tag.</span></span> <span data-ttu-id="bb121-117">如果您的應用程式必須限制註冊 toospecific 標記 toospecific 用戶端 （例如標籤表示使用者 Id 時），您的應用程式後端必須執行 hello 註冊。</span><span class="sxs-lookup"><span data-stu-id="bb121-117">If your app must restrict registrations toospecific tags toospecific clients (for example, when tags represent user IDs), then your app backend must perform hello registrations.</span></span> <span data-ttu-id="bb121-118">如需詳細資訊，請參閱＜註冊管理＞。</span><span class="sxs-lookup"><span data-stu-id="bb121-118">For more information, see Registration Management.</span></span> <span data-ttu-id="bb121-119">請注意，如此一來，hello 用戶端應用程式將不需要直接存取 tooNotification 集線器。</span><span class="sxs-lookup"><span data-stu-id="bb121-119">Note that in this way, hello client app will not have direct access tooNotification Hubs.</span></span>

## <a name="security-claims"></a><span data-ttu-id="bb121-120">安全性宣告</span><span class="sxs-lookup"><span data-stu-id="bb121-120">Security claims</span></span>
<span data-ttu-id="bb121-121">類似 tooother 實體，通知中樞作業可以有三種安全性宣告： 接聽、 傳送和管理。</span><span class="sxs-lookup"><span data-stu-id="bb121-121">Similar tooother entities, Notification Hub operations are allowed for three security claims: Listen, Send, and Manage.</span></span>

| <span data-ttu-id="bb121-122">宣告</span><span class="sxs-lookup"><span data-stu-id="bb121-122">Claim</span></span> | <span data-ttu-id="bb121-123">說明</span><span class="sxs-lookup"><span data-stu-id="bb121-123">Description</span></span> | <span data-ttu-id="bb121-124">允許的作業</span><span class="sxs-lookup"><span data-stu-id="bb121-124">Operations allowed</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb121-125">接聽</span><span class="sxs-lookup"><span data-stu-id="bb121-125">Listen</span></span> |<span data-ttu-id="bb121-126">建立/更新、讀取及刪除單一註冊</span><span class="sxs-lookup"><span data-stu-id="bb121-126">Create/Update, Read, and Delete single registrations</span></span> |<span data-ttu-id="bb121-127">建立/更新註冊</span><span class="sxs-lookup"><span data-stu-id="bb121-127">Create/Update registration</span></span><br><br><span data-ttu-id="bb121-128">讀取註冊</span><span class="sxs-lookup"><span data-stu-id="bb121-128">Read registration</span></span><br><br><span data-ttu-id="bb121-129">讀取控制代碼的所有註冊</span><span class="sxs-lookup"><span data-stu-id="bb121-129">Read all registrations for a handle</span></span><br><br><span data-ttu-id="bb121-130">刪除註冊</span><span class="sxs-lookup"><span data-stu-id="bb121-130">Delete registration</span></span> |
| <span data-ttu-id="bb121-131">傳送</span><span class="sxs-lookup"><span data-stu-id="bb121-131">Send</span></span> |<span data-ttu-id="bb121-132">傳送訊息 toohello 通知中樞</span><span class="sxs-lookup"><span data-stu-id="bb121-132">Send messages toohello notification hub</span></span> |<span data-ttu-id="bb121-133">傳送訊息</span><span class="sxs-lookup"><span data-stu-id="bb121-133">Send message</span></span> |
| <span data-ttu-id="bb121-134">管理</span><span class="sxs-lookup"><span data-stu-id="bb121-134">Manage</span></span> |<span data-ttu-id="bb121-135">對通知中樞執行 CRUD (包含更新 PNS 認證及安全性金鑰) 並依標記讀取的註冊</span><span class="sxs-lookup"><span data-stu-id="bb121-135">CRUDs on Notification Hubs (including updating PNS credentials, and security keys), and read registrations based on tags</span></span> |<span data-ttu-id="bb121-136">建立/更新/讀取/刪除通知中樞</span><span class="sxs-lookup"><span data-stu-id="bb121-136">Create/Update/Read/Delete notification hubs</span></span><br><br><span data-ttu-id="bb121-137">依標記讀取註冊</span><span class="sxs-lookup"><span data-stu-id="bb121-137">Read registrations by tag</span></span> |

<span data-ttu-id="bb121-138">通知中心接受授與 Microsoft Azure 存取控制權杖，以及產生含有設定直接在 hello 通知中樞上的共用金鑰簽章權杖的宣告。</span><span class="sxs-lookup"><span data-stu-id="bb121-138">Notification Hubs accept claims granted by Microsoft Azure Access Control tokens, and by signature tokens generated with shared keys configured directly on hello Notification Hub.</span></span>

