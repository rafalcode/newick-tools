# Copyright (C) 2015 Tomas Flouri
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU Affero General Public License as
# published by the Free Software Foundation, either version 3 of the
# License, or (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU Affero General Public License for more details.
#
# You should have received a copy of the GNU Affero General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.
#
# Contact: Tomas Flouri <Tomas.Flouri@h-its.org>,
# Heidelberg Institute for Theoretical Studies,
# Schloss-Wolfsbrunnenweg 35, D-69118 Heidelberg, Germany

# Profiling
#PROFILING=-g -pg
PROFILING=-g

# Compiler warnings
WARN=-Wall -Wsign-compare

CC = gcc
CFLAGS = -g $(WARN) -D_GNU_SOURCE
LINKFLAGS=$(PROFILING)
LIBS=-lm

BISON = bison
FLEX = flex

PROG=newick-tools

all: $(PROG)

OBJS=util.o newick-tools.o parse_rtree.o parse_utree.o lex_rtree.o lex_utree.o \
     arch.o rtree.o utree.o lca_tips.o lca_utree.o prune.o svg.o subtree.o \
     parse_ntree.o lex_ntree.o ntree.o info.o utree_bf.o stats.o create.o dist.o \
     bd.o labels.o attach.o

$(PROG): $(OBJS)
	$(CC) -Wall $(LINKFLAGS) $+ -o $@ $(LIBS)

%.o: %.c
	$(CC) $(CFLAGS) -c -o $@ $<

parse_%.c: parse_%.y
	$(BISON) -p $*_ -d -o $@ $<

%.c: %.l
	$(FLEX) -o $@ $<

clean:
	rm -f *~ $(OBJS) gmon.out $(PROG) parse_rtree.c parse_utree.c parse_ntree.c lex_rtree.c lex_utree.c lex_ntree.c parse_rtree.h parse_utree.h parse_ntree.h
