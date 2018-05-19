# Makefile quick tutorial

A Makefile is __a collection of rules__. Each rule is a recipe to do a specific thing, sort of like a grunt task or an npm ``package.json`` script.

A rule looks like this:

```makefile
<target>: <prerequisites...>
	<commands>
```

The ``target`` is required. The ``prerequisites`` are optional, and the ``commands`` are also optional, but you have to have one or the other.

---

__Special Variables :__

```makefile
$@
```

>The file that is being made right now by this rule (aka the ``target``).
>
>``@`` is like a letter ``a`` for ``argument``. When you type ``make foo``, the ``foo`` is the argument.

```makefile
$<
```

> The input file (this is, __the first prerequisite__ in the list).
>
> The ``<`` is like a file input pipe in bash.

```makefile
$^
```

> This is the list of __all__ input files, not just the first one.

```makefile
$?
```

> All the input files that are newer than the target.
>
> _It's like a question. "Wait, why are you doing this? What files changed to make this necessary?_

```makefile
$$
```

> _More dollar signs equals more cash money equals dollar sign._

```makefile
$*
```

> The __stem__ part that matched in the rule definition's ``%`` bit.
>
> _The `%` is like ``*`` on the shell, so ``$*`` is telling you what matched the pattern._

You can also use the special syntax ``$(@D)`` and ``$(@F)`` to refer to just the __directory__ and __file__ portions of ``$@``, respectively.  ``$(<D)`` and ``$(<F)`` work the same way on the ``$<`` variable.  You can do the __D/F__ trick on any variable that looks like a filename.

Example:

```makefile
result-using-var.txt: source.txt
	@echo "buildling result-using-var.txt using the $$< and $$@ vars"
	cp $< $@
```

>  _If we had 100 source files, that we want to convert into 100 result files. Rather than list them out one by one in the makefile, we can use a bit of shell scripting to generate them, and save them in variable._

```makefile
srcfiles := $(shell ehco src/{00..99}.txt)

@# ------------------------------------------------------------------------------------
src/%.txt:
	@# First things first, create the dir if it doesn't exist.
	@# Prepend with @ because srsly who cares about dir creation
	@[ -d src ] || mkdir src
	@# then, we just echo some data into the file
	@# The $* expands to the "stem" bit matched by %
	@# So, we get a bunch of files with numeric names, containing their number
	echo $* > $@
@# Note that you have to type `make src/#.txt` 100 times.
@# ------------------------------------------------------------------------------------

source: $(srcfiles)
@# Just running `make source` will make ALL of th files in the src/dir.

@# ------------------------------------------------------------------------------------
dest/%.txt: src/%.txt
	@[ -d dest ] || mkdir dest
	cp $< $@
@# Note that this is great and all, but you have to type `make dest/#.txt` 100 times.
@# ------------------------------------------------------------------------------------

destfiles := $(patsubst src/%.txt,dest/%.txt,$(srcfiles))
destination: $(destination)

@# ------------------------------------------------------------------------------------
@# All of these dest files should be gathered up into a proper compiled program, 
@# then we use the `kitty`.
kitty: $(destfiles)
	cat $^ > kitty
@# ------------------------------------------------------------------------------------

@# ------------------------------------------------------------------------------------
@# We can not test the kitty unless it exists, so we have to depend on that.
test: kitty
	@echo "miao" && echo "test all pass!"
@# ------------------------------------------------------------------------------------

@# ------------------------------------------------------------------------------------
clean:
	rm -rf *txt src dest kitty

@# ------------------------------------------------------------------------------------
@# Make will abort and refuse to proceed if any of the commands exits with a non-zero 
@# error code. To demonstrate this, we'll use the `false` program, which just exits 
@# with a code of 1 and does nothing else.
badkitty:
	$(MAKE) kitty # The special var $(MAKE) means "the make currently in use".
	false # <-- this will fail
	echo "should not get there"

@# ------------------------------------------------------------------------------------
@# Since source, destination, clean, test and badkitty all aren't actual filename, 
@# we define that as a .PHONY as well. This way, Make won't bother itself checking 
@# to see if the file named "destination" exists if we have something that depends 
@# on it later.
.PHONY: source destination clean test badkitty
```

***

You'd want to [See more](https://gist.github.com/isaacs/62a2d1825d04437c6f08).

