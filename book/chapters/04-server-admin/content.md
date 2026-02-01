# Chapter 4: Server Administration - Windows & Linux

---

## Chapter Overview

- **Domain**: Server Administration and Infrastructure Management
- **Estimated Study Time**: 7-8 hours
- **Prerequisites**: Chapter 2 (Core Networking Fundamentals), Basic operating system concepts
- **Difficulty Progression**: Beginner → Intermediate → Advanced → Expert

---

## Learning Objectives

By the end of this chapter, you will be able to:

1. **Describe** the key components and roles of Windows Server and Linux server environments (B)
2. **Explain** Active Directory concepts including users, groups, OUs, and Group Policy (B)
3. **Configure** essential server services including DNS, DHCP, and file sharing on both platforms (I)
4. **Implement** server hardening and patch management strategies (I)
5. **Analyze** server logs and performance metrics to **troubleshoot** system issues (A)
6. **Compare** virtualization platforms and **evaluate** their suitability for different scenarios (A)
7. **Design** a high-availability server infrastructure with load balancing and clustering (E)
8. **Assess** backup and disaster recovery strategies for enterprise server environments (E)

---

## Introduction

Server administration is a fundamental competency for IT management. Whether running critical government applications, hosting databases, or providing network services, servers form the backbone of organizational IT infrastructure. As an Assistant Director IT, you will oversee server environments, make procurement decisions, ensure service availability, and guide technical staff.

This chapter covers both Windows Server and Linux server administration, as most enterprise environments run a heterogeneous mix of both platforms. Understanding the strengths of each platform enables you to make informed decisions about which technology best fits specific use cases.

The concepts covered here connect directly to database management (Chapter 5), cloud computing (Chapter 9), and disaster recovery (Chapter 23). Mastering server administration fundamentals is essential for effective IT leadership.

---

## Section 4.1: Windows Server Fundamentals (B)

Microsoft Windows Server is the dominant enterprise server operating system in many government and corporate environments, providing identity services, file storage, application hosting, and more.

### 4.1.1 Windows Server Editions and Roles

**Current Windows Server Editions**:

| Edition | Use Case | Licensing |
|---------|----------|-----------|
| Standard | Physical or minimally virtualized | Per-core + CALs |
| Datacenter | Highly virtualized environments | Per-core + CALs, unlimited VMs |
| Essentials | Small businesses (≤25 users) | Per-server, no CALs |

**Common Server Roles**:
- **Active Directory Domain Services (AD DS)**: Identity and access management
- **DNS Server**: Domain name resolution
- **DHCP Server**: Dynamic IP address assignment
- **File and Storage Services**: Centralized file sharing
- **Web Server (IIS)**: Web application hosting
- **Remote Desktop Services**: Remote access and virtual desktops
- **Hyper-V**: Server virtualization

### 4.1.2 Active Directory Domain Services

Active Directory (AD) is the cornerstone of Windows enterprise environments, providing centralized identity management and policy enforcement.

**Key AD Components**:

**Domain**: A logical grouping of network objects (users, computers, groups) that share the same AD database.

**Forest**: A collection of one or more domains that share a common schema, configuration, and global catalog.

**Organizational Unit (OU)**: A container within a domain used to organize objects and apply Group Policy.

**Domain Controller (DC)**: A server that hosts AD DS and authenticates users and computers.

**Global Catalog**: A distributed data repository containing a searchable, partial representation of every object in every domain in a forest.

### Practical Example 4.1: AD Structure Design

**Scenario**: Design an AD structure for a government agency with headquarters and 5 regional offices.

**Proposed Structure**:

```
Forest: agency.gov
└── Domain: agency.gov
    ├── OU: Headquarters
    │   ├── OU: IT Department
    │   ├── OU: Finance
    │   ├── OU: HR
    │   └── OU: Operations
    ├── OU: Regional Offices
    │   ├── OU: Region-North
    │   ├── OU: Region-South
    │   ├── OU: Region-East
    │   ├── OU: Region-West
    │   └── OU: Region-Central
    ├── OU: Servers
    │   ├── OU: Domain Controllers
    │   ├── OU: File Servers
    │   └── OU: Application Servers
    └── OU: Service Accounts
```

**Design Rationale**:
- Single domain simplifies management
- OUs organized by function and geography
- Separate OUs for servers enable targeted policies
- Service accounts isolated for security

### 4.1.3 Group Policy Objects (GPOs)

Group Policy enables centralized configuration management for users and computers in an AD environment.

**GPO Processing Order** (LSDOU):
1. **L**ocal Policy
2. **S**ite Policy
3. **D**omain Policy
4. **O**U Policy (processed in hierarchical order)
5. **U**ser Policy (if different from computer)

**Common GPO Settings**:
- Password policies (complexity, length, expiration)
- Account lockout policies
- Software deployment
- Security settings (firewall, audit policies)
- Desktop settings (wallpaper, restrictions)
- Mapped drives and printers

### Practical Example 4.2: GPO Implementation

**Scenario**: Create GPOs for security baseline compliance.

**Security GPOs**:

| GPO Name | Link | Key Settings |
|----------|------|--------------|
| Password Policy | Domain | Min length: 12, Complexity: Enabled, Max age: 90 days |
| Account Lockout | Domain | Threshold: 5 attempts, Duration: 30 min |
| Workstation Security | Workstations OU | Windows Firewall enabled, Auto-updates |
| Server Security | Servers OU | Audit policy, Remote access restrictions |
| Restricted Groups | Domain | Local Admins = Domain Admins only |

**GPO Command Reference**:
```powershell
# Create new GPO
New-GPO -Name "Security Baseline" -Comment "Organization security settings"

# Link GPO to OU
New-GPLink -Name "Security Baseline" -Target "OU=Workstations,DC=agency,DC=gov"

# Generate GPO report
Get-GPOReport -Name "Security Baseline" -ReportType HTML -Path "C:\Reports\SecurityGPO.html"
```

### 4.1.4 DNS and DHCP Configuration

**DNS Server Configuration**:

DNS integrates closely with Active Directory, providing name resolution for domain resources.

**DNS Zone Types**:
- **Primary Zone**: Authoritative, read-write copy
- **Secondary Zone**: Read-only copy for redundancy
- **AD-Integrated Zone**: Stored in AD, replicates automatically

**Common DNS Records**:
| Record Type | Purpose | Example |
|-------------|---------|---------|
| A | IPv4 address mapping | server01.agency.gov → 10.1.1.10 |
| AAAA | IPv6 address mapping | server01.agency.gov → 2001:db8::10 |
| CNAME | Alias (canonical name) | www → webserver01.agency.gov |
| MX | Mail exchanger | agency.gov → mail.agency.gov (priority 10) |
| SRV | Service location | _ldap._tcp.agency.gov (for AD) |
| PTR | Reverse lookup | 10.1.1.10 → server01.agency.gov |

**DHCP Server Configuration**:

| Scope Element | Description | Example |
|---------------|-------------|---------|
| Scope | IP address range | 10.1.10.100 - 10.1.10.200 |
| Subnet Mask | Network mask | 255.255.255.0 |
| Default Gateway | Router address | 10.1.10.1 |
| DNS Servers | Name resolution | 10.1.1.10, 10.1.1.11 |
| Lease Duration | IP assignment period | 8 days |
| Exclusions | Reserved addresses | 10.1.10.1 - 10.1.10.10 |
| Reservations | MAC-to-IP binding | 00:1A:2B:3C:4D:5E → 10.1.10.50 |

### Practical Example 4.3: DNS Troubleshooting

**Scenario**: Users cannot resolve internal server names but can browse the Internet.

**Troubleshooting Steps**:

1. **Verify client DNS settings**:
   ```cmd
   ipconfig /all
   ```
   Check DNS server addresses point to internal DNS servers

2. **Test DNS resolution**:
   ```cmd
   nslookup internalserver.agency.gov
   nslookup internalserver.agency.gov 10.1.1.10
   ```

3. **Test DNS server**:
   ```cmd
   nslookup agency.gov 10.1.1.10
   ```

4. **Check DNS server logs**:
   Event Viewer → Applications and Services Logs → DNS Server

5. **Verify zone configuration**:
   DNS Manager → Forward Lookup Zones → Verify records exist

6. **Common Issues**:
   - Forwarders not configured (external resolution works, internal fails)
   - Zone transfer failure (secondary zones outdated)
   - Stale DNS records (old server entries)

---

## Section 4.2: Linux Server Administration (B)

Linux servers power much of the Internet infrastructure and are common in government environments for web servers, databases, and specialized applications.

### 4.2.1 Linux Distributions

**Enterprise Distributions**:

| Distribution | Support | Package Manager | Use Case |
|--------------|---------|-----------------|----------|
| Red Hat Enterprise Linux (RHEL) | Commercial | dnf/yum (RPM) | Enterprise, commercial support |
| Ubuntu Server LTS | Canonical | apt (DEB) | Cloud, containers, general purpose |
| CentOS Stream | Community | dnf/yum (RPM) | Development, testing |
| Rocky Linux | Community | dnf/yum (RPM) | RHEL-compatible, free |
| Debian | Community | apt (DEB) | Stability, servers |
| SUSE Linux Enterprise | Commercial | zypper (RPM) | Enterprise, SAP environments |

### 4.2.2 Linux File System Hierarchy

Understanding the Linux file system is essential for server administration.

| Directory | Purpose |
|-----------|---------|
| / | Root directory |
| /bin | Essential user binaries |
| /boot | Boot loader files |
| /dev | Device files |
| /etc | Configuration files |
| /home | User home directories |
| /lib | Essential shared libraries |
| /opt | Optional application software |
| /proc | Virtual filesystem for process info |
| /root | Root user home directory |
| /sbin | System binaries |
| /tmp | Temporary files |
| /usr | User utilities and applications |
| /var | Variable data (logs, spool, cache) |

### 4.2.3 Command Line Operations

**Essential Commands**:

**File Operations**:
```bash
ls -la              # List files with details
cd /path/to/dir     # Change directory
cp source dest      # Copy files
mv source dest      # Move/rename files
rm filename         # Remove files
mkdir dirname       # Create directory
cat filename        # Display file contents
less filename       # Page through file
head -n 20 filename # First 20 lines
tail -f /var/log/syslog # Follow log file
```

**File Permissions**:
```bash
# Permission format: rwxrwxrwx (owner-group-other)
# r=4, w=2, x=1

chmod 755 file      # rwxr-xr-x
chmod 640 file      # rw-r-----
chmod u+x file      # Add execute for owner
chown user:group file  # Change ownership
```

**User Management**:
```bash
useradd -m username     # Create user with home directory
passwd username         # Set password
usermod -aG sudo user   # Add user to sudo group
userdel -r username     # Delete user and home directory
groups username         # List user's groups
```

### Practical Example 4.4: Linux User Administration

**Scenario**: Create a new administrator account with sudo privileges.

**Steps**:
```bash
# Create user
sudo useradd -m -s /bin/bash -c "John Smith - IT Admin" jsmith

# Set password
sudo passwd jsmith

# Add to sudo group (Ubuntu/Debian)
sudo usermod -aG sudo jsmith

# Or add to wheel group (RHEL/CentOS)
sudo usermod -aG wheel jsmith

# Verify groups
groups jsmith
# Output: jsmith : jsmith sudo

# Test sudo access
su - jsmith
sudo whoami
# Output: root
```

### 4.2.4 Service Management with systemd

Modern Linux distributions use systemd for service management.

**Common systemctl Commands**:
```bash
# Service status
systemctl status sshd

# Start/stop/restart
systemctl start sshd
systemctl stop sshd
systemctl restart sshd
systemctl reload sshd   # Reload config without restart

# Enable/disable at boot
systemctl enable sshd
systemctl disable sshd

# List services
systemctl list-units --type=service
systemctl list-unit-files --state=enabled

# View logs
journalctl -u sshd
journalctl -u sshd -f    # Follow
journalctl -u sshd --since "1 hour ago"
```

### Practical Example 4.5: Deploying a Web Server

**Scenario**: Install and configure Apache web server on Ubuntu.

**Steps**:
```bash
# Update packages
sudo apt update

# Install Apache
sudo apt install apache2 -y

# Start and enable
sudo systemctl start apache2
sudo systemctl enable apache2

# Verify status
sudo systemctl status apache2

# Configure firewall
sudo ufw allow 'Apache Full'

# Test
curl http://localhost

# Create virtual host
sudo nano /etc/apache2/sites-available/mysite.conf
```

**Virtual Host Configuration**:
```apache
<VirtualHost *:80>
    ServerName www.agency.gov
    ServerAlias agency.gov
    DocumentRoot /var/www/agency
    ErrorLog ${APACHE_LOG_DIR}/agency-error.log
    CustomLog ${APACHE_LOG_DIR}/agency-access.log combined
</VirtualHost>
```

```bash
# Enable site
sudo a2ensite mysite.conf
sudo systemctl reload apache2
```

### 4.2.5 Package Management

**APT (Debian/Ubuntu)**:
```bash
apt update              # Update package lists
apt upgrade             # Upgrade installed packages
apt install package     # Install package
apt remove package      # Remove package
apt search keyword      # Search packages
apt show package        # Package details
apt autoremove          # Remove unused dependencies
```

**DNF/YUM (RHEL/CentOS/Rocky)**:
```bash
dnf check-update        # Check for updates
dnf upgrade             # Upgrade packages
dnf install package     # Install package
dnf remove package      # Remove package
dnf search keyword      # Search packages
dnf info package        # Package details
dnf clean all           # Clear cache
```

### 4.2.6 SSH Configuration

SSH (Secure Shell) is the primary method for remote Linux server administration.

**SSH Server Configuration** (`/etc/ssh/sshd_config`):
```
# Recommended security settings
Port 22
PermitRootLogin no
PasswordAuthentication no    # Use key-based auth
PubkeyAuthentication yes
MaxAuthTries 3
ClientAliveInterval 300
ClientAliveCountMax 2
AllowUsers admin jsmith
```

**SSH Key-Based Authentication**:
```bash
# Generate key pair (on client)
ssh-keygen -t ed25519 -C "admin@agency.gov"

# Copy public key to server
ssh-copy-id user@server

# Or manually
cat ~/.ssh/id_ed25519.pub | ssh user@server "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"

# Set permissions on server
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

---

## Section 4.3: Server Hardening and Security (I)

Server hardening reduces the attack surface by disabling unnecessary services, applying security configurations, and implementing access controls.

### 4.3.1 Windows Server Hardening

**Security Baseline Implementation**:

1. **Install only required roles and features**
2. **Apply security patches promptly**
3. **Configure Windows Firewall**
4. **Enable audit policies**
5. **Restrict administrative access**
6. **Disable unnecessary services**

**Key Hardening Steps**:

| Category | Action | Implementation |
|----------|--------|----------------|
| Services | Disable unnecessary | Services.msc → Disable Print Spooler if not needed |
| Firewall | Enable and configure | Windows Defender Firewall → Advanced Settings |
| Updates | Configure automatic | WSUS or Windows Update for Business |
| Accounts | Rename/disable default | Rename Administrator, disable Guest |
| RDP | Restrict access | NLA enabled, specific user access |
| Audit | Enable logging | GPO → Computer Config → Audit Policy |

**PowerShell Security Commands**:
```powershell
# Disable SMBv1
Set-SmbServerConfiguration -EnableSMB1Protocol $false

# Enable audit policy
auditpol /set /category:"Logon/Logoff" /success:enable /failure:enable

# Check open ports
Get-NetTCPConnection -State Listen

# Review local administrators
Get-LocalGroupMember -Group "Administrators"
```

### 4.3.2 Linux Server Hardening

**Essential Hardening Steps**:

1. **Keep system updated**:
```bash
# Automatic security updates (Ubuntu)
sudo apt install unattended-upgrades
sudo dpkg-reconfigure unattended-upgrades
```

2. **Configure firewall (UFW)**:
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
sudo ufw status verbose
```

3. **Disable root SSH login**:
```bash
# /etc/ssh/sshd_config
PermitRootLogin no
PasswordAuthentication no
```

4. **Implement fail2ban**:
```bash
sudo apt install fail2ban
sudo systemctl enable fail2ban
```

**fail2ban configuration** (`/etc/fail2ban/jail.local`):
```ini
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
bantime = 3600
findtime = 600
```

5. **Remove unnecessary packages**:
```bash
# List installed packages
dpkg --list

# Remove unused packages
sudo apt autoremove
```

### Practical Example 4.6: Security Audit Checklist

**Scenario**: Perform a security audit on a Linux server.

**Checklist**:

| Check | Command | Expected Result |
|-------|---------|-----------------|
| OS updated | `apt list --upgradable` | No critical updates |
| Root SSH disabled | `grep PermitRootLogin /etc/ssh/sshd_config` | no |
| Password auth disabled | `grep PasswordAuthentication /etc/ssh/sshd_config` | no |
| Firewall enabled | `ufw status` | Status: active |
| Unnecessary services | `systemctl list-units --state=running` | Minimal services |
| Open ports | `ss -tuln` | Only required ports |
| Failed logins | `grep "Failed" /var/log/auth.log \| tail -20` | Review attempts |
| Sudo users | `grep -Po '^sudo.+:\K.*$' /etc/group` | Expected users only |
| SUID files | `find / -perm -4000 2>/dev/null` | Known binaries only |

### 4.3.3 Patch Management

Effective patch management balances security with system stability.

**Patch Management Process**:

1. **Assessment**: Identify applicable patches
2. **Testing**: Test patches in non-production environment
3. **Approval**: Change management review
4. **Deployment**: Apply patches in maintenance window
5. **Verification**: Confirm successful installation
6. **Documentation**: Record changes

**Windows Patch Management Options**:
- Windows Server Update Services (WSUS)
- Microsoft Endpoint Configuration Manager (MECM/SCCM)
- Windows Update for Business
- Third-party patch management tools

**Linux Patch Management**:
```bash
# Check available updates
apt list --upgradable

# Install security updates only (Ubuntu)
sudo apt install unattended-upgrades
sudo unattended-upgrade --dry-run  # Preview
sudo unattended-upgrade            # Apply

# Schedule automatic updates
sudo systemctl enable apt-daily.timer
sudo systemctl enable apt-daily-upgrade.timer
```

---

## Section 4.4: Virtualization Technologies (I)

Virtualization enables running multiple operating systems on a single physical server, improving resource utilization and flexibility.

### 4.4.1 Virtualization Concepts

**Hypervisor Types**:

**Type 1 (Bare-Metal)**:
- Runs directly on hardware
- Better performance
- Examples: VMware ESXi, Microsoft Hyper-V, KVM, Citrix Hypervisor

**Type 2 (Hosted)**:
- Runs on host operating system
- Easier setup, lower performance
- Examples: VMware Workstation, VirtualBox, Parallels

**Virtualization Terminology**:
| Term | Definition |
|------|------------|
| Host | Physical machine running hypervisor |
| Guest/VM | Virtual machine running on hypervisor |
| vCPU | Virtual CPU allocated to VM |
| vRAM | Memory allocated to VM |
| Virtual Switch | Software network switch for VMs |
| Snapshot | Point-in-time capture of VM state |
| Template | Master image for deploying VMs |
| vMotion/Live Migration | Move running VM between hosts |

### 4.4.2 VMware vSphere

VMware vSphere is the leading enterprise virtualization platform.

**Key Components**:
- **ESXi**: Bare-metal hypervisor
- **vCenter Server**: Centralized management
- **vSphere Client**: Web-based management interface
- **vMotion**: Live VM migration
- **HA (High Availability)**: Automatic VM restart on failure
- **DRS (Distributed Resource Scheduler)**: Automatic load balancing
- **vSAN**: Software-defined storage

### Practical Example 4.7: VM Provisioning

**Scenario**: Create a new Windows Server VM in vSphere.

**Specifications**:
| Resource | Allocation |
|----------|------------|
| vCPUs | 4 |
| Memory | 16 GB |
| Disk | 100 GB (thin provisioned) |
| Network | Production VLAN |
| OS | Windows Server 2022 |

**Steps**:
1. Right-click cluster → New Virtual Machine
2. Select "Create a new virtual machine"
3. Assign name and folder
4. Select compute resource (cluster/host)
5. Select datastore
6. Configure hardware (CPU, memory, disk, network)
7. Mount Windows Server ISO
8. Power on and install OS

### 4.4.3 Microsoft Hyper-V

Hyper-V is Microsoft's virtualization platform, integrated into Windows Server.

**Hyper-V Features**:
- **Generation 1 vs Generation 2 VMs**: Gen 2 supports UEFI, Secure Boot
- **Virtual Hard Disks**: VHD (legacy) and VHDX (current)
- **Checkpoints**: VM state snapshots (use carefully in production)
- **Live Migration**: Move VMs between hosts
- **Replica**: DR replication to another site

**PowerShell Management**:
```powershell
# Create VM
New-VM -Name "Server01" -MemoryStartupBytes 8GB -Generation 2 -Path "D:\VMs"

# Configure CPU
Set-VMProcessor -VMName "Server01" -Count 4

# Add virtual hard disk
New-VHD -Path "D:\VMs\Server01\Server01.vhdx" -SizeBytes 100GB -Dynamic
Add-VMHardDiskDrive -VMName "Server01" -Path "D:\VMs\Server01\Server01.vhdx"

# Connect to network
Connect-VMNetworkAdapter -VMName "Server01" -SwitchName "Production"

# Start VM
Start-VM -Name "Server01"

# Get VM status
Get-VM | Select-Object Name, State, CPUUsage, MemoryAssigned
```

### 4.4.4 KVM and Proxmox

**KVM (Kernel-based Virtual Machine)**:
- Open-source hypervisor built into Linux kernel
- Managed via libvirt and tools like virt-manager
- Command-line tools: virsh, qemu-img

**Proxmox VE**:
- Open-source virtualization platform
- Combines KVM and LXC containers
- Web-based management interface
- High availability and clustering
- Popular in government and education

**virsh Commands**:
```bash
# List VMs
virsh list --all

# Start/stop VM
virsh start vmname
virsh shutdown vmname

# Create snapshot
virsh snapshot-create-as --domain vmname --name "pre-update"

# View VM info
virsh dominfo vmname
```

---

## Section 4.5: Monitoring and Performance (A)

Effective monitoring ensures system reliability, identifies issues before they impact users, and supports capacity planning.

### 4.5.1 Windows Server Monitoring

**Performance Monitor**:
- Real-time and historical performance data
- Custom Data Collector Sets
- Key counters:
  - Processor: % Processor Time
  - Memory: Available MBytes, Pages/sec
  - Disk: % Disk Time, Avg. Disk Queue Length
  - Network: Bytes Total/sec

**Event Viewer**:
- Windows Logs: Application, Security, System
- Applications and Services Logs

**PowerShell Monitoring**:
```powershell
# CPU usage
Get-Counter '\Processor(_Total)\% Processor Time' -SampleInterval 2 -MaxSamples 5

# Memory usage
Get-Counter '\Memory\Available MBytes'

# Disk usage
Get-Counter '\PhysicalDisk(_Total)\% Disk Time'

# Event log queries
Get-EventLog -LogName System -Newest 50 -EntryType Error
Get-WinEvent -LogName Security -MaxEvents 100 | Where-Object {$_.Id -eq 4625}
```

### 4.5.2 Linux Server Monitoring

**Essential Monitoring Commands**:

```bash
# System overview
top
htop        # Enhanced version (install first)

# CPU info
cat /proc/cpuinfo
mpstat 1 5  # CPU stats every 1 second, 5 times

# Memory usage
free -h
vmstat 1 5

# Disk usage
df -h           # Filesystem usage
du -sh /var/*   # Directory sizes
iostat -x 1 5   # Disk I/O stats

# Network
netstat -tuln   # Listening ports
ss -tuln        # Modern alternative
iftop           # Network traffic (install)

# Process management
ps aux
ps aux --sort=-%mem | head -10  # Top memory users
```

**Log Analysis**:
```bash
# System logs
journalctl -xe              # Recent entries with explanation
journalctl -u sshd -f       # Follow service log
journalctl --since "1 hour ago"

# Traditional log files
tail -f /var/log/syslog     # System log
tail -f /var/log/auth.log   # Authentication
grep "error" /var/log/syslog
```

### Practical Example 4.8: Performance Troubleshooting

**Scenario**: Users report slow application performance on a Linux server.

**Investigation Steps**:

1. **Check overall system load**:
```bash
uptime
# Output: load average: 8.52, 7.89, 6.43 (high for 4-core system)
```

2. **Identify resource bottleneck**:
```bash
top
# Check: %CPU, %MEM, load average
# Look for processes consuming high resources
```

3. **Check memory**:
```bash
free -h
# If low available memory + high swap usage = memory pressure
```

4. **Check disk I/O**:
```bash
iostat -x 1 5
# High %util or await = disk bottleneck
```

5. **Check network**:
```bash
sar -n DEV 1 5
# High rxkB/s or txkB/s may indicate saturation
```

6. **Identify problematic process**:
```bash
ps aux --sort=-%cpu | head -10
# Or
pidstat 1 5
```

### 4.5.3 Centralized Monitoring Solutions

**Enterprise Monitoring Platforms**:

| Tool | Type | Best For |
|------|------|----------|
| Nagios | Open-source | Traditional infrastructure |
| Zabbix | Open-source | Enterprise monitoring |
| Prometheus + Grafana | Open-source | Cloud-native, metrics |
| Datadog | Commercial | Cloud and hybrid |
| Microsoft SCOM | Commercial | Windows-centric |
| SolarWinds | Commercial | Network and server |

---

## Section 4.6: High Availability and Clustering (A)

High availability ensures systems remain operational despite component failures.

### 4.6.1 Windows Server Clustering

**Failover Clustering**:
- Multiple servers (nodes) working as a single system
- Shared storage (SAN, iSCSI, S2D)
- Automatic failover of workloads
- Uses quorum for cluster decisions

**Cluster Components**:
- Cluster Nodes: Individual servers
- Cluster Network: Communication between nodes
- Cluster Shared Volumes (CSV): Shared storage
- Cluster Roles: Workloads that can fail over

### Practical Example 4.9: SQL Server Always On

**Scenario**: Implement high availability for SQL Server.

**Architecture**:
```
[SQL Node 1: Primary] ←── Synchronous Replication ──→ [SQL Node 2: Secondary]
                                                              ↓
                                                    Asynchronous Replication
                                                              ↓
                                            [SQL Node 3: DR Site Secondary]
```

**Key Components**:
- Windows Server Failover Cluster (WSFC)
- Availability Group containing databases
- Availability Group Listener (virtual network name)

### 4.6.2 Linux High Availability

**Pacemaker and Corosync**:
- Pacemaker: Cluster resource manager
- Corosync: Cluster communication layer

**DRBD (Distributed Replicated Block Device)**:
- Real-time block-level replication
- Active-passive or active-active configurations

**HAProxy**:
- Load balancing and high availability proxy
- Health checks and automatic failover

### 4.6.3 Load Balancing

**Load Balancing Methods**:
| Method | Description | Use Case |
|--------|-------------|----------|
| Round Robin | Sequential distribution | Equal capacity servers |
| Least Connections | Send to server with fewest connections | Variable request duration |
| IP Hash | Consistent server based on client IP | Session persistence |
| Weighted | Proportional to server capacity | Mixed capacity servers |

**Windows Network Load Balancing (NLB)**:
- Built into Windows Server
- Layer 4 load balancing
- Best for stateless applications

**HAProxy Configuration Example**:
```
frontend web_frontend
    bind *:80
    default_backend web_servers

backend web_servers
    balance roundrobin
    option httpchk GET /health
    server web1 10.1.100.10:80 check
    server web2 10.1.100.11:80 check
    server web3 10.1.100.12:80 check
```

---

## Section 4.7: Backup and Recovery (E)

Backup and recovery capabilities are essential for business continuity and data protection.

### 4.7.1 Backup Strategies

**Backup Types**:

| Type | Description | Pros | Cons |
|------|-------------|------|------|
| Full | Complete copy of all data | Simple restore | Time and storage intensive |
| Incremental | Changes since last backup (any type) | Fast, efficient | Complex restore chain |
| Differential | Changes since last full backup | Faster restore than incremental | Grows over time |
| Synthetic Full | Combines full + incrementals | Fast, efficient | Requires processing |

**3-2-1 Backup Rule**:
- 3 copies of data
- 2 different storage media types
- 1 offsite copy

### 4.7.2 Windows Server Backup

**Windows Server Backup Features**:
- Block-level backup
- Bare metal recovery
- System state backup
- Application-aware (VSS)

**PowerShell Backup Commands**:
```powershell
# Install Windows Server Backup feature
Install-WindowsFeature Windows-Server-Backup

# Create backup policy
$policy = New-WBPolicy
$filespec = New-WBFileSpec -FileSpec "C:\Data"
Add-WBFileSpec -Policy $policy -FileSpec $filespec
$backupTarget = New-WBBackupTarget -NetworkPath "\\backup\share"
Add-WBBackupTarget -Policy $policy -Target $backupTarget
Set-WBSchedule -Policy $policy -Schedule 02:00

# Start backup
Start-WBBackup -Policy $policy
```

### 4.7.3 Linux Backup Solutions

**rsync**:
```bash
# Basic rsync backup
rsync -avz /data/ /backup/data/

# Remote backup
rsync -avz -e ssh /data/ user@backup:/backup/data/

# Incremental with hard links
rsync -avz --link-dest=/backup/yesterday /data/ /backup/today/
```

**tar and cron**:
```bash
# Create compressed archive
tar -czvf /backup/data-$(date +%Y%m%d).tar.gz /data/

# Cron job for daily backup
0 2 * * * /usr/local/bin/backup-script.sh
```

### Practical Example 4.10: Disaster Recovery Plan

**Scenario**: Design backup and recovery for a government agency.

**Backup Schedule**:

| Data Type | Frequency | Retention | Method |
|-----------|-----------|-----------|--------|
| System State | Daily | 30 days | Full |
| Database | Every 4 hours | 14 days | Full + Transaction logs |
| File Servers | Daily | 90 days | Incremental |
| Full System | Weekly | 52 weeks | Full image |

**Recovery Objectives**:
- RTO (Recovery Time Objective): 4 hours for critical systems
- RPO (Recovery Point Objective): 1 hour maximum data loss

**Recovery Testing**:
- Quarterly: Full system recovery test
- Monthly: File/folder recovery verification
- Weekly: Backup verification and integrity check

---

## Hands-on Labs

### Lab 4.1: Active Directory Setup

See [labs/lab-04-01-ad-setup.md](labs/lab-04-01-ad-setup.md) for complete lab instructions.

**Objective**: Install and configure Active Directory Domain Services, create OUs, users, and groups.

### Lab 4.2: Group Policy Implementation

See [labs/lab-04-02-group-policy.md](labs/lab-04-02-group-policy.md) for complete lab instructions.

**Objective**: Create and link GPOs for security baseline configuration.

### Lab 4.3: Linux Server Configuration

See [labs/lab-04-03-linux-config.md](labs/lab-04-03-linux-config.md) for complete lab instructions.

**Objective**: Install and configure a Linux web server with hardening.

### Lab 4.4: Server Monitoring Setup

See [labs/lab-04-04-monitoring.md](labs/lab-04-04-monitoring.md) for complete lab instructions.

**Objective**: Configure monitoring tools and create performance baselines.

### Lab 4.5: Backup and Recovery

See [labs/lab-04-05-backup-recovery.md](labs/lab-04-05-backup-recovery.md) for complete lab instructions.

**Objective**: Implement and test backup and recovery procedures.

---

## Chapter Summary

Key points covered in this chapter:

- Windows Server provides enterprise features including Active Directory for identity management, Group Policy for configuration, and integrated DNS/DHCP services.
- Active Directory structure uses domains, forests, OUs, and GPOs to organize and manage network resources with centralized policies.
- Linux servers offer flexibility and cost-effectiveness, with distributions like RHEL, Ubuntu, and Rocky Linux serving different enterprise needs.
- Linux administration relies on command-line proficiency for user management, service control with systemd, and package management with apt or dnf.
- Server hardening reduces attack surface through patching, firewall configuration, service minimization, and access controls on both platforms.
- Virtualization technologies (VMware vSphere, Hyper-V, KVM/Proxmox) enable efficient resource utilization and simplified management.
- Performance monitoring requires understanding key metrics (CPU, memory, disk, network) and using appropriate tools for each platform.
- High availability through clustering, replication, and load balancing ensures service continuity despite component failures.
- Backup strategies must balance RPO and RTO requirements with the 3-2-1 rule as a baseline.

---

## Key Takeaways

1. **Active Directory is central to Windows enterprise environments**: Understanding AD structure, GPOs, and security is essential for managing Windows infrastructure.

2. **Linux command-line proficiency is non-negotiable**: Even with GUI tools available, effective Linux administration requires strong CLI skills.

3. **Server hardening is not optional**: Both Windows and Linux servers must be hardened, patched, and monitored to maintain security.

4. **Virtualization is the standard**: Most enterprise servers run as VMs; understanding hypervisor technologies is essential for capacity planning and management.

5. **High availability requires planning**: Clustering, load balancing, and disaster recovery must be designed and tested before they're needed.

---

## Self-Assessment Questions

Answer these questions in your own words (2-3 paragraphs each):

1. **Design an Active Directory structure** for a government agency with headquarters and 10 regional offices. Include OU hierarchy, GPO strategy, and domain controller placement. (I/A)

2. **Compare VMware vSphere, Microsoft Hyper-V, and Proxmox** for a government virtualization project. What factors would influence your recommendation? (A)

3. **A Linux server is experiencing high load average and slow application response**. Describe your systematic troubleshooting approach, including specific commands and what you would look for. (A)

4. **Design a backup and disaster recovery strategy** for a government agency with 50 servers, 10TB of data, and RTO/RPO requirements of 4 hours/1 hour. Include backup schedule, retention, and recovery testing plan. (E)

5. **You are tasked with migrating a physical Windows Server 2012 R2 to a new virtual environment**. Outline your migration plan, including pre-migration checks, migration method, and post-migration validation. (E)

---

## Chapter MCQs

See [mcqs.md](mcqs.md) for complete MCQ set with:
- 55 Beginner (B) questions (25%)
- 77 Intermediate (I) questions (35%)
- 66 Advanced (A) questions (30%)
- 22 Expert (E) questions (10%)

Total: 220 MCQs

---

## References

- Microsoft. "Windows Server Documentation." 2025. https://docs.microsoft.com/en-us/windows-server/
- Microsoft. "Active Directory Domain Services Overview." 2025. https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/
- Red Hat. "Red Hat Enterprise Linux Documentation." 2025. https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/
- Ubuntu. "Ubuntu Server Guide." 2025. https://ubuntu.com/server/docs
- VMware. "vSphere Documentation." 2025. https://docs.vmware.com/en/VMware-vSphere/
- NIST. "SP 800-123 - Guide to General Server Security." 2008. https://csrc.nist.gov/publications/detail/sp/800-123/final
- CIS. "CIS Benchmarks." 2025. https://www.cisecurity.org/cis-benchmarks
- Linux Foundation. "Linux System Administration." 2024.

---

**Chapter Status**: Draft
**Last Updated**: 2026-02-01
**Author**: Content Development Team
**Reviewer**: Pending Technical Review
