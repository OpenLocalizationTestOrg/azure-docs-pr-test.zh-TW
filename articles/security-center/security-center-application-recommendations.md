---
title: "aaaProtecting Azure 資訊安全中心中的應用程式 |Microsoft 文件"
description: "本文件說明可協助您保護 Azure 應用程式及遵守安全性原則的 Azure 資訊安全中心建議。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: b5fc7a9e-24b1-415f-b3b5-62a53f5dd424
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: terrylan
ms.openlocfilehash: da5e02cc2bad55c64e4da14e4e10efd6ddeab39e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-applications-in-azure-security-center"></a>保護 Azure 資訊安全中心內的應用程式
Azure 資訊安全中心會分析您的 Azure 資源 hello 安全性狀態。 當資訊安全中心識別潛在的安全性漏洞時，它會建立可引導您完成設定所需的 hello 控制項的 hello 程序的建議。  適用於建議 tooAzure 資源類型： SQL，以及應用程式網路的虛擬機器 (Vm)。

本文適用 tooapplications 的建議。  應用程式建議圍繞在 Web 應用程式防火牆的部署。  使用 hello 表當做參考 toohelp 您了解 hello 可用的應用程式的建議，每個用途如果您將其套用。

## <a name="available-application-recommendations"></a>可用的應用程式建議
| 建議 | 說明 |
| --- | --- |
| [新增 Web 應用程式防火牆](security-center-add-web-application-firewall.md) |建議您為 Web 端點部署「Web 應用程式防火牆」(WAF)。 系統會針對任何具有相關聯網路安全性群組 (包含開放輸入 Web 連接埠 (80,443)) 的公開 IP (執行個體層級 IP 或負載平衡 IP)，顯示 WAF 建議。</br></br>資訊安全中心建議您佈建 WAF toohelp 防禦目標 web 應用程式的 App Service 環境和虛擬機器上的攻擊。 App Service 環境 (ASE) 是Azure App Service 的 [Premium](https://azure.microsoft.com/pricing/details/app-service/) 服務方案選項，可提供完全隔離和專用的環境，以便安全地執行 Azure App Service 應用程式。 toolearn 深入了解 ASE，請參閱 hello[應用程式服務環境的文件](../app-service/app-service-app-service-environments-readme.md)。</br></br>您可以藉由新增這些應用程式 tooyour 現有 WAF 部署保護的資訊安全中心中的多個 web 應用程式。 |
| [完成應用程式保護](security-center-add-web-application-firewall.md#finalize-application-protection) |toocomplete hello 的 WAF，流量必須路由的 toohello WAF 應用裝置。 遵循這個建議完成 hello 必要的設定變更。 |

## <a name="see-also"></a>另請參閱
toolearn 深入了解建議，套用 tooother Azure 資源類型，請參閱 hello 下列資訊：

* [保護 Azure 資訊安全中心內的虛擬機器](security-center-virtual-machine-recommendations.md)
* [保護 Azure 資訊安全中心內的網路](security-center-network-recommendations.md)
* [保護 Azure 資訊安全中心內的 Azure SQL 服務](security-center-sql-service-recommendations.md)

toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
