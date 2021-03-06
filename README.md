counterwallet-create-enhanced-feed
==================================

## INSTALL

### Installing server (graphics client)

Now it is called the client in the same sense that the X11 (graphic system) in Unix.

[Using http://socket.io with Node http server](http://socket.io/docs/#)

    $ npm install http
    $ npm install socket.io
    $ npm install fs
    $ node app.js

In the test nodejs application we use port 8080

    app.listen(8080);
    
### Installing client (grapics server)
You can enter the command in the same directory, where to be index.html.
In the page index.html we have link to server code: https://cdn.socket.io/socket.io-1.1.0.js
    <script src="https://cdn.socket.io/socket.io-1.1.0.js"></script>
    
But possible shared from our CounterWallet node server or from servers (identification or authentication or keys or license) .

    <script src="/socket.io/socket.io-1.1.0.js"></script>

    
Port inside the index.html the same like in server

    <script>
        var socket = io('http://localhost:8080');
     ....
    </script>
    
For run client (grapics server) with port 8080 just open www/index.html in browser


## OBJECTIVE

A single-page wizard inside of Counterwallet that helps the user to create a binary feed using one of his 
Counterwallet addresses and update it as necessary.

Below is approximate description of how these features should work. It doesn't have to be done that way - anything that works and that project leaders accept is good.

## WORKFLOW, INPUTS AND OUTPUTS

NOTE: There already is a Create Feed feature in Counterwallet (see under Address Actions > Create Feed) but it does not create Enhanced Feed.

The page initially presents a drop down list of user's addresses with non-zero balance in both BTC and XCP. 

Because only one feed can exist per address, upon selection:

a) If there is no active feed at the adress, a Create Enhanced Feed form is presented

b) If there is an active feed at the address, an Edit Enhanced Feed form is presented

### INPUTS / OPTIONS

#### CREATE 

- Feed address (a drop-down list; one of user's Counterwallet addresses that has non-zero balance in BTC and XCP)

- Type of bet (2 radio buttons ("binary" and "CfD"; at first this is to be locked to binary, while CfD is reserved 
for the future)

- Category (drop-down list; sports, politics, economics, entertainment, technology, other)

- Date/time picker is not necessary; date must be entered in format that does not require translation, 
that is "2014-07-01T05:06:07+00:00" (this is to keep it simple)

- The rest is as per [https://wiki.counterparty.io/w/Enhanced_Feed_Info_in_Counterwallet](https://wiki.counterparty.io/w/Enhanced_Feed_Info_in_Counterwallet) (or scroll down to see a reference JSON file at the bottom)

- **NOTE**: In example below there are multiple `targets`. The first version of Create Feed Wizard only needs to be ablie to create a single target `text`.
 
#### UPDATE
 
- The same fields can be displayed as in Created Enhanced Feed wizard, but updates can be made to only one field: `value` (to keep it simple)

### OUTPUTS

Create Feed wizard creates a broadcasts and shows (at the bottom) a JSON file for it as per example at the bottom of this page.
Then it's up to the user to take care of the rest.

Update Feed wizard updates `value` and creates another broadcasts from the same wallet address which effectively updates the broadcast.

## QUESTIONS?

Questions related to this document should be posted under Issues for this repository.
Questions related to actual implementation and coding should be posted under:
[https://github.com/CounterpartyXCP/counterwallet/issues/449](https://github.com/CounterpartyXCP/counterwallet/issues/449)

## COMMITS

Create pull requests against https://github.com/CounterpartyXCP/counterwallet/tree/develop

## REFERENCE

0) Source code of interest
* https://github.com/CounterpartyXCP/counterwallet/blob/develop/src/js/components/betting.js
* https://github.com/CounterpartyXCP/counterwallet/blob/develop/src/pages/betting.html
* 

1) How to test/develop

- Install Federated Node, let it sync: 
http://counterpartyd-build.readthedocs.org/en/latest/SettingUpAFederatedNode.html#introduction

- Modify/edit/create files as necessary:
http://support.counterparty.io/support/solutions/articles/5000049867-i-installed-federated-node-what

Create a wallet and add required files. 

Create pull request against Counterwallet develop branch.

2) API

Some API commands that may come handy for creates and updates:

* `create_broadcast` (to create)
* `get_{table}` (e.g. `get_broadcasts` (to get a list of broadcasts))

See [https://github.com/CounterpartyXCP/counterpartyd/blob/master/docs/API.rst](https://github.com/CounterpartyXCP/counterpartyd/blob/master/docs/API.rst) for examples and additional details.

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
