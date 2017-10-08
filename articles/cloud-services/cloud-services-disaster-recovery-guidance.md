---
title: "在 Azure 雲端服務，將會影響 Azure 服務中斷的 hello 事件 aaaWhat toodo |Microsoft 文件"
description: "了解哪些 toodo hello Azure 雲端服務，將會影響 Azure 服務中斷事件中。"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: e52634ab-003d-4f1e-85fa-794f6cd12ce4
ms.service: cloud-services
ms.workload: cloud-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: mmccrory
ms.openlocfilehash: bb1f1835fc91a23772f81801b67d5786c190ba19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-of-an-azure-service-disruption-that-impacts-azure-cloud-services"></a>Azure 雲端服務，將會影響 Azure 服務中斷的 hello 事件中的哪些 toodo
Microsoft 在我們處理硬 toomake 確定我們的服務時，都是永遠可用 tooyou 需要它們。 有時候因為不可抗力之影響，造成服務意外中斷。

Microsoft 為其服務提供服務等級協定 (SLA)，作為執行時間和連接承諾。 hello SLA 個別 Azure 服務，請參閱[Azure 服務等級協定](https://azure.microsoft.com/support/legal/sla/)。

Azure 已經有許多支援高可用性應用程式的內建平台功能。 如需這些服務的詳細資訊，請參閱 [Azure 應用程式的災害復原與高可用性](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)。

本文涵蓋真正的災害復原案例中，當整個地區發生中斷，因為 toomajor 天然災害或廣泛的服務中斷時。 這些都是極少數的相符項目，但是您必須準備 hello 是整個區域發生中斷的可能性。 如果整個區域發生服務中斷，hello 本機備援份資料會暫時無法使用。 如果已啟用異地複寫，會在不同的區域儲存額外三份 Azure 儲存體 Blob 和資料表。 萬一 hello 的全面性地區中斷或災害中的 hello 主要區域是無法復原，Azure 重新對應所有 hello DNS 項目 toohello 進行地理複寫的區域。

> [!NOTE]
> 請注意，您完全無法控制這個程序，而且它只有在整個資料中心服務中斷時才會發生。 因為這個緣故，您必須也依賴其他應用程式特定的備份策略 tooachieve hello 最高層級的可用性。 如需詳細資訊，請參閱[建置在 Microsoft Azure 上之應用程式的災害復原和高可用性](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)。 如果您想要 toobe 無法 tooaffect 您自己的容錯移轉，您可能會想 tooconsider hello 使用[讀取權限的地理備援儲存體 (RA-GRS)](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage)，其中另一個區域中建立資料的唯讀副本。
>
>


## <a name="option-1-use-a-backup-deployment-through-azure-traffic-manager"></a>選項 1︰透過 Azure 流量管理員使用備份部署
hello 最強固的災害復原方案牽涉到維護多個部署的應用程式在不同的區域，然後使用[Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) toodirect 它們之間的流量。 Azure Traffic Manager 提供多個[路由方式](../traffic-manager/traffic-manager-routing-methods.md)，因此您可以選擇是否 toomanage 您使用的主要/備份模型或 toosplit 的部署之間的流量它們。

![使用 Azure 流量管理員平衡區域間的 Azure 雲端服務](./media/cloud-services-disaster-recovery-guidance/using-azure-traffic-manager.png)

Hello 最快回應 toohello 區域耗損，是很重要，您設定 Traffic Manager[端點監視](../traffic-manager/traffic-manager-monitoring.md)。

## <a name="option-2-deploy-your-application-tooa-new-region"></a>選項 2： 部署應用程式 tooa 的新區域
Hello 前一個選項中所述，維護多個作用中的部署帶來的額外成本。 如果您的復原時間目標 (RTO) 是有足夠的彈性，而且您擁有 hello 原始的程式碼或編譯的雲端服務封裝，您可以在另一個區域中建立您的應用程式的新執行個體，並更新您的 DNS 記錄 toopoint toohello 新部署。

如需詳細資訊的方式 toocreate 和部署雲端服務應用程式，請參閱[如何 toocreate 及部署雲端服務](cloud-services-how-to-create-deploy-portal.md)。

根據您應用程式的資料來源，您可能需要 toocheck hello 復原程序，您的應用程式資料來源。

* Azure 儲存體資料來源，請參閱[Azure 儲存體複寫](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage)toocheck hello 可用的選項根據 hello 上選擇您的應用程式的複寫模型。
* SQL 資料庫來源的讀取[概觀： 雲端 SQL Database 的業務續航力和資料庫嚴重損壞修復](../sql-database/sql-database-business-continuity.md)hello 選擇您的應用程式的複寫模型為基礎的 toocheck 上可用的 hello 選項。


## <a name="option-3-wait-for-recovery"></a>選項 3︰等待復原
在此情況下，不需要您採取動作是必要的但您的服務將無法使用，直到還原 hello 區域。 您可以在 hello 看到 hello 目前的服務狀態[Azure 服務健全狀況儀表板](https://azure.microsoft.com/status/)。

## <a name="next-steps"></a>後續步驟
深入了解如何 tooimplement 災害復原和高可用性策略，請參閱 toolearn[災害復原與高可用性 Azure 應用程式](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)。

toodevelop 詳細了解技術的雲端平台的功能，請參閱[Azure 復原技術的指引](../resiliency/resiliency-technical-guidance.md)。
