# EIP-0025: URI scheme for payment requests


> 🔗 From [EIP-0025](https://raw.githubusercontent.com/ergoplatform/eips/master/eip-0025.md)


* Author: MrStahlfelge
* Created: 14-Dec-2021
* License: CC0
* Forking: not needed

Motivation
----------

Like [BIP-0021](https://github.com/bitcoin/bips/blob/master/bip-0021.mediawiki) for Bitcoin, this EIP proposes a URI scheme for initiating payments.

The purpose of this URI scheme is to enable users to easily make payments by simply clicking links on webpages or in e-mails.

In difference to Ergo Pay (EIP-0020), this URI scheme does not contain a prepared transaction that the wallet should sign or discard. Instead, it contains 
the data that the wallet application should use to fill its payment form. The user can change the details when needed. The wallet will build the transaction, 
so this scheme is easier to handle on static websites or in e-mails.


Format
------

    ergourn        = "ergo:" ergoaddress [ "?" ergoparams ]
    ergoaddress    = *base58
    ergoparams     = ergoparam [ "&" ergoparams ]
    ergoparam      = [ amountparam / labelparam / messageparam / tokenparam ]
    amountparam    = "amount=" *digit [ "." *digit ]
    labelparam     = "label=" *qchar
    messageparam   = "description=" *qchar
    tokenparam     = "token-" qchar *qchar "=" *digit [ "." *digit ]


* label: Label for that address (e.g. name of receiver)
* address: ergo P2PK or P2S address
* description: message that describes the transaction to the user
 
### Amount

If an amount is provided, it MUST be specified in decimal ERG. All amounts MUST contain no commas and use a period (.) as the separating character to separate 
whole numbers and decimal fractions. I.e. amount=50.00 or amount=50 is treated as 50 ERG, and amount=50,000.00 is invalid.

### Tokens

If a token parameter is provided, it specifies the token id and the desired amount separated by an equals sign. The amount must be specified in decimal token 
value, for example "3.45" for 3.45 SigUSD. The amount MUST contain no commas and use a period (.) as the separating character to separate whole numbers and decimal fractions.


Examples
--------

     ergoplatform:9ewA9T53dy5qvAkcR5jVCtbaDW2XgWzbLPs5H4uCJJavmA4fzDx

     ergoplatform:9ewA9T53dy5qvAkcR5jVCtbaDW2XgWzbLPs5H4uCJJavmA4fzDx?amount=1.0&description=Hard%20work
requests 1 ERG for hard work

     ergoplatform:9ewA9T53dy5qvAkcR5jVCtbaDW2XgWzbLPs5H4uCJJavmA4fzDx?token-03faf2cb329f2e90d6d23b58d91bbb6c046aa143261cc21f52fbe2824bfcbf04=5
requests 5 SigUSD

In the case of sending token only, a minimum amount of ERGs MUST also be sent to a new box (it is not possible to create boxes containing tokens only with zero ERGs).

The wallet should process the URI as long as it can parse and interpret the content unambiguously. Any ambiguity should be detected and if it cannot be resolved, the wallet should give a descriptive message to the user (not just "Invalid URI", but what exactly has been detected as invalid).

At the same time the wallet should not do anything implicitly, even if it is smart enough to so some implicit actions, it should display what is going on to the user on the transaction sending screen. The user should be aware that some implicit action where taken by wallet and that those actions will take effect when the Send button is pressed.

Applying the above principles to the missing ERGs amount parameter problem we can see that it can be automatically resolved by the wallet, so the wallet shouldn't reject the URI as invalid when the amount of ERGs is missing. At the same time, the screen should have an explanation that non-zero amount of ERGs in the field is required and that it was suggested by the wallet.

For the case of duplicate tokens, the wallet CAN consider such URI as invalid, and clearly communicate the problem to the user so that the user can take a screenshot and send it back to the dApp developer. The duplication problem should be clear from the screenshot.