# High-Performance C++ Trading Backtester

A low-latency, event-driven trading backtester engineered with custom memory management and price-time priority order matching. Built to handle massive throughput with sub-microsecond latency.

[![C++20](https://img.shields.io/badge/C%2B%2B-20-blue.svg)](https://en.cppreference.com/w/cpp/20)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 🚀 Performance Metrics (Apple Silicon M1)

- **Throughput:** 34 Million ticks/sec & 7.65 Million orders/sec matching.
- **Latency:** 0.131 µs average per order.
- **Memory Allocation:** 1.69 ns per allocation via custom memory pool (zero allocations in hot path).
- **Execution:** Full backtest of 1M ticks and 200K orders completed in just **57 milliseconds**.

## 🧠 Technical Highlights

- **Hardware Symbiosis:** All core structures (`Order`, `Tick`, `Trade`) are perfectly cache-aligned to 64 bytes to eliminate false sharing and optimize CPU cache utilization.
- **Zero-Copy Design:** Events are passed by const reference; objects are allocated in pre-allocated custom memory pools, avoiding `malloc`/`new` overhead entirely.
- **Deterministic Math:** Utilizes fixed-point `int64_t` arithmetic instead of floating-point to ensure consistent, speedy calculations and eliminate rounding errors.
- **SIMD Optimization:** Code is auto-vectorized capitalizing on modern CPU extensions like ARM NEON and Intel AVX2.
- **Event-Driven Architecture:** Highly modular design supporting pluggable custom algorithms ranging from momentum strategies to high-frequency market-making logic.

## 🏗 System Architecture

1. **Tick Engine:** The central event loop that ingests data, updates order books, and pushes events to strategies.
2. **Order Book:** A deterministic matching engine implementing realistic Price-Time Priority (FIFO), using high-speed tree structures for bid/ask queues.
3. **Memory Pool:** Pre-allocates massive blocks of memory at startup to offer near-instantaneous `placement new` allocations.
4. **Strategies Layer:** Provides an Object-Oriented interface for evaluating custom logic (`on_tick`, `on_trade`).

## 💻 Quick Start

### Build Instructions
```bash
cmake -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build -j
```

### Run Tests and Benchmarks
```bash
./build/backtester              # Run with synthetic data
./build/backtester data.csv     # Run with your own historical tick data
./build/benchmark               # Execute latency & throughput benchmarks
make test                       # Run all unit tests
```

## 🛠 Project Structure
```
├── include/          # Headers (types, order_book, tick_engine, memory_pool)
├── src/              # Core implementation and automated testing suite
├── strategies/       # Base strategy interface and sample algorithms (Momentum, Market Maker)
└── data/             # Sample historical tick data (CSV format)
```

## 📄 Documentation

For a deep dive into the system design, data flow, complexity analysis, and optimization techniques, please refer to the [Architecture Details](ARCHITECTURE.md).

## 👨‍💻 Author

Built to demonstrate advanced proficiency in low-latency systems programming, C++20 features, memory management, and quantitative trading infrastructure.
