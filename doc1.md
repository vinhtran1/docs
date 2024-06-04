
# Step: Prepare S3 paths

1. Create bucket name: 
2. Create folders:
    1. s3:// /scripts/glue
    2. s3:// /scripts/cloudformation
    3. s3:// /scripts/conf
    4. s3:// /scripts/archived
    5. s3:// /scripts/logs
    6. s3:// /scripts/temp
    7. s3:// /data/stage
    8. s3:// /data/silver

# Step: Upload scripts to S3

1. Upload file .yaml to path s3:// /scripts/cloudformation
2. Upload file .py to path s3:// /scripts/glue

# Step: Use CloudFormation to create resources

There are resources will be created by CloudFormation

1. Secret Manager: to store PostgreSQL credential
2. Glue Database: to organize metadata tables in AWS Glue
3. Glue Connection: To connect to data stores
4. Glue Crawler: Use Glue Connection to get the metadata of tables and store in Glue Database
5. Glue Job: Python scripts to ETL data

Access CloudFormation → Create Stack → With new resources (standard)

Choose an existing template → Amazon S3 URL → Paste the URL: https:// scripts/cloudformation/.yaml → Next

Fill the info:

1. RoleName: role name created for K2 deployment
2. SecretManagerName: Any name, default is <>
3. DBSubnetId: The Subnet of PostgreSQL database
4. ConnectionSubnetId: The Subnet for Glue Connection
5. DBSecurityGroupIdList: The security group of PostgreSQL. If there are more than 1 security group, use comma to separate them
6. S3Bucket: Default is <>
7. DBHost: Host string of PostgreSQL database. Default is: 
8. DBPort: Port number of PostgreSQL database. Default is:
9. DBUsername: User name of PostgreSQL database. Default is:
10. DBPassword: Password of PostgreSQL database
11. Database: Database name of PostgreSQL database. Default is:
12. DefaultRegion: region of AWS used by default. Default value is ap-southeast-1

Choose Next → Choose Acknowledge

# Step: Run Glue Crawler

To get metadata, access Glue → Data Catalog → Crawlers

Choose crawler <> → Run
