# Guide to Deploy

## Prerequisites

- AWS Account
- Billing info must be prsent

## Steps - backend

1. Create a cluster in AWS
2. Enter name
3. Tick on Create VPC
4. Create
5. Go to Cluster
6. Create a Task Desfinition from Sidebar
7. Select Fargat, Enter name
8. Select ECS task execution role
9. Specify container name, evironment vaiable (Use URL as localhost, Check dockerfie for env required)
10. Add another container (Mongodb)
11. Create
12. Select Application Load balancer (Create if not exist)
    1. EC2 sectio
    2. Load Balancer -> Application Load balancer
    3. Specif name, Select IP, Enter a target grgoup name, select VPC same as ECS VPC
    4. Create
13. Specify the VPC, target group
14. Create
15. Access `<public_ip_addr>/goals` or `<load_balancer_dns>/goals`

### NOTE

- If you are getting unhealthy status fom container, upg=date the path from `/` to `/goals` i target group
- Wait for atleast 5 min for above step to be executed
- Make sure you are using same VPC

## Adding Persistence

- Make sure you are using same VPCs everywhere

1. Task deinition
2. Select the task
3. Create new revision
4. In add volume section, give any name to volume
   1. Go to Security Groyps
   2. Create security group
   3. Add inboud rule for EFS, Source must be 'Custom', Select security group by ECS
   4. Save
5. Create the EFS (Make sure security group is selecte properly in VPC section)
6. Go to mongo DB container
7. Go to Mount points section
8. Mount the named volume with `/data/db`

## Steps - Frontend

1. Build a docker image
2. Push to dockehub
3. Create a load balancer
   1. Select VPC same as Server's VPC
   2. It must be internalfacing
   3. Expose port 80
   4. Expose port 80 in security group
