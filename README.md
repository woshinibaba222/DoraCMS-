# DoraCMS File Upload Vulnerability

## Vulnerability Description

DoraCMS User Management allows the upload of avatars for any user, enabling the alteration of uploaded avatars to HTML files that can execute XSS statements. Additionally, it permits the insertion of malicious links into uploaded images, deceiving users into clicking and downloading malicious programs.

## Affected Versions

DoraCMS version 2.1.8

## Source Code Download Link

https://github.com/doramart/DoraCMS

## Reproduction Steps:

Access the user management interface and randomly edit the details of a user.

![1](https://github.com/woshinibaba222/DoraCMS-/assets/55568679/421b3b02-7553-47e5-bf7e-7ab17642e026)

Click on the avatar in the image and choose a picture to upload.

![2](https://github.com/woshinibaba222/DoraCMS-/assets/55568679/a3d188e5-bb47-4464-9326-f5682dc5349a)

![3](https://github.com/woshinibaba222/DoraCMS-/assets/55568679/1ebc182f-bb64-4eaa-9f7f-ffa6e520b9a9)

Modify the request packet as shown in the image.

Change the file extension of the image to HTML in the request packet as shown in the picture.

![4](https://github.com/woshinibaba222/DoraCMS-/assets/55568679/2c78306a-8877-4018-8f26-d5f1d3ac0749)

![5](https://github.com/woshinibaba222/DoraCMS-/assets/55568679/1b485dd9-2ae3-4e9a-be2b-568f01ac33e1)

Append XSS statements at the end; here, I will make the following selection.
<script>alert(document.cookie)</script>
#Popup cookie

![6](https://github.com/woshinibaba222/DoraCMS-/assets/55568679/3f7bf6e3-c654-40f2-9ac2-5ba389340669)

Continuously send.

You can see that the upload was successful.

![10](https://github.com/woshinibaba222/DoraCMS-/assets/55568679/4f6890b3-6da9-4090-a7e5-ecefed661688)

Click on the update button as shown in the picture.

![7](https://github.com/woshinibaba222/DoraCMS-/assets/55568679/bdd4e1ef-a482-41d9-b002-6b357ea723aa)

Let's go back and review the request history in Burp. You can see the path to the logo. Now, concatenate the address and access it.

http://127.0.0.1:8080/static/upload/images/20231123/1700705529363061526.html

![8](https://github.com/woshinibaba222/DoraCMS-/assets/55568679/8aac5cd9-8a58-403e-9fbe-b7193262963e)

XSS popup successful.

![9](https://github.com/woshinibaba222/DoraCMS-/assets/55568679/7dfbe3e9-92ad-4060-8644-15350d68e360)


Attackers can also insert links they want system users to click into the image.

![11](https://github.com/woshinibaba222/DoraCMS-/assets/55568679/4eb66df6-ce02-4a1f-9e91-47ca33e8a75b)

Upload successful.

![13](https://github.com/woshinibaba222/DoraCMS-/assets/55568679/fc494cb9-7ba7-4578-8007-ae711e6c3e31)


Access  http://127.0.0.1:8080/static/upload/images/20231123/1700707364548976301.html

![12](https://github.com/woshinibaba222/DoraCMS-/assets/55568679/b3778c42-c677-423f-9282-2d26466560b7)


This way, attackers can leverage the trust of users in the system to download malicious programs or perform other attacks.
