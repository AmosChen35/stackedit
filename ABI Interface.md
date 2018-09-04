---


---

<h2 id="contract-management">Contract Management</h2>

<table>
<thead>
<tr>
<th>Command</th>
<th>Abi interface</th>
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
</table><h3 id="example-contract-abi-of--contract-management">Example contract abi of  contract management</h3>
<ul>
<li>changeAdmin(address):
<ul>
<li><code>0x8f28397</code> the Method ID. This is derived from the signature <code>changeAdmin(address)</code>.</li>
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
<h2 id="contract-deposit">Contract Deposit</h2>

<table>
<thead>
<tr>
<th>Command</th>
<th>Abi interface</th>
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
</table><h3 id="example-contract-abi-of-contract-deposit">Example contract abi of contract deposit</h3>
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
<h2 id="contract-withdraw">Contract Withdraw</h2>
<h2 id="contract-transfer">Contract Transfer</h2>

