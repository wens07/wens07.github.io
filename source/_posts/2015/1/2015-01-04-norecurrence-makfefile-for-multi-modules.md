---
title: norecurrence makfefile for multi-modules
date: 2015-01-04 21:53:02
categories: technique
tags: script
keywords: makefile
---

## modules makefile(module.mk)

```makefile
	    local_dir  := lib/codec
	    local_lib  := $(local_dir)/libcodec.a
		local_src  := $(addprefix $(local_dir)/,codec.c)
		local_objs := $(subst .c,.o,$(local_src))

		libraries  += $(local_lib)
		sources    += $(local_src)

		$(local_lib): $(local_objs)
		        $(AR) $(ARFLAGS) $@ $^
```
<!-- more -->

## top makefile

```makefile
		# Collect information from each module in these four variables.
		# Initialize them here as simple variables.
		programs     :=
		sources      :=
		libraries    :=
		extra_clean  :=

		# objects and dependencies are recursive variable because at this
		# point in the makefile the sources variable is empty, so they will
		# be populated later when the include files are read
		objects      = $(subst .c,.o,$(sources))
		dependencies = $(subst .c,.d,$(sources))

		# include_dirs is used to avoid duplicated the include dirs
		include_dirs := lib include
		CPPFLAGS     += $(addprefix -I ,$(include_dirs))
		vpath %.h $(include_dirs)

		# see makefile convention post for variable
		MV  := mv -f
		RM  := rm -f
		SED := sed

		# we should set all as the default goal, because in the include file
		# there exist targets, but we also should include the module makefile
		# first because programs variable is empty(the all target's prerequisites
		# is varibale programs), so the following code solve the awkward.
		all:

		include lib/codec/module.mk
		include lib/db/module.mk
		include lib/ui/module.mk
		include app/player/module.mk

		.PHONY: all
		all: $(programs)

		.PHONY: libraries
		libraries: $(libraries)

		.PHONY: clean
		clean:
		        $(RM) $(objects) $(programs) $(libraries) \
		              $(dependencies) $(extra_clean)

		ifneq "$(MAKECMDGOALS)" "clean"
		  include $(dependencies)
		endif

		%.c %.h: %.y
		        $(YACC.y) --defines $<
		        $(MV) y.tab.c $*.c
		        $(MV) y.tab.h $*.h

		# sed command use to add relative path to the dependency, because some tools
		# like gcc are not include the relative path to the dependency output
		%.d: %.c
		        $(CC) $(CFLAGS) $(CPPFLAGS) $(TARGET_ARCH) -M $< | \
		        $(SED) 's,\($(notdir $*)\.o\) *:,$(dir $@)\1 $@: ,' > $@.tmp
		        $(MV) $@.tmp $@

```



## optimized top makefile for projects

```makefile
		# $(call source-to-object, source-file-list)
		source-to-object = $(subst .c,.o,$(filter %.c,$1)) \
	                       $(subst .y,.o,$(filter %.y,$1)) \
	                       $(subst .l,.o,$(filter %.l,$1))
		# $(subdirectory)
		subdirectory = $(patsubst %/module.mk,%,                      \
	                   $(word                                         \
	                     $(words $(MAKEFILE_LIST)),$(MAKEFILE_LIST)))

		# $(call make-library, library-name, source-file-list)
		define make-library
	  	libraries += $1
	  	sources   += $2
	 	$1: $(call source-to-object,$2)
	        $(AR) $(ARFLAGS) $$@ $$^

		endef

		# $(call generated-source, source-file-list)
		generated-source = $(subst .y,.c,$(filter %.y,$1))      \
	                       $(subst .y,.h,$(filter %.y,$1))      \
	                       $(subst .l,.c,$(filter %.l,$1))

		# Collect information from each module in these four variables.
		# Initialize them here as simple variables.
		modules      := lib/codec lib/db lib/ui app/player
		programs     :=
		libraries    :=
		sources      :=

		objects      =  $(call source-to-object,$(sources))
		dependencies =  $(subst .o,.d,$(objects))

		include_dirs := lib include
		CPPFLAGS     += $(addprefix -I ,$(include_dirs))
		vpath %.h $(include_dirs)

		MV  := mv -f
		RM  := rm -f
		SED := sed

		all:

		include $(addsuffix /module.mk,$(modules))

		.PHONY: all
		all: $(programs)

		.PHONY: libraries
		libraries: $(libraries)

		.PHONY: clean
		clean:
		        $(RM) $(objects) $(programs) $(libraries) $(dependencies)       \
		              $(call generated-source, $(sources))
		ifneq "$(MAKECMDGOALS)" "clean"
		  include $(dependencies)
		endif

		%.c %.h: %.y
		        $(YACC.y) --defines $<
		        $(MV) y.tab.c $*.c
		        $(MV) y.tab.h $*.h
		%.d: %.c
		        $(CC) $(CFLAGS) $(CPPFLAGS) $(TARGET_ARCH) -M $< | \
		        $(SED) 's,\($(notdir $*)\.o\) *:,$(dir $@)\1 $@: ,' > $@.tmp
		        $(MV) $@.tmp $@
```

## optimized module.mk makefile(lib/codec) for module

```makefile
	 	# $(call make-library, library-name, source-file-list)
	    define make-library
	       libraries += $1
	       sources   += $2
	       $1: $(call source-to-object,$2)
	           $(AR) $(ARFLAGS) $$@ $$^
		endef

		local_src := $(wildcard $(subdirectory)/*.c)
		     $(eval $(call make-library, $(subdirectory)/libcodec.a, $(local_src)))
```
