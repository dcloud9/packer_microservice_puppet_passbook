# packer\_microservice\_puppet\_passbook

... used to build role AMIs for the passbook product

## Structure

Each subdir is a role definition containing a Makefile,
and any bespoke uploads or build scripts for that role.
Building a role generates an AWS AMI.

## Usage

### 1. choose the ami you want to build.
Enter the role directory corresponding to the AMI you wish to build.

### 2. packer\_includes
Clone _packer\_includes_ at level of Makefile.

Checkout a tag if desired. You really should ...

(The x.y.z tags should represent a stable version of packer_includes).

If you do use a tag, add the line:

        export PACKER_INCLUDES_GIT_TAG=... # replace dots with the tag value.

This will invoke special validation during the build to verify the checked-out
version **and** lets future 'you' know which dependency to use to reproduce
this build.

### 3. export env vars

Export vars deliberately not defined in Makefile.

Currently these are things like the $AWS\_\* vars for access creds and other
things we don't want to publically expose.

TODO: _sidebar_ - use iam during building so we don't need to pass these creds anyway.

### 4. make sure any other dependencies exist.

Check all of the sources defined in the Makefile
including git tags etc ... exist.

Amend the Makefile as required.

### 5. Commit any changes, tag the current repo

If you have local changes, the build will fail - commit any changes first.

**Then**, locally, tag your repo with semver of form x.y.z.

Depending on the role you are building, you might apply additional tags.

e.g. for an appsvr role, we apply a tag to signify the app's version as well

e.g
    git tag -a app_version-1.0.1-$(date +'%Y%m%d%H%M%S') -m 'using app 1.0.1'

_Please note that you must make each tag unique across the whole repo - use_
_current timestamp or something to guarantee this_.

### 6. build

        make clean build

If you are playing around with the puppet stuff that appears under uploads/puppet,
on subsequent _make_ runs, omit the _clean_ target or you'll lose your local
changes,

        make build # don't trash my modifications under puppet dir

### 7. push tag on success

Push the tag only if the build succeeds.

While this will version the AMI, it does not mark the AMI as stable.

## Known Issues

* The puppet stuff depends on a bunch of 3rd party modules.
  
  These may cease to exist at a future date. 

* When building an appsvr (EUROSTAR\_SERVICE\_ROLE), you need to

  specify an APP\_VERSION that actually exists in AWS dev s3 under:

  /enovation/$EUROSTAR\_SERVICE\_NAME/artefacts/**integration**/$APP\_VERSION/

**TODO: stop using env specific folders for versioned artefacts!**

**TODO: additionally, use the pom's app version - put it in the filename!**

* _Make error: \*\*\* You must pass env var AMI_PREVIOUS\_SOURCES to make.  Stop._

  Usually this indicates that a suitable source ami can't be found.

  Are you specifying a channel in your Makefile? e.g. stable or \*

