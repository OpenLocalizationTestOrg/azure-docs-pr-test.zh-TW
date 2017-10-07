---
title: "Analysis Services 的高可用性 aaaAzure |Microsoft 文件"
description: "確保 Azure Analysis Services 的高可用性。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a>Analysis Services 的高可用性
本文說明如何確保 Azure Analysis Services 伺服器的高可用性。 


## <a name="assuring-high-availability-during-a-service-disruption"></a>在服務中斷期間確保高可用性
雖然很罕見，但 Azure 資料中心也可能會有中斷的時候。 發生中斷時，業務可能只會中斷幾分鐘，也可能會持續幾小時。 高可用性最常透過伺服器備援來實現。 使用 Azure Analysis Services，您就可以藉由在一或多個區域建立其他的次要伺服器來實現備援。 當在那些伺服器上建立備援伺服器、 tooassure hello 資料和中繼資料是在同步處理與 hello 伺服器區域中，已離線，您可以：

* 部署模型 tooredundant 伺服器中的其他區域。 此方法需要平行處理主要伺服器和備援伺服器的資料，以確保所有伺服器保持同步。

* 從主要伺服器備份資料庫並還原到備援伺服器上。 比方說，您可以自動化夜間備份 tooAzure 存放裝置，並還原 tooother 備援伺服器的其他區域中。 

在任一情況下，如果您的主要伺服器發生中斷，您必須變更在報表中不同的地區資料中心的用戶端 tooconnect toohello 伺服器 hello 連接字串。 此變更作業應視為最後手段，只有在發生重大的區域資料中心中斷時才應考慮使用。 比較常見的情況是，您可能還未更新所有用戶端上的連線，裝載主要伺服器的資料中心就已從中斷狀態恢復為上線狀態。 



## <a name="related-information"></a>相關資訊
[備份與還原](analysis-services-backup.md)   
[管理 Azure Analysis Services](analysis-services-manage.md) 

