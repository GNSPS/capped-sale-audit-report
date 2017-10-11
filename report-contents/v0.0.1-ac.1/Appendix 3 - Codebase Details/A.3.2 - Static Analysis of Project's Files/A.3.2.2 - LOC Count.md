The number of LOC present in the project is:

```
$ find . -name '*.sol' | xargs wc -l

     104 ./contracts/Disbursement.sol
      23 ./contracts/Migrations.sol
     288 ./contracts/Sale.sol
      57 ./installed_contracts/tokens/contracts/HumanStandardToken.sol
      62 ./installed_contracts/tokens/contracts/HumanStandardTokenFactory.sol
      24 ./installed_contracts/tokens/contracts/Migrations.sol
      23 ./installed_contracts/tokens/contracts/SampleRecipientSuccess.sol
       8 ./installed_contracts/tokens/contracts/SampleRecipientThrow.sol
      54 ./installed_contracts/tokens/contracts/StandardToken.sol
      48 ./installed_contracts/tokens/contracts/Token.sol
      15 ./installed_contracts/tokens/contracts/TokenTester.sol
     706 total
```