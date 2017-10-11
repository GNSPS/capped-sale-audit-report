# Summary


## v0.0.1-ac.1


### 1 - Introduction


* [1.1 - Review Goals](/report-contents/v0.0.1-ac.1/1 - Introduction/1.1 - Review Goals.md)


* [1.2 - General Overview of Contract System](/report-contents/v0.0.1-ac.1/1 - Introduction/1.2 - General Overview of Contract System.md)


### 2 - General Findings


* [](/report-contents/v0.0.1-ac.1/2 - General Findings/0 - no_title.md)


### 3 - Specific Findings


#### 3.1 - Critical


* [](/report-contents/v0.0.1-ac.1/3 - Specific Findings/3.1 - Critical/0 - no_title.md)


#### 3.2 - Major


* [](/report-contents/v0.0.1-ac.1/3 - Specific Findings/3.2 - Major/0 - no_title.md)


#### 3.3 - Medium


* [3.3.1 - `Disbursement.sol` missing check in constructor](/report-contents/v0.0.1-ac.1/3 - Specific Findings/3.3 - Medium/3.3.1 - `Disbursement.sol` missing check in constructor.md)


* [3.3.2 - `Sale.sol` constructor is not enforcing chronological succession of events](/report-contents/v0.0.1-ac.1/3 - Specific Findings/3.3 - Medium/3.3.2 - `Sale.sol` constructor is not enforcing chronological succession of events.md)


* [3.3.3 - Pre-buyer and timelock tokens distribution should happen mandatorily before the sale starts](/report-contents/v0.0.1-ac.1/3 - Specific Findings/3.3 - Medium/3.3.3 - Pre-buyer and timelock tokens distribution should happen mandatorily before the sale starts.md)


* [3.3.4 - `purchaseTokens()` should not allow `msg.value == 0`](/report-contents/v0.0.1-ac.1/3 - Specific Findings/3.3 - Medium/3.3.4 - `purchaseTokens()` should not allow `msg.value == 0`.md)


* [3.3.5 - The `changeStartBlock()` function should make sure that the new block is smaller than the end block](/report-contents/v0.0.1-ac.1/3 - Specific Findings/3.3 - Medium/3.3.5 - The `changeStartBlock()` function should make sure that the new block is smaller than the end block.md)


#### 3.4 - Minor


* [3.4.1 - Modifier `saleEnded()` and `saleNotEnded()` names are not accurate](/report-contents/v0.0.1-ac.1/3 - Specific Findings/3.4 - Minor/3.4.1 - Modifier `saleEnded()` and `saleNotEnded()` names are not accurate.md)


* [3.4.2 - Modifier `notFrozen()` name is not accurate](/report-contents/v0.0.1-ac.1/3 - Specific Findings/3.4 - Minor/3.4.2 - Modifier `notFrozen()` name is not accurate.md)


* [3.4.3 - Make sure `owner` is not also a vestee](/report-contents/v0.0.1-ac.1/3 - Specific Findings/3.4 - Minor/3.4.3 - Make sure `owner` is not also a vestee.md)


* [Appendix 1 - Audit Participants](/report-contents/v0.0.1-ac.1/Appendix 1 - Audit Participants.md)


### Appendix 2 - Terminology


#### A.2.1 - Severity


* [](/report-contents/v0.0.1-ac.1/Appendix 2 - Terminology/A.2.1 - Severity/0 - no_title.md)


* [A.2.1.1 - minor](/report-contents/v0.0.1-ac.1/Appendix 2 - Terminology/A.2.1 - Severity/A.2.1.1 - minor.md)


* [A.2.1.2 - medium](/report-contents/v0.0.1-ac.1/Appendix 2 - Terminology/A.2.1 - Severity/A.2.1.2 - medium.md)


* [A.2.1.3 - major](/report-contents/v0.0.1-ac.1/Appendix 2 - Terminology/A.2.1 - Severity/A.2.1.3 - major.md)


* [A.2.1.4 - critical](/report-contents/v0.0.1-ac.1/Appendix 2 - Terminology/A.2.1 - Severity/A.2.1.4 - critical.md)


### Appendix 3 - Codebase Details


* [A.3.1 - File List](/report-contents/v0.0.1-ac.1/Appendix 3 - Codebase Details/A.3.1 - File List.md)


#### A.3.2 - Static Analysis of Project's Files


* [A.4.2.1 - File Count](/report-contents/v0.0.1-ac.1/Appendix 3 - Codebase Details/A.3.2 - Static Analysis of Project's Files/A.4.2.1 - File Count.md)


* [A.4.2.2 - LOC Count](/report-contents/v0.0.1-ac.1/Appendix 3 - Codebase Details/A.3.2 - Static Analysis of Project's Files/A.4.2.2 - LOC Count.md)


* [A.4.2.3 - External Call Count](/report-contents/v0.0.1-ac.1/Appendix 3 - Codebase Details/A.3.2 - Static Analysis of Project's Files/A.4.2.3 - External Call Count.md)


* [A.3.3 - File Signatures](/report-contents/v0.0.1-ac.1/Appendix 3 - Codebase Details/A.3.3 - File Signatures.md)


