### 数据结构说明

- 为了更好的使用该模块，整理了用于读取系统信息各个模块的数据结构。

#### 内存数据结构

[代码位置](https://github.com/Mykrobin/gopsutil/blob/master/mem/mem.go)

```c
type VirtualMemoryStat struct {
	// Total amount of RAM on this system
	Total uint64 `json:"total"`

	// RAM available for programs to allocate
	//
	// This value is computed from the kernel specific values.
	Available uint64 `json:"available"`

	// RAM used by programs
	//
	// This value is computed from the kernel specific values.
	Used uint64 `json:"used"`

	// Percentage of RAM used by programs
	//
	// This value is computed from the kernel specific values.
	UsedPercent float64 `json:"usedPercent"`

	// This is the kernel's notion of free memory; RAM chips whose bits nobody
	// cares about the value of right now. For a human consumable number,
	// Available is what you really want.
	Free uint64 `json:"free"`

	// OS X / BSD specific numbers:
	// http://www.macyourself.com/2010/02/17/what-is-free-wired-active-and-inactive-system-memory-ram/
	Active   uint64 `json:"active"`
	Inactive uint64 `json:"inactive"`
	Wired    uint64 `json:"wired"`

	// FreeBSD specific numbers:
	// https://reviews.freebsd.org/D8467
	Laundry uint64 `json:"laundry"`

	// Linux specific numbers
	// https://www.centos.org/docs/5/html/5.1/Deployment_Guide/s2-proc-meminfo.html
	// https://www.kernel.org/doc/Documentation/filesystems/proc.txt
	// https://www.kernel.org/doc/Documentation/vm/overcommit-accounting
	Buffers        uint64 `json:"buffers"`
	Cached         uint64 `json:"cached"`
	Writeback      uint64 `json:"writeback"`
	Dirty          uint64 `json:"dirty"`
	WritebackTmp   uint64 `json:"writebacktmp"`
	Shared         uint64 `json:"shared"`
	Slab           uint64 `json:"slab"`
	SReclaimable   uint64 `json:"sreclaimable"`
	SUnreclaim     uint64 `json:"sunreclaim"`
	PageTables     uint64 `json:"pagetables"`
	SwapCached     uint64 `json:"swapcached"`
	CommitLimit    uint64 `json:"commitlimit"`
	CommittedAS    uint64 `json:"committedas"`
	HighTotal      uint64 `json:"hightotal"`
	HighFree       uint64 `json:"highfree"`
	LowTotal       uint64 `json:"lowtotal"`
	LowFree        uint64 `json:"lowfree"`
	SwapTotal      uint64 `json:"swaptotal"`
	SwapFree       uint64 `json:"swapfree"`
	Mapped         uint64 `json:"mapped"`
	VMallocTotal   uint64 `json:"vmalloctotal"`
	VMallocUsed    uint64 `json:"vmallocused"`
	VMallocChunk   uint64 `json:"vmallocchunk"`
	HugePagesTotal uint64 `json:"hugepagestotal"`
	HugePagesFree  uint64 `json:"hugepagesfree"`
	HugePageSize   uint64 `json:"hugepagesize"`
}
```

#### CPU数据结构

[代码位置](https://github.com/Mykrobin/gopsutil/blob/master/cpu/cpu.go)

```c
type TimesStat struct {
	CPU       string  `json:"cpu"`
	User      float64 `json:"user"`
	System    float64 `json:"system"`
	Idle      float64 `json:"idle"`
	Nice      float64 `json:"nice"`
	Iowait    float64 `json:"iowait"`
	Irq       float64 `json:"irq"`
	Softirq   float64 `json:"softirq"`
	Steal     float64 `json:"steal"`
	Guest     float64 `json:"guest"`
	GuestNice float64 `json:"guestNice"`
}

type InfoStat struct {
	CPU        int32    `json:"cpu"`
	VendorID   string   `json:"vendorId"`
	Family     string   `json:"family"`
	Model      string   `json:"model"`
	Stepping   int32    `json:"stepping"`
	PhysicalID string   `json:"physicalId"`
	CoreID     string   `json:"coreId"`
	Cores      int32    `json:"cores"`
	ModelName  string   `json:"modelName"`
	Mhz        float64  `json:"mhz"`
	CacheSize  int32    `json:"cacheSize"`
	Flags      []string `json:"flags"`
	Microcode  string   `json:"microcode"`
}
```

#### 磁盘数据结构

[代码位置](https://github.com/Mykrobin/gopsutil/blob/master/disk/disk.go)

```c
type UsageStat struct {
	Path              string  `json:"path"`
	Fstype            string  `json:"fstype"`
	Total             uint64  `json:"total"`
	Free              uint64  `json:"free"`
	Used              uint64  `json:"used"`
	UsedPercent       float64 `json:"usedPercent"`
	InodesTotal       uint64  `json:"inodesTotal"`
	InodesUsed        uint64  `json:"inodesUsed"`
	InodesFree        uint64  `json:"inodesFree"`
	InodesUsedPercent float64 `json:"inodesUsedPercent"`
}

type PartitionStat struct {
	Device     string `json:"device"`
	Mountpoint string `json:"mountpoint"`
	Fstype     string `json:"fstype"`
	Opts       string `json:"opts"`
}

type IOCountersStat struct {
	ReadCount        uint64 `json:"readCount"`
	MergedReadCount  uint64 `json:"mergedReadCount"`
	WriteCount       uint64 `json:"writeCount"`
	MergedWriteCount uint64 `json:"mergedWriteCount"`
	ReadBytes        uint64 `json:"readBytes"`
	WriteBytes       uint64 `json:"writeBytes"`
	ReadTime         uint64 `json:"readTime"`
	WriteTime        uint64 `json:"writeTime"`
	IopsInProgress   uint64 `json:"iopsInProgress"`
	IoTime           uint64 `json:"ioTime"`
	WeightedIO       uint64 `json:"weightedIO"`
	Name             string `json:"name"`
	SerialNumber     string `json:"serialNumber"`
	Label            string `json:"label"`
}
```



#### 网络数据结构

[代码位置](https://github.com/Mykrobin/gopsutil/blob/master/net/net.go)

```c
type IOCountersStat struct {
	Name        string `json:"name"`        // interface name
	BytesSent   uint64 `json:"bytesSent"`   // number of bytes sent
	BytesRecv   uint64 `json:"bytesRecv"`   // number of bytes received
	PacketsSent uint64 `json:"packetsSent"` // number of packets sent
	PacketsRecv uint64 `json:"packetsRecv"` // number of packets received
	Errin       uint64 `json:"errin"`       // total number of errors while receiving
	Errout      uint64 `json:"errout"`      // total number of errors while sending
	Dropin      uint64 `json:"dropin"`      // total number of incoming packets which were dropped
	Dropout     uint64 `json:"dropout"`     // total number of outgoing packets which were dropped (always 0 on OSX and BSD)
	Fifoin      uint64 `json:"fifoin"`      // total number of FIFO buffers errors while receiving
	Fifoout     uint64 `json:"fifoout"`     // total number of FIFO buffers errors while sending

}

// Addr is implemented compatibility to psutil
type Addr struct {
	IP   string `json:"ip"`
	Port uint32 `json:"port"`
}

type ConnectionStat struct {
	Fd     uint32  `json:"fd"`
	Family uint32  `json:"family"`
	Type   uint32  `json:"type"`
	Laddr  Addr    `json:"localaddr"`
	Raddr  Addr    `json:"remoteaddr"`
	Status string  `json:"status"`
	Uids   []int32 `json:"uids"`
	Pid    int32   `json:"pid"`
}

// System wide stats about different network protocols
type ProtoCountersStat struct {
	Protocol string           `json:"protocol"`
	Stats    map[string]int64 `json:"stats"`
}

// NetInterfaceAddr is designed for represent interface addresses
type InterfaceAddr struct {
	Addr string `json:"addr"`
}

type InterfaceStat struct {
	Index        int             `json:"index"`
	MTU          int             `json:"mtu"`          // maximum transmission unit
	Name         string          `json:"name"`         // e.g., "en0", "lo0", "eth0.100"
	HardwareAddr string          `json:"hardwareaddr"` // IEEE MAC-48, EUI-48 and EUI-64 form
	Flags        []string        `json:"flags"`        // e.g., FlagUp, FlagLoopback, FlagMulticast
	Addrs        []InterfaceAddr `json:"addrs"`
}

type FilterStat struct {
	ConnTrackCount int64 `json:"conntrackCount"`
	ConnTrackMax   int64 `json:"conntrackMax"`
}

// ConntrackStat has conntrack summary info
type ConntrackStat struct {
	Entries       uint32 `json:"entries"`        // Number of entries in the conntrack table
	Searched      uint32 `json:"searched"`       // Number of conntrack table lookups performed
	Found         uint32 `json:"found"`          // Number of searched entries which were successful
	New           uint32 `json:"new"`            // Number of entries added which were not expected before
	Invalid       uint32 `json:"invalid"`        // Number of packets seen which can not be tracked
	Ignore        uint32 `json:"ignore"`         // Packets seen which are already connected to an entry
	Delete        uint32 `json:"delete"`         // Number of entries which were removed
	DeleteList    uint32 `json:"delete_list"`    // Number of entries which were put to dying list
	Insert        uint32 `json:"insert"`         // Number of entries inserted into the list
	InsertFailed  uint32 `json:"insert_failed"`  // # insertion attempted but failed (same entry exists)
	Drop          uint32 `json:"drop"`           // Number of packets dropped due to conntrack failure.
	EarlyDrop     uint32 `json:"early_drop"`     // Dropped entries to make room for new ones, if maxsize reached
	IcmpError     uint32 `json:"icmp_error"`     // Subset of invalid. Packets that can't be tracked d/t error
	ExpectNew     uint32 `json:"expect_new"`     // Entries added after an expectation was already present
	ExpectCreate  uint32 `json:"expect_create"`  // Expectations added
	ExpectDelete  uint32 `json:"expect_delete"`  // Expectations deleted
	SearchRestart uint32 `json:"search_restart"` // Conntrack table lookups restarted due to hashtable resizes
}
```



#### 进程数据结构

[代码位置](https://github.com/Mykrobin/gopsutil/blob/master/process/process.go)

```c
type Process struct {
	Pid            int32 `json:"pid"`
	name           string
	status         string
	parent         int32
	parentMutex    sync.RWMutex // for windows ppid cache
	numCtxSwitches *NumCtxSwitchesStat
	uids           []int32
	gids           []int32
	groups         []int32
	numThreads     int32
	memInfo        *MemoryInfoStat
	sigInfo        *SignalInfoStat
	createTime     int64

	lastCPUTimes *cpu.TimesStat
	lastCPUTime  time.Time

	tgid int32
}

type OpenFilesStat struct {
	Path string `json:"path"`
	Fd   uint64 `json:"fd"`
}

type MemoryInfoStat struct {
	RSS    uint64 `json:"rss"`    // bytes
	VMS    uint64 `json:"vms"`    // bytes
	HWM    uint64 `json:"hwm"`    // bytes
	Data   uint64 `json:"data"`   // bytes
	Stack  uint64 `json:"stack"`  // bytes
	Locked uint64 `json:"locked"` // bytes
	Swap   uint64 `json:"swap"`   // bytes
}

type SignalInfoStat struct {
	PendingProcess uint64 `json:"pending_process"`
	PendingThread  uint64 `json:"pending_thread"`
	Blocked        uint64 `json:"blocked"`
	Ignored        uint64 `json:"ignored"`
	Caught         uint64 `json:"caught"`
}

type RlimitStat struct {
	Resource int32  `json:"resource"`
	Soft     int32  `json:"soft"` //TODO too small. needs to be uint64
	Hard     int32  `json:"hard"` //TODO too small. needs to be uint64
	Used     uint64 `json:"used"`
}

type IOCountersStat struct {
	ReadCount  uint64 `json:"readCount"`
	WriteCount uint64 `json:"writeCount"`
	ReadBytes  uint64 `json:"readBytes"`
	WriteBytes uint64 `json:"writeBytes"`
}

type NumCtxSwitchesStat struct {
	Voluntary   int64 `json:"voluntary"`
	Involuntary int64 `json:"involuntary"`
}

type PageFaultsStat struct {
	MinorFaults      uint64 `json:"minorFaults"`
	MajorFaults      uint64 `json:"majorFaults"`
	ChildMinorFaults uint64 `json:"childMinorFaults"`
	ChildMajorFaults uint64 `json:"childMajorFaults"`
}
```

