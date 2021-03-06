# Copyright © 2015-2018 Jakub Wilk <jwilk@jwilk.net>
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the “Software”), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in
# all copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

.PHONY: all
all:

.PHONY: clean
clean:
	rm -rf *.arj tmp* moo* zoo* cur* par*

ifeq "$(shell command -v arj;)" ""
$(error arj(1) is needed to create ARJ samples)
endif

all: absolute1.arj
absolute1.arj:
	rm -f $(@)
	umask 022 && echo moo > moo
	arj m $(@) moo
	printf '/tmp/moo\n' | arj n $(@)

all: absolute2.arj
absolute2.arj:
	rm -f $(@)
	umask 022 && echo moo > moo
	arj m $(@) moo
	printf '//tmp/moo\n' | arj n $(@)

all: relative0.arj
relative0.arj:
	rm -f $(@)
	umask 022 && echo moo > moo
	arj m $(@) moo
	printf '../moo\n' | arj n $(@)

all: relative2.arj
relative2.arj:
	rm -f $(@)
	umask 022 && echo moo > moo
	arj m $(@) moo
	printf 'tmp/../../moo\n' | arj n $(@)

all: symlink.arj
symlink.arj:
	rm -f $(@)
	ln -sf /tmp/moo moo
	arj m -a $(@) moo
	umask 022 && echo moo > zoo
	arj m -a $(@) zoo
	printf '\nmoo\n' | arj n $(@)

all: dirsymlink.arj
dirsymlink.arj:
	ln -sf /tmp tmp
	arj m -a $(@) tmp
	mkdir -m 755 tmp
	umask 022 && echo moo > tmp/moo
	arj a -a $(@) tmp/moo
	rm -rf tmp

all: dirsymlink2a.arj
dirsymlink2a.arj:
	ln -sf . cur
	ln -sf cur/.. par
	arj m -a $(@) cur par
	mkdir -m 755 par
	umask 022 && echo moo > par/moo
	arj a -a $(@) par/moo
	rm -rf par

all: dirsymlink2b.arj
dirsymlink2b.arj:
	ln -sf . cur
	ln -sf .. par
	arj a -a $(@) cur cur/par
	rm -f cur par
	mkdir -m 755 par
	umask 022 && echo moo > par/moo
	arj a -a $(@) par/moo
	rm -rf par

.error = GNU make is required

# vim:ts=4 sts=4 sw=4 noet
