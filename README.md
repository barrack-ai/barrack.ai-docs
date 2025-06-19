# Platform Documentation

Complete guide to deploying and managing GPU-accelerated virtual machines

## Getting Started

### Platform Overview

Welcome to our GPU-accelerated cloud platform. This documentation covers everything you need to deploy, manage, and optimize virtual machines with powerful GPU resources.

### Authentication & Access

Multiple ways to access your account:

- **Email & Password:** Traditional login with your registered email and password
- **OTP Login:** Secure one-time password login via email
- **Google OAuth:** Quick sign-in with your Google account
- **Password Recovery:** Email-based password reset with secure verification

### First Steps

Recommended setup process:

1. Create an account using email/password or Google OAuth
2. Complete your profile in **My Account** section (required for payments)
3. Add credits to your account in the **Credits** section
4. Create or import an SSH key from the **SSH Keys** section
5. Deploy your first virtual machine using the **Deploy VM** wizard

## Storage Management

The Storage Management system allows you to create and manage persistent storage volumes for your virtual machines.

### Prerequisites

**Required Before Creating Volumes**

- **Complete Profile:** Your profile must be complete with billing information (address, postal code, country)
- **Minimum Balance:** Account must have sufficient credits:
  - USD: Minimum $1.00
  - EUR: Minimum €1.00
  - INR: Minimum ₹100.00

### Volume Types

The platform supports different volume types:

#### Standard Volumes
General-purpose storage for data and applications

- **Minimum size:** 10GB
- **Maximum size:** 1,048,576GB (1TB)
- **Performance:** Optimized for GPU workloads
- **Persistence:** Across VM lifecycles
- **Attachment:** Any VM in the same region

#### Bootable Volumes
Volumes that contain an operating system and can be used to start a VM

- **Minimum size:** 100GB
- **Maximum size:** 1,048,576GB (1TB)
- **Initialization:** Must have a valid OS image
- **Usage:** Can be used to deploy new VMs
- **Benefit:** Preserves installed software and configurations

### Volume Storage Pricing

| Storage Type | USD | EUR | INR |
|-------------|-----|-----|-----|
| Volume Storage | $0.1 per TB per hour | €0.1 per TB per hour | ₹10 per TB per hour |

### Volume Dashboard Statistics

The Volumes page displays key statistics for your storage in the selected region:

- **Total Volumes:** Number of volumes in the selected region
- **Total Storage:** Combined storage allocated across all volumes (in GB)
- **Attached Volumes:** Number of volumes currently attached to VMs
- **Bootable Volumes:** Number of volumes that can be used to boot VMs

### Pagination and Display

Volume management includes efficient pagination:

- 6 volumes displayed per page
- Previous/Next navigation with page numbers
- Pagination controls appear when more than 6 volumes exist
- Grid layout adjusts for desktop (3 columns) and mobile (1 column)

## Creating Volumes

Creating storage volumes allows you to add persistent storage to your virtual machines or create bootable volumes for new VM deployments.

### Volume Creation Process

To create a storage volume:

1. Navigate to the Volumes page or click "Create Volume" from the dashboard
2. Ensure your profile is complete and you have sufficient credits
3. Click `Create Volume`
4. Enter required information in the modal:
   - Volume name (the system will suggest a sequential name like volume1, volume2)
   - Region selection from dropdown
   - Size in GB (minimum 10GB for standard, 100GB for bootable)
5. For bootable volumes, toggle the "Make Bootable" option and:
   - Select an OS image from the dropdown
   - Size will automatically adjust to minimum 100GB if less than that
6. Click `Create Volume`

### Create Volume Modal Features

- **Grid Layout:** Name and Region on first row, Size and Bootable toggle on second row
- **Real-time Validation:** Form validates inputs as you type with immediate feedback
- **Character Counter:** Name field shows character count (up to 50 characters)
- **Auto-adjustment:** Size automatically increases to 100GB when bootable is enabled
- **Dynamic OS Images:** OS image dropdown loads based on selected region
- **Stylized Toggle:** Custom toggle switch with animation for bootable option

### Form Validation Rules

#### Volume Name Validation
- Required field (cannot be empty)
- 1-50 characters maximum
- Allowed: Letters, numbers, spaces, hyphens (-), underscores (_), periods (.)
- Must be unique within your account
- Real-time duplicate name checking

#### Size and Type Validation
- Standard volumes: 10GB minimum
- Bootable volumes: 100GB minimum (auto-enforced)
- Maximum size: 1,048,576GB for all volumes
- OS image required for bootable volumes
- Region must be selected for all volumes

**Automatic Volume Naming**

The system automatically suggests names for new volumes using a sequential pattern (volume1, volume2, etc.). This suggestion is generated server-side to avoid conflicts. You can accept the suggested name or enter your own custom name following the validation rules.

**Bootable Volume Creation**

- When you enable "Make Bootable", the size field automatically increases to 100GB if it's below that threshold
- OS images are dynamically loaded based on your selected region
- If no OS images are available for your region, an error message will be displayed
- Bootable volumes can be used as boot sources when creating new VMs

## Managing Volumes

The Volumes page provides comprehensive tools for managing your storage, including attaching, detaching, and deleting volumes.

### Attaching Volumes

To attach a volume to a VM:

1. Click `Attach` on an available volume card
2. The Volume Attach Modal opens showing:
   - Volume details (name, size, region, type)
   - List of VMs in the same region with ACTIVE status
   - VM information (name, status, region) in a table format
3. Select a VM using the radio button selection
4. Click "Attach Volume" to confirm

#### Volume Attach Modal Features

- **Smart VM Filtering:** Only shows VMs in the same region as the volume
- **Status Validation:** Only ACTIVE VMs can be selected for attachment
- **Visual Status Indicators:** VM status badges with color coding (green for ACTIVE)
- **Helpful Messages:** Displays reason why non-ACTIVE VMs cannot be selected
- **Auto-selection:** Automatically selects the first ACTIVE VM if available
- **Loading States:** Shows progress during attachment operation

**Attachment Requirements:**

- VM must be in `ACTIVE` state for volume operations
- Volume and VM must be in the same region
- Bootable volumes that are already in use cannot be attached to another VM
- VM must not be undergoing another operation

### Detaching Volumes

To detach a volume from a VM:

1. Click `Detach` on an attached volume
2. A confirmation modal appears with volume details and warnings
3. Review the warning about potential application disruption
4. Click "Detach" to confirm the operation

#### Smart Detachment System

- **Automatic VM Detection:** System automatically finds the VM to detach from
- **Multi-source VM ID:** Uses instance_id, attached volume mapping, or region-based VM search
- **VM Status Validation:** Ensures VM is in ACTIVE state before detachment
- **Graceful Error Handling:** Clear error messages for various failure scenarios
- **Status Display:** Shows VM status when volume is attached

**Detachment Requirements:**

- VM must be in `ACTIVE` state for volume detachment
- Cannot detach the system/boot volume of a running VM
- Volume must currently be attached to a VM

### Deleting Volumes

To delete a volume:

1. Click `Delete` on an unattached volume
2. A delete confirmation modal appears showing:
   - Volume name to be deleted
   - Warning that action cannot be undone
   - Permanent data loss warning
3. Click "Delete" to confirm the permanent deletion

**Deletion Requirements:**

- Volumes must be detached before deletion
- Deletion is permanent and cannot be undone
- All data on the volume will be permanently lost

### Volume Status Indicators

Volumes display status indicators to show their current state:

- **Available:** The volume is ready to be attached to a VM
- **Attached / In-use:** The volume is currently attached to a VM
- **Creating:** The volume is currently being created
- **Error:** There was an issue creating or attaching the volume

### Volume Information Display

Each volume card displays comprehensive information:

- **Header:** Volume name with database icon and current status badge
- **Attachment Info:** Shows which VM the volume is attached to (if any)
- **VM Status:** Displays the status of the attached VM for operational context
- **Specifications Grid:** Size, Region, Type (Cloud-SSD), and Bootable status
- **Action Buttons:** Dynamic buttons based on volume state (Attach/Detach and Delete)

**Storage Best Practices**

Recommendations for effective storage management:

- Create volumes in the same region as your VMs to avoid compatibility issues
- Size volumes appropriately for your workload to optimize cost
- Use bootable volumes for persistent OS configurations that you want to reuse
- Detach volumes before deleting VMs if you want to preserve the data
- Consider creating snapshots before major changes to ensure data recovery options
- Monitor your volume usage to avoid unnecessary storage costs
- Complete your profile and maintain sufficient credits before creating volumes

**Volume Management Tips**

- The page automatically refreshes after volume operations to show updated status
- Loading states show progress for create, attach, detach, and delete operations
- Pagination automatically adjusts when volumes are added or removed
- Region filtering allows you to manage volumes across different geographic locations
- Volume statistics update in real-time as you perform operations

## GPU Configuration

Select from our high-performance GPU options based on your computational needs.

### Available GPU Types

| GPU Model | Performance | Best For |
|-----------|-------------|----------|
| H100-SXM5-80GB | Highest performance for large-scale AI training | Large language models, complex AI research |
| H100-PCIe-NVLink-80GB | High-performance with NVLink | Multi-GPU workloads, distributed training |
| H100-PCIe-80GB | High-performance PCIe interface | Single-GPU inference, model training |
| A100-SXM4-80GB-NVLink | Excellent for deep learning and HPC | Deep learning, scientific computing |
| A100-PCIe-80GB | High-performance PCIe A100 | ML training, data analytics |
| L40 | Balanced performance for diverse workloads | AI inference, graphics workloads |
| RTX-A6000 | Cost-effective for smaller workloads | Development, small-scale training |
| A40 | Versatile professional GPU | Professional graphics, AI development |

### GPU Count Selection

Choose the number of GPUs for your virtual machine:

- Available counts are dynamically updated based on current stock
- Higher GPU counts provide more computational power for parallel workloads
- Multi-GPU setups automatically include NVLink for supported GPU types
- GPU availability varies by region and is updated in real-time

## Region Selection

Choose the geographic location for your VM deployment:

| Region | Location | Available GPU Types |
|--------|----------|-------------------|
| NORWAY-1 | Europe | All GPUs Available |
| CANADA-1 | North America | All GPUs Available |
| US-1 | North America | All GPUs Available |

**Region Selection Tips**

- Select the region closest to your primary users for lowest latency
- Regions are automatically filtered based on GPU availability
- Storage volumes and snapshots are region-specific
- Consider regions with higher availability of your preferred GPU type

## Boot Source Configuration

Select from available boot source options:

### OS Images
Pre-configured operating systems optimized for GPU workloads.

- Ubuntu Server 22.04 LTS R550 CUDA 12.4
- Ubuntu Server 22.04 LTS R550 CUDA 12.4 with Docker
- Ubuntu Server 20.04 LTS R535 CUDA 12.2
- Ubuntu Server 20.04 LTS R535 CUDA 12.2 with Docker
- Images are filtered by selected region

### Volumes
Boot from an existing storage volume (authenticated users only).

- Requires a bootable volume in the same region
- Volumes are filtered by region and bootable status
- Persistent between deployments
- Minimum 100GB for bootable volumes

### Custom Images
Use your own saved VM images (authenticated users only).

- Created from your own snapshots
- Pre-configured environments
- Region-specific availability
- Standardize deployments across teams

**Important Considerations**

- OS images are automatically filtered by your selected region
- Volume and custom image options require user authentication
- Bootable volumes must be in the same region as your VM
- Custom images are created from your snapshots and are region-specific

## SSH Key Configuration

SSH keys provide secure access to your virtual machines. SSH key management requires user authentication.

### Managing SSH Keys

- SSH keys are automatically loaded when you're authenticated
- Create new keys or import existing keys directly from the deployment interface
- Keys are automatically selected if you have only one available
- Multiple keys can be selected for team access

### Creating a New SSH Key

1. Click "Create Key" in the SSH key section
2. Enter a unique name for the key (1-50 characters)
3. The system generates and downloads the private key automatically
4. Store the private key securely - it cannot be retrieved later
5. Set proper permissions: `chmod 600`

### Importing an Existing SSH Key

1. Click "Import Key" in the SSH key section
2. Enter a unique name (1-50 characters, alphanumeric, underscore, hyphen, period)
3. Paste your public key content (OpenSSH format)
4. The key will be validated and added to your account

### SSH Connection Example

```
ssh -i ~/.ssh/your_private_key ubuntu@vm_ip_address
```

Connection details:
- `~/.ssh/your_private_key` is the path to your downloaded private key file
- `ubuntu` is the default username for Ubuntu images (use "root" for other OS)
- `vm_ip_address` is the public IP shown in your VM dashboard
- Ensure your private key has correct permissions: `chmod 600 ~/.ssh/your_private_key`

**SSH Key Requirements**

- Key names: 1-50 characters, letters, numbers, underscores, hyphens, periods only
- Public keys must be in standard OpenSSH format (ssh-rsa, ssh-ed25519, etc.)
- At least one SSH key is required for VM deployment
- SSH key management requires user authentication
- Private keys are only available for download during creation

## Advanced Configuration

Configure additional options for your VM to enhance security, access, and initial setup:

### Public IP
- Enable or disable public IP address assignment
- Public IPs allow internet access to your VM
- Disabling public IP restricts access to internal network only
- Security warning displayed when public IP is enabled

### Security Rules
- Configure firewall rules through the integrated interface
- Add rules for specific protocols (TCP, UDP, ICMP)
- Define allowed IP ranges and port restrictions
- Rules are applied automatically after VM becomes active

### Jupyter Notebook
- Optionally enable Jupyter Notebook server
- Password required (minimum 8 characters)
- Password strength validation (weak/medium/strong)
- Access via browser at `http://<vm-ip>:8888`

### Cloud-Init Script
- Add custom initialization scripts (maximum 16KB)
- Configure software installation and setup
- Customize VM environment at first boot
- Input validation and sanitization applied

**Security Considerations**

- Security rules may take up to 10 minutes to be fully applied after VM deployment
- Public IP makes your VM accessible from the internet - ensure proper security
- Jupyter password must meet minimum security requirements
- Cloud-init scripts are sanitized for security

## VM States & Billing

Virtual machines can exist in various states, each with different billing implications. Understanding these states helps you manage costs effectively.

### Primary VM States

| State | Description | Billing |
|-------|-------------|---------|
| ACTIVE | The VM is running with all resources allocated. This is the standard working state. | Full rate (per-minute billing) |
| SHUTOFF | The VM is stopped but resources remain reserved exclusively for your use. | Full rate (per-minute billing) |
| HIBERNATED | The VM's state is saved while hardware resources are released. Only root disk storage remains allocated. | Reduced rate ($0.01/€0.01/₹1.00 per hour) |
| DELETED | The VM is permanently removed with all resources released. | No charge |

### Per-Minute Billing

The platform uses precise per-minute billing for optimal cost efficiency:

- Billing is calculated in one-minute increments for exact usage tracking
- You pay only for the time your resources are actually running
- No minimum usage requirements or rounding to hours
- Hibernated VMs are billed at a significantly reduced rate

### Transitional VM States

During operations, your VM may temporarily be in one of these states. No additional charges apply during these transitional states.

- **CREATING/BUILD:** Initial VM creation and configuration
- **STARTING:** VM is powering on
- **STOPPING:** VM is powering off
- **HIBERNATING:** VM is entering hibernation mode
- **RESTORING:** VM is returning from hibernation
- **REBOOTING:** VM is restarting
- **DELETING:** VM is being removed
- **ERROR:** VM encountered an issue during an operation

## Dashboard Overview

The Dashboard provides a comprehensive overview of your virtual machines, account information, and quick access to platform features.

### Main Dashboard Layout

The dashboard is organized into three main sections:

#### Instance Details (Left)
- Selected VM overview and specifications
- Hardware details (CPU, Memory, Storage, GPU)
- Network information (Private/Public IPs)
- Real-time status indicators
- Quick action buttons

#### VM Operations (Center)
- VM selector dropdown
- VM configuration controls
- Status control actions (Start, Stop, Hibernate)
- Management operations (Delete, Snapshot)
- Pricing information

#### Account & Actions (Right)
- Account information and Barrack ID
- Credit balance and billing details
- GST/VAT information management
- Quick navigation actions
- Logout functionality

### Key Dashboard Features

- **Real-time VM Status:** Live updates on virtual machine states and health
- **Quick Actions:** One-click access to common operations like hibernation and snapshots
- **Cost Monitoring:** Transparent pricing display with per-minute billing breakdown
- **Resource Overview:** Complete hardware specifications and network configuration
- **Account Management:** Credit balance monitoring and billing information

**Navigation Tip**

Use the VM selector dropdown to quickly switch between multiple virtual machines. The dashboard automatically updates to show details for the selected VM.

## VM Management

The dashboard provides comprehensive tools for managing your virtual machines throughout their lifecycle.

### VM Status Management

Control your virtual machines with these state management options:

#### Power Management
- **Start:** Power on a stopped VM
- **Stop:** Gracefully shut down an active VM
- **Reboot:** Restart an active VM
- **Hibernate:** Save VM state and release resources
- **Restore:** Resume a hibernated VM from saved state

#### Resource Management
- **View Details:** Access comprehensive VM information
- **Create Volume:** Add persistent storage to VMs
- **Take Snapshot:** Create point-in-time backups
- **Delete:** Permanently remove VMs and free resources

### VM Information Display

The dashboard shows comprehensive information for each virtual machine:

| Information Type | Description |
|-----------------|-------------|
| Hardware Specs | CPU cores, RAM, storage, and GPU configuration |
| Network Details | Private IP, public IP (if assigned), and SSH key information |
| Pricing Info | Real-time cost per hour and per minute for active usage |
| Storage Volumes | Attached persistent storage volumes and their configurations |
| Regional Info | Deployment region and availability zone |

### Quick Actions

Access frequently used platform features directly from the dashboard:

- **Deploy VM**
- **SSH Keys**
- **Volumes**
- **Snapshots**

**Billing Information**

- Pricing is calculated per minute for exact usage tracking
- ACTIVE VMs are billed at the full rate shown in the dashboard
- HIBERNATED VMs are charged only for storage at a reduced rate
- STOPPED and SHUTOFF VMs continue to be billed at the full rate as resources remain reserved

## Firewall Management

The Firewall Management system allows you to create and configure network security rules to protect your virtual machines. Maximum limit: **25 firewalls per account**.

### Firewall Overview

The Firewall page displays your existing firewalls with detailed information (6 firewalls per page):

- Firewall name and description
- Status indicator (SUCCESS, CREATING, ERROR)
- Region information
- Creation date
- Rule count
- Attached VM count

Action buttons for each firewall: View Details, Add Rule, Attach to VMs, Delete. The system provides statistics cards showing Total Firewalls, Total Rules, Attachments, and Active firewalls.

### Creating Firewalls

To create a new firewall:

1. Click the "Create Firewall" button (disabled when limit reached)
2. Enter a firewall name (required, maximum 50 characters)
3. Optionally add a description (maximum 255 characters)
4. Select a region from the dropdown
5. Click "Create Firewall"

**Name Requirements:** Must be 1-50 characters, supports letters, numbers, spaces, hyphens (-), underscores (_), and dots (.). Must be unique within your account.

Security rules may take up to 10 minutes to be fully applied after creation. During this time, your VM may appear to have limited connectivity.

## Firewall Rules

Firewall rules define what network traffic is allowed to and from your VMs.

### Rule Components

Each rule consists of:

- **Direction:** Ingress (incoming) or Egress (outgoing)
- **Protocol:** TCP, UDP, ICMP
- **IP Version:** IPv4 or IPv6
- **Remote IP Range:** CIDR notation of allowed IP addresses
- **Port Range:** For TCP/UDP, specific ports or port ranges (1-65535)

### Adding Rules

To add a rule:

1. From the firewall details or click "Add Rule" button
2. Select direction: Ingress (Incoming) or Egress (Outgoing)
3. Select protocol: TCP, UDP, or ICMP
4. Choose IP version: IPv4 or IPv6
5. Enter remote IP range in CIDR format
6. For TCP/UDP: specify port ranges (both min and max required)
7. Click "Add Rule" to save

### Port Range Specifications

For TCP and UDP protocols:

- Port numbers must be between 1 and 65535
- Minimum port must be less than or equal to maximum port
- Both minimum and maximum ports must be specified together
- For single port access, set both minimum and maximum to the same value
- Port ranges are not applicable for ICMP protocol

### IP Range Validation

Remote IP ranges must follow CIDR notation:

- **IPv4:** Example: 192.168.1.0/24, 0.0.0.0/0 (all IPs)
- **IPv6:** Example: 2001:db8::/32, ::/0 (all IPs)
- IPv4 address parts must be 0-255
- IPv4 CIDR prefix must be 0-32
- IPv6 CIDR prefix must be 0-128

### Common Rule Configurations

| Use Case | Direction | Protocol | Port Range | Remote IP |
|----------|-----------|----------|------------|-----------|
| SSH Access | Ingress | TCP | 22 | Your IP or trusted range |
| Web Server | Ingress | TCP | 80, 443 | 0.0.0.0/0 (public access) |
| Jupyter Notebook | Ingress | TCP | 8888 | Your IP or trusted range |
| Database Access | Ingress | TCP | 3306, 5432 | Internal network only |
| ICMP (Ping) | Ingress | ICMP | N/A | Your IP or trusted range |

## Attaching Firewalls to VMs

Firewalls must be attached to VMs to take effect. You can manage these attachments through the firewall management interface.

### Attaching Process

1. From the firewall card, click "Attach" button
2. Select VM from the list of available machines
   - Only VMs with ACTIVE status are displayed
   - VMs that have server_uuid are eligible for attachment
   - Single VM selection (radio button interface)
   - Already attached VMs are marked with checkmark icon
3. Click "Attach Firewall" to confirm attachment

### VM Compatibility

- VM must be in ACTIVE state to attach firewall
- VM must have a valid server_uuid
- VMs in HIBERNATED or STOPPED state cannot be attached
- Multiple firewalls can be attached to the same VM
- When multiple firewalls are attached, all rules apply cumulatively

### Viewing Attachments

To view firewall attachments:

1. Click "View Details" on any firewall
2. Select the "Attached VMs" tab
3. View table showing: VM Name, VM Status, Attachment Status
4. Attachment statuses: SUCCESS, ATTACHING, ERROR

### Detaching Firewalls

Firewalls can be detached through the firewall details interface. Use caution when detaching as it immediately removes network protection.

**Important Security Notes**

- Firewall rules are applied immediately when attached to VMs
- Detaching all firewalls from a VM will leave it with no protection
- VM must be in ACTIVE state for firewall attachment
- Changes to firewall rules affect all attached VMs
- Rule changes may take up to 10 minutes to fully propagate
- Cannot delete firewall if it has active VM attachments

### Firewall Deletion

Firewalls can only be deleted if they have no active VM attachments. If attachment count is greater than 0, you must first detach all VMs before deletion is allowed.

## Snapshots Management

The Snapshots page allows you to create point-in-time backups of your virtual machines, restore them to create new VMs, and manage your backup history.

### Dashboard Overview

The snapshots dashboard provides key statistics and management capabilities:

- **Total Snapshots:** Number of snapshots in the selected region
- **Total Storage:** Combined storage used by all snapshots
- **Available VMs:** Number of active VMs that can be snapshotted
- **Restorable:** Number of snapshots with SUCCESS/available status

### Region Filtering

Snapshots are organized by region:

- Use the region dropdown to filter snapshots by location (US-1, CANADA-1, NORWAY-1)
- Only snapshots and VMs in the selected region are displayed
- Snapshots are region-specific and cannot be moved between regions

### Snapshot Information Display

Each snapshot displays comprehensive information:

| Field | Description |
|-------|-------------|
| Name | User-defined snapshot name (up to 50 characters) |
| Size | Storage space used by the snapshot in GB |
| Region | Geographic location where snapshot is stored |
| Created | Date and time when snapshot was created |
| Type | VM Snapshot or Image (if created as image) |
| Status | SUCCESS/available (restorable) or other states |

### Pagination and Navigation

The snapshots interface includes pagination for easy navigation:

- 6 snapshots displayed per page
- Previous/Next navigation buttons
- Direct page number selection
- Pagination only appears when more than 6 snapshots exist

**Profile Requirement**

Your profile must be complete with billing information before creating snapshots. Ensure your account has the required details configured.

## Creating Snapshots

Create point-in-time backups of your virtual machines to preserve their current state, data, and configuration.

### Prerequisites

- At least one virtual machine must be in ACTIVE state
- VM must be in the same region as where you want to create the snapshot
- Your account profile must be complete with billing information
- Sufficient credits for snapshot storage costs

### Step-by-Step Process

To create a new snapshot:

1. Navigate to the Snapshots page
2. Select your desired region from the dropdown menu
3. Click the "Create Snapshot" button (disabled if no active VMs are available)
4. In the Create Snapshot modal, select a virtual machine from the dropdown
5. Enter a unique snapshot name (required, 1-50 characters)
6. Optionally click "Show advanced options" to access additional settings
7. Review your settings and click "Create Snapshot"

### Basic Configuration

#### Virtual Machine Selection

- Dropdown shows only ACTIVE VMs in the selected region
- Displays VM name, GPU type, and region for easy identification
- Example format: "my-vm - H100-SXM5-80GB (CANADA-1)"
- If no VMs are available, you'll see "No active VMs available"

#### Snapshot Name Requirements

- **Required field** - cannot be empty
- **Length limit:** 1-50 characters
- **Allowed characters:** Letters, numbers, spaces, hyphens (-), underscores (_), periods (.)
- **Must be unique** within your account
- Real-time character count display (e.g., "25/50")
- Instant validation feedback for invalid names

### Advanced Options

Click "Show advanced options" to access additional configuration:

#### Description Field
- Optional text area for snapshot description
- Helps identify the snapshot's purpose
- Useful for team collaboration
- No character limit enforced in UI

#### Create as Image Toggle
- Toggle switch to create snapshot as an image
- Images can be used for future VM deployments
- Appears in boot source options during VM creation
- Useful for standardizing environments

### Creation Process

After clicking "Create Snapshot":

- Form validation occurs instantly (name format, VM selection)
- Button shows "Creating..." state with spinner animation
- Modal remains open during creation process
- Any errors are displayed in red alert boxes
- Success results in modal closure and snapshots list refresh

**Important Notes**

- Snapshot creation can take several minutes depending on VM disk size
- The source VM remains operational during snapshot creation
- Snapshot names must be unique across your entire account
- Only VMs in ACTIVE state can be snapshotted
- If no active VMs exist, the Create Snapshot button will be disabled

## Restoring Snapshots

Restore snapshots to create new virtual machines with the exact configuration and data from when the snapshot was taken.

### Prerequisites for Restoration

- Snapshot must have SUCCESS or available status
- Snapshot must be in a complete, non-corrupted state
- Sufficient credits for new VM deployment
- Valid VM name for the restored instance

### Restoration Process

To restore a snapshot:

1. Navigate to the Snapshots page and locate your snapshot
2. Verify the snapshot status shows SUCCESS or available (green indicator)
3. Click the "Restore" button on the snapshot card
4. Review the snapshot information in the restore modal
5. **Auto-suggestion:** System suggests "{snapshot-name}-restored"
6. Click "Restore Snapshot" to begin the process

### Restore Modal Information

The restore modal displays comprehensive snapshot details:

| Field | Description |
|-------|-------------|
| Name | Original snapshot name |
| Size | Storage size in GB |
| VM | Original VM name with server icon |
| Region | Geographic location |
| Created | Full date and time of creation |
| Status | Color-coded status indicator |

### New VM Name Configuration

#### Name Requirements

- **Auto-suggestion:** System suggests "{original-snapshot-name}-restored"
- **Length limit:** 1-50 characters with real-time counter
- **Allowed characters:** Letters, numbers, spaces, hyphens (-), underscores (_), periods (.)
- **Uniqueness:** Must be unique within your account
- **Validation:** Real-time feedback for invalid names

### What Happens During Restoration

- A completely new virtual machine is created
- All data and configuration from the snapshot is applied
- The new VM gets a new IP address (both private and public if applicable)
- SSH keys need to be reconfigured for access
- The original VM (if it still exists) remains unchanged
- The restored VM will be in the same region as the snapshot

### Restoration States

During the restoration process:

- **Initiating:** Button shows "Restoring..." with spinner animation
- **Processing:** Modal remains open while restoration is in progress
- **Success:** Modal closes and snapshots page refreshes
- **Error:** Error message displayed in red alert box

**Important Restoration Notes**

- Restoration creates a completely new VM - it does not overwrite existing VMs
- The new VM will have a different IP address than the original
- You'll need to update any SSH configurations or firewall rules
- Only snapshots with SUCCESS or available status can be restored
- Restoration process may take several minutes depending on snapshot size
- Ensure you have sufficient credits before starting restoration

## Managing Snapshots

Comprehensive tools for viewing, organizing, and managing your snapshot collection throughout their lifecycle.

### Snapshot Details View

Click the info icon (ⓘ) on any snapshot to view detailed information:

#### Basic Information Section

- **Name:** Full snapshot name
- **VM Name:** Original source VM name
- **Size:** Storage space used in GB
- **Created:** Full timestamp of creation
- **Status:** Color-coded status indicator
- **Image:** Yes/No indicating if snapshot is also an image

#### VM Configuration Section

- **Region:** Geographic location of the snapshot
- **CPU:** Number of vCPUs (if available)
- **RAM:** Memory allocation in GB (if available)
- **GPU:** GPU type and count (if available)
- **Disk:** Storage allocation in GB (if available)

#### Description Section

If a description was provided during creation, it appears in a scrollable text area with custom styling. Maximum height of 24px with overflow scrolling for longer descriptions.

### Snapshot Status Indicators

Status badges provide instant visual feedback:

- **SUCCESS / available:** Snapshot is complete and ready for restoration
- **Other states:** Snapshot is processing or encountered an issue

### Deleting Snapshots

Remove snapshots to free up storage space and manage costs:

1. Click the red "Delete" button on any snapshot card
2. A confirmation modal appears with snapshot details
3. Review the warning message about permanent deletion
4. Click "Delete" to confirm, or "Cancel" to abort
5. Deletion process shows spinner and "Deleting..." text
6. Snapshot list automatically refreshes after successful deletion

#### Deletion Confirmation Modal

- Shows exact snapshot name being deleted
- Warning triangle icon with danger messaging
- Clear statement that action cannot be undone
- Cancel and Delete buttons with distinct styling
- Delete button becomes disabled during processing
- Loading state with spinner animation

### Refresh and Data Management

Keep your snapshot data current:

- **Automatic Refresh:** List updates automatically after create/delete operations
- **Manual Refresh:** Refresh button with spinning animation during loading
- **Real-time Updates:** Status changes reflect immediately
- **Error Handling:** Clear error messages for failed operations

### Mobile and Responsive Design

The snapshot interface adapts to different screen sizes:

- **Desktop:** Full sidebar with 3-column grid layout
- **Mobile/Tablet:** Single column cards with responsive wrapper
- **Touch-Friendly:** Larger buttons and touch targets
- **Optimized Text:** Appropriate font sizes for each screen size

**Deletion Safety**

- Snapshot deletion is permanent and cannot be undone
- Deleting a snapshot does not affect VMs or images created from it
- Consider creating an image from important snapshots before deletion
- Deletion frees up storage space and reduces ongoing storage costs
- If a snapshot is being used for restoration, wait for completion before deleting

## Custom Images

Custom images allow you to create reusable VM templates from your snapshots. These images can be used as boot sources when deploying new virtual machines, enabling you to quickly replicate configurations and software setups.

### What are Custom Images?

Custom images are created from your VM snapshots and serve as templates for new virtual machine deployments. They contain:

- The complete operating system and all installed software
- System configurations and settings
- User data and applications
- Custom scripts and automation

### Creating Custom Images

To create a custom image from a snapshot:

1. Navigate to the Images page or access it from the snapshots interface
2. Click "Create Image" in the Images section
3. Select a snapshot from the available list (must have SUCCESS status)
4. Enter a unique name for your image (1-50 characters)
5. Optionally add a description to help identify the image's purpose
6. Click "Create Image" to begin the creation process

#### Image Creation Requirements

- **Source Snapshot:** Must be in SUCCESS or available status
- **Name Requirements:** 1-50 characters, letters, numbers, spaces, hyphens, underscores, periods
- **Uniqueness:** Image names must be unique within your account
- **Region Specific:** Images are created in the same region as the source snapshot

### Using Custom Images

Once created, custom images can be used when deploying new VMs:

1. In the VM deployment wizard, select "Custom Images" as your boot source
2. Choose your custom image from the dropdown list
3. Images are filtered by the selected region automatically
4. Complete the rest of your VM configuration and deploy

#### Custom Image Benefits

- **Rapid Deployment:** Skip manual software installation and configuration
- **Consistency:** Ensure identical environments across multiple VMs
- **Team Collaboration:** Share standardized environments with team members
- **Version Control:** Create multiple image versions for different use cases

### Managing Custom Images

The Images page provides comprehensive management capabilities:

#### Image Information
- View image name, size, and creation date
- Check image status and region information
- Access detailed image properties and metadata
- Monitor storage usage across all images

#### Image Operations
- Delete images that are no longer needed
- View detailed image information and properties
- Filter images by region for easier management
- Track image creation from source snapshots

### Image Status and Lifecycle

Custom images go through different states during their lifecycle:

- **Available / SUCCESS:** Image is ready to be used for VM deployment
- **Creating:** Image is being created from the source snapshot

### Region-Based Management

Custom images are managed on a per-region basis:

- Images are created in the same region as their source snapshot
- Use the region dropdown to view images in different locations
- Images can only be used to deploy VMs in their respective regions
- Transfer between regions requires creating new snapshots and images

**Image Best Practices**

- Use descriptive names that indicate the image's purpose and software versions
- Create images from clean, well-configured snapshots for best results
- Document your images with detailed descriptions for team collaboration
- Regularly clean up unused images to manage storage costs
- Test newly created images by deploying test VMs before production use
- Consider creating versioned images for different software configurations

**Important Considerations**

- Custom images inherit the storage footprint of their source snapshots
- Deleting an image does not affect VMs that were deployed from it
- Image creation can take several minutes depending on snapshot size
- Images are private to your account and cannot be shared with other users
- Ensure source snapshots are from stable, properly configured VMs

## Creating SSH Keys

SSH keys provide secure access to your virtual machines, replacing password-based authentication with more secure cryptographic keys. At least one SSH key is required for VM deployment.

### SSH Key Creation Process

To create a new SSH key:

1. Navigate to the SSH Keys page from the sidebar
2. Click "Create Key" button
3. Enter a descriptive name for the key (maximum 50 characters)
   - Names must contain only letters, numbers, underscores, hyphens, and periods
   - Use descriptive names like "my-project-key" or "development-server"
4. Click "Create Key" to generate the keypair
5. The system automatically generates a secure 2048-bit RSA public/private key pair
6. The private key file will automatically download to your computer

**Critical Security Notice**

Important information about your private key:

• The private key is only available for download once during creation
• Store it securely as it cannot be retrieved later from our servers
• The private key file is automatically downloaded for security reasons
• Never share your private key with anyone or upload it to version control
• Back up your private key in a secure location

### Setting Private Key Permissions

After downloading your private key file, you must set the correct permissions for security:

#### Linux/MacOS
```
chmod 600 /path/to/your_private_key.pem
```

Replace `/path/to/your_private_key.pem` with the actual path to your downloaded key file. This command ensures only you can read and write the file.

#### Windows (using PowerShell)
```
icacls "C:\path\to\your_private_key.pem" /inheritance:r /grant:r "$($env:USERNAME):(R,W)"
```

Replace `C:\path\to\your_private_key.pem` with the actual path to your downloaded key file. This removes inheritance and grants only the current user read/write access.

### Key Limits and Restrictions

• Maximum of 25 SSH keys per region
• Key names must be unique within your account
• Generated keys use 2048-bit RSA encryption
• Keys are automatically distributed to all regions upon creation

## Importing SSH Keys

If you already have SSH keys that you use for other services (GitHub, GitLab, other cloud providers), you can import the public key to use with your virtual machines on our platform.

### SSH Key Import Process

To import an existing SSH public key:

1. Navigate to the SSH Keys page from the sidebar
2. Click "Import Key" button
3. Enter a descriptive name for the key (maximum 50 characters)
   - Names must contain only letters, numbers, underscores, hyphens, and periods
   - Use descriptive names like "github-key" or "laptop-ssh-key"
4. Paste your public key content in the text area (begins with ssh-rsa, ssh-ed25519, etc.)
5. Click "Import Key" to add it to your account

This adds your existing public key to the platform, allowing you to use SSH keys generated elsewhere while keeping your private key secure on your local machine.

### Finding Your Public Key

If you're not sure where to find your public key on your system:

#### Linux/MacOS

Your public key is typically located at:
```
~/.ssh/id_rsa.pub or ~/.ssh/id_ed25519.pub
```

You can display and copy it with:
```
cat ~/.ssh/id_rsa.pub
```

For Ed25519 keys: `cat ~/.ssh/id_ed25519.pub`

#### Windows

**With Git Bash or WSL:**
```
~/.ssh/id_rsa.pub or ~/.ssh/id_ed25519.pub
```
```
cat ~/.ssh/id_rsa.pub
```

**With PowerShell:**
```
Get-Content $env:USERPROFILE\.ssh\id_rsa.pub
```

**Public Key Format Requirements**

Understanding the correct format for import:

A valid public key must:
- Begin with a key type: `ssh-rsa`, `ssh-ed25519`, or `ssh-dss`
- Contain a long base64-encoded string of characters
- Optionally end with a comment (usually email address or description)
- Be on a single line with no line breaks

**Example format:**
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC0WGP1EZykEtv5YGC9nMiPFW3U3DmZNzKFO5nEu6uozEHh3JLi9bii user@example.com
```

### Supported Key Types

- **RSA Keys:** ssh-rsa (2048+ bits recommended)
- **Ed25519 Keys:** ssh-ed25519 (recommended for new keys)
- **ECDSA Keys:** ecdsa-sha2-nistp256/384/521

## Managing SSH Keys

The SSH Keys page provides comprehensive tools for managing your credentials throughout their lifecycle, from creation to deletion.

### Viewing and Organizing Keys

#### Key Information
- View key name, fingerprint, and creation date
- Access the full public key content
- Copy public keys to clipboard with one click
- View regional distribution of keys

#### Organization Features
- Search keys by name
- Filter keys by region
- Sort by name or creation date
- Paginated view for large key collections

### Deleting SSH Keys

To remove an SSH key from your account:

1. Navigate to the SSH Keys page
2. Find the key you want to delete using search or filters
3. Click the "Delete" button on the key card
4. Confirm the deletion in the popup dialog
5. The key will be immediately removed from all regions

**Key Deletion Considerations**

Important factors when deleting SSH keys:

- Deleted keys cannot be recovered - this action is permanent
- You cannot delete keys that are currently in use by active VMs
- Ensure you have at least one working SSH key before deleting others
- Keys are removed from all regions simultaneously
- VMs using deleted keys will lose SSH access until a new key is configured

### Using SSH Keys with Virtual Machines

SSH keys are automatically integrated into the VM deployment process:

#### During VM Creation

1. In the SSH Key Configuration section of VM deployment, select from your available keys
2. Multiple keys can be selected for a single VM to allow access by different team members
3. Selected keys are automatically installed on the VM during provisioning
4. Keys are configured for the default user account (ubuntu, centos, etc. depending on OS)

#### Connecting to VMs

**Basic SSH Connection**
```
ssh -i /path/to/private_key username@vm_ip_address
```

**Parameter explanations:**
- `/path/to/private_key` - Path to your downloaded private key file
- `username` - Default user for your OS (ubuntu, centos, admin, etc.)
- `vm_ip_address` - Public IP address of your VM

**SSH Config File (Recommended)**

For easier connections, add entries to your SSH config file (`~/.ssh/config`):

```
Host my-vm
  HostName 203.0.113.1
  User ubuntu
  IdentityFile ~/.ssh/my_private_key.pem
  IdentitiesOnly yes
```

After adding this configuration, you can connect simply with: `ssh my-vm`

### Regional Key Distribution

SSH keys are automatically distributed across all available regions when created or imported:

- **Norway Region:** NORWAY-1
- **Canada Region:** CANADA-1
- **US Region:** US-1

### SSH Key Best Practices

Security and Management Recommendations

#### Key Creation
- Generate separate keys for different projects or environments
- Use descriptive names that identify the key's purpose
- Prefer Ed25519 keys for new generations (more secure)
- Use minimum 2048-bit RSA keys (4096-bit recommended)

#### Key Storage
- Store private keys securely and never share them
- Use passphrase protection for your private keys
- Back up private keys in encrypted storage
- Set correct file permissions (600 for private keys)

#### Key Maintenance
- Regularly audit and rotate your SSH keys
- Remove unused or unnecessary keys promptly
- Monitor key usage and access patterns
- Keep an inventory of where keys are deployed

#### Access Control
- Use separate keys for different team members
- Implement key rotation policies
- Revoke access immediately when team members leave
- Consider using SSH certificates for large teams

### Troubleshooting Common Issues

#### Connection Refused Errors
- Verify the VM is running and accessible
- Check if the correct port (usually 22) is open in firewall rules
- Ensure you're using the correct username for the OS
- Confirm the private key file path is correct

#### Permission Denied Errors
- Check private key file permissions (should be 600)
- Verify the public key was properly added during VM creation
- Ensure you're using the matching private key for the public key
- Try connecting with verbose output: `ssh -v`

#### Key Import Failures
- Ensure the public key is in the correct format (single line, proper prefix)
- Remove any line breaks or extra whitespace
- Verify the key type is supported (RSA, Ed25519, ECDSA)
- Check that the key isn't corrupted or truncated

## Account Management

Your account profile contains essential information for using the platform and processing payments.

### Personal Information

Update your basic personal details:

- **Name:** Full name (required, letters, spaces, hyphens, apostrophes only, 2-100 characters)
- **Email:** Your registered email address (cannot be changed after registration)
- **Phone Number:** Optional contact number (international format supported)

### Billing Address

Complete your billing address to enable payments on the platform:

- **Address Line:** Street address, apartment, suite, etc. (required)
- **City:** City name (optional)
- **State/Province:** State or province name (optional)
- **Postal Code:** Postal or ZIP code (required)
- **Country:** Select your country from the dropdown list (required)

### Payment Information

Your country selection automatically determines the currency used for all transactions:

- **India:** Indian Rupee (₹)
- **European Countries:** Euro (€)
- **All other countries:** US Dollar ($)

### Profile Completion

The system tracks whether your profile has all required information:

- A profile status indicator shows whether your profile is complete
- Complete profiles have the required address information (address line, postal code, and country)
- You must complete your profile to enable payments and credit purchases

**Form Validation**

Input validation requirements:

- **Name:** Only letters, spaces, hyphens, and apostrophes are allowed
- **Phone Number:** Must be in a valid format with digits, plus sign, spaces, dashes, and parentheses only
- **Address Line:** Required field with a maximum of 255 characters
- **City:** Only letters, spaces, hyphens, periods, and apostrophes are allowed
- **State/Province:** Only letters, spaces, and hyphens are allowed
- **Postal Code:** Required field that accepts alphanumeric characters, hyphens, and spaces
- **Country:** Required selection from the provided list

## Credits System

The Credits System allows you to purchase and manage credits to pay for your virtual machine and storage usage on the platform.

### Purchasing Credits

The platform provides a simple process for purchasing credits:

1. Navigate to the Credits page or click "Add Credits" in your account dashboard
2. Choose from predefined credit packages or specify a custom amount:
   - Starter Package: Perfect for small projects
   - Professional Package: Ideal for medium-sized workloads
   - Enterprise Package: For large compute needs
3. Review the payment summary, which includes:
   - Base amount
   - Applicable taxes (GST at 18% is applied for Indian customers)
   - Total amount
4. Click "Proceed to Payment"
5. Complete the payment via Razorpay, our secure payment processor
6. After successful payment, credits are instantly added to your account

**Important Considerations**

Key points about credits:

- Minimum credit purchases vary by currency:
  - USD: $5
  - EUR: €5
  - INR: ₹100
- Your profile must be complete with billing information before making a purchase
- Payment is processed in your local currency based on your profile settings
- All credit purchases are final and non-refundable
- Credits have no expiry date and remain in your account until used
- Credits have no cash value and cannot be withdrawn or converted to cash

### Credit Usage

Credits are automatically deducted from your account based on your resource consumption:

#### Compute Resources
- Credits are consumed based on your VM configuration
- Different GPU types have different consumption rates
- Multiple GPUs increase consumption proportionally
- Billing is calculated in per-minute increments
- You only pay for the exact time your resources are running

#### Storage Resources
Credits are consumed for:
- Volume storage based on provisioned size
- Snapshot storage based on actual size

Storage billing is calculated hourly

### GPU Instance Pricing

| GPU Model | USD | EUR | INR |
|-----------|-----|-----|-----|
| H100-SXM5-80GB | $2.69 per hour | €2.49 per hour | ₹239 per hour |
| H100-PCIe-NVLink-80GB | $2.29 per hour | €2.09 per hour | ₹199 per hour |
| H100-PCIe-80GB | $2.25 per hour | €2.05 per hour | ₹195 per hour |
| A100-SXM4-80GB-NVLink | $1.59 per hour | €1.45 per hour | ₹135 per hour |
| A100-PCIe-80GB | $1.55 per hour | €1.39 per hour | ₹135 per hour |
| L40 | $1.19 per hour | €1.09 per hour | ₹99 per hour |
| RTX-A6000 | $0.69 per hour | €0.45 per hour | ₹49 per hour |
| A40 | $0.69 per hour | €0.45 per hour | ₹49 per hour |

**Frequently Asked Questions**

Common questions about the credit system:

**How does per-minute billing work?**
The platform calculates usage in one-minute increments. You're only charged for the exact time your resources are running, with no minimum usage requirements.

**What happens if I run out of credits?**
When your credit balance runs low, you'll receive notifications. If you run out completely, your resources will be hibernated to prevent data loss.

**Can I transfer credits between different currencies?**
No, credits are maintained in separate balances for each currency (USD, EUR, INR) and cannot be transferred between them.

**Are there any discounts for larger credit purchases?**
For enterprise customers with large workloads, custom pricing plans are available. Contact the sales team for more information.

## Troubleshooting

This section provides solutions to common issues you may encounter when using the platform.

### VM Deployment Issues

#### Insufficient Credits
If you receive an "Insufficient Credits" error during deployment:

1. Navigate to the Credits page
2. Purchase additional credits
3. Return to the deployment page and try again

#### Resource Availability
If your selected GPU type or count is unavailable in the region:

1. Try selecting a different region
2. Reduce the GPU count
3. Select an alternative GPU type
4. Try again later as availability changes frequently

#### SSH Connection Failures
If you can't connect to your VM via SSH:

1. Verify that the VM is in ACTIVE state
2. Check that you're using the correct private key
3. Ensure you're using the correct username for the OS (e.g., "ubuntu" for Ubuntu images)
4. Verify that port 22 is open in your security rules
5. Check the permissions on your private key file (chmod 600)

### Firewall Issues

#### Rule Not Taking Effect
If your firewall rules aren't working as expected:

1. Rules may take up to 10 minutes to fully apply after creation
2. Verify the rule configuration (protocol, ports, IP ranges)
3. Ensure the firewall is properly attached to the VM
4. Check that the VM is in ACTIVE state

#### Cannot Delete Firewall
If you're unable to delete a firewall:

1. Detach the firewall from all VMs first or use the force option
2. Verify the firewall is not in a transitional state

### Volume Issues

#### Volume Attachment Failures
If you can't attach a volume to a VM:

1. Verify VM is in ACTIVE state
2. Confirm volume and VM are in the same region
3. Check that the volume is not already attached to another VM
4. Ensure the VM is not undergoing another operation

#### Volume Detachment Issues
If you can't detach a volume:

1. Ensure the VM is in ACTIVE state
2. Verify that the volume is not the system boot volume
3. Wait a few minutes if a previous attachment or detachment operation was recently performed

#### Volume Creation Problems
If you're having trouble creating a volume:

1. Verify you have entered a valid size (minimum 10GB for standard, 100GB for bootable)
2. Ensure you're using a unique volume name
3. For bootable volumes, confirm you've selected a valid OS image
4. Check that you have sufficient credits for storage allocation

### Snapshot and Image Issues

#### Snapshot Creation Failure
If you're unable to create a snapshot:

1. Verify the VM is in ACTIVE state
2. Check that the VM has sufficient disk space
3. Ensure you have a unique name for the snapshot
4. Wait a few minutes and try again if the VM is under heavy load

#### Image Creation Issues
If you're having trouble creating an image:

1. Verify the snapshot is in a completed state
2. Ensure you have a unique name for the image
3. Check that the snapshot is accessible and has not been deleted
4. Make sure you have sufficient credits for image storage

### Getting Support

If you're experiencing issues that aren't resolved by the troubleshooting steps above, contact our support team:

- Email: support@enterprise-gpu.ai
- Include detailed information about the issue
- Provide relevant error messages or screenshots
- Include your deployment ID and VM IDs if applicable

**Support Checklist**

Information to include when contacting support:

- Account email address
- Deployment ID (format: DEP1234567)
- Date and time when the issue occurred
- Step-by-step description of what you were doing
- Any error messages or codes received
- Region where resources are deployed
- Screenshots of the issue if applicable
