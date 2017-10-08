---
title: "Azure 批次中的使用者帳戶下 aaaRun 工作 |Microsoft 文件"
description: "設定在 Azure Batch 中執行工作所需的使用者帳戶"
services: batch
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.openlocfilehash: 13d7d76451d89a3cca090c4ef24ed0ed781bbf09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a>在 Batch 中的使用者帳戶執行工作

Azure Batch 中的工作一律會在使用者帳戶下執行。 根據預設，會在標準使用者帳戶中執行工作，而不需要系統管理員權限。 這些預設使用者帳戶設定通常已足夠。 某些情況下，不過，對於您想要在其下工作 toorun 有用 toobe 無法 tooconfigure hello 使用者帳戶。 這篇文章討論 hello 類型的使用者帳戶以及如何設定這些案例。

## <a name="types-of-user-accounts"></a>使用者帳戶的類型

Azure Batch 提供執行工作所需的兩種使用者帳戶類型︰

- **自動使用者帳戶。** 自動使用者帳戶是 hello 批次服務會自動建立的內建的使用者帳戶。 根據預設，工作會在自動使用者帳戶下執行。 您可以設定的自動使用者帳戶工作執行工作 tooindicate hello 自動使用者規格。 hello 自動使用者規格可讓您 toospecify hello 提高權限層級和領域的 hello 工作執行的 hello 自動使用者帳戶。 

- **具名的使用者帳戶。** 當您建立 hello 集區時，您可以指定一或多個名稱的使用者帳戶集區。 每個使用者帳戶會建立 hello 集區的每個節點上。 此外 toohello 帳戶名稱，您指定 hello 使用者帳戶密碼，提高權限層級，並針對 Linux 集區，hello SSH 私密金鑰。 當您新增工作時，您可以指定 hello 名為該工作應該執行的使用者帳戶。

> [!IMPORTANT] 
> hello 批次服務版本 2017年-01-01.4.0 導入了需要您更新您的程式碼 toocall 該版本的重大變更。 如果您是從較舊版本的批次移轉程式碼，請注意該 hello **runElevated** hello REST API 或批次用戶端程式庫中不再支援屬性。 使用新的 hello **userIdentity**工作 toospecify 提高權限層級屬性。 請參閱 < hello > 一節[更新您的程式碼 toohello 最新批次用戶端程式庫](#update-your-code-to-the-latest-batch-client-library)需更新您的批次程式碼，如果您使用其中一個 hello 用戶端程式庫的快速指導方針。
>
>

> [!NOTE] 
> 本文所討論的 hello 使用者帳戶不支援遠端桌面通訊協定 (RDP) 或安全殼層 (SSH)，基於安全性考量。 
>
> tooconnect tooa 節點執行 hello Linux 虛擬機器中的設定透過 SSH，請參閱[使用遠端桌面 tooa 在 Azure 中的 Linux VM](../virtual-machines/virtual-machines-linux-use-remote-desktop.md)。 tooconnect toonodes 執行 Windows，透過 RDP，請參閱[連接 tooa Windows Server VM](../virtual-machines/windows/connect-logon.md)。<br /><br />
> tooconnect tooa 節點執行 hello 雲端服務中的設定透過 RDP，請參閱[Azure 雲端服務中的角色啟用遠端桌面連線](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md)。
>
>

## <a name="user-account-access-toofiles-and-directories"></a>使用者帳戶存取 toofiles 和目錄

自動使用者帳戶和名稱的使用者帳戶有讀取/寫入存取 toohello 工作的工作目錄、 共用的目錄和多重執行個體的工作目錄。 這兩種類型的帳戶有讀取權限 toohello 啟動和工作準備的目錄。

如果工作執行下 hello 用於執行啟動工作、 hello 工作的相同帳戶具有讀寫存取 toohello 開始工作目錄。 相同同樣地，hello 如果之下執行的工作執行作業準備工作、 hello 工作所使用的帳戶具有讀寫存取 toohello 作業準備工作目錄。 如果工作執行比 hello 啟動工作或作業準備工作不同的帳戶，然後 hello 工作有只讀取權限 toohello 個別目錄。

如需從工作存取檔案和目錄的相關詳細資訊，請參閱[使用 Batch 開發大規模的平行計算解決方案](batch-api-basics.md#files-and-directories)。

## <a name="elevated-access-for-tasks"></a>提高工作的權限 

hello 使用者帳戶的提高權限層級表示工作是否執行具有提高權限的存取權。 自動使用者帳戶和具名的使用者帳戶都可以使用提高權限的存取權來執行。 提高權限層級的 hello 兩個選項如下：

- **NonAdmin:** hello 工作沒有提高權限的存取權的標準使用者身分執行。 批次的使用者帳戶的 hello 預設提高權限層級是一律**NonAdmin**。
- **系統管理員：** hello 工作具有提高權限的存取權的使用者身分執行，並且作業具有完整的系統管理員權限。 

## <a name="auto-user-accounts"></a>自動使用者帳戶

根據預設，Batch 中的工作會在自動使用者帳戶下執行，以標準使用者身分執行，沒有提高權限的存取權，並具有工作範圍。 Hello 自動使用者規格工作範圍的設定時，hello 批次服務會建立只有該工作的自動使用者帳戶。

hello 替代 tootask 範圍為集區範圍。 Hello 自動使用者規格工作設定為集區範圍，hello 工作會在 hello 集區中的可用 tooany 工作自動使用者帳戶下執行。 多個集區範圍的詳細資訊，請參閱 < hello > 一節[執行工作，如 hello 與集區範圍自動使用者](#run-a-task-as-the-autouser-with-pool-scope)。   

hello 預設範圍是在不同的 Windows 和 Linux 節點上：

- 在 Windows 節點上，工作根據預設會在工作範圍下執行。
- Linux 節點一律會在集區範圍下執行。

有四個可能的設定 hello 自動使用者規格，其中每個對應 tooa 唯一的自動使用者帳戶：

- 與工作範圍 （hello 預設自動使用者規格） 的非系統管理員存取權
- 具有工作範圍的系統管理員 (提升權限) 存取權
- 具有集區範圍的非系統管理員存取權
- 具有集區範圍的系統管理員存取權

> [!IMPORTANT] 
> 工作範圍下執行的工作不需要在節點上的既定存取 tooother 工作。 不過，具有存取 toohello 帳戶的惡意使用者無法解決這項限制提交的工作，以系統管理員權限執行，以及存取其他的工作目錄。 惡意使用者可能也會使用 RDP 或 SSH tooconnect tooa 節點。 很重要的 tooprotect 存取 tooyour 批次帳戶金鑰 tooprevent 這類案例中。 如果您懷疑可能受到危害您的帳戶，是確定 tooregenerate 您的金鑰。
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a>以具有提高權限之存取權的自動使用者身分執行工作

當您需要 toorun 高存取權限的工作時，您可以設定系統管理員權限的 hello 自動使用者規格。 例如，啟動工作可能需要提高權限的存取 tooinstall 軟體 hello 節點上。

> [!NOTE] 
> 一般情況下，建議您最好 toouse 提高權限只在必要時的存取。 最佳作法建議授與 hello 最低權限所需的 tooachieve hello 所要的結果。 比方說，如果啟動工作以安裝軟體 hello 目前的使用者，而不是針對所有使用者，您可能無法授與提高權限的存取 tootasks 的 tooavoid。 您可以設定需要 toorun 下 hello 使用相同帳戶，包括 hello 啟動工作的所有工作的集區範圍和非系統管理員存取權的 hello 自動使用者規格。 
>
>

hello，下列程式碼片段顯示如何 tooconfigure hello 自動使用者規格。 hello 範例設定 hello 提高權限層級太`Admin`和太 hello 範圍`Task`。 工作範圍 hello 預設設定，但是此處涵蓋了 hello 不錯的範例。

#### <a name="batch-net"></a>Batch .NET

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a>Batch Java

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a>Batch Python

```python
user = batchmodels.UserIdentity(
    auto_user=batchmodels.AutoUserSpecification(
        elevation_level=batchmodels.ElevationLevel.admin,
        scope=batchmodels.AutoUserScope.task))
task = batchmodels.TaskAddParameter(
    id='task_1',
    command_line='cmd /c "echo hello world"',
    user_identity=user)
batch_client.task.add(job_id=jobid, task=task)
```

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a>以具有集區範圍的自動使用者身分執行工作

節點會佈建時，會建立兩個整個集區的自動使用者帳戶上 hello 集區中的每個節點，一個具有提高權限的存取權，一個沒有提高權限的存取權。 設定特定工作的 hello 自動為使用者的範圍 toopool 範圍執行 hello 工作，其中兩個整個集區的自動使用者帳戶下。 

當您指定 hello 自動使用者集區範圍時，以系統管理員存取權執行的所有工作都執行下 hello 相同整個集區的自動使用者帳戶。 同樣地，不具系統管理員權限執行的工作，也會在單一的全集區自動使用者帳戶下執行。 

> [!NOTE] 
> hello 兩個整個集區的自動使用者帳戶是不同的帳戶。 Hello 整個集區的系統管理帳戶下執行的工作無法共用資料，與工作執行 hello 標準帳戶，反之亦然。 
>
>

hello 利用 toorunning hello 工作是與 hello 上執行其他工作能 tooshare 資料的相同的自動使用者帳戶是在相同的節點。

共用工作之間的密碼是一種情況，其中執行的工作在其中兩個 hello 整個集區的自動使用者帳戶底下是很有用。 例如，假設啟動工作需要 tooprovision 到可以使用其他工作的 hello 節點上的密碼。 您可以使用 hello Windows 資料保護 API (DPAPI)，但它需要系統管理員權限。 相反地，您可以保護 hello hello 使用者層級的密碼。 工作執行相同的使用者帳戶可以存取的 hello hello 沒有提高權限的存取權的密碼。

另一種情形，您可能需要 toorun 工作與集區範圍自動使用者帳戶是訊息傳遞介面 (MPI) 檔案共用。 MPI 檔案共用時，在 hello MPI 工作需要 toowork 上 hello 節點 hello 相同的檔案資料。 hello 前端節點建立的檔案共用如果 hello 下執行，可以存取 hello 子節點相同的自動使用者帳戶。 

下列程式碼片段的 hello 設定批次.NET hello 自動位使用者的範圍 toopool 範圍的工作。 省略 hello 提高權限層級，因此 hello 工作 hello 標準整個集區的自動使用者帳戶下執行。

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a>具名的使用者帳戶

當您建立集區時，可以定義具名的使用者帳戶。 具名的使用者帳戶具有您提供的名稱和密碼。 您可以指定名稱的使用者帳戶的 hello 提高權限層級。 您也可以提供適用於 Linux 節點的 SSH 私密金鑰。

具名的使用者帳戶存在 hello 集區中的所有節點上，且可用 tooall 工作執行那些節點上。 您可以針對集區定義任意數目的使用者名稱。 當您新增工作或工作集合時，您可以指定其中一個 hello 名為 hello 集區上定義的使用者帳戶執行該 hello 工作。

具名的使用者帳戶是很有用時想 toorun 作業中的所有工作底下 hello 相同的使用者帳戶，但會將從端 hello 其他作業中執行的工作相同的時間。 例如，您可以為每個作業建立具名的使用者，並在該具名的使用者帳戶下執行每個作業的工作。 接著，每個作業可與它自己的工作共用祕密，但不可與其他作業中執行的工作共用祕密。

您也可以使用名稱的使用者帳戶 toorun 外部資源，例如檔案共用設定權限的工作。 使用具名的使用者帳戶，您可以控制 hello 使用者識別，並且可以使用該使用者身分識別 tooset 權限。  

具名的使用者帳戶會啟用 Linux 節點之間的無密碼 SSH。 您可以使用名稱的使用者帳戶與 Linux 節點需要 toorun 多重執行個體的工作。 Hello 集區中的每個節點可以執行 hello 整個集區上定義的使用者帳戶的工作。 如需多重執行個體工作的詳細資訊，請參閱[使用多重\-toorun MPI 應用程式的執行個體工作](batch-mpi.md)。

### <a name="create-named-user-accounts"></a>建立具名的使用者帳戶

toocreate 名為批次中的使用者帳戶新增使用者帳戶 toohello 集區的集合。 hello 下列程式碼片段顯示如何 toocreate 命名.NET、 Java 和 Python 中的使用者帳戶。 這些程式碼片段顯示如何 toocreate 管理員和非管理員帳戶的集區上名為。 hello 範例會建立集區使用 hello 雲端服務組態，但使用相同方法時建立 Windows 或 Linux 的集區，使用 hello 虛擬機器組態的 hello。

#### <a name="batch-net-example-windows"></a>Batch .NET 範例 (Windows)

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using hello cloud service configuration.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                                         
    virtualMachineSize: "small",                                                
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));   

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount("adminUser", "xyz123", ElevationLevel.Admin),
    new UserAccount("nonAdminUser", "123xyz", ElevationLevel.NonAdmin),
};

// Commit hello pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a>Batch .NET 範例 (Linux)

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello virtual machine configuration toouse toocreate hello pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create hello unbound pool.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                             
    virtualMachineSize: "Standard_A1",                                      
    virtualMachineConfiguration: virtualMachineConfiguration);                  

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount(
        name: "adminUser",
        password: "xyz123",
        elevationLevel: ElevationLevel.Admin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 12345,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
    new UserAccount(
        name: "nonAdminUser",
        password: "123xyz",
        elevationLevel: ElevationLevel.NonAdmin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 45678,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
};

// Commit hello pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a>Batch Java 範例

```java
List<UserAccount> userList = new ArrayList<>();
userList.add(new UserAccount().withName(adminUserAccountName).withPassword(adminPassword).withElevationLevel(ElevationLevel.ADMIN));
userList.add(new UserAccount().withName(nonAdminUserAccountName).withPassword(nonAdminPassword).withElevationLevel(ElevationLevel.NONADMIN));
PoolAddParameter addParameter = new PoolAddParameter()
        .withId(poolId)
        .withTargetDedicatedNodes(POOL_VM_COUNT)
        .withVmSize(POOL_VM_SIZE)
        .withCloudServiceConfiguration(configuration)
        .withUserAccounts(userList);
batchClient.poolOperations().createPool(addParameter);
```

#### <a name="batch-python-example"></a>Batch Python 範例

```python
users = [
    batchmodels.UserAccount(
        name='pool-admin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.admin)
    batchmodels.UserAccount(
        name='pool-nonadmin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.nonadmin)
]
pool = batchmodels.PoolAddParameter(
    id=pool_id,
    user_accounts=users,
    virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
        image_reference=image_ref_to_use,
        node_agent_sku_id=sku_to_use),
    vm_size=vm_size,
    target_dedicated=vm_count)
batch_client.pool.add(pool)
```

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a>在具有提高權限之存取權的具名使用者帳戶下執行工作

以提高的使用者，hello 任務的任務 toorun **UserIdentity**屬性 tooa 名為所建立的使用者帳戶其**ElevationLevel**屬性設定太`Admin`。

此程式碼片段會指定該 hello 工作應該執行具名的使用者帳戶。 建立 hello 集區時，此名稱的使用者帳戶已定義 hello 集區上。 在此情況下，建立名為使用者帳戶的 hello 與系統管理員權限：

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a>更新您的程式碼 toohello 最新批次用戶端程式庫

2017-01-01.4.0 導入了一項重大變更，取代 hello hello 批次服務版本**runElevated**屬性可用在舊版本中以 hello **userIdentity**屬性。 下表中的 hello 提供簡單的對應，您可以使用 tooupdate hello 用戶端程式庫的舊版程式碼。

### <a name="batch-net"></a>Batch .NET

| 如果您的程式碼使用...                  | 將它更新為...                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| `CloudTask.RunElevated` 未指定 | 不需要更新                                                                                               |

### <a name="batch-java"></a>Batch Java

| 如果您的程式碼使用...                      | 將它更新為...                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| `CloudTask.withRunElevated` 未指定 | 不需要更新                                                                                                                     |

### <a name="batch-python"></a>Batch Python

| 如果您的程式碼使用...                      | 將它更新為...                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | `user_identity=user`，其中 <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | `user_identity=user`，其中 <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| `run_elevated` 未指定 | 不需要更新                                                                                                                                  |


## <a name="next-steps"></a>後續步驟

### <a name="batch-forum"></a>Batch 論壇

hello [Azure Batch 論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch)MSDN 上會很大的放置 toodiscuss 批次，並詢問 hello 服務有關的問題。 請前去查看很有幫助的釘選文章，在建立 Batch 解決方案時，出現問題就張貼。
