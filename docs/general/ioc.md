# smallstack IOC
With a custom IOC (inversion of control) we closed the gap between the very dynamic way of creating large javascript and configuring an even bigger system dynamically. Our IOC is nothing more than a unique key->reference storage which is available in all environments (server, browser, native mobile applications).

## Register an object/class
```
IOC.register(NAME, OBJECT);
```

## Get an object/class
```
IOC.get<TYPE>(NAME);
```

## Example
One of our core services is called 'userService'. We registered it via IOC.register("userService", new UserService()), that way we can ensure that there exists exactly one instance of this service. Lateron, in our source, we can get that instance by calling IOC.get<UserService>("userService").

## Decorator
For typescript classes we created a typescript decorator called "Autowired":
```
class Test {
  @Autowired("userService")
  private userService: UserService;
}

// or, in short form

class Test {
  @Autowired()
  private userService: UserService;
}
```
Please note that the ladder version uses the property name to determine which object to get from our IOC. @Autowired() usersService: UserService will therefor fail!
