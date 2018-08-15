<h3 id="how-does-ethereum-virtual-machine-working">How Does Ethereum Virtual Machine Working</h3>
<hr>
<ul>
<li>The EVM is a database engine. To understand how smart contracts work in any EVM language, you have to understand how data is organized, stored and manipulated.</li>
</ul>
<p>In the following of description, I’d like to analyse simple Solidity contracts in order to understand how it work as EVM bytecode.</p>
<pre><code>pragma solidity ^0.4.11;
contract simple {
    uint256 public a;
    function simple() {
      a = 1;
    }
}
</code></pre>
<p>Assemble and binary result of compiling contract with <code>solc</code></p>
<pre><code>#Initalate
00|60   PUSH1
01|80   0x80
02|60   PUSH1
03|40   0x40
04|52   MSTORE
05|34   CALLVALUE &lt;----------|
06|80   DUP1                 |---&gt; Check transaction value, if that isn't zero then revert it.
07|15   ISZERO &lt;-------------|
08|60   PUSH1
09|0f   0xF
10|57   JUMPI ---&gt; jump to 0xf
11|60   PUSH
12|00   0x0
13|80   DUP1
14|fd   REVERT
#Tag 1
15|5b   JUMPDEST
16|50   POP
17|60   PUSH &lt;---|
18|01   0x1      |---&gt; store address 0x0 =&gt; 0x1 (a=1)
19|60   PUSH     |
20|00   0x0      |
21|55   SSTORE &lt;-|
22|60   PUSH1
23|35   0x99 ---&gt; Code copy size
24|80   DUP1
25|61   PUSH2
26|00   0x00 &lt;---|---&gt; 0x0023 code copy offset
27|23   0x25 &lt;---|
28|60   PUSH1
29|00   0x00
30|39   CODECOPY
31|60   PUSH1
32|00   0x00
33|f3   RETURN
34|00   STOP
#Data 0
35|608060405260043610603e5763ffffff &lt;---|
51|ff7c0100000000000000000000000000     |---&gt; store to memroy address 0x0 (size 0x99)
67|00000000000000000000000000000060     |
83|00350416630dbe671f81146043575b60     |
99|0080fd5b348015604e57600080fd5b50     |
115|60556067565b60408051918252519081    |
131|900360200190f35b600054815600a165    |
147|627a7a72305820d0a8fe23edbe3f2798    |
163|2145f0a91df1527499dc1c4bdf2d655b    |
179|b198d53737c7560029 &lt;----------------|
</code></pre>
<p>The contract ABI <code>0dbe671f a()</code> execute  result and analysis</p>
<pre><code>00|6080604052 
05|60 PUSH1 &lt;----------|
06|04 0x4              |
07|36 CALLDATASIZE     |---&gt; check transaction data size, if that is less than 0x4 and ready to jump
08|10 LT &lt;-------------|
09|60 PUSH1
10|3e 0x3e
11|57 JUMPI ---&gt; jump to 0x3e
12|63 PUSH4 &lt;------------------------------------------------------|
13|ffffffff 0xFFFFFFFF                                             |---&gt; function filter out
17|7c PUSH29                                                       |
46|0100000000000000000000000000000000000000000000000000000000      |
47|60 PUSH1                                                        |
48|00 0x0                                                          |
49|35 CALLDATALOAD                                                 |
50|04 DIV                                                          |
51|16 AND &lt;--------------------------------------------------------|
52|63 PUSH3 &lt;---------------------------|
53|0dbe671f                             |---&gt; verify the function existing function name
54|81 DUP2                              |
55|14 EQ                                |
56|60 PUSH1                             |
57|43 0x43                              |
58|57 JUMPI &lt;---------------------------|
59|5b JUMPDEST
60|60 PUSH1
61|00 0x0
62|80 DUP1
63|fd REVERT
64|5b JUMPDEST
65|34 CALLVALUE &lt;---|
66|80 DUP1          |---&gt; Check transaction value, if that isn't zero then revert it.
67|15 ISZERO &lt;------|
67|60 PUSH1
68|4e 0x4e
69|57 JUMPI
70|60 PUSH1
71|00 0x0
72|80 DUP1
73|fd REVERT
74|5b JUMPDEST
75|50 POP ---&gt; pop 0x0
80|60 PUSH1
81|55 0x55
82|60 PUSH1
83|67 0x67
84|56 JUMP ---&gt; jump to 0x67
85|5b JUMPDEST
86|60 PUSH1 &lt;-------------------|-------------------------------|
87|40 0x40                      |                               |---&gt; prepare return memroy
88|80 DUP1                      |---&gt; store value to 0x80       |
89|51 MLOAD                     |                               |
90|91 SWAP2                     |                               |
91|82 DUP3                      |                               |
92|52 MSTORE &lt;------------------|                               |
93|51 MLOAD                                                     |
94|90 SWAP1                                                     |
95|81 DUP2                                                      |
96|90 SWAP1                                                     |
97|03 SUB                                                       |
98|60 PUSH1                                                     |
99|20 0x20                                                      |
100|01 ADD                                                      |
101|90 SWAP1                                                    |
102|f3 RETURN --------------------------------------------------|
103|5b JUMPDEST
104|60 PUSH1
105|00 0x0
106|54 SLOAD
107|81 DUP2
108|56 JUMP ---&gt; jump to 0x55
109|00 STOP
110|a1 LOG1
111|65 PUSH6
112|627a7a723058
118|20 SHA3
119|d0 INVALID
120|a8 INVALID
121|fe INVALID
122|23 INVALID
123|ed INVALID
124|be INVALID
125|3f INVALID
126|27 INVALID
127|98 SWAP9
128|21 INVALID
129|45 GASLIMIT
130|f0 CREATE
131|a9 INVALID
132|1d INVALID
133|f1 CALL
134|52 MSTORE
135|74 PUSH21
136|99dc1c4bdf2d655bb198d53737c7560029
</code></pre>
<h3 id="where-is-the-smart-contract-">Where is the Smart Contract ?</h3>
<hr>
<p><img src="https://lh3.googleusercontent.com/pWIiV8sw7os9jIMPxkrGfyY7w84Lq2KyKOISYNCckEDJ0u823rh4JVPnNthw02677T3tMsrQimVL=s1024" alt="enter image description here"></p>

