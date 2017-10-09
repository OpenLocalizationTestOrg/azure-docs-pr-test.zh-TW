---
title: "aaaLoad 平衡器自訂探查和監視的健全狀況狀態 |Microsoft 文件"
description: "了解如何自訂 toouse 探查 Azure 負載平衡器負載平衡器後方的 toomonitor 執行個體"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 46b152c5-6a27-4bfc-bea3-05de9ce06a57
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3dfcfcd2d5cffa58b160cb38d63acffbd997d452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-load-balancer-probes"></a>了解負載平衡器探查

Azure 負載平衡器使用探查提供 hello 功能 toomonitor hello 健全狀況的伺服器執行個體。 當探查失敗 toorespond 時，負載平衡器會停止傳送新連線 toohello 狀況不良的執行個體。 hello 現有的連接不受影響，還新的連線傳送 toohealthy 執行個體。

雲端服務角色 (背景工作角色和 Web 角色) 會使用客體代理程式進行探查監視。 當您在負載平衡器後方使用虛擬機器時，必須設定 TCP 或 HTTP 自訂探查。

## <a name="understand-probe-count-and-timeout"></a>了解探查計數及逾時

探查行為取決於︰

* hello 成功允許標示為執行個體 toobe 的探查數目。
* hello 會標示為停機的執行個體 toobe 造成的失敗探查數目。

hello 逾時和頻率的設定值 SuccessFailCount 判斷執行個體是否已確認的 toobe 執行或未執行。 在 hello Azure 入口網站，設定 tootwo hello 值倍 hello 頻率的 hello 逾時。

hello 探查設定所有負載平衡的執行個體的端點 （也就是負載平衡集） 必須是 hello 相同。 這表示您不能有不同的探查設定每個角色執行個體或虛擬機器在 hello 相同託管之特定端點組合的服務。 例如，每個執行個體必須具有相同的本機連接埠和逾時。

> [!IMPORTANT]
> 負載平衡器探查使用 hello IP 位址 168.63.129.16。 這個公用 IP 位址可加快 hello 帶您-擁有-IP Azure 虛擬網路案例的通訊 toointernal 平台資源。 hello 虛擬公用 IP 位址 168.63.129.16 用於所有區域中，不會變更。 建議您在任何本機防火牆原則中允許此 IP 位址。 它不應視為安全性風險因為只有 hello 內部 Azure 平台可以來源來自該位址的訊息。 如果不這麼做，會有未預期的行為中的各種案例，例如設定 hello 168.63.129.16 和具有重複的 IP 位址相同的 IP 位址範圍。

## <a name="learn-about-hello-types-of-probes"></a>深入了解探查的 hello 類型

### <a name="guest-agent-probe"></a>客體代理程式探查

此探查僅供 Azure 雲端服務使用。 負載平衡器會利用 hello hello 虛擬機器，內部的客體代理程式然後會接聽並回應 HTTP 200 OK 回應時，才 hello hello 就緒狀態中目前的執行個體 （也就是在另一個狀態例如忙碌、 回收、 或停止）。

如需詳細資訊，請參閱[設定 hello 服務定義檔 (csdef) 健全狀況探查](https://msdn.microsoft.com/library/azure/ee758710.aspx)或[開始建立雲端服務的網際網路對向負載平衡器](load-balancer-get-started-internet-classic-cloud.md#check-load-balancer-health-status-for-cloud-services)。

### <a name="what-makes-a-guest-agent-probe-mark-an-instance-as-unhealthy"></a>什麼原因會讓客體代理程式探查將執行個體標示為狀況不良？

如果 hello 客體代理程式無法與 HTTP 200 「 確定 toorespond，hello 負載平衡器標記 hello 為沒有回應的執行個體和停止傳送流量 toothat 執行個體。 hello 負載平衡器會繼續 tooping hello 執行個體。 如果 hello 客體代理程式回應 HTTP 200，hello 負載平衡器會再次傳送流量 toothat 執行個體。

當您使用 web 角色時，不會監視 hello Azure 網狀架構或客體代理程式的 w3wp.exe 中通常執行 hello 網站程式碼。 這表示 （例如，HTTP 500 回應） 的 w3wp.exe 中失敗將不會報告的 toohello 客體代理程式，，和 hello 負載平衡器會等到該執行個體退出循環。

### <a name="http-custom-probe"></a>HTTP 自訂探查

hello 自訂 HTTP 負載平衡器探查會覆寫 hello 預設客體代理程式探查，這表示您可以建立您自己的自訂邏輯 toodetermine hello 健全狀況的 hello 角色執行個體。 hello 負載平衡器探查您的端點每 15 秒，根據預設。 hello 例項會被視為 toobe hello 負載平衡器輪替循環中的，如果它的回應 HTTP 200 hello 逾時期限 （預設 31 秒） 內。

這可以是如果您想 tooimplement 您自己的邏輯 tooremove 執行個體從負載平衡器輪替。 比方說，您可以決定 tooremove 執行個體，如果它超過 90%的 CPU，並傳回-200 狀態。 如果您有使用 w3wp.exe 的 web 角色，這也表示您會自動監視您的網站，因為在網站上的程式碼中的失敗會傳回非 200 狀態 toohello 負載平衡器探查。

> [!NOTE]
> hello HTTP 自訂探查支援 HTTP 通訊協定只能和相對路徑。 不支援 HTTPS。

### <a name="what-makes-an-http-custom-probe-mark-an-instance-as-unhealthy"></a>什麼原因會讓 HTTP 自訂探查將執行個體標示為狀況不良？

* hello HTTP 應用程式會傳回 200 （例如，403、 404、 或 500） 以外的 HTTP 回應碼。 這是正值通知 hello 應用程式的執行個體應該超出服務以立即開始。
* hello HTTP 伺服器未完全回應 hello 逾時期限之後。 根據 hello 逾時設定的值，這可能表示該多個探查要求移至未接聽之前 hello 探查取得標示為不執行 （也就是前 SuccessFailCount 探查傳送）。
* hello 伺服器關閉 hello 連接，透過 TCP 重設。

### <a name="tcp-custom-probe"></a>TCP 自訂探查

TCP 探查起始的連線，藉由執行三種方式與信號交換 hello 定義連接埠。

### <a name="what-makes-a-tcp-custom-probe-mark-an-instance-as-unhealthy"></a>什麼原因會讓 TCP 自訂探查將執行個體標示為狀況不良？

* hello TCP 伺服器未完全回應 hello 逾時期限之後。 當 hello 探查標示為不執行 hello 失敗探查數目而定，要求是設定的 toogo 再將標示為不執行 hello 探查未接聽。
* hello 探查收到 hello 角色執行個體上重設的 TCP。

如需有關設定 HTTP 健全狀況探查或 TCP 探查的詳細資訊，請參閱 [開始使用 PowerShell 在資源管理員中建立網際網路對向負載平衡器](load-balancer-get-started-internet-arm-ps.md)。

## <a name="add-healthy-instances-back-into-load-balancer-rotation"></a>將狀況良好的執行個體重新加入負載平衡器循環

TCP 和 HTTP 探查被視為狀況良好，並將標示為狀況良好時 hello 角色執行個體：

* hello 負載平衡器取得第一個時間 hello VM 會開機正數探查 hello。
* hello 編號 SuccessFailCount （前述） 會定義 hello 成功的探查需要的 toomark hello 角色執行個體為狀況良好的值。 已移除的角色執行個體，如果成功，請連續探查的 hello 數目必須等於或超過 hello SuccessFailCount toomark hello 角色執行個體為 執行中的值。

> [!NOTE]
> 如果角色執行個體的 hello 健全狀況有變動，hello 負載平衡器的等候時間之前將 hello 角色執行個體放入 hello 狀況良好狀態。 這是透過原則 tooprotect hello 使用者和 hello 基礎結構。

## <a name="use-log-analytics-for-load-balancer"></a>使用負載平衡器的記錄分析

您可以使用[記錄分析的負載平衡器](load-balancer-monitor-log.md)toocheck hello 探查健全狀況狀態和探查計數。 記錄可以搭配負載平衡器健全狀況狀態相關的 Power BI 或 Azure Operational Insights tooprovide 統計資料。
