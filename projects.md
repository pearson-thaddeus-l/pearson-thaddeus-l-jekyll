---
layout: default
title: "Projects"
permalink: /projects/
---

<h2 class="headline">Featured Projects</h2>

<p>
Welcome to my portfolio of featured work — a mix of builds, active automation, and ongoing experiments.
</p>

<div class="neon-border project-card">
  <h3>AWS RDS Encryption at Rest</h3>
  <p>
    Contract DevOps work on a live AWS platform, adding encryption at rest to existing Amazon RDS MySQL databases for a compliance effort. The engagement was a chance to go deeper on KMS, CloudFormation, and Multi-AZ while the application stayed online. Lower-environment databases are encrypted and serving traffic. Production is still ahead. In progress.
  </p>
  <p><strong>Tech:</strong> Amazon RDS, MySQL, AWS KMS, CloudFormation, Route 53, Multi-AZ, read replicas</p>
  <ul>
    <li>Inventoried the RDS fleet and published an encryption-by-service page for the primary, its replicas, and the application services that store data on them.</li>
    <li>Created a customer-managed KMS key in the test account, symmetric AES-256, with automatic annual rotation turned on.</li>
    <li>Stood up an isolated environment with the team scaffolder so the test did not run on the shared QA stack.</li>
    <li>Matched the non-production primary to the production layout before encrypting it: Multi-AZ on, one read replica added. The first CloudFormation update rolled back on an export conflict; retargeted the read-only names and reran it to completion.</li>
    <li>Brought up an encrypted replacement for the smaller application database, cut its name over, and confirmed the public sites loaded. Left the previous instance up for rollback.</li>
    <li>Repeated the cutover for the primary database in that environment. Application traffic there now uses the encrypted instance.</li>
    <li>Opened a draft infrastructure change so the database templates record the encrypted settings and stay in line with what is running.</li>
  </ul>
</div>

<div class="neon-border project-card">
  <h3>Synology DNS Implementation</h3>
  <p>
    Designed and implemented a local DNS infrastructure on the Synology RT6600ax router to support hostname resolution across a flat lab network. This project was a prerequisite to expanding the Proxmox cluster from a single node to a multi-node configuration, which requires reliable bi-directional hostname resolution between cluster members. The implementation involved deliberate architectural decisions around DNS placement for high availability, DHCP reservation management, and forward zone configuration built to mirror enterprise DNS practices in a lab environment.
  </p>
  <p><strong>Tech:</strong> Synology RT6600ax, Synology DNS Server, BIND9 (underlying), DHCPv4, DNS Forward Zone, Proxmox VE</p>
  <ul>
    <li>Evaluated DNS hosting options including a dedicated Proxmox LXC running BIND9, the Synology NAS, and the Synology RT6600ax router selected the router as the DNS host to ensure DNS availability is fully independent of Proxmox uptime, a critical consideration when DNS is required to bring cluster nodes online.</li>
    <li>Configured DHCP reservations on the RT6600ax for all infrastructure hosts in Proxmox ensuring stable IP assignments across reboots and DHCP lease renewals.</li>
    <li>Updated DHCP scope options to distribute the new DNS server as the primary DNS server and 8.8.8.8 as the secondary fallback, with domain name set as the local domain name handed to all clients.</li>
    <li>Installed the Synology DNS Server package on the RT6600ax and created a master forward zone for domain name, with A records for all infrastructure hosts and the Proxmox cluster nodes including the planned new node.</li>
    <li>Validated DNS resolution from the Proxmox cluster using dig against the DNS server, confirming NOERROR responses for all host records and verifying /etc/resolv.conf was correctly populated via DHCP with the domain name search domain and correct nameserver entries.</li>
  </ul>
</div>




<div class="neon-border project-card">
  <h3>Lab Network Infrastructure & Firewall Architecture</h3>
  <p>
   Designed and implemented a segmented lab network using OPNsense as the primary router and firewall, running virtualized on a Proxmox host. The project involved full network architecture design including subnet segmentation, inter-VLAN routing, DNS filtering, and DHCP services - built to mirror enterprise networking practices in a lab environment.
  </p>
  <p><strong>Tech:</strong> OPNsense,Proxmox VE,KEA DHCPv4,Pi-hole,DNS,Static Routing,Network Segmentation</p>
  <ul>
    <li>Deployed OPNsense as a VM on Proxmox with dedicated WAN and LAN bridge interfaces, replacing a consumer router for core routing and firewall duties.</li>
    <li>Architected a segmented network with a dedicated LAN subnet (10.x.x.x/24) isolated from the upstream ISP network, with a static route on the Synology router directing LAN-bound traffic through the OPNsense WAN interface.</li>
    <li>Configured KEA DHCPv4 on the OPNsense LAN to manage address allocation across the 10.x.x.100 - 200 pool with static reservations for infrastructure hosts.</li>
    <li>Integrated Pi-hole as the primary DNS server for the LAN, enforcing network-wide ad and tracker blocking with Cloudflare as the upstream fallback resolver.</li>
    <li>Established inter-VLAN routing and firewall rules through OPNsense to control traffic flow between the virtualized LAN environment and the broader lab network.</li>
  </ul>
</div>

<div class="neon-border project-card">
  <h3>Backblaze B2 Offsite Data Protection</h3>
  <p>
    Data Protection project to implement off-site backup of on-prem NAS storage server. In Progress.
  </p>
  <p><strong>Tech:</strong> Backblaze B2 Cloud Storage, Synology NAS, HyperBackup, API Configurations.</p>
  <ul>
    <li>Configured Synology NAS software "HyperBackup" to use client side encryption before pushing out a full backup of NAS data to 
backblaze B2.</li>
    <li>Backblaze B2 bucket and application API configuration with HyperBackup software. Including nightly incrementals.</li>
    <li>Successful restore testing performed on local storage environment.</li>
  </ul>
</div>

<div class="neon-border project-card">
  <h3>Datacenter Storage Migrations</h3>
  <p>
    A 13+ month project involving migration of production SAN data and storage infrastructure. This included NetApp clusters, volumes, NFS and CIFS shares, LIFS, SVMs, Export Policies, and more. Leveraged rsync and AWS to reduce the amount of data needing to be migrated from site to site.
  </p>
  <p><strong>Tech:</strong> ONTAP, rsync, NFS, CIFS, SAN, Scripting, SaltStack, AIQUM, Nagios, Icinga2</p>
  <ul>
    <li>Performed production migrations of prod data between sites.</li>
    <li>Seeded data payloads between volumes ahead of time to automate cut-overs.</li>
    <li>Manage NAS, Scripting, and Automation Linux servers in planning and executing production cut-overs.</li>
  </ul>
</div>

<div class="neon-border project-card">
  <h3>Proxmox VE Lab Cluster</h3>
  <p>
    Designed and built a full-stack lab virtualization platform from the ground up, starting with custom PC hardware assembly and progressing through bare-metal OS installation, Proxmox VE cluster configuration, and network integration. The cluster serves as the foundational infrastructure for all lab projects, hosting Linux VMs and LXC containers across a dedicated lab network.
  </p>
  <p><strong>Tech:</strong> Proxmox VE, LXC, KVM, Debian, Custom PC Hardware, Network Configuration</p>
  <ul>
    <li>Assembled a custom workstation-class server using an Intel i7-12700KF with ~32GB RAM and ~11.76TB storage, purpose-built for lab virtualization workloads.</li>
    <li>Performed bare-metal installation and configuration of Proxmox VE, including storage pool setup, network bridge configuration, and cluster initialization.</li>
    <li>Configured the Proxmox cluster to serve as the primary virtualization platform for the lab network, providing on-demand LXC containers and KVM virtual machines for infrastructure, development, and automation projects.</li>
    <li>Established cluster networking on a flat TCP/IP lab network with the Synology RT6600ax as the upstream router, integrating DHCP reservations and local DNS for all cluster-hosted workloads.</li>
  </ul>
</div>

<div class="neon-border project-card">
  <h3>GitHub Pages Portfolio</h3>
  <p>
    A custom neon-themed static site built with Jekyll and GitHub Actions for automated CI/CD deployment. Designed to showcase my IT engineering projects, experience, and technical growth.
  </p>
  <p><strong>Tech:</strong> Jekyll, GitHub Actions, HTML/CSS</p>
  <ul>
    <li>Custom glowing CSS aesthetic built from scratch</li>
    <li>Deployed automatically through GitHub Actions</li>
    <li>Optimized for clean navigation and responsive design</li>
  </ul>
</div>

