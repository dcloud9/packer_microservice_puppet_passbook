# packer\_microservice\_puppet\_notifications

... used to build role AMIs for the notifications product

## Structure

Each subdir is a role definition that can build an AMI
containing a Makefile, and any bespoke uploads or build
scripts for that role.

## Usage

### 1. choose the ami you want to build.
Enter the role directory corresponding to the AMI you wish to build.

### 2. packer\_includes
Clone _packer\_includes_ at level of Makefile. Checkout a tag if desired.
(The x.y.z tags should represent a stable version of packer_includes).

If you do use a tag, add the line:

        export PACKER_INCLUDES_GIT_TAG=... # replace dots with the tag value.

This will let you know in the future which dependency to use to reproduce
this build.

### 3. export env vars

Export vars deliberately not defined in Makefile.

### 4. make sure any other dependencies exist.

Check all of the sources defined in the Makefile
including git tags etc ... exist.

Amend the Makefile as required.

### 5. build

        make clean build

If you are playing around with the puppet stuff that
appears under uploads/puppet, on subsequent avoid the _clean_ target.

        make build # don't trash my modifications under puppet dir

## Known Issues

* The puppet stuff depends on a bunch of 3rd party modules.
  
  These may cease to exist at a future date. 

* When building an appsvr (EUROSTAR\_SERVICE\_ROLE), you need to

  specify an APP\_VERSION that actually exists in AWS dev s3 under:

  /enovation/$EUROSTAR\_SERVICE\_NAME/artefacts/integration/$APP_VERSION

**TODO: stop using env specific folders for versioned artefacts!**

* _Make error: \*\*\* You must pass env var AMI_PREVIOUS\_SOURCES to make.  Stop._

  Usually this indicates that a suitable source ami can't be found.

  Are you specifying a channel in your Makefile? e.g. stable or \*

