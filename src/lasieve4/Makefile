# Copyright (C) 2001,2002 Jens Franke
# This file is part of gnfs4linux, distributed under the terms of the
# GNU General Public Licence and WITHOUT ANY WARRANTY.

# You should have received a copy of the GNU General Public License along
# with this program; see the file COPYING.  If not, write to the Free
# Software Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA
# 02111-1307, USA.
#
# 6/13/04: Hacked up for use in GGNFS by Chris Monico.

INC=-I.. -I../../include

BINDIR=../../bin
FACT=prho.o

.SUFFIXES:

.SECONDARY: *.c *.o

.PHONY: all clean

SRCFILES=fbgen.c gnfs-lasieve4e.c input-poly.c mpqs.c mpz-ull.c \
         real-poly-aux.c redu2.c gmp-aux.c if.c lasieve-prepn.c \
         primgen32.c recurrence6.c lasieve.h ppc32/siever-config.h

OBJS=../if.o input-poly.o redu2.o recurrence6.o ../fbgen.o \
     real-poly-aux.o primgen32.o lasieve-prepn.o mpqs.o

all: $(BINDIR)/gnfs-lasieve4I12e $(BINDIR)/gnfs-lasieve4I13e \
     $(BINDIR)/gnfs-lasieve4I14e

%.o: %.c lasieve.h
	$(CC) $(CFLAGS) $(INC) -c -o $@ $<

input-poly.o: lasieve.h

recurrence6.o: recurrence6.c lasieve.h
	$(CC) $(CFLAGS) $(INC) -c -o $@ $<

redu2.o: lasieve.h

primgen32.o ../fbgen.o: lasieve.h

gnfs-lasieve4eI%.o: gnfs-lasieve4e.c lasieve.h
	$(CC) $(CFLAGS) $(INC) -c -DI_bits=$* -o $@ $<

libgmp-aux.a: gmp-aux.o mpz-ull.o
	$(AR) rcs $@ $^

lasieve-prepn.o: lasieve.h

$(BINDIR)/gnfs-lasieve4I12e: gnfs-lasieve4eI12.o libgmp-aux.a $(OBJS) \
                             ppc32/liblasieve.a ppc32/liblasieveI12.a $(FACT)
	$(CC) $(CFLAGS) $(INC) -o $@ $^ -L. -lgmp-aux -lgmp -lm

$(BINDIR)/gnfs-lasieve4I13e: gnfs-lasieve4eI13.o libgmp-aux.a $(OBJS) \
                             ppc32/liblasieve.a ppc32/liblasieveI13.a $(FACT)
	$(CC) $(CFLAGS) $(INC) -o $@ $^ -L. -lgmp-aux -lgmp -lm

$(BINDIR)/gnfs-lasieve4I14e: gnfs-lasieve4eI14.o libgmp-aux.a $(OBJS) \
                             ppc32/liblasieve.a ppc32/liblasieveI14.a $(FACT)
	$(CC) $(CFLAGS) $(INC) -o $@ $^ -L. -lgmp-aux -lgmp -lm

ppc32/lib%.a:
	$(MAKE) -C ppc32

clean:
	-rm -f *.o *.a $(BINDIR)/gnfs-lasieve4I1?e
	make -C ppc32 clean
