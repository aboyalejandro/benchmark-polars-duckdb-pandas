# 🔎 File Processing Benchmark

This project provides a comprehensive benchmark for comparing the performance of different file formats (CSV, Parquet, and Arrow) and data processing libraries (Polars, DuckDB, and Pandas) in Python.

## 📝 Introduction

The project consists of three main Python scripts:

- `generate_data.py`: Generates fake transaction data.
- `export_data.py`: Exports the generated data to CSV, Parquet, and Arrow formats.
- `benchmark.py`: Performs the benchmark tests on the exported files.

## 👨🏻‍💻 Prerequisites

- Docker Desktop

## 🔨 Usage

1. Build the Docker image:

    ```sh
    docker build -t file-reading-benchmark .
    ```

2. You can customize the number of records generated by setting the `NUM_RECORDS` environment variable:

    ```sh
    docker run -e NUM_RECORDS=500000 -it file-reading-benchmark
    ```

This example will generate and benchmark 500.000 records instead of the default 10.000. Be patient if going above 100.000 rows since it will take time to generate the files.

This command will:
1. Generate a fake transaction dataset with foreign key relationships to user/product datasets.
2. Export the data to CSV, Parquet, and Arrow formats.
3. Run the benchmark tests on each file format using Polars, DuckDB, and Pandas.

You can also check output screenshots in the repo or view yours in the terminal output.

## 📊 Results:

| Rows | Tool | CSV (secs) | Parquet (secs) | Arrow (secs) |
|----------------|------|----------|--------------|------------|
| 50000 | Polars | 0.0080 | 0.0072 | 0.0038 |
| 100000 | Polars | 0.0111 | 0.0126 | 0.0073 |
| 500000 | Polars | 0.0416 | 0.0566 | 0.0407 |
| 1000000 | Polars | 0.1850 | 0.1477 | 0.1013 |
| 2000000 | Polars | 0.7114 | 0.4499 | 0.5114 |
| 50000 | DuckDB | 0.0723 | 0.0147 | 0.0183 |
| 100000 | DuckDB | 0.0701 | 0.0149 | 0.0196 |
| 500000 | DuckDB | 0.1402 | 0.0213 | 0.0774 |
| 1000000 | DuckDB | 0.1224 | 0.0246 | 0.1338 |
| 2000000 | DuckDB | 0.1603 | 0.0199 | 0.5840 |
| 50000 | Pandas | 0.1609 | 0.0377 | 0.0297 |
| 100000 | Pandas | 0.2601 | 0.0713 | 0.0520 |
| 500000 | Pandas | 1.6821 | 0.7335 | 1.3132 |
| 1000000 | Pandas | 3.3145 | 1.5929 | 1.2287 |
| 2000000 | Pandas | 7.6832 | 4.4177 | 4.8564 |

### 🧪 Some conclusions:

- **Tool comparison**:

    - Polars is consistently fast across all dataset sizes, especially for smaller datasets.
    - DuckDB shows excellent performance, particularly with Parquet files.
    - Pandas is generally slower than both Polars and DuckDB, especially for larger datasets.

- **File format efficiency**:
  
    - Parquet format is usually the fastest to read for all tools, especially for larger datasets.
    - CSV is typically the slowest format, particularly for Pandas with large datasets.
    - Arrow format shows mixed results, sometimes outperforming CSV but rarely beating Parquet.

- **Use case considerations**:

    - For applications requiring fast processing of large datasets, DuckDB with Parquet files seems optimal.
    - For smaller datasets or when using CSV files, Polars might be the best choice.
    - Pandas, while popular, may not be the best choice for performance-critical applications with large datasets.

### 😎 [Follow me on Linkedin](https://www.linkedin.com/in/alejandro-aboy/)
- Get tips, learnings and tricks for your Data career!

### 📩 [Subscribe to The Pipe & The Line](https://thepipeandtheline.substack.com/?utm_source=github&utm_medium=referral)
- Join the Substack newsletter to get similar content to this one and more to improve your Data career!
