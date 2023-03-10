# Key management<a name="key-management"></a>

In this section, you can find information about SSH keys, including how to generate them and how to rotate them\.

**Note**  
AWS Transfer Family accepts RSA, ECDSA, and ED25519 keys\.

This section also covers how to generate and manage Pretty Good Privacy \(PGP\) keys\. 

**Topics**
+ [Supported algorithms for user and server keys](#key-algorithms)
+ [Generate SSH keys](#sshkeygen)
+ [Rotate SSH keys](#keyrotation)
+ [Generate and manage PGP keys](#pgp-key-management)
+ [Supported PGP clients](#pgp-key-clients)

## Supported algorithms for user and server keys<a name="key-algorithms"></a>

The following key algorithms are supported for use within AWS Transfer Family:
+ For ED25519: `ssh-ed25519`
+ For RSA:
  + `rsa-sha2-256`
  + `rsa-sha2-512`
+ For ECDSA:
  + `ecdsa-sha2-nistp256`
  + `ecdsa-sha2-nistp384`
  + `ecdsa-sha2-nistp521`

**Note**  
We support `ssh-rsa` with SHA1 for our older security policies \(all policies except for [TransferSecurityPolicy\-2022\-03](security-policies.md#security-policy-transfer-2022-03)\)\.

## Generate SSH keys<a name="sshkeygen"></a>

You can set up your server to authenticate users using the service managed authentication method, where usernames and SSH keys are stored within the service\. The user's public SSH key is uploaded to the server as a user's property\. This key is used by the server as part of a standard key\-based authentication process\. Each user can have multiple public SSH keys on file with an individual server\. For limits on number of keys that can be stored per user, see the [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) in the *AWS General Reference*\.

As an alternative to the service managed authentication method, you can authenticate users using a custom identity provider\. This allows you to plug in an existing identity provider using an Amazon API Gateway endpoint\. For more information, see [Authenticating using an API Gateway method](custom-identity-provider-users.md#authentication-custom-ip)\.

A server can only authenticate users using one method \(service managed or custom identity provider\), and that method cannot be changed after the server is created\.

**Topics**
+ [Creating SSH Keys on macOS, Linux, or Unix](#macOS-linux-unix-ssh)
+ [Creating SSH Keys on Microsoft Windows](#windows-ssh)

### Creating SSH Keys on macOS, Linux, or Unix<a name="macOS-linux-unix-ssh"></a>

On the macOS, Linux, or Unix operating systems, you use the `ssh-keygen` command to create an SSH public key and SSH private key also known as a key pair\.

**Note**  
For a tutorial on creating SSH keys using PuTTYgen on Windows, see the [SSH\.com website\.](https://www.ssh.com/ssh/putty/windows/puttygen)\.

**To create SSH keys on a macOS, Linux, or Unix operating system**

1. On macOS, Linux, or Unix operating systems, open a command terminal\.

1. AWS Transfer Family accepts RSA\-, ECDSA\-, and ED25519\-formatted keys\. Choose the appropriate command based on the type of key\-pair you are generating\.
**Note**  
In the following examples, we do not specify a passphrase: in this case, the tool asks you to enter your passphrase and then repeat it to verify\. Creating a passphrase offers better protection for your private key, and might also improve overall system security\. You cannot recover your passphrase: if you forget it, you must create a new key\.  
However, if you are generating a server host key, you *must* specify an empty passphrase, by specifying the `-N ""` option in the command \(or by pressing **Enter** twice when prompted\), because Transfer Family servers cannot request a password at start\-up\.
   + To generate an RSA 4096\-bit key pair:

     ```
     ssh-keygen -t rsa -b 4096 -f key_name
     ```
   + To generate an ECDSA 521\-bit key\-pair \(ECDSA has bit sizes of 256, 384, and 521\):

     ```
     ssh-keygen -t ecdsa -b 521 -f key_name
     ```
   + To generate an ED25519 key pair:

     ```
     ssh-keygen -t ed25519 -f key_name
     ```
**Note**  
 `key_name` is the SSH key pair file name\.

   The following shows an example of the `ssh-keygen` output\.

   ```
   ssh-keygen -t rsa -b 4096 -f key_name
   Generating public/private rsa key pair.
   
   Enter passphrase (empty for no passphrase): 
   Enter same passphrase again:
   Your identification has been saved in key_name.
   Your public key has been saved in key_name.pub.
   The key fingerprint is:
   SHA256:8tDDwPmanTFcEzjTwPGETVWOGW1nVz+gtCCE8hL7PrQ bob.amazon.com
   The key's randomart image is:
   +---[RSA 4096]----+
   |    . ....E      |
   | .   = ...       |
   |. . . = ..o      |
   | . o +  oo =     |
   |  + =  .S.= *    |
   | . o o ..B + o   |
   |     .o.+.* .    |
   |     =o*+*.      |
   |    ..*o*+.      |
   +----[SHA256]-----+
   ```
**Note**  
When you run the `ssh-keygen` command as shown preceding, it creates the public and private keys as files in the current directory\.

1. Navigate to the `key_name.pub` file and open it\.

1. Copy the text and paste it in **SSH public key** for the service\-managed user\.

   1. Open the AWS Transfer Family console at [https://console\.aws\.amazon\.com/transfer/](https://console.aws.amazon.com/transfer/), then select **Servers** from the navigation pane\.

   1. On the **Servers** page, select the **Server ID** for server that contains the user that you want to update\.

   1. Select the user for which you are adding a public key\.

   1. In the **SSH public keys** pane, choose **Add SSH public key**\.  
![\[The AWS Transfer Family console, showing the user details for a selected user.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/edit-user-add-key-01.png)

   1. Paste the text of the public key you generated into the SSH public key text box, and then choose **Add key**\.  
![\[The AWS Transfer Family console, showing the Add key page for adding a public key.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/edit-user-add-key-02.png)

      The new key is listed in the SSH public key pane\.  
![\[The AWS Transfer Family console, showing the newly added public key in the SSH public keys section.\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/edit-user-add-key-03.png)

### Creating SSH Keys on Microsoft Windows<a name="windows-ssh"></a>

Windows uses a slightly different SSH key pair format\. The public key must be in the `PUB` format, and the private key must be in the `PPK` format\. On Windows, you can use PuTTYgen to create an SSH key pair in the appropriate formats\. You can also use PuTTYgen to convert a private key generated using `ssh-keygen` to a `.ppk` file\.

**Note**  
If you present WinSCP with a private key file not in `.ppk` format, that client offers to convert the key into `.ppk` format for you\.

For a tutorial about creating SSH keys by using PuTTYgen on Windows, see the [SSH\.com website](https://www.ssh.com/ssh/putty/windows/puttygen)\.

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

   Choose the username to see the **User details** page, and then choose **Add SSH public key** to see the **Add key** page\.

1. Enter the new SSH public key and choose **Add key**\.
**Important**  
The format of the SSH public key depends on the type of key you generated\.  
For RSA keys, the format is `ssh-rsa string`\.
For ED25519 keys, the format is `ssh-ed25519 string`\.
For ECDSA keys, the key begins with `ecdsa-sha2-nistp256`, `ecdsa-sha2-nistp384`, or `ecdsa-sha2-nistp521`, depending on the size of the key you generated\. The beginning string is then followed by `string`, similar to the other key types\.

   You are returned to the **User details** page, and the new SSH public key that you just entered appears in the **SSH public keys** section\.

1. Select the check box of the old you key that you want to delete and then choose **Delete**\.

1. Confirm the deletion operation by entering the word `delete`, and then choose **Delete**\.

------
#### [ API ]

**To perform a key rotation using the API**

1. On macOS, Linux, or Unix operating systems, open a command terminal\.

1.  Retrieve the SSH key that you want to delete by entering the following command\. To use this command, replace `serverID` with the server ID for your Transfer Family server, and replace `username` with your username\.

   ```
   aws transfer describe-user --server-id='serverID' --user-name='username'
   ```

   The command returns details about the user\. Copy the contents of the `"SshPublicKeyId":` field\. You will need to enter this value later in this procedure\. 

   ```
   "SshPublicKeys": [ { "SshPublicKeyBody": "public-key", "SshPublicKeyId": "keyID",
      "DateImported": 1621969331.072 } ],
   ```

1.  Next, import a new SSH key for your user\. At the prompt, enter the following command\. To use this command, replace `serverID` with the server ID for your Transfer Family server, replace `username` with your username, and replace `public-key` with the fingerprint of your new public key\. 

   ```
   aws transfer import-ssh-public-key --server-id='serverID' --user-name='username'
      --ssh-public-key-body='public-key'
   ```

   ``If the command is successful, no output is returned\.

1.  Finally, delete the old key by running the following command\. To use this command, replace `serverID` with the server ID for your Transfer Family server, replace `username` with your username, and replace `keyID-from-step-2` with the key ID value that you copied in step 2 of this procedure 

   ```
   aws transfer delete-ssh-public-key --server-id='serverID' --user-name='username'
      --ssh-public-key-id='keyID-from-step-2'
   ```

1. \(Optional\) To confirm that the old key no longer exists, repeat step 2\.

------

## Generate and manage PGP keys<a name="pgp-key-management"></a>

You can use Pretty Good Privacy \(PGP\) decryption with the files that Transfer Family processes with workflows\. To use decryption in a workflow step, you must provide a PGP key\.

### Generate PGP keys<a name="generate-pgp-keys"></a>

The method that you use to generate your PGP keys depends on your operating system and the version of the key\-generation software that you're using\.

If you're using Linux or Unix, use your package installer to install `gpg`\. Depending on your Linux distribution, one of the following commands should work for you\.

```
sudo yum install gnupg
```

```
sudo apt-get install gnupg
```

For Windows or macOS, you can download what you need from [https://gnupg\.org/download/](https://gnupg.org/download/)\.

After you install your PGP key generator software, you run the `gpg ‐‐gen-key` command to generate a key pair\.  

**Note**  
Make sure to choose RSA as the key type\.

The following are some useful subcommands for `gpg`:
+ `gpg --help` – This command lists the available options and might include some examples\.
+ `gpg --list-keys` – This command lists the details for all of the key pairs that you have created\.
+ `gpg --fingerprint` – This command lists the details for all of your key pairs, including each key's fingerprint\.
+ `gpg --export -a user-name` – This command exports the public key portion of the key for the `user-name` that was used when the key was generated\.

### Manage PGP keys<a name="manage-pgp-keys"></a>

To manage your PGP keys, you must use AWS Secrets Manager\.

**Note**  
Your secret name includes your Transfer Family server ID\. This means you should have already identified or created a server *before* you can store your PGP key information in AWS Secrets Manager\.

If you want to use one key and passphrase for all of your users, you can store the PGP key block information under the secret name `aws/transfer/server-id/@pgp-default`, where `server-id` is the ID for your Transfer Family server\. This default key is used if there is no key where the `user-name` matches the user that is executing the workflow\. 

Alternatively, you can create a key for a specific user\. In this case, the format for the secret name is `aws/transfer/server-id/user-name`, where `user-name` matches the user that is running the workflow for a Transfer Family server\.

**Note**  
You can store a maximum of 3 PGP private keys, per Transfer Family server, per user\.

**To configure PGP keys for use with decryption**

1. Generate a PGP key pair by running the following command and answering all of the prompts\.

   ```
   gpg --gen-key
   ```
**Important**  
During the key\-generation process, you must provide a passphrase and an email address\. Make sure to take note of these values\. You must provide the passphrase when you enter the key's details into AWS Secrets Manager later in this procedure\. And you must provide the same email address to export the private key in the next step\.

1. Run the following command to export the private key\. To use this command, replace `private.pgp` with the name of the file in which to save the private key block, and `marymajor@example.com` with the email address that you used when you generated the key pair\.

   ```
   gpg --output private.pgp --armor --export-secret-key marymajor@example.com
   ```

1. <a name="store-pgp-key-details"></a>Use AWS Secrets Manager to store your PGP key\.

   1. Sign in to the AWS Management Console and open the AWS Secrets Manager console at [https://console\.aws\.amazon\.com/secretsmanager/](https://console.aws.amazon.com/secretsmanager/)\.

   1. In the left navigation pane, choose **Secrets**\. 

   1. On the **Secrets** page, choose **Store a new secret**\.

   1. On the **Choose secret type** page, for **Secret type**, select **Other type of secret**\.

   1. In the **Key/value pairs** section, choose the **Key/value** tab\.
      + **Key** – Enter **PGPPrivateKey**\.
**Note**  
You must enter the **PGPPrivateKey** string exactly: do not add any spaces before or between characters\.
      + **value** – Paste the text of your private key into the value field\. You can find the text of your private key in the file \(for example, `private.pgp`\) that you specified when you exported your key earlier in this procedure\. The key begins with `-----BEGIN PGP PRIVATE KEY BLOCK-----` and ends with `-----END PGP PRIVATE KEY BLOCK-----`\.
**Note**  
Make sure that the text block contains only the private key and does not contain the public key as well\.

   1. Select **Add row** and in the **Key/value pairs** section, choose the **Key/value** tab\.
      + **Key** – Enter **PGPPassphrase**\.
**Note**  
You must enter the **PGPPassphrase** string exactly: do not add any spaces before or between characters\.
      + **value** – Enter the passphrase you used when you generated your PGP key pair\.  
![\[\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/pgp-secrets-01.png)
**Note**  
You can add up to 3 sets of keys and passphrases\. To add a second set, add two new rows, and enter **PGPPrivateKey2** and **PGPPassphrase2** for the keys, and paste in another private key and passphrase\. To add a third set, key values must be **PGPPrivateKey3** and **PGPPassphrase3**\.

   1. Choose **Next**\.

   1. On the **Configure secret** page, enter a name and description for your secret\.
      + If you're creating a default key, that is, a key that can be used by any Transfer Family user, enter **aws/transfer/*server\-id*/@pgp\-default**\. Replace `server-id` with the ID of the server that contains the workflow that has a decrypt step\.
      + If you're creating a key to be used by a specific Transfer Family user, enter **aws/transfer/*server\-id*/*user\-name***\. Replace `server-id` with the ID of the server that contains the workflow that has a decrypt step, and replace `user-name` with the name of the user that's running the workflow\. The `user-name` is stored in the identity provider that the Transfer Family server is using\.

   1. Choose **Next** and accept the defaults on the **Configure rotation** page\. Then choose **Next**\.

   1. On the **Review** page, choose **Store** to create and store the secret\.

The following screenshot shows the details for the user **marymajor** for a specific Transfer Family server\. This example shows three keys and their corresponding passphrases\.

![\[\]](http://docs.aws.amazon.com/transfer/latest/userguide/images/pgp-secrets-02.png)

## Supported PGP clients<a name="pgp-key-clients"></a>

The following clients have been tested with Transfer Family and can be used to generate PGP keys, and to encrypt files that you intend to decrypt with a workflow\.
+ **Gpg4win \+ Kleopatra**\. Gpg4win 4\.0\.4 contains GnuPG 2\.3\.8\. 
**Important**  
If you are using **Gpg4win \+ Kleopatra**, you must use the **GnuPG** command\-line tool to pass the `--openpgp` flag\.
+ Major **GnuPG** versions: 2\.3, 2\.2, and 2\.0

Note that other PGP clients might work as well, but only the clients mentioned here have been tested with Transfer Family\.