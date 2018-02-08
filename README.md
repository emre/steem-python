# Fork of Python STEEM Library

`steem-python` is the official STEEM library for Python. Due to inactivity and lack of response to pull requests in the official repo, I will maintain a seperate fork.


## Installation
You can install `steem-python-dshot` with `pip`:

```
pip install -U steem_dshot
```
## Differences

### Beneficiaries

Removed all beneficiary helpers and syntactic sugar around it. It wasn't working anyway. 
It still supports extensions. So you can set beneficiaries like this:

```python
from steem import Steem

s = Steem(keys=["posting_wif"])

comment_options = {
    "extensions": [[0, {
        'beneficiaries': [
            {'account': 'crokkon', 'weight': 1000},
            {'account': 'emrebeyler', 'weight': 5000},
        ]}]]
}

s.commit.post(
    title='my title',
    body="my body",
    author='post_author',
    tags=['test'],
    comment_options=comment_options,
)
```


### Change of default node

Default node is jussi (api.steemit.com) now instead of the deprecated steemd.steemit.com.

### Current voting Power

Account class has a new helper method to get current voting power. It also takes into account the regenerated
VP after the last vote cast.

```python
from steem.account import Account
print(Account('emrebeyler').current_voting_power())
```

### Propagation of custom steemd instance to internal constructors 

Account, Post, Blockchain, Converter, Block classes now obeys the custom node selection. (credits to [@crokkon](https://steemit.com/@crokkon))

### Fix custom node selection on steempy CLI.

The steempy cli ignored the setting from the --node command line option and always used the default node due to a parameter name mismatch/typo on the Steem()
constructor parameters.  (credits to [@crokkon](https://steemit.com/@crokkon))

### Fix the version of TOML in dependencies.

Package should be installed in any environment without hassle.

### Fix reputation calculation

Reputation calculation is aligned with the condenser. 

```python
from steem.account import Account

print(Account('emrebeyler').rep)
```

### Implement DeleteComment operation.

delete_comment now has a high-level abstraction in **operations.py**. 

## Documentation
Documentation of the main package is available at **http://steem.readthedocs.io**
