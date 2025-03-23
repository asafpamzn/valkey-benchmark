# Valkey Polyglot Benchmark

The GO implementation of the Valkey Polyglot Benchmark provides a robust performance testing framework using the [valkey-GLIDE](https://github.com/valkey-io/valkey-glide) client library. This tool enables developers to conduct comprehensive benchmarks of Valkey operations, including throughput testing, latency measurements, and custom command evaluation. 

## Installation

1. Clone the repository:
    ```bash
    git clone <repository-url>
    cd valkey-glide-benchmark/go
    ```

2. Install dependencies:
    ```bash
    go mod init valkey-benchmark
    go get github.com/valkey-io/valkey-glide/go
    go mod tidy
    
    ```

## Basic Usage

Run a basic benchmark:
```bash
go build
./valkey-benchmark -H localhost -p 6379
```

Common usage patterns:
```bash
# Run SET benchmark with 50 parallel clients
./valkey-benchmark -c 50 -t set

# Run GET benchmark with rate limiting
./valkey-benchmark -t get --qps 1000

# Run benchmark for specific duration
./valkey-benchmark --test-duration 60

# Run benchmark with sequential keys
./valkey-benchmark --sequential 1000000
```

## Configuration Options

### Basic Options
- `-H, --host <hostname>`: Server hostname (default: "127.0.0.1")
- `-p, --port <port>`: Server port (default: 6379)
- `-c, --clients <num>`: Number of parallel connections (default: 50)
- `-n, --requests <num>`: Total number of requests (default: 100000)
- `-d, --datasize <bytes>`: Data size for SET operations (default: 3)
- `-t, --type <command>`: Command to benchmark (e.g., SET, GET)

### Advanced Options
- `--threads <num>`: Number of worker threads (default: 1)
- `--test-duration <seconds>`: Run test for specified duration
- `--sequential <keyspace>`: Use sequential keys
- `-r, --random <keyspace>`: Use random keys from keyspace

### Rate Limiting Options
- `--qps <num>`: Limit queries per second
- `--start-qps <num>`: Starting QPS for dynamic rate
- `--end-qps <num>`: Target QPS for dynamic rate
- `--qps-change-interval <seconds>`: Interval for QPS changes
- `--qps-change <num>`: QPS change amount per interval

### Security Options
- `--tls`: Enable TLS connection

### Cluster Options
- `--cluster`: Use cluster client
- `--read-from-replica`: Read from replica nodes

## Output Format

The benchmark tool provides real-time statistics during execution:

```
Progress: 1234 requests, Current RPS: 1234.56, Overall RPS: 1230.45, Errors: 0
Latencies (ms) - Avg: 0.12, p50: 0.11, p99: 0.18
```

Final results include:
- Total execution time
- Total requests completed
- Average requests per second
- Error count
- Latency statistics (min, avg, max, p50, p95, p99)

## Dependencies

This tool requires:
- Go 1.21 or higher
- [github.com/valkey-io/valkey-glide](https://github.com/valkey-io/valkey-glide) - Valkey GLIDE client library

## Examples

### Basic SET Benchmark
```bash
./valkey-benchmark -H localhost -p 6379 -t set -n 100000
```

### GET Benchmark with Rate Limiting
```bash
./valkey-benchmark -H localhost -p 6379 -t get --qps 5000
```

### Cluster Benchmark
```bash
./valkey-benchmark -H localhost -p 6379 --cluster --read-from-replica
```

### High Concurrency Test
```bash
./valkey-benchmark -H localhost -p 6379 -c 200 -n 1000000
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.