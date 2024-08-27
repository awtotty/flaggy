# Flaggy
A home grown feature flag service. 

## Approach
1. Build an REST API 
    - Oof, I have to write a parser for a rule language. Cool, I'll get to learn
    about parsers. 
1. Build front end webapp application. 
    - Preferrably something very light. Maybe htmx/unpoly. 
1. Containerize. 
    - Docker probably. About time I learned how to properly write a Dockerfile.

## API 
Flaggy has a simple API to manage feature flags: 

### Flags 
```
flaggy.create_flag(str name) -> bool : 

flaggy.set_flag(bool flag) -> bool : 

flaggy.get_flag(str name) -> bool : 

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
flaggy.init(str host, str secret_key) -> flaggy_client : 
    # Connect to a flaggy server at @host with @secret_key for auth. 
    # Returns a flaggy client instance for this session. 
    # 
    # TODO: Will eventually create a websocket connection for broadcasts. 

flaggy.FlaggyClient : 
```
