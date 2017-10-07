---
title: "Azure Vm 的 aaaDisaster 復原案例 |Microsoft 文件"
description: "了解哪些 toodo hello Azure 服務中斷影響 Azure 虛擬機器的事件中。"
services: virtual-machines
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 65272148-ff06-4bce-91f1-851d706d4d40
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: kmouss;aglick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 839c6f9c51a7f35b48ef3636bc346eef332bb06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-that-an-azure-service-disruption-impacts-azure-vms"></a>Azure 服務中斷影響 Azure Vm 的 hello 事件中的哪些 toodo
Microsoft 在我們處理硬 toomake 確定我們的服務時，都是永遠可用 tooyou 需要它們。 有時候因為不可抗力之影響，造成服務意外中斷。

Microsoft 為其服務提供服務等級協定 (SLA)，作為執行時間和連接承諾。 hello SLA 個別 Azure 服務，請參閱[Azure 服務等級協定](https://azure.microsoft.com/support/legal/sla/)。

Azure 已經有許多支援高可用性應用程式的內建平台功能。 如需這些服務的詳細資訊，請參閱 [Azure 應用程式的災害復原與高可用性](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)。

本文涵蓋真正的災害復原案例中，當整個地區發生中斷，因為 toomajor 天然災害或廣泛的服務中斷時。 這些都是極少數的相符項目，但是您必須準備 hello 是整個區域發生中斷的可能性。 如果整個區域發生服務中斷，hello 本機備援份資料會暫時無法使用。 如果已啟用異地複寫，會在不同的區域儲存額外三份 Azure 儲存體 Blob 和資料表。 萬一 hello 的全面性地區中斷或災害中的 hello 主要區域是無法復原，Azure 重新對應所有 hello DNS 項目 toohello 進行地理複寫的區域。

toohelp 處理這些極少數的發生次數，我們提供下列指引 Azure 虛擬網路中的 hello Azure 虛擬機器應用程式部署所在的整個區域服務中斷的 hello 大小寫的 hello。

## <a name="option-1-initiate-a-failover-by-using-azure-site-recovery"></a>選項 1︰使用 Azure Site Recovery 起始容錯移轉
您可以為 VM 設定 Azure Site Recovery，如此一來，只要按一下花幾分鐘就能復原應用程式。 您可以在您選擇的 tooAzure 區域和不受限制的 toopaired 區域複寫。 您可以[複寫虛擬機器](https://aka.ms/a2a-getting-started)來開始進行。 您可以[建立復原計劃](../site-recovery/site-recovery-create-recovery-plans.md)，讓您可以自動化 hello 整個容錯移轉程序，您的應用程式。 您可以[測試您的容錯移轉](../site-recovery/site-recovery-test-failover-to-azure.md)可以事先做好而不會影響實際執行應用程式或 hello 進行中的複寫。 在您剛在 hello 事件中的主要區域中斷，[起始容錯移轉](../site-recovery/site-recovery-failover.md)目標區域中，讓您的應用程式狀態。


## <a name="option-2-wait-for-recovery"></a>選項 2︰等待復原
在此情況下，您不需要採取任何動作。 知道，我們正努力 toorestore 服務可用性。 您可以看到 hello 目前服務的狀態上我們[Azure 服務健全狀況儀表板](https://azure.microsoft.com/status/)。

如果未設定 Azure 站台復原 」、 「 讀取權限地理備援儲存體或 「 地理備援儲存體先前 toohello 中斷，這會是 hello 最佳選項。 如果您有設定地理備援儲存體或 hello 儲存體帳戶的讀取權限地理備援儲存體儲存 VM 虛擬硬碟 (Vhd)，您可以尋找 toorecover hello 基底映像 VHD，然後再次嘗試 tooprovision 中它的新 VM。 因為不保證能夠同步處理資料，所以這不是慣用的選項。 因此，此選項不保證 toowork。


> [!NOTE]
> 請注意，您完全無法控制這個程序，而且它只有在全區域服務中斷時才會發生。 因為這個緣故，您必須也依賴其他應用程式特定的備份策略 tooachieve hello 最高層級的可用性。 如需詳細資訊，請參閱 hello 一節[災害復原的資料策略](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery)。
>
>

## <a name="next-steps"></a>後續步驟

- 使用 Azure Site Recovery 開始[保護在 Azure 虛擬機器上執行的應用程式](https://aka.ms/a2a-getting-started)

- 深入了解如何 tooimplement 災害復原和高可用性策略，請參閱 toolearn[災害復原與高可用性 Azure 應用程式](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)。

- toodevelop 詳細了解技術的雲端平台的功能，請參閱[Azure 復原技術的指引](../resiliency/resiliency-technical-guidance.md)。


- 如果 hello 指示不清除，或如果您想要代表您的 Microsoft toodo hello 作業，請連絡[客戶支援](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。
