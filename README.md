# Hybrid Cloud Identity Lab — `aniketlab.shop`

> Complete hybrid identity build: on-prem Active Directory on Windows Server 2022 (VMware Workstation) synchronized to Microsoft Entra (Azure AD) using **Azure AD Connect** with **Seamless SSO** (Kerberos).  
> Includes step-by-step reproduction, verification commands, troubleshooting, screenshots and demo video.

---

## Contents
- [Overview](#overview)  
- [Topology](#topology)  
- [Prerequisites](#prerequisites)  
- [Quick reproduction (summary)](#quick-reproduction-summary)  
- [Detailed steps & useful commands](#detailed-steps--useful-commands)  
- [How to verify SSO](#how-to-verify-sso)  
- [Screenshots to include (recommended filenames)](#screenshots-to-include-recommended-filenames)  
- [Demo video (recording & embedding guidance)](#demo-video-recording--embedding-guidance)  
- [Troubleshooting checklist](#troubleshooting-checklist)  
- [Repository structure](#repository-structure)  
- [License](#license)

---

## Overview
This repo documents a working hybrid identity environment for domain `aniketlab.shop`. The lab demonstrates:
- On-prem AD DS on Windows Server 2022 (Domain Controller `DC01`, static IP `192.168.1.10`)  
- Internal DNS/DHCP for enterprise-style name resolution and IP management  
- Azure AD integration via **Azure AD Connect** (Password Hash Sync + Seamless SSO)  
- Seamless Single Sign-On (Kerberos) for domain-joined clients to access cloud apps (e.g., Microsoft 365)

---

## Topology
A simple diagram you can render with Mermaid (GitHub renders Mermaid in README):

```mermaid
graph TD
  Internet["Internet"]
  Router["Router / Gateway\n(192.168.1.1)"]
  DC["DC01\nWindows Server 2022\nAD DS, DNS (192.168.1.10)"]
  Client["CLIENT01\nWindows 10/11\n(Domain-joined)"]
  Azure["Microsoft Entra (Azure AD)\n(aniketlab.shop)"]
  Internet --> Router
  Router --> DC
  Router --> Client
  DC --> Azure
  Client --> Azure
