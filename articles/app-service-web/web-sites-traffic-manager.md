---
title: "aaaControlling Azure web 應用程式流量搭配 Azure 流量管理員"
description: "本文章提供 Azure Traffic Manager 的摘要資訊與相關 tooAzure web 應用程式。"
services: app-service\web
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: dabda633-e72f-4dd4-bf1c-6e945da456fd
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: a93d4c9370046d54e401e36e7b495af8b711a2aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-azure-web-app-traffic-with-azure-traffic-manager"></a>使用 Azure 流量管理員來控制 Azure Web 應用程式的流量
> [!NOTE]
> 本文提供 Microsoft Azure Traffic Manager 的摘要資訊與相關 tooAzure App Service Web 應用程式。 瀏覽 hello 本文結尾處的 hello 連結可以找到有關 Azure Traffic Manager 本身的詳細資訊。
> 
> 

## <a name="introduction"></a>簡介
您可以使用 Azure Traffic Manager toocontrol 來自 web 用戶端要求的 Azure App Service 中的分散式的 tooweb 應用程式的方式。 當 web 應用程式端點加入 tooa Azure 流量管理員設定檔時，Azure Traffic Manager 會追蹤的 hello （執行中、 已停止或已刪除） 的 web 應用程式狀態，讓它可以決定這些端點應該接收流量。

## <a name="load-balancing-methods"></a>負載平衡方法
Azure 流量管理員使用三種不同的負載平衡方法。 這些都是以 hello 與 tooAzure web 應用程式清單後面所述。

* **容錯移轉**： 如果您有 web 應用程式複製程式碼在不同的區域中，您可以使用此方法 tooconfigure 一個 web 應用程式 tooservice 所有的 web 用戶端流量，並在流量案例 hello 第一個 web 應用程式中不同的區域 tooservice 中設定其他 web 應用程式會變成無法使用。
* **循環配置資源**： 如果您有 web 應用程式複製程式碼在不同的區域中，您可以使用此方法 toodistribute 流量平均跨不同區域中的 hello web 應用程式。
* **效能**: hello 效能方法會根據 hello 最短的來回行程時間 tooclients 的流量。 hello 效能方法可以用於 hello 內的 web 應用程式相同區域或不同區域。

## <a name="web-apps-and-traffic-manager-profiles"></a>Web 應用程式和流量管理員設定檔
tooconfigure hello web 應用程式流量控制，您在 Azure Traffic Manager 中使用其中一個 hello 三個負載平衡方法，建立設定檔，然後再新增想 toocontrol 流量 toohello 的 hello 端點 （在此情況下，web 應用程式）設定檔。 Web 應用程式狀態 （執行中、 已停止或已刪除） 會定期溝通的 toohello 設定檔，讓 Azure Traffic Manager 可以將流量導向據此。

時搭配 Azure 使用 Azure Traffic Manager，請遵循點注意 hello:

* Web 應用程式僅部署 hello 內相同的區域，Web 應用程式已提供容錯移轉和循環配置資源的功能，而不會考慮 tooweb 應用程式模式。
* 針對部署在 hello 與另一個 Azure 雲端服務搭配使用 Web 應用程式的相同區域中，您可以結合兩種類型的端點 tooenable 混合式案例。
* 在設定檔中，您只能針對每個地區指定一個 Web 應用程式。 當您選取的 web 應用程式為端點，一個區域時，hello 其餘的 web 應用程式在該區域變成無法選取該設定檔中。
* 您在 Azure Traffic Manager 設定檔中指定的 hello web 應用程式端點會出現在 hello**網域名稱**區段 hello hello hello 設定檔中的 web 應用程式設定 頁面上，但不是會設定有。
* 加入 web 應用程式 tooa 設定檔之後，hello**網站 URL** hello 儀表板的 hello web 上應用程式的入口網站頁面會顯示 hello hello web 應用程式的自訂網域 URL 如果您已設定其中一個。 否則，它會顯示 hello Traffic Manager 設定檔 URL (例如， `contoso.trafficmgr.com`)。 同時 hello hello web 應用程式的直接的網域名稱，hello 流量管理員 URL 就可以看到在 hello hello web 應用程式的 [設定] 頁面上**網域名稱**> 一節。
* 自訂網域名稱運作正常，但在加法 tooadding 它們 tooyour web 應用程式，您也必須設定您的 DNS 對應 toopoint toohello 流量管理員 URL。 如需詳細資訊請參閱 < Azure web 應用程式中，自訂網域 tooset[設定 Azure 網站的自訂網域名稱](app-service-web-tutorial-custom-domain.md)。
* 您只能新增標準或進階模式 tooa Azure 流量管理員設定檔中的 web 應用程式。

## <a name="next-steps"></a>後續步驟
如需 Azure 流量管理員的概念和技術概觀，請參閱 [Traffic Manager 概觀](../traffic-manager/traffic-manager-overview.md)。

如需與 Web 應用程式使用 Traffic Manager 的詳細資訊，請參閱 hello 部落格文章[使用 Azure Traffic Manager 與 Azure 網站](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx)和[Azure 流量管理員現在可以整合與 Azure 網站](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/)。

