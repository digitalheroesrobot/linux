# Linux Commands for Web & Android Developers
## University Computer Science Course
### Specialized Developer CLI — No RPM/Package-Management Commands

> **Scope**
>
> This course is intentionally different from the general Ubuntu/Linux command course and the RPM/DNF course.
>
> It focuses on commands and workflows that are particularly useful for:
>
> - Web developers
> - Backend developers
> - Frontend developers
> - DevOps-oriented developers
> - Android developers
> - Mobile application developers
> - API developers
> - Full-stack developers
>
> **Important:** Package-management commands such as `rpm`, `dnf`, and the package-management material from the RPM course are intentionally excluded.

---

# Table of Contents

1. [Developer Linux Mindset](#1-developer-linux-mindset)
2. [Command Discovery](#2-command-discovery)
3. [Environment Inspection](#3-environment-inspection)
4. [Text and JSON Processing](#4-text-and-json-processing)
5. [curl for Web Developers](#5-curl-for-web-developers)
6. [wget for Web Developers](#6-wget-for-web-developers)
7. [HTTP Debugging](#7-http-debugging)
8. [DNS Debugging](#8-dns-debugging)
9. [TCP and Port Debugging](#9-tcp-and-port-debugging)
10. [Web Server Testing](#10-web-server-testing)
11. [TLS/HTTPS Debugging](#11-tlshttps-debugging)
12. [API Development Workflows](#12-api-development-workflows)
13. [jq for JSON](#13-jq-for-json)
14. [Git for Developers](#14-git-for-developers)
15. [SSH Developer Workflows](#15-ssh-developer-workflows)
16. [Archive and Build Artifacts](#16-archive-and-build-artifacts)
17. [Node.js Development](#17-nodejs-development)
18. [npm](#18-npm)
19. [npx](#19-npx)
20. [Alternative JavaScript Package Managers](#20-alternative-javascript-package-managers)
21. [Frontend Development](#21-frontend-development)
22. [Environment Variables](#22-environment-variables)
23. [Process Environment Debugging](#23-process-environment-debugging)
24. [Android Development Overview](#24-android-development-overview)
25. [ADB Fundamentals](#25-adb-fundamentals)
26. [ADB Device Inspection](#26-adb-device-inspection)
27. [ADB Application Management](#27-adb-application-management)
28. [ADB Files and Data](#28-adb-files-and-data)
29. [ADB Logcat](#29-adb-logcat)
30. [ADB Shell](#30-adb-shell)
31. [Android Debugging with Activity Manager](#31-android-debugging-with-activity-manager)
32. [Android Package Manager Through ADB](#32-android-package-manager-through-adb)
33. [Android Device Properties](#33-android-device-properties)
34. [Android Performance Inspection](#34-android-performance-inspection)
35. [Fastboot](#35-fastboot)
36. [Android SDK Command-Line Tools](#36-android-sdk-command-line-tools)
37. [sdkmanager](#37-sdkmanager)
38. [avdmanager](#38-avdmanager)
39. [emulator](#39-emulator)
40. [Gradle Wrapper](#40-gradle-wrapper)
41. [Android Build Commands](#41-android-build-commands)
42. [APK Inspection](#42-apk-inspection)
43. [APK Signing Tools](#43-apk-signing-tools)
44. [Android App Bundles](#44-android-app-bundles)
45. [Android Debugging Workflow](#45-android-debugging-workflow)
46. [Web + Android Integration](#46-web--android-integration)
47. [Developer Automation](#47-developer-automation)
48. [Useful Developer Pipelines](#48-useful-developer-pipelines)
49. [University Laboratory Exercises](#49-university-laboratory-exercises)
50. [12-Week Course Plan](#50-12-week-course-plan)
51. [Developer Cheat Sheet](#51-developer-cheat-sheet)

---

# 1. Developer Linux Mindset

A web or Android developer uses Linux differently from a normal desktop user.

The command line becomes a development interface:

```text
Editor
   │
   ▼
Terminal
   │
   ├── source control
   ├── HTTP/API testing
   ├── build systems
   ├── device debugging
   ├── logs
   ├── emulators
   └── automation
```

A developer should become comfortable with:

```text
stdin
stdout
stderr
pipes
exit codes
environment variables
processes
network sockets
logs
build artifacts
device interfaces
```

---

# 2. Command Discovery

## Find a command

```bash
command -v node
```

Another useful form:

```bash
type node
```

Inspect all matching locations:

```bash
type -a node
```

---

## Discover command documentation

```bash
help cd
```

For external programs:

```bash
info coreutils
```

Search the shell's command history:

```bash
history | grep curl
```

---

# 3. Environment Inspection

Show environment variables:

```bash
printenv
```

Show one:

```bash
printenv HOME
```

Check whether a variable exists:

```bash
printenv ANDROID_HOME
```

Display the shell's current environment:

```bash
env
```

Set a variable temporarily:

```bash
export API_URL=https://api.example.com
```

Test:

```bash
printf '%s\n' "$API_URL"
```

---

# 4. Text and JSON Processing

Web development generates enormous amounts of text.

Typical data:

```text
HTTP responses
JSON
logs
configuration
compiler output
test output
CI output
```

Useful specialized tools:

```text
jq
sed
awk
cut
tr
sort
uniq
xargs
```

These are covered here from a developer perspective rather than as general Linux commands.

---

# 5. curl for Web Developers

`curl` is one of the most important Linux commands for web developers.

Basic request:

```bash
curl https://example.com
```

Save response:

```bash
curl -o response.html https://example.com
```

Show headers:

```bash
curl -i https://example.com
```

Headers only:

```bash
curl -I https://example.com
```

Follow redirects:

```bash
curl -L https://example.com
```

Verbose HTTP/TLS diagnostics:

```bash
curl -v https://example.com
```

Quiet mode:

```bash
curl -s https://example.com
```

---

# 6. wget for Web Developers

Download:

```bash
wget https://example.com/file.zip
```

Specify output:

```bash
wget -O output.zip https://example.com/file.zip
```

Continue an interrupted download:

```bash
wget -c https://example.com/file.zip
```

Useful for:

```text
large files
CI downloads
test data
SDK archives
static resources
```

---

# 7. HTTP Debugging

## GET

```bash
curl https://api.example.com/users
```

---

## POST JSON

```bash
curl \
  -X POST \
  -H 'Content-Type: application/json' \
  -d '{"name":"Alice"}' \
  https://api.example.com/users
```

---

## PUT

```bash
curl \
  -X PUT \
  -H 'Content-Type: application/json' \
  -d '{"name":"Bob"}' \
  https://api.example.com/users/10
```

---

## DELETE

```bash
curl \
  -X DELETE \
  https://api.example.com/users/10
```

---

## Authentication header

```bash
curl \
  -H "Authorization: Bearer $TOKEN" \
  https://api.example.com/profile
```

---

# 8. DNS Debugging

## dig

Query DNS:

```bash
dig example.com
```

IPv4:

```bash
dig A example.com
```

IPv6:

```bash
dig AAAA example.com
```

Mail:

```bash
dig MX example.com
```

Nameservers:

```bash
dig NS example.com
```

Short answer:

```bash
dig +short example.com
```

Trace DNS:

```bash
dig +trace example.com
```

---

## nslookup

```bash
nslookup example.com
```

Useful for quick DNS investigation.

---

# 9. TCP and Port Debugging

## ss

Show listening sockets:

```bash
ss -lnt
```

Show listening TCP ports with processes:

```bash
ss -lntp
```

Show UDP:

```bash
ss -lnup
```

Check a specific port:

```bash
ss -lntp | grep ':8080'
```

This is extremely useful when:

```text
Spring Boot won't start
Node server is unreachable
Android emulator cannot connect
Docker service appears unavailable
```

---

# 10. Web Server Testing

Start a quick Python development server:

```bash
python3 -m http.server 8080
```

Then test:

```bash
curl http://localhost:8080
```

This is useful for testing:

```text
HTML
JavaScript
static assets
browser connectivity
local API clients
```

---

# 11. TLS/HTTPS Debugging

Inspect TLS negotiation:

```bash
openssl s_client -connect example.com:443
```

Show certificate information:

```bash
openssl s_client -connect example.com:443 </dev/null 2>/dev/null |
openssl x509 -noout -subject -issuer -dates
```

Check certificate dates:

```bash
openssl s_client -connect example.com:443 </dev/null 2>/dev/null |
openssl x509 -noout -dates
```

Developers can use this to investigate:

```text
expired certificates
wrong hostname
certificate chains
TLS negotiation
HTTPS connection problems
```

---

# 12. API Development Workflows

A useful API debugging sequence is:

```text
1. DNS
2. TCP connection
3. TLS
4. HTTP
5. authentication
6. JSON
7. application logic
```

Example:

```bash
dig +short api.example.com
```

Then:

```bash
curl -v https://api.example.com/health
```

Then:

```bash
curl -s https://api.example.com/health | jq
```

This gives a clean diagnostic chain.

---

# 13. jq for JSON

`jq` is one of the most useful developer CLI tools.

Pretty-print:

```bash
curl -s https://api.example.com/users | jq
```

Select a field:

```bash
jq '.name'
```

Select nested data:

```bash
jq '.user.profile.name'
```

Array:

```bash
jq '.[0]'
```

Map:

```bash
jq '.[].name'
```

Filter:

```bash
jq '.[] | select(.active == true)'
```

Count:

```bash
jq 'length'
```

---

# 14. Git for Developers

Git is fundamental to modern software development.

Check repository state:

```bash
git status
```

Show branches:

```bash
git branch
```

Create branch:

```bash
git switch -c feature/login
```

Switch:

```bash
git switch main
```

Inspect commits:

```bash
git log --oneline
```

Show recent commits:

```bash
git log --oneline -10
```

Compare:

```bash
git diff
```

Show staged changes:

```bash
git diff --cached
```

---

# 15. SSH Developer Workflows

Generate a key:

```bash
ssh-keygen -t ed25519
```

Test remote access:

```bash
ssh user@server
```

Specify key:

```bash
ssh -i ~/.ssh/dev_key user@server
```

Use a custom port:

```bash
ssh -p 2222 user@server
```

SSH configuration:

```text
~/.ssh/config
```

Example:

```text
Host dev-server
    HostName 192.168.1.50
    User developer
    IdentityFile ~/.ssh/dev_key
```

Then:

```bash
ssh dev-server
```

---

# 16. Archive and Build Artifacts

Create tar archive:

```bash
tar -czf build.tar.gz dist/
```

Extract:

```bash
tar -xzf build.tar.gz
```

List:

```bash
tar -tzf build.tar.gz
```

Create ZIP:

```bash
zip -r source.zip src/
```

Inspect:

```bash
unzip -l source.zip
```

Extract:

```bash
unzip source.zip
```

Useful for:

```text
release artifacts
CI/CD
SDK distribution
backup of build output
```

---

# 17. Node.js Development

Check Node:

```bash
node --version
```

Run JavaScript:

```bash
node app.js
```

Execute inline:

```bash
node -e 'console.log(2 + 2)'
```

Inspect runtime:

```bash
node -p 'process.version'
```

Inspect platform:

```bash
node -p 'process.platform'
```

Inspect architecture:

```bash
node -p 'process.arch'
```

---

# 18. npm

Check:

```bash
npm --version
```

Initialize project:

```bash
npm init
```

Install project dependencies:

```bash
npm install
```

Install a development dependency:

```bash
npm install --save-dev eslint
```

List dependencies:

```bash
npm ls
```

Run a package script:

```bash
npm run build
```

Run tests:

```bash
npm test
```

Audit:

```bash
npm audit
```

---

# 19. npx

`npx` runs Node command-line packages.

Example:

```bash
npx eslint .
```

Run a tool without permanently installing it globally:

```bash
npx prettier .
```

Inspect:

```bash
npx --yes cowsay "Linux developer"
```

In production projects, prefer explicit project dependencies and lockfiles rather than relying on arbitrary remote packages.

---

# 20. Alternative JavaScript Package Managers

## pnpm

```bash
pnpm --version
```

Install:

```bash
pnpm install
```

Run:

```bash
pnpm dev
```

Build:

```bash
pnpm build
```

---

## Yarn

```bash
yarn --version
```

Install:

```bash
yarn install
```

Run:

```bash
yarn dev
```

The exact package-manager choice should follow the project's existing configuration.

---

# 21. Frontend Development

Typical development flow:

```bash
npm install
npm run dev
```

Production build:

```bash
npm run build
```

Preview:

```bash
npm run preview
```

Inspect generated files:

```bash
find dist -type f
```

Test an HTTP build:

```bash
python3 -m http.server 8080 --directory dist
```

Then:

```bash
curl -I http://localhost:8080
```

---

# 22. Environment Variables

Development configuration often uses:

```text
API_URL
DATABASE_URL
NODE_ENV
ANDROID_HOME
JAVA_HOME
```

Set:

```bash
export NODE_ENV=development
```

Read:

```bash
printf '%s\n' "$NODE_ENV"
```

Temporary command-specific variable:

```bash
NODE_ENV=production npm run build
```

This is especially useful in CI pipelines.

---

# 23. Process Environment Debugging

Find process IDs:

```bash
pgrep node
```

Find a particular process:

```bash
pgrep -af node
```

Inspect process information:

```bash
ps -p PID -o pid,ppid,etime,%cpu,%mem,cmd
```

Follow a process:

```bash
top -p PID
```

Send a graceful termination signal:

```bash
kill PID
```

Force termination only when necessary:

```bash
kill -9 PID
```

---

# 24. Android Development Overview

Android development from Linux commonly uses:

```text
Android SDK
Android SDK Platform Tools
ADB
Fastboot
Gradle
Android Gradle Plugin
Android Emulator
SDK Manager
AVD Manager
APK tools
```

Architecture:

```text
Linux
 │
 ├── Android SDK
 │
 ├── Gradle
 │
 ├── ADB
 │      │
 │      └── physical Android device
 │
 └── Emulator
        │
        └── Android Virtual Device
```

---

# 25. ADB Fundamentals

ADB means:

```text
Android Debug Bridge
```

Check:

```bash
adb version
```

Start ADB server:

```bash
adb start-server
```

Stop:

```bash
adb kill-server
```

List devices:

```bash
adb devices
```

Verbose device listing:

```bash
adb devices -l
```

---

# 26. ADB Device Inspection

Device serial:

```bash
adb get-serialno
```

Android version:

```bash
adb shell getprop ro.build.version.release
```

SDK level:

```bash
adb shell getprop ro.build.version.sdk
```

Manufacturer:

```bash
adb shell getprop ro.product.manufacturer
```

Model:

```bash
adb shell getprop ro.product.model
```

Architecture:

```bash
adb shell getprop ro.product.cpu.abi
```

---

# 27. ADB Application Management

List packages:

```bash
adb shell pm list packages
```

Search package names:

```bash
adb shell pm list packages | grep example
```

Show APK path:

```bash
adb shell pm path com.example.app
```

Install APK:

```bash
adb install app-debug.apk
```

Replace existing application:

```bash
adb install -r app-debug.apk
```

Uninstall:

```bash
adb uninstall com.example.app
```

---

# 28. ADB Files and Data

Push a file:

```bash
adb push config.json /sdcard/config.json
```

Pull:

```bash
adb pull /sdcard/config.json .
```

List Android-side storage:

```bash
adb shell ls -la /sdcard/
```

Create directory:

```bash
adb shell mkdir -p /sdcard/test-data
```

Remove:

```bash
adb shell rm /sdcard/test-data/file.txt
```

---

# 29. ADB Logcat

Android logs are central to application debugging.

Show logs:

```bash
adb logcat
```

Clear:

```bash
adb logcat -c
```

Dump and exit:

```bash
adb logcat -d
```

Filter by text:

```bash
adb logcat | grep MyActivity
```

Show errors:

```bash
adb logcat '*:E'
```

Useful developer workflow:

```bash
adb logcat -c
adb shell am force-stop com.example.app
adb shell monkey -p com.example.app 1
adb logcat -d
```

---

# 30. ADB Shell

Open Android shell:

```bash
adb shell
```

Execute one command:

```bash
adb shell getprop
```

Check current user:

```bash
adb shell id
```

Inspect processes:

```bash
adb shell ps
```

Inspect memory:

```bash
adb shell dumpsys meminfo
```

---

# 31. Android Debugging with Activity Manager

The Android Activity Manager command is:

```bash
am
```

Launch an application:

```bash
adb shell am start -n com.example.app/.MainActivity
```

Force stop:

```bash
adb shell am force-stop com.example.app
```

Send broadcast:

```bash
adb shell am broadcast -a com.example.ACTION_TEST
```

This is useful for automated testing and debugging.

---

# 32. Android Package Manager Through ADB

Android has its own package manager command:

```bash
pm
```

List packages:

```bash
adb shell pm list packages
```

Show package information:

```bash
adb shell dumpsys package com.example.app
```

Clear application data:

```bash
adb shell pm clear com.example.app
```

Enable:

```bash
adb shell pm enable com.example.app
```

Disable:

```bash
adb shell pm disable-user --user 0 com.example.app
```

Be careful with package-management operations on system applications.

---

# 33. Android Device Properties

Get all properties:

```bash
adb shell getprop
```

Specific:

```bash
adb shell getprop ro.build.version.sdk
```

Network-related:

```bash
adb shell getprop | grep -i network
```

Boot information:

```bash
adb shell getprop | grep -i boot
```

These properties are useful for device-specific debugging.

---

# 34. Android Performance Inspection

CPU/memory:

```bash
adb shell top
```

Memory:

```bash
adb shell dumpsys meminfo com.example.app
```

CPU information:

```bash
adb shell cat /proc/cpuinfo
```

Memory information:

```bash
adb shell cat /proc/meminfo
```

Battery:

```bash
adb shell dumpsys battery
```

Graphics/display:

```bash
adb shell dumpsys SurfaceFlinger
```

---

# 35. Fastboot

Fastboot operates at a lower level than ADB.

Check:

```bash
fastboot --version
```

List devices:

```bash
fastboot devices
```

Reboot:

```bash
fastboot reboot
```

Get variables:

```bash
fastboot getvar all
```

> **Warning:** Fastboot can modify boot partitions and other low-level device state. Never execute flashing commands on an important device without understanding the exact target partition and recovery procedure.

---

# 36. Android SDK Command-Line Tools

The Android SDK normally contains tools such as:

```text
adb
fastboot
sdkmanager
avdmanager
emulator
```

Find Android SDK location:

```bash
printf '%s\n' "$ANDROID_HOME"
```

or:

```bash
printf '%s\n' "$ANDROID_SDK_ROOT"
```

A common SDK structure is:

```text
$ANDROID_SDK_ROOT/
├── platform-tools/
├── platforms/
├── build-tools/
├── emulator/
├── cmdline-tools/
└── system-images/
```

---

# 37. sdkmanager

List installed/available SDK packages:

```bash
sdkmanager --list
```

Install a platform:

```bash
sdkmanager "platforms;android-35"
```

Install build tools:

```bash
sdkmanager "build-tools;35.0.0"
```

Install platform tools:

```bash
sdkmanager "platform-tools"
```

Accept licenses:

```bash
yes | sdkmanager --licenses
```

Exact available versions depend on the installed SDK repository.

---

# 38. avdmanager

List virtual devices:

```bash
avdmanager list avd
```

List system images:

```bash
avdmanager list target
```

Create an AVD:

```bash
avdmanager create avd \
  -n Pixel_Test \
  -k "system-images;android-35;google_apis;x86_64"
```

Delete:

```bash
avdmanager delete avd -n Pixel_Test
```

---

# 39. emulator

List AVDs:

```bash
emulator -list-avds
```

Start:

```bash
emulator -avd Pixel_Test
```

Start without boot animation:

```bash
emulator -avd Pixel_Test -no-boot-anim
```

Cold boot:

```bash
emulator -avd Pixel_Test -no-snapshot
```

Useful for:

```text
automated testing
UI development
API testing
Android debugging
CI environments
```

---

# 40. Gradle Wrapper

Android projects normally include:

```text
gradlew
gradlew.bat
```

Linux:

```bash
./gradlew tasks
```

Clean:

```bash
./gradlew clean
```

Build debug APK:

```bash
./gradlew assembleDebug
```

Build release:

```bash
./gradlew assembleRelease
```

Run tests:

```bash
./gradlew test
```

Android instrumentation tests:

```bash
./gradlew connectedAndroidTest
```

---

# 41. Android Build Commands

List tasks:

```bash
./gradlew tasks
```

Build debug:

```bash
./gradlew assembleDebug
```

Build a specific module:

```bash
./gradlew :app:assembleDebug
```

Build release:

```bash
./gradlew :app:assembleRelease
```

Run lint:

```bash
./gradlew lint
```

Run unit tests:

```bash
./gradlew testDebugUnitTest
```

Run connected tests:

```bash
./gradlew connectedDebugAndroidTest
```

---

# 42. APK Inspection

Android SDK build tools provide:

```text
aapt
aapt2
apkanalyzer
```

Inspect APK:

```bash
apkanalyzer apk summary app-debug.apk
```

List files:

```bash
apkanalyzer files list app-debug.apk
```

Inspect manifest:

```bash
apkanalyzer manifest print app-debug.apk
```

Inspect APK size:

```bash
apkanalyzer apk file-size app-debug.apk
```

These tools are useful for understanding:

```text
APK structure
manifest
resources
DEX files
application size
```

---

# 43. APK Signing Tools

Android applications need appropriate signing for installation/distribution.

Check signature:

```bash
apksigner verify app-release.apk
```

Verbose:

```bash
apksigner verify --verbose app-release.apk
```

Sign:

```bash
apksigner sign --ks release.jks app-release-unsigned.apk
```

Verify again:

```bash
apksigner verify --verbose app-release-unsigned.apk
```

Never commit production keystores or passwords into source control.

---

# 44. Android App Bundles

Android projects can produce:

```text
APK
AAB
```

Build bundle:

```bash
./gradlew bundleRelease
```

Typical result:

```text
app/build/outputs/bundle/release/
```

AAB is commonly used for Google Play distribution.

---

# 45. Android Debugging Workflow

A practical workflow:

```text
1. Connect device
2. Verify ADB
3. Install application
4. Clear old logs
5. Launch application
6. Capture logcat
7. Inspect process
8. Inspect memory
9. Reproduce bug
10. Collect evidence
```

Example:

```bash
adb devices
adb install -r app-debug.apk
adb logcat -c
adb shell am force-stop com.example.app
adb shell am start -n com.example.app/.MainActivity
adb logcat -d > crash.log
```

Then search:

```bash
grep -i exception crash.log
```

---

# 46. Web + Android Integration

Many modern applications combine:

```text
Android app
    │
    ▼
HTTPS API
    │
    ▼
Web backend
    │
    ▼
Database
```

A developer can test the backend independently:

```bash
curl -v https://api.example.com/health
```

Inspect JSON:

```bash
curl -s https://api.example.com/health | jq
```

Test DNS:

```bash
dig +short api.example.com
```

Then test the Android application:

```bash
adb logcat
```

This separates:

```text
Android problem
from
network problem
from
backend problem
```

---

# 47. Developer Automation

A simple shell loop:

```bash
for f in *.json; do
    printf '%s\n' "$f"
done
```

Run a command over files:

```bash
for f in *.json; do
    jq '.' "$f" > "$f.pretty"
done
```

Conditional command:

```bash
if curl -fsS https://example.com/health >/dev/null; then
    printf '%s\n' "API is healthy"
else
    printf '%s\n' "API is unavailable"
fi
```

Exit status:

```bash
curl -fsS https://example.com/health
printf 'exit=%s\n' "$?"
```

These patterns become the foundation for:

```text
build scripts
CI pipelines
test automation
deployment scripts
Android test harnesses
```

---

# 48. Useful Developer Pipelines

## API → JSON → field

```bash
curl -s https://api.example.com/users |
jq '.[].name'
```

---

## API → save response → inspect

```bash
curl -s https://api.example.com/users > users.json
jq '.' users.json
```

---

## Android logs → filter

```bash
adb logcat -d |
grep -i 'exception'
```

---

## Build → locate APK

```bash
./gradlew assembleDebug
find app/build/outputs -name '*.apk'
```

---

## APK → inspect

```bash
apkanalyzer apk summary app-debug.apk
apkanalyzer manifest print app-debug.apk
```

---

# 49. University Laboratory Exercises

## Lab 1 — HTTP Investigation

Choose a public HTTPS endpoint.

Run:

```bash
curl -I https://example.com
curl -v https://example.com
```

Explain:

```text
HTTP status
response headers
TLS negotiation
redirect behavior
```

---

## Lab 2 — REST API

Use a test API.

Perform:

```text
GET
POST
PUT
DELETE
```

Use `curl`.

Record:

```text
HTTP method
URL
request headers
request body
status code
response body
```

---

## Lab 3 — JSON Processing

Save an API response:

```bash
curl -s API_URL > response.json
```

Use:

```bash
jq
```

to answer:

```text
How many objects?
Which fields exist?
Which objects satisfy a condition?
What are the IDs?
```

---

## Lab 4 — DNS

Investigate:

```bash
dig example.com
dig A example.com
dig AAAA example.com
dig NS example.com
```

Explain the difference between:

```text
A
AAAA
NS
MX
```

---

## Lab 5 — Node Web Server

Create a small Node.js server.

Run:

```bash
node server.js
```

Test:

```bash
curl -v http://localhost:3000
```

Inspect the listening port:

```bash
ss -lntp | grep ':3000'
```

---

## Lab 6 — Git Investigation

Create a repository.

Students should demonstrate:

```text
branch creation
commit history
working-tree changes
diff
branch switching
```

---

## Lab 7 — Android Device Investigation

Connect an Android device.

Run:

```bash
adb devices -l
adb shell getprop ro.product.model
adb shell getprop ro.build.version.release
adb shell getprop ro.product.cpu.abi
```

Write a device report.

---

## Lab 8 — Android Application Debugging

Install a debug APK.

Run:

```bash
adb install -r app-debug.apk
adb logcat -c
adb shell am force-stop com.example.app
adb shell am start -n com.example.app/.MainActivity
adb logcat -d > app.log
```

Identify application startup messages and errors.

---

## Lab 9 — Android Performance

Run:

```bash
adb shell dumpsys meminfo com.example.app
adb shell dumpsys battery
adb shell top
```

Record:

```text
memory
CPU
battery state
process information
```

---

## Lab 10 — Android Build

Build:

```bash
./gradlew assembleDebug
```

Locate the APK:

```bash
find app/build/outputs -name '*.apk'
```

Inspect:

```bash
apkanalyzer apk summary app-debug.apk
```

---

## Lab 11 — HTTPS Certificate Investigation

Use:

```bash
openssl s_client -connect example.com:443
```

Determine:

```text
certificate subject
issuer
validity period
TLS protocol
certificate chain
```

---

## Lab 12 — Final Full-Stack Debugging Project

Students receive a deliberately broken application.

They must determine whether the problem is:

```text
DNS
TCP
TLS
HTTP
API
JSON
Android application
Android permissions
application process
memory
build
APK
```

The report must include:

```text
symptom
hypothesis
command used
evidence
root cause
solution
verification
```

---

# 50. 12-Week Course Plan

## Week 1 — Developer CLI

Topics:

```text
environment
command discovery
processes
exit codes
pipes
automation
```

---

## Week 2 — HTTP

Learn:

```text
curl
HTTP methods
headers
status codes
JSON APIs
```

---

## Week 3 — DNS and Networking

Learn:

```text
dig
nslookup
ss
ports
DNS records
TLS
```

---

## Week 4 — JSON

Learn:

```text
jq
JSON filtering
JSON transformation
API pipelines
```

---

## Week 5 — Git

Learn:

```text
branches
commits
diffs
history
remote development
```

---

## Week 6 — Node.js

Learn:

```text
node
npm
npx
environment variables
development servers
```

---

## Week 7 — Frontend

Learn:

```text
npm scripts
development server
production build
static deployment
```

---

## Week 8 — Android CLI

Learn:

```text
ADB
devices
shell
package inspection
file transfer
```

---

## Week 9 — Android Debugging

Learn:

```text
logcat
am
pm
dumpsys
getprop
```

---

## Week 10 — Android SDK

Learn:

```text
sdkmanager
avdmanager
emulator
SDK platforms
system images
```

---

## Week 11 — Android Build

Learn:

```text
Gradle
APK
AAB
apkanalyzer
apksigner
```

---

## Week 12 — Integrated Project

Students build and debug:

```text
Web API
   │
   ▼
Android client
   │
   ▼
Linux development environment
```

The final project should demonstrate:

```text
Git
HTTP
JSON
DNS
TLS
Node.js
Android
ADB
Gradle
APK analysis
automated debugging
```

---

# 51. Developer Cheat Sheet

## Web

```bash
curl URL
curl -I URL
curl -v URL
curl -L URL
curl -X POST ...
wget URL
dig +short DOMAIN
dig A DOMAIN
dig AAAA DOMAIN
ss -lntp
openssl s_client -connect HOST:443
jq '.field'
```

## Node.js

```bash
node --version
node app.js
npm --version
npm install
npm run dev
npm run build
npm test
npx TOOL
pnpm install
yarn install
```

## Git

```bash
git status
git branch
git switch -c NAME
git switch NAME
git log --oneline
git diff
git diff --cached
```

## SSH

```bash
ssh-keygen -t ed25519
ssh user@host
ssh -i KEY user@host
```

## Android

```bash
adb version
adb devices -l
adb shell
adb shell getprop
adb shell pm list packages
adb install APK
adb uninstall PACKAGE
adb push FILE DEST
adb pull SRC DEST
adb logcat
adb logcat -c
adb shell am start ...
adb shell am force-stop PACKAGE
adb shell dumpsys meminfo PACKAGE
fastboot devices
```

## Android SDK

```bash
sdkmanager --list
sdkmanager "platform-tools"
avdmanager list avd
avdmanager create avd ...
emulator -list-avds
emulator -avd NAME
```

## Android Build

```bash
./gradlew tasks
./gradlew clean
./gradlew assembleDebug
./gradlew assembleRelease
./gradlew test
./gradlew connectedAndroidTest
apkanalyzer apk summary APP.apk
apkanalyzer manifest print APP.apk
apksigner verify APP.apk
```

---

# Final Developer Mental Model

A web/Android developer should think of Linux as a programmable development environment:

```text
                 Linux Developer Environment
                           │
          ┌────────────────┼────────────────┐
          │                │                │
        Web              Git             Android
          │                │                │
      HTTP/DNS         source code         ADB
          │                │                │
       curl/jq          branches          logcat
          │                │                │
       TLS/API          CI/CD             Gradle
          │                │                │
          └────────────────┼────────────────┘
                           │
                           ▼
                     Automation
                           │
                           ▼
                    Repeatable Builds
                    and Debugging
```

The most important progression is:

```text
HTTP
  ↓
DNS
  ↓
TLS
  ↓
API
  ↓
JSON
  ↓
Git
  ↓
Node.js
  ↓
Android SDK
  ↓
ADB
  ↓
Gradle
  ↓
APK/AAB
  ↓
Automated debugging
```

The goal is not to memorize hundreds of commands.

The goal is to develop the ability to move from:

```text
"Something doesn't work."
```

to:

```text
What layer is failing?
        ↓
What evidence do I need?
        ↓
Which CLI tool can provide it?
        ↓
What does the output mean?
        ↓
What hypothesis does it support?
        ↓
Can I reproduce the result?
        ↓
Can I automate the diagnosis?
```

That diagnostic mindset is one of the most valuable Linux skills for professional web and Android developers.
