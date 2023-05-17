# Notes for Google Cloud Digital Leader Certification

### Cheatsheets
https://www.thecloudgirl.dev


## General Cloud theory
#### What is cloud computing?
The practice of using a network of remote servers hosted on the Internet to store, manage and process data.

#### Evolution of Cloud Hosting
1. Dedicated Servers
    - Very Expensive
    - High Maintenance
    - High Security
2. Virtual Private Server
    - Use virtual machines to isolate our applications
3. Shared Hosting
    - One physical machine shared by hundred of business.
    - Very cheap
    - Ver limited
4. Cloud hosting
    - Multiple Machines that acts as one system.
    - The system is abstracted into multiple services
    - It's flexible, scalable, secure, cost effective and highly configurable


### Benefits of Cloud Computing
1. Cost-effective (Pay for what you consume)
2. Launch anywhere in the world
3. Security - Cloud provider takes care of physical security.
4. Reliable - Data backups, disaster recovery, data replication, fault tolerance
5. Scalable - Increase or decrease resources on deman
6. Elastic - Automate scaling during spikes and drop in deman
7. Current - Underlying hardware and software is upgraded and replaced by provider without interruption

### Common Cloud Services
1. Compute
2. Storage
3. Networking
4. Databases

GCP has 60+ cloud services

### Types of Cloud Computing
1. SaaS - Software as a Service
2. PasS - Platform as a Service
3. IaaS - Infrastructure as a Service

![Types of Cloud Computing](./media/tyoes-of-cloud-computing.PNG)

### Google's Shared Responsibility Model
Simple visualization that determine what the customer is responsible forand what Google is responsible for related to GCP.

![Google Cloud Responsibility Model](./media/google-shared-responsibility-model.PNG)

![Google Cloud Responsibility Model](./media/gcp-shared-responsibility-model-2.PNG)


### Cloud Computing Deployment Models
1. Public Cloud (CLoud-Native)
2. Private Cloud (On-Premise)
3. Hybrid Cloud (Use both on premise and CLoud Service Provider)
4. Cross-Cloud (Multiple Cloud Providers e.g. AWS, Azure, GCP)

## Total Cost of Ownership
### CAPEX vs OPEX (Capital vs. Operational Expenditure)
![Capital vs operational Expenses](./media/capital-vs-operational-expenses.PNG)

### Cloud Architecture Terminologies
1. High Availability - Ability for your service to remain available by ensuring there is no **single point of failure**
2. Scalability - Increase your capacity based on the demand (vertical vs horizontal scaling)
3. Elasticity - Automatically increase or decrease your capacity (AUTOMATED) (Scaling Out - Add more services, Scaling In - REmoving more servers of the same size)
4. Fault Tolerance - Ensure there is not single point of failure, **prevent** the chance of failure. You create fail-over services/plan to shift traffic to a redundant system in case the primary system fails.
5. High Dureability/Disaster Recovery - Ability to recovery your data (Backups/how fast you can restore)

