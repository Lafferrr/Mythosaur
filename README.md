# Mythosaur

Mythosaur is a Windows tool that helps server staff review potential cheating and rule violations in Minecraft Java Edition. Start in **Overview**, then open the category that reported the finding. Bracketed text in a title stands for a count or name from the scan. Check the finding details before deciding whether the evidence shows possession, loading, or use under your server’s rules.

## Overview

| Detection | Explanation |
| --- | --- |
| **Ban detections** | Lists findings flagged as **BAN** or **BAN DEFINITIVE**. Open the category shown beside each finding for its details. |
| **No ban detections** | The report lists no ban-level findings. Check individual tabs for review flags and scan coverage. |

## Generics

| Detection | Explanation |
| --- | --- |
| **Vulnerable Drivers / kdmapper Executed** | The report associates a driver or loader with activity on the computer. Check the named item and timing. A cheating ban needs evidence tying the activity to prohibited use. |
| **System Event Log Clear (Event 104)** | A Windows event log was cleared. Check which log was affected and whether the timing lines up with the scan or routine maintenance. This can support review under a separate scan-tampering rule. |
| **Security Audit Log Clear (Event 1102)** | The Windows Security log was cleared. Check who performed the action and when, if the details are available. The event alone is insufficient for a cheating ban. |
| **USN Journal Deletion (Event 3079)** | Windows file-change history was deleted. Check the time and any disk maintenance. Treat it as context for a cheating review. |
| **IFEO Debugger Hijacks** | Windows has a setting that redirects the launch of a listed program. Check which program it affects and whether a known debugger or administrative tool explains it. Corroborate before banning. |
| **Prefetch Folder Integrity** | The condition of the Windows Prefetch folder may limit what the report can say about past program launches. Check the folder status shown in the finding. This is context. |
| **Prefetch (EnablePrefetcher)** | Shows the Windows setting for Prefetch. An unusual value can affect launch history. This is context. |
| **ActivitiesCache (EnableActivityFeed)** | Shows the status of the Windows activity history setting. Check whether the device’s normal policy explains the value. This is context. |
| **Amcache hive (Amcache.hve)** | Shows whether a Windows program inventory source is available. An unavailable source limits coverage. This is context. |
| **SRUM database (SRUDB.dat)** | Shows whether a Windows resource-usage record is available. An unavailable source limits coverage. This is context. |
| **System Time Change (Event 4616)** | The system clock changed. Check the previous and new times before comparing events. This is context. |
| **CMD policy (DisableCMD)** | Shows a Windows policy controlling Command Prompt access. Check whether it is expected on the device. This is context. |
| **Registry Tools Policy** | Shows a Windows policy that restricts registry tools. Check the device’s normal administration policy. This is context. |
| **Pagefile Wipe at Shutdown** | Shows whether Windows is configured to clear the pagefile at shutdown. This can reflect a privacy or security policy and is insufficient for a ban. |
| **Named Windows service marked stopped, disabled, or restarted** | Check the specific service, when its state changed, and the device’s usual configuration. A service state alone is insufficient for a cheating ban. |

## Mods

| Detection | Explanation |
| --- | --- |
| **BAN** | The listed mod was flagged as a cheat or for prohibited functionality. Check the exact file, feature, and instance. It can support a ban when the finding establishes what your server prohibits. |
| **INVESTIGATE** | The listed mod or feature needs review. Some mods are allowed on one server and restricted on another. Check the stated reason and any required evidence of use. |
| **UNKNOWN** | The report could not verify this mod. Ask for the exact version and source, then compare it with the documented modpack or official release. Unknown status alone is insufficient for a ban. |
| **UNKNOWN MODS** | The tab contains one or more unverified mods. Open each entry to identify it. The number of unknown mods does not establish cheating. |
| **VERIFIED** | The report verified the mod’s identity. Check whether your server allows that mod and feature. |

## InjectionFucker

| Detection | Explanation |
| --- | --- |
| **BAN DEFINITIVE Mythosaur has detected cheats in the current Minecraft instance.** | Mythosaur confirmed prohibited functionality in the Minecraft instance being scanned. This is its strongest verdict and can support a ban. Verify that the report belongs to the player and instance under review. |
| **Cheat Detection** | The report identifies a cheat associated with Minecraft. Check the named client, the finding’s flag, and the game instance. A **BAN** finding can support enforcement when it establishes what the rule prohibits. |
| **Runtime Verdict** | A verdict about the running Minecraft instance. Read the actual flag and verdict text to determine whether the report supports a ban or calls for review. |
| **Mythosaur Evidence Verdict** | Summarizes the case outcome. Use the written verdict and its scope when deciding how to act. |
| **[Count] Unknown Classes** | The report could not match some loaded pieces of Java code to an expected source. Open the card, check the class names and listed sources, and compare against the same Minecraft version, launcher, mod loader, and modpack. Legitimate mods can create classes while the game runs. |
| **Faked Classes inside of net.minecraft** | A class uses a Minecraft package name unexpectedly. Check the exact game version and the listed owner. Corroborate with evidence of prohibited functionality before banning. |
| **Class Anomalies** | A Java class has an unusual identity or origin. Check its name, source, and whether the installed modpack accounts for it. Corroborate. |
| **Replacement Attacks** | The report flags a game file or component as a possible replacement. Verify the exact version, its expected source, and whether the game used it. Corroborate for a cheating ban. |
| **Library Jar Integrity** | A game dependency differs from the expected copy or has an unresolved integrity result. Check the stated result and compare it with the official file for that version. Corroborate. |
| **Custom ClassLoaders** | Minecraft has an additional component that loads Java code. Identify its owner and check whether the launcher or mod framework accounts for it. Corroborate. |
| **External / In-Memory ClassLoaders** | The report flags a loader associated with an external or memory-resident source. Check which code and instance it is linked to. Corroborate. |
| **ClassLoader Contents** | Lists code associated with a Java class loader. Use the list to identify the owner of another finding. This is context. |
| **Java Agents** | A Java helper has access to the running program. Check the listed agent and whether a known tool accounts for it. Corroborate. |
| **Dynamic Agents** | A Java agent was associated with the JVM after startup. Check which tool attached and when. Corroborate. |
| **Native Agent Libs** | A native library is associated with a JVM agent. Identify the library and its reason for being present. Corroborate. |
| **JVMTI Agents** | An agent is associated with the JVM’s tooling interface. Diagnostic and profiling tools can also use it. Identify the agent and its purpose. Corroborate. |
| **Hidden Agent Evidence** | The report flags possible agent activity with an unresolved identity or origin. Look for a matching component or runtime finding. Corroborate. |
| **Attach API Inventory** | Lists activity or tools associated with Java process attachment. Check the tool, target, and time. This is context unless separate evidence establishes prohibited activity. |
| **MBean Findings** | The report flags a Java management or monitoring component. Identify what it belongs to and why it was present. Corroborate. |
| **JVM Arg Flags** | A Java launch argument was flagged. Compare it with the expected launcher settings and check any named program. This is context. |
| **Env Var Flags** | An environment setting that can affect the game or Java was flagged. Check whether the launcher or system configuration explains it. This is context. |
| **Boot ClassPath Flags** | A Java startup setting changes where Java can load some classes from. Check the referenced path and owner. Corroborate. |
| **Unusual Working Directory** | The process started with an unexpected working folder. Check the launcher and instance configuration. This is context. |
| **Bytecode Transform** | Java code was changed. Mod frameworks can do this legitimately. Check which mod changed what and whether another finding establishes prohibited functionality. Corroborate. |
| **JNI Function Table Hooks** | The report flags redirected calls at the boundary between Java and native code. Identify the responsible component and its purpose. Corroborate. |
| **JVM Vtable / Table Hooks** | The report flags redirected calls inside the JVM. Check the owner and any related evidence of game changes. Corroborate. |
| **Inline Detour Hooks** | A code path was redirected. Check which component owns the change and where it leads. Corroborate. |
| **IAT Redirections** | A call a module makes to another library goes to an unexpected destination. Identify the module and destination. Corroborate. |
| **Export Table Redirections** | A function exposed by a library points to an unexpected destination. Identify the library and the destination named in the report. Corroborate. |
| **JNI Native Bindings** | Java code is linked to native functions. Check which Java component and native module are involved. This is context unless the link establishes prohibited activity. |
| **Native Libraries** | Lists or flags a library used by the process. Identify the publisher and the reason the game loaded it. Library presence alone is insufficient for a ban. |
| **Native Injection** | The report flags native code introduced into a process. Verify the target, code owner, and any evidence of what it did. It can support a ban when the evidence establishes prohibited activity. |
| **Module Stomping / Hollowing** | The report flags a mismatch between a listed executable component and the code associated with it. Verify the affected process and component. Corroborate. |
| **Reflective DLL / Manual Mapping** | The report flags a native library loaded in an unusual way. Verify its owner and its link to the game. Corroborate. |
| **VAD Ghosting / Phantom Modules** | An executable memory region has an unclear link to a normally listed module. Check its owning process and related findings. Corroborate. |
| **Corroborated Injection Sites** | Several observations point to the same possible injection site. Check the affected process, what the observations establish, and whether they identify prohibited code. |
| **Suspicious Threads** | A running thread was flagged for an unusual owner or activity. Check its process and related module. Corroborate. |
| **Remote Thread Injection** | The report flags a thread that may have been started from another process. Check the source and target. Corroborate. |
| **Unbacked Native Threads** | A thread is associated with code without a clear loaded-module owner. Check the memory owner and whether legitimate runtime-generated code explains it. Corroborate. |
| **Native Memory Anomaly** | An unusual native memory finding needs review. Check which process and region it refers to. Corroborate. |
| **Orphan Executable Memory** | Executable memory has no identified module owner. Check for related process or module evidence. Corroborate. |
| **Deadlock Evidence** | Threads appear to be stuck waiting on one another. Check for ordinary game or mod problems. This is context. |
| **Unloaded Module Trace** | The report found a reference to a module that was previously loaded. Check the module, process, and timing. Corroborate if your rule requires proof of use. |
| **Client References** | A reference to a client was found. Check the exact reference and source. A reference alone is insufficient for a ban. |
| **[Count] Unknown Jar(s) Executed** | The report flags historical references to Java archives. Open the card to see what the source actually establishes about the file and timing. Require stronger evidence if your rule prohibits in-game use. |
| **Historical Class File References** | A past reference to a Java class file was found. Identify the file and time. This is context. |
| **Suspicious Native in Temp Folder** | A native file in a temporary folder was flagged. Verify what it is and whether it was used with Minecraft. The location alone is insufficient. |
| **Service Artifacts** | A Windows service record was flagged. Check the service owner and historic timing. Corroborate. |
| **Service / Process Memory** | A finding comes from the memory of a service or process. Identify the owner and establish what links it to Minecraft. Corroborate. |
| **Pipe Anomalies** | A communication channel between programs was flagged. Check the programs involved. Corroborate. |
| **Foreign Process Handle Forensics** | Another process had access to Minecraft. Identify it and check for an expected purpose such as an overlay. Access alone is insufficient for a ban. |
| **Window Anomalies** | A window was flagged for review. Identify its application and purpose. Corroborate. |
| **AMSI / ETW Bypass** | The report flags possible interference with Windows security or event reporting. Identify the affected program and check whether the finding relates to the game. Corroborate. |
| **API-Hash Shellcode** | Unidentified native code was flagged as suspicious. Identify the code owner and process before drawing a conclusion. Corroborate. |
| **Code Execution Primitives** | A component exposes a way to run code. Check whether the report shows it was used for a prohibited purpose. Capability alone is insufficient. |
| **HWID License / Fingerprint Locks** | A program appears to associate a license or access control with a particular device. Identify the program. Ordinary licensing is context. |
| **C2 / License Server Communication** | Network or licensing activity was flagged. Check which program communicated and whether the destination belongs to it. This activity alone is insufficient for a ban. |
| **OS-Level Findings** | A Windows-level observation needs review. Read the specific finding and confirm its scope. Apply ban guidance to the underlying evidence. |
| **Timeline Events** | Shows when report events occurred. Use the timeline to verify whether findings overlap the game session. This is context. |
| **USN Journal** | Shows Windows file-change events. Check the file and whether the record shows creation, deletion, or another change. A file-change event alone is insufficient for a use-based ban. |
| **Behavioral Deviation** | The report flags activity that differs from its expected behavior. Check the described action and look for corroborating evidence. |
| **Mythosaur Finding** | A case-specific observation. Read its title, classification, and scope before deciding how it applies to your server’s rules. |

## Strings

| Detection | Explanation |
| --- | --- |
| **Hidden cheat features** | The report associated specific cheat-feature text with a source. Review the named feature and its owner. A **BAN** finding can support enforcement if it establishes what the rule prohibits. |
| **string "[text]" → cheat feature [feature]** | The report associates a readable term with a cheat feature. Read the full phrase and check the owner. Generic or unattributed text is insufficient for a ban. |
| **Encrypted In-Memory Pattern** | The report found an encoded pattern associated with a known term in memory. Check whether the term is specific and whether the owner is known. Corroborate. |
| **Present in memory, absent from scanned JARs** | The term was found in memory and did not appear in the JARs covered by the scan. Check the source and look for a linked finding. This alone is insufficient for a ban. |
| **String encryption** | The report describes encoded text and its recovery status. Check whether the result identifies a specific prohibited feature. The existence of encryption alone is insufficient. |
| **[Count] Strings Encrypted by [name] ([file])** | Groups entries the report attributes to the same source of decoded text. Check which entries were actually recovered and what they say. A count alone is insufficient. |
| **String concealment technique(s)** | The report flags text that was obscured. Review the associated item and any separately identified feature. Corroborate. |
| **Concealment technique(s)** | A native-program finding flags obscured content. Check which program it belongs to and whether there is a related prohibited feature. Corroborate. |
| **All decrypted strings** | Lists decoded text for review. The list is informational. Use any relevant entries alongside their source and classification. |

## MacroScanner

| Detection | Explanation |
| --- | --- |
| **[Tool] executed** | The named tool has an execution-related finding. Check which tool ran and when. A confirmed prohibited tool can support a ban if the rule covers that activity. |
| **[Program] ran [script]** | The report names a script run by a program. Check what the script did and when it ran. A scripting program alone is insufficient for a ban. |
| **[Program] ran inline code** | A command ran code directly. Review the action described and its connection to Minecraft. It can support a ban when it establishes prohibited automation. |
| **[Program]: [module]** | The report names a module associated with a scripting program. Verify what the module does and whether the evidence links it to the session. Corroborate. |
| **Fileless remote script loader ([program])** | The report flags activity involving a remotely supplied script. Check what action is identified and whether it relates to Minecraft. Corroborate. |
| **[Packer] program [name] ran** | An executable was flagged as packed and associated with execution. Identify the program. Packing alone is insufficient. |
| **[Vendor]: [profile]** | A named peripheral profile or macro was found. Check its assignment and whether the rule covers configuration or in-game use. |
| **Low debounce** | A peripheral setting affects how quickly it registers input. Compare it with any specific server rule. The setting alone does not establish automation. |
| **Hardware macro device** | A device associated with programmable input was flagged. Confirm the device and check for evidence of the prohibited action. Device presence alone is insufficient for a use-based ban. |
| **Interception input-injection driver** | Interception was installed or loaded. Check the reported status and whether a specific program used it with Minecraft. Driver presence alone is insufficient for a use-based ban. |
| **vJoy virtual input driver** | vJoy was installed or loaded. It can provide a virtual joystick for legitimate applications. Check for evidence connecting it to a prohibited action. |
| **ViGEmBus virtual controller driver** | ViGEmBus was installed or loaded. It can provide a virtual controller. The driver alone is insufficient for a ban. |
| **HidHide HID device-hiding driver** | HidHide was installed or loaded. It can manage which applications see input devices. Verify the context before drawing a conclusion. |
| **RawAccel mouse acceleration driver (informational)** | RawAccel was installed or loaded. It adjusts mouse movement. This is context. |
| **[Device type] unplugged during the instance** | A device was disconnected during the game session. Check the device and timing if it relates to another finding. A disconnect alone is insufficient for a ban. |
| **[Device type] connected during the instance** | A device was connected during the game session. Check its identity and any separate evidence of prohibited use. A connection alone is insufficient for a ban. |
| **[Count] active pointing devices connected** | The report lists multiple connected pointing devices. A mouse, touchpad, or other device can account for the count. This is context. |
| **Execution timeline** | Lists recorded execution times. **Since boot** covers a wider window than the Minecraft session. Use the timeline as context. |
| **Evidence sources checked** | Shows what the scan could review. Use it to assess coverage. This is context. |

## Volatility

| Detection | Explanation |
| --- | --- |
| **Reflective / manual-mapped PE in Minecraft (PID [number])** | The report found an executable component in the named Minecraft process that was loaded in an unusual way. Identify the component and what it does before treating it as prohibited code. |
| **BYOVD kernel loader driver loaded: [driver]** | The named driver was loaded at scan time. Check whether it is associated with prohibited activity in Minecraft. A loaded driver alone is insufficient for a cheating ban. |
| **Unlinked executable image in Minecraft (PID [number])** | An executable image was present in the named Minecraft process without a corresponding ordinary module entry. Identify the image and corroborate before banning. |
| **PE / reflective DLL injection** | An executable component was flagged in process memory. Verify the process and component. It can support a ban if the evidence links it to prohibited code in Minecraft. |
| **Process hollowing / unlinked module** | An executable or library is not accounted for by the process’s expected module information. Check the owning process and related evidence. Corroborate. |
| **Suspicious unbacked thread** | A thread is associated with code whose module could not be identified. Check the thread’s process and related memory findings. Corroborate. |
| **BYOVD / vulnerable kernel loader driver** | A vulnerable driver or associated loader was flagged. Identify the driver and look for a verified link to Minecraft. Driver presence alone is insufficient. |
| **Hidden / unlinked kernel driver** | A suspected driver lacks a clear entry in ordinary driver information. Check its identity and related findings. Corroborate. |
| **Manually mapped kernel driver (kdmapper)** | The report flags unusual driver-loading activity. Check the named driver, timing, and evidence of its purpose. Corroborate. |
| **Fileless execution** | The report flags execution without a clearly identified program file. Check the described command or activity and its link to the session. Corroborate. |
| **Suspicious LOLBin** | A legitimate Windows tool was flagged for how it was used. Review the reported action before attributing it to cheating. Corroborate. |
| **External process handle to Minecraft** | Another program had access to the Minecraft process. Identify it and check for normal explanations. Access alone is insufficient for a ban. |
| **Recovered commands** | Lists commands found during the scan. Check the source, time, and related finding before assigning a command to the player. This is context. |
| **Processes in the dump** | Lists processes visible in the captured memory. Process presence alone is insufficient for a ban. |
| **Tier 1 (Live Minecraft & Process Memory)** | Indicates that a result comes from live process checks. Review any unavailable checks before interpreting the result. This is context. |
| **Tier 2 (Live Kernel Memory)** | Indicates that a result comes from a kernel-memory capture. Check the coverage before drawing conclusions about Minecraft’s own process memory. This is context. |
| **Tier 3 (Full RAM Dump — DumpIt)** | Indicates that a result comes from a system-memory capture. Check the reported owner and coverage before attributing a hit to Minecraft. This is context. |

## Alts

| Detection | Explanation |
| --- | --- |
| **MINECRAFT** | A Minecraft account name appears in the report. Check the account ID and server records before attributing it to a player. Account presence alone is insufficient for a ban. |
| **DISCORD** | A Discord account name appears in the report. Shared computers can contain accounts from multiple people. Account presence alone is insufficient for a ban. |
| **Possible Old IGN** | A Minecraft name may have been used previously. Verify the account ID or server records before linking it to a player or an existing ban. |
| **Minecraft Accounts ([count])** | Counts Minecraft account entries listed in the report. This is context. |
| **Discord Accounts ([count])** | Counts Discord account entries listed in the report. This is context. |
| **1 ACCOUNT** | The report lists one account entry. This is informational. |
| **[Count] ACCOUNTS** | The report shows how many account entries were listed. This is informational. |

## Report flags

| Detection | Explanation |
| --- | --- |
| **BAN DEFINITIVE** | Mythosaur confirmed prohibited functionality in the current Minecraft instance. See the full banner in InjectionFucker. |
| **BAN** | A category flagged an item as ban-level evidence. Check whether the finding establishes what the server rule prohibits. |
| **STRONGLY SUSPICIOUS** | The findings warrant prompt manual review. Corroborate before banning. |
| **SUSPICIOUS** | The report identifies a concern that requires context and corroboration. |
| **INVESTIGATE** | Review the item and any related evidence. The flag alone is insufficient for a ban. |
| **INFORMATIONAL** | The entry provides context for other findings. |
| **INFO** | A short label for an informational entry. |
| **VERDICT** | Marks an outcome card. Read the classification shown with it. |
| **CLEAN** | The completed check reported no issue within its scope. |
| **NO EVIDENCE IDENTIFIED** | The completed checks found no evidence of concern in the area described. Review any stated coverage limits. |
| **INCONCLUSIVE** | The available results were insufficient to reach a conclusion. Check whether required results were incomplete or unavailable. |
| **N/A** | A result or score is unavailable for that view. |
