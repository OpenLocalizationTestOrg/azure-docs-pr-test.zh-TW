---
title: "Azure AD Connect 同步：作業工作和考量 | Microsoft Docs"
description: "本主題描述 Azure AD Connect 同步處理的作業工作以及如何準備操作此元件。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: b7583a1556bb1113f349a78890768451e39c6878
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="aa703-103">Azure AD Connect 同步處理：作業工作和考量</span><span class="sxs-lookup"><span data-stu-id="aa703-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="aa703-104">本主題的目標在於描述 Azure AD Connect 同步處理的操作工作。</span><span class="sxs-lookup"><span data-stu-id="aa703-104">The objective of this topic is to describe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="aa703-105">預備模式</span><span class="sxs-lookup"><span data-stu-id="aa703-105">Staging mode</span></span>
<span data-ttu-id="aa703-106">預備模式可以用於許多案例，包括：</span><span class="sxs-lookup"><span data-stu-id="aa703-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="aa703-107">高可用性。</span><span class="sxs-lookup"><span data-stu-id="aa703-107">High availability.</span></span>
* <span data-ttu-id="aa703-108">測試和部署新的組態變更。</span><span class="sxs-lookup"><span data-stu-id="aa703-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="aa703-109">引進新的伺服器並解除委任舊伺服器。</span><span class="sxs-lookup"><span data-stu-id="aa703-109">Introduce a new server and decommission the old.</span></span>

<span data-ttu-id="aa703-110">利用預備模式中的伺服器，您可以在啟用伺服器之前變更組態並預覽變更。</span><span class="sxs-lookup"><span data-stu-id="aa703-110">With a server in staging mode, you can make changes to the configuration and preview the changes before you make the server active.</span></span> <span data-ttu-id="aa703-111">它也可以讓您執行完整的匯入和完整的同步處理，以在生產環境中進行這些變更之前，確認所有變更皆如預期。</span><span class="sxs-lookup"><span data-stu-id="aa703-111">It also allows you to run full import and full synchronization to verify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="aa703-112">您可以在安裝期間選取狀態為 **預備模式**的伺服器。</span><span class="sxs-lookup"><span data-stu-id="aa703-112">During installation, you can select the server to be in **staging mode**.</span></span> <span data-ttu-id="aa703-113">此動作會讓伺服器進行匯入和同步處理，但它不會執行任何匯出。</span><span class="sxs-lookup"><span data-stu-id="aa703-113">This action makes the server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="aa703-114">預備模式的伺服器不會執行密碼同步處理或密碼回寫，即使您在安裝期間選取這些功能也一樣。</span><span class="sxs-lookup"><span data-stu-id="aa703-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="aa703-115">當您停用預備模式時，伺服器會開始匯出、啟用密碼同步處理及啟用密碼回寫。</span><span class="sxs-lookup"><span data-stu-id="aa703-115">When you disable staging mode, the server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="aa703-116">您仍然可以使用 Synchronization Service Manager 來強制執行匯出。</span><span class="sxs-lookup"><span data-stu-id="aa703-116">You can still force an export by using the synchronization service manager.</span></span>

<span data-ttu-id="aa703-117">預備模式的伺服器會繼續收到來自 Active Directory 和 Azure AD 的變更。</span><span class="sxs-lookup"><span data-stu-id="aa703-117">A server in staging mode continues to receive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="aa703-118">這樣永遠都有最新的變更複本，並且可以非常快速地接管另一部伺服器的責任。</span><span class="sxs-lookup"><span data-stu-id="aa703-118">It always has a copy of the latest changes and can very fast take over the responsibilities of another server.</span></span> <span data-ttu-id="aa703-119">如果您對您的主要伺服器進行組態變更，則您有責任對預備模式的伺服器進行相同的變更。</span><span class="sxs-lookup"><span data-stu-id="aa703-119">If you make configuration changes to your primary server, it is your responsibility to make the same changes to the server in staging mode.</span></span>

<span data-ttu-id="aa703-120">對於具備較舊同步處理技術知識的人員，預備模式是不同的，因為伺服器有它自己的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="aa703-120">For those of you with knowledge of older sync technologies, the staging mode is different since the server has its own SQL database.</span></span> <span data-ttu-id="aa703-121">此架構可讓預備模式伺服器位於不同的資料中心。</span><span class="sxs-lookup"><span data-stu-id="aa703-121">This architecture allows the staging mode server to be located in a different datacenter.</span></span>

### <a name="verify-the-configuration-of-a-server"></a><span data-ttu-id="aa703-122">驗證伺服器的組態</span><span class="sxs-lookup"><span data-stu-id="aa703-122">Verify the configuration of a server</span></span>
<span data-ttu-id="aa703-123">若要套用此方法，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="aa703-123">To apply this method, follow these steps:</span></span>

1. [<span data-ttu-id="aa703-124">準備</span><span class="sxs-lookup"><span data-stu-id="aa703-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="aa703-125">組態</span><span class="sxs-lookup"><span data-stu-id="aa703-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="aa703-126">匯入和同步處理</span><span class="sxs-lookup"><span data-stu-id="aa703-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="aa703-127">Verify</span><span class="sxs-lookup"><span data-stu-id="aa703-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="aa703-128">切換作用中的伺服器</span><span class="sxs-lookup"><span data-stu-id="aa703-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="aa703-129">準備</span><span class="sxs-lookup"><span data-stu-id="aa703-129">Prepare</span></span>
1. <span data-ttu-id="aa703-130">安裝 Azure AD Connect、選取**預備模式**，然後取消選取安裝精靈中最後一個頁面上的 [啟動同步處理]。</span><span class="sxs-lookup"><span data-stu-id="aa703-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on the last page in the installation wizard.</span></span> <span data-ttu-id="aa703-131">此模式可讓您手動執行同步處理引擎。</span><span class="sxs-lookup"><span data-stu-id="aa703-131">This mode allows you to run the sync engine manually.</span></span>
   <span data-ttu-id="aa703-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="aa703-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="aa703-133">登出/登入，並從 [開始] 功能表中選取 [同步處理服務] 。</span><span class="sxs-lookup"><span data-stu-id="aa703-133">Sign off/sign in and from the start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="aa703-134">組態</span><span class="sxs-lookup"><span data-stu-id="aa703-134">Configuration</span></span>
<span data-ttu-id="aa703-135">如果您已對主要伺服器進行變更，並想要將組態與預備伺服器進行比較，則請使用 [Azure AD Connect 組態文件產生器](https://github.com/Microsoft/AADConnectConfigDocumenter)。</span><span class="sxs-lookup"><span data-stu-id="aa703-135">If you have made custom changes to the primary server and want to compare the configuration with the staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="aa703-136">匯入和同步處理</span><span class="sxs-lookup"><span data-stu-id="aa703-136">Import and Synchronize</span></span>
1. <span data-ttu-id="aa703-137">選取 [連接器]，並選取第一個類型為 [Active Directory Domain Services] 的連接器。</span><span class="sxs-lookup"><span data-stu-id="aa703-137">Select **Connectors**, and select the first Connector with the type **Active Directory Domain Services**.</span></span> <span data-ttu-id="aa703-138">按一下 [執行]，選取 [完整匯入] 和 [確定]。</span><span class="sxs-lookup"><span data-stu-id="aa703-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="aa703-139">對這種類型的所有連接器執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="aa703-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="aa703-140">選取 [Azure Active Directory (Microsoft)] 類型的連接器。</span><span class="sxs-lookup"><span data-stu-id="aa703-140">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="aa703-141">按一下 [執行]，選取 [完整匯入] 和 [確定]。</span><span class="sxs-lookup"><span data-stu-id="aa703-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="aa703-142">確定仍然選取 [連接器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="aa703-142">Make sure the tab Connectors is still selected.</span></span> <span data-ttu-id="aa703-143">針對每一個 [Active Directory Domain Services] 類型的連接器按一下 [執行]、選取 [差異同步處理] 和 [確定]。</span><span class="sxs-lookup"><span data-stu-id="aa703-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="aa703-144">選取 [Azure Active Directory (Microsoft)] 類型的連接器。</span><span class="sxs-lookup"><span data-stu-id="aa703-144">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="aa703-145">按一下 [執行]，選取 [差異同步處理] 和 [確定]。</span><span class="sxs-lookup"><span data-stu-id="aa703-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="aa703-146">您現在已預備匯出變更至 Azure AD 和內部部署 AD (如果您正在使用 Exchange 混合部署)。</span><span class="sxs-lookup"><span data-stu-id="aa703-146">You have now staged export changes to Azure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="aa703-147">接下來的步驟可讓您在實際開始匯出至目錄之前，檢查將要變更的項目。</span><span class="sxs-lookup"><span data-stu-id="aa703-147">The next steps allow you to inspect what is about to change before you actually start the export to the directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="aa703-148">Verify</span><span class="sxs-lookup"><span data-stu-id="aa703-148">Verify</span></span>
1. <span data-ttu-id="aa703-149">啟動 CMD 命令提示字元並移至 `%ProgramFiles%\Microsoft Azure AD Sync\bin`</span><span class="sxs-lookup"><span data-stu-id="aa703-149">Start a cmd prompt and go to `%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="aa703-150">執行：`csexport "Name of Connector" %temp%\export.xml /f:x` 連接器名稱可以在同步處理服務中找到。</span><span class="sxs-lookup"><span data-stu-id="aa703-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` The name of the Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="aa703-151">它的名稱類似 Azure AD 的 "contoso.com – AAD"。</span><span class="sxs-lookup"><span data-stu-id="aa703-151">It has a name similar to "contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="aa703-152">從 [CSAnalyzer](#appendix-csanalyzer) 區段將 PowerShell 指令碼複製到名為 `csanalyzer.ps1` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="aa703-152">Copy the PowerShell script from the section [CSAnalyzer](#appendix-csanalyzer) to a file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="aa703-153">開啟 PowerShell 視窗，然後瀏覽至您建立 PowerShell 指令碼的資料夾。</span><span class="sxs-lookup"><span data-stu-id="aa703-153">Open a PowerShell window and browse to the folder where you created the PowerShell script.</span></span>
5. <span data-ttu-id="aa703-154">執行：`.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`。</span><span class="sxs-lookup"><span data-stu-id="aa703-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="aa703-155">您現在已有一個可在 Microsoft Excel 中檢查的名為 **processedusers1.csv** 的檔案。</span><span class="sxs-lookup"><span data-stu-id="aa703-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="aa703-156">您可以在此檔案中找到所有已暫存而要匯出到 Azure AD 的變更。</span><span class="sxs-lookup"><span data-stu-id="aa703-156">All changes staged to be exported to Azure AD are found in this file.</span></span>
7. <span data-ttu-id="aa703-157">對資料或組態進行必要的變更並再次執行這些步驟 (匯入和同步處理和驗證)，直到要匯出的變更皆如預期進行。</span><span class="sxs-lookup"><span data-stu-id="aa703-157">Make necessary changes to the data or configuration and run these steps again (Import and Synchronize and Verify) until the changes that are about to be exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="aa703-158">切換作用中的伺服器</span><span class="sxs-lookup"><span data-stu-id="aa703-158">Switch active server</span></span>
1. <span data-ttu-id="aa703-159">在目前作用中的伺服器上，關閉伺服器 (DirSync/FIM/Azure AD Sync) 讓它不會匯出至 Azure AD 或將它設為預備模式 (Azure AD Connect)。</span><span class="sxs-lookup"><span data-stu-id="aa703-159">On the currently active server, either turn off the server (DirSync/FIM/Azure AD Sync) so it is not exporting to Azure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="aa703-160">在**預備模式**的伺服器上執行安裝精靈並停用**預備模式**。</span><span class="sxs-lookup"><span data-stu-id="aa703-160">Run the installation wizard on the server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="aa703-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="aa703-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="aa703-162">災害復原</span><span class="sxs-lookup"><span data-stu-id="aa703-162">Disaster recovery</span></span>
<span data-ttu-id="aa703-163">實作設計的一部分是規劃您在失去同步處理伺服器的災害中應如何應對。</span><span class="sxs-lookup"><span data-stu-id="aa703-163">Part of the implementation design is to plan for what to do in case there is a disaster where you lose the sync server.</span></span> <span data-ttu-id="aa703-164">有不同的模型可供使用，要使用哪一個模組取決於許多因素，包括：</span><span class="sxs-lookup"><span data-stu-id="aa703-164">There are different models to use and which one to use depends on several factors including:</span></span>

* <span data-ttu-id="aa703-165">您在 Azure AD 的停機期間無法變更物件的容錯能力如何？</span><span class="sxs-lookup"><span data-stu-id="aa703-165">What is your tolerance for not being able make changes to objects in Azure AD during the downtime?</span></span>
* <span data-ttu-id="aa703-166">如果您使用密碼同步化，使用者是否接受他們在內部部署變更時必須在 Azure AD 中使用舊密碼？</span><span class="sxs-lookup"><span data-stu-id="aa703-166">If you use password synchronization, do the users accept that they have to use the old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="aa703-167">您是否對即時作業有相依性，例如密碼回寫？</span><span class="sxs-lookup"><span data-stu-id="aa703-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="aa703-168">根據這些問題的解答和組織的原則，可實作下列其中一個策略：</span><span class="sxs-lookup"><span data-stu-id="aa703-168">Depending on the answers to these questions and your organization’s policy, one of the following strategies can be implemented:</span></span>

* <span data-ttu-id="aa703-169">必要時重建。</span><span class="sxs-lookup"><span data-stu-id="aa703-169">Rebuild when needed.</span></span>
* <span data-ttu-id="aa703-170">具有備用的待命伺服器，稱為「預備模式」 。</span><span class="sxs-lookup"><span data-stu-id="aa703-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="aa703-171">使用虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="aa703-171">Use virtual machines.</span></span>

<span data-ttu-id="aa703-172">如果您未使用內建的 SQL Express 資料庫，您也應該檢閱 [SQL 高可用性](#sql-high-availability) 一節。</span><span class="sxs-lookup"><span data-stu-id="aa703-172">If you do not use the built-in SQL Express database, then you should also review the [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="aa703-173">必要時重建</span><span class="sxs-lookup"><span data-stu-id="aa703-173">Rebuild when needed</span></span>
<span data-ttu-id="aa703-174">必要時規劃伺服器重建為可行的策略。</span><span class="sxs-lookup"><span data-stu-id="aa703-174">A viable strategy is to plan for a server rebuild when needed.</span></span> <span data-ttu-id="aa703-175">安裝同步處理引擎並執行初始匯入和同步處理，通常可以在幾個小時內完成。</span><span class="sxs-lookup"><span data-stu-id="aa703-175">Usually, installing the sync engine and do the initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="aa703-176">如果沒有可用的備用伺服器，則可以暫時使用網域控制站裝載同步處理引擎。</span><span class="sxs-lookup"><span data-stu-id="aa703-176">If there isn’t a spare server available, it is possible to temporarily use a domain controller to host the sync engine.</span></span>

<span data-ttu-id="aa703-177">同步處理引擎伺服器不會儲存有關物件的任何狀態，因此可以從 Active Directory 與 Azure AD 中的資料重建資料庫。</span><span class="sxs-lookup"><span data-stu-id="aa703-177">The sync engine server does not store any state about the objects so the database can be rebuilt from the data in Active Directory and Azure AD.</span></span> <span data-ttu-id="aa703-178">**sourceAnchor** 屬性可用來聯結來自內部部署和雲端的物件。</span><span class="sxs-lookup"><span data-stu-id="aa703-178">The **sourceAnchor** attribute is used to join the objects from on-premises and the cloud.</span></span> <span data-ttu-id="aa703-179">如果您使用現有的內部部署與雲端物件重建伺服器，則同步處理引擎會在重新安裝時一起比對這些物件。</span><span class="sxs-lookup"><span data-stu-id="aa703-179">If you rebuild the server with existing objects on-premises and the cloud, then the sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="aa703-180">您需要記錄和儲存的項目是對伺服器進行的組態變更，例如篩選和同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="aa703-180">The things you need to document and save are the configuration changes made to the server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="aa703-181">這些自訂設定必須在您開始同步處理之前重新套用。</span><span class="sxs-lookup"><span data-stu-id="aa703-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="aa703-182">具有備用的待命伺服器 - 預備模式</span><span class="sxs-lookup"><span data-stu-id="aa703-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="aa703-183">如果您有更複雜的環境，則建議使用一或多個待命伺服器。</span><span class="sxs-lookup"><span data-stu-id="aa703-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="aa703-184">您可以在安裝期間啟用狀態為「預備模式」 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="aa703-184">During installation, you can enable a server to be in **staging mode**.</span></span>

<span data-ttu-id="aa703-185">如需詳細資訊，請參閱[預備模式](#staging-mode)。</span><span class="sxs-lookup"><span data-stu-id="aa703-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="aa703-186">使用虛擬機器</span><span class="sxs-lookup"><span data-stu-id="aa703-186">Use virtual machines</span></span>
<span data-ttu-id="aa703-187">一般和受支援的方法是在虛擬機器中執行同步處理引擎。</span><span class="sxs-lookup"><span data-stu-id="aa703-187">A common and supported method is to run the sync engine in a virtual machine.</span></span> <span data-ttu-id="aa703-188">如果主機有問題，可將內含同步處理引擎伺服器的映像移轉到另一部伺服器。</span><span class="sxs-lookup"><span data-stu-id="aa703-188">In case the host has an issue, the image with the sync engine server can be migrated to another server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="aa703-189">SQL 高可用性</span><span class="sxs-lookup"><span data-stu-id="aa703-189">SQL High Availability</span></span>
<span data-ttu-id="aa703-190">如果您未使用 Azure AD Connect 隨附的 SQL Server Express，也應該考慮 SQL Server 的高可用性。</span><span class="sxs-lookup"><span data-stu-id="aa703-190">If you are not using the SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="aa703-191">支援的高可用性解決方案包含 SQL 叢集和 AOA (「永遠開啟」可用性群組）。</span><span class="sxs-lookup"><span data-stu-id="aa703-191">The high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="aa703-192">不支援的解決方案包括鏡像。</span><span class="sxs-lookup"><span data-stu-id="aa703-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="aa703-193">Azure AD Connect 1.1.524.0 版中已新增 SQL AOA 支援。</span><span class="sxs-lookup"><span data-stu-id="aa703-193">Support for SQL AOA was added to Azure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="aa703-194">您必須在安裝 Azure AD Connect 之前啟用 SQL AOA。</span><span class="sxs-lookup"><span data-stu-id="aa703-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="aa703-195">在安裝期間，Azure AD Connect 會偵測所提供的 SQL 執行個體是否已啟用 SQL AOA。</span><span class="sxs-lookup"><span data-stu-id="aa703-195">During installation, Azure AD Connect detects whether the SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="aa703-196">如果已啟用 SQL AOA，Azure AD Connect 會進一步指出 SQL AOA 已設定為使用同步複寫或非同步複寫。</span><span class="sxs-lookup"><span data-stu-id="aa703-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured to use synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="aa703-197">設定可用性群組接聽程式時，建議將 RegisterAllProvidersIP 屬性設定為 0。</span><span class="sxs-lookup"><span data-stu-id="aa703-197">When setting up the Availability Group Listener, it is recommended that you set the RegisterAllProvidersIP property to 0.</span></span> <span data-ttu-id="aa703-198">這是因為 Azure AD Connect 目前使用 SQL Native Client 來連線至 SQL，且 SQL Native Client 不支援使用 MultiSubNetFailover 屬性。</span><span class="sxs-lookup"><span data-stu-id="aa703-198">This is because Azure AD Connect currently uses SQL Native Client to connect to SQL and SQL Native Client does not support the use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="aa703-199">附錄 CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="aa703-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="aa703-200">請參閱[驗證](#verify)一節，以了解如何使用此指令碼。</span><span class="sxs-lookup"><span data-stu-id="aa703-200">See the section [verify](#verify) on how to use this script.</span></span>

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve the file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader to deal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create the object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have the basics, go get the details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump the processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit the maximum users processed without completion... -ForegroundColor Yellow

        #export the collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment the output file counter
        $outputfilecount+=1

        #reset the collection and the user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need to bail out of the loop if no more users to process
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need to write out any users that didn't get picked up in a batch of 1000
#export the collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="aa703-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa703-201">Next steps</span></span>
<span data-ttu-id="aa703-202">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="aa703-202">**Overview topics**</span></span>  

* [<span data-ttu-id="aa703-203">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="aa703-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="aa703-204">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa703-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
