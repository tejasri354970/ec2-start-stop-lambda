import boto3
from datetime import datetime, timezone, timedelta

# AWS credentials and region
REGION_NAME = 'ap-south-1'

# EC2 instances to start and stop
INSTANCE_IDS = ['i-07c8e920108ec4971', 'i-07cd4fe25fec59d43']

def start_instances(instance_ids):
    ec2 = boto3.client('ec2', region_name=REGION_NAME)
    ec2.start_instances(InstanceIds=instance_ids)
    print("Starting instances:", instance_ids)

def stop_instances(instance_ids):
    ec2 = boto3.client('ec2', region_name=REGION_NAME)
    ec2.stop_instances(InstanceIds=instance_ids)
    print("Stopping instances:", instance_ids)

def lambda_handler(event, context):
    current_time = datetime.now(timezone.utc)
    stop_time = current_time.replace(hour=8, minute=12, second=0, microsecond=0)
     start_time = current_time.replace(hour=8, minute=15, second=0, microsecond=0)
    
    if start_time <= current_time <= stop_time:
        start_instances(INSTANCE_IDS)
    else:
        stop_instances(INSTANCE_IDS)

    return {
        'statusCode': 200,
        'body': 'EC2 instance(s) scheduled.'
    }
