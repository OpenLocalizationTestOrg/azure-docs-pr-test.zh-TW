---
title: "使用 Azure aaaIntegrating Azure 資訊安全中心警示記錄 integration |Microsoft 文件"
description: "本文可協助您開始整合資訊安全中心警示與 Azure 記錄整合。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: d2d088d3-d38d-47ff-a062-c78e0fd59226
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: terrylan
ms.openlocfilehash: 2649036ee990bf0f48fa0cb35c7495ac932c29ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-security-center-alerts-with-azure-log-integration"></a>整合 Azure 資訊安全中心警示與 Azure 記錄整合
許多安全性作業和事件回應小組依賴安全性資訊和事件管理 (SIEM) 方案作為 hello 分級和調查安全性警示的起點。 透過 Azure 記錄整合，您可以將 Azure 資訊安全中心的警示與您的 SIEM 方案整合。

Azure 記錄整合目前支援 HP ArcSight、Splunk 及 IBM QRadar。

## <a name="what-logs-can-i-integrate"></a>可以整合哪些記錄檔？
Azure 會為每項服務產生大量記錄。 這些記錄檔會分類為︰

* **控制/管理記錄檔**，讓 hello 掌握 Azure 資源管理員建立、 更新和刪除作業。 這些控制項的平面事件便會顯示在 hello Azure 活動記錄檔
* **資料平面記錄**，讓掌握 hello 事件引發時使用的 Azure 資源。 例如，hello Windows 事件記錄檔，您可以在其中取得 hello 事件檢視器的安全性通道的安全性事件資訊。 資料平面事件 (由虛擬機器或 Azure 服務所產生) 會由 Azure 診斷記錄顯示。

Azure 記錄檔整合目前支援 hello 的整合：

* Azure VM 記錄檔
* Azure 稽核記錄檔
* Azure 資訊安全中心警示

## <a name="install-azure-log-integration"></a>安裝 Azure 記錄檔整合
下載 [Azure 記錄檔整合](https://www.microsoft.com/download/details.aspx?id=53324)。

hello Azure 記錄檔整合服務會從其安裝所在的 hello 機器收集遙測資料。  所收集的遙測資料是︰

* Azure 記錄檔整合的執行期間所發生的例外狀況
* 大約 hello 數目的查詢和處理事件的度量
* 正在使用哪些 Azlog.exe 命令列選項的相關統計資料

> [!NOTE]
> 您可以取消核取此選項，以關閉遙測資料的收集。
>
>

## <a name="integrate-azure-audit-logs-and-security-center-alerts"></a>整合 Azure 稽核記錄檔和資訊安全中心警示
1. 開啟 hello 命令提示字元和**cd**到**c:\Program Files\Microsoft Azure 記錄檔整合**。
2. 執行 hello **azlog createazureid**命令 toocreate [Azure Active Directory 服務主體](../active-directory/active-directory-application-objects.md)hello Azure Active Directory (AD) 中裝載的租用戶 hello Azure 訂用帳戶。

    系統會提示您登入 Azure。

   > [!NOTE]
   > 您必須是 hello 訂用帳戶擁有者或 hello 訂用帳戶的共同管理員。
   >
   >

    驗證 tooAzure 是透過 Azure AD。  建立 Azure 記錄檔整合的服務主體，會建立從 Azure 訂用帳戶有存取 tooread hello Azure AD 身分識別。
3. 執行 hello **azlog 授權<SubscriptionID>**命令 tooassign 步驟 2 中建立的 hello 訂用帳戶 toohello 服務主體上的讀取器存取。 如果您未指定**SubscriptionID**，那麼 hello 服務主體是指派的 hello 讀取器角色 tooall 訂閱 toowhich 可以存取。

   > [!NOTE]
   > 您可能會看見警告，如果您要執行 hello**授權**命令後面 hello **createazureid**命令。 會有些延遲 hello Azure AD 帳戶建立時與 hello 帳戶時可供使用。 如果您需要等候約 10 秒後執行 hello **createazureid**命令 toorun hello**授權**命令時，就不應該會看到這些警告。
   >
   >
4. 請檢查下列 hello 稽核記錄檔的 JSON 檔案的資料夾 tooconfirm hello 有：

   * **c:\Users\azlog\AzureResourceManagerJson**
   * **c:\Users\azlog\AzureResourceManagerJsonLD**
5. 請檢查下列資訊安全中心警示存在於它們的資料夾 tooconfirm hello:

   * **c:\Users\azlog\ AzureSecurityCenterJson**
   * **c:\Users\azlog\AzureSecurityCenterJsonLD**
6. 設定 hello SIEM 檔案轉寄站連接器 toohello 適當的資料夾。 hello 程序會隨著 hello 使用您的 SIEM。

## <a name="next-steps"></a>後續步驟
toolearn 深入了解 Azure 活動記錄檔和屬性的定義，請參閱：

* [使用 Resource Manager 來稽核作業](../azure-resource-manager/resource-group-audit.md)

toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) — 了解如何 toomanage 和回應 toosecurity 警示。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)— 取得最新 Azure 安全性消息 hello 和資訊。
