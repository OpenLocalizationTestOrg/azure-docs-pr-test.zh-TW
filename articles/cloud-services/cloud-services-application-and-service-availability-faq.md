---
title: "aaaApplication 和服務可用性問題的 Microsoft Azure 雲端服務的常見問題集 |Microsoft 文件"
description: "本文列出 hello 常見問題集有關應用程式和服務可用性的 Microsoft Azure 雲端服務。"
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: cd0d9ba0beb1dc72d4761f8b89c2ecadb51c7e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Azure 雲端服務之應用程式和服務可用性問題：常見問題集 (FAQ)

本文包含 [Microsoft Azure 雲端服務](https://azure.microsoft.com/services/cloud-services)之應用程式和服務可用性問題的相關常見問題集。 此外，您也可以參考 hello[雲端服務 VM 大小頁面](cloud-services-sizes-specs.md)大小資訊。

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a>我的角色被回收了。 我的雲端服務是否推出任何更新？
Microsoft 大約一個月會發行一次適用於 Windows Azure PaaS VM 的新客體 OS 版本。 客體 OS 是 hello 管線中的只能有一個這類更新。 發行可能會受到許多其他因素所影響。 此外，Azure 是在成千上萬個電腦上執行。 因此，它是不可能 toopredict hello 確切日期和時間時將重新啟動您的角色。 我們更新客體 OS 更新 RSS 摘要的 hello 與 hello 最新的資訊，我們有，但您應該考慮，報告時間 toobe 近似的值。 我們了解這是對於客戶而言有問題，並使用計劃 toolimit 或精確時間重新開機。

如需最新客體 OS 更新的完整詳細資訊，請參閱 [Azure 客體 OS 版本與 SDK 相容性矩陣](cloud-services-guestos-update-matrix.md)。

很有幫助的來賓和主機作業系統更新的重新啟動和指標 tootechnical 詳細資料的詳細資訊，請參閱 hello MSDN 部落格文章[角色執行個體因而重新啟動 tooOS 升級](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)。

## <a name="why-does-hello-first-request-toomy-cloud-service-after-hello-service-has-been-idle-for-some-time-take-longer-than-usual"></a>為什麼沒有 hello 第一個要求 toomy 雲端服務之後，hello 服務閒置段時間比平常長？
Hello 網頁伺服器收到 hello 第一個要求時，它會先重新編譯 hello 程式碼，然後再處理 hello 要求。 原因是其他人 hello 第一個要求所花費的時間比 hello。 根據預設，hello 應用程式集區取得關閉在使用者閒置的情況下。 hello 應用程式集區將也會進行回收預設每隔 1,740 分鐘 （29 小時）。

網際網路資訊服務 (IIS) 應用程式集區可以定期回收的 tooavoid 可能會導致 tooapplication 當機、 無回應或記憶體流失的不穩定狀態。

下列文件的 hello 將協助您了解並減輕這個問題：
* [修正 IIS 的緩慢初始載入](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis)
* [應用程式集區回收非常緩慢之後 IIS 7.5 Web 應用程式的第一個要求](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow)

如果您想 toochange hello IIS 的預設行為，您需要 toouse 啟動工作，因為如果您手動套用變更 toohello Web 角色執行個體，最後會 hello 變更遺失。

如需詳細資訊，請參閱[tooconfigure] 和 [執行啟動工作的雲端服務的方式](cloud-services-startup-tasks.md)。
