# Penetration Testing

## Table of Contents

- [Penetration Testing](#penetration-testing)
  - [Table of Contents](#table-of-contents)
  - [Curriculum](#curriculum)
    - [01. First Day as a Junior Pentester](#01-first-day-as-a-junior-pentester)
    - [02. Your First External Network Pentest](#02-your-first-external-network-pentest)
    - [03. Your First Web Application Pentest](#03-your-first-web-application-pentest)
    - [04. Your First API Pentest](#04-your-first-api-pentest)
    - [05. Your First Internal Network Pentest](#05-your-first-internal-network-pentest)
    - [06. Your First Active Directory Pentest](#06-your-first-active-directory-pentest)
    - [07. Privilege Escalation \& Attack Chaining](#07-privilege-escalation--attack-chaining)
    - [08. Vulnerability Research \& Custom Exploitation](#08-vulnerability-research--custom-exploitation)
    - [09. Your First Professional Pentest Report](#09-your-first-professional-pentest-report)
    - [10. Your First Cloud \& Container Pentest](#10-your-first-cloud--container-pentest)

## Curriculum

### 01. First Day as a Junior Pentester
You’ll get a new client assignment, set up Kali Linux, Burp Suite, and your VPN, then read exactly which systems the client has allowed you to test. Before touching anything, you’ll check who to contact if something goes wrong and write down the tests you plan to run.

### 02. Your First External Network Pentest
Now you’ll take the client’s approved domain and IP addresses, find their public-facing hosts with DNS tools, and use Nmap to see which ports and services answer. You’ll check what each exposed service is running, look for known security issues, and confirm any suspected problems before reporting them.

### 03. Your First Web Application Pentest
Next you’ll test the client’s shopping website itself. You’ll use Burp Suite to follow what happens when customers log in, search for products, view orders, and pay, then check whether someone could see another customer’s data or change a price they shouldn’t be able to change.

### 04. Your First API Pentest
After testing the website in a browser, you’ll test the requests it sends to the server. You’ll import the API’s OpenAPI file into Postman, use Burp Repeater to change order IDs and account fields, and check whether the server accepts requests from the wrong customer or trusts a price supplied by the browser.

### 05. Your First Internal Network Pentest
This time the client gives you access to a company test network. You’ll use Nmap to find Windows and Linux machines, inspect services such as SMB, RDP, and SSH, and check whether shared folders, old software, or weak permissions let a normal user reach information they shouldn’t see.

### 06. Your First Active Directory Pentest
Once you’re inside the test network, you’ll look at how the company manages Windows users and computers through Active Directory. You’ll use BloodHound and domain queries to find who belongs to which groups, which accounts have powerful permissions, and whether those permissions expose other machines or accounts.

### 07. Privilege Escalation & Attack Chaining
You’ll start with a low-privilege test account on a Windows or Linux machine and check what it can read, run, and change. Using tools such as winPEAS and linPEAS in a lab, you’ll identify unsafe permissions and show how one confirmed weakness can lead to access that account was never meant to have.

### 08. Vulnerability Research & Custom Exploitation
When you find an unfamiliar service or software version, you’ll look up its CVEs in NVD and vendor advisories, read the conditions that make a vulnerability possible, and test a suitable proof of concept in a safe lab. You’ll also write small Python or Bash scripts to repeat checks and organize results.

### 09. Your First Professional Pentest Report
You’ll turn the problems you verified into a report a client can actually fix. For each one, you’ll include the affected URL or host, the exact request or command, what happened, why it matters, and what the developer or administrator should change. You’ll then repeat the same test after they apply a fix.

### 10. Your First Cloud & Container Pentest
You’ll work in an approved AWS or Azure test account and a Docker lab. You’ll check who can access storage, which services are exposed to the internet, what permissions cloud accounts and containers have, and whether a mistaken setting reveals data or gives someone more access than intended.