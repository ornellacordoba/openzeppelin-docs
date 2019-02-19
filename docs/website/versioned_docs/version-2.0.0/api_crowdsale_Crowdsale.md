---
id: version-2.0.0-crowdsale_Crowdsale
title: Crowdsale
original_id: crowdsale_Crowdsale
---

<div class="contract-doc"><div class="contract"><h2 class="contract-header"><span class="contract-kind">contract</span> Crowdsale</h2><p class="base-contracts"><span>is</span> <a href="utils_ReentrancyGuard.html">ReentrancyGuard</a></p><p class="description">Crowdsale is a base contract for managing a token crowdsale, allowing investors to purchase tokens with ether. This contract implements such functionality in its most fundamental form and can be extended to provide additional functionality and/or custom behavior. The external interface represents the basic interface for purchasing tokens, and conform the base architecture for crowdsales. They are *not* intended to be modified / overridden. The internal interface conforms the extensible and modifiable surface of crowdsales. Override the methods to add functionality. Consider using &#x27;super&#x27; where appropriate to concatenate behavior.</p><div class="source">Source: <a href="https://github.com/OpenZeppelin/zeppelin-solidity/blob/v2.0.0/contracts/crowdsale/Crowdsale.sol" target="_blank">crowdsale/Crowdsale.sol</a></div></div><div class="index"><h2>Index</h2><ul><li><a href="crowdsale_Crowdsale.html#TokensPurchased">TokensPurchased</a></li><li><a href="crowdsale_Crowdsale.html#_deliverTokens">_deliverTokens</a></li><li><a href="crowdsale_Crowdsale.html#_forwardFunds">_forwardFunds</a></li><li><a href="crowdsale_Crowdsale.html#_getTokenAmount">_getTokenAmount</a></li><li><a href="crowdsale_Crowdsale.html#_postValidatePurchase">_postValidatePurchase</a></li><li><a href="crowdsale_Crowdsale.html#_preValidatePurchase">_preValidatePurchase</a></li><li><a href="crowdsale_Crowdsale.html#_processPurchase">_processPurchase</a></li><li><a href="crowdsale_Crowdsale.html#_updatePurchasingState">_updatePurchasingState</a></li><li><a href="crowdsale_Crowdsale.html#buyTokens">buyTokens</a></li><li><a href="crowdsale_Crowdsale.html#">fallback</a></li><li><a href="crowdsale_Crowdsale.html#">fallback</a></li><li><a href="crowdsale_Crowdsale.html#rate">rate</a></li><li><a href="crowdsale_Crowdsale.html#token">token</a></li><li><a href="crowdsale_Crowdsale.html#wallet">wallet</a></li><li><a href="crowdsale_Crowdsale.html#weiRaised">weiRaised</a></li></ul></div><div class="reference"><h2>Reference</h2><div class="events"><h3>Events</h3><ul><li><div class="item event"><span id="TokensPurchased" class="anchor-marker"></span><h4 class="name">TokensPurchased</h4><div class="body"><code class="signature">event <strong>TokensPurchased</strong><span>(address purchaser, address beneficiary, uint256 value, uint256 amount) </span></code><hr/><div class="description"><p>Event for token purchase logging.</p></div><dl><dt><span class="label-parameters">Parameters:</span></dt><dd><div><code>purchaser</code> - who paid for the tokens</div><div><code>beneficiary</code> - who got the tokens</div><div><code>value</code> - weis paid for purchase</div><div><code>amount</code> - amount of tokens purchased</div></dd></dl></div></div></li></ul></div><div class="functions"><h3>Functions</h3><ul><li><div class="item function"><span id="_deliverTokens" class="anchor-marker"></span><h4 class="name">_deliverTokens</h4><div class="body"><code class="signature">function <strong>_deliverTokens</strong><span>(address beneficiary, uint256 tokenAmount) </span><span>internal </span></code><hr/><div class="description"><p>Source of tokens. Override this method to modify the way in which the crowdsale ultimately gets and sends its tokens.</p></div><dl><dt><span class="label-parameters">Parameters:</span></dt><dd><div><code>beneficiary</code> - Address performing the token purchase</div><div><code>tokenAmount</code> - Number of tokens to be emitted</div></dd></dl></div></div></li><li><div class="item function"><span id="_forwardFunds" class="anchor-marker"></span><h4 class="name">_forwardFunds</h4><div class="body"><code class="signature">function <strong>_forwardFunds</strong><span>() </span><span>internal </span></code><hr/><div class="description"><p>Determines how ETH is stored/forwarded on purchases.</p></div></div></div></li><li><div class="item function"><span id="_getTokenAmount" class="anchor-marker"></span><h4 class="name">_getTokenAmount</h4><div class="body"><code class="signature">function <strong>_getTokenAmount</strong><span>(uint256 weiAmount) </span><span>internal </span><span>view </span><span>returns  (uint256) </span></code><hr/><div class="description"><p>Override to extend the way in which ether is converted to tokens.</p></div><dl><dt><span class="label-parameters">Parameters:</span></dt><dd><div><code>weiAmount</code> - Value in wei to be converted into tokens</div></dd><dt><span class="label-return">Returns:</span></dt><dd>Number of tokens that can be purchased with the specified _weiAmount</dd></dl></div></div></li><li><div class="item function"><span id="_postValidatePurchase" class="anchor-marker"></span><h4 class="name">_postValidatePurchase</h4><div class="body"><code class="signature">function <strong>_postValidatePurchase</strong><span>(address beneficiary, uint256 weiAmount) </span><span>internal </span><span>view </span></code><hr/><div class="description"><p>Validation of an executed purchase. Observe state and use revert statements to undo rollback when valid conditions are not met.</p></div><dl><dt><span class="label-parameters">Parameters:</span></dt><dd><div><code>beneficiary</code> - Address performing the token purchase</div><div><code>weiAmount</code> - Value in wei involved in the purchase</div></dd></dl></div></div></li><li><div class="item function"><span id="_preValidatePurchase" class="anchor-marker"></span><h4 class="name">_preValidatePurchase</h4><div class="body"><code class="signature">function <strong>_preValidatePurchase</strong><span>(address beneficiary, uint256 weiAmount) </span><span>internal </span><span>view </span></code><hr/><div class="description"><p>Validation of an incoming purchase. Use require statements to revert state when conditions are not met. Use `super` in contracts that inherit from Crowdsale to extend their validations. Example from CappedCrowdsale.sol&#x27;s _preValidatePurchase method: super._preValidatePurchase(beneficiary, weiAmount); require(weiRaised().add(weiAmount) &lt;= cap);.</p></div><dl><dt><span class="label-parameters">Parameters:</span></dt><dd><div><code>beneficiary</code> - Address performing the token purchase</div><div><code>weiAmount</code> - Value in wei involved in the purchase</div></dd></dl></div></div></li><li><div class="item function"><span id="_processPurchase" class="anchor-marker"></span><h4 class="name">_processPurchase</h4><div class="body"><code class="signature">function <strong>_processPurchase</strong><span>(address beneficiary, uint256 tokenAmount) </span><span>internal </span></code><hr/><div class="description"><p>Executed when a purchase has been validated and is ready to be executed. Doesn&#x27;t necessarily emit/send tokens.</p></div><dl><dt><span class="label-parameters">Parameters:</span></dt><dd><div><code>beneficiary</code> - Address receiving the tokens</div><div><code>tokenAmount</code> - Number of tokens to be purchased</div></dd></dl></div></div></li><li><div class="item function"><span id="_updatePurchasingState" class="anchor-marker"></span><h4 class="name">_updatePurchasingState</h4><div class="body"><code class="signature">function <strong>_updatePurchasingState</strong><span>(address beneficiary, uint256 weiAmount) </span><span>internal </span></code><hr/><div class="description"><p>Override for extensions that require an internal state to check for validity (current user contributions, etc.).</p></div><dl><dt><span class="label-parameters">Parameters:</span></dt><dd><div><code>beneficiary</code> - Address receiving the tokens</div><div><code>weiAmount</code> - Value in wei involved in the purchase</div></dd></dl></div></div></li><li><div class="item function"><span id="buyTokens" class="anchor-marker"></span><h4 class="name">buyTokens</h4><div class="body"><code class="signature">function <strong>buyTokens</strong><span>(address beneficiary) </span><span>public </span><span>payable </span></code><hr/><div class="description"><p>Low level token purchase ***DO NOT OVERRIDE*** This function has a non-reentrancy guard, so it shouldn&#x27;t be called by another `nonReentrant` function.</p></div><dl><dt><span class="label-modifiers">Modifiers:</span></dt><dd><a href="utils_ReentrancyGuard.html#nonReentrant">nonReentrant </a></dd><dt><span class="label-parameters">Parameters:</span></dt><dd><div><code>beneficiary</code> - Recipient of the token purchase</div></dd></dl></div></div></li><li><div class="item function"><span id="fallback" class="anchor-marker"></span><h4 class="name">fallback</h4><div class="body"><code class="signature">function <strong></strong><span>() </span><span>external </span><span>payable </span></code><hr/><div class="description"><p>Fallback function ***DO NOT OVERRIDE*** Note that other contracts will transfer fund with a base gas stipend of 2300, which is not enough to call buyTokens. Consider calling buyTokens directly when purchasing tokens from a contract.</p></div></div></div></li><li><div class="item function"><span id="fallback" class="anchor-marker"></span><h4 class="name">fallback</h4><div class="body"><code class="signature">function <strong></strong><span>(uint256 rate, address wallet, IERC20 token) </span><span>internal </span></code><hr/><div class="description"><p>The rate is the conversion between wei and the smallest and indivisible token unit. So, if you are using a rate of 1 with a ERC20Detailed token with 3 decimals called TOK, 1 wei will give you 1 unit, or 0.001 TOK.</p></div><dl><dt><span class="label-parameters">Parameters:</span></dt><dd><div><code>rate</code> - Number of token units a buyer gets per wei</div><div><code>wallet</code> - Address where collected funds will be forwarded to</div><div><code>token</code> - Address of the token being sold</div></dd></dl></div></div></li><li><div class="item function"><span id="rate" class="anchor-marker"></span><h4 class="name">rate</h4><div class="body"><code class="signature">function <strong>rate</strong><span>() </span><span>public </span><span>view </span><span>returns  (uint256) </span></code><hr/><dl><dt><span class="label-return">Returns:</span></dt><dd>the number of token units a buyer gets per wei.</dd></dl></div></div></li><li><div class="item function"><span id="token" class="anchor-marker"></span><h4 class="name">token</h4><div class="body"><code class="signature">function <strong>token</strong><span>() </span><span>public </span><span>view </span><span>returns  (IERC20) </span></code><hr/><dl><dt><span class="label-return">Returns:</span></dt><dd>the token being sold.</dd></dl></div></div></li><li><div class="item function"><span id="wallet" class="anchor-marker"></span><h4 class="name">wallet</h4><div class="body"><code class="signature">function <strong>wallet</strong><span>() </span><span>public </span><span>view </span><span>returns  (address) </span></code><hr/><dl><dt><span class="label-return">Returns:</span></dt><dd>the address where funds are collected.</dd></dl></div></div></li><li><div class="item function"><span id="weiRaised" class="anchor-marker"></span><h4 class="name">weiRaised</h4><div class="body"><code class="signature">function <strong>weiRaised</strong><span>() </span><span>public </span><span>view </span><span>returns  (uint256) </span></code><hr/><dl><dt><span class="label-return">Returns:</span></dt><dd>the amount of wei raised.</dd></dl></div></div></li></ul></div></div></div>