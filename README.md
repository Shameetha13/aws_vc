# aws_vc
# AWS-hosted Virtual Classroom and Learning Platform

### Project Overview
This AWS-hosted Virtual Classroom and Learning Platform provides an efficient and scalable digital learning environment that leverages several AWS services. By integrating Amazon EC2, Amazon S3, and Amazon RDS, this project enables seamless access to learning materials, user management, and application deployment, creating a flexible and secure educational platform. The backend is developed with Flask, making it suitable for interactive, cloud-based web applications.

### Key AWS Resources Used
1. **Amazon S3 Bucket (`cloneBucket13`)**: Stores all course materials and user-uploaded content for easy access and management.
2. **EC2 Instance (`clone_ec`)**:
   - **Instance ID**: `ec2-user@18.234.190.159`
   - **Configuration**: Uses Amazon Linux 2, hosting the Flask app and handling web requests.
   - **Commands**:
     ```bash
     ssh -i "path/to/clone.pem" ec2-user@18.234.190.159
     source venv/bin/activate
     cd <project_directory>
     python3 app.py
     ```
3. **RDS MySQL Database (`clonedb`)**: Manages user data (e.g., registration and login information).
   - **Connection Command**:
     ```bash
     mysql -h clonedb.c56g4kmq4b38.us-east-1.rds.amazonaws.com -P 3306 -u admin1 -p
     ```

### MySQL Configuration and Database Setup
1. **Create the Database**:
   ```sql
   CREATE DATABASE clone_db;
   USE clone_db;
   ```
2. **User Table**:
   ```sql
   CREATE TABLE users (
       username VARCHAR(100) PRIMARY KEY,
       password_hash VARCHAR(255)
   );
   ```

### Project Directory Structure
- **Main Directory**: `shamee_aws_project/`
- **`app.py`**: Main Flask application file.
- **`requirements.txt`**: Lists all dependencies.
- **`static/`**: Contains static files, such as `styles.css`.
- **`templates/`**: HTML files (`home.html`, `dashboard.html`, `login.html`, `register.html`).
- **`venv/`**: Virtual environment folder for project dependencies.

### Flask Application Setup & Running
1. **Create Virtual Environment**:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```
2. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
3. **Run the Application**:
   ```bash
   python app.py
   ```

### Key Endpoints
- **Home Page**: `http://<EC2-Public-IP>:5000/`
- **User Login** and **Registration**: Allows users to authenticate and register.
- **Dashboard**: Displays downloadable course materials stored in S3.

### GitHub Integration
- **Clone the Repository**:
  ```bash
  git clone https://github.com/username/repository.git
  ```
- **Standard Git Commands** to track and push changes:
  ```bash
  git add .
  git commit -m "Commit message"
  git push origin main
  ```

### PuTTY Setup and SSH Configuration
To securely access your EC2 instance and manage file transfers, this project uses PuTTY for SSH connections and SCP (secure copy) commands.

1. **Convert `.pem` to `.ppk` using PuTTYgen**:
   - Open PuTTYgen, load the `.pem` file, and save the converted `.ppk` file.
   - If needed, you can reverse this process to convert `.ppk` back to `.pem`.

2. **SSH Authentication with PuTTY**:
   - Open PuTTY and go to `Connection > SSH > Auth`.
   - Browse for the `.ppk` file under the "Private key file for authentication" setting.
   - Set the host to your EC2 public IP address and connect.

3. **File Transfer Using SCP**:
   - To transfer files to the EC2 instance, use the following SCP command (adjust paths as needed):
     ```bash
     scp -i "path/to/clone.pem" path/to/yourfile ec2-user@<EC2-Public-IP>:/home/ec2-user/aws_vc/
     ```
   - Example for transferring `home.html`:
     ```bash
     scp -i "path/to/clone.pem" C:\shamee_aws_prjct\templates\home.html ec2-user@18.234.190.159:/home/ec2-user/aws_vc/templates/
     ```

4. **Using SCP to Transfer All Project Files**:
   - Transfer main files (like `app.py`, `requirements.txt`, `styles.css`, and HTML templates) as needed to `/home/ec2-user/aws_vc/`.

### Website Access
Once the Flask application is deployed on your EC2 instance, you can access the Virtual Classroom platform through a web browser.

1. **Application URL**:
   - Use the following format to access your application:
     ```
     http://<EC2-Public-IP>:5000/
     ```
   - Replace `<EC2-Public-IP>` with your actual EC2 instance's public IP address.

2. **Available Pages**:
   - **Home Page**: The landing page with information about the platform.
   - **Register**: Allows new users to create an account.
   - **Login**: Authenticates returning users and redirects them to the dashboard.
   - **Dashboard**: Lists available course materials with download links for easy access.

3. **Running the Application on EC2**:
   - Start the Flask application with the following command:
     ```bash
     python app.py
     ```
   - This command will run the app on all available IP addresses at port `5000`, making it accessible externally at `http://<EC2-Public-IP>:5000`.

### Example
If your EC2 instance IP is `18.234.190.159`, access the application at:
```
http://18.234.190.159:5000
```

### Conclusion
The AWS-hosted Virtual Classroom and Learning Platform demonstrates the integration of AWS cloud services and Flask-based web applications to build a highly responsive virtual learning environment. This project is a robust solution for delivering and managing educational resources securely and efficiently, utilizing Git for version control and PuTTY for secure file transfers.

