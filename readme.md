# Flaggy
A home grown feature flag service. 

## Approach
1. Build an REST API 
    - SQLite, it's home grown. Could deliver at scale as a service with something
    like Turso. 
    - HTTP server in ??? (Go, Python) 
    - Oof, I have to write a parser for a rule language. Cool, I'll get to learn
    about parsers. 
1. Containerize. 
    - Docker probably. About time I learned how to properly write a Dockerfile.
1. Build front end webapp application. 
    - Preferrably something very light. Maybe htmx/unpoly. 
    - See https://www.reddit.com/r/htmx/comments/11jwxeq/authentication_for_htmx_app/ 
    for htmx auth. 

## Data structures
```
Flag : 
    str id,
    str name, 

Rule(str) : 
    # A str in a language used to construct conditions and outcomes for 
    conditional returns of flag value. 
    
    str id,
    str value,

Auth : 
    str user_id, 
    str secret_key, 
```

## API 
Flaggy has a simple API to manage feature flags: 

### Flags 
```
flaggy.create_flag(str name) -> bool : 

flaggy.set_flag(bool flag) -> bool : 

flaggy.get_flag(Context ctx, str name) -> bool : 

flaggy.delete_flag(str name) -> bool : 
```

### Rules 
```
flaggy.create_rule(
    str name, 
    str flag_name, 
    str rule, 
) -> bool : 

flaggy.set_rule(
    str name, 
    str flag_name, 
    str rule, 
) -> bool : 

flaggy.get_rule(
    str name, 
    str flag_name, 
) -> bool : 

flaggy.delete_rule(
    str name, 
    str flag_name, 
) -> bool : 
```

## Flaggy Client

```
init(str host, str secret_key) -> FlaggyClient : 
    # Connect to a flaggy server at @host with @secret_key for auth. 
    # Returns a flaggy client instance for this session. 
    # 
    # TODO: Will eventually create a websocket connection for broadcasts. 

Context : 
    # Client context for interacting with a server.     

    str flaggy_server, 
    str secret_key,

FlaggyClient : 
    # Client side object used in the front end script to maintain a channel to 
    send requests and listen for broadcasts. 
    # Likely pure JS. 

    Context ctx,

```
