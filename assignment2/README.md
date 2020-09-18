# Assignment 2

## Dependency

- [Requests](https://requests.readthedocs.io/en/master/)
- [Schedule](https://stackabuse.com/scheduling-jobs-with-python-crontab/)

## Requirements

You will be building low-code/no-code HTTP client application that supports these features:

* Outbound HTTP GET calls
* Handle logic based on the response as INPUT.
* Trigger OUTPUT event based on the logic.
* Scheduler to execute the steps.


### Scheduler 'when' Format

```
┌───────────── minute (0 - 59)
│ ┌───────────── hour (0 - 23) 
│ │ ┌───────────── day of month (1 - 31)
│ │ │ ┌───────────── month (1 - 12)
│ │ │ │ ┌───────────── day of week (0 - 6) (Sunday to Saturday;
│ │ │ │ │                                       7 is also Sunday on some systems)
│ │ │ │ │
│ │ │ │ │
* * * * * 
```


_Flow Syntax_

```yaml
Step:
 id: 1
 method: GET
 outbound_url: http://requestbin.com/
 condition:
  if: 
    equal:
    left: http.response.code
    right: 200
  then:
    action: print
    data: http.response.body
  else:
    action: print
    data: "Error"
    
Scheduler:
  when: "5 * * * *"
  step_id_to_execute: [ 1 ]
```

Save the flow in _input.yaml_

## How to execute Flow Http Client

```
python3 httpflow.py input.yaml
```

### Expected Output

```
Response body

OR

Error
```