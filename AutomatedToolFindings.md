Summary
 - [arbitrary-send-erc20](#arbitrary-send-erc20) (1 results) (High)
 - [unchecked-transfer](#unchecked-transfer) (3 results) (High)
 - [constant-function-asm](#constant-function-asm) (5 results) (Medium)
 - [erc20-interface](#erc20-interface) (2 results) (Medium)
 - [incorrect-equality](#incorrect-equality) (2 results) (Medium)
 - [reentrancy-no-eth](#reentrancy-no-eth) (2 results) (Medium)
 - [unused-return](#unused-return) (1 results) (Medium)
 - [reentrancy-benign](#reentrancy-benign) (6 results) (Low)
 - [reentrancy-events](#reentrancy-events) (7 results) (Low)
 - [assembly](#assembly) (8 results) (Informational)
 - [dead-code](#dead-code) (14 results) (Informational)
 - [solc-version](#solc-version) (42 results) (Informational)
 - [naming-convention](#naming-convention) (100 results) (Informational)
 - [similar-names](#similar-names) (11 results) (Informational)
 - [unused-state](#unused-state) (3 results) (Informational)
## arbitrary-send-erc20
Impact: High
Confidence: High
 - [ ] ID-0
[SafeERC20.safeTransferFrom(address,address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L38-L48) uses arbitrary from in transferFrom: [LegacyERC20(_token).transferFrom(_from,address(this),_value)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L39)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L38-L48

### Recommendation
	
	Use msg.sender in `transferFrom`

## unchecked-transfer
Impact: High
Confidence: Medium
 - [ ] ID-1
[InterestConnector._transferInterest(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L182-L193) ignores return value by [ERC20(_token).transfer(receiver,_amount)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L186)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L182-L193


 - [ ] ID-2
[ForeignBridgeErcToNative.relayTokens(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L64-L75) ignores return value by [erc20token().transferFrom(msg.sender,address(this),_amount)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L73)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L64-L75


 - [ ] ID-3
[ERC20Bridge.relayTokens(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L19-L28) ignores return value by [erc20token().transferFrom(msg.sender,address(this),_amount)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L26)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L19-L28

### Recommendation

	Use SafeERC20, or ensure that the transfer/transferFrom return value is checked.


## constant-function-asm
Impact: Medium
Confidence: Medium
 - [ ] ID-4
[Message.recoverAddressFromSignedMessage(bytes,bytes,bool)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L51-L70) is declared view but contains assembly code

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L51-L70


 - [ ] ID-5
[BaseRelayRecipient._msgSender()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L18-L29) is declared view but contains assembly code

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L18-L29


 - [ ] ID-6
[Message.hasEnoughValidSignatures(bytes,bytes,IBridgeValidators,bool)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L95-L128) is declared view but contains assembly code

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L95-L128


 - [ ] ID-7
[Message.parseMessage(bytes)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L29-L41) is declared view but contains assembly code

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L29-L41


 - [ ] ID-8
[BaseRelayRecipient._msgData()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L39-L56) is declared view but contains assembly code

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L39-L56

### Recommendation

	Ensure the attributes of contracts compiled prior to Solidity 0.5.0, are correct.

## erc20-interface
Impact: Medium
Confidence: High
 - [ ] ID-9
[LegacyERC20](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/ERC677.sol#L13-L16) has incorrect ERC20 function interface:[LegacyERC20.transferFrom(address,address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/ERC677.sol#L15)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/ERC677.sol#L13-L16


 - [ ] ID-10
[LegacyERC20](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/ERC677.sol#L13-L16) has incorrect ERC20 function interface:[LegacyERC20.transfer(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/ERC677.sol#L14)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/ERC677.sol#L13-L16

### Recommendation

	Set the appropriate return values and types for the defined ERC20 functions.

## incorrect-equality
Impact: Medium
Confidence: High
 - [ ] ID-11
[InterestConnector._withdraw(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L219-L226) uses a dangerous strict equality:
	- [withdrawal == 0](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L222)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L219-L226


 - [ ] ID-12
[DecimalShiftBridge._shiftUint(uint256,int256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L55-L63) uses a dangerous strict equality:
	- [_shift == 0](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L56)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L55-L63

### Recommendation

	Don't use strict equality to determine if an account has enough Ether or tokens.


## reentrancy-no-eth
Impact: Medium
Confidence: Medium
 - [ ] ID-13
Reentrancy in [InterestConnector._withdraw(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L219-L226):
	
	External calls:
	- [redeemed = _safeWithdrawTokens(_token,withdrawal)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L223)
		- [ERC20(_token).balanceOf(address(this))](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L281)
	
	State variables written after the call(s):
	- [_setInvestedAmount(_token,invested - redeemed)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L225)
		- [uintStorage[keccak256()(abi.encodePacked(investedAmount,_token))] = _amount](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L210)
	[EternalStorage.uintStorage](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeability/EternalStorage.sol#L8) can be used in cross function reentrancies:
	- [BasicBridge._setGasPrice(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L57-L60)
	- [InterestConnector._setInvestedAmount(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L209-L211)
	- [InterestConnector._setMinCashThreshold(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L252-L254)
	- [InterestConnector._setMinInterestPaid(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L261-L263)
	- [BasicBridge._setRequiredBlockConfirmations(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L43-L47)
	- [BasicTokenBridge.addTotalSpentPerDay(uint256,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L62-L64)
	- [BasicTokenBridge.dailyLimit()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L28-L30)
	- [DecimalShiftBridge.decimalShift()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L27-L29)
	- [InitializableBridge.deployedAtBlock()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/InitializableBridge.sol#L8-L10)
	- [BasicTokenBridge.executionDailyLimit()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L32-L34)
	- [BasicTokenBridge.executionMaxPerTx()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L40-L42)
	- [BasicBridge.gasPrice()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L35-L37)
	- [InterestConnector.investedAmount(address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L155-L157)
	- [BasicTokenBridge.maxPerTx()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L36-L38)
	- [InterestConnector.minCashThreshold(address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L80-L82)
	- [InterestConnector.minInterestPaid(address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L99-L101)
	- [BasicTokenBridge.minPerTx()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L44-L46)
	- [BasicBridge.requiredBlockConfirmations()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L49-L51)
	- [BasicTokenBridge.setDailyLimit(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L70-L74)
	- [BasicTokenBridge.setExecutionDailyLimit(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L76-L80)
	- [BasicTokenBridge.setExecutionMaxPerTx(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L82-L85)
	- [BasicTokenBridge.setMaxPerTx(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L87-L90)
	- [BasicTokenBridge.setMinPerTx(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L92-L95)
	- [BasicTokenBridge.totalExecutedPerDay(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L24-L26)
	- [BasicTokenBridge.totalSpentPerDay(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L20-L22)
	- [_setInvestedAmount(_token,0)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L225)
		- [uintStorage[keccak256()(abi.encodePacked(investedAmount,_token))] = _amount](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L210)
	[EternalStorage.uintStorage](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeability/EternalStorage.sol#L8) can be used in cross function reentrancies:
	- [BasicBridge._setGasPrice(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L57-L60)
	- [InterestConnector._setInvestedAmount(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L209-L211)
	- [InterestConnector._setMinCashThreshold(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L252-L254)
	- [InterestConnector._setMinInterestPaid(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L261-L263)
	- [BasicBridge._setRequiredBlockConfirmations(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L43-L47)
	- [BasicTokenBridge.addTotalSpentPerDay(uint256,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L62-L64)
	- [BasicTokenBridge.dailyLimit()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L28-L30)
	- [DecimalShiftBridge.decimalShift()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L27-L29)
	- [InitializableBridge.deployedAtBlock()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/InitializableBridge.sol#L8-L10)
	- [BasicTokenBridge.executionDailyLimit()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L32-L34)
	- [BasicTokenBridge.executionMaxPerTx()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L40-L42)
	- [BasicBridge.gasPrice()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L35-L37)
	- [InterestConnector.investedAmount(address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L155-L157)
	- [BasicTokenBridge.maxPerTx()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L36-L38)
	- [InterestConnector.minCashThreshold(address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L80-L82)
	- [InterestConnector.minInterestPaid(address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L99-L101)
	- [BasicTokenBridge.minPerTx()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L44-L46)
	- [BasicBridge.requiredBlockConfirmations()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L49-L51)
	- [BasicTokenBridge.setDailyLimit(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L70-L74)
	- [BasicTokenBridge.setExecutionDailyLimit(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L76-L80)
	- [BasicTokenBridge.setExecutionMaxPerTx(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L82-L85)
	- [BasicTokenBridge.setMaxPerTx(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L87-L90)
	- [BasicTokenBridge.setMinPerTx(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L92-L95)
	- [BasicTokenBridge.totalExecutedPerDay(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L24-L26)
	- [BasicTokenBridge.totalSpentPerDay(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L20-L22)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L219-L226


 - [ ] ID-14
Reentrancy in [XDaiForeignBridge.onExecuteMessageGSN(address,uint256,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L85-L89):
	
	External calls:
	- [ensureEnoughTokens(daiToken(),amount)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L86)
		- [currentBalance = token.balanceOf(address(this))](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L92)
		- [ERC20(_token).balanceOf(address(this))](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L281)
		- [require(bool,string)(sDaiToken().withdraw(_amount,address(this),address(this)) > 0,Failed to withdraw)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/SavingsDaiConnector.sol#L69)
	- [super.onExecuteMessageGSN(recipient,amount,fee)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L88)
		- [first = token.transfer(addressStorage[PAYMASTER],fee)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L64)
		- [second = token.transfer(recipient,amount - fee)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L65)
	
	State variables written after the call(s):
	- [super.onExecuteMessageGSN(recipient,amount,fee)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L88)
		- [uintStorage[keccak256()(abi.encodePacked(totalExecutedPerDay,_day))] = totalExecutedPerDay(_day).add(_value)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L67)
	[EternalStorage.uintStorage](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeability/EternalStorage.sol#L8) can be used in cross function reentrancies:
	- [BasicTokenBridge._setExecutionLimits(uint256[2])](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L123-L130)
	- [BasicBridge._setGasPrice(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L57-L60)
	- [InterestConnector._setInvestedAmount(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L209-L211)
	- [BasicTokenBridge._setLimits(uint256[3])](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L109-L121)
	- [InterestConnector._setMinCashThreshold(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L252-L254)
	- [InterestConnector._setMinInterestPaid(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L261-L263)
	- [BasicBridge._setRequiredBlockConfirmations(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L43-L47)
	- [BasicTokenBridge.addTotalExecutedPerDay(uint256,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L66-L68)
	- [BasicTokenBridge.addTotalSpentPerDay(uint256,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L62-L64)
	- [BasicTokenBridge.dailyLimit()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L28-L30)
	- [DecimalShiftBridge.decimalShift()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L27-L29)
	- [InitializableBridge.deployedAtBlock()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/InitializableBridge.sol#L8-L10)
	- [BasicTokenBridge.executionDailyLimit()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L32-L34)
	- [BasicTokenBridge.executionMaxPerTx()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L40-L42)
	- [BasicBridge.gasPrice()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L35-L37)
	- [XDaiForeignBridge.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L8-L35)
	- [InterestConnector.investedAmount(address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L155-L157)
	- [BasicTokenBridge.maxPerTx()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L36-L38)
	- [InterestConnector.minCashThreshold(address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L80-L82)
	- [InterestConnector.minInterestPaid(address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L99-L101)
	- [BasicTokenBridge.minPerTx()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L44-L46)
	- [BasicBridge.requiredBlockConfirmations()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L49-L51)
	- [BasicTokenBridge.setDailyLimit(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L70-L74)
	- [BasicTokenBridge.setExecutionDailyLimit(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L76-L80)
	- [BasicTokenBridge.setExecutionMaxPerTx(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L82-L85)
	- [BasicTokenBridge.setMaxPerTx(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L87-L90)
	- [BasicTokenBridge.setMinPerTx(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L92-L95)
	- [BasicTokenBridge.totalExecutedPerDay(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L24-L26)
	- [BasicTokenBridge.totalSpentPerDay(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L20-L22)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L85-L89

### Recommendation

Apply the [`check-effects-interactions` pattern](http://solidity.readthedocs.io/en/v0.4.21/security-considerations.html#re-entrancy).


## unused-return
Impact: Medium
Confidence: Medium
 - [ ] ID-15
[SavingsDaiConnector._invest(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/SavingsDaiConnector.sol#L55-L59) ignores return value by [daiToken().approve(address(sDaiToken()),_amount)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/SavingsDaiConnector.sol#L57)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/SavingsDaiConnector.sol#L55-L59

### Recommendation

Ensure that all the return values of the function calls are used.

## reentrancy-benign
Impact: Low
Confidence: Medium
 - [ ] ID-16
Reentrancy in [InterestConnector.invest(address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L164-L174):
	
	External calls:
	- [balance = _selfBalance(_token)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L165)
		- [ERC20(_token).balanceOf(address(this))](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L281)
	
	State variables written after the call(s):
	- [_setInvestedAmount(_token,investedAmount(_token).add(amount))](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L171)
		- [uintStorage[keccak256()(abi.encodePacked(investedAmount,_token))] = _amount](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L210)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L164-L174


 - [ ] ID-17
Reentrancy in [ForeignBridgeErcToNative.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L7-L34):
	
	External calls:
	- [onlyRelevantSender()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L17)
		- [require(bool)(! address(this).call(abi.encodeWithSelector(UPGRADEABILITY_OWNER)) || msg.sender == IUpgradeabilityOwnerStorage(this).upgradeabilityOwner() || msg.sender == address(this))](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Ownable.sol#L34-L38)
	
	State variables written after the call(s):
	- [addressStorage[VALIDATOR_CONTRACT] = _validatorContract](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L21)
	- [setErc20token(_erc20token)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L22)
		- [addressStorage[ERC20_TOKEN] = _token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L16)
	- [_setOwner(_owner)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L29)
		- [addressStorage[OWNER] = newOwner](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Ownable.sol#L67)
	- [_setBridgeContractOnOtherSide(_bridgeOnOtherSide)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L30)
		- [addressStorage[BRIDGE_CONTRACT] = _bridgeContract](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/OtherSideBridgeStorage.sol#L10)
	- [setInitialize()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L31)
		- [boolStorage[INITIALIZED] = true](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Initializable.sol#L9)
	- [uintStorage[DEPLOYED_AT_BLOCK] = block.number](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L23)
	- [_setRequiredBlockConfirmations(_requiredBlockConfirmations)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L24)
		- [uintStorage[REQUIRED_BLOCK_CONFIRMATIONS] = _blockConfirmations](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L45)
	- [_setGasPrice(_gasPrice)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L25)
		- [uintStorage[GAS_PRICE] = _gasPrice](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L58)
	- [_setLimits(_dailyLimitMaxPerTxMinPerTxArray)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L26)
		- [uintStorage[DAILY_LIMIT] = _limits[0]](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L116)
		- [uintStorage[MAX_PER_TX] = _limits[1]](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L117)
		- [uintStorage[MIN_PER_TX] = _limits[2]](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L118)
	- [_setExecutionLimits(_homeDailyLimitHomeMaxPerTxArray)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L27)
		- [uintStorage[EXECUTION_DAILY_LIMIT] = _limits[0]](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L126)
		- [uintStorage[EXECUTION_MAX_PER_TX] = _limits[1]](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L127)
	- [_setDecimalShift(_decimalShift)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L28)
		- [uintStorage[DECIMAL_SHIFT] = uint256(_shift)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L20)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L7-L34


 - [ ] ID-18
Reentrancy in [XDaiForeignBridge.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L8-L35):
	
	External calls:
	- [onlyRelevantSender()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L18)
		- [require(bool)(! address(this).call(abi.encodeWithSelector(UPGRADEABILITY_OWNER)) || msg.sender == IUpgradeabilityOwnerStorage(this).upgradeabilityOwner() || msg.sender == address(this))](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Ownable.sol#L34-L38)
	
	State variables written after the call(s):
	- [addressStorage[VALIDATOR_CONTRACT] = _validatorContract](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L24)
	- [_setOwner(_owner)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L30)
		- [addressStorage[OWNER] = newOwner](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Ownable.sol#L67)
	- [_setBridgeContractOnOtherSide(_bridgeOnOtherSide)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L31)
		- [addressStorage[BRIDGE_CONTRACT] = _bridgeContract](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/OtherSideBridgeStorage.sol#L10)
	- [setInitialize()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L32)
		- [boolStorage[INITIALIZED] = true](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Initializable.sol#L9)
	- [uintStorage[DEPLOYED_AT_BLOCK] = block.number](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L25)
	- [_setRequiredBlockConfirmations(_requiredBlockConfirmations)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L26)
		- [uintStorage[REQUIRED_BLOCK_CONFIRMATIONS] = _blockConfirmations](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L45)
	- [_setGasPrice(_gasPrice)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L27)
		- [uintStorage[GAS_PRICE] = _gasPrice](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L58)
	- [_setLimits(_dailyLimitMaxPerTxMinPerTxArray)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L28)
		- [uintStorage[DAILY_LIMIT] = _limits[0]](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L116)
		- [uintStorage[MAX_PER_TX] = _limits[1]](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L117)
		- [uintStorage[MIN_PER_TX] = _limits[2]](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L118)
	- [_setExecutionLimits(_homeDailyLimitHomeMaxPerTxArray)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L29)
		- [uintStorage[EXECUTION_DAILY_LIMIT] = _limits[0]](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L126)
		- [uintStorage[EXECUTION_MAX_PER_TX] = _limits[1]](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L127)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L8-L35


 - [ ] ID-19
Reentrancy in [BasicForeignBridge.executeSignatures(bytes,bytes)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicForeignBridge.sol#L22-L39):
	
	External calls:
	- [Message.hasEnoughValidSignatures(message,signatures,validatorContract(),false)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicForeignBridge.sol#L23)
	
	State variables written after the call(s):
	- [setRelayedMessages(txHash,true)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicForeignBridge.sol#L33)
		- [boolStorage[keccak256()(abi.encodePacked(relayedMessages,_txHash))] = _status](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/MessageRelay.sol#L11)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicForeignBridge.sol#L22-L39


 - [ ] ID-20
Reentrancy in [GSNForeignERC20Bridge.executeSignaturesGSN(bytes,bytes,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L38-L58):
	
	External calls:
	- [Message.hasEnoughValidSignatures(message,signatures,validatorContract(),false)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L41)
	
	State variables written after the call(s):
	- [setRelayedMessages(txHash,true)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L52)
		- [boolStorage[keccak256()(abi.encodePacked(relayedMessages,_txHash))] = _status](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/MessageRelay.sol#L11)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L38-L58


 - [ ] ID-21
Reentrancy in [InterestConnector.disableInterest(address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L108-L111):
	
	External calls:
	- [_withdraw(_token,uint256(- 1))](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L109)
		- [ERC20(_token).balanceOf(address(this))](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L281)
	
	State variables written after the call(s):
	- [_setInterestEnabled(_token,false)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L110)
		- [boolStorage[keccak256()(abi.encodePacked(interestEnabled,_token))] = _enabled](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L201)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L108-L111

### Recommendation

Apply the [`check-effects-interactions` pattern](http://solidity.readthedocs.io/en/v0.4.21/security-considerations.html#re-entrancy).

## reentrancy-events
Impact: Low
Confidence: Medium
 - [ ] ID-22
Reentrancy in [ForeignBridgeErcToNative.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L7-L34):
	
	External calls:
	- [onlyRelevantSender()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L17)
		- [require(bool)(! address(this).call(abi.encodeWithSelector(UPGRADEABILITY_OWNER)) || msg.sender == IUpgradeabilityOwnerStorage(this).upgradeabilityOwner() || msg.sender == address(this))](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Ownable.sol#L34-L38)
	
	Event emitted after the call(s):
	- [DailyLimitChanged(_limits[0])](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L120)
		- [_setLimits(_dailyLimitMaxPerTxMinPerTxArray)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L26)
	- [ExecutionDailyLimitChanged(_limits[0])](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L129)
		- [_setExecutionLimits(_homeDailyLimitHomeMaxPerTxArray)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L27)
	- [GasPriceChanged(_gasPrice)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L59)
		- [_setGasPrice(_gasPrice)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L25)
	- [OwnershipTransferred(owner(),newOwner)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Ownable.sol#L66)
		- [_setOwner(_owner)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L29)
	- [RequiredBlockConfirmationChanged(_blockConfirmations)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L46)
		- [_setRequiredBlockConfirmations(_requiredBlockConfirmations)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L24)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L7-L34


 - [ ] ID-23
Reentrancy in [GSNForeignERC20Bridge.executeSignaturesGSN(bytes,bytes,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L38-L58):
	
	External calls:
	- [Message.hasEnoughValidSignatures(message,signatures,validatorContract(),false)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L41)
	- [require(bool)(onExecuteMessageGSN(recipient,amount,maxTokensFee))](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L53)
		- [first = token.transfer(addressStorage[PAYMASTER],fee)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L64)
		- [second = token.transfer(recipient,amount - fee)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L65)
	
	Event emitted after the call(s):
	- [RelayedMessage(recipient,amount,txHash)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L54)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L38-L58


 - [ ] ID-24
Reentrancy in [BasicForeignBridge.executeSignatures(bytes,bytes)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicForeignBridge.sol#L22-L39):
	
	External calls:
	- [Message.hasEnoughValidSignatures(message,signatures,validatorContract(),false)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicForeignBridge.sol#L23)
	
	Event emitted after the call(s):
	- [RelayedMessage(recipient,amount,txHash)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicForeignBridge.sol#L35)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicForeignBridge.sol#L22-L39


 - [ ] ID-25
Reentrancy in [InterestConnector._transferInterest(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L182-L193):
	
	External calls:
	- [ERC20(_token).transfer(receiver,_amount)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L186)
	- [IInterestReceiver(receiver).onInterestReceived(_token)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L189)
	
	Event emitted after the call(s):
	- [PaidInterest(_token,receiver,_amount)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L192)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L182-L193


 - [ ] ID-26
Reentrancy in [ERC20Bridge.relayTokens(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L19-L28):
	
	External calls:
	- [erc20token().transferFrom(msg.sender,address(this),_amount)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L26)
	
	Event emitted after the call(s):
	- [UserRequestForAffirmation(_receiver,_amount)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L27)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L19-L28


 - [ ] ID-27
Reentrancy in [XDaiForeignBridge.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L8-L35):
	
	External calls:
	- [onlyRelevantSender()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L18)
		- [require(bool)(! address(this).call(abi.encodeWithSelector(UPGRADEABILITY_OWNER)) || msg.sender == IUpgradeabilityOwnerStorage(this).upgradeabilityOwner() || msg.sender == address(this))](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Ownable.sol#L34-L38)
	
	Event emitted after the call(s):
	- [DailyLimitChanged(_limits[0])](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L120)
		- [_setLimits(_dailyLimitMaxPerTxMinPerTxArray)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L28)
	- [ExecutionDailyLimitChanged(_limits[0])](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L129)
		- [_setExecutionLimits(_homeDailyLimitHomeMaxPerTxArray)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L29)
	- [GasPriceChanged(_gasPrice)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L59)
		- [_setGasPrice(_gasPrice)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L27)
	- [OwnershipTransferred(owner(),newOwner)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Ownable.sol#L66)
		- [_setOwner(_owner)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L30)
	- [RequiredBlockConfirmationChanged(_blockConfirmations)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L46)
		- [_setRequiredBlockConfirmations(_requiredBlockConfirmations)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L26)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L8-L35


 - [ ] ID-28
Reentrancy in [ForeignBridgeErcToNative.relayTokens(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L64-L75):
	
	External calls:
	- [erc20token().transferFrom(msg.sender,address(this),_amount)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L73)
	
	Event emitted after the call(s):
	- [UserRequestForAffirmation(_receiver,_amount)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L74)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L64-L75

### Recommendation

Apply the [`check-effects-interactions` pattern](http://solidity.readthedocs.io/en/v0.4.21/security-considerations.html#re-entrancy).


## assembly
Impact: Informational
Confidence: High
 - [ ] ID-29
[Message.parseMessage(bytes)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L29-L41) uses assembly
	- [INLINE ASM](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L35-L41)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L29-L41


 - [ ] ID-30
[BaseRelayRecipient._msgData()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L39-L56) uses assembly
	- [INLINE ASM](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L43-L53)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L39-L56


 - [ ] ID-31
[Message.recoverAddressFromSignedMessage(bytes,bytes,bool)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L51-L70) uses assembly
	- [INLINE ASM](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L61-L66)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L51-L70


 - [ ] ID-32
[SafeERC20.safeTransfer(address,address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L20-L30) uses assembly
	- [INLINE ASM](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L22-L30)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L20-L30


 - [ ] ID-33
[BaseRelayRecipient._msgSender()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L18-L29) uses assembly
	- [INLINE ASM](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L23-L26)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L18-L29


 - [ ] ID-34
[Message.hasEnoughValidSignatures(bytes,bytes,IBridgeValidators,bool)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L95-L128) uses assembly
	- [INLINE ASM](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L104-L107)
	- [INLINE ASM](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L117-L123)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L95-L128


 - [ ] ID-35
[AddressUtils.isContract(address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/AddressUtils.sol#L16-L27) uses assembly
	- [INLINE ASM](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/AddressUtils.sol#L25-L26)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/AddressUtils.sol#L16-L27


 - [ ] ID-36
[SafeERC20.safeTransferFrom(address,address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L38-L48) uses assembly
	- [INLINE ASM](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L40-L48)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L38-L48

### Recommendation

	Do not use evm assembly. Use if and only if it is required and can't be managed otherwise.

## dead-code
Impact: Informational
Confidence: Medium
 - [ ] ID-37
[SafeMath.mul(uint256,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L13-L24) is never used and should be removed

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L13-L24


 - [ ] ID-38
[SafeMath.sub(uint256,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L39-L42) is never used and should be removed

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L39-L42


 - [ ] ID-39
[BaseRelayRecipient._msgSender()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L18-L29) is never used and should be removed

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L18-L29


 - [ ] ID-40
[InterestConnector._transferInterest(address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L182-L193) is never used and should be removed

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L182-L193


 - [ ] ID-41
[DecimalShiftBridge._unshiftValue(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L36-L38) is never used and should be removed

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L36-L38


 - [ ] ID-42
[SafeERC20.safeTransferFrom(address,address,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L38-L48) is never used and should be removed

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L38-L48


 - [ ] ID-43
[BaseRelayRecipient._msgData()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L39-L56) is never used and should be removed

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L39-L56


 - [ ] ID-44
[DecimalShiftBridge._shiftUint(uint256,int256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L55-L63) is never used and should be removed

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L55-L63


 - [ ] ID-45
[DecimalShiftBridge._shiftValue(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L45-L47) is never used and should be removed

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L45-L47


 - [ ] ID-46
[DecimalShiftBridge._setDecimalShift(int256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L17-L21) is never used and should be removed

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L17-L21


 - [ ] ID-47
[Message.recoverAddressFromSignedMessage(bytes,bytes,bool)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L51-L70) is never used and should be removed

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L51-L70


 - [ ] ID-48
[ERC20Bridge.setErc20token(address)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L14-L17) is never used and should be removed

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L14-L17


 - [ ] ID-49
[SafeMath.div(uint256,uint256)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L29-L34) is never used and should be removed

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L29-L34


 - [ ] ID-50
[ForeignBridgeErcToNative.onExecuteMessage(address,uint256,bytes32)](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L51-L58) is never used and should be removed

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L51-L58

### Recommendation

	Remove unused functions.

## solc-version
Impact: Informational
Confidence: High
 - [ ] ID-51
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/OtherSideBridgeStorage.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/OtherSideBridgeStorage.sol#L1


 - [ ] ID-52
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ValidatorStorage.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ValidatorStorage.sol#L1


 - [ ] ID-53
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/InitializableBridge.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/InitializableBridge.sol#L1


 - [ ] ID-54
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Validatable.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Validatable.sol#L1


 - [ ] ID-55
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L1


 - [ ] ID-56
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Sacrifice.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Sacrifice.sol#L1


 - [ ] ID-57
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Ownable.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Ownable.sol#L1


 - [ ] ID-58
Pragma version[^0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/token/ERC20/ERC20.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/token/ERC20/ERC20.sol#L1


 - [ ] ID-59
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/interfaces/IRelayRecipient.sol#L2) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/interfaces/IRelayRecipient.sol#L2


 - [ ] ID-60
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L1


 - [ ] ID-61
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L1


 - [ ] ID-62
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/VersionableBridge.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/VersionableBridge.sol#L1


 - [ ] ID-63
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/IInterestReceiver.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/IInterestReceiver.sol#L1


 - [ ] ID-64
solc-0.4.24 is not recommended for deployment

 - [ ] ID-65
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L1


 - [ ] ID-66
Pragma version[^0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L1


 - [ ] ID-67
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/ERC677.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/ERC677.sol#L1


 - [ ] ID-68
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L1


 - [ ] ID-69
Pragma version[^0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/AddressUtils.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/AddressUtils.sol#L1


 - [ ] ID-70
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L1


 - [ ] ID-71
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/ISavingsDai.sol#L18) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/ISavingsDai.sol#L18


 - [ ] ID-72
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L3) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/BaseRelayRecipient.sol#L3


 - [ ] ID-73
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Claimable.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Claimable.sol#L1


 - [ ] ID-74
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Upgradeable.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Upgradeable.sol#L1


 - [ ] ID-75
Pragma version[^0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/token/ERC20/ERC20Basic.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/token/ERC20/ERC20Basic.sol#L1


 - [ ] ID-76
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeability/EternalStorage.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeability/EternalStorage.sol#L1


 - [ ] ID-77
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/IUpgradeabilityOwnerStorage.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/IUpgradeabilityOwnerStorage.sol#L1


 - [ ] ID-78
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/IBridgeValidators.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/IBridgeValidators.sol#L1


 - [ ] ID-79
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Initializable.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Initializable.sol#L1


 - [ ] ID-80
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L1


 - [ ] ID-81
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicForeignBridge.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicForeignBridge.sol#L1


 - [ ] ID-82
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Address.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Address.sol#L1


 - [ ] ID-83
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L1


 - [ ] ID-84
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L1


 - [ ] ID-85
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L1


 - [ ] ID-86
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/SavingsDaiConnector.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/SavingsDaiConnector.sol#L1


 - [ ] ID-87
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/interfaces/IKnowForwarderAddress.sol#L2) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/gsn/interfaces/IKnowForwarderAddress.sol#L2


 - [ ] ID-88
Pragma version[0.4.24](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/MessageRelay.sol#L1) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/MessageRelay.sol#L1


 - [ ] ID-89
solc-0.8.22 is not recommended for deployment

 - [ ] ID-90
Pragma version[^0.8.13](https://github.com/balajipachai/audit-challenge/blob/main/test/Counter.t.sol#L2) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/test/Counter.t.sol#L2


 - [ ] ID-91
Pragma version[^0.8.13](https://github.com/balajipachai/audit-challenge/blob/main/src/Counter.sol#L2) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/src/Counter.sol#L2


 - [ ] ID-92
Pragma version[^0.8.13](https://github.com/balajipachai/audit-challenge/blob/main/script/Counter.s.sol#L2) allows old versions

https://github.com/balajipachai/audit-challenge/blob/main/script/Counter.s.sol#L2

### Recommendation

Deploy with any of the following Solidity versions:

0.8.18
The recommendations take into account:

- Risks related to recent releases
- Risks of complex code generation changes
- Risks of new language features
- Risks of known bugs

Use a simple pragma version that allows any of these versions. Consider using the latest version of Solidity for testing.

## naming-convention
Impact: Informational
Confidence: High
 - [ ] ID-93
Parameter [Message.hasEnoughValidSignatures(bytes,bytes,IBridgeValidators,bool)._validatorContract](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L98) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L98


 - [ ] ID-94
Parameter [BasicTokenBridge.setMinPerTx(uint256)._minPerTx](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L92) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L92


 - [ ] ID-95
Parameter [ForeignBridgeErcToNative.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._validatorContract](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L8) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L8


 - [ ] ID-96
Parameter [GSNForeignERC20Bridge.setTrustedForwarder(address)._trustedForwarder](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L20) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L20


 - [ ] ID-97
Parameter [XDaiForeignBridge.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._homeDailyLimitHomeMaxPerTxArray](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L14) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L14


 - [ ] ID-98
Parameter [ForeignBridgeErcToNative.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._decimalShift](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L15) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L15


 - [ ] ID-99
Parameter [MessageRelay.setRelayedMessages(bytes32,bool)._status](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/MessageRelay.sol#L10) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/MessageRelay.sol#L10


 - [ ] ID-100
Function [ISavingsDai.PERMIT_TYPEHASH()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/ISavingsDai.sol#L32) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/ISavingsDai.sol#L32


 - [ ] ID-101
Parameter [SafeMath.sub(uint256,uint256)._b](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L39) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L39


 - [ ] ID-102
Parameter [Message.hasEnoughValidSignatures(bytes,bytes,IBridgeValidators,bool)._message](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L96) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L96


 - [ ] ID-103
Parameter [ForeignBridgeErcToNative.claimTokens(address,address)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L45) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L45


 - [ ] ID-104
Parameter [InterestConnector.isInterestEnabled(address)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L39) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L39


 - [ ] ID-105
Parameter [XDaiForeignBridge.onExecuteMessage(address,uint256,bytes32)._recipient](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L73) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L73


 - [ ] ID-106
Parameter [SafeMath.mul(uint256,uint256)._b](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L13) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L13


 - [ ] ID-107
Parameter [ForeignBridgeErcToNative.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._bridgeOnOtherSide](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L16) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L16


 - [ ] ID-108
Parameter [Claimable.claimNativeCoins(address)._to](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Claimable.sol#L40) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Claimable.sol#L40


 - [ ] ID-109
Parameter [ForeignBridgeErcToNative.relayTokens(address,uint256)._receiver](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L64) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L64


 - [ ] ID-110
Parameter [SafeMath.div(uint256,uint256)._b](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L29) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L29


 - [ ] ID-111
Parameter [SafeMath.add(uint256,uint256)._b](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L47) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L47


 - [ ] ID-112
Parameter [XDaiForeignBridge.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._owner](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L15) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L15


 - [ ] ID-113
Parameter [InterestConnector.disableInterest(address)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L108) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L108


 - [ ] ID-114
Parameter [InterestConnector.setInterestReceiver(address,address)._receiver](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L128) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L128


 - [ ] ID-115
Parameter [SafeERC20.safeTransferFrom(address,address,uint256)._from](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L38) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L38


 - [ ] ID-116
Parameter [ForeignBridgeErcToNative.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._dailyLimitMaxPerTxMinPerTxArray](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L12) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L12


 - [ ] ID-117
Parameter [SafeMath.sub(uint256,uint256)._a](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L39) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L39


 - [ ] ID-118
Parameter [InterestConnector.setInterestReceiver(address,address)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L128) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L128


 - [ ] ID-119
Parameter [BasicTokenBridge.addTotalExecutedPerDay(uint256,uint256)._value](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L66) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L66


 - [ ] ID-120
Parameter [InterestConnector.setMinCashThreshold(address,uint256)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L71) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L71


 - [ ] ID-121
Parameter [Claimable.claimErc20Tokens(address,address)._to](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Claimable.sol#L50) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Claimable.sol#L50


 - [ ] ID-122
Parameter [BasicTokenBridge.setExecutionMaxPerTx(uint256)._maxPerTx](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L82) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L82


 - [ ] ID-123
Parameter [Claimable.claimValues(address,address)._to](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Claimable.sol#L28) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Claimable.sol#L28


 - [ ] ID-124
Function [ISavingsDai.DOMAIN_SEPARATOR()](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/ISavingsDai.sol#L33) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/interfaces/ISavingsDai.sol#L33


 - [ ] ID-125
Parameter [Claimable.claimValues(address,address)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Claimable.sol#L28) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Claimable.sol#L28


 - [ ] ID-126
Parameter [Claimable.claimErc20Tokens(address,address)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Claimable.sol#L50) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/Claimable.sol#L50


 - [ ] ID-127
Parameter [BasicTokenBridge.addTotalSpentPerDay(uint256,uint256)._value](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L62) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L62


 - [ ] ID-128
Parameter [InterestConnector.invest(address)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L164) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L164


 - [ ] ID-129
Parameter [XDaiForeignBridge.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._gasPrice](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L12) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L12


 - [ ] ID-130
Parameter [BasicTokenBridge.withinExecutionLimit(uint256)._amount](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L53) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L53


 - [ ] ID-131
Parameter [BasicTokenBridge.totalExecutedPerDay(uint256)._day](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L24) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L24


 - [ ] ID-132
Parameter [XDaiForeignBridge.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._dailyLimitMaxPerTxMinPerTxArray](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L13) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L13


 - [ ] ID-133
Parameter [SafeERC20.safeTransfer(address,address,uint256)._to](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L20) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L20


 - [ ] ID-134
Parameter [BasicTokenBridge.setDailyLimit(uint256)._dailyLimit](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L70) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L70


 - [ ] ID-135
Parameter [BasicTokenBridge.addTotalSpentPerDay(uint256,uint256)._day](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L62) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L62


 - [ ] ID-136
Parameter [XDaiForeignBridge.claimTokens(address,address)._to](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L64) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L64


 - [ ] ID-137
Parameter [InterestConnector.initializeInterest(address,uint256,uint256,address)._minInterestPaid](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L53) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L53


 - [ ] ID-138
Parameter [InterestConnector.payInterest(address,uint256)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L138) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L138


 - [ ] ID-139
Parameter [BasicTokenBridge.withinLimit(uint256)._amount](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L48) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L48


 - [ ] ID-140
Parameter [InterestConnector.minCashThreshold(address)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L80) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L80


 - [ ] ID-141
Parameter [BasicTokenBridge.setMaxPerTx(uint256)._maxPerTx](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L87) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L87


 - [ ] ID-142
Parameter [InterestConnector.initializeInterest(address,uint256,uint256,address)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L51) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L51


 - [ ] ID-143
Parameter [Address.safeSendValue(address,uint256)._value](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Address.sol#L15) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Address.sol#L15


 - [ ] ID-144
Parameter [ERC20Bridge.setErc20token(address)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L14) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L14


 - [ ] ID-145
Parameter [ERC20Bridge.relayTokens(address,uint256)._receiver](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L19) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L19


 - [ ] ID-146
Parameter [BasicTokenBridge.totalSpentPerDay(uint256)._day](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L20) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L20


 - [ ] ID-147
Parameter [MessageRelay.relayedMessages(bytes32)._txHash](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/MessageRelay.sol#L6) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/MessageRelay.sol#L6


 - [ ] ID-148
Parameter [SafeERC20.safeTransferFrom(address,address,uint256)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L38) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L38


 - [ ] ID-149
Parameter [SafeMath.mul(uint256,uint256)._a](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L13) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L13


 - [ ] ID-150
Parameter [InterestConnector.interestReceiver(address)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L118) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L118


 - [ ] ID-151
Parameter [ForeignBridgeErcToNative.onExecuteMessage(address,uint256,bytes32)._recipient](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L52) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L52


 - [ ] ID-152
Parameter [Address.safeSendValue(address,uint256)._receiver](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Address.sol#L15) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Address.sol#L15


 - [ ] ID-153
Parameter [BasicBridge.setRequiredBlockConfirmations(uint256)._blockConfirmations](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L39) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L39


 - [ ] ID-154
Parameter [ForeignBridgeErcToNative.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._gasPrice](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L11) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L11


 - [ ] ID-155
Parameter [ForeignBridgeErcToNative.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._requiredBlockConfirmations](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L10) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L10


 - [ ] ID-156
Parameter [XDaiForeignBridge.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._erc20token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L10) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L10


 - [ ] ID-157
Parameter [InterestConnector.setMinInterestPaid(address,uint256)._minInterestPaid](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L90) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L90


 - [ ] ID-158
Parameter [MessageRelay.setRelayedMessages(bytes32,bool)._txHash](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/MessageRelay.sol#L10) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/MessageRelay.sol#L10


 - [ ] ID-159
Parameter [ForeignBridgeErcToNative.relayTokens(address,uint256)._amount](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L64) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L64


 - [ ] ID-160
Parameter [ForeignBridgeErcToNative.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._homeDailyLimitHomeMaxPerTxArray](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L13) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L13


 - [ ] ID-161
Parameter [SafeMath.add(uint256,uint256)._a](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L47) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L47


 - [ ] ID-162
Parameter [ForeignBridgeErcToNative.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._owner](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L14) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L14


 - [ ] ID-163
Parameter [BasicBridge.setGasPrice(uint256)._gasPrice](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L31) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicBridge.sol#L31


 - [ ] ID-164
Parameter [XDaiForeignBridge.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._decimalShift](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L16) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L16


 - [ ] ID-165
Parameter [SafeERC20.safeTransferFrom(address,address,uint256)._value](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L38) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L38


 - [ ] ID-166
Parameter [InterestConnector.payInterest(address,uint256)._amount](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L138) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L138


 - [ ] ID-167
Parameter [BasicTokenBridge.addTotalExecutedPerDay(uint256,uint256)._day](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L66) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L66


 - [ ] ID-168
Parameter [InterestConnector.setMinCashThreshold(address,uint256)._minCashThreshold](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L71) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L71


 - [ ] ID-169
Parameter [XDaiForeignBridge.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._validatorContract](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L9) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L9


 - [ ] ID-170
Parameter [SafeERC20.safeTransfer(address,address,uint256)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L20) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L20


 - [ ] ID-171
Parameter [InterestConnector.initializeInterest(address,uint256,uint256,address)._interestReceiver](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L54) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L54


 - [ ] ID-172
Parameter [InterestConnector.setMinInterestPaid(address,uint256)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L90) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L90


 - [ ] ID-173
Parameter [InterestConnector.minInterestPaid(address)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L99) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L99


 - [ ] ID-174
Parameter [Message.isMessageValid(bytes)._msg](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L43) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/Message.sol#L43


 - [ ] ID-175
Parameter [SavingsDaiConnector.previewWithdraw(address,uint256)._amount](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/SavingsDaiConnector.sol#L78) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/SavingsDaiConnector.sol#L78


 - [ ] ID-176
Parameter [ForeignBridgeErcToNative.onExecuteMessage(address,uint256,bytes32)._amount](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L53) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L53


 - [ ] ID-177
Parameter [XDaiForeignBridge.claimTokens(address,address)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L64) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L64


 - [ ] ID-178
Parameter [ForeignBridgeErcToNative.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._erc20token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L9) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L9


 - [ ] ID-179
Parameter [InterestConnector.investedAmount(address)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L155) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L155


 - [ ] ID-180
Parameter [InterestConnector.initializeInterest(address,uint256,uint256,address)._minCashThreshold](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L52) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/InterestConnector.sol#L52


 - [ ] ID-181
Parameter [SavingsDaiConnector.interestAmount(address)._token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/SavingsDaiConnector.sol#L32) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/SavingsDaiConnector.sol#L32


 - [ ] ID-182
Parameter [ForeignBridgeErcToNative.claimTokens(address,address)._to](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L45) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L45


 - [ ] ID-183
Parameter [ERC20Bridge.relayTokens(address,uint256)._amount](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L19) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L19


 - [ ] ID-184
Parameter [SafeERC20.safeTransfer(address,address,uint256)._value](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L20) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/libraries/SafeERC20.sol#L20


 - [ ] ID-185
Parameter [XDaiForeignBridge.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._bridgeOnOtherSide](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L17) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L17


 - [ ] ID-186
Parameter [XDaiForeignBridge.onExecuteMessage(address,uint256,bytes32)._amount](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L74) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L74


 - [ ] ID-187
Parameter [BasicTokenBridge.setExecutionDailyLimit(uint256)._dailyLimit](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L76) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L76


 - [ ] ID-188
Parameter [GSNForeignERC20Bridge.setPayMaster(address)._paymaster](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L28) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L28


 - [ ] ID-189
Parameter [XDaiForeignBridge.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._requiredBlockConfirmations](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L11) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L11


 - [ ] ID-190
Parameter [SafeMath.div(uint256,uint256)._a](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L29) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/node_modules/openzeppelin-solidity/contracts/math/SafeMath.sol#L29


 - [ ] ID-191
Function [CounterTest.testFuzz_SetNumber(uint256)](https://github.com/balajipachai/audit-challenge/blob/main/test/Counter.t.sol#L20-L23) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/test/Counter.t.sol#L20-L23


 - [ ] ID-192
Function [CounterTest.test_Increment()](https://github.com/balajipachai/audit-challenge/blob/main/test/Counter.t.sol#L15-L18) is not in mixedCase

https://github.com/balajipachai/audit-challenge/blob/main/test/Counter.t.sol#L15-L18


### Recommendation

Follow the Solidity [`naming convention`](https://solidity.readthedocs.io/en/v0.4.25/style-guide.html#naming-conventions).

## similar-names
Impact: Informational
Confidence: Medium
 - [ ] ID-193
Variable [OtherSideBridgeStorage.BRIDGE_CONTRACT](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/OtherSideBridgeStorage.sol#L6) is too similar to [OtherSideBridgeStorage._setBridgeContractOnOtherSide(address)._bridgeContract](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/OtherSideBridgeStorage.sol#L8)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/OtherSideBridgeStorage.sol#L6


 - [ ] ID-194
Variable [ERC20Bridge.ERC20_TOKEN](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L8) is too similar to [XDaiForeignBridge.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._erc20token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L10)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L8


 - [ ] ID-195
Variable [BasicTokenBridge.DAILY_LIMIT](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L16) is too similar to [BasicTokenBridge.maxAvailablePerTx()._dailyLimit](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L103)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L16


 - [ ] ID-196
Variable [GSNForeignERC20Bridge.TRUSTED_FORWARDER](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L10) is too similar to [GSNForeignERC20Bridge.setTrustedForwarder(address)._trustedForwarder](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L20)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/GSNForeignERC20Bridge.sol#L10


 - [ ] ID-197
Variable [DecimalShiftBridge.DECIMAL_SHIFT](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L9) is too similar to [XDaiForeignBridge.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._decimalShift](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L16)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L9


 - [ ] ID-198
Variable [ValidatorStorage.VALIDATOR_CONTRACT](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ValidatorStorage.sol#L4) is too similar to [ForeignBridgeErcToNative.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._validatorContract](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L8)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ValidatorStorage.sol#L4


 - [ ] ID-199
Variable [BasicTokenBridge.DAILY_LIMIT](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L16) is too similar to [BasicTokenBridge.setDailyLimit(uint256)._dailyLimit](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L70)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L16


 - [ ] ID-200
Variable [DecimalShiftBridge.DECIMAL_SHIFT](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L9) is too similar to [ForeignBridgeErcToNative.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._decimalShift](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L15)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/DecimalShiftBridge.sol#L9


 - [ ] ID-201
Variable [BasicTokenBridge.DAILY_LIMIT](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L16) is too similar to [BasicTokenBridge.setExecutionDailyLimit(uint256)._dailyLimit](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L76)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/BasicTokenBridge.sol#L16


 - [ ] ID-202
Variable [ERC20Bridge.ERC20_TOKEN](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L8) is too similar to [ForeignBridgeErcToNative.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._erc20token](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/ForeignBridgeErcToNative.sol#L9)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ERC20Bridge.sol#L8


 - [ ] ID-203
Variable [ValidatorStorage.VALIDATOR_CONTRACT](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ValidatorStorage.sol#L4) is too similar to [XDaiForeignBridge.initialize(address,address,uint256,uint256,uint256[3],uint256[2],address,int256,address)._validatorContract](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L9)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/ValidatorStorage.sol#L4

### Recommendation

	Prevent variables from having similar 1598.

## unused-state
Impact: Informational
Confidence: High
 - [ ] ID-204
[EternalStorage.stringStorage](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeability/EternalStorage.sol#L9) is never used in [XDaiForeignBridge](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L7-L99)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeability/EternalStorage.sol#L9


 - [ ] ID-205
[EternalStorage.bytesStorage](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeability/EternalStorage.sol#L11) is never used in [XDaiForeignBridge](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L7-L99)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeability/EternalStorage.sol#L11


 - [ ] ID-206
[EternalStorage.intStorage](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeability/EternalStorage.sol#L13) is never used in [XDaiForeignBridge](https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeable_contracts/erc20_to_native/XDaiForeignBridge.sol#L7-L99)

https://github.com/balajipachai/audit-challenge/blob/main/src/mainnet/0x166124b75c798Cedf1B43655E9B5284eBd5203DB/contracts/upgradeability/EternalStorage.sol#L13

### Recommendation

	Remove unused state variables.