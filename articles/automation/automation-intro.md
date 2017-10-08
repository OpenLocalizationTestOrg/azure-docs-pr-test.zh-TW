---
title: "aaaWhat 是 Azure 自動化 |Microsoft 文件"
description: "了解 Azure 自動化提供了什麼價值，並取得答案 toocommon 問題，讓您可以開始建立時，使用 runbook 和 Azure 自動化 DSC。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "何謂自動化, azure 自動化, azure 自動化範例"
ms.assetid: 0cf1f3e8-dd30-4f33-b52a-e148e97802a9
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/10/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 1e5a90e272d6b2beb7b5007e2fea2c110dbd79b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-overview"></a>Azure 自動化概觀
Microsoft Azure 自動化提供方式為使用者 tooautomate hello 手動、 長時間執行、 易發生錯誤及經常重複工作通常會在雲端和企業環境中執行。 它可以節省時間和可以提升可靠性 hello 的日常管理工作和即使排程這些 toobe 自動定期執行。 您可以使用 Runbook 自動執行程序，或使用「期望狀態設定」自動進行組態管理。 本文提供 Azure 自動化的簡短概觀，並回答一些常見問題。 您可以參考 tooother 發行項，此文件庫中的 hello 不同主題的詳細資訊。

## <a name="automating-processes-with-runbooks"></a>使用 Runbook 自動執行程序
Runbook 是可在 Azure 自動化中執行一些自動程序的一組工作。 它可能是簡單的程序，例如正在啟動虛擬機器，以及建立記錄項目，或您可能會有複雜的 runbook，跨多個資源或更多個雲端和內部部署環境結合其他較小的 runbook tooperform 複雜的程序。  

例如，您可能有現有的手動程序的截斷如果它已接近最大大小，其中包含多個步驟，例如連線 toohello 伺服器，連接 toohello 資料庫的 SQL 資料庫、 取得 hello 目前的資料庫大小、 檢查是否閾值已超過然後截斷，並通知使用者。 不需手動執行每個步驟，您可以建立會以單一程序的形式執行這所有工作的 Runbook。 您會啟動 hello runbook、 提供 hello 所需的資訊，例如 hello SQL server 名稱、 資料庫名稱和收件者電子郵件，然後坐 hello 程序完成時。 

## <a name="what-can-runbooks-automate"></a>Runbook 可以自動化什麼？
Azure 自動化中的 Runbook 是以 Windows PowerShell 或 Windows PowerShell 工作流程為基礎，因此它們會執行 PowerShell 能做的一切功能。 如果應用程式或服務具有 API，則 Runbook 處理它。 如果您擁有 hello 應用程式的 PowerShell 模組，然後載入該模組至 Azure 自動化和 runbook 中包含這些指令程式。 Azure 自動化 runbook 執行 hello Azure 雲端，並可存取任何雲端外部資源，或是可以從 hello 雲端存取。 使用[Hybrid Runbook Worker](automation-hybrid-runbook-worker.md)，runbook 可以在中執行您的本機資料中心 toomanage 本機資源。 

## <a name="getting-runbooks-from-hello-community"></a>取得來自 hello 社群的 runbook
hello [Runbook 庫](automation-runbook-gallery.md#runbooks-in-runbook-gallery)包含 Microsoft 和 hello 社群，您可以變更使用您的環境中的 runbook，或自訂它們自己的目的。 它們也是很有用的 tooas 參考 toolearn 如何 toocreate 您自己的 runbook。 您甚至可以參與您認為其他使用者可能有幫助您自己的 runbook toohello 組件庫。 

## <a name="creating-runbooks-with-azure-automation"></a>利用 Azure 自動化建立 Runbook
您可以[建立您自己的 runbook](automation-creating-importing-runbook.md)從臨時或修改 runbook 從 hello [Runbook 庫](http://msdn.microsoft.com/library/azure/dn781422.aspx)為您自己的需求。 有四個不同的 [Runbook 類型](automation-runbook-types.md)，您可以依據需求和 PowerShell 經驗自行選擇。 如果您偏好 toowork 直接與 hello PowerShell 程式碼，則您可以使用[PowerShell runbook](automation-runbook-types.md#powershell-runbooks)或[PowerShell 工作流程 runbook](automation-runbook-types.md#powershell-workflow-runbooks)您編輯離線或 hello[文字編輯器](http://msdn.microsoft.com/library/azure/dn879137.aspx) hello Azure 入口網站中。 如果您偏好 tooedit runbook 不需要是公開 toohello 基礎程式碼中，那麼您可以建立[圖形化 runbook](automation-runbook-types.md#graphical-runbooks)使用 hello[圖形化編輯器](automation-graphical-authoring-intro.md)hello Azure 入口網站中。 

偏好觀看 tooreading 嗎？ 看看 hello 下方從 Microsoft Ignite 2015 年中的工作階段的視訊。 注意： 雖然 hello 概念和這段影片中所述的功能正確，因為這段影片錄製許多進入 Azure 自動化，它現在有更廣泛的 UI 中 hello Azure 入口網站和其他支援的功能。

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3451/player]
> 
> 

## <a name="automating-configuration-management-with-desired-state-configuration"></a>使用「預期狀態設定」自動進行組態管理
[PowerShell DSC](https://technet.microsoft.com/library/dn249912.aspx)是管理平台，可讓您 toomanage，部署和強制執行的實體主機和虛擬機器使用宣告式 PowerShell 語法的設定。 您可以在中央 DSC 提取伺服器上定義組態，該伺服器是以可自動擷取和套用的電腦為目標。 DSC 提供一組 PowerShell 指令程式，您可以使用 toomanage 設定和資源。  

[Azure Automation DSC](automation-dsc-overview.md) 是針對 PowerShell DSC 的雲端架構解決方案，可提供企業環境所需的服務。  您可以管理在 Azure 自動化 DSC 資源，並套用組態 toovirtual 或擷取 DSC 提取伺服器 hello Azure 雲端中的實體機器。  它也提供報告服務，以通知您重要的事件，例如當節點偏離其指派的組態時以及已套用新的組態時。 

## <a name="creating-your-own-dsc-configurations-with-azure-automation"></a>使用 Azure 自動化建立自己的 DSC 組態
[DSC 設定](automation-dsc-overview.md)指定節點的 hello 預期狀態。  多個節點可以套用 hello 相同組態 tooassure 它們都會維持相同的狀態。  您可以在本機電腦上使用任何文字編輯器來建立組態，然後將它匯入至 Azure 自動化加以編譯並套用至節點。

## <a name="getting-modules-and-configurations"></a>取得模組和組態
您可以取得[PowerShell 模組](automation-runbook-gallery.md#modules-in-powershell-gallery)包含您可以使用您的 runbook 和從 hello DSC 組態中的 cmdlet [PowerShell 資源庫](http://www.powershellgallery.com/)。 您可以啟動這個組件庫，從 hello Azure 入口網站，並直接在 Azure 自動化中，匯入模組，或您可以下載並手動匯入。 您無法直接從 hello Azure 入口網站安裝 hello 模組，但您也可以將其下載安裝它們，如同任何其他模組。 

## <a name="example-practical-applications-of-azure-automation"></a>Azure 自動化的實際應用範例
以下是幾個範例的什麼是 Azure 自動化的自動化案例的 hello 類型。 

* 在不同的 Azure 訂用帳戶中建立和複製虛擬機器。 
* 排程會從本機電腦 tooan Azure Blob 儲存體容器的檔案複製。 
* 在偵測到阻斷服務攻擊時自動執行安全性功能，例如來自用戶端的拒絕要求。 
* 確定機器持續依循設定的安全性原則。
* 跨雲端和內部部署基礎結構來管理應用程式程式碼的連續部署。 
* 在 Azure 中針對您的實驗室環境建置 Active Directory 樹系。 
* 如果資料庫已接近大小上限，請截斷 SQL Database 中的資料表。 
* 遠端更新 Azure 網站的環境設定。 

## <a name="how-does-azure-automation-relate-tooother-automation-tools"></a>Azure 自動化如何與 tooother 自動化工具？
[服務管理自動化 (SMA)](http://technet.microsoft.com/library/dn469260.aspx)是預定的 tooautomate hello 私人雲端中的管理工作。 它會安裝在您的本機資料中心，做為 [Microsoft Azure 套件](https://www.microsoft.com/en-us/server-cloud/)的元件。 SMA 和 Azure 自動化會使用 hello 相同 runbook 格式是根據 Windows PowerShell 和 Windows PowerShell 工作流程，但不是支援 SMA[圖形化 runbook](automation-graphical-authoring-intro.md)。  

[System Center 2012 Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) 旨在自動化內部部署資源。 它使用不同的 runbook 格式比 Azure 自動化和服務管理自動化，並具有圖形化介面 toocreate runbook 而不需要編寫任何指令碼。 其 Runbook 是由來自專門為 Orchestrator 編寫的整合套件的活動組成。 

## <a name="where-can-i-get-more-information"></a>我可以在哪裡取得詳細資訊？
許多資源可供更多關於 Azure 自動化，並建立您自己的 runbook 的您 toolearn。 

* **Azure 自動化程式庫** 是您目前的所在位置。 此文件庫中的 hello 文件會提供完整的文件上 hello 設定和管理 Azure 自動化並撰寫您自己的 runbook。 
* [Azure PowerShell Cmdlet](http://msdn.microsoft.com/library/jj156055.aspx) 提供使用 Windows PowerShell 自動執行 Azure 作業的資訊。 Runbook 會使用這些 cmdlet toowork Azure 資源。 
* [管理部落格](https://azure.microsoft.com/blog/tag/azure-automation/)microsoft 提供 hello 最新資訊 Azure 自動化，以及其他管理技術。 您應該 hello Azure 自動化小組的最新訂閱 toothis 部落格 toostay 向上 toodate 以 hello。 
* [自動化論壇](http://go.microsoft.com/fwlink/p/?LinkId=390561)可讓您 toopost Microsoft hello 自動化社群所定址的 Azure 自動化 toobe 疑問。 
* [Azure 自動化 Cmdlet](https://msdn.microsoft.com/library/mt244122.aspx) 提供自動執行管理工作的資訊。 它包含 cmdlet toomanage 自動化帳戶、 資產、 DSC 的 runbook。

## <a name="can-i-provide-feedback"></a>可以提供意見嗎？
**請不吝提供意見！** 如果您要尋找 Azure 自動化 Runbook 解決方案或整合模組，請在指令碼中心提出指令碼要求。 如果您有關於 Azure 自動化的任何意見或功能要求，請張貼在 [User Voice](http://feedback.windowsazure.com/forums/34192--general-feedback)上。 感謝您！ 

