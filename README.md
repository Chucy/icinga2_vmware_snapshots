# icinga2_vmware_snapshots
Icinga2 Check for monitoring the Age und Count of VMware Snapshots.

I modified the Original Check from https://github.com/simonmeggle/check_vmware_snapshots, by changing the Perl Nagios::Plugin to the Monitoring::Plugin. I also added Icinga Command Definitions.

## How to Use
Put the Plugin check_vmware_snapshots.pl in the IcingaPluginDir.
Put the Icinga Command Definitions in your Icinga Configuration Directory.
Add the Checks to your hosts.


## Example
### Services

```
apply Service "Vmware Snapshot Age" {
  check_command = "check_vmware_snapshots_age"
  assign where "vcenter" in host.templates
}
apply Service "Vmware Snapshot Count" {
  check_command = "check_vmware_snapshots_count"
  assign where "vcenter" in host.templates
}
```

### Host
```
object Host "Vcenter"  {
import "vcenter"

address = "192.168.10.100"
display_name = "Vcenter"
vars.snapshot_username = "vcenteruser"
vars.snapshot_password = "userpassword"
  
# More Options
# Age Check
# vars.snapshot_age_warning = 2
# vars.snapshot_age_critical = 7
    
# vars.snapshot_age_separator = ", "
# vars.snapshot_age_blacklist = "test"
# vars.snapshot_age_whitelist = "test"
# vars.snapshot_age_match_names = 1

# Count Check
# vars.snapshot_count_warning = 1
# vars.snapshot_count_critical = 2
    
# vars.snapshot_count_separator = ", "
# vars.snapshot_count_blacklist = "test"
# vars.snapshot_count_whitelist = "test"
# vars.snapshot_count_match_names = 1

}
```
