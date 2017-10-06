---
title: "在 OMS 中目標 aaaSolution |Microsoft 文件"
description: "方案的目標是在 Operations Management Suite (OMS)，可讓您 toolimit 管理解決方案 tooa 組特定的代理程式的功能。  本文說明如何 toocreate 領域設定並將它套用 tooa 方案。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 6f8c8109e0d9e282e18724bf8b673b10de8e498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-solution-targeting-in-operations-management-suite-oms-tooscope-management-solutions-toospecific-agents-preview"></a>使用解決方案目標 Operations Management Suite (OMS) tooscope 管理解決方案 toospecific 代理程式 （預覽）
當您加入方案 tooOMS 時，它會自動部署預設 tooall Windows 和 Linux 代理程式連接的 tooyour 記錄分析工作區。  您可能想的 toomanage 您的成本和限制 hello 量的資料收集的解決方案，藉由限制它 tooa 特定的一組代理程式。  本文說明如何 toouse**方案目標**這是一項 OMS 功能，可讓您 tooapply 範圍 tooyour 解決方案。

## <a name="how-tootarget-a-solution"></a>如何 tootarget 方案
有三個步驟 tootargeting 方案 hello 下列各節中所述。  請注意，您將需要 hello OMS 入口網站和 hello Azure 入口網站不同的步驟。


### <a name="1-create-a-computer-group"></a>1.建立電腦群組
指定您想 tooinclude 範圍中的，藉由建立 hello 電腦[電腦群組](../log-analytics/log-analytics-computer-groups.md)記錄分析中。  hello 電腦群組可以根據 記錄搜尋，或從其他來源，例如 Active Directory 或 WSUS 群組匯入。 做為[下述](#solutions-and-agents-that-cant-be-targeted)，只有電腦直接連線的 tooLog 分析將會包含在 hello 範圍。

一旦建立工作區中的 hello 電腦群組，然後您將會包含在可以套用的 tooone 或其他解決方案領域設定。
 
 
 ### <a name="2-create-a-scope-configuration"></a>2.建立範圍設定
 A**領域設定**包含一或多個電腦群組，而且可以是套用的 tooone 或其他解決方案。 
 
 建立使用下列程序的 hello 的範圍設定。  

 1. 在 hello Azure 入口網站中瀏覽過**記錄分析**並選取您的工作區。
 2. 在 hello 工作區下的 hello 屬性**工作區中的資料來源**選取**範圍組態**。
 3. 按一下**新增**toocreate 新的領域設定。
 4. 輸入**名稱**hello 範圍設定。
 5. 按一下 [選取電腦群組]。
 6. 選取您所建立的 hello 電腦群組和 （選擇性） 任何其他群組 tooadd toohello 組態。  按一下 [選取] 。  
 6. 按一下**確定**toocreate hello 領域設定。 


 ### <a name="3-apply-hello-scope-configuration-tooa-solution"></a>3.適用於 hello 範圍組態 tooa 方案。
一旦領域設定，然後您可以將它套用 tooone 或其他解決方案。  請注意，雖然單一範圍設定可以搭配多個解決方案使用，但每個解決方案僅可以使用一個範圍設定。

適用於使用下列程序的 hello 領域設定。  

 1. 在 hello Azure 入口網站中瀏覽過**記錄分析**並選取您的工作區。
 2. 在 [hello] 工作區的 hello 內容選取**解決方案**。
 3. 按一下您想 tooscope hello 方案。
 4. Hello 下 hello 方案內容中**工作區中的資料來源**選取**方案目標**。  如果不使用 hello 選項然後[無法針對此解決方案](#solutions-and-agents-that-cant-be-targeted)。
 5. 按一下 [新增範圍設定]。  如果您已經擁有組態套用 toothis 解決方案此選項將無法使用。  您必須移除 hello 現有組態，然後再加入另一個。
 6. 按一下您所建立的 hello 領域設定。
 7. 監看式 hello**狀態**的它會顯示 hello 組態 tooensure **Succeeded**。  如果 hello 狀態表示錯誤，然後按一下 hello 橢圓形 toohello 右邊的 hello 設定，並選取**編輯領域設定**toomake 變更。

## <a name="solutions-and-agents-that-cant-be-targeted"></a>無法設定目標的解決方案和代理程式
以下是代理程式和解決方案，不能與目標方案的 hello 準則。

- 方案為目標時，只適用於部署 tooagents toosolutions。
- 目標方案僅適用於由 Microsoft 提供的 toosolutions。  它不會套用 toosolutions[自己或其他協力廠商所建立](operations-management-suite-solutions-creating.md)。
- 您可以只會篩選掉 tooLog 分析直接連接的代理程式。  解決方案會自動將部署 tooany 代理程式已連線的 Operations Manager 管理群組，它們包含在範圍組態的一部分。

### <a name="exceptions"></a>例外狀況
方案的目標不能與 hello 下列方案，即使它們符合 hello 所述的準則。

- 代理程式健康狀態評估

## <a name="next-steps"></a>後續步驟
- 深入了解管理方案包括 hello 方案會在您環境中的可用 tooinstall[新增 Azure Log Analytics management 解決方案 tooyour 工作區](../log-analytics/log-analytics-add-solutions.md)。
- 在 [Log Analytics 記錄檔搜尋中的電腦群組](../log-analytics/log-analytics-computer-groups.md)中深入了解建立電腦群組。