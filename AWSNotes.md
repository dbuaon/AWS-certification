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

Instance Type

General Purpose

Compute Optimize

Memory Optimize

Storage Optimize
