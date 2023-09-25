DID Types
===

There can and maybe should be some basic DID types. A DID needn't identify a player or a room. It could make sense to have methods, policies, exits etc. all have DIDs. This would allow them to be referenced in a standard way.
This is a a place to start jottting down what goes into each type of DID.

Policy
---

This is just a simple policy, you should be able to attach it to anything.

```YAML
- did:space:my_policy123:
    name: MyFrontDoorPolicy
    description: This is my policy which is intended to grant access to my house through the frontdoor.
    controller:
      - did:space:myipns
    allow:
      - all
    deny:
      - did:space:robertsipns
- did:space:my_policy123:
    name: MyBackDoorPolicy
    description: This is my policy which is intended to grant access to my house through the backdoor
    controller:
      - did:space:myipns
    allow:
      - did:space:myipns
    deny:
      - all
```
  
This type of policy can be attached to anything. As an exit policy, it would allow or deny players from leaving the room. As a method policy, it would allow or deny players from using the method. As a room policy, it would allow or deny players from entering the room.

Objects
---

```YAML
did:space:myroom:
  controller:
    - did:space:myipns
  owner: did:space:myipns
  policy: did:space:my_policy123
  exits:
    - did:space:myroom_frontdoor
    - did:space:myroom_backdoor
  attributes:
    - name: My Room
      description: This is my room
  slots:
    - did:space:myroom_slot1
    - did:space:myroom_slot2
    - 
```

Exits
---

```YAML
did:space:myroom_frontdoor:
  controller:
    - did:space:myipns
  from: did:space:lobby
  to: did:space:myroom
  policy: did:space:my_policy123
  ```

Methods
---

```YAML
did:space:open:
  controller:
    - did:space:myworldwizard
  name: Open
  type: method
  evaluator: luerl
  description: Function to check if you have acccess to a container
  args:
    - name: container
      type: object
```
  