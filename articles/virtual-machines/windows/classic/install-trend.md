---
title: "在 VM 上 Trend Micro Deep Security aaaInstall |Microsoft 文件"
description: "本文說明如何 tooinstall 和設定 Trend 安全性與 hello 傳統部署模型，在 Azure 中建立的 VM 上。"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a>如何 tooinstall 和設定 Trend Micro Deep Security 作為 Windows VM 上的服務
> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

本文章將示範如何 tooinstall 和設定 Trend Micro Deep Security 作為新的或現有虛擬機器 (VM) 執行 Windows Server 上的服務。 Deep Security as a Service 包括反惡意程式碼防護、防火牆、入侵防禦系統及完整監視。

hello 用戶端會安裝為透過 hello VM 代理程式的安全性延伸模組。 新的虛擬機器中，您可以安裝 hello Deep Security Agent，為 hello hello Azure 入口網站所自動建立 VM 代理程式。

現有的 VM 使用 hello 傳統入口網站、 hello Azure CLI 或 PowerShell 建立可能沒有 VM 代理程式。 現有的虛擬機器沒有 hello VM 代理程式，您需要 toodownload 與先安裝它。 本文將探討這兩種狀況。

如果您有目前訂用帳戶趨勢科技從內部部署解決方案，您可以使用 toohelp 保護您的 Azure 虛擬機器。 如果您還不是 Symantec 客戶，您可以註冊試用訂用帳戶。 如需此解決方案的詳細資訊，請參閱 hello 趨勢科技部落格文章[Microsoft Azure VM 代理程式延伸模組的 Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945)。

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a>在新的 VM 上安裝 hello Deep Security Agent

hello [Azure 入口網站](http://portal.azure.com)可讓您安裝 hello 趨勢科技安全性延伸模組，當您使用映像從 hello **Marketplace** toocreate hello 虛擬機器。 如果您要建立單一的虛擬機器，使用 hello 入口網站是從趨勢科技輕鬆 tooadd 保護。

使用的項目從 hello **Marketplace**開啟精靈，可協助您設定 hello 虛擬機器。 使用 hello**設定**刀鋒視窗，hello hello 精靈 tooinstall hello 趨勢科技安全性延伸模組的第三個的面板。  一般指示，請參閱[建立執行 Windows hello Azure 入口網站中的虛擬機器](tutorial.md)。

當您取得 toohello**設定**刀鋒視窗中的 hello 精靈 中，執行下列步驟 hello:

1. 按一下**延伸**，然後按一下 **將延伸加入**hello 下一個窗格中。

   ![開始加入 hello 延伸模組][1]

2. 選取**Deep Security Agent**在 hello**新資源**窗格。 在 hello Deep Security Agent 窗格中，按一下 **建立**。

   ![識別 Deep Security Agent][2]

3. 輸入 hello**租用戶識別碼**和**租用戶啟用密碼**hello 延伸模組。 您可以選擇性地輸入**安全性原則識別碼**。 然後，按一下 **確定**tooadd hello 用戶端。

   ![提供擴充功能詳細資料][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a>在現有的 VM 上安裝 hello Deep Security Agent
現有的 VM 上 tooinstall hello 代理程式，您需要下列項目 hello:

* hello Azure PowerShell 模組、 0.8.2 版或更新版本，已安裝在本機電腦上。 您可以檢查 hello 版本的 Azure PowerShell，您已安裝使用 hello **Get-module azure | 格式資料表版本**命令。 如需指示和連結 toohello 最新版本，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。 登入 tooyour Azure 訂用帳戶使用`Add-AzureAccount`。
* hello hello 目標虛擬機器上安裝 VM 代理程式。

首先，確認已安裝 VM 代理程式的 hello。 填寫 hello 雲端服務名稱和虛擬機器名稱，然後執行下列命令，以系統管理員層級 Azure PowerShell 命令提示字元的 hello。 取代 hello 引號，包括 hello < 和 > 字元內的所有內容。

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

如果您不知道 hello 雲端服務和虛擬機器名稱，執行**Get-azurevm** toodisplay 所有資訊都 hello 您目前的訂用帳戶中的虛擬機器。

如果 hello**寫入主機**命令會傳回**True**，hello 安裝 VM 代理程式。 如果它傳回**False**，請參閱 hello 指示與下載 hello Azure 部落格文章中的連結 toohello [VM 代理程式和擴充功能-第 2 部分](http://go.microsoft.com/fwlink/p/?LinkId=403947)。

如果已安裝 VM 代理程式 hello，執行這些命令。

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a>後續步驟
花幾分鐘，讓 hello 代理程式 toostart 安裝時執行。 在這之後，您會需要 tooactivate Deep Security hello 虛擬機器上的，它可以管理由深層安全性管理員。 請參閱下列文章以取得其他指示的 hello:

* 與此解決方案相關的 Trend 文章： [Microsoft Azure 的即時雲端安全性](http://go.microsoft.com/fwlink/?LinkId=404101)
* A[範例 Windows PowerShell 指令碼](http://go.microsoft.com/fwlink/?LinkId=404100)tooconfigure hello 虛擬機器
* [指示](http://go.microsoft.com/fwlink/?LinkId=404099)hello 範例

## <a name="additional-resources"></a>其他資源
[如何 toolog tooa 虛擬機器執行 Windows Server 上]

[Azure VM 延伸模組與功能]

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[如何 toolog tooa 虛擬機器執行 Windows Server 上]:connect-logon.md
[Azure VM 延伸模組與功能]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
