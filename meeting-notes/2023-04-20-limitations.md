# Sync meeting
## Information
**Date:** 2023-03-15
**Purpose:** Address some limitations

## Attendees
People who attended:
- [aquint-zama](https://github.com/aquint-zama)
- [haroune-mohammedi](https://github.com/haroune-mohammedi)

## Outcome
We encountered the following limitations during https://github.com/open-dust/TFHE-UBIRIS/pull/2
- Performance issues
- We can't compare the iris sent from the client with a previously encrypted database of irises because of a limitation in Concrete-Python, to better understand this see the snippet below
```python
# Those values can't be encrypted
data = [1, 2, 3]
data_length = 3

def f(x):
    for i in range(data_length):
        x = x + data[i]
    return x
```
- We can't compare the resulting score to a threshold to decide whether the iris is matched or not, yet alone returing the encrypted ID of the matching iris

To address theses, we agreed with @aquint-zama to keep the database of irises clear in the server for the moment and to return the score from the server and let another part of the system decide whether it's a match or miss.

@aquint-zama think it's more representative to have both challenge and DB encrypted, that could be solved by sending the db with the challenge as inputs arguments.

For the performance issues, @aquint-zama suggested we take a look at what others are doing to optimize bitwise operations but reassure performance isn't what matters for now since it is a known issue they are working on with hardware accelartion ... also, they have big AWS machines that could be used to speed things up
