---
title: "在 Azure 中的 aaaUse Windows 用戶端映像 |Microsoft 文件"
description: "如何 toouse Visual Studio 訂閱優點 toodeploy Windows 7、 Windows 8 或 Windows 10 在 Azure 中開發/測試案例"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 91c3880a-cede-44f1-ae25-f8f9f5b6eaa4
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 4ac7c3d9872673030f4ea0f0ab38625dd9d9c1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-client-in-azure-for-devtest-scenarios"></a>在 Azure 中使用 Windows 用戶端進行開發/測試案例
假設您有適當的 Visual Studio (先前稱為 MSDN) 訂用帳戶，您可以在 Azure 中使用 Windows 7、Windows 8 或 Windows 10 進行開發/測試案例。 本文將概述在 Azure 中並使用 hello 的 Azure 資源庫映像執行 Windows 用戶端 hello 資格需求。

## <a name="subscription-eligibility"></a>訂用帳戶資格
有效的 Visual Studio 訂閱者 (已取得 Visual Studio 訂用帳戶授權的人) 可以使用 Windows 用戶端進行開發和測試。 Windows 用戶端可以用在您自己的硬體及以任何類型的 Azure 訂用帳戶執行的 Azure 虛擬機器。 Windows 用戶端可能不是已部署的 tooor Azure 用於一般實際執行環境，或使用不是有效的 Visual Studio 訂閱者的人員。

為了方便起見，我們進行了特定的 Windows 10 映像可從 hello Azure 組件庫內[適合開發/測試提供](#eligible-offers)。 提供項目的任何型別中的 visual Studio 訂閱者也可以[可以充分地準備及建立](prepare-for-upload-vhd-image.md)64 位元 Windows 7、 Windows 8 或 Windows 10 映像，然後[上載 tooAzure](upload-generalized-managed.md)。 hello 使用仍有限的 toodev/測試的方法是使用 Visual Studio 的 「 訂閱者 」。

## <a name="eligible-offers"></a>符合資格者的優惠
下列資料表詳細資料 hello hello 供應項目會透過 hello Azure 組件庫的合格 toodeploy Windows 10 的識別碼。 hello Windows 10 映像只會顯示 toohello 遵循優惠。 Visual Studio 訂閱者需要 toorun 其他優惠類型中的 Windows 用戶端需要太[可以充分地準備及建立](prepare-for-upload-vhd-image.md)64 位元 Windows 7、 Windows 8 或 Windows 10 映像和[然後上傳 tooAzure](upload-generalized-managed.md).

| 優惠名稱 | 優惠號碼 | 可用的用戶端映像 |
|:--- |:---:|:---:|
| [隨用隨付開發/測試](https://azure.microsoft.com/offers/ms-azr-0023p/) |0023P |Windows 10 |
| [Visual Studio Enterprise (MPN) 訂閱者](https://azure.microsoft.com/offers/ms-azr-0029p/) |0029P |Windows 10 |
| [Visual Studio Professional 訂閱者](https://azure.microsoft.com/offers/ms-azr-0059p/) |0059P |Windows 10 |
| [Visual Studio Test Professional 訂閱者](https://azure.microsoft.com/offers/ms-azr-0060p/) |0060P |Windows 10 |
| [Visual Studio Premium 含 MSDN (權益)](https://azure.microsoft.com/offers/ms-azr-0061p/) |0061P |Windows 10 |
| [Visual Studio Enterprise 訂閱者](https://azure.microsoft.com/offers/ms-azr-0063p/) |0063P |Windows 10 |
| [Visual Studio Enterprise (BizSpark) 訂閱者](https://azure.microsoft.com/offers/ms-azr-0064p/) |0064P |Windows 10 |
| [Enterprise 開發/測試](https://azure.microsoft.com/ofers/ms-azr-0148p/) |0148P |Windows 10 |

## <a name="check-your-azure-subscription"></a>檢查您的 Azure 訂用帳戶
如果您不知道您的優惠識別碼，您可以取得它透過 hello Azure 入口網站，這兩種方式之一：  

- Hello 'Subscriptions' 刀鋒視窗中：

  ![從 hello Azure 入口網站的優惠識別碼詳細資料](./media/client-images/offer-id-azure-portal.png) 

- 或者，按一下 [計費]，然後按一下訂用帳戶識別碼。 hello 供應項目識別碼會出現在 hello 帳單 刀鋒視窗。

您也可以檢視從 hello hello 供應項目識別碼['Subscriptions' 索引標籤](http://account.windowsazure.com/Subscriptions)hello Azure 帳戶入口網站的：

![從 hello Azure 帳戶入口網站中提供識別碼詳細資料](./media/client-images/offer-id-azure-account-portal.png) 

## <a name="next-steps"></a>後續步驟
您現在可以使用 [PowerShell](quick-create-powershell.md)、[Resource Manager templates](ps-template.md) 或 [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) 來部署您的 VM。

