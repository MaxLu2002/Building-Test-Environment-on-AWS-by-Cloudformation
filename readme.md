<!-- 英文版 -->
# AWS CloudFormation Automated Testing Environment

## Introduction
This project aims to automate the creation of a cloud-based testing environment using AWS CloudFormation, helping users quickly and efficiently deploy and tear down environments, enhancing the convenience of development and testing workflows.

## Objective
To design a comprehensive and user-friendly CloudFormation architecture that allows users to rapidly create or delete the necessary resources when entering a new environment. This architecture is particularly suitable for development and testing teams that need to frequently create and destroy environments.

## Features
1. **Tagging Rules**: Provides clear resource tagging rules so that all resources created by CloudFormation can be tagged based on the Stack Name. For example, if the Stack Name is `test01`, all resources will automatically have Name Tags such as `test01-EC2`, `test01-S3`, etc. This allows users to easily manage and identify resources and quickly determine if a resource was created by CloudFormation.

## AWS Services Included in the Environment
- **VPC**: One public subnet and one private subnet.
- **EC2**: Two instances, one in the public subnet and the other in the private subnet (both instances can be accessed via SSH).
- **S3 Bucket**: One S3 bucket for storage.
- **NAT Gateway**: A NAT gateway for network address translation for the private subnet.
- **Security Groups**: Security groups configured for both public and private subnets.

### Important Notes
- **Keypair**: Users need to create and manage their own key pairs.

## Steps to Access All EC2 Instances
1. **Create a Keypair and Download it to Your Local Machine**: Go to the AWS Management Console, create a new key pair, and download the `.pem` file to your local computer.
2. **Set the Region and AZ (Availability Zone) in the YAML File**: Specify the AWS Region and AZ where you want to deploy the resources in the CloudFormation YAML file.
3. **Execute the CloudFormation YAML**: Use the AWS CLI or AWS Management Console to deploy the CloudFormation stack.
4. **Upload the Keypair to the Public EC2**: Use a terminal to upload the local key pair file to the public EC2 instance. Use the following command:
   ```bash
   scp -i "{your_keypair_name}.pem" "{your_keypair_name}.pem" ec2-user@{public_IP}:
   ```
5. **SSH into the Public EC2**: Use SSH to connect to the public EC2 instance.

   ```bash
   ssh -i "{your_keypair_name}.pem" ec2-user@{public_IP}
   ```
6. **Set the Key to Read-Only**: On the public EC2, set the key pair to read-only to ensure security:

   ```bash
   chmod 400 {your_keypair_name}.pem
   ```
7. **SSH into the Private EC2**: Use the public EC2 as a jump host to SSH into the private EC2.

   ```bash
   ssh -i "{your_keypair_name}.pem" ec2-user@{private_IP}
   ```


<!-- 中文版 -->
## 簡介
本專案旨在透過 AWS CloudFormation 自動化建立雲端測試環境，幫助使用者快速且高效地部署與移除環境，提升開發與測試工作的便利性。

## 目的
設計一個完整且易於使用的 CloudFormation 架構，使得使用者在進入新環境時，可以快速建立或刪除所需的資源。這個架構特別適合於需要經常創建和銷毀環境的開發和測試團隊。

## 特色
1. **標籤規則**：提供清晰的資源標籤規則，使所有通過 CloudFormation 建立的資源都可以根據 Stack Name 進行標籤。例如，如果 Stack Name 為 `test01`，則所有資源的 Name Tag 會自動設置為 `test01-EC2`、`test01-S3` 等。這樣可以讓使用者更輕鬆地管理和識別各種資源，並一目了然地判斷資源是否由 CloudFormation 建立。

## 環境包含的 AWS 服務

- **VPC**：一個公網子網和一個私網子網。
- **EC2**：兩個實例，一個位於公網子網，另一個位於私網子網（兩個實例都可通過 SSH 訪問）。
- **S3 Bucket**：一個 S3 存儲桶。
- **NAT Gateway**：用於私網子網的網路地址轉換。
- **Security Group**：針對公網和私網的安全組設定。

### 重要事項

- **Keypair**：需要使用者自行創建並管理。

## 登入所有 EC2 的步驟

1. **創建 Keypair 並下載至本地主機**：進入 AWS Management Console 並創建一個新的 Keypair，然後下載該 `.pem` 檔案到您的本地電腦。
2. **設定 YAML 檔案中的 Region 和 AZ（可用區域）**：在 CloudFormation 的 YAML 檔案中指定您想要部署資源的 AWS Region 和 AZ。
3. **執行 CloudFormation YAML**：使用 AWS CLI 或 AWS Management Console 來部署 CloudFormation 堆疊。
4. **將 Keypair 上傳至公網 EC2**：利用 Terminal 將本地的 Keypair 檔案上傳到公網 EC2 實例。使用指令如下：
   
   ```bash
   scp -i "{your_keypair_name}.pem" "{your_keypair_name}.pem" ec2-user@{public_IP}:
   ```
5. **SSH 登入公網 EC2**：使用 SSH 連接到公網 EC2 實例。
   
   ```bash
   ssh -i "{your_keypair_name}.pem" ec2-user@{public_IP}
   ```
6. **將 Key 設置為唯讀**：在公網 EC2 上，將 Keypair 設置為唯讀以確保安全性：

   ```bash
   chmod 400 {your_keypair_name}.pem
   ```
7. **SSH 登入私網 EC2**：使用跳板機的方式從公網 EC2 SSH 進入私網 EC2。

   ```bash
   ssh -i "{your_keypair_name}.pem" ec2-user@{private_IP}
   ```
