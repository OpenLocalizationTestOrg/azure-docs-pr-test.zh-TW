---
title: "與 Azure Active Directory 稽核記錄檔的記錄檔整合 aaaAzure |Microsoft 文件"
description: "了解 tooinstall hello Azure 記錄檔整合服務，並整合來自 Azure 稽核記錄檔記錄檔"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a>整合 Azure Active Directory 稽核記錄

Azure Active Directory (Azure AD) 稽核事件可協助您識別 Azure Active Directory 中發生的特殊權限動作。 您可以查看您可以藉由檢視追蹤的事件 hello 類型[Azure Active Directory 稽核報告事件](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md)。

> [!NOTE]
> 您嘗試在本文中的 hello 步驟之前，您必須檢閱 hello[開始](security-azure-log-integration-get-started.md)發行項，並完成 hello 步驟。

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a>步驟 toointegrate Azure Active directory 稽核記錄檔

1. 開啟 hello 命令提示字元並執行此命令：

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. 請執行這個命令： 
 
   ``azlog createazureid``

   此命令會提示您登入 Azure。 hello 命令接著會建立 Azure Active Directory 服務主體在 hello Azure AD 租用戶主機 hello Azure 訂用帳戶中的 hello 登入的使用者是系統管理員、 共同管理員或擁有者。 如果 hello 登入的使用者是只 hello Azure AD 租用戶中的 guest 使用者，hello 命令會失敗。 驗證 tooAzure 是透過 Azure AD。 建立 Azure 記錄檔整合的服務主體建立 hello 根據存取 tooread 指定 Azure 訂用帳戶的 Azure AD 身分識別。

3. 執行下列命令 tooprovide hello 您的租用戶識別碼。 您需要 hello 租用戶系統管理員角色 toorun hello 命令 toobe 的成員。

   ``Azlog.exe authorizedirectoryreader tenantId``

   範例：

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. 請檢查下列 hello Azure Active Directory 的稽核記錄檔 JSON 檔案的資料夾 tooconfirm hello 中加以建立：

   * **C:\Users\azlog\AzureActiveDirectoryJson**
   * **C:\Users\azlog\AzureActiveDirectoryJsonLD**

hello 下列影片示範 hello 涵蓋在本文中的步驟：

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> 如需有關將在 hello JSON 檔案中的 hello 資訊送回您的安全性資訊和事件管理 (SIEM) 系統的特定指示，請連絡您的 SIEM 廠商。

社群協助是透過 hello [Azure 記錄檔整合 MSDN 論壇](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration)。 此論壇可讓使用者在 hello Azure 記錄檔整合社群 toosupport 彼此與問題、 解答、 秘訣與訣竅。 此外，hello Azure 記錄檔整合小組監視此論壇，而且只要它可以幫助。

您也可以建立[支援要求](../azure-supportability/how-to-create-azure-support-request.md)。 選取**記錄 Integration**為 hello 服務您要求支援。

## <a name="next-steps"></a>後續步驟
toolearn 進一步了解 Azure 記錄檔整合，請參閱：

* [Azure 記錄的 Microsoft Azure 記錄整合](https://www.microsoft.com/download/details.aspx?id=53324)：此下載中心頁面會提供關於 Azure 記錄整合的詳細資料、系統需求和安裝指示。
* [簡介 tooAzure 記錄 Integration](security-azure-log-integration-overview.md)： 本文介紹您 tooAzure 記錄整合、 其重要功能，和它的運作方式。
* [夥伴的設定步驟](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/)： 此部落格文章會示範如何與 tooconfigure Azure 記錄檔整合 toowork 夥伴解決方案 Splunk，HP 討論 ArcSight 和 IBM QRadar。
* [Azure 記錄整合常見問題集](security-azure-log-integration-faq.md)：本文提供 Azure 記錄整合的相關問題解答。
* [資訊安全中心警示整合搭配 Azure 記錄檔整合](../security-center/security-center-integrating-alerts-with-log-integration.md)： 本文章將示範如何 toosync 資訊安全中心發出警示通知，以及虛擬機器的安全性事件收集 Azure 診斷和記錄分析 Azure 稽核記錄檔，或SIEM 解決方案。
* [新功能的 Azure 診斷及 Azure 稽核記錄檔](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/)： 此部落格文章向您介紹 tooAzure 稽核記錄檔和其他功能，可協助您深入了解您的 Azure 資源的 hello 作業。
