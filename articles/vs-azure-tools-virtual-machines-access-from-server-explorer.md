---
title: "Azure 虛擬機器，從 伺服器總管 aaaAccessing |Microsoft 文件"
description: "取得 tooview 如何建立和管理 Azure 虛擬機器 (Vm) 在 Visual Studio 中的 伺服器總管中的概觀。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: f8326aed105a64ca558f766d712cc68701f82c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>從伺服器總管存取 Azure 虛擬機器
藉由使用 Visual Studio 中的 [伺服器總管]，您可以顯示 Azure 主控的虛擬機器相關資訊。

## <a name="accessing-virtual-machines-in-server-explorer"></a>在 [伺服器總管] 中存取 Azure 虛擬機器
如果您有 Azure 主控的虛擬機器，您可以在 [伺服器總管] 中存取它們。 您必須先登入 tooyour Azure 訂用帳戶 tooview 您的行動服務。 toosign 中，在 伺服器總管中開啟 hello hello Azure 節點的捷徑功能表，然後選擇 **連接 tooMicrosoft Azure**。

### <a name="tooget-information-about-your-virtual-machines"></a>您的虛擬機器的 tooget 資訊
1. 在伺服器總管 中，選擇為虛擬機器，，然後選擇 hello F4 鍵 tooshow 其屬性視窗。
   
    hello 下表顯示哪些屬性可用，但它們是唯讀。 toochange，使用 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。
   
   | 屬性 | 說明 |
   | --- | --- |
   | DNS 名稱 |hello 以 hello hello 虛擬機器網際網路位址的 URL。 |
   | Environment |對於虛擬機器，hello 這個屬性的值一律是生產環境。 |
   | 名稱 |hello hello 虛擬機器名稱。 |
   | 大小 |hello hello 虛擬機器，其會反映 hello 數量的記憶體和磁碟可用空間大小。 如需詳細資訊，請參閱如何：設定虛擬機器大小。 |
   | 狀態 |值包括 [啟動中]、[已啟動]、[停止中]、[已停止] 和 [正在擷取狀態]。 如果出現 正在擷取狀態，hello 目前狀態是未知的。 hello 這個屬性的值不同於用於 hello 的 hello 值[Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。 |
   | SubscriptionID |hello 您的 Azure 帳戶的訂用帳戶 ID。 您可以將這項資訊顯示在 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)檢視 hello 訂用帳戶的內容。 |
2. 選擇 endpoint 節點，然後檢視 hello**屬性**視窗。
3. hello 下表描述 hello 可用屬性的端點，但它們是唯讀狀態。 虛擬機器，tooadd 或編輯的 hello 端點使用 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。 
   
   | 屬性 | 說明 |
   | --- | --- |
   | 名稱 |Hello 端點識別碼。 |
   | 私人連接埠 |網路存取內部 tooyour 應用程式的 hello 連接埠。 |
   | 通訊協定 |使用 hello 這個端點的傳輸層的 hello 通訊協定，TCP 或 UDP。 |
   | 公用連接埠 |hello 用於公用存取 tooyour 應用程式的連接埠。 |

## <a name="next-steps"></a>後續步驟
進一步了解在 Visual Studio 中，使用 Azure 角色 toolearn 看到[透過 Azure 角色使用遠端桌面](vs-azure-tools-remote-desktop-roles.md)。

