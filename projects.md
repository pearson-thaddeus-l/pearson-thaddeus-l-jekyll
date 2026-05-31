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
  <h3>Synology DNS Implementation</h3>
  <p>
    Designed and implemented a local DNS infrastructure on the Synology RT6600ax router to support hostname resolution across a flat lab network. This project was a prerequisite to expanding the Proxmox cluster from a single node to a multi-node configuration, which requires reliable bi-directional hostname resolution between cluster members. The implementation involved deliberate architectural decisions around DNS placement for high availability, DHCP reservation management, and forward zone configuration built to mirror enterprise DNS practices in a home lab environment.
  </p>
  <p><strong>Tech:</strong> Synology RT6600ax, Synology DNS Server, BIND9 (underlying), DHCPv4, DNS Forward Zone, Proxmox VE</p>
  <ul>
    <li>Evaluated DNS hosting options including a dedicated Proxmox LXC running BIND9, the Synology NAS, and the Synology RT6600ax router selected the router as the DNS host to ensure DNS availability is fully independent of Proxmox uptime, a critical consideration when DNS is required to bring cluster nodes online.</li>
    <li>Simplified the home lab network from a segmented dual-subnet architecture (OPNsense-routed 10.0.0.x LAN + 192.168.1.x WAN) to a flat lab network network after decommissioning OPNsense and Pi-hole, requiring a full reassignment of all host IPs prior to DNS implementation.</li>
    <li>Configured DHCP reservations on the RT6600ax for all infrastructure hosts in Proxmox ensuring stable IP assignments across reboots and DHCP lease renewals.</li>
    <li>Updated DHCP scope options to distribute the new DNS server as the primary DNS server and 8.8.8.8 as the secondary fallback, with domain name set as the local domain name handed to all clients.</li>
    <li>Installed the Synology DNS Server package on the RT6600ax and created a master forward zone for domain name, with A records for all infrastructure hosts and the Proxmox cluster nodes including the planned new node.</li>
    <li>Validated DNS resolution from the Proxmox cluster using dig against the DNS server, confirming NOERROR responses for all host records and verifying /etc/resolv.conf was correctly populated via DHCP with the domain name search domain and correct nameserver entries.</li>
    <li>Established DNS infrastructure as the foundation for the next phase: joining the new Proxmox node to the Proxmox cluster, which requires both nodes to resolve each other by hostname prior to cluster formation.</li>
  </ul>
</div>




<div class="neon-border project-card">
  <h3>Home Network Infrastructure & Firewall Architecture</h3>
  <p>
   Designed and implemented a segmented home network using OPNsense as the primary router and firewall, running virtualized on a Proxmox host. The project involved full network architecture design including subnet segmentation, inter-VLAN routing, DNS filtering, and DHCP services - built to mirror enterprise networking practices in a home lab environment.
  </p>
  <p><strong>Tech:</strong> OPNsense,Proxmox VE,KEA DHCPv4,Pi-hole,DNS,Static Routing,Network Segmentation</p>
  <ul>
    <li>Deployed OPNsense as a VM on Proxmox with dedicated WAN and LAN bridge interfaces, replacing a consumer router for core routing and firewall duties.</li>
    <li>Architected a segmented network with a dedicated LAN subnet (10.x.x.x/24) isolated from the upstream ISP network, with a static route on the Synology router directing LAN-bound traffic through the OPNsense WAN interface.</li>
    <li>Configured KEA DHCPv4 on the OPNsense LAN to manage address allocation across the 10.x.x.100 - 200 pool with static reservations for infrastructure hosts.</li>
    <li>Integrated Pi-hole as the primary DNS server for the LAN, enforcing network-wide ad and tracker blocking with Cloudflare as the upstream fallback resolver.</li>
    <li>Established inter-VLAN routing and firewall rules through OPNsense to control traffic flow between the virtualized LAN environment and the broader home network.</li>
  </ul>
</div>

<div class="neon-border project-card">
  <h3>Hubitat Home Automation</h3>
  <p>
   Design and implement a secure home automation system using Hubitat hardware and Zigbee mesh networking.
  </p>
  <p><strong>Tech:</strong> Hubitat Model C-8 Pro, Zigbee Protocol, Mesh Networking, ZED Devices.</p>
  <ul>
    <li>In Progress.</li>
    <li>In Progress.</li>
    <li>In Progress.</li>
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
  <h3>Proxmox Homelab Automation</h3>
  <p>
    Automates provisioning and lifecycle management of VMs on a Proxmox cluster using Bash scripts and YAML configurations.
  </p>
  <p><strong>Tech:</strong> Bash, Proxmox API, YAML</p>
  <ul>
    <li>Creates and networks new VMs from predefined templates</li>
    <li>Integrates with Proxmox API for lightweight orchestration</li>
    <li>Logs provisioning events and task output for auditing</li>
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

<div class="neon-border project-card">
  <h3>IoT Water Pump Controller</h3>
  <p>
    A Raspberry Pi–based IoT controller that manages a water pump via Wi-Fi and scheduled cron jobs. The goal is to build a smart automation layer for local environmental control.
  </p>
  <p><strong>Tech:</strong> Raspberry Pi, Python, Cron, MQTT</p>
  <ul>
    <li>Wi-Fi controlled GPIO relay for water pump</li>
    <li>Scheduled tasks via Linux cron automation</li>
    <li>Future integration with Node-RED dashboard</li>
  </ul>
</div>

