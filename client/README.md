Role-based permissions and features available to each user type.

# 🎭 **Role-Based Feature Access in ProjectHub**

Comprehensive breakdown of what each role can do:

---

## 👑 **ADMIN ROLE** - _Full System Control_

### **🏢 Organization Management**

- ✅ **Create new organizations** during onboarding
- ✅ **Edit organization details** (name, description, settings)
- ✅ **View all organization members** and their details
- ✅ **Manage organization settings** and configurations
- ✅ **Delete organization** (with proper permissions)
- ✅ **View organization analytics** and statistics

### **👥 User & Role Management**

- ✅ **Invite users to organization** (manual process)
- ✅ **Change user roles** (Admin ↔ Project Manager ↔ Member)
- ✅ **Remove users from organization**
- ✅ **View all user profiles** in organization
- ✅ **Assign users to projects**
- ✅ **Update user positions and details**

```typescript:client/src/api/users/updateUserRole.ts
// Admin can update any user's role
export const useUpdateUserRole = (orgId: string) => {
  return useMutation({
    mutationFn: updateUserRole,
    // Admin has permission to change roles
  });
};
```

### **📋 Project Management**

- ✅ **Create unlimited projects**
- ✅ **Edit any project** in the organization
- ✅ **Delete any project** in the organization
- ✅ **Manage project members** (add/remove from any project)
- ✅ **View all projects** in organization
- ✅ **Access all project boards** and settings
- ✅ **Set project categories** (Business, Marketing, Software)

### **🎫 Issue Management**

- ✅ **Create issues in any project**
- ✅ **Edit any issue** across all projects
- ✅ **Delete any issue** across all projects
- ✅ **Assign issues to any team member**
- ✅ **Change issue status, priority, type**
- ✅ **View all issues** across organization
- ✅ **Bulk issue operations**

### **📊 Analytics & Reporting**

- ✅ **View organization-wide analytics**
- ✅ **Access all project metrics**
- ✅ **View team performance data**
- ✅ **Export reports and data**
- ✅ **View project history** for all projects
- ✅ **Access audit logs** and activity tracking

### **🔧 System Administration**

- ✅ **Manage system settings**
- ✅ **Configure organization preferences**
- ✅ **Access admin dashboard**
- ✅ **Manage demo accounts** (if applicable)

---

## 🎯 **PROJECT MANAGER ROLE** - _Project-Level Control_

### **📋 Project Management**

- ✅ **Create new projects** within organization
- ✅ **Edit projects they manage**
- ✅ **Manage assigned project members**
- ✅ **View all organization projects** (read-only for non-managed)
- ✅ **Access project settings** for managed projects
- ❌ **Cannot delete projects** (Admin only)

### **👥 Team Management (Project Level)**

- ✅ **Add members to their projects**
- ✅ **Remove members from their projects**
- ✅ **Assign project roles** within their projects
- ✅ **View team member profiles**
- ❌ **Cannot change organization-level roles** (Admin only)

### **🎫 Issue Management**

- ✅ **Create issues in managed projects**
- ✅ **Edit issues in managed projects**
- ✅ **Delete issues in managed projects**
- ✅ **Assign issues to project members**
- ✅ **Change issue priorities and status**
- ✅ **Manage issue workflows**
- ✅ **View issues across managed projects**

### **📊 Project Analytics**

- ✅ **View analytics for managed projects**
- ✅ **Access project performance metrics**
- ✅ **View team productivity data** for their projects
- ✅ **Generate project reports**
- ✅ **View project history** for managed projects
- ❌ **Cannot access organization-wide analytics**

### **🎨 Kanban Board Management**

- ✅ **Full access to project Kanban boards**
- ✅ **Move issues between columns**
- ✅ **Create issues directly on board**
- ✅ **Manage board filters and views**
- ✅ **Configure board settings**

### **🔍 Search & Discovery**

- ✅ **Search issues across managed projects**
- ✅ **Advanced filtering options**
- ✅ **View cross-project issue relationships**

---

## 👤 **MEMBER ROLE** - _Contributor Access_

### **📋 Project Access**

- ✅ **View assigned projects only**
- ✅ **Access project details** for assigned projects
- ❌ **Cannot create new projects**
- ❌ **Cannot edit project settings**
- ❌ **Cannot manage project members**

### **🎫 Issue Management (Limited)**

- ✅ **Create issues in assigned projects**
- ✅ **Edit issues they created or are assigned to**
- ✅ **Update status of assigned issues**
- ✅ **Add comments to issues**
- ✅ **View all issues in assigned projects**
- ❌ **Cannot delete issues** (unless they created them)
- ❌ **Cannot assign issues to others**
- ❌ **Limited priority change permissions**

```typescript:server/src/controllers/issues.ts
// Members can create issues but with limited permissions
const createIssue = async (req: Request, res: Response) => {
  // Members can create issues in projects they're assigned to
  // But cannot assign to others or set high priorities without approval
};
```

### **🎨 Kanban Board Usage**

- ✅ **View Kanban boards** for assigned projects
- ✅ **Move their assigned issues** between columns
- ✅ **Update issue status** via drag-and-drop
- ✅ **Create new issues** in To Do column
- ❌ **Cannot move other users' issues** (limited)
- ❌ **Cannot configure board settings**

### **👥 Team Interaction**

- ✅ **View team members** in assigned projects
- ✅ **See member profiles and contact info**
- ✅ **Collaborate on shared issues**
- ❌ **Cannot add/remove team members**
- ❌ **Cannot change member roles**

### **📊 Analytics (Limited)**

- ✅ **View personal productivity metrics**
- ✅ **See their issue completion stats**
- ✅ **View project progress** for assigned projects
- ❌ **Cannot access team performance data**
- ❌ **Cannot view organization analytics**

### **🔍 Search Capabilities**

- ✅ **Search issues in assigned projects**
- ✅ **Filter by assignee, type, priority**
- ✅ **View issue history** for accessible issues

### **⚙️ Profile Management**

- ✅ **Edit their own profile** (name, position)
- ✅ **Update personal settings**
- ✅ **Change password**
- ❌ **Cannot change their role** (Admin/PM only)
- ❌ **Cannot change organization**

---

## 🚫 **ROLE RESTRICTIONS SUMMARY**

### **What ONLY Admins Can Do:**

- Change user roles across the organization
- Delete projects and manage organization settings
- Access organization-wide analytics
- Manage organization members globally
- Configure system-level settings

### **What Project Managers Can Do (But Members Cannot):**

- Create and manage projects
- Assign team members to projects
- Manage project-level settings
- Access project analytics and reports
- Delete issues in managed projects

### **What All Roles Can Do:**

- Create and edit their own issues
- Update issue status for assigned items
- View assigned project details
- Use Kanban boards for assigned projects
- Search within accessible projects
- Manage their own profile

---

## 🔄 **ROLE TRANSITION WORKFLOW**

### **How Roles Can Be Changed:**

```typescript:client/src/api/users/updateUserRole.ts
// Only admins can change roles
const updateUserRole = async ({
  userId,
  userData,
}: {
  userId: string;
  userData: { role: User['role'] };
}): Promise<User> => {
  // Admin updates user role
  // System updates permissions automatically
};
```

### **Role Hierarchy:**

```
Admin (Highest)
    ↓ Can promote/demote
Project Manager (Middle)
    ↓ Can assign to projects
Member (Basic)
```

---

## 📋 **PRACTICAL EXAMPLES**

### **Scenario 1: New Feature Development**

```
Admin: Creates project "Mobile App v2.0"
Project Manager: Assigned to manage the project
    - Adds developers to project team
    - Creates epic issues and user stories
    - Assigns tasks to team members
Members:
    - Work on assigned issues
    - Update issue status
    - Create bug reports
    - Move issues through Kanban board
```

### **Scenario 2: Bug Fixing Workflow**

```
Member: Reports bug issue
    - Creates bug issue
    - Sets priority (limited to low/medium)
    - Assigns to themselves or leaves unassigned

Project Manager: Reviews bug
    - Can escalate priority to high
    - Assigns to appropriate developer
    - Tracks resolution progress

Admin: Can override any decisions
    - Change priority, assignee, or project
    - Access organization-wide bug metrics
```

---

## 🎯 **ROLE-BASED DASHBOARD VIEWS**

### **Admin Dashboard:**

- Organization overview with all metrics
- All projects and their status
- Team performance analytics
- System administration tools
- User management interface

### **Project Manager Dashboard:**

- Managed projects overview
- Team productivity for managed projects
- Issue distribution across managed projects
- Project-specific analytics
- Team member management tools

### **Member Dashboard:**

- Assigned projects only
- Personal issue queue
- Individual productivity metrics
- Assigned project progress
- Personal task management

This role-based system ensures proper access control while maintaining collaboration efficiency across the organization.
