
https://usa.visa.com/careers/job-details.jobid.743999772263330.deptid.2641535.html
https://usa.visa.com/careers/job-details.jobid.743999740858315.deptid.1146589.html

https://www.jb51.net/books/685395.html
from pyspark.sql import functions as F

grouped_df = (filtered_df.groupBy("asofdate")
              .agg(F.count("xrefid").alias("xrefid_count"),
                   F.countDistinct("xrefid").alias("distinct_xrefid_count")))

difference_df = grouped_df.withColumn("difference", 
                                      grouped_df["xrefid_count"] - grouped_df["distinct_xrefid_count"])
from pyspark.sql import functions as F

# Group by 'process_date' and aggregate by count of 'cust_ref_id' for each table
doom_grouped = doom.groupBy("process_date").agg(F.count("cust_ref_id").alias("doom_count"))
dumas_grouped = dumas.groupBy("process_date").agg(F.count("cust_ref_id").alias("dumas_count"))

# Left join dumas with doom on 'process_date' to compare counts
comparison_df = dumas_grouped.join(doom_grouped, on="process_date", how="left").fillna(0)

# Add a comparison column
comparison_df = comparison_df.withColumn("difference", F.col("dumas_count") - F.col("doom_count"))

# Show the comparison
comparison_df.show()

# If you only want to see dates where the counts are different:
# comparison_df.filter(comparison_df.difference != 0).show()
