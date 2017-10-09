
## <a name="size-table-definitions"></a>資料表大小定義

- 儲存容量會以 GiB 或是 1024^3 位元組為單位顯示。 當比較磁碟以 GB 為單位 (1000年 ^3 個位元組) toodisks 以 GiB (1024年 ^3) 請記住，GiB 中指定的容量數字可能會出現較小。 例如，1023 GiB = 1098.4 GB
- 磁碟輸送量是以每秒輸入/輸出作業 (IOPS) 和 MBps 進行測量，其中 MBps = 10^6 位元組/每秒。
- 資料磁碟可以在快取模式或取消快取模式下運作。 快取的資料磁碟的作業，hello 主機快取模式設定太**ReadOnly**或**ReadWrite**。  對於未快取的資料磁碟的作業，hello 主機快取模式設定太**無**。
- **預期的網路效能**hello 最大值的彙總頻寬配置每個 VM 類型的所有目的地的所有 nic。 上限不保證，但預期的 tooprovide 指導選取 hello 右 VM hello 適合應用程式類型。 實際網路效能取決於各種因素，包括網路壅塞、應用程式負載和網路設定。 如需最佳化網路輸送量的資訊，請參閱[最佳化 Windows 和 Linux 的網路輸送量](../articles/virtual-network/virtual-network-optimize-network-bandwidth.md)。 tooachieve hello 預期在 Linux 或 Windows 上的網路效能，它可能是必要的 tooselect 特定版本，或最佳化您的 VM。 如需詳細資訊，請參閱[tooreliably 如何測試虛擬機器輸送量](../articles/virtual-network/virtual-network-bandwidth-testing.md)。

- &#8224;16 vCPU 效能會以一致的方式達到 hello 近期版本中的時間上限。


