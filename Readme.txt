============================================================
PROJECT README
============================================================

Project Name:
CODMGO – CODM Software

Project URL:
https://codmgo.codmsoftware.com

Company:
CODM Software

Repository Type:
Static Website (Landing Page)

Version Control:
Git & GitHub

============================================================
PROJECT DESCRIPTION
============================================================

CODMGO Landing Page is a static, responsive website created for
CODM Software under the CODMGO product/brand.

This repository contains the complete website source code along
with step-by-step instructions to deploy the project on a Linux
VPS using the Nginx web server with SSL enabled.

The project is designed to be:
- Lightweight and fast
- SEO-friendly
- Mobile, tablet, and desktop responsive
- Easy to deploy and maintain

============================================================
TECHNOLOGY STACK
============================================================

Frontend Technologies:
- HTML5
- CSS3
- JavaScript
- Bootstrap Framework

Server & Deployment:
- Ubuntu Linux VPS
- Nginx Web Server
- SSL (Let’s Encrypt via Certbot)

Version Control:
- Git
- GitHub Repository

============================================================
PROJECT FOLDER STRUCTURE
============================================================

codmgo.codmsoftware.com/
│
├── assets/
│   ├── css/        (Stylesheets)
│   ├── js/         (JavaScript files)
│   ├── img/        (Images)
│   └── vendor/     (Third-party libraries)
│
├── index.html      (Main website entry file)
├── README.txt      (Project documentation)
└── favicon.ico     (Website icon)

NOTE:
Only index.html and assets/ are required for production.
Git folders and system files should NOT exist on the live server.

============================================================
STEP-BY-STEP DEPLOYMENT GUIDE
============================================================

------------------------------------------------------------
STEP 1: CREATE SUBDOMAIN (DNS)
------------------------------------------------------------

Create a subdomain in your DNS provider.

Type: A
Host: codmgo
Points To: YOUR_VPS_IP
TTL: Default

Result:
codmgo.codmsoftware.com → VPS IP

------------------------------------------------------------
STEP 2: CONNECT TO VPS SERVER
------------------------------------------------------------

Login to your server using SSH:

ssh root@YOUR_VPS_IP

------------------------------------------------------------
STEP 3: CREATE PROJECT DIRECTORY
------------------------------------------------------------

Create the web root directory:

mkdir -p /var/www/codmgo.codmsoftware.com
cd /var/www/codmgo.codmsoftware.com

------------------------------------------------------------
STEP 4: CLONE PROJECT FROM GITHUB
------------------------------------------------------------

Clone the repository into the directory:

git clone YOUR_GITHUB_REPOSITORY_URL .

IMPORTANT:
After deployment, remove the .git folder for security.

------------------------------------------------------------
STEP 5: REMOVE UNNECESSARY FILES (PRODUCTION)
------------------------------------------------------------

Delete Git and system files:

rm -rf .git
rm -f .DS_Store

------------------------------------------------------------
STEP 6: SET FILE PERMISSIONS (CRITICAL)
------------------------------------------------------------

Correct permissions prevent 403 Forbidden errors.

chown -R www-data:www-data /var/www/codmgo.codmsoftware.com
chmod -R 755 /var/www/codmgo.codmsoftware.com

------------------------------------------------------------
STEP 7: CREATE NGINX CONFIGURATION
------------------------------------------------------------

Create Nginx config file:

nano /etc/nginx/sites-available/codmgo.codmsoftware.com

Paste the following configuration:

server {
    listen 80;
    server_name codmgo.codmsoftware.com;

    root /var/www/codmgo.codmsoftware.com;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}

Save and exit.

------------------------------------------------------------
STEP 8: ENABLE NGINX SITE
------------------------------------------------------------

Enable the configuration:

ln -s /etc/nginx/sites-available/codmgo.codmsoftware.com /etc/nginx/sites-enabled/

Test and reload Nginx:

nginx -t
systemctl reload nginx

------------------------------------------------------------
STEP 9: INSTALL SSL (HTTPS)
------------------------------------------------------------

Secure the website with SSL:

certbot --nginx -d codmgo.codmsoftware.com

After success, the website will load on HTTPS.

============================================================
COMMON ERRORS & FIXES
============================================================

403 Forbidden Error:
- Fix ownership and permissions
- Ensure index.html exists

404 Not Found:
- Check Nginx root path
- Ensure files are not inside nested folders

Page Not Working:
- Check Nginx config is enabled
- Verify DNS points to correct VPS IP

============================================================
CUSTOMIZATION GUIDE
============================================================

To update content:
- Edit index.html for text and structure
- Replace images in assets/img/
- Modify styles in assets/css/
- Update scripts in assets/js/

============================================================
MAINTENANCE & UPDATES
============================================================

- Use GitHub for version control
- Deploy updates manually or via CI/CD
- Reload Nginx after configuration changes
- SSL renews automatically via Certbot

============================================================
PROJECT STATUS
============================================================

✔ Subdomain Configured
✔ DNS Connected
✔ Website Deployed
✔ Nginx Configured
✔ SSL Enabled
✔ Production Ready

============================================================
SUPPORT
============================================================

For support, updates, or maintenance:
CODM Software – Web Development Team

============================================================
END OF FILE
============================================================
