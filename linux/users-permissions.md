Mission: Engineering Department Onboarding
Objective

Set up a secure Linux environment for a new department by creating users, managing group permissions, restricting access, and enforcing login policy using command-line tools only.

Environment

OS: Ubuntu Server 22.04 LTS

VM Platform: VirtualBox

RAM: 2 GB

Disk: 20 GB

Access Method: SSH

Privileges: sudo (no direct root login)

Requirements

Create a department group named engineering

Create two users: eng01 and eng02

Restrict access to the department directory to engineering members only

Disable login access for eng02

Create a shared file readable by both users

Allow only eng01 to modify the shared file

Verify all permissions and restrictions

Implementation
1. Group Creation

A dedicated group was created to manage department-level permissions efficiently and avoid per-user permission management.

Group name: engineering
Command: sudo groupadd engineering

This allows access control to be managed at the group level instead of assigning permissions individually.

2. User Creation and Group Assignment

Two users were created and added to the engineering group.


eng01 – active employee

eng02 – access suspended (HR issue)

Commands: sudo adduser eng01
          sudo adduser eng02

Both users were assigned to the same group to inherit directory-level permissions.

3. Department Directory Setup

A directory was created to store engineering resources.

Directory: /engineering_dept

Ownership: root:engineering

Permissions were set so that:

Only the owner and group members can access the directory

Other users have no access

This prevents unauthorized access from users outside the department.

4. Login Restriction

Login access for eng02 was disabled without deleting the account.

Reason:

Account remains for auditing and future reactivation

Access control is enforced without data loss

This separates authentication control from file permission control.

5. Shared File Access Control

A shared file was created inside the department directory.

Access rules:

Both users can read the file

Only eng01 can modify the file

This was achieved by:

Assigning ownership of the file to eng01

Keeping group read access

Removing group write permissions

Verification
Group Membership

Confirmed both users belong to engineering

Verified using group inspection commands

Login Test

eng01 can log in successfully

eng02 login is denied as expected

File Access Test

eng01 can read and modify the shared file

eng02 can read the file but receives a permission error when attempting to write

Directory Access

Users outside engineering cannot access /srv/engineering

All requirements were successfully met.

Issues Encountered

Initial permission misconfiguration allowed unintended write access

Resolved by separating directory permissions from file permissions and re-evaluating ownership

This reinforced the importance of understanding ownership vs permissions.

Lessons Learned

Groups simplify permission management

Login access and file access are independent controls

Avoid using overly permissive permissions (e.g. 777)

Always verify access using the actual user account

Conclusion

The engineering department was successfully onboarded with proper access controls, restricted login enforcement, and documented verification. The system now follows the principle of least privilege and is ready for production use.              