---
title: "aaaProtecting Azure 資訊安全中心 中的您網路 |Microsoft 文件"
description: "本文件說明可協助您保護 Azure 網路及遵守安全性原則的 Azure 資訊安全中心建議。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a>保護 Azure 資訊安全中心內的網路
Azure 資訊安全中心會分析您的 Azure 資源 hello 安全性狀態。 當資訊安全中心識別潛在的安全性漏洞時，它會建立可引導您完成設定所需的 hello 控制項的 hello 程序的建議。  適用於建議 tooAzure 資源類型： SQL，以及應用程式網路的虛擬機器 (Vm)。

本文適用 tooyour 網路的建議。  網路建議圍繞在新一代防火牆、網路安全性群組、設定輸入流量規則等等。  使用 hello 表當做參考 toohelp 您了解 hello 可用網路的建議，每個用途如果您將其套用。

## <a name="available-network-recommendations"></a>可用的網路建議
| 建議 | 說明 |
| --- | --- |
| [新增新一代防火牆](security-center-add-next-generation-firewall.md) |建議您將加入 下一步產生防火牆 (NGFW) 從 Microsoft 夥伴 tooincrease 安全性保護。 |
| [僅透過 NGFW 路由傳送流量](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |建議您設定網路安全性群組 (NSG) 規則強制傳入的流量 tooyour 透過您 NGFW VM。 |
| [啟用子網路/虛擬機器上的網路安全性群組](security-center-enable-network-security-groups.md) |建議您在子網路或 VM 上啟用 NSG。 |
| [透過網際網路面向端點限制存取](security-center-restrict-access-through-internet-facing-endpoints.md) |建議您為 NSG 設定輸入流量規則。 |

## <a name="see-also"></a>另請參閱
toolearn 深入了解建議，套用 tooother Azure 資源類型，請參閱 hello 下列資訊：

* [保護 Azure 資訊安全中心內的虛擬機器](security-center-virtual-machine-recommendations.md)
* [保護 Azure 資訊安全中心內的應用程式](security-center-application-recommendations.md)
* [保護 Azure 資訊安全中心內的 Azure SQL 服務](security-center-sql-service-recommendations.md)

toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
