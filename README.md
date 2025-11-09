# 🚀 Workshop: The 2-Hour PySpark Pipeline

**Theme**: From Batch ML to Real-Time Order Value Prediction  
**Core Stack**: PySpark, MLlib (Pipelines), MLflow, & Structured Streaming  
**Target Platform**: Databricks Free Edition (or 14-Day Trial)

---

## 🎯 Workshop Overview

A hands-on 2-hour workshop designed to teach essential PySpark skills through building a real-world analytics system using the TPC-H dataset. Participants will learn distributed data processing, machine learning with MLlib, and structured streaming.

**Target Audience**: Data analysts, data engineers, and developers new to Apache Spark  
**Prerequisites**: Basic Python knowledge, SQL familiarity (optional but helpful)  
**Platform**: Databricks Free Edition (completely free!)

---

## 📚 What You'll Learn

### Core Topics
- ✅ Spark fundamentals and lazy evaluation
- ✅ DataFrame operations (filter, join, groupBy, aggregations)
- ✅ Data engineering patterns (cleaning, joining, saving)
- ✅ End-to-end machine learning pipeline with MLlib
- ✅ MLflow for experiment tracking
- ✅ Real-time streaming with Structured Streaming

### Skills You'll Gain
- Process large datasets efficiently
- Build predictive models at scale
- Create streaming data pipelines
- Track ML experiments automatically
- Apply production-ready patterns

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
├── Part3_ML_Capstone_Pipeline.ipynb       # Part 3: ML Capstone Pipeline (40 min)
└── Part4_Real_Time_Prediction.ipynb       # Part 4: Real-Time Prediction (15 min)
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
1. Download all 4 notebooks from this repository:
   - `Part1_PySpark_Speedrun.ipynb`
   - `Part2_Data_Engineer_Toolkit.ipynb`
   - `Part3_ML_Capstone_Pipeline.ipynb`
   - `Part4_Real_Time_Prediction.ipynb`
2. In Databricks: **Workspace** → Your User Folder → **Import**
3. Upload each `.ipynb` file
4. Attach to your cluster (dropdown at top of notebook)

#### Step 4: Access Datasets
- **No data download required!** The notebooks use the built-in TPC-H dataset in Databricks
- The TPC-H dataset is pre-loaded at `/databricks-datasets/tpch/data-001/`
- Datasets include: `orders.parquet` and `customer.parquet`
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

### Part 3: The ML Capstone Pipeline (40 Minutes)
**Objective**: Build, train, and track a complete, production-style ML pipeline using MLlib and MLflow.

- **Module 3.1**: Feature Engineering Pipeline (15 mins) - Extract time features, StringIndexer, VectorAssembler
- **Module 3.2**: Model Training & MLflow (15 mins) - Train RandomForest to predict order value and track with MLflow
- **Module 3.3**: Save & Load (10 mins) - Load model from MLflow and apply to new data

### Part 4: Real-Time Prediction (15 Minutes)
**Objective**: Use our saved batch model to score a live simulated stream.

- **Module 4.1**: The "Live Order" Simulator (10 mins) - Create streaming data with realistic rate (1 order/second)
- **Module 4.2**: Apply Model & Display Live (5 mins) - See live order value predictions updating in real-time

### Part 5: Wrap-Up & Next Steps (10 Minutes)
- Recap what we built
- The path forward (scaling, reliability, production)
- Final Q&A

**Total Time**: 2 hours (with buffer time)

---

## 📊 Dataset Description

### TPC-H Dataset

The notebooks use the TPC-H (Transaction Processing Performance Council - Benchmark H) dataset, which is built into Databricks and simulates a business data warehouse environment.

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
- Pre-loaded in Databricks at `/databricks-datasets/tpch/data-001/`
- Optimized Parquet format for fast reads
- Realistic business data patterns
- Perfect for learning joins, aggregations, and ML pipelines
- No download or upload required - ready to use!

---

## 🎓 Learning Outcomes

After completing this workshop, you will be able to:

1. **Understand Spark Fundamentals**
   - Explain lazy evaluation and the catalyst optimizer
   - Describe transformations vs actions
   - Use Spark UI for debugging

2. **Process Data at Scale**
   - Load and transform large datasets efficiently
   - Perform complex joins and aggregations
   - Clean data and save to Delta Lake

3. **Build ML Pipelines**
   - Engineer features from raw data
   - Train and evaluate ML models with MLlib
   - Create reusable ML pipelines
   - Track experiments with MLflow

4. **Implement Streaming Solutions**
   - Process unbounded data streams using rate source
   - Apply ML models to streaming data
   - See live predictions in real-time

5. **Apply Production Patterns**
   - Write clean, maintainable Spark code
   - Use Delta Lake for reliability
   - Follow industry best practices

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
- **Part1_PySpark_Speedrun.ipynb** - Spark fundamentals (20 min)
- **Part2_Data_Engineer_Toolkit.ipynb** - Data engineering patterns (35 min)
- **Part3_ML_Capstone_Pipeline.ipynb** - ML pipeline with MLflow (40 min)
- **Part4_Real_Time_Prediction.ipynb** - Real-time streaming (15 min)

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
