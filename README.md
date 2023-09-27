
https://usa.visa.com/careers/job-details.jobid.743999772263330.deptid.2641535.html
https://usa.visa.com/careers/job-details.jobid.743999740858315.deptid.1146589.html

https://www.jb51.net/books/685395.html
from pyspark.sql import functions as F

grouped_df = (filtered_df.groupBy("asofdate")
              .agg(F.count("xrefid").alias("xrefid_count"),
                   F.countDistinct("xrefid").alias("distinct_xrefid_count")))

difference_df = grouped_df.withColumn("difference", 
                                      grouped_df["xrefid_count"] - grouped_df["distinct_xrefid_count"])