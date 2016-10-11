# makefile for macros

# change these to reflect your Lua installation
LUA= /tmp/lhf/lua-5.1
LUAINC= $(LUA)/src
LUALIB= $(LUA)/src
LUASRC= $(LUA)/src

# no need to change anything below here
CFLAGS= $(INCS) $(WARN) -O2 $G
WARN= -ansi -pedantic -Wall

INCS= -I$(LUAINC) -I$(LUASRC)
LIBS= -L$(LUALIB) -llua -lm -ldl -lreadline -lcurses

MYNAME= tokenf
T= ./a.out
OBJS= llex.o
TEST= test.lua
FILTER= fdebug

all:	test

test:	$T
	-rm -f core core.*
	$T -l$(FILTER) $(TEST)

$T:	$(OBJS)
	$(CC) $(OBJS) $(LUASRC)/lua.o $(LIBS)

db:
	gdb $T core.*

patch:
	-diff $(LUASRC)/llex.c llex.c

clean:
	-rm -f $(OBJS) $T core core.* a.out

llex.o: proxy.c

# distribution

FTP= $(HOME)/public/ftp/lua/5.1
D= $(MYNAME)
A= $(MYNAME).tar.gz
TOTAR= Makefile,README,fdebug.lua,fnext.lua,ftrace.lua,llex.c,proxy.c,test.lua

tar:	clean
	tar zcvf $A -C .. $D/{$(TOTAR)}

distr:	tar
	touch -r $A .stamp
	mv $A $(FTP)

diff:	clean
	tar zxf $(FTP)/$A
	diff $D .

# eof
