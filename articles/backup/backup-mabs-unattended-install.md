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
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="a02d4-104">執行 Azure 備份伺服器 v2 的自動安裝</span><span class="sxs-lookup"><span data-stu-id="a02d4-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="a02d4-105">深入了解如何 toorun Azure 備份伺服器 v2 的自動安裝。</span><span class="sxs-lookup"><span data-stu-id="a02d4-105">Learn how toorun an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="a02d4-106">如果您要安裝 Azure 備份伺服器 v1，這些步驟並不適用。</span><span class="sxs-lookup"><span data-stu-id="a02d4-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="a02d4-107">安裝備份伺服器 v2</span><span class="sxs-lookup"><span data-stu-id="a02d4-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="a02d4-108">在裝載 Azure 備份伺服器 v2 hello 伺服器上，建立文字檔案。</span><span class="sxs-lookup"><span data-stu-id="a02d4-108">On hello server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="a02d4-109">（您可以建立 hello 檔案以 [記事本] 或其他文字編輯器）。將 hello 檔案儲存為 MABSSetup.ini。</span><span class="sxs-lookup"><span data-stu-id="a02d4-109">(You can create hello file in Notepad or in another text editor.) Save hello file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="a02d4-110">貼上下列程式碼 hello MABSSetup.ini 檔案中的 hello。</span><span class="sxs-lookup"><span data-stu-id="a02d4-110">Paste hello following code in hello MABSSetup.ini file.</span></span> <span data-ttu-id="a02d4-111">取代 hello 括號內的 hello 文字 (\< \>) 與環境中的值。</span><span class="sxs-lookup"><span data-stu-id="a02d4-111">Replace hello text inside hello brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="a02d4-112">下列文字的 hello 是範例：</span><span class="sxs-lookup"><span data-stu-id="a02d4-112">hello following text is an example:</span></span>

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

3. <span data-ttu-id="a02d4-113">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="a02d4-113">Save hello file.</span></span> <span data-ttu-id="a02d4-114">然後，在 hello 安裝伺服器上提升權限命令提示字元中輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="a02d4-114">Then, at an elevated command prompt on hello installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="a02d4-115">您可以使用這些旗標 hello 安裝：</span><span class="sxs-lookup"><span data-stu-id="a02d4-115">You can use these flags for hello installation:</span></span></br><span data-ttu-id="a02d4-116">
**/f**：.ini 檔案路徑</span><span class="sxs-lookup"><span data-stu-id="a02d4-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="a02d4-117">
**/l**：記錄路徑</span><span class="sxs-lookup"><span data-stu-id="a02d4-117">
**/l**: Log path</span></span></br><span data-ttu-id="a02d4-118">
**/i**：安裝路徑</span><span class="sxs-lookup"><span data-stu-id="a02d4-118">
**/i**: Installation path</span></span></br><span data-ttu-id="a02d4-119">
**/x**：解除安裝路徑</span><span class="sxs-lookup"><span data-stu-id="a02d4-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="a02d4-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a02d4-120">Next steps</span></span>
<span data-ttu-id="a02d4-121">安裝備份伺服器之後，了解如何 tooprepare 您的伺服器，或開始進行保護工作負載。</span><span class="sxs-lookup"><span data-stu-id="a02d4-121">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="a02d4-122">準備備份伺服器工作負載</span><span class="sxs-lookup"><span data-stu-id="a02d4-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="a02d4-123">使用 VMware 伺服器的備份伺服器 tooback</span><span class="sxs-lookup"><span data-stu-id="a02d4-123">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="a02d4-124">使用 SQL server 備份伺服器 tooback</span><span class="sxs-lookup"><span data-stu-id="a02d4-124">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="a02d4-125">新增現代化的備份儲存體 tooBackup 伺服器</span><span class="sxs-lookup"><span data-stu-id="a02d4-125">Add Modern Backup Storage tooBackup Server</span></span>](backup-mabs-add-storage.md)
