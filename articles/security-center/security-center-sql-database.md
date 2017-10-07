---
title: "aaaAzure 資訊安全中心和 Azure SQL Database 服務 |Microsoft 文件"
description: "本文說明資訊安全中心如何協助您保護 Azure SQL Database 中的資料庫。"
services: sql-database
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f109adfd-daed-4257-9692-2042a1399480
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 173590500f0ce64140f214ada24b9692e01dbd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-sql-database-service"></a>Azure 資訊安全中心和 Azure SQL Database 服務
[Azure 資訊安全中心](https://azure.microsoft.com/documentation/services/security-center/)可協助您防止、 偵測，並回應 toothreats。 它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。

本文說明資訊安全中心如何協助您保護 Azure SQL Database 中的資料庫。

## <a name="why-use-security-center"></a>為何使用資訊安全中心？
資訊安全中心可協助您藉由提供可見性的所有伺服器和資料庫的 hello 安全性保護 SQL 資料庫中的資料。 使用資訊安全中心，您可以︰

* 定義 SQL Database 加密和稽核原則。
* 監視 SQL Database 資源 hello 安全性在所有訂閱。
* 快速找出並修復安全性問題。
* 整合 [Azure SQL Database 威脅偵測](../sql-database/sql-database-threat-detection.md)所提供的警示。

此外 toohelping 保護您的 SQL Database 資源，資訊安全中心也提供安全性監視及管理 Azure 虛擬機器、 雲端服務、 應用程式服務、 虛擬網路，等等。 [在此](security-center-intro.md)深入了解資訊安全中心。

## <a name="prerequisites"></a>必要條件
tooget 啟動與資訊安全中心，您必須擁有 Azure 的訂用帳戶 tooMicrosoft。 hello 免費層的資訊安全中心會啟用與您的訂用帳戶。 如需資訊安全中心的免費和標準層的詳細資訊，請參閱[安全性中心價格](https://azure.microsoft.com/pricing/details/security-center/)。

資訊安全中心支援角色型存取。 toolearn 進一步了解角色型存取控制 (RBAC) 在 Azure 中，請參閱[Azure Active Directory 角色型存取控制](../active-directory/role-based-access-control-configure.md)。 hello 安全性中心常見問題集提供的資訊[如何處理權限的資訊安全中心](security-center-faq.md#permissions)。

## <a name="access-security-center"></a>存取資訊安全中心
您可以存取的資訊安全中心從 hello [Azure 入口網站](https://azure.microsoft.com/features/azure-portal/)。 [登入 toohello 入口網站](https://portal.azure.com/)和選取 hello**資訊安全中心選項**。

![資訊安全中心選項][1]

hello**資訊安全中心**刀鋒視窗隨即開啟。
![資訊安全中心刀鋒視窗][2]

## <a name="set-security-policy"></a>設定安全性原則
安全性原則定義 hello 組 hello 指定訂用帳戶或資源群組中資源的建議使用的控制項。 資訊安全中心，您可以定義原則，您的訂用帳戶或資源群組，根據 tooyour 公司的安全性需求與 hello 的應用程式的類型或大小寫的每個訂用帳戶中的 hello 資料。

您可以設定原則 tooshow SQL 稽核和 SQL 透明資料加密 (TDE) 的建議。

* 當您開啟**SQL 稽核和威脅偵測**，資訊安全中心建議的相容性，進階偵測和調查的目的啟用稽核存取 tooAzure 資料庫。
* 當您開啟 [SQL 透明資料加密] 時，資訊安全中心會建議為您的 Azure SQL Database、關聯的備份及交易記錄檔啟用待用期加密。

tooset 安全性原則，選取 hello**原則**hello 資訊安全中心 刀鋒視窗上的磚。 在 hello**安全性原則**刀鋒視窗中，選取 hello 訂用帳戶，您會想 tooenable hello 安全性原則。 選取**防止原則**開啟**上**hello 想 toouse 此訂用帳戶的安全性建議。
安全性原則![][3]

詳細資訊，請參閱 toolearn[設定安全性原則](security-center-policies.md)。

## <a name="manage-security-recommendation"></a>管理安全性建議
資訊安全中心定期分析您的 Azure 資源 hello 安全性狀態。 當資訊安全中心識別潛在的安全性弱點時，它會建立建議。 hello 建議會引導您完成設定所需的 hello 控制項的 hello 程序。

設定安全性原則之後，資訊安全中心會分析資源 tooidentify 的潛在弱點的 hello 安全性狀態。 hello 建議會顯示以資料表格式，其中每一行代表一個特定的建議。 使用下表做為您了解 Azure SQL Database，並每項建議當您將它套用的 hello 可用建議參考 toohelp hello。 選取的建議會帶您 tooan 文章說明如何 tooimplement hello 資訊安全中心的建議。

| 建議 | 說明 |
| --- | --- |
| [在 SQL Server 上啟用稽核與威脅偵測](security-center-enable-auditing-on-sql-servers.md) |建議您針對 SQL Database 伺服器開啟稽核和威脅偵測功能。 (僅限 SQL Database 服務。 不包含在虛擬機器上執行的 Microsoft SQL Server。) |
| [在 SQL Database 上啟用稽核與威脅偵測](security-center-enable-auditing-on-sql-databases.md) |針對 SQL Database 資料庫開啟稽核和威脅偵測的建議。 (僅限 SQL Database 服務。 不包含在虛擬機器上執行的 Microsoft SQL Server。) |
| [啟用透明資料加密](security-center-enable-transparent-data-encryption.md) |建議您針對 SQL Database 啟用加密功能。 (僅限 SQL Database 服務。) |

您的 Azure 資源，選取 hello toosee 建議**建議**hello 資訊安全中心 刀鋒視窗上的磚。 在 hello**建議**刀鋒視窗中，選取建議 toosee 詳細資料。 在此範例中，我們選取 [在 SQL Server 上啟用稽核與威脅偵測]。

![建議][4]

資訊安全中心顯示 hello SQL 伺服器未啟用稽核與威脅偵測如下所示。 您開啟稽核功能之後，您可以設定威脅偵測以及設定電子郵件設定 tooreceive 安全性警示。 威脅偵測會通知您偵測到異常資料庫活動，以指出潛在的安全性威脅 toohello 資料庫時。 hello 警示會顯示 hello 資訊安全中心儀表板中。
![稽核與威脅偵測][5]

中的 hello 步驟[hello Azure 入口網站中的 SQL Database 威脅偵測](../sql-database/sql-database-threat-detection-portal.md)tooturn 上的及設定威脅偵測和 tooconfigure hello 清單將會收到偵測的異常活動時的安全性警示的電子郵件。

toolearn 深入了解建議事項，請參閱[管理安全性建議](security-center-recommendations.md)。

## <a name="monitor-security-health"></a>監視安全性健康狀態
啟用後[安全性原則](security-center-policies.md)訂用帳戶的資源資訊安全中心會分析 hello 安全性資源 tooidentify 的潛在弱點的風險。  您可以檢視您資源的 hello 安全性狀態中 hello**資源安全性健全狀況**磚。 當您按一下**資料**在 hello**資源安全性健全狀況**磚，hello**資料資源**刀鋒視窗中開啟的問題，例如稽核和透明 SQL 建議未啟用資料加密。 它也有 hello 資料庫 hello 一般健全狀況狀態的建議。
![資源安全性健康狀態][6]

詳細資訊，請參閱 toolearn[安全性健全狀況監視](security-center-monitoring.md)。

## <a name="manage-and-respond-toosecurity-alerts"></a>管理及回應 toosecurity 警示
資訊安全中心會自動收集、 分析，並將記錄資料從相整合[Azure SQL 威脅偵測](../sql-database/sql-database-threat-detection.md)、 以及其他 Azure 資源，toodetect 威脅，並降低誤判。 優先順序的安全性警示的清單會顯示在資訊安全中心，以及 hello 資訊需要 tooquickly 調查 hello 問題，並建議如何 tooremediate 攻擊。

toosee 警示，選取 hello**安全性警示**hello 資訊安全中心 刀鋒視窗上的磚。 在 hello**安全性警示**刀鋒視窗中，選取 hello 事件觸發 hello 警示，以及項目，如果有的話會引導您進一步了解警示 toolearn 需要 tootake tooremediate 攻擊。 在此範例中，我們選取 [潛在的 SQL 插入式攻擊] 。
![安全性警示][7]

資訊安全中心如下所示，可提供深入了解哪些觸發的 hello 警示 hello 的其他詳細資料時適用的 hello 來源 IP 位址和相關建議，目標資源，tooremediate。
![潛在的 SQL 插入式攻擊][8]

詳細資訊，請參閱 toolearn[管理，而且有回應 toosecurity 警示](security-center-managing-and-responding-alerts.md)。

## <a name="next-steps"></a>後續步驟
* [資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集。
* [資訊安全中心規劃及作業指南](security-center-planning-and-operations-guide.md)-請遵循一組步驟和工作 toooptimize 根據組織的安全性需求和雲端管理模型的資訊安全中心貴用戶使用。
* [資訊安全中心資料安全性](security-center-data-security.md) – 了解資訊安全中心如何收集和處理 Azure 資源的相關資料，包括組態資訊、中繼資料、事件記錄檔、損毀傾印檔等等。
* [處理安全性事件](security-center-incident.md)-了解如何 toouse hello 安全性警示功能的資訊安全中心 tooassist 您在處理安全性事件。

<!--Image references-->
[1]: ./media/security-center-sql-database/security-center.png
[2]: ./media/security-center-sql-database/security-center-blade.png
[3]: ./media/security-center-sql-database/security-policy.png
[4]: ./media/security-center-sql-database/recommendation.png
[5]: ./media/security-center-sql-database/turn-on-auditing.png
[6]: ./media/security-center-sql-database/monitor-health.png
[7]: ./media/security-center-sql-database/alert.png
[8]: ./media/security-center-sql-database/sql-injection.png
