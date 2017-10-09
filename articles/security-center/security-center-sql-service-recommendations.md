---
title: "aaaProtecting Azure SQL 服務與 Azure 資訊安全中心中的資料 |Microsoft 文件"
description: "本文件說明「Azure 資訊安全中心」中的建議，這些建議可協助您保護您的資料和 Azure SQL 服務，以及遵守安全性原則。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a>保護 Azure 資訊安全中心內的 Azure SQL 服務和資料
Azure 資訊安全中心會分析您的 Azure 資源 hello 安全性狀態。 當資訊安全中心識別潛在的安全性漏洞時，它會建立可引導您完成設定所需的 hello 控制項的 hello 程序的建議。  適用於建議 tooAzure 資源類型： SQL 和資料，以及應用程式網路的虛擬機器 (Vm)。

本文適用 tooAzure SQL 服務和資料的建議。 這些建議是以下列主題為中心：為 Azure SQL 伺服器和資料庫啟用稽核、為 SQL 資料庫啟用加密，以及啟用 Azure 儲存體帳戶加密。  使用 hello 表當做參考 toohelp 您了解 hello 可用 SQL 服務與資料的建議，每個用途如果您將其套用。

## <a name="available-sql-service-and-data-recommendations"></a>可用的 SQL 服務和資料建議
| 建議 | 說明 |
| --- | --- |
| [在 SQL Server 上啟用稽核與威脅偵測](security-center-enable-auditing-on-sql-servers.md) |建議您針對 Azure SQL Server 開啟稽核與威脅偵測 (僅適用於 Azure SQL 服務，不包括在您虛擬機器上執行的 SQL)。 |
| [在 SQL 資料庫上啟用稽核與威脅偵測](security-center-enable-auditing-on-sql-databases.md) |建議您針對 Azure SQL Database 開啟稽核與威脅偵測 (僅適用於 Azure SQL 服務，不包括在您虛擬機器上執行的 SQL)。 |
| [在 SQL 資料庫上啟用透明資料加密](security-center-enable-transparent-data-encryption.md) |建議您針對 SQL 資料庫啟用加密 (僅適用於 Azure SQL 服務)。 |

## <a name="see-also"></a>另請參閱
toolearn 深入了解建議，套用 tooother Azure 資源類型，請參閱 hello 下列資訊：

* [保護 Azure 資訊安全中心內的虛擬機器](security-center-virtual-machine-recommendations.md)
* [保護 Azure 資訊安全中心內的應用程式](security-center-application-recommendations.md)
* [保護 Azure 資訊安全中心內的網路](security-center-network-recommendations.md)

toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
