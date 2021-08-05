## File mode permission

There are 3x3 bit flags for a mode:

- (owning) User
  - read
  - write
  - execute
- Group
  - read
  - write
  - execute
- Other
  - read
  - write
  - execute

So each triple encodes nicely as an octal digit.

```c
rwx oct    meaning
--- ---    -------
001 01   = execute
010 02   = write
011 03   = write & execute
100 04   = read
101 05   = read & execute
110 06   = read & write
111 07   = read & write & execute
```

So 0644 is:

```c
* (owning) User: read & write
* Group: read
* Other: read
```

[Reference]: https://stackoverflow.com/questions/18415904/what-does-mode-t-0644-mean/18415935	"What does mode_t 0644 mean?"

