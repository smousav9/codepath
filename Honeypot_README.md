# Honeypot Assignment

**Time spent:** **7** hours spent in total

**Objective:** Create a honeynet using MHN-Admin. Present your findings as if you were requested to give a brief report of the current state of Internet security. Assume that your audience is a current employer who is questioning why the company should allocate anymore resources to the IT security team.

### MHN-Admin Deployment (Required)

**Summary:** It was deployed using the google cloud platform. Two virtual machine was created on the GCP (mhn-admin, and Honeypot-1)

The first command lists the current default firewall rules. The subsequent multi-line commands will enable the required inbound ports for MHN Admin.

gcloud compute firewall-rules list

gcloud compute firewall-rules create http \
    --allow tcp:80 \
    --description="Allow HTTP from Anywhere" \
    --direction ingress \
    --target-tags="mhn-admin"

gcloud compute firewall-rules create honeymap \
    --allow tcp:3000 \
    --description="Allow HoneyMap Feature from Anywhere" \
    --direction ingress \
    --target-tags="mhn-admin"

gcloud compute firewall-rules create hpfeeds \
    --allow tcp:10000 \
    --description="Allow HPFeeds from Anywhere" \
    --direction ingress \
    --target-tags="mhn-admin"

Next, create the VM itself, which we'll call mhn-admin:

gcloud compute instances create "mhn-admin" \
    --machine-type "n1-standard-1" \
    --subnet "default" \
    --maintenance-policy "MIGRATE" \
    --tags "mhn-admin" \
    --image "ubuntu-minimal-1804-bionic-v20200703a" \
    --image-project "ubuntu-os-cloud" \
    --boot-disk-size "10" \
    --boot-disk-type "pd-standard" \
    --boot-disk-device-name "mhn-admin"

<img src="Unit6.gif">

### Dionaea Honeypot Deployment (Required)

**Summary:** Dionaea is a low-interaction honeypot that captures attack payloads and malware.
<img src="dionaea-honeypot.gif">

### Database Backup (Required) 

**Summary:** What is the RDBMS that MHN-Admin uses? What information does the exported JSON file record?
Relational Database Management System (RDBMS) that was used by MHN-Admin is MongoDB
The session.json file includes the information regrding the attacks and attackers

*Be sure to upload session.json directly to this GitHub repo/branch in order to get full credit.*


