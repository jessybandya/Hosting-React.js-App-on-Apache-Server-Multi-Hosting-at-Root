# Hosting React.js App on Apache Server

This guide will walk you through the steps to host a React.js app on an Apache server using XAMPP.

## Prerequisites

- XAMPP installed on your machine
- Basic understanding of React.js and Apache server configuration

## Steps

1. Configure Apache Server

   - Navigate to the `feng` folder under your XAMPP installation's `htdocs` directory. This is where your React app's build files should be placed.
   - Create an `.htaccess` file in the `feng` folder.
   - Add the following content to the `.htaccess` file:

     ```
      Options -MultiViews
     RewriteEngine On
     RewriteCond %{REQUEST_FILENAME} !-f
     RewriteRule ^ index.html [QSA,L]

     ```

   - Open the `httpd.conf` file located in the `xampp/apache/conf` directory.
   - Find the `<Directory>` section that corresponds to your `feng` folder.
   - Add the following line within the `<Directory>` block or at the bottom as as a new block:

     ```
     <Directory "C:/xampp/htdocs/feng">
      AllowOverride All
     </Directory>
     LoadModule rewrite_module modules/mod_rewrite.so
     ```

   - Open the `httpd-vhosts.conf` file located in the `xampp/apache/conf/extra` directory.
   - Add the following virtual host configuration at the end of the file:

     ```
     <VirtualHost *:80>
       DocumentRoot "C:/xampp/htdocs/feng"
       ServerName myreactapp.local
   
       <Directory "C:/xampp/htdocs/feng">
         Options Indexes FollowSymLinks Includes ExecCGI
         AllowOverride All
         Require all granted
       </Directory>
     </VirtualHost>
     ```

2. Restart Apache and MySQL

   - Restart both the Apache and MySQL servers through the XAMPP control panel.

3. Access Your React App

   - Open your web browser.
   - Visit `http://localhost/feng` (replace with the `ServerName` specified in the virtual host configuration) in the address bar.

## Conclusion

You have successfully hosted your React.js app on an Apache server using XAMPP. Now you can access your app by visiting the specified URL in your browser.

Please note that this guide assumes you are hosting the app on a local development environment. For production deployment, additional steps and configurations may be required.
