### Setting up Multiple SSH Keys for Different GitHub Accounts on the Same System

This guide explains how to configure SSH keys to manage multiple GitHub accounts from one system. It will allow you to push code to different GitHub accounts without needing to re-authenticate each time.

---

### Step 1: Open Terminal

Open a terminal on your system.

---

### Step 2: Generate a New SSH Key

1. Run the following command to generate a new SSH key:

   ```bash
   ssh-keygen
   ```

2. When prompted for the file location to save the SSH key, provide a unique name to identify it, like so:

   ```bash
   Enter file in which to save the key (/home/user/.ssh/id_rsa): /home/user/.ssh/ssh-example
   ```

3. Next, it will prompt for a passphrase. You can set a passphrase for added security or simply press **Enter** to skip this step.

   ```bash
   Enter passphrase (empty for no passphrase):
   ```

After these steps, your SSH key pair will be generated and saved to the specified directory.

---

### Step 3: Verify and Copy the SSH Public Key

1. Navigate to the `.ssh` directory to check for the new key files:

   ```bash
   cd /home/user/.ssh
   ```

2. List the contents of the `.ssh` folder to confirm the new files (`ssh-example` and `ssh-example.pub`) exist:

   ```bash
   ls
   ```

3. To copy the public key, display its contents:

   ```bash
   cat ssh-example.pub
   ```

4. Copy the entire output displayed in the terminal (this is your public SSH key).

---

### Step 4: Add the SSH Key to GitHub

1. Open the GitHub account where you want to add this SSH key.
2. Go to **Settings** > **SSH and GPG keys** > click on **New SSH Key**.
3. Enter a title to identify the key (e.g., "Work Laptop Key") and paste the public key you copied earlier.
4. Click **Add SSH Key** to save it.

Now, your system is authorized to push code to this GitHub account.

---

### Step 5: Configure SSH for Multiple GitHub Accounts

1. Go back to your terminal and open the `.ssh` directory.
2. Create or edit a `config` file inside the `.ssh` folder:

   ```bash
   touch config
   gedit config  # Use any editor you prefer
   ```

3. Add the following configuration to the `config` file:

   ```plaintext
   Host github.com-ssh-example
       HostName github.com
       User git
       IdentityFile ~/.ssh/ssh-example
   ```

   - **Host**: Use a unique name for this GitHub account. This name will be used when cloning or pushing repositories.
   - **IdentityFile**: Set this to the file path of your private SSH key (`~/.ssh/ssh-example` in this example).

4. Save and close the file.

---

### Step 6: Clone and Work with Repositories Using the New SSH Key

1. To clone a repository using this SSH configuration, use the following format:

   ```bash
   git clone git@github.com:username/repository-name.git
   ```

   Here, replace `github.com` with the `Host` name you set in the SSH config file like `git@github.com-ssh-example`, and `username/repository-name` with the GitHub repository you want to clone.

   ```bash
   git clone git@github.com-ssh-example:username/repository-name.git
   ```

2. After cloning, you can make changes and push code to the repository using the correct GitHub account associated with this SSH key.

---

This setup allows you to manage multiple GitHub accounts on the same system seamlessly. Each time you work with a repository from a different account, specify the correct SSH key configuration in the clone command or remote URL as shown in Step 6.
