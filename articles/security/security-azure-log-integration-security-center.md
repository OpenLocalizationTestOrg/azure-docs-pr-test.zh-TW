---
title: "aaaAzure 記錄整合與資訊安全中心 |Microsoft 文件"
description: "了解如何 tooget Azure 安全性中心警示使用的記錄檔整合"
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
ms.date: 03/22/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: bcc208d071ec03738215f2aee3b71c7b10927904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-your-security-center-alerts-in-azure-log-integration"></a>如何 tooget 資訊安全中心中的警示 Azure 記錄檔整合
本文章提供 hello 步驟需要的 tooenable hello Azure 記錄檔整合服務 toopull Azure 資訊安全中心所產生的警示安全性資訊。 您必須已順利完成 hello 中的 hello 步驟[開始](security-azure-log-integration-get-started.md)發行項，然後再執行本文章中的 hello 步驟。

## <a name="detailed-steps"></a>詳細步驟
hello 下列步驟將會建立 hello 需要 Azure Active Directory 服務主體，然後指派 hello 服務原則的讀取權限 toohello 訂用帳戶：
1. 開啟 hello 命令提示字元並瀏覽過**c:\Program Files\Microsoft Azure 記錄檔整合**
2. 執行 hello 命令``azlog createazureid``

    此命令會提示您登入 Azure。 hello 命令接著會建立[Azure Active Directory 服務主體](../active-directory/develop/active-directory-application-objects.md)hello 中裝載的 Azure AD 租用戶 hello Azure 訂用帳戶中的 hello 登入的使用者是系統管理員、 共同管理員或擁有者。 如果 hello 登入的使用者是只 hello Azure AD 租用戶中的 Guest 使用者，hello 命令會失敗。 驗證 tooAzure 是透過 Azure Active Directory (AD)。 建立服務主體 Azlog 整合建立 hello 會獲得存取 tooread 從 Azure 訂用帳戶的 Azure AD 身分識別。

2. 接下來您將會執行指派讀取器存取，在步驟 2 中建立的 hello 訂用帳戶 toohello 服務主體上的命令。 如果您未指定訂用帳戶 Id，hello 命令將嘗試 tooassign hello 服務主體的讀取器角色 tooall 訂閱 toowhich 任何存取。 </br></br>
``azlog authorize <SubscriptionID>`` </br> 例如 </br>
``azlog authorize 0ee55555-0bc4-4a32-a4e8-c29980000000``

    >[!NOTE]
    您可能會看見警告，如果您要執行 hello hello createazureid 命令之後立刻授權命令。 會有些延遲 hello Azure AD 帳戶建立時與 hello 帳戶時可供使用。 如果等候大約 60 秒後執行 hello createazureid 命令 toorun hello 授權命令，則您應該不會看到這些警告。

4. 請檢查下列 hello 稽核記錄檔的 JSON 檔案的資料夾 tooconfirm hello 有：
 * **c:\Users\azlog\AzureResourceManagerJson**
 * **c:\Users\azlog\AzureResourceManagerJsonLD** </br></br>
5. 請檢查下列資訊安全中心警示存在於它們的資料夾 tooconfirm hello:</br></br>
 * **c:\Users\azlog\AzureSecurityCenterJson**
 * **c:\Users\azlog\AzureSecurityCenterJsonLD** </br></br>

如果 hello 安裝和設定期間遇到任何問題，請開啟[支援要求](/azure-supportability/how-to-create-azure-support-request.md)，選取**記錄 Integration**為 hello 服務您要求支援。

## <a name="next-steps"></a>後續步驟
toolearn 進一步了解 Azure 記錄檔整合，請參閱下列文件的 hello:

* [Azure 記錄檔的 Microsoft Azure 記錄整合](https://www.microsoft.com/download/details.aspx?id=53324) – Azure 記錄整合詳細資料、系統需求和安裝指示的下載中心。
* [簡介 tooAzure 記錄 integration](security-azure-log-integration-overview.md) – 這份文件會為您介紹 tooAzure 記錄整合、 其重要功能，和它的運作方式。
* [夥伴的設定步驟](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/)– 此部落格文章會示範 tooconfigure Azure 與協力廠商解決方案 Splunk、 HP 討論 ArcSight 和 IBM QRadar 所記錄的整合 toowork。
* [Azure 記錄整合常見問題集 (FAQ)](security-azure-log-integration-faq.md) - 此常見問題集會回答有關 Azure 記錄整合的問題。
* [整合的資訊安全中心與 Azure 的警示記錄 Integration](../security-center/security-center-integrating-alerts-with-log-integration.md) – 本文件說明如何 toosync 資訊安全中心發出警示通知，以及虛擬機器的安全性事件記錄分析收集 Azure 診斷和 Azure 稽核記錄檔，或SIEM 解決方案。
* [Azure 診斷和 Azure 稽核記錄檔的新功能](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/)– 此部落格文章向您介紹 tooAzure 稽核記錄檔和其他功能，可協助您深入了解您的 Azure 資源的 hello 作業。
