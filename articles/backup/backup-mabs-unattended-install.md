---
title: "安裝 Azure 備份伺服器 v2 aaaSilent |Microsoft 文件"
description: "使用 PowerShell 指令碼 toosilently 安裝 Azure 備份伺服器 v2。 這種安裝也稱為自動安裝。"
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/30/2017
ms.author: markgal;masaran
ms.openlocfilehash: 6b94b4a278bfcd5f8c5c363cb811bd8eec984243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a>執行 Azure 備份伺服器 v2 的自動安裝

深入了解如何 toorun Azure 備份伺服器 v2 的自動安裝。 

如果您要安裝 Azure 備份伺服器 v1，這些步驟並不適用。

## <a name="install-backup-server-v2"></a>安裝備份伺服器 v2

1. 在裝載 Azure 備份伺服器 v2 hello 伺服器上，建立文字檔案。 （您可以建立 hello 檔案以 [記事本] 或其他文字編輯器）。將 hello 檔案儲存為 MABSSetup.ini。 

2. 貼上下列程式碼 hello MABSSetup.ini 檔案中的 hello。 取代 hello 括號內的 hello 文字 (\< \>) 與環境中的值。 下列文字的 hello 是範例：

  ```
  [OPTIONS]
  UserName=administrator
  CompanyName=<Microsoft Corporation>
  SQLMachineName=localhost
  SQLInstanceName=<SQL instance name>
  SQLMachineUserName=administrator
  SQLMachinePassword=<admin password>
  SQLMachineDomainName=<machine domain>
  ReportingMachineName=localhost
  ReportingInstanceName=<reporting instance name>
  SqlAccountPassword=<admin password>
  ReportingMachineUserName=<username>
  ReportingMachinePassword=<reporting admin password>
  ReportingMachineDomainName=<domain>
  VaultCredentialFilePath=<vault credential full path and complete name>
  SecurityPassphrase=<passphrase>
  PassphraseSaveLocation=<passphrase save location>
  UseExistingSQL=<1/0 use or do not use existing SQL>
  ```

3. 儲存 hello 檔案。 然後，在 hello 安裝伺服器上提升權限命令提示字元中輸入下列命令：

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

您可以使用這些旗標 hello 安裝：</br>
**/f**：.ini 檔案路徑</br>
**/l**：記錄路徑</br>
**/i**：安裝路徑</br>
**/x**：解除安裝路徑</br>

## <a name="next-steps"></a>後續步驟
安裝備份伺服器之後，了解如何 tooprepare 您的伺服器，或開始進行保護工作負載。

- [準備備份伺服器工作負載](backup-azure-microsoft-azure-backup.md)
- [使用 VMware 伺服器的備份伺服器 tooback](backup-azure-backup-server-vmware.md)
- [使用 SQL server 備份伺服器 tooback](backup-azure-sql-mabs.md)
- [新增現代化的備份儲存體 tooBackup 伺服器](backup-mabs-add-storage.md)
