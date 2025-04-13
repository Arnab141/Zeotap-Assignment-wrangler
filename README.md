# 📊 CDAP Wrangler - Custom Directive: `aggregate-stats`

## 🧩 Overview

This project extends the [CDAP Wrangler](https://github.com/data-integrations/wrangler) library by implementing a new custom directive called **`aggregate-stats`**, which introduces native support for:

- **Byte size parsing** (e.g., `10KB`, `5MB`, `2GB`)
- **Time duration parsing** (e.g., `500ms`, `1.2s`, `5min`, `1h`)

The directive aggregates these values across rows and outputs a **single summary row** containing total or average values in **MB** and **seconds** respectively.

> 🔗 GitHub Repository: [https://github.com/Arnab141/Zeotap-Assignment-wrangler](https://github.com/Arnab141/Zeotap-Assignment-wrangler)

---

## 🛠️ 1. Grammar Changes

- **Modified File**: `Directives.g4`
- **New Lexer Tokens**:
  - `BYTE_SIZE` – e.g., `10KB`, `1.5MB`
  - `TIME_DURATION` – e.g., `500ms`, `2s`
- **Helper Fragments**:
  - `BYTE_UNIT`, `TIME_UNIT`
- **Updated Rules**:
  - Modified `value` rule to support the new token types
- **Build**:
  - Regenerated ANTLR grammar using:  
    ```bash
    mvn compile
    ```

---

## 📦 2. API Changes (wrangler-api module)

- **New Token Classes**:
  - `ByteSize.java`
    - Parses strings like `10KB`, `1.5MB`, etc.
    - Converts to canonical form in **bytes**
  - `TimeDuration.java`
    - Parses strings like `300ms`, `2s`, etc.
    - Converts to canonical form in **nanoseconds**
- **Token Modifications**:
  - Added new `TokenType` entries: `BYTE_SIZE`, `TIME_DURATION`
  - Extended `Token.java` as needed to support parsing logic

---

## ⚙️ 3. Core Parser Updates (wrangler-core module)

- **Visitor Updates**:
  - Modified `RecipeVisitor.java`
    - Added support for `visitNumber`, `visitText`, `visitByteSizeArg`, and `visitTimeDurationArg`
    - Parsed these into `ByteSize` and `TimeDuration` token instances
- **TokenGroup**:
  - ByteSize and TimeDuration tokens added to the token group during parsing

---

## 📏 4. New Directive: `aggregate-stats`

- **File**: `AggregateStats.java`
- **Directive Usage**:
  ```plaintext
  aggregate-stats :<byte_column> :<time_column> <target_size_column> <target_time_column> [unit_size] [unit_time] [aggregation_type]
