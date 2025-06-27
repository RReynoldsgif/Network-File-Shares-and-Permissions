# Network-File-Shares-and-Permissions
# 📁 File Share Permissions Lab: DC-1 + Client-1

This lab focuses on creating Windows file shares with various permissions and testing group-based access using Active Directory.


# ✅ Prerequisites

 •	Both DC-1 and Client-1 VMs should be turned on.
	
 •	DC-1: Log in as mydomain.com\jane_admin
	
 •	Client-1: Log in as a regular domain user (e.g., mydomain.com\johndoe)


# 🛠️ Part 1: Create File Shares with Permissions

# 1. On DC-1

Create the folders:mkdir C:\read-access

mkdir C:\write-access

mkdir C:\no-access

mkdir C:\accounting

📸 ![Screenshot (16)](https://github.com/user-attachments/assets/54720f26-5060-4eeb-bac7-2205b86a0366)
Screenshot: File Explorer showing all 4 folders created on C:\


# 2. Set Share Permissions (Right-click each folder > Properties > Sharing tab > Advanced Sharing)

📁 Folder: read-access
	
 •	Group: Domain Users
	
 •	Permissions: ✅ Read only

📸![Screenshot (18)](https://github.com/user-attachments/assets/db467ea9-934b-4ad8-b71d-567a8f908692)



📁 Folder: write-access
	
 •	Group: Domain Users
	
 •	Permissions: ✅ Read/Write

📸![Screenshot (19)](https://github.com/user-attachments/assets/76d3e1ea-4faa-4adf-b55f-917afe02f3d0)



📁 Folder: no-access
	
 •	Group: Domain Admins
	
 •	Permissions: ✅ Read/Write
	
 •	No permissions for Domain Users

📸 ![Screenshot (20)](https://github.com/user-attachments/assets/1b3c9782-53d0-42c0-a01b-b6d27ee5dea3)

🧪 Part 2: Test Access as Regular User

# 3. On Client-1

Log in as: mydomain.com\<someuser>

In the Start Menu > Run dialog (Win + R), type:\\DC-1

Try to:
	•	Open each folder
	•	Create a file in each folder

📸![Screenshot (4)](https://github.com/user-attachments/assets/ebe395db-3727-4f4f-961f-f3d0ecc647d7)

	
 •	✅ Successful access (e.g., read-only)
	
 •	❌ Access denied (e.g., no-access)
	
 •	✅ Able to write (e.g., write-access)
 🧑‍💼 Part 3: ACCOUNTANTS Group + Permission Testing

# 4. On DC-1

Open Active Directory Users and Computers
	•	Right-click your domain > New > Group
	•	Name: ACCOUNTANTS
	•	Group scope: Global, Group type: Security

📸 ![Screenshot (22)](https://github.com/user-attachments/assets/f0506d2c-73f5-4735-aa15-fff55c047ec6)



# 5. Set Accounting Folder Permissions
	
	 •Go back to C:\accounting
	
	 •Share the folder
	
	 •Add ACCOUNTANTS group
	
 	•Permission: ✅ Read/Write

📸 ![Screenshot (23)](https://github.com/user-attachments/assets/e83d7dac-1db8-4dad-8e23-881c5ec1f0b1)



# 6. Back on Client-1

	As <someuser>, try:\\dc-1\accounting
	Expected: ❌ Access Denied

📸 ![Screenshot (4)](https://github.com/user-attachments/assets/36a017ff-1121-4b5d-ae2a-ba44651ebb0e)
Screenshot of denial prompt or access error


# 7. On DC-1

	Make <someuser> a member of the ACCOUNTANTS group:
	
 	•In ADUC > Users > double-click <someuser>
	
 	•Go to Member Of tab > Add → ACCOUNTANTS

📸 ![Screenshot (24)](https://github.com/user-attachments/assets/5056125d-58ec-45d0-b996-367af5f7d6c6)
Screenshot of user’s group membership updated


# 8. On Client-1

	• Sign out

	•Sign back in as <someuser>

	• Try accessing:\\dc-1\accounting
Expected: ✅ Access Granted

📸 ![Screenshot (10)](https://github.com/user-attachments/assets/a3971f6b-437e-4de9-b37e-398ee60b360b)
Screenshot showing success accessing accounting folder
