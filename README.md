# thrift-nicejson: A Nice JSON wire-format for Thrift

I'm a big fan of Apache Thrift, for many reasons:

1. modular, so you can modify bits of the underlying infrastructure
   without forking the entire thing.  I've
  
  * ported (C++) Thrift to run on Infiniband ibverbs
  * modified the way server- and client-side wrappers are initialized,
    so that a connection established from process P1 to process P2,
    can be used by process P2 to send RPCs to process P1
  * and so that the connection was initially established using
    socketpair(2) and not connect(2).
	
2. Supports my favorite programming language (Objective Caml)

But there's *one* big, big missing feature (for me): Thrift doesn't

1. have a human-readable wire-representation like Protocol Buffers'
"Compact Text Format", or (with Protocol Buffers 3) JSON.

2. And furthermore, if you have a (binary) serialized thrift message,
there's no quick, simple way to dump it in a format where all the
fields are there

3. and where the format is one that can be re-marshaled back into
   Thrift's binary serialized format.
   
In short, Thrift needs a human-readable wire-format, and a "type
library" facility so that one can use to "disassemble"
binary-serialized messages to that format.

This library provides those facilities.

## Licensing

All files are governed by the Apache license (included herein in file
LICENSE) except for json.hpp, which is governed by the MIT License,
and a number of GNU autotools files, which are all governed by their
own licenses, typically GPL.

## Credits and Thanks

First, this code is descended by modification from code and examples
found in Apache Thrift.  In many filies I've leaft the copyright
headers as-is, b/c as far as I'm concerned, I'm happy to cede
ownership of this code to Apache, with the following exceptions:

The file "json.hpp" was copied with permission from
[JSON for Modern C++](https://github.com/nlohmann/json) created by
Neils Lohmann, and he continues to own it.  He licenses that file
under the MIT license (included in the source). This thing is bloody
lovely marvel.

And of course, there aare a bunch of GNU files, owned by their
respective owners.

