# Overview

This gem provides a toolkit for interfacing with Netlink in pure ruby.

# Caveat Emptor

This gem is very much a work-in-progress. It can be used to do useful things in
its current state, but still has some rough edges (see Todo).

# Netlink 101

## Overview

Netlink provides an efficient mechanism for user-space to kernel-space and
user-space to user-space communication. It supports both unicast and multicast
communication and is implemented as a message oriented protocol using the BSD
sockets api. Sample use cases include updating routing tables, querying for
detailed task information, and receiving notifications when users exceed
disk quotas.

## Message format

The Netlink message format is fairly simple. All messages are composed of
a mandatory Netlink header, following by 0 or more family headers, followed by
the message payload. The majority of message payloads consist of a sequence
of attributes encoded using the TLV (Type, Length, Value) format. We attempt
to optimize for this case and provide a convenient DSL for declaring message
structure.

## Error Handling

Netlink provides two means of communicating errors back to the user: 1) through
the use of special error messages, and 2) through the BSD sockets api. The first
mechanism is used to signal errors pertaining to the various subsystems (invalid
arguments in requests, for example). The second mechanism is used to signal errors
that occur when transferring data between user-space and kernel-space. For example,
recvmsg() will return ENOBUFS if the kernel fails to transfer data to the user.

# Usage

See the `example' directory.

# Todo

## Must Have

- Nested attribute support
- Multi-part message support

## Nice to Have

- Pretty printing of messages

## MIT License (MIT)

Copyright (c) 2013 Matt Page

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
