# 2420 week12 Lab nginx and ufw Implementation

## Team Members 

- Darren Cheng
- Mihail Picus

## Procedures

This readme will assume that a droplet server called <strong>web-one</strong> has been created already. In all instances where the IP address is present, place your droplet server IP address there instead.

### 1. Install nginx on droplet server

ssh into your web-one server using `ssh -ssh -i ~/.ssh/DO2_key {user}@{IP_Address}`.

In web-one, update and upgade to ensure packages are up-to-date on your server, and then install nginx.

![image](https://user-images.githubusercontent.com/98194516/203473416-f508c310-b93c-49bb-8e24-a12d5ca3a602.png)

!![image](https://user-images.githubusercontent.com/98194516/203473456-08461049-a9ff-43ad-bd9d-1f851fe3ca95.png)

### 2. Create index.html

With WSL on your host machine, create an HTML document called index.html. This will be the page displayed by nginx.

You may find that storing these files in a a central directory may help. In my case, I've named a directory as W12 and store all the files needed in there.

![image](https://user-images.githubusercontent.com/98194516/203473540-9185d216-c4dd-46ec-acf0-4090db3b40ed.png)

Feel free to add anything you like beyond the initial HTML template.

![image](https://user-images.githubusercontent.com/98194516/203473561-fde82483-22f8-464b-bf3f-d1fd0c39be2b.png)

### 3. Create server block

With WSL on your host machine, create a server block.

![image](https://user-images.githubusercontent.com/98194516/203474074-74a1640d-6493-4071-bef0-fd1cec99ce0b.png)

Be sure to change out the IP address in this server block with the IP address of your droplet server. 

![image](https://user-images.githubusercontent.com/98194516/203474094-541ab73c-f3c4-4350-99e9-ca697593650c.png)

### 4. Move files to droplet via sftp and place in directories

Open a new WSL terminal and connect via sftp to droplet using `sftp -ssh -i ~/.ssh/DO2_key {user}@{IP_Address}`.

Use sftp to move the files from your host machine to your droplet server. The `put -r {folder}` command is useful here. 

![image](https://user-images.githubusercontent.com/98194516/203474939-07e9a33d-626f-4a84-983e-04b15e13f55d.png)

Make a directory that stores the HTML pages.

![image](https://user-images.githubusercontent.com/98194516/203476629-5005273f-a506-4430-9c0b-4740a9026525.png)

Copy the newly transferred index.html page into the HTML directory.

![image](https://user-images.githubusercontent.com/98194516/203477080-a4dd93b6-0871-4283-8e34-0959fe56619e.png)

Now copy the newly transferred server block into `/etc/nginx/sites-available/`.

![image](https://user-images.githubusercontent.com/98194516/203477180-8dac032a-e80a-41ea-aaaf-5b45fb7bfc07.png)

Create a soft link/symbolic link in `/etc/nginx/sites-enabled/`

![image](https://user-images.githubusercontent.com/98194516/203477573-5b09b5be-0871-4ede-98ac-a686c0476f51.png)

### 5. Restart nginx service

To ensure changes are saved, run `sudo systemctl daemon-reload`

![image](https://user-images.githubusercontent.com/98194516/203478984-a42a383e-e022-4c4c-aa20-9a6d0c7f18d6.png)

### 6. Check if it works by going to IP address in browser

In your preferred web browser, input IP address of droplet server and your index.html page should be shown.

![image](https://user-images.githubusercontent.com/98194516/203479499-74f663d3-e08d-4d19-a423-648a1eb44104.png)

Your nginx implementation is now complete!

### 7. Setup ufw 

ufw is a preinstalled package in ubuntu so need to install. 

To ensure connection issues don't occur, allow incoming HTTP and SSH connections.

![image](https://user-images.githubusercontent.com/98194516/203479922-64d93918-ad61-413b-b183-f8831fc2bce8.png)

When ready, run `sudo ufw enable` to turn on firewall.

![image](https://user-images.githubusercontent.com/98194516/203480087-87ed9b1a-f9da-49ed-acd0-a4ed31ae6a87.png)

Your firewall should be up and operational now!





