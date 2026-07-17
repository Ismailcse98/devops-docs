## AWS EC2 Launch

This guide provides step-by-step instructions for creating an Amazon EC2 instance using the AWS Management Console.


---

## Step 1: Open the EC2 Dashboard

1. Search for **EC2** in the AWS search bar.
2. Select **EC2** from the services list.
3. The EC2 Dashboard will open.

---

## Step 2: Launch an Instance

1. Click **Launch Instance**.
2. Enter a name for your instance.

**Example:**

```text
Web-Server-01
```

---

## Step 3: Choose an Amazon Machine Image (AMI)

Select the operating system for your instance.

- Ubuntu Server

---

## Step 4: Choose an Instance Type

For testing or Free Tier usage, select:

```text
t2.micro OR t3.micro
```

---

## Step 5: Create or Select a Key Pair

1. Click **Create new key pair** (if you don't already have one).
2. Enter a key pair name.
3. Select:
   - **.pem** (Linux/macOS)
4. Download and store the key securely.

---

## Step 6: Configure Network Settings

Choose your VPC and subnet.

Recommended Security Group rules:

| Type | Port | Source |
|------|------|--------|
| SSH | 22 | My IP |
| HTTP | 80 | Anywhere |
| HTTPS | 443 | Anywhere |

---

## Step 7: Configure Storage

Default storage is sufficient for most basic workloads.

Example:

- **Volume Type:** gp3
- **Size:** 8 GB

Increase the size if your application requires more storage.

---

## Step 8: Review and Launch

Review all settings:

- Instance Name
- AMI
- Instance Type
- Key Pair
- Network Settings
- Security Group
- Storage

Click **Launch Instance**.

---

## Step 9: Connect to the Instance

### Ubuntu (SSH)

```bash
chmod 400 MyKeyPair.pem

ssh -i MyKeyPair.pem ubuntu@<PUBLIC_IP>
```

---

### EC2 Instance Connect

1. Select the instance.
2. Click **Connect**.
3. Choose **EC2 Instance Connect**.
4. Click **Connect**.