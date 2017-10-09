---
title: "Office 與 Azure RemoteApp aaaUsing |Microsoft 文件"
description: "了解 Office 和 Azure RemoteApp 如何共同運作"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: f1773baf-8aa1-423c-a2f9-e4679e0463d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d065c1a0a2191c9e2e405264a835cecf791d6ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-office-with-azure-remoteapp"></a>使用 Office 與 Azure RemoteApp 搭配
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

在 Azure RemoteApp 中裝載 Office 應用程式有兩個選項：Office 365 ProPlus 或 Office 2013 Professional Plus 試用版。

**您知道我們即將取代這篇文章的更佳新文章嗎？簽出[如何 toouse 您 Office 365 訂用帳戶與 Azure RemoteApp 一起](remoteapp-officesubscription.md)。它涵蓋了所有您需要使用 Office 365 + Azure RemoteApp 的 hello 資訊。**

## <a name="office-365-proplus"></a>Office 365 ProPlus
您可以建立 RemoteApp 集合，使用 Office 365 ProPlus hello 範本映像。 此選項可讓您 tooextend 您 Office 365 服務 tooRemoteApp。 您必須擁有現有的訂用帳戶方案和您的使用者必須獲得授權，hello Office 365 ProPlus 服務，獨立或透過 hello Office 365 服務方案。

RemoteApp 支援 Office 365 共用電腦啟用。 當您啟用共用的電腦啟動過程中，並使用 hello [Office 部署工具](http://www.microsoft.com/download/details.aspx?id=36778)進行安裝，Office 365 ProPlus 會安裝但不啟動。 使用者會登入集合，包含 Office 365，Office 會檢查 toosee 如果已針對 Office 365 ProPlus hello 使用者佈建。 因此，Office 暫時啟用 Office 365 ProPlus-如果此啟用持續發生，直到停止 hello 服務該使用者登。

toouse Office 365 共用電腦啟動，您需要 toocreate[自訂範本](remoteapp-create-custom-image.md)並安裝 Office 365 ProPlus 存在，請遵循[這些指示](https://technet.microsoft.com/library/dn782858.aspx)。

您可以管理使用者的 Office 365 授權在 hello [Office 365 系統管理入口網站](https://portal.office365.com/)。 閱讀更多關於 [Office 365 服務方案](http://technet.microsoft.com/library/office-365-plan-options.aspx)的資訊。  

## <a name="office-2013-professional-plus-trial"></a>Office 2013 Professional Plus 試用版
在 RemoteApp 的 30 天試用版，您可以使用 hello Office 2013 Professional Plus （試用版） 範本映像 toocreate RemoteApp 集合。 您可以指派使用者 toothis 透過他們的 Azure Active Directory 工作帳戶或 Microsoft 帳戶的試用版集合。 不需再另外訂閱。

這是絕佳的選項 tookick hello 輪胎和良好感受 RemoteApp 中的 Office。 不過，此選項僅適用於評估和測試。 使用 hello Office 2013 Professional Plus （試用版） 範本映像建立 RemoteApp 集合無法轉換的 tooproduction 模式，且結尾 hello hello 試用期間將會停用。

## <a name="switching-from-trial-tooproduction"></a>從試用 tooproduction 切換
當您啟動您的 30 天免費試用版時，請注意，在 hello RemoteApp 區段 hello 入口網站會告訴您多久之前還剩下 hello 試用需要 tootransition tooa 付費帳戶。 您可以啟用您帳戶的和交換器 tooproduction 模式使用此注意事項中的 hello 連結。

當您啟動您的帳戶時，這會影響您的帳戶中的所有 hello RemoteApp 集合。

* 執行 Windows Server 2012 R2 hello 或 hello Office 365 ProPlus 範本映像的集合就會順暢地轉換 tooproduction。 所有使用者資料與設定 (包括進行中的工作階段) 都將維持不變。
* 如果您已上傳自訂範本映像，使用這些映像的收藏也將順利轉換。
* 僅供評估是 hello Office 2013 Professional Plus （試用版） 範本映像。 執行的範本映像的集合不能轉換的 tooproduction。 它們會成為「停用」狀態。

如果您無法執行轉換 tooproduction 模式由 hello 到期的試用版，將會停用 RemoteApp 集合。 也請別擔心-您的設定和使用者的資料會儲存另一個 90 天，所以您仍然可以啟動您的服務和交換器 tooproduction 模式不會遺失任何資料。

