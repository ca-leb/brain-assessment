# Take-home Assignment

## Getting Started

### Dependencies

* Jupyter Notebook

### Installing

* Download main.ipynb, and data files (restaurant_data.json and Country-Code.xlsx) into the same working directory.

### Executing program (local)

* Open Jupyter Notebook
```
jupyter notebook
```
* Navigate to working directory with source files and run main.ipynb

## Deployment 

I would deploy this in the cloud with AWS S3 and AWS Lambda, a fully managed service that runs code without provisioning or managing servers. It would automate the generation of CSV data files on the cloud, instead of locally (Jupyter Notebook).

Firstly, I would create and configure a new AWS Lambda function, using the Python script from the `main.ipynb` file, that processes the data and generates the CSV data files. I would also configure the function input and output by specifying the input and output format for your Lambda function. For example, the input could be a message containing any necessary parameters or settings for the function, and the output could be a response indicating whether the function completed successfully and the filenames of the generated CSV files. 

Next, I would create and configure the S3 buckets. The new S3 buckets will be used to store the input data files, and the generated CSV data files respectively. The input data files would then be uploaded to the S3 bucket using the AWS Management Console or the AWS CLI. 

Finally, the Lambda function can be triggered using an event trigger, such as when a new data file is uploaded to the S3 bucket. The Lambda function will then generate the CSV data files based on the Python script and save them to the S3 bucket.

## Architecture Diagram

![alt text](https://i.ibb.co/JtpJd75/Untitled-drawio.png)

In this architecture, the source data files are uploaded to an S3 bucket, and the AWS Lambda function is triggered by an event, such as an object uploaded to the Source S3 bucket. The Lambda function generates the CSV data files based on your Python script and saves them to the Destination S3 bucket. The entire process can be monitored using the AWS Management Console.

## Decisions and Considerations

One consideration that was taken into account is to create two separate S3 buckets for source and destination files. This is to avoid the situation where the bucket triggers a function each time an object is uploaded, and the function uploads an object to the bucket, then the function would indirectly triggers itself, resulting in the function running in a loop.

Furthermore, I chose to use AWS Cloud services due to the following factors:

- Simplicity: As AWS is managed, the solution would be simple as there is no need to start up underlying servers, and code can be automatically run.

- Cost: AWS Lambda only works when an event occurs, hence pay only for the compute time you consume. Additionally, The Lambda Free Tier includes 400,000 GB-seconds of compute time every month.

- Scale: As it is managed, AWS scales as needed to handle the incoming request. 

Another approach is using Amazon Managed Workflows for Apache Airflow (MWAA), a managed orchestration service for Apache Airflow that makes it easier to set up and operate end-to-end data pipelines in the cloud at scale. However, it would be more expensive and not necessary for the scale of this project.

