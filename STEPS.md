✅ Lab Summary:
You're acting as Nikhil, setting up a static website for the café using Amazon S3. The tasks cover:

Hosting a static website

Public access with a bucket policy

Versioning

Lifecycle policies for cost optimization

Cross-region replication for disaster recovery

✅ Task 1: Extract Website Files
Download the .zip file provided by the lab.

Extract it to a folder. You’ll see:

index.html

images/ folder (possibly also a CSS file/folder)

✅ Task 2: Create S3 Bucket & Enable Website Hosting
Go to the Amazon S3 Console.

Click Create bucket:

Name: cafe-static-website-yourname (must be globally unique)

Region: US East (N. Virginia) us-east-1

Uncheck: Block all public access

Check: Enable ACLs

After creating the bucket:

Open the bucket → Properties tab

Scroll to Static website hosting

Enable it and set:

Index document: index.html

✅ Task 3: Upload Website Content
Go to the bucket → Objects tab.

Upload:

index.html

images/ folder (or all contents inside it)

CSS folder/file (if any)

Get the website endpoint from the Static Website Hosting section.

Open that link in a browser. It should show your site.

✅ Task 4: Add Bucket Policy for Public Read Access
Go to your bucket → Permissions → Bucket Policy.

Add this JSON (replace your-bucket-name):

json
Copy
Edit
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
Save. Now all files are publicly accessible.

✅ Task 5: Enable Versioning
Go to the bucket → Properties → Enable Versioning.

Edit index.html:

Replace bgcolor="aquamarine" with gainsboro

Replace bgcolor="orange" with cornsilk

Upload the updated file (overwrite).

Go to the bucket → Click “Show versions” to see both versions.

📌 MCQ Q2 Hint: To prevent accidental deletion of preserved versions, you can use S3 Object Lock (WORM: Write Once Read Many). Also, enable MFA Delete for stricter controls.

✅ Task 6: Add Lifecycle Rules
Go to bucket → Management → Create lifecycle rule

Rule 1:

Apply to previous versions

Transition to S3 Standard-IA after 30 days

Rule 2:

Apply to previous versions

Expire after 365 days

You should now have 2 separate lifecycle rules.

✅ Task 7: Cross-Region Replication
Create a second S3 bucket in another Region (e.g., Oregon us-west-2)

Enable Versioning

Go to source bucket → Replication rules

Create a rule for entire bucket

Use IAM Role CafeRole

Select destination bucket

Choose: "Don’t replicate existing objects"

Edit index.html again and upload it.

Confirm you see 3 versions in source bucket.

Check if it's replicated in destination.

Now delete the latest version in the source.

Check if that version also disappears in the destination bucket.

📌 MCQ Q4 Hint: S3 CRR only deletes in destination if Delete Marker replication is enabled. Otherwise, deleted objects in source stay in destination.

✅ Submit Your Work.
Go to the Submit button at the top.

Check your Grades and Submission Report after a few minutes..