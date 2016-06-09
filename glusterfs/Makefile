# vim: ts=4 st=4 sr noet smartindent:
# SET THESE VARS BEFORE RUNNING make build:
# ... we don't want them committed to public scm
export AWS_ACCESS_KEY_ID?=
export AWS_SECRET_ACCESS_KEY?=
export METRICS_REMOTE_HOST?=
export METRICS_REMOTE_PORT?=

### ABOUT BUILD SOURCES
#   ... packer_includes
export PACKER_INCLUDES_GIT_TAG:=2.0.6
#   ... ami sources
export AMI_SOURCE_CHANNEL:=stable
export AMI_SOURCE_PREFIX:=eurostar_monlog

#   ... puppet sources (eif_puppet)
# ... using 2.0.0: app_version instead of build_id for deployer
export PUPPET_BRANCH=notification
export PUPPET_GIT_TAG=1.0.2
export PUPPET_REPO=git@github.com:dcloud9/eif_puppet.git

### ABOUT AWS ...
export AWS_INSTANCE_TYPE:=t2.large
export AWS_REGION:=eu-west-1

### ABOUT THIS PRODUCT

# ... EUROSTAR_RELEASE_VERSION overriden from THIS repo's checked-out
#     tag if one exists (e.g when building a release)
#export EUROSTAR_RELEASE_VERSION:=alpha
export EUROSTAR_SERVICE_NAME:=passbook
export EUROSTAR_SERVICE_ROLE:=glusterfs
export PUPPET_PRODUCT=passbook
export PUPPET_ROLE=shared-storage
export PUPPET_SERVICE=passbook

### ADDITIONAL FOR PUPPET CONFIG
export BASE_DOMAIN=eurostar.com

include packer_includes/make/bootstraps/microservice_puppet.mak
