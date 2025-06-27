# Network-File-Shares-and-Permissions
📁 File Share Permissions Lab: DC-1 + Client-1

This lab focuses on creating Windows file shares with various permissions and testing group-based access using Active Directory.

⸻

✅ Prerequisites
	•	Both DC-1 and Client-1 VMs should be turned on.
	•	DC-1: Log in as mydomain.com\jane_admin
	•	Client-1: Log in as a regular domain user (e.g., mydomain.com\johndoe)

⸻

🛠️ Part 1: Create File Shares with Permissions

1. On DC-1

Create the folders:mkdir C:\read-access
mkdir C:\write-access
mkdir C:\no-access
mkdir C:\accounting

📸 Screenshot: File Explorer showing all 4 folders created on C:\

⸻

2. Set Share Permissions (Right-click each folder > Properties > Sharing tab > Advanced Sharing)

📁 Folder: read-access
	•	Group: Domain Users
	•	Permissions: ✅ Read only

📸 Screenshot of permission settings

⸻

📁 Folder: write-access
	•	Group: Domain Users
	•	Permissions: ✅ Read/Write

📸 Screenshot of permission settings

⸻

📁 Folder: no-access
	•	Group: Domain Admins
	•	Permissions: ✅ Read/Write
	•	No permissions for Domain Users

📸 Screenshot showing that Domain Users is not listed

⸻

✅ Skip setting permissions for “accounting” for now

⸻

🧪 Part 2: Test Access as Regular User

3. On Client-1

Log in as: mydomain.com\<someuser>

In the Start Menu > Run dialog (Win + R), type:\\DC-1
📸 Screenshot of shared folders visible

Try to:
	•	Open each folder
	•	Create a file in each folder

📸 Screenshot results for:
	•	✅ Successful access (e.g., read-only)
	•	❌ Access denied (e.g., no-access)
	•	✅ Able to write (e.g., write-access)
 🧑‍💼 Part 3: ACCOUNTANTS Group + Permission Testing

4. On DC-1

Open Active Directory Users and Computers
	•	Right-click your domain > New > Group
	•	Name: ACCOUNTANTS
	•	Group scope: Global, Group type: Security

📸 Screenshot of group creation

⸻

5. Set Accounting Folder Permissions
	•	Go back to C:\accounting
	•	Share the folder
	•	Add ACCOUNTANTS group
	•	Permission: ✅ Read/Write

📸 Screenshot of accounting folder permissions

⸻

6. Back on Client-1

As <someuser>, try:\\dc-1\accounting
Expected: ❌ Access Denied

📸 Screenshot of denial prompt or access error

⸻

7. On DC-1

Make <someuser> a member of the ACCOUNTANTS group:
	•	In ADUC > Users > double-click <someuser>
	•	Go to Member Of tab > Add → ACCOUNTANTS

📸 Screenshot of user’s group membership updated

⸻

8. On Client-1
	•	Sign out
	•	Sign back in as <someuser>
	•	Try accessing:\\dc-1\accounting
Expected: ✅ Access Granted

📸 Screenshot showing success accessing accounting folder

⸻

🧹 Final Notes
	•	✅ Now you’ve tested shared folder security using:
	•	Domain groups
	•	Folder-level access control
	•	📴 You can stop or delete the VMs from the Azure Portal when finished.
