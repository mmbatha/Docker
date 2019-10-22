FROM		alpine

LABEL		Author="Monde MBATHA <mmbatha@student.42.fr>" \
			Description="Alpine-based container that launches my 'favourite' editor" \
			License="MIT License 2.0" \
			Usage="docker run ex00"

RUN			apk update && apk add vim

ENTRYPOINT	[ "vim" ]

### Build
# docker build -t ex00 .
