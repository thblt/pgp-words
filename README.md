# pgp-words

`pgp-words` is an implementation of the
[PGP Word List](https://en.wikipedia.org/wiki/PGP_word_list).  The
word list was designed to make it easy to convey sequences of bytes
using only voice, and is particularly suited for transmitting key
fingerprints and other similar sequences over the phone. Even in the
same physical place, it's easier to just read a bunch of words out
loud than to spell a sequence of hex digits (was that 3 times `F` or
`3F`?)

Each word represents exactly one byte.  To avoid errors, there are
actually 512 words in the list (two per possible byte value) and words
are selected depending on the parity of the byte position.  For
example, `0x9e` is *quiver* if the byte position in the sequence is an
even number, *onlooker* if it is odd.

`pgp-words` is a single-file script written in Python, depends only on
core features, its source code is really short (314 SLOCs, 256 of them
being the word list) and can be easily audited. It should work on any
system with a Python interpreter, and is compatible with Python 2 and
3.

# Usage

`pgp-words` reads a fingerprint or any other hexadecimal sequence,
either from the command line or the standard input, and converts it
into words:

```
$ pgp-words d1c2 25e4 26c6 33dd 94d1  a7e8 c3f4 08aa 9b34 2488

d1c225e426c633dd94d1a7e8c3f408aa9b342488:
	stairway repellent bombast tradition
	bookshelf responsive chisel tambourine
	Pluto scavenger repay typewriter
	snowcap Virginia aimless pedigree
	puppy confidence bluebird maritime

gpg --fingerprint 0x33CDE511  | pgp-words

EA5B 81C5 6498 8C73 EE90  DEE9 BAF1 E072 33CD E511:
        Trojan exodus minnow resistor
        flytrap narrative offload hurricane
        tycoon millionaire tactics ultimate
        shadow vacancy tapeworm holiness
        chisel sandalwood topmost Babylon
```

 - When called with command-line arguments, it concatenates them and treats them as a single value.
 - When called from stdin, it treats each lins as a single value and silently ignores invalid lines.
 - For simplicity, spaces, tabs and newlines are ignored.

# Installation

Either copy `pgp-words` somewhere in your `$PATH` and `chmod +x pgp-words`, or just run `sudo python setup.py install` from the root of the repository.

To uninstall, simply remove the `pgp-words` script from wherever you put it.
