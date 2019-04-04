# Fault Handling

## AM Policy
```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<AssignMessage async="false" continueOnError="false" enabled="true" 
		name="QuotaViolation">
	<DisplayName>QuotaViolation</DisplayName>
	<FaultRules/>
	<Properties/>
	<Set>
		<Headers/>
		<Payload contentType="application/json">
			{"error":"Quota Violation. Too many requests."}
		</Payload>
		<StatusCode>429</StatusCode>
		<ReasonPhrase>Too Many Requests</ReasonPhrase>
	</Set>
	<IgnoreUnresolvedVariables>true</IgnoreUnresolvedVariables>
	<AssignTo createNew="false" transport="http" type="response"/>
</AssignMessage>

```
## Raise Failt

```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<RaiseFault async="false" continueOnError="false" enabled="true" name="RaiseFaultNotFound">
    <DisplayName>RaiseFaultNotFound</DisplayName>
    <Properties/>
    <FaultResponse>
        <Set>
            <Headers/>
            <Payload contentType="text/plain">
                   Method "{proxy.pathsuffix}" Not Found
            </Payload>
            <StatusCode>404</StatusCode>
    <ReasonPhrase>Not Found</ReasonPhrase>
        </Set>
    </FaultResponse>
    <IgnoreUnresolvedVariables>true</IgnoreUnresolvedVariables>
</RaiseFault>

```

## Fault rule

```
<FaultRules>
		<FaultRule name="QuotaViolation">
			<Condition>fault.name == "QuotaViolation"</Condition>
			<Step><Name>QuotaViolation</Name></Step>
		</FaultRule>
</FaultRules>

```

## Default Flow

```
<Flow name="default">
<Description/>
<Request>
<Step>
	<Name>RaiseFaultNotFound</Name>
</Step>
</Request>
<Response/>
</Flow>

```
