---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Ygreky Embedded Security Training

## Day 1 - Why embedded security

### Security principles (the CIA triad)

#### Confidentiality

Examples:

* User data is encrypted
* Passwords are hashed and not in plain text

#### Integrity

Examples:

* Logs cannot be modified after storage
* User apps can't modify system files
* User data cannot be changed by the user

#### Availability

Examples:

* The device responds to user's commands
* The device responds rapidly enough

### Risk evaluation

As 100% security does not exist we have to choose what features/aspects to concentrate on, we must evaluate risk

* Can't prevent all attacks
  * Need to prioritize
* Bugs will happen
  * Will be exploited by attackers
* Risk-based analysis
  * List the "what can go wrong"s
  * Evaluate likelihood and potential impact
  * Create action list for critical items

How to evaluate risks

* Brainstorm with team members and/or users
* Consider
  * Attacks directly on your device
  * Attacks using your device (attack on satellite modem to shut down communication)
  * The CIA triad
  * What can the attacker gain?
  * What kind of accesses has the attacker? (e.b. network interfaces)
  * What is the critical functionality of the device?
  * Which features are difficult to test?
  * Which features are considered buggy?

```
Impact ^
       |          |
       | Unlikely,|           Evaluate, then deal with these first
       | severe   | CRITICAL   <---
       |          |
       |----------+----------
       |          |
       | Unlikely,| Likely,
       | clement  | clement
       |          |
       +------------------->
                    Likelihood
```

## Day 1 - Basic System Configuration

### Possible risks and solutions

* Risks considered:
  * A (security) bug in a unused feature
  * Access the system using a forgotten network service (badly configured)
  * Insecure default configuration of a network service (e.g. web server)
* Technical details to analyze
  * `DISTRO_FEATURES`, `IMAGE_FEATURES`, etc.
  * Included layers
  * Included reciped
* Best practices
  * Review the list of features
  * Remove what is not needed

### How to analyze features in a Yocto project

All features built in the Yocto projects are listed in [the doc](https://docs.yoctoproject.org/ref-manual/features.html#features)

#### [Machine features](https://docs.yoctoproject.org/ref-manual/features.html#machine-features)

Examples:

* bluetooth
* rtc
* serial

[Distro features](https://docs.yoctoproject.org/ref-manual/features.html#distro-features)

Some distro features are also machine features, see: [COMBINED FEATURES](https://docs.yoctoproject.org/ref-manual/variables.html#term-COMBINED_FEATURES)

Examples:

* acl
* bluetooth
* ext2

#### [Image features](https://docs.yoctoproject.org/ref-manual/features.html#image-features)

Controlled by the variables [`IMAGE_FEATURES`](https://app.gitbook.com/o/0IvWzQZO5B1SKmpbDAaT/s/qJ7ZZXiVbpEtlw3dgJZR/) and [`EXTRA_IMAGE_FEATURES`](https://docs.yoctoproject.org/ref-manual/variables.html#term-EXTRA_IMAGE_FEATURES)

Examples:

* allow-empty-password
* dbg-pkgs
* dev-pkgs
* empty-root-password

### Assignments

#### System options - practice 1

To check for features:

```
bitbake-getvar IMAGE_FEATURES
bitbake-getvar MACHINE_FEATURES
bitbake-getvar DISTRO_FEATURES
```

Me most blatant to disable would be the image-feature `debug-tweaks` which itself enables `allow-empty-password`, `empty-root-password` and `post-install-logging`.

It's very handy for development/debug as it allow to ssh as root with no password. This is obviously not very nice from a security POV.

#### System options - practice 2

To check for features in `core-image-minimal`:

```
bitbake-getbar -r core-image-minimal IMAGE_FEATURES
bitbake-getbar -r core-image-minimal MACHINE_FEATURES
bitbake-getbar -r core-image-minimal DISTRO_FEATURES
```

To add `read-only-rootfs` we must append `read-only-rootfs` to `IMAGE_FEATURES`, add this line to `conf/local.conf` (this is the easiest quick and dirty way)

```
EXTRA_IMAGE_FEATURES:append = " read-only-rootfs"
```

Then re-build

```
bitbake core-image-minimal
```

Test

```
# echo fdsaf > fdsaf
-sh: can't create fdsaf: Read-only file system
```

## Day 1 - Creating a distro

### Why?

* Only layers/recipes you need
  * Need to add them explicitly
  * Less "added by default" definitions from poky, sometimes hard to understand why they are there
  * Less unmaintained, unused, old packages
* Better control
  * Less software means less bugs
  * Check each new feature/recipe added
* Smaller footprint
* Not hard to do
  * Most tutorials start with poly...
  * but you can create a distro in less than an hour

### Distro best practices

* Maximum reuse
  * Update elements from other layers
* Add good quality dependencies
  * Well supported layers with active maintainers
* Modifications via bbappends
  * Use `bbappend`s instead of copying recipes
  * Easier to maintain
* Use `yocto-check-layer`
  * The script for **Yocto Compatible**
  * Checks for multiple best practices

### Create a simple distro

See [https://github.com/andrea-peter/mysecuredistro/commits/main/](https://github.com/andrea-peter/mysecuredistro/commits/main/) for the steps

#### Create layer

```
bitbake-layers create-layer ../../meta-mysecuredistro
```

#### Set distro

In the build directory, in the file `conf/local.conf`

```
DISTRO = "mysecuredistro"
```

#### Set distro config

In the file `meta-mysecuredistro/conf/distro/mysecuredistro.conf` (\<same-name-as-distro>.conf)

```
# Configuration of "mysecuredistro"
DISTRO_NAME = "My Secure Distro (based on OpenEmbedded)"
DISTRO_VERSION = "1.0.0"
DISTRO_FEATURES:remove =  "alsa bluetooth nfs 3g nfc x11"
DISTRO_EXTRA_RDEPENDS = ""
DISTRO_EXTRA_RRECOMMENDS = ""
TCLIBC = "glibc"

PACKAGE_CLASSES += "package_ipk"
INHERIT += "${PACKAGE_CLASSES} devshell sstate license remove-libtool create-spdx"
```

#### Remove debug-tweaks

In the file `<build-dir>/conf/local.conf` add

```
IMAGE_FEATURES:remove "debug-tweaks"
```

#### Add meta-security layer

All the dependencies or [meta-security](https://app.gitbook.com/o/0IvWzQZO5B1SKmpbDAaT/s/qJ7ZZXiVbpEtlw3dgJZR/) are included in the Open Embedded layer

```
cd ~/example-distro/
git clone -b kirkstone git://git.yoctoproject.org/meta-security
cd ~/openembedded-core
source oe-init-build-env
bitbake-layers add-layer ../../meta-oe/meta-oe
bitbake-layers add-layer ../../meta-oe/meta-python/
bitbake-layers add-layer ../../meta-oe/meta-perl/
bitbake-layers add-layer ../../meta-oe/meta-networking/
bitbake-layers add-layer ../../meta-security/
bitbake-layers add-layer ../../meta-security/meta-security-compliance
```

Modify the `meta-security` layer to have version `3.1.4` of `lynis`:

Rename `lynis`  recipe to `lynis_3.1.4.bb` and change `SRC_URI[scha256sum]` to `c4dbcddd429624d5b2319cd3b19728e18a7885b70b8eb0a9fdd3ca5f0ae28eb6`&#x20;

#### Add security in config

In `meta-mysecuredistro/conf/layer.conf` add `meta-security` layer as dependency:

```
LAYERDEPENDS_meta-mysecuredistro = "core security"
```

Add distro-feature "security", in  `meta-mysecuredistro/conf/distro/layer.conf` add:

```
DISTRO_FEATURES += "security"
```

#### Add security distro feature

In the distro config file `config/distro/mysecuredistro.conf` add `security` in `DISTRO_FEATURES`

#### Add security in config

In `meta-mysecuredistro/conf/layer.conf` add `meta-security` layer as dependency:

```
LAYERDEPENDS_meta-mysecuredistro = "core security"
```

Add distro-feature "security", in  `meta-mysecuredistro/conf/distro/layer.conf` add:

```
DISTRO_FEATURES += "security"
```

#### Add lynis

Add this to the `bbappend` file:

```
IMAGE_INSTALL:append = " lynis"
```

#### Set password to root user

In the `bbappend` file add:\
(password is `root`, generated with `openssl passwd root` ), `$` must be escaped

```
inherit extrausers


# Add user nonroot that belongs to sudo group
EXTRA_USERS_PARAMS = "\
    useradd -p '\$1\$uEYrbNqS\$wGKPDV1/.qDu0u/HLaZBu.' root; \
    "
```



#### Add user

In the `bbappend` file add the following line under `EXTRA_USER_PARAMS`:\
(password is `andrea` , generated with `openssl passwd andrea`)

```
useradd -p '\$1\$8RrQrwNz\$fT/kRwJjft.zwesyEZhK51' andrea; \
```

#### Configure sudo

Add `-G sudo` in the creation of the user `andrea` created above under `EXTRA_USER_PARAMS`

To add the `sudo` package, in the `bbappend` file add:

```
IMAGE_INSTALL:append = " sudo"
```

Uncomment `sudoers`, in the `bbapend` file add the following:

<pre><code># Add sudo access to users in the sudo group
<strong>update_sudoers(){
</strong>    # Uncomment the line adding the sudo group to sudoers
    sed -i 's/^#\s*\(%sudo\s*ALL=(ALL:ALL)\s*ALL\)/\1/'  ${IMAGE_ROOTFS}/etc/sudoers
}

ROOTFS_POSTPROCESS_COMMAND += "update_sudoers; "
</code></pre>

#### Disable root login

Change the line that sets the `root` password to

```
usermod -L -e 1 root; \
```

## CVE

* Biggest database of vulnerabilities
* Started in 1999
* About 250-300 new CVEs every day
* CVE list on github at [https://github.com/CVEProject/cvelistV5](https://github.com/CVEProject/cvelistV5) in JSON format
* `base_score` from  0 to 10, just an indication (depends on use case)
* [NVD](https://nvd.nist.gov/) created because until 2024 CVEs lacked some machine readable metadata

### Finance problems

* NVD had financial problems in 2023 and stopped to add entries for a couple of months: HOLE
* CVE had financial problems in 2024 and stopped for a while: HOLE

### EUVD

Because of the above problems, the EU created its own database at: [https://euvd.enisa.europa.eu/](https://euvd.enisa.europa.eu/)

* In beta right now
* Does not create entries, pulls from other sources

### Report security issues

* For source projects, check SECURITY.md
* Don't create a github issue
* CRA: If you use open source, you are obliged to signal security issues upstream

## CVE-check

Built-in check in Yocto project to scan recipes, add this to your `local.conf`

Check out this script to get lines of CVEs out of reports: [https://gitlab.com/ygreky/public/yocto-vex-check/-/blob/main/script/cve-report.py?ref\_type=heads](https://gitlab.com/ygreky/public/yocto-vex-check/-/blob/main/script/cve-report.py?ref_type=heads)

```
INHERIT += "cve-check"
CVE_DB_UPDATE_INTERVAL = -1
```

cve-check will run before building and will issue warnings if it detects software with known CVEs from [NVD](https://nvd.nist.gov/).

Reports are created at the end:

* .cve: Results for the compiled image
* Summaries: All vulnerabilities (including SDK)

The file `example_distro/openembedded-core/meta/conf/distro/include/cve-extra-exclusions.inc` contains handmade assessments, it can be included in the `local.conf` with:

```
include conf/distro/include/cve-extra-exclusions.inc
```

#### Assignment 2

Add `seccomp` to distro-features, then run

```
bitbake world --runall do_cve_check
```

## Risk analysis

* CRA does not specify how the risk analysis must be done, only that it must be done
* Risk evaluation is quite subjective to the company/use case

### Risk management stages

* Identify risks (assets, threats and vulnerabilities)
* Assess risk (calculate risk: likelihood and impact)
* Handle risks (implement mitigations and controls, re-calculate risk after their implementation)
* Monitor risks (check effectiveness and review analysis)

## Upgrade from kirkstone to scarthgap

TODO update

* git fetch and checkout kirkstone on layers (meta-my..., meta-security)
* re-copy `openembedded-core` and `meta-oe` from the `scarthgap` folder in the store (maybe git fetch and checkout would have worked here too)
* Set `DL_DIR` and `SSTATE_DIR` to the `scarthgap` folder in store (don't copy old local conf)
* Change vaule of "LAYERSERIES\_COMPAT\_meta-mysecuredistro" to "scarthgap" in layer.conf
* Re-add layers (since build dir does not exist anymore)

## CVE fixes in Yocto

When a CVE is issued, we would like to patch the recipes in a way that `cve-check` will acknowledge

### I have an unpatched CVE...

* From cve-check
* From monitoring of the new CVE stream
* As a part of a coordinated disclosure
* I implemented the fix upstream :sunglasses:

### A few check before you start

* Is there someone else working on it?
  * Ask! Check the mailing list archive
  * Check out this: [https://wiki.yoctoproject.org/wiki/Synchronization\_CVEs](https://wiki.yoctoproject.org/wiki/Synchronization_CVEs)
* Is the backported patch to the version in YP available?
  * Upstream first
  * Can check big distros like Debian
  * Remember: YP starts applying from master (if versions match)
* Which YP versions are affected?

-> Look for files named `CVE-...`

See:

* &#x20;[https://wiki.yoctoproject.org/wiki/Synchronization\_CVEs](https://wiki.yoctoproject.org/wiki/Synchronization_CVEs)
* [https://www.youtube.com/watch?v=CRDxJwsO4b4\&list=PLD4M5FoHz-Tw5-pazgQbITW\_HmuJhyrI-\&t=640s](https://www.youtube.com/watch?v=CRDxJwsO4b4\&list=PLD4M5FoHz-Tw5-pazgQbITW_HmuJhyrI-\&t=640s)

## Vulnerability reporting

* Risk considered:
  * A researcher sells a vulnerability to malicious actors
  * A researcher releases the vulnerability information to the public while there is no fix
  * An attacker uses an unfixed vulnerability in a package you include
* Technical details to analyze
  * Reports to your product (incoming), usually company-specific code
  * Reports to your upstream (outgoing), if you discover a possible security bug
* Best practices
  * Create a security policy at your company (and train on it)
  * Know how to report a security vulnerability to a supplier or an upstream project

#### Your company's best practices

* Have a security contact on the website
* If open source: add `SECURITY.md`
* Set-up security policy

#### Security policy basics

* How do you receive reports?
  * Dedicated mailing list
  * Dedicated (confidential) bug tracker
  * ONLY the security teams has initially access to them
* Who is the security team?
  * Representatives from all teams you need to get an update deployed: usually development, release, quality plus a dedicated communication contact
  * Simple exercise: Imagine an emergency release scenario
* Possible need to communicate with other companies/projects
  * If the issue is in a dependency
  * If there is a similar issue in similar project (e.g. protocol weakness)
* Your market might have special requirements
* There might be timing requirements
  * Example: Disclosure in 90 days

See: [https://docs.yoctoproject.org/dev-manual/security-subjects.html](https://docs.yoctoproject.org/dev-manual/security-subjects.html)

## SBOM

Software bill of material

* Package information
  * Exact download location
  * Licenses
  * (Possible) exact source files used
  * (Possible) build environment config
  * (Possible) build commands
* Dependency list
  * Dependency diagram

### Generate SBOM

* Risk considered:
  * An attacker exploits a dependency with a security vulnerability
  * An attacked replaces a dependency with a malicious one
* Technical details to analyze
  * Download locations, licenses, patches applied
* Best practices
  * Generate SBOMs
  * **Automate** analysis of what the product contains

### SBOM standards

SPDX and CycloneDX contain the same info

* SPDX
  * Designed for licensing and legal
  * SPX2.2 is an ISO standard
  * Recently released 3.0 add modularity and security options
  * A Linux Foundation project
  * Generated by the Yocto project by default
* Cyclone DX
  * Hosted by OWASP
  * Created for security-related use-cases
* Other - vendor specific

### Current state (2025)

* Generation tools for most build systems
  * Majority generate JSON
* Compatibility is a WIP
  * No 1:1 conversion SPDX <-> CycloneDX
  * Various incompatibilities between tools

### Yocto and SBOM

* Scarthgap and Kirkstone
  * SPDX 2.2
  * Out-of-tree CycloneDX patches
* Current "master"
  * SPDX 3.0
  * SPDX 2.2 (optional)

See: [https://www.youtube.com/watch?v=faDBoZOGuVE](https://www.youtube.com/watch?v=faDBoZOGuVE)





