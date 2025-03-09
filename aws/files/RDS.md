<div align="center">

# **RDS (Relational Database Service)**

</div>

A fully managed service that makes it easier to set up, operate, and scale a relational database in the cloud. AWS takes care of many administrative tasks like backups, patching, and scaling, so you can focus on using your database rather than managing it.

__* IMPORTANT__ befor Creating a Database (RDS) there a need to create a subnet group.

# Create RDS

Navigate to RDS webpage

__1. Create Subnet group__ setting on which AZ the Database will deploy.

      on the right menu, Choose "Subnet groups" --> create DB subnet group:

            under name: enter group name.
            choose the PVC for the group.
            choose only private subnet.

     now, press "create Database":

             name: set Database name
             choose DB type
             enable deletion protection (protect deleteing db - not allowed as long as it enabled)
             public acces not allowed

             Create Database

__IMportent__ check security group that is open for connection.
