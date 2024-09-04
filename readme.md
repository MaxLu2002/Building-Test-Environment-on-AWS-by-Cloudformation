簡介：這份專案希望透過Cloudformation的方式自動化建立在雲端上的測試環境

目的：設計完善的Cloudformation架構，方便使用者在登入新環境時能快速建立與環境

環境包含的AWS服務
。EC2 (密鑰)
。VPC (一個公網、一個私網)

Keypairs 要自己創建

*** 步驟 ***
1. 創建keypair並下載
2. 在YAML中設定region
3. 執行YAML
4. scp -i "---key.pem" "---key.pem" ec2-user@{public IP}
5. SSH進入public EC2
6. 把KEY變成唯讀
7. SSH 進入 private EC2 

<!-- NEXT STEP -->
參考這份檔案，把cloudformation變成Terraform 
    https://stackoverflow.com/questions/49743220/how-to-create-an-ssh-key-in-terraform