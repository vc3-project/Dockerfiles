FROM lincolnbryant/gentoo-rap-base:latest
MAINTAINER Lincoln Bryant <lincolnb@uchicago.edu>

# Export the environment. This should make it easy to redefine at runtime
ENV PATH "$EPREFIX/usr/bin:$EPREFIX/bin:$EPREFIX/tmp/usr/bin:$EPREFIX/tmp/bin:/usr/bin:/bin"

# Unmask the dependencies and exit 0 to make Docker happy
RUN emerge sci-physics/root --autounmask-write ; exit 0
# Write the dependencies to the package.use file
RUN cp $EPREFIX/etc/portage/._cfg0000_package.use $EPREFIX/etc/portage/package.use
# Build the package
RUN emerge sci-physics/root
