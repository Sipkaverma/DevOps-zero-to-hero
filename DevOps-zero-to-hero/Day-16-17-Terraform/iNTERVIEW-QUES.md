# Day 16: Terraform Basics & IaC Interview Questions

### Q1: What is the difference between Declarative and Imperative Infrastructure as Code?
**Answer:**
- **Declarative (Terraform):** You define *WHAT* the final state should look like. Terraform automatically calculates dependencies, ordering, and state changes required to achieve that target state.
- **Imperative (Bash/AWS CLI):** You specify step-by-step *HOW* to achieve the state (e.g., "Create VPC, then create Subnet, then attach Gateway").

---

### Q2: What happens under the hood when you run `terraform init`?
**Answer:**
1. Parses configuration files (`.tf`) in the working directory.
2. Identifies required cloud providers (e.g., `hashicorp/aws`) and downloads specified provider plugins into the hidden `.terraform/` directory.
3. Initializes modules referenced in the code.
4. Connects to and configures the backend (S3/Terraform Cloud) if declared.

---

### Q3: What is the purpose of the `terraform.tfstate` file?
**Answer:**
The state file maps real-world cloud resources to your configuration code. It:
- Stores metadata and resource tracking IDs assigned by the cloud provider.
- Enhances performance by caching resource attributes.
- Allows Terraform to determine necessary modifications (`plan`) by comparing desired code against current cloud state.

---

### Q4: How do you prevent accidental resource deletion in Terraform?
**Answer:**
1. **Lifecycle Rules:** Use `lifecycle { prevent_destroy = true }` inside sensitive resource blocks (e.g., Databases/S3 buckets).
2. **State Locking:** Prevent concurrent applies.
3. **Execution Reviews:** Enforce strict code review on `terraform plan` outputs in CI/CD before running `apply`.

---

### Q5: What is the difference between `variables.tf` and `terraform.tfvars`?
**Answer:**
- **`variables.tf`:** Declares the structure, type (string, map, list), default values, and descriptions of input variables.
- **`terraform.tfvars`:** Assigns actual runtime values to those declared variables (often excluded from version control if containing secrets).

# Day 17: Advanced Terraform & CI/CD Interview Questions

### Q1: Why should you never commit `terraform.tfstate` to Git?
**Answer:**
1. **Security Exposure:** State files store plain-text secrets, database passwords, and private API keys managed by Terraform.
2. **Merge Conflicts & Corruption:** Simultaneous commits by multiple engineers corrupt the state file, causing infrastructure drift or accidental resource destruction.
3. **Lack of Concurrency Control:** Git does not support real-time state locking during simultaneous deployment executions.

---

### Q2: How does State Locking work with S3 and DynamoDB?
**Answer:**
- **Storage:** S3 bucket holds the actual `.tfstate` file.
- **Locking:** DynamoDB table holds a lock key (`LockID`).
- When `terraform plan` or `apply` runs, Terraform writes a Lock ID into DynamoDB.
- If another engineer or CI/CD job attempts an apply concurrently, Terraform rejects the execution with a `State Locked` error until the primary operation releases the DynamoDB lock.

---

### Q3: How do you debug a `403 Forbidden` or `Access Denied` error during `terraform init` in a CI/CD pipeline?
**Answer:**
1. **IAM Policy Audit:** Check if the executing identity (IAM Role attached to runner or AWS credentials secret) has `s3:GetObject`, `s3:PutObject`, and `s3:ListBucket` permissions on the specified S3 ARN.
2. **Bucket Ownership & Policy:** Ensure S3 Bucket Policy doesn't explicitly deny access from external AWS accounts or non-SSL connections.
3. **Credential Propagation:** Verify if IAM role changes have propagated or if runner caches old credentials.

---

### Q4: What is a Terraform Module, and what are its best practices?
**Answer:**
A module is a container for multiple resources configured together.
- **Best Practices:**
  1. Maintain single-purpose modules (e.g., `modules/vpc`, `modules/ec2`).
  2. Use Input Variables for dynamic configurations instead of hardcoding values.
  3. Expose Outputs for cross-module resource referencing.
  4. Version control modules using Git tags or private registry paths.

---

### Q5: How do you handle Infrastructure Drift in production?
**Answer:**
Infrastructure drift occurs when manual changes are made directly in the cloud console outside of Terraform.
- **Detection:** Run `terraform plan`. Terraform compares current real-world infrastructure against state and code.
- **Resolution Options:**
  1. **Revert:** Run `terraform apply` to overwrite manual changes and restore system back to code definitions.
  2. **Import:** If manual changes must be kept, update `.tf` code to match and run `terraform refresh` / update state.