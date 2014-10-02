### Python client to [Neovim](https://github.com/neovim/neovim)

[![Build Status](https://travis-ci.org/neovim/python-client.svg?branch=master)](https://travis-ci.org/neovim/python-client)

Library for scripting Nvim processes through it's msgpack-rpc API.

#### Installation

```sh
pip install neovim
```

#### Usage through the python REPL

A number of different transports are supported, but the simplest way to get
started is with the python REPL. First, start Nvim with a known address(or
query the value of $NVIM_LISTEN_ADDRESS of a running instance): 

```sh
$ NVIM_LISTEN_ADDRESS=/tmp/nvim nvim
```

Open the python REPL with another terminal connect to Nvim(Note that the API is
similar to the one exposed by the [python-vim
bridge](http://vimdoc.sourceforge.net/htmldoc/if_pyth.html#python-vim))

```python
>>> from neovim import socket_session, Nvim
# Create a msgpack-rpc session to the unix domain socket created by Nvim:
>>> session = socket_session('/tmp/nvim')
# Create a Nvim instance from the session(don't call Nvim constructor!):
>>> nvim = Nvim.from_session(session)
# Now do some work. 
>>> buffer = nvim.buffers[0] # Get the first buffer
>>> buffer[0] = 'replace first line'
>>> buffer[:] = ['replace whole buffer']
>>> nvim.command('vsplit')
>>> nvim.windows[1].width = 10
>>> nvim.vars['global_var'] = [1, 2, 3]
>>> nvim.eval('g:global_var')
[1, 2, 3]
```

The tests can be consulted for more examples.
