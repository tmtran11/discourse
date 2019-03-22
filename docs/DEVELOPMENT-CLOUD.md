# Discourse Development in Cloud  

**Set up Discourse in the cloud for development purpose** without the need for domain name, mail server, and prior knowledge of Rails or Linux shell.  

This tutorial uses **AWS** as the cloud provider. Register as a new user, and you will be free-tier eligible. AWS Free Tier includes 750 hours of Linux and Windows t2.micro instances each month for one year. To stay within the Free Tier, use only EC2 Micro instances.  

## Create New Cloud Server  
- Sign up for AWS and create your new cloud server.  
- In EC2 Console, launch a new **Ubuntu 18.04 LTS x64** instance:  
   Step 1: Choose AMI
   > Search for Ubuntu 18.04 LTS x64
   Step 2: Choose Instance Type
   > Choose t2.micro for free-tier eleigible
   Step 3: Configure Instance
   > Skip  
   Step 4: Add Storage
   > Increase storage to 16 GB
   Step 5: Add Tags
   > Skip
   Step 6: Configure Security Group
   > Enable port 22 (SSH), port 80 (HTTP), port 443(HTTPS), and port 3000  
   Step 7: Review and Launch
   > Download key pair to SSH into the instance    
  
   Connect to your server via its **Public IPv4** address using SSH, or [Putty][put] on Windows.  
   Login as **ubuntu**  
  
## Install  

```
# Elevate to root user. You will need to be root through the rest of the setup and bootstrap process  
sudo -s  

# Install dependencies  
bash <(wget -qO- https://raw.githubusercontent.com/techAPJ/install-rails/master/linux)  

# Clone from discourse repository, or from your folk folder, into ~/discourse  
git clone https://github.com/discourse/discourse.git ~/discourse  

# Setup database  
sudo -u postgres createuser -s root  
```

## Bootstrap  

```
# Install gems  
cd ~/discourse  
source ~/.bashrc  
bundle install  
bundle exec rake db:create db:migrate  
RAILS_ENV=test bundle exec rake db:create db:migrate  

# Start Rails server*  
bundle exec rails server --binding=0.0.0.0  
```

#### --> Success! Open Discourse on port 3000 of your server.  
  
