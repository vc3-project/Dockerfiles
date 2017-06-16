FROM lincolnbryant/gentoo-rap-base:latest
MAINTAINER Lincoln Bryant <lincolnb@uchicago.edu>

# Export the environment. This should make it easy to redefine at runtime
ENV PATH "$EPREFIX/usr/bin:$EPREFIX/bin:$EPREFIX/tmp/usr/bin:$EPREFIX/tmp/bin:/usr/bin:/bin"

RUN emerge sci-physics/geant sci-physics/geant-data sci-physics/geant-python
