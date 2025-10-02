🎤 Interview Style Answer

👉 “IAM (Identity and Access Management) in AWS is a service that helps us securely control who can access AWS resources and what actions they can perform. In simple words, it’s about managing users, groups, and permissions. In my project, I used IAM to create roles for EC2 and EKS services, give least-privilege access to developers, and manage service-to-service communication without hardcoding credentials.”

🔹 How I Applied IAM in My Project

EC2 Role – Instead of putting AWS access keys in the server, we attached an IAM role to EC2 to allow it to access S3 buckets.

Example: An application running in EC2 uploaded logs to an S3 bucket using IAM role.

EKS Service Account (IRSA) – We created IAM roles mapped to Kubernetes service accounts so that specific pods could access AWS services like DynamoDB or S3.

Least Privilege Principle – Developers only got access to the services they needed. For example, Dev team could only access Dev environment resources, not Prod.

Multi-Factor Authentication (MFA) – For extra security, we enabled MFA for IAM users who had console access.


🔹 Main Functions of IAM (Explained + Project Use Case)
1. Users

✅ What it is:
An IAM User represents an individual person (e.g., developer, admin) who interacts with AWS. Each user has credentials (username/password or access keys) and can be assigned permissions.

🛠️ In Project:
In our project, we created individual IAM users for each team member (e.g., DevOps engineers, developers, testers).
Each user had least privilege access—for example, developers could deploy to development environments only.

2. Groups

✅ What it is:
A Group is a collection of users that share the same set of permissions. Instead of assigning policies to each user, you attach policies to a group.

🛠️ In Project:
We had IAM groups like:

DevGroup (developer access: EC2, S3, CodeCommit)

OpsGroup (admin-level access: CloudWatch, EC2, IAM read-only)
When new team members joined, we simply added them to the relevant group.

3. Policies

✅ What it is:
Policies are JSON documents that define permissions (what resources a user or role can access, and what actions are allowed or denied).
Two main types:

Managed policies (AWS or customer-created)

Inline policies (attached directly to a user, group, or role)

🛠️ In Project:
We used both:

AWS managed policies (like AmazonEC2ReadOnlyAccess) for standard roles.

Custom inline policies for fine-tuned access—for example, giving a Lambda function access to only one S3 bucket.

4. Roles

✅ What it is:
IAM Roles grant temporary access to AWS resources. They're assumed by:

AWS services (EC2, Lambda, EKS)

External identities (users from another AWS account or identity provider)

🛠️ In Project:

EC2 instances used a role with access to S3 and CloudWatch Logs, avoiding hardcoding keys.

Lambda functions used roles to access DynamoDB tables.

We also set up cross-account roles to allow CI/CD pipelines from one AWS account to deploy to another.

5. MFA (Multi-Factor Authentication)

✅ What it is:
Adds a second layer of security beyond username/password (e.g., TOTP via Google Authenticator).

🛠️ In Project:
MFA was mandatory for all users with console access, especially for admins.
We enforced it using IAM policy conditions that denied actions unless MFA was present.

6. Access Keys

✅ What it is:
Used for programmatic access (CLI, SDKs). Comprises an Access Key ID and a Secret Access Key.

🛠️ In Project:
Access keys were used by:

Automation scripts running in Jenkins or GitLab CI

Developers using AWS CLI to interact with S3 or deploy apps

We followed best practices:

Regularly rotated keys

Never committed them to code repos

Used environment variables or secrets managers
