# Fault Handling


## /stores/* GET

```
<Flow name="GetStore">
		<Condition>
           (proxy.pathsuffix MatchesPath "/stores/*") and (request.verb = "GET")
</Condition>
		<Request/>
		<Response/>
</Flow>

```

