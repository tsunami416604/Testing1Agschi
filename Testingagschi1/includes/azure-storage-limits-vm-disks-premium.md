**進階未受管理的虛擬機器磁碟：每一帳戶限制**

| 資源 | 預設限制 |
| --- | --- |
| 每一帳戶的磁碟容量總計 |35 TB |
| 每一帳戶的快照集容量總計 |10 TB |
| 每一帳戶的最大頻寬 (輸入 + 輸出<sup>1</sup>) |<=50 Gbps |

<sup>1</sup>「輸入」是指傳送至某個儲存體帳戶的所有資料 (要求)。 *輸出* 是指從某個儲存體帳戶接收的所有資料 (回應)。

**進階未受管理的虛擬機器磁碟：每一磁碟限制**

| 進階儲存體磁碟類型 | P10 | P20 | P30 |
| --- | --- | --- | --- |
| 磁碟大小 |128 GB |512 GB |1024 GB (1 TB) |
| 每一磁碟的 IOPS 上限 |500 |2300 |5000 |
| 每一磁碟的輸送量上限 |100 MB/秒 | 150 MB/秒 |200 MB/秒 |
| 每個儲存體帳戶的磁碟數量上限 |280 |70 |35 |

**進階未受管理的虛擬機器磁碟：每個 VM 限制**

| 資源 | 預設限制 |
| --- | --- |
| 每個 VM 的最大 IOPS |80,000 IOPS (使用 GS5 VM<sup>1</sup>) |
| 每一 VM 輸送量上限 |2,000 MB/秒 (使用 GS5 VM<sup>1</sup>) |

<sup>1</sup>如需其他 VM 大小的限制，請參考 [VM 大小](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 
