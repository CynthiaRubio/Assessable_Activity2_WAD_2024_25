DAW Assessable Exercise 2
=========================

Exercise 1
----------

1. Download the lab keys and adjust their permissions: `chmod 600 labsuser.pem`
2. Open the lab and create a new security group allowing inbound traffic on ports 22 and 80.
3. Create an Ubuntu EC2 instance, with the vockey keypair, using the security group we just created.
4. Create an elastic IP and assign it to the instance.
5. From the terminal, run: `ssh -i labsuser.pem ubuntu@`_instance_name_.
6. Install available updates: `sudo apt-get update`.
7. Install apache2: `sudo apt-get install apache2`.
8. Install npm: `sudo apt-get install npm`.
9. Install required Node modules: `sudo npm -g pm2 express`.
10. Clone the git repository: `git clone `_link_.
11. Enter the newly created directory.
12. Modify package.json: `nano package.json`
13. Before the _dependencies_ section, add: `homepage: "http://`_instance_name_`"`.
14. Within the project folder, run: `npm install`.
15. And then run: `npm run build`. This creates a folder with the project.
16. Run the project with: `sudo pm2 start npm --name "vite-server" -- run dev -- --host`
17. In the folder containing the Apache virtual hosts configurations, create a copy of the default configuration: `sudo cp 000-default.conf adivina.conf`.
18. Edit the file: `sudo nano adivina.conf`.
19. Uncomment `severName` and fill in with the public DNS name of our instance. Comment the `DocumentRoot`line, and add the `proxyPass` and `proxyPassReverse` directives.
20. Save your changes.
21. Enable the Apache2 proxy module: `sudo a2enmod proxy proxy_http`.
22. Check the list of enabled virtual hosts: `ll /etc/apache2/sites-enabled`.
23. Disable the default virtual host: `sudo a2dissite 000-default.conf`.
24. Enable our new virtual host: `sudo a2ensite adivina.conf`.
25. Restart apache2: `sudo systemctl reload apache2`.
26. In your web browser, visit `http://`_instance_name_ to verify the deployment.
