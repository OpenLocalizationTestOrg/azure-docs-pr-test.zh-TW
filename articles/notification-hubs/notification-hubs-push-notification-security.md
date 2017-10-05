---
title: "通知中樞的安全性"
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
ms.openlocfilehash: 7c3283799806135060bb8ca57ea398c93d1106bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="security"></a><span data-ttu-id="ea27f-103">安全性</span><span class="sxs-lookup"><span data-stu-id="ea27f-103">Security</span></span>
## <a name="overview"></a><span data-ttu-id="ea27f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ea27f-104">Overview</span></span>
<span data-ttu-id="ea27f-105">本主題說明 Azure 通知中樞的安全性模型。</span><span class="sxs-lookup"><span data-stu-id="ea27f-105">This topic describes the security model of Azure Notification Hubs.</span></span> <span data-ttu-id="ea27f-106">因為通知中樞是服務匯流排實體，所以會實作與服務匯流排相同的安全性模型。</span><span class="sxs-lookup"><span data-stu-id="ea27f-106">Because Notification Hubs are a Service Bus entity, they implement the same security model as Service Bus.</span></span> <span data-ttu-id="ea27f-107">如需詳細資訊，請參閱 [服務匯流排驗證](https://msdn.microsoft.com/library/azure/dn155925.aspx) 的各項主題。</span><span class="sxs-lookup"><span data-stu-id="ea27f-107">For more information, see the [Service Bus Authentication](https://msdn.microsoft.com/library/azure/dn155925.aspx) topics.</span></span>

## <a name="shared-access-signature-security-sas"></a><span data-ttu-id="ea27f-108">共用存取簽章的安全性 (SAS)</span><span class="sxs-lookup"><span data-stu-id="ea27f-108">Shared Access Signature Security (SAS)</span></span>
<span data-ttu-id="ea27f-109">通知中樞會實作實體層級的安全性配置，稱為 SAS (共用存取簽章)。</span><span class="sxs-lookup"><span data-stu-id="ea27f-109">Notification Hubs implements an entity-level security scheme called SAS (Shared Access Signature).</span></span> <span data-ttu-id="ea27f-110">此配置讓傳訊實體最多可以在其授與該實體權限的描述中宣告 12 項規則。</span><span class="sxs-lookup"><span data-stu-id="ea27f-110">This scheme enables messaging entities to declare up to 12 authorization rules in their description that grant rights on that entity.</span></span>

<span data-ttu-id="ea27f-111">如＜安全性宣告＞一節所述，每項規則都包含名稱、索引鍵值 (共用密碼) 及一組權限。</span><span class="sxs-lookup"><span data-stu-id="ea27f-111">Each rule contains a name, a key value (shared secret), and a set of rights, as explained in the section “Security Claims.”</span></span> <span data-ttu-id="ea27f-112">建立通知中樞時，會自動建立兩項規則：一項具有接聽權限 (供用戶端應用程式使用)，另一項則具有所有權限 (供應用程式後端使用)。</span><span class="sxs-lookup"><span data-stu-id="ea27f-112">When creating a Notification Hub, two rules are automatically created: one with Listen rights (that the client app uses) and one with all rights (that the app backend uses).</span></span>

<span data-ttu-id="ea27f-113">從用戶端應用程式執行註冊管理時，若透過通知傳送的資訊不是敏感性資訊 (例如氣象更新)，常見存取通知中樞的方法是將只具接聽存取權限之規則的索引鍵值，授與用戶端應用程式，並將該規則之完整存取權限的索引鍵值，授與應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="ea27f-113">When performing registration management from client apps, if the information sent via notifications is not sensitive (for example, weather updates), a common way to access a Notification Hub is to give the key value of the rule Listen-only access to the client app, and to give the key value of the rule full access to the app backend.</span></span>

<span data-ttu-id="ea27f-114">不建議您將索引鍵值內嵌在 Windows 市集用戶端應用程式中。</span><span class="sxs-lookup"><span data-stu-id="ea27f-114">It is not recommended that you embed the key value in Windows Store client apps.</span></span> <span data-ttu-id="ea27f-115">避免將索引鍵值內嵌在用戶端應用程式中的方法，是讓用戶端應用程式在啟動時，再從應用程式後端擷取此值。</span><span class="sxs-lookup"><span data-stu-id="ea27f-115">A way to avoid embedding the key value is to have the client app retrieve it from the app backend at startup.</span></span>

<span data-ttu-id="ea27f-116">請務必了解，具有接聽權限的索引鍵可以讓用戶端應用程式註冊任何標記。</span><span class="sxs-lookup"><span data-stu-id="ea27f-116">It is important to understand that the key with Listen access allows a client app to register for any tag.</span></span> <span data-ttu-id="ea27f-117">若您的應用程式必須限制特定用戶端 (例如，當標記代表使用者識別碼時) 的註冊，您的應用程式後端就必須執行該註冊。</span><span class="sxs-lookup"><span data-stu-id="ea27f-117">If your app must restrict registrations to specific tags to specific clients (for example, when tags represent user IDs), then your app backend must perform the registrations.</span></span> <span data-ttu-id="ea27f-118">如需詳細資訊，請參閱＜註冊管理＞。</span><span class="sxs-lookup"><span data-stu-id="ea27f-118">For more information, see Registration Management.</span></span> <span data-ttu-id="ea27f-119">請注意，如此一來，用戶端應用程式將無法直接存取通知中樞。</span><span class="sxs-lookup"><span data-stu-id="ea27f-119">Note that in this way, the client app will not have direct access to Notification Hubs.</span></span>

## <a name="security-claims"></a><span data-ttu-id="ea27f-120">安全性宣告</span><span class="sxs-lookup"><span data-stu-id="ea27f-120">Security claims</span></span>
<span data-ttu-id="ea27f-121">與其他實體類似，通知中樞作業也可有接聽、傳送及管理三種安全性宣告。</span><span class="sxs-lookup"><span data-stu-id="ea27f-121">Similar to other entities, Notification Hub operations are allowed for three security claims: Listen, Send, and Manage.</span></span>

| <span data-ttu-id="ea27f-122">宣告</span><span class="sxs-lookup"><span data-stu-id="ea27f-122">Claim</span></span> | <span data-ttu-id="ea27f-123">說明</span><span class="sxs-lookup"><span data-stu-id="ea27f-123">Description</span></span> | <span data-ttu-id="ea27f-124">允許的作業</span><span class="sxs-lookup"><span data-stu-id="ea27f-124">Operations allowed</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ea27f-125">接聽</span><span class="sxs-lookup"><span data-stu-id="ea27f-125">Listen</span></span> |<span data-ttu-id="ea27f-126">建立/更新、讀取及刪除單一註冊</span><span class="sxs-lookup"><span data-stu-id="ea27f-126">Create/Update, Read, and Delete single registrations</span></span> |<span data-ttu-id="ea27f-127">建立/更新註冊</span><span class="sxs-lookup"><span data-stu-id="ea27f-127">Create/Update registration</span></span><br><br><span data-ttu-id="ea27f-128">讀取註冊</span><span class="sxs-lookup"><span data-stu-id="ea27f-128">Read registration</span></span><br><br><span data-ttu-id="ea27f-129">讀取控制代碼的所有註冊</span><span class="sxs-lookup"><span data-stu-id="ea27f-129">Read all registrations for a handle</span></span><br><br><span data-ttu-id="ea27f-130">刪除註冊</span><span class="sxs-lookup"><span data-stu-id="ea27f-130">Delete registration</span></span> |
| <span data-ttu-id="ea27f-131">傳送</span><span class="sxs-lookup"><span data-stu-id="ea27f-131">Send</span></span> |<span data-ttu-id="ea27f-132">將訊息傳送到通知中樞</span><span class="sxs-lookup"><span data-stu-id="ea27f-132">Send messages to the notification hub</span></span> |<span data-ttu-id="ea27f-133">傳送訊息</span><span class="sxs-lookup"><span data-stu-id="ea27f-133">Send message</span></span> |
| <span data-ttu-id="ea27f-134">管理</span><span class="sxs-lookup"><span data-stu-id="ea27f-134">Manage</span></span> |<span data-ttu-id="ea27f-135">對通知中樞執行 CRUD (包含更新 PNS 認證及安全性金鑰) 並依標記讀取的註冊</span><span class="sxs-lookup"><span data-stu-id="ea27f-135">CRUDs on Notification Hubs (including updating PNS credentials, and security keys), and read registrations based on tags</span></span> |<span data-ttu-id="ea27f-136">建立/更新/讀取/刪除通知中樞</span><span class="sxs-lookup"><span data-stu-id="ea27f-136">Create/Update/Read/Delete notification hubs</span></span><br><br><span data-ttu-id="ea27f-137">依標記讀取註冊</span><span class="sxs-lookup"><span data-stu-id="ea27f-137">Read registrations by tag</span></span> |

<span data-ttu-id="ea27f-138">通知中樞接受授 Microsoft Azure 存取控制權杖所授與的宣告，以及直接在通知中樞設定，由共用金鑰所產生之簽章權杖所授與的宣告。</span><span class="sxs-lookup"><span data-stu-id="ea27f-138">Notification Hubs accept claims granted by Microsoft Azure Access Control tokens, and by signature tokens generated with shared keys configured directly on the Notification Hub.</span></span>

