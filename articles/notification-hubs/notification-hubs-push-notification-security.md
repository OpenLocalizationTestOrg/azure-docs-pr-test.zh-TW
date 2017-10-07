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
# <a name="security"></a>安全性
## <a name="overview"></a>概觀
本主題說明 Azure 通知中樞 hello 安全性模型。 由於通知中心為服務匯流排實體，這些物件實作 hello 與 Service Bus 相同的安全性模型。 如需詳細資訊，請參閱 hello[服務匯流排驗證](https://msdn.microsoft.com/library/azure/dn155925.aspx)主題。

## <a name="shared-access-signature-security-sas"></a>共用存取簽章的安全性 (SAS)
通知中樞會實作實體層級的安全性配置，稱為 SAS (共用存取簽章)。 此配置讓傳訊實體 toodeclare 描述 too12 授權規則，授與對該實體的權限。

每個規則包含名稱、 索引鍵的值 （共用密碼） 和一組權限，如述 hello > 一節 「 安全性宣告 」。 建立通知中心時，會自動建立兩個規則： 其中一個接聽的權限 （hello 用戶端應用程式使用)，另一個具有所有權限 （hello 應用程式後端會使用)。

如果透過傳送嗨資訊，從用戶端應用程式，請執行註冊管理時通知並不是敏感資訊 （如範例中，天氣更新），常見的方式 tooaccess 通知中樞的 hello 規則只限 「 接聽 」 存取 toohello toogive hello 機碼值用戶端應用程式和 toogive hello 索引鍵值 hello 規則的完整存取 toohello 應用程式後端。

不建議您在 Windows 市集用戶端應用程式中內嵌 hello 索引鍵值。 內嵌 hello 機碼值的方式 tooavoid 是 toohave hello 用戶端應用程式從擷取它在啟動 hello 應用程式後端。

請務必 toounderstand hello 與接聽 」 存取權的索引鍵，可讓用戶端應用程式 tooregister 任何標記。 如果您的應用程式必須限制註冊 toospecific 標記 toospecific 用戶端 （例如標籤表示使用者 Id 時），您的應用程式後端必須執行 hello 註冊。 如需詳細資訊，請參閱＜註冊管理＞。 請注意，如此一來，hello 用戶端應用程式將不需要直接存取 tooNotification 集線器。

## <a name="security-claims"></a>安全性宣告
類似 tooother 實體，通知中樞作業可以有三種安全性宣告： 接聽、 傳送和管理。

| 宣告 | 說明 | 允許的作業 |
| --- | --- | --- |
| 接聽 |建立/更新、讀取及刪除單一註冊 |建立/更新註冊<br><br>讀取註冊<br><br>讀取控制代碼的所有註冊<br><br>刪除註冊 |
| 傳送 |傳送訊息 toohello 通知中樞 |傳送訊息 |
| 管理 |對通知中樞執行 CRUD (包含更新 PNS 認證及安全性金鑰) 並依標記讀取的註冊 |建立/更新/讀取/刪除通知中樞<br><br>依標記讀取註冊 |

通知中心接受授與 Microsoft Azure 存取控制權杖，以及產生含有設定直接在 hello 通知中樞上的共用金鑰簽章權杖的宣告。

