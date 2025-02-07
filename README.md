# Audit Conformance Labeler for Process Predictions
This repository is a fork from bptlab/bpic implementing conformance checking and data labeling in pandas for predictive process mining.


# Examples

## Import XES log as pandas DataFrame
Import XES event log as a pandas DataFrame:
```python
import conformancelabeler as clab
path_to_log = '<path_to_xes_file>'
log = clab.read_xes(path_to_log)
```

## Conformance Checking
Enabeling labeling for exact point of violation in the trace:

```python
rc = clab.conformance_checking.RuleChecker() 
print(rc.check_precedence(log, 'Record Goods Receipt', 'Clear Invoice', label=False))

```
``
Conformance checking via precedence rules of 'Clear Invoice' requiring 'Record Goods Receipt' with 5665 violations: 3.08% of all cases.
``

## Labeling of Incompliance and Position within Pandas DataFrame
Returns an extra column signalling incompliance and position of the violated rule.

```python
log = rc.check_precedence(log, 'Record Goods Receipt', 'Clear Invoice', 
label=True)
```

## Sequence Encoding
Labeling of the position of conformance violation. Prefix reduction reduces the trace one event before the incident.
```python
log = rc.check_precedence(log, 'Record Goods Receipt', 'Clear Invoice', label=True, prefix_reduction=True)


```
