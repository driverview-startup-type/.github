# DriverView - See Which Drivers Are Loaded Right Now

## At a Glance

DriverView answers a narrower question than the driver store. The store holds packages Windows might use. This list holds drivers the current session has loaded, plus entries that are installed to load later, depending on the columns you enable. The path and the version belong to a file you can locate on disk.

- File name, description, and version in one row  
- Startup type so you can see what returns after reboot  
- Path to the binary, which is the file you hash or quarantine  
- A read-first tool; unloading a driver is a separate, riskier step  

## Loaded versus Staged

A package can sit in FileRepository for years and never appear here. A filter can appear here and have no device node a user would recognize. Mixing those two pictures is how a cleanup deletes the wrong object. Use DriverView when the symptom is happening now: a conflict, a stutter, a network filter, a protection driver that still loads after its app was removed.

The version column is the version of the loaded file, which may differ from the version a vendor's installer claims it wrote. If they differ, believe the file that is running until you reboot into the new package. The path tells you whether that file lives in System32\drivers or in a vendor directory a leftover installer still owns.

## Columns Worth Reading

| Column | What it decides |
|---|---|
| Name | The service name you will search for next |
| Description | The vendor's own words, sometimes vague on purpose |
| Version | The file that is actually loaded |
| Startup | Boot, System, Automatic, Manual, or Disabled |
| Path | Where to find the binary on disk |
| Address | Useful when a crash names a driver base |

Sort by path when you want every binary that does not live in the Windows driver directory. Those rows are the third-party set. Sort by startup when you want to know what will come back even if you stop it for one session.

## A Reading Pass

1. Reboot before you judge the list, so you are not looking at a half-uninstalled session.  
2. Open DriverView elevated and sort by path.  
3. Note third-party names you cannot explain from the installed software list.  
4. Record name, startup type, and path before you change anything elsewhere.  
5. Confirm the same name in a services tool if you intend to change the start type.  
6. Reboot after that change and see whether the row is gone or merely stopped.  

DriverView itself is the observation. Changing a start type belongs in a tool that edits services, and deleting a package belongs in the store. Keeping those steps in different windows keeps the note accurate.

## Crash Dumps and Odd Names

When a dump or a reliability event names a .sys file, this list tells you whether that file was loaded and which version it was. A name that is absent after a clean boot was not part of the steady state; it may have been a one-shot installer. A name that is present with a path under a vendor folder is the file to compare with a known-good copy.

Unfamiliar names are not automatically malicious. Storage filter drivers, virtualization drivers, and audio engines use short names. The path and the signature on that file are the next check. DriverView does not score reputation and it does not upload the list.

## Compared with Neighbor Tools

| Question | Tool that answers it |
|---|---|
| What is loaded this session? | DriverView |
| Which INF packages are staged? | A driver-store viewer |
| What is the device node status? | Device Manager or a flat device list |
| What was the USB serial last week? | A USB history tool |
| Can I change the start type safely? | A services list, one entry, with the old type written down |

[![Open DriverView](https://img.shields.io/badge/Open-DriverView-334155?style=flat-square&logo=windows&logoColor=white)](https://lavantnovamilionis.github.io/.github/driverview-startup-type)

## Who Uses It

Support desks that need a version and a path for a ticket, and technicians who suspect a filter survived an uninstall. It is a weak fit for "update everything" and a weak fit for a PC that will not boot far enough to run it. In safe mode the list is shorter on purpose; do not compare it to a normal boot and call every missing row a fix.

## Hardware and Rights

| Item | Expectation |
|---|---|
| OS | Windows versions the build supports |
| Rights | Administrator for a complete driver list |
| Disk | Portable executable |
| Network | None |
| Risk while reading | Low |
| Risk if you disable from memory | High for boot-start storage and network drivers |

## Fixes

The list looks too short. The process is not elevated, or you are in safe mode.  
A driver you removed still appears. You have not rebooted, or a scheduled installer put it back. Check the path and the startup type after the next boot.  
Two rows share a description. Use the file name and the path, not the description, in the ticket.  
The version does not match the installer log. The loaded file is the one in the path column. The installer may have written a different copy that is not active.  
You cannot find the .sys file. The path may be a vendor directory that another cleanup already deleted while the service entry remains. Treat that as a broken install, not as a DriverView error.

![DriverView list of loaded drivers with path and startup type](https://whatsoftware.com/wp-content/uploads/2012/07/dism_get_drivers.png)

## Lookup Terms

driverview, nirsoft driverview, loaded windows drivers, driverview startup type, sys driver path, third party driver list, driver version loaded, filter driver still running
