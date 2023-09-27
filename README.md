
https://usa.visa.com/careers/job-details.jobid.743999772263330.deptid.2641535.html
https://usa.visa.com/careers/job-details.jobid.743999740858315.deptid.1146589.html

https://www.jb51.net/books/685395.html
from pyspark.sql import functions as F

grouped_df = (filtered_df.groupBy("asofdate")
              .agg(F.count("xrefid").alias("xrefid_count"),
                   F.countDistinct("xrefid").alias("distinct_xrefid_count")))

difference_df = grouped_df.withColumn("difference", 
                                      grouped_df["xrefid_count"] - grouped_df["distinct_xrefid_count"])


spark.conf.set("spark.sql.repl.eagerEval.enabled", True) # Enables the display of DataFrames in a readable format
spark.conf.set("spark.sql.repl.eagerEval.truncate", 0)  # Disables truncation of the content
spark.conf.set("spark.sql.repl.eagerEval.maxNumRows", -1) # Display all rows without a limit