OUT := mgr-uccd
DISTRO := $(shell cat /etc/os-release | grep '^NAME=' | sed -e 's/.*=//')
GCCGO :=
GO :=
ifeq ($(DISTRO),"Ubuntu")
	GCCGO += gccgo
	GO += go
else ifeq (($DISTRO),"openSUSE Leap")
	GCCGO += gccgo-8
	GO += go-8
endif

SOURCES = \
	*.go

all: mainbuild

mainbuild: $(SOURCES)
	$(GO) build -x -o $(OUT) $(SOURCES)

gcc:
ifneq ($GCCGO,)
	$(GO) build -compiler $(GCCGO) -gccgoflags '-static-libgo' -o $(OUT)
else
	@echo "Cannot find gccgo"
endif

deps:
	$(GO) get -v ./... 2>/dev/null ||:
strip:
	strip $(OUT)

clean:
	$(GO) clean -x -i

flush-cache:
	$(GO) clean -cache -modcache -i -r

.PHONY: all install clean
