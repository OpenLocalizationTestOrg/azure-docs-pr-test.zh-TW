---
title: "以無訊息方式安裝 Azure 備份伺服器 v2 | Microsoft Docs"
description: "使用 PowerShell 指令碼來以無訊息方式安裝 Azure 備份伺服器 v2。 這種安裝也稱為自動安裝。"
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
ms.openlocfilehash: 91778a67f9ef523aa87b7918197e0d0ded0f5702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="fc6a5-104">執行 Azure 備份伺服器 v2 的自動安裝</span><span class="sxs-lookup"><span data-stu-id="fc6a5-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="fc6a5-105">了解如何執行 Azure 備份伺服器 v2 的自動安裝。</span><span class="sxs-lookup"><span data-stu-id="fc6a5-105">Learn how to run an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="fc6a5-106">如果您要安裝 Azure 備份伺服器 v1，這些步驟並不適用。</span><span class="sxs-lookup"><span data-stu-id="fc6a5-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="fc6a5-107">安裝備份伺服器 v2</span><span class="sxs-lookup"><span data-stu-id="fc6a5-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="fc6a5-108">在裝載 Azure 備份伺服器 v2 的伺服器上建立文字檔 </span><span class="sxs-lookup"><span data-stu-id="fc6a5-108">On the server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="fc6a5-109">(您可以在記事本或其他文字編輯器中建立檔案)。將檔案儲存為 MABSSetup.ini。</span><span class="sxs-lookup"><span data-stu-id="fc6a5-109">(You can create the file in Notepad or in another text editor.) Save the file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="fc6a5-110">在 MABSSetup.ini 檔案中貼上下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="fc6a5-110">Paste the following code in the MABSSetup.ini file.</span></span> <span data-ttu-id="fc6a5-111">以您的環境值取代括號內的文字 (\< \>)。</span><span class="sxs-lookup"><span data-stu-id="fc6a5-111">Replace the text inside the brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="fc6a5-112">範例如下列文字：</span><span class="sxs-lookup"><span data-stu-id="fc6a5-112">The following text is an example:</span></span>

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

3. <span data-ttu-id="fc6a5-113">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="fc6a5-113">Save the file.</span></span> <span data-ttu-id="fc6a5-114">然後，在安裝伺服器之提升權限的命令提示字元中輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="fc6a5-114">Then, at an elevated command prompt on the installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="fc6a5-115">您可以使用下列旗標來進行安裝：</span><span class="sxs-lookup"><span data-stu-id="fc6a5-115">You can use these flags for the installation:</span></span></br><span data-ttu-id="fc6a5-116">
**/f**：.ini 檔案路徑</span><span class="sxs-lookup"><span data-stu-id="fc6a5-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="fc6a5-117">
**/l**：記錄路徑</span><span class="sxs-lookup"><span data-stu-id="fc6a5-117">
**/l**: Log path</span></span></br><span data-ttu-id="fc6a5-118">
**/i**：安裝路徑</span><span class="sxs-lookup"><span data-stu-id="fc6a5-118">
**/i**: Installation path</span></span></br><span data-ttu-id="fc6a5-119">
**/x**：解除安裝路徑</span><span class="sxs-lookup"><span data-stu-id="fc6a5-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="fc6a5-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc6a5-120">Next steps</span></span>
<span data-ttu-id="fc6a5-121">在安裝備份伺服器之後，請了解如何準備您的伺服器或開始保護工作負載。</span><span class="sxs-lookup"><span data-stu-id="fc6a5-121">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="fc6a5-122">準備備份伺服器工作負載</span><span class="sxs-lookup"><span data-stu-id="fc6a5-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="fc6a5-123">使用備份伺服器來備份 VMware 伺服器</span><span class="sxs-lookup"><span data-stu-id="fc6a5-123">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="fc6a5-124">使用備份伺服器來備份 SQL Server</span><span class="sxs-lookup"><span data-stu-id="fc6a5-124">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="fc6a5-125">在備份伺服器中新增新式備份儲存體</span><span class="sxs-lookup"><span data-stu-id="fc6a5-125">Add Modern Backup Storage to Backup Server</span></span>](backup-mabs-add-storage.md)
