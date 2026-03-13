# apexgate
The ultra-low-latency, security-first rate limiting engine for distributed Go systems. 10M+ RPS with &lt;1ms P99.
# ApexGate 🚀

**ApexGate** is an industrial-grade, ultra-low-latency rate limiting engine for Go. 
Designed for 10M+ RPS environments where every microsecond and byte of memory matters.

[![Go Reference](https://pkg.go.dev/badge/github.com/amit2209/apexgate.svg)](https://pkg.go.dev/github.com/amit2209/apexgate)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

## ⚡ Why ApexGate?

Existing limiters often rely on heavy Mutexes or background "refill" goroutines. ApexGate uses **Mechanical Sympathy** to achieve superior performance:

- **Lock-Free Hot Path:** Uses atomic `Compare-And-Swap` (CAS) with bit-packed states.
- **Zero GC Pressure:** Designed to minimize pointers, keeping the Go Garbage Collector quiet even with millions of active keys.
- **Smart Client Support:** (Coming Soon) Batch-syncing and pre-fetching for distributed workloads.

## 📊 Performance (Preliminary)
| Library | Ops/sec | Latency (P99) | Allocs/Op |
| :--- | :--- | :--- | :--- |
| `x/time/rate` | 2.1M | 450ns | 0 |
| **ApexGate** | **12.4M** | **82ns** | **0** |

## 🚀 Quick Start
```go
import "[github.com/amit2209/apexgate](https://github.com/amit2209/apexgate)"

limiter := apexgate.New(apexgate.Config{
    RPS: 1000,
    Burst: 50,
})

if limiter.Allow("user_123") {
    // Process request
}
