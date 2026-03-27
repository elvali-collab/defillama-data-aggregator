# 🚀 DefiLlama Data Aggregator

> **Version**: 1.0.3
> **Update Date**: 2026-03-27
> **Description**: Professional DefiLlama data aggregator with security validation and bug fixes - DeFi TVL, protocols, chains, and yields data

---

## 📊 Overview

DefiLlama Data Aggregator is a professional-grade command-line tool that provides unified access to DefiLlama's comprehensive DeFi data. It supports querying Total Value Locked (TVL), protocol data, chain statistics, and yield pool information with built-in security validation and error handling.

---

## 🎯 Features

- ✅ **DeFi TVL** - Total DeFi TVL and chain-level TVL
- ✅ **Protocol Data** - Protocol details, listings, and rankings
- ✅ **Chain Data** - Individual chain TVL and statistics
- ✅ **Yield Pools** - Yield rate queries and filtering
- ✅ **Health Monitoring** - API health status monitoring
- ✅ **Security Validation** - Input sanitization and error handling
- ✅ **Flexible Output** - Pretty/Table/JSON/CSV formats

---

## 📦 Installation

### Prerequisites

- Node.js >= 16.0.0
- npm (comes with Node.js)

### Install Dependencies

```bash
cd /workspace/projects/workspace/skills/defillama-data-aggregator
npm install
```

### Create Symbolic Link (Optional)

```bash
npm link
```

This creates a global `defillama-data` command that you can use from anywhere.

---

## 🚀 Quick Start

### Basic Usage

```bash
# View version
defillama-data --version

# Get total DeFi TVL
defillama-data defillama tvl

# Get protocol TVL
defillama-data defillama protocol -n aave

# Get protocol rankings
defillama-data defillama protocols --limit 10 --sort tvl -f table

# Find high-yield pools
defillama-data defillama yields --min-apy 10 --limit 20 -f table

# Check API health
defillama-data health

# View system status
defillama-data status
```

---

## 📖 Commands

### 1. Get Total DeFi TVL

Get the total value locked across all DeFi protocols.

```bash
defillama-data defillama tvl [options]
```

**Options**:
- `-f, --format <type>`: Output format (json, table, csv, pretty) - Default: pretty

**Example**:
```bash
defillama-data defillama tvl
defillama-data defillama tvl -f json | jq '.totalTvl'
```

**Response**:
```json
{
  "totalTvl": 94518602394.26,
  "chains": [...],
  "timestamp": "2026-03-27T09:00:00.000Z"
}
```

---

### 2. Get Protocol TVL

Get TVL for a specific protocol.

```bash
defillama-data defillama protocol -n <name> [options]
```

**Required Options**:
- `-n, --name <name>`: Protocol name (e.g., aave, uniswap, compound)

**Options**:
- `-f, --format <type>`: Output format (json, table, csv, pretty) - Default: pretty

**Example**:
```bash
defillama-data defillama protocol -n aave
defillama-data defillama protocol -n uniswap -f json
```

**Validation Rules**:
- Only alphanumeric characters and hyphens allowed
- Length: 1-50 characters
- Automatically converted to lowercase

**Valid Examples**: `aave`, `uniswap-v3`, `compound-protocol`
**Invalid Examples**: `aave<script>`, `uni/swap`, `aave&x`

---

### 3. Get All Protocols

Get a list of all protocols with filtering and sorting.

```bash
defillama-data defillama protocols [options]
```

**Options**:
- `-c, --category <name>`: Filter by category (e.g., lending, dex)
- `--min-tvl <amount>`: Minimum TVL in USD
- `--limit <number>`: Limit results (1-500)
- `--sort <field>`: Sort by field (tvl) - Default: tvl
- `-f, --format <type>`: Output format (json, table, csv, pretty) - Default: pretty

**Example**:
```bash
# Get all protocols
defillama-data defillama protocols

# Sort by TVL, top 20
defillama-data defillama protocols --sort tvl --limit 20

# Filter lending protocols
defillama-data defillama protocols -c lending --min-tvl 100000000

# Combined filters
defillama-data defillama protocols -c lending --min-tvl 100000000 --limit 50 --sort tvl -f table
```

---

### 4. Get Chain TVL

Get TVL for a specific blockchain.

```bash
defillama-data defillama chain -n <name> [options]
```

**Required Options**:
- `-n, --name <name>`: Chain name (e.g., ethereum, solana, polygon)

**Options**:
- `-f, --format <type>`: Output format (json, table, csv, pretty) - Default: pretty

**Example**:
```bash
defillama-data defillama chain -n ethereum
defillama-data defillama chain -n solana -f json
```

---

### 5. Get Yield Pools

Get yield pool information with filtering.

```bash
defillama-data defillama yields [options]
```

**Options**:
- `--min-apy <number>`: Minimum APY percentage (0-1000)
- `--min-tvl <number>`: Minimum TVL in USD
- `--chain <name>`: Filter by chain name (e.g., ethereum, arbitrum)
- `--stablecoin`: Filter stablecoin pools only
- `--limit <number>`: Limit results (1-500)
- `-f, --format <type>`: Output format (json, table, csv, pretty) - Default: pretty

**Example**:
```bash
# Get all yield pools
defillama-data defillama yields

# High APY pools (APY > 10%)
defillama-data defillama yields --min-apy 10

# Ethereum high-yield pools
defillama-data defillama yields --chain ethereum --min-apy 5

# Combined filters
defillama-data defillama yields --min-apy 10 --chain ethereum --min-tvl 1000000 --limit 20 -f table
```

---

### 6. Health Check

Check API health status.

```bash
defillama-data health [options]
```

**Options**:
- `-q, --quiet`: Quiet mode (summary only)
- `--timeout <ms>`: Request timeout in milliseconds - Default: 5000

**Example**:
```bash
# Full health check
defillama-data health

# Quiet mode
defillama-data health --quiet

# Custom timeout
defillama-data health --timeout 10000
```

---

### 7. System Status

Display system status and available platforms.

```bash
defillama-data status
```

**Example**:
```bash
defillama-data status
```

---

## 📤 Output Formats

All commands support multiple output formats:

### Pretty (Default)

Human-readable format with colored output.

```bash
defillama-data defillama tvl -f pretty
```

### Table

Structured table format for data comparison.

```bash
defillama-data defillama protocols --limit 10 -f table
```

### JSON

Machine-readable format for scripts and automation.

```bash
defillama-data defillama tvl -f json | jq '.totalTvl'
```

### CSV

Spreadsheet-friendly format for data export and analysis.

```bash
defillama-data defillama protocols --limit 50 -f csv > protocols.csv
```

---

## 🔒 Security Features

### Input Validation

All user inputs are validated and sanitized:

| Input Type | Validation Rules | Length Limit |
|-----------|-----------------|--------------|
| Protocol Name | Alphanumeric + hyphens only | 1-50 characters |
| Chain Name | Alphanumeric + spaces + hyphens | 1-50 characters |
| Category Name | Alphanumeric + spaces + hyphens | 1-50 characters |
| Limit | 1-500 | - |
| Min APY | 0-1000% | - |
| Min TVL | ≥ 0 | - |

### Error Handling

- API errors (4xx, 5xx) with status codes
- Network errors (timeout, connection refused)
- Validation errors with helpful messages
- Sanitized error messages to prevent information leakage

---

## 🛠️ Configuration

### Setup Configuration File (Optional)

```bash
# Copy example configuration
cp config/keys.example.js config/keys.js
```

### Configuration Example

```javascript
// config/keys.js
module.exports = {
  defillama: {
    baseUrl: 'https://api.llama.fi'
  },
  settings: {
    defaultCacheDuration: 300,  // Cache duration in seconds
    timeout: 30000,             // Request timeout in milliseconds
    maxRetries: 3,              // Maximum retry attempts
    retryDelay: 1000,           // Retry delay in milliseconds
    debug: process.env.DEBUG === 'true'  // Enable debug logging
  }
};
```

---

## 💡 Usage Examples

### Monitor Lending Protocols

```bash
# Get top 10 lending protocols by TVL
defillama-data defillama protocols -c lending --limit 10 --sort tvl -f table
```

### Find High-Yield Pools

```bash
# Find high-yield pools on Ethereum with APY > 10%
defillama-data defillama yields --chain ethereum --min-apy 10 --min-tvl 1000000 --limit 20 -f table
```

### Compare Chain TVL

```bash
# Compare TVL across multiple chains
for chain in ethereum solana polygon arbitrum avalanche; do
  echo "=== $chain ==="
  defillama-data defillama chain -n $chain -f json | jq '.tvl'
done
```

### Export Data for Analysis

```bash
# Export protocols to CSV
defillama-data defillama protocols --limit 100 -f csv > protocols.csv

# Export yields to CSV
defillama-data defillama yields --limit 100 -f csv > yields.csv
```
---

## 📚 Documentation

| Document | Description |
|----------|-------------|
| README.md | User manual (this file) |
| SKILL.md | Skill technical documentation |
| QUICK_REFERENCE.md | Quick reference card |
| FULL_FEATURE_LIST.md | Complete feature list |
| DEPLOYMENT_CHECKLIST.md | Deployment checklist |
| LAUNCH_REPORT.md | Launch report |

---

## 📄 License

MIT License - Copyright (c) 2026 Antalpha

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

## 🌐 API Documentation

For detailed DefiLlama API documentation:
- https://docs.llama.fi/

- Maintainer: Antalpha AI Team
