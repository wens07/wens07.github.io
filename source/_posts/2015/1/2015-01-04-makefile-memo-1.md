---
title: makefile memo(1)
date: 2015-01-04 20:31:13
categories: technique
tags: script
keywords: makefile
---

### set makefile dependency

```makefile
	VPATH    = src include
	CPPFLAGS = -I include
	SOURCES  = count_words.c \
	             lexer.c       \
	             counter.c
	count_words: counter.o lexer.o -lfl
	  count_words.o: counter.h
	  counter.o: counter.h lexer.h
	  lexer.o: lexer.h
	  include $(subst .c,.d,$(SOURCES))
	  %.d: %.c
	     $(CC) -M $(CPPFLAGS) $< > $@.$$$$;  \
	     sed 's,\($*\)\.o[ :]*,\1.o $@ : ,g' < $@.$$$$ > $@;     \
	     rm -f $@.$$$$
```
<!-- more -->

### @ and -

@: the silent command modifier
	```bash
	ifndef VERBOSE
		QUIET := @
	endif

	target:
		$(QUIET) echo .....
	```  

 prevent makefile to print or output warning

### echo commands executed from shell function

`make SHELL='/bin/bash -x' -f makefile`


### *lazy initialization for variable*

```makefile
	#(call find-compilation-dirs, root-directory)
	find-compilation-dirs = 		\
		$(patsubst %/,%,			\
			$(sort					\
				$(dir				\
					$(shell $(FIND) $1 -name '*.cpp'))))

    PACKAGE_DIRS = $(redefine-package-dirs) $(PACKAGE_DIRS)

	redefine-packge-dirs = \
		$(eval PACKAGE_DIRS := $(call find-compilation-dirs, $(SOURCE_DIR)))

```

Explain above in detail:
1. When make reads these variables, it simply records their righthand side because the variables are recursive.
2. The first time the PACKAGE_DIRS variable is used, make retrieves the righthand side and expands the first variable, redefine-package-dirs.
3. The value of redefine-package-dirs is a single function call, eval.
4. The body of the eval redefines the recursive variable, PACKAGE_DIRS, as a simple variable whose value is the set of directories returned by find-compilation-dirs. Now PACKAGE_DIRS has been initialized with the directory list.￼￼￼￼￼
5. The redefine-package-dirs variable is expanded to the empty string (because eval expands to the empty string).
6. Now make continues to expand the original righthand side of PACKAGE_DIRS. The only thing left to do is expand the variable PACKAGE_DIRS. make looks up the value of the variable, sees a simple variable, and returns its value.
