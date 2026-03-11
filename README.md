*This project has been created as part of the 42 curriculum by nramalan*

## Description

Born2BeRoot is a system administration project that focuses on setting up a fully functional Linux operating system from scratch. The project requires students to understand and implement core system administration concepts including partitioning schemes, security policies, firewall configuration, and user management. The goal is to gain practical knowledge of Linux system configuration, security hardening, and infrastructure management by deploying a complete virtual machine with a strict set of security requirements and predefined service installations.

## Instructions

### Compilation
This project does not require compilation as it involves system setup and configuration.

### Installation
1. Create a virtual machine using VirtualBox or UTM (depending on your system)
2. Install Debian Linux with the specified partitioning scheme
3. Configure security policies and firewall as per project requirements
4. Set up mandatory services including SSH and sudo
5. Configure user permissions and access control
6. Enable and configure monitoring/logging tools

### Execution
The system runs as a fully functional virtual machine. Access it through:
- SSH: `ssh <username>@<vm_ip_address>`
- VirtualBox/UTM graphical console
- Commands can be executed directly within the VM once authenticated

## Project Description

### Operating System Choice: Debian vs Rocky Linux

#### Why Debian?
**Advantages:**
- Stable and well-established with extensive community support
- Large package repository (over 60,000 packages)
- Simpler configuration for beginners
- Excellent documentation and tutorials available
- Default firewall (UFW) is more user-friendly than firewalld
- AppArmor is easier to configure than SELinux
- Wide hardware compatibility

**Disadvantages:**
- More conservative with software updates (older versions)
- Requires more manual configuration in some areas
- Less suited for enterprise environments compared to Rocky

#### Rocky Linux (Not Chosen)
**Advantages:**
- Enterprise-focused with extended support
- RHEL compatibility (important for professional environments)
- SELinux provides granular security control
- firewalld offers advanced networking capabilities
- Better suited for production systems

**Disadvantages:**
- Steeper learning curve for beginners
- Smaller package ecosystem
- More complex configuration

### Security & System Comparisons

#### AppArmor vs SELinux

**AppArmor (Debian Default):**
- Path-based mandatory access control
- Easier to understand and configure
- Profile syntax is more intuitive
- Faster to implement and debug
- Less granular but sufficient for most purposes
- Used in: Debian, Ubuntu, SUSE

**SELinux (Rocky Linux Default):**
- Type-based mandatory access control
- More granular and powerful
- Steeper learning curve
- Better for enterprise security requirements
- Allows deny rules and transitions
- Used in: Red Hat, CentOS, Rocky Linux

**Recommendation:** AppArmor was chosen for its ease of use and reduced complexity while still providing essential security features.

#### UFW vs firewalld

**UFW (Debian Default):**
- Simple command-line interface: `ufw allow/deny <service>`
- Frontend to iptables
- Easier for beginners to understand
- Suitable for single-machine configurations
- Configuration stored in simple text files

**firewalld (Rocky Linux Default):**
- Zone-based firewall management
- Better for complex network environments
- Supports dynamic rule changes without reloading
- XML-based configuration
- More overhead but more flexible

**Recommendation:** UFW was chosen for simplicity and direct control of incoming/outgoing traffic.

#### VirtualBox vs UTM

**VirtualBox:**
- Cross-platform (Windows, macOS, Linux)
- Free and open-source
- Excellent performance
- Wide compatibility with snapshots and cloning
- Larger community and documentation
- More features for advanced users

**UTM:**
- Native macOS support with M-series chip optimization
- Lightweight and integrated with macOS
- Better performance on Apple Silicon
- Limited to macOS
- Simpler UI

**Recommendation:** VirtualBox was chosen for cross-platform compatibility and broader support, though UTM is excellent for macOS users with Apple Silicon.

### Main Design Choices

#### Partitioning Scheme
- Logical Volume Management (LVM) for flexible disk allocation
- Separate partitions for `/boot`, `/home`, `/tmp`, `/var`, and `/var/log`
- Reduces risk of disk space issues and improves security
- Allows for better resource management and snapshots

#### Security Policies
- Strong password policies enforced via `/etc/login.defs`
- Sudo restricted to group "sudo" with strict access control
- SSH key-based authentication preferred over passwords
- Firewall rules configured to allow only necessary services
- Automatic logout for inactive sudo sessions
- Regular security updates and patches

#### User Management
- Root account disabled with password set to complex value
- Standard user account with sudo privileges
- Clear separation of responsibilities
- User groups for service isolation

#### Services Installed
- OpenSSH Server for remote access
- ufw for firewall management
- Monitoring tools for system statistics
- Boot-time scripts for startup processes
- Minimal service footprint to reduce attack surface

## Resources

### Documentation & References
- [Debian Official Documentation](https://www.debian.org/doc/)
- [Linux Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.pdf)
- [UFW Documentation](https://manpages.ubuntu.com/manpages/focal/man8/ufw.8.html)
- [AppArmor Documentation](https://gitlab.com/apparmor/apparmor/-/wikis/Documentation)
- [SSH Security Best Practices](https://linux.die.net/man/5/ssh_config)
- [Linux User Management Guide](https://linux.die.net/man/5/passwd)
- [VirtualBox User Manual](https://www.virtualbox.org/manual/)

### AI Usage
AI was used for the following purposes:
- **Documentation Writing:** Drafting comprehensive documentation for system setup and configuration
- **Troubleshooting:** Debugging configuration issues and providing solutions for common problems
- **Research:** Gathering information on security best practices and comparative analysis between different tools (Debian vs Rocky, AppArmor vs SELinux, etc.)
- **Code Review:** Validating bash scripts and configuration files for correctness and security
- **Project Structure:** Planning the overall project organization and requirements
- **Technical Explanations:** Understanding complex concepts like LVM, firewall rules, and mandatory access control systems

---

**Created as part of the 42 school curriculum - System Administration Project**
