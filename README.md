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
## Service Callout

```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<ServiceCallout async="false" continueOnError="false" enabled="true" name="ServiceCalloutGeoLoc">
    <DisplayName>ServiceCalloutGeoLoc</DisplayName>
    <Properties/>
    <Request>
        <Set>
            <QueryParams>
                <QueryParam name="latlng">{lat},{long}</QueryParam>
                <QueryParam name="key">AIzaSyChgAv3onpLi5WN4NYioJh7ReUTkiwJmuo</QueryParam>
            </QueryParams>
        </Set>
    </Request>
    <Response>calloutResponse</Response>
    <HTTPTargetConnection>
        <Properties/>
        <URL>https://maps.googleapis.com/maps/api/geocode/json</URL>
    </HTTPTargetConnection>
</ServiceCallout>
```
