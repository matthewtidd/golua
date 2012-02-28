# Copyright 2009 The Go Authors.  All rights reserved.
# Use of this source code is governed by a BSD-style
# license that can be found in the LICENSE file.

include $(GOROOT)/src/Make.inc	

CGO_OFILES+=golua.o

ifndef LUA51_LIBNAME
LUA51_LIBNAME=lua5.1
endif

ifndef LUA51_INCLUDE_DIR
CGO_CFLAGS+=`pkg-config --cflags $(LUA51_LIBNAME)`
else
CGO_CFLAGS+=-I$(LUA51_INCLUDE_DIR)
endif

ifndef LUA51_LIB_DIR
CGO_LDFLAGS+=`pkg-config --libs $(LUA51_LIBNAME)`
else
CGO_LDFLAGS+=-L$(LUA51_LIB_DIR) -l$(LUA51_LIBNAME)
endif

TARG=lua51

CGOFILES=\
	lua.go \
	lauxlib.go \
	lua_defs.go

include $(GOROOT)/src/Make.pkg

%: install %.go
	$(QUOTED_GOBIN)/$(GC) $*.go
	$(QUOTED_GOBIN)/$(LD) -o $@ $*.$O

golua.o: golua.c
	gcc $(CGO_CFLAGS) $(_CGO_CFLAGS_$(GOARCH)) -fPIC $(CFLAGS) -c golua.c -o golua.o
