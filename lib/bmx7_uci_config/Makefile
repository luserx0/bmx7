
CFLAGS +=	$(CORE_CFLAGS) -fpic -I../../ -I/usr/local/include/uci/
LDFLAGS +=	-luci

PLUGIN_NAME =   bmx7_config

SRC_C = uci_config.c
SRC_H = uci_config.h
OBJS= $(SRC_C:.c=.o)

PLUGIN_FULLNAME = $(PLUGIN_NAME).so
PLUGIN_SHORTNAME = $(PLUGIN_NAME).so

LIBDIR = /usr/lib
THISDIR = $(shell pwd )

all:	$(PLUGIN_FULLNAME) Makefile


$(PLUGIN_FULLNAME):	$(OBJS) Makefile
	$(CC) -shared $(OBJS) $(LDFLAGS) $(EXTRA_LDFLAGS) -o $(PLUGIN_FULLNAME)
	ln -f -s $(THISDIR)/$(PLUGIN_FULLNAME) $(THISDIR)/../$(PLUGIN_FULLNAME)

%.o:	%.c %.h Makefile
	$(CC) $(CFLAGS) $(EXTRA_CFLAGS) -c $< -o $@


clean:
	rm -f *.o *.so
	

install:	all
		mkdir -p $(LIBDIR)
		install -D -m 755 $(PLUGIN_FULLNAME) $(LIBDIR)/$(PLUGIN_FULLNAME); /sbin/ldconfig -n $(LIBDIR)


strip:		all
		strip $(PLUGIN_FULLNAME)
