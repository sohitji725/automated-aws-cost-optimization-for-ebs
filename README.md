# 🧹 Automated AWS Cost Optimization for EBS

## 📘 Overview
A fully automated, serverless solution to reduce AWS storage costs by identifying and deleting orphaned **EBS snapshots** that are no longer attached to active EC2 instances or volumes.  
Built with **AWS Lambda**, **Amazon EventBridge**, and **Boto3 (Python SDK)**.

---

## 🚀 Architecture
**Components used:**
- **AWS Lambda:** Runs the Python automation.
- **Amazon EventBridge:** Triggers Lambda on a schedule.
- **AWS IAM Role:** Provides least-privilege access.
- **Amazon CloudWatch:** Stores logs and execution results.

📸 ![cost-optim](https://github.com/user-attachments/assets/bb5a4777-1f49-4be1-bae6-43df588feafb)


---

## 🎯 Goal
Automate the cleanup of orphaned EBS snapshots across multiple regions to reduce monthly storage costs by 35–40%.

---

## 🧪 Demonstration (AWS Console – No CLI)

### **Step 1: Log in and choose a region**
1. Visit [AWS Management Console](https://aws.amazon.com/console/).
2. Select your preferred region (e.g., **us-east-1**).

---

### **Step 2: Create an EC2 instance**
1. Open **EC2 → Launch instance**.
2. Name it `demo-cleanup-instance`.
3. Choose **Amazon Linux 2** and instance type **t2.micro (Free Tier)**.
4. Keep default configurations and launch.
5. Wait until status = **Running**.

📸 *Screenshot:* EC2 instance dashboard showing your instance running.
<img width="1920" height="1080" alt="Screenshot (101)" src="https://github.com/user-attachments/assets/976198a8-3d1c-4647-a810-79b041571b7b" />


---

### **Step 3: Create a snapshot**
1. Go to **EC2 → Instances → Storage tab**.
2. Click the **Volume ID** link.
3. Under **Actions → Create snapshot**.
4. Name it `demo-snapshot`.
5. Wait until status = **Completed**.

📸 *Screenshot:* Snapshot created in image showing snapshots (1)
<img width="1920" height="1080" alt="Screenshot (100)" src="https://github.com/user-attachments/assets/c47f3caa-529e-4481-af18-43079b58a699" />

---

### **Step 4: Delete the instance and volume**
1. Go back to **Instances → Terminate instance**.
2. Confirm the instance is **terminated**.
3. Check **Volumes** → confirm deleted.
4. Check **Snapshots** → orphan snapshot remains.

📸 *Screenshot:* Snapshot list showing orphan snapshot with no volume
<img width="1920" height="1080" alt="Screenshot (102)" src="https://github.com/user-attachments/assets/914cd216-eecc-49a7-b36f-21d7c4c2d2af" />

---

### **Step 5: Create IAM Role for Lambda**
1. Go to **IAM → Roles → Create role**.
2. Trusted entity: **AWS Service → Lambda**.
3. Name: `lambda-ebs-cleanup-role`.
4. After creation, attach inline policy:

<img width="1920" height="1080" alt="Screenshot (96)" src="https://github.com/user-attachments/assets/0b84ad94-4396-403d-aeef-24e7ebc37986" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6ffcc556-d41f-46ed-a1ed-9c79dfb75f4e" />
## 🚀 Step 6: Create Lambda Function

1. Go to **AWS Lambda → Create function**.  
2. Choose **Author from scratch**.  
3. Function name: `Cost-optimization-ebs`.  
4. Runtime: **Python 3.9**.  
5. Attach IAM Role: `cost-optimization-function-role-3cntwsnb`.

📸 **Screenshot:**  
Lambda function configuration screen.

<img width="1920" height="1080" alt="Screenshot (107)" src="https://github.com/user-attachments/assets/f31d4141-23e7-4801-8d8b-0bf651048af3" />
<img width="1920" height="1080" alt="Screenshot (104)" src="https://github.com/user-attachments/assets/a883639b-2317-4bf0-a3e7-7331d5a29e0f" />
<img width="1920" height="1080" alt="Screenshot (104)" src="https://github.com/user-attachments/assets/a5ca4c4b-44d9-4973-bc24-46064f4e9544" />

---

## 🧪 Step 8: Test the Function

1. Click **Test** in the Lambda console.  
2. Create a test event named `testEBSDelete`.  
3. Run the test and check **CloudWatch Logs**.  

You should see logs confirming orphaned snapshots were deleted successfully.

📸 **Screenshot:**  
Lambda test results showing snapshot deletion logs.

<img width="1920" height="1080" alt="Screenshot (103)" src="https://github.com/user-attachments/assets/6c90c41a-9461-49a8-9e78-ad7079ebeedc" />

---

## ⚙️ Step 9: Automate with Amazon EventBridge

1. Go to **Amazon EventBridge → Rules → Create rule**.  
2. Name the rule: `ebs-rule`.  
3. Rule type: **Schedule**.  
4. Set a **fixed rate of 1 day** (to run daily).  
5. Target: **Lambda function → EBS-CostOptimizer**.  
6. Create the rule.

📸 **Screenshot:**  
EventBridge rule page showing Lambda as the target.

<img width="1920" height="1080" alt="Screenshot (108)" src="https://github.com/user-attachments/assets/00afa3d2-63e6-40d7-b769-fe8b73532ee3" />

---

## 📊 Step 10: Monitor in CloudWatch

1. Go to **CloudWatch → Log groups**.  
2. Open `/aws/lambda/EBS-CostOptimizer`.  
3. Check the log stream for messages confirming deleted snapshots.  

📸 **Screenshot:**  
CloudWatch logs showing successful snapshot deletion.

<img width="1920" height="1080" alt="Screenshot (109)" src="https://github.com/user-attachments/assets/65982c3d-0c75-4118-bc84-2f172ab9ae6b" />

---

## 🧩 Technologies Used
- **AWS Lambda**  
- **Amazon EventBridge**  
- **AWS IAM**  
- **Amazon CloudWatch**  
- **Python (Boto3 SDK)**  

---

## 🧠 Key Learnings
- Automated AWS cost governance using **serverless architecture**.  
- Implemented **role-based access control** for Lambda.  
- Cross-referenced EBS snapshots and volumes programmatically.  
- Scheduled automation with **Amazon EventBridge**.  
- Achieved reliable, event-driven snapshot cleanup for cost efficiency.
