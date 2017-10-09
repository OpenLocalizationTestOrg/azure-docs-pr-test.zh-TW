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
# <a name="azure-log-integration-faq"></a><span data-ttu-id="e20ad-103">Azure 記錄整合常見問題集</span><span class="sxs-lookup"><span data-stu-id="e20ad-103">Azure Log Integration FAQ</span></span>
<span data-ttu-id="e20ad-104">本文提供 Azure 記錄整合的常見問題集 (FAQ) 解答。</span><span class="sxs-lookup"><span data-stu-id="e20ad-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span> 

<span data-ttu-id="e20ad-105">Azure 記錄檔整合是，您可以使用 toointegrate 原始記錄檔從您的 Azure 資源到您在內部部署安全性資訊和事件管理 (SIEM) 系統的 Windows 作業系統服務。</span><span class="sxs-lookup"><span data-stu-id="e20ad-105">Azure Log Integration is a Windows operating system service that you can use toointegrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="e20ad-106">這項整合提供統一的儀表板，針對所有的資產，在內部部署或 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="e20ad-106">This integration provides a unified dashboard for all your assets, on-premises or in hello cloud.</span></span> <span data-ttu-id="e20ad-107">您可以接著彙總、相互關聯、分析與應用程式建立關聯的安全性事件，並發出警示。</span><span class="sxs-lookup"><span data-stu-id="e20ad-107">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-hello-azure-log-integration-software-free"></a><span data-ttu-id="e20ad-108">Hello Azure 記錄檔整合軟體是免費的嗎？</span><span class="sxs-lookup"><span data-stu-id="e20ad-108">Is hello Azure Log Integration software free?</span></span>
<span data-ttu-id="e20ad-109">是。</span><span class="sxs-lookup"><span data-stu-id="e20ad-109">Yes.</span></span> <span data-ttu-id="e20ad-110">沒有 hello Azure 記錄檔整合軟體需付費。</span><span class="sxs-lookup"><span data-stu-id="e20ad-110">There is no charge for hello Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="e20ad-111">哪裡有提供 Azure 記錄整合？</span><span class="sxs-lookup"><span data-stu-id="e20ad-111">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="e20ad-112">它目前於 Azure Commercial 和 Azure Government 中提供，且無法在中國或德國使用。</span><span class="sxs-lookup"><span data-stu-id="e20ad-112">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="e20ad-113">如何查看 hello Azure 記錄檔整合為從中提取 Azure VM 的記錄檔的儲存體帳戶？</span><span class="sxs-lookup"><span data-stu-id="e20ad-113">How can I see hello storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>
<span data-ttu-id="e20ad-114">執行 hello 命令**azlog 來源清單**。</span><span class="sxs-lookup"><span data-stu-id="e20ad-114">Run hello command **azlog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a><span data-ttu-id="e20ad-115">如何分辨哪些訂閱 hello 記錄功能已從 Azure 記錄檔整合？</span><span class="sxs-lookup"><span data-stu-id="e20ad-115">How can I tell which subscription hello Azure Log Integration logs are from?</span></span>

<span data-ttu-id="e20ad-116">在稽核記錄檔放置在 hello 的案例中 hello **AzureResourcemanagerJson**目錄 hello 訂用帳戶 ID 位於 hello 記錄檔名稱。</span><span class="sxs-lookup"><span data-stu-id="e20ad-116">In hello case of audit logs that are placed in hello **AzureResourcemanagerJson** directories, hello subscription ID is in hello log file name.</span></span> <span data-ttu-id="e20ad-117">這也適用於記錄檔中 hello **AzureSecurityCenterJson**資料夾。</span><span class="sxs-lookup"><span data-stu-id="e20ad-117">This is also true for logs in hello **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="e20ad-118">例如：</span><span class="sxs-lookup"><span data-stu-id="e20ad-118">For example:</span></span>

<span data-ttu-id="e20ad-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span><span class="sxs-lookup"><span data-stu-id="e20ad-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="e20ad-120">Azure Active Directory 稽核記錄檔包含 hello 租用戶識別碼 hello 名稱的一部分。</span><span class="sxs-lookup"><span data-stu-id="e20ad-120">Azure Active Directory audit logs include hello tenant ID as part of hello name.</span></span>

<span data-ttu-id="e20ad-121">讀取自事件中心的診斷記錄檔不包含 hello 訂用帳戶 ID hello 名稱的一部分。</span><span class="sxs-lookup"><span data-stu-id="e20ad-121">Diagnostic logs that are read from an event hub do not include hello subscription ID as part of hello name.</span></span> <span data-ttu-id="e20ad-122">相反地，它們包含 hello hello 建立 hello 事件中樞來源中指定的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="e20ad-122">Instead, they include hello friendly name specified as part of hello creation of hello event hub source.</span></span> 

## <a name="how-can-i-update-hello-proxy-configuration"></a><span data-ttu-id="e20ad-123">如何更新 hello proxy 組態？</span><span class="sxs-lookup"><span data-stu-id="e20ad-123">How can I update hello proxy configuration?</span></span>
<span data-ttu-id="e20ad-124">如果您的 proxy 設定不直接允許存取 Azure 儲存體，開啟 hello **AZLOG。EXE。CONFIG**檔案**c:\Program Files\Microsoft Azure 記錄檔整合**。</span><span class="sxs-lookup"><span data-stu-id="e20ad-124">If your proxy setting does not allow Azure storage access directly, open hello **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="e20ad-125">更新 hello 檔案 tooinclude hello **defaultProxy** hello proxy 位址的組織的一節。</span><span class="sxs-lookup"><span data-stu-id="e20ad-125">Update hello file tooinclude hello **defaultProxy** section with hello proxy address of your organization.</span></span> <span data-ttu-id="e20ad-126">Hello 更新完成之後，停止並啟動 hello 服務使用 hello 命令**net stop azlog**和**net 啟動 azlog**。</span><span class="sxs-lookup"><span data-stu-id="e20ad-126">After hello update is done, stop and start hello service by using hello commands **net stop azlog** and **net start azlog**.</span></span>

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

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a><span data-ttu-id="e20ad-127">如何查看 Windows 事件中的 hello 訂用帳戶資訊？</span><span class="sxs-lookup"><span data-stu-id="e20ad-127">How can I see hello subscription information in Windows events?</span></span>
<span data-ttu-id="e20ad-128">Hello 訂用帳戶 ID toohello 易記名稱附加新增 hello 來源時：</span><span class="sxs-lookup"><span data-stu-id="e20ad-128">Append hello subscription ID toohello friendly name while adding hello source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="e20ad-129">hello 事件 XML 具有下列中繼資料，包括 hello 訂用帳戶 ID 的 hello:</span><span class="sxs-lookup"><span data-stu-id="e20ad-129">hello event XML has hello following metadata, including hello subscription ID:</span></span>

![事件 XML][1]

## <a name="error-messages"></a><span data-ttu-id="e20ad-131">錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="e20ad-131">Error messages</span></span>
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a><span data-ttu-id="e20ad-132">當我執行 hello 命令**azlog createazureid**，為什麼收到下列錯誤 hello？</span><span class="sxs-lookup"><span data-stu-id="e20ad-132">When I run hello command **azlog createazureid**, why do I get hello following error?</span></span>
<span data-ttu-id="e20ad-133">Error:</span><span class="sxs-lookup"><span data-stu-id="e20ad-133">Error:</span></span>

  <span data-ttu-id="e20ad-134">*Toocreate AAD 應用程式的租用戶 72f988bf-86f1-41af-91ab-2d7cd011db37-原因失敗，訊息 = '禁止'-= '權限不足，toocomplete hello operation'。*</span><span class="sxs-lookup"><span data-stu-id="e20ad-134">*Failed toocreate AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges toocomplete hello operation.'*</span></span>

<span data-ttu-id="e20ad-135">hello **azlog createazureid**命令嘗試的 toocreate hello Azure 登入的 hello 訂閱所有 hello Azure AD 租用戶中的服務主體具有存取權。</span><span class="sxs-lookup"><span data-stu-id="e20ad-135">hello **azlog createazureid** command attempts toocreate a service principal in all hello Azure AD tenants for hello subscriptions that hello Azure login has access to.</span></span> <span data-ttu-id="e20ad-136">如果您的 Azure 登入是僅有 guest 使用者的 Azure AD 租用戶中，hello 命令會失敗，「 權限不足，toocomplete hello 作業 」。</span><span class="sxs-lookup"><span data-stu-id="e20ad-136">If your Azure login is only a guest user in that Azure AD tenant, hello command fails with "Insufficient privileges toocomplete hello operation."</span></span> <span data-ttu-id="e20ad-137">詢問 hello 租用戶系統管理員 tooadd 您 hello 租用戶中的使用者身分的帳戶。</span><span class="sxs-lookup"><span data-stu-id="e20ad-137">Ask hello tenant admin tooadd your account as a user in hello tenant.</span></span>

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a><span data-ttu-id="e20ad-138">當我執行 hello 命令**azlog 授權**，為什麼收到下列錯誤 hello？</span><span class="sxs-lookup"><span data-stu-id="e20ad-138">When I run hello command **azlog authorize**, why do I get hello following error?</span></span>
<span data-ttu-id="e20ad-139">Error:</span><span class="sxs-lookup"><span data-stu-id="e20ad-139">Error:</span></span>

  <span data-ttu-id="e20ad-140">*警告 建立角色指派-AuthorizationFailed: hello client janedo@microsoft.com'與物件識別碼' fe9e03e4-4dad-4328-910f-fd24a9660bd2' 沒有授權 tooperform 動作 'Microsoft.Authorization/roleAssignments/write' 對範圍 ' /訂用帳戶/70 d 95299 d689 4 c 97 b971 0d8ff0000000'。*</span><span class="sxs-lookup"><span data-stu-id="e20ad-140">*Warning creating Role Assignment - AuthorizationFailed: hello client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="e20ad-141">hello **azlog 授權**命令指派 hello 的讀取器 toohello Azure AD 服務主體的角色 (使用建立**azlog createazureid**) toohello 提供訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e20ad-141">hello **azlog authorize** command assigns hello role of reader toohello Azure AD service principal (created with **azlog createazureid**) toohello provided subscriptions.</span></span> <span data-ttu-id="e20ad-142">如果 hello Azure 登入不是共同管理員或 hello 訂用帳戶的擁有者，它會失敗的 「 授權失敗 」 錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="e20ad-142">If hello Azure login is not a co-administrator or an owner of hello subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="e20ad-143">Azure 角色型存取控制 (RBAC) 的共同管理員或擁有者是所需的 toocomplete 此動作。</span><span class="sxs-lookup"><span data-stu-id="e20ad-143">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed toocomplete this action.</span></span>

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a><span data-ttu-id="e20ad-144">其中 hello 稽核記錄檔中找到 hello 屬性 hello 的定義？</span><span class="sxs-lookup"><span data-stu-id="e20ad-144">Where can I find hello definition of hello properties in hello audit log?</span></span>
<span data-ttu-id="e20ad-145">請參閱：</span><span class="sxs-lookup"><span data-stu-id="e20ad-145">See:</span></span>

* [<span data-ttu-id="e20ad-146">使用 Azure Resource Manager 來稽核作業</span><span class="sxs-lookup"><span data-stu-id="e20ad-146">Audit operations with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="e20ad-147">列出訂用帳戶中 hello Azure 監視 REST API 中的 hello 管理事件</span><span class="sxs-lookup"><span data-stu-id="e20ad-147">List hello management events in a subscription in hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="e20ad-148">哪裡可以找到 Azure 資訊安全中心警示的詳細資訊？</span><span class="sxs-lookup"><span data-stu-id="e20ad-148">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="e20ad-149">請參閱[中 Azure 資訊安全中心警示管理，而且有回應 toosecurity](../security-center/security-center-managing-and-responding-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="e20ad-149">See [Managing and responding toosecurity alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="e20ad-150">如何修改 VM 診斷會收集什麼？</span><span class="sxs-lookup"><span data-stu-id="e20ad-150">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="e20ad-151">如需 tooget，如何修改及設定 hello Azure 診斷組態，詳細資訊，請參閱[執行 Windows 的虛擬機器中使用 PowerShell tooenable Azure 診斷](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e20ad-151">For details on how tooget, modify, and set hello Azure Diagnostics configuration, see [Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="e20ad-152">下列範例中的 hello 取得 hello Azure 診斷組態：</span><span class="sxs-lookup"><span data-stu-id="e20ad-152">hello following example gets hello Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="e20ad-153">下列範例中的 hello 修改 hello Azure 診斷組態。</span><span class="sxs-lookup"><span data-stu-id="e20ad-153">hello following example modifies hello Azure Diagnostics configuration.</span></span> <span data-ttu-id="e20ad-154">在此組態中，只有事件識別碼 4624 和事件識別碼 4625 從收集 hello 安全性事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e20ad-154">In this configuration, only event ID 4624 and event ID 4625 are collected from hello security event log.</span></span> <span data-ttu-id="e20ad-155">Microsoft 反惡意程式碼的 Azure 事件會收集從 hello 系統事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e20ad-155">Microsoft Antimalware for Azure events are collected from hello system event log.</span></span> <span data-ttu-id="e20ad-156">如需 hello 使用 XPath 運算式的詳細資訊，請參閱[耗用事件](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85))。</span><span class="sxs-lookup"><span data-stu-id="e20ad-156">For details on hello use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="e20ad-157">hello 下列範例會設定 hello Azure 診斷組態：</span><span class="sxs-lookup"><span data-stu-id="e20ad-157">hello following example sets hello Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="e20ad-158">進行變更之後，請檢查 hello 儲存體帳戶 tooensure 該 hello 正確收集事件。</span><span class="sxs-lookup"><span data-stu-id="e20ad-158">After you make changes, check hello storage account tooensure that hello correct events are collected.</span></span>

<span data-ttu-id="e20ad-159">如果您在 hello 安裝和設定有任何問題，請開啟[支援要求](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request)。</span><span class="sxs-lookup"><span data-stu-id="e20ad-159">If you have any issues during hello installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="e20ad-160">選取**記錄 Integration**為 hello 服務您要求支援。</span><span class="sxs-lookup"><span data-stu-id="e20ad-160">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="e20ad-161">可以使用 Azure 記錄檔整合 toointegrate 網路監看員的記錄檔到我 SIEM 嗎？</span><span class="sxs-lookup"><span data-stu-id="e20ad-161">Can I use Azure Log Integration toointegrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="e20ad-162">Azure 網路監看員會產生大量的記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="e20ad-162">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="e20ad-163">這些記錄不會傳送它們的 toobe tooa SIEM。</span><span class="sxs-lookup"><span data-stu-id="e20ad-163">These logs are not meant toobe sent tooa SIEM.</span></span> <span data-ttu-id="e20ad-164">只支援 hello 目的地網路監看員的記錄檔是儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e20ad-164">hello only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="e20ad-165">Azure 記錄檔整合不支援讀取這些記錄檔，並使其可用 tooa SIEM。</span><span class="sxs-lookup"><span data-stu-id="e20ad-165">Azure Log Integration does not support reading these logs and making them available tooa SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
