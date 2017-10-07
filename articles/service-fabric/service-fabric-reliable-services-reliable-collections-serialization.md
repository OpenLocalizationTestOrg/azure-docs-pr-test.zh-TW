---
title: "Azure Service Fabric 中的集合物件序列化 aaaReliable |Microsoft 文件"
description: "Azure Service Fabric Reliable Collections 物件序列化"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 9d35374c-2d75-4856-b776-e59284641956
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/8/2017
ms.author: mcoskun
ms.openlocfilehash: 248defbe0ae6f65b4ac5dc7c74e80d8f1152ce94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a>Azure Service Fabric 中的 Reliable Collection 物件序列化
可靠集合複寫，並將保存其項目 toomake 確認他們的電腦故障和電力中斷等跨持久。
Tooreplicate 和 toopersist 項目、 可靠集合需要 tooserialize 它們。

可靠的集合取得可靠狀態管理員從指定的型別 hello 適當的序列化程式。
Reliable 狀態管理員包含內建的序列化程式，以及可讓自訂序列化程式 toobe 註冊指定的型別。

## <a name="built-in-serializers"></a>內建的序列化程式

Reliable State Manager 包含一些常見類型的內建序列化程式，以便透過預設方式有效率地將這些類型序列化。 對於其他類型，可靠的狀態管理員就會回到 toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx)。
內建的序列化程式會更有效率，因為他們知道無法變更其類型，而且它們不需要 tooinclude hello 型別，其型別名稱類似的資訊。

Reliable State Manager 具有下列類型的內建序列化程式： 
- Guid
- 布林
- byte
- sbyte
- byte[]
- char
- 字串
- decimal
- double
- float
- int
- uint
- long
- ulong
- short
- ushort

## <a name="custom-serialization"></a>自訂序列化

自訂序列化程式是常用的 tooincrease 效能或 tooencrypt hello 資料上 hello 傳輸，而在磁碟上。 其中一個原因，自訂序列化程式是比一般的序列化程式通常更有效率，因為它們不需要 tooserialize hello 類型的資訊。 

[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) hello 類型 t 的自訂序列化程式是使用的 tooregister此註冊應該在 hello StatefulServiceBase tooensure hello 建構復原啟動之前，所有可靠集合都具有存取 toohello 相關的序列化程式 tooread 保存的資料。

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed tooset OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> 自訂序列化程式的優先順序高於內建的序列化程式。 例如，int 的自訂序列化程式註冊時，它是使用的 tooserialize 整數而不是 int 的 hello 在內建序列化程式

### <a name="how-tooimplement-a-custom-serializer"></a>如何 tooimplement 自訂序列化程式

自訂序列化程式需要 tooimplement hello [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1)介面。

> [!NOTE]
> IStateSerializer<T> 包含會接受額外 T (稱為基底值) 的 Write 和 Read 多載。 此 API 適用於差異序列化。 目前並未公開差異序列化功能。 因此，將等到公開並啟用差異序列化之後，才會呼叫這兩個多載。

以下是一個名為 OrderKey 且包含四個屬性的範例自訂類型

```C#
public class OrderKey : IComparable<OrderKey>, IEquatable<OrderKey>
{
    public byte Warehouse { get; set; }

    public short District { get; set; }

    public int Customer { get; set; }

    public long Order { get; set; }

    #region Object Overrides for GetHashCode, CompareTo and Equals
    #endregion
}
```

以下是 IStateSerializer<OrderKey> 的範例實作。
請注意，接受 baseValue 的 Read 和 Write 多載會呼叫其個別的多載以滿足向後相容性。

```C#
public class OrderKeySerializer : IStateSerializer<OrderKey>
{
  OrderKey IStateSerializer<OrderKey>.Read(BinaryReader reader)
  {
      var value = new OrderKey();
      value.Warehouse = reader.ReadByte();
      value.District = reader.ReadInt16();
      value.Customer = reader.ReadInt32();
      value.Order = reader.ReadInt64();

      return value;
  }

  void IStateSerializer<OrderKey>.Write(OrderKey value, BinaryWriter writer)
  {
      writer.Write(value.Warehouse);
      writer.Write(value.District);
      writer.Write(value.Customer);
      writer.Write(value.Order);
  }
  
  // Read overload for differential de-serialization
  OrderKey IStateSerializer<OrderKey>.Read(OrderKey baseValue, BinaryReader reader)
  {
      return ((IStateSerializer<OrderKey>)this).Read(reader);
  }

  // Write overload for differential serialization
  void IStateSerializer<OrderKey>.Write(OrderKey baseValue, OrderKey newValue, BinaryWriter writer)
  {
      ((IStateSerializer<OrderKey>)this).Write(newValue, writer);
  }
}
```

## <a name="upgradability"></a>可升級性
在[復原應用程式升級](service-fabric-application-upgrade.md)，hello 升級已套用的 tooa 節點的子集，一次一個升級網域。 在此過程中，某些升級網域會 hello 較新版本的應用程式，而且某些升級網域會在 hello 較舊版本的應用程式。 Hello 首展期間 hello 新版本的應用程式必須是能夠 tooread hello 舊版本的資料，而且 hello 舊版本的應用程式必須能夠 tooread hello 新版本的資料。 如果 hello 資料格式不是向前和向後相容，hello 升級可能會失敗，或更糟的是，資料可能遺失或損毀。

如果您使用的在內建序列化程式，表示您沒有 tooworry 有關相容性。
不過，如果您使用自訂序列化程式或 hello DataContractSerializer，hello 資料有 toobe 無限回溯，往後相容性。
換句話說，每個版本的序列化程式需要 toobe 無法 tooserialize 和還原序列化 hello 類型的任何版本。

資料合約使用者應遵循新增、 移除和變更欄位的 hello 妥善定義的版本控制規則。 資料合約也有支援處理具有未知的欄位、 攔截到 hello 序列化和還原序列化程序，和處理的類別繼承。 如需詳細資訊，請參閱 [使用資料合約](https://msdn.microsoft.com/library/ms733127.aspx)。

自訂序列化程式的使用者均應遵守 toohello hello 他們使用 toomake 確定回溯，而且往後相容性的序列化程式的指導方針。
支援所有版本的常見方式在 hello 開頭，並只加入選擇性的屬性加入大小資訊。
這種方式可以讀取每個版本最多可以並跳過 hello hello 資料流的其餘部分。

## <a name="next-steps"></a>後續步驟
  * [序列化與升級](service-fabric-application-upgrade-data-serialization.md)
  * [可靠的集合的開發人員參考資料](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * [使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md) 將引導您完成使用 Visual Studio 進行應用程式升級的步驟。
  * [使用 PowerShell 升級您的應用程式](service-fabric-application-upgrade-tutorial-powershell.md) 將引導您完成使用 PowerShell 進行應用程式升級的步驟。
  * 使用 [升級參數](service-fabric-application-upgrade-parameters.md)來控制您應用程式的升級方式。
  * 了解 toouse 把太升級您的應用程式時所進階的功能[進階主題](service-fabric-application-upgrade-advanced.md)。
  * 藉由參考 toohello 步驟中的修正應用程式升級的一般問題[疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)。
