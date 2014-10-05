counterwallet-create-enhanced-feed
==================================

# OBJECTIVES

A single-page wizard inside of Counterwallet that helps the user to create a binary feed using one of his 
Counterwallet addresses and update it as necessary.


# WORKFLOW, INPUTS AND OUTPUTS

The page initially presents a drop down list of user's addresses with non-zero balance in both BTC and XCP. 

Because only one feed can exist per address, upon selection:

a) If there is no feed at the adress, a Create Enhanced Feed form is presented

b) If there is feed at the address, an Edit Enhanced Feed form is presented

## FIELD VALUES / OPTIONS

- Feed address (a drop-down list; one of user's Counterwallet addresses that has non-zero balance in BTC and XCP)

- Type of bet (2 radio buttons ("binary" and "CfD"; at first this is to be locked to binary, while CfD is reserved 
for the future)

- Category (drop-down list; sports, politics, economics, entertainment, technology, other)

- Date/time picker is not necessary; date must be entered in format that does not require translation, 
that is "2014-07-01T05:06:07+00:00" (this is to keep it simple)

- The rest is as per [https://wiki.counterparty.io/w/Enhanced_Feed_Info_in_Counterwallet](https://wiki.counterparty.io/w/Enhanced_Feed_Info_in_Counterwallet)

## UPDATE
 
- The same fields can be displayed as in Created Enhanced Feed wizard, but updates can be made to only one field: `value` (to keep it simple)

# REFERENCE

0) Source code of interest
* https://github.com/CounterpartyXCP/counterwallet/blob/develop/src/js/components/betting.js
* https://github.com/CounterpartyXCP/counterwallet/blob/develop/src/pages/betting.html

1) How to test/develop

Install Federated Node, let it sync. 
http://counterpartyd-build.readthedocs.org/en/latest/SettingUpAFederatedNode.html#introduction

Modify/edit/create files as necessary:
http://support.counterparty.io/support/solutions/articles/5000049867-i-installed-federated-node-what

Create pull request against Counterwallet develop branch

2) Feed format

Source: https://wiki.counterparty.io/w/Enhanced_Feed_Info_in_Counterwallet


```
{
    "version": "1.0",
    "address": "muYJYjRZDPmTEMfyEGe34BGN8tZ6rmRZCu",
    "type": "binary",
    "category": "sports",
    "title": "Superbowl 2014",
    "image": "https://www.jahpowerbit.org/feeds/image-1.png",
    "description": "The feed for the Super Bowl final",
    "url": "http://www.jahpowerbit.org/superbowl2014",
    "broadcast_date": "2014-11-01T05:06:07+00:00",,
    "operator": {
        "name": "JahPowerBit",
        "image": "https://www.jahpowerbit.org/feeds/image-1.png",
        "description": "Development site",
        "url": "http://www.jahpowerbit.org"
    },
    "targets": [{
        "text": "The Bronco wins",
        "image": "https://www.jahpowerbit.org/feeds/image-1.png",
        "value": 1,
        "labels": {
            "equal": "yes",
            "not_equal": "no"
        },
        "odds": {
            "initial": 2,
            "suggested": 3
        },
        "deadline": "2014-07-01T05:06:07+00:00"
    }, {
        "text": "The Seahawks wins",
        "image": "https://www.jahpowerbit.org/feeds/image-1.png",
        "value": 2,
        "labels": {
            "equal": "yes",
            "not_equal": "no"
        },
        "deadline": "2014-07-01T05:06:07+00:00"
    }, {
        "text": "They draw",
        "image": "https://www.jahpowerbit.org/feeds/image-1.png",
        "value": 3,
        "labels": {
           "equal": "yes",
            "not_equal": "no"
        },
        "odds": {
            "initial": 3,
            "suggested": 4
        },
        "deadline": "2014-09-01T05:06:07+00:00"
    }],
    "customs": {
        "key1": "value1",
        "key2": 2
    }
}
```
