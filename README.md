# Deploy Web Application on EC2 Instance (Manually)

## Project Overview

This project demonstrates how to deploy a full-stack web application on an AWS EC2 instance using Docker. The deployment process is performed manually, providing hands-on experience with managing virtual machines, securing access, and configuring firewalls.

## Technologies Used

- **Amazon Web Services (AWS)**
- **Docker**
- **Linux (Amazon Linux 2 / Ubuntu)**

## Key Features

- Provision and configure an EC2 instance
- SSH into the remote EC2 instance
- Install Docker and required dependencies
- Deploy Docker image from a private DockerHub repository
- Run the application as a Docker container
- Set up inbound rules on EC2 to access the app externally from a browser

## Steps to Deploy

1. **Create EC2 Instance on AWS:**

   - Launch an EC2 instance with a public IP
   - Assign a security group allowing inbound traffic on port 22 (SSH) and the app port (e.g., 3000)

2. **Connect via SSH:**

   ```bash
   ssh -i /path/to/your-key.pem ec2-user@<EC2_PUBLIC_IP>
   ```

3. **Install Docker:**

   ```bash
   sudo yum update -y
   sudo amazon-linux-extras install docker
   sudo service docker start
   sudo usermod -a -G docker ec2-user
   ```

   Log out and back in again to apply Docker permissions.

4. **Login to DockerHub (on EC2):**

   ```bash
   docker login
   ```

5. **Pull Docker Image from Private Repo:**

   ```bash
   docker pull shlaskin/demo-app:1.0
   ```

6. **Run Docker Container:**

   ```bash
   docker run -p 3000:3000 shlaskin/demo-app:1.0
   ```

7. **Adjust EC2 Security Group:**

   - Add an inbound rule to allow HTTP traffic (port 3000)

8. **Verify Deployment:**

   - Visit `http://<EC2_PUBLIC_IP>:3000` in your browser

## Author

**GitHub:** [shlaskin101](https://github.com/shlaskin101)

## License

This project is licensed under the MIT License - see the LICENSE file for details.
