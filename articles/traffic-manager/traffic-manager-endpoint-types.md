---
title: "aaaTraffic 管理員端點類型 |Microsoft 文件"
description: "本文說明可搭配 Azure 流量管理員使用的各類型端點"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 4e506986-f78d-41d1-becf-56c8516e4d21
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: kumud
ms.openlocfilehash: 787412ac6207f76791bf3ff753d1df2767b1a964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoints"></a>流量管理員端點
Microsoft Azure Traffic Manager 可讓您的網路流量的方式 toocontrol 分散式 tooapplication 部署在不同的資料中心中執行。 您可以在流量管理員中將每個應用程式部署設定為「端點」。 Traffic Manager 收到 DNS 要求時，則會選擇可用端點 tooreturn hello DNS 回應中。 流量管理員來建立 hello 選擇 hello 目前端點的狀態與 hello 流量路由方法。 如需詳細資訊，請參閱 [流量管理員的運作方式](traffic-manager-how-traffic-manager-works.md)。

流量管理員支援三種類型的端點：
* **Azure 端點** 用於在 Azure 中裝載的服務。
* **外部端點** 用於 Azure 外部裝載的服務 (在內部部署或使用不同的主機服務提供者)。
* **巢狀端點**會使用的 toocombine Traffic Manager 設定檔 toocreate 更有彈性流量路由配置 toosupport hello 需求的較大且較為複雜的部署。

在單一流量管理員設定檔中結合不同類型的端點的方式不受限。 每個設定檔可以包含任意混合的端點類型。

hello 下列各節描述每個端點中的型別更大深度。

## <a name="azure-endpoints"></a>Azure 端點

在流量管理員中，Azure 端點用於以 Azure 為基礎的服務。 支援下列 Azure 資源類型的 hello:

* 「傳統」IaaS VM 和 PaaS 雲端服務。
* Web Apps
* PublicIPAddress 資源 （這可以是連線的 tooVMs，直接或透過 Azure 負載平衡器）。 hello publicIpAddress 必須指派 toobe Traffic Manager 設定檔中使用的 DNS 名稱。

PublicIPAddress 資源是 Azure Resource Manager 資源。 它們不存在於 hello 傳統部署模型。 因此，僅在流量管理員的 Azure Resource Manager 經驗中才支援。 hello 其他端點型別支援資源管理員和 hello 傳統部署模型。

使用 Azure 端點時，流量管理員會偵測「傳統」IaaS VM、雲端服務或 Web 應用程式何時停止和啟動。 此狀態會反映在 hello 端點狀態。 如需詳細資訊，請參閱[流量管理員端點監視](traffic-manager-monitoring.md#endpoint-and-profile-status)。 Hello 基礎服務停止時，Traffic Manager 不會執行端點健全狀況檢查或直接流量 toohello 端點。 計費的事件會發生在 hello 沒有 Traffic Manager 會停止執行個體。 當 hello 服務重新啟動，計費會繼續，而且 hello 端點合格 tooreceive 流量。 在此偵測不適用 tooPublicIpAddress 端點。

## <a name="external-endpoints"></a>外部端點

外部端點用於 Azure 外部的服務。 例如，在內部部署託管或使用不同提供者的服務。 外部端點可以個別使用或結合 Azure 端點 hello 中相同的流量管理員設定檔。 結合 Azure 端點與外部端點可以解決各種情況：

* 在主動-主動或主動-被動容錯移轉模型，使用 Azure tooprovide 增加備援現有內部部署應用程式。
* hello 世界各地的使用者 tooreduce 應用程式的延遲會擴充現有內部部署應用程式 tooadditional 地理位置在 Azure 中。 如需詳細資訊，請參閱[流量管理員「效能」流量路由](traffic-manager-routing-methods.md#performance)。
* 連續或做為 '高載至雲端' 方案 toomeet 突然增加的需求，請使用 Azure tooprovide 額外的容量，供現有的內部部署應用程式。

在某些情況下，很有用的 toouse 外部端點 tooreference Azure 服務 (如需範例，請參閱 hello[常見問題集](traffic-manager-faqs.md#traffic-manager-endpoints))。 在此情況下，健康情況檢查費率支付費用 hello Azure 端點，hello 外部端點速率。 不過，不同於 Azure 端點，如果您停止或刪除基礎服務的 hello 健全狀況檢查計費會繼續執行直到您停用或刪除 hello 端點 Traffic Manager 中。

## <a name="nested-endpoints"></a>巢狀端點

巢狀的端點結合多個 Traffic Manager 設定檔 toocreate 彈性流量路由配置，而且支援較大且複雜部署的 hello 需求。 具有巢狀端點 'child' 設定檔會加入為端點 tooa 'parent' 設定檔。 這兩個 hello 子系和父系設定檔可以包含任何類型，包括其他巢狀設定檔的其他端點。 如需詳細資訊，請參閱 [巢狀流量管理員設定檔](traffic-manager-nested-profiles.md)。

## <a name="web-apps-as-endpoints"></a>Web Apps 做為端點

將 Web Apps 設定為流量管理員中的端點時，適用其他一些考量：

1. 只有 Web 應用程式於 hello 'Standard' SKU 或更適合使用流量管理員。 嘗試 tooadd Web 應用程式的較低的 SKU 失敗。 現有的 Web 應用程式的 SKU 降級 hello 結果在 Traffic Manager 不會再傳送流量 toothat Web 應用程式。
2. 當端點會接收 HTTP 要求時，它會使用 hello 要求 toodetermine 中的 hello 'host' 標頭的 Web 應用程式服務 hello 要求。 hello 主機標頭包含 hello DNS 名稱使用 tooinitiate hello 要求，例如 'contosoapp.azurewebsites.net'。 toouse Web 應用程式，hello DNS 名稱不同的 DNS 名稱必須註冊為 hello 應用程式的自訂網域名稱。 將 Web 應用程式端點新增為 Azure 端點，hello Traffic Manager 設定檔的 DNS 名稱會自動為 hello 應用程式登錄。 刪除 hello 端點時，會自動移除此註冊。
3. 每個流量管理員設定檔最多可以有來自每個 Azure 區域的一個 Web 應用程式端點。 這個條件約束的周圍 toowork，您可以設定 Web 應用程式做為外部的端點。 如需詳細資訊，請參閱 hello[常見問題集](traffic-manager-faqs.md#traffic-manager-endpoints)。

## <a name="enabling-and-disabling-endpoints"></a>啟用和停用端點

停用 Traffic Manager 中端點可能有用 tootemporarily 移除處於維護模式或重新部署的端點流量。 一旦再次執行 hello 端點時，就可以重新啟用。

端點可以啟用和停用 hello Traffic Manager 入口網站、 PowerShell、 CLI 或 REST API，全部都是支援資源管理員和 hello 傳統部署模型。

> [!NOTE]
> 停用的 Azure 端點會執行任何動作 toodo 與 Azure 中的部署狀態。 Azure 服務 （例如 VM 或 Web 應用程式就持續執行，而且要能 tooreceive 流量即使停用 Traffic Manager 中。 您可以解決流量，直接 toohello 服務執行個體，而非透過 hello Traffic Manager 設定檔的 DNS 名稱。 如需詳細資訊，請參閱 [流量管理員的運作方式](traffic-manager-how-traffic-manager-works.md)。

每個端點 tooreceive 流量 hello 目前適合取決於下列因素的 hello:

* hello 設定檔狀態 （啟用/停用）
* hello 端點狀態 （啟用/停用）
* hello hello 為該端點的健全狀況檢查結果

如需詳細資訊，請參閱 [流量管理員端點監視](traffic-manager-monitoring.md#endpoint-and-profile-status)。

> [!NOTE]
> Traffic Manager 會在 hello DNS 層級運作，因為它是無法 tooinfluence 現有連線 tooany 端點。 端點無法使用時，Traffic Manager 將導向新連線 tooanother 可用端點。 不過，hello 主機後方 hello 停用或狀況不良的端點可能會繼續 tooreceive 流量透過現有的連線，直到這些工作階段已終止。 應用程式應該限制 hello 工作階段持續時間 tooallow 流量 toodrain 從現有的連接。

如果設定檔中的所有端點已停都用，或已停都用 hello 設定檔本身，Traffic Manager 會傳送 'NXDOMAIN' 回應 tooa 新的 DNS 查詢。


## <a name="next-steps"></a>後續步驟

* 了解 [流量管理員的運作方式](traffic-manager-how-traffic-manager-works.md)。
* 了解「流量管理員」的 [端點監視和自動容錯移轉](traffic-manager-monitoring.md)。
* 了解「流量管理員」的 [流量路由方法](traffic-manager-routing-methods.md)。
