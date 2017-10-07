---
title: "分區化 Azure SQL database aaaQuery |Microsoft 文件"
description: "跨分區使用 hello 彈性資料庫用戶端程式庫執行查詢。"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: a4379c15-f213-4026-ab6f-a450ee9d5758
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2016
ms.author: torsteng
ms.openlocfilehash: a1f0763935a6807b74aa9dec477714e8d117417d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="multi-shard-querying"></a>多分區查詢
## <a name="overview"></a>概觀
以 hello[彈性資料庫工具](sql-database-elastic-scale-introduction.md)，您可以建立分區化資料庫解決方案。 **多分區查詢**用於資料收集/報告等工作，這些工作需要跨越數個分區執行查詢。 (這太[資料依存路由](sql-database-elastic-scale-data-dependent-routing.md)，會在單一分區上執行所有工作。) 

1. 取得[ **RangeShardMap** ](https://msdn.microsoft.com/library/azure/dn807318.aspx)或[ **ListShardMap** ](https://msdn.microsoft.com/library/azure/dn807370.aspx)使用 hello [ **TryGetRangeShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx)，hello [ **TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx)，或使用 hello [ **GetShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx)方法。 請參閱[**建構 ShardMapManager**](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) 和[**取得 RangeShardMap 或 ListShardMap**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap)。
2. 建立 **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)** 物件。
3. 建立 **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**。 
4. 設定 hello  **[CommandText 屬性](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)** tooa T-SQL 命令。
5. Hello 命令執行所呼叫的 hello  **[ExecuteReader 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**。
6. 檢視使用 hello hello 結果 **[MultiShardDataReader 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**。 

## <a name="example"></a>範例
hello 下列程式碼說明 hello 的使用方式的查詢時使用的多個分區指定**ShardMap**名為*myShardMap*。 

    using (MultiShardConnection conn = new MultiShardConnection( 
                                        myShardMap.GetShards(), 
                                        myShardConnectionString) 
          ) 
    { 
    using (MultiShardCommand cmd = conn.CreateCommand())
           { 
            cmd.CommandText = "SELECT c1, c2, c3 FROM ShardedTable"; 
            cmd.CommandType = CommandType.Text; 
            cmd.ExecutionOptions = MultiShardExecutionOptions.IncludeShardNameColumn; 
            cmd.ExecutionPolicy = MultiShardExecutionPolicy.PartialResults; 

            using (MultiShardDataReader sdr = cmd.ExecuteReader()) 
                { 
                    while (sdr.Read())
                        { 
                            var c1Field = sdr.GetString(0); 
                            var c2Field = sdr.GetFieldValue<int>(1); 
                            var c3Field = sdr.GetFieldValue<Int64>(2);
                        } 
                 } 
           } 
    } 


主要的差別是 hello 建構的多個分區的連線。 其中**SqlConnection**對單一資料庫，hello **MultiShardConnection**採用***的分區集合***做為輸入。 填入 hello 的分區，分區對應的集合。 然後使用分區的 hello 集合上執行 hello 查詢**UNION ALL**語意 tooassemble 單一的整體結果。 （選擇性） hello 名稱 hello 資料列會來自 hello 分區可以加入輸出使用 hello toohello **ExecutionOptions**命令上的屬性。 

請注意 hello 呼叫太**myShardMap.GetShards()**。 這個方法會從 hello 分區對應會擷取所有分區，提供簡單的方式 toorun 所有相關資料庫之間的查詢。 hello 的分區集合的多個分區查詢可以重新調整進一步執行 LINQ 查詢 hello 太 hello 呼叫傳回的集合上**myShardMap.GetShards()**。 在與 hello 部分結果原則的組合，hello 中多個分區查詢目前的功能已經過設計適合數以萬計的分區 toohundreds 向上 toowork。

Hello 缺乏驗證分區與 shardlet 是查詢的目前多分區查詢的限制。 雖然資料依存路由確認給定的分區是查詢的 hello 次 hello 分區對應的一部分時，多個分區查詢就不會執行這項檢查。 這可能會導致 toomulti 分區查詢已從 hello 分區對應中移除的資料庫上執行。

## <a name="multi-shard-queries-and-split-merge-operations"></a>多分區查詢與分割合併作業
多個分區的查詢不會確認 hello 查詢的資料庫上的 shardlet 是否參與進行中的分割合併作業。 (請參閱[調整使用 hello 彈性資料庫分割合併工具](sql-database-elastic-scale-overview-split-and-merge.md)。)這可能會導致 tooinconsistencies 其中的資料列 hello hello 中的多個資料庫的相同 shardlet 顯示相同的多個分區查詢。 注意這些限制，並考慮在執行多個分區的查詢時清空持續分割合併作業和變更 toohello 分區對應。

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

## <a name="see-also"></a>另請參閱
**[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)** 類別和方法。

管理使用 hello 分區[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)。 包含命名空間稱為[Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx)提供 hello 能力 tooquery 使用單一查詢和結果的多個分區。 它提供一組分區的查詢抽象方法。 它也會提供替代的執行原則，特別是部分結果、 toodeal 但失敗查詢透過許多分區時。  

