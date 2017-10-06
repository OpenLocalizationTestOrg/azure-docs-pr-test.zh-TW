---
title: "Azure 備份：Linux VM 的應用程式一致備份 | Microsoft Docs"
description: "使用指令碼 tooguarantee 應用程式一致備份 tooAzure，針對您的 Linux 虛擬機器。 hello 指令碼適用於只能在資源管理員部署; tooLinux Vmhello 指令碼不會套用 tooWindows Vm 或服務管理員部署。 這篇文章會引導您設定 hello 指令碼，包括疑難排解 hello 步驟。"
services: backup
documentationcenter: dev-center-name
author: anuragmehrotra
manager: shivamg
keywords: "應用程式一致備份; 應用程式一致 Azure VM 備份; Linux VM 備份; Azure 備份"
ms.assetid: bbb99cf2-d8c7-4b3d-8b29-eadc0fed3bef
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/12/2017
ms.author: anuragm;markgal
ms.openlocfilehash: d557dd973364d79bb4d8ce954f648de835dd345f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-consistent-backup-of-azure-linux-vms-preview"></a>Azure Linux VM 的應用程式一致備份 (預覽)

這篇文章討論需 hello Linux 前指令碼後置指令碼架構及方式，它可以是使用的 tootake Azure Linux Vm 的應用程式一致的備份。

> [!Note]
> hello 前指令碼和後置指令碼架構的 Azure Resource Manager 部署的 Linux 虛擬機器才支援。 Service Manager 所部署虛擬機器或 Windows 虛擬機器不支援應用程式一致指令碼。
>

## <a name="how-hello-framework-works"></a>Hello 架構的運作方式

hello framework 會提供選項 toorun 自訂前指令碼，並後置指令碼時，您要將 VM 的快照集。 前指令碼執行之前採取 hello VM 快照，且您拍攝 hello VM 快照後立即執行後置指令碼。 這讓您 hello 彈性 toocontrol 應用程式和環境時，您要將 VM 的快照集。

在此案例中，很重要的 tooensure 應用程式一致的 VM 備份。 hello 前指令碼可以叫用應用程式原生 Api tooquiesce hello IOs，並清除記憶體中內容 toohello 磁碟。 這可確保該 hello 快照集是應用程式一致 (亦即該 hello 應用程式出現時 VM 會開機的 hello 還原後)。 後置指令碼可以使用的 toothaw hello IOs。 它會使用應用程式原生應用程式開發介面，以便 hello 應用程式可繼續正常作業 post VM 快照集。

## <a name="steps-tooconfigure-pre-script-and-post-script"></a>步驟 tooconfigure 前指令碼和後置指令碼

1. Hello 根使用者 toohello 要 tooback 的 Linux VM，因為在登入。

2. 下載**VMSnapshotScriptPluginConfig.json**從[GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig)，然後將它複製 toohello **/etc/hosts azure**所有您要設定 tooback hello Vm 上的資料夾。 建立 hello **/etc/hosts azure**目錄，如果已經存在。

3. 將複製 hello 前指令碼和應用程式上所有 hello Vm 的想向上 tooback 後指令碼。 您可以複製 hello VM 上的 hello 指令碼 tooany 位置。 可確定 tooupdate hello 完整的路徑 hello 指令碼檔案中 hello **VMSnapshotScriptPluginConfig.json**檔案。

4. 請確定下列這些檔案的權限的 hello:

   - **VMSnapshotScriptPluginConfig.json**：權限 “600”。 例如，只有 「 根 」 使用者應該具有 「 讀取 」 和 「 寫入 」 權限 toothis 檔案，而使用者不應該有 「 執行 」 權限。

   - **前置指令碼檔案**：權限 “700”。  例如，只有 「 根 」 使用者應該具有 「 讀取 」、 「 寫入 」 和 「 執行 」 權限 toothis 檔案。
  
   - **後置指令碼**：權限 “700”。 例如，只有 「 根 」 使用者應該具有 「 讀取 」、 「 寫入 」 和 「 執行 」 權限 toothis 檔案。

   > [!Important]
   > hello framework 會提供強大的使用者。 請務必安全的做法是，只有 「 根 」 使用者具有存取 toocritical JSON 和指令碼檔案。
   > 如果不符合 hello 先前的需求，hello 指令碼無法執行。 這能產生檔案系統/損毀一致的備份。
   >

5. 如以下所述設定 VMSnapshotScriptPluginConfig.json：
    - **pluginName**：將此欄位保留原狀，否則您的指令碼可能無法如預期般運作。

    - **preScriptLocation**: hello 的持續 toobe 備份的 VM 提供 hello hello 前指令碼的完整路徑。

    - **postScriptLocation**: hello 的持續 toobe 備份的 VM 提供 hello hello 後指令碼的完整路徑。

    - **preScriptParams**： 提供 hello 需要 toobe 傳遞 toohello 前指令碼的選擇性參數。 所有參數都應該以引號括住，如果有多個參數，則應以逗號分隔。

    - **postScriptParams**： 提供 hello 需要 toobe 傳遞 toohello 後指令碼的選擇性參數。 所有參數都應該以引號括住，如果有多個參數，則應以逗號分隔。

    - **preScriptNoOfRetries**： 設定應該重試 hello 前指令碼，如果沒有任何錯誤，結束之前的 hello 次數。 零表示只嘗試一次，若系統故障則不重試。

    - **postScriptNoOfRetries**： 設定應該重試 hello 後指令碼，如果沒有任何錯誤，結束之前的 hello 次數。 零表示只嘗試一次，若系統故障則不重試。
    
    - **timeoutInSeconds**： 指定個別 hello 前指令碼和 hello 後指令碼的逾時。

    - **continueBackupOnFailure**： 將此值設定為太**true**如果您想 Azure Backup toofall 後 tooa 檔案系統一致/損毀一致備份前指令碼或後置指令碼會失敗。 將此設定太**false**失敗 hello 備份時 （除了當您有單一磁碟 VM 該便在 2008 年回 toocrash 一致備份，不論此設定為何） 的指令碼失敗。

    - **fsFreezeEnabled**： 指定當您在製作 hello VM 快照 tooensure 檔案系統一致性 Linux fsfreeze 是否應該呼叫。 我們建議您保持此設定設定值太**true**除非您的應用程式具有停用 fsfreeze 的相依性。

6. 現在已設定 hello 指令碼架構。 如果已經設定 hello VM 備份，hello 下一次備份就會叫用 hello 指令碼，並觸發應用程式一致備份。 如果未設定 hello VM 備份，設定使用[備份 Azure 虛擬機器 tooRecovery 服務保存庫。](https://docs.microsoft.com/azure/backup/backup-azure-vms-first-look-arm)

## <a name="troubleshooting"></a>疑難排解

請確定您加入適當的記錄，同時在您撰寫前指令碼和後置指令碼，並檢閱您的指令碼記錄檔 toofix 指令碼中的任何問題。 如果您仍有執行指令碼的問題，請參閱 toohello 下列資料表的詳細資訊。

| 錯誤 | 錯誤訊息 | 建議的動作 |
| ------------------------ | -------------- | ------------------ |
| Pre-ScriptExecutionFailed |hello 前指令碼會傳回錯誤，因此可能不是應用程式一致備份。 | 查看您的指令碼 toofix hello 問題 hello 失敗記錄檔。|  
|   Post-ScriptExecutionFailed |    hello 後指令碼傳回的錯誤，可能會影響應用程式狀態。 |  查看您的指令碼 toofix hello 問題 hello 失敗記錄檔，並檢查 hello 應用程式狀態。 |
| Pre-ScriptNotFound |  hello 前指令碼找不到位置 hello hello 中指定**VMSnapshotScriptPluginConfig.json**組態檔。 | 請確定也前指令碼會出現在 hello hello 設定檔 tooensure 應用程式一致備份中所指定的路徑。|
| Post-ScriptNotFound | hello 後指令碼找不到位置 hello hello 中指定**VMSnapshotScriptPluginConfig.json**組態檔。 | 請確定也後指令碼會出現在 hello hello 設定檔 tooensure 應用程式一致備份中所指定的路徑。|
| IncorrectPluginhostFile | hello **Pluginhost**隨附 hello VmSnapshotLinux 副檔名，檔案已損毀，因此前指令碼和後置指令碼無法執行，而且 hello 備份不會應用程式一致。   | 解除安裝 hello **VmSnapshotLinux**延伸模組和它將會自動重新安裝與 hello 下一個備份 toofix hello 問題。 |
| IncorrectJSONConfigFile | hello **VMSnapshotScriptPluginConfig.json**檔案是不正確，因此前指令碼後置指令碼無法執行，且 hello 備份將不會在應用程式一致。 | 下載從 hello 複製[GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig)和設定一次。 |
| InsufficientPermissionforPre-Script | 執行指令碼，「 根 」 使用者應該在 hello hello 檔案擁有者，而且 hello 檔案包含"700 」 權限 (亦即，僅 「 擁有者 」 應該有 「 讀取 」、 「 寫入 」 和 「 執行 」 權限)。 | 請確定 「 根 」 使用者為 hello hello 指令碼檔案的 「 擁有者 」，而且，只有 「 擁有者 」 有 「 讀取 」、 「 寫入 」 和 「 執行 」 權限。 |
| InsufficientPermissionforPost-Script | 執行指令碼，根使用者應該在 hello hello 檔案擁有者，而且 hello 檔案包含"700 」 權限 (亦即，僅 「 擁有者 」 應該有 「 讀取 」、 「 寫入 」 和 「 執行 」 權限)。 | 請確定 「 根 」 使用者為 hello hello 指令碼檔案的 「 擁有者 」，而且，只有 「 擁有者 」 有 「 讀取 」、 「 寫入 」 和 「 執行 」 權限。 |
| Pre-ScriptTimeout | hello hello 應用程式一致備份前指令碼執行逾時。 | 檢查 hello 指令碼，增加逾時 hello hello **VMSnapshotScriptPluginConfig.json**檔案位於**/etc/hosts azure**。 |
| Post-ScriptTimeout | hello 執行 hello 應用程式一致備份後指令碼逾時。 | 檢查 hello 指令碼，增加逾時 hello hello **VMSnapshotScriptPluginConfig.json**檔案位於**/etc/hosts azure**。 |

## <a name="next-steps"></a>後續步驟
[設定 VM 備份 tooa 復原服務保存庫](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms)
