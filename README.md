# 📦 **ERPNext Installing Guide**

Welcome to our comprehensive guide on installing **ERPNext Version 15** on **Ubuntu 24.04**.  
ERPNext is a powerful, open-source ERP system that streamlines business processes from inventory management to accounting.  
Whether you’re new to ERPNext or have worked with it for years, this **step-by-step tutorial** will walk you through the installation process, ensuring you have everything set up correctly on your Ubuntu 24.04 system.

---

## 🚀 **Prerequisites**

To ensure optimal functionality, prepare your server with the following requirements:

### 💾 **Software Requirements**
- ✅ Updated **Ubuntu 24.04**  
- ✅ A user with **sudo privileges**  
- ✅ **Python 3.11+**  
- ✅ **pip 20+**  
- ✅ **MariaDB 10.3.x**  
- ✅ **Node.js 18**  
- ✅ **Yarn 1.12+**  

### 🖥️ **Hardware Requirements (Recommended)**
- 💾 4GB RAM  
- 💿 40GB Hard Disk  

---

## 🏗️ **Step-by-Step Installation**

### 1️⃣ **Update and Upgrade Packages**


```
sudo apt-get update -y && sudo apt-get upgrade -y
```

Create a New User

It is advisable to avoid using the root user for daily tasks. Create a Frappe Bench user:


```
sudo adduser [frappe-user]
sudo usermod -aG sudo [frappe-user]
su [frappe-user]
cd /home/[frappe-user]
```

### ⚡ Replace [frappe-user] with your desired username, e.g., frappe.


### 📚 Installing Required Packages

### 3️⃣ Install Git


```
sudo apt-get install git -y
```

### 4️⃣ Install Python Dependencies

ERPNext requires Python 3.11+ and other dependencies:


```
sudo apt-get install python3-dev -y
sudo apt-get install python3-setuptools python3-pip -y
sudo apt install python3.12-venv -y
```

### 5️⃣ Install MariaDB

ERPNext relies on MariaDB:


```
sudo apt-get install software-properties-common -y
sudo apt install mariadb-server -y
sudo mysql_secure_installation
```


### ⚡ During the configuration:

   - 1️⃣ Set a root password
   - 2️⃣ Remove anonymous users
   - 3️⃣ Allow remote root login (set N)
   - 4️⃣ Remove the test database
   - 5️⃣ Reload privilege tables


### ✏️ Edit the MariaDB configuration file:



```
sudo nano /etc/mysql/my.cnf
```

Add the following lines:



```
[mysqld]
innodb-file-per-table=1
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
```


### 🔄 Restart MariaDB:

```
sudo service mysql restart
```

### 6️⃣ Install Redis Server


```
sudo apt-get install redis-server -y
```


### 7️⃣ Install CURL, Node.js, NPM, and Yarn

🔗 Install CURL:


```
sudo apt install curl
```

### ⚡ Install Node.js:


```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
source ~/.profile
nvm install 18
```

### 📦 Install NPM:


```
sudo apt-get install npm -y
```

### 8️⃣ Install wkhtmltopdf


```
sudo apt-get install xvfb libfontconfig wkhtmltopdf -y
```

🎛️ Setting Up Frappe Bench

### 9️⃣ Install Frappe Bench


```
sudo -H pip3 install frappe-bench --break-system-packages
sudo -H pip3 install ansible --break-system-packages
```

### 🔟 Initialize Frappe Bench


```
bench init frappe-bench --frappe-branch version-15
cd frappe-bench
```

### 🔑 Change directory permissions:


```
chmod -R o+rx /home/[frappe-user]
```

### 1️⃣1️⃣ Create a New Site


```
bench new-site [site-name]
```


### 1️⃣2️⃣ Install ERPNext and Other Apps

Download and install required apps:


```
bench get-app payments
bench get-app --branch version-15 erpnext
bench get-app hrms
bench --site [site-name] install-app erpnext
bench --site [site-name] install-app hrms
```

### 🌐 Start the server:


```
bench start
```


ERPNext will run on:

### 🌐 http://[YOUR SERVER IP]:8000


### 🌟 Deploying ERPNext in Production Mode

### 1️⃣3️⃣ Enable Scheduler and Disable Maintenance Mode


```
bench --site [site-name] enable-scheduler
bench --site [site-name] set-maintenance-mode off
```


### 1️⃣4️⃣ Setup Production Config


```
sudo bench setup production [frappe-user]
bench setup nginx
```


### 🔄 Restart Supervisor:


```
sudo supervisorctl restart all
sudo bench setup production [frappe-user]
```


### 🌐 Access your ERPNext site via:

### http://[YOUR SERVER IP]

# 🎉 Congratulations!

###You have successfully installed ERPNext Version 15 on Ubuntu 24.04.

##✅ Start exploring the powerful features of ERPNext and streamline your business operations.


---

## 📬 **Get in Touch**

If you have any questions or need assistance, feel free to contact me:

🌐 **Website:** [https://ava-ertebat.ir](https://ava-ertebat.ir)  
📧 **Email:**  support@ava-ertebat.ir  
📧 **Email2:** omidswordfish@gmail.com 

📱 **WhatsApp:** [Chat with me on WhatsApp](https://wa.me/989163422797)

---

