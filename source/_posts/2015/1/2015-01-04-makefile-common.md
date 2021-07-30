---
title: makefile_common
date: 2015-01-04 21:16:11
categories: technique
tags: script
keywords: makefile
---

## makefile to include commom.mk
```makefile
	  library := libcodec.a
		sources := $(wildcard *.c)

		include ../../common.mk
```
   		
<!-- more -->
## the common.mk file

```makefile
	    objects := $(subst .c,.o,$(sources))
		dependencies := $(subst .c,.d,$(sources))
		include_dirs := .. ../../include
		CPPFLAGS     += $(addprefix -I ,$(include_dirs))

		vpath %.h $(include_dirs)
		.PHONY: library
		library: $(library)
		     $(library): $(objects)
		             $(AR) $(ARFLAGS) $@ $^

		.PHONY: clean
		clean:
             $(RM) $(objects) $(program) $(library) $(dependencies) $(extra_clean)
	    ifneq "$(MAKECMDGOALS)" "clean"
		     -include $(dependencies)
		endif

	    %.c %.h: %.y
             $(YACC.y) --defines $<
             $(MV) y.tab.c $*.c
             $(MV) y.tab.h $*.h
	     %.d: %.c
             $(CC) $(CFLAGS) $(CPPFLAGS) $(TARGET_ARCH) -M $< |      \
             $(SED) 's,\($*\.o\) *:,\1 $@: ,' > $@.tmp
             $(MV) $@.tmp $@

```
