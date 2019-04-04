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
## Extract Variables

```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<ExtractVariables async="false" continueOnError="false" enabled="true" 
name="ExtractStoreLatLong">
    <DisplayName>ExtractStoreLatLong</DisplayName>
    <Properties/>
    <IgnoreUnresolvedVariables>true</IgnoreUnresolvedVariables>
    <JSONPayload>
        <Variable name="lat">
            <JSONPath>$.location.latitude</JSONPath>
        </Variable>
        <Variable name="long">
            <JSONPath>$.location.longitude</JSONPath>
        </Variable>
    </JSONPayload>
    <Source clearPayload="false">response</Source>
</ExtractVariables>
```

