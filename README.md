EthIR
=====


A framework for high-level Analysis of Ethereum Bytecode.

The tool extends [OYENTE framework](https://github.com/melonproject/oyente). [OYENTE](https://github.com/melonproject/oyente) builds CFGs of Ethereum bytecode and looks for different kind of vulnerabilities on the bytecode. Based on the CFG of a Ethereum bytecode,EthIR generates a *rule-based representation*(RBR) of it. This high-level representation enables the application of existing high-level analyses to infer properties of EVM code.

## Installation
1. Install Solidity compiler (last version tested 0.4.19)
```
 sudo add-apt-repository ppa:ethereum/ethereum
 sudo apt-get update
 sudo apt-get install solc
```

2. Install Ethereum (last version tested 1.7.3)
```
 sudo apt-get install software-properties-common
 sudo add-apt-repository -y ppa:ethereum/ethereum
 sudo apt-get update
 sudo apt-get install ethereum
```

3. Install [Z3](https://github.com/Z3Prover/z3/releases) (last version tested 4.5.0)

   Download the [source code folder](https://github.com/Z3Prover/z3/releases/tag/z3-4.5.0).

   Decompress the folder and install it.
```
 unzip z3-z3-4.5.0.zip
 cd z3-z3-4.5.0
 python scripts/mk_make.py --python
 cd build
 make
 sudo make install
```
4. Install dependencies

   Use `pip install` command to install six, requests, web3 python libraries.
```
pip install six
pip install requests
pip install web3
```
## Run EthIR

To execute EthIR, run one of the following commands inside the folder *ethir*:

1. Run ETHIR from a solidity file:
```
./oyente-ethir -s file_name.sol
```
2. Run ETHIR from an EVM file:
```
./oyente-ethir -s file_name.evm -b 
```
3. Run ETHIR from a disassembly EVM file:
```
./oyente-ethir -s file_name.disasm -disasm 
```

### Options
The command `./oyente-ethir -h` displays a list with all the available options of EthIR. Some of the most relevant ones are:

1. Store the control-flow-graph:
```
./oyente-ethir -s filename -cfg
```
2. Add nop annotations with EVM bytecodes:
```
./oyente-ethir -s filename -eop
```
3. Generate SACO RBR
```
./oyente-ethir -s filename -saco
```

All the files generated by EthIR during its execution are stored in the direcrtory /tmp/costabs/ .

### Running Example
Once EthIR is installed, suppose we want to generate the RBR of the disassembly file *blockking.evm.disasm* available in the folder *[examples](https://github.com/costa-group/EthIR/tree/master/examples)*. First, we have to go to *ethir* directory and execute the command `./oyente-ethir -s ../examples/blockking.evm.disasm -disasm` there.

During the execution, EthIR has created the directory */tmp/costabs/* where it stores the RBR associated with *blockking.evm.disasm* file. If we inspect this directory, we find a file called *rbr.rbr* that contains the RBR. If we open the file with any common editor (gedit, emacs) we can see the rbr generated. Below is a skecth of the RBR generated for *blockking.evm.disasm* file:
```
block0(g(11), g(10), g(9), g(8), g(7), g(6), g(5), g(4), g(3), g(2), g(1), g(0), l(8), l(7), l(6), l(5), l(4), l(3), l(2), l(1), l(0), calldatasize, calldataload, gas, caller, callvalue, number, gasprice, balance)=>
	s(0) = 96
	s(1) = 64
	l(0) = s(0)
	s(0) = calldatasize
	call(jump0(s(0),g(11), g(10), g(9), g(8), g(7), g(6), g(5), g(4), g(3), g(2), g(1), g(0), l(8), l(7), l(6), l(5), l(4), l(3), l(2), l(1), l(0), calldatasize, calldataload, gas, caller, callvalue, number, gasprice, balance))
 
jump0(s(0), g(11), g(10), g(9), g(8), g(7), g(6), g(5), g(4), g(3), g(2), g(1), g(0), l(8), l(7), l(6), l(5), l(4), l(3), l(2), l(1), l(0), calldatasize, calldataload, gas, caller, callvalue, number, gasprice, balance)=>
	eq(s(0), 0)
	call(block174(g(11), g(10), g(9), g(8), g(7), g(6), g(5), g(4), g(3), g(2), g(1), g(0), l(8), l(7), l(6), l(5), l(4), l(3), l(2), l(1), l(0), calldatasize, calldataload, gas, caller, callvalue, number, gasprice, balance))

jump0(s(0), g(11), g(10), g(9), g(8), g(7), g(6), g(5), g(4), g(3), g(2), g(1), g(0), l(8), l(7), l(6), l(5), l(4), l(3), l(2), l(1), l(0), calldatasize, calldataload, gas, caller, callvalue, number, gasprice, balance)=>
	neq(s(0), 0)
 call(block11(g(11), g(10), g(9), g(8), g(7), g(6), g(5), g(4), g(3), g(2), g(1), g(0), l(8), l(7), l(6), l(5), l(4), l(3), l(2), l(1), l(0), calldatasize, calldataload, gas, caller, callvalue, number, gasprice, balance))
 
block11(g(11), g(10), g(9), g(8), g(7), g(6), g(5), g(4), g(3), g(2), g(1), g(0), l(8), l(7), l(6), l(5), l(4), l(3), l(2), l(1), l(0), calldatasize, calldataload, gas, caller, callvalue, number, gasprice, balance)=>
	s(0) = 224
	s(1) = 2
	s(0) = s(1)^s(0)
	s(1) = 0
	s(1) = calldataload
	s(0) = s(1)/s(0)
	s(1) = 607252836
	s(2) = s(0)
	call(jump11(s(2),s(1),s(0),g(11), g(10), g(9), g(8), g(7), g(6), g(5), g(4), g(3), g(2), g(1), g(0), l(8), l(7), l(6), l(5), l(4), l(3), l(2), l(1), l(0), calldatasize, calldataload, gas, caller, callvalue, number, gasprice, balance))
```
If we execute the command `./oyente-ethir -s ../examples/blockking.evm.disasm -disasm -eop` instead of the above one, the RBR that EthIR produces has nops annotations, with the EVM bytecode translated, interleaved in the text. Below is a sketch of the RBR with nops annotations generated for *blockking.evm.disasm*:
```
block0(g(11), g(10), g(9), g(8), g(7), g(6), g(5), g(4), g(3), g(2), g(1), g(0), l(8), l(7), l(6), l(5), l(4), l(3), l(2), l(1), l(0), calldatasize, calldataload, gas, caller, callvalue, number, gasprice, balance)=>
	s(0) = 96
	nop(PUSH1)
	s(1) = 64
	nop(PUSH1)
	l(0) = s(0)
	nop(MSTORE)
	s(0) = calldatasize
	nop(CALLDATASIZE)
	call(jump0(s(0),globals,bc))
	nop(ISZERO)
	nop(PUSH2)
	nop(JUMPI)
 
jump0(s(0), g(11), g(10), g(9), g(8), g(7), g(6), g(5), g(4), g(3), g(2), g(1), g(0), l(8), l(7), l(6), l(5), l(4), l(3), l(2), l(1), l(0), calldatasize, calldataload, gas, caller, callvalue, number, gasprice, balance)=>
	eq(s(0), 0)
	call(block174(g(11), g(10), g(9), g(8), g(7), g(6), g(5), g(4), g(3), g(2), g(1), g(0), l(8), l(7), l(6), l(5), l(4), l(3), l(2), l(1), l(0), calldatasize, calldataload, gas, caller, callvalue, number, gasprice, balance))

jump0(s(0), g(11), g(10), g(9), g(8), g(7), g(6), g(5), g(4), g(3), g(2), g(1), g(0), l(8), l(7), l(6), l(5), l(4), l(3), l(2), l(1), l(0), calldatasize, calldataload, gas, caller, callvalue, number, gasprice, balance)=>
	neq(s(0), 0)
	call(block11(g(11), g(10), g(9), g(8), g(7), g(6), g(5), g(4), g(3), g(2), g(1), g(0), l(8), l(7), l(6), l(5), l(4), l(3), l(2), l(1), l(0), calldatasize, calldataload, gas, caller, callvalue, number, gasprice, balance))
 
block11(g(11), g(10), g(9), g(8), g(7), g(6), g(5), g(4), g(3), g(2), g(1), g(0), l(8), l(7), l(6), l(5), l(4), l(3), l(2), l(1), l(0), calldatasize, calldataload, gas, caller, callvalue, number, gasprice, balance)=>
	s(0) = 224
	nop(PUSH1)
	s(1) = 2
	nop(PUSH1)
	s(0) = s(1)^s(0)
	nop(EXP)
	s(1) = 0
	nop(PUSH1)
	s(1) = calldataload
	nop(CALLDATALOAD)
	s(0) = s(1)/s(0)
	nop(DIV)
	s(1) = 607252836
	nop(PUSH4)
	s(2) = s(0)
	nop(DUP2)
	call(jump11(s(2),s(1),s(0),globals,bc))
	nop(EQ)
	nop(PUSH2)
	nop(JUMPI)
```

EthIR also allows us to store the CFG bound to the file analysed. In that case, we have to execute the command `./oyente-ethir -s ../examples/blockking.evm.disasm -disasm -cfg`. EthIR stores the cfg in a file called *cfg.cfg* in the directory */tmp/costabs/*.

Note that a file may contain more than one smart contract. In that case, EthIR generates one file per each contract called rbr0.rbr, rbr1.rbr,...rbrn.rbr .

## Smart Contract Examples
The folder *[examples](https://github.com/costa-group/EthIR/tree/master/examples)* contains running examples to test the tool. There are both solidity, evm and disassembly files.

Most of the examples such as bloccking.evm.disasm, advertisement.sol, validToken.sol or cryptoPhoenix.sol are real-world contracts obtained from the blockchain while others such as loop1.sol and sum.sol are ad-hoc examples where it is easier to understand the decompilation process.

## Bounding Loops using SACO
[SACO](http://costa.fdi.ucm.es/saco/web/) is a static analyzer for concurrent objects which, is able to infer, among other properties,*upper bounds* on the number of iterations of loops. Note that this is the first crucial step to infer the gas
consumption of smart contracts.

The internal representation of [SACO](http://costa.fdi.ucm.es/saco/web/) matches the grammar of the RBR generated by EthIR after minor syntactic translations. Thanks to this, it is able to prove termination of the loops that some of the examples contain and produce a linear
bound for those loops. Here are some of the loop bounds inferred by SACO for some of the smart contracts contained in folder [*examples*](https://github.com/costa-group/EthIR/tree/master/examples):

|Smart Contract|Bound|Smart Contract|Bound|
|--|--|--|--|
| BlockKing | nat(g8/10)*36+8934493 | CryptoPhoenix | nat(g3)*228409344+4113285485 |
| Loop1 | nat(a)*25+234 | Eligma | nat(_numberOfReturns)*2628+134 |
| Lottery | 159 | BlockSquareSerieA | 286 |
| Enclaves | 268 | AuctusEther | 264 |
| Advertisement | inf |  validToken | inf |

[SACO](http://costa.fdi.ucm.es/saco/web/) infers a linear bound for the first four smart contracts shown in the table above. The bounds of BlockKing and CryptoPhoenix smart contracts depend on the value of one of their fields (the eighth and third respectively). For Loop1 and Eligma smart contracts, the bounds obtained rely on function arguments (a and _numberOfReturns). In case smart contracts do not contain any loop as Lottery or BlockSquareSerieA, [SACO](http://costa.fdi.ucm.es/saco/web/) infers a constant bound.

Note that due to precision limitations of [SACO](http://costa.fdi.ucm.es/saco/web/) (it does not have bit-operations) the analyzer forgets the information on bit variables. Due to this factor, [SACO](http://costa.fdi.ucm.es/saco/web/) is not able to infer a bound for some of the smart contracts such as ValidToken or Advertisement and returns *inf*.

Other high-level analyzers that work on intermediate forms like Integer transition systems or Horn clauses  (e.g., AproVe, T2, VeryMax, CoFloCo) could be easily adapted as well to work on RBR translated programs produced by EthIR. 

If you are interesting in using EthIR jointly with [SACO](http://costa.fdi.ucm.es/saco/web/) contact [SACO](http://costa.fdi.ucm.es/saco/web/) developers through a pull-request or a new issue.
