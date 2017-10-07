---
title: "不受管理的雲端應用程式使用 Cloud App Discovery aaaFinding |Microsoft 文件"
description: "提供有關尋找和管理應用程式，其中包含 Cloud App Discovery hello 優點為何，它的運作方式的資訊。"
services: active-directory
keywords: "雲端應用程式探索, 管理應用程式"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a>使用 Cloud App Discovery 尋找未受管理的雲端應用程式
## <a name="overview"></a>概觀
現代企業 IT 部門通常不會察覺所有的 hello 雲端應用程式，其組織的成員使用 toodo 其工作。 它是簡單 toosee 為什麼系統管理員就必須考慮未經授權的存取 toocorporate 資料、 可能的資料流失和其他安全性風險。 缺乏認知可能使得要建立一個可應付這些安全性風險的計劃讓人卻步。

雲端應用程式探索是 Azure Active Directory (AD) Premium 可讓您組織中的 hello 人士使用 toodiscover 雲端應用程式的功能。

**使用 Cloud App Discovery，您可以：**

* 尋找所使用的 hello 雲端應用程式和使用者數目、 流量或 web 要求 toohello 應用程式的數目來測量使用量。
* 找出 hello 使用者使用應用程式。
* 匯出資料以進行離線分析。
* 讓這些應用程式在 IT 的控制下並為使用者管理啟用單一登入。

## <a name="how-it-works"></a>運作方式
1. 應用程式使用代理程式會安裝在使用者的電腦上。
2. 透過安全加密通道 toohello 雲端應用程式探索服務傳送 hello hello 代理程式所擷取的應用程式使用資訊。
3. hello Cloud App Discovery 服務評估 hello 資料，並產生報告。

![Cloud App Discovery 圖表](./media/active-directory-cloudappdiscovery/cad01.png)

tooget 開始使用 Cloud App Discovery，請參閱[快速入門開始使用 Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)

## <a name="related-articles"></a>相關文章
* [Cloud App Discovery 的安全性和隱私權考量](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [Cloud App Discovery 群組原則部署指南](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [Cloud App Discovery System Center 部署指南](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [具有自訂連接埠的 Proxy 伺服器的 Cloud App Discovery 登錄設定](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [Cloud App Discovery 代理程式變更記錄 ](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [Cloud App Discovery 常見問題集](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](active-directory-apps-index.md)

