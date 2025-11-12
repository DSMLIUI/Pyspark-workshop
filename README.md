# 🚀 Workshop: PySpark Production Mastery

**Theme**: From Fundamentals to Production Optimization  
**Core Stack**: PySpark, Performance Optimization, Structured Streaming  
**Target Platform**: Databricks Free Edition (or 14-Day Trial)

---

## 🎯 Workshop Overview

A hands-on workshop designed to teach essential PySpark skills from fundamentals to production optimization. Participants will learn distributed data processing, performance optimization techniques, and production-ready patterns using real-world datasets (TPC-H and TPC-DS).

**Target Audience**: Data engineers, data analysts, and developers working with Apache Spark  
**Prerequisites**: Basic Python knowledge, SQL familiarity (optional but helpful)  
**Platform**: Databricks Free Edition (completely free!)

---

## 📚 What You'll Learn

### Core Topics
- ✅ Spark fundamentals and lazy evaluation
- ✅ DataFrame operations (filter, join, groupBy, aggregations)
- ✅ Data engineering patterns (cleaning, joining, saving)
- ✅ Intermediate patterns (window functions, caching, partitioning)
- ✅ Production optimization (shuffles, skew, broadcast joins, AQE)
- ✅ Streaming optimization (checkpoints, watermarks, output modes)
- ✅ Advanced PySpark patterns for production

### Skills You'll Gain
- Process large datasets efficiently
- Diagnose and fix performance bottlenecks
- Optimize Spark jobs using Spark UI
- Apply production-ready patterns
- Build reliable streaming pipelines
- Master advanced PySpark techniques

---

## 📁 Repository Structure

```
PySpark-Workshop/
├── README.md                              # This file
├── WORKSHOP_GUIDE.md                      # Complete workshop guide
├── DATABRICKS_FREE_EDITION_GUIDE.md       # Concise Databricks guide
├── PYSPARK_CHEATSHEET.md                  # Quick reference guide
│
├── Part1_PySpark_Speedrun.ipynb           # Part 1: The PySpark Speedrun (20 min)
├── Part2_Data_Engineer_Toolkit.ipynb      # Part 2: Data Engineer Toolkit (35 min)
├── Part3_Intermediate_Patterns.ipynb      # Part 3: Intermediate Patterns (40 min)
├── Part4_Batch_Processing_Optimization.ipynb  # Part 4: Batch Optimization (20 min)
│
└── BONUS/
    ├── Part6_Stream_Optimization_BONUS.ipynb   # Bonus: Streaming Optimization (20 min)
    └── Part7_Advanced_Pyspark_BONUS.ipynb      # Bonus: Advanced PySpark (40 min)
```

---

## 🚀 Quick Start

### For Workshop Participants

#### Step 1: Sign Up for Databricks
1. Go to [databricks.com/try-databricks](https://www.databricks.com/try-databricks)
2. Create a free account (no credit card required!)
3. Verify your email address

#### Step 2: Create Your Cluster
1. Navigate to **Compute** → **Create Cluster**
2. Name: "workshop-cluster"
3. Runtime: Latest LTS ML version (e.g., 14.3 LTS ML)
4. Click **Create** (takes 3-5 minutes to start)

#### Step 3: Import Workshop Notebooks
1. Download the core workshop notebooks from this repository:
   - `Part1_PySpark_Speedrun.ipynb` - Spark fundamentals
   - `Part2_Data_Engineer_Toolkit.ipynb` - Data engineering patterns
   - `Part3_Intermediate_Patterns.ipynb` - Advanced patterns
   - `Part4_Batch_Processing_Optimization.ipynb` - Production optimization
   
   **Optional Bonus Notebooks** (for advanced learners):
   - `Part6_Stream_Optimization_BONUS.ipynb` - Streaming production issues
   - `Part7_Advanced_Pyspark_BONUS.ipynb` - Comprehensive advanced patterns

2. In Databricks: **Workspace** → Your User Folder → **Import**
3. Upload each `.ipynb` file
4. Attach to your cluster (dropdown at top of notebook)

#### Step 4: Access Datasets
- **No data download required!** The notebooks use built-in datasets in Databricks
- **TPC-H dataset** (Parts 1-3): Pre-loaded at `samples.tpch.*` tables
  - Includes: `orders`, `customer`, `lineitem`, `nation`
- **TPC-DS dataset** (Part 4): Pre-loaded at `samples.tpcds_sf1.*` tables
  - Includes: `store_sales`, `customer`, `item`, `date_dim`
- Simply run the notebooks - the data is already available!

**Full setup instructions**: See [WORKSHOP_GUIDE.md](WORKSHOP_GUIDE.md)

---

## 📖 Workshop Agenda

### Part 1: The PySpark Speedrun (20 Minutes)
**Objective**: Get everyone writing code and understanding Spark's core "lazy" concept within minutes.

- **Module 1.1**: First Load (10 mins) - Load and explore data
- **Module 1.2**: Core API (10 mins) - Essential DataFrame operations

**Key Concepts**: DataFrame, Transformations (Lazy), Actions (Eager)

### Part 2: The Data Engineer's Toolkit (35 Minutes)
**Objective**: Master the true 80/20 of data engineering: shaping, joining, and aggregating data.

- **Module 2.1**: Aggregating (10 mins) - Group by order status and calculate order statistics
- **Module 2.2**: Joining (15 mins) - Combine customer data with orders (left vs inner join)
- **Module 2.3**: Cleaning & Saving (10 mins) - Handle nulls and save to Delta Lake

### Part 3: Intermediate Patterns (40 Minutes)
**Objective**: Master essential patterns that appear in 80% of production PySpark jobs.

- **Module 3.1**: Window Functions (15 mins) - Ranking, running totals, lag/lead
- **Module 3.2**: Caching & Persistence (10 mins) - When and how to cache effectively
- **Module 3.3**: Partitioning Fundamentals (10 mins) - Data layout and partition control
- **Module 3.4**: Query Plans & explain() (5 mins) - Understanding Spark's execution

### Part 4: Batch Processing Optimization (20 Minutes)
**Objective**: Identify, diagnose, and fix the most common Spark performance issues.

- **Issue #1**: Shuffle Explosion & Column Pruning
- **Issue #2**: Broadcast Joins for Small Dimensions
- **Issue #3**: Python UDF Performance Killer
- **Issue #4**: Data Skew - The Silent Killer
- **Issue #5**: Adaptive Query Execution (AQE)

### Bonus Content (Optional)

#### Part 6: Stream Optimization (20 Minutes)
**Objective**: Fix critical Structured Streaming production issues.

- Checkpoint management for fault tolerance
- Watermarks to prevent unbounded state growth
- Choosing the right output mode
- Handling small files in streaming sinks
- Idempotent writes with foreachBatch

#### Part 7: Advanced PySpark (40 Minutes)
**Objective**: Comprehensive advanced patterns for production data engineering.

- Performance optimization (shuffles, partitions, caching)
- Join strategies and AQE
- Schema hygiene and pushdown
- ML pipelines with proper validation
- Streaming with watermarks and checkpointing

### Wrap-Up & Next Steps (10 Minutes)
- Recap what we built
- The path forward (scaling, reliability, production)
- Final Q&A

**Total Time**: ~2.5 hours (core workshop) + 1 hour (bonus content)

---

## 📊 Dataset Description

### TPC-H Dataset (Parts 1-3)

The core notebooks use the TPC-H (Transaction Processing Performance Council - Benchmark H) dataset, which is built into Databricks and simulates a business data warehouse environment.

#### Orders Table
- **o_orderkey**: Unique identifier for each order
- **o_custkey**: Customer key (foreign key to customer table)
- **o_orderstatus**: Order status (O, F, P)
- **o_totalprice**: Total price of the order
- **o_orderdate**: Date of the order
- **o_orderpriority**: Order priority
- **o_clerk**: Clerk who processed the order
- **o_shippriority**: Shipping priority
- **o_comment**: Order comment

#### Customer Table
- **c_custkey**: Unique identifier for each customer
- **c_name**: Customer name
- **c_address**: Customer address
- **c_nationkey**: Nation key (foreign key)
- **c_phone**: Customer phone number
- **c_acctbal**: Customer account balance
- **c_mktsegment**: Market segment (AUTOMOBILE, BUILDING, MACHINERY, HOUSEHOLD, FURNITURE)
- **c_comment**: Customer comment

**Data Characteristics**:
- Pre-loaded in Databricks as `samples.tpch.*` tables
- Optimized Parquet format for fast reads
- Realistic business data patterns
- Perfect for learning joins, aggregations, and intermediate patterns
- No download or upload required - ready to use!

### TPC-DS Dataset (Part 4)

Part 4 uses the TPC-DS (Decision Support) dataset, a more complex benchmark perfect for performance testing and optimization exercises.

**Key Tables**:
- **store_sales**: Large fact table with sales transactions
- **customer**: Customer dimension table
- **item**: Item/product dimension table
- **date_dim**: Date dimension table

**Data Characteristics**:
- Pre-loaded in Databricks as `samples.tpcds_sf1.*` tables
- Scale Factor 1 (~1GB) - perfect for performance demos
- Simulates retail environment with stores, customers, and sales
- Ideal for demonstrating optimization techniques

---

## 🎓 Learning Outcomes

After completing this workshop, you will be able to:

1. **Understand Spark Fundamentals**
   - Explain lazy evaluation and the catalyst optimizer
   - Describe transformations vs actions
   - Use Spark UI for debugging and performance analysis

2. **Process Data at Scale**
   - Load and transform large datasets efficiently
   - Perform complex joins and aggregations
   - Clean data and save to Delta Lake
   - Use window functions for advanced analytics

3. **Optimize Spark Performance**
   - Diagnose performance bottlenecks using Spark UI
   - Fix shuffle explosion with column pruning
   - Use broadcast joins for small dimensions
   - Mitigate data skew with salting techniques
   - Enable and leverage Adaptive Query Execution (AQE)

4. **Master Production Patterns**
   - Apply caching strategies effectively
   - Control partitioning for optimal performance
   - Read and interpret query execution plans
   - Handle complex data types (arrays, structs)

5. **Build Reliable Streaming Pipelines** (Bonus)
   - Configure checkpoints for fault tolerance
   - Use watermarks to prevent unbounded state
   - Choose correct output modes
   - Implement idempotent sinks

---

## 💻 Technical Requirements

### For Participants
- **Laptop** with modern browser (Chrome/Firefox/Safari)
- **Internet connection** (stable, for Databricks)
- **Databricks account** (free - no credit card required!)
- **No local installation required!**

### For Instructors
- Databricks account (free edition works perfectly!)
- No additional setup required - datasets are built into Databricks

---

## 📚 Documentation

### Essential Guides
- **[WORKSHOP_GUIDE.md](WORKSHOP_GUIDE.md)** - Complete workshop guide with agenda, timing, and teaching tips
- **[DATABRICKS_FREE_EDITION_GUIDE.md](DATABRICKS_FREE_EDITION_GUIDE.md)** - Concise guide to Databricks Free Edition
- **[PYSPARK_CHEATSHEET.md](PYSPARK_CHEATSHEET.md)** - Quick reference for common PySpark operations

### Workshop Notebooks

**Core Workshop:**
- **Part1_PySpark_Speedrun.ipynb** - Spark fundamentals (20 min)
- **Part2_Data_Engineer_Toolkit.ipynb** - Data engineering patterns (35 min)
- **Part3_Intermediate_Patterns.ipynb** - Advanced patterns (40 min)
- **Part4_Batch_Processing_Optimization.ipynb** - Production optimization (20 min)

**Bonus Content:**
- **Part6_Stream_Optimization_BONUS.ipynb** - Streaming production issues (20 min)
- **Part7_Advanced_Pyspark_BONUS.ipynb** - Comprehensive advanced patterns (40 min)

---

## 🎯 Databricks Free Edition

This workshop is optimized for **Databricks Free Edition** (completely free!):

✅ **Full PySpark functionality**  
✅ **Single cluster** (15GB RAM, 2 cores)  
✅ **2GB DBFS storage** (we'll use cloud storage for datasets)  
✅ **MLflow tracking** (limited features)  
✅ **Spark UI** for debugging

⚠️ **Limitations**:
- Clusters auto-terminate after 2 hours of inactivity (notebook state is saved)
- No job scheduling (manual execution only)
- Single user (no team collaboration)

**Perfect for**: Learning, prototypes, workshops, personal projects!

See [DATABRICKS_FREE_EDITION_GUIDE.md](DATABRICKS_FREE_EDITION_GUIDE.md) for details.

---

## 🤝 Contributing

This workshop is open source! Contributions welcome:

- **Bug Reports**: Open an issue
- **Improvements**: Submit a pull request
- **New Exercises**: Add to bonus section
- **Translations**: Help make it accessible

---

## 📝 License

This workshop is released under the MIT License. Feel free to use, modify, and distribute for educational purposes.

---

## 📞 Support & Resources

### During Workshop
- Ask questions anytime
- Teaching assistants available
- Refer to workshop guide for timing

### After Workshop
- **GitHub Issues**: For bugs or questions
- **Databricks Community Forums**: [community.databricks.com](https://community.databricks.com/)
- **Databricks Academy**: [academy.databricks.com](https://academy.databricks.com/) - Free courses

### Learning Resources
- 📖 [Apache Spark Documentation](https://spark.apache.org/docs/latest/)
- 📖 [MLflow Documentation](https://mlflow.org/)
- 📖 [Delta Lake Documentation](https://docs.delta.io/)

---

## ⭐ Feedback

Help us improve! After the workshop, please:
1. Complete the feedback survey
2. Star this repository if you found it helpful
3. Share with colleagues who might benefit
4. Suggest topics for future workshops

---

## 🎉 Acknowledgments

- **Apache Spark Community**: For this amazing tool
- **Databricks**: For Free Edition and documentation
- **Workshop Participants**: Your engagement makes this worthwhile!

---

## 🚀 Next Steps

1. ✅ Complete [pre-workshop setup](WORKSHOP_GUIDE.md#pre-workshop-setup)
2. ✅ Review [PySpark cheat sheet](PYSPARK_CHEATSHEET.md)
3. ✅ Read [Databricks guide](DATABRICKS_FREE_EDITION_GUIDE.md)
4. ✅ Bring curiosity and questions!

**See you at the workshop! Let's build something amazing with Spark! ⚡**

---

**Happy Learning! 🎓✨**
