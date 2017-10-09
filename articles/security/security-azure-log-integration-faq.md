---
title: "aaaAzure 記錄 Integration 常見問題集 |Microsoft 文件"
description: "本文提供 Azure 記錄整合的相關問題解答。"
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: d06d1ac5-5c3b-49de-800e-4d54b3064c64
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload8: na
ms.date: 08/07/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: e886035c9a180d0cd5fcbe9cc02483782df6dbe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-faq"></a>Azure 記錄整合常見問題集
本文提供 Azure 記錄整合的常見問題集 (FAQ) 解答。 

Azure 記錄檔整合是，您可以使用 toointegrate 原始記錄檔從您的 Azure 資源到您在內部部署安全性資訊和事件管理 (SIEM) 系統的 Windows 作業系統服務。 這項整合提供統一的儀表板，針對所有的資產，在內部部署或 hello 雲端中。 您可以接著彙總、相互關聯、分析與應用程式建立關聯的安全性事件，並發出警示。

## <a name="is-hello-azure-log-integration-software-free"></a>Hello Azure 記錄檔整合軟體是免費的嗎？
是。 沒有 hello Azure 記錄檔整合軟體需付費。

## <a name="where-is-azure-log-integration-available"></a>哪裡有提供 Azure 記錄整合？

它目前於 Azure Commercial 和 Azure Government 中提供，且無法在中國或德國使用。

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a>如何查看 hello Azure 記錄檔整合為從中提取 Azure VM 的記錄檔的儲存體帳戶？
執行 hello 命令**azlog 來源清單**。

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a>如何分辨哪些訂閱 hello 記錄功能已從 Azure 記錄檔整合？

在稽核記錄檔放置在 hello 的案例中 hello **AzureResourcemanagerJson**目錄 hello 訂用帳戶 ID 位於 hello 記錄檔名稱。 這也適用於記錄檔中 hello **AzureSecurityCenterJson**資料夾。 例如：

20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json

Azure Active Directory 稽核記錄檔包含 hello 租用戶識別碼 hello 名稱的一部分。

讀取自事件中心的診斷記錄檔不包含 hello 訂用帳戶 ID hello 名稱的一部分。 相反地，它們包含 hello hello 建立 hello 事件中樞來源中指定的易記名稱。 

## <a name="how-can-i-update-hello-proxy-configuration"></a>如何更新 hello proxy 組態？
如果您的 proxy 設定不直接允許存取 Azure 儲存體，開啟 hello **AZLOG。EXE。CONFIG**檔案**c:\Program Files\Microsoft Azure 記錄檔整合**。 更新 hello 檔案 tooinclude hello **defaultProxy** hello proxy 位址的組織的一節。 Hello 更新完成之後，停止並啟動 hello 服務使用 hello 命令**net stop azlog**和**net 啟動 azlog**。

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress=http://127.0.0.1:8888
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a>如何查看 Windows 事件中的 hello 訂用帳戶資訊？
Hello 訂用帳戶 ID toohello 易記名稱附加新增 hello 來源時：

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
hello 事件 XML 具有下列中繼資料，包括 hello 訂用帳戶 ID 的 hello:

![事件 XML][1]

## <a name="error-messages"></a>錯誤訊息
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a>當我執行 hello 命令**azlog createazureid**，為什麼收到下列錯誤 hello？
Error:

  *Toocreate AAD 應用程式的租用戶 72f988bf-86f1-41af-91ab-2d7cd011db37-原因失敗，訊息 = '禁止'-= '權限不足，toocomplete hello operation'。*

hello **azlog createazureid**命令嘗試的 toocreate hello Azure 登入的 hello 訂閱所有 hello Azure AD 租用戶中的服務主體具有存取權。 如果您的 Azure 登入是僅有 guest 使用者的 Azure AD 租用戶中，hello 命令會失敗，「 權限不足，toocomplete hello 作業 」。 詢問 hello 租用戶系統管理員 tooadd 您 hello 租用戶中的使用者身分的帳戶。

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a>當我執行 hello 命令**azlog 授權**，為什麼收到下列錯誤 hello？
Error:

  *警告 建立角色指派-AuthorizationFailed: hello client janedo@microsoft.com'與物件識別碼' fe9e03e4-4dad-4328-910f-fd24a9660bd2' 沒有授權 tooperform 動作 'Microsoft.Authorization/roleAssignments/write' 對範圍 ' /訂用帳戶/70 d 95299 d689 4 c 97 b971 0d8ff0000000'。*

hello **azlog 授權**命令指派 hello 的讀取器 toohello Azure AD 服務主體的角色 (使用建立**azlog createazureid**) toohello 提供訂用帳戶。 如果 hello Azure 登入不是共同管理員或 hello 訂用帳戶的擁有者，它會失敗的 「 授權失敗 」 錯誤訊息。 Azure 角色型存取控制 (RBAC) 的共同管理員或擁有者是所需的 toocomplete 此動作。

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a>其中 hello 稽核記錄檔中找到 hello 屬性 hello 的定義？
請參閱：

* [使用 Azure Resource Manager 來稽核作業](../azure-resource-manager/resource-group-audit.md)
* [列出訂用帳戶中 hello Azure 監視 REST API 中的 hello 管理事件](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a>哪裡可以找到 Azure 資訊安全中心警示的詳細資訊？
請參閱[中 Azure 資訊安全中心警示管理，而且有回應 toosecurity](../security-center/security-center-managing-and-responding-alerts.md)。

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a>如何修改 VM 診斷會收集什麼？
如需 tooget，如何修改及設定 hello Azure 診斷組態，詳細資訊，請參閱[執行 Windows 的虛擬機器中使用 PowerShell tooenable Azure 診斷](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 

下列範例中的 hello 取得 hello Azure 診斷組態：

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

下列範例中的 hello 修改 hello Azure 診斷組態。 在此組態中，只有事件識別碼 4624 和事件識別碼 4625 從收集 hello 安全性事件記錄檔。 Microsoft 反惡意程式碼的 Azure 事件會收集從 hello 系統事件記錄檔。 如需 hello 使用 XPath 運算式的詳細資訊，請參閱[耗用事件](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85))。

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

hello 下列範例會設定 hello Azure 診斷組態：

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

進行變更之後，請檢查 hello 儲存體帳戶 tooensure 該 hello 正確收集事件。

如果您在 hello 安裝和設定有任何問題，請開啟[支援要求](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request)。 選取**記錄 Integration**為 hello 服務您要求支援。

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a>可以使用 Azure 記錄檔整合 toointegrate 網路監看員的記錄檔到我 SIEM 嗎？

Azure 網路監看員會產生大量的記錄資訊。 這些記錄不會傳送它們的 toobe tooa SIEM。 只支援 hello 目的地網路監看員的記錄檔是儲存體帳戶。 Azure 記錄檔整合不支援讀取這些記錄檔，並使其可用 tooa SIEM。

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
