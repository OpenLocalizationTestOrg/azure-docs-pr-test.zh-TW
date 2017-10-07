---
title: "Azure Active Directory 網域服務： 更新 hello Azure 虛擬網路的 DNS 設定 |Microsoft 文件"
description: "開始使用 Azure Active Directory 網域服務"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a>啟用 Azure Active Directory Domain Services (預覽)

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>工作 4： 更新 hello Azure 虛擬網路的 DNS 設定
在 hello 之前設定工作，您已成功啟用 Azure Active Directory 網域服務目錄。 hello 下一個工作是 tooensure hello 虛擬網路內的電腦可以連線，並使用這些服務。 在本文中，您可以更新 hello DNS 伺服器設定您虛擬網路 toopoint toohello 兩個 IP 位址的 Azure Active Directory 網域服務位於 hello 虛擬網路。

tooupdate hello DNS 伺服器設定為已啟用 Azure Active Directory 網域服務，完成下列步驟的 hello hello 虛擬網路的：

1. hello**概觀**索引標籤會列出一組**所需的設定步驟**toobe 執行之後完整佈建受管理的網域。 hello 第一個組態步驟是**更新 DNS 伺服器設定為您的虛擬網路**。

    ![Domain Services - 完全佈建後的 [概觀] 索引標籤](./media/getting-started/domain-services-provisioned-overview.png)

2. 完整佈建您的網域時，此圖格會顯示兩個 IP 位址。 每個 IP 位址都代表受控網域的網域控制站。

3. toocopy hello 第一個 IP 位址 tooclipboard，請按一下 hello 複製 按鈕的下一個 tooit。 然後按一下 [hello**設定 DNS 伺服器**] 按鈕。

4. 第一個 IP 位址 hello 貼入 hello**新增 DNS 伺服器**hello 中的文字方塊中**DNS 伺服器**刀鋒視窗。 水平捲動 toohello 剩餘 toocopy hello 第二個 IP 位址，並將它貼到 hello**新增 DNS 伺服器**文字方塊。

    ![Domain Services - 更新 DNS](./media/getting-started/domain-services-update-dns.png)

5. 按一下**儲存**當您完成 tooupdate hello hello 虛擬網路的 DNS 伺服器。

> [!NOTE]
> Hello 網路中的虛擬機器重新啟動之後，只能取得 hello 新的 DNS 設定。 如果您需要它們 tooget hello 更新 DNS 設定以立即開始，會觸發重新啟動依 hello 入口網站、 PowerShell 或 hello CLI。
>
>

## <a name="next-step"></a>後續步驟
[工作 5： 啟用密碼同步處理 tooAzure Active Directory 網域服務](active-directory-ds-getting-started-password-sync.md)
