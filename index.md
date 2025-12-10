# CMPN202 Operating Systems Coursework Journal

**Student ID:** [Your Student ID]  
**Module:** Operating Systems (Level 5)  
**Programme:** [Your Programme]  
**Academic Year:** 2025/26

---

## 📋 Project Overview

This technical journal documents my 7-week journey implementing, securing, and evaluating a Linux server operating system. Through hands-on configuration, security hardening, and performance analysis, I've developed practical competencies in Linux administration, remote system management, and infrastructure security aligned with industry-standard practices.

### Learning Outcomes

By completing this coursework, I will demonstrate:

✅ **LO3:** Assess security vulnerabilities and apply appropriate security mechanisms  
✅ **LO4:** Demonstrate proficiency with CLI tools for system administration  
✅ **LO5:** Critically evaluate operating system design trade-offs and constraints

### Professional Skills Developed

- Deploy and manage basic Linux server infrastructure
- Configure and harden remote systems using SSH
- Develop automation scripts for security and monitoring
- Analyze and document technical trade-offs with quantitative data
- Implement industry-standard security controls
- Create professional technical documentation with diagrams

---

## 📅 Weekly Progress

| Week | Phase | Topic | Deliverables | Status |
|------|-------|-------|--------------|--------|
| 1 | Planning | System Planning & Distribution Selection | Architecture, Justifications, Network Config | ✅ |
| 2 | Design | Security Planning & Testing Methodology | Testing Plan, Security Checklist, Threat Model | ⏳ |
| 3 | Selection | Application Selection for Performance Testing | App Matrix, Installation Docs, Monitoring Strategy | ⏳ |
| 4 | Implementation | Initial Security & System Configuration | SSH Config, Firewall, Users, Evidence | ⏳ |
| 5 | Advanced | Advanced Security & Monitoring Infrastructure | SELinux/AppArmor, Fail2Ban, Scripts | ⏳ |
| 6 | Testing | Performance Evaluation & Analysis | Performance Data, Graphs, Optimization Results | ⏳ |
| 7 | Audit | Security Audit & System Evaluation | Lynis Report, nmap Results, Risk Assessment | ⏳ |

### Quick Navigation

- **[Week 1: System Planning](week1.md)** - Architecture & distribution selection
- **[Week 2: Security Planning](week2.md)** - Testing methodology & threat modeling
- **[Week 3: Application Selection](week3.md)** - Workload application choices
- **[Week 4: Initial Security](week4.md)** - SSH, firewall, user management
- **[Week 5: Advanced Security](week5.md)** - SELinux, monitoring, scripts
- **[Week 6: Performance Analysis](week6.md)** - Testing & optimization
- **[Week 7: Security Audit](week7.md)** - Final audit & evaluation

---

## 🏗️ System Architecture

![System Architecture](assets/images/architecture.png)

**Architecture Summary:**
- **Server:** Ubuntu Server 22.04 LTS (headless, CLI-only)
- **Workstation:** [Your choice]
- **Network:** VirtualBox Host-Only Network
- **Administration:** SSH key-based authentication only
- **Security:** Firewall, SELinux/AppArmor, Fail2Ban, auto-updates

---

## 🔑 Key Findings Summary

### Security Implementation
- Implemented 5+ mandatory security controls
- Achieved Lynis score: [Your score] (target: >80)
- Zero default passwords; key-based SSH authentication
- Firewall restricted to single workstation access

### Performance Analysis
- Tested 5+ applications across different workload types
- Identified key bottlenecks: [e.g., disk I/O on large files, CPU on compression]
- Implemented 2+ optimizations with quantitative improvements
- Performance improvements: [e.g., 30% reduction in response time]

### Trade-offs Identified
- Security vs. Usability: Strict SSH key management enhances security but requires key backup
- Performance vs. Security: Mandatory access controls add 5-8% CPU overhead
- Storage vs. Security: Encrypted filesystems reduce write speed by ~12%

---

## 📚 Resources Used

- [Ubuntu Server Documentation](https://ubuntu.com/server/docs)
- [Linux Man Pages](https://man7.org/linux/man-pages/)
- [SSH Essentials Guide](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys)
- [VirtualBox Manual](https://www.virtualbox.org/manual/)
- [Module VLE Resources](https://moodle.roehampton.ac.uk)

---

## 📝 Submission Details

**GitHub Pages URL:**  
`https://yourusername.github.io/CMPN202-OS-Coursework/`

**Repository:** Public GitHub repository with weekly commits

**Video Demonstration:** [To be recorded - max 8 minutes]

**Deadline:** Week Commencing 15th December 2025, 14:00 GMT

---

## 🔍 How to Navigate This Journal

1. **Start here** on this home page for an overview
2. **Choose a week** from the links above to see detailed work
3. **Each week contains:**
   - Completed deliverables
   - Command-line evidence with screenshots
   - Explanations of decisions and outputs
   - Learning reflections
   - Next steps

4. **Return to home** using navigation links at the bottom of each week

---

**Last Updated:** [Date]  
**Repository Commits:** [Number of commits]  
**Total Documentation:** [Page count]

---

## 📧 Module Contact Information

- **Module Tutor:** Dr Shabih Fatima (shabih.fatima@roehampton.ac.uk)
- **Module Tutor:** Tanaya Bowade (Tanaya.Bowade@roehampton.ac.uk)
- **Module Leader:** Dr Ogechukwu Okonor (Ogechukwu.Okonor@roehampton.ac.uk)

---

[← Back to Top](#cmpn202-operating-systems-coursework-journal)
