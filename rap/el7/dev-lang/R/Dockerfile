FROM lincolnbryant/gentoo-rap-base:latest
MAINTAINER Lincoln Bryant <lincolnb@uchicago.edu>

#Run a sync
RUN emerge --sync
# Unmask the dependencies and exit 0 to make Docker happy
RUN emerge dev-lang/R --autounmask-write ; exit 0
# Write the dependencies to the package.use file
RUN cp $EPREFIX/etc/portage/._cfg0000_package.use $EPREFIX/etc/portage/package.use
# Build the package
RUN emerge dev-lang/R
