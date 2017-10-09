
## <a name="about-vhds"></a>關於 VHD

hello Azure 中使用的 Vhd 會儲存為 Azure 中的 standard 或 premium 儲存體帳戶中的分頁 blob 的.vhd 檔案。 如需分頁 Blob 的詳細資訊，請參閱 [了解區塊 Blob 和分頁 Blob](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs/)。 如需進階儲存體的詳細資訊，請參閱[高效能的進階儲存體和 Azure VM](../articles/storage/common/storage-premium-storage.md)。

Azure 支援固定磁碟 VHD 格式的 hello。 hello 固定格式奠定 hello 出而呈線性成長 hello 檔案內的邏輯磁碟，所以該磁碟位移 X 就會儲存在 blob 位移 X。在 hello hello blob 結尾的小型頁尾會描述 hello VHD hello 屬性。 通常，hello 固定的格式會因為大多數的磁碟中有大範圍未使用浪費空間。 不過，Azure 儲存.vhd 檔案是以疏鬆格式，因此接收的兩個固定的 hello 的 hello 優點和動態磁碟會在 hello 相同的時間。 如需詳細資訊，請參閱[開始使用虛擬硬碟](https://technet.microsoft.com/library/dd979539.aspx)。

在 Azure toouse 做為來源 toocreate 磁碟或映像處於唯讀狀態中的所有.vhd 檔案。 當您建立磁碟或映像時，Azure 會建立副本 hello.vhd 檔案。 這些複本可以是唯讀或讀-寫，取決於您如何使用 hello VHD。

當您從映像建立虛擬機器時，Azure 會建立 hello hello 來源.vhd 檔案的複本的虛擬機器的磁碟。 tooprotect 遭到意外刪除，Azure 會使用 toocreate 映像、 作業系統磁碟或資料磁碟的任何來源.vhd 檔案上的租用。

您可以刪除來源.vhd 檔案之前，您將需要 tooremove hello 租用的刪除 hello 磁碟或映像。 toodelete 正由虛擬機器做為作業系統磁碟的.vhd 檔案，您可以刪除 hello 虛擬機器、 hello 作業系統磁碟和 hello 來源.vhd 檔案一次刪除 hello 虛擬機器並刪除所有相關聯的磁碟。 不過，刪除做為資料磁碟來源的 .vhd 檔案檔案需要依設定的順序執行幾個步驟。 第一次您 hello 磁碟中的 hello 虛擬機器，然後刪除 hello 磁碟、 卸離，然後再刪除 hello.vhd 檔案。

> [!WARNING]
> 如果您刪除儲存體中的來源 .vhd 檔案從或刪除您的儲存體帳戶，Microsoft 便無法為您復原該資料。
> 

## <a name="types-of-disks"></a>磁碟類型 

Azure 磁碟設計成確保可用性達 99.999%。 Azure 磁碟一直提供企業級持久性，其年度失敗率為零，領先業界。

在建立磁碟時，您有兩個可供選擇的儲存體效能層級，分別是標準儲存體和進階儲存體。 此外，磁碟也有兩種類型，即非受控和受控，這兩種類型可以位於任一個效能層級。


### <a name="standard-storage"></a>標準儲存體 

標準儲存體是以 HDD 為後盾，既可提供符合成本效益的儲存體，又可保有效能。 標準儲存體可複寫到一個資料中心的本機位置，或是利用主要和次要資料中心提供異地備援。 如需儲存體複寫的詳細資訊，請參閱 [Azure 儲存體複寫](../articles/storage/common/storage-redundancy.md)。 

如需搭配使用標準儲存體與 VM 磁碟的詳細資訊，請參閱[標準儲存體和磁碟](../articles/storage/common/storage-standard-storage.md)。

### <a name="premium-storage"></a>進階儲存體 

進階儲存體是以 SSD 為後盾，可針對執行時需要大量 I/O 之工作負載的 VM 提供高效能、低延遲的磁碟支援。 進階儲存體可搭配 DS、DSv2、GS、Ls 或 FS 系列的 Azure VM 使用。 如需詳細資訊，請參閱[進階儲存體](../articles/storage/common/storage-premium-storage.md)。

### <a name="unmanaged-disks"></a>非受控磁碟

未受管理的磁碟是 hello 的已使用的 Vm 磁碟的傳統類型。 進行這些動作，您可以建立您自己的儲存體帳戶，並指定該儲存體帳戶，當您建立 hello 磁碟。 您必須確定您沒有將過多的磁碟放在 toomake hello 相同的儲存體帳戶，因為您可能會超出 hello[延展性目標](../articles/storage/common/storage-scalability-targets.md)hello 儲存體帳戶 (例如，20,000 IOPS)，導致 hello Vm 進行節流處理。 使用 unmanaged 磁碟時，您必須 toofigure 出 toomaximize hello 的一或多個儲存體帳戶 tooget hello 最佳效能 Vm 的使用方式。

### <a name="managed-disks"></a>受控磁碟 

管理磁碟控點 hello 儲存體帳戶建立/管理 hello 背景中，並確保您沒有 tooworry hello hello 儲存體帳戶的延展性限制的相關。 您只需要指定 hello 磁碟大小和 hello 效能層 （標準/優質），Azure 會建立，並會為您管理 hello 磁碟。 即使當您新增磁碟或向上和向下調整 hello VM 時，您不需要 tooworry 需 hello 所使用的儲存體。 

您也可以管理每個 Azure 區域中，一個儲存體帳戶中的自訂映像，並使用它們 toocreate 數以百計的 Vm 中 hello 相同訂用帳戶。 如需有關管理磁碟的詳細資訊，請參閱 hello[受管理的磁碟概觀](../articles/virtual-machines/windows/managed-disks-overview.md)。

我們建議您針對新的 Vm，使用 Azure 受管理磁碟和您轉換您先前未受管理的磁碟 toomanaged 的磁碟，hello tootake 利用適用於管理磁碟的許多功能。

### <a name="disk-comparison"></a>磁碟比較

hello 下表提供高階 vs 標準比較兩者 unmanaged 和 managed 磁碟 toohelp 決定哪些 toouse。

|    | Azure 進階磁碟 | Azure 標準磁碟 |
|--- | ------------------ | ------------------- |
| 磁碟類型 | 固態硬碟 (SSD) | 硬碟 (HDD)  |
| 概觀  | 以 SSD 為基礎，針對執行時需要大量 I/O 之工作負載的 VM 或裝載任務關鍵性生產環境的 VM，提供高效能、低延遲的磁碟支援 | 以 HDD 為基礎、符合成本效益的磁碟支援，適用於開發/測試 VM 案例 |
| 案例  | 生產環境和重視效能的工作負載 | 開發/測試、非關鍵性 <br>不常存取 |
| 磁碟大小 | P4: 32 GB (僅限受控磁碟)<br>P6: 64 GB (僅限受控磁碟)<br>P10：128 GB<br>P20：512 GB<br>P30：1024 GB<br>P40：2048 GB<br>P50：4095 GB | 非受控磁碟：1 GB – 4 TB (4095 GB) <br><br>受控磁碟：<br> S4：32 GB <br>S6：64 GB <br>S10：128 GB <br>S20：512 GB <br>S30：1024 GB <br>S40：2048 GB<br>S50：4095 GB| 
| 每一磁碟的輸送量上限 | 250 MB/秒 | 60 MB/秒 | 
| 每一磁碟的 IOPS 上限 | 7500 IOPS | 500 IOPS | 

