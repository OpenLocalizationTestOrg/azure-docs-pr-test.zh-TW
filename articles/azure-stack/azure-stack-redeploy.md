---
title: "aaaRedeploy Azure 堆疊 |Microsoft 文件"
description: "重新部署 Azure Stack。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 795af5ea-892d-40b1-a080-42e4472e4bba
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: erikje
ms.openlocfilehash: ec26745bcb54edd7c26960eec55d41504aff1911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-azure-stack"></a>重新部署 Azure Stack
tooredeploy Azure 堆疊，您必須透過從頭開始，如下所述。

## <a name="steps-tooredeploy-azure-stack"></a>步驟 tooredeploy Azure 堆疊
1. Hello 開發套件在主機上，開啟提升權限的 PowerShell 主控台 > 瀏覽 toohello asdk installer.ps1 指令碼 > 執行此程式碼 > 按一下**重新開機**。
2. 選取 hello 基礎作業系統 (不**Azure 堆疊**) 按一下**下一步**。
3. Hello 開發套件主機重新開機之後，刪除 hello CloudBuilder.vhdx 檔案已用來作為 hello 先前部署的一部分。
4. [部署 hello 開發套件](azure-stack-run-powershell-script.md)。

## <a name="next-steps"></a>後續步驟
[連接 tooAzure 堆疊](azure-stack-connect-azure-stack.md)

