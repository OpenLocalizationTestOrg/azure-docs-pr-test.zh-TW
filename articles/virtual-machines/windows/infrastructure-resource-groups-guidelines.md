---
title: "適用於 Windows Vm 在 Azure 中的 aaaResource 群組 |Microsoft 文件"
description: "深入了解 hello 金鑰設計和實作指導方針在 Azure 基礎結構服務中部署資源群組。"
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0fbcabcd-e96d-4d71-a526-431984887451
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56b5670ec98bf3e80b7a622d5d760a57a7d20809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-group-guidelines-for-windows-vms"></a>適用於 Windows VM 的 Azure 資源群組指導方針

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

本文著重在了解如何 toologically 建置您的環境和所有資源群組中的 hello 元件都群組。

## <a name="implementation-guidelines-for-resource-groups"></a>資源群組的實作指導方針
决策：

* 要何種 toobuild 出資源群組由 hello 核心基礎結構元件，或完整的應用程式部署嗎？
* 您需要 toorestrict 存取 tooResource 群組使用角色型存取控制？

工作：

* 定義核心基礎結構元件，以及您所需的專屬資源群組。
* 檢閱如何將資源管理員範本 tooimplement 一致、 可重現的部署。
* 如需可控制哪些使用者存取角色存取 tooResource 群組的定義。
* 建立資源群組使用您的命名慣例 hello 組。 您可以使用 Azure PowerShell 或 hello 入口網站。

## <a name="resource-groups"></a>資源群組
在 Azure 中，您以邏輯方式群組相關的資源，例如儲存體帳戶、 虛擬網路以及虛擬機器 (Vm) toodeploy、 管理和維護它們當做單一實體。 這個方法可讓它更容易 toodeploy 應用程式時保留所有 hello 相關聯的資源一起從管理的觀點來看或 toogrant 其他人存取 toothat 群組的資源。 資源群組名稱長度最多可以有 90 個字元。 資源群組更全面的瞭解，請參閱 hello [Azure 資源管理員概觀](../../azure-resource-manager/resource-group-overview.md)。

一項重要功能 tooResource 群組是您的環境使用範本的能力 toobuild。 範本是只在 JSON 檔案宣告 hello 儲存體、 網路功能，並計算資源。 您也可以定義任何相關的自訂指令碼或組態 tooapply。 透過使用這些範本，您可以為應用程式建立一致且可重現的部署。 此方法使其成為輕鬆 toobuild 出環境中開發，，然後使用該相同的範本 toocreate 生產部署，反之亦然。 進一步了解使用範本，讀取[hello 範本逐步解說](../../azure-resource-manager/resource-manager-template-walkthrough.md)，引導您完成 hello 範本建立的每個步驟。

您在使用資源群組設計環境時，有兩種不同的執行方式：

* 資源群組結合了 hello 儲存體帳戶、 虛擬網路和子網路的 Vm，每個應用程式部署的負載平衡器等。
* 集中式資源群組，其中包含您的核心虛擬網路和子網路或儲存體帳戶。 接著，您的應用程式會位於它們自己的資源群組中，其中只會包含 VM、負載平衡器、網路介面等項目。

當您向外延展，建立您的虛擬網路的集中式的資源群組和子網路可讓您更輕鬆 toobuild 跨單位網路連線的混合式連線選項。 hello 替代方法是針對每個應用程式 toohave 自己需要設定和維護的虛擬網路。  [角色型存取控制](../../active-directory/role-based-access-control-what-is.md)提供細微的方式 toocontrol 存取 tooResource 群組。 對於生產應用程式，您可以控制 hello 使用者可以存取這些資源，或 hello 核心基礎結構資源，您可以限制只有基礎結構工程師 toowork 它們。 您的應用程式擁有者只能有其資源群組和不 hello 核心 Azure 基礎結構，您的環境中存取 toohello 應用程式元件。 當您設計您的環境，請考慮 hello 使用者需要存取 toohello 資源，並據此設計您的資源群組。 

## <a name="next-steps"></a>後續步驟
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

