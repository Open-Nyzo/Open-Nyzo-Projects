# Possible transport layers

We'll differentiate the commands themselve - methods names and parameters - from the transport layer.

Command lists then only need to be specified and documented once, no matter the transport used.

See Commands.md for minimal and full command list

## json-rpc

Classic json-rpc calls, command and params sent as json with json-rpc header, answer sent as json.  

Usage: bitcoin like clients and wallets

Example:  
```
TODO
```

Implementations: ...

## websocket

Usage: full js light wallets, web dapps.

Example:  
```
TODO
```

Implementations: ...

## http(s) API

endpoint is base API endoint /command_name/ , parameters can be sent via POST or GET

Example:  
```
TODO
```

Implementations: ...
