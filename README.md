# Wrangler Enhancement: ByteSize and TimeDuration Parsers

## 📌 Overview

This project enhances the [CDAP Wrangler](https://github.com/data-integrations/wrangler) library by adding **native support** for parsing and aggregating:

- **Byte Size** units (e.g., `10KB`, `1.5MB`, `2GB`)
- **Time Duration** units (e.g., `300ms`, `1.5s`, `1h`)

A new directive `aggregate-stats` has been introduced to demonstrate this functionality and allow for easy aggregation of these units within recipes.

---

## 🚀 Features

### ✅ New Token Types
- `BYTE_SIZE` — Supports units like B, KB, MB, GB, TB
- `TIME_DURATION` — Supports units like ms, s, min, h

### ✅ New Classes
- `ByteSize.java` — Parses strings like `"10KB"` and provides size in bytes.
- `TimeDuration.java` — Parses strings like `"1.5s"` and provides duration in nanoseconds.

### ✅ New Directive: `aggregate-stats`

Performs aggregation over a dataset using byte size and time duration values.

#### **Syntax:**
```plaintext
aggregate-stats :<source_byte_column> :<source_time_column> <target_size_column> <target_time_column> [<output_unit_size>] [<output_unit_time>] [<aggregation_type>]
