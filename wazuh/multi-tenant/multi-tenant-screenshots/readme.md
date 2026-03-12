<img width="848" height="429" alt="Screenshot 2026-03-12 105118" src="https://github.com/user-attachments/assets/cc2eb174-dfb8-4bca-8a8e-e756ea3ef75e" />

<img width="981" height="419" alt="Screenshot 2026-03-12 105347" src="https://github.com/user-attachments/assets/292308e6-8ba0-4688-b8d2-338cc05422ed" />
1. Agent Groups Creation
The first screenshot shows the Groups section in the Wazuh Dashboard where multiple agent groups were created to logically separate monitored systems.
Groups configured:
default
server-A
server-B

<img width="1919" height="645" alt="Screenshot 2026-03-12 115335" src="https://github.com/user-attachments/assets/f4253b93-e48a-4ed0-85ad-7981dfb4f686" />
2. Agent Group Configuration
A label is added to agents belonging to the server-A group.
Labels help filter alerts and logs inside the dashboard.
This enables easier identification of which server generated a security event.

<img width="1919" height="424" alt="Screenshot 2026-03-12 115401" src="https://github.com/user-attachments/assets/159f7587-6fa5-4444-9064-9fd6c5005a2c" />
3. Role-Based Access Control
The third screenshot shows custom roles created in the Wazuh Security → Roles section.
Roles configured:
read_server_A
read_server_B
Each role includes:
Cluster permissions
Index permissions for wazuh-alerts-*
Multi-tenant access control
Users assigned:
user1 → read_server_A
user2 → read_server_B
Purpose:
Restrict access so users only view alerts from their assigned servers
Implement role-based security separation

<img width="1919" height="729" alt="Screenshot 2026-03-12 115628" src="https://github.com/user-attachments/assets/4016192b-6939-46dd-bda8-54a764871ed9" />
Two custom roles are created:
Role 1: read_server_A
Permissions:
cluster_monitor
cluster_composite_ops
multitenant
Index access:
wazuh-alerts-*
Assigned user:
user1
Tenant permission:
kibana_all_read
Role 2: read_server_B
Similar permissions.
Assigned user:
user2
Access to alerts index:
wazuh-alerts-*
Purpose
Each role limits what alerts the user can read, depending on the server.
This is role-based access control (RBAC) in Wazuh/OpenSearch.

<img width="1919" height="747" alt="Screenshot 2026-03-12 115722" src="https://github.com/user-attachments/assets/12d88016-b208-4104-a92a-6b9a810c60bf" />
List of users in the system:
user1 → intended to access Server A alerts
user2 → intended to access Server B alerts
logstash → used for log ingestion
admin → full admin account

<img width="1919" height="729" alt="Screenshot 2026-03-12 115812" src="https://github.com/user-attachments/assets/12f7570b-c60e-4b98-ada0-3d88bbae9fbb" />
Main elements visible:
Username field – used to create or modify a user account.
Password options
Toggle for password authentication.
Option to force password change on first login.
Backend roles (optional)
Allows assigning roles that define what permissions the user will have.
There is an option to add backend roles.

<img width="1919" height="377" alt="Screenshot 2026-03-12 115855" src="https://github.com/user-attachments/assets/b1f0d9d4-3dea-449b-85a6-62cff8aceffb" />
Policy being edited:
Policy name: read_server_A
Configuration details:
Action: Defines what the policy does.
Allowed action: agent:read
Resource:
agent:group:server-A

<img width="1919" height="741" alt="Screenshot 2026-03-12 115931" src="https://github.com/user-attachments/assets/cf0ca66c-b556-4f44-9351-44088e876da5" />
Key columns:
Policy name
Actions (permissions like agent:read)
Resource identifier
Effect: allow
Reserved policies (system policies that cannot be edited)
Purpose:
This page is used to view and manage all security policies controlling access to agents, clusters, and other system resources.

<img width="1919" height="595" alt="Screenshot 2026-03-12 115953" src="https://github.com/user-attachments/assets/3cc170e4-677f-4558-972e-8aae3deb4c90" />
Two custom roles are visible:
read_server_A
read_server_B
These roles define what permissions a user has in the Wazuh environment (for example reading agents, clusters, rules, or logs).

<img width="1919" height="740" alt="Screenshot 2026-03-12 120021" src="https://github.com/user-attachments/assets/5febc890-e897-47cd-a25a-dc57d89e4bf7" />
What it indicates:
You are editing the role read_server_A.
This role is assigned a policy named:
read_server_A
Policies determine the exact permissions (for example read access to specific data).
So this role likely allows read-only access to logs or data related to Server A.

<img width="1919" height="622" alt="Screenshot 2026-03-12 120047" src="https://github.com/user-attachments/assets/18075df6-4c11-4856-8b0f-09117e97e95b" />
Mappings shown include:
Mapping Name
Role Assigned
wui_elastic_admin
administrator
wui_opensearch_admin
administrator
read_server_A_mapping
read_server_A
read_server_B_mapping
read_server_B
admin
administrator
This means:
Users associated with these mappings will automatically receive the assigned role permissions.
Example:
A user mapped to read_server_A_mapping will get the read_server_A role permissions.

<img width="1919" height="742" alt="Screenshot 2026-03-12 120208" src="https://github.com/user-attachments/assets/98b6aee2-fff6-4127-90ee-a011ed2ba9ce" />
Currently logged in as admin user while making all of the above changes. As you can see, the admin user has access to both servers A and B.

<img width="1919" height="744" alt="Screenshot 2026-03-12 120231" src="https://github.com/user-attachments/assets/29edb55a-f971-40d6-b7b2-940fc29d1e60" />
We now login with "user1" which is a user dedicated to server-A.

<img width="1919" height="736" alt="Screenshot 2026-03-12 120302" src="https://github.com/user-attachments/assets/e9453d80-655c-45ca-921a-02f9c671c48b" />
User1 has access to Ubuntu wazuh agent and to all of its logs and data.

<img width="1919" height="737" alt="Screenshot 2026-03-12 120327" src="https://github.com/user-attachments/assets/019536a0-be40-4add-8803-9a84f7bd0152" />
The "user1" only has access to server A.

<img width="1919" height="736" alt="Screenshot 2026-03-12 120416" src="https://github.com/user-attachments/assets/ff9c3af3-ae2b-4a7b-8872-eb3eb8551225" />
User2 has access to Ubuntu wazuh agent and to all of its logs and data.

<img width="1919" height="737" alt="Screenshot 2026-03-12 120530" src="https://github.com/user-attachments/assets/aea03b33-9e9e-4f68-8ee2-55e1611a8128" />
The "user2" only has access to server B
