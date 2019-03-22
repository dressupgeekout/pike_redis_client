# redis_client.pmod

This is a Redis client implemented as a Pike module. I noticed that the
[list of clients][1] on Redis' website was lacking a Pike implementation,
and since I've recently decided to learn Pike, I thought I'd contribute
this.

The design of this library is primarily inspired by that of [the popular
Ruby gem][2] -- object-oriented, that is.

NOTE! **This code is not 100% ready.** It works but I don't know if
everything works. I also have no clue _how_ idiomatically Pike it is -- I've
just started learning the language. I promise I'll let everyone know when
I'm finally OK with this code. Most notably, there is no support for command
pipelining nor asynchronous execution just yet.


## Example

    include .redis_client;

    int main() {
      Redis db;
      
      db = Redis();
      db->connect();
      db->ping();
      db->echo("Hello, Redis -- from Pike");

      db->lpush("characters", "Marten");
      db->lpush("characters", "Dora");
      db->lpush("characters", "Hannelore");
      write("There are %d characters\n", db->llen("characters"));

      db->disconnect();
      return 0;
    }


## License (2-clause BSD-style)

Copyright (c) 2013, 2019 Charlotte Koch.
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

  - Redistributions of source code must retain the above copyright notice,
    this list of conditions and the following disclaimer.

  - Redistributions in binary form must reproduce the above copyright
    notice, this list of conditions and the following disclaimer in the
    documentation and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE
LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
POSSIBILITY OF SUCH DAMAGE.


[1]: http://pslib.sourceforge.net
[1]: http://redis.io/clients
[2]: http://redis-rb.keyvalue.org
