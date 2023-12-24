# WordPress Deployment on AWS EC2 using Docker Compose

This README provides a comprehensive guide on deploying a WordPress site on an AWS EC2 instance using Docker and Docker Compose. Follow these steps to get your WordPress site up and running on the cloud.

## Step 1: Launch an AWS EC2 Instance

1. **Log in to AWS Console**: Go to [AWS Management Console](https://aws.amazon.com/console/) and sign in.

2. **Navigate to EC2 Dashboard**: On the AWS Management Console, find and select “EC2” to open the EC2 Dashboard.

3. **Launch Instance**:
   - Click on “Launch Instances” to create a new EC2 instance.
   - **Choose an Amazon Machine Image (AMI)**: Select an appropriate AMI, like Amazon Linux 2 or Ubuntu Server.
   - **Choose an Instance Type**: Select an instance type (e.g., `t2.micro` for testing).
   - **Configure Instance Details**: Set the network and subnet as per your requirement. Leave other settings as default.
   - **Add Storage**: Adjust the size of the EBS volume if necessary.
   - **Add Tags**: Optionally, add tags for easier management.
   - **Configure Security Group**: Add a rule to allow HTTP traffic on port `80` and SSH traffic on port `22`.
   - **Review and Launch**: Review your settings and click “Launch”.
   - **Create a Key Pair**: Create a new key pair, download it, and keep it secure.

## Step 2: Connect to Your EC2 Instance

1. **Open Terminal or Command Prompt**.

2. **Locate Your Key Pair File** and change its permissions (for Linux/Mac):
   ```bash
   chmod 400 /path/to/your-key.pem
4. **Connect via SSH** (replace ec2-user and your-instance-ip with your instance's username and public IP):
   ```bash
   ssh -i /path/to/your-key.pem ec2-user@your-instance-ip
## Step 3: Install Docker on EC2
1. **Update Your Package Index** (based on your AMI):
   ```bash
   sudo yum update -y  # Amazon Linux, CentOS
   sudo apt update     # Ubuntu
2. **Install Docker:**
   ```bash
   sudo yum install docker -y  # Amazon Linux, CentOS
   sudo apt install docker.io -y # Ubuntu
3. **Start and Enable Docker:**
   ```bash
   sudo systemctl start docker
   sudo systemctl enable docker
4. **Add EC2 User to the Docker Group** (to use Docker as a non-root user):
   ```bash
   sudo usermod -aG docker ${USER}
## Step 4: Install Docker Compose on EC2
1. **Download Docker Compose** (replace 1.29.2 with the latest version):
   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
2. **Make Docker Compose Executable:**
   ```bash
   sudo chmod +x /usr/local/bin/docker-compose
3. **Verify Installation:**
   ```bash
   docker-compose --version
## Step 5: Deploy WordPress using Docker Compose
1. **Clone Your Repository** or copy the Docker Compose file to your EC2 instance.
2. **Navigate to the Directory** containing your docker-compose.yml file.
3. **Run Docker Compose:**
   ```bash
   docker-compose up -d
4. **Verify that Containers are Running:**
   ```bash
   docker-compose ps
## Step 6: Access Your WordPress Site
1. Open a web browser and navigate to http://your-ec2-instance-public-ip.
2. Follow the on-screen instructions to set up your WordPress site.
