---
title: "Azure AD Connect 同步：作業工作和考量 | Microsoft Docs"
description: "本主題描述 Azure AD Connect 同步處理的操作工作以及 tooprepare 來操作此元件。"
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
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="1d5e6-103">Azure AD Connect 同步處理：作業工作和考量</span><span class="sxs-lookup"><span data-stu-id="1d5e6-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="1d5e6-104">本主題的 hello 目標是 Azure AD Connect 同步處理的 toodescribe 操作工作。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-104">hello objective of this topic is toodescribe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="1d5e6-105">預備模式</span><span class="sxs-lookup"><span data-stu-id="1d5e6-105">Staging mode</span></span>
<span data-ttu-id="1d5e6-106">預備模式可以用於許多案例，包括：</span><span class="sxs-lookup"><span data-stu-id="1d5e6-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="1d5e6-107">高可用性。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-107">High availability.</span></span>
* <span data-ttu-id="1d5e6-108">測試和部署新的組態變更。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="1d5e6-109">介紹新的伺服器，並解除委任 hello 舊。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-109">Introduce a new server and decommission hello old.</span></span>

<span data-ttu-id="1d5e6-110">具有預備模式中的伺服器，您可以變更變更 toohello 組態和預覽 hello 進行 hello 伺服器作用中。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-110">With a server in staging mode, you can make changes toohello configuration and preview hello changes before you make hello server active.</span></span> <span data-ttu-id="1d5e6-111">它也可讓您 toorun 完整匯入和完整同步處理 tooverify 到生產環境的所有變更都會先進行這些變更。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-111">It also allows you toorun full import and full synchronization tooverify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="1d5e6-112">在安裝期間，您可以選取在 hello 伺服器 toobe**預備模式**。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-112">During installation, you can select hello server toobe in **staging mode**.</span></span> <span data-ttu-id="1d5e6-113">這個動作可 hello 伺服器作用中匯入和同步處理，但不會執行任何的匯出。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-113">This action makes hello server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="1d5e6-114">預備模式的伺服器不會執行密碼同步處理或密碼回寫，即使您在安裝期間選取這些功能也一樣。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="1d5e6-115">當您停用預備模式時，hello 伺服器就會啟動匯出、 啟用密碼同步處理，並啟用密碼回寫。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-115">When you disable staging mode, hello server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="1d5e6-116">您仍然可以使用 hello 同步處理服務管理員來強制執行匯出。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-116">You can still force an export by using hello synchronization service manager.</span></span>

<span data-ttu-id="1d5e6-117">預備模式中的伺服器會繼續從 Active Directory 和 Azure AD 的 tooreceive 變更。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-117">A server in staging mode continues tooreceive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="1d5e6-118">它永遠高於 hello 責任的另一部伺服器 hello 最新的變更，並可以非常快速採取的複本。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-118">It always has a copy of hello latest changes and can very fast take over hello responsibilities of another server.</span></span> <span data-ttu-id="1d5e6-119">如果您進行組態變更 tooyour 主要伺服器，則責任 toomake hello 中預備模式的相同變更 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-119">If you make configuration changes tooyour primary server, it is your responsibility toomake hello same changes toohello server in staging mode.</span></span>

<span data-ttu-id="1d5e6-120">對於了解的較舊的同步處理技術，預備模式的 hello 十分不同 hello 伺服器有它自己的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-120">For those of you with knowledge of older sync technologies, hello staging mode is different since hello server has its own SQL database.</span></span> <span data-ttu-id="1d5e6-121">此架構可讓 hello 預備模式伺服器 toobe 位於不同的資料中心。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-121">This architecture allows hello staging mode server toobe located in a different datacenter.</span></span>

### <a name="verify-hello-configuration-of-a-server"></a><span data-ttu-id="1d5e6-122">確認組態伺服器 hello</span><span class="sxs-lookup"><span data-stu-id="1d5e6-122">Verify hello configuration of a server</span></span>
<span data-ttu-id="1d5e6-123">tooapply 這種方法，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1d5e6-123">tooapply this method, follow these steps:</span></span>

1. [<span data-ttu-id="1d5e6-124">準備</span><span class="sxs-lookup"><span data-stu-id="1d5e6-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="1d5e6-125">組態</span><span class="sxs-lookup"><span data-stu-id="1d5e6-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="1d5e6-126">匯入和同步處理</span><span class="sxs-lookup"><span data-stu-id="1d5e6-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="1d5e6-127">Verify</span><span class="sxs-lookup"><span data-stu-id="1d5e6-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="1d5e6-128">切換作用中的伺服器</span><span class="sxs-lookup"><span data-stu-id="1d5e6-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="1d5e6-129">準備</span><span class="sxs-lookup"><span data-stu-id="1d5e6-129">Prepare</span></span>
1. <span data-ttu-id="1d5e6-130">安裝 Azure AD Connect，請選取**預備模式**，並取消選取**啟動同步處理**hello hello 安裝精靈 中的最後一頁上。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on hello last page in hello installation wizard.</span></span> <span data-ttu-id="1d5e6-131">此模式可讓您 toorun hello 同步處理引擎以手動方式。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-131">This mode allows you toorun hello sync engine manually.</span></span>
   <span data-ttu-id="1d5e6-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="1d5e6-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="1d5e6-133">符號登出/登入和 hello 從開始功能表中選取**同步處理服務**。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-133">Sign off/sign in and from hello start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="1d5e6-134">組態</span><span class="sxs-lookup"><span data-stu-id="1d5e6-134">Configuration</span></span>
<span data-ttu-id="1d5e6-135">如果您進行了自訂變更 toohello 主要伺服器和想 toocompare hello 組態以 hello 臨時伺服器，然後使用[Azure AD Connect 設定文件產生器](https://github.com/Microsoft/AADConnectConfigDocumenter)。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-135">If you have made custom changes toohello primary server and want toocompare hello configuration with hello staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="1d5e6-136">匯入和同步處理</span><span class="sxs-lookup"><span data-stu-id="1d5e6-136">Import and Synchronize</span></span>
1. <span data-ttu-id="1d5e6-137">選取**連接器**，並選取 hello 與 hello 類型的第一個連接器**Active Directory 網域服務**。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-137">Select **Connectors**, and select hello first Connector with hello type **Active Directory Domain Services**.</span></span> <span data-ttu-id="1d5e6-138">按一下 [執行]，選取 [完整匯入] 和 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="1d5e6-139">對這種類型的所有連接器執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="1d5e6-140">選取 hello 連接器類型**Azure Active Directory (Microsoft)**。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-140">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="1d5e6-141">按一下 [執行]，選取 [完整匯入] 和 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="1d5e6-142">請確定仍然選取連接器 hello 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-142">Make sure hello tab Connectors is still selected.</span></span> <span data-ttu-id="1d5e6-143">針對每一個 [Active Directory Domain Services] 類型的連接器按一下 [執行]、選取 [差異同步處理] 和 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="1d5e6-144">選取 hello 連接器類型**Azure Active Directory (Microsoft)**。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-144">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="1d5e6-145">按一下 [執行]，選取 [差異同步處理] 和 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="1d5e6-146">您必須現在分段的匯出變更 tooAzure AD 和內部部署 AD （如果您使用 Exchange 混合部署）。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-146">You have now staged export changes tooAzure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="1d5e6-147">hello 接下來的步驟可讓您 tooinspect 什麼是關於 toochange 之前您在真正開始 hello 匯出 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-147">hello next steps allow you tooinspect what is about toochange before you actually start hello export toohello directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="1d5e6-148">驗證</span><span class="sxs-lookup"><span data-stu-id="1d5e6-148">Verify</span></span>
1. <span data-ttu-id="1d5e6-149">啟動 cmd 提示字元並移過`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span><span class="sxs-lookup"><span data-stu-id="1d5e6-149">Start a cmd prompt and go too`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="1d5e6-150">執行： `csexport "Name of Connector" %temp%\export.xml /f:x` hello hello 連接器名稱可以在同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` hello name of hello Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="1d5e6-151">其名稱類似的 too"contoso.com – AAD"Azure ad。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-151">It has a name similar too"contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="1d5e6-152">複製 hello PowerShell 指令碼從 hello 區段[CSAnalyzer](#appendix-csanalyzer) tooa 檔名為`csanalyzer.ps1`。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-152">Copy hello PowerShell script from hello section [CSAnalyzer](#appendix-csanalyzer) tooa file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="1d5e6-153">開啟 PowerShell 視窗並瀏覽 toohello 資料夾建立 hello PowerShell 指令碼的位置。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-153">Open a PowerShell window and browse toohello folder where you created hello PowerShell script.</span></span>
5. <span data-ttu-id="1d5e6-154">執行：`.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="1d5e6-155">您現在已有一個可在 Microsoft Excel 中檢查的名為 **processedusers1.csv** 的檔案。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="1d5e6-156">這個檔案中找到所有分段的變更匯出 toobe tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-156">All changes staged toobe exported tooAzure AD are found in this file.</span></span>
7. <span data-ttu-id="1d5e6-157">進行必要的變更 toohello 資料或組態，直到即將匯出的 toobe 的變更預期的 hello 執行這些步驟一次 （匯入和同步處理和驗證）。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-157">Make necessary changes toohello data or configuration and run these steps again (Import and Synchronize and Verify) until hello changes that are about toobe exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="1d5e6-158">切換作用中的伺服器</span><span class="sxs-lookup"><span data-stu-id="1d5e6-158">Switch active server</span></span>
1. <span data-ttu-id="1d5e6-159">Hello 目前作用中伺服器上，讓它不會匯出 tooAzure AD 關閉 hello 伺服器 （DirSync/FIM/Azure AD 同步處理），或在預備模式 (Azure AD Connect) 進行設定。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-159">On hello currently active server, either turn off hello server (DirSync/FIM/Azure AD Sync) so it is not exporting tooAzure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="1d5e6-160">中的 hello 伺服器上執行 hello 安裝精靈**預備模式**和停用**預備模式**。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-160">Run hello installation wizard on hello server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="1d5e6-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="1d5e6-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="1d5e6-162">災害復原</span><span class="sxs-lookup"><span data-stu-id="1d5e6-162">Disaster recovery</span></span>
<span data-ttu-id="1d5e6-163">Hello 實作設計的一部分是針對哪些 toodo tooplan，以防萬一發生嚴重損壞您會遺失 hello 同步伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-163">Part of hello implementation design is tooplan for what toodo in case there is a disaster where you lose hello sync server.</span></span> <span data-ttu-id="1d5e6-164">有不同的模型 toouse 和哪一個 toouse 取決於數個因素，包括：</span><span class="sxs-lookup"><span data-stu-id="1d5e6-164">There are different models toouse and which one toouse depends on several factors including:</span></span>

* <span data-ttu-id="1d5e6-165">什麼是不被可以讓您對於容錯 hello 停機期間的 Azure AD 中變更 tooobjects 嗎？</span><span class="sxs-lookup"><span data-stu-id="1d5e6-165">What is your tolerance for not being able make changes tooobjects in Azure AD during hello downtime?</span></span>
* <span data-ttu-id="1d5e6-166">如果您使用密碼同步處理時，請勿 hello 使用者接受它們在 Azure AD 中有 toouse hello 舊密碼，如果他們變更它在內部部署嗎？</span><span class="sxs-lookup"><span data-stu-id="1d5e6-166">If you use password synchronization, do hello users accept that they have toouse hello old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="1d5e6-167">您是否對即時作業有相依性，例如密碼回寫？</span><span class="sxs-lookup"><span data-stu-id="1d5e6-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="1d5e6-168">根據 hello 答案 toothese 問題和貴組織的原則，其中一個 hello 下列策略可以實作：</span><span class="sxs-lookup"><span data-stu-id="1d5e6-168">Depending on hello answers toothese questions and your organization’s policy, one of hello following strategies can be implemented:</span></span>

* <span data-ttu-id="1d5e6-169">必要時重建。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-169">Rebuild when needed.</span></span>
* <span data-ttu-id="1d5e6-170">具有備用的待命伺服器，稱為「預備模式」 。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="1d5e6-171">使用虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-171">Use virtual machines.</span></span>

<span data-ttu-id="1d5e6-172">如果您不要使用 hello 內建 SQL Express 資料庫，則您也應該檢閱 hello [SQL 高可用性](#sql-high-availability)> 一節。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-172">If you do not use hello built-in SQL Express database, then you should also review hello [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="1d5e6-173">必要時重建</span><span class="sxs-lookup"><span data-stu-id="1d5e6-173">Rebuild when needed</span></span>
<span data-ttu-id="1d5e6-174">可行的策略是在伺服器重建時所需的 tooplan。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-174">A viable strategy is tooplan for a server rebuild when needed.</span></span> <span data-ttu-id="1d5e6-175">通常，安裝 hello 同步處理引擎及執行 hello 初始匯入，而且可以在幾小時的時間內完成同步處理。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-175">Usually, installing hello sync engine and do hello initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="1d5e6-176">如果沒有可用的備用的伺服器，則可能 tootemporarily 使用網域控制站 toohost hello 同步處理引擎。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-176">If there isn’t a spare server available, it is possible tootemporarily use a domain controller toohost hello sync engine.</span></span>

<span data-ttu-id="1d5e6-177">hello 同步作業引擎伺服器不會儲存有關 hello 物件的任何狀態，因此可以重建 hello 資料庫，從 Active Directory 與 Azure AD 中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-177">hello sync engine server does not store any state about hello objects so hello database can be rebuilt from hello data in Active Directory and Azure AD.</span></span> <span data-ttu-id="1d5e6-178">hello **sourceAnchor**屬性是使用的 toojoin hello 物件從內部部署和雲端的 hello。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-178">hello **sourceAnchor** attribute is used toojoin hello objects from on-premises and hello cloud.</span></span> <span data-ttu-id="1d5e6-179">如果您要重建 hello 與現有物件的伺服器內部部署且 hello 雲端，然後 hello 同步處理引擎比對一次上重新安裝這些物件。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-179">If you rebuild hello server with existing objects on-premises and hello cloud, then hello sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="1d5e6-180">hello toodocument，儲存事項 hello 設定的變更 toohello 伺服器，例如篩選和同步處理規則。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-180">hello things you need toodocument and save are hello configuration changes made toohello server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="1d5e6-181">這些自訂設定必須在您開始同步處理之前重新套用。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="1d5e6-182">具有備用的待命伺服器 - 預備模式</span><span class="sxs-lookup"><span data-stu-id="1d5e6-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="1d5e6-183">如果您有更複雜的環境，則建議使用一或多個待命伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="1d5e6-184">在安裝期間，您可以啟用在伺服器 toobe**預備模式**。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-184">During installation, you can enable a server toobe in **staging mode**.</span></span>

<span data-ttu-id="1d5e6-185">如需詳細資訊，請參閱[預備模式](#staging-mode)。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="1d5e6-186">使用虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1d5e6-186">Use virtual machines</span></span>
<span data-ttu-id="1d5e6-187">一般和受支援的方法是在虛擬機器的 toorun hello 同步處理引擎。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-187">A common and supported method is toorun hello sync engine in a virtual machine.</span></span> <span data-ttu-id="1d5e6-188">萬一 hello 主機有問題，與 hello 同步作業引擎伺服器 hello 映像可以是移轉的 tooanother 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-188">In case hello host has an issue, hello image with hello sync engine server can be migrated tooanother server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="1d5e6-189">SQL 高可用性</span><span class="sxs-lookup"><span data-stu-id="1d5e6-189">SQL High Availability</span></span>
<span data-ttu-id="1d5e6-190">如果您不使用 SQL Server Express 隨附於 Azure AD Connect 的 hello，然後 SQL Server 的高可用性也必須考量。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-190">If you are not using hello SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="1d5e6-191">支援的 hello 高可用性解決方案包含 SQL 叢集和 AOA （Alwayson 可用性群組）。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-191">hello high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="1d5e6-192">不支援的解決方案包括鏡像。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="1d5e6-193">已加入支援 SQL AOA tooAzure AD 1.1.524.0 版本中的連接。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-193">Support for SQL AOA was added tooAzure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="1d5e6-194">您必須在安裝 Azure AD Connect 之前啟用 SQL AOA。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="1d5e6-195">在安裝期間，Azure AD Connect 會偵測是否提供 hello SQL 執行個體已啟用 SQL AOA 與否。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-195">During installation, Azure AD Connect detects whether hello SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="1d5e6-196">如果已啟用 SQL AOA，Azure AD Connect 進一步找出 SQL AOA 是否設定的 toouse 同步或非同步複寫。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured toouse synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="1d5e6-197">當設定 hello 可用性群組接聽程式，建議您設定 hello RegisterAllProvidersIP 屬性 too0。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-197">When setting up hello Availability Group Listener, it is recommended that you set hello RegisterAllProvidersIP property too0.</span></span> <span data-ttu-id="1d5e6-198">這是因為 Azure AD Connect 目前使用 SQL Native Client tooconnect tooSQL 和 SQL Native Client 不支援使用 MultiSubNetFailover 屬性 hello。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-198">This is because Azure AD Connect currently uses SQL Native Client tooconnect tooSQL and SQL Native Client does not support hello use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="1d5e6-199">附錄 CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="1d5e6-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="1d5e6-200">請參閱 hello 節[確認](#verify)如何 toouse 此指令碼。</span><span class="sxs-lookup"><span data-stu-id="1d5e6-200">See hello section [verify](#verify) on how toouse this script.</span></span>

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

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
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

    #now that we have hello basics, go get hello details

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

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="1d5e6-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d5e6-201">Next steps</span></span>
<span data-ttu-id="1d5e6-202">**概觀主題**</span><span class="sxs-lookup"><span data-stu-id="1d5e6-202">**Overview topics**</span></span>  

* [<span data-ttu-id="1d5e6-203">Azure AD Connect 同步處理：了解及自訂同步處理</span><span class="sxs-lookup"><span data-stu-id="1d5e6-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="1d5e6-204">整合內部部署身分識別與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d5e6-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
