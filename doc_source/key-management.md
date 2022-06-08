# Key management<a name="key-management"></a>

In this section, you can find information about SSH keys, how to generate them, and how to rotate them\.

**Note**  
 Currently, Transfer Family does not accept elliptical curve keys \(keys beginning with `ecdsa`\)\.

**Topics**
+ [Generate SSH keys](#sshkeygen)
+ [Rotate SSH keys](#keyrotation)

## Generate SSH keys<a name="sshkeygen"></a>

You can set up your server to authenticate users using the service managed authentication method, where user names and SSH keys are stored within the service\. The user's public SSH key is uploaded to the server as a user's property\. This key is used by the server as part of a standard key\-based authentication process\. Each user can have multiple public SSH keys on file with an individual server\. For limits on number of keys that can be stored per user, see the [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) in the *AWS General Reference*\.

As an alternative to the service managed authentication method, you can authenticate users using a custom identity provider\. This allows you to plug in an existing identity provider using an Amazon API Gateway endpoint\. For more information, see [Authenticating using an API Gateway method](custom-identity-provider-users.md#authentication-custom-ip)\.

A server can only authenticate users using one method \(service managed or custom identity provider\), and that method cannot be changed after the server is created\.

**Topics**
+ [Creating SSH Keys on macOS, Linux, or UNIX](#macOS-linux-unix-ssh)
+ [Creating SSH Keys on Microsoft Windows](#windows-ssh)

### Creating SSH Keys on macOS, Linux, or UNIX<a name="macOS-linux-unix-ssh"></a>

On the macOS, Linux, or UNIX operating systems, you use the `ssh-keygen` command to create an SSH public key and SSH private key also known as a key pair\.

**To create SSH keys on a macOS, Linux, or UNIX operating system**

1. On macOS, Linux, or UNIX operating systems, open a command terminal\.

1. At the prompt, enter the following command: `ssh-keygen -P "" -m PEM -f key_name`\.
**Note**  
 `key_name` is the SSH key pair file name\.

   The following shows an example of the `ssh-keygen` output\.

   ```
   ssh-keygen -P "" -m PEM -f my_key_pair
   Generating public/private rsa key pair.
   
   Your identification has been saved in my_key_pair.
   Your public key has been saved in my_key_pair.pub.
   The key fingerprint is:
   SHA256:8tDDwPmanTFcEzjTwPGETVWOGW1nVz+gtCCE8hL7PrQ bob.amazon.com
   The key's randomart image is:
   +---[RSA 2048]----+
   |.o..  BOB&+o.    |
   |+ .. ++o%.Bo..   |
   |.   o.+=o* o.    |
   | . E o *+o       |
   |  . . . S o      |
   |   . o   . +     |
   |    .     o      |
   |                 |
   |                 |
   +----[SHA256]-----+
   ```

1. Navigate to the `key_name`\.pub file and open it\.

1. Copy the text and paste it in **SSH public key**\.

**Note**  
When you run the `ssh-keygen` command as shown preceding, it creates the public and private keys as files in the current directory\.

### Creating SSH Keys on Microsoft Windows<a name="windows-ssh"></a>

Windows uses a slightly different SSH key pair format\. The public key must be in the `PUB` format, and the private key must be in the `PPK` format\. On Windows, you can use PuTTYgen to create an SSH key pair in the appropriate formats\. You can also use PuTTYgen to convert a private key generated using `ssh-keygen` to a \.ppk file\.

**Note**  
If you present WinSCP with a private key file not in \.ppk format, that client offers to convert the key into \.ppk format for you\.

For a tutorial on creating SSH keys using PuTTYgen on Windows, see the [SSH\.com website](https://www.ssh.com/ssh/putty/windows/puttygen)\.

## Rotate SSH keys<a name="keyrotation"></a>

For security, we recommend the best practice of rotating your SSH keys\. Usually, this rotation is specified as a part of a security policy and is implemented in some automated fashion\. Depending upon the level of security, for a highly sensitive communication, an SSH key pair might be used only once\. Doing this eliminates any risk due to stored keys\. However, it is much more common to store SSH credentials for a period of time and set an interval that doesn't place undue burden on users\. A time interval of three months is common\.

There are two methods used to perform SSH key rotation:
+ On the console, you can upload a new SSH public key and delete an existing SSH public key\.
+ Using the API, you can update existing users by using the [DeleteSshPublicKey](https://docs.aws.amazon.com/transfer/latest/userguide/API_DeleteSshPublicKey.html) API to delete a user's Secure Shell \(SSH\) public key and the [ImportSshPublicKey](https://docs.aws.amazon.com/transfer/latest/userguide/API_ImportSshPublicKey.html) API to add a new Secure Shell \(SSH\) public key to the user's account\.

------
#### [ Console ]

**To perform a key rotation in the console**

1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/)\.

1. Navigate to the **Servers** page\.

1. Choose the identifier in the **Server ID** column to see the **Server details** page\.

1. Under **Users**, select the check box of the user whose SSH public key that you want to rotate, then choose **Actions**, and then choose **Add key** to see the **Add key** page\.

   or

   Choose the user name to see the **User details** page, and then choose **Add SSH public key** to see the **Add key** page\.

1. Enter the new SSH public key and choose **Add key**\.
**Important**  
The format of the SSH public key is `ssh-rsa <string>`\.

   You are returned to the **User details** page, and the new SSH public key that you just entered appears in the **SSH public keys** section\.

1. Select the check box of the old you key that you want to delete and then choose **Delete**\.

1. Confirm the deletion operation by entering the word `delete`, and then choose **Delete**\.

------
#### [ API ]

**To perform a key rotation using the API**

1. On macOS, Linux, or UNIX operating systems, open a command terminal\.

1.  Retrieve the SSH key that you want to delete by entering the following command: 

   ```
   aws transfer describe-user --server-id='serverID' --user-name='username'
   ```

   where *serverID* is the Server ID for your Transfer Family server, and *username* is your user name\.

    The command returns details about the user\. Copy the contents of the `"SshPublicKeyId":` field: you need to enter this value later in this procedure\. 

   ```
   "SshPublicKeys": [ { "SshPublicKeyBody": "public-key", "SshPublicKeyId": "keyID",
      "DateImported": 1621969331.072 } ],
   ```

1.  Next, import a new SSH key for your user\. At the prompt, enter the following command: 

   ```
   aws transfer import-ssh-public-key --server-id='serverID' --user-name='username'
      --ssh-public-key-body='public-key'
   ```

   Where the *public\-key* is the fingerprint of your new public key\. If the command is successful, no output is returned\.

1.  Finally, delete the old key by running the following command: 

   ```
   aws transfer delete-ssh-public-key --server-id='serverID' --user-name='username'
      --ssh-public-key-id='keyID-from-step-2'
   ```

    where *keyID\-from\-step\-2* is the key ID value you copied in step 2 of this procedure\. 

1. \(Optional\) Repeat step 2, to confirm that the old key no longer exists\.

------