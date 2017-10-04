# Capped Token Sale Audit Report by ConsenSys Diligence


<!--
Nothing should go into this file except maybe general COMMENTS, ROLES and this TODO list

TODOs:

* 

 -->

<!-- Please don't change these comments -->
<!-- MarkdownTOC -->
- [v0.0.1-ac.1](#v001-ac1)
	- [1 - Introduction](#1---introduction)
	- [2 - General Findings](#2---general-findings)
	- [3 - Specific Findings](#3---specific-findings)
	- [Appendix 1 - Audit Participants](#appendix-1---audit-participants)
	- [Appendix 2 - Terminology](#appendix-2---terminology)
	- [Appendix 3 - Codebase Details](#appendix-3---codebase-details)
<!--EP-->
<!-- /MarkdownTOC -->
<!-- Please don't change these comments -->

  
  
The codebase version under analysis in this section can be found at [https://github.com/GNSPS/simple-token-sale/releases/tag/v0.0.1-ac.1](https://github.com/GNSPS/simple-token-sale/releases/tag/v0.0.1-ac.1)


## v0.0.1-ac.1

### 1 - Introduction

#### 1.1 - Review Goals

The focus of this review was to ensure the following properties:

**Security**:
identifying security related issues within each
contract and within the system of contracts.

**Sound Architecture**:
evaluation of the architecture of this system through the lens of established smart contract best practices and general software best practices.

**Code Correctness and Quality**:
a full review of the contract source code.  The primary areas of focus include:

* Correctness (does it do was it is supposed to do)
* Readability (How easily it can be read and understood)
* Sections of code with high complexity
* Improving scalability
* Quantity and quality of test coverage


#### 1.2 - General Overview of Contract System

The codebase is comprised of two contracts: _Sale.sol_  and _Disbursement.sol_.


The first, _Sale.sol_ is the actual crowdsale contract. It runs as a single instance (gets deployed only once) and holds all the operational rules and parameters of the sale.

_Disbursement.sol_ on the other side is the contract ruling the vesting of offered tokens (to keep the right incentives in place and trustlessness alive). This one gets deployed multiple times (as much as the vestee number).

There is also an EthPM package being used which is an [ERC20, EIP610-compliant token from ConsenSys](https://github.com/ConsenSys/Tokens), these contracts are **outside** the scope of this review.


### 2 - General Findings

_General Findings_ would be comprised of the kind of issues found throughout a whole codebase. These would include bad practices and repeated mistakes.  
  
  
No general issues were found in this version of `simple-token-sale`.


### 3 - Specific Findings

#### 3.1 - Critical

No critical issues found.


#### 3.2 - Major

No major issues found.


#### 3.3 - Medium

##### 3.3.1 - `Disbursement.sol` missing check in constructor

The constructor function of the Disbursement.sol contract does not guarantee that the `owner` is not equal to `receiver` which would in turn let the vestee completely bypass the vesting schedule completely defeating the purpose of the timelock.

**Recommendation**

Change the initial conditions check in the constructor, adding:

`_receiver == msg.sender`

to [L54](https://github.com/GNSPS/simple-token-sale/blob/master/contracts/Disbursement.sol#L54) of the contract, turning the conditional check into:

`if (_receiver == 0 || _disbursementPeriod == 0 || _receiver == msg.sender)`



##### 3.3.2 - `Sale.sol` constructor is not enforcing chronological succession of events

The constructor function of the _Sale.sol_ contract does not guarantee that the end block effectively comes after the start block which in turn should always come before the freeze block.

**Recommendation**

Enforce chronological succession for the block state variables in the contract's constructor (`freezeBlock < startBlock && startBlock < endBlock`).



##### 3.3.3 - Pre-buyer and timelock tokens distribution should happen mandatorily before the sale starts

The disbursement of both the pre-buyers and timelocked vesting contracts should forcibly happen before the public sale starts or even better, before the freeze period.

**Recommendation**

Apply the `notFrozen()` modifier to the `distributePreBuyersRewards()` and the `distributeTimelockedTokens()` functions.


##### 3.3.4 - `purchaseTokens()` should not allow `msg.value == 0`

The disbursement of both the pre-buyers and timelocked vesting contracts should forcibly happen before the public sale starts or even better, before the freeze period.

**Recommendation**

Apply the `notFrozen()` modifier to the `distributePreBuyersRewards()` and the `distributeTimelockedTokens()` functions.


##### 3.3.5 - The `changeStartBlock()` function should make sure that the new block is smaller than the end block

The `changeStartBlock()` should require the new start block to be smaller than the current end block.

**Recommendation**

Add a requirement to the beggining of the function (or as a modifier) similar to:

`require(_newBlock < endBlock);`


#### 3.4 - Minor

##### 3.4.1 - Modifier `saleEnded()` and `saleNotEnded()` names are not accurate

The modifiers' names are not exactly representative of the conditions they enforce.

Their only checks are related to the end block, but the sale might end sooner by selling all the tokens before the end block.

The function `withdrawRemainder()` implements the `saleEnded()` modifier correctly (since there would be no remainder if the sale ended sooner).
The `purchaseTokens()` tokens function, on the other hand, does implement the `saleNotEnded()` modifier hence letting people still send requests even after there are no more tokens to sell.

**Recommendation**

Change `saleEnded` to `afterEndBlock`.

Add another check to `saleNotEnded()` making sure the sale contract's token balance is bigger than 0.


##### 3.4.2 - Modifier `notFrozen()` name is not accurate

The modifier name is not exactly representative of the conditions it enforces.

Like the `saleEnded()` and `saleNotEnded()` modifiers this one also doesn't have a name that is representative of the conditions it actually enforces. However it's design is well implemented in the several functions that use it so only a name change is in order.

Naming in a general use codebase like this is important for in future upgrades and changes a different developer might mistake this modifier's behaviour and introduce a new security hole inadvertently.

**Recommendation**

Change `notFrozen` to `beforeFreeze`.


##### 3.4.3 - Make sure `owner` is not also a vestee

In the `distributeTimelockedTokens()` function of the `Sale.sol` contract a check should exist to make sure that the `owner` account is not also a vestee in one of the disbursement contracts deployed.

**Recommendation**

Add a requirement to each iteration of the function's `for` loop:

`require(owner != beneficiary);`


### Appendix 1 - Audit Participants

Security audit was performed by ConsenSys Diligence.


### Appendix 2 - Terminology

#### A.2.1 - Severity

Measurement of magnitude of an issue.


##### A.2.1.1 - minor

Minor issues are generally subjective in nature, or potentially deal with
topics like "best practices" or "readability".  Minor issues in general will
not indicate an actual problem or bug in code.

The maintainers should use their own judgement as to whether addressing these
issues improves the codebase.


##### A.2.1.2 - medium

Medium issues are generally objective in nature but do not represent actual
bugs or security problems.

These issues should be addressed unless there is a clear reason not to.


##### A.2.1.3 - major

Major issues will be things like bugs or security vulnerabilities.  These
issues may not be directly exploitable, or may require a certain condition to
arise in order to be exploited.

Left unaddressed these issues are highly likely to cause problems with the
operation of the contract or lead to a situation which allows the system to be
exploited in some way.


##### A.2.1.4 - critical

Critical issues are directly exploitable bugs or security vulnerabilities.

Left unaddressed these issues are highly likely or guaranteed to cause major
problems or potentially a full failure in the operations of the contract.


### Appendix 3 - Codebase Details

#### A.3.1 - File List

The following source files were included in the audit.

https://github.com/GNSPS/simple-token-sale/releases/tag/v0.0.1-ac.1

* Disbursement.sol
* Sale.sol



#### A.3.2 - Static Analysis of Project's Files

##### A.4.2.1 - File Count

The number of solidity files present in the project is:

```
$ find . -name '*.sol' | wc -l

      11
```


##### A.4.2.2 - LOC Count

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


##### A.4.2.3 - External Call Count

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


#### A.3.3 - File Signatures

The SHA256 hash of each files at the time of the audit was as follows.

https://github.com/GNSPS/simple-token-sale/releases/tag/v0.0.1-ac.1

```
$ shasum -a 256 *

<output of the command>
```


