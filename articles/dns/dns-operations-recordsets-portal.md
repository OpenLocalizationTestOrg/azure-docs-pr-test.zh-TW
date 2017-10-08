---
title: "aaaManage DNS 記錄集而且要使用 Azure DNS 記錄 |Microsoft 文件"
description: "Azure DNS 提供 hello 功能 toomanage DNS 記錄設定和裝載您的網域時，記錄。"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a>使用 hello Azure 入口網站管理 DNS 記錄和資料錄集

> [!div class="op_single_selector"]
> * [Azure 入口網站](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

本文章將示範如何 toomanage 資料錄集和您所使用的 DNS 區域的記錄 hello Azure 入口網站。

它是重要的 toounderstand hello 差異 DNS 資料錄集和個別的 DNS 記錄。 資料錄集是在區域中有的 hello 相同名稱，且會 hello 相同類型的記錄的集合。 如需詳細資訊，請參閱[建立 DNS 記錄集而且要使用的記錄 hello Azure 入口網站](dns-getstarted-create-recordset-portal.md)。

## <a name="create-a-new-record-set-and-record"></a>建立新的記錄集和記錄

請參閱 toocreate hello Azure 入口網站中設定的記錄[建立 DNS 記錄，使用 hello Azure 入口網站](dns-getstarted-create-recordset-portal.md)。

## <a name="view-a-record-set"></a>檢視記錄集

1. 在 hello Azure 入口網站，移 toohello **DNS 區域**刀鋒視窗。
2. 搜尋 hello 資料錄集，並選取它。 這會開啟 hello 記錄集屬性。

    ![搜尋資料錄集](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a>加入新的記錄 tooa 資料錄集

您可以加總 too20 記錄 tooany 記錄集。 記錄集不能包含兩筆相同的記錄。 可以建立空的資料錄集 （具有零的記錄），但不是會出現在 hello Azure DNS 名稱伺服器。 類型為 CNAME 的記錄集最多只能包含一筆記錄。

1. 在 hello**記錄設定屬性**刀鋒視窗，您的 DNS 區域，按一下 hello 記錄設定您想 tooadd 某筆記錄。

    ![選取記錄集](./media/dns-operations-recordsets-portal/selectset500.png)

2. 指定 hello 記錄填入 hello 欄位中設定屬性。

    ![新增記錄](./media/dns-operations-recordsets-portal/addrecord500.png)

3. 按一下**儲存**在 hello 頂端 hello 刀鋒視窗 toosave 您的設定。 然後關閉 hello 刀鋒視窗。
4. 在 hello 角中，您會看到 hello 記錄會儲存。

    ![儲存記錄集](./media/dns-operations-recordsets-portal/saving150.png)

儲存 hello 記錄之後，hello 上 hello 值**DNS 區域**刀鋒視窗中會反映 hello 新記錄。

## <a name="update-a-record"></a>更新記錄

當您更新現有的記錄組中的記錄時，您可以更新 hello 欄位，取決於 hello 您正在使用的記錄類型。

1. 在 hello**記錄設定屬性**刀鋒視窗中為您的資料錄集，hello 記錄搜尋。
2. 修改 hello 記錄。 當您修改記錄時，您可以變更 hello hello 記錄可用的設定。 在下列範例的 hello，hello **IP 位址**選取欄位，而且 hello IP 位址為正在修改的 hello 程序中。

    ![修改記錄](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. 按一下**儲存**在 hello 頂端 hello 刀鋒視窗 toosave 您的設定。 Hello 右上角，您會看到已保存 hello 記錄的 hello 通知。

    ![已儲存記錄集](./media/dns-operations-recordsets-portal/saved150.png)

Hello 記錄的 hello 值儲存 hello 記錄之後，設定 hello **DNS 區域**刀鋒視窗中會反映 hello 更新記錄。

## <a name="remove-a-record-from-a-record-set"></a>從記錄集移除記錄

您可以使用的記錄組從 hello Azure 入口網站 tooremove 記錄。 請注意，從資料錄集移除 hello 最後一筆記錄並不會刪除 hello 記錄集。

1. 在 hello**記錄設定屬性**刀鋒視窗中為您的資料錄集，hello 記錄搜尋。
2. 按一下您想 tooremove hello 記錄。 然後選取 [移除] 。

    ![移除記錄](./media/dns-operations-recordsets-portal/removerecord500.png)

3. 按一下**儲存**在 hello 頂端 hello 刀鋒視窗 toosave 您的設定。
4. 移除 hello 記錄之後，hello 上 hello hello 記錄的值**DNS 區域**刀鋒視窗中會反映 hello 移除。

## <a name="delete"></a>刪除記錄集

1. 在 hello**記錄設定屬性**刀鋒視窗中為您的資料錄集，按一下**刪除**。

    ![刪除記錄集](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. 訊息會出現，詢問您是否 toodelete hello 記錄集。
3. 請確認您想 toodelete，，然後按一下設定 hello 名稱相符項目 hello 記錄**是**。
4. 在 hello **DNS 區域**刀鋒視窗中，確認 hello 記錄集不再顯示。

## <a name="work-with-ns-and-soa-records"></a>使用 NS 和 SOA 記錄

自動建立之 NS 和 SOA 記錄的管理方式不同於其他記錄類型。

### <a name="modify-soa-records"></a>修改 SOA 記錄

您無法加入或移除 hello 自動建立在 hello 區域的 apex 設定 SOA 記錄中的記錄 (名稱 ="@")。 不過，您可以修改任何 hello （除了 「 主機 」） 的 SOA 記錄中的 hello 參數，而且 hello 記錄設定的 TTL。

### <a name="modify-ns-records-at-hello-zone-apex"></a>修改在 hello 區域的 apex NS 記錄

在 hello 區域的 apex 設定 hello NS 記錄會自動建立與每個 DNS 區域。 它包含 hello hello Azure DNS 名稱伺服器指派的 toohello 區域名稱。

您可以加入其他的名稱伺服器 toothis NS 記錄集，toosupport 共同裝載網域使用一個以上的 DNS 提供者。 您也可以修改 hello TTL 和此記錄集的中繼資料。 不過，您無法移除或修改 hello 預先填入的 Azure DNS 名稱伺服器。

請注意這適用於僅 toohello NS 記錄集在 hello 區域的 apex。 如果沒有限制，您可以修改其他 NS 記錄集在您的區域 （做為使用的 toodelegate 子區域）。

### <a name="delete-soa-or-ns-record-sets"></a>刪除 SOA 或 NS 記錄集

您無法刪除 hello SOA 和 NS 記錄集在 hello 區域的 apex (名稱 ="@")，會自動建立時，建立 hello 區域。 當您刪除 hello 區域時，它們會自動刪除。

## <a name="next-steps"></a>後續步驟

* 如需有關 Azure DNS 的詳細資訊，請參閱 hello [Azure DNS 概觀](dns-overview.md)。
* 如需有關如何自動化 DNS 的詳細資訊，請參閱[建立 DNS 區域和使用資料錄集 hello.NET SDK](dns-sdk.md)。
* 如需反向 DNS 記錄的詳細資訊，請參閱 [Azure 反向 DNS 和支援概觀](dns-reverse-dns-overview.md)。
