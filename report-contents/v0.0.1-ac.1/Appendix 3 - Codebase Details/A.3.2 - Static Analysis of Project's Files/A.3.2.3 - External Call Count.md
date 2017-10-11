How many external calls are there in the project?

```
contracts/Disbursement.sol:89:        token.transfer(_to, _value);
contracts/Disbursement.sol:99:        uint maxTokens = (token.balanceOf(this) + withdrawnTokens) * (now - startDate) / disbursementPeriod;
contracts/Migrations.sol:21:    upgraded.setCompleted(last_completed_migration);
contracts/Sale.sol:116:        token.transfer(this, token.totalSupply());
contracts/Sale.sol:117:        assert(token.balanceOf(this) == token.totalSupply());
contracts/Sale.sol:118:        assert(token.balanceOf(this) == _tokenSupply);
contracts/Sale.sol:139:            token.transfer(_preBuyers[i], _preBuyersTokens[i]);
contracts/Sale.sol:179:          disbursement.setup(token);
contracts/Sale.sol:181:          token.transfer(disbursement, beneficiaryTokens);
contracts/Sale.sol:210:        require(purchaseAmount <= token.balanceOf(this));
contracts/Sale.sol:214:            msg.sender.transfer(excessAmount);
contracts/Sale.sol:218:        wallet.transfer(this.balance);
contracts/Sale.sol:221:        token.transfer(msg.sender, purchaseAmount);
contracts/Sale.sol:243:         uint remainder = token.balanceOf(this);
contracts/Sale.sol:244:         token.transfer(wallet, remainder);
```

NIX command used for the statistic:

```
egrep '\.\w*\(.*\)' contracts/* -nr
```