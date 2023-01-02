## Unicode!

Python 3!

Speaker: Lukasz Langa

### Is unicode important?

Yes! Plane ticket unicode errors can stop you from flying...

### How does Python decode a file when you import a module?

Python2 imports as ascii by default. Python3 imports as unicode by default.

Python reads the encoding you give and additionally has a `filesystem encoding` it uses but he did not cover details of this.


### What is text?

Words! Communication.


### On `bytes` and `unicode`

Programs that assume you can open a plain text file without encoding are broken.

A character is not a byte, it is a unicode codepoint. And it can have a long name and you can even use that name in python.

A codepoint cannot go on a drive. A code point is a platonic ideal, an abstract theoretical concept.

A code point specifies what character you mean, for example `U+0142`, in python `\u1402`.

In Python 2, the string type tries to be byte too which isn't truly possible.  In python 3, bytes is just bytes.


### Text Transmission

Transmitting text is challenging!

#### UTF-16

- UTF-16 had to prefix the string with a byte order mark. Must be right, must be there... not likely!
- Null bytes in the middle of your string! How do we align the bytes in the string?
- Not all characters fit in UTF-16


#### UTF-8

- Tries to be ascii compatible.
- First seven bits are ascii, after that we do 2,3,4 bytes.
- Simple algorithm: `if this is a special byte, i expect 1-3 continuation bytes after it.
    - This must be how we know where the codepoint ends at variable length...

```
>>> len(u'frog'.encode("utf-8")
??
>>> len(u'a'.encode("utf-16")
4
>>> len(u'4'.encode("utf-16")
4
```


### Real Purpose for Unicode... emojis??

Unicode is that thick book with each codepoint. UTF-8 is the encoding!!

- Unprecedented growth in the standard... We can't fit all the characters in 4 bytes.
- Solution: two pseudocode unicode characters to produce one - 8 bytes... good for now.
- Basic multilingual plane. 65536 characters.  After this we use two pseudocode. Python3 does this for you.
    - Is this for UTF-16 or UTF-8?
- You can encode codepoints in many ways, but codepoints do not have any way to write them into a file.
    - Not all encodings can encode all characters.  Code points are stored by encoding into bytes.
    - `UnicodeEncodeError` - current encoding doesn't support all the codepoints you are trying to encode to bytes
    - You can only read unicode back correctly if you know what codepoints was used to encode the bytes

### How does Python3 make things better?

Python2 does not have full unicode support - does not have the full multilingual plane or something.

```
>>> len(u'a')
1
>>> len(u'f')
1
```

- A Single Character - Python 2 does (doesn't?) work well with all but the first one.
    - BMP code point (base multilingual plane)
    - U-Dxxxx surrogate pair
    - grapheme cluster
    - sorting element (example dzs in Hungarian)


### Grapheme Cluster -- wtf!!

Use the library `unicodedata` to combine these grapheme clusters... somehow...

```
unicodedata.normalize('NFS', u'\u00c7')
unicodedata.normalize('NFS', u'\u00c7').encode('utf8')
```


### Tips!

- Using bytes for text is heading for a bug!
- Python3 reused `str` for unicode text
- In Python3 `bytes` means `bytes`
- When reading data just do `b.decode('utf-8')`
- When writing data back, just do `b.encode('utf-8)`
- Avoid using `str()` and `bytes()` without an encoding to convert between types.
- In some languages, uppercase and lowercase may not do the same things, so you can't just go back and forth.
    - Python doesn't reliably do this!!
- Python2: narrow build of python - no wide character processing, raise weird inaccurate exceptions...
    - Not common anymore
- Text segmenting, regular expression, right-to-left text
- Literary characters: en-dash, em-dash, separators, etc.
- Using bytes for text handling is a bug.
- Decode Early, Encode Late. 
    - Paraphrased: Your data should exist as codepoints for as long as possible
