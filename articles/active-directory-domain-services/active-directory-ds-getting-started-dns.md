---
title: "Azure Active Directory Domain Services：更新 Azure 虛擬網路的 DNS 設定 | Microsoft Docs"
description: "開始使用 Azure Active Directory Domain Services"
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
ms.openlocfilehash: c704ee189072ce8ed196d1ef0a23edd528a10025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a>啟用 Azure Active Directory Domain Services (預覽)

## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a>工作 4：更新 Azure 虛擬網路的 DNS 設定
在先前的組態工作中，您已成功為目錄啟用 Azure Active Directory Domain Services。 下一個工作是確保虛擬網路內的電腦可以連線並取用這些服務。 在本文中，您可以更新虛擬網路的 DNS 伺服器設定，以指向虛擬網路上可以使用 Azure Active Directory Domain Services 的兩個 IP 位址。

若要為已啟用 Azure Active Directory Domain Services 的虛擬網路更新 DNS 伺服器設定，請完成下列步驟︰

1. [概觀] 索引標籤會列出在完整佈建受控網域之後所要執行的一組**必要設定步驟**。 第一個設定步驟是**更新虛擬網路的 DNS 伺服器設定**。

    ![Domain Services - 完全佈建後的 [概觀] 索引標籤](./media/getting-started/domain-services-provisioned-overview.png)

2. 完整佈建您的網域時，此圖格會顯示兩個 IP 位址。 每個 IP 位址都代表受控網域的網域控制站。

3. 若要將第一個 IP 位址複製到剪貼簿，請按一下其旁邊的複製按鈕。 然後按一下 [設定 DNS 伺服器] 按鈕。

4. 將第一個 IP 位址貼上到 [DNS 伺服器] 刀鋒視窗的 [新增 DNS 伺服器] 文字方塊中。 水平捲動至左邊以複製第二個 IP 位址，並將它貼到 [新增 DNS 伺服器] 文字方塊中。

    ![Domain Services - 更新 DNS](./media/getting-started/domain-services-update-dns.png)

5. 當您完成虛擬網路的 DNS 伺服器更新時，按一下 [儲存]。

> [!NOTE]
> 網路中的虛擬機器只會在重新啟動後取得新的 DNS 設定。 如果您希望它們立即取得更新後的 DNS 設定，請透過入口網站、PowerShell 或 CLI 觸發重新啟動。
>
>

## <a name="next-step"></a>後續步驟
[工作 5：啟用 Azure Active Directory Domain Services 的密碼同步處理](active-directory-ds-getting-started-password-sync.md)
