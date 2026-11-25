# Mythosaur

Mythosaur is a Windows forensic scanner built for Minecraft Java Edition screenshares and cheat investigations. It combines live JVM & native injection analysis, mod verification, in-memory string decryption, macro/peripheral forensics, memory & self-destruct analysis, and alt account discovery into a single interactive HTML report.

---

## How to Use

1. **Run `Mythosaur.exe` as Administrator**
2. **Enter your 6-digit Scan Code**:
   - Launching Mythosaur generates a unique **6-digit code** tied to your PC name in the Discord code channel.
   - Each code is valid for **10 minutes**. Once used, the code is crossed out in Discord; if you close the app before scanning, the pending code is automatically removed.
3. **Click `Start Scan`** (or press `Enter`).
4. **View Results**:

### How to Get a Scan Code

Access to scan codes is available to:
- **Friends**
- **Server Boosters**
- **Anyone who stars this repository** (`⭐ Star` at the top right of this page)

Here is the discord: https://discord.gg/z33yQ58QTk

---

## Reading the Report

Start in **Overview**, then open the category that reported the finding. Bracketed text in a title stands for a count or name from the scan. Check the finding details before deciding whether the evidence shows possession, loading, or use under your server’s rules.

## Overview

| Detection | Explanation |
| --- | --- |
| **Ban detections** | Lists findings flagged as **BAN** or **BAN DEFINITIVE**. When Mythosaur confirms cheats in the current Minecraft instance, its **BAN DEFINITIVE** finding is pinned at the very top above all other detections. |
| **Clean** | Displayed in green when Overview or any category tab has no detections. |

## Generics

| Detection | Explanation |
| --- | --- |
| **Faker / 2-PC MITM Proxy** | Detects `o1seth/faker` and 2-PC Windows Mobile Hotspot MITM proxies on the clean PC — checks for Windows ICS hotspot gateways (`192.168.137.x`), Windows PCs acting as hotspot routers (TTL=128 + Wi-Fi Direct locally-administered MAC or open Windows RPC/SMB ports, catching Faker's DHCP bypass), and `javaw.exe` connections to local/LAN port `25565`. |
| **2-PC Network & Serial Bridges** | Flags non-browser processes maintaining established LAN/RFC1918 connections on non-standard ports or USB-to-serial / microcontroller bridges (KMBox, Makcu, CH340, CP210x, FTDI, Arduino, RP2040) commonly used in 2-PC setups. |
| **Private Proxies & Tunnels** | Flags active Windows system proxies, `HTTP_PROXY`/`HTTPS_PROXY` variables, `netsh portproxy` rules, local proxy listeners, or active tunnel clients (`v2ray`, `xray`, `clash`, `sing-box`, `proxifier`, `ngrok`, `cloudflared`, `frpc`). |
| **Network Drives & Remote Shares** | Lists mapped SMB/WebDAV network drives (`HKCU\Network`) or active WebDAV/UNC executions that can run cheats from a second PC or remote share without writing locally. |
| **NTFS Alternate Data Streams (ADS)** | Scans user and Minecraft directories for hidden NTFS Alternate Data Streams. Flags executable, DLL, script, or JAR (`MZ`/`PK`) payloads hidden inside ADS as **BAN**, and other non-standard streams as **INVESTIGATE**. |
| **PCIe DMA / FPGA Hardware** | Enumerates PCIe devices for known FPGA/DMA board IDs (Xilinx, Altera, PCILeech, Squirrel, Screamer, CaptainDMA, Enigma, LeetDMA) and unbound/failed-driver PCIe endpoints. |
| **Kernel DMA & HVCI Protection** | Checks whether both HVCI (Memory Integrity) and default Kernel DMA protection policies are explicitly disabled. |
| **EFI / Fileless EFI & Boot Integrity** | Checks BCD boot integrity flags (`TESTSIGNING`, `DISABLE_INTEGRITY_CHECKS`, `DEBUG`), custom non-Windows `.efi` boot paths, UEFI Secure Boot state, and suspicious UEFI NVRAM variables used by fileless EFI mappers. |
| **SMM & Firmware Flash Drivers** | Checks registered Windows services for raw physical-memory, MSR, or SPI/SMM firmware-flashing drivers (`RwDrv`, `chipsec`, `EfiGuard`, `DirectIo`, `PhyMem`, `WinRing0`). |
| **Hypervisor Integrity (CPUID / Timing)** | Uses `CPUID` and `RDTSC` timing checks to distinguish bare metal and legitimate `Microsoft Hv` (Hyper-V/VBS) from unauthorized, spoofed, or stealth EPT/NPT hypervisors. |
| **Vulnerable Drivers / kdmapper Executed** | The report associates a driver or loader with activity on the computer. Check the named item and timing. A cheating ban needs evidence tying the activity to prohibited use. |
| **System Event Log Clear (Event 104)** | A Windows event log was cleared. Check which log was affected and whether the timing lines up with the scan or routine maintenance. |
| **Security Audit Log Clear (Event 1102)** | The Windows Security log was cleared. Check who performed the action and when, if the details are available. |
| **USN Journal Deletion (Event 3079)** | Windows file-change history was deleted. Check the time and any disk maintenance. |
| **IFEO Debugger Hijacks** | Windows has a setting that redirects the launch of a listed program. Check which program it affects and whether a known debugger or administrative tool explains it. |
| **Prefetch Folder Integrity** | The condition of the Windows Prefetch folder may limit what the report can say about past program launches. |
| **Prefetch (EnablePrefetcher)** | Shows the Windows setting for Prefetch. An unusual value can affect launch history. |
| **ActivitiesCache (EnableActivityFeed)** | Shows the status of the Windows activity history setting. |
| **Amcache hive (Amcache.hve)** | Shows whether the Windows program inventory source is available. |
| **SRUM database (SRUDB.dat)** | Shows whether the Windows resource-usage record is available. |
| **System Time Change (Event 4616)** | The system clock changed. Check the previous and new times before comparing events. |
| **CMD policy (DisableCMD)** | Shows a Windows policy controlling Command Prompt access. |
| **Registry Tools Policy** | Shows a Windows policy that restricts registry tools. |
| **Pagefile Wipe at Shutdown** | Shows whether Windows is configured to clear the pagefile at shutdown. |
| **Named Windows service marked stopped, disabled, or restarted** | Check the specific service, when its state changed, and the device’s usual configuration. |

## Mods

| Detection | Explanation |
| --- | --- |
| **BAN** | The listed mod was flagged as a known cheat mod or for prohibited combat/automation bytecode. |
| **INVESTIGATE** | The listed mod or feature needs review (such as policy mods like minimaps, freecam, or inventory macros). Fullbright mods are always allowed, and Litematica is not flagged as a policy mod. |
| **UNKNOWN** | The JAR could not be verified on Modrinth (verified via direct TLS SHA-512 + SHA-1 + `cdn.modrinth.com` matching with `hosts`/DNS integrity checks). Unknown status alone is insufficient for a ban. |
| **UNKNOWN MODS** | The tab contains one or more unverified mods. Open each entry to identify it. |
| **Jar Loaded outside of Mods** | A JAR was loaded into the running Minecraft instance via `-javaagent:` or `-cp` outside the `mods` folder (excluding official Minecraft version JARs, known benign libraries, and Modrinth’s `theseus.jar`). Check the reported path. |
| **Unknown library JAR loaded in Minecraft classpath** | An unrecognized library JAR was loaded on Minecraft’s classpath. Inspect its path and bytecode findings. |
| **VERIFIED** | The mod’s SHA-512 and SHA-1 hashes matched an official Modrinth release (or an allowed Fullbright mod). |

## InjectionFucker

| Detection | Explanation |
| --- | --- |
| **BAN DEFINITIVE — Mythosaur has detected cheats in the current Minecraft instance.** | Mythosaur confirmed prohibited functionality or verified runtime cheat/injection evidence in the Minecraft instance being scanned. Pinned at the very top of Overview and InjectionFucker. |
| **Dump cross-reference: [finding]** | Cross-references live JNI/JVMTI/module checks against kernel/RAM dump findings (manually mapped drivers, reflective PE injection, unbacked threads, external handles, unloaded modules, self-destruct remnants) that survive self-destruct. |
| **[Count] Unknown Classes** | The report could not match some loaded pieces of Java code to an expected source. Open the card, check the class names and listed sources, and compare against the same Minecraft version, launcher, mod loader, and modpack. |
| **Faked Classes inside of net.minecraft** | A class uses a Minecraft package name unexpectedly. Check the exact game version and the listed owner. Corroborate before banning. |
| **Class Anomalies** | A Java class has an unusual identity or origin. Check its name, source, and whether the installed modpack accounts for it. Corroborate. |
| **Replacement Attacks** | The report flags a game file or component as a possible replacement. Verify the exact version, its expected source, and whether the game used it. Corroborate. |
| **Library Jar Integrity** | A game dependency differs from the expected copy or has an unresolved integrity result. Compare it with the official file for that version. Corroborate. |
| **Custom ClassLoaders** | Minecraft has an additional component that loads Java code. Identify its owner and check whether the launcher or mod framework accounts for it. Corroborate. |
| **External / In-Memory ClassLoaders** | The report flags a loader associated with an external or memory-resident source. Check which code and instance it is linked to. Corroborate. |
| **ClassLoader Contents** | Lists code associated with a Java class loader. Use the list to identify the owner of another finding. |
| **Java Agents** | A Java helper has access to the running program. Check the listed agent and whether a known tool accounts for it. Corroborate. |
| **Dynamic Agents** | A Java agent was associated with the JVM after startup. Check which tool attached and when. Corroborate. |
| **Native Agent Libs** | A native library is associated with a JVM agent. Identify the library and its reason for being present. Corroborate. |
| **JVMTI Agents** | An agent is associated with the JVM’s tooling interface. Diagnostic and profiling tools can also use it. Identify the agent and its purpose. Corroborate. |
| **Hidden Agent Evidence** | The report flags possible agent activity with an unresolved identity or origin. Look for a matching component or runtime finding. Corroborate. |
| **Attach API Inventory** | Lists activity or tools associated with Java process attachment. Check the tool, target, and time. |
| **MBean Findings** | The report flags a Java management or monitoring component. Identify what it belongs to and why it was present. Corroborate. |
| **JVM Arg Flags** | A Java launch argument was flagged. Compare it with the expected launcher settings and check any named program. |
| **Env Var Flags** | An environment setting that can affect the game or Java was flagged. Check whether the launcher or system configuration explains it. |
| **Boot ClassPath Flags** | A Java startup setting changes where Java can load some classes from. Check the referenced path and owner. Corroborate. |
| **Unusual Working Directory** | The process started with an unexpected working folder. Check the launcher and instance configuration. |
| **Bytecode Transform** | Java code was changed. Mod frameworks can do this legitimately. Check which mod changed what and whether another finding establishes prohibited functionality. Corroborate. |
| **JNI Function Table Hooks** | The report flags redirected calls at the boundary between Java and native code. Identify the responsible component and its purpose. Corroborate. |
| **JVM Vtable / Table Hooks** | The report flags redirected calls inside the JVM. Check the owner and any related evidence of game changes. Corroborate. |
| **Inline Detour Hooks** | A code path was redirected. Check which component owns the change and where it leads. Corroborate. |
| **IAT Redirections** | A call a module makes to another library goes to an unexpected destination. Identify the module and destination. Corroborate. |
| **Export Table Redirections** | A function exposed by a library points to an unexpected destination. Identify the library and destination named in the report. Corroborate. |
| **JNI Native Bindings** | Java code is linked to native functions. Check which Java component and native module are involved. |
| **Native Libraries** | Lists or flags a library used by the process. Identify the publisher and the reason the game loaded it. |
| **Native Injection** | The report flags native code introduced into a process. Verify the target, code owner, and any evidence of what it did. |
| **Module Stomping / Hollowing** | The report flags a mismatch between a listed executable component and the code associated with it. Verify the affected process and component. Corroborate. |
| **Reflective DLL / Manual Mapping** | The report flags a native library loaded in an unusual way. Verify its owner and its link to the game. Corroborate. |
| **VAD Ghosting / Phantom Modules** | An executable memory region has an unclear link to a normally listed module. Check its owning process and related findings. Corroborate. |
| **Corroborated Injection Sites** | Several observations point to the same possible injection site. Check the affected process and what the observations establish. |
| **Suspicious Threads** | A running thread was flagged for an unusual owner or activity. Check its process and related module. Corroborate. |
| **Remote Thread Injection** | The report flags a thread that may have been started from another process. Check the source and target. Corroborate. |
| **Unbacked Native Threads** | A thread is associated with code without a clear loaded-module owner. Check the memory owner and whether legitimate runtime-generated code explains it. Corroborate. |
| **Native Memory Anomaly** | An unusual native memory finding needs review. Check which process and region it refers to. Corroborate. |
| **Orphan Executable Memory** | Executable memory has no identified module owner. Check for related process or module evidence. Corroborate. |
| **Deadlock Evidence** | Threads appear to be stuck waiting on one another. Check for ordinary game or mod problems. |
| **Unloaded Module Trace** | The report found a reference to a module that was previously loaded. Check the module, process, and timing. Corroborate. |
| **Client References** | A reference to a client was found. Check the exact reference and source. A reference alone is insufficient for a ban. |
| **[Count] Unknown Jar(s) Executed** | The report flags historical references to Java archives. Open the card to see what the source actually establishes about the file and timing. |
| **Historical Class File References** | A past reference to a Java class file was found. Identify the file and time. |
| **Suspicious Native in Temp Folder** | A native file in a temporary folder was flagged. Verify what it is and whether it was used with Minecraft. |
| **Service Artifacts** | A Windows service record was flagged. Check the service owner and historic timing. Corroborate. |
| **Service / Process Memory** | A finding comes from the memory of a service or process. Identify the owner and establish what links it to Minecraft. Corroborate. |
| **Pipe Anomalies** | A communication channel between programs was flagged. Check the programs involved. Corroborate. |
| **Foreign Process Handle Forensics** | Another process had access to Minecraft. Identify it and check for an expected purpose such as an overlay. |
| **Window Anomalies** | A window was flagged for review. Identify its application and purpose. Corroborate. |
| **AMSI / ETW Bypass** | The report flags possible interference with Windows security or event reporting. Identify the affected program and check whether it relates to the game. Corroborate. |
| **API-Hash Shellcode** | Unidentified native code was flagged as suspicious. Identify the code owner and process before drawing a conclusion. Corroborate. |
| **Code Execution Primitives** | A component exposes a way to run code. Check whether the report shows it was used for a prohibited purpose. |
| **HWID License / Fingerprint Locks** | A program appears to associate a license or access control with a particular device. Identify the program. |
| **C2 / License Server Communication** | Network or licensing activity was flagged. Check which program communicated and whether the destination belongs to it. |
| **OS-Level Findings** | A Windows-level observation needs review. Read the specific finding and confirm its scope. |
| **Timeline Events** | Shows when report events occurred. Use the timeline to verify whether findings overlap the game session. |
| **USN Journal** | Shows Windows file-change events. Check the file and whether the record shows creation, deletion, or another change. |
| **Behavioral Deviation** | The report flags activity that differs from its expected behavior. Check the described action and look for corroborating evidence. |
| **Mythosaur Finding** | A confirmed or high-confidence structural/injection observation produced by Mythosaur’s live JVM and native analysis. |

## Strings

Scans **both** disk JARs (mods, nested JARs, `-javaagent`/`-cp` JARs) **and** live `javaw.exe` private memory (carving in-memory `.class` files and running the bytecode string-decryptor emulator on them, so clients loaded outside of `mods` or self-destructed are still caught).

| Detection | Explanation |
| --- | --- |
| **[Client] detected** | Known cheat client detection (e.g., Bloom Client, Doomsday, etc.) pinned at the very top of Strings above all individual module hits. |
| **[Feature] module** | Identifies a cheat feature string recovered from a JAR, native binary, or live JVM memory (plaintext or decrypted by the JVM string-decryptor emulator). Expand to see the matched term and source. |

## MacroScanner

| Detection | Explanation |
| --- | --- |
| **Koffi executed since boot** | Consolidated detection for Electron/Node processes loading `koffi.node` (live + kernel/RAM dump forensics), detailing which app loaded it, bound Win32 APIs (`SendInput`, `mouse_event`, `GetAsyncKeyState`, `WriteProcessMemory`, etc.), loaded DLLs, and file paths. |
| **[Tool] executed** | The named tool has an execution-related finding. Check which tool ran and when. |
| **[Program] ran [script]** | The report names a script run by a program. Check what the script did and when it ran. |
| **[Program] ran inline code** | A command ran code directly. Review the action described and its connection to Minecraft. |
| **[Program]: [module]** | The report names a module associated with a scripting program. Verify what the module does and whether the evidence links it to the session. |
| **Fileless remote script loader ([program])** | The report flags activity involving a remotely supplied script fetched and executed in memory. |
| **[Packer] program [name] ran** | An executable was flagged as packed (PyInstaller, compiled AHK/AutoIt, Node pkg) and associated with execution. Check bundled input-automation modules. |
| **[Vendor]: [profile]** | A named peripheral profile, Lua script, rapid-fire macro, or config modification/deletion (Logitech G HUB, Razer Synapse, Corsair iCUE, SteelSeries GG, Bloody, Glorious Core, HyperX, ROCCAT, Redragon, X-Mouse, reWASD). |
| **[Vendor] deleted macro remnant in RAM/kernel dump** | Deleted peripheral macro file or inline Lua macro artifact recovered from memory dump correlation. |
| **Low debounce** | A peripheral setting affects how quickly it registers input. Compare it with any specific server rule. |
| **Hardware macro device** | A device associated with programmable input was flagged. Confirm the device and check for evidence of prohibited use. |
| **Interception input-injection driver** | Interception was installed or loaded. Check the reported status and whether a specific program used it with Minecraft. |
| **vJoy virtual input driver** | vJoy was installed or loaded. Check for evidence connecting it to a prohibited action. |
| **ViGEmBus virtual controller driver** | ViGEmBus was installed or loaded. The driver alone is insufficient for a ban. |
| **HidHide HID device-hiding driver** | HidHide was installed or loaded. Verify the context before drawing a conclusion. |
| **RawAccel mouse acceleration driver (informational)** | RawAccel was installed or loaded. It adjusts mouse movement. |
| **[Device type] unplugged during the instance** | A device was disconnected during the game session. |
| **[Device type] connected during the instance** | A device was connected during the game session. |
| **[Count] active pointing devices connected** | The report lists multiple connected pointing devices. |

## Memory

| Detection | Explanation |
| --- | --- |
| **[Program] ran code in memory** | True fileless execution (no file on disk): a command fetched or decoded code and ran it directly in memory. Displays the **Command** and the recovered **Code block** executed in memory. |
| **Injected PE payload ([payload]) in [process] (PID [number])** | Unbacked executable PE/DLL payload detected across **all running processes** (reflective/manual-mapped PE, `NtMapViewOfSection` mapped-section PE, or headerless/wiped-MZ PE). Displays the **Method**, **Payload** identity (export DLL name, exports, PDB path, APIs/markers, SHA-256), **Injected by** attribution, and **Status** (still active in memory vs unloaded/self-destructed). |
| **Code-cave injection in [module] inside [process] (PID [number])** | Copy-on-Write (`QueryWorkingSetEx` private `.text` page) + on-disk `.text` diff detected `0xCC`/`0x00` padding inside a loaded DLL overwritten with live shellcode/PIC payload. Displays the stomped module, modified byte count, payload SHA-256, markers, injector attribution, and live status. |
| **Module stomping in [module] inside [process] (PID [number])** | Copy-on-Write (`QueryWorkingSetEx` private `.text` page) + on-disk `.text` diff detected executable `.text` code inside a loaded DLL overwritten in memory. Displays the stomped module, modified byte count, payload SHA-256, markers, injector attribution, and live status. |
| **Unloaded module in [process]: [dll]** | Reads Windows `ntdll!RtlpUnloadEventTrace` to flag non-system or known cheat/injector DLLs that were loaded into Minecraft or Discord and later unloaded (`FreeLibrary` / self-destruct). |
| **De-executable / hidden PE remnant in [process] (PID [number])** | Detects private `PAGE_READWRITE` (non-executable) memory containing a PE header or stripped `.text`/`.rdata` + `GetProcAddress` left behind when a payload strips execute permissions instead of freeing. |
| **Unloaded / self-destructed payload remnant in [process] (PID [number])** | Detects surviving overlay/backend remnants (such as Dear ImGui Win32/OpenGL3/DX11/DX12 backends) in private RW heap memory after the code image has been unloaded. |
| **Reflective / manual-mapped PE in Minecraft (PID [number])** | An executable component in the Minecraft process loaded without a normal module backing. Identify the component and what it does. |
| **BYOVD kernel loader driver loaded: [driver]** | A known vulnerable BYOVD driver (`iqvw64e.sys`, `rtcore64.sys`, `dbutil_2_3.sys`, `capcom.sys`, etc.) is loaded in kernel memory. |
| **Unlinked executable image in Minecraft (PID [number])** | An executable image was present in the Minecraft process without a corresponding ordinary module entry. |
| **PE / reflective DLL injection** | An executable component was flagged in process memory. Verify the process, payload, and attribution. |
| **Process hollowing / unlinked module** | An executable or library is not accounted for by the process’s expected module information. |
| **Suspicious unbacked thread** | A thread is associated with code whose module could not be identified. |
| **BYOVD / vulnerable kernel loader driver** | A vulnerable driver or associated loader was flagged. |
| **Hidden / unlinked kernel driver** | A suspected driver lacks a clear entry in ordinary driver information. |
| **Manually mapped kernel driver (kdmapper)** | Memory traces consistent with a manually mapped kernel driver. |
| **External process handle to Minecraft** | Another process held memory-write or thread-creation access to Minecraft. |

## Alts

| Detection | Explanation |
| --- | --- |
| **MINECRAFT** | A Minecraft account discovered from launcher account files (`launcher_accounts.json`, Modrinth, Prism, MultiMC, Lunar, Feather, Badlion, LabyMod, Essential, IAS) or verified client startup logs. |
| **DISCORD** | A Discord account discovered from live Discord desktop clients (`sentry/scope_v3.json`) and Chromium/Gecko browser `Local Storage` (`user_id_cache` and strict `MultiAccountStore` `_state.users` parsing). |
| **Possible Old IGN** | A Minecraft name observed in verified client startup logs without a local UUID mapping. |
| **Minecraft Accounts ([count])** | Counts Minecraft account entries listed in the report. |
| **Discord Accounts ([count])** | Counts Discord account entries listed in the report. |
| **1 ACCOUNT** | The report lists one account entry. |
| **[Count] ACCOUNTS** | The report shows how many account entries were listed. |

## Report flags

| Flag | Explanation |
| --- | --- |
| **BAN DEFINITIVE** | Mythosaur confirmed prohibited functionality or verified runtime cheat/injection evidence in the current Minecraft instance. |
| **BAN** | A category flagged an item as ban-level evidence. Check whether the finding establishes what the server rule prohibits. |
| **STRONGLY SUSPICIOUS** | The findings warrant prompt manual review. Corroborate before banning. |
| **SUSPICIOUS** | The report identifies a concern that requires context and corroboration. |
| **INVESTIGATE** | Review the item and any related evidence. The flag alone is insufficient for a ban. |
| **INFORMATIONAL** | The entry provides context for other findings. |
| **INFO** | A short label for an informational entry. |
| **CLEAN** | No detections were found in that category. |
| **NO EVIDENCE IDENTIFIED** | Completed checks found no evidence of concern within their scope. |
| **INCONCLUSIVE** | Required results were incomplete or unavailable for that view. |
| **N/A** | A result or score is unavailable for that view. |
