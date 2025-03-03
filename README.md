# AWS Cloud Image Copy Project

This guide provides a step-by-step process to set up S3 and Lambda integration to automatically copy images from one S3 bucket to another.

## 1. Create S3 Buckets:

1. Go to the AWS S3 console.
2. Click "Create bucket".
3. Name the first bucket (e.g., `bucket-source-yourname`), leave settings default, and click "Create".
4. Create the second bucket (e.g., `bucket-destination-yourname`) the same way.

## 2. Set Up the Lambda Function:

1. Go to the AWS Lambda console.
2. Click "Create function" → Choose "Author from scratch".
3. Function name: `function-copy-anyname`
4. Runtime: Python 3.x
5. Click "Create function".

## 3. Add Environment Variable:

1. In the Lambda function, go to the "Configuration" tab → "Environment variables".
2. Add a variable:
   - Key: `DEST_BUCKET`
   - Value: `bucket-destination-yourname`

## 4. Add Permissions (IAM Role):

1. Go to the "Configuration" tab → "Permissions" → Click the role name.
2. Attach the following policy:

```json
{
  "Effect": "Allow",
  "Action": ["s3:GetObject", "s3:PutObject"],
  "Resource": [
    "arn:aws:s3:::bucket-source-yourname/*",
    "arn:aws:s3:::bucket-destination-yourname/*"
  ]
}
```

3. Save changes.

## 5. Add the Code:

1. In the "Code" tab of the Lambda function, paste the required code.
2. Click "Deploy".

## 6. Set S3 Trigger:

1. Go to the "Configuration" tab → "Triggers" → Add trigger.
2. Select "S3" as the source.
3. Choose `bucket-source-yourname`.
4. Event type: `PUT` (For new object creation).
5. Click "Add".

## 7. Test It:

1. Go to the S3 console and upload an image to `bucket-source-yourname`.
2. Check `bucket-destination-yourname` — the image should be copied automatically!

