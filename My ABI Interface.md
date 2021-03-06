---


---

<h1 id="contract-terminology">Contract Terminology</h1>

<table>
<thead>
<tr>
<th>Terms</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Application binary interface (Abi)</td>
<td>The standard way to interact with contracts in the Ethereum ecosystem, The first four bytes of the call data for a function call specifies the function to be called. It is the first (left, high-order in big-endian) four bytes of the Keccak256 hash of the signature of the function. The signature is defined as the canonical expression of the basic prototype, i.e. the function name with the parenthesised list of parameter types. Parameter types are split by a single comma - no spaces are used.</td>
</tr>
<tr>
<td>Withdraw</td>
<td>This function is helping user export their token from current contract to the origin contract or account.</td>
</tr>
<tr>
<td>FallBack</td>
<td>This is specific function of ERC223 token. If the receiver is a contract ERC223 token contract will try to call <code>tokenFallback</code> function on receiver contract. If there is no <code>tokenFallback</code> function on receiver contract transaction will fail.</td>
</tr>
<tr>
<td>Fund Migration</td>
<td>It’s convenient way to help user transfer their tokens from current contract to new contract.</td>
</tr>
</tbody>
</table><h1 id="contract-management">Contract Management</h1>

<table>
<thead>
<tr>
<th>Command</th>
<th>Abi</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>changeAdmin(address)</td>
<td>8f283970</td>
<td>Changes the official admin user address. Accepts Ethereum address.</td>
</tr>
<tr>
<td>changeFeeAccount(address)</td>
<td>71ffcb16</td>
<td>Changes the account address that receives trading fees. Accepts Ethereum address.</td>
</tr>
<tr>
<td>changeFreeUntilDate(uint256)</td>
<td>a70e82d4</td>
<td>Changes the date that trades are free until. Accepts UNIX timestamp.</td>
</tr>
<tr>
<td>changeFeeTake(uint256)</td>
<td>8823a9c0</td>
<td>Changes the fee on takes. Can only be changed to a value less than it is currently set at.</td>
</tr>
</tbody>
</table><h3 id="command-detail">Command Detail</h3>
<ul>
<li>changeAdmin(address admin_):</li>
<li>changeFeeAccount(address feeAccount_):</li>
<li>changeFreeUntilDate(uint256 freeUntilDate_):</li>
<li>changeFeeTake(uint256 feeTake_):</li>
</ul>
<h3 id="example-contract-abi-of--contract-management">Example contract abi of  contract management</h3>
<ul>
<li>changeAdmin(address):
<ul>
<li><code>8f28397</code> the Method ID. This is derived from the signature <code>changeAdmin(address)</code>.</li>
<li><code>0x000000000000000000000000ca35b7d915458ef540ade6068dfe2f44e8fa733c</code> (account address padded to 32 bytes)</li>
</ul>
</li>
<li>All together, the encoding is (newline after function selector and each 32-bytes for clarity):<pre><code>0x8f28397
000000000000000000000000ca35b7d915458ef540ade6068dfe2f44e8fa733c
</code></pre>
</li>
<li>In total:<pre><code>0x8f28397000000000000000000000000ca35b7d915458ef540ade6068dfe2f44e8fa733c
</code></pre>
</li>
</ul>
<h1 id="contract-deposit">Contract Deposit</h1>

<table>
<thead>
<tr>
<th>Command</th>
<th>Abi</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>deposit()</td>
<td>d0e30db0</td>
<td>This function handles deposits of Ether into the contract.</td>
</tr>
<tr>
<td>depositToken(address,uint256)</td>
<td>338b5dea</td>
<td>This function handles deposits of Ethereum based tokens to the contract. Does not allow Ether. If token transfer fails, transaction is reverted and remaining gas is refunded.</td>
</tr>
</tbody>
</table><h3 id="command-detail-1">Command Detail</h3>
<ul>
<li>deposit()</li>
<li>depositToken(address token, uint256 amount):</li>
</ul>
<h3 id="example-contract-abi-of-contract-deposit">Example contract abi of contract deposit</h3>
<ul>
<li>depositToken(address,uint256):
<ul>
<li><code>338b5dea</code> the Method ID.</li>
<li><code>0x000000000000000000000000692a70d2e424a56d2c6c27aa97d1a86395877b3a</code> (contract address padded to 32 bytes)</li>
<li><code>0x0000000000000000000000000000000000000000000000000000000000100000</code> (number of ethereum based tokens padded to 32 bytes)</li>
</ul>
</li>
<li>All together, the encoding is (newline after function selector and each 32-bytes for clarity):<pre><code>338b5dea
0x000000000000000000000000692a70d2e424a56d2c6c27aa97d1a86395877b3a
0x0000000000000000000000000000000000000000000000000000000000100000
</code></pre>
</li>
<li>In total:<pre><code>0x338b5dea000000000000000000000000692a70d2e424a56d2c6c27aa97d1a86395877b3a0000000000000000000000000000000000000000000000000000000000100000
</code></pre>
</li>
</ul>
<h1 id="contract-withdraw">Contract Withdraw</h1>

<table>
<thead>
<tr>
<th>Command</th>
<th>Abi</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>withdraw(uint256)</td>
<td>2e1a7d4d</td>
<td>This function handles withdrawals of Ether from the contract. Verifies that the user has enough funds to cover the withdrawal.</td>
</tr>
<tr>
<td>withdrawToken(address,uint256)</td>
<td>9e281a98</td>
<td>This function handles withdrawals of Ethereum based tokens from the contract. Does not allow Ether. If token transfer fails, transaction is reverted and remaining gas is refunded.</td>
</tr>
</tbody>
</table><h3 id="command-detail-2">Command Detail</h3>
<ul>
<li>withdraw(uint256 amount):</li>
<li>withdrawToken(address token, uint256 amount):</li>
</ul>
<h3 id="example-contract-abi-of-contract-withdraw">Example contract abi of contract withdraw</h3>
<ul>
<li>withdrawToken(address, uint256):
<ul>
<li><code>9e281a98</code> the Method ID.</li>
<li><code>0x000000000000000000000000692a70d2e424a56d2c6c27aa97d1a86395877b3a</code> (contract address padded to 32 bytes)</li>
<li><code>0x0000000000000000000000000000000000000000000000000000000000100000</code> (number of ethereum based tokens padded to 32 bytes)</li>
</ul>
</li>
<li>All together, the encoding is (newline after function selector and each 32-bytes for clarity):<pre><code>9e281a98
0x000000000000000000000000692a70d2e424a56d2c6c27aa97d1a86395877b3a
0x0000000000000000000000000000000000000000000000000000000000100000
</code></pre>
</li>
<li>In total:<pre><code>0x9e281a98000000000000000000000000692a70d2e424a56d2c6c27aa97d1a86395877b3a0000000000000000000000000000000000000000000000000000000000100000
</code></pre>
</li>
</ul>
<h1 id="contract-transfer">Contract Transfer</h1>

<table>
<thead>
<tr>
<th>Command</th>
<th>Abi</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>depositForUser(address)</td>
<td>6a523c5e</td>
<td>This function handles deposits of Ether into the contract, but allows specification of a user.</td>
</tr>
<tr>
<td>depositTokenForUser(address,uint256…)</td>
<td>3c2e2a75</td>
<td>This function handles deposits of Ethereum based tokens into the contract, but allows specification of a user. Does not allow Ether. If token transfer fails, transaction is reverted and remaining gas is refunded.</td>
</tr>
</tbody>
</table><h3 id="command-detail-3">Command Detail</h3>
<ul>
<li>depositForUser(address user):</li>
<li>depositTokenForUser(address token, uint256 amount, address user):</li>
</ul>
<h3 id="example-contract-abi-of-contract-transfer">Example contract abi of contract transfer</h3>
<ul>
<li>depositTokenForUser(address,uint256,address):
<ul>
<li><code>3c2e2a75</code> the Method ID.</li>
<li><code>0x000000000000000000000000692a70d2e424a56d2c6c27aa97d1a86395877b3a</code> (contract address padded to 32 bytes)</li>
<li><code>0x0000000000000000000000000000000000000000000000000000000000100000</code> (number of ethereum based tokens padded to 32 bytes)</li>
<li><code>0x000000000000000000000000ca35b7d915458ef540ade6068dfe2f44e8fa733c</code> (account address padded to 32 bytes)</li>
</ul>
</li>
<li>All together, the encoding is (new line after function selector and each 32-bytes of clarity):<pre><code>3c2e2a75
0x000000000000000000000000692a70d2e424a56d2c6c27aa97d1a86395877b3a
0x0000000000000000000000000000000000000000000000000000000000100000
0x000000000000000000000000ca35b7d915458ef540ade6068dfe2f44e8fa733c
</code></pre>
</li>
<li>In total:<pre><code>0x3c2e2a75000000000000000000000000692a70d2e424a56d2c6c27aa97d1a86395877b3a0000000000000000000000000000000000000000000000000000000000100000000000000000000000000000ca35b7d915458ef540ade6068dfe2f44e8fa733c
</code></pre>
</li>
</ul>
<h1 id="contract-token-fallback">Contract Token Fallback</h1>

<table>
<thead>
<tr>
<th>Command</th>
<th>Abi</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>tokenFallback()</td>
<td>bd23eb39</td>
<td>This function provides a fallback solution as outlined in ERC223. If tokens are deposited through depositToken(), the transaction will continue. If tokens are sent directly to this contract, the transaction is reverted.</td>
</tr>
</tbody>
</table><h1 id="contract-trade">Contract Trade</h1>

<table>
<thead>
<tr>
<th>Command</th>
<th>Abi</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>trade(address,uint256…)</td>
<td>0a19b14a</td>
<td>Facilitates a trade from one user to another. Requires that the transaction is signed properly, the trade isn’t past its expiration, and all funds are present to fill the trade.</td>
</tr>
<tr>
<td>order(address,uint256…)</td>
<td>0b927666</td>
<td>Store activate order inside of the contract.</td>
</tr>
<tr>
<td>cancelOrder(address,uint256…)</td>
<td>278b8c0e</td>
<td>This function cancels a given order by editing its fill data to the full amount. Requires that the transaction is signed properly.</td>
</tr>
</tbody>
</table><h3 id="command-detail-4">Command Detail</h3>
<ul>
<li>trade(address tokenGet, uint256 amountGet, address tokenGive, uint256 amountGive, uint256 expires, uint256 nonce, address user, uint8 v, bytes32 r, bytes32 s, uint256 amount):
<ul>
<li>tokenGet: Ethereum contract address of the token to receive</li>
<li>amountGet: uint256 amount of tokens being received</li>
<li>tokenGive: Ethereum contract address of the token to give</li>
<li>amountGive: uint256 amount of tokens being given</li>
<li>expires: uint256 of block number when this order should expire</li>
<li>nonce: arbitrary random number</li>
<li>user: Ethereum address of the user who placed the order</li>
<li>v: part of signature for the order hash as signed by user</li>
<li>r: part of signature for the order hash as signed by user</li>
<li>s: part of signature for the order hash as signed by user</li>
<li>amount: uint256 amount in terms of tokenGet that will be “buy” in the trade</li>
</ul>
</li>
<li>order(address tokenGet, uint256 amountGet, address tokenGive, uint256 amountGive, uint256 expires, uint256 nonce):
<ul>
<li>tokenGet: Ethereum contract address of the token to receive</li>
<li>amountGet: uint256 amount of tokens being received</li>
<li>tokenGive: Ethereum contract address of the token to give</li>
<li>amountGive: uint256 amount of tokens being given</li>
<li>expires: uint256 of block number when this order should expire</li>
<li>nonce: arbitrary random number</li>
</ul>
</li>
<li>cancelOrder(address tokenGet, uint256 amountGet, address tokenGive, uint256 amountGive, uint256 expires, uint256 nonce, uint8 v, bytes32 r, bytes32 s):
<ul>
<li>tokenGet: Ethereum contract address of the token to receive</li>
<li>amountGet: uint256 amount of tokens being received</li>
<li>tokenGive: Ethereum contract address of the token to give</li>
<li>amountGive: uint256 amount of tokens being given</li>
<li>expires: uint256 of block number when this order should expire</li>
<li>nonce: arbitrary random number</li>
<li>v: part of signature for the order hash as signed by user</li>
<li>r: part of signature for the order hash as signed by user</li>
<li>s: part of signature for the order hash as signed by user</li>
</ul>
</li>
</ul>
<h3 id="example-contract-abi-of-contract-trade-buy">Example contract abi of contract trade (Buy)</h3>
<ul>
<li>example signature :<pre><code>//eth.sign(account, msg)
0x9242685bf161793cc25603c231bc2f568eb630ea16aa137d2664ac80388256084f8ae3bd7535248d0bd448298cc2e2071e56992d0774dc340c368ae950852ada1c
</code></pre>
</li>
<li>trade(address,uint256,address,uint256,uint256,uint256,address,uint8,bytes32,bytes32,uint256):
<ul>
<li><code>0a19b14a</code> the Method ID.</li>
<li><code>0x000000000000000000000000692a70d2e424a56d2c6c27aa97d1a86395877b3a</code> (token contract address of expect to buy padding to 32 bytes)</li>
<li><code>0x0000000000000000000000000000000000000000000000000000000000100000</code> (buying amount padding to 32 bytes)</li>
<li><code>0x0000000000000000000000000000000000000000000000000000000000000000</code> (paying contract address of zero address is default to ether and padding to 32 bytes)</li>
<li><code>0x0000000000000000000000000000000000000000000000000000000000010000</code> (paying amount padding to 32 bytes)</li>
<li><code>0x0000000000000000000000000000000000000000000000000010000000000000</code> (expire block number padding to 32 bytes)</li>
<li><code>0x0000000000000000000000000000000000000000000000000000000000000001</code> (nonce padding to 32 bytes</li>
<li><code>0x00000000000000000000000014723a09acff6d2a60dcdf7aa4aff308fddc160c</code> (address of the user who placed the order padding to 32 bytes)</li>
<li><code>0x0000000000000000000000000000000000000000000000000000000000000028</code> (chain id)</li>
<li><code>0x9242685bf161793cc25603c231bc2f568eb630ea16aa137d2664ac8038825608</code> (part of signature)</li>
<li><code>0x4f8ae3bd7535248d0bd448298cc2e2071e56992d0774dc340c368ae950852ada</code> (part of signature)</li>
<li><code>0x0000000000000000000000000000000000000000000000000000000000100000</code> (will be buy)</li>
</ul>
</li>
<li>All together, the encoding is (new line after function selector and each 32-bytes of clarity):<pre><code>0a19b14a
0x000000000000000000000000692a70d2e424a56d2c6c27aa97d1a86395877b3a
0x0000000000000000000000000000000000000000000000000000000000100000
0x0000000000000000000000000000000000000000000000000000000000000000
0x0000000000000000000000000000000000000000000000000000000000010000
0x0000000000000000000000000000000000000000000000000010000000000000
0x0000000000000000000000000000000000000000000000000000000000000001
0x00000000000000000000000014723a09acff6d2a60dcdf7aa4aff308fddc160c
0x0000000000000000000000000000000000000000000000000000000000000028
0x9242685bf161793cc25603c231bc2f568eb630ea16aa137d2664ac8038825608
0x4f8ae3bd7535248d0bd448298cc2e2071e56992d0774dc340c368ae950852ada
0x0000000000000000000000000000000000000000000000000000000000100000
</code></pre>
</li>
<li>In Total:<pre><code>0x0a19b14a000000000000000000000000692a70d2e424a56d2c6c27aa97d1a86395877b3a0000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000100000000000000000000000014723a09acff6d2a60dcdf7aa4aff308fddc160c00000000000000000000000000000000000000000000000000000000000000289242685bf161793cc25603c231bc2f568eb630ea16aa137d2664ac80388256084f8ae3bd7535248d0bd448298cc2e2071e56992d0774dc340c368ae950852ada0000000000000000000000000000000000000000000000000000000000100000
</code></pre>
</li>
</ul>
<h1 id="contract-amount">Contract Amount</h1>

<table>
<thead>
<tr>
<th>Command</th>
<th>Abi</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>balanceOf(address,address)</td>
<td>f7888aec</td>
<td>Retrieves the balance of a token based on a user address and token address.</td>
</tr>
<tr>
<td>availableVolume(address,uint256…)</td>
<td>fb6e155f</td>
<td>This function checks the available volume for a given order.</td>
</tr>
<tr>
<td>amountFilled(address,uint256…)</td>
<td>2d804ca2</td>
<td>This function checks the amount of an order that has already been filled.</td>
</tr>
</tbody>
</table><h3 id="command-detail-5">Command Detail</h3>
<ul>
<li>balanceOf(address token, address user):
<ul>
<li>token: Ethereum contract address of the token or 0 for Ether</li>
<li>user: Ethereum address of the user</li>
</ul>
</li>
<li>availableVolume(address tokenGet, uint256 amountGet, address tokenGive, uint256 amountGive, uint256 expires, uint256 nonce, address user, uint8 v, bytes32 r, bytes32 s):
<ul>
<li>tokenGet: Ethereum contract address of the token to receive</li>
<li>amountGet: uint256 amount of tokens being received</li>
<li>tokenGive: Ethereum contract address of the token to give</li>
<li>amountGive: uint256 amount of tokens being given</li>
<li>expires: uint256 of block number when this order should expire</li>
<li>nonce: arbitrary random number</li>
<li>user: Ethereum address of the user who placed the order</li>
<li>v: part of signature for the order hash as signed by user</li>
<li>r: part of signature for the order hash as signed by user</li>
<li>s: part of signature for the order hash as signed by user</li>
</ul>
</li>
<li>amountFilled(address tokenGet, uint256 amountGet, address tokenGive, uint256 amountGive, uint256 expires, uint256 nonce, address user, uint8 v, bytes32 r, bytes32 s):
<ul>
<li>tokenGet: Ethereum contract address of the token to receive</li>
<li>amountGet: uint256 amount of tokens being received</li>
<li>tokenGive: Ethereum contract address of the token to give</li>
<li>amountGive: uint256 amount of tokens being given</li>
<li>expires: uint256 of block number when this order should expire</li>
<li>nonce: arbitrary random number</li>
<li>user: Ethereum address of the user who placed the order</li>
<li>v: part of signature for the order hash as signed by user</li>
<li>r: part of signature for the order hash as signed by user</li>
<li>s: part of signature for the order hash as signed by user</li>
</ul>
</li>
</ul>
<h3 id="example-contract-abi-of-contract-amount">Example contract abi of contract amount</h3>
<ul>
<li>balanceOf(address,address):
<ul>
<li><code>f7888aec</code> the Method ID.</li>
<li><code>0x000000000000000000000000692a70d2e424a56d2c6c27aa97d1a86395877b3a</code> (token contract address of expect to buy padding to 32 bytes)</li>
<li><code>0x000000000000000000000000ca35b7d915458ef540ade6068dfe2f44e8fa733c</code> (account address padded to 32 bytes)</li>
</ul>
</li>
<li>All together, the encoding is (new line after function selector and each 32-bytes of clarity):<pre><code>f7888aec
0x000000000000000000000000692a70d2e424a56d2c6c27aa97d1a86395877b3a
0x000000000000000000000000ca35b7d915458ef540ade6068dfe2f44e8fa733c
</code></pre>
</li>
<li>In Total:<pre><code>0xf7888aec000000000000000000000000692a70d2e424a56d2c6c27aa97d1a86395877b3a000000000000000000000000ca35b7d915458ef540ade6068dfe2f44e8fa733c
</code></pre>
</li>
</ul>
<h1 id="contract-fund-migration">Contract Fund Migration</h1>

<table>
<thead>
<tr>
<th>Command</th>
<th>Abi</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>migrateFunds(address,address[])</td>
<td>515fdde3</td>
<td>User triggered function to migrate funds into a new contract to ease updates.</td>
</tr>
</tbody>
</table><h3 id="command-detail-6">Command Detail</h3>
<ul>
<li>migrateFunds(address newContract, address[] tokens_):
<ul>
<li>newContract: Contract address of the new contract we are migrating funds to</li>
<li>tokens_: Array of token addresses that we will be migrating to the new contract</li>
</ul>
</li>
</ul>
<h3 id="example-contract-abi-of-contract-fund-migration">Example contract abi of contract fund migration</h3>
<ul>
<li>migrateFunds(address,address[]):
<ul>
<li><code>515fdde3</code> the Method ID.</li>
<li><code>0x0000000000000000000000000fdf4894a3b7c5a101686829063be52ad45bcfb7</code>  (new token contract address padding to 32 bytes)</li>
<li><code>0x0000000000000000000000000000000000000000000000000000000000000003</code> (this argument it’s starts with the length of the array in elements)</li>
<li><code>0x0000000000000000000000001439818dd11823c45fff01af0cd6c50934e27ac0</code> (the first entry of the array parameter)</li>
<li><code>0x0000000000000000000000006431fd0c29d024c5b04c7dab157fccd329e62e55</code> (the second entry of the array parameter)</li>
<li><code>0x0000000000000000000000001df11fca869524326dad2937ae8398e2296bda71</code> (the third entry of the array parameter)</li>
</ul>
</li>
<li>All together, the encoding is (new line after function selector and each 32-bytes of clarity):<pre><code>515fdde3
0x0000000000000000000000000fdf4894a3b7c5a101686829063be52ad45bcfb7
0x0000000000000000000000000000000000000000000000000000000000000003
0x0000000000000000000000001439818dd11823c45fff01af0cd6c50934e27ac0
0x0000000000000000000000006431fd0c29d024c5b04c7dab157fccd329e62e55
0x0000000000000000000000001df11fca869524326dad2937ae8398e2296bda71
</code></pre>
</li>
<li>In Total:<pre><code>0x515fdde30000000000000000000000000fdf4894a3b7c5a101686829063be52ad45bcfb700000000000000000000000000000000000000000000000000000000000000030000000000000000000000001439818dd11823c45fff01af0cd6c50934e27ac00000000000000000000000006431fd0c29d024c5b04c7dab157fccd329e62e550000000000000000000000001df11fca869524326dad2937ae8398e2296bda71
</code></pre>
</li>
</ul>
<h1 id="a-simple-interact-with-smart-contract-by-json-rpc">A Simple Interact With Smart Contract By JSON-RPC</h1>
<ul>
<li><a href="https://github.com/ethereum/wiki/wiki/JSON-RPC">More information</a></li>
<li>Use <code>curl</code> as following instruction to send a transaction
<ul>
<li><code>curl -X POST -d @filename.json 127.0.0.1:8545</code></li>
</ul>
</li>
<li>eth_sendTransaction - Parameter detaili
<ul>
<li><code>from</code>:  <code>DATA</code>, 20 Bytes - The address the transaction is send from.</li>
<li><code>to</code>:  <code>DATA</code>, 20 Bytes - (optional when creating new contract) The address the transaction is directed to.</li>
<li><code>gas</code>:  <code>QUANTITY</code>  - (optional, default: 90000) Integer of the gas provided for the transaction execution. It will return unused gas.</li>
<li><code>gasPrice</code>:  <code>QUANTITY</code>  - (optional, default: To-Be-Determined) Integer of the gasPrice used for each paid gas</li>
<li><code>value</code>:  <code>QUANTITY</code>  - (optional) Integer of the value sent with this transaction</li>
<li><code>data</code>:  <code>DATA</code>  - The compiled code of a contract OR the hash of the invoked method signature and encoded parameters.</li>
<li><code>nonce</code>:  <code>QUANTITY</code>  - (optional) Integer of a nonce. This allows to overwrite your own pending transactions that use the same nonce.</li>
</ul>
</li>
<li>eth_sendTransaction - Request<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
<span class="token string">"jsonrpc"</span><span class="token punctuation">:</span> <span class="token string">"2.0"</span><span class="token punctuation">,</span>
<span class="token string">"method"</span><span class="token punctuation">:</span> <span class="token string">"eth_sendTransaction"</span><span class="token punctuation">,</span>
<span class="token string">"params"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token punctuation">{</span>
    <span class="token string">"from"</span><span class="token punctuation">:</span><span class="token string">"0xa7058e40991e255b0af393fbed6476d66706af5a"</span><span class="token punctuation">,</span>
    <span class="token string">"to"</span><span class="token punctuation">:</span><span class="token string">"0x657e171821adee4d5ba4e401da24e0079c2f268d"</span><span class="token punctuation">,</span>
    <span class="token string">"gas"</span><span class="token punctuation">:</span><span class="token string">"0x76c0"</span><span class="token punctuation">,</span> <span class="token comment">// 30400,</span>
    <span class="token string">"gasPrice"</span><span class="token punctuation">:</span><span class="token string">"0x9184e72a000"</span><span class="token punctuation">,</span> <span class="token comment">// 10000000000000</span>
    <span class="token string">"data"</span><span class="token punctuation">:</span><span class="token string">"0x8f28397000000000000000000000000ca35b7d915458ef540ade6068dfe2f44e8fa733c"</span>
<span class="token punctuation">}</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
<span class="token string">"id"</span><span class="token punctuation">:</span> <span class="token number">1</span>
<span class="token punctuation">}</span>
</code></pre>
</li>
<li>eth_sendTransaction - Response
<ul>
<li><code>result</code> : <code>DATA</code>, 32 Bytes - the transaction hash, or the zero hash if the transaction is not yet available.</li>
<li>Use <a href="https://github.com/ethereum/wiki/wiki/JSON-RPC#eth_gettransactionreceipt">eth_getTransactionReceipt</a> to get the contract address or transaction detail, after the transaction was mined, when you created a contract.</li>
</ul>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
<span class="token string">"id"</span><span class="token punctuation">:</span><span class="token number">1</span><span class="token punctuation">,</span>
<span class="token string">"jsonrpc"</span><span class="token punctuation">:</span> <span class="token string">"2.0"</span><span class="token punctuation">,</span>
<span class="token string">"result"</span><span class="token punctuation">:</span> <span class="token string">"0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331"</span>
<span class="token punctuation">}</span>
</code></pre>
</li>
</ul>
<h1 id="additional">Additional</h1>
<ul>
<li><a href="https://emn178.github.io/online-tools/keccak_256.html">Online Hash Tool</a></li>
<li><a href="http://tomeko.net/online_tools/hex_to_file.php?lang=en">Online Hex To Binary</a></li>
</ul>

