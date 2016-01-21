[BACK TO HOME](README.md)

# Install Sendy in a subdomain in DigitalOcean

## Requirements
  * [DigitalOcean](https://digitalocean.com)
  * [DNSMadeEasy](https://cp.dnsmadeeasy.com)
  * [Sendy](https://sendy.co)
  * [Vesta](https://vestacp.com)
  * [Bitbucket](https://bitbucket.com)

## Installations Steps
  1. Login to DNSMadeEasy to find a domain e.g. nascentnexus.com

  2. Go to DNS dropdown option and choose "Managed DNS"

  ![Screen Shot 2016-01-21 at 10.01.36 PM](images/Screen Shot 2016-01-21 at 10.01.36 PM.png)

  3. Enter the domain you have in mind in the search box on the left

  ![Screen Shot 2016-01-21 at 10.02.48 PM](images/Screen Shot 2016-01-21 at 10.02.48 PM.png)

  4. You are now the domain control panel. We will go back to this after we create a digitalocean droplet

  5. Log in to your digitalocean account and click the "Create Droplet" button at the top

  6. Choose from options below

  ![Screen Shot 2016-01-21 at 9.59.49 PM](images/Screen Shot 2016-01-21 at 9.59.49 PM.png)
  ![Screen Shot 2016-01-21 at 10.00.13 PM](images/Screen Shot 2016-01-21 at 10.00.13 PM.png)

  7. In the hostname, enter the <subdomain.domain.com> you choose on the DNSMadeEasy step, e.g. sample.nascentnexus.com

  8. Wait for the droplet to finish installation

  ![Screen Shot 2016-01-21 at 10.07.36 PM](images/Screen Shot 2016-01-21 at 10.07.36 PM.png)

  9. When it's done copy the IP Address

  10. Go back to DNSMadeEasy domain control panel and enter the IP address when you create an "A Record"

  ![Screen Shot 2016-01-21 at 10.09.21 PM](images/Screen Shot 2016-01-21 at 10.09.21 PM.png)

  11. You should see the submdomain you created in the "A Records List"

  ![Screen Shot 2016-01-21 at 10.09.09 PM](images/Screen Shot 2016-01-21 at 10.09.09 PM.png)

  12. Open terminal and ping the submodomain you created to make sure the IP Address is correct

  ![Screen Shot 2016-01-21 at 10.11.34 PM](images/Screen Shot 2016-01-21 at 10.11.34 PM.png)

  13. We now SSH into our digitalocean droplet.

  ![Screen Shot 2016-01-21 at 10.12.29 PM]!(images/Screen Shot 2016-01-21 at 10.12.29 PM.png)

  14. We need to download [Vesta](https://vestacp.com/#install) for our sendy requirements

  15. Run this command in your terminal

  `wget http://vestacp.com/pub/vst-install.sh`

  16. You should get a file name `vst-install.sh`

  ![Screen Shot 2016-01-21 at 10.14.40 PM](images/Screen Shot 2016-01-21 at 10.14.40 PM.png)

  17. To run the installer, copy this command

  ```
  bash vst-install.sh --nginx no --apache yes --phpfpm no --vsftpd no --proftpd no --exim no --dovecot no --spamassassin no --clamav no --named no --iptables no --fail2ban no --mysql yes --postgresql no --remi no --quota no
  ```

  18. Press `y` to continue, and add intented email

  ![Screen Shot 2016-01-21 at 10.16.38 PM](images/Screen Shot 2016-01-21 at 10.16.38 PM.png)

  19. Just press `return/enter` to continue

  20. The setup will proceed. Wait until you see the screen below.

  ![Screen Shot 2016-01-21 at 10.20.38 PM](images/Screen Shot 2016-01-21 at 10.20.38 PM.png)

  21. Save the credentials to our horse table document

  22. Log in to your Vesta Control Panel. Click "Advanced" to see the options below, and proceed.

  ![Screen Shot 2016-01-21 at 10.23.19 PM](images/Screen Shot 2016-01-21 at 10.23.19 PM.png)

  23. Log in with the credentials you have earlier when you finish the installation.

  ![Screen Shot 2016-01-21 at 10.25.00 PM](images/Screen Shot 2016-01-21 at 10.25.00 PM.png)

  24. Go to the "WEB" menu, and "Edit" our domain.

  ![Screen Shot 2016-01-21 at 10.26.08 PM](images/Screen Shot 2016-01-21 at 10.26.08 PM.png)

  25. Click the "IP Address" option to pick the IP Address of our droplet and save

  ![Screen Shot 2016-01-21 at 10.26.32 PM](images/Screen Shot 2016-01-21 at 10.26.32 PM.png)

  26. Check your domain, it should output something like below

  ![Screen Shot 2016-01-21 at 10.27.44 PM](images/Screen Shot 2016-01-21 at 10.27.44 PM.png)

  27. SSH back to your droplet

  28. Go to your `public_html` folder of your domain, replace the `sample.nascentnexus.com` with your own subdomain.domain.com

  ```
  cd /home/admin/web/sample.nascentnexus.com/public_html
  ```

  ![Screen Shot 2016-01-21 at 10.34.23 PM](images/Screen Shot 2016-01-21 at 10.34.23 PM.png)

  29. Log in to your bitbucket account and go to our sendy repository

  30. Clone using `HTTPS` to our `public_html` folder

  ```
  git clone https://iamarmanjon@bitbucket.org/iamarmanjon/sendy.git
  ```

  31. You should be prompt by your bitbucket password, enter to proceed

  32. You should see the sendy folder in your current directory, go inside of this folder.

  ![Screen Shot 2016-01-21 at 10.32.48 PM](images/Screen Shot 2016-01-21 at 10.32.48 PM.png)

  33. We need to create an `uploads` folder and change it's permission

  ```
  mkdir uploads && chmod -R 777 uploads
  ```

  34. Go back to Vesta Control Panel, we need to create an account for our database

  35. Go to the `DB` menu and click the `(+) button` to add a database

  ![Screen Shot 2016-01-21 at 10.37.00 PM](images/Screen Shot 2016-01-21 at 10.37.00 PM.png)

  36. Enter the credentials, **note: the database name and user is on the right, they have admin as a prefix**

  ![Screen Shot 2016-01-21 at 10.37.50 PM](images/Screen Shot 2016-01-21 at 10.37.50 PM.png)

  37. Go back to our sendy folder

  38. We need to edit our sendy credentials, open `includes/config.php`

  ```
  nano includes/config.php
  ```

  39. We need to edit the following: `APP_PATH, $dbHost, $dbUser, $dbPass, $dbName`. We created those in our Vesta Control Panel.

  40. Make sure that the details you have are correct, below is a sample after the changes made.

  ![Screen Shot 2016-01-21 at 10.41.36 PM](images/Screen Shot 2016-01-21 at 10.41.36 PM.png)

  41. To save the document, `Control + X` then `Y` and `Enter/Return`

  42. We can now setup sendy by going to the our `APP_PATH` url e.g. sample.nascentnexus.com/sendy

  43. You should see the screen like this, enter the needed credentials from our horse stable

  ![Screen Shot 2016-01-21 at 10.43.47 PM](images/Screen Shot 2016-01-21 at 10.43.47 PM.png)

  44. If successful you should be on a login screen

  ![Screen Shot 2016-01-21 at 10.45.33 PM](images/Screen Shot 2016-01-21 at 10.45.33 PM.png)

  45. Enter the details and that ends our Sendy installation guide.

  ![Screen Shot 2016-01-21 at 10.47.03 PM](images/Screen Shot 2016-01-21 at 10.47.03 PM.png)






