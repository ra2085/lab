# Mashup

## Extract Variables

```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<ExtractVariables async="false" continueOnError="false" enabled="true" name="ExtractStoreAddress">
    <DisplayName>ExtractStoreAddress</DisplayName>
    <Properties/>
    <IgnoreUnresolvedVariables>true</IgnoreUnresolvedVariables>
    <JSONPayload>
        <Variable name="address">
            <JSONPath>$.results[0].formatted_address</JSONPath>
        </Variable>
    </JSONPayload>
    <Source clearPayload="false">calloutResponse.content</Source>
</ExtractVariables>
```
## JS

```
var address = context.getVariable('address');
var responsePayload = JSON.parse(context.getVariable('response.content'));
try{
    responsePayload.address = address;
    context.setVariable('response.content', JSON.stringify(responsePayload));
    context.setVariable('mashupAddressSuccess', true);

} catch(e){
    print('Error occurred when trying to add the address to the response.');
    context.setVariable('mashupAddressSuccess', false);
}
```
