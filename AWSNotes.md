| col1 | col2 | col3 |
| ---- | ---- | ---- |
|      |      |      |
|      |      |      |

# **AWS Notes**

## Identity and Access Management

### IAM

* Global Service
* Elements:
  * **Root Account**
    * created by default
    * NOT USE/SHARE
  * **IAM User**
    * Dont have to belong to a group
  * **Group**
    * Only contains Users - NOT Groups
  * **Policies**
    * JSON document with permissions
* Least privileges principles

#### Password Policy

* Min lenght
* Specific char types
* Allow IAM user to change password
* Force user to change password after a time
* Prevent reuse

#### MFA

* Recommended (At least for root)
* May be Virtual or Physical MFA

### AWS Access

* AWS Management Console

  * User/Password + MFA
* AWS API (CLI and SDK)

  * Access Keys (Key ID + Secret Access Key)
* Access Keys

  * User manage access keys, generated with Management Consol
    * Access Key ID
    * Secret Access Key

#### AWS CLI

* Use shell
* Direct access to public API
* Scripts
* Open Source: [https://github.com/aws/aws-cli](https://github.com/aws/aws-cli)
* Built on Python SDK

#### SDK

* Set of libraries
* Language specific
* Programaticall Access
* Embedded in Apps
* SDKs:
  * Python
  * JS
  * Mobile SDK
  * IoT SDK
  * and more...

#### AWS CloudShell

* Not all regions

### Audit Permissions

#### IAM Credential Report

* Lists all users in your account and the status of their credentials:

  * passwords
  * access keys
  * MFA devices.
* Can be generated from

  * AWS Management Console
  * AWS SDKs
  * Command Line Tools
  * IAM API
* csv file

#### IAM Roles - Access Advisor

* Go to IAM - Roles - Access Advisor Tab
* Shows the services that the role can access
* Shows when those services were last accessed.
* Data can be used to remove unused permissions (least privilege)

## Shared Responsibility Model

| AWS                   | User                                    |
| --------------------- | --------------------------------------- |
| Security OF the Cloud | Security IN the Cloud                   |
| All Infrastructure    | User, groups, roles, MFA, Key rotation. |
|                       | How to use infrastructure               |

## EC2

* EC2 instance = VM
* EBS = Volumes

### EC2 Config

* OS (AMI)
* CPU
* RAM
* Storage
* Network (public IP)
* Firewall Rules (Security Groups)
* Boot script: User Data (run as root)
* Key Pair:

  * Linux/MAC .pem
  * Windows .ppk (putty)
* EBS root volume delete on termination true by default
* Stopped Instance: no charge

  * But EBS volumes YES
  * Public IPv4 changes if started

#### Instance Types

### m5.2xlarge

| m: Class | 5: Generation | 2xlarge: size |
| -------- | ------------- | ------------- |


#### Classes

| General Purpose                                 |       M,Mac,T       | Compute<br />Memory<br />Networking | Web Servers<br />Code Repositories                                                   |
| ----------------------------------------------- | :-----------------: | :---------------------------------- | :----------------------------------------------------------------------------------- |
| Compute Optimized                               |          C          | Compute                             | Batch Processing<br />Media Transcoding<br />Scientific Modeling<br />Gaming Servers |
| Memory Optimized                                | R,X,High Memory, z | Memory                              | Databases<br />in-memory caches<br />real time big data analytics                    |
| Accelerated Computing                           | P,G,Trn,Inf,DL,F,VT | Co-Processors (GPU)                 | Generative AI<br />Video Transcoding<br />Deep Learning                              |
| Storage Optimized                               |        I,D,H        | low-latency IOPS                    | Transactional Databases (OLTP)<br />Distributed FS<br />Real time Analytics          |
| HPC Optimized<br />(High Performance Computing) |         Hpc         | High Performances Processors        | Complex Simulation<br />Deep Learning                                                |


Security Groups

* Multiple Instances
* Locked down to Region / VPC combination
* Live outside EC2
* Goot practise:
  * Separate SG for SSH
  * If "timeout" -> SG issue
  * If "connections refuse" -> App error or not launched
* Can refer to other SG
* Ports to Know
  * 22 = SSH, SFTP
  * 21 = FTP
  * 80 = HTTP
  * 443 = HTTPS
  * 3389 = RDP (Windows)

Connect to Instances

SSH 

Linux / Mac

ssh -i key.pem ec2-user@< IP or URL >

Unprotected key file = ERROR, 	FIX: chmod 0400 key.pem

Windows:

Putty


EC2 Instance Connect

* Browser based SSH connection
* No need ssh key (automatically generated internally)
* Need SSH opened in SG
* NEVER STORE KEY id AND SECRET IN EC2, use a Role


EC2 Purchase Options

On-demand

* Seconds (Windows, Linux) . Hours (Others)
* No long-term commitments
* Full control over instance lifecycle
* Short-term irregulaqr workloads that cannot be interrupted.

Reserved

* 1 or 3 years
* Committed instance configuration (type, region, tenancy, OS)
* Payment options:
  * All upfront
  * Partial upfront
  * No upfront
* Scope: Region or AZ
* Offering class:
  * Standard : can be modified but cannot be exchanged
  * Convertible: can change type, fammily, OS, scope, tenancy (66% discount).
* Steady state usage app (e.g DB), long workloads
* Can buy and sell in Marketplace

Saving Plans

* 1 or 3 years
* Discount baed on long term usage (up to 72%)
* Committed amount of usage in USD per hour
* Usage beyond saving plan billed at on-demand rate
* Locked for specifig fammily and region
* Flexible across: Size, OS, Tenancy (dedicated host by default)

Spot Instances

* Most cost-efficient (90%)
* Workloads resilient to failuer:
  * Batch jobs
  * Data Analysis
  * Image Processing
* NO for critical jobs or DBs

Dedicated Hosts

* On-demand
* Reserved (1,3 years)
* Most expensive

Dedicated Instances

* Hardware dedicated to account
* Share hardware with other instance of same account
* No control over placement - Can be moved HW if stopped/started

Capacity Reservation

* On demand in AZ, any duration
* No time commitment, no billing dis uounts
* To get discounts: combien with Regional Reserved and Saving Plans
* Charged at on-demand rates - running or not running
* Short-term uninterrupted workload in specific AZ
