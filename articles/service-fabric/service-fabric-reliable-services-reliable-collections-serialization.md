---
title: "Azure Service Fabric 中的 Reliable Collection 物件序列化 | Microsoft Docs"
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
ms.openlocfilehash: c14794b71ce7340d9e90a56d781c712e247ded06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="ccf1a-103">Azure Service Fabric 中的 Reliable Collection 物件序列化</span><span class="sxs-lookup"><span data-stu-id="ccf1a-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="ccf1a-104">Reliable Collections 會複寫並保存其項目，以確保在電腦發生失敗和電力中斷時能持續保留這些項目。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-104">Reliable Collections' replicate and persist their items to make sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="ccf1a-105">不論是要複寫還是保存項目，Reliable Collections 都必須將它們序列化。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-105">Both to replicate and to persist items, Reliable Collections' need to serialize them.</span></span>

<span data-ttu-id="ccf1a-106">Reliable Collections 會從 Reliable State Manager 為指定的類型取得適當的序列化程式。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-106">Reliable Collections' get the appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="ccf1a-107">Reliable State Manager 包含內建的序列化程式，並允許為指定的類型註冊自訂序列化程式。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-107">Reliable State Manager contains built-in serializers and allows custom serializers to be registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="ccf1a-108">內建的序列化程式</span><span class="sxs-lookup"><span data-stu-id="ccf1a-108">Built-in Serializers</span></span>

<span data-ttu-id="ccf1a-109">Reliable State Manager 包含一些常見類型的內建序列化程式，以便透過預設方式有效率地將這些類型序列化。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="ccf1a-110">針對其他類型，Reliable State Manager 會回復為使用 [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-110">For other types, Reliable State Manager falls back to use the [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="ccf1a-111">內建的序列化程式較有效率，因為它們知道它們的類型無法變更，所以不需要包含類型的相關資訊 (例如其類型名稱)。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-111">Built-in serializers are more efficient since they know their types cannot change and they do not need to include information about the type like its type name.</span></span>

<span data-ttu-id="ccf1a-112">Reliable State Manager 具有下列類型的內建序列化程式：</span><span class="sxs-lookup"><span data-stu-id="ccf1a-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="ccf1a-113">Guid</span><span class="sxs-lookup"><span data-stu-id="ccf1a-113">Guid</span></span>
- <span data-ttu-id="ccf1a-114">布林</span><span class="sxs-lookup"><span data-stu-id="ccf1a-114">bool</span></span>
- <span data-ttu-id="ccf1a-115">byte</span><span class="sxs-lookup"><span data-stu-id="ccf1a-115">byte</span></span>
- <span data-ttu-id="ccf1a-116">sbyte</span><span class="sxs-lookup"><span data-stu-id="ccf1a-116">sbyte</span></span>
- <span data-ttu-id="ccf1a-117">byte[]</span><span class="sxs-lookup"><span data-stu-id="ccf1a-117">byte[]</span></span>
- <span data-ttu-id="ccf1a-118">char</span><span class="sxs-lookup"><span data-stu-id="ccf1a-118">char</span></span>
- <span data-ttu-id="ccf1a-119">字串</span><span class="sxs-lookup"><span data-stu-id="ccf1a-119">string</span></span>
- <span data-ttu-id="ccf1a-120">decimal</span><span class="sxs-lookup"><span data-stu-id="ccf1a-120">decimal</span></span>
- <span data-ttu-id="ccf1a-121">double</span><span class="sxs-lookup"><span data-stu-id="ccf1a-121">double</span></span>
- <span data-ttu-id="ccf1a-122">float</span><span class="sxs-lookup"><span data-stu-id="ccf1a-122">float</span></span>
- <span data-ttu-id="ccf1a-123">int</span><span class="sxs-lookup"><span data-stu-id="ccf1a-123">int</span></span>
- <span data-ttu-id="ccf1a-124">uint</span><span class="sxs-lookup"><span data-stu-id="ccf1a-124">uint</span></span>
- <span data-ttu-id="ccf1a-125">long</span><span class="sxs-lookup"><span data-stu-id="ccf1a-125">long</span></span>
- <span data-ttu-id="ccf1a-126">ulong</span><span class="sxs-lookup"><span data-stu-id="ccf1a-126">ulong</span></span>
- <span data-ttu-id="ccf1a-127">short</span><span class="sxs-lookup"><span data-stu-id="ccf1a-127">short</span></span>
- <span data-ttu-id="ccf1a-128">ushort</span><span class="sxs-lookup"><span data-stu-id="ccf1a-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="ccf1a-129">自訂序列化</span><span class="sxs-lookup"><span data-stu-id="ccf1a-129">Custom Serialization</span></span>

<span data-ttu-id="ccf1a-130">自訂序列化程式通常是用來提升效能，或是透過網路和在磁碟上加密資料。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-130">Custom serializers are commonly used to increase performance or to encrypt the data over the wire and on disk.</span></span> <span data-ttu-id="ccf1a-131">自訂序列化程式通常比一般序列化程式更有效率，最主要的原因是因為它們不需要將類型的相關資訊序列化。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need to serialize information about the type.</span></span> 

<span data-ttu-id="ccf1a-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) 可用來為指定的類型 T 註冊自訂序列化程式。您應該在建構 StatefulServiceBase 時進行這項註冊，以確保在開始復原之前，所有 Reliable Collections 都能存取相關的序列化程式以讀取其保存資料。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used to register a custom serializer for the given type T. This registration should happen in the construction of the StatefulServiceBase to ensure that before recovery starts, all Reliable Collections have access to the relevant serializer to read their persisted data.</span></span>

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed to set OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> <span data-ttu-id="ccf1a-133">自訂序列化程式的優先順序高於內建的序列化程式。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="ccf1a-134">例如，在為 int 註冊自訂序列化程式之後，系統就會使用它將整數序列化，而不會使用 int 的內建序列化程式。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-134">For example, when a custom serializer for int is registered, it is used to serialize integers instead of the built-in serializer for int.</span></span>

### <a name="how-to-implement-a-custom-serializer"></a><span data-ttu-id="ccf1a-135">如何實作自訂序列化程式</span><span class="sxs-lookup"><span data-stu-id="ccf1a-135">How to implement a custom serializer</span></span>

<span data-ttu-id="ccf1a-136">自訂序列化程式需要實作 [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) 介面。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-136">A custom serializer needs to implement the [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="ccf1a-137">IStateSerializer<T> 包含會接受額外 T (稱為基底值) 的 Write 和 Read 多載。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="ccf1a-138">此 API 適用於差異序列化。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-138">This API is for differential serialization.</span></span> <span data-ttu-id="ccf1a-139">目前並未公開差異序列化功能。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="ccf1a-140">因此，將等到公開並啟用差異序列化之後，才會呼叫這兩個多載。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="ccf1a-141">以下是一個名為 OrderKey 且包含四個屬性的範例自訂類型</span><span class="sxs-lookup"><span data-stu-id="ccf1a-141">Following is an example custom type called OrderKey that contains four properties</span></span>

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

<span data-ttu-id="ccf1a-142">以下是 IStateSerializer<OrderKey> 的範例實作。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="ccf1a-143">請注意，接受 baseValue 的 Read 和 Write 多載會呼叫其個別的多載以滿足向後相容性。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

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

## <a name="upgradability"></a><span data-ttu-id="ccf1a-144">可升級性</span><span class="sxs-lookup"><span data-stu-id="ccf1a-144">Upgradability</span></span>
<span data-ttu-id="ccf1a-145">在 [輪流應用程式升級](service-fabric-application-upgrade.md)中，升級會套用至節點的子集，一次一個升級網域。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), the upgrade is applied to a subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="ccf1a-146">在此過程中，某些升級網域會比您的應用程式版本新，而某些升級網域會比您的應用程式的版本舊。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-146">During this process, some upgrade domains will be on the newer version of your application, and some upgrade domains will be on the older version of your application.</span></span> <span data-ttu-id="ccf1a-147">在首度發行期間，新版的應用程式必須能夠讀取舊版的資料，而舊版的應用程式必須能夠讀取新版的資料。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-147">During the rollout, the new version of your application must be able to read the old version of your data, and the old version of your application must be able to read the new version of your data.</span></span> <span data-ttu-id="ccf1a-148">如果資料格式沒有向前及向後相容，升級便可能會失敗，或是發生更糟糕的狀況，像是資料可能會遺失或損毀。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-148">If the data format is not forward and backward compatible, the upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="ccf1a-149">如果您使用的是內建序列化程式，就不需要擔心相容性。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-149">If you are using  built-in serializer, you do not have to worry about compatibility.</span></span>
<span data-ttu-id="ccf1a-150">不過，如果您使用的是自訂序列化程式或 DataContractSerializer，資料就必須無限地往前和往後相容。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-150">However, if you are using a custom serializer or the DataContractSerializer, the data have to be infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="ccf1a-151">換句話說，每個還原序列化版本都必須能夠將該類型的任何版本序列化或還原序列化。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-151">In other words, each version of serializer needs to be able to serialize and de-serialize any version of the type.</span></span>

<span data-ttu-id="ccf1a-152">「資料合約」使用者應該依照妥善定義的版本控制規則來新增、移除及變更欄位。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-152">Data Contract users should follow the well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="ccf1a-153">「資料合約」也支援處理未知欄位、連結到序列化和還原序列化程序，以及處理類別繼承。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-153">Data Contract also has support for dealing with unknown fields, hooking into the serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="ccf1a-154">如需詳細資訊，請參閱 [使用資料合約](https://msdn.microsoft.com/library/ms733127.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="ccf1a-155">自訂序列化程式使用者應該遵守所使用序列化程式的準則，以確保能夠往前和往後相容。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-155">Custom serializer users should adhere to the guidelines of the serializer they are using to make sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="ccf1a-156">支援所有版本的常見方式是在開頭新增大小資訊，並且只新增選用的屬性。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-156">Common way of supporting all versions is adding size information at the beginning and only adding optional properties.</span></span>
<span data-ttu-id="ccf1a-157">如此一來，每個版本便可儘可能地讀取資料，然後跳過資料流的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-157">This way each version can read as much it can and jump over the remaining part of the stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccf1a-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ccf1a-158">Next steps</span></span>
  * [<span data-ttu-id="ccf1a-159">序列化與升級</span><span class="sxs-lookup"><span data-stu-id="ccf1a-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="ccf1a-160">可靠的集合的開發人員參考資料</span><span class="sxs-lookup"><span data-stu-id="ccf1a-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="ccf1a-161">[使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md) 將引導您完成使用 Visual Studio 進行應用程式升級的步驟。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="ccf1a-162">[使用 PowerShell 升級您的應用程式](service-fabric-application-upgrade-tutorial-powershell.md) 將引導您完成使用 PowerShell 進行應用程式升級的步驟。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="ccf1a-163">使用 [升級參數](service-fabric-application-upgrade-parameters.md)來控制您應用程式的升級方式。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="ccf1a-164">參考 [進階主題](service-fabric-application-upgrade-advanced.md)，以了解如何在升級您的應用程式時使用進階功能。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-164">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="ccf1a-165">參考 [疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)中的步驟，以修正應用程式升級中常見的問題。</span><span class="sxs-lookup"><span data-stu-id="ccf1a-165">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
