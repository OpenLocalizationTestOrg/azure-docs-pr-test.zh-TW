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
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="72829-103">Azure Service Fabric 中的 Reliable Collection 物件序列化</span><span class="sxs-lookup"><span data-stu-id="72829-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="72829-104">可靠集合複寫，並將保存其項目 toomake 確認他們的電腦故障和電力中斷等跨持久。</span><span class="sxs-lookup"><span data-stu-id="72829-104">Reliable Collections' replicate and persist their items toomake sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="72829-105">Tooreplicate 和 toopersist 項目、 可靠集合需要 tooserialize 它們。</span><span class="sxs-lookup"><span data-stu-id="72829-105">Both tooreplicate and toopersist items, Reliable Collections' need tooserialize them.</span></span>

<span data-ttu-id="72829-106">可靠的集合取得可靠狀態管理員從指定的型別 hello 適當的序列化程式。</span><span class="sxs-lookup"><span data-stu-id="72829-106">Reliable Collections' get hello appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="72829-107">Reliable 狀態管理員包含內建的序列化程式，以及可讓自訂序列化程式 toobe 註冊指定的型別。</span><span class="sxs-lookup"><span data-stu-id="72829-107">Reliable State Manager contains built-in serializers and allows custom serializers toobe registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="72829-108">內建的序列化程式</span><span class="sxs-lookup"><span data-stu-id="72829-108">Built-in Serializers</span></span>

<span data-ttu-id="72829-109">Reliable State Manager 包含一些常見類型的內建序列化程式，以便透過預設方式有效率地將這些類型序列化。</span><span class="sxs-lookup"><span data-stu-id="72829-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="72829-110">對於其他類型，可靠的狀態管理員就會回到 toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="72829-110">For other types, Reliable State Manager falls back toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="72829-111">內建的序列化程式會更有效率，因為他們知道無法變更其類型，而且它們不需要 tooinclude hello 型別，其型別名稱類似的資訊。</span><span class="sxs-lookup"><span data-stu-id="72829-111">Built-in serializers are more efficient since they know their types cannot change and they do not need tooinclude information about hello type like its type name.</span></span>

<span data-ttu-id="72829-112">Reliable State Manager 具有下列類型的內建序列化程式：</span><span class="sxs-lookup"><span data-stu-id="72829-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="72829-113">Guid</span><span class="sxs-lookup"><span data-stu-id="72829-113">Guid</span></span>
- <span data-ttu-id="72829-114">布林</span><span class="sxs-lookup"><span data-stu-id="72829-114">bool</span></span>
- <span data-ttu-id="72829-115">byte</span><span class="sxs-lookup"><span data-stu-id="72829-115">byte</span></span>
- <span data-ttu-id="72829-116">sbyte</span><span class="sxs-lookup"><span data-stu-id="72829-116">sbyte</span></span>
- <span data-ttu-id="72829-117">byte[]</span><span class="sxs-lookup"><span data-stu-id="72829-117">byte[]</span></span>
- <span data-ttu-id="72829-118">char</span><span class="sxs-lookup"><span data-stu-id="72829-118">char</span></span>
- <span data-ttu-id="72829-119">字串</span><span class="sxs-lookup"><span data-stu-id="72829-119">string</span></span>
- <span data-ttu-id="72829-120">decimal</span><span class="sxs-lookup"><span data-stu-id="72829-120">decimal</span></span>
- <span data-ttu-id="72829-121">double</span><span class="sxs-lookup"><span data-stu-id="72829-121">double</span></span>
- <span data-ttu-id="72829-122">float</span><span class="sxs-lookup"><span data-stu-id="72829-122">float</span></span>
- <span data-ttu-id="72829-123">int</span><span class="sxs-lookup"><span data-stu-id="72829-123">int</span></span>
- <span data-ttu-id="72829-124">uint</span><span class="sxs-lookup"><span data-stu-id="72829-124">uint</span></span>
- <span data-ttu-id="72829-125">long</span><span class="sxs-lookup"><span data-stu-id="72829-125">long</span></span>
- <span data-ttu-id="72829-126">ulong</span><span class="sxs-lookup"><span data-stu-id="72829-126">ulong</span></span>
- <span data-ttu-id="72829-127">short</span><span class="sxs-lookup"><span data-stu-id="72829-127">short</span></span>
- <span data-ttu-id="72829-128">ushort</span><span class="sxs-lookup"><span data-stu-id="72829-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="72829-129">自訂序列化</span><span class="sxs-lookup"><span data-stu-id="72829-129">Custom Serialization</span></span>

<span data-ttu-id="72829-130">自訂序列化程式是常用的 tooincrease 效能或 tooencrypt hello 資料上 hello 傳輸，而在磁碟上。</span><span class="sxs-lookup"><span data-stu-id="72829-130">Custom serializers are commonly used tooincrease performance or tooencrypt hello data over hello wire and on disk.</span></span> <span data-ttu-id="72829-131">其中一個原因，自訂序列化程式是比一般的序列化程式通常更有效率，因為它們不需要 tooserialize hello 類型的資訊。</span><span class="sxs-lookup"><span data-stu-id="72829-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need tooserialize information about hello type.</span></span> 

<span data-ttu-id="72829-132">[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) hello 類型 t 的自訂序列化程式是使用的 tooregister此註冊應該在 hello StatefulServiceBase tooensure hello 建構復原啟動之前，所有可靠集合都具有存取 toohello 相關的序列化程式 tooread 保存的資料。</span><span class="sxs-lookup"><span data-stu-id="72829-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used tooregister a custom serializer for hello given type T. This registration should happen in hello construction of hello StatefulServiceBase tooensure that before recovery starts, all Reliable Collections have access toohello relevant serializer tooread their persisted data.</span></span>

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
> <span data-ttu-id="72829-133">自訂序列化程式的優先順序高於內建的序列化程式。</span><span class="sxs-lookup"><span data-stu-id="72829-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="72829-134">例如，int 的自訂序列化程式註冊時，它是使用的 tooserialize 整數而不是 int 的 hello 在內建序列化程式</span><span class="sxs-lookup"><span data-stu-id="72829-134">For example, when a custom serializer for int is registered, it is used tooserialize integers instead of hello built-in serializer for int.</span></span>

### <a name="how-tooimplement-a-custom-serializer"></a><span data-ttu-id="72829-135">如何 tooimplement 自訂序列化程式</span><span class="sxs-lookup"><span data-stu-id="72829-135">How tooimplement a custom serializer</span></span>

<span data-ttu-id="72829-136">自訂序列化程式需要 tooimplement hello [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1)介面。</span><span class="sxs-lookup"><span data-stu-id="72829-136">A custom serializer needs tooimplement hello [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="72829-137">IStateSerializer<T> 包含會接受額外 T (稱為基底值) 的 Write 和 Read 多載。</span><span class="sxs-lookup"><span data-stu-id="72829-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="72829-138">此 API 適用於差異序列化。</span><span class="sxs-lookup"><span data-stu-id="72829-138">This API is for differential serialization.</span></span> <span data-ttu-id="72829-139">目前並未公開差異序列化功能。</span><span class="sxs-lookup"><span data-stu-id="72829-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="72829-140">因此，將等到公開並啟用差異序列化之後，才會呼叫這兩個多載。</span><span class="sxs-lookup"><span data-stu-id="72829-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="72829-141">以下是一個名為 OrderKey 且包含四個屬性的範例自訂類型</span><span class="sxs-lookup"><span data-stu-id="72829-141">Following is an example custom type called OrderKey that contains four properties</span></span>

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

<span data-ttu-id="72829-142">以下是 IStateSerializer<OrderKey> 的範例實作。</span><span class="sxs-lookup"><span data-stu-id="72829-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="72829-143">請注意，接受 baseValue 的 Read 和 Write 多載會呼叫其個別的多載以滿足向後相容性。</span><span class="sxs-lookup"><span data-stu-id="72829-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

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

## <a name="upgradability"></a><span data-ttu-id="72829-144">可升級性</span><span class="sxs-lookup"><span data-stu-id="72829-144">Upgradability</span></span>
<span data-ttu-id="72829-145">在[復原應用程式升級](service-fabric-application-upgrade.md)，hello 升級已套用的 tooa 節點的子集，一次一個升級網域。</span><span class="sxs-lookup"><span data-stu-id="72829-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), hello upgrade is applied tooa subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="72829-146">在此過程中，某些升級網域會 hello 較新版本的應用程式，而且某些升級網域會在 hello 較舊版本的應用程式。</span><span class="sxs-lookup"><span data-stu-id="72829-146">During this process, some upgrade domains will be on hello newer version of your application, and some upgrade domains will be on hello older version of your application.</span></span> <span data-ttu-id="72829-147">Hello 首展期間 hello 新版本的應用程式必須是能夠 tooread hello 舊版本的資料，而且 hello 舊版本的應用程式必須能夠 tooread hello 新版本的資料。</span><span class="sxs-lookup"><span data-stu-id="72829-147">During hello rollout, hello new version of your application must be able tooread hello old version of your data, and hello old version of your application must be able tooread hello new version of your data.</span></span> <span data-ttu-id="72829-148">如果 hello 資料格式不是向前和向後相容，hello 升級可能會失敗，或更糟的是，資料可能遺失或損毀。</span><span class="sxs-lookup"><span data-stu-id="72829-148">If hello data format is not forward and backward compatible, hello upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="72829-149">如果您使用的在內建序列化程式，表示您沒有 tooworry 有關相容性。</span><span class="sxs-lookup"><span data-stu-id="72829-149">If you are using  built-in serializer, you do not have tooworry about compatibility.</span></span>
<span data-ttu-id="72829-150">不過，如果您使用自訂序列化程式或 hello DataContractSerializer，hello 資料有 toobe 無限回溯，往後相容性。</span><span class="sxs-lookup"><span data-stu-id="72829-150">However, if you are using a custom serializer or hello DataContractSerializer, hello data have toobe infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="72829-151">換句話說，每個版本的序列化程式需要 toobe 無法 tooserialize 和還原序列化 hello 類型的任何版本。</span><span class="sxs-lookup"><span data-stu-id="72829-151">In other words, each version of serializer needs toobe able tooserialize and de-serialize any version of hello type.</span></span>

<span data-ttu-id="72829-152">資料合約使用者應遵循新增、 移除和變更欄位的 hello 妥善定義的版本控制規則。</span><span class="sxs-lookup"><span data-stu-id="72829-152">Data Contract users should follow hello well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="72829-153">資料合約也有支援處理具有未知的欄位、 攔截到 hello 序列化和還原序列化程序，和處理的類別繼承。</span><span class="sxs-lookup"><span data-stu-id="72829-153">Data Contract also has support for dealing with unknown fields, hooking into hello serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="72829-154">如需詳細資訊，請參閱 [使用資料合約](https://msdn.microsoft.com/library/ms733127.aspx)。</span><span class="sxs-lookup"><span data-stu-id="72829-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="72829-155">自訂序列化程式的使用者均應遵守 toohello hello 他們使用 toomake 確定回溯，而且往後相容性的序列化程式的指導方針。</span><span class="sxs-lookup"><span data-stu-id="72829-155">Custom serializer users should adhere toohello guidelines of hello serializer they are using toomake sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="72829-156">支援所有版本的常見方式在 hello 開頭，並只加入選擇性的屬性加入大小資訊。</span><span class="sxs-lookup"><span data-stu-id="72829-156">Common way of supporting all versions is adding size information at hello beginning and only adding optional properties.</span></span>
<span data-ttu-id="72829-157">這種方式可以讀取每個版本最多可以並跳過 hello hello 資料流的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="72829-157">This way each version can read as much it can and jump over hello remaining part of hello stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72829-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="72829-158">Next steps</span></span>
  * [<span data-ttu-id="72829-159">序列化與升級</span><span class="sxs-lookup"><span data-stu-id="72829-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="72829-160">可靠的集合的開發人員參考資料</span><span class="sxs-lookup"><span data-stu-id="72829-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="72829-161">[使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md) 將引導您完成使用 Visual Studio 進行應用程式升級的步驟。</span><span class="sxs-lookup"><span data-stu-id="72829-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="72829-162">[使用 PowerShell 升級您的應用程式](service-fabric-application-upgrade-tutorial-powershell.md) 將引導您完成使用 PowerShell 進行應用程式升級的步驟。</span><span class="sxs-lookup"><span data-stu-id="72829-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="72829-163">使用 [升級參數](service-fabric-application-upgrade-parameters.md)來控制您應用程式的升級方式。</span><span class="sxs-lookup"><span data-stu-id="72829-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="72829-164">了解 toouse 把太升級您的應用程式時所進階的功能[進階主題](service-fabric-application-upgrade-advanced.md)。</span><span class="sxs-lookup"><span data-stu-id="72829-164">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="72829-165">藉由參考 toohello 步驟中的修正應用程式升級的一般問題[疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="72829-165">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
